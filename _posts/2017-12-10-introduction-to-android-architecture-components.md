---
layout: post
title: Введение в Android Architecture Components
date: 2017-12-10 13:07
tags:
- Java
- Android
- Architecture Components
- Translate
---
<img src="{{ site.baseurl }}/images/introduction-arch/hat_37.png">

:books: *Вольный перевод статьи Nazmul Idris (Naz) <a href="https://proandroiddev.com/introduction-to-android-architecture-components-cab33baa65f6">"Introduction to Android Architecture Components"</a>.*

<br>
### Верните магию в Android-разработку 
В ноябре 2017 года Android Architecture Components были представлены в стабильной версии 1.0. Это большое дело т.к. долгое время постоянно возникали вопросы по поводу архитектуры Android-приложений.

Это такие вопросы: как сохранить данные при повороте экрана, обмен данными между Fragment и Activity, зависимость от жизненного цикла, etc.

Пока эти сложности не были преодолены они огорчали Android-разработчика и лишали его ощущения магии. 😠

Architecture Components вернули магию обратно в Android-разработку! 🎩

<br>
### Что это?

Существует довольно много паттернов для архитектуры приложений, таких как MVP, MVVM, и однонаправленные (NB от переводчика: это какие?). Я большой фанат однонаправленных, мне нравится MVVM. У MVVM есть три части - Model, View и ViewModel. Давайте рассмотрим, что представляет каждая из них:

1. View - Это компонент UI, слой, который отвечает за отображение на экране и взаимодействие с пользователем.
2. ViewModel - View подписывается на ViewModel, которая содержит данные, необходимые для View. Поэтому, когда данные меняются, подписчикам (View) отпраляются сообщения, что данные изменились.
    - ViewModel отвечает за подготовку данных для потребления View
    - Cостояние ViewModel стабильно на протяжении жизненных циклов Activity и Fragment. Так, что когда Activity перестраивается (при измененении ориентации экрана) она использует ту же ViewModel. И вы можете охватить жизненный цикл этих ViewModel в жизненном цикле Activity, и когда Activity неактивна (не уничтожена), тогда ViewModel может быть очищена.
   - LiveData это интересная часть ViewModel, в которую вы можете обернуть быстро изменяющиеся данные и об этих изменениях будут уведомлены UI-компоненты.
   - ViewModel не должна хранить ссылки ни на какие View. И если для View необходим ApplicationContext, тогда вы можете использовать AndroidViewModel который предоставит его.
   - Вы не создаете ViewModel напрямую, вместо этого вы просите систему создать ViewModel, используя код написанный вами. И система заканчивает создание ViewModel и управляет тем, что с ней связано. В основном вы должны использовать фабричный паттерн проектирования, чтобы получить ссылку на ViewModel, а не создать его через конструктор. 
3. Model - здесь хранятся ваши базовые данные. Model может обращаться к вашим локальным хранилищам данных, и синхронизироваться с удаленными источниками данных. Вы можете истпользовать Room для упрощения работы с SQLite. Или вы можете использовать Firebase для хранения данных, что позволяет синхронизировать данные сразу на нескольких платформах. У вас есть большой выбор и, как следствие, гибкость архитектуры. Вы даже можете использовать что-то наподобие Redux в дополнение к Firebase для построения вашей Model.

<img src="{{ site.baseurl }}/images/introduction-arch/arch_37.png">

Эта статья больше касается ViewModel и LiveData концепций Architecture Components. О жизненных циклах и Model я расскажу в других статьях.

<br>
### Пример
Я создал простое приложение, демонстрирующее как вы можете использовать ViewModel и LiveData в своих приложениях. Вы можете посмотреть этот пример на <a href="https://github.com/nazmulidris/android_arch_comp">GitHub</a>.

В этом примере всего один Java-файл - MainActivity.java. Эта Activity загружает состояние из StateViewModel, которая содержит два вида данных. Вот, сама Activity:

{% gist 33729832c19cfa063a1ee2959cd15f28 %}

**Данные №1** это UUID строка генерируемая при первом создании StateViewModel, и она отображается на UI. Эта строка неизменна на всем протяжении жизненного цикла Activity. Она стабильна при сменах конфигурации. Вы можете менять ориентацию экрана, Activity будет пересоздаваться, и эта строка не изменит своего значения. Но когда вы уничтожите Activity, нажав на back button, или переключитесь на другое приложение, тогда ViewModel будет уничтожена и сработает onCleared(). 

{% gist c9ed2e789e8201e3c11b0b23b43a017e %}

**Данные №2**. ViewModel также создает ScheduledExecutor который запускает простой task каждую секунду. Этот task просто обновляет счетчик и генерирует сообщение в log ("тик" или "так"). Этот Executor также устанавливает значение счетчика в объект CounterLiveData. UI подписан на этот объект, и когда его значение меняется, UI воспроизводит актуальное значение счетчика. Алгоритм стабильно работает и при смене конфигурации. Когда Activity уничтожается, метод onCleared() останавливает Executor. Кроме того, вам следует знать в каком потоке устанавливается значение CounterLiveData:

{% gist 5f1f4b5e03e5583891d174263dad2f8d %}

<br>
### Добавление Architecture Components к вашему проекту
Читайте больше о том как менять ваш файл build.gradle на developer.android.com. Это простой фрагмент файла build.gradle для подключения Lifecycles, ViewModel, и LiveData. 

{% gist 091bd1340ce939f2f93493b168cbc8a7 %}

<br>
### Что потом?
- <a href="https://codelabs.developers.google.com/codelabs/android-lifecycles/#0">Codelab</a> поможет начать знакомство с Android компонетами, осведомленными о жизненном цикле.
- <a href="https://medium.com/@margaretmz/exploring-the-android-architecture-components-117515acfa8">“Model View ViewModel on Android”</a> - статья на medium
- <a href="https://medium.com/google-developers/lifecycle-aware-data-loading-with-android-architecture-components-f95484159de4">“Deep dive into Data Loading with Architecture Components”</a> на medium
- Tutorial по Architecture Components - <a href="https://riggaroo.co.za/android-architecture-components-looking-room-livedata-part-1/">часть 1</a>, <a href="https://riggaroo.co.za/android-architecture-components-looking-viewmodels-part-2/">часть 2</a>

end.

:fist:
