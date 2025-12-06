---
## Front matter
lang: ru-RU
title: Сетевые технологии
subtitle: Простые сети в GNS3. Анализ трафика
author:
  - Хамди Мохаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 30 октября 2025

## Formatting pdf
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

## Основная цель

Построение простейших моделей сети на базе коммутатора и маршрутизаторов **FRR** и **VyOS** в **GNS3**, анализ трафика посредством **Wireshark**.

# Простая сеть на базе коммутатора

## Топология сети

   ![Топология сети в GNS3](Screenshot_1.png){ #fig:001 width=70% }

## Назначение IP-адресов

   ![Настройка IP-адреса на PC1](Screenshot_3.png){ #fig:003 width=70% }

## Проверка связности

   ![Проверка связности между PC1 и PC2](Screenshot_4.png){ #fig:004 width=70% }

# Анализ трафика Wireshark

## ARP-пакеты

   ![Захват ARP-пакетов в Wireshark](Screenshot_5.png){ #fig:005 width=70% }

## ICMP-пакеты

   ![ICMP-запрос и ответ](Screenshot_6.png){ #fig:006 width=70% }

## UDP и TCP-запросы

   ![TCP-эхо-запрос](Screenshot_8.png){ #fig:008 width=70% }

# Сеть с маршрутизатором FRR

## Топология и настройка устройств

   ![Топология сети с маршрутизатором FRR](Screenshot_10.png){ #fig:010 width=70% }

## Конфигурация FRR

   ![Настройка маршрутизатора FRR](Screenshot_12.png){ #fig:012 width=70% }

## Проверка соединения

   ![Проверка соединения между ПК и маршрутизатором](Screenshot_14.png){ #fig:014 width=70% }

# Анализ трафика FRR

## ICMP-тест и ARP-обмен

   ![Анализ ICMP-трафика в Wireshark](Screenshot_15.png){ #fig:015 width=70% }

# Сеть с маршрутизатором VyOS

## Топология сети

   ![Настройка маршрутизатора VyOS](Screenshot_16.png){ #fig:016 width=70% }

## Интерфейсы маршрутизатора

   ![Просмотр интерфейсов VyOS](Screenshot_17.png){ #fig:017 width=70% }

## Проверка соединения

   ![Проверка связи между ПК и маршрутизатором VyOS](Screenshot_18.png){ #fig:018 width=70% }

# Анализ трафика VyOS

## Обмен ICMP Echo

   ![ICMP-анализ для VyOS](Screenshot_19.png){ #fig:019 width=70% }

# Заключение

## Выводы

В результате лабораторной работы:  
- Смоделированы три топологии сети — на базе коммутатора, FRR и VyOS.  
- Выполнена настройка IP-адресации и проверена связность между устройствами.  
- Проанализированы пакеты **ARP** и **ICMP** в **Wireshark**.  
- Все конфигурации работали корректно, подтверждая правильность сетевых настроек.
