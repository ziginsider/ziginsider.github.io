---
layout: post
title: Видео. Architecture Components. Improve Your App's Design. Перевод субтитров.
date: 2017-09-01 19:25
tags:
- Java
- Android
- Архитектура
- Video
- Youtube
- Translate
- Architecture Components
- Философия
---
*Перевод английских субтитров на русские из видео Architecture Components: Improve Your App's Design. Начало 01.09.2017, конец - 07.09.2017. All rights reserved.*

Смотри другие переводы видео (субтитры) по этой теме: <a href="https://ziginsider.github.io/tags/#Architecture+Components">Tag: Architecture Components</a>

Мой клон с русскими `субтитрами`:
<iframe width="560" height="315" src="https://www.youtube.com/embed/P_XPLT5ZwcE" frameborder="0" allowfullscreen></iframe>

Оригинальное видео:
<iframe width="560" height="315" src="https://www.youtube.com/embed/vOJCrbr144o" frameborder="0" allowfullscreen></iframe>

Аннотация к видео:
+ Build robust Android apps using the new architecture components. New classes and interfaces, such as ViewModel, LiveData and LifecycleObserver, make it easy to access and manage the Activity and Fragment Lifecycle. Room, an object mapping library for SQLite, simplifies caching, loading and displaying your app’s data. Used together, you can quickly generate SQLite databases and get information into your app’s UI with far less boilerplate code, letting you focus on the code that makes your app unique.

Перевод:
+ Создавайте надежные приложения для Android, используя новые архитектурные компоненты. Новые классы и интерфейсы, такие как ViewModel, LiveData и LifecycleObserver, облегчают доступ к жизненному циклу Activity и Fragment и управлению ими. Room, object mapping library для SQLite, упрощает кэширование, загрузку и отображение данных вашего приложения. Используя все это, вы можете быстро создавать базы данных SQLite и получать информацию в UI вашего приложения с гораздо меньшим количеством шаблонного кода. Это позволяет вам сосредоточиться на коде, который делает ваше приложение уникальным.

Ссылки к видео:
- <a href="https://goo.gl/po4gyH">единая точка входа для архитектурных компонентов</a> - LiveData, ViewModel, LifecycleObserver, LifecycleOwner, Room (абстрация над SQLite базой данных), etc.
- <a href="https://codelabs.developers.google.com/codelabs/android-persistence/#0">Android Persistence: Room Library</a> - tutorial codelab.
- <a href="https://medium.com/@tonyowen/a-room-with-a-view-getting-started-ec010f9f5448">о Room</a> - article with Kotlin.
- <a href="https://academy.realm.io/posts/android-architecture-components-and-realm/">Room, ViewModel, LifeCycle, LiveData</a> - article
- <a href="https://codelabs.developers.google.com/codelabs/android-lifecycles/#0">Android lifecycle-aware components</a> - tutorial codelab.
- <a href="https://www.youtube.com/watch?v=vOJCrbr144o">Architecture Components: Improve Your App's Design</a> - видео-обзор от Google новых архитектурных компонентов, 5 мин 41 сек на просмотр.


<style type="text/css">
   table{
    border-collapse: collapse;
    border-spacing: 0;
    border:1px solid #000000;
    cellpadding: 3px;

}

th{
    border:1px solid #000000;
}

td{
    border:1px solid #000000;
    padding: 10px;
}
</style>
<table bordercolor="black" border="1">
   <caption>Перевод субтитров</caption>
  <tr>
    <th>English</th>
    <th>Русский</th>
  </tr>
  <tr><td>1<br>
00:00:00,000 --> 00:00:02,130<br>
LYLA: In response<br>
to popular demand,<br>
<br>
2<br>
00:00:02,130 --> 00:00:05,010<br>
the Android Framework team has<br>
written an opinionated guide<br>
<br>
3<br>
00:00:05,010 --> 00:00:06,960<br>
to architecting Android<br>
apps, and they've<br>
<br>
4<br>
00:00:06,960 --> 00:00:09,870<br>
developed a companion set<br>
of architecture components.<br>
<br>
5<br>
00:00:09,870 --> 00:00:12,960<br>
Hi, my name's Lyla, a<br>
developer advocate for Android,<br>
<br>
6<br>
00:00:12,960 --> 00:00:15,900<br>
and I'm here to introduce you<br>
to these shiny new architecture<br>
<br>
7<br>
00:00:15,900 --> 00:00:17,070<br>
components.<br>
<br>
8<br>
00:00:17,070 --> 00:00:19,890<br>
These components persist<br>
data, manage lifecycle,<br>
<br>
9<br>
00:00:19,890 --> 00:00:22,860<br>
make your app modular, help<br>
you avoid memory leaks,<br>
<br>
10<br>
00:00:22,860 --> 00:00:26,430<br>
and prevent you from having to<br>
write boring boilerplate code.<br>
<br>
11<br>
00:00:26,430 --> 00:00:28,680<br>
Your basic Android<br>
app needs a database<br>
<br>
12<br>
00:00:28,680 --> 00:00:30,780<br>
connected to a robust UI.<br>
<br>
13<br>
00:00:30,780 --> 00:00:33,890<br>
The new components, Room,<br>
ViewModel, LiveData,<br>
<br>
14<br>
00:00:33,890 --> 00:00:35,732<br>
and Lifecycle, make that easy.<br>
<br>
15<br>
00:00:35,732 --> 00:00:38,190<br>
They're also designed to fit<br>
together like building blocks,<br>
<br>
16<br>
00:00:38,190 --> 00:00:39,690<br>
so let's see how.<br>
<br>
17<br>
00:00:39,690 --> 00:00:42,990<br>
I'll tackle the database using<br>
Room, which is a new SQLite<br>
<br>
18<br>
00:00:42,990 --> 00:00:44,820<br>
object mapping library.<br>
<br>
19<br>
00:00:44,820 --> 00:00:46,440<br>
To set up the tables<br>
using Room, we<br>
<br>
20<br>
00:00:46,440 --> 00:00:49,550<br>
can define a Plain Old<br>
Java Object, or a POJO.<br>
<br>
21<br>
00:00:49,550 --> 00:00:52,950<br>
We then mark this POJO<br>
with the @Entity annotation<br>
<br>
22<br>
00:00:52,950 --> 00:00:56,650<br>
and create an ID marked with<br>
the @PrimaryKey annotation.<br>
<br>
23<br>
00:00:56,650 --> 00:00:59,820<br>
Now for each POJO, you need<br>
to define a DAO, or a Database<br>
<br>
24<br>
00:00:59,820 --> 00:01:01,290<br>
Access Object.<br>
<br>
25<br>
00:01:01,290 --> 00:01:03,130<br>
The annotated methods<br>
represent the SQLite<br>
<br>
26<br>
00:01:03,130 --> 00:01:05,950<br>
commands that you need to<br>
interact with your POJO's data.<br>
<br>
27<br>
00:01:05,950 --> 00:01:08,790<br>
Now, take a look at this insert<br>
method and this query method.<br>
<br>
28<br>
00:01:08,790 --> 00:01:11,400<br>
Room has automatically<br>
converted your POJO objects<br>
<br>
29<br>
00:01:11,400 --> 00:01:14,265<br>
into the corresponding database<br>
tables, and back again.<br>
<br>
30<br>
00:01:14,265 --> 00:01:17,130<br>
Room also verifies your<br>
SQLite at compile time.<br>
<br>
31<br>
00:01:17,130 --> 00:01:19,150<br>
So if you spell something<br>
a little bit wrong,<br>
<br>
32<br>
00:01:19,150 --> 00:01:21,150<br>
or if you reference a<br>
column that's not actually<br>
<br>
33<br>
00:01:21,150 --> 00:01:24,310<br>
in the database, it will<br>
throw a helpful error.<br>
<br>
34<br>
00:01:24,310 --> 00:01:26,070<br>
Now that you have<br>
a Room database,<br>
<br>
35<br>
00:01:26,070 --> 00:01:27,570<br>
you can use another<br>
new architecture<br>
<br>
36<br>
00:01:27,570 --> 00:01:30,210<br>
component, called LiveData,<br>
to monitor changes<br>
<br>
37<br>
00:01:30,210 --> 00:01:31,320<br>
in the database.<br>
<br>
38<br>
00:01:31,320 --> 00:01:33,900<br>
LiveData is an<br>
observable data holder.<br>
<br>
39<br>
00:01:33,900 --> 00:01:35,910<br>
That means it holds<br>
data and notifies you<br>
<br>
40<br>
00:01:35,910 --> 00:01:39,090<br>
with the data changes so<br>
that you can update the UI.<br>
<br>
41<br>
00:01:39,090 --> 00:01:41,790<br>
LiveData is an abstract<br>
class that you can extend,<br>
<br>
42<br>
00:01:41,790 --> 00:01:45,600<br>
or, for simple cases, you can<br>
use the MutableLiveData class.<br>
<br>
43<br>
00:01:45,600 --> 00:01:47,730<br>
If you update the value<br>
of the MutableLiveData<br>
<br>
44<br>
00:01:47,730 --> 00:01:50,230<br>
with a call to set value, it<br>
could then trigger and update<br>
<br>
45<br>
00:01:50,230 --> 00:01:51,570<br>
in your UI.<br>
<br>
46<br>
00:01:51,570 --> 00:01:53,170<br>
What's even more<br>
powerful though,<br>
<br>
47<br>
00:01:53,170 --> 00:01:55,680<br>
is that Room is built<br>
to support LiveData.<br>
<br>
48<br>
00:01:55,680 --> 00:01:58,080<br>
To use them together,<br>
you just modify your DAO<br>
<br>
49<br>
00:01:58,080 --> 00:02:00,450<br>
to return objects that are<br>
wrapped with the LiveData<br>
<br>
50<br>
00:02:00,450 --> 00:02:01,360<br>
class.<br>
<br>
51<br>
00:02:01,360 --> 00:02:04,850<br>
Room will create a LiveData<br>
object observing the database.<br>
<br>
52<br>
00:02:04,850 --> 00:02:08,258<br>
Then you could write code<br>
like this to update your UI.<br>
<br>
53<br>
00:02:08,258 --> 00:02:10,959<br>
The end result is that if<br>
your Room database updates,<br>
<br>
54<br>
00:02:10,960 --> 00:02:13,410<br>
it changes the data in<br>
your LiveData object, which<br>
<br>
55<br>
00:02:13,410 --> 00:02:15,930<br>
automatically<br>
triggers UI updates.<br>
<br>
56<br>
00:02:15,930 --> 00:02:18,840<br>
This brings me to another<br>
awesome feature of LiveData.<br>
<br>
57<br>
00:02:18,840 --> 00:02:21,344<br>
LiveData is a<br>
lifecycle-aware component.<br>
<br>
58<br>
00:02:21,344 --> 00:02:23,010<br>
Now, you might be<br>
thinking, what exactly<br>
<br>
59<br>
00:02:23,010 --> 00:02:24,990<br>
is a lifecycle-aware component?<br>
<br>
60<br>
00:02:24,990 --> 00:02:26,390<br>
Well, I'm glad you asked.<br>
<br>
61<br>
00:02:26,390 --> 00:02:28,620<br>
Through the magic of<br>
lifecycle observation,<br>
<br>
62<br>
00:02:28,620 --> 00:02:31,160<br>
LiveData knows when your<br>
activity is on screen,<br>
<br>
63<br>
00:02:31,160 --> 00:02:34,200<br>
off screen, or destroyed, so<br>
that it doesn't send database<br>
<br>
64<br>
00:02:34,200 --> 00:02:36,600<br>
updates to a non-active UI.<br>
<br>
65<br>
00:02:36,600 --> 00:02:38,520<br>
There are two<br>
interfaces for this--<br>
<br>
66<br>
00:02:38,520 --> 00:02:41,070<br>
Lifecycle Owner and<br>
Lifecycle Observer.<br>
<br>
67<br>
00:02:41,070 --> 00:02:43,200<br>
Lifecycle Owners are<br>
objects with lifecycles,<br>
<br>
68<br>
00:02:43,200 --> 00:02:44,820<br>
like activities and fragments.<br>
<br>
69<br>
00:02:44,820 --> 00:02:46,620<br>
Lifecycle Observers,<br>
on the other hand,<br>
<br>
70<br>
00:02:46,620 --> 00:02:50,509<br>
observe Lifecycle Owners and are<br>
notified of lifecycle changes.<br>
<br>
71<br>
00:02:50,509 --> 00:02:52,050<br>
Here's a quick peek<br>
at the simplified<br>
<br>
72<br>
00:02:52,050 --> 00:02:55,770<br>
code for LiveData, which is<br>
also a Lifecycle Observer.<br>
<br>
73<br>
00:02:55,770 --> 00:02:58,890<br>
The methods annotated<br>
with @OnLifecycleEvent<br>
<br>
74<br>
00:02:58,890 --> 00:03:00,970<br>
take care of initialization<br>
and tear down<br>
<br>
75<br>
00:03:00,970 --> 00:03:04,350<br>
when the associated Lifecycle<br>
Owner starts and stops.<br>
<br>
76<br>
00:03:04,350 --> 00:03:07,530<br>
This allows LiveData objects<br>
to take care of their own setup<br>
<br>
77<br>
00:03:07,530 --> 00:03:09,690<br>
and tear down, so<br>
the UI components<br>
<br>
78<br>
00:03:09,690 --> 00:03:12,000<br>
observe the LiveData, and<br>
the LiveData components<br>
<br>
79<br>
00:03:12,000 --> 00:03:13,890<br>
observe the Lifecycle Owners.<br>
<br>
80<br>
00:03:13,890 --> 00:03:16,380<br>
As a side note to all you<br>
Android library designers out<br>
<br>
81<br>
00:03:16,380 --> 00:03:19,350<br>
there, you can use this exact<br>
same lifecycle observation<br>
<br>
82<br>
00:03:19,350 --> 00:03:22,350<br>
code to call setup and tear<br>
down functions automatically<br>
<br>
83<br>
00:03:22,350 --> 00:03:24,240<br>
for your own libraries.<br>
<br>
84<br>
00:03:24,240 --> 00:03:26,559<br>
Now you still have one<br>
more problem to solve.<br>
<br>
85<br>
00:03:26,559 --> 00:03:29,100<br>
As your app is used, it will go<br>
through various configuration<br>
<br>
86<br>
00:03:29,100 --> 00:03:32,070<br>
changes that destroy and<br>
rebuild the activity.<br>
<br>
87<br>
00:03:32,070 --> 00:03:34,800<br>
We don't want to tie the<br>
initialization of LiveData<br>
<br>
88<br>
00:03:34,800 --> 00:03:36,660<br>
to the activity<br>
lifecycle because that<br>
<br>
89<br>
00:03:36,660 --> 00:03:39,830<br>
causes a lot of needlessly<br>
re-executed code.<br>
<br>
90<br>
00:03:39,830 --> 00:03:41,910<br>
An example of this is<br>
your database query,<br>
<br>
91<br>
00:03:41,910 --> 00:03:44,820<br>
which is executed every<br>
time you rotate the phone.<br>
<br>
92<br>
00:03:44,820 --> 00:03:46,300<br>
So what do you do?<br>
<br>
93<br>
00:03:46,300 --> 00:03:48,750<br>
Well, you put your<br>
LiveData and any other data<br>
<br>
94<br>
00:03:48,750 --> 00:03:52,230<br>
associated with the UI<br>
in a ViewModel instead.<br>
<br>
95<br>
00:03:52,230 --> 00:03:55,650<br>
ViewModels are objects that<br>
provide data for UI components<br>
<br>
96<br>
00:03:55,650 --> 00:03:57,750<br>
and survive<br>
configuration changes.<br>
<br>
97<br>
00:03:57,750 --> 00:04:01,500<br>
To create a ViewModel object,<br>
you extend the ViewModel class.<br>
<br>
98<br>
00:04:01,500 --> 00:04:03,450<br>
You then put all of<br>
the necessary data<br>
<br>
99<br>
00:04:03,450 --> 00:04:06,030<br>
for your activity UI<br>
into the ViewModel.<br>
<br>
100<br>
00:04:06,030 --> 00:04:08,850<br>
Since you've cached data for<br>
the UI inside of the ViewModel,<br>
<br>
101<br>
00:04:08,850 --> 00:04:10,590<br>
your app won't<br>
requery the database<br>
<br>
102<br>
00:04:10,590 --> 00:04:13,860<br>
if your activity is recreated<br>
due to a configuration change.<br>
<br>
103<br>
00:04:13,860 --> 00:04:16,140<br>
Then, when you're creating<br>
your activity or fragment,<br>
<br>
104<br>
00:04:16,140 --> 00:04:18,660<br>
you can get a reference to<br>
the ViewModel and use it.<br>
<br>
105<br>
00:04:18,660 --> 00:04:19,680<br>
And that's it!<br>
<br>
106<br>
00:04:19,680 --> 00:04:21,269<br>
The first time you<br>
get a ViewModel,<br>
<br>
107<br>
00:04:21,269 --> 00:04:23,160<br>
it's generated<br>
for your activity.<br>
<br>
108<br>
00:04:23,160 --> 00:04:24,840<br>
When you request<br>
a ViewModel again,<br>
<br>
109<br>
00:04:24,840 --> 00:04:27,000<br>
your activity receives<br>
the original ViewModel<br>
<br>
110<br>
00:04:27,000 --> 00:04:28,980<br>
with the UI data<br>
cache, so there's<br>
<br>
111<br>
00:04:28,980 --> 00:04:31,410<br>
no more useless database calls.<br>
<br>
112<br>
00:04:31,410 --> 00:04:34,290<br>
To summarize all of this<br>
new architecture shininess,<br>
<br>
113<br>
00:04:34,290 --> 00:04:37,140<br>
we've talked about Room,<br>
which is an object mapping<br>
<br>
114<br>
00:04:37,140 --> 00:04:40,350<br>
library for SQLite,<br>
LiveData, which notifies you<br>
<br>
115<br>
00:04:40,350 --> 00:04:43,080<br>
when its data changes so<br>
that you could update the UI,<br>
<br>
116<br>
00:04:43,080 --> 00:04:45,200<br>
and importantly, it<br>
works well with Room,<br>
<br>
117<br>
00:04:45,200 --> 00:04:47,070<br>
so that you can easily<br>
update the UI when<br>
<br>
118<br>
00:04:47,070 --> 00:04:48,820<br>
the database values change.<br>
<br>
119<br>
00:04:48,820 --> 00:04:51,480<br>
We've also talked about<br>
Lifecycle Observers and Owners,<br>
<br>
120<br>
00:04:51,480 --> 00:04:55,020<br>
which allow non-UI objects<br>
to observe lifecycle events.<br>
<br>
121<br>
00:04:55,020 --> 00:04:57,150<br>
And finally, we talked<br>
about ViewModels,<br>
<br>
122<br>
00:04:57,150 --> 00:04:58,770<br>
which provide you<br>
data objects that<br>
<br>
123<br>
00:04:58,770 --> 00:05:00,890<br>
survive configuration changes.<br>
<br>
124<br>
00:05:00,890 --> 00:05:03,710<br>
Altogether, they make up a<br>
set of architecture components<br>
<br>
125<br>
00:05:03,710 --> 00:05:07,190<br>
for writing modular, testable,<br>
and robust Android apps.<br>
<br>
126<br>
00:05:07,190 --> 00:05:08,660<br>
You can sensibly<br>
use them together,<br>
<br>
127<br>
00:05:08,660 --> 00:05:10,700<br>
or you can pick and<br>
choose what you need.<br>
<br>
128<br>
00:05:10,700 --> 00:05:12,530<br>
But this is just the<br>
tip of the iceberg.<br>
<br>
129<br>
00:05:12,530 --> 00:05:14,720<br>
In fact, a more<br>
fully-fledged Android app<br>
<br>
130<br>
00:05:14,720 --> 00:05:16,310<br>
might look like this.<br>
<br>
131<br>
00:05:16,310 --> 00:05:19,150<br>
For an in-depth look at how<br>
everything works together<br>
<br>
132<br>
00:05:19,150 --> 00:05:20,900<br>
and the reasoning<br>
behind these components,<br>
<br>
133<br>
00:05:20,900 --> 00:05:23,174<br>
check out the links in<br>
the description below.<br>
<br>
134<br>
00:05:23,174 --> 00:05:24,590<br>
To jump straight<br>
into code and get<br>
<br>
135<br>
00:05:24,590 --> 00:05:26,090<br>
started working<br>
with these objects,<br>
<br>
136<br>
00:05:26,090 --> 00:05:27,840<br>
you can check out the<br>
codelabs and samples<br>
<br>
137<br>
00:05:27,840 --> 00:05:29,500<br>
for lifecycle and persistence.<br>
<br>
138<br>
00:05:29,500 --> 00:05:32,180<br>
Happy building and, as always,<br>
don't forget to subscribe.<br>
<br>
139<br>
00:05:32,180 --> 00:05:34,330<br>
[MUSIC PLAYING]<br>
<br>
140<br>
00:05:34,330 --> 00:00:00,000<br>
<br>
<br>
    </td>
    <td>
1<br>
00:00:00,000 --> 00:00:02,130<br>
LYLA: В ответ на<br>
популярный запрос,<br>
<br>
2<br>
00:00:02,130 --> 00:00:05,010<br>
команда Android Framework<br>
написала свой гид<br>
<br>
3<br>
00:00:05,010 --> 00:00:06,960<br>
по архитектуре Android<br>
приложений, и они<br>
<br>
4<br>
00:00:06,960 --> 00:00:09,870<br>
разработали соответствующие<br>
архитектурные компоненты.<br>
<br>
5<br>
00:00:09,870 --> 00:00:12,960<br>
Hi, меня зовут Lyla, и я<br>
разработчик Android,<br>
<br>
6<br>
00:00:12,960 --> 00:00:15,900<br>
И я сейчас представлю для вас<br>
эти замечательные архитектурные<br>
<br>
7<br>
00:00:15,900 --> 00:00:17,070<br>
компоненты.<br>
<br>
8<br>
00:00:17,070 --> 00:00:19,890<br>
Эти компоненты хранят данные,<br>
управляют жизненным циклом,<br>
<br>
9<br>
00:00:19,890 --> 00:00:22,860<br>
делают ваше приложение модульным,<br>
помогают избежать утечек памяти,<br>
<br>
10<br>
00:00:22,860 --> 00:00:26,430<br>
И не заставляют вас использовать<br>
скучные шаблоны кода.<br>
<br>
11<br>
00:00:26,430 --> 00:00:28,680<br>
Основной части Android<br>
приложений нужна база данных<br>
<br>
12<br>
00:00:28,680 --> 00:00:30,780<br>
подключенная надежно к UI.<br>
<br>
13<br>
00:00:30,780 --> 00:00:33,890<br>
Новые компоненты: Room,<br>
ViewModel, LiveData,<br>
<br>
14<br>
00:00:33,890 --> 00:00:35,732<br>
и Lifecycle, делают это простым.<br>
<br>
15<br>
00:00:35,732 --> 00:00:38,190<br>
Они могут использоваться совместно,<br>
как строительные блоки,<br>
<br>
16<br>
00:00:38,190 --> 00:00:39,690<br>
давайте посмотрим каким образом.<br>
<br>
17<br>
00:00:39,690 --> 00:00:42,990<br>
Я собираюсь использовать базу данных<br>
Room, как новую SQLite<br>
<br>
18<br>
00:00:42,990 --> 00:00:44,820<br>
ORM библиотеку.<br>
<br>
19<br>
00:00:44,820 --> 00:00:46,440<br>
Чтобы настроить таблицы<br>
используя Room, мы<br>
<br>
20<br>
00:00:46,440 --> 00:00:49,550<br>
можем определить Старый Добрый<br>
Java Объект, или POJO.<br>
<br>
21<br>
00:00:49,550 --> 00:00:52,950<br>
Мы тогда помечаем этот POJO<br>
аннотацией @Entity<br>
<br>
22<br>
00:00:52,950 --> 00:00:56,650<br>
и создаем ID маркер с<br>
аннотацией @PrimaryKey.<br>
<br>
23<br>
00:00:56,650 --> 00:00:59,820<br>
Теперь для каждого POJO, мы должны<br>
определить DAO, или Database<br>
<br>
24<br>
00:00:59,820 --> 00:01:01,290<br>
Access Object.<br>
<br>
25<br>
00:01:01,290 --> 00:01:03,130<br>
Аннотированные методы <br>
представляют собой SQLite<br>
<br>
26<br>
00:01:03,130 --> 00:01:05,950<br>
команды, которые должны<br>
взаимодействовать с данными POJO .<br>
<br>
27<br>
00:01:05,950 --> 00:01:08,790<br>
Теперь взгляните на этот insert<br>
метод и на query метод.<br>
<br>
28<br>
00:01:08,790 --> 00:01:11,400<br>
Room автоматически конвертирует<br>
ваш POJO объект<br>
<br>
29<br>
00:01:11,400 --> 00:01:14,265<br>
в соответствующие таблицы<br>
базы данных и обратно.<br>
<br>
30<br>
00:01:14,265 --> 00:01:17,130<br>
Room также проверяет правильность<br>
вашего SQLite во время компиляции.<br>
<br>
31<br>
00:01:17,130 --> 00:01:19,150<br>
И если вы напишите что-то<br>
немного не так,<br>
<br>
32<br>
00:01:19,150 --> 00:01:21,150<br>
или ваша ссылка на столбец<br>
будет не актуальна а БД,<br>
<br>
33<br>
00:01:21,150 --> 00:01:24,310<br>
то выкинится полезная<br>
предупреждающая ошибка.<br>
<br>
34<br>
00:01:24,310 --> 00:01:26,070<br>
Теперь, когда у вас есть<br>
Room база данных,<br>
<br>
35<br>
00:01:26,070 --> 00:01:27,570<br>
вы можете использовать другие<br>
новые архитектурные компоненты<br>
<br>
36<br>
00:01:27,570 --> 00:01:30,210<br>
называемые LiveData,<br>
для мониторинга изменений<br>
<br>
37<br>
00:01:30,210 --> 00:01:31,320<br>
в базе данных.<br>
<br>
38<br>
00:01:31,320 --> 00:01:33,900<br>
LiveData это наблюдаемый<br>
[observable] держатель данных.<br>
<br>
39<br>
00:01:33,900 --> 00:01:35,910<br>
Это значит, что он хранит<br>
данные и оповещает вас<br>
<br>
40<br>
00:01:35,910 --> 00:01:39,090<br>
если данные изменились,<br>
и вы можете обновить UI.<br>
<br>
41<br>
00:01:39,090 --> 00:01:41,790<br>
LiveData это абстрактный класс<br>
который вы можете расширить,<br>
<br>
42<br>
00:01:41,790 --> 00:01:45,600<br>
или, для простых случаев, вы можете<br>
использовать MutableLiveData класс.<br>
<br>
43<br>
00:01:45,600 --> 00:01:47,730<br>
Если вы обновляете данные<br>
в MutableLiveData<br>
<br>
44<br>
00:01:47,730 --> 00:01:50,230<br>
с установлением нового значения,<br>
это может обновить и изменить<br>
<br>
45<br>
00:01:50,230 --> 00:01:51,570<br>
ваш UI.<br>
<br>
46<br>
00:01:51,570 --> 00:01:53,170<br>
Что еще более мощно,<br>
так это то, что<br>
<br>
47<br>
00:01:53,170 --> 00:01:55,680<br>
Room построена на<br>
поддержке LiveData.<br>
<br>
48<br>
00:01:55,680 --> 00:01:58,080<br>
Чтобы использовать их вместе,<br>
вы просто изменяете DAO<br>
<br>
49<br>
00:01:58,080 --> 00:02:00,450<br>
так чтобы возвращать объекты<br>
завернутые в LiveData<br>
<br>
50<br>
00:02:00,450 --> 00:02:01,360<br>
класс.<br>
<br>
51<br>
00:02:01,360 --> 00:02:04,850<br>
Room создаст объект LiveData<br>
наблюдающий базу данных.<br>
<br>
52<br>
00:02:04,850 --> 00:02:08,258<br>
Тогда вы могли бы писать код<br>
для обновления вашего UI.<br>
<br>
53<br>
00:02:08,258 --> 00:02:10,959<br>
В конечном счете если вы <br>
обновляете вашу Room БД,<br>
<br>
54<br>
00:02:10,960 --> 00:02:13,410<br>
эти изменения изменят данные<br>
вашего LiveData объекта,<br>
<br>
55<br>
00:02:13,410 --> 00:02:15,930<br>
который автоматически<br>
включит обновление UI.<br>
<br>
56<br>
00:02:15,930 --> 00:02:18,840<br>
Это подводит меня к другой<br>
удивительной особенности LiveData.<br>
<br>
57<br>
00:02:18,840 --> 00:02:21,344<br>
LiveData осведомлен о<br>
жизненном цикле.<br>
<br>
58<br>
00:02:21,344 --> 00:02:23,010<br>
Теперь вы можете подумать,<br>
что именно представляет собой<br>
<br>
59<br>
00:02:23,010 --> 00:02:24,990<br>
осведомленный о жизненном<br>
цикле компонент?<br>
<br>
60<br>
00:02:24,990 --> 00:02:26,390<br>
Хорошо, я рада, что вы спросили.<br>
<br>
61<br>
00:02:26,390 --> 00:02:28,620<br>
Через магическое наблюдение<br>
за жизненным циклом,<br>
<br>
62<br>
00:02:28,620 --> 00:02:31,160<br>
LiveData знает когда ваша<br>
активити на экране,<br>
<br>
63<br>
00:02:31,160 --> 00:02:34,200<br>
спит, или разрушена, итак<br>
база данных не отправляет<br>
<br>
64<br>
00:02:34,200 --> 00:02:36,600<br>
обнавления неактивному UI.<br>
<br>
65<br>
00:02:36,600 --> 00:02:38,520<br>
Есть два интерфейса<br>
для этого -<br>
<br>
66<br>
00:02:38,520 --> 00:02:41,070<br>
Lifecycle Owner и<br>
Lifecycle Observer.<br>
<br>
67<br>
00:02:41,070 --> 00:02:43,200<br>
Lifecycle Owners это<br>
объекты с жизненным циклом<br>
<br>
68<br>
00:02:43,200 --> 00:02:44,820<br>
подобным таковым у<br>
Activity и Fragment.<br>
<br>
69<br>
00:02:44,820 --> 00:02:46,620<br>
Lifecycle Observers,<br>
с другой стороны, наблюдают<br>
<br>
70<br>
00:02:46,620 --> 00:02:50,509<br>
Lifecycle Owners и уведомляются<br>
об изменниях жизненного цикла.<br>
<br>
71<br>
00:02:50,509 --> 00:02:52,050<br>
Вот упрощенный взгляд на<br>
простой пример кода<br>
<br>
72<br>
00:02:52,050 --> 00:02:55,770<br>
для LiveData, который есть<br>
также Lifecycle Observer.<br>
<br>
73<br>
00:02:55,770 --> 00:02:58,890<br>
Эти методы аннотируются<br>
с @OnLifecycleEvent<br>
<br>
74<br>
00:02:58,890 --> 00:03:00,970<br>
для заботы об инициализации<br>
и остановке, когда<br>
<br>
75<br>
00:03:00,970 --> 00:03:04,350<br>
связанный Lifecycle Owner<br>
стартует и останавливается.<br>
<br>
76<br>
00:03:04,350 --> 00:03:07,530<br>
это позволяет объектам LiveData<br>
заботится о своей настройке и<br>
<br>
77<br>
00:03:07,530 --> 00:03:09,690<br>
остановке, поэтому<br>
UI компоненты наблюдают<br>
<br>
78<br>
00:03:09,690 --> 00:03:12,000<br>
LiveData, и <br>
LiveData компоненты<br>
<br>
79<br>
00:03:12,000 --> 00:03:13,890<br>
наблюдатели Lifecycle Owners.<br>
<br>
80<br>
00:03:13,890 --> 00:03:16,380<br>
В качестве заметки для всех вас,<br>
разработчики библиотек Android,<br>
<br>
81<br>
00:03:16,380 --> 00:03:19,350<br>
вы можете использовать такое же<br>
наблюдение за жизненным циклом<br>
<br>
82<br>
00:03:19,350 --> 00:03:22,350<br>
для ваших функций настроек и<br>
завершения работы, для ваших<br>
<br>
83<br>
00:03:22,350 --> 00:03:24,240<br>
собственных библиотек.<br>
<br>
84<br>
00:03:24,240 --> 00:03:26,559<br>
Теперь, у вас есть еще одна<br>
проблема для решения.<br>
<br>
85<br>
00:03:26,559 --> 00:03:29,100<br>
Поскольку ваше приложение используется<br>
оно будет в разных состояниях<br>
<br>
86<br>
00:03:29,100 --> 00:03:32,070<br>
в onDestroy и onResume,<br>
onStart и onStop.<br>
<br>
87<br>
00:03:32,070 --> 00:03:34,800<br>
Мы не хотим привязывать<br>
LiveData к жизненному циклу<br>
<br>
88<br>
00:03:34,800 --> 00:03:36,660<br>
Activity, потому что это<br>
вызывает много<br>
<br>
89<br>
00:03:36,660 --> 00:03:39,830<br>
случаев не необходимого<br>
переиспользования кода.<br>
<br>
90<br>
00:03:39,830 --> 00:03:41,910<br>
Примером этого является ваш<br>
запрос к базе данных,<br>
<br>
91<br>
00:03:41,910 --> 00:03:44,820<br>
каждый раз когда вы<br>
поворачиваете телефон.<br>
<br>
92<br>
00:03:44,820 --> 00:03:46,300<br>
Итак, что же вам делать?<br>
<br>
93<br>
00:03:46,300 --> 00:03:48,750<br>
Хорошо, вы кладете ваш<br>
LiveData и другие данные<br>
<br>
94<br>
00:03:48,750 --> 00:03:52,230<br>
ассоциированные с UI<br>
во ViewModel.<br>
<br>
95<br>
00:03:52,230 --> 00:03:55,650<br>
ViewModels это объекты, которые<br>
доставляют данные для UI компонентов<br>
<br>
96<br>
00:03:55,650 --> 00:03:57,750<br>
и не зависят от изменений<br>
конфигураций устройства.<br>
<br>
97<br>
00:03:57,750 --> 00:04:01,500<br>
для создания объекта ViewModel,<br>
вы наследуетесь от класса ViewModel.<br>
<br>
98<br>
00:04:01,500 --> 00:04:03,450<br>
Вы кладете все<br>
необходимые данные<br>
<br>
99<br>
00:04:03,450 --> 00:04:06,030<br>
для UI вашего Activity<br>
во ViewModel.<br>
<br>
100<br>
00:04:06,030 --> 00:04:08,850<br>
И с тех пор как вы храните<br>
ваши UI-данные во ViewModel,<br>
<br>
101<br>
00:04:08,850 --> 00:04:10,590<br>
ваше приложение не будет<br>
запрашивать базу данных<br>
<br>
102<br>
00:04:10,590 --> 00:04:13,860<br>A
если ваша Activity пересоздана<br>
или изменилась конфигурация.<br>
<br>
103<br>
00:04:13,860 --> 00:04:16,140<br>
Затем, когда вы создаете ваши<br>
Activity или Fragment,<br>
<br>
104<br>
00:04:16,140 --> 00:04:18,660<br>
вы можете получить ссылку<br>
на ViewModel и использовать его.<br>
<br>
105<br>
00:04:18,660 --> 00:04:19,680<br>
Вот и все!<br>
<br>
106<br>
00:04:19,680 --> 00:04:21,269<br>
Когда вы впервые<br>
получаете ViewModel,<br>
<br>
107<br>
00:04:21,269 --> 00:04:23,160<br>
он создается для<br>
вашей Activity.<br>
<br>
108<br>
00:04:23,160 --> 00:04:24,840<br>
Когда вы снова<br>
запрашиваете ViewModel,<br>
<br>
109<br>
00:04:24,840 --> 00:04:27,000<br>
ваша Activity получает<br>
оригинальную ViewModel<br>
<br>
110<br>
00:04:27,000 --> 00:04:28,980<br>
с данными для UI из кеша,<br>
так что никаких бесполезных<br>
<br>
111<br>
00:04:28,980 --> 00:04:31,410<br>
запросов к базе данных.<br>
<br>
112<br>
00:04:31,410 --> 00:04:34,290<br>
Подводя всему итог:<br>
новая архитектура блестяща,<br>
<br>
113<br>
00:04:34,290 --> 00:04:37,140<br>
мы поговорили о Room,<br>
которая является object mapping<br>
<br>
114<br>
00:04:37,140 --> 00:04:40,350<br>
library для SQLite,<br>
LiveData, который предупреждает вас<br>
<br>
115<br>
00:04:40,350 --> 00:04:43,080<br>
если данные изменились, и вы<br>
можете обновить ваш IU,<br>
<br>
116<br>
00:04:43,080 --> 00:04:45,200<br>
и, что важно, он<br>
хорошо работает с Room,<br>
<br>
117<br>
00:04:45,200 --> 00:04:47,070<br>
так что вы легко сможете<br>
обноовить ваш UI, когда<br>
<br>
118<br>
00:04:47,070 --> 00:04:48,820<br>
данные из базы изменились.<br>
<br>
119<br>
00:04:48,820 --> 00:04:51,480<br>
Мы также поговорили о<br>
Lifecycle Observers и Owners,<br>
<br>
120<br>
00:04:51,480 --> 00:04:55,020<br>
которые позволяют не-UI объектам<br>
наблюдать за событиями жизненного цикла.<br>
<br>
121<br>
00:04:55,020 --> 00:04:57,150<br>
И наконец, мы поговорили<br>
о ViewModels, которые<br>
<br>
122<br>
00:04:57,150 --> 00:04:58,770<br>
предоставляют вам<br>
объекты с данными, которые<br>
<br>
123<br>
00:04:58,770 --> 00:05:00,890<br>
сохраняются при изменениях конфигураций.<br>
<br>
124<br>
00:05:00,890 --> 00:05:03,710<br>
В целом они составляют набор<br>
архитектурных компонентов<br>
<br>
125<br>
00:05:03,710 --> 00:05:07,190<br>
для написания модульных, тестируемых,<br>
и надежных Android-приложений.<br>
<br>
126<br>
00:05:07,190 --> 00:05:08,660<br>
Вы можете, где необходимо,<br>
использовать их вместе,<br>
<br>
127<br>
00:05:08,660 --> 00:05:10,700<br>
или использовать только то,<br>
что вам нужно.<br>
<br>
128<br>
00:05:10,700 --> 00:05:12,530<br>
Но это только<br>
верхушка айзберга.<br>
<br>
129<br>
00:05:12,530 --> 00:05:14,720<br>
Фактически, более функциональное<br>
Android-приложение<br>
<br>
130<br>
00:05:14,720 --> 00:05:16,310<br>
может выглядеть так.<br>
<br>
131<br>
00:05:16,310 --> 00:05:19,150<br>
Для детального изучения, как<br>
все работает вместе,<br>
<br>
132<br>
00:05:19,150 --> 00:05:20,900<br>
и для понимания этих<br>
компонентов, ознакомтесь<br>
<br>
133<br>
00:05:20,900 --> 00:05:23,174<br>
со ссылками под<br>
этим видео.<br>
<br>
134<br>
00:05:23,174 --> 00:05:24,590<br>
Чтобы перейти прямо к<br>
коду и начать работу<br>
<br>
135<br>
00:05:24,590 --> 00:05:26,090<br>
с этими компонентами,<br>
вы можете перейти,<br>
<br>
136<br>
00:05:26,090 --> 00:05:27,840<br>
к codelabs и примерам<br>
для жизненного цикла<br>
<br>
137<br>
00:05:27,840 --> 00:05:29,500<br>
и поддержки сохранности данных.<br>
<br>
138<br>
00:05:29,500 --> 00:05:32,180<br>
Хорошего проектирования, и как всегда,<br>
не забывайте подписываться.<br>
<br>
139<br>
00:05:32,180 --> 00:05:34,330<br>
[ИГРАЕТ МУЗЫКА]<br>
<br>
140<br>
00:05:34,330 --> 00:00:00,000<br>
<br>
<br>
    </td>
  </tr> 
</table>
