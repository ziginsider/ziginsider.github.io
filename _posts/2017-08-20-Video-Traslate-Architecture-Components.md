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
Когда вы пишете на Java,<br>
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
mapping library для SQLite". [т.е. ORM]<br>
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
Feed, который<br>
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
Тогда, нам всего лишь нужно<br>
сказать Room "это DAO".<br>
<br>
539<br>
00:23:32,252 --> 00:23:34,360<br>
Сказать Room: "это сущность".<br>
<br>
540<br>
00:23:34,360 --> 00:23:37,960<br>
И наконец, у нас был класс<br>
базы данных, который говорил:<br>
<br>
541<br>
00:23:37,960 --> 00:23:41,050<br>
"Что у меня есть сущности -<br>
поэтому есть несколько сущностей,<br>
<br>
542<br>
00:23:41,050 --> 00:23:45,240<br>
и у меня есть данные для доступа<br>
к объектам, которые вы видели.<br>
<br>
543<br>
00:23:45,240 --> 00:23:46,210<br>
Это все, что вы пишите.<br>
<br>
544<br>
00:23:46,210 --> 00:23:48,760<br>
Как только вы напишите это, вы<br>
можете получить реализацию этого<br>
<br>
545<br>
00:23:48,760 --> 00:23:49,590<br>
с помощью Room.<br>
<br>
546<br>
00:23:49,590 --> 00:23:52,750<br>
Это очень похоже на то, когда<br>
вы используете Retrofit или Dagger -<br>
<br>
547<br>
00:23:52,750 --> 00:23:57,080<br>
вы определяете интерфейсы,<br>
мы обеспечиваем реализацию.<br>
<br>
548<br>
00:23:57,080 --> 00:23:59,740<br>
Теперь, как только мы узнали,<br>
что это DAO, мы можем<br>
<br>
549<br>
00:23:59,740 --> 00:24:01,210<br>
использовать методы быстрого доступа.<br>
<br>
550<br>
00:24:01,210 --> 00:24:05,350<br>
Такие как, insert() это, или<br>
deleteAll() это, or updateAll() -<br>
<br>
551<br>
00:24:05,350 --> 00:24:06,930<br>
Куча методов бытрого доступа.<br>
<br>
552<br>
00:24:06,930 --> 00:24:08,710<br>
Вы можете задавать<br>
множесто параметров.<br>
<br>
553<br>
00:24:08,710 --> 00:24:11,115<br>
Так много, пока сможете читать.<br>
И это имеет смысл,<br>
<br>
554<br>
00:24:11,115 --> 00:24:13,930<br>
Room поймет их.<br>
<br>
555<br>
00:24:13,930 --> 00:24:16,000<br>
Но наиболее важная<br>
часть Room - это то,<br>
<br>
556<br>
00:24:16,000 --> 00:24:18,680<br>
что он понимает ваш SQL.<br>
<br>
557<br>
00:24:18,680 --> 00:24:20,320<br>
Итак часть - все те<br>
константы, о которых<br>
<br>
558<br>
00:24:20,320 --> 00:24:23,630<br>
я упомянул, мы определили, чтобы<br>
избежать ошибок во время компиляции,<br>
<br>
559<br>
00:24:23,630 --> 00:24:26,560<br>
Room реально дает это<br>
все бесплатно.<br>
<br>
560<br>
00:24:26,560 --> 00:24:28,380<br>
Поэтому, когда Room видит<br>
этот запрос, то говорит:<br>
<br>
561<br>
00:24:28,380 --> 00:24:31,060<br>
"ОК, вы получаете эти<br>
три столбца<br>
<br>
562<br>
00:24:31,060 --> 00:24:34,900<br>
из этой таблицы, где название<br>
похоже на это ключевое слово.<br>
<br>
563<br>
00:24:34,900 --> 00:24:36,705<br>
Откуда это<br>
ключевое слово?<br>
<br>
564<br>
00:24:36,705 --> 00:24:38,710<br>
О, да оно приходит<br>
из параметров функции.<br>
<br>
565<br>
00:24:38,710 --> 00:24:39,567<br>
Имеет смысл.<br>
<br>
566<br>
00:24:39,567 --> 00:24:40,900<br>
И что она хочет вернуть?<br>
<br>
567<br>
00:24:40,900 --> 00:24:42,970<br>
Она хочет вернуть<br>
список объектов Feed."<br>
<br>
568<br>
00:24:42,970 --> 00:24:45,330<br>
И тогда Room идет и проверяет.<br>
<br>
569<br>
00:24:45,330 --> 00:24:47,980<br>
"Подходят ли эти столбцы<br>
к объекту, который<br>
<br>
570<br>
00:24:47,980 --> 00:24:49,690<br>
пользователь хочет вернуть?"<br>
<br>
571<br>
00:24:49,690 --> 00:24:53,812<br>
И, как только они равны, говорится:<br>
"OK, я могу сгенерировать этот код."<br>
<br>
572<br>
00:24:53,812 --> 00:24:55,270<br>
Вы можете даже, скажем,<br>
выбрать звездочку [все столбцы].<br>
<br>
573<br>
00:24:55,270 --> 00:24:56,600<br>
Вам не нужно их перечислять.<br>
<br>
574<br>
00:24:56,600 --> 00:25:00,190<br>
Room реально, реально<br>
понимает ваш запрос.<br>
<br>
575<br>
00:25:00,190 --> 00:25:03,130<br>
Вы можете даже соединить 10<br>
таблиц, и это все еще будет работать.<br>
<br>
576<br>
00:25:03,130 --> 00:25:05,020<br>
Но что, если вы сделали опечатку?<br>
<br>
577<br>
00:25:05,020 --> 00:25:07,750<br>
Вместо того, чтобы написать<br>
"feed" вы пишите "feeds".<br>
<br>
578<br>
00:25:07,750 --> 00:25:10,750<br>
Теперь, если это случится,<br>
Room собирается дать вам<br>
<br>
579<br>
00:25:10,750 --> 00:25:12,940<br>
ошибку времени компиляции.<br>
<br>
580<br>
00:25:12,940 --> 00:25:15,040<br>
Так что выходит, что<br>
ваш запрос проверяется<br>
<br>
581<br>
00:25:15,040 --> 00:25:17,080<br>
по схеме, которую<br>
вы определили.<br>
<br>
582<br>
00:25:17,080 --> 00:25:19,562<br>
И вам сообщается, если<br>
вы где-то ошиблись.<br>
<br>
583<br>
00:25:19,562 --> 00:25:22,508<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
584<br>
00:25:22,508 --> 00:25:27,797<br>
<br>
<br>
585<br>
00:25:27,797 --> 00:25:29,380<br>
Но это не единственное,<br>
что Room делает.<br>
<br>
586<br>
00:25:29,380 --> 00:25:30,860<br>
Итак, если вы скажите -<br>
<br>
587<br>
00:25:30,860 --> 00:25:34,070<br>
если ваш запрос верен, вы<br>
хотите получить ID и title.<br>
<br>
588<br>
00:25:34,070 --> 00:25:35,870<br>
Говорится: "Хорошо,<br>
это запрос, но вы<br>
<br>
589<br>
00:25:35,870 --> 00:25:37,350<br>
хотите вернуть это как строку."<br>
<br>
590<br>
00:25:37,350 --> 00:25:40,460<br>
И тогда Room отвечает: "ОК, ты<br>
возвращаешь две колонки,<br>
<br>
591<br>
00:25:40,460 --> 00:25:42,260<br>
но у тебя есть только одна строка.<br>
<br>
592<br>
00:25:42,260 --> 00:25:43,320<br>
Это не имеет смысла."<br>
<br>
593<br>
00:25:43,320 --> 00:25:46,800<br>
И это обратно выдаст вам<br>
ошибку во время компиляции.<br>
<br>
594<br>
00:25:46,800 --> 00:25:49,220<br>
И это действительно хороший<br>
способ исправить это в Room.<br>
<br>
595<br>
00:25:49,220 --> 00:25:51,095<br>
Вы можете в принципе<br>
создать любой Java класс.<br>
<br>
596<br>
00:25:51,095 --> 00:25:52,580<br>
Это не нужно<br>
аннотировать,<br>
<br>
597<br>
00:25:52,580 --> 00:25:55,170<br>
Не надо говорить ничего<br>
специально об этом Pojo,<br>
<br>
598<br>
00:25:55,170 --> 00:25:57,080<br>
просто сказать Room вернуть его.<br>
<br>
599<br>
00:25:57,080 --> 00:25:59,780<br>
Пока какой-либо запрос<br>
возвращает то, что<br>
<br>
600<br>
00:25:59,780 --> 00:26:01,880<br>
соответствует тому,<br>
что вы хотите вернуть,<br>
<br>
601<br>
00:26:01,880 --> 00:26:05,250<br>
Room напишет этот код<br>
вместо вас.<br>
<br>
602<br>
00:26:05,250 --> 00:26:07,470<br>
И теперь наблюдатели, которые<br>
очень важны, не так ли?<br>
<br>
603<br>
00:26:07,470 --> 00:26:09,390<br>
Если у вас есть запрос,<br>
подобный этому, то вы<br>
<br>
604<br>
00:26:09,390 --> 00:26:11,460<br>
показывая список Feed'ов,<br>
вы очевидно<br>
<br>
605<br>
00:26:11,460 --> 00:26:14,295<br>
захотите получить уведомление,<br>
когда данные изменятся.<br>
<br>
606<br>
00:26:14,295 --> 00:26:17,842<br>
И в Room, если вы хотите<br>
сделать это, вы можете<br>
<br>
607<br>
00:26:17,842 --> 00:26:19,290<br>
сказать и сделать. Скажите,<br>
<br>
608<br>
00:26:19,290 --> 00:26:22,980<br>
чтобы она вернул LiveData,<br>
и она сделает это для вас.<br>
<br>
609<br>
00:26:22,980 --> 00:26:26,400<br>
Потому что она знает ваш запрос,<br>
знает, что на него влияет.<br>
<br>
610<br>
00:26:26,400 --> 00:26:29,520<br>
Таким образом это поможет вам<br>
узнать, если запрос изменится.<br>
<br>
611<br>
00:26:29,520 --> 00:26:32,280<br>
И это та часть, где все эти<br>
архитектурные компоненты<br>
<br>
612<br>
00:26:32,280 --> 00:26:33,750<br>
прекрасно работают вместе.<br>
<br>
613<br>
00:26:33,750 --> 00:26:36,640<br>
Room уже знает<br>
о LiveData.<br>
<br>
614<br>
00:26:36,640 --> 00:26:40,340<br>
Итак ваша ViewModel, все, что вы<br>
можете написать - из данных,<br>
<br>
615<br>
00:26:40,340 --> 00:26:42,600<br>
вызовите этот запрос, и<br>
это все он сделает.<br>
<br>
616<br>
00:26:42,600 --> 00:26:46,650<br>
Всякий раз, когда данные меняются,<br>
ваш UI обновляется также.<br>
<br>
617<br>
00:26:46,650 --> 00:26:49,470<br>
И это только тогда происходит<br>
когда ваш UI виден [visible]<br>
<br>
618<br>
00:26:49,470 --> 00:26:52,958<br>
И последнее, но не менее важное,<br>
Room также поддерживает RxJava 2.<br>
<br>
619<br>
00:26:52,958 --> 00:26:55,448<br>
[ОВАЦИИ]<br>
<br>
620<br>
00:26:55,448 --> 00:27:01,930<br>
<br>
<br>
621<br>
00:27:01,930 --> 00:27:04,390<br>
OK, если сказать о<br>
Room в двух словах,<br>
<br>
622<br>
00:27:04,390 --> 00:27:06,730<br>
Она пишет шаблонный<br>
код для вас [вместо вас].<br>
<br>
623<br>
00:27:06,730 --> 00:27:08,050<br>
И она полностью поддерживает SQLite.<br>
<br>
624<br>
00:27:08,050 --> 00:27:10,990<br>
Вы можете все просто писать на<br>
SQLite, будет работать и так.<br>
<br>
625<br>
00:27:10,990 --> 00:27:14,070<br>
Она проверяет ваши запросы<br>
во время компиляции.<br>
<br>
626<br>
00:27:14,070 --> 00:27:17,350<br>
Это стимулирует лучшие практики,<br>
которые помогают вам<br>
<br>
627<br>
00:27:17,350 --> 00:27:19,480<br>
с тестами, миграцией и.<br>
<br>
628<br>
00:27:19,480 --> 00:27:23,020<br>
также наблюдателями, и все<br>
это прямо из коробки.<br>
<br>
629<br>
00:27:23,020 --> 00:27:28,000<br>
OK, архитектура,<br>
наша последняя тема на сегодня.<br>
<br>
630<br>
00:27:28,000 --> 00:27:30,000<br>
Итак, с чего мы начали, верно?<br>
<br>
631<br>
00:27:30,000 --> 00:27:31,860<br>
И теперь вы, возможно,<br>
спросите себя:<br>
<br>
632<br>
00:27:31,860 --> 00:27:34,335<br>
"Что изменилось в<br>
2017 году, что вы вдруг<br>
<br>
633<br>
00:27:34,335 --> 00:27:36,930<br>
заговорили про архитектуру?"<br>
<br>
634<br>
00:27:36,930 --> 00:27:38,740<br>
Хорошо, реально<br>
ничего не изменилось.<br>
<br>
635<br>
00:27:38,740 --> 00:27:40,560<br>
Мы говорим об этой теме<br>
много.<br>
<br>
636<br>
00:27:40,560 --> 00:27:44,460<br>
Adam Powell и я вели много<br>
разговоров на эту тему.<br>
<br>
637<br>
00:27:44,460 --> 00:27:49,050<br>
Этот разговор начался с 2010,<br>
который я наблюдаю как разработчик.<br>
<br>
638<br>
00:27:49,050 --> 00:27:51,630<br>
И это та тема, которую мы<br>
вполне четко обсуждали.<br>
<br>
639<br>
00:27:51,630 --> 00:27:54,720<br>
Но чего не хватало, так это <br>
четко определенной ссылки<br>
<br>
640<br>
00:27:54,720 --> 00:27:56,022<br>
на архитектуру.<br>
<br>
641<br>
00:27:56,022 --> 00:27:57,480<br>
И это то, что мы<br>
запускаем в эти дни.<br>
<br>
642<br>
00:27:57,480 --> 00:27:59,370<br>
Если вы пройдете сегодня на<br>
developer.android.com,<br>
<br>
643<br>
00:27:59,370 --> 00:28:01,680<br>
после нашей сессии,<br>
есть секция<br>
<br>
644<br>
00:28:01,680 --> 00:28:05,246<br>
о том, как быть архитектором<br>
в Android приложении.<br>
<br>
645<br>
00:28:05,246 --> 00:28:08,697<br>
[АПЛОДИСМЕНТЫ]<br>
<br>
646<br>
00:28:08,697 --> 00:28:13,640<br>
<br>
<br>
647<br>
00:28:13,640 --> 00:28:15,890<br>
И, таким образом, это<br>
гид по архитектуре.<br>
<br>
648<br>
00:28:15,890 --> 00:28:17,780<br>
Это не книга догматических правил.<br>
<br>
649<br>
00:28:17,780 --> 00:28:20,600<br>
Мы верим, что это очень хороший<br>
путь, чтобы писать приложения,<br>
<br>
650<br>
00:28:20,600 --> 00:28:24,320<br>
но вы не обязаны, следовать<br>
за нами строчка за строчкой.<br>
<br>
651<br>
00:28:24,320 --> 00:28:27,400<br>
Поэтому я кратко остановлюсь<br>
на архитектуре,<br>
<br>
652<br>
00:28:27,400 --> 00:28:28,960<br>
но если вы потеряетесь немного,<br>
не волнуйтесь.<br>
<br>
653<br>
00:28:28,960 --> 00:28:31,950<br>
У нас есть вся документации на<br>
developer.аndroid.com<br>
<br>
654<br>
00:28:31,950 --> 00:28:34,264<br>
с простыми примерами.<br>
<br>
655<br>
00:28:34,264 --> 00:28:35,680<br>
Итак, мы считаем, что<br>
приложение состоит<br>
<br>
656<br>
00:28:35,680 --> 00:28:37,300<br>
из четырех главных частей -<br>
<br>
657<br>
00:28:37,300 --> 00:28:41,680<br>
это UI-контроллеры, <br>
ViewModels, хранилище данных,<br>
<br>
658<br>
00:28:41,680 --> 00:28:43,030<br>
и источники данных.<br>
<br>
659<br>
00:28:43,030 --> 00:28:45,640<br>
Давайте разберем это<br>
в деталях.<br>
<br>
660<br>
00:28:45,640 --> 00:28:47,980<br>
UI-контроллеры это<br>
ваши Activities,<br>
<br>
661<br>
00:28:47,980 --> 00:28:51,100<br>
Fragments, custom Views.<br>
<br>
662<br>
00:28:51,100 --> 00:28:52,750<br>
У них действительно простые задачи.<br>
<br>
663<br>
00:28:52,750 --> 00:28:55,270<br>
Они наблюдают за полями<br>
у ViewModel<br>
<br>
664<br>
00:28:55,270 --> 00:28:56,720<br>
и обновляют себя.<br>
<br>
665<br>
00:28:56,720 --> 00:28:58,540<br>
И они хотят больше<br>
ответственности.<br>
<br>
666<br>
00:28:58,540 --> 00:29:01,540<br>
Всякий раз, когда пользователь<br>
совершает действие в UI,<br>
<br>
667<br>
00:29:01,540 --> 00:29:04,450<br>
они понимают это действие,<br>
и сообщают о нем во ViewModel<br>
<br>
668<br>
00:29:04,450 --> 00:29:07,540<br>
так, что становится понятно,<br>
что пользователь хотел сделать.<br>
<br>
669<br>
00:29:07,540 --> 00:29:10,390<br>
Если мы посмотрим на ViewModel,<br>
то это та сущность, которая<br>
<br>
670<br>
00:29:10,390 --> 00:29:13,450<br>
готовит данные<br>
для UI,<br>
<br>
671<br>
00:29:13,450 --> 00:29:14,480<br>
и держит их.<br>
<br>
672<br>
00:29:14,480 --> 00:29:16,740<br>
Это то, где данные<br>
для UI-интерфейса.<br>
<br>
673<br>
00:29:16,740 --> 00:29:20,050<br>
ViewModel знает как<br>
получить эти данные.<br>
<br>
674<br>
00:29:20,050 --> 00:29:21,949<br>
Обычно есть LiveData.<br>
<br>
675<br>
00:29:21,949 --> 00:29:23,740<br>
Если вы используете RxJava,<br>
это наблюдение за данными,<br>
<br>
676<br>
00:29:23,740 --> 00:29:26,940<br>
или сбор информации от наблюдений.<br>
<br>
677<br>
00:29:26,940 --> 00:29:28,830<br>
Это помогает "пережить"<br>
изменения конфигурации.<br>
<br>
678<br>
00:29:28,830 --> 00:29:32,200<br>
И это то, почему мы помещаем<br>
данные во ViewModels.<br>
<br>
679<br>
00:29:32,200 --> 00:29:33,680<br>
И это также шлюз.<br>
<br>
680<br>
00:29:33,680 --> 00:29:37,040<br>
И это тоже понятно т.к.<br>
ваш UI-контроллер, когда<br>
<br>
681<br>
00:29:37,040 --> 00:29:39,230<br>
говорит с ViewModel,<br>
связывается с остальными<br>
<br>
682<br>
00:29:39,230 --> 00:29:42,690<br>
частями приложения.<br>
<br>
683<br>
00:29:42,690 --> 00:29:44,360<br>
И что же тгда репозиторий?<br>
<br>
684<br>
00:29:44,360 --> 00:29:47,100<br>
ViewModel выполняет функцию<br>
хранилища данных<br>
<br>
685<br>
00:29:47,100 --> 00:29:48,920<br>
для UI-контроллера, правильно?<br>
<br>
686<br>
00:29:48,920 --> 00:29:51,060<br>
Репозиторий хранит их,<br>
в предсталении хранилища данных<br>
<br>
687<br>
00:29:51,060 --> 00:29:53,520<br>
для всего вашего приложения.<br>
<br>
688<br>
00:29:53,520 --> 00:29:56,070<br>
Таким образом, это полная<br>
модель данных для приложения,<br>
<br>
689<br>
00:29:56,070 --> 00:29:58,560<br>
и он обеспечивает обмен [предоставление]<br>
данными через простые API<br>
<br>
690<br>
00:29:58,560 --> 00:30:00,210<br>
для остальной части приложения.<br>
<br>
691<br>
00:30:00,210 --> 00:30:03,420<br>
У вас может быть пользовательский<br>
репозиторий, где вы даете user-ID,<br>
<br>
692<br>
00:30:03,420 --> 00:30:06,000<br>
И получаете<br>
LiveData о пользователе<br>
<br>
693<br>
00:30:06,000 --> 00:30:07,650<br>
Откуда у него данные?<br>
<br>
694<br>
00:30:07,650 --> 00:30:10,260<br>
Вы не должны заботиться,<br>
это работа репозитория.<br>
<br>
695<br>
00:30:10,260 --> 00:30:11,280<br>
Но как он это делает?<br>
<br>
696<br>
00:30:11,280 --> 00:30:12,420<br>
Он беседует с - <br>
<br>
697<br>
00:30:12,420 --> 00:30:15,920<br>
выборкой, синхронизацией,<br>
глядя на базу данных,<br>
<br>
698<br>
00:30:15,920 --> 00:30:17,990<br>
или общаясь через ваш<br>
Retrofit.<br>
<br>
699<br>
00:30:17,990 --> 00:30:20,770<br>
Это работа репозитория.<br>
<br>
700<br>
00:30:20,770 --> 00:30:23,100<br>
И последнее но не менее важное,<br>
у нас есть источники данных,<br>
<br>
701<br>
00:30:23,100 --> 00:30:25,020<br>
наподобие ваших REST API клиентов.<br>
<br>
702<br>
00:30:25,020 --> 00:30:28,470<br>
Вы можете использовать Retrofit,<br>
или у вас есть SQLite база.<br>
<br>
703<br>
00:30:28,470 --> 00:30:30,500<br>
Вы можете использовать Room,<br>
или вы можете использовать<br>
<br>
704<br>
00:30:30,500 --> 00:30:32,460<br>
GRAM, это не слишком важно.<br>
<br>
705<br>
00:30:32,460 --> 00:30:34,920<br>
И вы можете говорить<br>
другим провайдерам контента<br>
<br>
706<br>
00:30:34,920 --> 00:30:36,390<br>
из других процессов.<br>
<br>
707<br>
00:30:36,390 --> 00:30:39,090<br>
Эти вещи мы называем<br>
источниками данных.<br>
<br>
708<br>
00:30:39,090 --> 00:30:41,940<br>
И мы думаем, что<br>
все эти слои<br>
<br>
709<br>
00:30:41,940 --> 00:30:43,830<br>
могут обнаруживать друг<br>
друга чтобы создавать<br>
<br>
710<br>
00:30:43,830 --> 00:30:45,630<br>
проверки зависимостей<br>
в системе, которые мы будем<br>
<br>
711<br>
00:30:45,630 --> 00:30:47,370<br>
использовать с помощью Dagger.<br>
<br>
712<br>
00:30:47,370 --> 00:30:49,800<br>
Но мы также озознаем, что<br>
понимание ситуации зависимости<br>
<br>
713<br>
00:30:49,800 --> 00:30:51,810<br>
не очень легко.<br>
<br>
714<br>
00:30:51,810 --> 00:30:55,560<br>
Это более сложная тема, и<br>
иногда может быть излишней.<br>
<br>
715<br>
00:30:55,560 --> 00:30:57,750<br>
И вы могли бы использовать<br>
Service Locator, если<br>
<br>
716<br>
00:30:57,750 --> 00:31:01,560<br>
вы чувствуете себя более<br>
комфортно с ним.<br>
<br>
717<br>
00:31:01,560 --> 00:31:04,050<br>
Итак, давайте вернемся к конкретному -<br>
<br>
718<br>
00:31:04,050 --> 00:31:06,700<br>
пройдем через конкретный пример.<br>
<br>
719<br>
00:31:06,700 --> 00:31:10,110<br>
Допустим, у нас есть UI, который<br>
показывает профиль пользователя,<br>
<br>
720<br>
00:31:10,110 --> 00:31:12,380<br>
и у нас есть источник<br>
данных который - мы сохраняем<br>
<br>
721<br>
00:31:12,380 --> 00:31:16,080<br>
данные в базе данных, также<br>
можем получить их через сеть.<br>
<br>
722<br>
00:31:16,080 --> 00:31:18,210<br>
Как мы получаем<br>
эти две вещи?<br>
<br>
723<br>
00:31:18,210 --> 00:31:21,240<br>
Хорошо, мы говорим, что сначала<br>
нужен репозиторий пользователя.<br>
<br>
724<br>
00:31:21,240 --> 00:31:23,880<br>
Пользовательский репозиторий знает,<br>
что он должен проверять базу данных.<br>
<br>
725<br>
00:31:23,880 --> 00:31:25,680<br>
Если там нет,<br>
то сделать веб-запрос.<br>
<br>
726<br>
00:31:25,680 --> 00:31:28,500<br>
Или между тем, также попытаться<br>
запустить базу данных.<br>
<br>
727<br>
00:31:28,500 --> 00:31:30,750<br>
Не имеет значения,<br>
как делать это,<br>
<br>
728<br>
00:31:30,750 --> 00:31:32,820<br>
но он [репозиторий] знает,<br>
как создать LiveData<br>
<br>
729<br>
00:31:32,820 --> 00:31:36,780<br>
пользователя или наблюдателя,<br>
все равно кого.<br>
<br>
730<br>
00:31:36,780 --> 00:31:38,430<br>
И тогда нам нужна<br>
ViewModel, правильно,<br>
<br>
731<br>
00:31:38,430 --> 00:31:41,670<br>
потому что данные для<br>
UI живут в ViewModel.<br>
<br>
732<br>
00:31:41,670 --> 00:31:44,220<br>
Итак мы создаем<br>
ProfileViewModel,<br>
<br>
733<br>
00:31:44,220 --> 00:31:48,030<br>
который "говорит" с репозиторием,<br>
чтобы получить эту информацию.<br>
<br>
734<br>
00:31:48,030 --> 00:31:50,850<br>
А затем реальный фрагиент<br>
получает данные<br>
<br>
735<br>
00:31:50,850 --> 00:31:54,450<br>
из ViewModel, так что,<br>
если фрагмент возвращается,<br>
<br>
736<br>
00:31:54,450 --> 00:31:57,270<br>
то LiveData будет в<br>
ProfileViewModel.<br>
<br>
737<br>
00:31:57,270 --> 00:32:00,070<br>
Но если фрагмент<br>
исчезает полностью,<br>
<br>
738<br>
00:32:00,070 --> 00:32:01,680<br>
мы избавляемя<br>
от ViewModel,<br>
<br>
739<br>
00:32:01,680 --> 00:32:05,240<br>
и данных, которые могут быть<br>
собраны сборщиком мусора.<br>
<br>
740<br>
00:32:05,240 --> 00:32:07,100<br>
Теперь, вся эта абстракция,<br>
которую мы создали,<br>
<br>
741<br>
00:32:07,100 --> 00:32:10,640<br>
если вы заметели, каждый отдельный<br>
компонент говорит только о том, что<br>
<br>
742<br>
00:32:10,640 --> 00:32:14,520<br>
находится прямо по ним, что помогает<br>
массштабировать ваше приложение.<br>
<br>
743<br>
00:32:14,520 --> 00:32:16,340<br>
И это также имеет<br>
огромную побочную выгоду,<br>
<br>
744<br>
00:32:16,340 --> 00:32:18,260<br>
которая называется тестированием.<br>
<br>
745<br>
00:32:18,260 --> 00:32:19,230<br>
Вы же тестируете, правильно?<br>
<br>
746<br>
00:32:19,230 --> 00:32:24,500<br>
<br>
<br>
747<br>
00:32:24,500 --> 00:32:26,210<br>
Итак, скажем, вы хотите<br>
протестировать ваш UI.<br>
<br>
748<br>
00:32:26,210 --> 00:32:27,880<br>
Сейчас люди говорят UI-<br>
тестирование сложное.<br>
<br>
749<br>
00:32:27,880 --> 00:32:30,990<br>
UI-тестирование -<br>
да, это сложно.<br>
<br>
750<br>
00:32:30,990 --> 00:32:33,320<br>
Но часто это сложно потому,<br>
что вы пишете много кода<br>
<br>
751<br>
00:32:33,320 --> 00:32:35,290<br>
внутри Activity.<br>
<br>
752<br>
00:32:35,290 --> 00:32:38,630<br>
Теперь мы говорим, пиши<br>
больше во ViewModel,<br>
<br>
753<br>
00:32:38,630 --> 00:32:41,510<br>
и вы знаете, что UI только<br>
говорит к ViewModel,<br>
<br>
754<br>
00:32:41,510 --> 00:32:43,520<br>
так что вы можете избавиться от<br>
двух остальных [частей архитектуры].<br>
<br>
755<br>
00:32:43,520 --> 00:32:47,170<br>
Вам только нужно создать фальшивку<br>
ViewModel для тестирование вашего UI.<br>
<br>
756<br>
00:32:47,170 --> 00:32:50,900<br>
Тестирование вашего UI становится супер,<br>
супер easy with Espresso.<br>
<br>
757<br>
00:32:50,900 --> 00:32:52,880<br>
И у нас есть пример<br>
приложения на GitHub<br>
<br>
758<br>
00:32:52,880 --> 00:32:56,346<br>
где вы можете проверить<br>
с [НЕРАЗБОРЧИВО].<br>
<br>
759<br>
00:32:56,346 --> 00:32:58,220<br>
And the same thing as<br>
well as for ViewModels.<br>
<br>
760<br>
00:32:58,220 --> 00:32:59,660<br>
If you want to<br>
test the ViewModel,<br>
<br>
761<br>
00:32:59,660 --> 00:33:02,330<br>
you know it's only talks<br>
to the repositories.<br>
<br>
762<br>
00:33:02,330 --> 00:33:05,860<br>
You replace it with a mock<br>
respository, and it works.<br>
<br>
763<br>
00:33:05,860 --> 00:33:08,570<br>
And you can even<br>
test your ViewModels<br>
<br>
764<br>
00:33:08,570 --> 00:33:11,150<br>
on your host machine, on JVM.<br>
<br>
765<br>
00:33:11,150 --> 00:33:12,780<br>
And last but not<br>
least, you can test<br>
<br>
766<br>
00:33:12,780 --> 00:33:14,030<br>
the respository the same way.<br>
<br>
767<br>
00:33:14,030 --> 00:33:16,040<br>
You just mock the data sources.<br>
<br>
768<br>
00:33:16,040 --> 00:33:21,000<br>
You can easily test your<br>
repositories as JUnit test.<br>
<br>
769<br>
00:33:21,000 --> 00:33:23,060<br>
Now, I know this has been<br>
a lot of information.<br>
<br>
770<br>
00:33:23,060 --> 00:33:26,420<br>
We have two sessions tomorrow,<br>
and also documentation.<br>
<br>
771<br>
00:33:26,420 --> 00:33:29,630<br>
But now I want to call<br>
our product manager lUKAS<br>
<br>
772<br>
00:33:29,630 --> 00:33:32,646<br>
to talk about what to do next.<br>
<br>
773<br>
00:33:32,646 --> 00:33:35,574<br>
[APPLAUSE]<br>
<br>
774<br>
00:33:35,574 --> 00:33:41,425<br>
<br>
<br>
775<br>
00:33:41,425 --> 00:33:42,800<br>
LUKAS BERGSTROM:<br>
Like Yigit said,<br>
<br>
776<br>
00:33:42,800 --> 00:33:44,870<br>
we just covered a lot of ground.<br>
<br>
777<br>
00:33:44,870 --> 00:33:46,820<br>
And actually, we glossed<br>
over a lot of detail<br>
<br>
778<br>
00:33:46,820 --> 00:33:48,080<br>
while we did that.<br>
<br>
779<br>
00:33:48,080 --> 00:33:50,420<br>
But luckily, you don't<br>
have to remember everything<br>
<br>
780<br>
00:33:50,420 --> 00:33:51,950<br>
that you just heard.<br>
<br>
781<br>
00:33:51,950 --> 00:33:56,180<br>
We have a lot of material<br>
for you to check out<br>
<br>
782<br>
00:33:56,180 --> 00:33:58,910<br>
at developer.android.com/arch.<br>
<br>
783<br>
00:33:58,910 --> 00:34:03,305<br>
And that link should start<br>
working in 21 minutes.<br>
<br>
784<br>
00:34:03,305 --> 00:34:06,260<br>
<br>
<br>
785<br>
00:34:06,260 --> 00:34:07,790<br>
We wanted to give<br>
you guys a chance<br>
<br>
786<br>
00:34:07,790 --> 00:34:10,219<br>
to kind of blog and tweet<br>
about this before anybody else.<br>
<br>
787<br>
00:34:10,219 --> 00:34:13,190<br>
So that's why we held it back.<br>
<br>
788<br>
00:34:13,190 --> 00:34:15,560<br>
So yeah, we made having<br>
good documentation<br>
<br>
789<br>
00:34:15,560 --> 00:34:18,469<br>
and samples a priority from<br>
the beginning of this project,<br>
<br>
790<br>
00:34:18,469 --> 00:34:22,310<br>
since providing good guidance is<br>
really one of the major goals.<br>
<br>
791<br>
00:34:22,310 --> 00:34:24,800<br>
So you're going to find<br>
in-depth documentation that's<br>
<br>
792<br>
00:34:24,800 --> 00:34:27,337<br>
written from the perspective<br>
of an app developer.<br>
<br>
793<br>
00:34:27,337 --> 00:34:29,420<br>
You're going to find really<br>
meaty sample apps that<br>
<br>
794<br>
00:34:29,420 --> 00:34:31,280<br>
show how to build a real app.<br>
<br>
795<br>
00:34:31,280 --> 00:34:34,650<br>
And just as an example of<br>
how much work went into this,<br>
<br>
796<br>
00:34:34,650 --> 00:34:36,139<br>
we have a GitHub<br>
browser sample app<br>
<br>
797<br>
00:34:36,139 --> 00:34:39,440<br>
that probably has better test<br>
coverage than many real world<br>
<br>
798<br>
00:34:39,440 --> 00:34:42,170<br>
apps, written by that guy.<br>
<br>
799<br>
00:34:42,170 --> 00:34:44,820<br>
<br>
<br>
800<br>
00:34:44,820 --> 00:34:47,420<br>
And of course, we have the<br>
guide to app architecture,<br>
<br>
801<br>
00:34:47,420 --> 00:34:50,929<br>
which internally, we called the<br>
Opinionated Guide for a while.<br>
<br>
802<br>
00:34:50,929 --> 00:34:53,210<br>
And we think that<br>
label still applies.<br>
<br>
803<br>
00:34:53,210 --> 00:34:55,639<br>
But even if you're not<br>
planning to use our recommended<br>
<br>
804<br>
00:34:55,639 --> 00:34:58,580<br>
architecture, we think people<br>
should check out the guide.<br>
<br>
805<br>
00:34:58,580 --> 00:35:04,010<br>
It has principles that we think<br>
apply to all apps on Android.<br>
<br>
806<br>
00:35:04,010 --> 00:35:07,760<br>
And you're probably asking<br>
yourself, do I not--<br>
<br>
807<br>
00:35:07,760 --> 00:35:09,830<br>
what's the impact of<br>
this going to be on me?<br>
<br>
808<br>
00:35:09,830 --> 00:35:13,160<br>
Am I going to have to change the<br>
way that I'm doing everything?<br>
<br>
809<br>
00:35:13,160 --> 00:35:15,315<br>
You know, if you're<br>
starting a new project,<br>
<br>
810<br>
00:35:15,315 --> 00:35:16,940<br>
or if you have an<br>
existing app, but you<br>
<br>
811<br>
00:35:16,940 --> 00:35:19,190<br>
want to improve the<br>
core architecture,<br>
<br>
812<br>
00:35:19,190 --> 00:35:22,100<br>
then yeah, we recommend<br>
taking a look at this stuff.<br>
<br>
813<br>
00:35:22,100 --> 00:35:24,050<br>
It's still preview.<br>
<br>
814<br>
00:35:24,050 --> 00:35:26,790<br>
We won't be hitting<br>
1.0 for a few months,<br>
<br>
815<br>
00:35:26,790 --> 00:35:30,050<br>
but we think it's definitely<br>
ready for you guys<br>
<br>
816<br>
00:35:30,050 --> 00:35:32,460<br>
to check out, and<br>
use in projects.<br>
<br>
817<br>
00:35:32,460 --> 00:35:34,250<br>
But if you're happy<br>
with what you have,<br>
<br>
818<br>
00:35:34,250 --> 00:35:37,360<br>
you don't need to<br>
rewrite your app.<br>
<br>
819<br>
00:35:37,360 --> 00:35:39,530<br>
So in the spirit of be<br>
together, not the same,<br>
<br>
820<br>
00:35:39,530 --> 00:35:41,890<br>
we're not dictating what<br>
everyone has to use.<br>
<br>
821<br>
00:35:41,890 --> 00:35:44,590<br>
If you're happy with your app<br>
architecture, you can keep it.<br>
<br>
822<br>
00:35:44,590 --> 00:35:46,510<br>
If you're happy with<br>
your existing ORM,<br>
<br>
823<br>
00:35:46,510 --> 00:35:48,820<br>
you don't have to use Room.<br>
<br>
824<br>
00:35:48,820 --> 00:35:51,910<br>
Architecture components are<br>
designed to work well together,<br>
<br>
825<br>
00:35:51,910 --> 00:35:55,780<br>
but they do work<br>
perfectly fine standalone.<br>
<br>
826<br>
00:35:55,780 --> 00:35:58,300<br>
And mixing and matching<br>
applies not only<br>
<br>
827<br>
00:35:58,300 --> 00:36:04,730<br>
to architecture components,<br>
but also third party libraries.<br>
<br>
828<br>
00:36:04,730 --> 00:36:11,760<br>
So-- I'm waiting for<br>
this slide to come up.<br>
<br>
829<br>
00:36:11,760 --> 00:36:14,389<br>
So yeah, so you can<br>
use what you have,<br>
<br>
830<br>
00:36:14,389 --> 00:36:16,680<br>
and to start to integrate<br>
architecture components where<br>
<br>
831<br>
00:36:16,680 --> 00:36:18,310<br>
they make sense.<br>
<br>
832<br>
00:36:18,310 --> 00:36:21,000<br>
So for example, if you're<br>
happy with Rx Java,<br>
<br>
833<br>
00:36:21,000 --> 00:36:24,510<br>
but you really like the<br>
Lifecycle aware component stuff<br>
<br>
834<br>
00:36:24,510 --> 00:36:27,360<br>
that Yigit just showed, so that<br>
you have these self-sufficient<br>
<br>
835<br>
00:36:27,360 --> 00:36:31,590<br>
components, you can use<br>
LiveData together with Rx Java.<br>
<br>
836<br>
00:36:31,590 --> 00:36:34,800<br>
So you can get all the<br>
power of Rx Java operators,<br>
<br>
837<br>
00:36:34,800 --> 00:36:36,420<br>
and now it's Lifecycle safe.<br>
<br>
838<br>
00:36:36,420 --> 00:36:39,510<br>
So kind of the best<br>
of both worlds.<br>
<br>
839<br>
00:36:39,510 --> 00:36:41,760<br>
And we've got additional<br>
integrations to come.<br>
<br>
840<br>
00:36:41,760 --> 00:36:45,890<br>
We're definitely looking at<br>
a lot of stuff internally<br>
<br>
841<br>
00:36:45,890 --> 00:36:48,480<br>
that would be nice if<br>
it were self-sufficient<br>
<br>
842<br>
00:36:48,480 --> 00:36:50,500<br>
and Lifecycle aware.<br>
<br>
843<br>
00:36:50,500 --> 00:36:53,460<br>
And if you're a<br>
library developer,<br>
<br>
844<br>
00:36:53,460 --> 00:36:55,920<br>
we really recommend<br>
checking out Lifecycles<br>
<br>
845<br>
00:36:55,920 --> 00:36:57,690<br>
and LifecycleObserver<br>
because we think<br>
<br>
846<br>
00:36:57,690 --> 00:37:00,480<br>
there is a really bright<br>
future, and a lot of potential<br>
<br>
847<br>
00:37:00,480 --> 00:37:03,420<br>
in making libraries and<br>
components that are Lifecycle<br>
<br>
848<br>
00:37:03,420 --> 00:37:07,870<br>
aware by default.<br>
But before you go<br>
<br>
849<br>
00:37:07,870 --> 00:37:11,110<br>
do that, we have a lot more<br>
for you at I/O this year.<br>
<br>
850<br>
00:37:11,110 --> 00:37:15,310<br>
We have two more talks,<br>
one on Lifecycles<br>
<br>
851<br>
00:37:15,310 --> 00:37:18,280<br>
that's even more in-depth than<br>
what we just showed tomorrow<br>
<br>
852<br>
00:37:18,280 --> 00:37:20,020<br>
morning.<br>
<br>
853<br>
00:37:20,020 --> 00:37:24,040<br>
We have another one on<br>
Room and Persistence,<br>
<br>
854<br>
00:37:24,040 --> 00:37:25,480<br>
and going a little<br>
bit beyond Room<br>
<br>
855<br>
00:37:25,480 --> 00:37:27,790<br>
starting at 12:30 tomorrow.<br>
<br>
856<br>
00:37:27,790 --> 00:37:31,950<br>
And we'll have people who are<br>
well-versed in architecture<br>
<br>
857<br>
00:37:31,950 --> 00:37:36,740<br>
components in the<br>
sandbox for all of I/O.<br>
<br>
858<br>
00:37:36,740 --> 00:37:41,600<br>
And we also have codelabs,<br>
which we're pretty happy with.<br>
<br>
859<br>
00:37:41,600 --> 00:37:43,890<br>
And there's more to come.<br>
<br>
860<br>
00:37:43,890 --> 00:37:46,100<br>
So we think we've just<br>
scratched the surface of ways<br>
<br>
861<br>
00:37:46,100 --> 00:37:48,260<br>
that we can improve the<br>
experience of using Android<br>
<br>
862<br>
00:37:48,260 --> 00:37:51,320<br>
Frameworks, and we're looking<br>
at applying this approach<br>
<br>
863<br>
00:37:51,320 --> 00:37:53,310<br>
in other areas as well.<br>
<br>
864<br>
00:37:53,310 --> 00:37:54,980<br>
So some things<br>
already in the works.<br>
<br>
865<br>
00:37:54,980 --> 00:37:58,310<br>
And we're also interested in<br>
hearing from you on what else<br>
<br>
866<br>
00:37:58,310 --> 00:37:59,720<br>
you'd like to see.<br>
<br>
867<br>
00:37:59,720 --> 00:38:04,010<br>
So come by, talk to us, tell us<br>
what you like, what you don't.<br>
<br>
868<br>
00:38:04,010 --> 00:38:06,800<br>
And stay tuned, because we're<br>
really excited about the future<br>
<br>
869<br>
00:38:06,800 --> 00:38:08,570<br>
of Android development.<br>
<br>
870<br>
00:38:08,570 --> 00:38:09,310<br>
Thank you.<br>
<br>
871<br>
00:38:09,310 --> 00:38:11,460<br>
[APPLAUSE]<br>
<br>
872<br>
00:38:11,460 --> 00:00:00,000<br>
<br>
<br>


</td></tr> 
  </table>
  
