---
layout: post
title: Google I/O '17 Architecture Components - Introduction. Перевод субтитров.
date: 2017-08-20 9:44
tags:
- Java
- Android
- архитектура
- video
- youtube
- translate
- Google I/O '17
- философия
---
*Перевод английских субтитров на русские из видео Architecture Components - Introduction (Google I/O '17). Предпринят только для практики перевода с английского, скажем так to improve my reading and listening skills. Делается постепенно. Начало 20.08.2017, конец - . All rights reserved.*

<iframe width="560" height="315" src="https://www.youtube.com/embed/FrteWKKVyzI" frameborder="0" allowfullscreen></iframe>

Аннотация к видео:

+ Writing robust Android apps can be challenging, between complex lifecycle issues, unreliable mobile networks, and constrained device capabilities. Mistakes in these areas lead to memory leaks, crashing apps, drained batteries, and unhappy users. This session will cover a new approach to good Android app architecture, including an overview of functionality that will make these problems fundamentally easier to solve. This session is the first of three on this new initiative; be sure to check out the other two “Architecture Components” sessions.

Перевод:
+ Написание надежных приложений для Android может оказаться сложной задачей среди нетривиальных проблем регулирования жизненного цикла компонентов, ненадежных мобильных сетей и ограниченной производительности устройств. Ошибки в этих областях приводят к утечкам памяти, падениям приложений, неэффективному расходу батареи и, в итоге, к несчастным пользователям. Эта сессия будет посвящена новому подходу к хорошей архитектуре приложений для Android. В ней представлен обзор функциональности, которая позволит принципиально упростить решение данных проблем. Эта сессия является первой из трёх посвященных архитектурным компонентам. Обязательно посмотрите две другие.

Некоторые ссылки для понимая того, о чем говорится в докладе:
- <a href="https://developer.android.com/topic/libraries/architecture/livedata.html">класс LiveData</a> - documentation.
- <a href="https://developer.android.com/topic/libraries/architecture/room.html">Абстрация над SQLite базой данных, называемая Room</a> - documentation about Room Persistence Library, и еще <a href="https://medium.com/@tonyowen/a-room-with-a-view-getting-started-ec010f9f5448">о ней же</a> - article with Kotlin.
- <a href="https://academy.realm.io/posts/android-architecture-components-and-realm/">Room, ViewModel, LifeCycle, LiveData</a> - article
- <a href="https://codelabs.developers.google.com/codelabs/android-lifecycles/#0">Android lifecycle-aware components</a> - tutorial codelab.
- <a href="https://codelabs.developers.google.com/codelabs/android-persistence/#0">Android Persistence: Room Library</a> - tutorial codelab.
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
00:00:00,000 --> 00:00:05,189<br>
[MUSIC PLAYING] <br>
<br>
2<br>
00:00:05,189 --> 00:00:05,980<br>
MIKE CLERON: So hi. <br>
<br>
3<br>
00:00:05,980 --> 00:00:07,080<br> 
I'm Mike Cleron.  <br>
<br>
4<br>
00:00:07,080 --> 00:00:08,650<br> 
I'm on the Android team.<br>
<br>
5<br>
00:00:08,650 --> 00:00:14,120<br>
I manage the system UI framework <br>
and UI toolkit teams there.  <br>
<br>
6<br>
00:00:14,120 --> 00:00:17,650<br> 
We're going to be talking<br>
today in a lot of detail<br>  
<br> 
7<br> 
00:00:17,650 --> 00:00:21,790<br> 
about some big changes to <br>
how we recommend that you  <br>
<br>
8 <br>
00:00:21,790 --> 00:00:23,710 <br>
build Android applications.  <br>
<br>
9 <br>
00:00:23,710 --> 00:00:26,110<br> 
But before we go into <br>
a lot of the details, <br>
<br>
10 <br>
00:00:26,110 --> 00:00:28,510<br> 
I thought would be helpful <br>
to step back a bit, <br>
<br>
11 <br>
00:00:28,510 --> 00:00:31,960<br> 
and frame the discussion by <br>
talking about where we came <br>
<br>
12 <br>
00:00:31,960 --> 00:00:34,730<br>
from, and where we're going. <br>
<br>
13<br> 
00:00:34,730 --> 00:00:36,100<br> 
So let's do that. <br>
<br>
14<br>
00:00:36,100 --> 00:00:39,010<br> 
So to start, Android <br>
has always been based <br>
<br>
15<br>
00:00:39,010 --> 00:00:41,230<br> 
on some strong principles. <br>
<br>
16<br>
00:00:41,230 --> 00:00:43,330<br>
Not surprisingly, those<br>
were best expressed<br>
<br>
17<br>
00:00:43,330 --> 00:00:44,860<br>
by Dianne Hackborn.<br>
<br>
18<br>
00:00:44,860 --> 00:00:46,600<br>
She's the one who<br>
actually architected<br>
<br>
19<br>
00:00:46,600 --> 00:00:48,880<br>
most of the Android framework.<br>
<br>
20<br>
00:00:48,880 --> 00:00:51,160<br>
She wrote a post about<br>
this a few months back,<br>
<br>
21<br>
00:00:51,160 --> 00:00:54,310<br>
and I have some<br>
excerpts from that here.<br>
<br>
22<br>
00:00:54,310 --> 00:00:56,230<br>
If you look at our<br>
core primitives--<br>
<br>
23<br>
00:00:56,230 --> 00:01:00,100<br>
activity, broadcast receiver,<br>
service content provider,<br>
<br>
24<br>
00:01:00,100 --> 00:01:03,880<br>
you might reasonably think that<br>
those constitute an application<br>
<br>
25<br>
00:01:03,880 --> 00:01:05,012<br>
framework.<br>
<br>
26<br>
00:01:05,012 --> 00:01:06,970<br>
But that's not the right<br>
way to think about it.<br>
<br>
27<br>
00:01:06,970 --> 00:01:10,120<br>
These classes are<br>
actually contracts<br>
<br>
28<br>
00:01:10,120 --> 00:01:14,910<br>
between the application<br>
and the operating system.<br>
<br>
29<br>
00:01:14,910 --> 00:01:16,950<br>
They represent the minimal<br>
amount of information<br>
<br>
30<br>
00:01:16,950 --> 00:01:20,790<br>
necessary so that the OS knows<br>
what's going on inside your app<br>
<br>
31<br>
00:01:20,790 --> 00:01:23,220<br>
so we can manage it properly.<br>
<br>
<br>
32<br>
00:01:23,220 --> 00:01:27,060<br>
So as an example, if your app<br>
is running in the background,<br>
<br>
33<br>
00:01:27,060 --> 00:01:29,600<br>
but is also exposing data<br>
to another application<br>
<br>
34<br>
00:01:29,600 --> 00:01:32,492<br>
through a content provider,<br>
the OS needs to know that.<br>
<br>
35<br>
00:01:32,492 --> 00:01:34,950<br>
And we need to know that so we<br>
don't accidentally kill you.<br>
<br>
36<br>
00:01:34,950 --> 00:01:37,500<br>
The content provider is a<br>
mechanism that tells us that<br>
<br>
37<br>
00:01:37,500 --> 00:01:39,990<br>
so that we can keep you alive.<br>
<br>
38<br>
00:01:39,990 --> 00:01:41,970<br>
So we think of<br>
these core classes<br>
<br>
39<br>
00:01:41,970 --> 00:01:44,790<br>
as really being like the<br>
fundamental laws of physics<br>
<br>
40<br>
00:01:44,790 --> 00:01:47,520<br>
for Android, hence<br>
the illustration.<br>
<br>
41<br>
00:01:47,520 --> 00:01:49,920<br>
That is the cover<br>
of the manuscript<br>
<br>
42<br>
00:01:49,920 --> 00:01:52,170<br>
where Isaac Newton<br>
first presented<br>
<br>
43<br>
00:01:52,170 --> 00:01:53,430<br>
the basic laws of motion.<br>
<br>
44<br>
00:01:53,430 --> 00:01:56,620<br>
<br>
<br>
45<br>
00:01:56,620 --> 00:01:59,580<br>
Now, fundamental laws<br>
are a good thing.<br>
<br>
46<br>
00:01:59,580 --> 00:02:01,560<br>
I use a shorthand when<br>
talking about this.<br>
<br>
47<br>
00:02:01,560 --> 00:02:04,530<br>
I say, Android has good bones,<br>
even though people look at me<br>
<br>
48<br>
00:02:04,530 --> 00:02:06,780<br>
funny after I say that.<br>
<br>
49<br>
00:02:06,780 --> 00:02:09,960<br>
But what I mean by<br>
that is that Android<br>
<br>
50<br>
00:02:09,960 --> 00:02:13,650<br>
is based on a small,<br>
stable, cohesive set<br>
<br>
51<br>
00:02:13,650 --> 00:02:15,150<br>
of core primitives.<br>
<br>
52<br>
00:02:15,150 --> 00:02:18,390<br>
And that allows a<br>
common programming model<br>
<br>
53<br>
00:02:18,390 --> 00:02:20,940<br>
across a really<br>
incredibly diverse range<br>
<br>
54<br>
00:02:20,940 --> 00:02:24,750<br>
of devices from wearables<br>
to phones to tablets<br>
<br>
55<br>
00:02:24,750 --> 00:02:27,870<br>
to TVs to cars, and more.<br>
<br>
56<br>
00:02:27,870 --> 00:02:30,210<br>
This model also gives<br>
application developers<br>
<br>
57<br>
00:02:30,210 --> 00:02:32,310<br>
the freedom to choose<br>
whatever framework<br>
<br>
58<br>
00:02:32,310 --> 00:02:34,170<br>
they want inside<br>
their application<br>
<br>
59<br>
00:02:34,170 --> 00:02:36,010<br>
for their internal framework.<br>
<br>
60<br>
00:02:36,010 --> 00:02:38,070<br>
So that means that we<br>
on the Android team<br>
<br>
61<br>
00:02:38,070 --> 00:02:41,250<br>
don't have to get involved<br>
in debates about whether MVC<br>
<br>
62<br>
00:02:41,250 --> 00:02:45,540<br>
is better than MVP, or whether<br>
MVP is better than [? MVVBM. ?]<br>
<br>
63<br>
00:02:45,540 --> 00:02:49,260<br>
You guys can pick whatever<br>
makes sense to you.<br>
<br>
64<br>
00:02:49,260 --> 00:02:52,680<br>
Now, that's a pretty good story<br>
if you are in the operating<br>
<br>
65<br>
00:02:52,680 --> 00:02:55,921<br>
system business like, say, me.<br>
<br>
66<br>
00:02:55,921 --> 00:02:57,420<br>
But if you're in<br>
the app development<br>
<br>
67<br>
00:02:57,420 --> 00:03:01,110<br>
business like, say,<br>
all of you, that's<br>
<br>
68<br>
00:03:01,110 --> 00:03:03,120<br>
really only chapter<br>
one of the story.<br>
<br>
69<br>
00:03:03,120 --> 00:03:04,890<br>
And the reason for<br>
that is because<br>
<br>
70<br>
00:03:04,890 --> 00:03:08,190<br>
while strong fundamentals<br>
and freedom of choice<br>
<br>
71<br>
00:03:08,190 --> 00:03:12,000<br>
are good things, we know that<br>
in your day to day jobs--<br>
<br>
72<br>
00:03:12,000 --> 00:03:16,730<br>
and we know this because you<br>
told us, you want more from us.<br>
<br>
73<br>
00:03:16,730 --> 00:03:19,690<br>
So I'm going to abuse<br>
my analogy a bit here.<br>
<br>
74<br>
00:03:19,690 --> 00:03:22,810<br>
We can all appreciate the<br>
simple elegance of Newton's laws<br>
<br>
75<br>
00:03:22,810 --> 00:03:27,725<br>
of motion, but if your job<br>
is to land a Rover on Mars,<br>
<br>
76<br>
00:03:27,725 --> 00:03:29,350<br>
you don't want to<br>
come to work each day<br>
<br>
77<br>
00:03:29,350 --> 00:03:31,810<br>
and start with only F equals<br>
ma, and derive everything<br>
<br>
78<br>
00:03:31,810 --> 00:03:35,230<br>
from first principles.<br>
<br>
79<br>
00:03:35,230 --> 00:03:37,780<br>
So we've been talking to<br>
developers, both inside<br>
<br>
80<br>
00:03:37,780 --> 00:03:41,140<br>
and outside of Google, and<br>
taking a hard look at the app<br>
<br>
81<br>
00:03:41,140 --> 00:03:42,830<br>
development experience.<br>
<br>
82<br>
00:03:42,830 --> 00:03:45,230<br>
And we've realized<br>
a couple of things.<br>
<br>
83<br>
00:03:45,230 --> 00:03:47,770<br>
First, there are<br>
peaks and valleys.<br>
<br>
84<br>
00:03:47,770 --> 00:03:51,550<br>
Some aspects of app development<br>
are better served by our APIs<br>
<br>
85<br>
00:03:51,550 --> 00:03:52,570<br>
than others.<br>
<br>
86<br>
00:03:52,570 --> 00:03:56,470<br>
For example, we think<br>
RecyclerView is that the better<br>
<br>
87<br>
00:03:56,470 --> 00:03:57,830<br>
end of that spectrum.<br>
<br>
88<br>
00:03:57,830 --> 00:04:02,020<br>
So with RecyclerView, we didn't<br>
say, hey, we give you events,<br>
<br>
89<br>
00:04:02,020 --> 00:04:03,810<br>
and you can draw stuff.<br>
<br>
90<br>
00:04:03,810 --> 00:04:07,600<br>
And in between you have a Turing<br>
complete language, so good luck<br>
<br>
91<br>
00:04:07,600 --> 00:04:09,550<br>
with everything else.<br>
<br>
92<br>
00:04:09,550 --> 00:04:12,640<br>
On the other hand,<br>
maybe Activity<br>
<br>
93<br>
00:04:12,640 --> 00:04:16,510<br>
and Fragment Lifecycles belong<br>
down in that dark shadowy place<br>
<br>
94<br>
00:04:16,510 --> 00:04:18,730<br>
because there, I<br>
think, too much of it<br>
<br>
95<br>
00:04:18,730 --> 00:04:21,790<br>
is indeed left as an<br>
exercise for the reader.<br>
<br>
96<br>
00:04:21,790 --> 00:04:24,730<br>
And we want to fix that.<br>
<br>
97<br>
00:04:24,730 --> 00:04:27,250<br>
So as we thought about this,<br>
we realized the good solution<br>
<br>
98<br>
00:04:27,250 --> 00:04:29,930<br>
has key properties.<br>
<br>
99<br>
00:04:29,930 --> 00:04:32,194<br>
First, we have to solve<br>
the right problems.<br>
<br>
100<br>
00:04:32,194 --> 00:04:33,860<br>
This is going to be<br>
a sustained effort--<br>
<br>
101<br>
00:04:33,860 --> 00:04:36,320<br>
like sustained<br>
for us on Android.<br>
<br>
102<br>
00:04:36,320 --> 00:04:38,410<br>
But for the first cut,<br>
we want to make sure<br>
<br>
103<br>
00:04:38,410 --> 00:04:39,910<br>
that we are going<br>
after the problems<br>
<br>
104<br>
00:04:39,910 --> 00:04:42,040<br>
that every developer<br>
faces, the things that<br>
<br>
105<br>
00:04:42,040 --> 00:04:45,040<br>
are hard to do right right now.<br>
<br>
106<br>
00:04:45,040 --> 00:04:47,574<br>
Again, app Lifecycles is<br>
a really good example.<br>
<br>
107<br>
00:04:47,574 --> 00:04:49,240<br>
If you don't get that<br>
right in your app,<br>
<br>
108<br>
00:04:49,240 --> 00:04:51,236<br>
nothing is going to<br>
work on top of that.<br>
<br>
109<br>
00:04:51,236 --> 00:04:53,110<br>
And that's true for your<br>
app, but that's also<br>
<br>
110<br>
00:04:53,110 --> 00:04:55,026<br>
true for the frameworks<br>
we're trying to build.<br>
<br>
111<br>
00:04:55,026 --> 00:04:58,420<br>
We have to get that right<br>
before we can do anything else.<br>
<br>
112<br>
00:04:58,420 --> 00:05:00,370<br>
Second, we have to<br>
play well with others.<br>
<br>
113<br>
00:05:00,370 --> 00:05:02,830<br>
We know that you all have huge<br>
investments in your existing<br>
<br>
114<br>
00:05:02,830 --> 00:05:05,196<br>
code bases, and we<br>
can't create a model<br>
<br>
115<br>
00:05:05,196 --> 00:05:06,820<br>
where the first thing<br>
we say to you is,<br>
<br>
116<br>
00:05:06,820 --> 00:05:08,940<br>
throw all that out<br>
and start over.<br>
<br>
117<br>
00:05:08,940 --> 00:05:12,070<br>
So we're trying to create APIs<br>
that you can adopt a little bit<br>
<br>
118<br>
00:05:12,070 --> 00:05:15,580<br>
at a time, and also<br>
that interoperate well<br>
<br>
119<br>
00:05:15,580 --> 00:05:19,710<br>
with other libraries<br>
or other frameworks.<br>
<br>
120<br>
00:05:19,710 --> 00:05:22,054<br>
Third, we want to<br>
be more opinionated.<br>
<br>
121<br>
00:05:22,054 --> 00:05:23,970<br>
We're going to take a<br>
stronger, clearer stance<br>
<br>
122<br>
00:05:23,970 --> 00:05:26,000<br>
on how to Android and<br>
app the right way,<br>
<br>
123<br>
00:05:26,000 --> 00:05:27,100<br>
at least as we see it.<br>
<br>
124<br>
00:05:27,100 --> 00:05:29,100<br>
Now, this is all still optional.<br>
<br>
125<br>
00:05:29,100 --> 00:05:31,330<br>
And if you already have<br>
something that works for you,<br>
<br>
126<br>
00:05:31,330 --> 00:05:33,030<br>
then great.<br>
<br>
127<br>
00:05:33,030 --> 00:05:36,210<br>
But developers are telling us<br>
that they want more guidance<br>
<br>
128<br>
00:05:36,210 --> 00:05:38,590<br>
on how apps should be<br>
built. And by the way,<br>
<br>
129<br>
00:05:38,590 --> 00:05:40,770<br>
we're not changing any of<br>
the laws of physics here,<br>
<br>
130<br>
00:05:40,770 --> 00:05:43,860<br>
we're just layering some<br>
higher level constructs on top.<br>
<br>
131<br>
00:05:43,860 --> 00:05:46,620<br>
Because after all, F is<br>
going to equal ma whether you<br>
<br>
132<br>
00:05:46,620 --> 00:05:49,860<br>
believe it should or not.<br>
<br>
133<br>
00:05:49,860 --> 00:05:52,140<br>
Next, it needs to scale.<br>
<br>
134<br>
00:05:52,140 --> 00:05:54,420<br>
We want solutions that<br>
are industrial strength,<br>
<br>
135<br>
00:05:54,420 --> 00:05:56,760<br>
and that will scale to the<br>
real world requirements<br>
<br>
136<br>
00:05:56,760 --> 00:05:58,474<br>
of real world applications.<br>
<br>
137<br>
00:05:58,474 --> 00:06:01,140<br>
We don't want to build something<br>
that's awesome for Hello World,<br>
<br>
138<br>
00:06:01,140 --> 00:06:03,181<br>
but then it's going to<br>
collapse the first time it<br>
<br>
139<br>
00:06:03,181 --> 00:06:07,620<br>
bumps into the messy<br>
complexities of reality.<br>
<br>
140<br>
00:06:07,620 --> 00:06:09,410<br>
And finally, reach.<br>
<br>
141<br>
00:06:09,410 --> 00:06:11,310<br>
For this problem,<br>
for making it easier<br>
<br>
142<br>
00:06:11,310 --> 00:06:13,830<br>
for you to write Android<br>
applications the right way--<br>
<br>
143<br>
00:06:13,830 --> 00:06:15,690<br>
what we think is<br>
the right way, we<br>
<br>
144<br>
00:06:15,690 --> 00:06:18,390<br>
want to use libraries like<br>
Support Lib wherever possible<br>
<br>
145<br>
00:06:18,390 --> 00:06:21,150<br>
rather than adding new<br>
APIs to the platform,<br>
<br>
146<br>
00:06:21,150 --> 00:06:24,030<br>
because lets our solution<br>
reach older versions of the OS<br>
<br>
147<br>
00:06:24,030 --> 00:06:26,745<br>
as well.<br>
<br>
148<br>
00:06:26,745 --> 00:06:29,370<br>
OK, so that's the background on<br>
what we're trying to accomplish<br>
<br>
149<br>
00:06:29,370 --> 00:06:30,440<br>
and why we're here.<br>
<br>
150<br>
00:06:30,440 --> 00:06:33,309<br>
Now we'd like to introduce<br>
Yigit, tool kit engineer<br>
<br>
151<br>
00:06:33,309 --> 00:06:35,600<br>
extraordinaire, and he's<br>
going to walk you through what<br>
<br>
152<br>
00:06:35,600 --> 00:06:36,860<br>
we actually built. Thank you.<br>
<br>
153<br>
00:06:36,860 --> 00:06:37,290<br>
[APPLAUSE]<br>
<br>
154<br>
00:06:37,290 --> 00:06:38,248<br>
YIGIT BOYAR: All right.<br>
<br>
155<br>
00:06:38,248 --> 00:06:39,322<br>
Thanks, Frank.<br>
<br>
156<br>
00:06:39,322 --> 00:06:43,610<br>
<br>
<br>
157<br>
00:06:43,610 --> 00:06:44,410<br>
Hello everybody.<br>
<br>
158<br>
00:06:44,410 --> 00:06:46,930<br>
So that was the background.<br>
<br>
159<br>
00:06:46,930 --> 00:06:49,050<br>
What are we shipping today?<br>
<br>
160<br>
00:06:49,050 --> 00:06:51,210<br>
The very first thing<br>
we are shipping<br>
<br>
161<br>
00:06:51,210 --> 00:06:55,230<br>
is an architecture guide<br>
on developer Android com.<br>
<br>
162<br>
00:06:55,230 --> 00:06:58,440<br>
Now for over years, you've<br>
been asking us for our opinion.<br>
<br>
163<br>
00:06:58,440 --> 00:07:02,220<br>
Like how do we think that an<br>
application should be built?<br>
<br>
164<br>
00:07:02,220 --> 00:07:03,900<br>
And this is that guide.<br>
<br>
165<br>
00:07:03,900 --> 00:07:06,270<br>
So we believe that<br>
it's very good,<br>
<br>
166<br>
00:07:06,270 --> 00:07:08,730<br>
covers lots of<br>
application cases.<br>
<br>
167<br>
00:07:08,730 --> 00:07:10,890<br>
But even if you<br>
have an architecture<br>
<br>
168<br>
00:07:10,890 --> 00:07:14,040<br>
that you are comfortable<br>
with, you can keep it.<br>
<br>
169<br>
00:07:14,040 --> 00:07:18,300<br>
But you can probably learn<br>
something from this guide.<br>
<br>
170<br>
00:07:18,300 --> 00:07:20,910<br>
Second, we are shipping<br>
a new set of libraries<br>
<br>
171<br>
00:07:20,910 --> 00:07:23,290<br>
that we call<br>
architecture components.<br>
<br>
172<br>
00:07:23,290 --> 00:07:24,900<br>
These are more<br>
fundamental components<br>
<br>
173<br>
00:07:24,900 --> 00:07:28,440<br>
where you can build<br>
your application on top.<br>
<br>
174<br>
00:07:28,440 --> 00:07:29,760<br>
The first thing is Lifecycles.<br>
<br>
175<br>
00:07:29,760 --> 00:07:33,000<br>
So this is the biggest developer<br>
complaint that we have.<br>
<br>
176<br>
00:07:33,000 --> 00:07:35,610<br>
Lifecycles are hard,<br>
Lifecycles are hard.<br>
<br>
177<br>
00:07:35,610 --> 00:07:38,020<br>
And we said, OK, we<br>
should solve this problem.<br>
<br>
178<br>
00:07:38,020 --> 00:07:41,850<br>
And the first level of this,<br>
this new set of components.<br>
<br>
179<br>
00:07:41,850 --> 00:07:44,070<br>
Second one is<br>
Lifecycle-aware observables,<br>
<br>
180<br>
00:07:44,070 --> 00:07:46,860<br>
which will go in detail<br>
later, but this is basically<br>
<br>
181<br>
00:07:46,860 --> 00:07:51,730<br>
things that can do something<br>
based on the Lifecycle.<br>
<br>
182<br>
00:07:51,730 --> 00:07:54,810<br>
Third, we are going to introduce<br>
a lightweight ViewModel, which<br>
<br>
183<br>
00:07:54,810 --> 00:07:58,020<br>
is all of our effort<br>
to take out that code<br>
<br>
184<br>
00:07:58,020 --> 00:08:00,150<br>
outside of your<br>
Activities and Fragments,<br>
<br>
185<br>
00:08:00,150 --> 00:08:03,550<br>
and put it somewhere else<br>
where you can easily test it.<br>
<br>
186<br>
00:08:03,550 --> 00:08:06,630<br>
Last but not least, we are<br>
going to introduce a new object<br>
<br>
187<br>
00:08:06,630 --> 00:08:10,290<br>
mapping library for SQLite.<br>
<br>
188<br>
00:08:10,290 --> 00:08:15,248<br>
And all of this is available for<br>
you today on Maven Google com.<br>
<br>
189<br>
00:08:15,248 --> 00:08:24,290<br>
[APPLAUSE]<br>
<br>
190<br>
00:08:24,290 --> 00:08:25,790<br>
Let's talk about Lifecycles.<br>
<br>
191<br>
00:08:25,790 --> 00:08:27,830<br>
So what is what's<br>
hard about Lifecycles?<br>
<br>
192<br>
00:08:27,830 --> 00:08:29,970<br>
Why do we hear so many<br>
complaints about that?<br>
<br>
193<br>
00:08:29,970 --> 00:08:31,510<br>
Let's go through an example.<br>
<br>
194<br>
00:08:31,510 --> 00:08:33,440<br>
Assume we have an<br>
activity where we<br>
<br>
195<br>
00:08:33,440 --> 00:08:36,591<br>
want to show the location<br>
of the device on the screen.<br>
<br>
196<br>
00:08:36,591 --> 00:08:38,090<br>
So you will try<br>
something like this.<br>
<br>
197<br>
00:08:38,090 --> 00:08:41,280<br>
You create a LocationListener<br>
on Create method,<br>
<br>
198<br>
00:08:41,280 --> 00:08:43,250<br>
you need to initialize<br>
it with the context,<br>
<br>
199<br>
00:08:43,250 --> 00:08:46,520<br>
and you have a callback that<br>
it calls whenever the location<br>
<br>
200<br>
00:08:46,520 --> 00:08:48,800<br>
changes, and you update the UI.<br>
<br>



</td>
      
<td>1<br>
00:00:00,000 --> 00:00:05,189<br>
[Музыка] <br>
<br>
2<br>
00:00:05,189 --> 00:00:05,980<br>
MIKE CLERON: Привет! <br>
<br>
3<br>
00:00:05,980 --> 00:00:07,080<br>
Я Майк Клерон. <br>
<br>
4<br>
00:00:07,080 --> 00:00:08,650<br>
Я из Android team.<br>
<br>
5<br>
00:00:08,650 --> 00:00:14,120<br>
Я разрабатываю UI фреймворк<br>
и UI средства разработки [toolkit] <br>
<br>
6<br>
00:00:14,120 --> 00:00:17,650<br>
Сегодня мы будем говорить<br>
о многих деталях <br>
<br>
7<br>
00:00:17,650 --> 00:00:21,790<br>
и о некоторых больших изменениях в подходах, <br>
которые мы рекомендуем <br>
<br>
8<br>
00:00:21,790 --> 00:00:23,710<br>
при проектировании приложений для Android. <br>
<br>
9<br>
00:00:23,710 --> 00:00:26,110<br> 
Но прежде чем мы погрузимся<br>
в детали,<br>
<br>
10<br>
00:00:26,110 --> 00:00:28,510<br> 
я думаю, что будет полезно<br>
сделать шаг в сторону, <br>
<br>
11<br>
00:00:28,510 --> 00:00:31,960<br> 
и поговорить о том,<br>
откуда мы пришли <br>
<br>
12<br>
00:00:31,960 --> 00:00:34,730<br> 
и куда мы идем.<br>
<br>
13<br>
00:00:34,730 --> 00:00:36,100<br> 
Давайте начнем.<br>
<br>
14<br> 
00:00:36,100 --> 00:00:39,010<br> 
Итак, Android<br>
всегда основывался на<br> 
<br>
15<br>
00:00:39,010 --> 00:00:41,230<br> 
на нескольких прочных принципах<br>
<br>
16<br>
00:00:41,230 --> 00:00:43,330<br>
Не удивительно, они<br>
были лучше всего выражены<br>
<br>
17<br>
00:00:43,330 --> 00:00:44,860<br>
Дианой Хакборн.<br>
<br>
18<br>
00:00:44,860 --> 00:00:46,600<br>
Она из тех, кто<br>
реально проектировали<br>
<br>
19<br>
00:00:46,600 --> 00:00:48,880<br>
большую часть Android фреймворков.<br>
<br>
20<br>
00:00:48,880 --> 00:00:51,160<br>
Она написала пост об этом<br>
несколько месяцев назад,<br>
<br>
21<br>
00:00:51,160 --> 00:00:54,310<br>
и у меня есть некоторые<br>
выдержки оттуда.<br>
<br>
22<br>
00:00:54,310 --> 00:00:56,230<br>
Если вы посмотрите на примитивы<br>
ядра Android --<br>
<br>
23<br>
00:00:56,230 --> 00:01:00,100<br>
Activity, BroadcastReceiver,<br>
Service, ContentProvider,<br>
<br>
24<br>
00:01:00,100 --> 00:01:03,880<br>
у вас есть основание думать, что<br>
они составляют каркас<br>
<br>
25<br>
00:01:03,880 --> 00:01:05,012<br>
приложения (framework).<br>
<br>
26<br>
00:01:05,012 --> 00:01:06,970<br>
Но это не верный способ<br>
думать об этом.<br>
<br>
27<br>
00:01:06,970 --> 00:01:10,120<br>
Эти классы фактически<br>
контракты<br>
<br>
28<br>
00:01:10,120 --> 00:01:14,910<br>
между приложением<br>
и операционной системой (ОС).<br>
<br>
29<br>
00:01:14,910 --> 00:01:16,950<br>
Они представляют собой минимальное<br>
количество информации<br>
<br>
30<br>
00:01:16,950 --> 00:01:20,790<br>
необходимое, чтобы ОС знала,<br>
что происходит внутри вашего приложения<br>
<br>
31<br>
00:01:20,790 --> 00:01:23,220<br>
т.о. мы можем управлять этим правильно.<br>
<br>
<br>
32<br>
00:01:23,220 --> 00:01:27,060<br>
Итак, для примера, если ваше<br>
приложение работает в фоне,<br>
<br>
33<br>
00:01:27,060 --> 00:01:29,600<br>
но также предоставляет данные<br>
другому приложению<br>
<br>
34<br>
00:01:29,600 --> 00:01:32,492<br>
через ContentProvider,<br>
то ОС должна об этом знать.<br>
<br>
35<br>
00:01:32,492 --> 00:01:34,950<br>
И мы должны знать, что случайно<br>
не убьем его.<br>
<br>
36<br>
00:01:34,950 --> 00:01:37,500<br>
ContentProvider это механизм<br>
который говорит нам,<br>
<br>
37<br>
00:01:37,500 --> 00:01:39,990<br>
что мы должны держать вас живыми.<br>
<br>
38<br>
00:01:39,990 --> 00:01:41,970<br>
Итак, мы думаем об<br>
этих основных классах<br>
<br>
39<br>
00:01:41,970 --> 00:01:44,790<br>
как действительно существующих<br>
подобно фундаментальным законам физики<br>
<br>
40<br>
00:01:44,790 --> 00:01:47,520<br>
для Android. Тогда<br>
иллюстрация.<br>
<br>
41<br>
00:01:47,520 --> 00:01:49,920<br>
Это обложка книги,<br>
где впервые<br>
<br>
42<br>
00:01:49,920 --> 00:01:52,170<br>
Исаак Ньютон<br>
описал<br>
<br>
43<br>
00:01:52,170 --> 00:01:53,430<br>
фундаментальные законы движения.<br>
<br>
44<br>
00:01:53,430 --> 00:01:56,620<br>
<br>
<br>
45<br>
00:01:56,620 --> 00:01:59,580<br>
Теперь, фундаментальные законы<br>
это отличная вещь.<br>
<br>
46<br>
00:01:59,580 --> 00:02:01,560<br>
Я использую условные обозначения<br>
Когда говорю об этом.<br>
<br>
47<br>
00:02:01,560 --> 00:02:04,530<br>
Я говорю "У Android хорошие кости",<br>
даже если люди смотрят на меня<br>
<br>
48<br>
00:02:04,530 --> 00:02:06,780<br>
с усмешкой после этого.<br>
<br>
49<br>
00:02:06,780 --> 00:02:09,960<br>
Но что я имею в виду, когда<br>
говорю, что Android это Android<br>
<br>
50<br>
00:02:09,960 --> 00:02:13,650<br>
он небольшой, стабильный,<br>
имеет связанный набор<br>
<br>
51<br>
00:02:13,650 --> 00:02:15,150<br>
примитивов ядра.<br>
<br>
52<br>
00:02:15,150 --> 00:02:18,390<br>
И это позволяет иметь<br>
общую программную модель Android<br>
<br>
53<br>
00:02:18,390 --> 00:02:20,940<br>
на очень широком диапазоне<br>
различных устройств<br>
<br>
54<br>
00:02:20,940 --> 00:02:24,750<br>
от носимых устройств, телефонов,<br>
планшетов<br>
<br>
55<br>
00:02:24,750 --> 00:02:27,870<br>
до ТВ, автомобилей и т.д.<br>
<br>
56<br>
00:02:27,870 --> 00:02:30,210<br>
И эта же модель дает<br>
разработчикам приложений<br>
<br>
57<br>
00:02:30,210 --> 00:02:32,310<br>
свободу выбора<br>
любого фреймворка<br>
<br>
58<br>
00:02:32,310 --> 00:02:34,170<br>
какой они хотят использовать<br>
для своего приложения<br>
<br>
59<br>
00:02:34,170 --> 00:02:36,010<br>
для их внутренней структуры.<br>
<br>
60<br>
00:02:36,010 --> 00:02:38,070<br>
Это означает, что нам<br>
в команде Android<br>
<br>
61<br>
00:02:38,070 --> 00:02:41,250<br>
не следует заниматься дебатами<br>
что лучше: MVC<br>
<br>
62<br>
00:02:41,250 --> 00:02:45,540<br>
или MVP, или что<br>
MVP лучше чем [? MVVBM. ?]<br>
<br>
63<br>
00:02:45,540 --> 00:02:49,260<br>
Вы, ребята, выбирайте что угодно<br>
что имеет смысл для вас.<br>
<br>
64<br>
00:02:49,260 --> 00:02:52,680<br>
И это звучит хорошо для нас,<br>
находящихся<br>
<br>
65<br>
00:02:52,680 --> 00:02:55,921<br>
в разработке ОС, как я<br>
<br>
66<br>
00:02:55,921 --> 00:02:57,420<br>
Но если вы разработчик<br>
приложений<br>
<br>
67<br>
00:02:57,420 --> 00:03:01,110<br>
скажем, каждый из вас.<br>
Что ж, тогда<br>
<br>
68<br>
00:03:01,110 --> 00:03:03,120<br>
это только одна глава<br>
в этой истории.<br>
<br>
69<br>
00:03:03,120 --> 00:03:04,890<br>
И причина в том,<br>
что хотя<br>
<br>
70<br>
00:03:04,890 --> 00:03:08,190<br>
строгие фундаментальные основы<br>
и свобода выбора [реализации]<br>
<br>
71<br>
00:03:08,190 --> 00:03:12,000<br>
это хорошие вещи, мы знаем, что<br>
в повседневной работе [этого мало]-<br>
<br>
72<br>
00:03:12,000 --> 00:03:16,730<br>
и мы знаем это потому, что<br>
вы говорите, что хотите большего от нас.<br>
<br>
73<br>
00:03:16,730 --> 00:03:19,690<br>
Так что я буду немного надоедать<br>
моей аналогией.<br>
<br>
74<br>
00:03:19,690 --> 00:03:22,810<br>
Мы все можем оценить<br>
простую элегантность законов Ньютона<br>
<br>
75<br>
00:03:22,810 --> 00:03:27,725<br>
о движении, но если вы собираетесь<br>
высадить марсоход на Марс,<br>
<br>
76<br>
00:03:27,725 --> 00:03:29,350<br>
вам не захочется, приходить<br>
на работу каждый день и<br>
<br>
77<br>
00:03:29,350 --> 00:03:31,810<br>
и начинать с того, что сила равна<br>
масса на ускорение, и получить все<br>
<br>
78<br>
00:03:31,810 --> 00:03:35,230<br>
из оснований классической механики Ньютона.<br>
<br>
79<br>
00:03:35,230 --> 00:03:37,780<br>
Итак, мы поговорили с разработчиками<br>
с обеих сторон, внутри<br>
<br>
80<br>
00:03:37,780 --> 00:03:41,140<br>
и вне Google, и при этом<br>
внимательно изучали<br>
<br>
81<br>
00:03:41,140 --> 00:03:42,830<br>
опыт разработки приложений.<br>
<br>
82<br>
00:03:42,830 --> 00:03:45,230<br>
И нам удалось понять<br>
несколько вещей.<br>
<br>
83<br>
00:03:45,230 --> 00:03:47,770<br>
Первое, у нас есть вершины<br>
и есть долины.<br>
<br>
84<br>
00:03:47,770 --> 00:03:51,550<br>
Некоторые аспекты разработки<br>
прекрасно обслуживаются нашими API<br>
<br>
85<br>
00:03:51,550 --> 00:03:52,570<br>
другие - хуже.<br>
<br>
86<br>
00:03:52,570 --> 00:03:56,470<br>
Например, мы думаем, что<br>
RecyclerView это лучшая вершина<br>
<br>
87<br>
00:03:56,470 --> 00:03:57,830<br>
из этого спектра.<br>
<br>
88<br>
00:03:57,830 --> 00:04:02,020<br>
С RecyclerView, мы не говорим:<br>
эй, мы даем вам события,<br>
<br>
89<br>
00:04:02,020 --> 00:04:03,810<br>
и вы можете рисовать вещи.<br>
<br>
90<br>
00:04:03,810 --> 00:04:07,600<br>
И у вас есть тьюринг-полный язык,<br>
так что удачи<br>
<br>
91<br>
00:04:07,600 --> 00:04:09,550<br>
со всем остальным!<br>
<br>
92<br>
00:04:09,550 --> 00:04:12,640<br>
С другой стороны,<br>
возможно жизненные циклы<br>
<br>
93<br>
00:04:12,640 --> 00:04:16,510<br>
Activity и Fragment принадлежат<br>
к темным впадинам<br>
<br>
94<br>
00:04:16,510 --> 00:04:18,730<br>
потому что там, я<br>
думаю, оставлено действительно<br>
<br>
95<br>
00:04:18,730 --> 00:04:21,790<br>
слишком много упражнений<br>
для читателя [необходимо много читать].<br>
<br>
96<br>
00:04:21,790 --> 00:04:24,730<br>
И мы хотим исправить это.<br>
<br>
97<br>
00:04:24,730 --> 00:04:27,250<br>
Итак, мы думаем,<br>
что хорошее решение имеет<br>
<br>
98<br>
00:04:27,250 --> 00:04:29,930<br>
ключевые свойства.<br>
<br>
99<br>
00:04:29,930 --> 00:04:32,194<br>
Во-первых, мы обязаны находить<br>
правильные проблемы.<br>
<br>
100<br>
00:04:32,194 --> 00:04:33,860<br>
И это будет<br>
непрерывным усилием --<br>
<br>
101<br>
00:04:33,860 --> 00:04:36,320<br>
так же как и с нашей стороны<br>
для нас на Android.<br>
<br>
102<br>
00:04:36,320 --> 00:04:38,410<br>
Но для первого сокращения,<br>
мы хотим убедиться,<br>
<br>
103<br>
00:04:38,410 --> 00:04:39,910<br>
что мы будем решать<br>
проблемы, с которыми<br>
<br>
104<br>
00:04:39,910 --> 00:04:42,040<br>
сталкивается каждый разработчик.<br>
Те, которые трудно решить<br>
<br>
105<br>
00:04:42,040 --> 00:04:45,040<br>
прямо сейчас. Опять же,<br>
<br>
106<br>
00:04:45,040 --> 00:04:47,574<br>
жизненный цикл приложения - <br>
на самом деле хороший пример.<br>
<br>
107<br>
00:04:47,574 --> 00:04:49,240<br>
Если вы не получите это право<br>
[управлять циклом] в своем приложении,<br>
<br>
108<br>
00:04:49,240 --> 00:04:51,236<br>
на нем ничего<br>
не будет работать.<br>
<br>
109<br>
00:04:51,236 --> 00:04:53,110<br>
Это верно для вашего<br>
приложения, но так же<br>
<br>
110<br>
00:04:53,110 --> 00:04:55,026<br>
верно для фреймворков,<br>
которые мы пытаемся создавать.<br>
<br>
111<br>
00:04:55,026 --> 00:04:58,420<br>
Мы должны получить это право<br>
до того как можем сделать что-нибудь еще.<br>
<br>
112<br>
00:04:58,420 --> 00:05:00,370<br>
Второе, мы должны хорошо<br>
координировать свою работу с другими.<br>
<br>
113<br>
00:05:00,370 --> 00:05:02,830<br>
Мы знаем, что вы здорово<br>
вкладываетесь в существующие<br>
<br>
114<br>
00:05:02,830 --> 00:05:05,196<br>
модели программирования, и мы<br>
не можем создать модель,<br>
<br>
115<br>
00:05:05,196 --> 00:05:06,820<br>
где сразу скажем<br>
вам, чтобы вы,<br>
<br>
116<br>
00:05:06,820 --> 00:05:08,940<br>
бросили все старое<br>
и начали сначала.<br>
<br>
117<br>
00:05:08,940 --> 00:05:12,070<br>
Итак, мы стараемся создать API,<br>
на которое вы не потратите много<br>
<br>
118<br>
00:05:12,070 --> 00:05:15,580<br>
времени, и также которое<br>
хорошо взаимодействует<br>
<br>
119<br>
00:05:15,580 --> 00:05:19,710<br>
с другими библиотеками<br>
и другими фреймворками.<br>
<br>
120<br>
00:05:19,710 --> 00:05:22,054<br>
В-третьих, мы хотим быть<br>
более настойчивыми.<br>
<br>
121<br>
00:05:22,054 --> 00:05:23,970<br>
Мы собираемся занять более<br>
сильную и четкую позицию<br>
<br>
122<br>
00:05:23,970 --> 00:05:26,000<br>
о том, каким должен быть<br>
правильный путь развития Android,<br>
<br>
123<br>
00:05:26,000 --> 00:05:27,100<br>
По крайней мере, как мы это видим.<br>
<br>
124<br>
00:05:27,100 --> 00:05:29,100<br>
Теперь, это все еще необязательно.<br>
<br>
125<br>
00:05:29,100 --> 00:05:31,330<br>
И если у вас уже есть,<br>
то, что работает для вас,<br>
<br>
126<br>
00:05:31,330 --> 00:05:33,030<br>
то это здорово.<br>
<br>
127<br>
00:05:33,030 --> 00:05:36,210<br>
Но разработчики говорят нам,<br>
что хотели бы большей ясности о том,<br>
<br>
128<br>
00:05:36,210 --> 00:05:38,590<br>
как следует строить приложения.<br>
И к слову<br>
<br>
129<br>
00:05:38,590 --> 00:05:40,770<br>
мы не меняем "законов<br>
физики" [core Android] здесь,<br>
<br>
130<br>
00:05:40,770 --> 00:05:43,860<br>
мы просто меняем конструкции<br>
более высокого уровня.<br>
<br>
131<br>
00:05:43,860 --> 00:05:46,620<br>
Потому что сила будет равна масса<br>
умножить на ускорение несмотря на то<br>
<br>
132<br>
00:05:46,620 --> 00:05:49,860<br>
верите ли вы в это или нет.<br>
<br>
133<br>
00:05:49,860 --> 00:05:52,140<br>
Следующее, необходимо масштабировать.<br>
<br>
134<br>
00:05:52,140 --> 00:05:54,420<br>
Нам нужны решения, которые<br>
обладают индустриальной мощью<br>
<br>
135<br>
00:05:54,420 --> 00:05:56,760<br>
и могут масштабироваться<br>
под реальные мировые требования<br>
<br>
136<br>
00:05:56,760 --> 00:05:58,474<br>
реальных приложений.<br>
<br>
137<br>
00:05:58,474 --> 00:06:01,140<br>
Мы не хотим создавать что-то,<br>
что хорошо работает для Hello World,<br>
<br>
138<br>
00:06:01,140 --> 00:06:03,181<br>
но сдает позиции сразу же <br>
при первом использовании,<br>
<br>
139<br>
00:06:03,181 --> 00:06:07,620<br>
когда сталкивается с суровой,<br>
сложной реальностью.<br>
<br>
140<br>
00:06:07,620 --> 00:06:09,410<br>
И наконец, поддержка и обогащение [версий Android].<br>
<br>
141<br>
00:06:09,410 --> 00:06:11,310<br>
Для [решения] этой проблемы,<br>
для упрощения<br>
<br>
142<br>
00:06:11,310 --> 00:06:13,830<br>
написания приложений Android<br>
правильным способом --<br>
<br>
143<br>
00:06:13,830 --> 00:06:15,690<br>
мы думаем,<br>
что будет правильным<br>
<br>
144<br>
00:06:15,690 --> 00:06:18,390<br>
использовать библиотеки наподобие<br>
Support Lib где это только возможно,<br>
<br>
145<br>
00:06:18,390 --> 00:06:21,150<br>
а не добавлять новые<br>
API на платформу,<br>
<br>
146<br>
00:06:21,150 --> 00:06:24,030<br>
потому что таким образом мы<br>
сможем обогатить старые версии ОС<br>
<br>
147<br>
00:06:24,030 --> 00:06:26,745<br>
так же.<br>
<br>
148<br>
00:06:26,745 --> 00:06:29,370<br>
OK, это то на чем мы основываемся,<br>
что, что мы пытаемся осуществить,<br>
<br>
149<br>
00:06:29,370 --> 00:06:30,440<br>
и почему мы находимся здесь.<br>
<br>
150<br>
00:06:30,440 --> 00:06:33,309<br>
Теперь мы бы хотели представить<br>
Yigit, инженера средств разработки.<br>
<br>
151<br>
00:06:33,309 --> 00:06:35,600<br>
И он собирается рассказать вам<br>
как мы это<br>
<br>
152<br>
00:06:35,600 --> 00:06:36,860<br>
осуществляли на практике. Спасибо.<br>
<br>
153<br>
00:06:36,860 --> 00:06:37,290<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
154<br>
00:06:37,290 --> 00:06:38,248<br>
YIGIT BOYAR: Хорошо.<br>
<br>
155<br>
00:06:38,248 --> 00:06:39,322<br>
Спасибо, Frank.<br>
<br>
156<br>
00:06:39,322 --> 00:06:43,610<br>
<br>
<br>
157<br>
00:06:43,610 --> 00:06:44,410<br>
Привет всем.<br>
<br>
158<br>
00:06:44,410 --> 00:06:46,930<br>
Итак, это было то, на чем мы основываемся.<br>
<br>
159<br>
00:06:46,930 --> 00:06:49,050<br>
К чему мы идем сегодня?<br>
<br>
160<br>
00:06:49,050 --> 00:06:51,210<br>
Первая вещь<br>
к которой мы идем<br>
<br>
161<br>
00:06:51,210 --> 00:06:55,230<br>
это руководство по архитектуре<br>
на developer Android com.<br>
<br>
162<br>
00:06:55,230 --> 00:06:58,440<br>
На протяжении многих лет вы<br>
спрашивали наше мнение,<br>
<br>
163<br>
00:06:58,440 --> 00:07:02,220<br>
как по-нашему приложение<br>
должно быть построено?<br>
<br>
164<br>
00:07:02,220 --> 00:07:03,900<br>
И это и есть это руководство.<br>
<br>
165<br>
00:07:03,900 --> 00:07:06,270<br>
И мы считаем, что<br>
оно достаточно хорошо,<br>
<br>
166<br>
00:07:06,270 --> 00:07:08,730<br>
и покрывает большинство<br>
видов приложений.<br>
<br>
167<br>
00:07:08,730 --> 00:07:10,890<br>
Но даже если вы имеете<br>
свою архитектуру<br>
<br>
168<br>
00:07:10,890 --> 00:07:14,040<br>
которая удобна для вас,<br>
вы можете сохранять ее.<br>
<br>
169<br>
00:07:14,040 --> 00:07:18,300<br>
Но вы можете попробовать узнать<br>
что-то новое из этого руководства<br>
<br>
170<br>
00:07:18,300 --> 00:07:20,910<br>
Во-вторых, мы движемся к созданию <br>
нового набора библиотек,<br>
<br>
171<br>
00:07:20,910 --> 00:07:23,290<br>
которые мы называем<br>
архитектурные компоненты.<br>
<br>
172<br>
00:07:23,290 --> 00:07:24,900<br>
Это более фундаментальные<br>
компоненты [строительные блоки]<br>
<br>
173<br>
00:07:24,900 --> 00:07:28,440<br>
на которых вы можете<br>
основывать ваше приложение.<br>
<br>
174<br>
00:07:28,440 --> 00:07:29,760<br>
Первая вещь - жизненный цикл.<br>
<br>
175<br>
00:07:29,760 --> 00:07:33,000<br>
Это самая частая жалоба,<br>
которую мы получаем от разработчиков.<br>
<br>
176<br>
00:07:33,000 --> 00:07:35,610<br>
Жизненный цикл сложен,<br>
Жизненный цикл сложен.<br>
<br>
177<br>
00:07:35,610 --> 00:07:38,020<br>
И мы сказали "ОК", нам<br>
следует решить эту проблему.<br>
<br>
178<br>
00:07:38,020 --> 00:07:41,850<br>
И первый шаг для этого,<br>
это новый набор компонентов.<br>
<br>
179<br>
00:07:41,850 --> 00:07:44,070<br>
Второе - это учитывающие<br>
жизненный цикл Observables,<br>
<br>
180<br>
00:07:44,070 --> 00:07:46,860<br>
которые в деталях будут рассмотрены<br>
позже, но базово это<br>
<br>
181<br>
00:07:46,860 --> 00:07:51,730<br>
сделать что-то, базируясь<br>
на жизненном цикле.<br>
<br>
182<br>
00:07:51,730 --> 00:07:54,810<br>
В-третьих, мы собираемся представить<br>
легковесные ViewModel, которые<br>
<br>
183<br>
00:07:54,810 --> 00:07:58,020<br>
помогут вывести<br>
ваш код<br>
<br>
184<br>
00:07:58,020 --> 00:08:00,150<br>
наружу из ваших<br>
Activities и Fragments,<br>
<br>
185<br>
00:08:00,150 --> 00:08:03,550<br>
и поместить его где-нибудь еще,<br>
где вы сможете легко протестировать его.<br>
<br>
186<br>
00:08:03,550 --> 00:08:06,630<br>
И последнее, но не менее важное,<br>
мы собираемся представить новый объект<br>
<br>
187<br>
00:08:06,630 --> 00:08:10,290<br>
mapping library для SQLite.<br>
<br>
188<br>
00:08:10,290 --> 00:08:15,248<br>
И все это доступно для вас<br>
сегодня на Maven Google com.<br>
<br>
189<br>
00:08:15,248 --> 00:08:24,290<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
190<br>
00:08:24,290 --> 00:08:25,790<br>
Давайте поговорим о жизненных циклах.<br>
<br>
191<br>
00:08:25,790 --> 00:08:27,830<br>
Итак, что же сложного<br>
в жизненных циклах?<br>
<br>
192<br>
00:08:27,830 --> 00:08:29,970<br>
Почему мы слышим так много<br>
жалоб об этом?<br>
<br>
193<br>
00:08:29,970 --> 00:08:31,510<br>
Давайте перейдем к примеру.<br>
<br>
194<br>
00:08:31,510 --> 00:08:33,440<br>
Предположим, что у нас есть<br>
Activity где мы<br>
<br>
195<br>
00:08:33,440 --> 00:08:36,591<br>
хотим выводить местоположение<br>
устройства на экран.<br>
<br>
196<br>
00:08:36,591 --> 00:08:38,090<br>
Итак, вы попробуете сделать<br>
что-то вроде этого.<br>
<br>
197<br>
00:08:38,090 --> 00:08:41,280<br>
Вы создадите LocationListener<br>
в методе onCreate(),<br>
<br>
198<br>
00:08:41,280 --> 00:08:43,250<br>
вам нужно будет инициализировать<br>
его контекстом [Context],<br>
<br>
199<br>
00:08:43,250 --> 00:08:46,520<br>
и у вас будет обратный вызов [callback],<br>
который вызывается всякий раз, когда<br>
<br>
200<br>
00:08:46,520 --> 00:08:48,800<br>
локация меняется, и вы обновляете UI.<br>
<br>
201<br>
00:08:48,800 --> 00:08:51,230<br>
Теперь, если вы когда-либо<br>
писали приложение на Android,<br>
<br>
202<br>
00:08:51,230 --> 00:08:54,330<br>
вы знаете, что этого<br>
кода недостаточно.<br>
<br>
203<br>
00:08:54,330 --> 00:08:57,440<br>
Вам также нужно пойти дальше и<br>
переопределить onStart(), и затем<br>
<br>
204<br>
00:08:57,440 --> 00:09:01,880<br>
дать команду начинать, и переопределить<br>
onStop(), и дать команду остановиться.<br>
<br>
205<br>
00:09:01,880 --> 00:09:04,040<br>
Вы всегда должны<br>
таким образом присматривать<br>
<br>
206<br>
00:09:04,040 --> 00:09:05,510<br>
за этими компонентами.<br>
<br>
207<br>
00:09:05,510 --> 00:09:06,840<br>
Но это приемлемо.<br>
<br>
208<br>
00:09:06,840 --> 00:09:09,680<br>
Это простой пример,<br>
это выглядит хорошо.<br>
<br>
209<br>
00:09:09,680 --> 00:09:11,750<br>
Но тогда появляется ваш<br>
Product Manager и говорит,<br>
<br>
210<br>
00:09:11,750 --> 00:09:12,560<br>
"О, ды та знаешь что?"<br>
<br>
211<br>
00:09:12,560 --> 00:09:16,160<br>
"Нам необходимо проверить сначала<br>
настройки пользователя перед разрешением--<br>
<br>
212<br>
00:09:16,160 --> 00:09:17,710<br>
спрашивать о местоположении."<br>
<br>
213<br>
00:09:17,710 --> 00:09:22,160<br>
Тогда вам разработчик скажет "OK"<br>
конечно, "Это просто изменить."<br>
<br>
214<br>
00:09:22,160 --> 00:09:25,570<br>
"Я изменю этот метод, который<br>
будет вызывать утилиту,<br>
<br>
215<br>
00:09:25,570 --> 00:09:27,980<br>
которая, вероятно, сделает<br>
запрос к веб-сервису<br>
<br>
216<br>
00:09:27,980 --> 00:09:29,900<br>
и проверить настройки пользователя.<br>
<br>
217<br>
00:09:29,900 --> 00:09:32,030<br>
И тогда, если<br>
пользователь зарегистрирован,<br>
<br>
218<br>
00:09:32,030 --> 00:09:34,160<br>
мы запустим наш<br>
LocationListener."<br>
<br>
219<br>
00:09:34,160 --> 00:09:37,010<br>
Это похоже на<br>
очень простое изменение,<br>
<br>
220<br>
00:09:37,010 --> 00:09:39,440<br>
вы подумаете, что это могло бы<br>
сработать, но давайте посмотрим,<br>
<br>
221<br>
00:09:39,440 --> 00:09:42,440<br>
что происходит в жизненном цикле<br>
этой Activity.<br>
<br>
222<br>
00:09:42,440 --> 00:09:43,990<br>
Итак наша Activity была создана.<br>
<br>
223<br>
00:09:43,990 --> 00:09:49,526<br>
Мы говорим "OK", запускаем проверку<br>
зарегистрирован ли пользователь.<br>
<br>
224<br>
00:09:49,526 --> 00:09:52,370<br>
Но вдруг, пользователь захотел<br>
повернуть устройство.<br>
<br>
225<br>
00:09:52,370 --> 00:09:54,930<br>
И поворот означает<br>
смену конфигурации,<br>
<br>
226<br>
00:09:54,930 --> 00:09:58,430<br>
что означает, что Android начнет<br>
пересоздавать Activity.<br>
<br>
227<br>
00:09:58,430 --> 00:10:00,200<br>
Итак в onStop(), мы<br>
узнаем об этом,<br>
<br>
228<br>
00:10:00,200 --> 00:10:03,292<br>
и мы скажем "OK"<br>
location manager остановился.<br>
<br>
229<br>
00:10:03,292 --> 00:10:05,780<br>
И затем появляется новая<br>
Activity, и она также<br>
<br>
230<br>
00:10:05,780 --> 00:10:07,430<br>
проходит через то же самое.<br>
<br>
231<br>
00:10:07,430 --> 00:10:10,280<br>
Выглядит хорошо, исключая,<br>
как вы помните, наш запрос, <br>
<br>
232<br>
00:10:10,280 --> 00:10:12,140<br>
который мы сделали до того.<br>
<br>
233<br>
00:10:12,140 --> 00:10:15,400<br>
Это маленькое изменение [поворот],<br>
и затем запрос возвращает ответ.<br>
<br>
234<br>
00:10:15,400 --> 00:10:17,110<br>
"Эй, пользователь зарегистрирован".<br>
<br>
235<br>
00:10:17,110 --> 00:10:18,080<br>
И что мы тогда делаем?<br>
<br>
236<br>
00:10:18,080 --> 00:10:20,790<br>
Мы скажем "OK, стартуй!".<br>
<br>
237<br>
00:10:20,790 --> 00:10:22,250<br>
И вы осознаете [НЕРАЗБОРЧИВО]?<br>
<br>
238<br>
00:10:22,250 --> 00:10:26,510<br>
Мы вызываем onStart() после<br>
вызова onStop(), это означает,<br>
<br>
239<br>
00:10:26,510 --> 00:10:28,700<br>
наша Activity будет жить вечно.<br>
<br>
240<br>
00:10:28,700 --> 00:10:31,130<br>
Мы будем наблюдать это<br>
местоположение вечно,<br>
<br>
241<br>
00:10:31,130 --> 00:10:32,257<br>
пока батарея не разрядится.<br>
<br>
242<br>
00:10:32,257 --> 00:10:33,215<br>
Мы опечалим наших пользователей.<br>
<br>
243<br>
00:10:33,215 --> 00:10:37,078<br>
<br>
<br>
244<br>
00:10:37,078 --> 00:10:38,600<br>
Знакомая ситуация, не так ли?<br>
<br>
245<br>
00:10:38,600 --> 00:10:40,220<br>
Мы хотим избавиться от этого.<br>
<br>
246<br>
00:10:40,220 --> 00:10:41,840<br>
Мы хотим положить этому конец.<br>
<br>
247<br>
00:10:41,840 --> 00:10:43,950<br>
Итак, мы говорим "OK", нам<br>
нужно признать -<br>
<br>
248<br>
00:10:43,950 --> 00:10:46,670<br>
как упоминал Майк,<br>
мы не можем изменить законы.<br>
<br>
249<br>
00:10:46,670 --> 00:10:49,670<br>
Но мы можем поступить проще:<br>
иметь дело с вещами.<br>
<br>
250<br>
00:10:49,670 --> 00:10:52,430<br>
Поэтому мы решили ввести<br>
новый интерфейс называемый<br>
<br>
251<br>
00:10:52,430 --> 00:10:53,970<br>
LifecycleOwner.<br>
<br>
252<br>
00:10:53,970 --> 00:10:55,970<br>
Эта вещь идет вместе с<br>
жизненным циклом.<br>
<br>
253<br>
00:10:55,970 --> 00:10:58,400<br>
Если у вас Activity, или<br>
ваш Fragment - или, возможно,<br>
<br>
254<br>
00:10:58,400 --> 00:11:02,270<br>
ваш собственный UI фреймворк,<br>
независимо от того, что у вас есть,<br>
<br>
255<br>
00:11:02,270 --> 00:11:05,570<br>
это можно представить, как LifecycleOwner.<br>
<br>
256<br>
00:11:05,570 --> 00:11:08,780<br>
И у нас есть [наблюдатели] <br>
LifecycleObservers,<br>
<br>
257<br>
00:11:08,780 --> 00:11:11,180<br>
цель которых заботиться<br>
о жизненном цикле.<br>
<br>
258<br>
00:11:11,180 --> 00:11:13,310<br>
Как и в<br>
LocationListener у нас было,<br>
<br>
259<br>
00:11:13,310 --> 00:11:16,580<br>
он заботится о жизненном цикле,<br>
хочет остановить себя<br>
<br>
260<br>
00:11:16,580 --> 00:11:18,680<br>
Если жизненный цикл не активен.<br>
<br>
261<br>
00:11:18,680 --> 00:11:21,130<br>
Итак, мы сказали "OK, <br>
мы признаем это.<br>
<br>
262<br>
00:11:21,130 --> 00:11:23,600<br>
И у нас есть<br>
LifecycleObservers."<br>
<br>
263<br>
00:11:23,600 --> 00:11:26,090<br>
Мы пройдем через код<br>
в нашей Acivity.<br>
<br>
264<br>
00:11:26,090 --> 00:11:30,080<br>
Сейчас мы наследуем нашу Activity<br>
от класса LifecycleActivity.<br>
<br>
265<br>
00:11:30,080 --> 00:11:33,320<br>
Это лишь временный класс<br>
пока эти компоненты дойдут<br>
<br>
266<br>
00:11:33,320 --> 00:11:34,410<br>
до версии 1.0.<br>
<br>
267<br>
00:11:34,410 --> 00:11:35,900<br>
Затем все в<br>
Support Library<br>
<br>
268<br>
00:11:35,900 --> 00:11:39,980<br>
реализует интерфейс<br>
LifecycleOwner.<br>
<br>
269<br>
00:11:39,980 --> 00:11:42,550<br>
Внутри нашей Activity,<br>
где мы инициализируем<br>
<br>
270<br>
00:11:42,550 --> 00:11:45,710<br>
наш LocationListener,<br>
мы собираемя сказать, что<br>
<br>
271<br>
00:11:45,710 --> 00:11:48,240<br>
это наш жизненный цикл,<br>
о котором мы заботимся.<br>
<br>
272<br>
00:11:48,240 --> 00:11:50,390<br>
И это все, что мы делаем.<br>
<br>
273<br>
00:11:50,390 --> 00:11:54,410<br>
Но поскольку это то же самое,<br>
он вызывает обновление UI.<br>
<br>
274<br>
00:11:54,410 --> 00:11:57,020<br>
Итак, как мы можем изменить<br>
наш LocationListener<br>
<br>
275<br>
00:11:57,020 --> 00:12:00,890<br>
используя преимущества<br>
этого жизненного цикла?<br>
<br>
276<br>
00:12:00,890 --> 00:12:03,500<br>
О, мы делаем тоже самое<br>
для UserStatus также.<br>
<br>
277<br>
00:12:03,500 --> 00:12:06,240<br>
<br>
<br>
278<br>
00:12:06,240 --> 00:12:08,880<br>
Итак, есть некоторые шаблоны<br>
кода здесь, чтобы получить поля.<br>
<br>
279<br>
00:12:08,880 --> 00:12:10,950<br>
Это на самом деле<br>
не важно, но у нас есть<br>
<br>
280<br>
00:12:10,950 --> 00:12:14,850<br>
этот метод, enable(), который вызывается,<br>
если пользователь зарегистрирован.<br>
<br>
281<br>
00:12:14,850 --> 00:12:16,500<br>
Внутри этого метода<br>
мы теперь<br>
<br>
282<br>
00:12:16,500 --> 00:12:18,420<br>
хотим начать<br>
отслеживать местоположение<br>
<br>
283<br>
00:12:18,420 --> 00:12:21,360<br>
только, если Activity запущена.<br>
<br>
284<br>
00:12:21,360 --> 00:12:23,040<br>
Теперь вы можете сделать это.<br>
<br>
285<br>
00:12:23,040 --> 00:12:26,590<br>
Вы можете узнать, какое ваше текущее<br>
состояние, и это удивительно.<br>
<br>
286<br>
00:12:26,590 --> 00:12:29,370<br>
У нас не было<br>
такого API до сих пор.<br>
<br>
287<br>
00:12:29,370 --> 00:12:32,010<br>
Ну, теперь вы можете это.<br>
<br>
288<br>
00:12:32,010 --> 00:12:34,110<br>
Итак, хорошо, это было простое изменение.<br>
<br>
289<br>
00:12:34,110 --> 00:12:36,510<br>
Но мы также получаем уведомление,<br>
что мы зарегистрированы,<br>
<br>
290<br>
00:12:36,510 --> 00:12:38,710<br>
когда Activity<br>
будет не в активном состоянии,<br>
<br>
291<br>
00:12:38,710 --> 00:12:40,800<br>
и пользователь<br>
вернется к Activity.<br>
<br>
292<br>
00:12:40,800 --> 00:12:43,290<br>
Теперь нам следует на самом деле<br>
запустить LocationManager.<br>
<br>
293<br>
00:12:43,290 --> 00:12:46,290<br>
Для этого мы хотим наблюдать за<br>
жизненным циклом.<br>
<br>
294<br>
00:12:46,290 --> 00:12:48,690<br>
Здесь мы имплементируем<br>
этот интерфейс,<br>
<br>
295<br>
00:12:48,690 --> 00:12:50,670<br>
который позволяет нам<br>
использовать эти методы.<br>
<br>
296<br>
00:12:50,670 --> 00:12:52,710<br>
Вы можете аннотировать эти<br>
методы, говоря что,<br>
<br>
297<br>
00:12:52,710 --> 00:12:56,152<br>
если ON_START<br>
случился, вызывай этот метод.<br>
<br>
298<br>
00:12:56,152 --> 00:12:58,360<br>
И новые компоненты будут<br>
заботиться о вызовах.<br>
<br>
299<br>
00:12:58,360 --> 00:13:00,660<br>
Итак, если вы теперь доступны,<br>
то теперь вы начинаете,<br>
<br>
300<br>
00:13:00,660 --> 00:13:03,540<br>
и если ON_STOP<br>
вы отключаетесь.<br>
<br>
301<br>
00:13:03,540 --> 00:13:06,700<br>
И последнее по порядку, но не по значимости,<br>
Если Activity остановлено и уничтожено,<br>
<br>
302<br>
00:13:06,700 --> 00:13:09,220<br>
вам ничего не нужно делать<br>
с этой Activity<br>
<br>
303<br>
00:13:09,220 --> 00:13:11,796<br>
Вы можете разрегистрироваться.<br>
<br>
304<br>
00:13:11,796 --> 00:13:13,920<br>
Итак, вы тогда можете скать себе:<br>
"Хорошо, вы просто<br>
<br>
305<br>
00:13:13,920 --> 00:13:16,710<br>
перенесли эти ON_START, ON_STOP<br>
методы из Activity<br>
<br>
306<br>
00:13:16,710 --> 00:13:18,450<br>
в Location Manager.<br>
<br>
307<br>
00:13:18,450 --> 00:13:20,150<br>
Почему это проще?"<br>
<br>
308<br>
00:13:20,150 --> 00:13:22,250<br>
Это проще потому, что<br>
эти методы<br>
<br>
309<br>
00:13:22,250 --> 00:13:23,610<br>
находятся в правильном месте.<br>
<br>
310<br>
00:13:23,610 --> 00:13:27,690<br>
И это LocationManager, который<br>
заботиться о жизненном цикле.<br>
<br>
311<br>
00:13:27,690 --> 00:13:30,780<br>
И это следует делать<br>
без того, чтобы Activity<br>
<br>
312<br>
00:13:30,780 --> 00:13:32,460<br>
нянчила сама себя.<br>
<br>
313<br>
00:13:32,460 --> 00:13:34,170<br>
Я уверен, если вы посмотрите<br>
в ваш код сегодня,<br>
<br>
314<br>
00:13:34,170 --> 00:13:37,260<br>
в вашей Activity методы<br>
ON_START, ON_STOP, будут занимать,<br>
<br>
315<br>
00:13:37,260 --> 00:13:38,730<br>
не менее 20-30 строк кода.<br>
<br>
316<br>
00:13:38,730 --> 00:13:42,060<br>
Мы хотим, чтобы они<br>
занимали 0 строк кода.<br>
<br>
317<br>
00:13:42,060 --> 00:13:43,800<br>
И если мы вернемся к Activity,<br>
я хочу указать<br>
<br>
318<br>
00:13:43,800 --> 00:13:45,780<br>
на кое-что -<br>
<br>
319<br>
00:13:45,780 --> 00:13:49,260<br>
Смотрите, в onCreate(), мы<br>
инициализируем эти компоненты.<br>
<br>
320<br>
00:13:49,260 --> 00:13:50,580<br>
И это все, что мы делаем.<br>
<br>
321<br>
00:13:50,580 --> 00:13:53,230<br>
Мы не переопределяем, мы<br>
не пишем ON_STOP, ON_START,<br>
<br>
322<br>
00:13:53,230 --> 00:13:55,020<br>
мы не переопределяем<br>
никакие из этих сущностей,<br>
<br>
323<br>
00:13:55,020 --> 00:13:59,630<br>
потому что LocationManager это компонент,<br>
осведомленный о жизненном цикле<br>
<br>
324<br>
00:13:59,630 --> 00:14:01,875<br>
теперь.<br>
<br>
325<br>
00:14:01,875 --> 00:14:03,990<br>
Итак, это новая концепция,<br>
которую мы хотим представить.<br>
<br>
326<br>
00:14:03,990 --> 00:14:08,130<br>
Компонент осведомленный о жизненном<br>
цикле, может получить его состояние,<br>
<br>
327<br>
00:14:08,130 --> 00:14:09,170<br>
и поступать правильно таким образом.<br>
<br>
328<br>
00:14:09,170 --> 00:14:12,210<br>
Он может заботиться о себе сам,<br>
так что в вашей Activity<br>
<br>
329<br>
00:14:12,210 --> 00:14:15,120<br>
вы можете просто инициализировать<br>
это и забыть об этом.<br>
<br>
330<br>
00:14:15,120 --> 00:14:19,060<br>
Вы можете не беспокоиться,<br>
что это утечет от вас.<br>
<br>
331<br>
00:14:19,060 --> 00:14:22,480<br>
Теперь, конечно, это было похоже<br>
на перемещение комплекса<br>
<br>
332<br>
00:14:22,480 --> 00:14:24,520<br>
из Activity в<br>
LocationManager,<br>
<br>
333<br>
00:14:24,520 --> 00:14:27,310<br>
и затем все еще нужно<br>
иметь дело с  жизненным циклом.<br>
<br>
334<br>
00:14:27,310 --> 00:14:29,190<br>
Мы сказали "OK, чего мы хотим?"<br>
<br>
335<br>
00:14:29,190 --> 00:14:32,540<br>
Это приятно суметь сделать это,<br>
но мы хотим большего.<br>
<br>
336<br>
00:14:32,540 --> 00:14:35,230<br>
Мы хотим больше удобства<br>
для обработки этого общего случая.<br>
<br>
337<br>
00:14:35,230 --> 00:14:38,390<br>
Довольно часто бывает, что<br>
ваша Activity или Fragment<br>
<br>
338<br>
00:14:38,390 --> 00:14:41,830<br>
наблюдают некоторые данные, и<br>
всякий раз, когда данные меняются,<br>
<br>
339<br>
00:14:41,830 --> 00:14:43,300<br>
они хотят обновить свое состояние.<br>
<br>
340<br>
00:14:43,300 --> 00:14:46,910<br>
Это случается практически<br>
в каждом пользовательском UI.<br>
<br>
341<br>
00:14:46,910 --> 00:14:49,870<br>
И мы хотим подеиться ресурсами<br>
через несколько Fragments<br>
<br>
342<br>
00:14:49,870 --> 00:14:51,250<br>
или Activities.<br>
<br>
343<br>
00:14:51,250 --> 00:14:54,580<br>
Местоположение устройства одинаково<br>
от фрагмента<br>
<br>
344<br>
00:14:54,580 --> 00:14:55,240<br>
к фрагменту.<br>
<br>
345<br>
00:14:55,240 --> 00:14:57,040<br>
И если у вас два Fragment'a,<br>
почему вы должны создавать<br>
<br>
346<br>
00:14:57,040 --> 00:15:01,610<br>
два Listener'a, чтобы слушать<br>
одно и то же местоположение?<br>
<br>
347<br>
00:15:01,610 --> 00:15:05,080<br>
Следовательно, мы создали<br>
новую штуку: LiveData.<br>
<br>
348<br>
00:15:05,080 --> 00:15:06,600<br>
Давайте посмотрим что это.<br>
<br>
349<br>
00:15:06,600 --> 00:15:10,390<br>
Итак, LiveData это держатель данных,<br>
он просто содержит некоторые данные.<br>
<br>
350<br>
00:15:10,390 --> 00:15:13,690<br>
Это похоже на слушателя, но<br>
LiveData более хитрая вещь,<br>
<br>
351<br>
00:15:13,690 --> 00:15:15,760<br>
которая знает о жизненном цикле.<br>
<br>
352<br>
00:15:15,760 --> 00:15:18,310<br>
Он понимает жизненный цикл.<br>
<br>
353<br>
00:15:18,310 --> 00:15:20,820<br>
Он понимает о жизненном<br>
цикле потому,<br>
<br>
354<br>
00:15:20,820 --> 00:15:22,850<br>
что автоматически<br>
управляет подписками.<br>
<br>
355<br>
00:15:22,850 --> 00:15:25,220<br>
Так что очень похоже<br>
на предыдущий пример,<br>
<br>
356<br>
00:15:25,220 --> 00:15:29,290<br>
и если вы наблюдаете LiveData,<br>
вам нет необходимости отписываться.<br>
<br>
357<br>
00:15:29,290 --> 00:15:33,040<br>
Нужные вещи будут происходить<br>
в нужное время.<br>
<br>
358<br>
00:15:33,040 --> 00:15:37,660<br>
Так что если бы LocationListener<br>
был LiveData, и был singleton<br>
<br>
359<br>
00:15:37,660 --> 00:15:40,000<br>
потому что метоположение это<br>
singleton, мы могли бы<br>
<br>
360<br>
00:15:40,000 --> 00:15:41,800<br>
написать что-то вроде этого -<br>
<br>
361<br>
00:15:41,800 --> 00:15:43,930<br>
get distance, start observing.<br>
<br>
362<br>
00:15:43,930 --> 00:15:47,280<br>
И когда вы наблюдаете, вы<br>
говорите: "Это мой жизненный цикл".<br>
<br>
363<br>
00:15:47,280 --> 00:15:48,280<br>
Это все, что вам нужно сделать.<br>
<br>
364<br>
00:15:48,280 --> 00:15:51,880<br>
Раньше на Android, если вы<br>
наблюдали что-то, что было singleton<br>
<br>
365<br>
00:15:51,880 --> 00:15:55,180<br>
из Activity, каждый<br>
снизит вам два балла<br>
<br>
366<br>
00:15:55,180 --> 00:15:56,650<br>
при обзоре этого кода.<br>
<br>
367<br>
00:15:56,650 --> 00:15:57,805<br>
Теперь вы можете делать это.<br>
<br>
368<br>
00:15:57,805 --> 00:16:01,600<br>
Это безопасно,<br>
это не грозит утечками.<br>
<br>
369<br>
00:16:01,600 --> 00:16:03,790<br>
Итак, если вы захотите изменить<br>
ваш LocationListener<br>
<br>
370<br>
00:16:03,790 --> 00:16:07,430<br>
используйте это API, мы<br>
избавились от ненужных вещей.<br>
<br>
371<br>
00:16:07,430 --> 00:16:09,590<br>
Все, что нам нужно,<br>
Это Context для подключения.<br>
<br>
372<br>
00:16:09,590 --> 00:16:15,540<br>
Что мы говорим: это LiveData,<br>
это LiveData местоположения.<br>
<br>
373<br>
00:16:15,540 --> 00:16:18,110<br>
и мы даем эти два<br>
новых метода.<br>
<br>
374<br>
00:16:18,110 --> 00:16:20,520<br>
Один из двух называется<br>
onActive(), что значит<br>
<br>
375<br>
00:16:20,520 --> 00:16:22,920<br>
у вас есть активный наблюдатель.<br>
<br>
376<br>
00:16:22,920 --> 00:16:24,475<br>
Другой называется<br>
onInactive(),<br>
<br>
377<br>
00:16:24,475 --> 00:16:27,555<br>
что означает, что у вас нет<br>
ни одного активного наблюдателя.<br>
<br>
378<br>
00:16:27,555 --> 00:16:30,360<br>
Теперь, на данный момент, вы,<br>
возможно, спрашиваете себя:<br>
<br>
379<br>
00:16:30,360 --> 00:16:32,590<br>
"Что такое активный наблюдатель?"<br>
<br>
380<br>
00:16:32,590 --> 00:16:34,290<br>
Хорошо, мы дадим определение<br>
активному наблюдателю.<br>
<br>
381<br>
00:16:34,290 --> 00:16:37,710<br>
Это наблюдатель который находится<br>
в состоянии START или RESUME, который<br>
<br>
382<br>
00:16:37,710 --> 00:16:40,440<br>
как пользователь Activity,<br>
в настоящее время смотрит.<br>
<br>
383<br>
00:16:40,440 --> 00:16:43,020<br>
Итак, если у вас есть наблюдатель<br>
на заднем фоне,<br>
<br>
384<br>
00:16:43,020 --> 00:16:45,300<br>
Нет никаких оснований полагать<br>
что она не активна.<br>
<br>
385<br>
00:16:45,300 --> 00:16:47,190<br>
Нет причин<br>
обновлять Activity<br>
<br>
386<br>
00:16:47,190 --> 00:16:49,950<br>
потому что пользователь никогда<br>
не увидит, что там происходит.<br>
<br>
387<br>
00:16:49,950 --> 00:16:53,390<br>
<br>
<br>
388<br>
00:16:53,390 --> 00:16:56,130<br>
Т.к. внутри нашего метода connect(),<br>
все, что мы должны сделать<br>
<br>
389<br>
00:16:56,130 --> 00:16:58,540<br>
это всякий раз, когда<br>
LocationManager отправляет нам<br>
<br>
390<br>
00:16:58,540 --> 00:17:02,120<br>
новое местоположение, мы<br>
вызываем setValue() с ним.<br>
<br>
391<br>
00:17:02,120 --> 00:17:05,589<br>
Тогда LiveData знает какие<br>
наблюдатели активны,<br>
<br>
392<br>
00:17:05,589 --> 00:17:08,410<br>
и предоставляет данные<br>
этим наблюдателям.<br>
<br>
393<br>
00:17:08,410 --> 00:17:11,930<br>
Или, если один из наблюдателей<br>
был в фоне<br>
<br>
394<br>
00:17:11,930 --> 00:17:14,290<br>
и зате снова стал<br>
видимым, то LiveData<br>
<br>
395<br>
00:17:14,290 --> 00:17:17,079<br>
Позаботится о том, чтобы<br>
отправить последние данные.<br>
<br>
396<br>
00:17:17,079 --> 00:17:19,608<br>
этому наблюдателю.<br>
<br>
397<br>
00:17:19,608 --> 00:17:22,858<br>
И тогда мы сможем сделать наш<br>
LocationListener singleton объектом<br>
<br>
398<br>
00:17:22,858 --> 00:17:26,019<br>
потому как мы не нуждаемся<br>
в нескольких экземплярах.<br>
<br>
399<br>
00:17:26,020 --> 00:17:30,400<br>
Итак, если мы взглянем на LiveData, то<br>
это жизненный цикл знающий о наблюдателе.<br>
<br>
400<br>
00:17:30,400 --> 00:17:32,520<br>
Это очень просто начать и<br>
остановить semantics [эти действия??].<br>
<br>
401<br>
00:17:32,520 --> 00:17:34,650<br>
Не важно как много<br>
у вас наблюдателей,<br>
<br>
402<br>
00:17:34,650 --> 00:17:39,740<br>
или в каком они состоянии, вы<br>
сливаете их в один жизненный цикл.<br>
<br>
403<br>
00:17:39,740 --> 00:17:42,000<br>
И этого нет ни в<br>
Activities, ни в Fragments<br>
<br>
404<br>
00:17:42,000 --> 00:17:44,620<br>
внутри их, но это работает<br>
с любыми из них.<br>
<br>
405<br>
00:17:44,620 --> 00:17:47,460<br>
И LiveData тестировалась,<br>
потому что<br>
<br>
406<br>
00:17:47,460 --> 00:17:49,080<br>
Android открытая платформа.<br>
<br>
407<br>
00:17:49,080 --> 00:17:52,720<br>
И если вы знакомы с печально<br>
известной FragmentTransaction<br>
<br>
408<br>
00:17:52,720 --> 00:17:56,670<br>
exception, мы гарантируем вам,<br>
что наблюдатель никогда не будет,<br>
<br>
409<br>
00:17:56,670 --> 00:17:59,750<br>
вызван в состоянии,<br>
когда вы не сможете запустить<br>
<br>
410<br>
00:17:59,750 --> 00:18:01,260<br>
вашу FragmentTransaction.<br>
<br>
411<br>
00:18:01,260 --> 00:18:03,780<br>
Итак, это очень и очень<br>
особенно разработанные средства<br>
<br>
412<br>
00:18:03,780 --> 00:18:08,100<br>
для работы с вашими<br>
Activities и Fragments.<br>
<br>
413<br>
00:18:08,100 --> 00:18:11,520<br>
OK, давайте поговорим<br>
о смене ориентации экрана.<br>
<br>
414<br>
00:18:11,520 --> 00:18:14,460<br>
Ну, этот пример был легким<br>
т.к. местоположение является глобальным,<br>
<br>
415<br>
00:18:14,460 --> 00:18:17,550<br>
Но в большинстве случаев,<br>
данные связаны с UI.<br>
<br>
416<br>
00:18:17,550 --> 00:18:22,770<br>
Итак, если у нас есть Activity,<br>
где показывается профиль пользователя,<br>
<br>
417<br>
00:18:22,770 --> 00:18:24,660<br>
и мы добавили веб-сервис<br>
который может вернуть<br>
<br>
418<br>
00:18:24,660 --> 00:18:28,260<br>
данные как LiveData,<br>
которые мы можем безопасно<br>
<br>
419<br>
00:18:28,260 --> 00:18:32,580<br>
наблюдать, не опасаясь<br>
утечки из Activity,<br>
<br>
420<br>
00:18:32,580 --> 00:18:33,470<br>
это выглядит прекрасно.<br>
<br>
421<br>
00:18:33,470 --> 00:18:35,030<br>
Мы никогда не упустим<br>
эту Activity,<br>
<br>
422<br>
00:18:35,030 --> 00:18:36,390<br>
это будет работать очень хорошо.<br>
<br>
423<br>
00:18:36,390 --> 00:18:40,340<br>
Исключая... Что случится если<br>
пользователь повернет устройство?<br>
<br>
424<br>
00:18:40,340 --> 00:18:42,850<br>
Давайте взглянем на линию<br>
жизненного цикла снова.<br>
<br>
425<br>
00:18:42,850 --> 00:18:44,790<br>
Итак, Activity создано,<br>
это запомнили, OK.<br>
<br>
426<br>
00:18:44,790 --> 00:18:46,752<br>
Получаем пользователя.<br>
<br>
427<br>
00:18:46,752 --> 00:18:48,460<br>
И пока мы получаем<br>
[проверяем accaunt] пользователя,<br>
<br>
428<br>
00:18:48,460 --> 00:18:51,390<br>
пользователь решает<br>
поверну-ка я телефон.<br>
<br>
429<br>
00:18:51,390 --> 00:18:53,130<br>
и тогда Activity<br>
разрушится.<br>
<br>
430<br>
00:18:53,130 --> 00:18:55,740<br>
К счастью, мы не получили<br>
утечку, это здорово.<br>
<br>
431<br>
00:18:55,740 --> 00:18:57,810<br>
Но когда наше новое<br>
Activity запустилось,<br>
<br>
432<br>
00:18:57,810 --> 00:18:59,620<br>
делаем новый вызов.<br>
<br>
433<br>
00:18:59,620 --> 00:19:02,160<br>
Ну, ничего страшного, но не айс.<br>
<br>
434<br>
00:19:02,160 --> 00:19:03,640<br>
Чего мы хотим?<br>
<br>
435<br>
00:19:03,640 --> 00:19:05,700<br>
Мы хотим реально удерживать<br>
эти данные, правильно?<br>
<br>
436<br>
00:19:05,700 --> 00:19:09,870<br>
Мы уже отправляли это запрос,<br>
зачем отправлять его опять?<br>
<br>
437<br>
00:19:09,870 --> 00:19:12,780<br>
Мы хотим, чтобы наш график<br>
выглядел так.<br>
<br>
438<br>
00:19:12,780 --> 00:19:14,640<br>
Итак, если новая Activity<br>
появляется, нам следует<br>
<br>
439<br>
00:19:14,640 --> 00:19:18,330<br>
быть способными вернуть ту же<br>
view model, которая и есть<br>
<br>
440<br>
00:19:18,330 --> 00:19:20,340<br>
новый класс называемый ViewModel.<br>
<br>
441<br>
00:19:20,340 --> 00:19:22,290<br>
Итак, мы представляем этот<br>
новый класс<br>
<br>
442<br>
00:19:22,290 --> 00:19:23,760<br>
очень спецефичный для<br>
этой вещи, где<br>
<br>
443<br>
00:19:23,760 --> 00:19:27,210<br>
вам следует поместить данные<br>
внутри вашей Activity<br>
<br>
444<br>
00:19:27,210 --> 00:19:30,940<br>
во ViewModel, и сделать вашу<br>
Activity свободной от данных.<br>
<br>
445<br>
00:19:30,940 --> 00:19:33,000<br>
Итак, если вы хотите<br>
изменить эту Activity,<br>
<br>
446<br>
00:19:33,000 --> 00:19:36,910<br>
вы создаете этот новый класс,<br>
наследуемый от VewModel class.<br>
<br>
447<br>
00:19:36,910 --> 00:19:41,830<br>
Независимо от того, какие данные<br>
были внутри Activity, мы помещаем их<br>
<br>
448<br>
00:19:41,830 --> 00:19:45,630<br>
во ViewModel-класс, и там, все,<br>
что мы делаем, делаем внутри getUser(),<br>
<br>
449<br>
00:19:45,630 --> 00:19:48,790<br>
если это первый запуск,<br>
получаем данные из веб-службы.<br>
<br>
450<br>
00:19:48,790 --> 00:19:51,800<br>
Иначе, возвращаем<br>
текущее значение.<br>
<br>
451<br>
00:19:51,800 --> 00:19:53,220<br>
Теперь, супер просто.<br>
<br>
452<br>
00:19:53,220 --> 00:19:55,800<br>
И внутри нашей Activity мы<br>
избавляемся от всего этого кода.<br>
<br>
453<br>
00:19:55,800 --> 00:19:58,590<br>
Мы говорим получить <br>
ViewModelProviders.of(this)<br>
<br>
454<br>
00:19:58,590 --> 00:20:01,620<br>
В каждой Activity или Fragment'е<br>
есть ViewModelProvider<br>
<br>
455<br>
00:20:01,620 --> 00:20:04,680<br>
который вы можете получить, и<br>
этот ViewModelProvider знает<br>
<br>
456<br>
00:20:04,680 --> 00:20:06,510<br>
как предоставить вам ViewModel.<br>
<br>
457<br>
00:20:06,510 --> 00:20:08,880<br>
Итак, когда вы вызываете<br>
get(MyViewModel),<br>
<br>
458<br>
00:20:08,880 --> 00:20:10,530<br>
в самый первый раз<br>
вы делаете этот вызов,<br>
<br>
459<br>
00:20:10,530 --> 00:20:11,940<br>
мы даем вам новое состояние.<br>
<br>
460<br>
00:20:11,940 --> 00:20:13,780<br>
Когда вращение Activity<br>
завершилось,<br>
<br>
461<br>
00:20:13,780 --> 00:20:16,760<br>
начинается переподключение<br>
к той же ViewModel.<br>
<br>
462<br>
00:20:16,760 --> 00:20:19,432<br>
А затем и остального<br>
этого кода также.<br>
<br>
463<br>
00:20:19,432 --> 00:20:22,318<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
464<br>
00:20:22,318 --> 00:20:28,580<br>
<br>
<br>
465<br>
00:20:28,580 --> 00:20:31,060<br>
Итак, если вы посмотрите на<br>
жизненный цикл, он выглядит так.<br>
<br>
466<br>
00:20:31,060 --> 00:20:32,040<br>
Это то, чего мы хотели.<br>
<br>
467<br>
00:20:32,040 --> 00:20:35,800<br>
Новая Activity запускается,<br>
заетем переподключается.<br>
<br>
468<br>
00:20:35,800 --> 00:20:38,140<br>
И когда новая<br>
Activity завершается,<br>
<br>
469<br>
00:20:38,140 --> 00:20:41,050<br>
Например, когда нам нечего<br>
делать с этой Activity,<br>
<br>
470<br>
00:20:41,050 --> 00:20:42,580<br>
и тогда мы идем<br>
и говорим ViewModel,<br>
<br>
471<br>
00:20:42,580 --> 00:20:44,350<br>
что он больше не нужен.<br>
<br>
472<br>
00:20:44,350 --> 00:20:48,340<br>
Это на самом деле единственный<br>
метод во ViewModel классе.<br>
<br>
473<br>
00:20:48,340 --> 00:20:49,570<br>
Так что это очень просто.<br>
<br>
474<br>
00:20:49,570 --> 00:20:51,640<br>
Поэтому, если мы посотрим на<br>
жизненные циклы, они<br>
<br>
475<br>
00:20:51,640 --> 00:20:53,310<br>
хранят данные для Activity.<br>
<br>
476<br>
00:20:53,310 --> 00:20:56,500<br>
Они выживают при<br>
изменениях конфигурации.<br>
<br>
477<br>
00:20:56,500 --> 00:20:58,930<br>
Они никогда не должны,<br>
каждый раз ссылаться на Views<br>
<br>
478<br>
00:20:58,930 --> 00:21:00,870<br>
потому что они [НЕРАЗБОРЧИВО]<br>
покидают эти Activities.<br>
<br>
479<br>
00:21:00,870 --> 00:21:03,430<br>
Итак, вы не можете ссылаться<br>
обратно на Activity.<br>
<br>
480<br>
00:21:03,430 --> 00:21:05,640<br>
Вот почему вы используете<br>
такие вещи, как LiveData,<br>
<br>
481<br>
00:21:05,640 --> 00:21:08,550<br>
Rx Java, или наблюдатели<br>
с хранением данных<br>
<br>
482<br>
00:21:08,550 --> 00:21:10,270<br>
чтобы совершать эту коммуникацию.<br>
<br>
483<br>
00:21:10,270 --> 00:21:12,730<br>
И это то, почему все наши<br>
разговоры про Activity - это всегда<br>
<br>
484<br>
00:21:12,730 --> 00:21:15,070<br>
разговоры о ViewModel.<br>
<br>
485<br>
00:21:15,070 --> 00:21:19,210<br>
Теперь еще одна большая<br>
тема о живучести [надежное сохранение].<br>
<br>
486<br>
00:21:19,210 --> 00:21:22,000<br>
Теперь мы знаем, написать хорошее,<br>
отзывчивое приложение на Android<br>
<br>
487<br>
00:21:22,000 --> 00:21:24,860<br>
означает то, что необходимо<br>
сохранять данные на диск.<br>
<br>
488<br>
00:21:24,860 --> 00:21:27,700<br>
Если мы взглянем на Android, там<br>
есть 3-4 основных API для этого.<br>
<br>
489<br>
00:21:27,700 --> 00:21:29,980<br>
Один из которых это<br>
ContentProvider, который<br>
<br>
490<br>
00:21:29,980 --> 00:21:32,320<br>
переносит данные между процессами.<br>
<br>
491<br>
00:21:32,320 --> 00:21:35,530<br>
В реальности это не имеет<br>
общего с живучестью данных.<br>
<br>
492<br>
00:21:35,530 --> 00:21:37,510<br>
Другой способ это<br>
SharedPreferences,<br>
<br>
493<br>
00:21:37,510 --> 00:21:40,090<br>
который сохраняет данные в XML.<br>
<br>
494<br>
00:21:40,090 --> 00:21:43,190<br>
Вы можете сохранить только<br>
немного данных с его помощью.<br>
<br>
495<br>
00:21:43,190 --> 00:21:44,800<br>
Последний способ это<br>
SQLite, которая<br>
<br>
496<br>
00:21:44,800 --> 00:21:48,160<br>
была введена с версии<br>
Android 1.<br>
<br>
497<br>
00:21:48,160 --> 00:21:49,720<br>
Итак, вы знаете, вам<br>
нужно использовать SQLite<br>
<br>
498<br>
00:21:49,720 --> 00:21:51,890<br>
если вы хотите хранить много данных.<br>
<br>
499<br>
00:21:51,890 --> 00:21:55,330<br>
Вы идете на<br>
developer.android.com/ это<br>
<br>
500<br>
00:21:55,330 --> 00:21:57,960<br>
самое первое сохранение<br>
ваших данных.<br>
<br>
501<br>
00:21:57,960 --> 00:22:00,130<br>
Это очень запутывает.<br>
<br>
502<br>
00:22:00,130 --> 00:22:01,642<br>
Это очень грустно.<br>
<br>
503<br>
00:22:01,642 --> 00:22:03,370<br>
[СМЕХ]<br>
<br>
504<br>
00:22:03,370 --> 00:22:06,190<br>
Итак - OK, мы хотим<br>
сделать это менее грустным.<br>
<br>
505<br>
00:22:06,190 --> 00:22:07,960<br>
Мы хотим сделать это приятным.<br>
<br>
506<br>
00:22:07,960 --> 00:22:10,060<br>
Итак, посмотрим на<br>
пример, правильно?<br>
<br>
507<br>
00:22:10,060 --> 00:22:11,740<br>
Так что - сверху,<br>
он пытается сказать,<br>
<br>
508<br>
00:22:11,740 --> 00:22:15,670<br>
"Я хочу выбрать эти три<br>
столбца с таким-то условием,<br>
<br>
509<br>
00:22:15,670 --> 00:22:17,950<br>
и я хочу отсортировать<br>
результат так-то."<br>
<br>
510<br>
00:22:17,950 --> 00:22:20,670<br>
Это на самом деле,<br>
довольно простой SQL-запрос,<br>
<br>
511<br>
00:22:20,670 --> 00:22:22,210<br>
но вам нужно написать<br>
весь этот код.<br>
<br>
512<br>
00:22:22,210 --> 00:22:24,160<br>
Плюс, этот код<br>
даже не показывает где<br>
<br>
513<br>
00:22:24,160 --> 00:22:27,720<br>
вы определяете все эти константы.<br>
<br>
514<br>
00:22:27,720 --> 00:22:29,430<br>
Чего же мы хотим на самом деле?<br>
<br>
515<br>
00:22:29,430 --> 00:22:32,060<br>
мы хотим избавиться от этого<br>
кода без шаблонов.<br>
<br>
516<br>
00:22:32,060 --> 00:22:34,890<br>
Когда вы пиштте на Java,<br>
если вы делаете опечатку в Java,<br>
<br>
517<br>
00:22:34,890 --> 00:22:36,630<br>
он не компилирует код.<br>
<br>
518<br>
00:22:36,630 --> 00:22:39,010<br>
Мы хотим похожую вещь для SQL.<br>
<br>
519<br>
00:22:39,010 --> 00:22:42,000<br>
Мы все еще хотим использовать SQLite,<br>
потому что на каждом девайсе Android<br>
<br>
520<br>
00:22:42,000 --> 00:22:43,740<br>
есть эта проверенная технология.<br>
<br>
521<br>
00:22:43,740 --> 00:22:46,230<br>
Мы знаем, это отлично работает.<br>
<br>
522<br>
00:22:46,230 --> 00:22:48,280<br>
Но мы хотим проверять<br>
компиляцию на лету.<br>
<br>
523<br>
00:22:48,280 --> 00:22:49,970<br>
Поэтому мы не хотим<br>
код по шаблонам,<br>
<br>
524<br>
00:22:49,970 --> 00:22:52,480<br>
мы хотим проверять компиляцию<br>
на лету, в реальном времени.<br>
<br>
525<br>
00:22:52,480 --> 00:22:56,220<br>
Мы сказали "ОК - мы пришли с<br>
Room, которая является объектом<br>
<br>
526<br>
00:22:56,220 --> 00:22:59,649<br>
mapping library для SQLite".<br>
<br>
527<br>
00:22:59,649 --> 00:23:05,800<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
528<br>
00:23:05,800 --> 00:23:08,210<br>
Если мы посмотрим на<br>
этот запрос, мы скажем,<br>
<br>
529<br>
00:23:08,210 --> 00:23:10,770<br>
"OK, давайте поместим этот<br>
запрос под аннотацию.<br>
<br>
530<br>
00:23:10,770 --> 00:23:12,610<br>
Мы любим аннотации".<br>
<br>
531<br>
00:23:12,610 --> 00:23:14,560<br>
И у нас есть объект<br>
для сохранения, который<br>
<br>
532<br>
00:23:14,560 --> 00:23:16,360<br>
мы хотим сохранить в базе данных.<br>
<br>
533<br>
00:23:16,360 --> 00:23:19,270<br>
Я хочу поместить этот запрос<br>
внутри интерфейса.<br>
<br>
534<br>
00:23:19,270 --> 00:23:21,280<br>
Вы хотите создать FeedDao -<br>
<br>
535<br>
00:23:21,280 --> 00:23:24,040<br>
Dao означает<br>
Data Access Object.<br>
<br>
536<br>
00:23:24,040 --> 00:23:27,430<br>
Обычно для баз данных, лучший<br>
способ разместить там данные<br>
<br>
537<br>
00:23:27,430 --> 00:23:29,350<br>
это сделать это через абстракцию.<br>
<br>
538<br>
00:23:29,350 --> 00:23:32,252<br>
Then we just need to tell<br>
the Room, this is a Dow.<br>
<br>
539<br>
00:23:32,252 --> 00:23:34,360<br>
Tell Room this is an entity.<br>
<br>
540<br>
00:23:34,360 --> 00:23:37,960<br>
And finally, we had a<br>
database class which says,<br>
<br>
541<br>
00:23:37,960 --> 00:23:41,050<br>
I have these entities-- so<br>
you have multiple entities,<br>
<br>
542<br>
00:23:41,050 --> 00:23:45,240<br>
and I have these data access<br>
objects, as you saw them.<br>
<br>
543<br>
00:23:45,240 --> 00:23:46,210<br>
This is all you write.<br>
<br>
544<br>
00:23:46,210 --> 00:23:48,760<br>
Once you write that, you can<br>
get an implementation of it<br>
<br>
545<br>
00:23:48,760 --> 00:23:49,590<br>
from Room.<br>
<br>
546<br>
00:23:49,590 --> 00:23:52,750<br>
It's very similar to how<br>
you use Retrofit or Dagger--<br>
<br>
547<br>
00:23:52,750 --> 00:23:57,080<br>
you define the interfaces, we<br>
provide the implementation.<br>
<br>
548<br>
00:23:57,080 --> 00:23:59,740<br>
Now, once we know<br>
this is a Dow, we<br>
<br>
549<br>
00:23:59,740 --> 00:24:01,210<br>
can do these shortcut methods.<br>
<br>
550<br>
00:24:01,210 --> 00:24:05,350<br>
Like, insert these items, or<br>
delete these items, or update--<br>
<br>
551<br>
00:24:05,350 --> 00:24:06,930<br>
a bunch of shortcut methods.<br>
<br>
552<br>
00:24:06,930 --> 00:24:08,710<br>
And you can press<br>
multiple parameters.<br>
<br>


</td></tr> 
  </table>
  
