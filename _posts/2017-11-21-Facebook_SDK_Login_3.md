---
layout: post
title: Android Tutorial - Facebook SDK Login. Part III. Get Posts.
date: 2017-11-21 22:39
tags:
- Android
- Java
- Facebook SDK
---
<img src="{{ site.baseurl }}/images/facebook-login_small.png">
<br>

*Как вытащить посты из Facebook на Android приложение?*

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo/tree/get_post">https://github.com/ziginsider/FacebookSDKDemo</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login/">Часть I. Android. Facebook-SDK. Как залогиниться на Facebook?</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login_2/">Часть II. Android. Facebook-SDK. Как запостить контент на Facebook?</a>

<br>
### Введение
Постановка задачи: Познакомиться с Facebook SDK. Вытащить посты в формате JSON.

<br>
### Начало и сразу рабочий код
Аналогично Части II, добавим кнопку. Создаем макет кнопки:

{% gist a56a036017fd41b919f839a9f3bdacf4 %}

В Activity добавляем константы и инициализируем кнопку, а также к списку разрешений добавляем "user_posts":

{% gist 466ac71ecb1eeec6f218fa3054089f71 %}

И не забываем сделать кнопку видимой, когда это необходимо. Тут аналогично <a href="https://ziginsider.github.io/Facebook_SDK_Login_2/">Части II</a>.

Добавляем обработчик нажатия на кнопку:

{% gist 1805076aa1b0dae622cb1a790c426ec9%}

Вообще, это пример запроса GraphReques, который запускается асинхронно. В запросе мы указываем токен доступа, путь Graph API, HTTP метод запроса, и сallback c получением ответа. Ответ получаем как JSON-объект и сохраняем его в логах. Должны получить что-то такое:

<img src="{{ site.baseurl }}/images/json_posts.jpg">

NB: для разбора JSON есть неплохой сайт http://www.jsoneditoronline.org/

<img src="{{ site.baseurl }}/images/jsoneditor.jpg">

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo/tree/get_post">https://github.com/ziginsider/FacebookSDKDemo</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login/">Часть I. Android. Facebook-SDK. Как залогиниться на Facebook?</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login_2/">Часть II. Android. Facebook-SDK. Как запостить контент на Facebook?</a>

end.

