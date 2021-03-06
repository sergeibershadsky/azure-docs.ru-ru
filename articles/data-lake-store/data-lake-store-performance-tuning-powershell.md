---
title: Рекомендации по настройке производительности для использования PowerShell с Data Lake Store | Документация Майкрософт
description: Советы по повышению производительности при использовании Azure PowerShell с Data Lake Store.
services: data-lake-store
documentationcenter: ''
author: stewu
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.date: 01/09/2018
ms.author: stewu
ms.openlocfilehash: 7b19972ed4a75ac899a4b78b28ab36ba305a5a64
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="performance-tuning-guidance-for-using-powershell-with-azure-data-lake-store"></a>Рекомендации по настройке производительности для использования PowerShell с Azure Data Lake Store

В этой статье приведены свойства, настроив которые, можно повысить производительность при использовании PowerShell с Data Lake Store.

## <a name="performance-related-properties"></a>Свойства, связанные с производительностью

| Свойство            | значение по умолчанию | ОПИСАНИЕ |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Этот параметр позволяет выбрать количество параллельных потоков для отправки или скачивания каждого файла. Это количество представляет собой максимальное количество потоков, которые можно выделить для каждого файла. В зависимости от сценария количество потоков может быть меньше (например, при передаче файла размером 1 КБ вы получите один поток, даже если запросите 20 потоков).  |
| ConcurrentFileCount | 10      | Этот параметр предназначен для отправки или скачивания папок. Он определяет количество одновременно отправляемых или скачиваемых файлов. Это количество представляет собой максимальное количество файлов, которые можно передать или скачать одновременно. В зависимости от сценария количество параллельно передаваемых или скачиваемых файлов может быть меньше (например, при передаче двух файлов одновременно будут передаваться два файла, даже если запрошено 15). |

**Пример**

Эта команда скачивает файлы из Azure Data Lake Store на локальный диск пользователя, используя 20 потоков на один файл и 100 одновременно скачиваемых файлов.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

## <a name="how-do-i-determine-the-value-for-these-properties"></a>Как определить значения этих свойств?

Следующий вопрос, возможно, будет заключается в том, как определить, какое значение задать для свойств, связанных с производительностью. Ниже представлены некоторые полезные рекомендации.

* **Шаг 1. Определение общего числа потоков.** Сначала нужно определить общее число потоков, которые следует использовать. Как правило, следует использовать 6 потоков для каждого физического ядра.

        Total thread count = total physical cores * 6

    **Пример**

    Предположим, что вы выполняете команды PowerShell на виртуальной машине D14 с 16 ядрами.

        Total thread count = 16 cores * 6 = 96 threads


* **Шаг 2. Расчет значения параметра PerFileThreadCount.** Мы вычисляем значение параметра PerFileThreadCount на основе размера файлов. Для файлов размером менее 2,5 ГБ не нужно изменять этот параметр, так как значения по умолчанию 10 будет достаточно. Для файлов размером более 2,5 ГБ следует использовать 10 потоков для изначальных 2,5 ГБ и добавлять по 1 потоку для каждых дополнительных 256 МБ файла. При копировании папки с файлами разного размера рекомендуется разделить их на группы по схожим размерам. Использование файлов разных размеров может привести к снижению производительности. Если невозможно сгруппировать файлы по схожим размерам, следует задать значение параметра PerFileThreadCount в соответствии с максимальным размером файла.

        PerFileThreadCount = 10 threads for the first 2.5 GB + 1 thread for each additional 256 MB increase in file size

    **Пример**

    Предположим, что у вас есть 100 файлов размером от 1 до 10 ГБ. Мы используем файл размером 10 ГБ в качестве максимального размера файла в формуле следующего вида.

        PerFileThreadCount = 10 + ((10 GB - 2.5 GB) / 256 MB) = 40 threads

* **Шаг 3. Вычисление значения параметра ConcurrentFilecount.** Используйте общее число потоков и значение параметра PerFileThreadCount, чтобы вычислить значение параметра ConcurrentFileCount по следующей формуле.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Пример**

    На основе использованных примеров значений.

        96 = 40 * ConcurrentFileCount

    Таким образом значение **ConcurrentFileCount** — **2,4**, которое можно округлить до **2**.

## <a name="further-tuning"></a>Дополнительные настройки

Вам могут потребоваться дополнительные настройки, так как вы работаете с файлами разного размера. Вычисления выше подходят, если размер всех или большинства файлов больше 10 ГБ и ближе к этому значению. Однако если у вас есть множество файлов разных размеров (меньше 10 ГБ), можно уменьшить значение параметра PerFileThreadCount. Сделав так, мы увеличим значение ConcurrentFileCount. Таким образом, если предположить, что размер большей части файлов меньше 5 ГБ, можно повторно выполнить вычисления.

    PerFileThreadCount = 10 + ((5 GB - 2.5 GB) / 256 MB) = 20

Итак, значение **ConcurrentFileCount** равно 96/20 — 4,8, которое можно округлить до **4**.

Вы можете продолжить изменять значения этих параметров, уменьшая и увеличивая значение **PerFileThreadCount** в зависимости от размера файлов.

### <a name="limitation"></a>Ограничение

* **Число файлов меньше, чем значение ConcurrentFileCount.** Если количество отправляемых файлов меньше вычисленного значения **ConcurrentFileCount**, следует уменьшить значение **ConcurrentFileCount** в соответствии с числом файлов. Все остальные потоки можно использовать для увеличения значения **PerFileThreadCount**.

* **Слишком много потоков.** Указав слишком большое число потоков, не увеличивая размер кластера, вы рискуете снизить производительность. При переключении контекста в ЦП могут возникнуть конфликты.

* **Недостаточный уровень параллелизма.** Если уровень параллелизма недостаточный, кластер может быть слишком мал. Вы можете увеличить количество узлов в кластере, что повысит уровень параллелизма.

* **Ошибки регулирования.** При слишком высоком уровне параллелизма могут возникнуть ошибки регулирования. При этом необходимо уменьшить уровень параллелизма или обратиться к нам.

## <a name="next-steps"></a>Дополнительная информация
* [Использование Azure Data Lake Store для потребностей больших данных](data-lake-store-data-scenarios.md) 
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

