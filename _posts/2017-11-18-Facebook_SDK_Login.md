---
layout: post
title: Android Tutorial - Facebook SDK Login
date: 2017-11-18 19:52
tags:
- Android
- Java
- Facebook SDK
---
<img src="{{ site.baseurl }}/images/facebook-login_small.png">
<br>

*По мотивам: <a href="https://www.youtube.com/watch?v=KjBNFWKNMOY">Android Studio Tutorial - Facebook SDK Login</a>*

<br>
### Введение
Постановка задачи: Познакомиться с Facebook SDK. Залогиниться. Получить некоторые данные, как то картинка профиля, дата рождения, email, число френдов, etc.

### Начало
Создаем новый проект, выбираем Empty Activity. Затем подключаем библиотеки: 
- Facebook SDK
- Picaso

{% gist f2ad9ffeeccfeac3228a4a500d7268d6 %}

Подготавливаем макет Activity:

{% gist 25b7947b45be90c506572acec2a153bb%}

Прописываем разрешения мета-данные в манифесте. Перед тегом <application> пишем:

{% gist 058c9231d295e351827503bb93870802 %}

Теперь внутри <application> добавляем ApplicationId:

{% gist cbf3abf6a23182fcf415d0e7e4d9f257 %}

В res/values/strings.xml добавим две строчки, значения в которые добавим позднее:

{% gist fd9234fdbc0865b8e849bf2e8aab450c %}



