---
layout: post
title: Монтирование SD карты в Ubuntu 13.04
date: 2014-03-18 01:33
tags:
- ubuntu
- usb
- linux
- памятка
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

1. `sudo cp /etc/modules /etc/modules.bak`
2. открываем `sudo vim /etc/modules` и добавляем новую строку: `tifm_sd`
3. далее выполняем `sudo modprobe tifm_sd`
4. ребутимся

Теперь, после загрузки сиcтемы, sd-карта должна автоматически примонтироваться.
