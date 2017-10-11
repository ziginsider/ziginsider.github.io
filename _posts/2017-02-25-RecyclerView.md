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
### Принцип работы RecyclerView в общих словах:
1. Прокручивается список, создаются вьюхи и выводятся на экран, при этом выполняется <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onCreateViewHolder()</span> и <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span>. 

2. Ушедшие за экран вьюхи не уничтожаются, а попадают в пул объектов <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">Recycled Pool</span>. 

3. При дальнейшем скролле, вьюхи появляющиеся из-за пределов экрана не пересоздаются, а берутся из этого самого пула . При этом срабатывает только <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span>. 

Говоря отвлеченно, метод <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onCreateViewHolder()</span> создает "бассейн", а метод  <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span> "наполняет бассейн водой". Если каждый раз, когда меняется представление (скролл) не "менять воду в бассейне" полностью т.е. не переопределять содержание всех элементов, которые могут измениться, в <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span>, то вьюха может выдавать сюрпризы в виде старых значений. 

### Компоненты RecyclerView:
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">LayoutManager</span> - размещает элементы
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">ItemAnimator</span> - анимирует элементы
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">Adapter</span> - создает элементы
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">Decorator</span> - дорисовывает элементы 
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">ViewHolder</span> - кеширует findViewById

## LayoutManager
Бывает:
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">LinearLayoutManager</span> (линейное размещение элементов)
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">GridLayoutManager</span> (табличное)
- <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">StaggeredGridLayoutManager</span> (сложное) 

<img src="{{ site.baseurl }}/images/LayoutManager_looks.jpg">
<br>
Обязаности LayoutManager'а:
- размещает элементы
- отвечает за размер элементов (measure)
- отвечает за то, какие элементы больше не нужны
- отвечает за скроллинг
- отвечает за View Focusing (В случае <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">ListView</span> отвечал сам <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">ListView</span>); т.е. на каком элементе сфокусироваться.
- отвечает за Accessibility; для людей с ограниченными возможностями. 

Что делать, если стандартная реализация не подходит? Два варианта:
- Переопределить стандартный LayoutManager:<br>
Например, у нас есть LinearLayoutManager. Нам необходимо сделать так, что при малом количестве элементов, наш LinearManager будет по высоте занимать ровно столько места, сколько нужно под это количество элементов. Тогда делаем свой ExtendedLinearLayoutManager, где переопределяем метод onMeasure().
- Написать свой LayoutManager:<br>
Достаточно переопределить (для компиляции) метод RecyclerView.LayoutParams generateDefaultLayoutParams(...), который будет говорить, какие по умолчанию параметры должны быть применены к новым View.<br>
Не стоит забывать также void onLayoutChildren(...) - непосредственное размещение наших дочерних View на экране.<br>
boolean canScrollHorizontally(...) - говорим можем ли мы листать горизонтально<br>
boolean canScrollVertically(...) - вертикально...<br>


### Adapter
<img src="{{ site.baseurl }}/images/RecyclerView2.png"> 
Обязанности Adapter'а: 
- создание ViewHolder'ов
- заполнение ViewHolder'ов информацией
- уведомление <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">RecyclerView</span> о том какие элементы изменились.
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
### Методы notifyItemX() 
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
- Нет лишних вызовов <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span>; 
- Возможность анимировать и перемещать элементы как угодно 
- Нет лишних вызовов <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onCreateViewHolder()</span> 

{% highlight java %}
void setHasStableIds(boolean hasStableIds)
{% endhighlight %} - если в конструкторе вызвать этот метод с true, то <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">RecyclerView</span> сам будет вычислять, какие элементы поменялись местами, какие добавились, удалились и т.д. Для этого необходимо реализовать:
{% highlight java %}
long getItemId(int position)
{% endhighlight %}
и давать уникальное Id элемента на основе его содержимого или создавать Id на основе Id layout'a, из которого мы надуваем это view, и который всегда уникальный.


### Типичные ошибки  
1) Обработка нажатий на элемент внутри onBindViewHolder(...):
{% highlight java %}
public void onBindViewHolder(...) {
    holder.itemView
    .setOnClickListener(v -> {
        itemClicked(position);
    });
}
{% endhighlight %}
Во-первых, создается объект на каждый Bind. Во-вторых, берется position элемента, которая у него была до <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onBindViewHolder()</span>. Но элемент с помощью <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">notify()</span> может быть перемещен/удален и его position, следовательно, измениться. Для этой ситуации есть решение, а именно установить слушатель нажатия при создании элемента:
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
Очень важно проверить на <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">NO_POSITION</span>. Сложно представить, как можно кликнуть на то, у чего нет позиции, но иногда такое происходит. Рекомендация от Google не забывать делать эту проверку.

2)
{% highlight java %}
public ViewHolder onCreateViewHolder(...) {
    if (cachedHeader == null) {
        cachedHeader = createHeader();
    }
    if (viewType == R.layout.header) {
        return cachedHeader;
    } else {
        return createItem();
    }
}
{% endhighlight %}

Но зачем кэшировать (создавать) заранее? Надо создавать, когда в этом есть необходимость. 

### ViewHolder 

<img src="{{ site.baseurl }}/images/RecyclerView3.png">

Обязателен, в отличии от реализации ListView.

Для чего нужен был ViewHolder раньше?
Ответ: кеширование относительно дорогого findViewById 

Для чего нужен ViewHolder теперь? 
- кеширование относительно дорогого findViewById 
- Мост между LayoutManager, Animator’ами и Decorator’ами
- Основной элемент Recycling’а

API ViewHolder’а:
{% highlight java %}
getAdapterPosition();
getItenId();
getItemViewType();
getLayoutPosition();
getOldPosition();
isRecyclable() / setRecyclable(Boolean)
{% endhighlight %}

### Жизнь и смерть ViewHolder’а  

- LayoutManager  дает запрос RecyclerView на элемент: getViewForPosition 
- RecyclerView обращается в Cache 
- Если в Cache нет элемента, RecyclerView  идет в Adapter и просит у него viewType 
- Получив ViewType RecyclerView идет в Recycler Pool: getViewHolderByType, в котором может хранится элемент с неправильными данными, которые надо потом заполнить. 
- Если Recycler Pool не вернул элемент, он идет в Adapter и просит последнего создать элемент. 
- Если Recycler Pool вернул элемент, то RecyclerView просит Adapter сделать bindViewHolder (заполнить данные) и возвращает элемент LayoutManager’у 

В случае, если LayoutManager добавляет элемент: 
- LayoutManager сообщает RecyclerView о том, что создает элемент: addView 
- RecyclerView посылает запрос Adapter’у: onViewAttachedToWindow  

В случае удаления элемента: 
- LayoutManager сообщает RecyclerView о том, что удаляет элемент: removeAndRecycleView 
- RecyclerView посылает запрос Adapter’у: onViewDettachedToWindow 
- RecyclerView идет в Cache, если элемент валидный (isValid? А если не valid то сразу идет в Recycler Pool) для этой позиции, помещает туда элемент 
- Cache помещает старые элементы в Recycler Pool (recycle) 
- Recycled Pool сообщает Adapter’у, что элемент (view) был переиспользован и Adapter может сделать с ним что хочет: onViewRecycled (те элементы которые попадают в Recycled Pool, понадобятся нескоро, в отличии от тех, которые находятся в Cache) 

Удаление из представления с т.з. RecyclerView:  
RecyclerView при удалении своего child из представления (прокрутка, удаление элемента) view не удаляет ее сразу, но помещает в re add to ViewGroup, скрывает view от LayoutManager’а (иначе LM упадет с exeption, т.к. он занет только о видимых элементах) и говорит ItemAnimator’у, что ее надо анимировать. 

Удаление из представления с т.з. LayoutManager’а:  
Если LayoutManager удаляет элемент из представления он посылает запрос к RecyclerView removeAndRecycleView. RecyclerView проверяет view на валидность (isValid?) NO! -> отправляет view в Recycler Pool. Recycled Pool проверяет элемент на транзиентность hasTransientState? – состояние (на системном уровне, а не уровне RecyclerView) когда не ясно в каком состоянии view (например, анимация или selection text). И тут (hasTransientState = true) выходит на сцену Adapter. У него есть возможность последний раз сказать RecyclerView, что view можно переиспользовать. И если он скажет, что можно, то recycle’м его, иначе – навсегда его теряем (отсюда вывод: единственный, кто может анимировать view – ItemAnimator. Остальное на свой страх и риск: можно потерять ViewHolder) 

NB: как проверить список на ошибки (торможнение, неправильное использование hasTransientState и глюки из-за этого). Открывает дебажный лог и начинаем прокручивать список. Если видим, что потребление памяти растет, то у нас ошибка в архитектуре Recycler’а (ViewHolder не освобождается) 

Еще один способ умереть ViewHolder’у. RecyclerView обращается к Recycled Pool: addViewToPool. Recycled Pool проверяет есть ли место для еще одного ViewHolder’а типа Х. Если место есть, то ОК. Иначе, ViewHolder умирает. 

Почему места может не быть? 
- Слишком много ViewHolder’ов одного типа 
Почему слишком много? 
- Произошла crossfade анимация для всего списка 
- notifyItemRangeChanged(0, getItemCount());  
Как исправить? 
- Правильно вызывать notifyItemChanged 
- pool.setMaxRecycledViews(type, count); (кол-во эл-ов кот. будут кэшиться, важно для тех у кого неоднородные списки, для одних типов (тех кот.больше на экране) можно увеличить значения, для других (тех кот. меньше) – уменьшить)  

### ItemDecorator 

Adapter - для того чтобы представить какой-либо массив данных на экране.
ItemDecorator - для того чтобы дополнить это представление в зависимости от какой-либо логики (например, смена ориентации экрана) вашего приложения. 

Для чего применяется:  
- добавление разделителей и отступов
- отображение выбранного элемента (выделение)
- рисование любого контента за и перед view 

API: 
{% highlight java %}

//определяет расстояние, которое 
//будет между элементами списка
public void getItemOffsets(Rect out Rect, //top, bottom, right, left
    View view, //view to decorate
    RecyclerView parent,
    RecyclerView.State state)

//вызывается до того как все элементы
//списка будут отрисованы
public void onDraw(Canvas c,
    RecyclerView parent,
    RecyclerView.State state)

//после всех элементов...
public void onDrawOver(Canvas c,
    RecyclerView parent,
    RecyclerView.State state) 

{% endhighlight %}

onDraw() и onDrawOver() - вызываются на каждый шаг отрисовки списка, поэтому в этих методах не стоит помещать тяжелых операций (инициализация объекта и т.д.)

Декораторов у RecyclerView может быть не один, а несколько, что позволяет помещать различную логику в разные классы.

Реализация:
{% highlight java %}
Class CustomDecoration extends RecyclerView.ItemDecoration {
    @Override
    getItemOffset(...){...}
}
{% endhighlight %}


Частые ошибки: 
{% highlight java %}
public void getItemOffsets(Rect out Rect,
        View view,
        RecyclerView parent,
        RecyclerView.State state) {
    parent.indexOfChild(view); //так делать можно, но не нужно
//т.к. состояние view когда их обрабатывает декоратор
// может сильно отличаться от реального состояния вещей
    parent.getAdapter().getItemCount(); //some problem 
}
{% endhighlight %}

И для избегания таких ситуаций есть замечательные методы: 
{% highlight java %}
public void getItemOffsets(Rect out Rect,
        View view,
        RecyclerView parent,
        RecyclerView.State state) {
    parent.getchildViewHolder(view).getLayoutPosition();
    parent.getChildViewHolder(view).getAdapterPosition();
    state.getItemCount();
}
{% endhighlight %}

### ItemTouchHelper 

Статья призванная показать, как использовать ItemTouchHelper в RecyclerView: <a href="https://medium.com/@ipaulpro/drag-and-swipe-with-recyclerview-b9456d2b1aaf">Drag and Swipe with RecyclerView</a>

Для чего нужен?
- Drag&Drop
- Swipe to dismiss 

API:
{% highlight java %}
public int getMovementFlags(RecyclerView recyclerView,
                            RecyclerView.ViewHolder viewHolder)

public boolean onMove(RecyclerView recyclerView,
                      RecyclerView.ViewHolder viewHolder,
                      RecyclerView.ViewHolder target)

public void onSwiped(RecyclerView.ViewHolder viewHolder,
                     int direction)

etc.  
{% endhighlight %}

Реализация:
{% highlight java %}
ItemTouchHelper.SimpleCallback touchCallback = new ... {
    @Override
    public int getMovementFlags(RecyclerView recyclerView, 
    RecyclerView.ViewHolder viewHolder) {
        int dragFlags = ItemTouchHelper.UP | ItemTouchHelper.DOWN;
        int swipeFlags = ItemTouchHelper.START | ItemTouchHelper.END;
        return makeMovementFlags(dragFlags, swipeFlags);
    }
    @Override
    public Boolean onMove(...){...}
    @Override
    public void onSwipe(...){...}
};

ItemTouchHelper itemTouchHelper = new ItemTouchHelper(touchCallback);

itemTouchHelper.attachToRecyclerView(recyclerView);
{% endhighlight %}

<br><br>
### ItemAnimator 

ItemAnimator - позволяет анимировать добавление, удаление, изменение элементов.

Схема запуска анимации после методов notifyItemX() (методы см. выше):
<br>
<img src="{{ site.baseurl }}/images/ItemAnimatorTimeLine.jpg">
<br>

Отрисовка элементов делится на два этапа:
- preLayout - элементы до изменения списка + те, что должны появиться;
- postLayout - элементы после окончания анимации.
RecyclerView запоминает состояние preLayout и сравнивает его с состоянием PostLayout. И определив эту разницу, RecyclerView запускает анимацию элементов.

#### ExpandableLayout

- Подход 1 (неправильный):
Дерграем requestLayout() для view:
{% highlight java %}
v.getLayoutParams().height = (int)(targetHight * interpolatedTime);
v.requestLayout();
{% endhighlight %}

Плохой подход т.к. requestLayout() не предназначен для анимации 

- Подход 2: Кастомный Adapter


### Практика

*Как заполнить RecyclerView данными, когда их много?* 

Способ №1:

Повесьте на RecyclerView слушатель прокрутки и, когда он будет прокручен до последнего элемента, подгружайте новую порцию данных.

Пример реализации: <a href="https://github.com/ziginsider/DynamicLoadingRecyclerView/tree/master">https://github.com/ziginsider/DynamicLoadingRecyclerView/tree/master</a>

Способ №2:

{% highlight java %}
@Override
  public void onViewAttachedToWindow(final ViewHolder holder) {
    super.onViewAttachedToWindow(holder);
    int layoutPosition = holder.getLayoutPosition();
    ...
  }
{% endhighlight %}

В адаптере можно получить позицию только что появившегося элемента списка. Если позиция появившегося элемента последняя, значит пора подгружать новую порцию данных








