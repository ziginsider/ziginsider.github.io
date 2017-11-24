---
layout: post
title: У меня было 10 Android собеседований за последние два года... (перевод)
date: 2017-11-22 11:16
tags:
- Android
- Java
- Interview
---
<img src="{{ site.baseurl }}/images/android_interview.jpg">
<br>
*Перевод статьи Mohamed Ibrahim <a href="https://medium.com/@MohamedIsoliman/i-had-10-android-interviews-during-the-last-two-years-heres-the-questions-plus-some-lessons-i-ve-cdc583dfbc65">I had 10 Android interviews during the last two years, here’s the questions plus some lessons I’ve learned</a>*.

## У меня было 10 Android собеседований за последние два года. Вот вопросы, которые мне задавали, и уроки которые я извлек.

Прошло два года с тех пор, как я стал заниматься разработкой на Android. Я был поражен количеством ресурсов для изучения Android, и тем, как сообщество разработчиков делится знаниями и объединяется, чтобы сделать разработку более увлекательной, и тем как постепенно растут требования разработчиков к тестированию кода, его поддержке и удобочитаемости.

На протяжении этих двух лет у меня было около десяти собеседований. Одни из них проходили гладко, другие - не очень, но каждое из них показывало мои пробелы в знаниях. Обычно, цель соискателя на собеседовании - получить работу, но кроме того это может быть хороший инструмент, чтобы понять свой уровень в аспектах языка, средств программирования и бизнес-циклах разработки. 

У меня не было опыта в компьютерных науках, поэтому я решил черпать знания из чтения, прохождения различных руководств, включая, разумеется, материалы на Udacity. Я даже начал проходидь курс на MAL под названием "Основы Android", и с этого момента началась моя история разработки под Android.

Давайте сначала я расскажу о стилях собеседований в разных компаниях, куда я попадал (названия компаний я обозначил инициалами), а затем перейдем к вопросам, которые мне запомнились.

<br>
### Стиль собеседования
EP: Мэйнстрим Android разработки и вопросы по Java. - Задачи: экран входа в систему с email и паролем, зарегистрированный пользователь должен автоматически входить в систему, при повторном использовании приложения.

IC: Собеседование в свободной, дружественной форме. Разговор о средствах разработки, технологиях и качестве кода. - Задачи: нет.

SD: Тестирования гибкости кандидата (например, способность переключатся между нативной и гибридной разработкой). - Задачи: сделать игру, в которой предметы только определенного рода собираются в ведро.

AT: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

AR: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

SW: Мэйнстрим Android разработки и вопросы по Java. - Задачи: нет.

RA: Чем больше вы верно отвечаете, тем сложнее вопросы. - Задачи: приложение для фото, в котором изображения хранят метку о погоде.

VN: Чем больше вы верно отвечаете, тем сложнее вопросы. Общение в дружественной форме - Задачи: нет.

IB: Упор на Java. Вопросы становятся сложнее. - Задачи: приложение, которое показывает список авиакомпаний с сервера api.

WM: Java и Android и тестирование гибкости. - Задачи: нет.

Это все. Надеюсь я ничего не забыл. Однако, почему я дал список собеседований в таком виде? Потому что компании разные, некоторым из них нужен Android разработчик чтобы сделать конкретную работу, и сделать ее идеально - это, обычно, большие компании.

Другим может потребоваться разработчик, открытый для новых знаний, который быстро обучается, может работать с разными технологиями (бэкенд, системное администрирование и т.д.) - это могут быть небольшие компании или стартапы. И у каждой компании своя перспектива на вас. Поэтому вам не стоит опираться только на технические детали. Узнайте больше о компании, гляньте ее продукты, перед тем как идти на собеседование. Подготовьте свои вопросы для них, потому что это не одностороннее интервью и никогда не должно быть таким.

Сейчас я приведу список вопросов. Но не стоит просто запоминать ответы на них. Это плохой путь. Необходимо самому прийти к пониманию каждого вопроса. Попробуйте почитать stackoverflow по каждой теме, читайте комменты также, я нахожу этот портал лучшим, для объяснения технических вопросов, потому что каждый из отвечающих хочет сделать это лучше.

Старайтесь создавать небольшие приложения, чтобы понять, как работает та или иная штука. Примеры Google - хороший способ для изучения разных областей Android разработки.

*NB (от переводчика): хорошая статья о темной стороне собеседований https://danluu.com/programmer-moneyball/*

<br>
### Вопросы на собеседованиях (не упорядочены по сложности)
<details>
 <summary>1. Какие последние версии Android? Наиболее важные новые фичи в Marshmallow?</summary>
 <p>
  Версии:
  <br><br>
  4.0.3. Ice Cream Sandwich
  <br><br>
  4.1. Jelly Bean
  <br><br>
  4.4. KitKat
  <br><br>
  5.0. Lollipop
  <br><br>
  6.0. Marshallow
  <br><br>
  7.0. Nougat
  <br><br>
  8.0. Oreo
  <br><br>
  Marshallow:
  1. https://ru.wikipedia.org/wiki/Android_Marshmallow
  2. https://4pda.ru/2015/10/05/249631/</p>
</details>

<br>
<details>
 <summary>2. Какая цель у Activity?</summary>
 <p>ссс</p>
</details>

<br>
<details>
 <summary>3. Какая цель у Fragment'ов?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>4. Расскажите о жизненном цикле Activity?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>5. Расскажите о жизненном цикле Fragment?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>6. Вы используете приложение для путешествий, затем нажимаете кнопку настроек, открывается Activity настроек, затем вы кликаете "назад" - что происходит с жизненным циклом Activity настроек и с циклом главного Activity при этом?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>7. Что вы знаете о Material design?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>8. Какая разница между абстрактным классом и интерфейсом в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>8. Какая разница между абстрактным классом и интерфейсом в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>10. Что такое абстрактный класс в Java? </summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>11. Почему нельзя создать экземпляр абстрактного класса?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>12. Какая разница между Dialog и AlertDialog в Android?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>13. Какая разница между LinearLayout и RelativeLayout?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>14. Где выше производительность, у LinearLayout или RelativeLayout?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>15. Возьмем макет контакта с картинкой, именем и номером, как вы реализуете его в XML?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>16. Что такое Service, с какими потоками он работает?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>17. Какая разница между Service и IntentService?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>18. Что такое ANR message? :scream_cat:</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>19. Объясните работу BroadcastReciever и его реализацию.</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>20. Можете ли вы использовать фрагмент без UI? В каких случаях вы бы использовали этот паттерн?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>21. Расскажите о модификаторах доступа в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>22. Какая разница между Default и Protected модификаторами в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>23. Что вы знаете об AsyncTask?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>24. В чем разница между Parcelable и Serializable? Что лучше? Почему?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>25. Как получить доступ к переменной в Activity из Fragment'а?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>26. У вас есть Activity с двумя Fragment'ами, у одного есть кнопка, у другого - TextView, кликая на кнопку, меняется TextView. Как вы реализуете это?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>27. Как сделать переменную потоко-безопасной?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>28. Какие стратегии мы можем использовать, чтобы достигнуть потоко-безопасности?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>29. В чем цель ключевого слова "static" в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>30. Как можно инициализировать static-переменную в Java?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>31. Какие паттерны проектирования вы знаете?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>32. Объясните принцип паттерна проектирования "Строитель"?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>33. Где вы использовали паттерн "Наблюдатель"?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>34. Паттерн Singleton, где его использовать в Android?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>35. В чем разница между LinkedList, ArrayList и Arrays?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>36. Над каким проектом вы сейчас работаете? Каков ваш рабочий процесс реализации задуманной функциональности?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>37. Как вы управляетесь с Firebase push notifications?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>38. Как реализовать Firebase realtime Database?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>39. У вас есть большой проект и у вас есть требования к безопасному входу в систему. Как вы будете реализовывать эти требования? :grimacing:</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>40. Что такое Eventbus?</summary>
 <p>ответ: http://greenrobot.org/ru-eventbus/</p>
</details>

<br>
<details>
 <summary>41. В каком потоке вызывается  метод onRecieve() в BroadcastReceiver'е?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>42. Как реализовать кастомный BroadcastReceiver?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>43. В чем разница между MVC и MVP?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>44. Объясните как устроен MVVM?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>45. Что означает M в MVP? Ответ … могло бы это быть чем-то еще? :confounded:</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>46. Какова цель Content Provider'а?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>47. Для чего используется библиотека SQLite?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>48. Какие библиотеки вы используете для работы с сетью (networking), загрузки картинок, баз данных?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>49. Что вы используете для очень быстрого Sensor, который излучает много показаний за раз в Rx? :disappointed_relieved: (what do you use to handle a very fast Sensor that emit many readings at a time in Rx way?)</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>50. В чем разница между map и flatMap() в Rxjava?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>51. Как создавать параллельные сетевые запросы в Rxjava?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>52. Если у вас есть запрос к сети и вы хотите запросить кеш, если сеть выдает ошибку, как это сделать на RxJava? Самое смешное, что я читал об этом в <a href="http://blog.danlew.net/">блоге Дэна Лью</a>, затем реализовал это дважды, но не смог ответить на этот вопрос на интервью. Плохие вещи случаются...</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>53. В чем разница между concatMap() и flatMap() в Rxjava?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>54. Что вам известно об Intents? Какова цель категорий в Intents?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>55. В чем цель FrameLayout?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>56. Как сравнить два объекта?</summary>
 <p>ответ:</p>
</details>

<br>
<details>
 <summary>57. Переменные в Java передаются по ссылке или по значению?</summary>
 <p>ответ: http://info.javarush.ru/translation/2014/06/30/%D0%9F%D0%B5%D1%80%D0%B5%D0%B4%D0%B0%D1%87%D0%B0-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D0%BE%D0%B2-%D0%B2-Java-%D0%9F%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4-.html</p>
</details>

<br>
<details>
 <summary>58. Когда вы используете observeOn() и когда subscribeOn()?</summary>
 <p>ответ:</p>
</details>
:triumph:

Ну, это все что я могу вспомнить на сегодняшний момент. Обычно в большинстве случаев спрашивают ООП, особенности Android и паттерны проетирования. 

К счастью, благодаря сообществу Android, существуют ответы на многие из вышеперечисленных вопросов. Не спешите. Потратьте ваше время, чтобы понять основы. Не накидывайтесь сразу на такие вещи как RxJava или Dagger без хорошей основы.

end.

### Bonus

*Еще парочка вопросов с ответами* :whale:

Основные вопросы:

<br>
<details>
 <summary>1. Что такое Android и кем он основан?</summary>
 <p>Android - это операционная система на основе Linux с открытым исходным кодом. Она была создана Эндрю Рубином и предназначена для мобильных телефонов, планшетов, телевизоров... и т.д.</p>
</details>
 
<br>
<details>
 <summary>2. Назовите основные компоненты Android-фреймворка</summary>
 <p>
  - Activity - хранит UI и организует взаимодействие пользователя с отдельным экраном смартфона<br><br>
  - Broadcast Receiver - организует отправку сообщений для других приложений или других систем. Это реализуется с помощью подкласса класса BroadcastReceiver и каждое сообщение организуется как Intent-объект<br><br>
  - Service - используется для фоновых операций<br><br>
  - Intent - эта сущность позволяет взаимодействовать разным Activity и организовать механизмы обмена данными<br><br>
  - Resource - хранит строковые и графические ресурсы<br><br>
  - Notification - для диалоговых окон, иконок, уведомлений, звука и всплывающих сообщений<br><br>
  - Content Provider - для обмена данными между приложениями или компонентами внутри одного приложения. Управляет доступом к структурированному набору данных. Он инкапсулирует данные и предоставляет механизмы для определения их безопасности. ContentProvider — это стандартный интерфейс, который соединяет данные в одном процессе с кодом, запущенным в другом процессе.
 </p>
</details>

<br>
<details>
 <summary>3. Какие дополнительные компоненты у Android?</summary>
 <p>
  - Fragment - содержит часть UI в Activity
  <br><br>
  - View - элементы UI, которые рисуются на экране, включая кнопки, списки, формы ввода, и т.д.
  <br><br>
  - Layout - организация иерархии View и взаимного расположения View, и особенностей показа View на экране
  <br><br>
  - Manifest - конфигурационный файл приложения
 </p>
</details>

<br>
<details>
 <summary>4. Какие уведомления доступны в Android и каково их использование?</summary>
 <p>
  <a href="https://material.io/guidelines/components/snackbars-toasts.html#snackbars-toasts-specs">Snackbars & Toast Notification</a> − отображается как всплывающее сообщение на поверхности окна.
  <br><br>
  Snackbar содержит одну строку текста, который непосредственно связан с выполняемой операцией. Только одно сообщение за один раз может быть на экране и может содержать только одно действие, которое не может быть "отменить".
  <br><br>
  Toast используется для системных сообщений. Обычно они отображаются на короткое время (два варианта 3.5 и 2 секунды) внизу экрана (можно настраивать).
  <br><br>
  Status bar уведомления отображаются в строке состояния.
  <br><br>
  Dialogue Notification − активное окно с уведомлением.
 </p>
</details>

<br>
<details>
 <summary>5. Какие флаги используются при запуске приложения Android?</summary>
 <p>
  FLAG_ACTIVITY_NEW_TASK
  <br><br>
  FLAG_ACTIVITY_CLEAR_TOP.</p>
</details>

<br>
<details>
 <summary>6. Версии Android идут под кодовыми номерами. Назовите как можно больше этих имен.</summary>
 <p>Aestro, Blender, Cupcake, Donut, Eclair, Froyo, Gingerbread, Honeycomb, Ice Cream Sandwich, Jelly Bean, Kitkat, Lollipop, Marshmallow</p>
</details>

<br>
<details>
 <summary>7. Какие главные преимущества Android?</summary>
 <p>Android - это ОС c открытым исходным кодом, это означает, что она бесплатна для конечного пользователя. Плата за лицензию, разработку и распространение не взимается. Она поддерживает множество различных технологий включая камеру, bluetooth, wifi и т.д. К томуже она имеет оптимизированную для маломощных устройств виртуальную машину Dalvik.</p>
</details>

<br>
<details>
 <summary>8. Назовите базу данных, которую использует Android, и расскажите о ней.</summary>
 <p>Android использует SQLite реляционную базу данных с открытым исходным кодом. Она встроена в Andoid по-умолчанию. Достаточно быстрая и удобная в работе. </p>
</details>

<br>
<details>
 <summary>9. Как можно организовать хранение данных в Android? Расскажите об этих способах.</summary>
 <p>
  Shared Preferences - хранит данные в виде приметивов ключ-значение. Класс SharedPreferences организует основную работу, которая позволяет пользователям хранить и получать данные по типу ключ-значение. Shared Preferences можно использовать для хранения таких типов данных как int, float, long, string... Эти данные сохраняются относительно постоянно (если только их не удалить целенаправленно). Больше информации <a href="https://developer.android.com/guide/topics/data/data-storage.html">здесь</a>.
  <br><br>
  Internal Storage - хранит данные в памяти устройства в виде файлов. Файлы, сохраненные для вашего приложения, по-умолчанию приватны, и другое приложение не может получит к ним доступ. Когда пользователь удаляет приложение, файлы, связанные с приложением, также удаляются.
  <br><br>
  External Storage - хранит данные в общем хранилище. Все приложения имеют доступ к этим данным. 
  <br><br>
  SQLite Database - хранит данные в структурированнов виде в базе данных. Android полностью поддерживает SQLite. Вне приложения база данных недоступна.
  <br><br>
  Также возможно хранение данных в сети на сервере. Доступ - посредством сетевого соединения. Организация сетевого соединения возможна посредвом пакетов java.net и android.net, но чаще используют готовые библиотеки.
 </p>
</details>

<br>
<details>
 <summary>10. Что такое виджеты приложений?</summary>
 <p>Это миниатюрные представления приложений, которые доступны для демонстрации в других приложениях (таких как Home screen). Больше см. <a href="https://developer.android.com/guide/topics/appwidgets/index.html#Basics">здесь</a></p>
</details>


 

<br>
### Bonus 2 
 
 *Ссылки на аналогичные списки и разговоры о собеседовании:*
 
 1. https://proglib.io/p/15-android-questions/ - :confused:
 2. http://www.quizful.net/interview/android?page=0 :smile:
 3. https://goo.gl/qgry1C
 4. https://habrahabr.ru/post/199280/
 5. https://dou.ua/forums/topic/17020/
 6. https://www.youtube.com/watch?v=igDSTgjhpN4
 7. http://www.tutorialspoint.com/android/android_questions_answers.htm :gb:
 8. http://www.careerride.com/android-interview-questions.aspx :gb:
 9. https://www.toptal.com/android/interview-questions :gb:
 10. https://intellipaat.com/interview-question/android-interview-questions/ :gb:
 11. https://github.com/MindorksOpenSource/android-interview-questions :gb: :thumbsup: :fire:
 
 
 [дополняется по мере сил, возможностей и способностей]
 
 <img src="{{ site.baseurl }}/images/hitrozhopye.jpg">
