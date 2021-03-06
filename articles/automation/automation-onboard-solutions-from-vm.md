---
title: Сведения о том, как подключить решения для управления обновлениями, отслеживания изменений и инвентаризации на виртуальной машине Azure
description: Сведения о том, как на виртуальной машине Azure подключить решения для управления обновлениями, отслеживания изменений и инвентаризации, входящие в состав службы автоматизации Azure
services: automation
author: georgewallace
ms.author: gwallace
ms.date: 04/25/2018
ms.topic: conceptual
ms.service: automation
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 2fbfd733a57d0e2f91d119b614917abf172b8379
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34193100"
---
# <a name="onboard-update-management-change-tracking-and-inventory-solutions-from-an-azure-virtual-machine"></a>Подключение решений для управления обновлениями, отслеживания изменений и инвентаризации на виртуальной машине Azure

Служба автоматизации Azure предоставляет решения для управления обновлениями безопасности операционной системы, отслеживания изменений и инвентаризации компонентов, установленных на компьютерах. Существует несколько способов подключения решений на компьютерах. Подключить решение можно с виртуальной машины, [из учетной записи службы автоматизации](automation-onboard-solutions-from-automation-account.md) или с помощью модуля [runbook](automation-onboard-solutions.md). В этой статье рассматривается подключение таких решений c виртуальной машины Azure.

## <a name="log-in-to-azure"></a>Вход в Azure

Войдите в Azure: https://portal.azure.com

## <a name="enable-the-solutions"></a>Включение решений

Перейдите к существующей виртуальной машине и выберите в разделе **Операции** один из пунктов: **Управление обновлениями**, **Инвентаризация** или **Отслеживание изменений**.

Чтобы включить решение, выберите рабочую область Log Analytics и учетную запись службы автоматизации, а затем щелкните **Включить**. Процесс включения решения может занять до 15 минут.

![Подключение решения по обновлению](media/automation-onboard-solutions-from-vm/onboard-solution.png)

Перейдите к другим решениям и нажмите кнопку **Включить**. Раскрывающиеся поля Log Analytics и учетной записи службы автоматизации отключены, так как в них используются те же рабочая область и учетная запись автоматизации, что и в ранее включенном решении.

![Подключение решения по обновлению](media/automation-onboard-solutions-from-vm/onboard-solutions2.png)

> [!NOTE]
> Для **отслеживания изменений** и **инвентаризации** используется одно и то же решение — при включение одного параметра включается и другой.

## <a name="scope-configuration"></a>Конфигурация области

В каждом решении используется конфигурация области в пределах рабочей области для определения целевых компьютеров, на которых будет внедрено решение. Конфигурация области представляет собой группу из одного или нескольких сохраненных поисковых запросов, которая используется для ограничения области применения решения к конкретным компьютерам. Для доступа к конфигурациям области в учетной записи службы автоматизации в разделе **Связанные ресурсы** выберите **Рабочая область**. Затем в рабочей области **Источники данных рабочей области** выберите **Конфигурации области**.

Если в выбранной рабочей области еще нет решений "Управление обновлениями" или "Отслеживание изменений", создаются следующие конфигурации области:

* **MicrosoftDefaultScopeConfig-ChangeTracking**;

* **MicrosoftDefaultScopeConfig-Updates**.

Если выбранная рабочая область уже имеет решение, решение повторно не развертывается и к нему не добавляется конфигурация области.

Нажмите кнопку с многоточием (…) для любой из конфигураций и выберите **Изменить**. На странице **Изменение конфигурации области** выберите **Select Computer Groups** (Выбор групп компьютеров), чтобы открыть страницу **Группы компьютеров**. На этой странице отображаются сохраненные поисковые запросы, которые используются для создания конфигурации области.

## <a name="saved-searches"></a>Сохраненные поисковые запросы

При добавлении компьютера в решениях "Управление обновлениями" или "Отслеживание изменений" и "Инвентаризация" он добавляется в один из двух сохраненных поисковых запросов в рабочей области. Эти сохраненные поисковые запросы содержат компьютеры, которым будут назначены соответствующие решения.

Перейдите к своей рабочей области и выберите **Сохраненные поисковые запросы** в разделе **Общие**. Два сохраненных поисковых запроса, используемые в этих решениях, показаны в следующей таблице:

|ИМЯ     |Категория  |Alias  |
|---------|---------|---------|
|MicrosoftDefaultComputerGroup     |  ChangeTracking       | ChangeTracking__MicrosoftDefaultComputerGroup        |
|MicrosoftDefaultComputerGroup     | Обновления        | Updates__MicrosoftDefaultComputerGroup         |

Выберите один из сохраненных поисковых запросов, чтобы просмотреть запрос, используемый для заполнения группы. На следующем рисунке показан запрос и его результаты.

![Сохраненные поисковые запросы](media/automation-onboard-solutions-from-vm/logsearch.png)

## <a name="next-steps"></a>Дополнительная информация

Чтобы узнать, как использовать то или иное решение, ознакомьтесь с соответствующими руководствами.

* [Управление обновлениями Windows в службе автоматизации Azure](automation-tutorial-update-management.md)

* [Получение данных об установленном программном обеспечении на виртуальных машинах Azure и других компьютерах](automation-tutorial-installed-software.md)

* [Устранение неполадок при изменениях в среде](automation-tutorial-troubleshoot-changes.md)
