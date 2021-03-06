---
title: включение файла
description: включение файла
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 205c67377e4bff66c02e3ee508c0f6f4e2823608
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
Вы платите за каждый час использования вычислительных ресурсов шлюза виртуальной сети и за его исходящий трафик. Дополнительные сведения о ценах можно просмотреть на [этой странице](https://azure.microsoft.com/pricing/details/vpn-gateway) .

**Имя шлюза виртуальной сети: VNet1GW**.<br>Плата за использование вычислительных ресурсов шлюза виртуальной сети взимается по почасовому тарифу. Тариф зависит от SKU шлюза, выбранного при создании шлюза виртуальной сети. В стоимость входит сам шлюз и трафик, который через него проходит.

**расходы, связанные с передачей данных**;<br>Стоимость передачи данных вычисляется на основе исходящего трафика исходного шлюза виртуальной сети.

* Если вы отправляете трафик в локальное VPN-устройство, с вас будет взиматься плата как за исходящий сетевой трафик.
* При обмене данными между виртуальными сетями в разных регионах цена зависит от региона.
* При обмене данными между виртуальными сетями в одном регионе плата не взимается. Обмен данными между виртуальными сетями в одном регионе бесплатный.