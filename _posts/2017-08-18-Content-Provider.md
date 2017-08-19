---
layout: post
title: Препарирование ContentProvider
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

1. Как уже было сказано, ContentProvider предоставляет унифицированный интерфейс для доступа к данным. Это говорит о том, что не нужно беспокоится о реализации хранения данных. Она может меняться, но данные остаются доступны.

2. Не нужно управлять жизненным циклом объекта для доступа к данным (к примеру, экземпляра SQLiteDatabase). Ведь в случае прямого использования таких объектов возникает немало вопросов: где хранить этот объект? Когда закрывать базу данных? Когда уничтожать этот объект? ContentProvider позволяет получать доступ к данным из любого места, где доступен контекст приложения (экземпляр Context).

3. ContentProvider полностью соответствует концепциям REST (о которых мы говорили <a href="https://ziginsider.github.io/rest-api/">в этих заметках</a>)

Немного о последнем пункте. Итак, соответствие REST:

- Для каждой сущности ContentProvider'a есть свой URI. 
- Регистрация в манифесте ContentProvider'a выглядит следующим образом (пока без пояснения и др. возможных атрибутов):
{% highlight xml %}
<provider
   android:name=".peopleprovider"
   android:authorities="io.github.ziginsider.peopleprovider"
   android:exported="false"/>
{% endhighlight %}
- рекомендуется использовать в качестве authority имя пакета с префиксом поясняющим суть провайдера, например для нашего списка контактов можно было бы применить: io.github.ziginsider.peopleprovider
- URI образуется по схеме:
{% highlight xml %}
<prefix>://<authority>/<data_type>/<id>
{% endhighlight %}
- У ContentProvider'a приложения всегда определен базовый URI. Он складывается из префикса "content://" и authorities. Таким образом, для нашего примера базовый URI = "content://io.github.ziginsider.peopleprovider"
- Далее, допустим мы хотим создать группу, в которой будет храниться информация о писателях (в рамках базы данных это будет таблица). Тогда URI для этой группы должно выглядеть следующим образом: "content://io.github.ziginsider.peopleprovider/writers". Если мы обратимся к данным в ContentProvider по этому URI, то получим все экземпляры, сохраненные в этой группе.  
- И наконец, если нам нужно URI для отдельного объекта, то оно будет выглядеть следующим образом: "content://io.github.ziginsider.peopleprovider/writers/4". Где 4 – это номер добавленного экземпляра. 

## Создание своего СontentProvider'a

На практике нам необходимо наследоваться от класса ContentProvider и реализовать следующие методы:
{% highlight java %}
public boolean onCreate()
{% endhighlight %} - инициализирует ContentProvider. Провайдер будет создан как только вы обратитесь к нему с помощью ContentResolver'a. Возвращает true, если ContentProvider создан успешно. В общем случае, не рекомендуется делать в onCreate() ContentProvider'a длительных операций т.к. это может повесить onCreate() Application (??)
{% highlight java %}
public Cursor query(@NonNull Uri uri,
            String[] projection, 
            String selection, 
            String[] selectionArgs, 
            String sortOrder)
{% endhighlight %} -  Возвращает объект Cursor по полученному URI. URI парсится, согласно заданным нами правилам. В случае использования в качестве источника данных БД SQLite извлекает данные из БД, и возвращает их в виде Cursor. (соответствует HTTP методу GET). 
{% highlight java %}
public Uri insert(@NonNull Uri uri, 
            ContentValues values)
{% endhighlight %} - добавляет новые данные, возвращает URI новой записи. (соответствует HTTP методу POST)
{% highlight java %}
public final int bulkInsert(@NonNull Uri uri, 
            @NonNull ContentValues[] values)
{% endhighlight %} - добавляет массив элементов (не является обязательным для реализации в отличии от всех остальных методов)
{% highlight java %}
public final int update(@NonNull Uri uri, 
            ContentValues values, 
            String selection, 
            String[] selectionArgs)
{% endhighlight %} - обновляет строки в хранилище данных согласно заданным условиям. (в терминологии HTTP методов – PUT или PATCH)
{% highlight java %}
public final int delete(@NonNull Uri uri, 
            String selection, 
            String[] selectionArgs)
{% endhighlight %} - удаляет данные. ( единственный метод ContentProvider, HTTP аналог которого имеет такое же название)
{% highlight java %}
public final String getType(@NonNull Uri uri)
{% endhighlight %} - возвращает MIME-тип для заданной content URI. Обычно этот метод используют для сопоставления имени таблицы и URI, чтобы потом выполнить запрос к базе данных.

Следует помнить, что все перечисленные методы кроме onCreate() могут выполняться одновременно в нескольких потоках, и поэтому должны быть потоко-безопасными (thread-safe).

Допустим, мы создали свой ContentProvider, добавили его в манифесте и теперь можем обращаться к нему в качестве интерфейса для работы с данными. Но здесь есть небольшая тонкость – мы создавали объект ContentProvider, но обращаться к данным нужно через объект ContentResolver, который можно получить через метод getContentResolver в классе Context:
{% highlight java %}
Cursor cursor = mContext.getContentResolver().query(table.getUri(), 
            null, 
            where.where(), 
            where.whereArgs(), 
            where.limit());
{% endhighlight %}


> проверка микрофона



### Где используют?

## Практика использования Content Provider'a
