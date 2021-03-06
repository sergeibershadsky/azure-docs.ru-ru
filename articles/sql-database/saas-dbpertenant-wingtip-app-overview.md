---
title: 'SaaS Wingtip: пример мультитенантного приложения Базы данных SQL Azure | Документация Майкрософт'
description: Изучите пример мультитенантного приложения SaaS Wingtip, использующего Базу данных SQL Azure
keywords: руководство по базе данных sql
services: sql-database
author: stevestein
manager: craigg
ms.service: sql-database
ms.custom: scale out apps
ms.topic: article
ms.date: 04/01/2018
ms.author: sstein
ms.openlocfilehash: cf54c789d766c4bd3d353028e75e34c961470070
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="introduction-to-a-multitenant-saas-app-that-uses-the-database-per-tenant-pattern-with-sql-database"></a>Общие сведения о мультитенантном приложении SaaS на основе Базы данных SQL, в котором используется отдельная база данных для каждого клиента

Приложение Wingtip SaaS — это пример мультитенантного приложения. Для обслуживания нескольких клиентов приложение использует шаблон приложения SaaS, в котором для каждого клиента используется отдельная база данных. Приложение демонстрирует возможности Базы данных SQL Azure, которые позволяют работать со сценариями SaaS, используя несколько моделей проектирования и управления SaaS. Приложение SaaS Wingtip развертывается менее чем за пять минут, поэтому вы сможете быстро приступить к работе.

Исходный код приложения и сценарии управления доступны в репозитории GitHub [WingtipTicketsSaaS-DbPerTenant](https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant). Прежде чем начать, изучите инструкции по скачиванию и разблокированию сценариев управления Wingtip Tickets в статье [Общие рекомендации по работе с примерами приложений SaaS Wingtip Tickets](saas-tenancy-wingtip-app-guidance-tips.md).

## <a name="application-architecture"></a>Архитектура приложения

Приложение Wingtip SaaS использует модель базы данных для каждого клиента. Чтобы добиться максимальной эффективности, оно использует пулы эластичных БД SQL. Для подготовки и сопоставления клиентов с их данными используется база данных каталога. Основное приложение SaaS Wingtip использует пул с тремя клиентами и базу данных каталога. Серверы каталога и клиента подготовлены с применением псевдонимов DNS. В этих псевдонимах содержатся ссылки на активные ресурсы, используемые приложением Wingtip. В руководствах по аварийному восстановлению эти псевдонимы обновляются с добавлением ссылок на ресурсы восстановления. Многие руководства по Wingtip SaaS позволяют получить надстройки для базового развертывания. Доступны такие надстройки, как аналитические базы данных и схемы управления для нескольких баз данных.


![Архитектура SaaS Wingtip](media/saas-dbpertenant-wingtip-app-overview/app-architecture.png)


Изучая это руководство и описанное здесь приложение, уделяйте особое внимание шаблонам SaaS, так как они относятся к уровню данных. То есть сосредоточьтесь именно на уровне данных, а не увлекайтесь анализом приложения. Если вы поймете реализацию этих шаблонов SaaS, вы сможете реализовать их в своих приложениях. Обращайте также внимание на изменения, которые потребуется внести для учета конкретных бизнес-требований.

## <a name="sql-database-wingtip-saas-tutorials"></a>Руководства по SaaS Wingtip базы данных SQL

Развернув приложение, изучите перечисленные ниже руководства, которые основываются на базовом развертывании. В этих руководствах рассматриваются распространенные шаблоны SaaS, использующие встроенные функции Базы данных SQL, хранилища данных SQL и других служб Azure. Руководства содержат скрипты PowerShell с подробными описаниями. Эти описания позволят быстрее разобраться в шаблонах управления SaaS и применить их в приложениях.


| Учебник | ОПИСАНИЕ |
|:--|:--|
| [Общие рекомендации по работе с примерами приложений SaaS Wingtip Tickets](saas-tenancy-wingtip-app-guidance-tips.md) | Скачайте и выполните скрипты PowerShell для подготовки частей приложения. |
|[Развертывание и изучение мультитенантного приложения SaaS, использующего базу данных SQL Azure](saas-dbpertenant-get-started-deploy.md)|  Разверните в подписке Azure мультитенантное приложение SaaS и изучите его возможности. |
|[Подготовка новых клиентов и их регистрация в каталоге](saas-dbpertenant-provision-and-catalog.md)| Узнайте, как приложение подключается к клиентам с помощью базы данных каталога и как клиенты сопоставляются с данными каталога. |
|[Мониторинг производительности примера приложения SaaS Wingtip](saas-dbpertenant-performance-monitoring.md)| Узнайте, как использовать функции мониторинга Базы данных SQL и настроить оповещения при превышении пороговых значений производительности. |
|[Мониторинг с помощью Log Analytics](saas-dbpertenant-log-analytics.md) | Узнайте, как применить [Log Analytics](../log-analytics/log-analytics-overview.md) для мониторинга большого количества ресурсов в нескольких пулах. |
|[Восстановление базы данных отдельного клиента](saas-dbpertenant-restore-single-tenant.md)| Узнайте, как восстановить базу данных клиента до предыдущей точки во времени. Научитесь восстанавливать данные в параллельную базу данных, сохраняя работоспособность существующей базы данных клиента. |
|[Manage schema for multiple tenants in the WTP SaaS application](saas-tenancy-schema-management.md) (Управление схемой нескольких клиентов в SaaS-приложении WTP)| Узнайте, как обновить схему и опорные данные во всех базах данных клиентов. |
|[Отчеты по всем клиентам с использованием распределенных запросов](saas-tenancy-cross-tenant-reporting.md) | Создайте базу данных ad-hoc-аналитики и выполняйте распределенные запросы ко всем клиентам в реальном времени.  |
|[Межклиентская аналитика с помощью извлеченных данных](saas-tenancy-tenant-analytics.md) | Извлечение данных клиента в базу данных аналитики или хранилище данных для автономных аналитических запросов. |


## <a name="next-steps"></a>Дополнительная информация

- [Общие рекомендации по работе с примерами приложений SaaS Wingtip Tickets](saas-tenancy-wingtip-app-guidance-tips.md)
- [Развертывание и изучение мультитенантного приложения SaaS, использующего базу данных SQL Azure](saas-dbpertenant-get-started-deploy.md)
