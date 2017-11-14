---
layout: post
title: Volley vs Retrofit. Описание библиотек REST API.
date: 2017-07-01 12:40
tags:
- Java
- REST API
- JSON
- Android
- Lib
- Volley
- Retrofit
---
## Краткое сравнение. Для чего использовать.
Использовать <a href="http://square.github.io/retrofit/">Retrofit</a>:
- когда нужно стандартная реализаци REST API для парсинга JSON
- реализация без кастомным запросов, запросов с приоритетом, кэширования, повторов etc.

Использовать <a href="https://developer.android.com/training/volley/index.html">Volley</a>:
- необычные требования к запросам
- возможно, будет необходимость расширения функциональности вашего REST API в дальнейшем

NB: Если необходимо загружать большие файлы или потоки, то не следует использовать ни то ни другое. Используйте <a href="https://developer.android.com/reference/android/app/DownloadManager.html">Download Manager</a>

## Retrofit
Свойства:
- made in Square
- не поддерживает обработку изображений (хорошо использовать для этого Picasso (см. ссылки о Picasso vs Glide ниже))
- использует пул потоков, параллельные запросы и библиотеку OkHttp
- приоритезация, отмена, повторные запросы - вручную (в Retrofit 2 немного удобнее)
- полная поддержка POST-запросов и multipart загрузок файлов
- Retofit 2 работает с RxJava проще (with Observable types)
- HTTP-запросы описываются через аннотации, синхронные и асинхронные вызовы REST-методов, данные могут передаваться в виде JSON, XML, Protobuf. С этой библиотекой на пару умеет работать <a href="https://github.com/stephanenicolas/robospice">RoboSpice</a>. 

Итак, Retrofit - библиотека REST-клиент для работы в Android.

Подключение: 
{% highlight gridle %}
compile 'com.squareup.retrofit2:retrofit:2.3.0'
{% endhighlight %}



## Volley
Свойства:
- made in Google
- поддерживает минимальный функционал обработки изображений (для более полного функционала, можно использовать <a href="https://github.com/bumptech/glide">Glide</a>, + о Glide см. <a href="https://blog.mindorks.com/how-the-android-image-loading-library-glide-and-fresco-works-962bc9d1cc40">тут</a>, + отличия Glide от Picasso <a href="https://medium.com/@multidots/glide-vs-picasso-930eed42b81d">тут</a> или <a href="https://inthecheesefactory.com/blog/get-to-know-glide-recommended-by-google/en">тут</a> или  <a href="https://appdictive.dk/blog/2015/06/25/Picasso-vs-glide/">наглядно тут</a>)
- использует пул потоков, параллельные запросы и библиотеку OkHttp
- гибкий механизм кеширования (который хорошо подходит для Glide)
- поддерживает выставление приоритетов, отмену запросов, повторные запросы - используя для этого немного кода
- поддерживает POST-запросы (но необходимо конвертировать Java-объекты в JSON-объкты используя, например, библиотеку Gson), также поддерживает multipart загрузки, но, предоставляя большую гибкость, api не такой отполированный, как у Retrofit'а

### Слухи
- (UPD: 26.08.2017) Google как-то склоняется к Retrofit (вывод по примерам, которые они показывают в своих же лекциях), что делает им честь, конечно. Но всегда нужно помнить о разных условиях, в которых лучше применять одну или вторую библиотеки.
