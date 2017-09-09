---
layout: post
title: Зачем нужны интерфейсы в ООП?
date: 2017-09-09 19:19
tags:
- Java
- Android
- Философия
- ООП
---
На русском Stackoverflow <a href="https://goo.gl/zvYH28">спросили</a> зачем в Java нужны интерфейсы? Народ дал много интересных ответов, но все они так или иначе говорили о том ЧТО есть интерфейс и КАК устроена его реализация. О практической пользе никто не сказал. Т.е. ответ на вопрос для чего используются интерфейсы дан не был. Видимо потому, что для большинства это и так ЯСНО. Но, думаю, есть те, которые понимаю ЧТО и КАК, но не знают ДЛЯ ЧЕГО.

Я дал такой ответ:

--

Допустим, мы создали Framework, который определяет, совершил ли пользователь double-click по экрану.

Там мы определили функцию: что_делать_если_пользователь_кликнул_2_раза_по_экрану().

Но мы решаем не определять поведение этой функции сами, а предоставить эту реализацию программисту, использующему наш фреймворк. Предоставление этой реализации можно сделать через механизм интерфейсов.

Функцию: что_делать_если_пользователь_кликнул_2_раза_по_экрану() засовываем в интерфейс.

И, таким образом, сам момент двойного клика по экрану определяет наш фреймворк, а вот что делать (рисовать звездочки на экране, запустить проигрывание музыки и т.д.) после этого события решает программист, который реализует наш интерфейс.

Польза: программисту не надо думать, как словить double-click. За ним только реализация ответа на это событие.

--

Для себя так понял практическую пользу интерфейсов. Как-то разбирал одну библиотеку, которая реализовывала Swipe&Dismiss карточек в RecyclerView. Эта библиотека реализовывала свой колбэк тоучхелпера:

{% highlight java %}
public class ItemTouchHelperCallBack extends ItemTouchHelper.Callback {
...
}
{% endhighlight %}

И соответственно в адаптере RecyclerView, нужно было реализовать функцию, которая вызывалась после Swipe&Dismiss в ItemTouchHelperCallBack. Соответственно передать реализацию этой функции в адаптер можно было только через механизм интерфейсов.

Еще раз наш колбэк тоучхелпера уже с интерфейсом и функцией, которая использует реализацию интерфейса:

{% highlight java %}
public class ItemTouchHelperCallBack extends ItemTouchHelper.Callback {
  ...
  private onSwipListener mOnSwipListener; //экземпляр интерфейса,
                                          //через который мы получим
                                          //реализованную Swipe&Dismiss
  ...
  //получаем реализацию интерфейса
  //эта функция связывает нашу реализацию с 
  //функциональностью библиотеки
  public void setOnSwipListener(onSwipListener onSwipListener) {
        this.mOnSwipListener = onSwipListener;
  }
  ...
  //функция, которая использует реализацию (имплементацию) интерфейса
  public void onSwiped(RecyclerView.ViewHolder viewHolder, int direction) {
        int position = viewHolder.getAdapterPosition();
        if (mOnSwipListener != null) {
            mOnSwipListener.onSwip(viewHolder,position);
        }
     }
  }
  ...
  //сам интерфейс
  public interface onSwipListener {
     void onSwip(RecyclerView.ViewHolder viewHolder, int position);
  }
  ...
}
{% endhighlight %}


Вот схема адаптера:

{% highlight java %}
public class RecyclerViewCardStackAdapter 
    extends RecyclerView.Adapter<RecyclerViewCardStackAdapter.CardStackViewHolder> 
    implements ItemTouchHelperCallBack.onSwipListener {
    ...
    //реализация интерфейса
    @Override
    public void onSwip(RecyclerView.ViewHolder viewHolder, int position) {
        remove(position);
    }
    ...
}
{% endhighlight %}

Таким образом, мы видим чем может быть полезен интерфейс. Скажем так, отложеной реализацией, когда мы все подготавливаем для какого-то действия, а потом, пользуясь этой подготовкой, реализуем только само действие.

Кстати, вот как приделывалась реализация интерфейса (в классе, где мы готовили наш RecyclerView и привязывали к нему адаптер):

{% highlight java %}
...
if (adapter instanceof ItemTouchHelperCallBack.onSwipListener) {
    ItemTouchHelperCallBack.onSwipListener swipListener =
            (ItemTouchHelperCallBack.onSwipListener) adapter;
    ItemTouchHelperCallBack itemTouchHelperCallBack = new ItemTouchHelperCallBack();
    itemTouchHelperCallBack.setOnSwipListener(swipListener);

    ItemTouchHelper itemTouchHelper = new ItemTouchHelper(itemTouchHelperCallBack);
    itemTouchHelper.attachToRecyclerView(recyclerView);
}
...

С помощью instanseof мы проверяем, есть ли реализация нашего интерфейса в адаптере. Получаем эту реализацию - swipListener. И привязываем ее - setOnSwipListener(swipListener).

Так то.
