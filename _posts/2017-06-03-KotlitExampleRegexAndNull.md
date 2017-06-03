---
layout: post
title: Два примера на Kotlin
date: 2017-06-03 14:19
tags:
- Kotlin
- example
- моё
---
*Просто чтобы не забыть. Первый пример показывает работу с регулярными выражениями, второй - с null и получением элементов массива через лямбда-выражение*
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
