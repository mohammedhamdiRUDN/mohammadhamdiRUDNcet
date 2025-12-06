---
## Front matter
lang: ru-RU
title: Сетевые технологии
subtitle: Анализ трафика в Wireshark
author:
  - Хамди Мохаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 15 октября 2025

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

# Цели и задачи работы

## Цель лабораторной работы

Изучение посредством Wireshark кадров Ethernet, анализ PDU протоколов транспортного и прикладного уровней стека TCP/IP.

# Выполнение лабораторной работы

## Анализ кадров канального уровня

   ![Результат команды ipconfig](Screenshot_1.png){ #fig:001 width=70% }

## Анализ кадров канального уровня

   ![Проверка доступности шлюза](Screenshot_2.png){ #fig:002 width=70% }

## Анализ кадров канального уровня

   ![ICMP-запрос и ответ в Wireshark](Screenshot_3.png){ #fig:003 width=70% }

## Анализ кадров канального уровня

   ![Детализация ICMP-запроса](Screenshot_4.png){ #fig:004 width=70% }

## Анализ кадров канального уровня

   ![Детализация ICMP-ответа](Screenshot_5.png){ #fig:005 width=70% }

## Анализ ARP

   ![Анализ ARP-запроса](Screenshot_6.png){ #fig:006 width=70% }

## Анализ ARP

   ![Анализ ARP-ответа](Screenshot_7.png){ #fig:007 width=70% }

## Анализ ICMP и ARP при ping внешнего ресурса

   ![Проверка доступности внешнего ресурса](Screenshot_8.png){ #fig:008 width=70% }

## Анализ ICMP и ARP при ping внешнего ресурса

   ![Анализ ICMP-трафика при ping google.com](Screenshot_9.png){ #fig:009 width=70% }

## Анализ транспортного уровня: HTTP

   ![HTTP-запрос в Wireshark](Screenshot_10.png){ #fig:010 width=70% }

## Анализ транспортного уровня: HTTP

   ![HTTP-ответ в Wireshark](Screenshot_11.png){ #fig:011 width=70% }

## Анализ транспортного уровня: DNS

   ![DNS-запрос](Screenshot_12.png){ #fig:012 width=70% }

## Анализ транспортного уровня: DNS

   ![DNS-ответ](Screenshot_13.png){ #fig:013 width=70% }

## Анализ транспортного уровня: QUIC

   ![QUIC-запрос](Screenshot_14.png){ #fig:014 width=70% }

## Анализ транспортного уровня: QUIC

   ![QUIC-ответ](Screenshot_15.png){ #fig:015 width=70% }

## Анализ TCP handshake

   ![Анализ TCP-сессии](Screenshot_16.png){ #fig:016 width=70% }

## График потока TCP

   ![График потока TCP](Screenshot_17.png){ #fig:017 width=70% }

# Выводы по проделанной работе

## Вывод

В ходе работы был проведён анализ установления соединения по протоколу **TCP** с использованием программы **Wireshark**.  
Было зафиксировано трёхстороннее рукопожатие (SYN → SYN+ACK → ACK), подтверждающее успешное начало TCP-сессии.  
С помощью графика потока были проанализированы этапы установления и завершения соединения, а также последующая передача данных.
