---
layout: post
title: Firebase Tutorial - Firebase database. Part I.
date: 2017-11-26 21:59
tags:
- Android
- Java
- Firebase
---
<img src="{{ site.baseurl }}/images/firebase/firebase_logo.png">
<br>

*Firebase. Регистрация приложения. База данных Firebase.*

Проект на github: <a href="https://github.com/ziginsider/FirebaseDemo/tree/master">https://github.com/ziginsider/FirebaseDemo</a>

<br>
### Введение
Постановка задачи: Познакомиться с Firebase. Зарегистрировать приложение на console.firebase.google.com. Познакомиться с NoSQL базой данных Firebase.

О Firebase (обзор):
1. https://www.youtube.com/watch?v=0mRmHqz0-W8
2. https://www.youtube.com/watch?v=CDXUczHzZn8
3. https://www.youtube.com/watch?v=4kcN65wICVs 
4. https://www.youtube.com/watch?v=KGsPL7o2R7E - краткий обзор

### Подключение к Firebase

Подключится можно двумя способами: автоматически и вручную. Подключимся автоматически. В Android Studio выбираем Tools - Firebase. Открывается Firebase Assistant. Нам нужно Realtime Database.

<img src="{{ site.baseurl }}/images/firebase/firebase_1.jpg">

Сначала Assiatant предложит подключить приложение к Firebase. Нажимаем. Следуем инструкциям (необходим аккаутн Google). Подключили. Затем добавляем Realtime Database в наше приложение. Если все ок, в Assistant мы получим надпись зеленым шрифтом: "Dependencies set up correctly". 

<img src="{{ site.baseurl }}/images/firebase/firebase_2.jpg">

В консоли Firebase теперь можно увидеть наш проект:

<img src="{{ site.baseurl }}/images/firebase/firebase_3.jpg">

Если что-то пошло не так, можно подключить проект вручную. Наглядный пример см. <a href="https://youtu.be/tAV_ehyZmTE?t=1m5s">здесь</a>

Теперь добавим простое меню, по которому мы будем добавлять, сохранять и удалять записи в базе данных. Итак, добавим три иконки (ic_new, ic_remove, ic_save), например такие:

<img src="{{ site.baseurl }}/images/firebase/icons.jpg">

и добавим соответствующий им файл меню в наш проект. Для этого в res добавляем папку menu и там создаем файл "menu_main.xml":

{% gist f2e42d5f892da9000ecf938536f8f207 %}

Теперь добавим Toolbar. В файле res - values - styles.xml параметр parent у "AppTheme" меняем на parent="Theme.AppCompat.Light.NoActionBar"

В "activity_main.xml" добавляем описание макета Toolbar:

{% gist cf692fabf96c2566f45d9663483d2a85 %}

И, наконец, регистрируем Toolbar в MainActivity:

{% gist a868876e7219067718de9914db2a25ed %}


[в процессе...]
