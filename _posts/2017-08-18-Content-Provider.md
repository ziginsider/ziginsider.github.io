---
layout: post
title: Препарирование ContentProvider.
date: 2017-08-18 12:55
tags:
- Java
- Android
- ContentProvider
---
<img src="{{ site.baseurl }}/images/content.jpg">

## What?

<a href="https://developer.android.com/guide/topics/providers/content-providers.html?hl=ru">ContentProvider</a> – это класс, предоставляющий унифицированный интерфейс для доступа к данным приложения. Этот класс позволяет вам использовать единый источник данных в вашем приложении.

*Sources:*
- <a href="https://www.youtube.com/watch?v=3HhBKfjuvf4">https://www.youtube.com/watch?v=3HhBKfjuvf4</a> - ContentProvider & Loader (обзор)
- <a href="https://www.youtube.com/watch?v=QEqGgmMkRDk">https://www.youtube.com/watch?v=QEqGgmMkRDk</a> - ContentProvider & SQLite (опыт использования)
- <a href="https://www.youtube.com/watch?v=zeDzbzLmpLs">https://www.youtube.com/watch?v=zeDzbzLmpLs</a> - ContentProvider (опыт использования)
- <a href="http://www.nerdgrl.org/ru/programming/sqlite-contentprovider-1/">http://www.nerdgrl.org/ru/programming/sqlite-contentprovider-1/</a> - цикл статей ContentProvider & SQLite
- <a href="https://ru.stackoverflow.com/questions/653346/%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-contentprovider">https://ru.stackoverflow.com/questions/653346/%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-contentprovider</a> - Ответ на русском StackOverflow "Что такое ContentProvider?"
- <a href="https://www.tutorialspoint.com/android/android_content_providers.htm">https://www.tutorialspoint.com/android/android_content_providers.htm</a> - Tutorial ContentProvider
- <a href="https://www.youtube.com/watch?v=xHXn3Kg2IQE">https://www.youtube.com/watch?v=xHXn3Kg2IQE</a> - классика (паттерны A/B/C)

Задуман, как способ предоставлять данные вашего приложения для сторонних приложений, + для реализации поиска среди данных вашего приложения с использованием search suggestions (подсказки при вводе слов для поиска).

На практике часто используется для создания единого источника данных внутри приложения (В противовес заявлению в оф.докумментации: "You don't need to develop your own provider if you don't intend to share your data with other applications."). При этом получаем связки: ContentProvider & SQLite, ContentProvider & CursorLoader, ContentProvider & Loader...

В пользу только лишь внутреннего использования (польза для внешнего очевидна) ContentProvider'a говорит следующее:

1) Как уже было сказано, ContentProvider предоставляет унифицированный интерфейс для доступа к данным. Это говорит о том, что не нужно беспокоится о реализации хранения данных. Она может меняться, но данные остаются доступны.

2) Не нужно управлять жизненным циклом объекта для доступа к данным (к примеру, экземпляра SQLiteDatabase). Ведь в случае прямого использования таких объектов возникает немало вопросов: где хранить этот объект? Когда закрывать базу данных? Когда уничтожать этот объект? ContentProvider позволяет получать доступ к данным из любого места, где доступен контекст приложения (экземпляр Context).

3) ContentProvider полностью соответствует концепциям REST (о которых мы говорили <a href="https://ziginsider.github.io/rest-api/">в этих заметках</a>)

Немного о последнем пункте. Итак, соответствие REST:

- Для каждой сущности ContentProvider'a есть свой URI. 
- Регистрация в манифесте ContentProvider'a выглядит следующим образом:
{% highlight xml %}
<provider
   android:name=".data.sqlite.WeatherContentProvider"
   android:authorities="io.github.ziginsider"
   android:exported="false"/>
{% endhighlight %}
- У ContentProvider'a приложения всегда определен базовый URI. Он складывается из префикса "content://" и authorities. Таким образом, для нашего примера базовый URI = "content://io.github.ziginsider"
- Далее, допустим мы хотим создать группу, в которой будет храниться информация о погоде (в рамках базы данных это будет таблица). Тогда URI для этой группы должно выглядеть следующим образом: "content://ru.gdgkazan.simpleweather/weather". Если мы обратимся к данным в ContentProvider по этому URI, то получим все экземпляры, сохраненные в этой группе.  
- И наконец, если нам нужно URI для отдельного объекта, то оно будет выглядеть следующим образом: "content://ru.gdgkazan.simpleweather/weather/4". Где 4 – это номер добавленного экземпляра. 

## Создание своего СontentProvider'a

На практике нам необходимо наследоваться от класса ContentProvider и реализовать следующие методы:
- onCreate() - инициализирует ContentProvider. Провайдер будет создан как только вы обратитесь к нему с помощью ContentResolver'a 
- query() - извлекает данные из БД, и возвращает их в виде Cursor 
- insert() - добавляет новые данные в БД, возвращает uri новой записи
- bulkInsert() - добавляет массив элементов 
- update() - обновляет строки в БД согласно заданным условиям 
- delete() - удаляет данные 
- getType() - возвращает MIME-тип для заданной content URI









{% highlight xml %}


{% endhighlight %}
## Где используют?

## Практика использования Content Provider'a
