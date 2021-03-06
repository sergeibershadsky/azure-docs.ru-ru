---
title: Имитация сбоя при обращении к избыточному хранилищу с доступом на чтение в Azure | Документация Майкрософт
description: Имитация ошибки при обращении к геоизбыточному хранилищу с доступом на чтение
services: storage
author: tamram
manager: jeconnoc
ms.service: storage
ms.tgt_pltfrm: na
ms.devlang: ''
ms.topic: tutorial
ms.date: 12/23/2017
ms.author: tamram
ms.openlocfilehash: a86f54d580db6e577b878cb1701c7b969d23c129
ms.sourcegitcommit: 6fcd9e220b9cd4cb2d4365de0299bf48fbb18c17
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/05/2018
---
# <a name="simulate-a-failure-in-accessing-read-access-redundant-storage"></a>Имитация сбоя при обращении к избыточному хранилищу с доступом на чтение

Это руководство представляет собой вторую часть цикла.  В этом руководстве вы можете с помощью [Fiddler](#simulate-a-failure-with-fiddler) или [статической маршрутизации](#simulate-a-failure-with-an-invalid-static-route) имитировать сбой запросов к основной конечной точке учетной записи [геоизбыточного хранилища с доступом на чтение](../common/storage-redundancy-grs.md#read-access-geo-redundant-storage) (RA-GRS) и проверить переключение приложения на вторичную конечную точку.

![Приложение для сценария](media/storage-simulate-failure-ragrs-account-app/scenario.png)

Чтобы выполнить инструкции этого руководства, сначала следует ознакомиться с предыдущим руководством по хранилищу: [Обеспечение высокой доступности данных приложений в хранилище Azure][previous-tutorial].

Из второй части цикла вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * запуск и приостановка приложения;
> * имитирование сбоя с использованием [fiddler](#simulate-a-failure-with-fiddler) или [недопустимого статического маршрута](#simulate-a-failure-with-an-invalid-static-route); 
> * имитация восстановления основной конечной точки.


## <a name="prerequisites"></a>предварительным требованиям

Для имитации сбоя с помощью Fiddler: 

* скачайте и [установите Fiddler](https://www.telerik.com/download/fiddler).

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="simulate-a-failure-with-fiddler"></a>Имитация сбоя с Fiddler

Для имитации сбоя с помощью Fiddler нужно внедрить неудачный ответ на запросы к основной конечной точке учетной записи RA-GRS.

Выполните следующие действия, чтобы имитировать сбой и восстановление основной конечной точки с помощью Fiddler.

### <a name="launch-fiddler"></a>Запуск Fiddler

Откройте Fiddler, выберите **Правила** и **Настроить правила**.

![Настройка правил Fiddler](media/storage-simulate-failure-ragrs-account-app/figure1.png)

Откроется средство Fiddler ScriptEditor, в котором отображается файл **SampleRules.js**. Этот файл используется для настройки Fiddler. Скопируйте приведенный ниже пример кода и вставьте его в функцию `OnBeforeResponse`. Новый код закомментирован, чтобы реализованная в нем логика не применялась немедленно. Внеся изменения, сохраните их с помощью меню **Файл** > **Сохранить**.

```javascript
    /*
        // Simulate data center failure
        // After it is successfully downloading the blob, pause the code in the sample,
        // uncomment these lines of script, and save the script.
        // It will intercept the (probably successful) responses and send back a 503 error. 
        // When you're ready to stop sending back errors, comment these lines of script out again 
        //     and save the changes.

        if ((oSession.hostname == "contosoragrs.blob.core.windows.net") 
            && (oSession.PathAndQuery.Contains("HelloWorld"))) {
            oSession.responseCode = 503;  
        }
    */
```

![Вставка настраиваемого правила](media/storage-simulate-failure-ragrs-account-app/figure2.png)

### <a name="start-and-pause-the-application"></a>Запуск и приостановка приложения

Запустите приложение в интегрированной среде разработки или текстовом редакторе. Когда приложение начнет чтение из основной конечной точки, нажмите **любую клавишу** в окне консоли, чтобы приостановить работу приложения.

### <a name="simulate-failure"></a>Имитация сбоя

Теперь, когда приложение приостановлено, раскомментируйте настраиваемое правило, сохраненное в Fiddler на предыдущем шаге. Этот пример кода отслеживает запросы к учетной записи хранения RA-GRS, и если путь содержит имя образа `HelloWorld`, возвращает код ответа `503 - Service Unavailable`.

Перейдите к Fiddler и выберите **Правила** -> **Настроить правила**.  Раскомментируйте приведенные ниже строки и замените `STORAGEACCOUNTNAME` именем вашей учетной записи хранения. Выберите **Файл** -> **Сохранить**, чтобы сохранить изменения. 

> [!NOTE]
> При выполнении примера приложения на платформе Linux необходимо перезапускать Fiddler каждый раз, когда изменяется файл **CustomRule.js**, чтобы Fiddler установил настраиваемую логику. 
> 
> 


```javascript
         if ((oSession.hostname == "STORAGEACCOUNTNAME.blob.core.windows.net")
         && (oSession.PathAndQuery.Contains("HelloWorld"))) {
         oSession.responseCode = 503;
         }
```

Чтобы возобновить работу приложения, нажмите **любую клавишу**.

Когда приложение продолжит работу, все запросы к основной конечной точке будут завершаться сбоем. Приложение выполнит пять попыток подключиться к основной конечной точке. Достигнув порогового значения (пять попыток), приложение запросит образ из вторичной конечной точки с доступом на чтение. После 20 успешных обращений для получения образа из вторичной конечной точки приложение снова попытается подключиться к основной конечной точке. Если основная конечная точка по-прежнему недоступна, приложение продолжит чтение из вторичной конечной точки. Этот алгоритм [прерывателя цепи](https://docs.microsoft.com/azure/architecture/patterns/circuit-breaker) мы описывали в предыдущем руководстве.

![Вставка настраиваемого правила](media/storage-simulate-failure-ragrs-account-app/figure3.png)

### <a name="simulate-primary-endpoint-restoration"></a>Имитация восстановления основной конечной точки

Пока в Fiddler настроен представленный выше набор правил, все запросы к основной конечной точке завершаются сбоем. Чтобы имитировать восстановление работоспособности основной конечной точки, удалите логику внедрения ошибки `503`.

Приостановите работу приложения, нажав **любую клавишу**.

Перейдите к Fiddler и выберите **Правила** > **Настроить правила**.  Закомментируйте или удалите настраиваемую логику в функции `OnBeforeResponse`, восстановив стандартный вид функции. Выберите **Файл** и **Сохранить**, чтобы сохранить изменения.

![Удаление настраиваемого правила](media/storage-simulate-failure-ragrs-account-app/figure5.png)

Завершив этот процесс, возобновите работу приложения, нажав **любую клавишу**. Приложение продолжит чтение из основной конечной точки, пока не выполнит 999 операций чтения.

![Возобновление работы приложения](media/storage-simulate-failure-ragrs-account-app/figure4.png)


## <a name="simulate-a-failure-with-an-invalid-static-route"></a>Имитирование сбоя с помощью недопустимого статического маршрута 
Вы можете создать недопустимый статический маршрут для всех запросов к основной конечной точке учетной записи хранения [геоизбыточного хранилища с доступом на чтение](../common/storage-redundancy-grs.md#read-access-geo-redundant-storage) (RA-GRS). В этом руководстве локальный узел используется в качестве шлюза для направления запросов в учетную запись хранения. Использование локального узла в качестве шлюза приводит к тому, что все запросы к основной конечной точке учетной записи хранения возвращаются обратно в узел, что впоследствии приводит к сбою. Выполните следующие действия, чтобы имитировать сбой и восстановление основной конечной точки с использованием недопустимого статического маршрута. 

### <a name="start-and-pause-the-application"></a>Запуск и приостановка приложения

Запустите приложение в интегрированной среде разработки или текстовом редакторе. Когда приложение начнет чтение из основной конечной точки, нажмите **любую клавишу** в окне консоли, чтобы приостановить работу приложения. 

### <a name="simulate-failure"></a>Имитация сбоя

Приостановите приложение, откройте командную строку в Windows с правами администратора или запустите терминал с правами привилегированного пользователя в Linux. Чтобы получить сведения о домене основной конечной точки учетной записи хранения, введите следующую команду в командной строке или терминале.

```
nslookup STORAGEACCOUNTNAME.blob.core.windows.net
``` 
 Замените `STORAGEACCOUNTNAME` именем своей учетной записи хранения. Скопируйте IP-адрес учетной записи хранения в текстовый редактор для последующего использования. Чтобы получить IP-адрес локального узла, введите `ipconfig` в командной строке Windows или `ifconfig` — в терминале Linux. 

Чтобы добавить статический маршрут для узла назначения, введите следующую команду в командной строке Windows или терминале Linux. 


# <a name="linuxtablinux"></a>[Linux](#tab/linux)

  route add <destination_ip> gw <gateway_ip>

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

  route add <destination_ip> <gateway_ip>

---
 
Замените `<destination_ip>` IP-адресом вашей учетной записи хранения, а `<gateway_ip>` — IP-адресом локального узла. Чтобы возобновить работу приложения, нажмите **любую клавишу**.

Когда приложение продолжит работу, все запросы к основной конечной точке будут завершаться сбоем. Приложение выполнит пять попыток подключиться к основной конечной точке. Достигнув порогового значения (пять попыток), приложение запросит образ из вторичной конечной точки с доступом на чтение. После 20 успешных обращений для получения образа из вторичной конечной точки приложение снова попытается подключиться к основной конечной точке. Если основная конечная точка по-прежнему недоступна, приложение продолжит чтение из вторичной конечной точки. Этот алгоритм [прерывателя цепи](/azure/architecture/patterns/circuit-breaker.md) мы описывали в предыдущем руководстве.

### <a name="simulate-primary-endpoint-restoration"></a>имитация восстановления основной конечной точки.

Для повторной имитации восстановления работы основной конечной точки удалите ее статический маршрут из таблицы маршрутизации. Таким образом все запросы к основной конечной точке смогут направляться через шлюз по умолчанию. 

Чтобы удалить статический маршрут для узла назначения (учетной записи хранения), введите следующую команду в командной строке Windows или терминале Linux. 
 
# <a name="linuxtablinux"></a>[Linux](#tab/linux)

route del <destination_ip> gw <gateway_ip>

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

route delete <destination_ip>

---

Чтобы возобновить работу приложения, нажмите **любую клавишу**. Приложение продолжит чтение из основной конечной точки, пока не выполнит 999 операций чтения.

![Возобновление работы приложения](media/storage-simulate-failure-ragrs-account-app/figure4.png)


## <a name="next-steps"></a>Дополнительная информация

Во второй части этой серии руководств вы научились имитировать сбой для проверки алгоритма обращения к геоизбыточному хранилищу с доступом на чтение, в том числе выполнили следующие операции:

> [!div class="checklist"]
> * запуск и приостановка приложения;
> * имитирование сбоя с использованием [fiddler](#simulate-a-failure-with-fiddler) или [недопустимого статического маршрута](#simulate-a-failure-with-an-invalid-static-route); 
> * имитация восстановления основной конечной точки.

Ознакомьтесь с указанной ниже статьей, чтобы получить дополнительные сведения о работе хранилища RA-GRS (и связанных рисках).

> [!div class="nextstepaction"]
> [Разработка высокодоступных приложений c помощью RA-GRS](../common/storage-designing-ha-apps-with-ragrs.md)

[previous-tutorial]: storage-create-geo-redundant-storage.md