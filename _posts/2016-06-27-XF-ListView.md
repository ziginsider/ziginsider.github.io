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
## Картинки, иконки и производительность ##
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

Вот так можно еще немного улучшить работу FFImageLoading (класс AppDelegate.cs для iOS и MainActivity.cs для Android):

{% highlight csharp %}
var config = new Configuration
            {
                HttpClient = new HttpClient(new ModernHttpClient.NativeMessageHandler()),  //используем быстрые библиотеки для загрузки
                FadeAnimationDuration = 250,  //ускоряем анимацию появления
            };
FFImageLoading.ImageService.Instance.Initialize(config);
{% endhighlight %}

## Работаем со спискам в Xamarin.Forms ##

С помощью FFImageLoading мы оптимизировали отображение изображений в списках и теперь можем перейти к следующему шагу. 

Первая рекомендация касается механизмов работы ListView. В ранних версиях Xamarin.Forms не поддерживался механизм повторного использования созданных ячеек, что приводило к созданию экземпляров ViewCell каждый раз при необходимости их отображения — это и было первой серьезной причиной залипаний при скроле. 

В последних версиях Xamarin.Forms реализован механизм повторного использования созданных ячеек и для его активации необходимо задать свойству CachingStrategy значение ListViewCachingStrategy.RecycleElement.

Реализация в XAML:
{% highlight xml %}
<ListView CachingStrategy="RecycleElement">
	...
</ListView>
{% endhighlight %}

Реализация на C#:
{% highlight csharp %}
var listView = new ListView(ListViewCachingStrategy.RecycleElement);
{% endhighlight %}

После этого созданные экземпляры ViewCell начинают использоваться повторно и к ним просто подключаются (через Binding) необходимые модели данных по мере отображения.

Еще один интересный способ — просто останавливать загрузку и отображение картинок во время прокрутки списка. Этот способ также рекомендуют использовать и создатели FFImageLoading. 

Для этого необходимо сделать свой рендерер для ListView для каждой платформы и переопределить события прокрутки. 

Пример для Android:
{% highlight csharp %}
_listView.ScrollStateChanged += (object sender, ScrollStateChangedEventArgs scrollArgs) => {
  switch (scrollArgs.ScrollState)
  {
  case ScrollState.Fling:
      ImageService.Instance.SetPauseWork(true); // ставим загрузку картинок на паузу 
      break; 
      case ScrollState.Idle: 
      ImageService.Instance.SetPauseWork(false); // возобновляем загрузку картинок 
     // здесь должен быть ваш код отображения изображений в отображаемых ячейках 
      ShowMyImage();      
      break;</p>
   } 
 }; 
{% endhighlight %}

При необходимости вы также можете создать свои реализации ViewCell через механизм [Custom Renderer](https://developer.xamarin.com/guides/xamarin-forms/custom-renderer) для каждой платформы — такой подход может быть актуален для сложных ячеек с большим количеством встроенных контролов. 

Также хорошие результаты при работе с большими объемами данных и сложными ячейками позволяет достичь использование нативных компонентов UICollectionView (для [iOS](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UICollectionView_class/)) и RecyclerView (для [Android](https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html)), но это решение можно рекомендовать продвинутым разработчикам. 

Пример использования данных классов представлен в библиотеке [TwinTechs](https://github.com/twintechs/TwinTechsFormsLib) — обязательно к знакомству, так как там есть видео-ролики с результатами оптимизации.

Итак, на первых порах освоения Xamarin.Forms необходимо уделить особое внимание работе со списками и [подходам к повышению производительности](https://developer.xamarin.com/guides/xamarin-forms/deployment,_testing,_and_metrics/performance/). Это позволит не отвлекаться на данные особенности в последующей разработке.

Оригинал: <https://habrahabr.ru/company/microsoft/blog/303630/>
