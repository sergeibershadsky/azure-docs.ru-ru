---
title: Использование локального шлюза данных для источников данных виртуальной сети Azure | Документация Майкрософт
description: Узнайте, как настроить сервер, чтобы использовать шлюз для источников данных в виртуальной сети.
author: minewiskan
manager: kfile
ms.service: analysis-services
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 7e792114c61c6257f4f5be5bfa65474d595f0d36
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
ms.locfileid: "32149584"
---
# <a name="use-gateway-for-data-sources-on-an-azure-virtual-network-vnet"></a>Использование шлюза для источников данных в виртуальной сети Azure

В этой статье описывается свойство сервера **AlwaysUseGateway**, которое следует использовать при размещении источников данных в [виртуальной сети Azure](../virtual-network/virtual-networks-overview.md).

## <a name="server-access-to-vnet-data-sources"></a>Доступ сервера к источникам данных виртуальной сети

Если доступ к источникам данных осуществляется через виртуальную сеть, сервер служб Azure Analysis Services должен подключаться к этим источникам данных так, как если бы они размещались в вашей локальной среде. Свойство сервера **AlwaysUseGateway** позволяет указать сервер для доступа ко всем источникам данных через [локальный шлюз](analysis-services-gateway.md). 

> [!NOTE]
> Это свойство действует только в тех случаях, если установлен и настроен [локальный шлюз данных](analysis-services-gateway.md). Шлюз может находиться в виртуальной сети.

## <a name="configure-alwaysusegateway-property"></a>Настройка свойства AlwaysUseGateway

1. Последовательно выберите SSMS > сервер > **Свойства** > **Общие** > **Показать дополнительные (все) свойства**.
2. Для параметра **ASPaaS\AlwaysUseGateway** выберите **true**.

    ![Свойство AlwaysUseGateway](media/analysis-services-vnet-gateway/aas-ssms-always-property.png)


## <a name="see-also"></a>См. также
[Подключение к локальным источникам данных](analysis-services-gateway.md)   
[Установка и настройка локального шлюза данных](analysis-services-gateway-install.md)   
[Виртуальная сеть Azure](../virtual-network/virtual-networks-overview.md)   

