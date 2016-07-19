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

<p style="max-width: 400px;">
```
lspci | grep Card
```
</p>
g


``` python
"""Copyright (c) 2013-2014 Stephan Groß, under MIT license."""
from __future__ import unicode_literals

import re

from django import template
from django.template import Node
from django.utils import six
from django.utils.encoding import force_text
from django.utils.functional import allow_lazy


register = template.Library()


def strip_spaces_between_tags_except_pre(value):
    def replacement(count, matches, match):
        matches.append(match.group(0)[1:-1])  # save the whole match without leading "<" and trailing ">"
        count[0] += 1
        return '<{{{0}}}>'.format(count[0])  # add "<" and ">" to preserve space stripping
    count = [-1]
    matches = []
    value = re.sub(r'<pre(\s.*)?>(.*?)</pre>', lambda match: replacement(count, matches, match), force_text(value), flags=re.S | re.M | re.I)
    value = re.sub(r'>\s+<', '><', force_text(value))
    return value.format(*matches)
strip_spaces_between_tags_except_pre = allow_lazy(strip_spaces_between_tags_except_pre, six.text_type)


class SpacelessExceptPreNode(Node):
    def __init__(self, nodelist):
        self.nodelist = nodelist

    def render(self, context):
        return strip_spaces_between_tags_except_pre(self.nodelist.render(context).strip())


@register.tag
def spaceless_except_pre(parser, token):
    """Remove whitespace between HTML tags, including tab and newline characters except content between <pre>"""
    nodelist = parser.parse(('endspaceless_except_pre',))
    parser.delete_first_token()
    return SpacelessExceptPreNode(nodelist)
```



{% highlight python linenos %}
"""Copyright (c) 2013-2014 Stephan Groß, under MIT license."""
from __future__ import unicode_literals

import re

from django import template
from django.template import Node
from django.utils import six
from django.utils.encoding import force_text
from django.utils.functional import allow_lazy


register = template.Library()


def strip_spaces_between_tags_except_pre(value):
    def replacement(count, matches, match):
        matches.append(match.group(0)[1:-1])  # save the whole match without leading "<" and trailing ">"
        count[0] += 1
        return '<{{{0}}}>'.format(count[0])  # add "<" and ">" to preserve space stripping
    count = [-1]
    matches = []
    value = re.sub(r'<pre(\s.*)?>(.*?)</pre>', lambda match: replacement(count, matches, match), force_text(value), flags=re.S | re.M | re.I)
    value = re.sub(r'>\s+<', '><', force_text(value))
    return value.format(*matches)
strip_spaces_between_tags_except_pre = allow_lazy(strip_spaces_between_tags_except_pre, six.text_type)


class SpacelessExceptPreNode(Node):
    def __init__(self, nodelist):
        self.nodelist = nodelist

    def render(self, context):
        return strip_spaces_between_tags_except_pre(self.nodelist.render(context).strip())


@register.tag
def spaceless_except_pre(parser, token):
    """Remove whitespace between HTML tags, including tab and newline characters except content between <pre>"""
    nodelist = parser.parse(('endspaceless_except_pre',))
    parser.delete_first_token()
    return SpacelessExceptPreNode(nodelist)
{% endhighlight %}

``` html
<html><body><div class="codehilite"><pre><code><span class="k">def</span> <span class="nf">hello</span><span class="p">():</span>
    <span class="k">print</span> <span class="s">&quot;world&quot;</span>
</code></pre></div></body></html>
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
{% highlight js linenos %}
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

Продолжаем...

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
