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
*Перевод английских субтитров на русские из видео Architecture Components - Introduction (Google I/O '17). Предпринят только для практики перевода с английского, скажем так to improve my reading and listening scills. Делается постепенно. Начало 20.08.2017, конец - . All rights reserved.*

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
и UI инструментарий (toolkit) <br>
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

</td></tr> 
  </table>
  
