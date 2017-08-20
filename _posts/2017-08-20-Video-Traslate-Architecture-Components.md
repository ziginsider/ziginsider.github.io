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
}

th{
    border:1px solid #000000;
}

td{
    border:1px solid #000000;
}
</style>
<table bordercolor="black" border="1" width="100%">
   <caption>Перевод субтитров</caption>
   <tr>
    <th>English</th>
    <th>Русский</th>
   </tr>
   <tr><td>1 
00:00:00,000 --> 00:00:05,189 
[MUSIC PLAYING] 
 
2 
00:00:05,189 --> 00:00:05,980 
MIKE CLERON: So hi. 
 
3 
00:00:05,980 --> 00:00:07,080 
I'm Mike Cleron.  
 
4 
00:00:07,080 --> 00:00:08,650 
I'm on the Android team. 
 
5 
00:00:08,650 --> 00:00:14,120 
I manage the system UI framework 
and UI toolkit teams there.  
 
6 
00:00:14,120 --> 00:00:17,650 
We're going to be talking 
today in a lot of detail  
 
7 
00:00:17,650 --> 00:00:21,790 
about some big changes to 
how we recommend that you  
 
8 
00:00:21,790 --> 00:00:23,710 
build Android applications.  
 
9 
00:00:23,710 --> 00:00:26,110 
But before we go into 
a lot of the details, 
 
10 
00:00:26,110 --> 00:00:28,510 
I thought would be helpful 
to step back a bit, 
 
11 
00:00:28,510 --> 00:00:31,960 
and frame the discussion by 
talking about where we came 
 
12 
00:00:31,960 --> 00:00:34,730 
from, and where we're going. 
 
13 
00:00:34,730 --> 00:00:36,100 
So let's do that. 
 
14 
00:00:36,100 --> 00:00:39,010 
So to start, Android 
has always been based 
 
15 
00:00:39,010 --> 00:00:41,230 
on some strong principles. 
</td><td>1 
00:00:00,000 --> 00:00:05,189 
[Музыка] 
 
2 
00:00:05,189 --> 00:00:05,980 
MIKE CLERON: Привет! 
 
3 
00:00:05,980 --> 00:00:07,080 
Я Майк Клерон. 
 
4 
00:00:07,080 --> 00:00:08,650 
Я из Android team. 
 
5 
00:00:08,650 --> 00:00:14,120 
Я разрабатываю UI фреймворк и UI инструментарий (toolkit) 
 
6 
00:00:14,120 --> 00:00:17,650 
Сегодня мы будем говорить о многих деталях 
 
7 
00:00:17,650 --> 00:00:21,790 
и о некоторых больших изменениях в подходах, 
которые мы рекомендуем 
 
8 
00:00:21,790 --> 00:00:23,710 
при проектировании приложений для Android. 
 
9 
00:00:23,710 --> 00:00:26,110 
Но прежде чем мы погрузимся 
в детали, 
 
10 
00:00:26,110 --> 00:00:28,510 
я думаю, что будет полезно 
сделать шаг в сторону, 
 
11 
00:00:28,510 --> 00:00:31,960 
и поговорить о том, 
откуда мы пришли 
 
12 
00:00:31,960 --> 00:00:34,730 
и куда мы идем. 
 
13 
00:00:34,730 --> 00:00:36,100 
Давайте начнем. 
 
14 
00:00:36,100 --> 00:00:39,010 
Итак, Android 
всегда основывался на 
 
15 
00:00:39,010 --> 00:00:41,230 
на нескольких прочных принципах 
</td></tr> 
  </table>
  
