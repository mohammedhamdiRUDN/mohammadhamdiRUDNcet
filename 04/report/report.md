---
## Front matter
title: "Отчёт по лабораторной работе 4"
subtitle: "Подготовка экспериментального стенда GNS3"
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

Установка и настройка GNS3 и сопутствующего программного обеспечения.

# Ход выполнения  

## Настройка и запуск GNS3  

1. Была запущена **виртуальная машина GNS3 VM**, после чего в основной операционной системе открыто приложение **GNS3**.  
   При первом запуске приложения открылся мастер настройки, где выбран режим работы — **Run appliances in a virtual machine**, что позволяет запускать устройства непосредственно в виртуальной среде.  

2. На этапе конфигурации удалённого контроллера GNS3 были указаны параметры подключения:  
   - **Protocol:** HTTP  
   - **Host:** 192.168.133.131  
   - **Port:** 80 TCP  
   - **Username:** admin  

   После ввода данных была выполнена успешная аутентификация с сервером.  

   ![Настройка удалённого контроллера GNS3](Screenshot_1.png){ #fig:001 width=80% }  

3. После завершения настройки сервер успешно подключился, что подтверждается зелёным индикатором состояния **gns3vm (controller)** в окне **Servers Summary**. Приложение готово к работе и созданию новых проектов.  

   ![Подключение GNS3 VM и готовность среды](Screenshot_2.png){ #fig:002 width=80% }  

## Добавление образа маршрутизатора FRR  

4. В панели маршрутизаторов (**Browse Routers**) был выбран пункт **New template** для добавления нового образа. В открывшемся окне из списка серверных шаблонов выбран образ **FRR (FRRouting Project)** и инициирована установка.  

   ![Выбор шаблона маршрутизатора FRR](Screenshot_3.png){ #fig:003 width=80% }  

5. В окне установки указано, что образ **FRR версии 8.2.2** найден локально и готов к установке, после чего был выбран пункт **Next** для продолжения.  

   ![Импорт и установка FRR](Screenshot_4.png){ #fig:004 width=80% }  

6. На этапе конфигурации шаблона во вкладке **General settings** были заданы основные параметры виртуальной машины:  
   - Категория — *Routers*  
   - Оперативная память — *256 MB*  
   - Количество vCPU — *1*  
   - Платформа — *x86_64*  
   - Тип консоли — *Telnet*  
   - Поведение при закрытии — *Send the shutdown signal (ACPI)*  

   ![Общие настройки шаблона FRR](Screenshot_5.png){ #fig:005 width=80% }  

7. Во вкладке **HDD** активирована опция *Automatically create a config disk on HDD*, что обеспечивает автоматическое создание диска для хранения конфигурации устройства.  

   ![Настройка HDD для FRR](Screenshot_6.png){ #fig:006 width=80% }  

## Добавление образа маршрутизатора VyOS  

8. Аналогичным образом добавлен образ маршрутизатора **VyOS**. В списке установочных файлов выбрана версия **1.3.3**, найденная локально и готовая к установке.  

   ![Импорт образа VyOS](Screenshot_7.png){ #fig:007 width=80% }  

## Проверка запуска устройств  

9. После добавления маршрутизаторов **FRR** и **VyOS** в рабочее пространство GNS3 они были запущены. В результате открылись консольные окна **PuTTY**, подтверждающие успешную загрузку систем.  
   - Устройство **VyOS** запросило ввод логина (`vyos login:`).  
   - Устройство **FRR** отобразило приветственное сообщение о запуске **FRRouting (version 8.2.2)**.  

   ![Запуск маршрутизаторов VyOS и FRR в GNS3](Screenshot_8.png){ #fig:008 width=80% }  

# Заключение  

В ходе работы была выполнена настройка виртуальной машины **GNS3 VM**, произведено подключение к контроллеру и добавлены образы маршрутизаторов **FRR** и **VyOS**.  
Оба устройства успешно установлены и запущены в среде GNS3, что подтверждает корректность конфигурации виртуальной лаборатории и готовность её к дальнейшей работе по моделированию сетевых сценариев.
