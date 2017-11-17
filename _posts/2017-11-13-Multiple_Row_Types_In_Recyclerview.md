---
layout: post
title: Различные типы Item View в RecyclerView
date: 2017-11-13 21:06
tags:
- Java
- Android
- RecyclerView
- Refactoring
---
*Заметка основана на статье Mateusz Dziubek  <a href="https://android.jlelse.eu/multiple-row-types-in-recyclerview-2febf66e96a4">"Multiple row types in RecyclerView"</a>. Приводится пример создания RecyclerView c различными типами View. В процессе написания код подвергается рефакторингу. Показывается эффективность применения различных паттернов программирования и рефакторинга в целом на простом для понимания примере.*

Проект на github: <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo">https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo</a>

<br>
### Постановка задачи
Итак, представим ситуацию, когда нам надо в один RecyclerView поместить несколько различных типов View. Допустим, это:

- кнопка
- картинка с текстом
- заголовок с текстом

На смартфоне мы должны получить что-то вроде этого:

<img src="{{ site.baseurl }}/images/dif_type_view.png">

Вдохновляясь статьей <a href="https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism">Replace Conditional with Polymorphism</a>, попробуем сделать это. Основная идея - каждому типу View соответсвует отдельный класс, и эти классы объединяются общим интерфейсом.

<br>
### layout
Создаем, три layout, соответствующих трем типам View.

Например, для row_type_button.xml примерно так:
{% gist a0110c871086c441be940beef168171d %}
<br>
Для <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo/blob/master/app/src/main/res/layout/row_type_image.xml">row_type_image.xm</a> и <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo/blob/master/app/src/main/res/layout/row_type_text.xml">row_type_text.xml</a> аналогично. Или см. по ссылкам.

layout <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo/blob/master/app/src/main/res/layout/activity_main.xml">activity_main.xml</a> см. по ссылке.

<br>
### Классы для каждого типа View
Имея в виду row_type_button, создаем для него класс. Не забываем о конструкторе и обработчике нажатия:
{% gist 01530f13258c4241bb569068cc50ea50 %}
<br>
Как видим, RowType и будет нашим объединяющим интерфейсом.

Далее, переходим к row_type_image. Незабываем о геттере для текста:
{% gist ebea55ea153afa99098e597c1095f4f5 %}
<br>
Наконец, row_type_text. Тут добавим геттеры для заголовка и текста:
{% gist 125d1fda79d847f1da5a930251c90c41 %}
<br>
### Объединяющий интерфейс
В адаптере мы будем различать типы наших View посредством int getItemViewType(int position). Теперь вспомним об особенности интерфейсов, в силу уникальности, хранить в себе константы. Т.е. сигнатура int в интерфейсе соответсвует сигнатуре public static final int в классе наследующем интерфейс.

Учитывая данную особенность, сконструируем наш интерфейс для различения типов View:

{% gist a9497c250d7695f47f18a62bb93941a0 %}
<br>
Теперь в адаптере мы сможем различать типы View используя instanceof и, таким образом, возвращать тип View. Итак...

<br>
### Адаптер
Получаем примерно такой адаптер:
{% gist 3ee7474e58eb22ab4ce5180e8b35a31e %}
<br>
Что сказать? Невооруженным взглядом можно видеть что кода много. Лично у меня возникает ощущение захламленности. Давайте улучшать ситуацию.

NB: Однако же все работает. Можно запустить и проверить. Реализацию MainActivity можно глянуть на github <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo/blob/master/app/src/main/java/io/github/ziginsider/multiplerowtypesinrecyclerviewdemo/MainActivity.java">тут</a>. Рефакторинг мы делаем исключительно из-за архитектурных соображений. В конечном итоге такой подход приносит пользу. Да и на код не страшно смотреть.

<br>
### Рефакторинг
Во-первых, у нас три различных ViewHolder. Ничто не мешает нам применить к этой тройке шаблон проектирования <a href="https://ru.wikipedia.org/wiki/%D0%A4%D0%B0%D0%B1%D1%80%D0%B8%D1%87%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D1%82%D0%BE%D0%B4_(%D1%88%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD_%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F)">"Фабрика"</a>. Одной ответственностью станет меньше.

Заводим отдельный класс ViewHolderFactory и выносим туда наши холдеры. Внутри класса определяем функцию viewHolder create(parent, viewType), которая будет создавать необходимый холдер, согласно типу View:
{% gist d987cfc648bf4b4891020e07feeaf856 %}
<br>
Кроме того каждый data-класc, представляющий определенный тип View (ButtonRowType, ImageRowType, TextRowType), сам может возвращать тип своего View и самостоятельно Bind'ить ViewHolder. Для этого добавляем в интерфейс RowType две фунции:

{% gist f23498cb4c30197fe719deb7b71488cf %}

Ниже пример реализации этих функций для класса TextRowType. Обратите внимание, что теперь нет необходимости в геттерах. 
<br>
{% gist 28bc3f08f1f897a3328d02858334c05b %}

Полностью классы после рефакторинга см. github <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo/tree/master/app/src/main/java/io/github/ziginsider/multiplerowtypesinrecyclerviewdemo/Data">тут</a>

<br>
Аналогично реализуем методы для остальных классов. В итоге получаем такой адаптер:
{% gist 96af4bce9c802d12efc66ac238843e53 %}
<br>
Кода в адаптере в три раза меньше. Код понятнее. Масштабировать/изменять проект гораздо легче. 

А что еще надо?

<br>
### Bonus
Допольнительно поговорим о более тонкой настройке RecyclerView. 

RecyclerView с разными типами Item View, для того, чтобы избежать притормаживания при прокрутке, можно настроть чуть эффективнее.

Только сразу оговорим откуда может взяться притормаживание: в тех случаях когда в пуле RecyclerView (куда уходят ViewHolder после попадания за экран для последующего переиспользования) банально не будет места. Это может случится, например, при crossfade анимации всего списка элементов.

Дело в том, что по-умолчанию количество объектов конкретного View попадающих в пул RecyclerView равно 5. Причем все типы View у RecyclerView используют один пул объектов. Таким образом, зная что одни типы View появляются в нашем списке чаще, а другие реже, мы можем увеличить максимальное количество первых в пуле и уменьшить максимальное количество вторых. Как это сделать?

{% gist f3ebf2ede8a8c12bc65ddecebdce348a %}

Это важно знать. Т.к. допустим, элемент списка конкретного View, который как мы знаем на экране всегда представлен в одном экземпляре, может забивать пул объектов RecyclerView до пяти и, таким образом, четыре из этих ViewHolder будут напрасно хранится в пуле, занимая место, которое могли бы занимать элементы с типом View, которого на экране может быть больше.

Теперь все.

Проект на github: <a href="https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo">https://github.com/ziginsider/MultipleRowTypesInRecyclerViewDemo</a>



