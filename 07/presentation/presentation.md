---
## Front matter
lang: ru-RU
title: Сетевые технологии
subtitle: Настройка DHCP для IPv4 и IPv6 в GNS3
author:
  - Хамди Мохаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 28 ноября 2025

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

Настройка служб **DHCPv4**, **DHCPv6 Stateless** и **DHCPv6 Stateful** в GNS3  
на маршрутизаторе **VyOS**, с проверкой работы клиентов и анализом трафика в **Wireshark**.

# Ход выполнения

## Топология сети

![Топология сети](Screenshot_1.png){ width=70% }

## Настройка VyOS

![Системные параметры VyOS](Screenshot_2.png){ width=70% }

## DHCPv4-сервер

![Настройка DHCPv4](Screenshot_3.png){ width=70% }

## Получение IPv4-адреса

![Получение адреса по DHCP](Screenshot_4.png){ width=70% }

## Проверка конфигурации

![IP-адресация PC1](Screenshot_5.png){ width=70% }

## DHCPv4 leases и лог

![Журнал и статистика DHCP](Screenshot_6.png){ width=70% }

## Процесс выдачи адреса

![DHCP трафик](Screenshot_8.png){ width=70% }

## Топология сети

![Топология IPv6](Screenshot_9.png){ width=70% }

## Настройка интерфейсов IPv6

![IPv6 интерфейсы на VyOS](Screenshot_10.png){ width=70% }

## RA и общие параметры сети

![DHCPv6 Stateless](Screenshot_11.png){ width=70% }

## SLAAC-адресация клиента PC2

![Конфигурация PC2](Screenshot_12.png){ width=70% }

## DHCPv6 Information-Request

![DHCPv6 запрос параметров](Screenshot_13.png){ width=70% }

## Проверка DNS и связности

![Параметры после DHCPv6](Screenshot_14.png){ width=70% }

## Логи сервера

![DHCPv6 leases (stateless)](Screenshot_15.png){ width=70% }

## Wireshark-анализ

![DHCPv6 Wireshark](Screenshot_16.png){ width=70% }

## Конфигурация сети на VyOS

![DHCPv6 Stateful настройки](Screenshot_17.png){ width=70% }

## Начальное состояние интерфейса

![PC3 начальные параметры](Screenshot_18.png){ width=70% }

## Получение адреса по DHCPv6

![DHCPv6 Stateful процесс](Screenshot_19.png){ width=70% }

## Конфигурация интерфейса и DNS

![Проверка после назначения адреса](Screenshot_20.png){ width=70% }

## Активные leases

![DHCPv6 Stateful leases](Screenshot_21.png){ width=70% }

## Анализ Wireshark

![Анализ Stateful DHCPv6](Screenshot_22.png){ width=70% }

# Заключение

## Основные результаты

- Настроены три механизма автоматической адресации:
  - **DHCPv4**
  - **DHCPv6 Stateless**
  - **DHCPv6 Stateful**
- Реализована работа с RA, SLAAC и DHCPv6-параметрами.
- Клиенты корректно получили IPv4/IPv6-адреса и параметры DNS.
- Трафик DHCP и ICMP был подробно проанализирован в Wireshark.
- Конфигурация сети подтверждена функционирующей связностью.

