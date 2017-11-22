---
layout: post
title: У меня было 10 Android собеседований за последние два года... (перевод)
date: 2017-11-22 11:16
tags:
- Android
- Java
- Interview
---
<img src="{{ site.baseurl }}/images/android_interview.jpg">
<br>
*Перевод статьи Mohamed Ibrahim <a href="https://medium.com/@MohamedIsoliman/i-had-10-android-interviews-during-the-last-two-years-heres-the-questions-plus-some-lessons-i-ve-cdc583dfbc65">I had 10 Android interviews during the last two years, here’s the questions plus some lessons I’ve learned</a>*.

## У меня было 10 Android собеседований за последние два года. Вот вопросы, которые мне задавали, и уроки которые я извлек.

Прошло два года с тех пор, как я стал заниматься разработкой на Android. Я был поражен количеством ресурсов для изучения Android, и тем, как сообщество разработчиков делится знаниями и объединяется, чтобы сделать разработку более увлекательной, и тем как постепенно растут требования разработчиков к тестированию кода, его поддержке и удобочитаемости.

На протяжении этих двух лет у меня было около десяти собеседований. Одни из них проходили гладко, другие - не очень, но каждое из них показывало мои пробелы в знаниях. Обычно, цель соискателя на собеседовании - получить работу, но кроме того это может быть хороший инструмент, чтобы понять свой уровень в аспектах языка, средств программирования и бизнес-циклах разработки. 

У меня не было опыта в компьютерных науках, поэтому я решил черпать знания из чтения, прохождения различных руководств, включая, разумеется, материалы на Udacity. Я даже начал проходидь курс на MAL под названием "Основы Android", и с этого момента началась моя история разработки под Android.

Давайте сначала я расскажу о стилях собеседований в разных компаниях, куда я попадал (названия компаний я обозначил инициалами), а затем перейдем к вопросам, которые мне запомнились.

<br>
### Стиль собеседования
EP: Мэйнстрим Android разработки и вопросы по Java. - Задачи: экран входа в систему с email и паролем, зарегистрированный пользователь должен автоматически входить в систему, при повторном использовании приложения.

IC: Собеседование в свободной, дружественной форме. Разговор о средствах разработки, технологиях и качестве кода. - Задачи: нет.

SD: Тестирования гибкости кандидата (например, способность переключатся между нативной и гибридной разработкой). - Задачи: сделать игру, в которой предметы только определенного рода собираются в ведро.

AT: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

AR: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

SW: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

RA: Чем больше вы верно отвечаете, тем сложнее вопросы. - Задачи: приложение для фото, в котором изображения хранят метку о погоде.

VN: Чем больше вы верно отвечаете, тем сложнее вопросы. Общение в дружественной форме - Задачи: нет.

IB: Упор на Java. Вопросы становятся сложнее. - Задачи: приложение, которое показывает список авиакомпаний с сервера api.

WM: Java и Android и тестирование гибкости. - Задачи: нет.

Это все. Надеюсь я ничего не забыл. Однако, почему я дал список собеседований в таком виде? Потому что компании разные, некоторым из них нужен Android разработчик чтобы сделать конкретную работу, и сделать ее идеально - это, обычно, большие компании.

Другим может потребоваться разработчик, открытый для новых знаний, который быстро обучается, может работать с разными технологиями (бэкенд, системное администрирование и т.д.) - это могут быть небольшие компании или стартапы. И у каждой компании своя перспектива на вас. Поэтому вам не стоит опираться только на технические детали. Узнайте больше о компании, гляньте ее продукты, перед тем как идти на собеседование. Подготовьте свои вопросы для них, потому что это не одностороннее интервью и никогда не должно быть таким.

Сейчас я приведу список вопросов. Но не стоит просто запоминать ответы на них. Это плохой путь. Необходимо самому прийти к пониманию каждого вопроса. Попробуйте почитать stackoverflow по каждой теме, читайте комменты также, я нахожу этот портал лучшим, для объяснения технических вопросов, потому что каждый из отвечающих хочет сделать это лучше.

Старайтесь создавать небольшие приложения, чтобы понять, как работает та или иная штука. Примеры Google - хороший способ для изучения разных областей Android разработки.

<br>
### Вопросы на собеседованиях (не упорядочены по сложности)

1. Какие последние версии Android? Наиболее важные новые фичи в Marshmallow?

2. Какая цель у Activity?

3. Какая цель у Fragment'ов?

4. Расскажите о жизненном цикле Activity?

5. Расскажите о жизненном цикле Fragment?

6. Вы используете приложение для путешествий, затем нажимаете кнопку настроек, открывается Activity настроек, затем вы кликаете "назад" - что происходит с жизненным циклом Activity настроек и с циклом главного Activity при этом?

7. 
6- you’re using a traveling app then you clicked settings button, Settings Activity opened, then you click Android back, what’s the lifeCycle of the Settings Activity and the Home Activity when you did that?
7- what do you know about Material design?
8- what’s the difference between Abstract class and Interface in Java?
9- what’s an Interface in Java?
10- what’s an Abstract class in Java?
11- why you couldn’t create an instance from an abstract class?
12- what’s the difference between Dialog and AlertDialog in Android?
13- what’s the difference between LinearLayout and RelativeLayout?
14- which has better performance, LinearLayout or RelativeLayout?
15- given a simple contact item, with image and name and number, how could you implement it in XML?
16- what’s the Service, which thread it operates on?
17- what’s the difference between Service and IntentService?
18- what’s ANR message?
19- explain the BroadcastReciever job and implementation?
20- can you use a Fragment with no UI? What cases could make you use this pattern?
21- explain the Java access modifiers?
22- what’s the difference between Default and Protected access modifiers in Java?
23- what do you know about AsyncTask?
24- what’s the difference between Parcelable and Serializable? Which one is better? why?
25- how to access a variable in Activity from fragment?
26- you have one Activity with two fragments, one has a button and the second has a TextView, clicking the button change the TextView, how do you implement it?
27- how to make a variable thread safe?
28- what strategies we can use to achieve thread safety?
29- what is the purpose of “static” keyword in Java?
30- how could you initialize a static variable in Java?
31- what design patterns you know?
32- explain the builder pattern?
33- when do you use an observer pattern?
33- what’s the Singleton, when do you use it in Android?
34- what’s the difference between the LinkedList, ArrayList and Arrays?
35- what projects currently you work on? What is your workflow to implement a specific feature?
36- how do you handle Firebase push notifications?
37- how do you implement Firebase realtime Database?
38- you have a big project, and you have a login screen requirement, what processes you will follow to ship it?
39- what’s an Eventbus?
40- what the thread that onRecieve() method of a BroadcastReceiver operates on?
41- how to implement a custom BroadcastReceiver?
42- what’s the difference between MVC and MVP?
43- could you explain MVVM?
44- what’s the M in MVP? Answering … could it be a something else?
45- what’s the purpose of Content Provider?
46- what Sqlite library do you use?
47- what libraries do you use for Networking, Image loading, Database?
48- what do you use to handle a very fast Sensor that emit many readings at a time in Rx way?
49- what’s the difference between map and flatMap() in Rxjava?
50- how to create parallel Network calls with Rxjava?
51- if you have one request from the network and you want to call the cache if Network throw an error … how to achieve that via Rxjava?
The funny thing that I’ve read Dan lew blog post about this case, implemented it twice before, but couldn’t answering this question during the interview … bad things happen.
52- what’s the difference between concatMap() and flatMap() in Rxjava?
53- what do you know about Intents? What is the purpose of categories in Intents?
54- what’s the purpose of FrameLayout?
55- how to compare between Two objects?
56- Java is pass by Value or pass by Reference?
57- when you use observeOn() and subscribeOn()?

<details>
   <summary>1</summary>
   <p>2</p>
</details>

:+1:
:sweat:

:wink:

:triumph:
[to be continued...]
