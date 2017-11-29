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

Теперь добавим простое меню, по которому мы будем добавлять записи, сохранять изменения редактируемых записей и удалять записи в базе данных. Итак, добавим три иконки (ic_new, ic_remove, ic_save), например такие:

<img src="{{ site.baseurl }}/images/firebase/icons.jpg">

и добавим соответствующий им файл меню в наш проект. Для этого в res добавляем папку menu и там создаем файл "menu_main.xml":

{% gist f2e42d5f892da9000ecf938536f8f207 %}

Теперь добавим Toolbar. В файле res - values - styles.xml параметр parent у "AppTheme" меняем на parent="Theme.AppCompat.Light.NoActionBar"

В "activity_main.xml" добавляем описание макета Toolbar:

{% gist cf692fabf96c2566f45d9663483d2a85 %}

И, наконец, регистрируем Toolbar в MainActivity:

{% gist a868876e7219067718de9914db2a25ed %}

Инициализируем созданное нами меню. Для этого переопределяем в MainActivity onCreateOptionsMenu(...):

{% gist be8c18b09c2ed658e0d57168bd49c017 %}

Создадим модель данных, которые мы будем хранить в Firebase. Пусть это будет список контактов у которых есть поле name и поле email.

В MainActivity будем отображать список контактов в виде ListView. Добавим макет элемента списка. В layout создаем "listview_item.xml":

{% gist 56653a80c032f5d655e798f901ba6733 %}

Добавим формы для ввода в макет главного окна, в "activity_main.xml" добавляем: 

{% gist 57f915b601d3d5ea7b6860d7a584a7b8 %}

При этом надо учесть, что т.к. мы используем TextInputLayout у нас должна быть в build.gradle (Module:app) подключена библотека design, например 'com.android.support:design:26.1.0'

Добавим в "activity_main.xml" ListView в котором будет отображаться список контактов:

{% gist fe23e485fc8fc559ddea4f220db4dca1 %}

Добавим также ProgressBar в "activity_main.xml", который будет показывать что данные загружаются с Firebase:

{% gist 455e6674540aa0f614ccd2495da95646 %}

В Preview получим примерно такое:

<img src="{{ site.baseurl }}/images/firebase/maket_1.jpg">

Таким образом, макет отображения данных у нас есть. Теперь возмемся за начинку.

Создаем модель данных:

{% gist f1db847f923ccac8088813231af3f1f0 %}

Пишем адаптер для ListView:

{% gist a58dcf7da0b658c26b8994b96130cdf7 %}

И инициализируем все View, используемые нами, в MainActivity:

{% gist 8904df6a2c93b27e07e39951def61a31 %}

Наконец, перейдет к Firebase. Инициализируем Firebase и получим ссылку на базу данных. Для этого добавляем в onCreate(...) функцию initFirebase():

{% gist 3938d0c98fc3406d358b243b1437468b %}

Теперь в onCreate(...) добавляем функцию addEventFirebaseListener() в которой создадим слушатель, который будет обнавлять записи в ListView, когда в базе данных Firebase происходят изменения:

{% gist 25bfdee33a531a3f85c2c745acb41d16 %}

Теперь в консоли Firebase в разделе Database изменим правила, чтобы данные читались и писались из нашего приложения в базу данных Firebase. Для этого для чтения и записи выставляем "true". Публикуем правила.

<img src="{{ site.baseurl }}/images/firebase/firebase_rules.jpg">

Наконец описываем что-же произойдет когда мы нажимаем на кнопки ранее созданного меню (напомним: "создать запись", "сохранить изменения в записи", "удалить запись").

Переопределяем функцию onOptionsItemSelected(MenuItem item), которая ловит нажатия на кнопки меню:

{% gist 9f311e54f0fae1634c6bbdc886af70d9 %}

Теперь нам надо написать тело функций createUser(), updateUser(selectedUser) и deleteUser(selectedUser), но для начала переопределим слушатель нажатия на элемент списка ListView, чтобы определять выбранную запись = selectedUser. Создаем глобальную переменную selectedUser и пишем тело слушателя нажатия на элемент ListView в onCreate(...):

{% gist f2e572778c12249d8eac2833d2c9a678 %}

Пишем createUser():

{% gist 290da8bbb5acc5aa3bfca279271a6193 %}

updateUser(selectedUser):

{% gist f540b589b47b59a843584216bdbfc751 %}

deleteUser(selectedUser)

{% gist a949606fbae8f56842c2334b3050148c %}

Если все сделали правильно, длжно работать. Мы можем добавлять данные в базуданных Firebase, редактировать и удалять их. В консоли Firebase изменение данных можно наблюдать "в прямом эфире":

На телефоне:

<img src="{{ site.baseurl }}/images/firebase/firebase_phone.jpg">

В консоле Firebase:

<img src="{{ site.baseurl }}/images/firebase/firebase_database.jpg">

Например, когда мы удаляем данные, в консоли они окрашиваются в красный цвет:

<img src="{{ site.baseurl }}/images/firebase/remove_firebase_database_item.jpg.jpg">

end.

