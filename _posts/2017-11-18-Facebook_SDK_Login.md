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

Facebook <a href="https://developers.facebook.com/docs/android/componentsdks">советует</a>: В своем проекте откройте your_app -&gt; Gradle Scripts -&gt; build.gradle (Project) и добавьте следующий репозиторий в раздел buildscript { repositories {}}, чтобы скачать SDK с Maven Central Repository:

{% gist c59968cb47f18e468c70335aa50504c3 %}

Теперь в build.gradle (Module: app) добавляем инструкции компиляции в раздел dependencies{}.

{% gist f2ad9ffeeccfeac3228a4a500d7268d6 %}

Подготавливаем макет Activity:

{% gist 25b7947b45be90c506572acec2a153bb%}

Прописываем разрешения и мета-данные в манифесте. Перед тегом &lt;application&gt; пишем:

{% gist 058c9231d295e351827503bb93870802 %}

Теперь внутри &lt;application&gt; добавляем ApplicationId:

{% gist cbf3abf6a23182fcf415d0e7e4d9f257 %}

В res/values/strings.xml добавим две строчки, значения в которые пропишем позднее:

{% gist fd9234fdbc0865b8e849bf2e8aab450c %}

Теперь получим Key Hash в формате Base64 согласно <a href="https://developers.facebook.com/docs/android/getting-started/?locale=ru_RU">данной документации</a>. В Activity временно пишем код (разумеется "..." это пропуски кода):

{% gist 742ea2b0b4441835cae244c2024af888 %}

Запускаем приложение и в логах находим наш Key Hash:

<img src="{{ site.baseurl }}/images/KeyHashFacebook.jpg">

<br>
Если вы еще не зарегистрированы как разработчик на Facebook, то заходим на сайт developers.facebook.com и в правом верхнем углу находим кнопку "начать", жмем, выполняем инструкции и попадаем в панель управления приложением.

Далее "Настройки" ("Settings") -&gt; "Основное"("Basic"). Внизу видим кнопку "+ Добавить платформу" ("+ Add platform"). Жмем. Добавляем Android. В поле "Название пакета Google Play" ("Google Play package name") вводим свой package. В моем случае это "io.github.ziginsider.facebooksdkdemo". В поле "Название класса" ("Class name") полное имя класса Activity - в моем случае "io.github.ziginsider.facebooksdkdemo.MainActivity". В поле "Ключевые хэш-адреса" ("Key Hashes") вводим полученный ранее Key Hash.

<img src="{{ site.baseurl }}/images/facebook_dashboard_1.jpg">

<br>
Сохраняем изменения.

Далее берем "Идентификатор приложения" ("App ID") и записываем его в значения res/values/strings.xml. В моем случае:

{% gist b00e38794881875c7d51735efd67e65a %}

Т.е., во второй строке, просто добавляем "fb" перед идентификатором.

Теперь добавим в MainActivity некоторые переменные, которые нам понадобятся в дальнейшем, и переопределим onActivityResult(...), чтобы ловить ответы, которые будут приходить от Facebook:

{% gist a51081568c05398d776886a351861a00 %}

Итак, по requestCode будем определять на какой именно запрос пришел ответ, resultCode показывает удачно ли завершился запрос, а data - массив данных, из которых мы будем получать информацию. CallbackManager, согласно <a href="https://developers.facebook.com/docs/reference/android/current/interface/CallbackManager/">документации Facebook</a>, будет управлять нашими запросами к Facebook через onActivityResult(...).

Теперь в MainActivity onCreate(...) определим наши View и зададим CallbackManager для кнопки:

{% gist c3b8b3410ec7b6fb17f842b5c6f10f19 %}




