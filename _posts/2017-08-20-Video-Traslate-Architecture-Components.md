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
</td><td>1<br>
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
</td></tr> 
  </table>
  
