---
layout: post
title: Simple Custom View demo App - circular progress bar
date: 2021-07-05 17:21
tags:
- Android
- Kotlin
- CustomView
---

<img src="{{ site.baseurl }}/images/rs/customview.gif" width="400">

## Custom View - circular progress bar

В [лекции курса](https://youtu.be/rhqFONf7O74) подробно про Custom View расказанно. Поэтому тут кратко.

Добавляем кастомные аттрибуты, которые мы потом сможем использовать при создании view:

{% gist 720e4b22c2410c80a7836ad0f95f2faf %}

Пишем класс CustomView:

{% gist 14eee431d869caa697bd82aee55aff40 %}

Тут не забываем релизнуть аттрибуты, после того как их прочитали `styledAttrs.recycle()`

В методе `onDraw()` не делаем никаких сложных вычислений, чтобы не загружать Main поток. Скажем, если можно создать необходимые объекты заранее, как например `Paint()` - то так и делаем.

Для демострации используем корутины. Тут мы запускаем корутину на GlobalScope и каждую 0.1 sec сетаем новый стейт View. Но это для простоты и тестовых целей. Но в продакш GlobalScope [лучше не использовать](https://elizarov.medium.com/the-reason-to-avoid-globalscope-835337445abc)

Репозиторий - [https://github.com/ziginsider/Simple-Custom-View_Android-Demo-App](https://github.com/ziginsider/Simple-Custom-View_Android-Demo-App)
