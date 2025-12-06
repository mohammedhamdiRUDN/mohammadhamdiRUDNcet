---
## Front matter
title: "Отчёт по лабораторной работе 5"
subtitle: "Простые сети в GNS3. Анализ трафика"
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

Построение простейших моделей сети на базе коммутатора и маршрутизаторов FRR и VyOS в GNS3, анализ трафика посредством Wireshark.

# Ход выполнения  

## Построение простой сети в GNS3  

1. В рабочей области **GNS3** была создана топология сети, состоящая из двух виртуальных ПК и одного коммутатора Ethernet. Устройства соединены между собой прямыми линками.  

   ![Топология сети в GNS3](Screenshot_1.png){ #fig:001 width=80% }  

2. Каждому устройству было присвоено имя в соответствии с требованиями задания:  
   - **PC1-hamdimohammad**  
   - **PC2-hamdimohammad**  
   - **msk-hamdimohammad-sw-01**  

   После соединения устройств проверено отображение интерфейсов и активное состояние линков.  

## Настройка IP-адресов на узлах  

3. В терминале VPCS выполнена проверка доступных команд с помощью запроса `?`, что позволило ознакомиться с синтаксисом конфигурации.  

   ![Просмотр синтаксиса команд VPCS](Screenshot_2.png){ #fig:002 width=80% }  

4. На **PC1-hamdimohammad** был задан IP-адрес `192.168.1.11/24` с шлюзом `192.168.1.1`, после чего конфигурация сохранена.  

   ![Настройка IP-адреса на PC1](Screenshot_3.png){ #fig:003 width=80% }  

5. На **PC2-hamdimohammad** аналогично был настроен адрес `192.168.1.12/24` с тем же шлюзом. Проверка связности командой `ping 192.168.1.11` показала успешный обмен ICMP-пакетами.  

   ![Проверка связности между PC1 и PC2](Screenshot_4.png){ #fig:004 width=80% }  

## Анализ трафика в Wireshark  

6. На соединении между **PC1** и **коммутатором** запущен захват пакетов в **Wireshark**. После старта узлов в окне анализатора появились **ARP-запросы** — объявления об IP-адресах устройств в сети.  

   ![Захват ARP-пакетов в Wireshark](Screenshot_5.png){ #fig:005 width=80% }  

   В частности, зафиксированы **Gratuitous ARP**-пакеты от обоих ПК, а также ответы вида *“Who has 192.168.1.12? Tell 192.168.1.11”*, подтверждающие нормальную работу ARP-протокола.  

7. Далее при выполнении команды `ping` был зафиксирован обмен **ICMP Echo Request** и **Echo Reply** между адресами `192.168.1.11` и `192.168.1.12`.  

   ![ICMP-запрос и ответ](Screenshot_6.png){ #fig:006 width=80% }  

8. При выполнении эхо-запросов в различных режимах (`ICMP`, `UDP`, `TCP`) с помощью параметра `-p` зафиксированы пакеты соответствующих протоколов:  
   - **UDP-эхо-запросы** передавались по порту 7 с полезной нагрузкой в 56 байт.  
     ![UDP-эхо-запрос](Screenshot_7.png){ #fig:007 width=80% }  
   - **TCP-эхо-запросы** сопровождались установкой соединения по схеме **SYN–ACK–FIN**, что подтверждает корректное выполнение трёхстороннего рукопожатия TCP.  
     ![TCP-эхо-запрос](Screenshot_8.png){ #fig:008 width=80% }  

9. В терминале PC2 были выполнены по одному эхо-запросу в каждом из режимов (ICMP, UDP, TCP), что подтвердило доступность узла PC1 на всех уровнях транспортного протокола.  

   ![Эхо-запросы в разных режимах](Screenshot_9.png){ #fig:009 width=80% }  

## Моделирование сети с маршрутизатором FRR  

1. В рабочей области **GNS3** была создана топология, включающая один маршрутизатор **FRR**, один коммутатор Ethernet и одно оконечное устройство **VPCS**.  

   ![Топология сети с маршрутизатором FRR](Screenshot_10.png){ #fig:010 width=80% }  

2. Оконечному устройству **PC1-hamdimohammad** присвоен IP-адрес `192.168.1.10/24` и шлюз по умолчанию `192.168.1.1`. Конфигурация сохранена, проверка выполнена с помощью команды `show ip`.  

   ![Настройка IP-адреса на PC1](Screenshot_11.png){ #fig:011 width=80% }  

3. На маршрутизаторе **FRR** выполнена базовая настройка:  
   - изменено имя устройства на **msk-hamdimohammad-gw-01**;  
   - активирован интерфейс `eth0`;  
   - назначен IP-адрес `192.168.1.1/24`.  

   ![Настройка маршрутизатора FRR](Screenshot_12.png){ #fig:012 width=80% }  

4. Конфигурация маршрутизатора проверена командами `show running-config` и `show interface brief`. Видно, что интерфейс `eth0` активен и имеет корректный IP-адрес.  

   ![Проверка конфигурации FRR](Screenshot_13.png){ #fig:013 width=80% }  

5. Проверка связности между ПК и маршрутизатором командой `ping 192.168.1.1` показала успешный обмен ICMP-пакетами.  

   ![Проверка соединения между ПК и маршрутизатором](Screenshot_14.png){ #fig:014 width=80% }  

6. В **Wireshark** зафиксированы ICMP-запросы и ответы между устройствами. Анализ показал корректную работу протоколов **ARP** и **ICMP**, обеспечивающих адресное разрешение и обмен эхо-запросами.  

   ![Анализ ICMP-трафика в Wireshark](Screenshot_15.png){ #fig:015 width=80% }  

## Моделирование сети с маршрутизатором VyOS  

7. В новой топологии **GNS3** размещены маршрутизатор **VyOS**, коммутатор Ethernet и устройство **PC1-hamdimohammad**.  

8. ПК получил IP-адрес `192.168.1.10/24` и шлюз `192.168.1.1`. Настройка сохранена.  

9. После входа на маршрутизатор VyOS под учетной записью **vyos/vyos** и установки системы выполнена базовая настройка:  
   - установлено имя устройства **msk-hamdimohammad-gw-01**;  
   - интерфейсу `eth0` присвоен адрес `192.168.1.1/24`.  

   ![Настройка маршрутизатора VyOS](Screenshot_16.png){ #fig:016 width=80% }  

10. Проверка интерфейсов показала, что `eth0` активен и имеет правильный адрес.  

   ![Просмотр интерфейсов VyOS](Screenshot_17.png){ #fig:017 width=80% }  

11. Проверка связи с ПК командой `ping 192.168.1.1` прошла успешно — получены ответы от маршрутизатора с временем отклика менее 5 мс.  

   ![Проверка связи между ПК и маршрутизатором VyOS](Screenshot_18.png){ #fig:018 width=80% }  

12. В **Wireshark** зафиксированы пакеты **ICMP Echo Request** и **Echo Reply** между адресами `192.168.1.10` и `192.168.1.1`. Протокол отработал корректно, обмен пакетами происходил без потерь.  

   ![ICMP-анализ для VyOS](Screenshot_19.png){ #fig:019 width=80% }  

# Заключение  

В ходе лабораторной работы были смоделированы две простейшие сети на базе маршрутизаторов **FRR** и **VyOS**. Для обеих конфигураций выполнена настройка IP-адресации, проверена связность между устройствами и проанализирован сетевой трафик.  

Захват в **Wireshark** подтвердил корректную работу протоколов **ARP** и **ICMP**, обеспечивающих базовый обмен сообщениями между маршрутизатором и оконечным устройством.  

