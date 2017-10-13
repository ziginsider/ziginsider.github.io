---
layout: post
title: Android. Два способа записать результат Timer в пользовательский поток (UI Thread).
date: 2017-10-13 01:44
tags:
- Java
- Android
- Timer
- Threads
- примеры
---

*Timer в Android - это класс, который позволяет запланировать выполнение задачи на определенное время и, при необходимости, обеспечить циклическое повторение запуска задачи через определенные промежутки времени. Описание задачи дается в классе TimerTask.*

*Часто, при описании задачи в TimerTask, возникает необходимость вернуть результат в пользовательский поток. Ниже приведены два способа для этого.*

### Способ первый

<a href="https://goo.gl/MXtkMn">https://github.com/ziginsider/TimerDemo</a>

{% highlight java %}
    class MyTimerTask extends TimerTask {
        @Override
        public void run() {
            Calendar calendar = Calendar.getInstance();
            SimpleDateFormat simpleDateFormat = new SimpleDateFormat("HH:mm:ss a");
            final String strDate = simpleDateFormat.format(calendar.getTime());

            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    txtCounter.setText(strDate);
                }
            });
        }
    }
{% endhighlight %}

### Способ второй

<a href="https://goo.gl/bm9kHF">https://github.com/ziginsider/CodeLabsAndroidLifeCycle</a>

{% highlight java %}
    public LiveDataTimerViewModel() {
        mInitalTime = SystemClock.elapsedRealtime();
        Timer timer = new Timer();

        //Update the elapsed time every second
        timer.scheduleAtFixedRate(new TimerTask() {
            @Override
            public void run() {
                final long newValue = (SystemClock.elapsedRealtime() - mInitalTime) / 1000;

                //use tne Main looper
                new Handler(Looper.getMainLooper()).post(new Runnable() {
                    @Override
                    public void run() {
                        mElapsedTime.setValue(newValue);
                    }
                });
            }
        }, ONE_SECOND, ONE_SECOND);
    }
{% endhighlight %}
