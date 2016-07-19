---
layout: post
title: Xamarin.Forms. Ускорение отображения окна (Activity)
date: 2016-06-26 01:33
tags:
- Xamarin
- Xamarin.Forms
- Android
- C#
---

Для Xamarin.Forms версии 1.х характерна одна вещь: XAML-файлы интерпретируются на лету, включая создание всех необходимых контролов и их размещение на экране. Из-за этого каждое открытие нового окна со сложной компоновкой происходит дольше, чем хотелось бы.

В версии 2.0 этот недостаток устранили, реализовав предварительную компиляцию XAML. Использовать ее можно как для отдельных страниц и View на XAML, так и для всего проекта целиком.

Включаем компиляцию отдельной XAML-страницы (файл `MainPage.xaml.cs`, например)

{% highlight csharp linenos %}
using Xamarin.Forms.Xaml;
...
[XamlCompilation (XamlCompilationOptions.Compile)]
public class MainPage : ContentPage
{ 
...
}
{% endhighlight %}

Активируем компиляцию по всему проекту — добавляем новую строку в конец файла `Properties/AssemblyInfo.cs` в PCL-проекте: 

{% highlight csharp %}
...
[assembly: XamlCompilation(XamlCompilationOptions.Compile)
{% highlight %}

Оригинал: <https://habrahabr.ru/company/microsoft/blog/303630/>
