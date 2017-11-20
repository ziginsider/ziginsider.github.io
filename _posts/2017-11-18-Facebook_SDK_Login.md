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

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo">https://github.com/ziginsider/FacebookSDKDemo</a>

<br>
### Введение
Постановка задачи: Познакомиться с Facebook SDK. Залогиниться. Получить некоторые данные, как то картинка профиля, дата рождения, email, число френдов, etc.

<br>
### Начало
Создаем новый проект, выбираем Empty Activity. Затем подключаем библиотеки: 
- Facebook SDK
- Picaso

NB: Не стоит включать в название проекта слово "Facebook" или "FB" - как показал опыт Facebook ругается на это, когда регистрируешь приложение.

Facebook <a href="https://developers.facebook.com/docs/android/componentsdks">советует</a>: В своем проекте откройте your_app -&gt; Gradle Scripts -&gt; build.gradle (Project) и добавьте следующий репозиторий в раздел buildscript { repositories {}}, чтобы скачать SDK с Maven Central Repository:

{% gist c59968cb47f18e468c70335aa50504c3 %}

Теперь в build.gradle (Module: app) добавляем инструкции компиляции в раздел dependencies{}.

{% gist f2ad9ffeeccfeac3228a4a500d7268d6 %}

<br>
### Макет
Подготавливаем макет Activity:

{% gist 25b7947b45be90c506572acec2a153bb%}

Прописываем разрешения и мета-данные в манифесте. Перед тегом &lt;application&gt; пишем:

{% gist 058c9231d295e351827503bb93870802 %}

Теперь внутри &lt;application&gt; добавляем ApplicationId:

{% gist cbf3abf6a23182fcf415d0e7e4d9f257 %}

И последнее, но не обязательное как показал опыт. Прописываем в манифесте внутри тегов &lt;activity&gt; &lt;intent-filter&gt; ... схему (тип) данных, которые будет принимать наша Activity:

{% gist 6e6d29d0ba04220288a4d609dc3d6de6 %}

В res/values/strings.xml добавим две строчки, значения в которые пропишем позднее:

{% gist fd9234fdbc0865b8e849bf2e8aab450c %}

<br>
### Key Hash и регистрация приложения на Facebook
Теперь получим Key Hash в формате Base64 согласно <a href="https://developers.facebook.com/docs/android/getting-started/?locale=ru_RU">данной документации</a>. В Activity временно пишем код (разумеется "..." это пропуски кода):

{% gist 742ea2b0b4441835cae244c2024af888 %}

Запускаем приложение и в логах находим Key Hash:

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

<br>
### Рабочий код
Теперь добавим в MainActivity некоторые переменные, которые нам понадобятся в дальнейшем, и переопределим onActivityResult(...), чтобы ловить ответы, которые будут приходить от Facebook:

{% gist a51081568c05398d776886a351861a00 %}

Итак, по requestCode будем определять на какой именно запрос пришел ответ, resultCode показывает удачно ли завершился запрос, а data - массив данных, из которых мы будем получать информацию. CallbackManager, согласно <a href="https://developers.facebook.com/docs/reference/android/current/interface/CallbackManager/">документации Facebook</a>, будет управлять нашими запросами к Facebook через onActivityResult(...).

Теперь в MainActivity onCreate(...) определим наши View и зададим CallbackManager для кнопки:

{% gist c3b8b3410ec7b6fb17f842b5c6f10f19 %}

printKeyHash() можно удалить или закомментить. Эта функция нам больше не понадобится.

setReadPermissions(List) - задаем разрешения на использование информации, которая будет предоставлена, если пользователь залогинился. Разрешения дается только на чтение. Список разрешений можно глянуть на <a href="https://developers.facebook.com/docs/facebook-login/permissions/v2.2">этой странице</a>.

Переопределим функцию ответа на запрос о регистрации onSuccess(...)  (onCancel(...) и onError(...) за рамками данной заметки):

{% gist dcfaff1ec5eb9d3dca010440828c0b61 %}

Классы GraphRequest и GraphResponse позволяют отправлять запросы и получать ответы в формате JSON в асинхронном режиме. Собственно это обертка Facebook SDK для интеграции с API Graph (основной инструмент для загрузки и получения данных из социального графа Facebook). 

В классе GraphRequest метод newMeRequest вызывает эндпойнт /user/me, чтобы извлечь данные пользователя для указанного маркера доступа.

Facebook Android SDK отправляет все разрешения, указанные в access_token, тем самым обеспечивая контроль доступа к данным. 

По умолчанию метод newMeRequest извлекает из объекта пользователя поля, заданные по умолчанию. Если вам нужны дополнительные поля или в целях повышения производительности нужно сократить полезную нагрузку ответа, добавьте параметр fields и запросите требуемые поля. В нашем случае это "id, email, location, birthday, friends".

В методе обратного вызова данные ответа десериализуются в JSONObject, если запрос выполнен успешно. Поля, которые невозможно извлечь из-за отсутствия необходимых разрешений, будут исключены из результата. Вот пример ответа в формате JSON, который мы будем разбирать:

{% gist c52abad2c21733072158a37fd3f854f0 %}

Итак, десериализуем полученный ответ в методе getData(JSONObject)

{% gist 0b60055652a7275f5ba879e58c0b1047 %}

Первым делом извлекаем картинку профиля. В дело вступает библиотека Picasso. Далее получаем необходимые нам поля. Все довольно просто и интуитивно понятно.

Если регистрация уже пройдена, то незачем запускать ее снова. Добавим в onCreate(...):

{% gist aa36769010d2de0ecb32d6421e5e8acf %}

Стоит запустить проект на реальном устройстве. Получим что-то подобное:

<img src="{{ site.baseurl }}/images/success_facebook_1.png">
<br>
<br>

<img src="{{ site.baseurl }}/images/success_facebook_2.png">


Совет: пользуйтесь документацией developers.facebook.com - там вполне понятно и доступно изложены основы и нюансы работы с Android Facebook SDK.

Проект на github: <a href="https://github.com/ziginsider/FacebookSDKDemo">https://github.com/ziginsider/FacebookSDKDemo</a>
<br>
end.
