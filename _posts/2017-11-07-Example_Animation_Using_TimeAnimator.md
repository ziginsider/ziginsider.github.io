---
layout: post
title: Пример анимации в Android с использованием TimeAnimator.
date: 2017-11-07 12:19
tags:
- Java
- Android
- TimeAnimator
- Animation
- примеры
---

*Пример создания бесконечной, случайной анимации с помощью TimeAnimator*

<img src="{{ site.baseurl }}/images/capture_revolution.png">

### Введение

Данная заметка базируется на статье <a href="https://medium.com/@patrick_iv/continuous-animation-using-timeanimator-5b8a903603fb">Continuous animation in Android using TimeAnimator</a>.

Цель: используя <a href="https://developer.android.com/reference/android/animation/TimeAnimator.html">TimeAnimator</a>, создать анимацию конечного числа объектов, которые, уходя за экран, переиспользовались бы снова (повышение производительности). Расположение объектов случайное. С помощью анимаций перемещения, вращения, изменения масштаба и прозрачности, создать эффект глубины.

Другими словами, мы хотим создать анимацию, которая была бы бесконечной, но не циклической. Объекты должны переиспользоваться, но при каждой инициализации их расположение должно задаваться случайным образом.

Почему ТimeAnimator? Для анимаций, у которых известно начальное и конечное состояние, удобно использовать ValueAnimator. Это также справедливо, когда наша анимация бесконечно циклически повторяется. Но если у нас бесконечная анимация, которая в той или иной степени рандомная (или чем-либо детерминируема), то ValueAnimator нам не подойдет. В этом случае прекрасно подходит TimeAnimator, который предоставляет слушатель, куда на каждом шаге анимации передается общее время анимации и время, которое прошло с последнего шага анимации (все в миллисекундах).

Итак, перед началом наглядные примеры ValueAnimator и TimeAnimator, которые дает Патрик в своей статье:

{% highlight java %}
// Example ValueAnimator
// Change color from white to blue
int from = Color.WHITE;
int to = Color.BLUE;
ValueAnimator animator = ValueAnimator.ofArgb(from, to);
animator.addUpdateListener(new AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator animation) {
        final int currentColor = (int)animation.getAnimatedValue();
    }
});
{% endhighlight %}

{% highlight java %}
// Example TimeAnimator
TimeAnimator animator = new TimeAnimator();
animator.setTimeListener(new TimeAnimator.TimeListener() {
    @Override
    public void onTimeUpdate(TimeAnimator a, long total, long dt){
        // total = millis since animation started
        // dt = millis since last update
    }
});
{% endhighlight %}

### Начнем

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

