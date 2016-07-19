---
layout: post
title: Xamarin.Forms. Оптимизация ListView.
date: 2016-06-26 23:14
tags:
- Xamarin
- Xamarin.Forms
- C#
- Android
- ListView
---
Первое, с чем сталкиваются начинающие разработчики на Xamarin.Forms — залипания при прокрутке в списках на базе ListView. Чего греха таить, это одно из болезненных мест платформы, отбрасывающее тень на весь остальной функционал, так как списки используются в больших количествах и практически во всех приложениях. 

Для начала мы рассмотрим работу с изображениями, так как очень часто это является одной из причин залипаний.

Стандартный компонент для отображения Image хорош, даже поддерживает кеширование, но он мало пригоден при использовании в реальных проектах. Когда год назад мы уперлись в ограничения Image, пришлось сделать свой простенький кешер изображений с автоматическим масштабированием — для отображения в ячейку передавалась уменьшенная версия, так как с большими изображениями списки просто умирали (это не проблема Xamarin.Forms, а вообще любой разработки приложений, но на Xamarin.Forms она была очень острой). 

Потом мы перепробовали несколько различных библиотек и в конце концов остановились на превосходном компоненте под названием [FFImageLoading](https://github.com/luberda-molinet/FFImageLoading).

![FFImageLoading]({{ site.baseurl }}/images/x1.png)

Он доступен в Nuget () и позволяет решить сразу несколько задач:
+ фоновая загрузку изображений с возможностью повтора запросов;
+ использование placeholder во время загрузки;
+ автоматическое масштабирование изображений до размеров контрола, включая удаление Alpha-канала на Android для еще большей производительности;
+ возможность применения трансформаций к изображениям после загрузки (обрезать до круга или другой формы, наложить blur или другой спец. эффект);
+ fade-анимация появления изображения после загрузки.

Вот так использовать компонент при разработке на XAML:

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
  xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
  x:Class="Sample.Pages.MainPage"
  xmlns:ffimageloading="clr-namespace:FFImageLoading.Forms;assembly=FFImageLoading.Forms"
  Title="FFImageLoading Demo">
    <ContentPage.Content>
        <ffimageloading:CachedImage HorizontalOptions="Center" VerticalOptions="Center"
            WidthRequest="300" HeightRequest="300"
            DownsampleToViewSize="true"
            Source = "https://unsplash.it/600/600/?random"
		LoadingPlaceholder = "placeholder.png">
        </ffimageloading:CachedImage>
   </ContentPage.Content>
</ContentPage>
{% endhighlight %}

Вот так можно еще немного улучшить работу FFImageLoading (класс `AppDelegate.cs` для iOS и `MainActivity.cs` для Android):

{% highlight csharp %}
var config = new Configuration
            {
                HttpClient = new HttpClient(new ModernHttpClient.NativeMessageHandler()),  //используем быстрые библиотеки для загрузки
                FadeAnimationDuration = 250,  //ускоряем анимацию появления
            };
FFImageLoading.ImageService.Instance.Initialize(config);
{% endhighlight %}
