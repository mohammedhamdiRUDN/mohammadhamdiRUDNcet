---
## Front matter
title: "Отчёт по лабораторной работе 1"
subtitle: "Методы кодирования и модуляция сигналов"
author: "Хамди Мохаммад"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить и закрепить методы кодирования и модуляции сигналов в среде Octave. Построить временные диаграммы, выполнить спектральный анализ, определить характеристики сигналов и проверить свойства самосинхронизации.

# Ход выполнения

## 1.3.1. Построение графиков функций

1. Подготовлен скрипт **plot_sin.m** для построения функции  

y1 = sin(x) + 1/3·sin(3x) + 1/5·sin(5x)  

на интервале [-10; 10].  

![График функции y1](files/plot-sin.png){ #fig:001 width=80% }

2. На том же интервале построена функция  

y2 = cos(x) + 1/3·cos(3x) + 1/5·cos(5x)  

Обе функции выведены в одном окне.  

![Графики функций y1 и y2](files/plot-sin2.png){ #fig:002 width=80% }

---

## 1.3.2. Разложение импульсного сигнала в ряд Фурье

1. Разработан скрипт **meandr.m** для построения меандра с различным числом гармоник.  
2. Получены графики меандра через cos-компоненты.  

![Меандр через cos](files/meandr.png){ #fig:003 width=80% }

3. Выполнен аналогичный вариант через sin-компоненты.  

![Меандр через sin](files/meandr2.png){ #fig:004 width=80% }

---

## 1.3.3. Анализ спектров и характеристик сигналов

1. Сгенерированы синусоидальные сигналы с частотами 10 Гц и 40 Гц, построены их временные диаграммы.  

![Сигналы разной частоты](files/spectre1/signal/spectre.png){ #fig:005 width=80% }

2. Построены спектры указанных сигналов.  

![Спектры сигналов](files/spectre1/spectre/spectre.png){ #fig:006 width=80% }

3. Исправлен вариант спектров с исключением отрицательных частот.  

![Исправленные спектры](files/spectre1/spectre/spectre_fix.png){ #fig:007 width=80% }

4. Определён спектр суммы сигналов.  

![Суммарный сигнал](files/specter_sum/signal/spectre_sum.png){ #fig:008 width=80% }  
![Спектр суммы сигналов](files/specter_sum/spectre/spectre_sum.png){ #fig:009 width=80% }

---

## 1.3.4. Амплитудная модуляция

1. Создан скрипт **am.m** для моделирования амплитудной модуляции: несущая частота 50 Гц, модулирующий сигнал 5 Гц.  

![АМ-сигнал](files/modulation/signal/am.png){ #fig:010 width=80% }

2. Получен спектр модулированного сигнала.  

![Спектр АМ-сигнала](files/modulation/spectre/am.png){ #fig:011 width=80% }

---

## 1.3.5. Методы кодирования и проверка самосинхронизации

1. Реализованы скрипты, формирующие различные виды кодирования: униполярное, AMI, NRZ, RZ, Манчестерское и дифференциальное Манчестерское.  

### Примеры сигналов

![Unipolar](files/coding/signal/unipolar.png){ #fig:012 width=80% }  
![AMI](files/coding/signal/ami.png){ #fig:013 width=80% }  
![Bipolar NRZ](files/coding/signal/bipolarnrz.png){ #fig:014 width=80% }  
![Bipolar RZ](files/coding/signal/bipolarrz.png){ #fig:015 width=80% }  
![Manchester](files/coding/signal/manchester.png){ #fig:016 width=80% }  
![Diff Manchester](files/coding/signal/diffmanc.png){ #fig:017 width=80% }

### Проверка синхронизации

![Unipolar sync](files/coding/sync/unipolar.png){ #fig:018 width=80% }  
![AMI sync](files/coding/sync/ami.png){ #fig:019 width=80% }  
![Bipolar NRZ sync](files/coding/sync/bipolarnrz.png){ #fig:020 width=80% }  
![Bipolar RZ sync](files/coding/sync/bipolarrz.png){ #fig:021 width=80% }  
![Manchester sync](files/coding/sync/manchester.png){ #fig:022 width=80% }  
![Diff Manchester sync](files/coding/sync/diffmanc.png){ #fig:023 width=80% }

### Спектры сигналов

![Unipolar spectre](files/coding/spectre/unipolar.png){ #fig:024 width=80% }  
![AMI spectre](files/coding/spectre/ami.png){ #fig:025 width=80% }  
![Bipolar NRZ spectre](files/coding/spectre/bipolarnrz.png){ #fig:026 width=80% }  
![Bipolar RZ spectre](files/coding/spectre/bipolarrz.png){ #fig:027 width=80% }  
![Manchester spectre](files/coding/spectre/manchester.png){ #fig:028 width=80% }  
![Diff Manchester spectre](files/coding/spectre/diffmanc.png){ #fig:029 width=80% }

---

# Вывод

В ходе лабораторной работы были рассмотрены методы генерации и анализа сигналов, исследованы их спектры, реализована амплитудная модуляция, а также различные виды цифрового кодирования. Результаты подтвердили теоретические положения о разложении функций в ряд Фурье, свойствах самосинхронизации и спектральных особенностях сигналов. Работа в Octave способствовала закреплению практических навыков по моделированию сигналов и их визуализации.
