---
title: Изменение размера виртуальной машины Windows в классической модели развертывания Azure | Документация Майкрософт
description: Изменение размера виртуальной машины Windows, созданной в классической модели развертывания, с использованием Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: Drewm3
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 6afc8125462a659d0892e7dbb53f1f71789815cc
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2018
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a>Изменение размера виртуальной машины Windows, созданной в классической модели развертывания
В этой статье описано изменение размера виртуальной машины Windows, созданной в классической модели развертывания, с использованием Azure Powershell.

Собираясь изменять размер виртуальной машины, обратите внимание на два фактора, которые определяют диапазон размеров, доступных для виртуальной машины. Первый фактор — регион, в котором развернута виртуальная машина. Список размеров виртуальных машин, доступных в регионе, находится на вкладке "Службы" веб-страницы "Регионы Azure". Второй фактор — физическое оборудование, на котором размещена виртуальная машина. Физические серверы, на которых размещены виртуальные машины, группируются в кластеры общего физического оборудования. Метод изменения размера виртуальной машины зависит от того, поддерживает ли оборудование кластера, в котором размещена виртуальная машина, новый размер.

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../../../resource-manager-deployment-model.md). В этой статье рассматривается использование классической модели развертывания. Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов. Кроме того, можно [изменить размер виртуальной машины, созданной с использованием модели развертывания на основе Resource Manager](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Добавление учетной записи
Для работы с классическими ресурсами Azure необходимо настроить Azure PowerShell. Выполните следующие действия, чтобы настроить Azure PowerShell для управления классическими ресурсами.

1. В командной строке PowerShell введите `Add-AzureAccount` и нажмите клавишу **ВВОД**. 
2. Введите адрес электронной почты, связанный с подпиской Azure, и нажмите кнопку **Продолжить**. 
3. Введите пароль к учетной записи. 
4. Щелкните **Войти**. 

## <a name="resize-in-the-same-hardware-cluster"></a>Изменение размеров в том же кластере оборудования
Чтобы изменить размер виртуальной машины до размера, доступного в кластере оборудования, в котором размещена машина, выполните следующие действия.

1. Выполните следующую команду PowerShell, чтобы получить список размеров виртуальных машин, доступных в оборудовании кластера облачной службы, в которой находится машина.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Выполните следующие команды, чтобы изменить размер виртуальной машины.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Изменение размера в новом кластере оборудования
Для изменения размера виртуальной машины до размера, недоступного в оборудовании кластера, в котором размещена эта виртуальная машина, необходимо заново создать облачную службу и все виртуальные машины в ней. Каждая облачная служба размещается в одном кластере оборудования, поэтому все виртуальные машины в облачной службе должны иметь размер, поддерживаемый этим кластером. Ниже описано изменение размера виртуальной машины путем удаления и повторного создания облачной службы.

1. Выполните следующую команду PowerShell, чтобы получить список размеров виртуальных машин, доступных в регионе. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Зафиксируйте все параметры каждой виртуальной машины в облачной службе, содержащей виртуальную машину, размер которой необходимо изменить. 
3. Удалите все виртуальные машины в облачной службе, выбрав параметр сохранения дисков для каждой виртуальной машины.
4. Повторно создайте виртуальную машину, размер которой следует изменить, указав необходимый размер машины.
5. Заново создайте все остальные виртуальные машины, которые были в облачной службе. При этом укажите размер виртуальной машины, доступный в кластере оборудования, в котором теперь размещается облачная служба.

Пример сценария для удаления и повторного создания облачной службы с использованием нового размера виртуальной машины можно найти [здесь](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Дополнительная информация
* [Resize a Windows VM](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Изменение размера виртуальной машины Windows).

