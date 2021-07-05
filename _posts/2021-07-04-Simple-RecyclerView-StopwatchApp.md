---
layout: post
title: Simple RecyclerView demo App - Stopwatch
date: 2021-07-04 21:30
tags:
- Android
- Kotlin
- RecyclerView
---

## Задание

Напишем простое приложение с RecyclerView. Элементом списка сделаем секундомер с возможностью запускать, останавливать и сбрасывать таймер.

Всегда начинаем с продумывания, что у нас должно получиться. Допустим, мы хотим что-то такое:

<img src="{{ site.baseurl }}/images/rs/img1.gif" width="400">

## init-00

Первым делом создаём проект в Android Studio c одной empty Activity, и убираем всё лишнее. Скажем, в данном проекте мы не используем тесты или proguard - поэтому убираем зависимости, папки, файлы - все, что нам не понадобится. Версии зависимостей должны быть актуальными - обновляем на стабильные последние версии.

Мы будем использовать <a href="https://developer.android.com/topic/libraries/view-binding">View Binding</a>. Добавляем в проект, чуть переписываем MainActivity:

{% gist 360c4d84aa8f5275c7e3fe9adbb77a47 %}

Проверяем, что всё компилиться: <a href="https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/init-00">https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/init-00</a>

Мы готовы двигаться дальше.

## layouts-01

Итак, у нас есть один экран, один RecyclerView, UI элемента RecyclerView известен. Начнем с разметки layout'ов приложения и будем от этого отталкиваться. 

В activity_main.xml один RecyclerView и кнопка для создания таймера. Элемент RecyclerView таймер, который содержит:
1. мигающий индикатор
2. текстовое представление таймера 
3. кнопка "Start/Pause"
4. кнопка "Restart"
5. кнопка "Delete"

Для кнопок будем использовать подходящие иконки. Добавим в проект векторные файлы "ic_baseline_delete_24.xml", "ic_baseline_pause_24.xml", "ic_baseline_play_arrow_24.xml" и "ic_baseline_refresh_24.xml" - см. в репозитории: <a href="https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/layouts-01/app/src/main/res/drawable">https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/layouts-01/app/src/main/res/drawable</a>

Для индикатора создадим animation-list:

{% gist 50d35277cd23a2917fa52b5129567193 %}

Тут я думаю всё понятно, 700 ms показываем кружок, 700 ms не показываем - создается впечатление мигания. Ниже мы увидим, как запускать такую анимацию.

Таким образом layout для элемента списка:

{% gist 71e3f3fa6165d4ffd9edb586ded6b088 %}

activity_main.xml:

{% gist edb5dbc0c84d0ebed6ec394b0e9a7e14 %}

Обратите внимание, для RecyclerView в разметке мы испоьзовали такую хитрую штуку `tools:listitem` - которая позволяет сразу увидеть, как будет выглядеть Recycler c айтемами.

Когда закончили с разметкой, можно двигаться дальше. Если что-то в дальнейшем в UI нам не понравится - всегда сможем поправить.

## recycler-02

Далее набросаем логику RecyclerView. Пока просто: нажимаем на кнопку "Add Timer" - элемент добавляется в список.

Для этого сперва подумаем, что у нас будет элементом списка RecyclerView. Создадим модель айтема:

{% gist 85b77ef1414186d5c4d08156eec40b72 %}

1. `id` - чтобы отличать айтемы друг от друга
2. `currentMs` - количество миллисекунд прошедших со старта
3. `isStarted` - работает ли секундомер или остановлен

Теперь в `MainActivity` добавляем `private val stopwatches = mutableListOf<Stopwatch>()` - в этом списке будут хранится стейты секундомеров

Создаем класс адаптера для RecyclerView. Будем использовать <a href="https://developer.android.com/reference/androidx/recyclerview/widget/ListAdapter">ListAdapter</a>. Это адаптер для Recycler "на стероидах", он является частью фреймворка RecyclerView, по-умолчанию использует DiffUtil с асинхронными потоками - короче штука удобная и в простых случаях его стоит использовать. Для RecyclerView нам понадобится ViewHolder, поэтому сперва создаем этот класс:

{% gist b5403c038446dbfb52df82efed27b22d %}

пройдемся по коду:
1. `private val binding: StopwatchItemBinding` - передаем во ViewHolder сгенерированный класс байдинга для разметки элемента RecyclerView. В родительский ViewHolder передаем `bindig.root` т.е. ссылку на View данного элемента RecyclerView
2. `fun bind(stopwatch: Stopwatch) {` - в метод `bind` передаем экземпляр Stopwatch, он приходит к нам из метода `onBindViewHolder` адаптера и содержит актуальные параметры для данного элемента списка.
3. `binding.stopwatchStopwatch.text = stopwatch.currentMs.displayTime()` - пока просто выводим время секундомера.
4. `displayTime()` - данный метод расширения для Long конвертирует текущее значение таймера в миллисекундах в формат "HH:MM:SS:MsMs" и возвращает соответствующую строку

Теперь можно приступить к созданию класса адаптера:

{% gist 4d320ea659d18213909743e3fab9ef93 %}

1. В `onCreateViewHolder` инфлейтим View и возвращаем созданный ViewHolder
2. `holder.bind(getItem(position))` - тут понятно - для конкретного ViewHolder обновляем параметры. `onBindViewHolder` вызывается в момент создания айтема, в моменты пересоздания (например, айтем вышел за пределы экрана, затем вернулся) и в моменты обновления айтемов (этим у нас занимается DiffUtil)
3. Имплементация DiffUtil помогает понять RecyclerView какой айтем изменился (был удален, добавлен) и контент какого айтема изменился - чтобы правильно проиграть анимацию и показать результат пользователю. В `areContentsTheSame` лучше проверять на равество только те параметры модели, которые влияют на её визуальное представление на экране.

 B MainActivity пока просто генерим айтем, при нажатии на "Add stopwatch", добавляем его в список и список сабмитим в RecyclerView. По сути это и есть основной алгоритм работы с Recycler:
 1. Работаем с айтемом
 2. Обновляем список
 3. Список сабмитим в адаптер RecyclerView
 
 {% gist fd206bb80001cef6b07480bdf309346b %}

Проверям, что все компилется и работает как надо <a href="https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/recycler-02">https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/recycler-02</a>


## timer-03

Теперь займемся логикой. Сначала просто запустим наш секундомер, а на следующей стадии заставим кнопки выполнять свою функцию. Итак, мы создаем элемент списка RecyclerView и секундомер должен начать работать.

В Android можно по-разному решить эту задачу: например, использовать Handler(), чтобы создать свой таймер, или что-нибудь с потоками создать или с корутинами или стороннюю либу можем подключить... Но в учебных целях мы пойдем по простому пути - будем использовать класс Android <a href="https://developer.android.com/reference/android/os/CountDownTimer">CountDownTimer</a>

Класс имеет интуитивно понятное API - мы задаем продолжительность работы  `millisInFuture` и величну интервала `countDownInterval` - через данное время будет вызываться коллбэк `onTick()` - пока это всё что нужно понимать. 

Изменяем код ViewHolder'a:

{% gist 3fccd7d80bd69dcba5846c50944386f6 %}

Код простой. Обратите внимание, что в методе `startTimer` обязательно нужно кэнсельнуть таймер перед созданием нового. Это необзодимо по той причине, что RecyclerView переиспользует ViewHolder'ы и один таймер может наложится на другой. Будут трабблы с шагом интервала.

В целях тестирования в MainActivity, в момент создания экземпляра Stopwatch выставляйте значение `isStarted` как `true`. Теперь можно стартануть проект и посмотреть, что получилось:

<a href="https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/timer-03">https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/timer-03</a>

Ура! Что-то работает:

<img src="{{ site.baseurl }}/images/rs/img2.gif" width="400">

Возможно, вы заметили некоторые проблемы с подобной организацией работы таймера прямо внутри ViewHolder. Если нет, то мы еще об этом скажем в конце статьи.


## buttons-04

Займемся кнопками. Мы можем стратовать, останавливать, сбрасывать и удалять таймер. Создаём соответствующий интерфейс, имплементируем который в MainActivity (поскольку именно в этом классе у нас логика управления списком таймеров), и передадим эту имплементацию в качестве параметра в адаптер RecyclerView:

{% gist ab387f5ae5d82e5a24091e076349d1b7 %}

В MainActivity имплементируем:

{% gist 3d3ea0c0fff65a07546250fec370ab4b %}

Заметьте, что когда мы модифицируем айтем, мы пересоздаём список. Это не очень эффективно. Попробуйте переписать код так, чтобы искомый айтем менялся в списке `stopwatches` и сабмитайте список в адаптер.

В ViewHolder:

{% gist 5a299aac0caa2674313eccad32005c3e %}

Заметьте, что мы добавили старт (и остановку) анимации для индикатора. По остальному должно быть понятно - мы меняем состояние айтема через listener.

Такой подход, когда ViewHolder обрабатывает только визуальное представление айтема, который пришел ему в методе `bind`, и ничего не меняет напрямую, а все колбэки обрабатываются снаружи (в нашем случае через listener) - является предпочтительным. Тут мы можем указать на проблему данного приложения. Если создать достаточное количество таймеров, и после скролла, запущенный таймер окажется за экраном, то таймер может остановится, и продолжит работу, только когда опять окажется видимым. Это происходит потому, что ViewHolder переиспользуется. Поэтому нужно быть аккуратным когда меняешь состоние айтема внутри ViewHolder'a - как в нашем случае с использованием CountDownTimer.

P.S. В адаптере, в имплементации DiffUtil мы добавили метод getChangePayload. В данном случае это утовка, чтобы айтем не бликовал (проигрывается анимация для всего айтема), когда мы нажимаем на кнопки. Нормальная реализация payload выходит за рамки этого простого примера. 

`override fun getChangePayload(oldItem: Stopwatch, newItem: Stopwatch) = Any()`

<br>

Результат:
<a href="https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/buttons-04">https://github.com/ziginsider/Simple-RecyclerView-Android-Demo-app-Stopwatch/tree/buttons-04</a>

</br>






 
