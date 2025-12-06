---
## Front matter
title: "Отчёт по лабораторной работе 3"
subtitle: "Анализ трафика в Wireshark"
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

Изучение посредством Wireshark кадров Ethernet, анализ PDU протоколов транспортного и прикладного уровней стека TCP/IP.

# Ход выполнения  

## Анализ кадров канального уровня в Wireshark  

1. На устройство была установлена программа **Wireshark** и запущен захват трафика на активном сетевом интерфейсе.  

2. С помощью команды **ipconfig** были определены параметры сетевого подключения:  
   - IP-адрес устройства — **192.168.1.35**  
   - Маска подсети — **255.255.255.0**  
   - Шлюз по умолчанию — **192.168.1.1**  

   ![Результат команды ipconfig](Screenshot_1.png){ #fig:001 width=80% }  

3. Для проверки доступности шлюза по умолчанию выполнена команда **ping 192.168.1.1**.  
   Ответы получены успешно, потерь пакетов нет.  

   ![Проверка доступности шлюза](Screenshot_2.png){ #fig:002 width=80% }  

4. В **Wireshark** был применён фильтр `arp or icmp`, после чего зафиксированы ICMP-запросы и ответы между устройством и шлюзом.  

   ![ICMP-запрос и ответ в Wireshark](Screenshot_3.png){ #fig:003 width=80% }  
   ![Детализация ICMP-запроса](Screenshot_4.png){ #fig:004 width=80% }  
   ![Детализация ICMP-ответа](Screenshot_5.png){ #fig:005 width=80% }  

   **Анализ ICMP-запроса:**  
   - Длина кадра: **74 байта**  
   - Тип кадра: **Ethernet II**  
   - MAC-адрес источника: **4c:fb:45:66:db:28** (устройство)  
   - MAC-адрес получателя (шлюз): **c8:7f:54:78:b6:f2**  
   - Тип MAC-адресов: **уникальные (unicast)**  

   **Анализ ICMP-ответа:**  
   - Длина кадра: **74 байта**  
   - Тип кадра: **Ethernet II**  
   - MAC-адрес источника (шлюз): **c8:7f:54:78:b6:f2**  
   - MAC-адрес получателя (устройство): **4c:fb:45:66:db:28**  
   - Тип MAC-адресов: **уникальные (unicast)**  

5. Далее изучены кадры протокола **ARP**, фиксирующие обмен информацией об IP- и MAC-адресах в сети.  

   ![Анализ ARP-запроса](Screenshot_6.png){ #fig:006 width=80% }  
   ![Анализ ARP-ответа](Screenshot_7.png){ #fig:007 width=80% }  

   **ARP-запрос:**  
   - "Кто имеет IP **192.168.1.35**?"  
   - Источник: **c8:7f:54:78:b6:f2**  
   - Адрес назначения: **ff:ff:ff:ff:ff:ff** (широковещательный, broadcast)  

   **ARP-ответ:**  
   - "IP **192.168.1.35** принадлежит MAC **4c:fb:45:66:db:28**"  
   - Источник: **4c:fb:45:66:db:28**  
   - Адрес назначения: **c8:7f:54:78:b6:f2**  

6. Для анализа взаимодействия с внешними ресурсами был выполнен **ping google.com**.  
   Устройство получило ответы от IP-адреса **209.85.233.138**, время отклика составило в среднем **18 мс**.  

   ![Проверка доступности внешнего ресурса](Screenshot_8.png){ #fig:008 width=80% }  

   В Wireshark были зафиксированы соответствующие ICMP-запросы и ответы, а также ARP-обмен для определения адреса шлюза.  

   ![Анализ ICMP-трафика при ping google.com](Screenshot_9.png){ #fig:009 width=80% }  

## Анализ протоколов транспортного уровня в Wireshark  

1. В программе **Wireshark** был запущен захват трафика на активном сетевом интерфейсе.  

2. В браузере произведён переход на сайт **http://info.cern.ch/**, работающий по протоколу **HTTP**.  

3. В Wireshark применён фильтр `http`. Зафиксирован обмен HTTP-запросами и ответами поверх протокола **TCP**.  

   ![HTTP-запрос в Wireshark](Screenshot_10.png){ #fig:010 width=80% }  
   ![HTTP-ответ в Wireshark](Screenshot_11.png){ #fig:011 width=80% }  

   **Пояснение:**  
   - Запрос отправляется с порта **61111** клиента (192.168.1.35) на порт **80** сервера (188.184.67.127).  
   - Используется протокол **Ethernet II → IPv4 → TCP → HTTP**.  
   - В TCP-сегменте указывается **Sequence Number** и **Acknowledgment Number**, обеспечивающие надёжную доставку данных.  
   - В кадре видно передачу **HTTP GET-запроса** и ответ **HTTP/1.1 200 OK** с HTML-страницей.  

4. В Wireshark применён фильтр `dns`. Зафиксированы запросы и ответы по протоколу **DNS**, работающему поверх **UDP**.  

   ![DNS-запрос](Screenshot_12.png){ #fig:012 width=80% }  
   ![DNS-ответ](Screenshot_13.png){ #fig:013 width=80% }  

   **Пояснение:**  
   - Запрос отправляется с порта **49854** клиента (192.168.1.35) на порт **53** сервера (192.168.1.1).  
   - Пример: запрос имени `info.cern.ch` с типом записи **A**.  
   - В ответ сервер возвращает IP-адрес **188.184.67.127**, что подтверждает успешное разрешение имени.  
   - Используется структура: **Ethernet II → IPv4 → UDP → DNS**.  

5. В Wireshark применён фильтр `quic`. Зафиксирован обмен трафиком по протоколу **QUIC**, работающему поверх **UDP**.  

   ![QUIC-запрос](Screenshot_14.png){ #fig:014 width=80% }  
   ![QUIC-ответ](Screenshot_15.png){ #fig:015 width=80% }  

   **Пояснение:**  
   - Источник: клиент **192.168.1.35**, назначение: сервер **173.194.220.198**, порт **443**.  
   - Используется протокол: **Ethernet II → IPv4 → UDP → QUIC**.  

## Анализ handshake протокола TCP в Wireshark  

1. В программе **Wireshark** был запущен захват трафика на активном сетевом интерфейсе.  

2. Для генерации TCP-трафика было выполнено соединение с веб-сервером по протоколу **HTTP**.  

3. В Wireshark зафиксирован процесс установления TCP-сессии (трёхстороннее рукопожатие).  

   ![Анализ TCP-сессии](Screenshot_16.png){ #fig:016 width=80% }  

   **Этапы установления соединения:**  
   - **SYN**: клиент (192.168.1.35) отправляет на сервер (188.184.67.127) запрос на установление соединения с флагом SYN и начальным номером последовательности (**Seq = 1**).  
   - **SYN + ACK**: сервер отвечает подтверждением с флагами SYN и ACK, устанавливая свой номер последовательности (**Seq = 1**) и подтверждая получение данных клиента (**Ack = 2**).  
   - **ACK**: клиент подтверждает получение пакета от сервера, устанавливая **Ack = 2**.  
   После этого соединение считается установленным, и возможна передача данных (HTTP-запрос/ответ).  

4. Для анализа был построен **график потока** (Flow Graph) в Wireshark.  

   ![График потока TCP](Screenshot_17.png){ #fig:017 width=80% }  

   **Пояснение к графику:**  
   - На графике наглядно отображены все этапы TCP-взаимодействия.  
   - Видно трёхстороннее рукопожатие (SYN → SYN+ACK → ACK).  
   - После установления соединения фиксируется передача данных (HTTP GET, ответы сервера, обмен ACK).  
   - Завершение соединения происходит с помощью пакетов **FIN, ACK**, что также отражено на графике.  

5. После анализа захват трафика в Wireshark был остановлен.  

# Заключение  

В ходе работы был проведён анализ установления соединения по протоколу **TCP** с использованием программы **Wireshark**.  
Было зафиксировано трёхстороннее рукопожатие (SYN → SYN+ACK → ACK), подтверждающее успешное начало TCP-сессии.  
С помощью графика потока были проанализированы этапы установления и завершения соединения, а также последующая передача данных.  
