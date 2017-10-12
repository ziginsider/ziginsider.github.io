---
layout: post
title: Несколько примеров на Kotlin
date: 2017-06-03 14:19
tags:
- Android
- Kotlin
- примеры
- моё
---
*Просто чтобы не забыть. Первый пример показывает работу с регулярными выражениями, второй - с null и получением элементов массива через лямбда-выражение.*
<br>
{% highlight kotlin %}
fun main(args: Array<String>) {
    
    //regex
    val month = "(JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)"
	fun getPattern(): String = """\d{2}\h$month\h\d{4}"""
    val regex = Regex(getPattern())
    val str ="12 DEC 1996"
    val flag = regex.containsMatchIn(str)
    if (flag)
    	println("{$str} is true!")
    else
    	println("{$str} is wrong!")
    
    //null
    val listWithNulls: List<String?> = listOf("A", null, "B", "ERROR 404", null)
	for (item in listWithNulls) {
     	item?.let  {println(it)}  ?: println("element is empty") 
	}
}
{% endhighlight %}

*Работа с object expressions (аналог анонимных внутренних классов в Java, позволяет переопределять классы, расширять функциональность, реализовывать интерфейсы). Так же в примере показывается переопределение интерфейса Comparator, для реализации сортировки массива целых чисел в обратном порядке.* 
<br>
{% highlight kotlin %}
import java.util.*

fun getList(): List<Int> {
    val arrayList = arrayListOf(1, 5, 2)
    Collections.sort(arrayList, object : Comparator<Int> {
        override fun compare(a: Int, b: Int) = b - a
    })
    return arrayList
}
{% endhighlight %}

*Предыдущий пример, но с использование лямбда-выражения*
{% highlight kotlin %}
import java.util.*

fun getList(): List<Int> {
    val arrayList = arrayListOf(1, 5, 2)
    Collections.sort(arrayList, { x, y -> y - x })
    return arrayList
}
{% endhighlight %}

*Наконец, тот же пример но с использованием библиотечной функции из Kotlin*
{% highlight kotlin %}
fun getList(): List<Int> {
    return arrayListOf(1, 5, 2).sortedDescending()
}
{% endhighlight %}
<br>
<br>
<br>
Кстати, вот схемка как "подправлены" коллекции в Kotlin. Подробнее <a href="https://blog.jetbrains.com/kotlin/2012/09/kotlin-m3-is-out/#Collections" title="Kotlin collections">read-only and mutable views on Java collections</a>
<br>
<img src="{{ site.baseurl }}/images/Collections.png">
<br> 



