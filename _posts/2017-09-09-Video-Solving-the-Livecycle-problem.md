---
layout: post
title: Видео. Architecture Components. Solving the Lifecycle Problem. Перевод субтитров.
date: 2017-09-09 20:42
tags:
- Java
- Android
- архитектура
- video
- youtube
- translate
- Architecture Components
- философия
---
*Перевод английских субтитров на русские из видео Architecture Components: Solving the Lifecycle Problem. Начало 09.09.2017, конец - .09.2017. All rights reserved.*

Смотри другие переводы видео (субтитры) по этой теме: <a href="https://ziginsider.github.io/tags/#Architecture+Components">Tag: Architecture Components</a>

Мой клон с русскими `субтитрами`:
<iframe width="560" height="315" src="https://www.youtube.com/embed/P_XPLT5ZwcE" frameborder="0" allowfullscreen></iframe>

Оригинальное видео:
<iframe width="560" height="315" src="https://www.youtube.com/embed/bEKNi1JOrNs" frameborder="0" allowfullscreen></iframe>

Аннотация к видео:
+ Handling Application & UI lifecycle on Android has always been a challenge for applications: subclassing, overriding, and entirely too much code in your Activity class leads to fragile, complicated application logic. Wouldn’t it be nice if this was easier? This session will cover a new approach to lifecycles and explore functionality that makes the problem dramatically easier. Be sure to also check out the other two “Architecture Components” sessions for more information on architecting better Android applications.

Перевод:
+ Управление жизненным циклом приложений и пользовательского интерфейса на Android всегда было проблемой для приложений: подклассы, переопределение и слишком много кода в классе Activity приводят к хрупкой, сложной логике приложений. Было бы неплохо, если бы это было проще? В этой сессии попробуем охватить новый подход к жизненным циклам и изучить функциональность, которая значительно упростит проблему. Обязательно ознакомьтесь с двумя другими разделами «Компоненты архитектуры» для получения дополнительной информации об архитектуре лучших приложений для Android.


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
  <tr><td>
  1<br>
00:00:00,000 --> 00:00:06,201<br>
[MUSIC PLAYING]<br>
<br>
2<br>
00:00:06,201 --> 00:00:09,380<br>
SERGEI VASILINETC:<br>
Good morning, everyone.<br>
<br>
3<br>
00:00:09,380 --> 00:00:10,130<br>
My name is Sergei.<br>
<br>
4<br>
00:00:10,130 --> 00:00:12,620<br>
This is Adam and<br>
Yigit with me today,<br>
<br>
5<br>
00:00:12,620 --> 00:00:15,780<br>
and we will speak about<br>
LifeCycle problems.<br>
<br>
6<br>
00:00:15,780 --> 00:00:21,240<br>
So probably many of you attended<br>
yesterday at Yigit's talk<br>
<br>
7<br>
00:00:21,240 --> 00:00:24,670<br>
where he introduced new<br>
architecture components.<br>
<br>
8<br>
00:00:24,670 --> 00:00:27,550<br>
He introduced LiveData,<br>
ViewModel, new persistence<br>
<br>
9<br>
00:00:27,550 --> 00:00:28,540<br>
slide named Room.<br>
<br>
10<br>
00:00:28,540 --> 00:00:31,900<br>
And today we will focus<br>
on the LifeCycle part<br>
<br>
11<br>
00:00:31,900 --> 00:00:34,990<br>
of these architectural<br>
components.<br>
<br>
12<br>
00:00:34,990 --> 00:00:37,715<br>
So we will speak again about<br>
LiveData And ViewModel.<br>
<br>
13<br>
00:00:37,715 --> 00:00:41,140<br>
We will speak about LifeCycle<br>
honors and LifeCycle that<br>
<br>
14<br>
00:00:41,140 --> 00:00:45,210<br>
are basics for these libraries.<br>
<br>
15<br>
00:00:45,210 --> 00:00:49,150<br>
But we will have more details.<br>
<br>
16<br>
00:00:49,150 --> 00:00:51,890<br>
We will have some reasoning<br>
behind our decisions.<br>
<br>
17<br>
00:00:51,890 --> 00:00:56,360<br>
So if you attended yesterday,<br>
it will be still interesting.<br>
<br>
18<br>
00:00:56,360 --> 00:00:57,900<br>
If you didn't<br>
attend yesterday, we<br>
<br>
19<br>
00:00:57,900 --> 00:00:59,600<br>
will reintroduce<br>
all of these things<br>
<br>
20<br>
00:00:59,600 --> 00:01:03,370<br>
so you will<br>
understand everything.<br>
<br>
21<br>
00:01:03,370 --> 00:01:07,480<br>
So let's see what we have today.<br>
<br>
22<br>
00:01:07,480 --> 00:01:11,280<br>
Today we have an activity<br>
in the fragments.<br>
<br>
23<br>
00:01:11,280 --> 00:01:14,300<br>
I'll start with is that not<br>
for length length but dozens<br>
<br>
24<br>
00:01:14,300 --> 00:01:17,330<br>
and dozens line of lines.<br>
<br>
25<br>
00:01:17,330 --> 00:01:22,190<br>
And this line's the results<br>
from a very natural process.<br>
<br>
26<br>
00:01:22,190 --> 00:01:24,690<br>
Google pay services<br>
asked to register them<br>
<br>
27<br>
00:01:24,690 --> 00:01:25,670<br>
in onStart methods.<br>
<br>
28<br>
00:01:25,670 --> 00:01:29,620<br>
It's Your own components need<br>
to know about this LifeCycle<br>
<br>
29<br>
00:01:29,620 --> 00:01:34,640<br>
event, so you need to forward<br>
them in some kind of API.<br>
<br>
30<br>
00:01:34,640 --> 00:01:38,100<br>
And correspondingly,<br>
on onStop method,<br>
<br>
31<br>
00:01:38,100 --> 00:01:42,530<br>
you have to call all<br>
pairings stop methods,<br>
<br>
32<br>
00:01:42,530 --> 00:01:44,900<br>
and it's very easy<br>
to forget one.<br>
<br>
33<br>
00:01:44,900 --> 00:01:46,880<br>
And will result in [INAUDIBLE].<br>
<br>
34<br>
00:01:46,880 --> 00:01:51,950<br>
It will drain the<br>
user's battery,<br>
<br>
35<br>
00:01:51,950 --> 00:01:54,920<br>
and they will enjoy<br>
your app a bit less.<br>
<br>
36<br>
00:01:54,920 --> 00:01:58,190<br>
Which is probably healthier for<br>
them, but we think that's bad.<br>
<br>
37<br>
00:01:58,190 --> 00:02:02,180<br>
And they think the<br>
answer in this situation<br>
<br>
38<br>
00:02:02,180 --> 00:02:04,130<br>
is to introduce LifeCycle<br>
aware components.<br>
<br>
39<br>
00:02:04,130 --> 00:02:06,770<br>
So components which<br>
handle LifeCycle.<br>
<br>
40<br>
00:02:06,770 --> 00:02:08,538<br>
And the first step<br>
in this direction<br>
<br>
41<br>
00:02:08,538 --> 00:02:11,750<br>
is to introduce LifeCycle<br>
as a first class citizen.<br>
<br>
42<br>
00:02:11,750 --> 00:02:13,550<br>
So it's a very<br>
simple object which<br>
<br>
43<br>
00:02:13,550 --> 00:02:17,370<br>
answers the question, what is<br>
the current state right now?<br>
<br>
44<br>
00:02:17,370 --> 00:02:19,130<br>
And notifies you<br>
about new events.<br>
<br>
45<br>
00:02:19,130 --> 00:02:22,340<br>
And then no feature is important<br>
but sounds ridiculous right<br>
<br>
46<br>
00:02:22,340 --> 00:02:26,060<br>
now, events and states<br>
are different things.<br>
<br>
47<br>
00:02:26,060 --> 00:02:28,540<br>
So let's see what I mean.<br>
<br>
48<br>
00:02:28,540 --> 00:02:31,610<br>
Your case is instantiated<br>
in initialized state.<br>
<br>
49<br>
00:02:31,610 --> 00:02:37,965<br>
And all creation phases<br>
pass very routinely.<br>
<br>
50<br>
00:02:37,965 --> 00:02:39,680<br>
OnCreate, create the state.<br>
<br>
51<br>
00:02:39,680 --> 00:02:42,460<br>
OnStart, start the state,<br>
same thing for resume.<br>
<br>
52<br>
00:02:42,460 --> 00:02:45,070<br>
But the road down is a<br>
bit more interesting.<br>
<br>
53<br>
00:02:45,070 --> 00:02:48,920<br>
So onPause event, leads<br>
you from a resume state<br>
<br>
54<br>
00:02:48,920 --> 00:02:50,480<br>
back to a starting state.<br>
<br>
55<br>
00:02:50,480 --> 00:02:53,490<br>
Not some new pause state,<br>
or something like that.<br>
<br>
56<br>
00:02:53,490 --> 00:02:57,870<br>
And the reason for this is<br>
from a system perspective,<br>
<br>
57<br>
00:02:57,870 --> 00:03:01,880<br>
the states after onPause event<br>
and onStart event are the same<br>
<br>
58<br>
00:03:01,880 --> 00:03:05,790<br>
because the sets of the actions<br>
that you are allowed to do<br>
<br>
59<br>
00:03:05,790 --> 00:03:07,010<br>
is the same.<br>
<br>
60<br>
00:03:07,010 --> 00:03:11,960<br>
And the same is true for<br>
onStop and Creative state.<br>
<br>
61<br>
00:03:11,960 --> 00:03:14,350<br>
And last event is onDestroy.<br>
<br>
62<br>
00:03:14,350 --> 00:03:18,390<br>
It's pretty straightforward.<br>
<br>
63<br>
00:03:18,390 --> 00:03:20,150<br>
It brings it to destroy state.<br>
<br>
64<br>
00:03:20,150 --> 00:03:21,730<br>
Your activity is destroyed.<br>
<br>
65<br>
00:03:21,730 --> 00:03:25,720<br>
It's going to be thrown<br>
away and garbage collected.<br>
<br>
66<br>
00:03:25,720 --> 00:03:28,020<br>
So let's make our<br>
component LifeCycle aware.<br>
<br>
67<br>
00:03:28,020 --> 00:03:29,390<br>
That's super straightforward.<br>
<br>
68<br>
00:03:29,390 --> 00:03:32,780<br>
We take it with LifeCycle<br>
observer interface,<br>
<br>
69<br>
00:03:32,780 --> 00:03:34,350<br>
accepted interface.<br>
<br>
70<br>
00:03:34,350 --> 00:03:40,320<br>
To get the actual events, we add<br>
annotation and pass the events<br>
<br>
71<br>
00:03:40,320 --> 00:03:43,200<br>
that we are interested in,<br>
you can pass multiple events<br>
<br>
72<br>
00:03:43,200 --> 00:03:43,950<br>
if you want to.<br>
<br>
73<br>
00:03:43,950 --> 00:03:48,180<br>
The last step is to add<br>
ourselves as an observer.<br>
<br>
74<br>
00:03:48,180 --> 00:03:53,910<br>
And we may have a<br>
potential problem here.<br>
<br>
75<br>
00:03:53,910 --> 00:03:57,810<br>
What if the activity is<br>
already started at this point?<br>
<br>
76<br>
00:03:57,810 --> 00:04:02,730<br>
Does this mean that we are<br>
going to receive onStop event,<br>
<br>
77<br>
00:04:02,730 --> 00:04:05,970<br>
and and we didn't<br>
receive onStart.<br>
<br>
78<br>
00:04:05,970 --> 00:04:09,540<br>
And our component probably<br>
is not ready for this.<br>
<br>
79<br>
00:04:09,540 --> 00:04:12,570<br>
But it took care<br>
of it, and we bring<br>
<br>
80<br>
00:04:12,570 --> 00:04:14,412<br>
the observer to correct state.<br>
<br>
81<br>
00:04:14,412 --> 00:04:15,370<br>
So what does this mean?<br>
<br>
82<br>
00:04:15,370 --> 00:04:17,670<br>
Let's take this example,<br>
which I just discussed.<br>
<br>
83<br>
00:04:17,670 --> 00:04:20,610<br>
From activity perspective<br>
onStart and onCreate<br>
<br>
84<br>
00:04:20,610 --> 00:04:26,250<br>
create already happened, and<br>
after that we add an observer.<br>
<br>
85<br>
00:04:26,250 --> 00:04:31,740<br>
But observer will still receive<br>
onCreate and onStart events<br>
<br>
86<br>
00:04:31,740 --> 00:04:34,950<br>
immediately when<br>
they were registered.<br>
<br>
87<br>
00:04:34,950 --> 00:04:38,130<br>
So let's take one step further.<br>
<br>
88<br>
00:04:38,130 --> 00:04:39,870<br>
OnResume, same situation.<br>
<br>
89<br>
00:04:39,870 --> 00:04:41,400<br>
Resume state will<br>
bring to resume<br>
<br>
90<br>
00:04:41,400 --> 00:04:45,550<br>
state we got an onResume<br>
event in addition to onCreate<br>
<br>
91<br>
00:04:45,550 --> 00:04:46,610<br>
and onStart.<br>
<br>
92<br>
00:04:46,610 --> 00:04:48,660<br>
A bit more<br>
interesting situation,<br>
<br>
93<br>
00:04:48,660 --> 00:04:54,590<br>
onPause In this situation, we<br>
are in a start state as well as<br>
<br>
94<br>
00:04:54,590 --> 00:04:55,830<br>
we learned.<br>
<br>
95<br>
00:04:55,830 --> 00:04:59,060<br>
So we bring the oberserver<br>
to the correct state<br>
<br>
96<br>
00:04:59,060 --> 00:05:00,030<br>
which is start.<br>
<br>
97<br>
00:05:00,030 --> 00:05:04,040<br>
So it's a similar situation<br>
as we had one minute ago.<br>
<br>
98<br>
00:05:04,040 --> 00:05:06,930<br>
Observer will receive<br>
onCreate and onStart events,<br>
<br>
99<br>
00:05:06,930 --> 00:05:09,090<br>
and that's it.<br>
<br>
100<br>
00:05:09,090 --> 00:05:13,460<br>
So we don't have a<br>
problem in this code.<br>
<br>
101<br>
00:05:13,460 --> 00:05:17,240<br>
So how to get this<br>
magical lifecycle object?<br>
<br>
102<br>
00:05:17,240 --> 00:05:20,940<br>
We have this interface<br>
which is super simple,<br>
<br>
103<br>
00:05:20,940 --> 00:05:25,060<br>
but this probably doesn't<br>
help much right now.<br>
<br>
104<br>
00:05:25,060 --> 00:05:26,580<br>
And the actual<br>
question is who are<br>
<br>
105<br>
00:05:26,580 --> 00:05:29,600<br>
LifeCycle owners out of box.<br>
<br>
106<br>
00:05:29,600 --> 00:05:34,310<br>
And the answer in this question<br>
is support library fragments<br>
<br>
107<br>
00:05:34,310 --> 00:05:35,630<br>
and support activities.<br>
<br>
108<br>
00:05:35,630 --> 00:05:40,140<br>
But unfortunately, this is<br>
true only in the bright future.<br>
<br>
109<br>
00:05:40,140 --> 00:05:44,300<br>
And right now we have<br>
LifeCycle activity<br>
<br>
110<br>
00:05:44,300 --> 00:05:46,040<br>
and LifeCycle fragment.<br>
<br>
111<br>
00:05:46,040 --> 00:05:49,520<br>
But at the point<br>
of 1.0 release, we<br>
<br>
112<br>
00:05:49,520 --> 00:05:53,720<br>
will merge our library to<br>
support libraries so you<br>
<br>
113<br>
00:05:53,720 --> 00:05:56,070<br>
don't have to use them later.<br>
<br>
114<br>
00:05:56,070 --> 00:05:59,400<br>
And now Adam will speak<br>
about some key differences<br>
<br>
115<br>
00:05:59,400 --> 00:06:02,242<br>
between fragment and<br>
LifeCyle observers<br>
<br>
116<br>
00:06:02,242 --> 00:06:04,200<br>
ADAM POWELL: So if you've<br>
been following along,<br>
<br>
117<br>
00:06:04,200 --> 00:06:06,616<br>
you probably recognize some<br>
similarities with the fragment<br>
<br>
118<br>
00:06:06,616 --> 00:06:07,950<br>
API in this as well.<br>
<br>
119<br>
00:06:07,950 --> 00:06:10,850<br>
So at this point we've got<br>
these two different components.<br>
<br>
120<br>
00:06:10,850 --> 00:06:12,480<br>
Which one do you use?<br>
<br>
121<br>
00:06:12,480 --> 00:06:14,870<br>
Well, as the slides are<br>
already spoiling for you,<br>
<br>
122<br>
00:06:14,870 --> 00:06:17,594<br>
this really isn't an<br>
either- or question.<br>
<br>
123<br>
00:06:17,594 --> 00:06:20,010<br>
One of these things doesn't<br>
necessarily replace the other.<br>
<br>
124<br>
00:06:20,010 --> 00:06:22,040<br>
And here's why.<br>
<br>
125<br>
00:06:22,040 --> 00:06:25,830<br>
Fragments, on one hand, that<br>
everybody knows and loves,<br>
<br>
126<br>
00:06:25,830 --> 00:06:28,190<br>
are statefully<br>
managed and recreated<br>
<br>
127<br>
00:06:28,190 --> 00:06:32,030<br>
after either a process death,<br>
an activity recreation,<br>
<br>
128<br>
00:06:32,030 --> 00:06:35,630<br>
or recreation of any hosts that<br>
you have the fragment within.<br>
<br>
129<br>
00:06:35,630 --> 00:06:37,760<br>
Fragments manage views<br>
and also interact<br>
<br>
130<br>
00:06:37,760 --> 00:06:39,620<br>
with the navigation<br>
stack, which are<br>
<br>
131<br>
00:06:39,620 --> 00:06:42,230<br>
things that are firmly out<br>
of scope of what LifeCycle<br>
<br>
132<br>
00:06:42,230 --> 00:06:43,880<br>
observers are meant to do.<br>
<br>
133<br>
00:06:43,880 --> 00:06:45,740<br>
Instead, LifeCycle<br>
observers are meant<br>
<br>
134<br>
00:06:45,740 --> 00:06:47,930<br>
to enable more granular<br>
factoring of your code,<br>
<br>
135<br>
00:06:47,930 --> 00:06:50,360<br>
whether you're in an<br>
activity or a fragment.<br>
<br>
136<br>
00:06:50,360 --> 00:06:51,110<br>
They're stateless.<br>
<br>
137<br>
00:06:51,110 --> 00:06:53,570<br>
So that means that they<br>
must be registered each time<br>
<br>
138<br>
00:06:53,570 --> 00:06:54,770<br>
the owner is recreated.<br>
<br>
139<br>
00:06:54,770 --> 00:06:56,186<br>
We're not going<br>
to try to recreate<br>
<br>
140<br>
00:06:56,186 --> 00:06:57,290<br>
these magically for you.<br>
<br>
141<br>
00:06:57,290 --> 00:06:59,150<br>
They don't have any<br>
concept of instant state<br>
<br>
142<br>
00:06:59,150 --> 00:07:00,780<br>
that they carry<br>
around with them.<br>
<br>
143<br>
00:07:00,780 --> 00:07:02,510<br>
So these are meant to be<br>
very, very lightweight,<br>
<br>
144<br>
00:07:02,510 --> 00:07:04,968<br>
so that you don't have a whole<br>
lot of additional management<br>
<br>
145<br>
00:07:04,968 --> 00:07:06,170<br>
overhead.<br>
<br>
146<br>
00:07:06,170 --> 00:07:09,470<br>
And last, there's no relation<br>
to the viewer navigation<br>
<br>
147<br>
00:07:09,470 --> 00:07:10,010<br>
management.<br>
<br>
148<br>
00:07:10,010 --> 00:07:12,470<br>
These really are meant<br>
to be very tightly<br>
<br>
149<br>
00:07:12,470 --> 00:07:16,330<br>
scoped, isolated components.<br>
<br>
150<br>
00:07:16,330 --> 00:07:17,950<br>
So they can really<br>
help everyone.<br>
<br>
151<br>
00:07:17,950 --> 00:07:21,040<br>
It means that it's much<br>
simpler to integrate libraries<br>
<br>
152<br>
00:07:21,040 --> 00:07:23,860<br>
with your code, as long as<br>
those libraries have provided<br>
<br>
153<br>
00:07:23,860 --> 00:07:26,124<br>
LifeCycle observer<br>
aware components.<br>
<br>
154<br>
00:07:26,124 --> 00:07:28,540<br>
It means that you can break<br>
up those really large fragment<br>
<br>
155<br>
00:07:28,540 --> 00:07:31,300<br>
or activity classes to make<br>
them much simpler to understand<br>
<br>
156<br>
00:07:31,300 --> 00:07:32,440<br>
for a reader.<br>
<br>
157<br>
00:07:32,440 --> 00:07:35,200<br>
And you can provide much<br>
more granular guarantees<br>
<br>
158<br>
00:07:35,200 --> 00:07:38,660<br>
around what operations are valid<br>
at any given point in time.<br>
<br>
159<br>
00:07:38,660 --> 00:07:41,860<br>
You can make it so that if<br>
an operation happens then<br>
<br>
160<br>
00:07:41,860 --> 00:07:44,050<br>
you're guaranteed to<br>
be in a correct state<br>
<br>
161<br>
00:07:44,050 --> 00:07:45,130<br>
when something is called.<br>
<br>
162<br>
00:07:45,130 --> 00:07:48,060<br>
<br>
<br>
163<br>
00:07:48,060 --> 00:07:50,685<br>
So LifeCycle owner<br>
as already introduced<br>
<br>
164<br>
00:07:50,685 --> 00:07:51,900<br>
is just an interface.<br>
<br>
165<br>
00:07:51,900 --> 00:07:53,630<br>
Anyone can implement this.<br>
<br>
166<br>
00:07:53,630 --> 00:07:55,680<br>
This means that you<br>
can improve testability<br>
<br>
167<br>
00:07:55,680 --> 00:07:56,802<br>
by creating your own.<br>
<br>
168<br>
00:07:56,802 --> 00:07:59,010<br>
You can create your own sort<br>
of fragment-like library<br>
<br>
169<br>
00:07:59,010 --> 00:08:01,170<br>
implementations if<br>
you feel so inclined.<br>
<br>
170<br>
00:08:01,170 --> 00:08:03,330<br>
But you can also create<br>
composite life cycles.<br>
<br>
171<br>
00:08:03,330 --> 00:08:06,780<br>
Life cycles that span across<br>
other smaller lifecycle<br>
<br>
172<br>
00:08:06,780 --> 00:08:08,010<br>
definitions.<br>
<br>
173<br>
00:08:08,010 --> 00:08:10,710<br>
So you can answer questions<br>
like, is my app visible?<br>
<br>
174<br>
00:08:10,710 --> 00:08:12,750<br>
So this is a really<br>
common composite lifecycle<br>
<br>
175<br>
00:08:12,750 --> 00:08:15,000<br>
that many of you may<br>
be interested in.<br>
<br>
176<br>
00:08:15,000 --> 00:08:17,160<br>
It lets you do things<br>
like session management<br>
<br>
177<br>
00:08:17,160 --> 00:08:19,530<br>
to track a particular<br>
session across perhaps<br>
<br>
178<br>
00:08:19,530 --> 00:08:23,100<br>
some sort of a flow<br>
or a series of logged<br>
<br>
179<br>
00:08:23,100 --> 00:08:24,870<br>
in versus logged out events.<br>
<br>
180<br>
00:08:24,870 --> 00:08:29,020<br>
And it may help you<br>
with analytics as well.<br>
<br>
181<br>
00:08:29,020 --> 00:08:32,280<br>
So we have the process LifeCycle<br>
owner as kind of a component<br>
<br>
182<br>
00:08:32,280 --> 00:08:35,350<br>
that I think a lot of you will<br>
be interested in for this.<br>
<br>
183<br>
00:08:35,350 --> 00:08:39,058<br>
It's the composite lifecycle of<br>
all the activities in your app.<br>
<br>
184<br>
00:08:39,058 --> 00:08:41,009<br>
So there's no configuration<br>
changes to handle,<br>
<br>
185<br>
00:08:41,010 --> 00:08:44,440<br>
because we're not going to be<br>
dealing with those from these.<br>
<br>
186<br>
00:08:44,440 --> 00:08:46,350<br>
The process LifeCycle<br>
owner just stays<br>
<br>
187<br>
00:08:46,350 --> 00:08:48,000<br>
alive through the whole process.<br>
<br>
188<br>
00:08:48,000 --> 00:08:50,041<br>
But that also means that<br>
you don't get state risk<br>
<br>
189<br>
00:08:50,041 --> 00:08:52,660<br>
restoration after process death<br>
like we mentioned earlier.<br>
<br>
190<br>
00:08:52,660 --> 00:08:54,600<br>
So that means that<br>
you don't have<br>
<br>
191<br>
00:08:54,600 --> 00:08:56,905<br>
to handle saving and<br>
restoring that state<br>
<br>
192<br>
00:08:56,905 --> 00:08:59,280<br>
but at the same time, you need<br>
to remember to re-register<br>
<br>
193<br>
00:08:59,280 --> 00:09:02,199<br>
these process lifecycle-based<br>
observers if that's something<br>
<br>
194<br>
00:09:02,199 --> 00:09:03,240<br>
that you're working with.<br>
<br>
195<br>
00:09:03,240 --> 00:09:05,750<br>
<br>
<br>
196<br>
00:09:05,750 --> 00:09:09,110<br>
So many indirect<br>
components provide a lot<br>
<br>
197<br>
00:09:09,110 --> 00:09:11,330<br>
of deep plumbing<br>
layers for things<br>
<br>
198<br>
00:09:11,330 --> 00:09:13,790<br>
that you can plug<br>
into and work with.<br>
<br>
199<br>
00:09:13,790 --> 00:09:15,800<br>
But a lot of times<br>
we've kind of omitted<br>
<br>
200<br>
00:09:15,800 --> 00:09:17,720<br>
the idea of higher<br>
level components that<br>
<br>
201<br>
00:09:17,720 --> 00:09:20,210<br>
make use of that plumbing<br>
so that you can just plug<br>
<br>
202<br>
00:09:20,210 --> 00:09:21,280<br>
play and go.<br>
<br>
203<br>
00:09:21,280 --> 00:09:24,300<br>
So do we have anything more<br>
high level than the bare events<br>
<br>
204<br>
00:09:24,300 --> 00:09:25,530<br>
and states here?<br>
<br>
205<br>
00:09:25,530 --> 00:09:26,800<br>
YIGIT BOYAR: Maybe we do.<br>
<br>
206<br>
00:09:26,800 --> 00:09:27,760<br>
I will show you.<br>
<br>
207<br>
00:09:27,760 --> 00:09:28,870<br>
ADAM POWELL: Great<br>
<br>
208<br>
00:09:28,870 --> 00:09:30,530<br>
YIGIT BOYAR: Thanks, Adam.<br>
<br>
209<br>
00:09:30,530 --> 00:09:33,680<br>
So it's so nice<br>
now you can observe<br>
<br>
210<br>
00:09:33,680 --> 00:09:37,310<br>
a LifeCycle is well-defined,<br>
is a first class citizen.<br>
<br>
211<br>
00:09:37,310 --> 00:09:40,530<br>
But you still need to<br>
deal with these things.<br>
<br>
212<br>
00:09:40,530 --> 00:09:44,780<br>
And we told like, there's<br>
some common LifeCycle problems<br>
<br>
213<br>
00:09:44,780 --> 00:09:47,100<br>
that we should be able to<br>
solve with this component.<br>
<br>
214<br>
00:09:47,100 --> 00:09:48,860<br>
So we'll look at the<br>
problems that people<br>
<br>
215<br>
00:09:48,860 --> 00:09:51,740<br>
are having, and<br>
this was probably<br>
<br>
216<br>
00:09:51,740 --> 00:09:54,110<br>
the most major problem<br>
we've been seeing,<br>
<br>
217<br>
00:09:54,110 --> 00:09:56,320<br>
the untimely UI updates.<br>
<br>
218<br>
00:09:56,320 --> 00:09:58,920<br>
It's like your activity<br>
receives a callback,<br>
<br>
219<br>
00:09:58,920 --> 00:10:00,530<br>
but the activity's<br>
already stopped.<br>
<br>
220<br>
00:10:00,530 --> 00:10:03,050<br>
They tried to start a<br>
new activity and crashes.<br>
<br>
221<br>
00:10:03,050 --> 00:10:06,010<br>
Or it tries to add a<br>
fragment and crashes.<br>
<br>
222<br>
00:10:06,010 --> 00:10:09,410<br>
If an activity or a<br>
fragment is stopped,<br>
<br>
223<br>
00:10:09,410 --> 00:10:12,317<br>
there is no reason to<br>
update that activity.<br>
<br>
224<br>
00:10:12,317 --> 00:10:13,400<br>
You don't want to do that.<br>
<br>
225<br>
00:10:13,400 --> 00:10:16,190<br>
If the activity happens to<br>
become visible again, then<br>
<br>
226<br>
00:10:16,190 --> 00:10:17,480<br>
you want to do it.<br>
<br>
227<br>
00:10:17,480 --> 00:10:20,480<br>
So we realized that this<br>
is a very common problem,<br>
<br>
228<br>
00:10:20,480 --> 00:10:23,990<br>
and we wanted to solve this with<br>
a higher level component which<br>
<br>
229<br>
00:10:23,990 --> 00:10:26,060<br>
we call LiveData.<br>
<br>
230<br>
00:10:26,060 --> 00:10:29,780<br>
When we look at the<br>
LiveData in detail,<br>
<br>
231<br>
00:10:29,780 --> 00:10:32,840<br>
it's actually an<br>
observable data holder.<br>
<br>
232<br>
00:10:32,840 --> 00:10:35,180<br>
It just holds on<br>
to some information<br>
<br>
233<br>
00:10:35,180 --> 00:10:36,490<br>
that you can observe.<br>
<br>
234<br>
00:10:36,490 --> 00:10:38,270<br>
Now the difference<br>
between LiveData<br>
<br>
235<br>
00:10:38,270 --> 00:10:41,225<br>
and your other observables<br>
in data mining or RxJava<br>
<br>
236<br>
00:10:41,225 --> 00:10:45,350<br>
or whatever, is that<br>
LiveData is LifeCycle aware.<br>
<br>
237<br>
00:10:45,350 --> 00:10:48,020<br>
It knows about<br>
Android life cycles,<br>
<br>
238<br>
00:10:48,020 --> 00:10:50,030<br>
and when you want to<br>
observe a LiveData,<br>
<br>
239<br>
00:10:50,030 --> 00:10:52,580<br>
you can pass in this<br>
LifeCycle so that it<br>
<br>
240<br>
00:10:52,580 --> 00:10:54,480<br>
can manage your subscription.<br>
<br>
241<br>
00:10:54,480 --> 00:10:57,210<br>
The nice thing about LiveData<br>
that is that you observe,<br>
<br>
242<br>
00:10:57,210 --> 00:10:59,340<br>
and that's all you do.<br>
<br>
243<br>
00:10:59,340 --> 00:11:00,860<br>
So if we look at<br>
the usage example,<br>
<br>
244<br>
00:11:00,860 --> 00:11:02,210<br>
let's say we have an activity.<br>
<br>
245<br>
00:11:02,210 --> 00:11:04,110<br>
We receive a LiveData<br>
from somewhere.<br>
<br>
246<br>
00:11:04,110 --> 00:11:08,040<br>
It doesn't really matter, and<br>
now we call observe on it.<br>
<br>
247<br>
00:11:08,040 --> 00:11:10,160<br>
And when we are<br>
calling observe, we<br>
<br>
248<br>
00:11:10,160 --> 00:11:13,600<br>
are passing this, which<br>
is the LiveData owner.<br>
<br>
249<br>
00:11:13,600 --> 00:11:14,780<br>
That's all you need to say.<br>
<br>
250<br>
00:11:14,780 --> 00:11:18,770<br>
I want to observe this<br>
LiveData within this LifeCycle.<br>
<br>
251<br>
00:11:18,770 --> 00:11:21,830<br>
Which also means if<br>
this LifeCycle is gone,<br>
<br>
252<br>
00:11:21,830 --> 00:11:23,150<br>
I don't want to observe it.<br>
<br>
253<br>
00:11:23,150 --> 00:11:26,550<br>
Or if this LifeCycle is stopped,<br>
I don't want to receive events.<br>
<br>
254<br>
00:11:26,550 --> 00:11:30,466<br>
<br>
<br>
255<br>
00:11:30,466 --> 00:11:32,340<br>
And then once you do<br>
this, that's all you do.<br>
<br>
256<br>
00:11:32,340 --> 00:11:34,410<br>
You don't need to<br>
write onStart, onStop.<br>
<br>
257<br>
00:11:34,410 --> 00:11:37,870<br>
We want Android to want<br>
to look more like this.<br>
<br>
258<br>
00:11:37,870 --> 00:11:40,040<br>
You initialze things as<br>
more like find and forget.<br>
<br>
259<br>
00:11:40,040 --> 00:11:43,060<br>
You initialize, and you're done.<br>
<br>
260<br>
00:11:43,060 --> 00:11:45,990<br>
So let's look at what happens<br>
when our activity starts<br>
<br>
261<br>
00:11:45,990 --> 00:11:47,910<br>
observing that LiveData.<br>
<br>
262<br>
00:11:47,910 --> 00:11:52,560<br>
So onCreate, it called observe,<br>
it said LiveData is observable.<br>
<br>
263<br>
00:11:52,560 --> 00:11:54,630<br>
And as soon as the<br>
activity starts,<br>
<br>
264<br>
00:11:54,630 --> 00:11:56,470<br>
it starts receiving<br>
data changes.<br>
<br>
265<br>
00:11:56,470 --> 00:11:59,490<br>
So whenever the<br>
LiveData value changes,<br>
<br>
266<br>
00:11:59,490 --> 00:12:01,950<br>
we displace that event<br>
back to your observer<br>
<br>
267<br>
00:12:01,950 --> 00:12:03,530<br>
inside the activity.<br>
<br>
268<br>
00:12:03,530 --> 00:12:05,450<br>
It can also be a fragment.<br>
<br>
269<br>
00:12:05,450 --> 00:12:07,260<br>
Let's say a user<br>
decides to rotate<br>
<br>
270<br>
00:12:07,260 --> 00:12:09,090<br>
the activity at this moment.<br>
<br>
271<br>
00:12:09,090 --> 00:12:11,540<br>
So you know that the<br>
activity will be stopped.<br>
<br>
272<br>
00:12:11,540 --> 00:12:13,320<br>
And what happens<br>
at the same time,<br>
<br>
273<br>
00:12:13,320 --> 00:12:16,110<br>
the LiveData happens<br>
to be updated.<br>
<br>
274<br>
00:12:16,110 --> 00:12:18,990<br>
If that happens, we are not<br>
going to tell the activity<br>
<br>
275<br>
00:12:18,990 --> 00:12:22,590<br>
about this change because there<br>
cannot be any reason for you<br>
<br>
276<br>
00:12:22,590 --> 00:12:27,210<br>
to update the UI, because<br>
it already stopped.<br>
<br>
277<br>
00:12:27,210 --> 00:12:29,640<br>
Similarly, if the<br>
activity is destroyed,<br>
<br>
278<br>
00:12:29,640 --> 00:12:31,980<br>
we will automatically<br>
remove that subscription<br>
<br>
279<br>
00:12:31,980 --> 00:12:34,320<br>
because that activity is gone.<br>
<br>
280<br>
00:12:34,320 --> 00:12:36,990<br>
There is no reason to<br>
keep a reference back<br>
<br>
281<br>
00:12:36,990 --> 00:12:39,240<br>
to that activity.<br>
<br>
282<br>
00:12:39,240 --> 00:12:41,010<br>
Now we said the<br>
activity was rotating,<br>
<br>
283<br>
00:12:41,010 --> 00:12:42,630<br>
so you know that<br>
Android is going<br>
<br>
284<br>
00:12:42,630 --> 00:12:44,880<br>
to recreate that activity.<br>
<br>
285<br>
00:12:44,880 --> 00:12:48,270<br>
And then we are observing<br>
the same LiveData back.<br>
<br>
286<br>
00:12:48,270 --> 00:12:49,985<br>
As soon as that<br>
activity starts, it's<br>
<br>
287<br>
00:12:49,985 --> 00:12:53,190<br>
going to receive<br>
last available data.<br>
<br>
288<br>
00:12:53,190 --> 00:12:57,720<br>
So your UI is going to have the<br>
data before it gets a chance<br>
<br>
289<br>
00:12:57,720 --> 00:12:59,790<br>
to draw.<br>
<br>
290<br>
00:12:59,790 --> 00:13:01,920<br>
So similarly, I<br>
say the user hits<br>
<br>
291<br>
00:13:01,920 --> 00:13:05,330<br>
the Home button, which means<br>
the activity will be stopped.<br>
<br>
292<br>
00:13:05,330 --> 00:13:08,700<br>
Again, if the LiveData changes<br>
while the activity is stopped,<br>
<br>
293<br>
00:13:08,700 --> 00:13:10,840<br>
it's not going to<br>
receive any events.<br>
<br>
294<br>
00:13:10,840 --> 00:13:14,010<br>
Even if the data changes,<br>
we are not going to tell it.<br>
<br>
295<br>
00:13:14,010 --> 00:13:17,280<br>
But as soon as if the user<br>
comes back to the application,<br>
<br>
296<br>
00:13:17,280 --> 00:13:19,510<br>
we will give it the<br>
last available data.<br>
<br>
297<br>
00:13:19,510 --> 00:13:22,990<br>
So this is why we call LiveData<br>
is not just a stream of events.<br>
<br>
298<br>
00:13:22,990 --> 00:13:26,910<br>
It holds onto the data so<br>
that if any observer comes,<br>
<br>
299<br>
00:13:26,910 --> 00:13:30,430<br>
it receives the last<br>
available value.<br>
<br>
300<br>
00:13:30,430 --> 00:13:33,620<br>
And then eventually, the user<br>
backs out of that activity,<br>
<br>
301<br>
00:13:33,620 --> 00:13:37,830<br>
and then we remove<br>
that subscription.<br>
<br>
302<br>
00:13:37,830 --> 00:13:40,730<br>
You can also extend<br>
the LiveData class.<br>
<br>
303<br>
00:13:40,730 --> 00:13:45,950<br>
Because LiveData provides<br>
two really handy callbacks.<br>
<br>
304<br>
00:13:45,950 --> 00:13:48,410<br>
The first one is called<br>
onactive which means<br>
<br>
305<br>
00:13:48,410 --> 00:13:50,930<br>
you have an active observer.<br>
<br>
306<br>
00:13:50,930 --> 00:13:52,580<br>
Another one is<br>
called oninactive,<br>
<br>
307<br>
00:13:52,580 --> 00:13:54,370<br>
which means you don't<br>
have any observers,<br>
<br>
308<br>
00:13:54,370 --> 00:13:56,450<br>
so don't bother<br>
changing your value<br>
<br>
309<br>
00:13:56,450 --> 00:14:00,020<br>
if it is something<br>
that you care about.<br>
<br>
310<br>
00:14:00,020 --> 00:14:03,800<br>
You probably ask now what<br>
is an active observer?<br>
<br>
311<br>
00:14:03,800 --> 00:14:06,220<br>
An active observer<br>
is an observer<br>
<br>
312<br>
00:14:06,220 --> 00:14:09,680<br>
whose attached LifeCycle<br>
is started or resumed.<br>
<br>
313<br>
00:14:09,680 --> 00:14:12,890<br>
So it's like a fragment that's<br>
currently visible to the user.<br>
<br>
314<br>
00:14:12,890 --> 00:14:15,380<br>
If the fragment is<br>
on the back stack,<br>
<br>
315<br>
00:14:15,380 --> 00:14:16,660<br>
the user is not seeing it.<br>
<br>
316<br>
00:14:16,660 --> 00:14:18,260<br>
It stopped, so it's not active.<br>
<br>
317<br>
00:14:18,260 --> 00:14:22,430<br>
There's no reason to do<br>
any work for that fragment.<br>
<br>
318<br>
00:14:22,430 --> 00:14:24,850<br>
Let's see how we can take<br>
advantage of these named<br>
<br>
319<br>
00:14:24,850 --> 00:14:25,770<br>
callbacks.<br>
<br>
320<br>
00:14:25,770 --> 00:14:28,270<br>
We are going to create<br>
a new location LiveData<br>
<br>
321<br>
00:14:28,270 --> 00:14:31,190<br>
class, which presents<br>
the location of something<br>
<br>
322<br>
00:14:31,190 --> 00:14:32,580<br>
on the device.<br>
<br>
323<br>
00:14:32,580 --> 00:14:37,920<br>
So we say this data holds<br>
an instance of a location.<br>
<br>
324<br>
00:14:37,920 --> 00:14:40,460<br>
In cross-sector, we just<br>
get the location manager<br>
<br>
325<br>
00:14:40,460 --> 00:14:41,850<br>
from the system service.<br>
<br>
326<br>
00:14:41,850 --> 00:14:43,670<br>
There's nothing fancy here.<br>
<br>
327<br>
00:14:43,670 --> 00:14:47,210<br>
We have a listener whenever<br>
the system server sends us<br>
<br>
328<br>
00:14:47,210 --> 00:14:50,830<br>
any location, we just<br>
call setValue on us.<br>
<br>
329<br>
00:14:50,830 --> 00:14:51,530<br>
This all you do.<br>
<br>
330<br>
00:14:51,530 --> 00:14:53,460<br>
There is no LifeCycle<br>
handling here.<br>
<br>
331<br>
00:14:53,460 --> 00:14:56,120<br>
You just call setValue,<br>
and LiveData takes<br>
<br>
332<br>
00:14:56,120 --> 00:14:57,710<br>
care of handling the LifeCycle.<br>
<br>
333<br>
00:14:57,710 --> 00:15:00,080<br>
And you may have any<br>
number of observers.<br>
<br>
334<br>
00:15:00,080 --> 00:15:02,450<br>
It doesn't really matter.<br>
<br>
335<br>
00:15:02,450 --> 00:15:04,850<br>
So we want to override onactive.<br>
<br>
336<br>
00:15:04,850 --> 00:15:07,340<br>
The very first active<br>
observer comes.<br>
<br>
337<br>
00:15:07,340 --> 00:15:10,280<br>
We want to start listening<br>
to the system service.<br>
<br>
338<br>
00:15:10,280 --> 00:15:14,300<br>
Similarly, when the last<br>
active observer goes away,<br>
<br>
339<br>
00:15:14,300 --> 00:15:19,140<br>
we want to stop observing<br>
the system service.<br>
<br>
340<br>
00:15:19,140 --> 00:15:21,800<br>
Now if you look at that<br>
location LiveData class<br>
<br>
341<br>
00:15:21,800 --> 00:15:24,020<br>
we just created in the<br>
previous example, let's look<br>
<br>
342<br>
00:15:24,020 --> 00:15:26,210<br>
at the properties of that class.<br>
<br>
343<br>
00:15:26,210 --> 00:15:28,100<br>
First of all, it<br>
is LifeCycle area.<br>
<br>
344<br>
00:15:28,100 --> 00:15:31,280<br>
It knows when to start<br>
itself, when to stop itself.<br>
<br>
345<br>
00:15:31,280 --> 00:15:34,340<br>
You just don't need<br>
to babysit it anymore.<br>
<br>
346<br>
00:15:34,340 --> 00:15:36,110<br>
It is self-sufficient.<br>
<br>
347<br>
00:15:36,110 --> 00:15:37,140<br>
You start it.<br>
<br>
348<br>
00:15:37,140 --> 00:15:39,480<br>
You forget about it.<br>
<br>
349<br>
00:15:39,480 --> 00:15:40,470<br>
It can be a singleton.<br>
<br>
350<br>
00:15:40,470 --> 00:15:42,620<br>
Like all of the subscriptions<br>
are automatically<br>
<br>
351<br>
00:15:42,620 --> 00:15:43,850<br>
managed for you.<br>
<br>
352<br>
00:15:43,850 --> 00:15:47,090<br>
So if the data is logically<br>
singleton your codebase,<br>
<br>
353<br>
00:15:47,090 --> 00:15:50,030<br>
you can make the LiveData<br>
instance singleton.<br>
<br>
354<br>
00:15:50,030 --> 00:15:51,710<br>
So there's this<br>
thing where normally<br>
<br>
355<br>
00:15:51,710 --> 00:15:54,800<br>
if you keep referencing<br>
an activity or a fragment<br>
<br>
356<br>
00:15:54,800 --> 00:15:57,720<br>
from a certain context,<br>
that will be a big no no.<br>
<br>
357<br>
00:15:57,720 --> 00:16:00,350<br>
But if you are using<br>
LiveData it is yes yes,<br>
<br>
358<br>
00:16:00,350 --> 00:16:05,340<br>
because we manage the<br>
substitution for you.<br>
<br>
359<br>
00:16:05,340 --> 00:16:08,550<br>
So you also don't need to<br>
subclass LiveData all the time.<br>
<br>
360<br>
00:16:08,550 --> 00:16:10,910<br>
So if you just need<br>
an instance of it<br>
<br>
361<br>
00:16:10,910 --> 00:16:12,790<br>
but you already<br>
have the value, you<br>
<br>
362<br>
00:16:12,790 --> 00:16:14,990<br>
could use this mutable<br>
LiveData class,<br>
<br>
363<br>
00:16:14,990 --> 00:16:18,770<br>
which comes inside the library<br>
that has a public setter.<br>
<br>
364<br>
00:16:18,770 --> 00:16:21,170<br>
But usually when you<br>
are using this class,<br>
<br>
365<br>
00:16:21,170 --> 00:16:24,530<br>
internally you will have<br>
it but the API you expose<br>
<br>
366<br>
00:16:24,530 --> 00:16:26,360<br>
will just return a<br>
LiveData, because you<br>
<br>
367<br>
00:16:26,360 --> 00:16:28,370<br>
don't want to expose<br>
the fact that anyone<br>
<br>
368<br>
00:16:28,370 --> 00:16:31,470<br>
can set the value on it.<br>
<br>
369<br>
00:16:31,470 --> 00:16:34,920<br>
Now when we were designing<br>
these LifeCycle components,<br>
<br>
370<br>
00:16:34,920 --> 00:16:38,730<br>
the LiveData, see we<br>
spent a lot of time<br>
<br>
371<br>
00:16:38,730 --> 00:16:41,380<br>
to get rid of one exception.<br>
<br>
372<br>
00:16:41,380 --> 00:16:43,350<br>
This fragment exception that I--<br>
<br>
373<br>
00:16:43,350 --> 00:16:50,520<br>
[APPLAUSE]<br>
<br>
374<br>
00:16:50,520 --> 00:16:54,350<br>
We really wanted to say, please,<br>
no more fragment transaction<br>
<br>
375<br>
00:16:54,350 --> 00:16:55,460<br>
exceptions.<br>
<br>
376<br>
00:16:55,460 --> 00:16:58,570<br>
So LiveData guarantees that<br>
if you received anywhere,<br>
<br>
377<br>
00:16:58,570 --> 00:17:00,910<br>
you could run a<br>
fragment transaction.<br>
<br>
378<br>
00:17:00,910 --> 00:17:05,310<br>
And to see how we are making<br>
it part of the history,<br>
<br>
379<br>
00:17:05,310 --> 00:17:10,118<br>
I want to invite Adam<br>
back to explain it to us.<br>
<br>
380<br>
00:17:10,118 --> 00:17:11,539<br>
ADAM POWELL: All<br>
right, so anyone<br>
<br>
381<br>
00:17:11,540 --> 00:17:13,205<br>
who has received one<br>
of these exceptions<br>
<br>
382<br>
00:17:13,205 --> 00:17:15,289<br>
realizes that it<br>
doesn't just come<br>
<br>
383<br>
00:17:15,290 --> 00:17:18,710<br>
from trying to do something<br>
when you just completely stopped<br>
<br>
384<br>
00:17:18,710 --> 00:17:20,348<br>
and you absolutely know it.<br>
<br>
385<br>
00:17:20,348 --> 00:17:21,889<br>
These exceptions<br>
tend to come in when<br>
<br>
386<br>
00:17:21,890 --> 00:17:26,010<br>
you get into very intricate,<br>
nested life cycles.<br>
<br>
387<br>
00:17:26,010 --> 00:17:28,910<br>
So we wanted to make sure to be<br>
very thoughtful about defining<br>
<br>
388<br>
00:17:28,910 --> 00:17:34,190<br>
how the LifeCycle observer<br>
callbacks are invoked and when.<br>
<br>
389<br>
00:17:34,190 --> 00:17:37,400<br>
So in a case like<br>
this, what happens?<br>
<br>
390<br>
00:17:37,400 --> 00:17:42,120<br>
You have defined handler<br>
for the stop event.<br>
<br>
391<br>
00:17:42,120 --> 00:17:44,872<br>
So in the container<br>
your activity onStop,<br>
<br>
392<br>
00:17:44,872 --> 00:17:47,330<br>
you want to make sure that you<br>
don't get an onChanged event<br>
<br>
393<br>
00:17:47,330 --> 00:17:48,770<br>
after the onStop has happened.<br>
<br>
394<br>
00:17:48,770 --> 00:17:52,660<br>
<br>
<br>
395<br>
00:17:52,660 --> 00:17:54,570<br>
But in order for<br>
that to happen, what<br>
<br>
396<br>
00:17:54,570 --> 00:17:56,490<br>
needs to be true<br>
about when we actually<br>
<br>
397<br>
00:17:56,490 --> 00:18:00,030<br>
invoke all of the<br>
onStop listeners<br>
<br>
398<br>
00:18:00,030 --> 00:18:02,610<br>
that are attached<br>
to these observers.<br>
<br>
399<br>
00:18:02,610 --> 00:18:05,770<br>
So we have to define a<br>
really strict order for this.<br>
<br>
400<br>
00:18:05,770 --> 00:18:09,420<br>
So as we go through create<br>
and start and onResume,<br>
<br>
401<br>
00:18:09,420 --> 00:18:11,940<br>
we know that we need<br>
to invoke the LifeCycle<br>
<br>
402<br>
00:18:11,940 --> 00:18:15,480<br>
observers after the<br>
container event happens.<br>
<br>
403<br>
00:18:15,480 --> 00:18:18,090<br>
So you know in your<br>
observer that everything<br>
<br>
404<br>
00:18:18,090 --> 00:18:20,461<br>
about your LifeCycle<br>
owner has been configured.<br>
<br>
405<br>
00:18:20,461 --> 00:18:21,960<br>
If you check any<br>
state about it, you<br>
<br>
406<br>
00:18:21,960 --> 00:18:25,397<br>
know that you're already<br>
completely in that state.<br>
<br>
407<br>
00:18:25,397 --> 00:18:27,480<br>
But that means something<br>
really special for coming<br>
<br>
408<br>
00:18:27,480 --> 00:18:29,470<br>
back down the other direction.<br>
<br>
409<br>
00:18:29,470 --> 00:18:33,540<br>
It means that when the activity<br>
starts to become paused,<br>
<br>
410<br>
00:18:33,540 --> 00:18:34,995<br>
you want your<br>
LifeCycle observers<br>
<br>
411<br>
00:18:34,995 --> 00:18:36,870<br>
to be able to shut down<br>
anything that they're<br>
<br>
412<br>
00:18:36,870 --> 00:18:39,060<br>
doing before the activity<br>
does all of the work<br>
<br>
413<br>
00:18:39,060 --> 00:18:41,400<br>
to actually become paused.<br>
<br>
414<br>
00:18:41,400 --> 00:18:42,810<br>
Similar for stop.<br>
<br>
415<br>
00:18:42,810 --> 00:18:44,850<br>
And this is where<br>
this becomes really<br>
<br>
416<br>
00:18:44,850 --> 00:18:47,220<br>
important for the fragment<br>
transaction exception.<br>
<br>
417<br>
00:18:47,220 --> 00:18:49,260<br>
You want to make<br>
sure that you're<br>
<br>
418<br>
00:18:49,260 --> 00:18:52,440<br>
recording, that you're fully<br>
stopped before the fragment<br>
<br>
419<br>
00:18:52,440 --> 00:18:54,600<br>
system goes through<br>
and flags everything<br>
<br>
420<br>
00:18:54,600 --> 00:18:58,180<br>
as being completely locked out.<br>
<br>
421<br>
00:18:58,180 --> 00:19:01,410<br>
So what that means is that the<br>
stop event of your LifeCycle<br>
<br>
422<br>
00:19:01,410 --> 00:19:04,770<br>
observer will always be invoked<br>
before the activity onStop<br>
<br>
423<br>
00:19:04,770 --> 00:19:10,710<br>
or before the full stop event<br>
for your container happens.<br>
<br>
424<br>
00:19:10,710 --> 00:19:13,260<br>
So this seems really similar<br>
to some other libraries<br>
<br>
425<br>
00:19:13,260 --> 00:19:15,480<br>
that some people may<br>
have seen in the past.<br>
<br>
426<br>
00:19:15,480 --> 00:19:16,600<br>
Can you talk about that?<br>
<br>
427<br>
00:19:16,600 --> 00:19:22,530<br>
SERGEI VASILINETC: Yes, when we<br>
create new observable pattern,<br>
<br>
428<br>
00:19:22,530 --> 00:19:26,220<br>
nowadays this question<br>
is unavoidable.<br>
<br>
429<br>
00:19:26,220 --> 00:19:29,220<br>
Is it another RxJava?<br>
<br>
430<br>
00:19:29,220 --> 00:19:32,490<br>
And the answer to<br>
this question is, yes,<br>
<br>
431<br>
00:19:32,490 --> 00:19:34,740<br>
because we want to promote<br>
a reactive programming<br>
<br>
432<br>
00:19:34,740 --> 00:19:37,980<br>
model, especially when it<br>
comes to the relationship<br>
<br>
433<br>
00:19:37,980 --> 00:19:40,710<br>
between your UI and the<br>
state [INAUDIBLE] UI.<br>
<br>
434<br>
00:19:40,710 --> 00:19:45,490<br>
We want you to react on<br>
the changes of the state.<br>
<br>
435<br>
00:19:45,490 --> 00:19:48,300<br>
So it means that it's a<br>
reactive programming model.<br>
<br>
436<br>
00:19:48,300 --> 00:19:51,000<br>
But on the other hand, no.<br>
<br>
437<br>
00:19:51,000 --> 00:19:54,840<br>
Because it's the LifeCycle<br>
aware out of box,<br>
<br>
438<br>
00:19:54,840 --> 00:19:57,930<br>
as Yigit mentioned,<br>
and it's much easier.<br>
<br>
439<br>
00:19:57,930 --> 00:20:02,940<br>
As many of you may know,<br>
the learning curve of RxJava<br>
<br>
440<br>
00:20:02,940 --> 00:20:04,560<br>
is super steep.<br>
<br>
441<br>
00:20:04,560 --> 00:20:08,850<br>
And if you have an<br>
Android learner curve,<br>
<br>
442<br>
00:20:08,850 --> 00:20:13,350<br>
and after that we add RxJava<br>
learning curve on top of it,<br>
<br>
443<br>
00:20:13,350 --> 00:20:16,050<br>
it becomes very<br>
hard to new people<br>
<br>
444<br>
00:20:16,050 --> 00:20:19,420<br>
to start to develop<br>
on our platform.<br>
<br>
445<br>
00:20:19,420 --> 00:20:25,890<br>
So we can't just say to them,<br>
oh let's go, just learn this,<br>
<br>
446<br>
00:20:25,890 --> 00:20:27,330<br>
that's it. .<br>
<br>
447<br>
00:20:27,330 --> 00:20:32,310<br>
No, but if you already<br>
learned RxJava,<br>
<br>
448<br>
00:20:32,310 --> 00:20:37,020<br>
we don't expect you to migrate<br>
from it to our solution.<br>
<br>
449<br>
00:20:37,020 --> 00:20:41,280<br>
Because you already<br>
passed the learning curve,<br>
<br>
450<br>
00:20:41,280 --> 00:20:45,960<br>
you and your coworkers are<br>
comfortable with it, fine.<br>
<br>
451<br>
00:20:45,960 --> 00:20:48,190<br>
We are totally fine with this.<br>
<br>
452<br>
00:20:48,190 --> 00:20:51,330<br>
But one thing we ask<br>
you to do is to be sure<br>
<br>
453<br>
00:20:51,330 --> 00:20:53,920<br>
that you manage LifeCycle.<br>
<br>
454<br>
00:20:53,920 --> 00:20:58,210<br>
RxJava has common<br>
approaches to solve this.<br>
<br>
455<br>
00:20:58,210 --> 00:21:02,430<br>
Be sure to use it and<br>
everything will be fine.<br>
<br>
456<br>
00:21:02,430 --> 00:21:09,885<br>
But when you start a new app,<br>
I think this model is the best.<br>
<br>
457<br>
00:21:09,885 --> 00:21:15,010<br>
The best is to start the project<br>
with LiveData, because it's<br>
<br>
458<br>
00:21:15,010 --> 00:21:17,310<br>
simpler, it's faster,<br>
it's lightweight,<br>
<br>
459<br>
00:21:17,310 --> 00:21:20,270<br>
it's well integrated<br>
with a framework.<br>
<br>
460<br>
00:21:20,270 --> 00:21:24,970<br>
And if you feel like you love<br>
reacting programming a lot,<br>
<br>
461<br>
00:21:24,970 --> 00:21:28,480<br>
you want to bring it<br>
not only to relation<br>
<br>
462<br>
00:21:28,480 --> 00:21:31,930<br>
between UI and the state.<br>
<br>
463<br>
00:21:31,930 --> 00:21:33,430<br>
You want to bring<br>
it to the business<br>
<br>
464<br>
00:21:33,430 --> 00:21:36,340<br>
part of your application.<br>
<br>
465<br>
00:21:36,340 --> 00:21:41,070<br>
Then you may consider<br>
the addition of RxJava,<br>
<br>
466<br>
00:21:41,070 --> 00:21:44,230<br>
because it gives you more power.<br>
<br>
467<br>
00:21:44,230 --> 00:21:47,140<br>
And we will actually<br>
help you to do that.<br>
<br>
468<br>
00:21:47,140 --> 00:21:51,790<br>
We have this extension<br>
to our library, which<br>
<br>
469<br>
00:21:51,790 --> 00:21:55,780<br>
gives a possibility to create<br>
LiveData from Publisher<br>
<br>
470<br>
00:21:55,780 --> 00:21:58,930<br>
and create Publisher<br>
from LiveData.<br>
<br>
471<br>
00:21:58,930 --> 00:22:03,970<br>
So this integration<br>
should be quite smooth.<br>
<br>
472<br>
00:22:03,970 --> 00:22:07,330<br>
But I want to highlight a<br>
key difference between RxJava<br>
<br>
473<br>
00:22:07,330 --> 00:22:08,080<br>
and LiveData.<br>
<br>
474<br>
00:22:08,080 --> 00:22:11,980<br>
So as Yigit already<br>
said, LiveData<br>
<br>
475<br>
00:22:11,980 --> 00:22:13,870<br>
is a holder and not a stream.<br>
<br>
476<br>
00:22:13,870 --> 00:22:17,320<br>
So we have a reference<br>
to the last value,<br>
<br>
477<br>
00:22:17,320 --> 00:22:20,290<br>
and observers immediately<br>
receive the last value when<br>
<br>
478<br>
00:22:20,290 --> 00:22:24,820<br>
they start to observe LiveData.<br>
<br>
479<br>
00:22:24,820 --> 00:22:27,550<br>
And now the big difference<br>
is a threading model.<br>
<br>
480<br>
00:22:27,550 --> 00:22:31,840<br>
As you know, RxJava has a very<br>
sophisticated threading model.<br>
<br>
481<br>
00:22:31,840 --> 00:22:35,390<br>
It's extremely powerful,<br>
but in most cases,<br>
<br>
482<br>
00:22:35,390 --> 00:22:37,610<br>
you probably don't need it.<br>
<br>
483<br>
00:22:37,610 --> 00:22:40,360<br>
And we have everything<br>
on the main thread.<br>
<br>
484<br>
00:22:40,360 --> 00:22:42,190<br>
And the reason for<br>
this is we want<br>
<br>
485<br>
00:22:42,190 --> 00:22:47,150<br>
to give you all these guarantees<br>
about when we will notify you<br>
<br>
486<br>
00:22:47,150 --> 00:22:50,740<br>
about state changes.<br>
<br>
487<br>
00:22:50,740 --> 00:22:56,200<br>
And we can't do this<br>
on a background thread.<br>
<br>
488<br>
00:22:56,200 --> 00:22:58,330<br>
We have just the one exception.<br>
<br>
489<br>
00:22:58,330 --> 00:23:00,850<br>
We have a post<br>
value method which<br>
<br>
490<br>
00:23:00,850 --> 00:23:03,720<br>
just is a method<br>
which trampoline value<br>
<br>
491<br>
00:23:03,720 --> 00:23:07,725<br>
from a background thread to the<br>
main thread and sets it there.<br>
<br>
492<br>
00:23:07,725 --> 00:23:08,770<br>
It's super simple.<br>
<br>
493<br>
00:23:08,770 --> 00:23:11,400<br>
So quick summary of what<br>
we have at this point.<br>
<br>
494<br>
00:23:11,400 --> 00:23:13,870<br>
LiveData events,<br>
observable pattern<br>
<br>
495<br>
00:23:13,870 --> 00:23:16,460<br>
which respects these events.<br>
<br>
496<br>
00:23:16,460 --> 00:23:20,090<br>
But there is one big thing<br>
which is not covered yet.<br>
<br>
497<br>
00:23:20,090 --> 00:23:23,590<br>
And this is how to handle<br>
onConfigurationChanges.<br>
<br>
498<br>
00:23:23,590 --> 00:23:28,690<br>
In 2017, almost nine<br>
years after Android<br>
<br>
499<br>
00:23:28,690 --> 00:23:32,050<br>
was first time released, we<br>
still discuss this question.<br>
<br>
500<br>
00:23:32,050 --> 00:23:34,090<br>
And this is a totally<br>
legit question.<br>
<br>
501<br>
00:23:34,090 --> 00:23:38,290<br>
And we hear it constantly<br>
from new Android developers.<br>
<br>
502<br>
00:23:38,290 --> 00:23:40,730<br>
Many of you probably know<br>
whats the deal with it.<br>
<br>
503<br>
00:23:40,730 --> 00:23:44,770<br>
But let's take a look at<br>
this oversimplified example,<br>
<br>
504<br>
00:23:44,770 --> 00:23:47,830<br>
but it's still very vivid.<br>
<br>
505<br>
00:23:47,830 --> 00:23:50,050<br>
So he wants to show<br>
this information<br>
<br>
506<br>
00:23:50,050 --> 00:23:52,060<br>
about user and your activity.<br>
<br>
507<br>
00:23:52,060 --> 00:23:54,830<br>
And you want to make<br>
some web service request.<br>
<br>
508<br>
00:23:54,830 --> 00:24:00,340<br>
We will use LiveData to get<br>
this result. It's super simple.<br>
<br>
509<br>
00:24:00,340 --> 00:24:02,800<br>
When the request is just<br>
started, it's empty.<br>
<br>
510<br>
00:24:02,800 --> 00:24:06,620<br>
When the request<br>
response is received,<br>
<br>
511<br>
00:24:06,620 --> 00:24:11,740<br>
we put it to<br>
LiveData as a value.<br>
<br>
512<br>
00:24:11,740 --> 00:24:14,070<br>
And later we'll update our UI.<br>
<br>
513<br>
00:24:14,070 --> 00:24:19,917<br>
We will notify the activity, and<br>
it will do everything it needs.<br>
<br>
514<br>
00:24:19,917 --> 00:24:22,250<br>
So what happens if the activity<br>
is going to [INAUDIBLE].<br>
<br>
515<br>
00:24:22,250 --> 00:24:25,750<br>
We're going to<br>
make a call twice,<br>
<br>
516<br>
00:24:25,750 --> 00:24:28,560<br>
and I hope that you don't<br>
call web service right<br>
<br>
517<br>
00:24:28,560 --> 00:24:29,740<br>
into your activity.<br>
<br>
518<br>
00:24:29,740 --> 00:24:33,670<br>
But you probably have<br>
some abstractions<br>
<br>
519<br>
00:24:33,670 --> 00:24:36,010<br>
that does something<br>
like that, which<br>
<br>
520<br>
00:24:36,010 --> 00:24:41,040<br>
goes to a network, which goes<br>
to caching and persistence<br>
<br>
521<br>
00:24:41,040 --> 00:24:43,030<br>
storages.<br>
<br>
522<br>
00:24:43,030 --> 00:24:47,170<br>
And all the separations<br>
are synchronized by nature.<br>
<br>
523<br>
00:24:47,170 --> 00:24:51,070<br>
So communication of these<br>
components are synchronized.<br>
<br>
524<br>
00:24:51,070 --> 00:24:55,510<br>
And you probably don't want to<br>
make these calls twice anyway.<br>
<br>
525<br>
00:24:55,510 --> 00:24:58,060<br>
So what you want<br>
to do is to cache.<br>
<br>
526<br>
00:24:58,060 --> 00:25:01,470<br>
This is our data,<br>
like in our example.<br>
<br>
527<br>
00:25:01,470 --> 00:25:04,480<br>
And what are the ways<br>
today to do that?<br>
<br>
528<br>
00:25:04,480 --> 00:25:06,960<br>
Well, one of a<br>
proposed way to do it<br>
<br>
529<br>
00:25:06,960 --> 00:25:10,570<br>
is a Fragment.setRetainInstance,<br>
and Yigit<br>
<br>
530<br>
00:25:10,570 --> 00:25:12,340<br>
can rant about this for hours.<br>
<br>
531<br>
00:25:12,340 --> 00:25:14,770<br>
Unfortunately, we don't<br>
have time for this today.<br>
<br>
532<br>
00:25:14,770 --> 00:25:17,600<br>
But I just say that<br>
the only effect<br>
<br>
533<br>
00:25:17,600 --> 00:25:19,900<br>
that you have to run<br>
fragment transaction<br>
<br>
534<br>
00:25:19,900 --> 00:25:22,400<br>
is terrifying for<br>
a lot of people.<br>
<br>
535<br>
00:25:22,400 --> 00:25:25,780<br>
People go nuts and<br>
another possible way<br>
<br>
536<br>
00:25:25,780 --> 00:25:29,960<br>
to solve this is loaders, but<br>
we don't fit here well as well.<br>
<br>
537<br>
00:25:29,960 --> 00:25:33,010<br>
So we decided to tackle<br>
this problem once again<br>
<br>
538<br>
00:25:33,010 --> 00:25:35,230<br>
and create ViewModel.<br>
<br>
539<br>
00:25:35,230 --> 00:25:36,030<br>
So what is this?<br>
<br>
540<br>
00:25:36,030 --> 00:25:39,070<br>
ViewModel is an object<br>
which is associated<br>
<br>
541<br>
00:25:39,070 --> 00:25:41,440<br>
with a fragment or an<br>
activity, but is retained<br>
<br>
542<br>
00:25:41,440 --> 00:25:43,750<br>
during configuration changes.<br>
<br>
543<br>
00:25:43,750 --> 00:25:48,190<br>
So its scope is a kind of a<br>
logical scope of your activity.<br>
<br>
544<br>
00:25:48,190 --> 00:25:51,300<br>
So what does this mean?<br>
<br>
545<br>
00:25:51,300 --> 00:25:51,900<br>
Let's see.<br>
<br>
546<br>
00:25:51,900 --> 00:25:54,220<br>
If we have access time and<br>
the current moment, and we<br>
<br>
547<br>
00:25:54,220 --> 00:25:55,540<br>
can predict the future.<br>
<br>
548<br>
00:25:55,540 --> 00:25:57,670<br>
And we know that activity<br>
is going to be created,<br>
<br>
549<br>
00:25:57,670 --> 00:25:59,390<br>
and this means that<br>
all construction<br>
<br>
550<br>
00:25:59,390 --> 00:26:01,690<br>
events are going to happen.<br>
<br>
551<br>
00:26:01,690 --> 00:26:05,440<br>
During onCreate we will request<br>
ViewModel for the first time.<br>
<br>
552<br>
00:26:05,440 --> 00:26:07,780<br>
We will create it, and<br>
after that this activity<br>
<br>
553<br>
00:26:07,780 --> 00:26:10,850<br>
just uses this ViewModel.<br>
<br>
554<br>
00:26:10,850 --> 00:26:12,220<br>
Very simple.<br>
<br>
555<br>
00:26:12,220 --> 00:26:16,060<br>
Now we predict that the<br>
activity is going to be rotated.<br>
<br>
556<br>
00:26:16,060 --> 00:26:20,700<br>
Let's see what's going to<br>
happen with our ViewModel.<br>
<br>
557<br>
00:26:20,700 --> 00:26:27,400<br>
We will receive events,<br>
onPause, onStop, and onDestroy.<br>
<br>
558<br>
00:26:27,400 --> 00:26:30,880<br>
But when all the<br>
segments are cured<br>
<br>
559<br>
00:26:30,880 --> 00:26:34,090<br>
and your activity is<br>
destroyed, it's thrown away<br>
<br>
560<br>
00:26:34,090 --> 00:26:38,210<br>
and is garbage collected,<br>
ViewModel survived it.<br>
<br>
561<br>
00:26:38,210 --> 00:26:42,070<br>
And the new activity, which was<br>
created in place the old one<br>
<br>
562<br>
00:26:42,070 --> 00:26:44,510<br>
uses the same, old object.<br>
<br>
563<br>
00:26:44,510 --> 00:26:48,520<br>
So you can easily cache<br>
there LiveData as we want to<br>
<br>
564<br>
00:26:48,520 --> 00:26:50,690<br>
or something else.<br>
<br>
565<br>
00:26:50,690 --> 00:26:52,720<br>
The last case, what<br>
is going to happen<br>
<br>
566<br>
00:26:52,720 --> 00:26:55,600<br>
if you have finished goal?<br>
<br>
567<br>
00:26:55,600 --> 00:26:58,280<br>
Once again, we will receive<br>
these destruction events,<br>
<br>
568<br>
00:26:58,280 --> 00:27:01,570<br>
but this time,<br>
ViewModel is available<br>
<br>
569<br>
00:27:01,570 --> 00:27:03,130<br>
until onDestroy method.<br>
<br>
570<br>
00:27:03,130 --> 00:27:08,340<br>
During onDestroy method, we<br>
will call onClear on this.<br>
<br>
571<br>
00:27:08,340 --> 00:27:11,860<br>
Which notifies you if you have<br>
any currently running actions<br>
<br>
572<br>
00:27:11,860 --> 00:27:15,610<br>
or any resources<br>
its time to close.<br>
<br>
573<br>
00:27:15,610 --> 00:27:18,900<br>
And after that, it's<br>
going to be destroyed<br>
<br>
574<br>
00:27:18,900 --> 00:27:20,150<br>
and garbage collected as well.<br>
<br>
575<br>
00:27:20,150 --> 00:27:24,310<br>
So at the point when your<br>
activity is destroyed,<br>
<br>
576<br>
00:27:24,310 --> 00:27:27,340<br>
it's not going to be<br>
recreated it again.<br>
<br>
577<br>
00:27:27,340 --> 00:27:30,980<br>
Your ViewModel is gone as well.<br>
<br>
578<br>
00:27:30,980 --> 00:27:37,970<br>
So let's quickly make<br>
our sample in ViewModel.<br>
<br>
579<br>
00:27:37,970 --> 00:27:40,900<br>
So it starts with<br>
instantiating-- with creation<br>
<br>
580<br>
00:27:40,900 --> 00:27:43,270<br>
of ViewModel class.<br>
<br>
581<br>
00:27:43,270 --> 00:27:47,860<br>
We want to cache for user data<br>
to create a fill for that.<br>
<br>
582<br>
00:27:47,860 --> 00:27:50,680<br>
We agree our activity needs<br>
to access this LiveData,<br>
<br>
583<br>
00:27:50,680 --> 00:27:52,450<br>
so we create a getter for this.<br>
<br>
584<br>
00:27:52,450 --> 00:27:55,960<br>
And finally, getter is<br>
extremely straightforward.<br>
<br>
585<br>
00:27:55,960 --> 00:27:59,530<br>
If we already requested the<br>
data, we just return it.<br>
<br>
586<br>
00:27:59,530 --> 00:28:04,780<br>
If the data is now, we'll<br>
request it from a web service<br>
<br>
587<br>
00:28:04,780 --> 00:28:06,580<br>
and return it.<br>
<br>
588<br>
00:28:06,580 --> 00:28:07,422<br>
Fine.<br>
<br>
589<br>
00:28:07,422 --> 00:28:08,880<br>
We had [INAUDIBLE]<br>
on our activity.<br>
<br>
590<br>
00:28:08,880 --> 00:28:12,580<br>
Now we need to get this<br>
LiveData from ViewModel.<br>
<br>
591<br>
00:28:12,580 --> 00:28:18,370<br>
To get it, we need to create<br>
to get ViewModel somehow.<br>
<br>
592<br>
00:28:18,370 --> 00:28:19,450<br>
So this is how we do it.<br>
<br>
593<br>
00:28:19,450 --> 00:28:21,970<br>
Let's take a precise look at it.<br>
<br>
594<br>
00:28:21,970 --> 00:28:25,000<br>
First of all, we need to get<br>
ViewModel provider object.<br>
<br>
595<br>
00:28:25,000 --> 00:28:27,250<br>
This is an object<br>
which is associated<br>
<br>
596<br>
00:28:27,250 --> 00:28:28,570<br>
with a fragment or an activity.<br>
<br>
597<br>
00:28:28,570 --> 00:28:34,270<br>
It knows how to get already<br>
existing ViewModel from it<br>
<br>
598<br>
00:28:34,270 --> 00:28:36,740<br>
or how to create a new one.<br>
<br>
599<br>
00:28:36,740 --> 00:28:39,250<br>
If there is no<br>
existing ViewModel.<br>
<br>
600<br>
00:28:39,250 --> 00:28:44,650<br>
After that, we request<br>
our myActivity ViewModel,<br>
<br>
601<br>
00:28:44,650 --> 00:28:48,617<br>
and later everything<br>
is quite simple.<br>
<br>
602<br>
00:28:48,617 --> 00:28:49,450<br>
We get the userData.<br>
<br>
603<br>
00:28:49,450 --> 00:28:54,730<br>
We observe it to update the UI.<br>
<br>
604<br>
00:28:54,730 --> 00:28:59,860<br>
So what are the rules<br>
of usage of ViewModel?<br>
<br>
605<br>
00:28:59,860 --> 00:29:04,660<br>
So ViewModel manages<br>
the data for the UI.<br>
<br>
606<br>
00:29:04,660 --> 00:29:08,290<br>
It means that it<br>
speaks with business<br>
<br>
607<br>
00:29:08,290 --> 00:29:11,510<br>
parts of your application<br>
to retrieve the data.<br>
<br>
608<br>
00:29:11,510 --> 00:29:15,470<br>
So it may be a repository<br>
pattern or any other pattern<br>
<br>
609<br>
00:29:15,470 --> 00:29:17,890<br>
that they use.<br>
<br>
610<br>
00:29:17,890 --> 00:29:22,450<br>
It also, it's for its<br>
user modifications<br>
<br>
611<br>
00:29:22,450 --> 00:29:24,140<br>
back to these components.<br>
<br>
612<br>
00:29:24,140 --> 00:29:26,720<br>
And now a good<br>
case for ViewModel<br>
<br>
613<br>
00:29:26,720 --> 00:29:30,730<br>
is acting as a communication<br>
layer between fragments<br>
<br>
614<br>
00:29:30,730 --> 00:29:32,530<br>
in one activity.<br>
<br>
615<br>
00:29:32,530 --> 00:29:36,490<br>
And Yigit will speak<br>
about this later.<br>
<br>
616<br>
00:29:36,490 --> 00:29:40,840<br>
But prior to this,<br>
things that you must not<br>
<br>
617<br>
00:29:40,840 --> 00:29:42,560<br>
do in your ViewModel.<br>
<br>
618<br>
00:29:42,560 --> 00:29:46,580<br>
So first of all,<br>
you must not access<br>
<br>
619<br>
00:29:46,580 --> 00:29:51,870<br>
views and any other<br>
UI- related entities.<br>
<br>
620<br>
00:29:51,870 --> 00:29:54,670<br>
The reason for<br>
that, they are going<br>
<br>
621<br>
00:29:54,670 --> 00:29:57,010<br>
to be created during<br>
configuration change.<br>
<br>
622<br>
00:29:57,010 --> 00:30:02,400<br>
If you try to use them, you will<br>
ever use stale data from there,<br>
<br>
623<br>
00:30:02,400 --> 00:30:05,250<br>
ever to leak them.<br>
<br>
624<br>
00:30:05,250 --> 00:30:09,230<br>
That's going to finish bad.<br>
<br>
625<br>
00:30:09,230 --> 00:30:12,280<br>
And it's fragmented<br>
or activity's job<br>
<br>
626<br>
00:30:12,280 --> 00:30:17,110<br>
to bind the data which you<br>
will get from a ViewModel<br>
<br>
627<br>
00:30:17,110 --> 00:30:21,260<br>
with actual UI,<br>
text use, buttons.<br>
<br>
628<br>
00:30:21,260 --> 00:30:23,190<br>
I don't know what else.<br>
<br>
629<br>
00:30:23,190 --> 00:30:26,590<br>
And one more thing,<br>
there are sources<br>
<br>
630<br>
00:30:26,590 --> 00:30:31,120<br>
which sound more harmless<br>
like strings or drawable,<br>
<br>
631<br>
00:30:31,120 --> 00:30:33,790<br>
and you may think,<br>
I may cash it here.<br>
<br>
632<br>
00:30:33,790 --> 00:30:38,020<br>
No, they depend on current<br>
configuration state of state<br>
<br>
633<br>
00:30:38,020 --> 00:30:38,800<br>
as well.<br>
<br>
634<br>
00:30:38,800 --> 00:30:43,360<br>
So yes, right now you may<br>
have just one resource<br>
<br>
635<br>
00:30:43,360 --> 00:30:46,540<br>
for every configuration,<br>
but later, you<br>
<br>
636<br>
00:30:46,540 --> 00:30:49,870<br>
will add in the same resource<br>
for a different configuration.<br>
<br>
637<br>
00:30:49,870 --> 00:30:54,010<br>
You will easily forget<br>
to update your ViewModel.<br>
<br>
638<br>
00:30:54,010 --> 00:30:58,540<br>
And you may not notice<br>
this, but your users<br>
<br>
639<br>
00:30:58,540 --> 00:31:00,250<br>
will see the invalid UI.<br>
<br>
640<br>
00:31:00,250 --> 00:31:02,230<br>
And this is just ugly.<br>
<br>
641<br>
00:31:02,230 --> 00:31:06,970<br>
And now Yigit will speak about<br>
Inter Fragment communications.<br>
<br>
642<br>
00:31:06,970 --> 00:31:10,510<br>
<br>
<br>
643<br>
00:31:10,510 --> 00:31:12,270<br>
YIGIT BOYAR: So I<br>
want to talk about one<br>
<br>
644<br>
00:31:12,270 --> 00:31:16,050<br>
of my favorite features<br>
about ViewModel,<br>
<br>
645<br>
00:31:16,050 --> 00:31:19,020<br>
which is communicating<br>
between multiple fragments<br>
<br>
646<br>
00:31:19,020 --> 00:31:21,980<br>
of the same activity.<br>
<br>
647<br>
00:31:21,980 --> 00:31:25,200<br>
It's good that UI like this,<br>
like the Gmail on the tablet<br>
<br>
648<br>
00:31:25,200 --> 00:31:29,500<br>
where on the left side you pick<br>
an email and on the right side,<br>
<br>
649<br>
00:31:29,500 --> 00:31:31,860<br>
it shows the contents<br>
of the email.<br>
<br>
650<br>
00:31:31,860 --> 00:31:34,560<br>
Now usually you will<br>
implement this as a fragment<br>
<br>
651<br>
00:31:34,560 --> 00:31:37,940<br>
on the left which picks<br>
something from the list,<br>
<br>
652<br>
00:31:37,940 --> 00:31:39,780<br>
and another fragment<br>
on the right, which<br>
<br>
653<br>
00:31:39,780 --> 00:31:42,960<br>
shows how to show the<br>
contents of an email<br>
<br>
654<br>
00:31:42,960 --> 00:31:45,330<br>
so that if you're on the<br>
phone you can reuse the same<br>
<br>
655<br>
00:31:45,330 --> 00:31:48,150<br>
fragments but separate<br>
from each other.<br>
<br>
656<br>
00:31:48,150 --> 00:31:52,170<br>
Now if you ever tried to write<br>
a UI like this, if you ever<br>
<br>
657<br>
00:31:52,170 --> 00:31:55,105<br>
tried to make these two<br>
fragments talk to each other,<br>
<br>
658<br>
00:31:55,105 --> 00:31:56,220<br>
it's a pain in the neck.<br>
<br>
659<br>
00:31:56,220 --> 00:31:57,240<br>
It's very, very hard.<br>
<br>
660<br>
00:31:57,240 --> 00:31:59,510<br>
Like you need to<br>
create an interface.<br>
<br>
661<br>
00:31:59,510 --> 00:32:01,530<br>
But then what if<br>
one fragment gets<br>
<br>
662<br>
00:32:01,530 --> 00:32:03,540<br>
created before the other one.<br>
<br>
663<br>
00:32:03,540 --> 00:32:05,940<br>
An activity needs to<br>
talk to each other.<br>
<br>
664<br>
00:32:05,940 --> 00:32:07,931<br>
Or like when the<br>
activities are restored,<br>
<br>
665<br>
00:32:07,931 --> 00:32:09,430<br>
you don't really<br>
know which fragment<br>
<br>
666<br>
00:32:09,430 --> 00:32:11,340<br>
will be restored first.<br>
<br>
667<br>
00:32:11,340 --> 00:32:14,880<br>
It is really hard to<br>
manage this state.<br>
<br>
668<br>
00:32:14,880 --> 00:32:21,020<br>
But we can actually solve this<br>
very elegantly using ViewModel.<br>
<br>
669<br>
00:32:21,020 --> 00:32:23,930<br>
So let's say so these two<br>
families actually want<br>
<br>
670<br>
00:32:23,930 --> 00:32:26,390<br>
to talk about a selected email.<br>
<br>
671<br>
00:32:26,390 --> 00:32:29,060<br>
This is the information<br>
they want to share.<br>
<br>
672<br>
00:32:29,060 --> 00:32:30,950<br>
So let's put it<br>
inside a ViewModel<br>
<br>
673<br>
00:32:30,950 --> 00:32:33,920<br>
and we are going to call<br>
this shared ViewModel.<br>
<br>
674<br>
00:32:33,920 --> 00:32:36,130<br>
So it has a mutable<br>
LiveData inside it<br>
<br>
675<br>
00:32:36,130 --> 00:32:41,430<br>
which you call selected, and it<br>
provides two very simple APIs.<br>
<br>
676<br>
00:32:41,430 --> 00:32:45,410<br>
The first one says, set the<br>
select email to this email.<br>
<br>
677<br>
00:32:45,410 --> 00:32:49,610<br>
Another one says, get the<br>
selected email as a LiveData.<br>
<br>
678<br>
00:32:49,610 --> 00:32:52,510<br>
It's a really simple ViewModel.<br>
<br>
679<br>
00:32:52,510 --> 00:32:56,030<br>
But now once we have this,<br>
let's go back to our fragments<br>
<br>
680<br>
00:32:56,030 --> 00:32:58,260<br>
and see how we can use this.<br>
<br>
681<br>
00:32:58,260 --> 00:33:00,920<br>
So inside the content<br>
fragment, which is the one<br>
<br>
682<br>
00:33:00,920 --> 00:33:03,650<br>
that wants to display the<br>
contents of the email.<br>
<br>
683<br>
00:33:03,650 --> 00:33:07,550<br>
It wants to know when the<br>
selected email changes.<br>
<br>
684<br>
00:33:07,550 --> 00:33:09,930<br>
So we're going to go-- so<br>
we have already seen this.<br>
<br>
685<br>
00:33:09,930 --> 00:33:12,470<br>
You can go to ViewModel<br>
providers class<br>
<br>
686<br>
00:33:12,470 --> 00:33:15,230<br>
and get the ViewModel<br>
providers of this fragment.<br>
<br>
687<br>
00:33:15,230 --> 00:33:19,170<br>
But we actually want ViewModel<br>
not from this fragment,<br>
<br>
688<br>
00:33:19,170 --> 00:33:21,330<br>
we want it from our activity.<br>
<br>
689<br>
00:33:21,330 --> 00:33:25,480<br>
So all you have to do tell it<br>
to do it from your activity.<br>
<br>
690<br>
00:33:25,480 --> 00:33:28,520<br>
Now it's going to return your<br>
ViewModel in the activity<br>
<br>
691<br>
00:33:28,520 --> 00:33:33,140<br>
scope, and I will say, get<br>
for the shared ViewModel.<br>
<br>
692<br>
00:33:33,140 --> 00:33:35,770<br>
Now, the very first time one<br>
of the fragments called this,<br>
<br>
693<br>
00:33:35,770 --> 00:33:37,460<br>
we are going to<br>
create a new one.<br>
<br>
694<br>
00:33:37,460 --> 00:33:39,520<br>
When the other<br>
fragment comes alive,<br>
<br>
695<br>
00:33:39,520 --> 00:33:42,830<br>
it's going to receive the<br>
same ViewModel instance.<br>
<br>
696<br>
00:33:42,830 --> 00:33:44,100<br>
And I will do the same thing.<br>
<br>
697<br>
00:33:44,100 --> 00:33:46,650<br>
So this one says, get<br>
the selected email.<br>
<br>
698<br>
00:33:46,650 --> 00:33:48,662<br>
Start observing on it.<br>
<br>
699<br>
00:33:48,662 --> 00:33:50,540<br>
Really similarly, in<br>
the select fragment<br>
<br>
700<br>
00:33:50,540 --> 00:33:54,500<br>
which was the one on the<br>
left by user pics and email,<br>
<br>
701<br>
00:33:54,500 --> 00:33:57,410<br>
we get the same ViewModel.<br>
<br>
702<br>
00:33:57,410 --> 00:34:00,680<br>
And whenever the user selects<br>
an email from the list,<br>
<br>
703<br>
00:34:00,680 --> 00:34:03,080<br>
we just call the<br>
ViewModel- related method<br>
<br>
704<br>
00:34:03,080 --> 00:34:05,120<br>
to change the selected email.<br>
<br>
705<br>
00:34:05,120 --> 00:34:08,239<br>
Now these two fragments<br>
talking to each other<br>
<br>
706<br>
00:34:08,239 --> 00:34:10,710<br>
without actually<br>
talking to each other.<br>
<br>
707<br>
00:34:10,710 --> 00:34:13,730<br>
How does this really happen?<br>
<br>
708<br>
00:34:13,730 --> 00:34:15,380<br>
So if we go back to our UI.<br>
<br>
709<br>
00:34:15,380 --> 00:34:18,679<br>
So we have the selector on the<br>
left, the content on the right.<br>
<br>
710<br>
00:34:18,679 --> 00:34:21,320<br>
But if you look at the<br>
details, actually both of these<br>
<br>
711<br>
00:34:21,320 --> 00:34:23,060<br>
are talking to a<br>
shared ViewModel.<br>
<br>
712<br>
00:34:23,060 --> 00:34:25,040<br>
They never talk to each other.<br>
<br>
713<br>
00:34:25,040 --> 00:34:28,580<br>
The video of this solution is<br>
that if you're on the phone,<br>
<br>
714<br>
00:34:28,580 --> 00:34:31,280<br>
let's say one fragment<br>
replaces the other one,<br>
<br>
715<br>
00:34:31,280 --> 00:34:33,080<br>
there's no room for error.<br>
<br>
716<br>
00:34:33,080 --> 00:34:35,270<br>
Like the fragment still<br>
talks to a ViewModel.<br>
<br>
717<br>
00:34:35,270 --> 00:34:37,370<br>
ViewModels always that<br>
nothing will crash.<br>
<br>
718<br>
00:34:37,370 --> 00:34:39,770<br>
They don't even care<br>
the other one is there.<br>
<br>
719<br>
00:34:39,770 --> 00:34:42,810<br>
<br>
<br>
720<br>
00:34:42,810 --> 00:34:45,349<br>
Okay, so this is a<br>
lot of information,<br>
<br>
721<br>
00:34:45,349 --> 00:34:47,670<br>
and there's further<br>
details about how<br>
<br>
722<br>
00:34:47,670 --> 00:34:49,170<br>
these life cycles work.<br>
<br>
723<br>
00:34:49,170 --> 00:34:51,330<br>
We really spent a<br>
lot of time to make<br>
<br>
724<br>
00:34:51,330 --> 00:34:55,260<br>
these handle most common<br>
used cases on Android.<br>
<br>
725<br>
00:34:55,260 --> 00:34:58,620<br>
So we come in just<br>
the first trade out.<br>
<br>
726<br>
00:34:58,620 --> 00:35:03,150<br>
You could try it<br>
now, in [INAUDIBLE].<br>
<br>
727<br>
00:35:03,150 --> 00:35:05,850<br>
Please check out all of the<br>
architecture components.<br>
<br>
728<br>
00:35:05,850 --> 00:35:08,640<br>
These are things that actually<br>
work very well together.<br>
<br>
729<br>
00:35:08,640 --> 00:35:11,070<br>
We have an architecture<br>
guide which shows you<br>
<br>
730<br>
00:35:11,070 --> 00:35:15,330<br>
how to use these things together<br>
to write a good application.<br>
<br>
731<br>
00:35:15,330 --> 00:35:16,980<br>
And also check our code labs.<br>
<br>
732<br>
00:35:16,980 --> 00:35:20,490<br>
We have code lab sections that<br>
will give you a first glimpse<br>
<br>
733<br>
00:35:20,490 --> 00:35:23,841<br>
of how LifeCycles work.<br>
<br>
734<br>
00:35:23,841 --> 00:35:24,340<br>
Thank you<br>
<br>
735<br>
00:35:24,340 --> 00:35:26,815<br>
[APPLAUSE]<br>
<br>
736<br>
00:35:26,815 --> 00:35:29,055<br>
[MUSIC PLAYING]<br>
<br>
737<br>
00:35:29,055 --> 00:00:00,000<br>
<br>
<br>

  </td>
  <td>
   1<br>
00:00:00,000 --> 00:00:06,201<br>
[ИГРАЕТ МУЗЫКА]<br>
<br>
2<br>
00:00:06,201 --> 00:00:09,380<br>
СЕРГЕЙ ВАСИЛИНЕЦ:<br>
Доброе утро всем!.<br>
<br>
3<br>
00:00:09,380 --> 00:00:10,130<br>
Меня зовут Сергей<br>
<br>
4<br>
00:00:10,130 --> 00:00:12,620<br>
Это Adam и Yigit,<br>
они сегодня со мной,<br>
<br>
5<br>
00:00:12,620 --> 00:00:15,780<br>
и мы поговорим о проблемах<br>
жизненного цикла.<br>
<br>
6<br>
00:00:15,780 --> 00:00:21,240<br>
Возможно, многие из вас<br>
присутствовали вчера,<br>
<br>
7<br>
00:00:21,240 --> 00:00:24,670<br>
когда Yigit представил новые<br>
архитектурные компоненты.<br>
<br>
8<br>
00:00:24,670 --> 00:00:27,550<br>
Он представил LiveData,<br>
ViewModel, новую ORM<br>
<br>
9<br>
00:00:27,550 --> 00:00:28,540<br>
называемую Room.<br>
<br>
10<br>
00:00:28,540 --> 00:00:31,900<br>
И сегодня мы будем говорить<br>
о жизненном цикле из<br>
<br>
11<br>
00:00:31,900 --> 00:00:34,990<br>
парадигмы архитектурных<br>
компонентов.<br>
<br>
12<br>
00:00:34,990 --> 00:00:37,715<br>
Поэтому мы снова поговорим о<br>
LiveData и ViewModel.<br>
<br>
13<br>
00:00:37,715 --> 00:00:41,140<br>
Мы поговорим о преимуществах<br>
жизненного цикла и о том, на каких<br>
<br>
14<br>
00:00:41,140 --> 00:00:45,210<br>
библиотеках он основывается.<br>
<br>
15<br>
00:00:45,210 --> 00:00:49,150<br>
Но мы затронем много деталей.<br>
<br>
16<br>
00:00:49,150 --> 00:00:51,890<br>
У нас будут некоторые аргументы<br>
в пользу наших решений.<br>
<br>
17<br>
00:00:51,890 --> 00:00:56,360<br>
И, если вы были на вчерашней сессии,<br>
вам будет все еще интересно.<br>
<br>
18<br>
00:00:56,360 --> 00:00:57,900<br>
Но даже если вы не<br>
присутствовали вчера, мы<br>
<br>
19<br>
00:00:57,900 --> 00:00:59,600<br>
заново расскажем обо<br>
всех этих вещах<br>
<br>
20<br>
00:00:59,600 --> 00:01:03,370<br>
так что вам будет<br>
все понятно.<br>
<br>
21<br>
00:01:03,370 --> 00:01:07,480<br>
Ну, давайте посмотрим что у нас есть.<br>
<br>
22<br>
00:01:07,480 --> 00:01:11,280<br>
Сегодня у нас Activity<br>
по частям.<br>
<br>
23<br>
00:01:11,280 --> 00:01:14,300<br>
Я начну стого, что<br>
длинно, но с того, где<br>
<br>
24<br>
00:01:14,300 --> 00:01:17,330<br>
десятки и десятки строк.<br>
<br>
25<br>
00:01:17,330 --> 00:01:22,190<br>
И эти строки результат очень<br>
естественного процесса.<br>
<br>
26<br>
00:01:22,190 --> 00:01:24,690<br>
Сервисы Google play<br>
попросили зарегистрировать их<br>
<br>
27<br>
00:01:24,690 --> 00:01:25,670<br>
в onStart методах.<br>
<br>
28<br>
00:01:25,670 --> 00:01:29,620<br>
Ваши компоненты должны знать<br>
о событиях жизненного цикла,<br>
<br>
29<br>
00:01:29,620 --> 00:01:34,640<br>
поэтому вам нужно получить их<br>
в каком-либо API.<br>
<br>
30<br>
00:01:34,640 --> 00:01:38,100<br>
И соответственно,<br>
в onStop методе,<br>
<br>
31<br>
00:01:38,100 --> 00:01:42,530<br>
вы должны вызвать все<br>
методы-остановки,<br>
<br>
32<br>
00:01:42,530 --> 00:01:44,900<br>
и тогда очень легко<br>
забыть о каком-либо из них.<br>
<br>
33<br>
00:01:44,900 --> 00:01:46,880<br>
И в результате утечка.<br>
<br>
34<br>
00:01:46,880 --> 00:01:51,950<br>
И это приведет к растрате<br>
батареи пользователя,<br>
<br>
35<br>
00:01:51,950 --> 00:01:54,920<br>
и ваше приложение понравится<br>
ему немного меньше.<br>
<br>
36<br>
00:01:54,920 --> 00:01:58,190<br>
И это, возможно, нормально для них,<br>
но мы не думаем, что это хорошо.<br>
<br>
37<br>
00:01:58,190 --> 00:02:02,180<br>
И они думают, что ответ<br>
в этой ситуации - это<br>
<br>
38<br>
00:02:02,180 --> 00:02:04,130<br>
представление жизненного цикла<br>
осведомленным о компонентах.<br>
<br>
39<br>
00:02:04,130 --> 00:02:06,770<br>
Компоненты, которые взаимодействуют<br>
с жизненным циклом.<br>
<br>
40<br>
00:02:06,770 --> 00:02:08,538<br>
И первый щаг в этом r>
направлении - представление<br>
<br>
41<br>
00:02:08,538 --> 00:02:11,750<br>
жизненного цикла как<br>
объекта первого класса.<br>
<br>
42<br>
00:02:11,750 --> 00:02:13,550<br>
Итак, это очень простой<br>
объект, который отвечает на<br>
<br>
43<br>
00:02:13,550 --> 00:02:17,370<br>
вопрос, какое<br>
состояние сейчас?<br>
<br>
44<br>
00:02:17,370 --> 00:02:19,130<br>
И уведомляет вас о<br>
новых событиях. И тогда<br>
<br>
45<br>
00:02:19,130 --> 00:02:22,340<br>
никакая особенность не важна<br>
но звучит нелепо прямо сейчас,<br>
<br>
46<br>
00:02:22,340 --> 00:02:26,060<br>
события и состояния -<br>
разные вещи.<br>
<br>
47<br>
00:02:26,060 --> 00:02:28,540<br>
Вот, что я имею в виду.<br>
<br>
48<br>
00:02:28,540 --> 00:02:31,610<br>
Ваша Activity создается в<br>
инициализированном состоянии.<br>
<br>
49<br>
00:02:31,610 --> 00:02:37,965<br>
И все этапы создания<br>
проходят очень регулярно.<br>
<br>
50<br>
00:02:37,965 --> 00:02:39,680<br>
OnCreate(), создание состояния.<br>
<br>
51<br>
00:02:39,680 --> 00:02:42,460<br>
OnStart, старт состояния,<br>
то же самое для resume.<br>
<br>
52<br>
00:02:42,460 --> 00:02:45,070<br>
Но дорога назад немного<br>
более интересная.<br>
<br>
53<br>
00:02:45,070 --> 00:02:48,920<br>
So onPause event, leads<br>
you from a resume state<br>
<br>
54<br>
00:02:48,920 --> 00:02:50,480<br>
back to a starting state.<br>
<br>
55<br>
00:02:50,480 --> 00:02:53,490<br>
Not some new pause state,<br>
or something like that.<br>
<br>
56<br>
00:02:53,490 --> 00:02:57,870<br>
And the reason for this is<br>
from a system perspective,<br>
<br>
57<br>
00:02:57,870 --> 00:03:01,880<br>
the states after onPause event<br>
and onStart event are the same<br>
<br>
58<br>
00:03:01,880 --> 00:03:05,790<br>
because the sets of the actions<br>
that you are allowed to do<br>
<br>
59<br>
00:03:05,790 --> 00:03:07,010<br>
is the same.<br>
<br>
60<br>
00:03:07,010 --> 00:03:11,960<br>
And the same is true for<br>
onStop and Creative state.<br>
<br>
61<br>
00:03:11,960 --> 00:03:14,350<br>
And last event is onDestroy.<br>
<br>
62<br>
00:03:14,350 --> 00:03:18,390<br>
It's pretty straightforward.<br>
<br>
63<br>
00:03:18,390 --> 00:03:20,150<br>
It brings it to destroy state.<br>
<br>
64<br>
00:03:20,150 --> 00:03:21,730<br>
Your activity is destroyed.<br>
<br>
65<br>
00:03:21,730 --> 00:03:25,720<br>
It's going to be thrown<br>
away and garbage collected.<br>
<br>
66<br>
00:03:25,720 --> 00:03:28,020<br>
So let's make our<br>
component LifeCycle aware.<br>
<br>
67<br>
00:03:28,020 --> 00:03:29,390<br>
That's super straightforward.<br>
<br>
68<br>
00:03:29,390 --> 00:03:32,780<br>
We take it with LifeCycle<br>
observer interface,<br>
<br>
69<br>
00:03:32,780 --> 00:03:34,350<br>
accepted interface.<br>
<br>
70<br>
00:03:34,350 --> 00:03:40,320<br>
To get the actual events, we add<br>
annotation and pass the events<br>
<br>
71<br>
00:03:40,320 --> 00:03:43,200<br>
that we are interested in,<br>
you can pass multiple events<br>
<br>
72<br>
00:03:43,200 --> 00:03:43,950<br>
if you want to.<br>
<br>
73<br>
00:03:43,950 --> 00:03:48,180<br>
The last step is to add<br>
ourselves as an observer.<br>
<br>
74<br>
00:03:48,180 --> 00:03:53,910<br>
And we may have a<br>
potential problem here.<br>
<br>
75<br>
00:03:53,910 --> 00:03:57,810<br>
What if the activity is<br>
already started at this point?<br>
<br>
76<br>
00:03:57,810 --> 00:04:02,730<br>
Does this mean that we are<br>
going to receive onStop event,<br>
<br>
77<br>
00:04:02,730 --> 00:04:05,970<br>
and and we didn't<br>
receive onStart.<br>
<br>
78<br>
00:04:05,970 --> 00:04:09,540<br>
And our component probably<br>
is not ready for this.<br>
<br>
79<br>
00:04:09,540 --> 00:04:12,570<br>
But it took care<br>
of it, and we bring<br>
<br>
80<br>
00:04:12,570 --> 00:04:14,412<br>
the observer to correct state.<br>
<br>
81<br>
00:04:14,412 --> 00:04:15,370<br>
So what does this mean?<br>
<br>
82<br>
00:04:15,370 --> 00:04:17,670<br>
Let's take this example,<br>
which I just discussed.<br>
<br>
83<br>
00:04:17,670 --> 00:04:20,610<br>
From activity perspective<br>
onStart and onCreate<br>
<br>
84<br>
00:04:20,610 --> 00:04:26,250<br>
create already happened, and<br>
after that we add an observer.<br>
<br>
85<br>
00:04:26,250 --> 00:04:31,740<br>
But observer will still receive<br>
onCreate and onStart events<br>
<br>
86<br>
00:04:31,740 --> 00:04:34,950<br>
immediately when<br>
they were registered.<br>
<br>
87<br>
00:04:34,950 --> 00:04:38,130<br>
So let's take one step further.<br>
<br>
88<br>
00:04:38,130 --> 00:04:39,870<br>
OnResume, same situation.<br>
<br>
89<br>
00:04:39,870 --> 00:04:41,400<br>
Resume state will<br>
bring to resume<br>
<br>
90<br>
00:04:41,400 --> 00:04:45,550<br>
state we got an onResume<br>
event in addition to onCreate<br>
<br>
91<br>
00:04:45,550 --> 00:04:46,610<br>
and onStart.<br>
<br>
92<br>
00:04:46,610 --> 00:04:48,660<br>
A bit more<br>
interesting situation,<br>
<br>
93<br>
00:04:48,660 --> 00:04:54,590<br>
onPause In this situation, we<br>
are in a start state as well as<br>
<br>
94<br>
00:04:54,590 --> 00:04:55,830<br>
we learned.<br>
<br>
95<br>
00:04:55,830 --> 00:04:59,060<br>
So we bring the oberserver<br>
to the correct state<br>
<br>
96<br>
00:04:59,060 --> 00:05:00,030<br>
which is start.<br>
<br>
97<br>
00:05:00,030 --> 00:05:04,040<br>
So it's a similar situation<br>
as we had one minute ago.<br>
<br>
98<br>
00:05:04,040 --> 00:05:06,930<br>
Observer will receive<br>
onCreate and onStart events,<br>
<br>
99<br>
00:05:06,930 --> 00:05:09,090<br>
and that's it.<br>
<br>
100<br>
00:05:09,090 --> 00:05:13,460<br>
So we don't have a<br>
problem in this code.<br>
<br>
101<br>
00:05:13,460 --> 00:05:17,240<br>
So how to get this<br>
magical lifecycle object?<br>
<br>
102<br>
00:05:17,240 --> 00:05:20,940<br>
We have this interface<br>
which is super simple,<br>
<br>
103<br>
00:05:20,940 --> 00:05:25,060<br>
but this probably doesn't<br>
help much right now.<br>
<br>
104<br>
00:05:25,060 --> 00:05:26,580<br>
And the actual<br>
question is who are<br>
<br>
105<br>
00:05:26,580 --> 00:05:29,600<br>
LifeCycle owners out of box.<br>
<br>
106<br>
00:05:29,600 --> 00:05:34,310<br>
And the answer in this question<br>
is support library fragments<br>
<br>
107<br>
00:05:34,310 --> 00:05:35,630<br>
and support activities.<br>
<br>
108<br>
00:05:35,630 --> 00:05:40,140<br>
But unfortunately, this is<br>
true only in the bright future.<br>
<br>
109<br>
00:05:40,140 --> 00:05:44,300<br>
And right now we have<br>
LifeCycle activity<br>
<br>
110<br>
00:05:44,300 --> 00:05:46,040<br>
and LifeCycle fragment.<br>
<br>
111<br>
00:05:46,040 --> 00:05:49,520<br>
But at the point<br>
of 1.0 release, we<br>
<br>
112<br>
00:05:49,520 --> 00:05:53,720<br>
will merge our library to<br>
support libraries so you<br>
<br>
113<br>
00:05:53,720 --> 00:05:56,070<br>
don't have to use them later.<br>
<br>
114<br>
00:05:56,070 --> 00:05:59,400<br>
And now Adam will speak<br>
about some key differences<br>
<br>
115<br>
00:05:59,400 --> 00:06:02,242<br>
between fragment and<br>
LifeCyle observers<br>
<br>
116<br>
00:06:02,242 --> 00:06:04,200<br>
ADAM POWELL: So if you've<br>
been following along,<br>
<br>
117<br>
00:06:04,200 --> 00:06:06,616<br>
you probably recognize some<br>
similarities with the fragment<br>
<br>
118<br>
00:06:06,616 --> 00:06:07,950<br>
API in this as well.<br>
<br>
119<br>
00:06:07,950 --> 00:06:10,850<br>
So at this point we've got<br>
these two different components.<br>
<br>
120<br>
00:06:10,850 --> 00:06:12,480<br>
Which one do you use?<br>
<br>
121<br>
00:06:12,480 --> 00:06:14,870<br>
Well, as the slides are<br>
already spoiling for you,<br>
<br>
122<br>
00:06:14,870 --> 00:06:17,594<br>
this really isn't an<br>
either- or question.<br>
<br>
123<br>
00:06:17,594 --> 00:06:20,010<br>
One of these things doesn't<br>
necessarily replace the other.<br>
<br>
124<br>
00:06:20,010 --> 00:06:22,040<br>
And here's why.<br>
<br>
125<br>
00:06:22,040 --> 00:06:25,830<br>
Fragments, on one hand, that<br>
everybody knows and loves,<br>
<br>
126<br>
00:06:25,830 --> 00:06:28,190<br>
are statefully<br>
managed and recreated<br>
<br>
127<br>
00:06:28,190 --> 00:06:32,030<br>
after either a process death,<br>
an activity recreation,<br>
<br>
128<br>
00:06:32,030 --> 00:06:35,630<br>
or recreation of any hosts that<br>
you have the fragment within.<br>
<br>
129<br>
00:06:35,630 --> 00:06:37,760<br>
Fragments manage views<br>
and also interact<br>
<br>
130<br>
00:06:37,760 --> 00:06:39,620<br>
with the navigation<br>
stack, which are<br>
<br>
131<br>
00:06:39,620 --> 00:06:42,230<br>
things that are firmly out<br>
of scope of what LifeCycle<br>
<br>
132<br>
00:06:42,230 --> 00:06:43,880<br>
observers are meant to do.<br>
<br>
133<br>
00:06:43,880 --> 00:06:45,740<br>
Instead, LifeCycle<br>
observers are meant<br>
<br>
134<br>
00:06:45,740 --> 00:06:47,930<br>
to enable more granular<br>
factoring of your code,<br>
<br>
135<br>
00:06:47,930 --> 00:06:50,360<br>
whether you're in an<br>
activity or a fragment.<br>
<br>
136<br>
00:06:50,360 --> 00:06:51,110<br>
They're stateless.<br>
<br>
137<br>
00:06:51,110 --> 00:06:53,570<br>
So that means that they<br>
must be registered each time<br>
<br>
138<br>
00:06:53,570 --> 00:06:54,770<br>
the owner is recreated.<br>
<br>
139<br>
00:06:54,770 --> 00:06:56,186<br>
We're not going<br>
to try to recreate<br>
<br>
140<br>
00:06:56,186 --> 00:06:57,290<br>
these magically for you.<br>
<br>
141<br>
00:06:57,290 --> 00:06:59,150<br>
They don't have any<br>
concept of instant state<br>
<br>
142<br>
00:06:59,150 --> 00:07:00,780<br>
that they carry<br>
around with them.<br>
<br>
143<br>
00:07:00,780 --> 00:07:02,510<br>
So these are meant to be<br>
very, very lightweight,<br>
<br>
144<br>
00:07:02,510 --> 00:07:04,968<br>
so that you don't have a whole<br>
lot of additional management<br>
<br>
145<br>
00:07:04,968 --> 00:07:06,170<br>
overhead.<br>
<br>
146<br>
00:07:06,170 --> 00:07:09,470<br>
And last, there's no relation<br>
to the viewer navigation<br>
<br>
147<br>
00:07:09,470 --> 00:07:10,010<br>
management.<br>
<br>
148<br>
00:07:10,010 --> 00:07:12,470<br>
These really are meant<br>
to be very tightly<br>
<br>
149<br>
00:07:12,470 --> 00:07:16,330<br>
scoped, isolated components.<br>
<br>
150<br>
00:07:16,330 --> 00:07:17,950<br>
So they can really<br>
help everyone.<br>
<br>
151<br>
00:07:17,950 --> 00:07:21,040<br>
It means that it's much<br>
simpler to integrate libraries<br>
<br>
152<br>
00:07:21,040 --> 00:07:23,860<br>
with your code, as long as<br>
those libraries have provided<br>
<br>
153<br>
00:07:23,860 --> 00:07:26,124<br>
LifeCycle observer<br>
aware components.<br>
<br>
154<br>
00:07:26,124 --> 00:07:28,540<br>
It means that you can break<br>
up those really large fragment<br>
<br>
155<br>
00:07:28,540 --> 00:07:31,300<br>
or activity classes to make<br>
them much simpler to understand<br>
<br>
156<br>
00:07:31,300 --> 00:07:32,440<br>
for a reader.<br>
<br>
157<br>
00:07:32,440 --> 00:07:35,200<br>
And you can provide much<br>
more granular guarantees<br>
<br>
158<br>
00:07:35,200 --> 00:07:38,660<br>
around what operations are valid<br>
at any given point in time.<br>
<br>
159<br>
00:07:38,660 --> 00:07:41,860<br>
You can make it so that if<br>
an operation happens then<br>
<br>
160<br>
00:07:41,860 --> 00:07:44,050<br>
you're guaranteed to<br>
be in a correct state<br>
<br>
161<br>
00:07:44,050 --> 00:07:45,130<br>
when something is called.<br>
<br>
162<br>
00:07:45,130 --> 00:07:48,060<br>
<br>
<br>
163<br>
00:07:48,060 --> 00:07:50,685<br>
So LifeCycle owner<br>
as already introduced<br>
<br>
164<br>
00:07:50,685 --> 00:07:51,900<br>
is just an interface.<br>
<br>
165<br>
00:07:51,900 --> 00:07:53,630<br>
Anyone can implement this.<br>
<br>
166<br>
00:07:53,630 --> 00:07:55,680<br>
This means that you<br>
can improve testability<br>
<br>
167<br>
00:07:55,680 --> 00:07:56,802<br>
by creating your own.<br>
<br>
168<br>
00:07:56,802 --> 00:07:59,010<br>
You can create your own sort<br>
of fragment-like library<br>
<br>
169<br>
00:07:59,010 --> 00:08:01,170<br>
implementations if<br>
you feel so inclined.<br>
<br>
170<br>
00:08:01,170 --> 00:08:03,330<br>
But you can also create<br>
composite life cycles.<br>
<br>
171<br>
00:08:03,330 --> 00:08:06,780<br>
Life cycles that span across<br>
other smaller lifecycle<br>
<br>
172<br>
00:08:06,780 --> 00:08:08,010<br>
definitions.<br>
<br>
173<br>
00:08:08,010 --> 00:08:10,710<br>
So you can answer questions<br>
like, is my app visible?<br>
<br>
174<br>
00:08:10,710 --> 00:08:12,750<br>
So this is a really<br>
common composite lifecycle<br>
<br>
175<br>
00:08:12,750 --> 00:08:15,000<br>
that many of you may<br>
be interested in.<br>
<br>
176<br>
00:08:15,000 --> 00:08:17,160<br>
It lets you do things<br>
like session management<br>
<br>
177<br>
00:08:17,160 --> 00:08:19,530<br>
to track a particular<br>
session across perhaps<br>
<br>
178<br>
00:08:19,530 --> 00:08:23,100<br>
some sort of a flow<br>
or a series of logged<br>
<br>
179<br>
00:08:23,100 --> 00:08:24,870<br>
in versus logged out events.<br>
<br>
180<br>
00:08:24,870 --> 00:08:29,020<br>
And it may help you<br>
with analytics as well.<br>
<br>
181<br>
00:08:29,020 --> 00:08:32,280<br>
So we have the process LifeCycle<br>
owner as kind of a component<br>
<br>
182<br>
00:08:32,280 --> 00:08:35,350<br>
that I think a lot of you will<br>
be interested in for this.<br>
<br>
183<br>
00:08:35,350 --> 00:08:39,058<br>
It's the composite lifecycle of<br>
all the activities in your app.<br>
<br>
184<br>
00:08:39,058 --> 00:08:41,009<br>
So there's no configuration<br>
changes to handle,<br>
<br>
185<br>
00:08:41,010 --> 00:08:44,440<br>
because we're not going to be<br>
dealing with those from these.<br>
<br>
186<br>
00:08:44,440 --> 00:08:46,350<br>
The process LifeCycle<br>
owner just stays<br>
<br>
187<br>
00:08:46,350 --> 00:08:48,000<br>
alive through the whole process.<br>
<br>
188<br>
00:08:48,000 --> 00:08:50,041<br>
But that also means that<br>
you don't get state risk<br>
<br>
189<br>
00:08:50,041 --> 00:08:52,660<br>
restoration after process death<br>
like we mentioned earlier.<br>
<br>
190<br>
00:08:52,660 --> 00:08:54,600<br>
So that means that<br>
you don't have<br>
<br>
191<br>
00:08:54,600 --> 00:08:56,905<br>
to handle saving and<br>
restoring that state<br>
<br>
192<br>
00:08:56,905 --> 00:08:59,280<br>
but at the same time, you need<br>
to remember to re-register<br>
<br>
193<br>
00:08:59,280 --> 00:09:02,199<br>
these process lifecycle-based<br>
observers if that's something<br>
<br>
194<br>
00:09:02,199 --> 00:09:03,240<br>
that you're working with.<br>
<br>
195<br>
00:09:03,240 --> 00:09:05,750<br>
<br>
<br>
196<br>
00:09:05,750 --> 00:09:09,110<br>
So many indirect<br>
components provide a lot<br>
<br>
197<br>
00:09:09,110 --> 00:09:11,330<br>
of deep plumbing<br>
layers for things<br>
<br>
198<br>
00:09:11,330 --> 00:09:13,790<br>
that you can plug<br>
into and work with.<br>
<br>
199<br>
00:09:13,790 --> 00:09:15,800<br>
But a lot of times<br>
we've kind of omitted<br>
<br>
200<br>
00:09:15,800 --> 00:09:17,720<br>
the idea of higher<br>
level components that<br>
<br>
201<br>
00:09:17,720 --> 00:09:20,210<br>
make use of that plumbing<br>
so that you can just plug<br>
<br>
202<br>
00:09:20,210 --> 00:09:21,280<br>
play and go.<br>
<br>
203<br>
00:09:21,280 --> 00:09:24,300<br>
So do we have anything more<br>
high level than the bare events<br>
<br>
204<br>
00:09:24,300 --> 00:09:25,530<br>
and states here?<br>
<br>
205<br>
00:09:25,530 --> 00:09:26,800<br>
YIGIT BOYAR: Maybe we do.<br>
<br>
206<br>
00:09:26,800 --> 00:09:27,760<br>
I will show you.<br>
<br>
207<br>
00:09:27,760 --> 00:09:28,870<br>
ADAM POWELL: Great<br>
<br>
208<br>
00:09:28,870 --> 00:09:30,530<br>
YIGIT BOYAR: Thanks, Adam.<br>
<br>
209<br>
00:09:30,530 --> 00:09:33,680<br>
So it's so nice<br>
now you can observe<br>
<br>
210<br>
00:09:33,680 --> 00:09:37,310<br>
a LifeCycle is well-defined,<br>
is a first class citizen.<br>
<br>
211<br>
00:09:37,310 --> 00:09:40,530<br>
But you still need to<br>
deal with these things.<br>
<br>
212<br>
00:09:40,530 --> 00:09:44,780<br>
And we told like, there's<br>
some common LifeCycle problems<br>
<br>
213<br>
00:09:44,780 --> 00:09:47,100<br>
that we should be able to<br>
solve with this component.<br>
<br>
214<br>
00:09:47,100 --> 00:09:48,860<br>
So we'll look at the<br>
problems that people<br>
<br>
215<br>
00:09:48,860 --> 00:09:51,740<br>
are having, and<br>
this was probably<br>
<br>
216<br>
00:09:51,740 --> 00:09:54,110<br>
the most major problem<br>
we've been seeing,<br>
<br>
217<br>
00:09:54,110 --> 00:09:56,320<br>
the untimely UI updates.<br>
<br>
218<br>
00:09:56,320 --> 00:09:58,920<br>
It's like your activity<br>
receives a callback,<br>
<br>
219<br>
00:09:58,920 --> 00:10:00,530<br>
but the activity's<br>
already stopped.<br>
<br>
220<br>
00:10:00,530 --> 00:10:03,050<br>
They tried to start a<br>
new activity and crashes.<br>
<br>
221<br>
00:10:03,050 --> 00:10:06,010<br>
Or it tries to add a<br>
fragment and crashes.<br>
<br>
222<br>
00:10:06,010 --> 00:10:09,410<br>
If an activity or a<br>
fragment is stopped,<br>
<br>
223<br>
00:10:09,410 --> 00:10:12,317<br>
there is no reason to<br>
update that activity.<br>
<br>
224<br>
00:10:12,317 --> 00:10:13,400<br>
You don't want to do that.<br>
<br>
225<br>
00:10:13,400 --> 00:10:16,190<br>
If the activity happens to<br>
become visible again, then<br>
<br>
226<br>
00:10:16,190 --> 00:10:17,480<br>
you want to do it.<br>
<br>
227<br>
00:10:17,480 --> 00:10:20,480<br>
So we realized that this<br>
is a very common problem,<br>
<br>
228<br>
00:10:20,480 --> 00:10:23,990<br>
and we wanted to solve this with<br>
a higher level component which<br>
<br>
229<br>
00:10:23,990 --> 00:10:26,060<br>
we call LiveData.<br>
<br>
230<br>
00:10:26,060 --> 00:10:29,780<br>
When we look at the<br>
LiveData in detail,<br>
<br>
231<br>
00:10:29,780 --> 00:10:32,840<br>
it's actually an<br>
observable data holder.<br>
<br>
232<br>
00:10:32,840 --> 00:10:35,180<br>
It just holds on<br>
to some information<br>
<br>
233<br>
00:10:35,180 --> 00:10:36,490<br>
that you can observe.<br>
<br>
234<br>
00:10:36,490 --> 00:10:38,270<br>
Now the difference<br>
between LiveData<br>
<br>
235<br>
00:10:38,270 --> 00:10:41,225<br>
and your other observables<br>
in data mining or RxJava<br>
<br>
236<br>
00:10:41,225 --> 00:10:45,350<br>
or whatever, is that<br>
LiveData is LifeCycle aware.<br>
<br>
237<br>
00:10:45,350 --> 00:10:48,020<br>
It knows about<br>
Android life cycles,<br>
<br>
238<br>
00:10:48,020 --> 00:10:50,030<br>
and when you want to<br>
observe a LiveData,<br>
<br>
239<br>
00:10:50,030 --> 00:10:52,580<br>
you can pass in this<br>
LifeCycle so that it<br>
<br>
240<br>
00:10:52,580 --> 00:10:54,480<br>
can manage your subscription.<br>
<br>
241<br>
00:10:54,480 --> 00:10:57,210<br>
The nice thing about LiveData<br>
that is that you observe,<br>
<br>
242<br>
00:10:57,210 --> 00:10:59,340<br>
and that's all you do.<br>
<br>
243<br>
00:10:59,340 --> 00:11:00,860<br>
So if we look at<br>
the usage example,<br>
<br>
244<br>
00:11:00,860 --> 00:11:02,210<br>
let's say we have an activity.<br>
<br>
245<br>
00:11:02,210 --> 00:11:04,110<br>
We receive a LiveData<br>
from somewhere.<br>
<br>
246<br>
00:11:04,110 --> 00:11:08,040<br>
It doesn't really matter, and<br>
now we call observe on it.<br>
<br>
247<br>
00:11:08,040 --> 00:11:10,160<br>
And when we are<br>
calling observe, we<br>
<br>
248<br>
00:11:10,160 --> 00:11:13,600<br>
are passing this, which<br>
is the LiveData owner.<br>
<br>
249<br>
00:11:13,600 --> 00:11:14,780<br>
That's all you need to say.<br>
<br>
250<br>
00:11:14,780 --> 00:11:18,770<br>
I want to observe this<br>
LiveData within this LifeCycle.<br>
<br>
251<br>
00:11:18,770 --> 00:11:21,830<br>
Which also means if<br>
this LifeCycle is gone,<br>
<br>
252<br>
00:11:21,830 --> 00:11:23,150<br>
I don't want to observe it.<br>
<br>
253<br>
00:11:23,150 --> 00:11:26,550<br>
Or if this LifeCycle is stopped,<br>
I don't want to receive events.<br>
<br>
254<br>
00:11:26,550 --> 00:11:30,466<br>
<br>
<br>
255<br>
00:11:30,466 --> 00:11:32,340<br>
And then once you do<br>
this, that's all you do.<br>
<br>
256<br>
00:11:32,340 --> 00:11:34,410<br>
You don't need to<br>
write onStart, onStop.<br>
<br>
257<br>
00:11:34,410 --> 00:11:37,870<br>
We want Android to want<br>
to look more like this.<br>
<br>
258<br>
00:11:37,870 --> 00:11:40,040<br>
You initialze things as<br>
more like find and forget.<br>
<br>
259<br>
00:11:40,040 --> 00:11:43,060<br>
You initialize, and you're done.<br>
<br>
260<br>
00:11:43,060 --> 00:11:45,990<br>
So let's look at what happens<br>
when our activity starts<br>
<br>
261<br>
00:11:45,990 --> 00:11:47,910<br>
observing that LiveData.<br>
<br>
262<br>
00:11:47,910 --> 00:11:52,560<br>
So onCreate, it called observe,<br>
it said LiveData is observable.<br>
<br>
263<br>
00:11:52,560 --> 00:11:54,630<br>
And as soon as the<br>
activity starts,<br>
<br>
264<br>
00:11:54,630 --> 00:11:56,470<br>
it starts receiving<br>
data changes.<br>
<br>
265<br>
00:11:56,470 --> 00:11:59,490<br>
So whenever the<br>
LiveData value changes,<br>
<br>
266<br>
00:11:59,490 --> 00:12:01,950<br>
we displace that event<br>
back to your observer<br>
<br>
267<br>
00:12:01,950 --> 00:12:03,530<br>
inside the activity.<br>
<br>
268<br>
00:12:03,530 --> 00:12:05,450<br>
It can also be a fragment.<br>
<br>
269<br>
00:12:05,450 --> 00:12:07,260<br>
Let's say a user<br>
decides to rotate<br>
<br>
270<br>
00:12:07,260 --> 00:12:09,090<br>
the activity at this moment.<br>
<br>
271<br>
00:12:09,090 --> 00:12:11,540<br>
So you know that the<br>
activity will be stopped.<br>
<br>
272<br>
00:12:11,540 --> 00:12:13,320<br>
And what happens<br>
at the same time,<br>
<br>
273<br>
00:12:13,320 --> 00:12:16,110<br>
the LiveData happens<br>
to be updated.<br>
<br>
274<br>
00:12:16,110 --> 00:12:18,990<br>
If that happens, we are not<br>
going to tell the activity<br>
<br>
275<br>
00:12:18,990 --> 00:12:22,590<br>
about this change because there<br>
cannot be any reason for you<br>
<br>
276<br>
00:12:22,590 --> 00:12:27,210<br>
to update the UI, because<br>
it already stopped.<br>
<br>
277<br>
00:12:27,210 --> 00:12:29,640<br>
Similarly, if the<br>
activity is destroyed,<br>
<br>
278<br>
00:12:29,640 --> 00:12:31,980<br>
we will automatically<br>
remove that subscription<br>
<br>
279<br>
00:12:31,980 --> 00:12:34,320<br>
because that activity is gone.<br>
<br>
280<br>
00:12:34,320 --> 00:12:36,990<br>
There is no reason to<br>
keep a reference back<br>
<br>
281<br>
00:12:36,990 --> 00:12:39,240<br>
to that activity.<br>
<br>
282<br>
00:12:39,240 --> 00:12:41,010<br>
Now we said the<br>
activity was rotating,<br>
<br>
283<br>
00:12:41,010 --> 00:12:42,630<br>
so you know that<br>
Android is going<br>
<br>
284<br>
00:12:42,630 --> 00:12:44,880<br>
to recreate that activity.<br>
<br>
285<br>
00:12:44,880 --> 00:12:48,270<br>
And then we are observing<br>
the same LiveData back.<br>
<br>
286<br>
00:12:48,270 --> 00:12:49,985<br>
As soon as that<br>
activity starts, it's<br>
<br>
287<br>
00:12:49,985 --> 00:12:53,190<br>
going to receive<br>
last available data.<br>
<br>
288<br>
00:12:53,190 --> 00:12:57,720<br>
So your UI is going to have the<br>
data before it gets a chance<br>
<br>
289<br>
00:12:57,720 --> 00:12:59,790<br>
to draw.<br>
<br>
290<br>
00:12:59,790 --> 00:13:01,920<br>
So similarly, I<br>
say the user hits<br>
<br>
291<br>
00:13:01,920 --> 00:13:05,330<br>
the Home button, which means<br>
the activity will be stopped.<br>
<br>
292<br>
00:13:05,330 --> 00:13:08,700<br>
Again, if the LiveData changes<br>
while the activity is stopped,<br>
<br>
293<br>
00:13:08,700 --> 00:13:10,840<br>
it's not going to<br>
receive any events.<br>
<br>
294<br>
00:13:10,840 --> 00:13:14,010<br>
Even if the data changes,<br>
we are not going to tell it.<br>
<br>
295<br>
00:13:14,010 --> 00:13:17,280<br>
But as soon as if the user<br>
comes back to the application,<br>
<br>
296<br>
00:13:17,280 --> 00:13:19,510<br>
we will give it the<br>
last available data.<br>
<br>
297<br>
00:13:19,510 --> 00:13:22,990<br>
So this is why we call LiveData<br>
is not just a stream of events.<br>
<br>
298<br>
00:13:22,990 --> 00:13:26,910<br>
It holds onto the data so<br>
that if any observer comes,<br>
<br>
299<br>
00:13:26,910 --> 00:13:30,430<br>
it receives the last<br>
available value.<br>
<br>
300<br>
00:13:30,430 --> 00:13:33,620<br>
And then eventually, the user<br>
backs out of that activity,<br>
<br>
301<br>
00:13:33,620 --> 00:13:37,830<br>
and then we remove<br>
that subscription.<br>
<br>
302<br>
00:13:37,830 --> 00:13:40,730<br>
You can also extend<br>
the LiveData class.<br>
<br>
303<br>
00:13:40,730 --> 00:13:45,950<br>
Because LiveData provides<br>
two really handy callbacks.<br>
<br>
304<br>
00:13:45,950 --> 00:13:48,410<br>
The first one is called<br>
onactive which means<br>
<br>
305<br>
00:13:48,410 --> 00:13:50,930<br>
you have an active observer.<br>
<br>
306<br>
00:13:50,930 --> 00:13:52,580<br>
Another one is<br>
called oninactive,<br>
<br>
307<br>
00:13:52,580 --> 00:13:54,370<br>
which means you don't<br>
have any observers,<br>
<br>
308<br>
00:13:54,370 --> 00:13:56,450<br>
so don't bother<br>
changing your value<br>
<br>
309<br>
00:13:56,450 --> 00:14:00,020<br>
if it is something<br>
that you care about.<br>
<br>
310<br>
00:14:00,020 --> 00:14:03,800<br>
You probably ask now what<br>
is an active observer?<br>
<br>
311<br>
00:14:03,800 --> 00:14:06,220<br>
An active observer<br>
is an observer<br>
<br>
312<br>
00:14:06,220 --> 00:14:09,680<br>
whose attached LifeCycle<br>
is started or resumed.<br>
<br>
313<br>
00:14:09,680 --> 00:14:12,890<br>
So it's like a fragment that's<br>
currently visible to the user.<br>
<br>
314<br>
00:14:12,890 --> 00:14:15,380<br>
If the fragment is<br>
on the back stack,<br>
<br>
315<br>
00:14:15,380 --> 00:14:16,660<br>
the user is not seeing it.<br>
<br>
316<br>
00:14:16,660 --> 00:14:18,260<br>
It stopped, so it's not active.<br>
<br>
317<br>
00:14:18,260 --> 00:14:22,430<br>
There's no reason to do<br>
any work for that fragment.<br>
<br>
318<br>
00:14:22,430 --> 00:14:24,850<br>
Let's see how we can take<br>
advantage of these named<br>
<br>
319<br>
00:14:24,850 --> 00:14:25,770<br>
callbacks.<br>
<br>
320<br>
00:14:25,770 --> 00:14:28,270<br>
We are going to create<br>
a new location LiveData<br>
<br>
321<br>
00:14:28,270 --> 00:14:31,190<br>
class, which presents<br>
the location of something<br>
<br>
322<br>
00:14:31,190 --> 00:14:32,580<br>
on the device.<br>
<br>
323<br>
00:14:32,580 --> 00:14:37,920<br>
So we say this data holds<br>
an instance of a location.<br>
<br>
324<br>
00:14:37,920 --> 00:14:40,460<br>
In cross-sector, we just<br>
get the location manager<br>
<br>
325<br>
00:14:40,460 --> 00:14:41,850<br>
from the system service.<br>
<br>
326<br>
00:14:41,850 --> 00:14:43,670<br>
There's nothing fancy here.<br>
<br>
327<br>
00:14:43,670 --> 00:14:47,210<br>
We have a listener whenever<br>
the system server sends us<br>
<br>
328<br>
00:14:47,210 --> 00:14:50,830<br>
any location, we just<br>
call setValue on us.<br>
<br>
329<br>
00:14:50,830 --> 00:14:51,530<br>
This all you do.<br>
<br>
330<br>
00:14:51,530 --> 00:14:53,460<br>
There is no LifeCycle<br>
handling here.<br>
<br>
331<br>
00:14:53,460 --> 00:14:56,120<br>
You just call setValue,<br>
and LiveData takes<br>
<br>
332<br>
00:14:56,120 --> 00:14:57,710<br>
care of handling the LifeCycle.<br>
<br>
333<br>
00:14:57,710 --> 00:15:00,080<br>
And you may have any<br>
number of observers.<br>
<br>
334<br>
00:15:00,080 --> 00:15:02,450<br>
It doesn't really matter.<br>
<br>
335<br>
00:15:02,450 --> 00:15:04,850<br>
So we want to override onactive.<br>
<br>
336<br>
00:15:04,850 --> 00:15:07,340<br>
The very first active<br>
observer comes.<br>
<br>
337<br>
00:15:07,340 --> 00:15:10,280<br>
We want to start listening<br>
to the system service.<br>
<br>
338<br>
00:15:10,280 --> 00:15:14,300<br>
Similarly, when the last<br>
active observer goes away,<br>
<br>
339<br>
00:15:14,300 --> 00:15:19,140<br>
we want to stop observing<br>
the system service.<br>
<br>
340<br>
00:15:19,140 --> 00:15:21,800<br>
Now if you look at that<br>
location LiveData class<br>
<br>
341<br>
00:15:21,800 --> 00:15:24,020<br>
we just created in the<br>
previous example, let's look<br>
<br>
342<br>
00:15:24,020 --> 00:15:26,210<br>
at the properties of that class.<br>
<br>
343<br>
00:15:26,210 --> 00:15:28,100<br>
First of all, it<br>
is LifeCycle area.<br>
<br>
344<br>
00:15:28,100 --> 00:15:31,280<br>
It knows when to start<br>
itself, when to stop itself.<br>
<br>
345<br>
00:15:31,280 --> 00:15:34,340<br>
You just don't need<br>
to babysit it anymore.<br>
<br>
346<br>
00:15:34,340 --> 00:15:36,110<br>
It is self-sufficient.<br>
<br>
347<br>
00:15:36,110 --> 00:15:37,140<br>
You start it.<br>
<br>
348<br>
00:15:37,140 --> 00:15:39,480<br>
You forget about it.<br>
<br>
349<br>
00:15:39,480 --> 00:15:40,470<br>
It can be a singleton.<br>
<br>
350<br>
00:15:40,470 --> 00:15:42,620<br>
Like all of the subscriptions<br>
are automatically<br>
<br>
351<br>
00:15:42,620 --> 00:15:43,850<br>
managed for you.<br>
<br>
352<br>
00:15:43,850 --> 00:15:47,090<br>
So if the data is logically<br>
singleton your codebase,<br>
<br>
353<br>
00:15:47,090 --> 00:15:50,030<br>
you can make the LiveData<br>
instance singleton.<br>
<br>
354<br>
00:15:50,030 --> 00:15:51,710<br>
So there's this<br>
thing where normally<br>
<br>
355<br>
00:15:51,710 --> 00:15:54,800<br>
if you keep referencing<br>
an activity or a fragment<br>
<br>
356<br>
00:15:54,800 --> 00:15:57,720<br>
from a certain context,<br>
that will be a big no no.<br>
<br>
357<br>
00:15:57,720 --> 00:16:00,350<br>
But if you are using<br>
LiveData it is yes yes,<br>
<br>
358<br>
00:16:00,350 --> 00:16:05,340<br>
because we manage the<br>
substitution for you.<br>
<br>
359<br>
00:16:05,340 --> 00:16:08,550<br>
So you also don't need to<br>
subclass LiveData all the time.<br>
<br>
360<br>
00:16:08,550 --> 00:16:10,910<br>
So if you just need<br>
an instance of it<br>
<br>
361<br>
00:16:10,910 --> 00:16:12,790<br>
but you already<br>
have the value, you<br>
<br>
362<br>
00:16:12,790 --> 00:16:14,990<br>
could use this mutable<br>
LiveData class,<br>
<br>
363<br>
00:16:14,990 --> 00:16:18,770<br>
which comes inside the library<br>
that has a public setter.<br>
<br>
364<br>
00:16:18,770 --> 00:16:21,170<br>
But usually when you<br>
are using this class,<br>
<br>
365<br>
00:16:21,170 --> 00:16:24,530<br>
internally you will have<br>
it but the API you expose<br>
<br>
366<br>
00:16:24,530 --> 00:16:26,360<br>
will just return a<br>
LiveData, because you<br>
<br>
367<br>
00:16:26,360 --> 00:16:28,370<br>
don't want to expose<br>
the fact that anyone<br>
<br>
368<br>
00:16:28,370 --> 00:16:31,470<br>
can set the value on it.<br>
<br>
369<br>
00:16:31,470 --> 00:16:34,920<br>
Now when we were designing<br>
these LifeCycle components,<br>
<br>
370<br>
00:16:34,920 --> 00:16:38,730<br>
the LiveData, see we<br>
spent a lot of time<br>
<br>
371<br>
00:16:38,730 --> 00:16:41,380<br>
to get rid of one exception.<br>
<br>
372<br>
00:16:41,380 --> 00:16:43,350<br>
This fragment exception that I--<br>
<br>
373<br>
00:16:43,350 --> 00:16:50,520<br>
[APPLAUSE]<br>
<br>
374<br>
00:16:50,520 --> 00:16:54,350<br>
We really wanted to say, please,<br>
no more fragment transaction<br>
<br>
375<br>
00:16:54,350 --> 00:16:55,460<br>
exceptions.<br>
<br>
376<br>
00:16:55,460 --> 00:16:58,570<br>
So LiveData guarantees that<br>
if you received anywhere,<br>
<br>
377<br>
00:16:58,570 --> 00:17:00,910<br>
you could run a<br>
fragment transaction.<br>
<br>
378<br>
00:17:00,910 --> 00:17:05,310<br>
And to see how we are making<br>
it part of the history,<br>
<br>
379<br>
00:17:05,310 --> 00:17:10,118<br>
I want to invite Adam<br>
back to explain it to us.<br>
<br>
380<br>
00:17:10,118 --> 00:17:11,539<br>
ADAM POWELL: All<br>
right, so anyone<br>
<br>
381<br>
00:17:11,540 --> 00:17:13,205<br>
who has received one<br>
of these exceptions<br>
<br>
382<br>
00:17:13,205 --> 00:17:15,289<br>
realizes that it<br>
doesn't just come<br>
<br>
383<br>
00:17:15,290 --> 00:17:18,710<br>
from trying to do something<br>
when you just completely stopped<br>
<br>
384<br>
00:17:18,710 --> 00:17:20,348<br>
and you absolutely know it.<br>
<br>
385<br>
00:17:20,348 --> 00:17:21,889<br>
These exceptions<br>
tend to come in when<br>
<br>
386<br>
00:17:21,890 --> 00:17:26,010<br>
you get into very intricate,<br>
nested life cycles.<br>
<br>
387<br>
00:17:26,010 --> 00:17:28,910<br>
So we wanted to make sure to be<br>
very thoughtful about defining<br>
<br>
388<br>
00:17:28,910 --> 00:17:34,190<br>
how the LifeCycle observer<br>
callbacks are invoked and when.<br>
<br>
389<br>
00:17:34,190 --> 00:17:37,400<br>
So in a case like<br>
this, what happens?<br>
<br>
390<br>
00:17:37,400 --> 00:17:42,120<br>
You have defined handler<br>
for the stop event.<br>
<br>
391<br>
00:17:42,120 --> 00:17:44,872<br>
So in the container<br>
your activity onStop,<br>
<br>
392<br>
00:17:44,872 --> 00:17:47,330<br>
you want to make sure that you<br>
don't get an onChanged event<br>
<br>
393<br>
00:17:47,330 --> 00:17:48,770<br>
after the onStop has happened.<br>
<br>
394<br>
00:17:48,770 --> 00:17:52,660<br>
<br>
<br>
395<br>
00:17:52,660 --> 00:17:54,570<br>
But in order for<br>
that to happen, what<br>
<br>
396<br>
00:17:54,570 --> 00:17:56,490<br>
needs to be true<br>
about when we actually<br>
<br>
397<br>
00:17:56,490 --> 00:18:00,030<br>
invoke all of the<br>
onStop listeners<br>
<br>
398<br>
00:18:00,030 --> 00:18:02,610<br>
that are attached<br>
to these observers.<br>
<br>
399<br>
00:18:02,610 --> 00:18:05,770<br>
So we have to define a<br>
really strict order for this.<br>
<br>
400<br>
00:18:05,770 --> 00:18:09,420<br>
So as we go through create<br>
and start and onResume,<br>
<br>
401<br>
00:18:09,420 --> 00:18:11,940<br>
we know that we need<br>
to invoke the LifeCycle<br>
<br>
402<br>
00:18:11,940 --> 00:18:15,480<br>
observers after the<br>
container event happens.<br>
<br>
403<br>
00:18:15,480 --> 00:18:18,090<br>
So you know in your<br>
observer that everything<br>
<br>
404<br>
00:18:18,090 --> 00:18:20,461<br>
about your LifeCycle<br>
owner has been configured.<br>
<br>
405<br>
00:18:20,461 --> 00:18:21,960<br>
If you check any<br>
state about it, you<br>
<br>
406<br>
00:18:21,960 --> 00:18:25,397<br>
know that you're already<br>
completely in that state.<br>
<br>
407<br>
00:18:25,397 --> 00:18:27,480<br>
But that means something<br>
really special for coming<br>
<br>
408<br>
00:18:27,480 --> 00:18:29,470<br>
back down the other direction.<br>
<br>
409<br>
00:18:29,470 --> 00:18:33,540<br>
It means that when the activity<br>
starts to become paused,<br>
<br>
410<br>
00:18:33,540 --> 00:18:34,995<br>
you want your<br>
LifeCycle observers<br>
<br>
411<br>
00:18:34,995 --> 00:18:36,870<br>
to be able to shut down<br>
anything that they're<br>
<br>
412<br>
00:18:36,870 --> 00:18:39,060<br>
doing before the activity<br>
does all of the work<br>
<br>
413<br>
00:18:39,060 --> 00:18:41,400<br>
to actually become paused.<br>
<br>
414<br>
00:18:41,400 --> 00:18:42,810<br>
Similar for stop.<br>
<br>
415<br>
00:18:42,810 --> 00:18:44,850<br>
And this is where<br>
this becomes really<br>
<br>
416<br>
00:18:44,850 --> 00:18:47,220<br>
important for the fragment<br>
transaction exception.<br>
<br>
417<br>
00:18:47,220 --> 00:18:49,260<br>
You want to make<br>
sure that you're<br>
<br>
418<br>
00:18:49,260 --> 00:18:52,440<br>
recording, that you're fully<br>
stopped before the fragment<br>
<br>
419<br>
00:18:52,440 --> 00:18:54,600<br>
system goes through<br>
and flags everything<br>
<br>
420<br>
00:18:54,600 --> 00:18:58,180<br>
as being completely locked out.<br>
<br>
421<br>
00:18:58,180 --> 00:19:01,410<br>
So what that means is that the<br>
stop event of your LifeCycle<br>
<br>
422<br>
00:19:01,410 --> 00:19:04,770<br>
observer will always be invoked<br>
before the activity onStop<br>
<br>
423<br>
00:19:04,770 --> 00:19:10,710<br>
or before the full stop event<br>
for your container happens.<br>
<br>
424<br>
00:19:10,710 --> 00:19:13,260<br>
So this seems really similar<br>
to some other libraries<br>
<br>
425<br>
00:19:13,260 --> 00:19:15,480<br>
that some people may<br>
have seen in the past.<br>
<br>
426<br>
00:19:15,480 --> 00:19:16,600<br>
Can you talk about that?<br>
<br>
427<br>
00:19:16,600 --> 00:19:22,530<br>
SERGEI VASILINETC: Yes, when we<br>
create new observable pattern,<br>
<br>
428<br>
00:19:22,530 --> 00:19:26,220<br>
nowadays this question<br>
is unavoidable.<br>
<br>
429<br>
00:19:26,220 --> 00:19:29,220<br>
Is it another RxJava?<br>
<br>
430<br>
00:19:29,220 --> 00:19:32,490<br>
And the answer to<br>
this question is, yes,<br>
<br>
431<br>
00:19:32,490 --> 00:19:34,740<br>
because we want to promote<br>
a reactive programming<br>
<br>
432<br>
00:19:34,740 --> 00:19:37,980<br>
model, especially when it<br>
comes to the relationship<br>
<br>
433<br>
00:19:37,980 --> 00:19:40,710<br>
between your UI and the<br>
state [INAUDIBLE] UI.<br>
<br>
434<br>
00:19:40,710 --> 00:19:45,490<br>
We want you to react on<br>
the changes of the state.<br>
<br>
435<br>
00:19:45,490 --> 00:19:48,300<br>
So it means that it's a<br>
reactive programming model.<br>
<br>
436<br>
00:19:48,300 --> 00:19:51,000<br>
But on the other hand, no.<br>
<br>
437<br>
00:19:51,000 --> 00:19:54,840<br>
Because it's the LifeCycle<br>
aware out of box,<br>
<br>
438<br>
00:19:54,840 --> 00:19:57,930<br>
as Yigit mentioned,<br>
and it's much easier.<br>
<br>
439<br>
00:19:57,930 --> 00:20:02,940<br>
As many of you may know,<br>
the learning curve of RxJava<br>
<br>
440<br>
00:20:02,940 --> 00:20:04,560<br>
is super steep.<br>
<br>
441<br>
00:20:04,560 --> 00:20:08,850<br>
And if you have an<br>
Android learner curve,<br>
<br>
442<br>
00:20:08,850 --> 00:20:13,350<br>
and after that we add RxJava<br>
learning curve on top of it,<br>
<br>
443<br>
00:20:13,350 --> 00:20:16,050<br>
it becomes very<br>
hard to new people<br>
<br>
444<br>
00:20:16,050 --> 00:20:19,420<br>
to start to develop<br>
on our platform.<br>
<br>
445<br>
00:20:19,420 --> 00:20:25,890<br>
So we can't just say to them,<br>
oh let's go, just learn this,<br>
<br>
446<br>
00:20:25,890 --> 00:20:27,330<br>
that's it. .<br>
<br>
447<br>
00:20:27,330 --> 00:20:32,310<br>
No, but if you already<br>
learned RxJava,<br>
<br>
448<br>
00:20:32,310 --> 00:20:37,020<br>
we don't expect you to migrate<br>
from it to our solution.<br>
<br>
449<br>
00:20:37,020 --> 00:20:41,280<br>
Because you already<br>
passed the learning curve,<br>
<br>
450<br>
00:20:41,280 --> 00:20:45,960<br>
you and your coworkers are<br>
comfortable with it, fine.<br>
<br>
451<br>
00:20:45,960 --> 00:20:48,190<br>
We are totally fine with this.<br>
<br>
452<br>
00:20:48,190 --> 00:20:51,330<br>
But one thing we ask<br>
you to do is to be sure<br>
<br>
453<br>
00:20:51,330 --> 00:20:53,920<br>
that you manage LifeCycle.<br>
<br>
454<br>
00:20:53,920 --> 00:20:58,210<br>
RxJava has common<br>
approaches to solve this.<br>
<br>
455<br>
00:20:58,210 --> 00:21:02,430<br>
Be sure to use it and<br>
everything will be fine.<br>
<br>
456<br>
00:21:02,430 --> 00:21:09,885<br>
But when you start a new app,<br>
I think this model is the best.<br>
<br>
457<br>
00:21:09,885 --> 00:21:15,010<br>
The best is to start the project<br>
with LiveData, because it's<br>
<br>
458<br>
00:21:15,010 --> 00:21:17,310<br>
simpler, it's faster,<br>
it's lightweight,<br>
<br>
459<br>
00:21:17,310 --> 00:21:20,270<br>
it's well integrated<br>
with a framework.<br>
<br>
460<br>
00:21:20,270 --> 00:21:24,970<br>
And if you feel like you love<br>
reacting programming a lot,<br>
<br>
461<br>
00:21:24,970 --> 00:21:28,480<br>
you want to bring it<br>
not only to relation<br>
<br>
462<br>
00:21:28,480 --> 00:21:31,930<br>
between UI and the state.<br>
<br>
463<br>
00:21:31,930 --> 00:21:33,430<br>
You want to bring<br>
it to the business<br>
<br>
464<br>
00:21:33,430 --> 00:21:36,340<br>
part of your application.<br>
<br>
465<br>
00:21:36,340 --> 00:21:41,070<br>
Then you may consider<br>
the addition of RxJava,<br>
<br>
466<br>
00:21:41,070 --> 00:21:44,230<br>
because it gives you more power.<br>
<br>
467<br>
00:21:44,230 --> 00:21:47,140<br>
And we will actually<br>
help you to do that.<br>
<br>
468<br>
00:21:47,140 --> 00:21:51,790<br>
We have this extension<br>
to our library, which<br>
<br>
469<br>
00:21:51,790 --> 00:21:55,780<br>
gives a possibility to create<br>
LiveData from Publisher<br>
<br>
470<br>
00:21:55,780 --> 00:21:58,930<br>
and create Publisher<br>
from LiveData.<br>
<br>
471<br>
00:21:58,930 --> 00:22:03,970<br>
So this integration<br>
should be quite smooth.<br>
<br>
472<br>
00:22:03,970 --> 00:22:07,330<br>
But I want to highlight a<br>
key difference between RxJava<br>
<br>
473<br>
00:22:07,330 --> 00:22:08,080<br>
and LiveData.<br>
<br>
474<br>
00:22:08,080 --> 00:22:11,980<br>
So as Yigit already<br>
said, LiveData<br>
<br>
475<br>
00:22:11,980 --> 00:22:13,870<br>
is a holder and not a stream.<br>
<br>
476<br>
00:22:13,870 --> 00:22:17,320<br>
So we have a reference<br>
to the last value,<br>
<br>
477<br>
00:22:17,320 --> 00:22:20,290<br>
and observers immediately<br>
receive the last value when<br>
<br>
478<br>
00:22:20,290 --> 00:22:24,820<br>
they start to observe LiveData.<br>
<br>
479<br>
00:22:24,820 --> 00:22:27,550<br>
And now the big difference<br>
is a threading model.<br>
<br>
480<br>
00:22:27,550 --> 00:22:31,840<br>
As you know, RxJava has a very<br>
sophisticated threading model.<br>
<br>
481<br>
00:22:31,840 --> 00:22:35,390<br>
It's extremely powerful,<br>
but in most cases,<br>
<br>
482<br>
00:22:35,390 --> 00:22:37,610<br>
you probably don't need it.<br>
<br>
483<br>
00:22:37,610 --> 00:22:40,360<br>
And we have everything<br>
on the main thread.<br>
<br>
484<br>
00:22:40,360 --> 00:22:42,190<br>
And the reason for<br>
this is we want<br>
<br>
485<br>
00:22:42,190 --> 00:22:47,150<br>
to give you all these guarantees<br>
about when we will notify you<br>
<br>
486<br>
00:22:47,150 --> 00:22:50,740<br>
about state changes.<br>
<br>
487<br>
00:22:50,740 --> 00:22:56,200<br>
And we can't do this<br>
on a background thread.<br>
<br>
488<br>
00:22:56,200 --> 00:22:58,330<br>
We have just the one exception.<br>
<br>
489<br>
00:22:58,330 --> 00:23:00,850<br>
We have a post<br>
value method which<br>
<br>
490<br>
00:23:00,850 --> 00:23:03,720<br>
just is a method<br>
which trampoline value<br>
<br>
491<br>
00:23:03,720 --> 00:23:07,725<br>
from a background thread to the<br>
main thread and sets it there.<br>
<br>
492<br>
00:23:07,725 --> 00:23:08,770<br>
It's super simple.<br>
<br>
493<br>
00:23:08,770 --> 00:23:11,400<br>
So quick summary of what<br>
we have at this point.<br>
<br>
494<br>
00:23:11,400 --> 00:23:13,870<br>
LiveData events,<br>
observable pattern<br>
<br>
495<br>
00:23:13,870 --> 00:23:16,460<br>
which respects these events.<br>
<br>
496<br>
00:23:16,460 --> 00:23:20,090<br>
But there is one big thing<br>
which is not covered yet.<br>
<br>
497<br>
00:23:20,090 --> 00:23:23,590<br>
And this is how to handle<br>
onConfigurationChanges.<br>
<br>
498<br>
00:23:23,590 --> 00:23:28,690<br>
In 2017, almost nine<br>
years after Android<br>
<br>
499<br>
00:23:28,690 --> 00:23:32,050<br>
was first time released, we<br>
still discuss this question.<br>
<br>
500<br>
00:23:32,050 --> 00:23:34,090<br>
And this is a totally<br>
legit question.<br>
<br>
501<br>
00:23:34,090 --> 00:23:38,290<br>
And we hear it constantly<br>
from new Android developers.<br>
<br>
502<br>
00:23:38,290 --> 00:23:40,730<br>
Many of you probably know<br>
whats the deal with it.<br>
<br>
503<br>
00:23:40,730 --> 00:23:44,770<br>
But let's take a look at<br>
this oversimplified example,<br>
<br>
504<br>
00:23:44,770 --> 00:23:47,830<br>
but it's still very vivid.<br>
<br>
505<br>
00:23:47,830 --> 00:23:50,050<br>
So he wants to show<br>
this information<br>
<br>
506<br>
00:23:50,050 --> 00:23:52,060<br>
about user and your activity.<br>
<br>
507<br>
00:23:52,060 --> 00:23:54,830<br>
And you want to make<br>
some web service request.<br>
<br>
508<br>
00:23:54,830 --> 00:24:00,340<br>
We will use LiveData to get<br>
this result. It's super simple.<br>
<br>
509<br>
00:24:00,340 --> 00:24:02,800<br>
When the request is just<br>
started, it's empty.<br>
<br>
510<br>
00:24:02,800 --> 00:24:06,620<br>
When the request<br>
response is received,<br>
<br>
511<br>
00:24:06,620 --> 00:24:11,740<br>
we put it to<br>
LiveData as a value.<br>
<br>
512<br>
00:24:11,740 --> 00:24:14,070<br>
And later we'll update our UI.<br>
<br>
513<br>
00:24:14,070 --> 00:24:19,917<br>
We will notify the activity, and<br>
it will do everything it needs.<br>
<br>
514<br>
00:24:19,917 --> 00:24:22,250<br>
So what happens if the activity<br>
is going to [INAUDIBLE].<br>
<br>
515<br>
00:24:22,250 --> 00:24:25,750<br>
We're going to<br>
make a call twice,<br>
<br>
516<br>
00:24:25,750 --> 00:24:28,560<br>
and I hope that you don't<br>
call web service right<br>
<br>
517<br>
00:24:28,560 --> 00:24:29,740<br>
into your activity.<br>
<br>
518<br>
00:24:29,740 --> 00:24:33,670<br>
But you probably have<br>
some abstractions<br>
<br>
519<br>
00:24:33,670 --> 00:24:36,010<br>
that does something<br>
like that, which<br>
<br>
520<br>
00:24:36,010 --> 00:24:41,040<br>
goes to a network, which goes<br>
to caching and persistence<br>
<br>
521<br>
00:24:41,040 --> 00:24:43,030<br>
storages.<br>
<br>
522<br>
00:24:43,030 --> 00:24:47,170<br>
And all the separations<br>
are synchronized by nature.<br>
<br>
523<br>
00:24:47,170 --> 00:24:51,070<br>
So communication of these<br>
components are synchronized.<br>
<br>
524<br>
00:24:51,070 --> 00:24:55,510<br>
And you probably don't want to<br>
make these calls twice anyway.<br>
<br>
525<br>
00:24:55,510 --> 00:24:58,060<br>
So what you want<br>
to do is to cache.<br>
<br>
526<br>
00:24:58,060 --> 00:25:01,470<br>
This is our data,<br>
like in our example.<br>
<br>
527<br>
00:25:01,470 --> 00:25:04,480<br>
And what are the ways<br>
today to do that?<br>
<br>
528<br>
00:25:04,480 --> 00:25:06,960<br>
Well, one of a<br>
proposed way to do it<br>
<br>
529<br>
00:25:06,960 --> 00:25:10,570<br>
is a Fragment.setRetainInstance,<br>
and Yigit<br>
<br>
530<br>
00:25:10,570 --> 00:25:12,340<br>
can rant about this for hours.<br>
<br>
531<br>
00:25:12,340 --> 00:25:14,770<br>
Unfortunately, we don't<br>
have time for this today.<br>
<br>
532<br>
00:25:14,770 --> 00:25:17,600<br>
But I just say that<br>
the only effect<br>
<br>
533<br>
00:25:17,600 --> 00:25:19,900<br>
that you have to run<br>
fragment transaction<br>
<br>
534<br>
00:25:19,900 --> 00:25:22,400<br>
is terrifying for<br>
a lot of people.<br>
<br>
535<br>
00:25:22,400 --> 00:25:25,780<br>
People go nuts and<br>
another possible way<br>
<br>
536<br>
00:25:25,780 --> 00:25:29,960<br>
to solve this is loaders, but<br>
we don't fit here well as well.<br>
<br>
537<br>
00:25:29,960 --> 00:25:33,010<br>
So we decided to tackle<br>
this problem once again<br>
<br>
538<br>
00:25:33,010 --> 00:25:35,230<br>
and create ViewModel.<br>
<br>
539<br>
00:25:35,230 --> 00:25:36,030<br>
So what is this?<br>
<br>
540<br>
00:25:36,030 --> 00:25:39,070<br>
ViewModel is an object<br>
which is associated<br>
<br>
541<br>
00:25:39,070 --> 00:25:41,440<br>
with a fragment or an<br>
activity, but is retained<br>
<br>
542<br>
00:25:41,440 --> 00:25:43,750<br>
during configuration changes.<br>
<br>
543<br>
00:25:43,750 --> 00:25:48,190<br>
So its scope is a kind of a<br>
logical scope of your activity.<br>
<br>
544<br>
00:25:48,190 --> 00:25:51,300<br>
So what does this mean?<br>
<br>
545<br>
00:25:51,300 --> 00:25:51,900<br>
Let's see.<br>
<br>
546<br>
00:25:51,900 --> 00:25:54,220<br>
If we have access time and<br>
the current moment, and we<br>
<br>
547<br>
00:25:54,220 --> 00:25:55,540<br>
can predict the future.<br>
<br>
548<br>
00:25:55,540 --> 00:25:57,670<br>
And we know that activity<br>
is going to be created,<br>
<br>
549<br>
00:25:57,670 --> 00:25:59,390<br>
and this means that<br>
all construction<br>
<br>
550<br>
00:25:59,390 --> 00:26:01,690<br>
events are going to happen.<br>
<br>
551<br>
00:26:01,690 --> 00:26:05,440<br>
During onCreate we will request<br>
ViewModel for the first time.<br>
<br>
552<br>
00:26:05,440 --> 00:26:07,780<br>
We will create it, and<br>
after that this activity<br>
<br>
553<br>
00:26:07,780 --> 00:26:10,850<br>
just uses this ViewModel.<br>
<br>
554<br>
00:26:10,850 --> 00:26:12,220<br>
Very simple.<br>
<br>
555<br>
00:26:12,220 --> 00:26:16,060<br>
Now we predict that the<br>
activity is going to be rotated.<br>
<br>
556<br>
00:26:16,060 --> 00:26:20,700<br>
Let's see what's going to<br>
happen with our ViewModel.<br>
<br>
557<br>
00:26:20,700 --> 00:26:27,400<br>
We will receive events,<br>
onPause, onStop, and onDestroy.<br>
<br>
558<br>
00:26:27,400 --> 00:26:30,880<br>
But when all the<br>
segments are cured<br>
<br>
559<br>
00:26:30,880 --> 00:26:34,090<br>
and your activity is<br>
destroyed, it's thrown away<br>
<br>
560<br>
00:26:34,090 --> 00:26:38,210<br>
and is garbage collected,<br>
ViewModel survived it.<br>
<br>
561<br>
00:26:38,210 --> 00:26:42,070<br>
And the new activity, which was<br>
created in place the old one<br>
<br>
562<br>
00:26:42,070 --> 00:26:44,510<br>
uses the same, old object.<br>
<br>
563<br>
00:26:44,510 --> 00:26:48,520<br>
So you can easily cache<br>
there LiveData as we want to<br>
<br>
564<br>
00:26:48,520 --> 00:26:50,690<br>
or something else.<br>
<br>
565<br>
00:26:50,690 --> 00:26:52,720<br>
The last case, what<br>
is going to happen<br>
<br>
566<br>
00:26:52,720 --> 00:26:55,600<br>
if you have finished goal?<br>
<br>
567<br>
00:26:55,600 --> 00:26:58,280<br>
Once again, we will receive<br>
these destruction events,<br>
<br>
568<br>
00:26:58,280 --> 00:27:01,570<br>
but this time,<br>
ViewModel is available<br>
<br>
569<br>
00:27:01,570 --> 00:27:03,130<br>
until onDestroy method.<br>
<br>
570<br>
00:27:03,130 --> 00:27:08,340<br>
During onDestroy method, we<br>
will call onClear on this.<br>
<br>
571<br>
00:27:08,340 --> 00:27:11,860<br>
Which notifies you if you have<br>
any currently running actions<br>
<br>
572<br>
00:27:11,860 --> 00:27:15,610<br>
or any resources<br>
its time to close.<br>
<br>
573<br>
00:27:15,610 --> 00:27:18,900<br>
And after that, it's<br>
going to be destroyed<br>
<br>
574<br>
00:27:18,900 --> 00:27:20,150<br>
and garbage collected as well.<br>
<br>
575<br>
00:27:20,150 --> 00:27:24,310<br>
So at the point when your<br>
activity is destroyed,<br>
<br>
576<br>
00:27:24,310 --> 00:27:27,340<br>
it's not going to be<br>
recreated it again.<br>
<br>
577<br>
00:27:27,340 --> 00:27:30,980<br>
Your ViewModel is gone as well.<br>
<br>
578<br>
00:27:30,980 --> 00:27:37,970<br>
So let's quickly make<br>
our sample in ViewModel.<br>
<br>
579<br>
00:27:37,970 --> 00:27:40,900<br>
So it starts with<br>
instantiating-- with creation<br>
<br>
580<br>
00:27:40,900 --> 00:27:43,270<br>
of ViewModel class.<br>
<br>
581<br>
00:27:43,270 --> 00:27:47,860<br>
We want to cache for user data<br>
to create a fill for that.<br>
<br>
582<br>
00:27:47,860 --> 00:27:50,680<br>
We agree our activity needs<br>
to access this LiveData,<br>
<br>
583<br>
00:27:50,680 --> 00:27:52,450<br>
so we create a getter for this.<br>
<br>
584<br>
00:27:52,450 --> 00:27:55,960<br>
And finally, getter is<br>
extremely straightforward.<br>
<br>
585<br>
00:27:55,960 --> 00:27:59,530<br>
If we already requested the<br>
data, we just return it.<br>
<br>
586<br>
00:27:59,530 --> 00:28:04,780<br>
If the data is now, we'll<br>
request it from a web service<br>
<br>
587<br>
00:28:04,780 --> 00:28:06,580<br>
and return it.<br>
<br>
588<br>
00:28:06,580 --> 00:28:07,422<br>
Fine.<br>
<br>
589<br>
00:28:07,422 --> 00:28:08,880<br>
We had [INAUDIBLE]<br>
on our activity.<br>
<br>
590<br>
00:28:08,880 --> 00:28:12,580<br>
Now we need to get this<br>
LiveData from ViewModel.<br>
<br>
591<br>
00:28:12,580 --> 00:28:18,370<br>
To get it, we need to create<br>
to get ViewModel somehow.<br>
<br>
592<br>
00:28:18,370 --> 00:28:19,450<br>
So this is how we do it.<br>
<br>
593<br>
00:28:19,450 --> 00:28:21,970<br>
Let's take a precise look at it.<br>
<br>
594<br>
00:28:21,970 --> 00:28:25,000<br>
First of all, we need to get<br>
ViewModel provider object.<br>
<br>
595<br>
00:28:25,000 --> 00:28:27,250<br>
This is an object<br>
which is associated<br>
<br>
596<br>
00:28:27,250 --> 00:28:28,570<br>
with a fragment or an activity.<br>
<br>
597<br>
00:28:28,570 --> 00:28:34,270<br>
It knows how to get already<br>
existing ViewModel from it<br>
<br>
598<br>
00:28:34,270 --> 00:28:36,740<br>
or how to create a new one.<br>
<br>
599<br>
00:28:36,740 --> 00:28:39,250<br>
If there is no<br>
existing ViewModel.<br>
<br>
600<br>
00:28:39,250 --> 00:28:44,650<br>
After that, we request<br>
our myActivity ViewModel,<br>
<br>
601<br>
00:28:44,650 --> 00:28:48,617<br>
and later everything<br>
is quite simple.<br>
<br>
602<br>
00:28:48,617 --> 00:28:49,450<br>
We get the userData.<br>
<br>
603<br>
00:28:49,450 --> 00:28:54,730<br>
We observe it to update the UI.<br>
<br>
604<br>
00:28:54,730 --> 00:28:59,860<br>
So what are the rules<br>
of usage of ViewModel?<br>
<br>
605<br>
00:28:59,860 --> 00:29:04,660<br>
So ViewModel manages<br>
the data for the UI.<br>
<br>
606<br>
00:29:04,660 --> 00:29:08,290<br>
It means that it<br>
speaks with business<br>
<br>
607<br>
00:29:08,290 --> 00:29:11,510<br>
parts of your application<br>
to retrieve the data.<br>
<br>
608<br>
00:29:11,510 --> 00:29:15,470<br>
So it may be a repository<br>
pattern or any other pattern<br>
<br>
609<br>
00:29:15,470 --> 00:29:17,890<br>
that they use.<br>
<br>
610<br>
00:29:17,890 --> 00:29:22,450<br>
It also, it's for its<br>
user modifications<br>
<br>
611<br>
00:29:22,450 --> 00:29:24,140<br>
back to these components.<br>
<br>
612<br>
00:29:24,140 --> 00:29:26,720<br>
And now a good<br>
case for ViewModel<br>
<br>
613<br>
00:29:26,720 --> 00:29:30,730<br>
is acting as a communication<br>
layer between fragments<br>
<br>
614<br>
00:29:30,730 --> 00:29:32,530<br>
in one activity.<br>
<br>
615<br>
00:29:32,530 --> 00:29:36,490<br>
And Yigit will speak<br>
about this later.<br>
<br>
616<br>
00:29:36,490 --> 00:29:40,840<br>
But prior to this,<br>
things that you must not<br>
<br>
617<br>
00:29:40,840 --> 00:29:42,560<br>
do in your ViewModel.<br>
<br>
618<br>
00:29:42,560 --> 00:29:46,580<br>
So first of all,<br>
you must not access<br>
<br>
619<br>
00:29:46,580 --> 00:29:51,870<br>
views and any other<br>
UI- related entities.<br>
<br>
620<br>
00:29:51,870 --> 00:29:54,670<br>
The reason for<br>
that, they are going<br>
<br>
621<br>
00:29:54,670 --> 00:29:57,010<br>
to be created during<br>
configuration change.<br>
<br>
622<br>
00:29:57,010 --> 00:30:02,400<br>
If you try to use them, you will<br>
ever use stale data from there,<br>
<br>
623<br>
00:30:02,400 --> 00:30:05,250<br>
ever to leak them.<br>
<br>
624<br>
00:30:05,250 --> 00:30:09,230<br>
That's going to finish bad.<br>
<br>
625<br>
00:30:09,230 --> 00:30:12,280<br>
And it's fragmented<br>
or activity's job<br>
<br>
626<br>
00:30:12,280 --> 00:30:17,110<br>
to bind the data which you<br>
will get from a ViewModel<br>
<br>
627<br>
00:30:17,110 --> 00:30:21,260<br>
with actual UI,<br>
text use, buttons.<br>
<br>
628<br>
00:30:21,260 --> 00:30:23,190<br>
I don't know what else.<br>
<br>
629<br>
00:30:23,190 --> 00:30:26,590<br>
And one more thing,<br>
there are sources<br>
<br>
630<br>
00:30:26,590 --> 00:30:31,120<br>
which sound more harmless<br>
like strings or drawable,<br>
<br>
631<br>
00:30:31,120 --> 00:30:33,790<br>
and you may think,<br>
I may cash it here.<br>
<br>
632<br>
00:30:33,790 --> 00:30:38,020<br>
No, they depend on current<br>
configuration state of state<br>
<br>
633<br>
00:30:38,020 --> 00:30:38,800<br>
as well.<br>
<br>
634<br>
00:30:38,800 --> 00:30:43,360<br>
So yes, right now you may<br>
have just one resource<br>
<br>
635<br>
00:30:43,360 --> 00:30:46,540<br>
for every configuration,<br>
but later, you<br>
<br>
636<br>
00:30:46,540 --> 00:30:49,870<br>
will add in the same resource<br>
for a different configuration.<br>
<br>
637<br>
00:30:49,870 --> 00:30:54,010<br>
You will easily forget<br>
to update your ViewModel.<br>
<br>
638<br>
00:30:54,010 --> 00:30:58,540<br>
And you may not notice<br>
this, but your users<br>
<br>
639<br>
00:30:58,540 --> 00:31:00,250<br>
will see the invalid UI.<br>
<br>
640<br>
00:31:00,250 --> 00:31:02,230<br>
And this is just ugly.<br>
<br>
641<br>
00:31:02,230 --> 00:31:06,970<br>
And now Yigit will speak about<br>
Inter Fragment communications.<br>
<br>
642<br>
00:31:06,970 --> 00:31:10,510<br>
<br>
<br>
643<br>
00:31:10,510 --> 00:31:12,270<br>
YIGIT BOYAR: So I<br>
want to talk about one<br>
<br>
644<br>
00:31:12,270 --> 00:31:16,050<br>
of my favorite features<br>
about ViewModel,<br>
<br>
645<br>
00:31:16,050 --> 00:31:19,020<br>
which is communicating<br>
between multiple fragments<br>
<br>
646<br>
00:31:19,020 --> 00:31:21,980<br>
of the same activity.<br>
<br>
647<br>
00:31:21,980 --> 00:31:25,200<br>
It's good that UI like this,<br>
like the Gmail on the tablet<br>
<br>
648<br>
00:31:25,200 --> 00:31:29,500<br>
where on the left side you pick<br>
an email and on the right side,<br>
<br>
649<br>
00:31:29,500 --> 00:31:31,860<br>
it shows the contents<br>
of the email.<br>
<br>
650<br>
00:31:31,860 --> 00:31:34,560<br>
Now usually you will<br>
implement this as a fragment<br>
<br>
651<br>
00:31:34,560 --> 00:31:37,940<br>
on the left which picks<br>
something from the list,<br>
<br>
652<br>
00:31:37,940 --> 00:31:39,780<br>
and another fragment<br>
on the right, which<br>
<br>
653<br>
00:31:39,780 --> 00:31:42,960<br>
shows how to show the<br>
contents of an email<br>
<br>
654<br>
00:31:42,960 --> 00:31:45,330<br>
so that if you're on the<br>
phone you can reuse the same<br>
<br>
655<br>
00:31:45,330 --> 00:31:48,150<br>
fragments but separate<br>
from each other.<br>
<br>
656<br>
00:31:48,150 --> 00:31:52,170<br>
Now if you ever tried to write<br>
a UI like this, if you ever<br>
<br>
657<br>
00:31:52,170 --> 00:31:55,105<br>
tried to make these two<br>
fragments talk to each other,<br>
<br>
658<br>
00:31:55,105 --> 00:31:56,220<br>
it's a pain in the neck.<br>
<br>
659<br>
00:31:56,220 --> 00:31:57,240<br>
It's very, very hard.<br>
<br>
660<br>
00:31:57,240 --> 00:31:59,510<br>
Like you need to<br>
create an interface.<br>
<br>
661<br>
00:31:59,510 --> 00:32:01,530<br>
But then what if<br>
one fragment gets<br>
<br>
662<br>
00:32:01,530 --> 00:32:03,540<br>
created before the other one.<br>
<br>
663<br>
00:32:03,540 --> 00:32:05,940<br>
An activity needs to<br>
talk to each other.<br>
<br>
664<br>
00:32:05,940 --> 00:32:07,931<br>
Or like when the<br>
activities are restored,<br>
<br>
665<br>
00:32:07,931 --> 00:32:09,430<br>
you don't really<br>
know which fragment<br>
<br>
666<br>
00:32:09,430 --> 00:32:11,340<br>
will be restored first.<br>
<br>
667<br>
00:32:11,340 --> 00:32:14,880<br>
It is really hard to<br>
manage this state.<br>
<br>
668<br>
00:32:14,880 --> 00:32:21,020<br>
But we can actually solve this<br>
very elegantly using ViewModel.<br>
<br>
669<br>
00:32:21,020 --> 00:32:23,930<br>
So let's say so these two<br>
families actually want<br>
<br>
670<br>
00:32:23,930 --> 00:32:26,390<br>
to talk about a selected email.<br>
<br>
671<br>
00:32:26,390 --> 00:32:29,060<br>
This is the information<br>
they want to share.<br>
<br>
672<br>
00:32:29,060 --> 00:32:30,950<br>
So let's put it<br>
inside a ViewModel<br>
<br>
673<br>
00:32:30,950 --> 00:32:33,920<br>
and we are going to call<br>
this shared ViewModel.<br>
<br>
674<br>
00:32:33,920 --> 00:32:36,130<br>
So it has a mutable<br>
LiveData inside it<br>
<br>
675<br>
00:32:36,130 --> 00:32:41,430<br>
which you call selected, and it<br>
provides two very simple APIs.<br>
<br>
676<br>
00:32:41,430 --> 00:32:45,410<br>
The first one says, set the<br>
select email to this email.<br>
<br>
677<br>
00:32:45,410 --> 00:32:49,610<br>
Another one says, get the<br>
selected email as a LiveData.<br>
<br>
678<br>
00:32:49,610 --> 00:32:52,510<br>
It's a really simple ViewModel.<br>
<br>
679<br>
00:32:52,510 --> 00:32:56,030<br>
But now once we have this,<br>
let's go back to our fragments<br>
<br>
680<br>
00:32:56,030 --> 00:32:58,260<br>
and see how we can use this.<br>
<br>
681<br>
00:32:58,260 --> 00:33:00,920<br>
So inside the content<br>
fragment, which is the one<br>
<br>
682<br>
00:33:00,920 --> 00:33:03,650<br>
that wants to display the<br>
contents of the email.<br>
<br>
683<br>
00:33:03,650 --> 00:33:07,550<br>
It wants to know when the<br>
selected email changes.<br>
<br>
684<br>
00:33:07,550 --> 00:33:09,930<br>
So we're going to go-- so<br>
we have already seen this.<br>
<br>
685<br>
00:33:09,930 --> 00:33:12,470<br>
You can go to ViewModel<br>
providers class<br>
<br>
686<br>
00:33:12,470 --> 00:33:15,230<br>
and get the ViewModel<br>
providers of this fragment.<br>
<br>
687<br>
00:33:15,230 --> 00:33:19,170<br>
But we actually want ViewModel<br>
not from this fragment,<br>
<br>
688<br>
00:33:19,170 --> 00:33:21,330<br>
we want it from our activity.<br>
<br>
689<br>
00:33:21,330 --> 00:33:25,480<br>
So all you have to do tell it<br>
to do it from your activity.<br>
<br>
690<br>
00:33:25,480 --> 00:33:28,520<br>
Now it's going to return your<br>
ViewModel in the activity<br>
<br>
691<br>
00:33:28,520 --> 00:33:33,140<br>
scope, and I will say, get<br>
for the shared ViewModel.<br>
<br>
692<br>
00:33:33,140 --> 00:33:35,770<br>
Now, the very first time one<br>
of the fragments called this,<br>
<br>
693<br>
00:33:35,770 --> 00:33:37,460<br>
we are going to<br>
create a new one.<br>
<br>
694<br>
00:33:37,460 --> 00:33:39,520<br>
When the other<br>
fragment comes alive,<br>
<br>
695<br>
00:33:39,520 --> 00:33:42,830<br>
it's going to receive the<br>
same ViewModel instance.<br>
<br>
696<br>
00:33:42,830 --> 00:33:44,100<br>
And I will do the same thing.<br>
<br>
697<br>
00:33:44,100 --> 00:33:46,650<br>
So this one says, get<br>
the selected email.<br>
<br>
698<br>
00:33:46,650 --> 00:33:48,662<br>
Start observing on it.<br>
<br>
699<br>
00:33:48,662 --> 00:33:50,540<br>
Really similarly, in<br>
the select fragment<br>
<br>
700<br>
00:33:50,540 --> 00:33:54,500<br>
which was the one on the<br>
left by user pics and email,<br>
<br>
701<br>
00:33:54,500 --> 00:33:57,410<br>
we get the same ViewModel.<br>
<br>
702<br>
00:33:57,410 --> 00:34:00,680<br>
And whenever the user selects<br>
an email from the list,<br>
<br>
703<br>
00:34:00,680 --> 00:34:03,080<br>
we just call the<br>
ViewModel- related method<br>
<br>
704<br>
00:34:03,080 --> 00:34:05,120<br>
to change the selected email.<br>
<br>
705<br>
00:34:05,120 --> 00:34:08,239<br>
Now these two fragments<br>
talking to each other<br>
<br>
706<br>
00:34:08,239 --> 00:34:10,710<br>
without actually<br>
talking to each other.<br>
<br>
707<br>
00:34:10,710 --> 00:34:13,730<br>
How does this really happen?<br>
<br>
708<br>
00:34:13,730 --> 00:34:15,380<br>
So if we go back to our UI.<br>
<br>
709<br>
00:34:15,380 --> 00:34:18,679<br>
So we have the selector on the<br>
left, the content on the right.<br>
<br>
710<br>
00:34:18,679 --> 00:34:21,320<br>
But if you look at the<br>
details, actually both of these<br>
<br>
711<br>
00:34:21,320 --> 00:34:23,060<br>
are talking to a<br>
shared ViewModel.<br>
<br>
712<br>
00:34:23,060 --> 00:34:25,040<br>
They never talk to each other.<br>
<br>
713<br>
00:34:25,040 --> 00:34:28,580<br>
The video of this solution is<br>
that if you're on the phone,<br>
<br>
714<br>
00:34:28,580 --> 00:34:31,280<br>
let's say one fragment<br>
replaces the other one,<br>
<br>
715<br>
00:34:31,280 --> 00:34:33,080<br>
there's no room for error.<br>
<br>
716<br>
00:34:33,080 --> 00:34:35,270<br>
Like the fragment still<br>
talks to a ViewModel.<br>
<br>
717<br>
00:34:35,270 --> 00:34:37,370<br>
ViewModels always that<br>
nothing will crash.<br>
<br>
718<br>
00:34:37,370 --> 00:34:39,770<br>
They don't even care<br>
the other one is there.<br>
<br>
719<br>
00:34:39,770 --> 00:34:42,810<br>
<br>
<br>
720<br>
00:34:42,810 --> 00:34:45,349<br>
Okay, so this is a<br>
lot of information,<br>
<br>
721<br>
00:34:45,349 --> 00:34:47,670<br>
and there's further<br>
details about how<br>
<br>
722<br>
00:34:47,670 --> 00:34:49,170<br>
these life cycles work.<br>
<br>
723<br>
00:34:49,170 --> 00:34:51,330<br>
We really spent a<br>
lot of time to make<br>
<br>
724<br>
00:34:51,330 --> 00:34:55,260<br>
these handle most common<br>
used cases on Android.<br>
<br>
725<br>
00:34:55,260 --> 00:34:58,620<br>
So we come in just<br>
the first trade out.<br>
<br>
726<br>
00:34:58,620 --> 00:35:03,150<br>
You could try it<br>
now, in [INAUDIBLE].<br>
<br>
727<br>
00:35:03,150 --> 00:35:05,850<br>
Please check out all of the<br>
architecture components.<br>
<br>
728<br>
00:35:05,850 --> 00:35:08,640<br>
These are things that actually<br>
work very well together.<br>
<br>
729<br>
00:35:08,640 --> 00:35:11,070<br>
We have an architecture<br>
guide which shows you<br>
<br>
730<br>
00:35:11,070 --> 00:35:15,330<br>
how to use these things together<br>
to write a good application.<br>
<br>
731<br>
00:35:15,330 --> 00:35:16,980<br>
And also check our code labs.<br>
<br>
732<br>
00:35:16,980 --> 00:35:20,490<br>
We have code lab sections that<br>
will give you a first glimpse<br>
<br>
733<br>
00:35:20,490 --> 00:35:23,841<br>
of how LifeCycles work.<br>
<br>
734<br>
00:35:23,841 --> 00:35:24,340<br>
Thank you<br>
<br>
735<br>
00:35:24,340 --> 00:35:26,815<br>
[APPLAUSE]<br>
<br>
736<br>
00:35:26,815 --> 00:35:29,055<br>
[MUSIC PLAYING]<br>
<br>
737<br>
00:35:29,055 --> 00:00:00,000<br>
<br>
<br>

  </td>
  </tr> 
  </table>
  
