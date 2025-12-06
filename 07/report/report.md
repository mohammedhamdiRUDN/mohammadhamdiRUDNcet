---
## Front matter
title: "Отчёт по лабораторной работе 7"
subtitle: "Адресация IPv4 и IPv6. Настройка DHCP"
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

Получение навыков настройки службы DHCP на сетевом оборудовании для распределения адресов IPv4 и IPv6.

# Ход выполнения

## Построение топологии сети в GNS3

1. После запуска GNS3 VM и GNS3 был создан новый проект.  
   В рабочей области размещены устройства в соответствии с топологией задания: маршрутизатор VyOS, коммутатор hamdimohammad-sw-01 и хост PC1-hamdimohammad. Устройства соединены прямыми линками.

   ![Топология сети](Screenshot_1.png){ #fig:001 width=80% }

2. Устройствам присвоены имена:
   - PC1-hamdimohammad  
   - hamdimohammad-sw-01  
   - hamdimohammad-gw-01  

3. На соединении между коммутатором sw-01 и маршрутизатором gw-01 включён захват трафика.

## Настройка маршрутизатора VyOS

4. На маршрутизаторе выполнена установка системы VyOS и перезагрузка. Затем изменены имя устройства, доменное имя и создан пользователь hamdimohammad. После входа под новым пользователем удалён стандартный пользователь vyos.

   ![Настройка системных параметров VyOS](Screenshot_2.png){ #fig:002 width=80% }

## Настройка IPv4-адресации на маршрутизаторе

5. На интерфейсе eth0 маршрутизатора настроен адрес 10.0.0.1/24.

## Настройка DHCP-сервера на маршрутизаторе

6. Создана DHCP-конфигурация с доменным именем hamdimohammad.net, DNS-сервером 10.0.0.1, шлюзом 10.0.0.1 и диапазоном адресов 10.0.0.2–10.0.0.253.

   ![Настройка DHCP-сервера](Screenshot_3.png){ #fig:003 width=80% }

## Получение IP-адреса клиентом PC1

7. На ПК выполнено получение адреса через DHCP с отображением декодированных пакетов. Клиент получил IP 10.0.0.2, шлюз 10.0.0.1, DNS 10.0.0.1 и доменное имя hamdimohammad.net.

   ![Получение IP от DHCP](Screenshot_4.png){ #fig:004 width=80% }

## Проверка конфигурации ПК

8. На ПК проверены сетевые параметры и выполнена успешная проверка связности с маршрутизатором.

   ![Проверка адресации на PC1](Screenshot_5.png){ #fig:005 width=80% }

## Проверка DHCP-сервера на маршрутизаторе

9. Просмотрена статистика DHCP-сервера и список выданных адресов. Сервер выдал один адрес — 10.0.0.2 клиенту VPCS.

   ![Статистика и leases DHCP](Screenshot_6.png){ #fig:006 width=80% }

10. Просмотрен журнал работы DHCP-сервера, где отражены этапы Discover, Offer, Request и Ack.

   ![Журнал DHCP-событий](Screenshot_7.png){ #fig:007 width=80% }

## Анализ трафика DHCP в Wireshark

11. В трафике между sw-01 и gw-01 зафиксирована последовательность DHCP-процесса:
    - DHCP Discover  
    - DHCP Offer  
    - DHCP Request  
    - DHCP Ack  

    После получения адреса клиент отправляет Gratuitous ARP, что подтверждается захваченными кадрами.

   ![DHCP-пакеты в Wireshark](Screenshot_8.png){ #fig:008 width=80% }

## Построение расширенной топологии сети

1. В предыдущий проект была добавлена новая часть сети. В рабочем пространстве размещены и соединены дополнительные устройства: PC2-hamdimohammad, PC3-hamdimohammad, коммутаторы hamdimohammad-sw-02 и hamdimohammad-sw-03.  

   Итоговая топология соответствует структуре, приведённой в задании.

   ![Топология сети](Screenshot_9.png){ #fig:009 width=80% }

2. Всем устройствам присвоены имена в соответствии с шаблоном:
   - маршрутизатор: hamdimohammad-gw-01  
   - коммутаторы: hamdimohammad-sw-01, hamdimohammad-sw-02, hamdimohammad-sw-03  
   - хосты: PC1-hamdimohammad, PC2-hamdimohammad, PC3-hamdimohammad  

3. На соединениях между маршрутизатором и коммутаторами sw-02 и sw-03 включён захват трафика для анализа выполнения DHCPv6 и RA.

## Настройка IPv6 на маршрутизаторе

4. На интерфейсах маршрутизатора настроена IPv6-адресация:
   - eth1 — адрес из сети 2000::/64  
   - eth2 — адрес из сети 2001::/64  

   Настроенные параметры отображены в выводе интерфейсов.

   ![Настройка IPv6 интерфейсов](Screenshot_10.png){ #fig:010 width=80% }

## Настройка Router Advertisement и DHCPv6 Stateless

5. На маршрутизаторе выполнена настройка RA для интерфейса, подключённого к сети 2000::/64.  
   Включена передача префикса и установлен флаг other-config-flag, что говорит клиентам использовать DHCPv6 только для получения дополнительных параметров, но не адреса.

6. Создана разделяемая DHCPv6-сеть с именем hamdimohammad-stateless.  
   Заданы общие параметры: DNS-сервер 2000::1 и доменное имя hamdimohammad.net.  
   Настройка позволяет клиентам получать адрес через SLAAC, а вспомогательные параметры — через DHCPv6.

   ![Настройка DHCPv6 без отслеживания состояния](Screenshot_11.png){ #fig:011 width=80% }

## Проверка конфигурации на узле PC2

7. На PC2 (Kali Linux) проверены параметры интерфейса.  
   Интерфейс eth0 получил глобальный IPv6-адрес в сети 2000::/64 через SLAAC.

   ![Параметры интерфейса PC2](Screenshot_12.png){ #fig:012 width=80% }

8. Выполнена проверка маршрутов IPv6.  
   В таблице маршрутизации присутствует маршрут по умолчанию, полученный по RA.

9. Хост успешно проверил доступность маршрутизатора по IPv6.

10. Проверены настройки DNS.  
    Файл resolv.conf содержит доменное имя и IPv6-адрес DNS-сервера, полученные через DHCPv6.

## Получение параметров DHCPv6

11. На хосте выполнен запрос параметров DHCPv6.  
    Клиент запросил только конфигурацию (без адреса), поскольку используется Stateless DHCPv6.

    ![Запрос DHCPv6](Screenshot_13.png){ #fig:013 width=80% }

12. После получения данных DNS и доменного имени хост повторно проверил доступность маршрутизатора и содержимое resolv.conf.

    ![Проверка после получения DHCPv6 параметров](Screenshot_14.png){ #fig:014 width=80% }

## Проверка DHCPv6-сервера на маршрутизаторе

13. На маршрутизаторе проверена таблица выданных параметров DHCPv6.  
    В статeless-режиме сервер не назначает клиентам адреса, поэтому таблица выдачи пуста — это является корректным поведением.

    ![Просмотр leases DHCPv6](Screenshot_15.png){ #fig:015 width=80% }

## Анализ DHCPv6-трафика

14. В захваченном трафике Wireshark видны следующие пакеты:
    - Information-Request от клиента с просьбой выдать дополнительные параметры  
    - Ответ Reply с доменным именем, DNS-сервером и другими опциями  
    - Neighbor Solicitation и Neighbor Advertisement — часть стандартной работы IPv6  
    - Echo Request и Echo Reply — ICMPv6-проверка доступности  

    На кадре DHCPv6 Reply видны:
    - идентификаторы клиента и сервера  
    - DNS-сервер 2000::1  
    - домен hamdimohammad.net  

    Это подтверждает правильную работу stateless-конфигурации.

    ![Анализ трафика DHCPv6 в Wireshark](Screenshot_16.png){ #fig:016 width=80% }

## Настройка DHCPv6 с отслеживанием состояния (Stateful)

### Конфигурация маршрутизатора

1. На интерфейсе eth2 маршрутизатора были настроены объявления RA с установленным managed-flag.  
   Это означает, что узлы в данной сети должны использовать DHCPv6 с отслеживанием состояния для получения IPv6-адреса, а не только дополнительные параметры.

2. На маршрутизаторе создана новая разделяемая DHCPv6-сеть hamdimohammad-stateful.  
   Для подсети 2001::/64 заданы:
   - DNS-сервер 2001::1  
   - доменное имя hamdimohammad.net  
   - диапазон адресов 2001::100 — 2001::199  

   ![Настройка DHCPv6 Stateful на маршрутизаторе](Screenshot_17.png){ #fig:017 width=80% }

3. Конфигурация сохранена.

## Проверка параметров на клиенте PC3

4. На узле PC3 (Kali Linux) выполнена проверка состояния интерфейса.  
   До получения DHCPv6-адреса интерфейс имеет только link-local адрес fe80::/64.

5. Просмотр таблицы маршрутизации показывает наличие маршрута по умолчанию, полученного через RA с managed-flag.

   ![Начальные сетевые параметры PC3](Screenshot_18.png){ #fig:018 width=80% }

6. Проверены текущие настройки DNS — доменные параметры ещё не получены.

## Получение IPv6-адреса через DHCPv6 Stateful

7. Узел PC3 отправил запрос DHCPv6, получив:
   - уникальный идентификатор клиента  
   - IA_NA (Non-temporary Address), назначенный сервером  
   - адрес из диапазона 2001::100 — 2001::199  
   - доменное имя hamdimohammad.net  
   - адрес DNS-сервера 2001::1  

   ![Получение IPv6-адреса через DHCPv6](Screenshot_19.png){ #fig:019 width=80% }

## Проверка настроек после получения DHCPv6

8. На ПК проверено появление глобального IPv6-адреса в подсети 2001::/64.  
   Адрес соответствует диапазону, настроенному на маршрутизаторе.

9. Таблица маршрутизации обновилась, присутствует маршрут ::/0 через fe80::e3c:b8ff:fe62:2.

10. Хост успешно пропинговал маршрутизатор по адресу 2001::1.

11. Проверка файла resolv.conf показала получение DNS-параметров:
   - домен: hamdimohammad.net  
   - DNS: 2001::1  

   ![Проверка адреса, маршрутов и DNS после DHCPv6](Screenshot_20.png){ #fig:020 width=80% }

## Проверка работы DHCPv6-сервера

12. На маршрутизаторе просмотрены выданные адреса.  
   В таблице lease отображены два активных адреса:
   - 2001::198  
   - 2001::199  

   Эти записи содержат:
   - состояние аренды  
   - время окончания  
   - IAID/DUID клиента  
   - соответствующий пул hamdimohammad-stateful  

   ![Выданные адреса DHCPv6 Stateful](Screenshot_21.png){ #fig:021 width=80% }

## Анализ DHCPv6-трафика в Wireshark

13. В захваченном трафике видна последовательность обмена DHCPv6:
   - Solicit — клиент ищет сервер  
   - Advertise — сервер предлагает параметры и доступный адрес  
   - Request — клиент подтверждает выбор  
   - Reply — сервер выдаёт адрес и параметры  

14. В пакете Reply присутствуют:
   - IA_NA с назначенным адресом (Identity Association for Non-temporary Address)  
   - Preferred и valid lifetime  
   - DUID клиента  
   - DUID сервера  
   - DNS recursive name server: 2001::1  
   - Domain Search List: hamdimohammad.net  

   ![Анализ DHCPv6-трафика](Screenshot_22.png){ #fig:022 width=80% }

В режиме DHCPv6 Stateful клиент получает **полноценный IPv6-адрес** от сервера, а не формирует его через SLAAC.  
Маршрутизатор, используя managed-flag в RA, указывает клиенту использовать DHCPv6-сервер для конфигурации адреса.  
Клиент PC3 получил:
- индивидуальный глобальный адрес  
- DNS-сервер  
- доменное имя  
- параметры аренды  

Эти данные совпадают с конфигурацией, заданной на маршрутизаторе.

# Заключение

В процессе выполнения лабораторной работы была развернута и исследована сеть с поддержкой **IPv6**, включающая маршрутизатор **VyOS**, несколько коммутаторов и два клиента на основе Kali Linux. Последовательно были реализованы оба варианта автоматической настройки IPv6-адресов: **Stateless DHCPv6** и **Stateful DHCPv6**.
