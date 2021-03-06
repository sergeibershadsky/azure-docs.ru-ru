---
title: Функции Log Analytics для поставщиков служб | Документация Майкрософт
description: Log Analytics позволяет поставщикам управляемых служб (MSP), крупным предприятиям, независимым поставщикам программного обеспечения (ISV) и поставщикам услуг размещения управлять серверами, размещенными в локальной сети клиента или в облачной инфраструктуре, и осуществлять мониторинг таких серверов.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: jochan
editor: ''
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 6934e92df562099122eaede39fd26cf51cf1ee44
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="log-analytics-features-for-service-providers"></a>Функции Log Analytics для поставщиков услуг
Log Analytics позволяет поставщикам управляемых служб (MSP), крупным предприятиям, независимым поставщикам программного обеспечения (ISV) и поставщикам услуг размещения управлять серверами, размещенными в локальной сети клиента или в облачной инфраструктуре, и осуществлять мониторинг таких серверов. 

Крупные предприятия во многом сходны с поставщиками услуг, особенно те, которые используют единую ИТ-структуру для централизованного управления ИТ-системами в различных подразделениях. Для простоты в этом документе мы будем использовать термин *поставщик услуг*, но все описанные возможности доступны также для предприятий и других клиентов.

## <a name="cloud-solution-provider"></a>Поставщик облачных решений
Log Analytics входит в число служб Azure, доступных в рамках подписки [CSP Azure](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-overview), для партнеров и поставщиков услуг, работающих по программе [поставщика облачных решений (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview). 

В подписку *поставщика облачных решений* входят перечисленные ниже возможности Log Analytics.

*Поставщик облачных решений* может:

* Создавать рабочие области Log Analytics в подписке клиента.
* Использовать рабочие области, созданные клиентами. 
* Предоставлять и отменять доступ пользователей к рабочей области с помощью управления пользователями Azure. Если на портале OMS выполнен вход в рабочую область клиента, страница управления пользователями в разделе "Параметры" будет недоступна.
  * Log Analytics пока не поддерживает доступ на основе ролей. Если пользователю на портале Azure предоставлено разрешение `reader`, он сможет вносить изменения в конфигурацию на портале OMS.

Чтобы войти в подписку клиента, необходимо указать идентификатор клиента. Обычно в качестве этого идентификатора используется последняя часть адреса электронной почты, используемого для входа.

* На портале OMS добавьте к URL-адресу портала строку `?tenant=contoso.com`. Например, `mms.microsoft.com/?tenant=contoso.com`
* В PowerShell укажите параметр `-Tenant contoso.com` при использовании командлета `Connect-AzureRmAccount`.
* Если для входа на портал OMS для выбранной рабочей области вы используете ссылку `OMS portal` на портале Azure, идентификатор клиента добавляется автоматически.

*Клиент* поставщика облачных решений (CSP) может:

* Создавать рабочие области Log Analytics в своей подписке CSP.
* Использовать рабочие области, созданные поставщиком.
  * Для входа на портал OMS для выбранной рабочей области следует использовать ссылку `OMS portal` на портале Azure.
* Просматривать и использовать страницу управления пользователя в разделе параметров на портале OMS.

> [!NOTE]
> Включенные в комплект решения для архивации и восстановления сайта (Site Recovery) для Log Analytics не могут подключаться к хранилищу служб восстановления, поэтому их нельзя настроить в подписке CSP. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Управление несколькими клиентами с помощью Log Analytics
Для каждого клиента мы рекомендуем создать отдельную рабочую область Log Analytics. Рабочая область Log Analytics предоставляет следующие преимущества:

* Географическое расположение для хранения данных 
* Детализация данных для выставления счетов 
* Изоляция данных 
* уникальная конфигурация.

Создав рабочую область для каждого клиента, вы сможете разделить данные разных клиентов и отслеживать использование службы каждым из них.

Дополнительные сведения о том, когда и для чего следует создавать несколько рабочих областей, приведены в разделе [Управление доступом к Log Analytics](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Создание и настройку рабочих областей для клиентов можно автоматизировать с помощью [PowerShell](log-analytics-powershell-workspace-configuration.md), [шаблонов Resource Manager](log-analytics-template-workspace-configuration.md) или [REST API](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

Использование шаблонов Resource Manager для настройки рабочей области позволяет создать базовую конфигурацию и многократно использовать ее для создания и настройки рабочих областей. Вы можете быть уверены, что все создаваемые для клиентов рабочие области автоматически получат все нужные вам настройки. Когда изменятся требования к рабочим областям, шаблон можно обновить и заново применить для уже существующих рабочих областей. Этот процесс гарантирует, что все рабочие области, в том числе уже созданные, всегда будут соответствовать вашим новым стандартам.    

При управлении несколькими рабочими областями Log Analytics мы рекомендуем интегрировать каждую рабочую область с существующей системой отправки запросов или консолью управления с помощью функции [оповещений](log-analytics-alerts.md). Интеграция с существующими системами позволит специалистам службы поддержки использовать уже знакомые рабочие процессы. Log Analytics регулярно проверяет каждую рабочую область на соответствие заданным вами условиям оповещений и создает оповещение, если требуется вмешательство.

Чтобы получить персонализированные представления данных, используйте [панели мониторинга](../azure-portal/azure-portal-dashboards.md) на портале Azure.  

Чтобы объединять данные из нескольких рабочих областей для создания отчетов для высшего руководства, можно интегрировать Log Analytics с [Power BI](log-analytics-powerbi.md). Если потребуется интеграция с другой системой отчетности, вы можете применить API поиска (через PowerShell или [REST](log-analytics-log-search-api.md)) для отправки запросов и экспорта полученных результатов.

## <a name="next-steps"></a>Дальнейшие действия
* Автоматизация создания и настройки рабочих областей с помощью [шаблонов Resource Manager](log-analytics-template-workspace-configuration.md).
* Автоматизация создания рабочих областей с помощью [PowerShell](log-analytics-powershell-workspace-configuration.md). 
* Использование [оповещений](log-analytics-alerts.md) для интеграции с существующими системами.
* Создание сводных отчетов с помощью [Power BI](log-analytics-powerbi.md).

