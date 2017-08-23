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
на вы можете основывать<br>
ваше приложение.<br>
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

</td></tr> 
  </table>
  
