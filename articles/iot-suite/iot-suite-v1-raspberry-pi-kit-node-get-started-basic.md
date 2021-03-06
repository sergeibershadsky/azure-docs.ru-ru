---
title: "Подключение устройства Raspberry Pi с физическими датчиками к Azure IoT Suite с помощью Node.js | Документация Майкрософт"
description: "Используйте начальный набор Microsoft Azure IoT для Raspberry Pi 3, а также Azure IoT Suite. С помощью Node.js вы можете подключать устройства Raspberry Pi к решению для удаленного мониторинга, отправлять данные телеметрии с датчиков в облако, а также реагировать на методы, вызываемые на панели мониторинга этого решения."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: 9bb4f62b1a3de68ce8796b60fe76cd97b9ab9ade
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="connect-your-raspberry-pi-3-to-the-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a>Подключение устройства Raspberry Pi 3 к решению для удаленного мониторинга и отправка данных телеметрии с физического датчика с помощью Node.js

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-selector](../../includes/iot-suite-v1-raspberry-pi-kit-selector.md)]

В этом руководстве показано, как использовать начальный набор Microsoft Azure IoT для Raspberry Pi 3 при разработке средства для считывания температуры и влажности, которое может обмениваться данными с облаком. В руководстве используются следующие ресурсы:

- Операционная система Raspbian, язык программирования Node.js и пакет SDK Microsoft Azure IoT для Node.js для реализации примера устройства.
- Предварительно настроенное решение для удаленного мониторинга IoT Suite в качестве облачного сервера.

## <a name="overview"></a>Обзор

В этом руководстве выполняются следующие шаги:

- Развертывание экземпляра предварительно настроенного решения удаленного мониторинга в подписке Azure. На этом шаге автоматически разворачивается и настраивается несколько служб Azure.
- Настройка устройства и датчиков для взаимодействия с компьютером и решением для удаленного мониторинга.
- Обновление кода примера устройства для подключения к решению для удаленного мониторинга и отправка данных телеметрии, которые можно просмотреть на панели мониторинга решения.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prerequisites](../../includes/iot-suite-v1-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-v1-provision-remote-monitoring](../../includes/iot-suite-v1-provision-remote-monitoring.md)]

> [!WARNING]
> Решение для удаленного мониторинга подготавливает набор служб Azure в подписке Azure. Развертывание отражает реальную корпоративную архитектуру. Чтобы избежать ненужных расходов на использование ресурсов Azure, удалите экземпляр предварительно настроенного решения на сайте azureiotsuite.com после завершения работы с ним. Если предварительно настроенное решение понадобится снова, его можно легко восстановить. Дополнительные сведения о сокращении затрат во время выполнения решения для удаленного мониторинга см. в статье [Configuring Azure IoT Suite preconfigured solutions for demo purposes][lnk-demo-config] (Настройка предварительно настроенных решений Azure IoT Suite для демонстрационных целей).

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-solution](../../includes/iot-suite-v1-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-v1-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-the-sample"></a>Скачивание и настройка примера

Теперь можно скачать и настроить клиентское приложение для удаленного мониторинга на устройстве Raspberry Pi.

### <a name="install-nodejs"></a>Установка Node.js

Установите Node.js на устройстве Raspberry Pi. Для пакета SDK IoT для Node.js требуется версия Node.js 0.11.5 или более поздняя. Ниже описывается установка Node.js версии 6.10.2 на устройстве Raspberry Pi.

1. Чтобы обновить устройство Raspberry Pi, используйте следующую команду:

    ```sh
    sudo apt-get update
    ```

1. Чтобы скачать двоичные файлы Node.js на устройство Raspberry Pi, используйте следующую команду:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Чтобы установить эти двоичные файлы, используйте следующую команду:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Чтобы убедиться в успешной установке Node.js версии 6.10.2, используйте следующую команду:

    ```sh
    node --version
    ```

### <a name="clone-the-repositories"></a>Клонирование репозиториев

Клонируйте необходимые репозитории (если вы еще не сделали этого), выполнив следующие команды на устройстве Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-the-device-connection-string"></a>Обновление строки подключения устройства

Откройте исходный файл примера в редакторе **nano**, используя следующую команду:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Найдите следующую строку:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Замените значения заполнителей сведениями об устройстве и Центре Интернета вещей, созданными и сохраненными в начале этого руководства. Сохраните изменения (клавиши **CTRL+O**, **ВВОД**) и закройте редактор (клавиши **CTRL+X**).

## <a name="run-the-sample"></a>Запуск примера

Чтобы установить пакеты необходимых компонентов для примера, выполните следующие команды:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

Теперь вы можете запустить пример программы на устройстве Raspberry Pi. Введите команду:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Следующий пример с выходными данными отобразится в командной строке на устройстве Raspberry Pi:

![Выходные данные приложения Raspberry Pi][img-raspberry-output]

Вы можете в любое время нажать комбинацию клавиш **CTRL+C**, чтобы выйти из программы.

[!INCLUDE [iot-suite-v1-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-v1-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные примеры и документацию по Azure IoT можно найти в [Центре разработчиков Azure IoT](https://azure.microsoft.com/develop/iot/).

[img-raspberry-output]: ./media/iot-suite-v1-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
