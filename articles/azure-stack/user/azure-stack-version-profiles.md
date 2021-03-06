---
title: Управление профилями версий API в Azure Stack | Документация Майкрософт
description: Сведения о профилях версии API в Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: mabrigg
ms.reviewer: sijuman
ms.openlocfilehash: e568ffd2c3adb97ed0b727b85e7888fb797db1f9
ms.sourcegitcommit: 96089449d17548263691d40e4f1e8f9557561197
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34258215"
---
# <a name="manage-api-version-profiles-in-azure-stack"></a>Управление профилями версий API в Azure Stack

*Область применения: интегрированные системы Azure Stack и Пакет средств разработки Azure Stack*

Профили API определяют поставщик ресурсов Azure и версию API для конечных точек Azure REST. С помощью профилей API можно создать пользовательские клиенты на разных языках. Каждый клиент использует профиль API для связи с правильным поставщиком ресурсов и версией API для Azure Stack.

Вы можете создать приложение для работы с поставщиками ресурсов Azure без необходимости точно определять, какая версия каждого API поставщика ресурсов совместима с Azure Stack. Просто сопоставьте приложение с профилем. Пакет SDK отменит изменения до правильной версии API.

В этой статье содержатся сведения:

 - о профилях API для Azure Stack;
 - о том, как разрабатывать решения с их помощью;
 - о том, как найти руководство по написанию кода.

## <a name="summary-of-api-profiles"></a>Сводка по профилям API

- Профили API используются для представления набора поставщиков ресурсов Azure и их версий API.
- Профили API предназначены для разработчиков, создающих шаблоны в нескольких облаках Azure. Профили обеспечивают совместимый и стабильный интерфейс.
- Профили выпускаются четыре раза в год.
- Ниже перечислены три соглашения об именовании профилей.
    - **latest**  
        Содержит самые последние версии API, выпущенные в глобальной среде Azure.
    - **гггг-мм-дд-hybrid**  
    Этот выпуск (выходит два раза в год) обеспечивает согласованность и стабильность в нескольких облаках. Этот профиль предназначен для оптимальной совместимости с Azure Stack.
    - **гггг-мм-дд-profile** обеспечивает разумное соотношение между оптимальной стабильностью и новейшими функциями.

### <a name="azure-api-profiles-and-azure-stack-compatibility"></a>Профили API Azure и совместимость с Azure Stack

Новейшие профили API Azure несовместимы с Azure Stack. Можно использовать следующие соглашения об именовании для идентификации профилей, которые необходимо использовать для своих решений Azure Stack.

**latest**  
Этот профиль включает в себя последние версии API, доступные в глобальной среде Azure. Эти версии не будут работать в Azure Stack. Профиль **latest** содержит наибольшее количество критических изменений. Он не учитывает стабильность и совместимость с другими облаками. Если вам необходимы последние версии API, используйте профиль **latest**.

**гггг-мм-дд-hybrid**  
Этот профиль выпускается в марте и сентябре каждого года. Он обладает оптимальной стабильностью и совместимостью с различными облаками. Профиль **гггг-мм-дд-hybrid** предназначен как для глобальной среды Azure, так и для Azure Stack. Версии API Azure, указанные в этом профиле, соответствуют версиям, указанным в Azure Stack. Вы можете использовать этот профиль для разработки кода для гибридных облачных решений.

**yyyy-mm-dd-profile**  
Этот профиль выпускается в глобальной среде Azure в июне и декабре каждого года. Этот профиль не будет работать в Azure Stack. Как правило, он будет содержать большое число критических изменений. Хотя этот профиль не обладает оптимальной стабильностью и не содержит последних компонентов, различие между этим профилем и профилем **latest** состоит в том, что профиль **latest** всегда содержит последние версии API, независимо от того, когда они были выпущены. Например, если завтра будет выпущена новая версия API для вычислительных операций, эта версия API будет указана в профиле **latest**, но не будет указана в профиле **гггг-мм-дд-profile**, так как этот профиль уже существует.  Профиль **гггг-мм-дд-profile** охватывает большинство последних версий, выпущенных до июня или декабря.

## <a name="azure-resource-manager-api-profiles"></a>Профили API Azure Resource Manager

Azure Stack не использует последнюю версию из версий API в глобальной среде Azure. При создании решения необходимо найти версию API для каждого поставщика ресурсов Azure, которая совместима с Azure Stack.

Вместо исследования каждого поставщика ресурсов и определенной версии, поддерживаемой Azure Stack, можно использовать профиль API. Профиль определяет набор поставщиков ресурсов и версий API. Пакет SDK или инструмент, созданный с его помощью, выполнит откат до целевой версии API, указанной в профиле. С помощью профилей API можно указать версию профиля, которая применяется ко всему шаблону, а в среде выполнения Azure Resource Manager выберет правильную версию ресурса.

Профили API работают с инструментами, которые используют Azure Resource Manager, такими как PowerShell, Azure CLI, предоставленный в пакете SDK код и Microsoft Visual Studio. Инструменты и пакеты SDK могут использовать профили, чтобы определить, какую версию модулей и библиотек следует включать при создании приложения.

**Сценарий разработки с использованием профиля**  
Предположим, что вы используете PowerShell для создания следующих компонентов.

* Учетная запись хранения, которая использует поставщик ресурсов **Microsoft.Storage**, поддерживающий версию API 2016-03-30.
* Виртуальная машина, которая использует поставщик ресурсов **Microsoft.Compute**, поддерживающий версию API 2015-12-01.

Вместо того, чтобы искать и устанавливать модули PowerShell, которые поддерживают эти версии API, необходимые для ресурсов хранения и вычислительных ресурсов, можно использовать профиль. Используйте командлет **Install-Profile *profilename***, и PowerShell скачает правильные версии модулей.

Аналогичным образом при использовании пакета SDK для Python, чтобы создать приложение на основе Python, можно указать профиль. Пакет SDK загружает правильные модули для поставщиков ресурсов, которые указаны в сценарии.

Разработчик может сосредоточиться на написании решения. Можно использовать профиль, зная, что код будет выполняться во всех облаках, которые поддерживают этот профиль.

## <a name="api-profile-code-samples"></a>Примеры кода для профиля API

Вы можете найти примеры кода, которые помогут интегрировать решение с предпочитаемым языком с помощью Azure Stack, используя профили. В настоящее время руководства и примеры можно найти для следующих языков:

- **PowerShell**  
Вы можете использовать модуль **AzureRM.Bootstrapper**, доступный в коллекции PowerShell, чтобы получить командлеты PowerShell, необходимые для работы с профилями версий API. Дополнительные сведения см. в статье [Use API version profiles for PowerShell in Azure Stack](azure-stack-version-profiles-powershell.md) (Использование профилей версии API для PowerShell в Azure Stack).
- **Azure CLI 2.0**  
Укажите в конфигурации среды версию API-интерфейса, специально предназначенную для Azure Stack. Дополнительные сведения см. в статье [Use API version profiles with Azure CLI 2.0 in Azure Stack](azure-stack-version-profiles-azurecli2.md) (Использование профилей версии API для PowerShell в Azure CLI 2.0).
- **GO**  
В пакете SDK для GO профиль является сочетанием различных типов ресурсов с разными версиями различных служб. Профили доступны в пути profiles/ с версией в формате **ГГГГ-ММ-ДД**. Дополнительные сведения см. в статье [Использование профилей версии API в Go](azure-stack-version-profiles-go.md).
- **Ruby**  
Пакет SDK Ruby для Azure Stack Resource Manager предоставляет средства для создания инфраструктуры и управления ей. Поставщики ресурсов в пакете SDK включают вычисления, виртуальные сети и хранилища на языке Ruby. Дополнительные сведения см. в статье [Использование профилей версии API в Ruby](azure-stack-version-profiles-ruby.md).

## <a name="next-steps"></a>Дополнительная информация

* [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)
* [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md) (Настройка пользовательской среды PowerShell в Azure Stack)
* [Resource provider API versions supported by profiles in Azure Stack](azure-stack-profiles-azure-resource-manager-versions.md) (Версии API поставщика ресурсов, поддерживаемые профилями в Azure Stack).
