---
layout: post
title: Android изнутри. Часть I
date: 2017-12-17 19:03
tags:
- Java
- Android
- Translate
- Android Kernel
---
<img src="{{ site.baseurl }}/images/internals/internals_1.png">

:books: *Вольный перевод статьи Hemant Joshi <a href="https://android.jlelse.eu/android-internals-for-developers-part-i-982a4409f4b5">"Android Internals For Developers : Part I"</a>.*

Что есть Android? Что вы имеете в виду, когда говорите о root-правах на телефоне Android? Нужно ли знать разработчику Android о начинке системы, чтобы быть профессионалом?

В двух статьях мы попытаемся дать ответы на эти вопросы, а также покажем хитросплетения операционной системы Android. На заметку, *эта статья написана с точки зрения разработчика и поэтому она не будет говорить о деталях системы Android, которые не касаются разработки*. Предварительные требования для понимания статьи: базовые знания и знания команд Linux, разработка Android-приложений.

Часть I : Android изнутри для разработчиков

Часть II : Углубляемся в систему Android

Первое, *Что такое Android*?

<img src="{{ site.baseurl }}/images/internals/internals_2.png">

Это картинка объясняет положение дел в Android. Мы видим, что внутри талисмана Android пингвин, т.е. талисман Linux. Это потому что Android базируется на ядре Linux. Большинство разработчиков знает об этом, но если вы узнали об этом только сейчас - теперь вы можете при случае блеснуть знаниями!!!

Отвечаем на вопрос: *Android - это мобильная операционная система, которая основана на ядре Linux*. Поскольку она основана на Linux, большинство операций, о которых мы расскажем, относятся к спецификации POSIX, с которыми вы могли сталкиваться, работая с Mac / Linux. Тогда у вас должен возникнуть вопрос: если Android основан на Linux, зачем мне читать этот пост? Это потому, что ядро Android это не то же самое, что и ядро Linux. Ядро было изменено разработчиками, чтобы сделать мобильную ОС, а не настольную.

Зачем было модифицировать ядро? Это потому что на настольной ОС вы можете легко убивать процессы, или использовать виртуальную память, и делать множество других вещей. Но производительность мобильной системы ограничена. Без правильного управления памятью, мобильные системы будут тормозить, и вы несможете, например, получать звонки или напоминания.

<br>
### Ядро Android

<img src="{{ site.baseurl }}/images/internals/internals_3.png">

Последняя верси Android 8.0 Oreo основывается на ядре Linux 4.4. Но я хотел бы еще раз подчеркнуть, что Android это не Linux-дистрибутив. В этом разделе мы поговорим о некоторых изменениях, которые внеc Google в ядро Linux.

1. <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">OOM Killer</span>
 (Нехватка памяти) : это не новая функция введенная Google. Нехватка памяти это довольно часто возникающее нежелательное состояние системы, когда запрашиваемая дополнительная память не может быть выделена программой или системой. Обработка нехватки памяти было изменено Google, чтобы подходить для мобильных ОС. Давайте посмотрим на внутренности:
- У Android есть множество фоновых процессов. Каждый раз, когда вы нажимаете "home button", приложение помещается в фоновый процесс. И как же тогда убиваются процессы, когда система близка к нехватке памяти? Adroid придал категорию важности каждому процессу, т.е. видимый (visible), скрытый (hidden). Каждый процесс получает <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj</span> в соответствии с его важностью.
- Обновление <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj</span> выполняется диспетчером активности (Activity Manager) автоматически. "Убийца процессов" (low memory killer) при нехватке памяти убивает процессы в соответствии с <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj</span>. *Процесс с более высоким* <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj</span> *скорее всего будет убит*. "Убийца процессов" конфигурируется несколькими пороговыми парами: (<span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">&lt;t1, oom_adj1&gt;</span>, <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">&lt;t2, oom_adj2&gt;</span>). Эти параметры означают что "убийца процессов" может начать убивать процессы с <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj</span> больше чем <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">oom_adj1</span>, когда памяти останется меньше, чем <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">t1</span>. 

<img src="{{ site.baseurl }}/images/internals/internals_4.gif">

Вопрос в том, зачем нам все это знать? Ответ: потому что тогда мы будет знать кто живет, а кто умирает в Android.

- **Процессы переднего плана** - наверняка вы подумали, что то, с чем взаимодействует пользователь - это самые главные процессы. И вы полностью правы. Любой процесс, который выполняет службу переднего плана, также получает приоритет переднего плана. Вот почему использование процессов переднего плана нелбходимо, если я нажимаю home button и не хочу, чтобы проигрывание музыки остановилось. Случаи подобные этому, хороший пример для для сервисов переднего плана. 

*Замечание*: Функционировании сервисов переднего плана, подрузамевает создание нотификаций, для того, чтобы пользователь знал, что ваш сервис запущен. Если для вашего случая нотфикации не нужны, возможно, сервис не должен быть сервисом переднего плана.

- **Видимые процессы** - Я не шучу! Это не то же самое, что и процессы переднего плана. Ваша Activity может быть видна и при этом не быть на переднем плане. Примером может быть диалоговое окно, которое появляется над Activity, или может быть полупрозрачным. 

Дальше цитата, которую я нахожу лучшей по поводу видимости: "Имейте это в виду, то что процесс видим, совсем не означает, что его нельзя убить". Если нет достаточно места для переднего плана, все же есть вероятность, что ваш видимый процесс будет убит. С точки зрения пользователя это означает, что видимая Activity, которая находится позади текущей  Activity иожет быть заменена на черный экран. Конечно, если вы правильно воссоздаете Activity, она будет восстановлена без потери данных сразу после закрытия Activity переднего плана.

- **Сервисы** - Если ваш процесс не попал ни в один из вышеперечисленных процессов, это значит что вы используете сервис. Это то место, где во многих приложениях выполняются фоновые задачи. Это не плохое место! В подовляющем большинстве случаев это хорошее место для фоновых процессов, т.к. оно гарантирует, что ваш фоновый процесс не будет убит, если только не слишком много происходит в вышеперечисленных проццессах. *Обратите внимание на константы используемые* в <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">onStartCommand()</span>, *они котроллируют что произойдет с вашим процессом, если он будет убит из-за нехватки памяти или действием другого процесса*.

- **Фоновые процессы** - предположим, что ваша Activity была Activity переднего плана, но пользователь нажал home button и вызвал <a href="https://developer.android.com/reference/android/app/Activity.html?utm_campaign=adp_series_processes_012016&utm_source=medium&utm_medium=blog#onStop%28%29">onStop()</a>. Тогда ваш процесс Activity попадет в категорию фоновых процессов. 

Помните, что Android не убивает просто фоновые процессы, он убивает их в том случае, если есть потребность в памяти. Это роль <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">OOM Killer</span>, о котором мы говорили выше, однако вы всегда можете <a href="https://developer.android.com/training/basics/activity-lifecycle/recreating.html?utm_campaign=adp_series_processes_012016&utm_source=medium&utm_medium=blog">восстановить ваши Activity</a>, как и в случае видимых процессов, о которых мы говорили выше.

<br>
### Wakelocks
Это вторая большая можификация ядра Linux в Android. **Wakelocks** - это программные механизмы управления питанием, которые гарантируют, что ваше устройство не погрузится в глубокий сон.

<img src="{{ site.baseurl }}/images/internals/internals_5.png">

*Хотя wakelocks на Android - это не обязательно плохая вещь, их минимизация должна быть приоритетом кажого Android- полтзователя, который стремится увеличить время автономной работы устройства.*

К сожалению, некоторые плохо написанные программы могут создать немалое количесво нежелательных wakelocks. Некоторые приложения требуют постоянного доступа в интернет для нормальной работы - Facebook и Messener, вероятно, являются самыми популярными представителями. Они настойчиво запрашивают информацию из интернета, эти запросы вызывают wakelocks, которые  разряжают аккумулятор, когда вы держите устройство в рабочем состоянии и когда вы нажимаете кнопку кнопку блокировки экрана, чтобы его выключить. 

<br>
### Вывод. Часть I
Ура!!! Это было и так слишком много! Потратьте время и прочитайте снова, если это имеет смысл.

Что же в следующей части? 

В следующей части мы узнаем о таких важных компонентах Android как <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">init</span> и <span style="background-color: #f4f4f4; color: #333; font-family: Consolas, monaco, monospace; font-size: 14px;  font-style: normal; max-width: 800px; word-break: break-all; white-space: normal; padding: 3px; border-radius: 3px;">zygote</span>. Также в следующей части вы узнаете о том, что же значит получить root-доступ к телефону.

end.

:clap:
