---
layout: post
title: Firebase Tutorial. Part II. - Как автоматически развернуть сайт на хостинге Firebase из GitHub-репозитория? 
date: 2017-12-09 00:19
tags:
- Android
- Java
- Firebase
- GitHub
- Travis CI
---
<img src="{{ site.baseurl }}/images/firebase/firebase_logo.png">
<br>

*Firebase. Хостинг Firebase. Деплоинг сайта из GitHub.*

<br>
### Введение

Firebase предоставляет услуги хостинга. Для бесплатного аккаунта это 1 Гб свободного места, домен типа &#42;.firebaseapp.com, где "&#42;" - ID проекта Firebase, ну и все плюшки Firebase. Т.е. удобная работа с хостингом через командную строку firebase CLI (например развертка сайта одной командой), быстрая сеть доставки контента CDN, которая позволяет вашему сайту быстро загружаться, защита данных (Zero-configuration SSL), ну и поддержка всевозможных технических мэйстримов современного веба.

Возможность развернуть сайт может понадобится и для Android-разработки. Например, для настройки индексации вашего приложения в поисковой системе Google (Firebase App Indexing), когда необходимо связать сайт и приложение. О самой индексации не знаю стоит ли писать: есть много англоязычных туториалов и, если не ошибаюсь, два Google Codelabs. Но кратко: она может быть полезна для привлечения поискового траффика для вашего приложения. Ну а начиная с Android M, <a href="https://firebase.google.com/docs/app-indexing/?utm_campaign=io15&utm_source=dac&utm_medium=blog">индексация</a> необходима для взаимодействия с помощником Google Now (этакий своеобразный бот, который не переключаясь между приложениями, поможет вам быстро и эффективно получать нужную информацию). Поэтому, думается, индексация станет хорошим тоном для разработки бизнес-приложений.

<br>
### Запуск хостинга Firebase из консоли.

В консоле Firebase перейдите на вкладку Hosting. Далее следуйте инструкциям и за пару шагов получите свой сайт.

Вам предложат установить Node.JS, затем из командной строки выполнить пару нехитрых инструкций и сайт развернется автоматически, с дефолтным index.html. Можно, конечно, заранее подготовить файлы сайта и развернуть их.

### Запуск из GitHub репозитория

Сайт можно развернуть сразу из GitHub репозитория.

Для этого нам нужно две вещи:

1. Собственно, аккаунт на GitHub с репозиторием вашего сайта 
2. Платформа непрерывной интеграции Travis CI 

Travis CI - это распределённый веб-сервис для сборки и тестирования программного обеспечения привязанный к GitHub. Т.е. простыми словами, вы можете настроить сборку вашего проекта автоматически, прямо с репозитория. Вы делаете коммит - проект автоматически собирается, без вашего участия. 

В той заметке, я не буду влезать в технические дебри Travis CI, просто пошагово покажу как двумя способами можно настроить автоматическую сборку проекта (в нашем случае - развернуть сайт на Firebase Hosting).

Итак, просто переходите на <a href="https://travis-ci.org">travis-ci.org</a>, регистрируйтесь, используя логин и пароль вашего аккаунта на GitHub. Получаете список ваших репозиториев:

<img src="{{ site.baseurl }}/images/firebase/travis_accaunts.jpg">

И активируете репозиторий с сайтом.

В корне репозитория нам нужно создать конфигурационный файл ".travis.yml", в котором мы пропишем инструкции для сервера Travis CI. Кроме того, создадим (не во всех случаях обзательно, но в учебных целях познакомимся с ними) конфигурационные файлы для Firebase Hosting. Начнем с последних:

Первый файл dabase.rules.json - прописываем правила доступа к базе данных Firebase. По умолчанию файл такой:

{% gist 43b8861b017f4b2f4221b9aee6827c88 %}

Второй: firebase.json - файл конфигурации репозитория, который будет учитывать Firebase, при развертывании сайта. Например, такой файл автоматически создается когда вы выполняете команду `firebase init` в консоли Node.JS:

{% gist e0ab9fefe8be5f8ec06b9cdf95897795 %}

Обратите внимание на пару ключ-значение "public": "public" - справа вы должны указать папку в которой находятся файлы сайта, они и будут перезалиты на хостинг. Соответственно в репозитории на GitHub у вас должна быть эта папка с сайтом. 

Больше о файле firebase.json см. <a href="https://firebase.google.com/docs/hosting/deploying#section-firebase-json">в документации</a>

Я создал папку public и поместил туда один единственный файл "index.html":

{% gist 6afa6fd5d76d64bb54f8e14ddf7321f5 %}

Теперь, когда мы подготовили файлы сайта и файлы конфигурации Firebase, нам надо в корне репозитория на GitHub создать вышеупомянутый файл ".travis.yml". Travis CI будет от нашего имени развертывать файлы сайта на хостинг, как только репозиторий будет меняться. Но для того, чтобы Travis смог действовать от нашего имени, нам нужно передать ему токен доступа. Получить токен довольно просто. В командной строке Node.JS выполняем следующую команду:

`firebase login:ci`

Получаем заветный токен. Идем на travis-ci.org/ваш_логин/ваш_репозиторий/settings. И в разделе Environment Variables добавляем токен. Назовем его, например, FIREBASE_TOKEN:

<img src="{{ site.baseurl }}/images/firebase/travis_token.jpg">

Наконец, все что нам осталось сделать - это написать ".travis.yml".

### .travis.yml для Firebase Hosting - способ №1

{% gist 7ed68cfc8e44438e2581d1d76a73b909 %}

Вместо "myapp-staging" должно быть ID вашего проекта (можно глянуть в насторойках проекта на Firebase или выполнить в консоли 'firebase list' и получить список текущих проектов Firebase с их ID) или его псевдоним. 

### .travis.yml для Firebase Hosting - способ №2

{% gist 2045d741f96981b1b1fb3c3fe776c5dc %}

Все, теперь наш сайт будет автоматически развертываться из GitHub при каждом изменении репозитория.

Процесс развертки можно наблюдать в аккаунте Travis CI

<img src="{{ site.baseurl }}/images/firebase/travis_success.jpg">

проект на GitHub: <a href="https://github.com/ziginsider/site">https://github.com/ziginsider/site</a> 

end.