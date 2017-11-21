---
layout: post
title: Android Tutorial - Facebook SDK Login. Part II. Share content.
date: 2017-11-21 18:17
tags:
- Android
- Java
- Facebook SDK
---
<img src="{{ site.baseurl }}/images/facebook-login_small.png">
<br>

*Как запостить контент на Facebook из Android-приложения?*

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo/tree/share_post">https://github.com/ziginsider/FacebookSDKDemo</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login/">Часть I. Android. Facebook-SDK. Как залогиниться на Facebook?</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login_3/">Часть III. Android. Facebook-SDK. Как вытащить посты из Facebook?</a>

<br>
### Введение
Постановка задачи: Познакомиться с Facebook SDK. Запостить контент.

### Начало и сразу рабочий код

Порой необходимо дать возможность пользователю поделиться каким-либо контентом на Facebook из вашего Android приложения. Покажем как это сделать.

Итак, создаем кнопку, которая будет постить контент. В рабочий проект из <a href="https://ziginsider.github.io/Facebook_SDK_Login/">Части I</a> добавляем макет кнопки:

{% gist a413b240ff7af7dc6ba9ab4b4811d507 %}

В Activity добавляем константы и инициализируем кнопку:

{% gist 1b250f6d8a5ba85869b7ca8acc5abf5b %}

И сразу делаем ее невидимой, чтобы до входа на Facebook она была не видна.

Теперь, в случае успешного входа делаем кнопку видимой. Добавляем View.VISIBLE в:

{% gist 41a3fac23be4159d579ce43388971214 %}

и в:

{% gist b7c3cfe2cbddf5335923d4a865a06662%}

Наконец, добавляем обработчик нажатия на кнопку:

{% gist b908b156b28eedf09577b0b928d00851 %}

Класс ShareLinkContent публикует контент по ссылке. Но мы можем использовать другие классы, например, SharePhotoContent, ShareVideoContent, ShareFeedContent, ShareMediaContent <a href="https://developers.facebook.com/docs/sharing/android">etc</a>. Контент, для публикации, всегда должен передаваться в ShareDialog.

На экране смартфона получаем такое окошко, публикуем...

<img src="{{ site.baseurl }}/images/share_content_facebook.png">

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo/tree/share_post">https://github.com/ziginsider/FacebookSDKDemo</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login/">Часть I. Android. Facebook-SDK. Как залогиниться на Facebook?</a>

<a href="https://ziginsider.github.io/Facebook_SDK_Login_3/">Часть III. Android. Facebook-SDK. Как вытащить посты из Facebook?</a>

to be continued...

