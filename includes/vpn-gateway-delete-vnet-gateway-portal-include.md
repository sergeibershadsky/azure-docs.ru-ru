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
ms.openlocfilehash: 5b2aa7fedbc203c50796a0e0c8d9cdb3895ae6c1
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
### <a name="step-1-navigate-to-the-virtual-network-gateway"></a>Шаг 1. Переход к шлюзу виртуальной сети

1. На [портале Azure](https://portal.azure.com) выберите **Все ресурсы**. 
2. Чтобы открыть страницу шлюза виртуальной сети, перейдите к шлюзу виртуальной сети, который требуется удалить, и щелкните его.

### <a name="step-2-delete-connections"></a>Шаг 2. Удаление подключений

1. На странице шлюза виртуальной сети щелкните **Подключения**, чтобы просмотреть все подключения к шлюзу.
2. В строке с именем подключения щелкните **…** и в раскрывающемся списке выберите **Удалить**.
3. Нажмите кнопку **Да**, чтобы подтвердить удаление подключения. Если имеется несколько подключений, удалите их все.

### <a name="step-3-delete-the-virtual-network-gateway"></a>Шаг 3. Удаление шлюза виртуальной сети

Учтите: если кроме конфигурации типа "сеть — сеть" в этой виртуальной сети есть конфигурация типа "точка — сеть", удаление шлюза виртуальной сети приведет к автоматическому отключению всех клиентов P2S без предупреждения.

1. На странице шлюза виртуальной сети щелкните **Обзор**.
2. На странице **Обзор** щелкните **Удалить**, чтобы удалить этот шлюз.
