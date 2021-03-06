---
title: Управление устройствами в приложении Azure IoT Central | Документация Майкрософт
description: Как оператор вы узнаете, как осуществлять управление устройствами в приложении Azure IoT Central.
services: iot-central
author: ellenfosborne
ms.author: elfarber
ms.date: 01/21/2018
ms.topic: article
ms.prod: microsoft-iot-central
manager: timlt
ms.openlocfilehash: 75472d701160e7cfd331d01efcdc1a19ae20fb2d
ms.sourcegitcommit: 688a394c4901590bbcf5351f9afdf9e8f0c89505
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/18/2018
ms.locfileid: "34303585"
---
# <a name="manage-devices-in-your-azure-iot-central-application"></a>Управление устройствами в приложении Azure IoT Central

В этой статье описывается, как оператор может управлять устройствами в приложении Microsoft Azure IoT Central. Как оператор вы можете:

- Использовать страницу **Explorer**, чтобы просматривать, добавлять и удалять устройства, подключенные к приложению Azure IoT Central.
- Поддерживать актуальность сведений об используемых устройствах.
- Поддерживать актуальность метаданных устройства путем изменения значений, хранимых в свойствах устройства.
- Управлять поведением устройств, обновляя параметр конкретного устройства на странице **Параметры**.

## <a name="view-your-devices"></a>Просмотр устройств

Чтобы просмотреть отдельное устройство, сделайте следующее:

1. В меню навигации слева щелкните **Explorer**. Отобразится список [шаблонов устройств](howto-set-up-template.md).

1. На панели слева выберите **Device Template** (Шаблон устройства).

1. На панели справа отобразится список устройств, созданных с использованием данного шаблона устройства. Выберите одно устройство, чтобы просмотреть для него страницу **Сведения об устройстве**:

    [![Страница сведений об устройстве](./media/howto-manage-devices/image1.png)](./media/howto-manage-devices/image1.png#lightbox)

## <a name="add-a-device"></a>Добавление устройства

Чтобы добавить устройство в приложение Azure IoT Central, сделайте следующее:

1. В меню навигации слева щелкните **Explorer**.

1. Выберите шаблон устройства, на основе которого требуется создать устройство.

1. Выберите **+ Создать**.

1. Выберите **Real** (Реальное) или **Simulated** (Имитированное). Под реальным устройством подразумевается физическое устройство, подключаемое к приложению Azure IoT Central. Имитированное устройство содержит образцы данных, созданные в Azure IoT Central. В этом примере используется реальное устройство. Выберите **Real** (Реальное), чтобы открыть страницу **Сведения об устройстве** для нового устройства.


## <a name="bulk-import-devices"></a>Массовый импорт устройств

Для подключения к приложению большого количества устройств Azure IoT Central предоставляет функцию массового импорта устройств с помощью CSV-файла. 

Требования к файлу CSV:
1. В CSV-файле должен быть только один столбец, содержащий идентификаторы устройств.

1. Файл не должен содержать заголовок.


Для массовой регистрации устройств в приложении сделайте следующее:

1. В меню навигации слева щелкните **Explorer**.

1. На левой панели выберите шаблон устройства, для которого требуется выполнить массовое создание устройств.

1. Выберите **Создать** и щелкните **Bulk Import** (Массовый импорт).

    [![Действие массового импорта](./media/howto-manage-devices/BulkImport1.png)](./media/howto-manage-devices/BulkImport1.png#lightbox)

1. Выберите CSV-файл, содержащий список идентификаторов устройств, которые нужно импортировать.

1. Импорт устройств начнется сразу после передачи файла. Вы можете отслеживать состояние импорта в верхней сетке устройств.

1. После завершения импорта в сетке устройств отображается сообщение об успешном выполнении.

    [![Успешное завершение массового импорта](./media/howto-manage-devices/BulkImport3.png)](./media/howto-manage-devices/BulkImport3.png#lightbox)

Если операция импорта устройств завершается ошибкой, ошибка отображается в сетке устройств. Все ошибки записываются в файл журнала. Его можно скачать, щелкнув сообщение об ошибке.



## <a name="delete-a-device"></a>Удалить устройство.

Чтобы удалить реальное или имитированное устройство из приложения Azure IoT Central, сделайте следующее:

1. В меню навигации щелкните **Explorer**.

1. Выберите шаблон устройства, которое требуется удалить.

1. Установите флажок рядом с устройством, которое нужно удалить.

1. Щелкните **Удалить**.

## <a name="change-a-device-setting"></a>Изменение параметров устройства

С помощью параметров можно контролировать поведение устройства. Другими словами, параметры позволяют предоставлять входные данные устройству. Вы можете просмотреть и обновить параметры устройства на странице **Сведения об устройстве**.

1. В меню навигации щелкните **Explorer**.

1. Выберите шаблон устройства, параметры которого требуется изменить.

1. Перейдите на вкладку **Параметры** . Здесь отобразятся все настроенные для устройства параметры, а также их текущие значения. Вы можете проверить, для каких параметров в данный момент выполняется синхронизация.

1. Задайте для параметров необходимые значения. Вы можете одновременно изменить и обновить несколько параметров.

1. Выберите **Обновить**. Значения отправляются на устройство. Когда устройство подтверждает изменение параметра, состояние параметра изменяется на **синхронизировано**.

## <a name="change-a-property"></a>Изменение свойства

Свойства являются метаданными, связанными с этим устройством (например, город и серийный номер): Вы можете просмотреть и обновить свойства на странице **Сведения об устройстве**.

1. В меню навигации щелкните **Explorer**.

1. Выберите шаблон устройства, свойства которого требуется изменить.

1. Выберите вкладку **Свойства**. На этой вкладке можно просмотреть все свойства.

1. Задайте для свойств необходимые значения. Вы можете одновременно изменить и обновить несколько свойств.

1. Выберите **Обновить**.

> [!NOTE]
> Вы не можете изменить значение _свойств устройства_. Свойства устройства устанавливаются самим устройством и доступны только для чтения в приложении Azure IoT Central.

## <a name="next-steps"></a>Дополнительная информация

Вы узнали, как управлять устройством в приложении Azure IoT Central, а значит вы готовы к следующему шагу.

> [!div class="nextstepaction"]
> [Использование наборов устройств](howto-use-device-sets.md)

<!-- Next how-tos in the sequence -->
