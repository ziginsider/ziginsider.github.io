---
layout: post
title: Большие запросы к базе данных на Android
date: 2017-12-11 16:28
tags:
- Java
- Android
- Architecture Components
- Translate
- SQLite
- Pagging Library
- CursorAdapter
---
<a href="https://ziginsider.github.io/large-database-queries-on-android/"><img src="{{ site.baseurl }}/images/largedatabase/intro_39.jpg"></a>

:books: *Перевод статьи Chris Craik <a href="https://medium.com/google-developers/large-database-queries-on-android-cb043ae626e8">"Large Database Queries on Android"</a>.*

*Статья упомянута в офф. документации Google в разделе <a href="">Pagging Library</a>. И является вполне программной в смысле видения Google дальнейшего развития работы с SQLite в Android. Это новое видение, вполне не ново, т.к. вопрос (скорость и удобство работы с SQLite, загрузка больших порций данных) стоял давно и те или иные сторонние библиотеки решали этот вопрос. Но представив свою концепцию архитектуры приложений <a href="https://developer.android.com/topic/libraries/architecture/index.html">Android Architecture Components</a> разработчики Android Team не обошли внимание проблемы SQLite. Данная статья обзорная, она говорит о проблемах работы с данными, при использовании SQLite, и описывает пути решения данных проблем.*

<br>
### Возможности
SQLite - отличный способ хранить множество данных на Android, но так сложилось, что загрузка этих наборов данных в UI довольно нетривиальна, и может привести к проблемам производительности. Перед запуском новой библиотеки Paging Library, мы исследовали существующие подходы к подгрузке данных, и особенно потенциальные ловушки, при использовании SQLiteCursor.

В этой статье мы рассмотрим его проблемы, и поймем почему мы заинтересованы в использование небольших запросов с помощью <a href="https://developer.android.com/topic/libraries/architecture/room.html">Room</a> и <a href="https://developer.android.com/topic/libraries/architecture/paging.html">Pagging Library</a> в <a href="https://developer.android.com/topic/libraries/architecture/index.html">Architecture Android Components</a>.

<br>
### SQLiteCursor и CursorAdapter
<a href="https://developer.android.com/reference/android/database/sqlite/SQLiteCursor.html">SQLiteCursor</a> это возвращаемый тип при запросе к базе данных SQLite в Android. Он позволяет получить большой объем данных за фиксированную "стоимость". Первое чтение данных инициализирует <a href="https://developer.android.com/reference/android/database/CursorWindow.html">CursorWindow</a>, буфер строк с дефолтным размером 2MB, который содержит контент из базы данных. SQLiteCursor обновляет этот буфер полностью каждый раз, когда вы делаете запрос на строку, которая еще не представлена в выборке. Таким образом SQLiteCursor реализует подкачку данных с фиксированным размером выборки.   

<a href="https://developer.android.com/reference/android/database/CursorWindow.html">CursorAdapter</a> был доступен начиная с API 1, и предоставил простой способ получения данных из курсора (обычно SQLiteCursor) для элементов ListView. Хотя он отлично справляется с этой функцией, он обращается к базе данных в пользовательском потоке всякий раз, когда требуется загрузка новых данных. Это само по себе не приемлемо для современных и отзывчивых приложений. Тогда мы можем спросить, не может ли у нас быть адаптера, основанного на курсоре, но который бы загружал данные в фоновом потоке? В конце концов у SQLiteCursor есть подкачка данных.

<br>
### Проблемы с подкачкой данных с ипользованием SQLiteCursor

Большинство проблем с подкачкой с использованием SQLiteCursor происходит из-за неожиданного поведения, поскольку он использует свое окно (CursorWindow) для загрузки выборки с данными. Ниже приведен список проблем, с которыми мы столкнулись, когда эксперементировали с (??внутренней??) выборкой SQLiteCursor для <a href="">Paging Library</a>:

- **SQLiteCursor не поддерживает транзакции базы данных**

Когда я начал исследовать подкачку данных, я был не опытен в SQLite и особенно в Cursor в Android. Я просто предположил, что SQLiteCursor, после загрузки окна данных, мог бы приостановить запрос, до того момента, когда ему понадобится следующее окно. Таким образом, доступ к десятому окну будет таким же эффективным, как и к первому. *Но это не так*. Каждый раз, когда читается новое окно, запрос перезапускается с начала и пропускает строки которые не запрашиваются для этого окна. Каждый раз полный проход по данным. Это от того, что *SQLiteCursor не может останавливать и возобновлять запросы*.
 
Это похоже на доступ к элементам с 1000-го по 1500-й в связном списке (LinkedList) - вам нужно проходить большое количество элементов, чтобы загрузить следующую порцию выборки. Когда вы загружаете, каждое последующее окно должно пропускать все больше и больше данных, прежде чем начнет загружать необходимые для него. Это замедляет загрузку. Это эквивалентно использованию ключевого слова SQL `OFFSET` для пропуска данных, которое <a href="http://www.sqlite.org/cvstrac/wiki?p=ScrollingCursor">не является самым эффективным способом заполнения выборки данными</a>, и этого нельзя  избежать, опираясь на подгрузку данных с помощью SQLiteCursor. Вы можете посмотреть как SQLiteCursor подгружает данные в новое окно <a href="https://android.googlesource.com/platform/frameworks/base/+/fee4546fd648b519ad828ea1f950554c1054699d/core/jni/android_database_SQLiteConnection.cpp#695">здесь</a>.

- **SQLiteCursor.getCount() обязателен, и проходит по всему запросу**

Перед чтением самой первой строки, SQLiteCursor вызыввает `getCount()` для проверки границ. Поскольку *SQLite вынужден сканировать весь результат запроса* для его подсчета (опять же, как в связном списке), это может привести к значительным накладным расходам. Если вы постепенно подгружаете большой запрос в UI, в ответ на прокрутку пользователя, вам может не понадобится знать весь его (запроса) размер, поэтому подсчет добавляет ненужную начальную работу. 

- **SQLiteCursor.getCount() всегда загружает первое окно данных**

Как часть подсчета количества, при сканировании полученной выборки, SQLiteCursor заранее заполняет свое окно с позиции 0, в предположении, что первые элементы в запросе будут нужны.

Он предварительно загружает эти элементы, чтобы он мог знать заранее сколько приблизительно строк попадает в окно (подробнее об этом ниже). Эта рискованная загрузка имеет смысл, если данные представляются с начала запроса, но позиция, восстанавливаемая из сохраненного состояния, может быть намного дальше по списку, где начальное окно не релевантно. Если вы хотите представить данные из третьего окна, вы вынуждены сначала загрузить и выбросить 2 MB данных первого окна. Код такого поведения смотрите <a href="https://android.googlesource.com/platform/frameworks/base/+/fee4546fd648b519ad828ea1f950554c1054699d/core/java/android/database/sqlite/SQLiteCursor.java#130">здесь</a>



It preloads these items so that it can know roughly how many rows fit into a window ahead of time (more on this below). This opportunistic loading is reasonable if you’re presenting data from the start of the query, but a position being restored from saved instance state may start the index much further down the list, where the initial window isn’t relevant. If you’d like to present data from the third window of content, you’re forced to load and throw away 2MB of data first. The code for this counting behavior is here.





[в процессе]

