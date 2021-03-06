---
title: Подготовка сертификатов инфраструктуры открытых ключей Azure Stack для развертывания интегрированных систем Azure Stack | Документация Майкрософт
description: В этой статье описано, как подготовить сертификаты PKI Azure Stack для интегрированных систем Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2018
ms.author: mabrigg
ms.reviewer: ppacent
ms.openlocfilehash: 934585082e2832c41885874c82ab43d64a1fa361
ms.sourcegitcommit: c47ef7899572bf6441627f76eb4c4ac15e487aec
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33203482"
---
# <a name="prepare-azure-stack-pki-certificates-for-deployment"></a>Подготовка сертификатов PKI Azure Stack к развертыванию
Файлы сертификатов, [полученные из выбранного центра сертификации](azure-stack-get-pki-certs.md), необходимо импортировать и экспортировать со свойствами, которые соответствуют требованиям к сертификату Azure Stack.


## <a name="prepare-certificates-for-deployment"></a>Подготовка сертификатов к развертыванию
Для подготовки и проверки сертификатов PKI Azure Stack выполните следующие действия: 

### <a name="import-the-certificate"></a>Импорт сертификата

1.  Скопируйте исходные версии сертификатов, [полученные из выбранного центра сертификации](azure-stack-get-pki-certs.md), в каталог на узле развертывания. 
  > [!WARNING]
  > Не копируйте файлы, которые уже были импортированы, экспортированы или изменены каким-либо образом относительно файлов, предоставленных непосредственно центром сертификации.

2.  Щелкните правой кнопкой мыши сертификат и выберите **Установить сертификат** или **Установить PFX**, в зависимости от того, как был доставлен сертификат из ЦС.

3. В окне **Мастер импорта сертификатов** выберите **Локальный компьютер** в качестве расположения импорта. Щелкните **Далее**. На следующем экране еще раз нажмите кнопку "Далее".

    ![Расположение импорта на локальном компьютере](.\media\prepare-pki-certs\1.png)

4.  Выберите **Place all certificate in the following store** (Поместить все сертификаты в следующее хранилище), а затем укажите **Доверительные отношения в предприятии** в качестве расположения. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно выбора хранилища сертификатов, а затем нажмите кнопку **Далее**.

    ![Настройка хранилища сертификатов](.\media\prepare-pki-certs\3.png)

    a. При импорте PFX-файла отобразится дополнительное диалоговое окно. На странице **Защита с помощью закрытого ключа** введите пароль для файлов сертификатов, а затем установите флажок **Mark this key as exportable. This allows you to back up or transport your keys at a later time** (Пометить этот ключ как доступный для экспорта. Это позволит позднее создать резервную копию ваших ключей или перенести их). Щелкните **Далее**.

    ![Пометка ключа доступным для экспорта](.\media\prepare-pki-certs\2.png)

5. Нажмите кнопку "Готово" для завершения импорта.

### <a name="export-the-certificate"></a>Экспорт сертификата

Откройте консоль MMC "Диспетчер сертификатов" и подключитесь к хранилищу сертификатов "Локальный компьютер".

1. Откройте консоль управления (MMC). В Windows 10 щелкните правой кнопкой мыши меню "Пуск", а затем щелкните "Выполнить". Введите **mmc** нажмите кнопку "ОК".

2. Щелкните "Файл" > "Добавить или удалить оснастку", затем выберите "Сертификаты" и нажмите кнопку "Добавить".

    ![Добавление оснастки "Сертификаты"](.\media\prepare-pki-certs\mmc-2.png)
 
3. Выберите учетную запись "Компьютер", нажмите кнопку "Далее", затем выберите "Локальный компьютер" и нажмите кнопку "Готово". Нажмите кнопку "ОК", чтобы закрыть страницу "Добавить или удалить оснастку".

    ![Добавление оснастки "Сертификаты"](.\media\prepare-pki-certs\mmc-3.png)

4. Выберите "Сертификаты" > "Доверительные отношения в предприятии" > "Расположение сертификата". Убедитесь, что сертификат отображается в области справа.

5. На панели задач консоли "Диспетчер сертификатов" выберите **Действия** > **Все задачи** > **Экспорт**. Щелкните **Далее**.

  > [!NOTE]
  > В зависимости от того, сколько у вас сертификатов Azure Stack, может потребоваться выполнить этот процесс более одного раза.

4. Выберите **Yes, Export the Private Key** (Да, экспортировать закрытый ключ), а затем нажмите кнопку **Далее**.

5. В разделе "Формат экспортируемого файла" выберите **Export all Extended Properties** (Экспортировать все расширенные свойства) и нажмите кнопку **Далее**.

6. Выберите **Пароль** и укажите пароль для сертификатов. Запомните этот пароль, так как он используется в качестве параметра развертывания. Щелкните **Далее**.

7. Выберите имя и расположение для экспортируемого PFX-файла. Щелкните **Далее**.

8. Выберите **Готово**.

## <a name="next-steps"></a>Дополнительная информация
[Validate Azure Stack PKI certificates](azure-stack-validate-pki-certs.md) (Проверка сертификатов PKI Azure Stack)