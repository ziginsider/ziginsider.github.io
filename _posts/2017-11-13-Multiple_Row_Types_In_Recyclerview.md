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
*Заметка основана на статье Mateusz Dziubek  <a href="https://android.jlelse.eu/multiple-row-types-in-recyclerview-2febf66e96a4">"Multiple row types in RecyclerView"</a>*

### Введение

Итак, представим ситуацию, когда нам надо в один RecyclerView поместить несколько различных типов View. Допустим, это:

- кнопка
- картинка с текстом
- заголовок с текстом

На смартфоне мы должны получить что-то вроде этого:

<img src="{{ site.baseurl }}/images/testing1.jpeg">

Вдохновляясь статьей <a href="https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism">Replace Conditional with Polymorphism</a>, попробуем сделать это. Основная идея - каждому типу View соответсвует отдельный класс, и эти классы объединяются общим интерфейсом.

### layout

Создаем, три layout, соответствующих трем типам View.

`row_type_button.xml`
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="GO!" />
</LinearLayout>
{% endhighlight %}

`row_type_image.xml`
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ImageView
        android:id="@+id/image"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@drawable/apple" />

    <TextView
        android:id="@+id/text_image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="text" />
</LinearLayout>
{% endhighlight %}

`row_type_text.xml`
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/header"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="I'm a header!"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="I'm a text!" />
</LinearLayout>
{% endhighlight %}

В 'activity_main.xml' добавляем RecyclerView:
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="io.github.ziginsider.multiplerowtypesinrecyclerviewdemo.MainActivity">

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</android.support.constraint.ConstraintLayout>
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

