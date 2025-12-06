---
## Front matter
lang: ru-RU
title: Сетевые технологии
subtitle: Двойной стек IPv4/IPv6. Анализ трафика в GNS3
author:
  - Хамди Мохаммад
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 11 ноября 2025

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

Построение сети с маршрутизаторами **FRR** и **VyOS** в GNS3, настройка двойного стека IPv4 и IPv6, анализ трафика в Wireshark.

# Разбиение адресного пространства

## IPv4

- Разбивка `172.16.20.0/24` на подсети с VLSM:  
  - `/25` → 126 хостов  
  - `/26` → 62 хоста  
  - `/26` → 62 хоста  

- Пример:  
  `172.16.20.0/25` — диапазон `172.16.20.1–126`

## IPv6

- Исходная сеть: `2001:db8:c0de::/48`
- Разбиение:
  - по Subnet ID → две сети `/49`
  - по Interface ID → два диапазона `/65`

# Построение сети в GNS3

## Топология

![Топология сети](Screenshot_1.png){ width=75% }

## IPv4 (VPCS)

| Узел | Адрес |
|------|-------|
| PC1 | `172.16.20.10/25` |
| PC2 | `172.16.20.138/25` |
| Server | `64.100.1.10/24` |

## IPv4 (маршрутизатор FRR)

![FRR config](Screenshot_5.png){ width=70% }

## Проверка связности (IPv4)

![Ping IPv4](Screenshot_7.png){ width=70% }

## Адресация узлов PC3, PC4, Server

| Узел | IPv6 адрес |
|------|-----------|
| PC3 | `2001:db8:c0de:12::a/64` |
| PC4 | `2001:db8:c0de:13::a/64` |
| Server | `2001:db8:c0de:11::a/64` |

## IPv6 (маршрутизатор VyOS)

![VyOS](Screenshot_12.png){ width=70% }

## Проверка связности (IPv6)

![Ping IPv6](Screenshot_14.png){ width=70% }

# Анализ трафика Wireshark

## ARP 

![Wireshark ARP](Screenshot_16.png){ width=80% }

## ICMP 

![Wireshark ICMP](Screenshot_17.png){ width=80% }

## ICMPv6 

![Wireshark ICMPv6](Screenshot_18.png){ width=80% }

# Самостоятельная часть

## Разбиение IPv4 и IPv6 на подсети

| Подсеть | IPv4 | IPv6 |
|---------|------|------|
| LAN1 | `10.10.1.96/27` | `2001:db8:1:1::/64` |
| LAN2 | `10.10.1.16/28` | `2001:db8:1:4::/64` |

## Разбиение IPv4 и IPv6 на подсети

![Топология подсетей](Screenshot_19.png){ width=75% }

## Проверка связности между подсетями

![Ping final](Screenshot_23.png){ width=65% }

# Итог

## Результаты

- Сети с IPv4 и IPv6 успешно настроены.
- FRR обеспечивает маршрутизацию IPv4, VyOS — IPv6.
- Wireshark подтвердил корректную работу ARP, ICMP и ICMPv6.

