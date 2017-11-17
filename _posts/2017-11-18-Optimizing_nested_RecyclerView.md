---
layout: post
title: Оптимизация прокрутки вложенных в друг друга RecyclerView
date: 2017-11-18 00:47
tags:
- Java
- Android
- RecyclerView
---
*Заметка основана на статье Ninad MG <a href="https://medium.com/@mgn524/optimizing-nested-recyclerview-a9b7830a4ba7">"Optimizing Nested RecyclerView"</a>.*

RecyclerView обеспечивает плавную прокрутку списка путем помещения ViewHolder'ов ушедших за пределы экрана элементов в так называемый пул (Pool). Далее, при появлении новых элементов, RecyclerView не создает их заново, но использует ViewHolder'ы из пула, надувая (inflate) их актуальными данными. Таким образом достигается переиспользованиe ViewHolder'а и повышается производетельность фреймворка.

NB: для более полной картины проблемы производительности в RecyclerView см. раздел "Жизнь и смерть ViewHolder'а" в <a href="https://ziginsider.github.io/RecyclerView/">данной заметке</a>. + раздел "Bonus" в <a href="https://ziginsider.github.io/Multiple_Row_Types_In_Recyclerview/">этой заметке</a>.

Итак, иногда, для создания некоторых макетов, нам необходимо вкладывать один RecyclerView в другой. Рассмотрим случай, когда горизонтальные RecyclerView вложены в вертикальный.

<img src="{{ site.baseurl }}/images/nested_recyclerview.jpeg">

Когда вы прокручивавете вложенные горизонтальные списки то прокрутка будет плавной, но если прокручивать вертикальный список - прокрутка может притормаживать. Это происходит от того, что у каждого RecyclerView свой пул ViewHolder'ов. И каждый раз, при прокрутке вертикального списка, горизонтальные будут заново создавать свои ViewHolder'ы.

Мы можем исправить эту ситуацию, разделив между всеми RecyclerView один пул ViewHolder'ов.

Это делается с помощью функции RecyclerView.setRecycledViewPool(RecycledViewPool):

{% gist af26d3d35c05e82150dac0c7ddec7dd4 %}

Теперь, когда у всех вложенных RecyclerView один пул ViewHolder'ов, они используют ViewHolder'ы друг друга, и прокрутка становится более плавной.

Но прокрутку можно оптимизировать еще больше. 

Во-первых, конкретному типу View, можно задать максимальное количество ViewHolder'ов, которые будут хранится в пуле:

{% gist f3ebf2ede8a8c12bc65ddecebdce348a %}

Таким образом, мы можем подкорректировать (т.е. увеличить) максимальные значения количества в пуле тех ViewHolder'ов, которых в каждый момент на экране больше, учитывая тот факт, что по умолчанию это количество равно пяти.

Во-вторых, начиная с <a href="https://developer.android.com/topic/libraries/support-library/revisions.html#25-1-0">support library 25.1.0</a> у нас <a href="https://developer.android.com/reference/android/support/v7/widget/LinearLayoutManager.html#setInitialPrefetchItemCount(int)">есть возможность</a> указать layoutManager'ам внутренних RecyclerView сколько View нужно подготовить перед появлением на экране:

{% gist 4f573b2c9047214e0affac11381d0f46 %}

где N - это количество видимых View.

Таким образом, если на экране внутренние горизонтальные списки за раз показывают минимум три с половиной View, мы можем написать так:

{% gist 71f1ddc6cc1b5c54ba66eec504953bf0 %}

NB: По-умолчанию данное N = 2

Это позволяет внутренним RecyclerView создавать свои View на ранней стадии, что повышает производительность при прокрутке внешнего списка.
