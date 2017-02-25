---
layout: post
title: Препарирование RecyclerView
date: 2017-02-25 18:19
tags:
- Android
- Java
- RecyclerView
- моё
---
<img src="{{ site.baseurl }}/images/RecyclerView1.png">
<br>

*Заметки о RecyclerView. Принципы работы. Внутреннее устройство.*
<br>
## Компоненты RecyclerView:
- LayoutManager - размещает элементы
- ItemAnimator - анимирует элементы
- Adapter - создает элементы
- Decorator - дорисовывает элементы 


## LayoutManager
Бывает:
- LinearLayoutManager (линейное размещение элементов)
- GridLayoutManager (табличное)
- StaggeredGridLayoutManager (сложное) 

Обязаности LayoutManager'а:
- размещает элементы
- отвечает за скроллинг
- отвечает за View Focusing (В случае ListView отвечал сам ListView); т.е. на каком элементе сфокусироваться.
- отвечает за Accessibility; для людей с ограниченными возможностями. 


## Adapter
<img src="{{ site.baseurl }}/images/RecyclerView2.png"> 
Обязанности Adapter'а: 
- создание ViewHolder'ов
- заполнение ViewHolder'ов информацией
- уведомление RecyclerView о том какие элементы изменились.
- обработка касаний
- частичное обновление данных
- управление количеством ViewType'ов
- информация о переиспользовании ViewHolder'а 

Основное API Adapter'a:
<br>
{% highlight java %}
ViewHolder onCreateViewHolder(ViewGroup parent, int viewType)
{% endhighlight %}
<br>
{% highlight java %}
void onBindViewHolder(ViewHolder holder, int position)
{% endhighlight %} 
При изменении позиции элемента не вызывается, поэтому нельзя вызывать так: см. типичные ошибки #1 
<br><br>
{% highlight java %}
int getItemViewType(int position)
{% endhighlight %}
<br>
{% highlight java %}
boolean onFailedToRecycleView(ViewHolder holder)
{% endhighlight %}
<br>
{% highlight java %}
void onViewRecycled(ViewHolder holder)
{% endhighlight %}
<br> 
## методы notifyItemX() 
<br>
Нужны для того, чтобы изменять, удалять, добавлять элементы и при этом анимировать их:

notifyItemChanged();

notifyItemInserted();

notifyItemMoved();

notifyItemRemoved();

notifyItemRangeChanged();

notifyItemRangeInserted();

notifyItemRangeMoved();

notifyItemRangeRemoved();
<br><br>
польза от методов notifyItemX(): 
- Нет лишних вызовов onBindViewHolder(); 
- Возможность анимировать и перемещать элементы как угодно 
- Нет лишних вызовов onCreateViewHolder 

{% highlight java %}
void setHasStableIds(boolean hasStableIds)
{% endhighlight %} - если в конструкторе вызвать этот метод с true, то RecyclerView сам будет вычислять, какие элементы поменялись местами, какие добавились, удалились и т.д. Для этого необходимо реализовать:
{% highlight java %}
long getItemId(int position)
{% endhighlight %}
и давать уникальное Id элемента на основе его содержимого или создавать Id на основе Id layout'a, из которого мы надуваем это view, и который всегда уникальный.


Типичные ошибки
1)
{% highlight java %}
public void onBindViewHolder(...) {
    holder.itemView
    .setOnClickListener(v -> {
        itemClicked(position);
    });
}
{% endhighlight %}
