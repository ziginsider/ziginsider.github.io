---
layout: post
title: Препарирование RecyclerView
date: 2017-02-25 18:19
tags:
- Android
- Java
- RecyclerView
- моё
---

RecyclerView:
- LayoutManager (Размещает)
- ItemAnimator (Анимирует)
- Adapter (Создает)
- Decorator (Дорисовывает

LayoutManager бывает
> LinearLayoutManager (линейное размещение элементов)
> GridLayoutManager (табличное)
> StaggeredGridLayoutManager (сложное)

- размещает элементы
- отвечает за скроллинг
- отвечает за View Focusing (В случае ListView отвечал сам ListView); т.е. на каком элементе сфокусироваться.
- отвечает за Accessibility; для людей с ограниченными возможностями.

Adapter

ответственен: 
- создание ViewHolder'ов
- заполнение ViewHolder'ов информацией
- за уведомление RecyclerView о том какие элементы изменились.
- обработка касаний
- частичное обновление данных
- управление количеством ViewType'ов
- информация о переиспользовании ViewHolder'а

Основное API Adapter'a:

ViewHolder onCreateViewHolder(ViewGroup parent, int viewType)

void onBindViewHolder(ViewHolder holder, int position) - при изменении позиции элемента не вызывается, поэтому нельзя вызывать так см. типичные ошибки #1

int getItemViewType(int position)

boolean onFailedToRecycleView(ViewHolder holder)

void onViewRecycled(ViewHolder holder)


методы notifyItemX() нужны для того, чтобы изменять, удалять, добавлять элементы и при этом анимировать (??):

notifyItemChanged();

notifyItemInserted();

notifyItemMoved();

notifyItemRemoved();

польза от методов notifyItemX():
- Нет лишних вызовов onBindViewHolder();
- Возможность анимировать и перемещать элементы как угодно
- Нет лишних вызовов onCreateViewHolder

void setHasStableIds(boolean hasStableIds) - еслт в конструкторе вызвать этот метод с true, то RecyclerView сам будет вычислять, какие элементы поменялись местами, какие добавились, удалились и т.д. Для этого необходимо реализовать:

long getItemId(int position)

и давать уникальное Id элемента на основе его содержимого или создавать Id на основе Id layout'a, из которого мы надуваем это view, и который всегда уникальный.


Типичные ошибки
#1
