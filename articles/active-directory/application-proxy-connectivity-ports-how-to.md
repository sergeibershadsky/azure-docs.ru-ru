---
title: Как открыть порты брандмауэра, необходимые для приложения прокси приложения | Документы Майкрософт
description: Узнайте, какие порты необходимо открыть для правильной работы прокси приложения Azure AD.
services: active-directory
documentationcenter: ''
author: ajamess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 72acfbd21159e15fe237be6d509cb2c4a2b1bffd
ms.sourcegitcommit: e14229bb94d61172046335972cfb1a708c8a97a5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/14/2018
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a>Как открыть порты брандмауэра, необходимые для приложения прокси приложения

Чтобы просмотреть полный список необходимых портов и функции каждого порта, обратитесь к разделу "Необходимые компоненты" в [документации по прокси приложения](manage-apps/application-proxy-enable.md). Обратите внимание, что прокси приложения использует только исходящие порты.

Проверить, что все необходимые порты открыты, также можно с помощью [Средства тестирования портов соединителя](https://aadap-portcheck.connectorporttest.msappproxy.net/) из локальной сети. Большее число зеленых флажков означает большую устойчивость. 

## <a name="app-proxy-regions"></a>Регионы прокси приложения

Мы работаем над тем, чтобы зеленым цветом выделялись только необходимые для вас регионы. Пока убедитесь, что все регионы выделены зеленым цветом. Регион "Центральная часть США" должен быть выделен зеленым цветом независимо от того, в каком регионе вы находитесь.

Чтобы получить правильные результаты, необходимо:

-   Откройте средство в браузере на сервере, на котором установлен соединитель.

-   Убедитесь, что все прокси-серверы или брандмауэры, которые применяются к соединителю, также применяются к этой странице. Для этого в Internet Explorer выберите **Параметры** -&gt; **Свойства обозревателя** -&gt; **Подключения** -&gt; **Настройка сети**. На этой странице появится флажок "Использовать прокси-сервер для локальной сети". Установите этот флажок и укажите адрес прокси-сервера в поле "Адрес".

## <a name="next-steps"></a>Дополнительная информация
[Сведения о соединителях прокси приложения Azure AD](manage-apps/application-proxy-connectors.md)
