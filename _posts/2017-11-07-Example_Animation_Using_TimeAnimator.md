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

Анимацию будем делать в кастомном View, который первым делом и создаем:

{% highlight java %}
public class RevolutionAnimationView extends View {

}
{% endhighlight %}

В качестве объектов для анимирования возмем такие:
<img src="{{ site.baseurl }}/images/hummer.png">
Создадим их 32 штуки, будем вращать, изменять прозрачность и размер. Объекты будут появляться у нижнего края экрана и уходить за верхний, после чего переиспользоваться. Начальное положение по оси Х, размер будем задавать случайно. Для создания эффекта глубины скорость перемещения и прозрачность объектов будет зависить от их размера.

Внутри нашего кастомного View  создаем класс который полностью описывает объект анимации на каждом шаге:
{% highlight java %}
private static class SerpMolot {
    private float x;
    private float y;
    private float scale;
    private float alpha;
    private float speed;
}
{% endhighlight %}

Так как экраны android-устройств могут иметь различные размеры, то зададим базовый размер наших объектов для анимации, базовую скорость, а заодно и прототип объекта, которой должен иметь тип Drawable:
{% highlight java %}
public class RevolutionAnimationView extends View {

    public static final int COUNT = 32;
    public static final int BASE_SPEED_DP_PER_S = 200;

    private static class SerpMolot {
        private float x;
        private float y;
        private float scale;
        private float alpha;
        private float speed;
    }

    private float mBaseSpeed;
    private float mBaseSize;
    private Drawable mDrawable;
    
    private void init() {
        mDrawable = ContextCompat.getDrawable(getContext(), R.drawable.ic_hammer);
        mBaseSize = Math.max(mDrawable.getIntrinsicWidth(), mDrawable.getIntrinsicHeight()) / 2f;
        mBaseSpeed = BASE_SPEED_DP_PER_S * getResources().getDisplayMetrics().density;
    }
}
{% endhighlight %}

При создадии или переиспользовании обекта для анимации мы должны его инициализировать. Добавляем эту фунцию в нашу кастомную View.. Но для этого нам понадобятся некоторые константы и класс для рандомизации:

{% highlight java %}
    /** минимальный размер объекта анимации */
    public static final float SCALE_MIN_PART = 0.45f;
    /** насколько сильно размер зависит от рандомной части */
    public static final float SCALE_RANDOM_PART = 0.55f;
    /** насколько сильно прозрачность зависит от размера объекта */
    private static final float ALPHA_SCALE_PART = 0.5f;
    /** насколько сильно прозрачность зависит от рандомной части */
    private static final float ALPHA_RANDOM_PART = 0.5f;

    //задаем генератор псевдослучайных чисел с инициализацией его
    public static final int SEED = 1337;
    private final Random mRnd = new Random(SEED);
    
{% endhighlight %}

Наконец, сама функция инициализации объекта для анимации:

{% highlight java %}
    private void initializeSerpMolot(SerpMolot serpMolot, int viewWidth, int viewHeight) {
        // размер объета 
        serpMolot.scale = SCALE_MIN_PART + SCALE_RANDOM_PART * mRnd.nextFloat();

        // координата X объекта
        serpMolot.x = viewWidth * mRnd.nextFloat();

        // координата Y - начинаем внизу View
        serpMolot.y = viewHeight;

        // Т.к. Y - середина объекта опускаем его на размер объекта
        // чтобы он внезапно не появлялся в нижней части View
        serpMolot.y += serpMolot.scale * mBaseSize;

        //Плюс опускаем объект на рандомное растояние за view,
        //чтобы появление всех объектов не было одновременным
        serpMolot.y += viewHeight * mRnd.nextFloat() / 4f;

        // Степень прозрачности зависит от размера и от рандомной состовляющей
        serpMolot.alpha = ALPHA_SCALE_PART * serpMolot.scale + ALPHA_RANDOM_PART * mRnd.nextFloat();

        // Скорость объекта зависит от прозрачности и от размера
        serpMolot.speed = mBaseSpeed * serpMolot.alpha * serpMolot.scale;
    }
{% endhighlight %}

Итак, где нам лучше инициализировать все объекты для анимации. Очевидно, что это лучше сделать в функции onSizeChanged(...) нашего View. Таким образом объеткы будут инициализированы при создании View и при каждом изменении ее размера:
{% highlight java %}
    //массив объектов для анимации
    private final SerpMolot[] mSerpMolots = new SerpMolot[COUNT]; 
    
    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);

        // исходная позиция зависит от размера View,
        // также обекты меняют позицию при изменении размера View
        for (int i = 0; i < mSerpMolots.length; i++) {
            final SerpMolot serpMolot = new SerpMolot();
            initializeSerpMolot(serpMolot, w, h);
            mSerpMolots[i] = serpMolot;
        }
    }
{% endhighlight %}

Теперь в функциях onAttachedToWindow() и onDetachedFromWindow() мы должны инициализировать, запустить и завершить работу TimeAnimator, соответственно. Приступим:
{% highlight java %}
    @Override
    protected void onAttachedToWindow() {
        super.onAttachedToWindow();

        //простота использования TimeAnimator:
        mTimeAnimator = new TimeAnimator(); //экземпляр класса TimeAnimator
        mTimeAnimator.setTimeListener(new TimeAnimator.TimeListener() { //задаем слушатель
            @Override
            public void onTimeUpdate(TimeAnimator animation, long totalTime, long deltaTime) {
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
                    if (!isLaidOut()) {
                        // Ignore all calls before the view has been measured and laid out.
                        return;
                    }
                }
                // deltaTime - столько времени в миллисекундах прошло с последнего шага анимации
                updateState(deltaTime); // см. ниже изменяем состояние объектов
                invalidate(); //обновляем View т.е. вызываем onDraw()
                // и т.о. делаем новое состояние видимым
            }
        });
        mTimeAnimator.start(); //запускаем Animator
    }
    
    // изменяем состояние объекта для анимации
    // т.е. перемещаем его вверх по View
    // и проверяем, если объект вышел за пределы View
    // то не уничтожаем его, но заного инициализируем (переиспользуем)
    private void updateState(float deltaMs) {
        // миллисекунды переводим в секунды
        final float deltaSeconds = deltaMs / 1000f;
        final int viewWidth = getWidth(); //Width of View
        final int viewHeight = getHeight(); //Height of View

        for (final SerpMolot serpMolot : mSerpMolots) {
            // Перемещаем объект учитывая скорость и время прошедшее после предыдущего шага
            serpMolot.y -= serpMolot.speed * deltaSeconds;

            // Если объект вышел за пределы View
            // переспользуем его снова
            final float size = serpMolot.scale * mBaseSize;
            if (serpMolot.y + size < 0) {
                initializeSerpMolot(serpMolot, viewWidth, viewHeight);
            }
        }
    }

    @Override
    protected void onDetachedFromWindow() {
        super.onDetachedFromWindow();

        mTimeAnimator.cancel();
        mTimeAnimator.setTimeListener(null);
        mTimeAnimator.removeAllListeners();
        mTimeAnimator = null;
    }
{% endhighlight %}

В функции updateState(float deltaMs), которая вызывается на каждом шаге анимации, происходит две вещи. Во-первых, мы перемещаем анимированный объект на требуемое расстояние, ориентируясь на время, прошедшее с момента предыдущего шага анимации. И таким образом, анимация будет подстраиваться под производительность системы. И, во-вторых, мы проверяем не ушел ли наш объект за пределы представления. Если ушел, то мы не уничтожаем его и создаем новый (это было бы не рационально), но переиспользуем, задавая новые значения, которые определяют его положение. Таким образом, достигается бесконечность и рандомность и не страдает производительность.

Производительность можно повысить учтывая версии систем и, например, на более ранних версиях уменшать количество анимируемых объектов.

Но, теперь нам нужно отобразить анимируемые объекты на нашем View, задавая необходимую прозрачность и размер. Кроме того, мы говорили, что объекты должны вращаться вокруг своей оси. Реализуем это все в функции рисования элементов View onDraw(...):
{% highlight java %}
    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        final int viewHight = getHeight();
        // для каждого объекта анимации делаем следующее
        for( final SerpMolot serpMolot : mSerpMolots) {
            //размер объекта
            final float serpMolotSize = serpMolot.scale * mBaseSize;
            // Если объект за пределами View, то игнорируем его
            if (serpMolot.y + serpMolotSize < 0 || serpMolot.y - serpMolotSize > viewHight) {
                continue;
            }

            // сохраняем текущее состояние canvas
            final int save = canvas.save();

            // перемещаем canvas в центр объекта
            canvas.translate(serpMolot.x, serpMolot.y);

            // вращение объекта (положение относительно своей оси) зависит от его размера
            // и положения по оси Y
            final float progress = (serpMolot.y + serpMolotSize) / viewHight;
            canvas.rotate(360 * progress);

            // подготавливваем размер и прозрачность для рисования
            final int size = Math.round(serpMolotSize);
            mDrawable.setBounds(-size, -size, size, size);
            mDrawable.setAlpha(Math.round(255 * serpMolot.alpha));

            // рисуем объект
            mDrawable.draw(canvas);

            // восстанавливаем canvas
            canvas.restoreToCount(save);
        }
    }
{% endhighlight %}

Кроме того добавим функции Pause() и Resume(), для остановки анимации и ее восстановления, если такое будет необходимо:
{% highlight java %}
    /**
     * Pause the animation if it's running
     */
    public void pause() {
        if (mTimeAnimator != null && mTimeAnimator.isRunning()) {
            // Сохраним текущее время произведения для последующего восстановления
            mCurrentPlayTime = mTimeAnimator.getCurrentPlayTime();
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
                mTimeAnimator.pause();
            }
        }
    }

    /**
     * Resume the animation if not already running
     */
    public void resume() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
            if (mTimeAnimator != null && mTimeAnimator.isPaused()) {
                mTimeAnimator.start();
                // восстанавливаем время воспроизведения TimeAnimator
                mTimeAnimator.setCurrentPlayTime(mCurrentPlayTime);
            }
        }
    }
{% endhighlight %}

Все, наш кастомный view почти готов, осталось добавить конструкторы. Вот полный листинг нашего View:
{% highlight java %}
package io.github.ziginsider.revolutiondemo;

import android.animation.TimeAnimator;
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.drawable.Drawable;
import android.os.Build;
import android.support.v4.content.ContextCompat;
import android.util.AttributeSet;
import android.view.View;

import java.util.Random;

/**
 * Created by zigin on 06.11.2017.
 */

public class RevolutionAnimationView extends View {

    private static class SerpMolot {
        private float x;
        private float y;
        private float scale;
        private float alpha;
        private float speed;
    }

    private float mBaseSpeed;
    private float mBaseSize;
    private long mCurrentPlayTime;

    public static final int SEED = 1337;
    public static final int COUNT = 32;
    public static final int BASE_SPEED_DP_PER_S = 200;


    /** The minimum scale of a SerpMolot */
    public static final float SCALE_MIN_PART = 0.45f;
    /** How much of the scale that's based on randomness */
    public static final float SCALE_RANDOM_PART = 0.55f;
    /** How much of the alpha that's based on the scale of the star */
    private static final float ALPHA_SCALE_PART = 0.5f;
    /** How much of the alpha that's based on randomness */
    private static final float ALPHA_RANDOM_PART = 0.5f;

    private final Random mRnd = new Random(SEED);
    private final SerpMolot[] mSerpMolots = new SerpMolot[COUNT];

    private TimeAnimator mTimeAnimator;
    private Drawable mDrawable;


    /** @see View#View(Context) */
    public RevolutionAnimationView(Context context) {
        super(context);
        init();
    }

    /** @see View#View(Context, AttributeSet) */
    public RevolutionAnimationView(Context context, AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    /** @see View#View(Context, AttributeSet, int) */
    public RevolutionAnimationView(Context context, AttributeSet attrs, int defStyle) {
        super(context, attrs, defStyle);
        init();
    }

    private void init() {
        mDrawable = ContextCompat.getDrawable(getContext(), R.drawable.ic_hammer);
        mBaseSize = Math.max(mDrawable.getIntrinsicWidth(), mDrawable.getIntrinsicHeight()) / 2f;
        mBaseSpeed = BASE_SPEED_DP_PER_S * getResources().getDisplayMetrics().density;
    }

    private void initializeSerpMolot(SerpMolot serpMolot, int viewWidth, int viewHeight) {
        // Set the scale based on a min value and a random multiplier
        serpMolot.scale = SCALE_MIN_PART + SCALE_RANDOM_PART * mRnd.nextFloat();

        // Set X to a random value within the width of the view
        serpMolot.x = viewWidth * mRnd.nextFloat();

        // Set Y - start at the bottom of the view
        serpMolot.y = viewHeight;

        // The value Y is in the center of the serpMolot, add the size
        // to make sure it starts outside of the view bound
        serpMolot.y += serpMolot.scale * mBaseSize;

        //Add a random offset to create a small delay before the serpMolot appears again
        serpMolot.y += viewHeight * mRnd.nextFloat() / 4f;

        // The alpha is determined by the scale of the serpMolot and a random multiplier
        serpMolot.alpha = ALPHA_SCALE_PART * serpMolot.scale + ALPHA_RANDOM_PART * mRnd.nextFloat();

        // The bigger and the brighter serpMolot is faster
        serpMolot.speed = mBaseSpeed * serpMolot.alpha * serpMolot.scale;
    }


    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        final int viewHight = getHeight();
        for( final SerpMolot serpMolot : mSerpMolots) {
            // Ignore the serpMolot if it's outside of the view bounds
            final float serpMolotSize = serpMolot.scale * mBaseSize;
            if (serpMolot.y + serpMolotSize < 0 || serpMolot.y - serpMolotSize > viewHight) {
                continue;
            }

            //Save the current canvas state
            final int save = canvas.save();

            // Move the canvas to the center of the serpMolot
            canvas.translate(serpMolot.x, serpMolot.y);

            //Rotate the canvas based on how far the serpMolot has moved
            final float progress = (serpMolot.y + serpMolotSize) / viewHight;
            canvas.rotate(360 * progress);

            //Prepare the size and alpha of the drawable
            final int size = Math.round(serpMolotSize);
            mDrawable.setBounds(-size, -size, size, size);
            mDrawable.setAlpha(Math.round(255 * serpMolot.alpha));

            // Draw the serpMolot to the canvas
            mDrawable.draw(canvas);

            // Restore the canvas to it's previous position and rotation
            canvas.restoreToCount(save);
        }
    }

    @Override
    protected void onSizeChanged(int w, int h, int oldw, int oldh) {
        super.onSizeChanged(w, h, oldw, oldh);

        // The starting position is dependent on the size of the view,
        // which is why the model is initialized here, when the view is measured.
        for (int i = 0; i < mSerpMolots.length; i++) {
            final SerpMolot serpMolot = new SerpMolot();
            initializeSerpMolot(serpMolot, w, h);
            mSerpMolots[i] = serpMolot;
        }
    }

    @Override
    protected void onAttachedToWindow() {
        super.onAttachedToWindow();

        mTimeAnimator = new TimeAnimator();
        mTimeAnimator.setTimeListener(new TimeAnimator.TimeListener() {
            @Override
            public void onTimeUpdate(TimeAnimator animation, long totalTime, long deltaTime) {
                if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
                    if (!isLaidOut()) {
                        // Ignore all calls before the view has been measured and laid out.
                        return;
                    }
                }
                updateState(deltaTime);
                invalidate();
            }
        });
        mTimeAnimator.start();
    }

    @Override
    protected void onDetachedFromWindow() {
        super.onDetachedFromWindow();

        mTimeAnimator.cancel();
        mTimeAnimator.setTimeListener(null);
        mTimeAnimator.removeAllListeners();
        mTimeAnimator = null;
    }

    /**
     * Progress the animation by moving the stars based on the elapsed time
     * @param deltaMs time delta since the last frame, in millis
     */
    private void updateState(float deltaMs) {
        // Converting to seconds since PX/S constants are easier to understand
        final float deltaSeconds = deltaMs / 1000f;
        final int viewWidth = getWidth();
        final int viewHeight = getHeight();

        for (final SerpMolot serpMolot : mSerpMolots) {
            // Move the serpMolot based on the elapsed time and it's speed
            serpMolot.y -= serpMolot.speed * deltaSeconds;

            // If the serpMolot is completely outside of the view bounds after
            // updating it's position, recycle it.
            final float size = serpMolot.scale * mBaseSize;
            if (serpMolot.y + size < 0) {
                initializeSerpMolot(serpMolot, viewWidth, viewHeight);
            }
        }
    }

    /**
     * Pause the animation if it's running
     */
    public void pause() {
        if (mTimeAnimator != null && mTimeAnimator.isRunning()) {
            // Store the current play time for later.
            mCurrentPlayTime = mTimeAnimator.getCurrentPlayTime();
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
                mTimeAnimator.pause();
            }
        }
    }

    /**
     * Resume the animation if not already running
     */
    public void resume() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
            if (mTimeAnimator != null && mTimeAnimator.isPaused()) {
                mTimeAnimator.start();
                // Why set the current play time?
                // TimeAnimator uses timestamps internally to determine the delta given
                // in the TimeListener. When resumed, the next delta received will the whole
                // pause duration, which might cause a huge jank in the animation.
                // By setting the current play time, it will pick of where it left off.
                mTimeAnimator.setCurrentPlayTime(mCurrentPlayTime);
            }
        }
    }
}
{% endhighlight %}

Наконец, используемый в примере layout: 
{% highlight xml %}
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="false"
    tools:context="io.github.ziginsider.revolutiondemo.FullscreenActivity">

    <FrameLayout
        android:id="@+id/animated_view_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorPrimary"
        >

        <io.github.ziginsider.revolutiondemo.RevolutionAnimationView
            android:id="@+id/animated_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_gravity="top|center_horizontal"
            android:layout_alignParentTop="true"
            />

        <android.support.v7.widget.AppCompatTextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="Revolution!"
            android:fontFamily="sans-serif-light"
            android:textAppearance="@style/Base.TextAppearance.AppCompat.Display2"
            android:textColor="#66000000"

            />

        <ImageView
            android:layout_width="200dp"
            android:layout_height="300dp"
            android:layout_gravity="bottom|center"
            android:background="@drawable/kremlin_part"
            />

        <LinearLayout
            android:id="@+id/buttons"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_gravity="bottom|center"
            android:orientation="horizontal"
            android:padding="16dp">

            <android.support.v7.widget.AppCompatButton
                android:id="@+id/btn_pause"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Pause"
                android:textColor="@color/white"
                android:background="@color/colorX"/>

            <android.support.v4.widget.Space
                android:layout_width="16dp"
                android:layout_height="16dp"/>

            <android.support.v7.widget.AppCompatButton
                android:id="@+id/btn_resume"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Resume"
                android:textColor="@color/white"
                android:background="@color/colorX"/>
                
        </LinearLayout>

    </FrameLayout>

</RelativeLayout>
{% endhighlight %}

И код Activity:
{% highlight java %}
package io.github.ziginsider.revolutiondemo;


import android.media.MediaPlayer;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;


public class FullscreenActivity extends AppCompatActivity implements View.OnClickListener {

    private RevolutionAnimationView mAnimationView;

    MediaPlayer mediaPlayer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        getWindow().getDecorView().setSystemUiVisibility(
                View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                        | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN);
        setContentView(R.layout.activity_fullscreen);

        mAnimationView = (RevolutionAnimationView) findViewById(R.id.animated_view);
        findViewById(R.id.btn_pause).setOnClickListener(this);
        findViewById(R.id.btn_resume).setOnClickListener(this);

        mediaPlayer = MediaPlayer.create(FullscreenActivity.this, R.raw.rodina_shostakovich);

        mediaPlayer.setLooping(true);
        mediaPlayer.setVolume(1.0f, 1.0f);
        mediaPlayer.start();

    }

    @Override
    protected void onResume() {
        super.onResume();
        mAnimationView.resume();
        mediaPlayer.start();
    }

    @Override
    protected void onPause() {
        super.onPause();
        mAnimationView.pause();
        mediaPlayer.pause();
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.btn_pause:
                mediaPlayer.pause();
                mAnimationView.pause();
                break;
            case R.id.btn_resume:
                mediaPlayer.start();
                mAnimationView.resume();
                break;
        }
    }
}
{% endhighlight %}

### Бонус
- Чтобы не было скучно, давайте добавим проигрывание музыки при запуске приложения. Для этого надо создать в ресурсах папку raw и поместить туда аудио-файл. В Activity прописать (как видно выше)
{% highlight java %}
    mediaPlayer = MediaPlayer.create(FullscreenActivity.this, R.raw.rodina_shostakovich);

    mediaPlayer.setLooping(true);
    mediaPlayer.setVolume(1.0f, 1.0f);
    mediaPlayer.start();
{% endhighlight %}

- Давайте добавим больше независимости кастомному View от Activity. Сделаем так, чтобы View сам следил за жизненным циклом Activity или Fragment в котором используется и реагировал бы на события onPause() и onResume(). Для этого воспользуемся возможностями Android Architecture Components:

Теперь наша Activity наследуется от LifecycleActivity. И в прописании функций onPause() и onResume() отпадает необходимость:
{% highlight java %}
public class FullscreenActivity extends LifecycleActivity implements View.OnClickListener {

    private RevolutionAnimationView mAnimationView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        getWindow().getDecorView().setSystemUiVisibility(
                View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                        | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN);
        setContentView(R.layout.activity_fullscreen);

        mAnimationView = (RevolutionAnimationView) findViewById(R.id.animated_view);
        findViewById(R.id.btn_pause).setOnClickListener(this);
        findViewById(R.id.btn_resume).setOnClickListener(this);
        ...
    }

    //@Override
    //protected void onResume() {
    //    super.onResume();
    //    mAnimationView.resume();
    //}

    //@Override
    //protected void onPause() {
    //    super.onPause();
    //    mAnimationView.pause();
    //}

    ...
}
{% endhighlight %}

При этом наша кастомная View реализует интерфейс LifecycleObserver. И перед функциями pause() и resume() появляются следующие аннотации:
{% highlight java %}
public class RevolutionAnimationView extends View implements LifecycleObserver {
...
    @OnLifecycleEvent(Lifecycle.Event.ON_PAUSE)
    public void pause() {
        if (mTimeAnimator != null && mTimeAnimator.isRunning()) {
            // Сохраним текущее время произведения для последующего восстановления
            mCurrentPlayTime = mTimeAnimator.getCurrentPlayTime();
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
                mTimeAnimator.pause();
            }
        }
    }

    @OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
    public void resume() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
            if (mTimeAnimator != null && mTimeAnimator.isPaused()) {
                mTimeAnimator.start();
                // восстанавливаем время воспроизведения TimeAnimator
                mTimeAnimator.setCurrentPlayTime(mCurrentPlayTime);
            }
        }
    }
    ...
}
{% endhighlight %}

Все.

Код проекта на github: <a href="https://github.com/ziginsider/RevolutionDemo">https://github.com/ziginsider/RevolutionDemo</a>
