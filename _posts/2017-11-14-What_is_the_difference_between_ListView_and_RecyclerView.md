---
layout: post
title: RecyclerView и ListView. В чем разница?
date: 2017-11-14 13:30
tags:
- Java
- Android
- RecyclerView
- ListView
---
*Заметка является переводом статьи Mateusz Budzar  <a href="https://proandroiddev.com/whats-the-difference-between-a-listview-and-a-recyclerview-cc02a2276b2c">"What’s the difference between a ListView and a RecyclerView?"</a>.*

<br>
### Введение
Поскольку мы Android разработчики, нам не сложно реализовать прокручиваемый список тем способом, который соответствует задаче. Но два наиболее популярных пути - <a href="https://developer.android.com/reference/android/widget/ListView.html">ListView</a> и <a href="https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html">RecyclerView</a>.

Первый из них прекрасный виджет, который был доступен с API 1. До Android Lollipop мы главным образом использовали этот способ, что было довольно неплохо - API был интуитивно понятен. Но к сожалению мы могли создать только вертикально прокручиваемый список, и чтобы он прокручивался плавно, прриходилось делать все надлежлащим способом. Кроме того, класс ListView довольно тяжелый - у него множество обязанностей. Всякий раз, когда нам требовалось обработать список, т.е. сконфигурировать его, единственный путь сделать это был через объект ListView внутри адаптера.

Сегодня мы используем RecyclerView. Как я упоминал, он появился в Android Lollipop и сразу изменил правила игры. Большинство вещей, которые мы ненавидели в ListView были убраны или изменены в RecyclerView. По умолчанию, мы получали больше возможностей. Создание макетов (LayoutManager) отделено, и мы получили больше свободы для манипуляции с данными, чем манипулирование только внутри адаптера.

*Если вы хотите узнать больше об этих механизмах, вы можете глянуть мои статьи, которые рассказывают, как реализовать <a href="https://medium.com/@mateuszbudzar/how-to-implement-a-listview-d5a2f718a7f1">ListView</a> и <a href="https://medium.com/@mateuszbudzar/how-to-implement-a-recyclerview-33fd4ff9988e">RecyclerView</a>*

*(От переводчика) O RecyclerView можно узнать больше в этой моей заметке <a href="https://ziginsider.github.io/RecyclerView/">https://ziginsider.github.io/RecyclerView/</a>*

Итак, опишем наиболее существенные различия между этими двумя механизмами..

<br>
### ViewHolder
Паттерн ViewHolder помогает сделать прокрутку нашего списка плавной. Он сохраняет ссылки на элементы списка, чтобы затем адаптер мог их переиспользовать. Благодаря этому надувание View элемента (inflating) и вызов дорогого метода findViewById() происходит всего пару раз, а не для каждого элемента списка.

Адаптер RecyclerView в обязательном порядке заставляет нас реализовать надувание элемента списка с помощью двух методов - onCreateViewHolder() и onBindViewHolder().

ListView, с другой стороны, не делает обязательным реализацию ViewHolder. И, если мы не реализуем надувание сами, внутри getView(), мы останемся без эффективной прокрутки в списке. 

<br>
### LayoutManager
<a href="https://developer.android.com/reference/android/support/v7/widget/RecyclerView.LayoutManager.html">LayoutManager</a> берет на себя ответсвенность за макетирование представления элементов. Благодаря этому у RecyclerView нет ответственности за поозиционирование элементов в списке. LayoutManager дает возможность выбирать позиционирование элементов списка относительно друг друга и выбирать способ прокрутки. Например, если нам нужен вертикальный или горизонтальный список, мы выбираем <a href="https://developer.android.com/reference/android/support/v7/widget/LinearLayoutManager.html">LinearLayoutManager</a>. Для табличного представления более подходит <a href="https://developer.android.com/reference/android/support/v7/widget/GridLayoutManager.html">GridLayoutManager</a>.

Раньше, с помощью ListView, мы могли создать список только с вертикальной прокруткой. Это было не удобно. Чтобы реализовать табличное представление, мы должны были использовать другой виджет - <a href="https://developer.android.com/reference/android/widget/GridView.html">GridView</a>.

<br>
### ItemDecoration
Обязанности <a href="https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ItemDecoration.html">ItemDecoration</a> просты в теории - декорировать элементы списка (рисование за ними, перед ними, между ними)- но нетривиальны в реализации. Вы должны наследоваться от класса ItemDecoration и реализовать ваше решение. У RecyclerView по-умолчанию нет разделителей между строк - это соответствует гайдлайнам <a href="https://material.io/guidelines/components/lists.html#">Material Design</a>. Однако, если нам необходим разделитель, мы можем использовать <a href="https://developer.android.com/reference/android/support/v7/widget/DividerItemDecoration.html">DividerItemDecoration</a> и добавить его в RecyclerView.

В случае ListView мы можем добавить разделитель прямо в описании layout ListView в файле xml. Но у нас нет гибкого механизма, наподобие ItemDecoration, для реализации разделителя.

<br>
### ItemAnimator
Последнее, но не менее важное отличие RecyclerView это наличие <a href="https://developer.android.com/reference/android/support/v7/widget/RecyclerView.ItemAnimator.html">ItemAnimator</a>. Как мы можем догадаться, он обрабатывает анимации появления или исчезновения элементов списка, или их изменения. По-умолчанию анимации RecyclerView красивые и плавные. Конечно, мы можем изменить эти анимации, реализовав свой ItemAnimator, но это также не очень просто. Чтобы упростить себе жизнь, мы можем расширить класс <a href="https://developer.android.com/reference/android/support/v7/widget/SimpleItemAnimator.html">SimpleItemAnimator</a> и реализовать методы, которые нам нужны (просто добавить анимации во ViewHolder наших View)

Честно говоря, реализация анимации в ListView была болью в заднице. Опять же, нам нужно было выяснять как мы справимся с этой задачей. Ничего хорошего. Я рад, что это закончилось.

<br>
### Notifying adapter
У нас есть несколько классных механизмов уведомления (notify) в адаптере RecyclerView. Мы все еще можем использовать notifyDataSetChanged(), но, если нам необходимо изменить только один элемент списка, к нашим услугам notifyItemInserted(), notifyItemRemoved() или даже notifyItemChanged() и т.д. Мы должны использовать подходящее уведомление, чтобы сработала надлежащая анимация. Используя ListView мы можем использовать лишь notifyDataSetChanged(), а со всем остальным мы должны были справляться сами.

<br>
### Вывод

ListView служил нам долгое время. Мы могли покрыть большинство случаев с его помощью. Но потребности пользователей сегодня более сложные. Дизайн списков становится все более и более сложным и ListView уже не справляется. Material Design принес другие изменения - красивее, но сложнее в реализации.

К счастью, когда был представлен RecyclerView, многие проблемы ушли. Этот механизм более эффективен по-умолчанию, анимации проще, макетирование проще и API намного приятнее.

Поэтому, если вы когда-либо задумываетесь какой из них выбрать - ваша первая мысль определенно должна быть о RecyclerView.

*NB от переводчика: Так и хочется добавить в конце статьи "Аминь!". Автор мастер рассказывать очевидные вещи. Но, мне кажется, он не совсем ясно дал понять, что RecyclerView намеренно сделан более сырым  (т.е. "не из коробки"), чтобы быть более гибким в реализации. И он определенно более сложен. Но это не должно пугать начинающих, т.к. c ghfrnbrjq реализация его не вызывает сложностей. Но, однако, есть очень много хитростей, которые я пока только начал описывать в заметке <a href="https://ziginsider.github.io/RecyclerView/">https://ziginsider.github.io/RecyclerView/</a>*

*А в тривиальных случаях вполне уместно использовать ListView.*
