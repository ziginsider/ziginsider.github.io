---
layout: post
title: Монтирование SD карты в Ubuntu 13.04
date: 2014-03-18 01:33
tags:
- ubuntu
- usb
- linux
- памятка
- удалить
---

Открываем терминал и пишем следующее:

```
lspci | grep Card
```

Если увидели что-то подобное:

```
15:00.0 CardBus bridge: Ricoh Co Ltd RL5c476 II (rev ba)
15:00.5 System peripheral: Ricoh Co Ltd xD-Picture Card Controller (rev 11)
```

продолжаем...
<kbd>Shift</kbd>+<kbd>F11</kbd>
1. `sudo cp /etc/modules /etc/modules.bak`
2. открываем `sudo vim /etc/modules` и добавляем новую строку: `tifm_sd`
3. далее выполняем `sudo modprobe tifm_sd`
4. ребутимся
5. 

![Скриншот "не отвлекающего" режима](http://i.imgur.com/VXyN7CL.png)

Теперь, после загрузки сиcтемы, sd-карта должна автоматически примонтироваться.
{% highlight json %}
{
  // В боковой панели папки отмечать жирным шрифтов
  "bold_folder_labels": true,
  // Красивенный плавно мигающий курсор
  "caret_style": "phase",
  // Цветовая схема из Atom, захватившая мой моск
  "color_scheme": "Packages/User/Seti_orig (SL).tmTheme",
  // Рисовать код по центру (!)
  // ...выровненным по левому краю (О_о)
  // ...отсчитывая по самой длинной строчке
  // Это просто эстетически красиво, когда кроме этого на экране ничего нет
  "draw_centered": true,
  // Не скрывать выключатели сворачивания кусочков кода
  "fade_fold_buttons": false,
  // Шрифт. Довольно милый :3
  "font_face": "Meslo LG L DZ",
  // Размер шрифта. Очевидно.
  "font_size": 11,
  // Рисовать строку с курсором особым цветом, зависящим от цветовой схемы
  "highlight_line": true,
  // Эти пакеты есть, но выключены
  "ignored_packages":
  [
    // Это "режим vim". Я не фанат vim.
    "Vintage"
  ],
  // Немножко пустого места вокруг каждой строки, так легче читать
  "line_padding_bottom": 2,
  "line_padding_top": 2,
  // Эта опция действует ровно наоборот, чем гласит её имя
  // При true в заголовке окна только имя файла, не полное, без пути к нему
  "show_full_path": true,
  // Табуляция по два пробела
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  // Тема, тоже из Atom
  "theme": "Seti.sublime-theme",

  "word_wrap": true
}
{% endhighlight %}

{% highlight cpp linenos %}

   #include <iostream>

   int main(int argc, char *argv[]) {

   /* An annoying "Hello World" example */
   for (auto i = 0; i < 0xFFFF; i++)
    cout << "Hello, World!" << endl;

   char c = '\n';
   unordered_map <string, vector<string> > m;
   m["key"] = "\\\\"; // this is an error

   return -2e3 + 12l;
   }
{% endhighlight %}
