---
layout: post
title: Различные типы Item View в RecyclerView
date: 2017-11-13 21:06
tags:
- Java
- Android
- RecyclerView
- Refactoring
---
*Заметка основана на статье Mateusz Dziubek  <a href="https://android.jlelse.eu/multiple-row-types-in-recyclerview-2febf66e96a4">"Multiple row types in RecyclerView"</a>. Приводится пример создания RecyclerView c различными типами View. В процессе написания код подвергается рефакторингу. Показывается эффективность применения различных паттернов программирования и рефакторинга в целом на простом для понимания примере.*

<br>
### Постановка задачи
Итак, представим ситуацию, когда нам надо в один RecyclerView поместить несколько различных типов View. Допустим, это:

- кнопка
- картинка с текстом
- заголовок с текстом

На смартфоне мы должны получить что-то вроде этого:

<img src="{{ site.baseurl }}/images/testing1.jpeg">

Вдохновляясь статьей <a href="https://sourcemaking.com/refactoring/replace-conditional-with-polymorphism">Replace Conditional with Polymorphism</a>, попробуем сделать это. Основная идея - каждому типу View соответсвует отдельный класс, и эти классы объединяются общим интерфейсом.

<br>
### layout
Создаем, три layout, соответствующих трем типам View.

`row_type_button.xml`:
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="GO!" />
</LinearLayout>
{% endhighlight %}

<br>
`row_type_image.xml`:
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ImageView
        android:id="@+id/image"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="@drawable/apple" />

    <TextView
        android:id="@+id/text_image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="text" />
</LinearLayout>
{% endhighlight %}

<br>
`row_type_text.xml`:
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/header"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="I'm a header!"
        android:textStyle="bold" />

    <TextView
        android:id="@+id/text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="I'm a text!" />
</LinearLayout>
{% endhighlight %}

<br>
В 'activity_main.xml' добавляем RecyclerView:
{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="io.github.ziginsider.multiplerowtypesinrecyclerviewdemo.MainActivity">

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</android.support.constraint.ConstraintLayout>
{% endhighlight %}

<br>
### Классы для каждого типа View
Имея в виду `row_type_button`, создаем для него класс. Не забываем о конструкторе и обработчике нажатия:
{% highlight java %}
public class ButtonRowType implements RowType {

    private Context context;

    public ButtonRowType(Context context) {
        this.context = context;
    }

    public View.OnClickListener getOnClickListener() {
        return new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(context, "Click!", Toast.LENGTH_SHORT).show();
            }
        };
    }
}
{% endhighlight %}

<br>
Как видим, `RowType` и будет нашим объединяющим интерфейсом.

Далее, переходим к `row_type_image`. Незабываем о геттере для текста:
{% highlight java %}
public class ImageRowType implements RowType {

    private String text;

    public ImageRowType(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }
}
{% endhighlight %}

<br>
Наконец, `row_type_text`. Тут добавим геттеры для заголовка и текста:
{% highlight java %}
public class TextRowType implements RowType {

    private String header;
    private String text;

    public TextRowType(String header, String text) {
        this.header = header;
        this.text = text;
    }

    public String getHeader() {
        return header;
    }

    public String getText() {
        return text;
    }
}
{% endhighlight %}

<br>
### Объединяющий интерфейс
В адаптере мы будем различать типы наших View посредством `int getItemViewType(int position)`. Теперь вспомним об особенности интерфейсов, в силу уникальности, хранить в себе константы. Т.е. сигнатура `int` в интерфейсе соответсвует сигнатуре `public static final int` в классе наследующем интерфейс.

Учитывая данную особенность, сконструируем наш интерфейс для различения типов View:

{% highlight java %}
public interface RowType {
    int BUTTON_ROW_TYPE =   0;
    int IMAGE_ROW_TYPE = 1;
    int TEXT_ROW_TYPE = 2;
}
{% endhighlight %}

<br>
Теперь в адаптере мы сможем различать типы View используя `instanceof` и, таким образом, возвращать тип View. Итак...

<br>
### Адаптер
Получаем примерно такой адаптер:
{% highlight java %}
public class MultipleTypesAdapter extends RecyclerView.Adapter {
    
    private List<RowType> dataSet;

    public MultipleTypesAdapter(List<RowType> dataSet) {
        this.dataSet = dataSet;
    }

    @Override
    public int getItemViewType(int position) {
        if (dataSet.get(position) instanceof ButtonRowType) {
            return RowType.BUTTON_ROW_TYPE;
        } else if (dataSet.get(position) instanceof ImageRowType) {
            return RowType.IMAGE_ROW_TYPE;
        } else if (dataSet.get(position) instanceof TextRowType) {
            return RowType.TEXT_ROW_TYPE;
        } else {
            return -1;
        }
    }

    @Override
    public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        if (viewType == RowType.BUTTON_ROW_TYPE) {
            View view = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.row_type_button, parent, false);
            return new ButtonViewHolder(view);
        } else if (viewType == RowType.IMAGE_ROW_TYPE) {
            View view = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.row_type_image, parent, false);
            return new ImageViewHolder(view);
        } else if (viewType == RowType.TEXT_ROW_TYPE) {
            View view = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.row_type_text, parent, false);
            return new TextViewHolder(view);
        } else {
            return null;
        }
    }

    @Override
    public void onBindViewHolder(final RecyclerView.ViewHolder holder, int position) {
        if (holder instanceof ButtonViewHolder) {
            ((ButtonViewHolder) holder).button
                    .setOnClickListener(((ButtonRowType) dataSet.get(position)).getOnClickListener());
        } else if (holder instanceof ImageViewHolder) {
            ((ImageViewHolder) holder).textView2
                    .setText(((ImageRowType) dataSet.get(position)).getText());
        } else if (holder instanceof TextViewHolder) {
            ((TextViewHolder) holder).headerTextView
                    .setText(((TextRowType) dataSet.get(position)).getHeader());
            ((TextViewHolder) holder).textView1
                    .setText(((TextRowType) dataSet.get(position)).getText());
        }
    }

    @Override
    public int getItemCount() {
        return dataSet.size();
    }

    public static class ButtonViewHolder extends RecyclerView.ViewHolder {

        public Button button;

        public ButtonViewHolder(View itemView) {
            super(itemView);
            button = (Button) itemView.findViewById(R.id.button);
        }
    }

    public static class TextViewHolder extends RecyclerView.ViewHolder {

        public TextView headerTextView;
        public TextView textView1;

        public TextViewHolder(View itemView) {
            super(itemView);
            headerTextView = (TextView) itemView.findViewById(R.id.header);
            textView1 = (TextView) itemView.findViewById(R.id.text);
        }

    }

    public static class ImageViewHolder extends RecyclerView.ViewHolder {

        public ImageView imageView;
        public TextView textView2;

        public ImageViewHolder(View itemView) {
            super(itemView);
            imageView = (ImageView) itemView.findViewById(R.id.image);
            textView2 = (TextView) itemView.findViewById(R.id.text_image);
        }
    }
}
{% endhighlight %}

<br>
Что сказать? Невооруженным взглядом можно видеть что кода много. Лично у меня возникает ощущение захламленности. Давайте улучшать ситуацию.

<br>
### Рефакторинг
{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

{% highlight java %}
{% endhighlight %}

