---
## Front matter
lang: ru-RU
title: Методы кодирования и модуляция сигналов
subtitle: Лабораторная работа №1
author:
  - Хамди Мохаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 12 сентября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---


# Введение

## Цель и задачи

Изучить и закрепить методы кодирования и модуляции сигналов в среде Octave. Построить временные диаграммы, выполнить спектральный анализ, определить характеристики сигналов и проверить свойства самосинхронизации.

# Ход выполнения

## Построение графиков функций

![Графики функций y1 и y2](files/plot-sin2.png){ #fig:002 width=80% }

## Разложение импульсного сигнала в ряд Фурье

![Меандр через sin](files/meandr2.png){ #fig:004 width=80% }

## Анализ спектров и характеристик сигналов

![Спектр суммы сигналов](files/specter_sum/spectre/spectre_sum.png){ width=78% }

## Амплитудная модуляция

![АМ сигнал](files/modulation/signal/am.png){ width=46% }
![Спектр АМ-сигнала](files/modulation/spectre/am.png){ width=46% }

## Примеры кодированных сигналов

![Unipolar](files/coding/signal/unipolar.png){ #fig:012 width=40% }  
![Bipolar RZ](files/coding/signal/bipolarrz.png){ #fig:015 width=40% }  


## Проверка самосинхронизации

![Diff Manchester sync](files/coding/sync/diffmanc.png){ #fig:023 width=80% }

## Спектры кодированных сигналов

![Diff Manchester spectre](files/coding/spectre/diffmanc.png){ #fig:029 width=80% }


# Итоги

## Выводы

В ходе лабораторной работы были рассмотрены методы генерации и анализа сигналов, исследованы их спектры, реализована амплитудная модуляция, а также различные виды цифрового кодирования. Результаты подтвердили теоретические положения о разложении функций в ряд Фурье, свойствах самосинхронизации и спектральных особенностях сигналов. Работа в Octave способствовала закреплению практических навыков по моделированию сигналов и их визуализации.
