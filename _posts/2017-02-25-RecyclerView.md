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
## Принцип работы RecyclerView в общих словах:
1) прокручивается список, создаются вьюхи и выводятся на экран, при этом выполняется `onCreateViewHolder()` и `onBindViewHolder()`. 
2) ушедшие за экран вьюхи не уничтожаются, а попадают в пул объектов `Recycled Pool`. 
3) При дальнейшем скролле, вьюхи появляющиеся из-за экране не пересоздаются, а берутся из этого самого пула . При этом срабатывает только onBindViewHolder(). 

Говоря отвлеченно, метод ``onCreateViewHolder()`` создает "бассейн", а метод  <kbd>onBindViewHolder()</kbd> "наполняет бассейн водой". Если каждый раз, когда меняется представление (скролл) не "менять воду в бассейне" полностью т.е. не переопределять содержание всех элементов, которые могут измениться, в [tag: "onBindViewHolder()"], то вьюха может выдавать сюрпризы в виде старых значений. 

## Компоненты RecyclerView:
- `LayoutManager` - размещает элементы
- `ItemAnimator` - анимирует элементы
- `Adapter` - создает элементы
- `Decorator` - дорисовывает элементы 

## LayoutManager
Бывает:
- `LinearLayoutManager` (линейное размещение элементов)
- `GridLayoutManager` (табличное)
- `StaggeredGridLayoutManager` (сложное) 

Обязаности LayoutManager'а:
- размещает элементы
- отвечает за скроллинг
- отвечает за View Focusing (В случае `ListView` отвечал сам `ListView`); т.е. на каком элементе сфокусироваться.
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
## Методы notifyItemX() 
Нужны для того, чтобы изменять, удалять, добавлять элементы и при этом анимировать их:
{% highlight java %}
notifyItemChanged();
notifyItemInserted();
notifyItemMoved();
notifyItemRemoved();
notifyItemRangeChanged();
notifyItemRangeInserted();
notifyItemRangeMoved();
notifyItemRangeRemoved();
{% endhighlight %}
польза от методов notifyItemX(): 
- Нет лишних вызовов `onBindViewHolder()`; 
- Возможность анимировать и перемещать элементы как угодно 
- Нет лишних вызовов `onCreateViewHolder()` 

{% highlight java %}
void setHasStableIds(boolean hasStableIds)
{% endhighlight %} - если в конструкторе вызвать этот метод с true, то `RecyclerView` сам будет вычислять, какие элементы поменялись местами, какие добавились, удалились и т.д. Для этого необходимо реализовать:
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
Во-первых, создается объект на каждый Bind. Во-вторых, берется position элемента, которая у него была до `onBindViewHolder()`. Но элемент с помощью `notify()` может быть перемещен/удален и его position, следовательно, измениться. Для этой ситуации есть решение, а именно установить слушатель нажатия при создании элемента:
{% highlight java %}
public RecyclerView.ViewHolder onCreateViewHolder(...) {
    View v = createView();
    RecyclerView.ViewHolder h = new RecyclerView.ViewHolder(v) {};
    v.setOnClickListener(it -> {
        int adapterPosition = h.getAdapterPosition();
        if (adapterPosition != RecyclerView.NO_POSITION) {
            itemClicked(adapterPosition);
        }
    });
    return h;
}
{% endhighlight %}
Очень важно проверить на `NO_POSITION`. Сложно представить, как можно кликнуть на то, у чего нет позиции, но иногда такое происходит. Рекомендация от Google не забывать делать эту проверку.
