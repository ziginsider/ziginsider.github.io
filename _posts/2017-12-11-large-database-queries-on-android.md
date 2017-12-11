---
layout: post
title: Большие запросы к базе данных на Android
date: 2017-12-11 16:28
tags:
- Java
- Android
- Architecture Components
- Translate
- SQLite
- Pagging Library
- CursorAdapter
---
<img src="{{ site.baseurl }}/images/largedatabase/intro_39.jpg">

:books: *Перевод статьи Chris Craik <a href="https://medium.com/google-developers/large-database-queries-on-android-cb043ae626e8">"Large Database Queries on Android"</a>.*

*Статья упомянута в офф. документации Google в разделе <a href="">Pagging Library</a>. И является вполне программной в смысле видения Google дальнейшего развития работы с SQLite в Android. Это новое видение, вполне не ново, т.к. вопрос (скорость и удобство работы с SQLite, загрузка больших порций данных) стоял давно и те или иные сторонние библиотеки решали этот вопрос. Но представив свою концепцию архитектуры приложений <a href="https://developer.android.com/topic/libraries/architecture/index.html">Android Architecture Components</a> разработчики Android Team не обошли внимание проблемы SQLite. Данная статья обзорная, она говорит о проблемах работы с данными, при использовании SQLite, и описывает пути решения данных проблем.*

<br>
### Возможности

SQLite - отличный способ хранить множество данных на Android, но так сложилось, что загрузка этих наборов данных в UI довольно нетривиальна, и может привести к проблемам производительности. Перед запуском новой библиотеки Paging Library, мы исследовали существующие подходы к подгрузке данных, и особенно потенциальные ловушки, при использовании SQLiteCursor.

В этой статье мы рассмотрим его проблемы, и поймем почему мы заинтересованы в использование небольших запросов с помощью <a href="https://developer.android.com/topic/libraries/architecture/room.html">Room</a> и <a href="https://developer.android.com/topic/libraries/architecture/paging.html">Pagging Library</a> в <a href="https://developer.android.com/topic/libraries/architecture/index.html">Architecture Android Components</a>.

<br>
### SQLiteCursor и CursorAdapter

SQLiteCursor это возвращаемый тип при запросе к базе данных SQLite в Android. Он позволяет получить большой объем данных за фиксированное время загрузки. 


The first read initializes a CursorWindow, a buffer of rows typically 2MB in size, with content from the database. The SQLiteCursor refreshes this window each time you request a row that isn’t present. In this way, SQLiteCursor implements paging, with a fixed page size.
CursorAdapter has been around since Android API 1, and has provided a simple way to bind data from a Cursor (typically a SQLiteCursor) to items in a ListView. While it serves this function fine, it queries the database directly on the UI thread any time a new load is needed. That in and of itself isn’t acceptable for a modern and responsive app. So one might ask: can’t we just have a Cursor-based adapter that loads on a background thread? SQLiteCursor has paging built right in, after all.

[в процессе]

