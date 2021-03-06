---
title: Использование эталонных данных для уточняющих запросов в Azure Stream Analytics
description: В этой статье описано использование эталонных данных для уточняющих запросов или корреляции в конструкторе запросов для заданий Azure Stream Analytics.
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 04/25/2018
ms.openlocfilehash: 6dd96ee96201b05e4b272214983e955fcc5b9125
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="using-reference-data-for-lookups-in-stream-analytics"></a>Использование эталонных данных для уточняющих запросов в Stream Analytics
Ссылочные данные (которые также называются таблицами подстановки) — это ограниченный набор данных, являющийся по своей сути статическим или медленно изменяющимся. Такие данные используются для выполнения уточняющего запроса или соотнесения с вашим потоком данных. Для использования ссылочных данных в задании Azure Stream Analytics обычно используется [соединение ссылочных данных](https://msdn.microsoft.com/library/azure/dn949258.aspx) в запросе. Служба Stream Analytics использует хранилище BLOB-объектов Azure как уровень хранилища для ссылочных данных. С помощью фабрики данных Azure ссылочные данные можно преобразовать и (или) скопировать в хранилище BLOB-объектов Azure из [любого числа облачных и локальных хранилищ данных](../data-factory/copy-activity-overview.md) для использования в качестве ссылочных данных. Ссылочные данные моделируются как последовательность больших двоичных объектов (с учетом конфигурации входных данных) в порядке возрастания даты и времени, указанных в имени большого двоичного объекта. Они добавляются **только** в конец последовательности, для чего используется **более поздние** дата и время, чем в последнем большом двоичном объекте в последовательности.

В Stream Analytics есть **ограничение в 100 МБ на большой двоичный объект**. При этом задания могут обрабатывать несколько ссылочных больших двоичных объектов с помощью свойства **path pattern**.

Для ссылочных данных сжатие не поддерживается. 

## <a name="configuring-reference-data"></a>Настройка ссылочных данных
Чтобы настроить **ссылочные данные**, необходимо сначала создать входные данные соответствующего типа. В таблице ниже описано каждое свойство, которое необходимо указать во время создания входных ссылочных данных.


<table>
<tbody>
<tr>
<td>Имя свойства</td>
<td>ОПИСАНИЕ</td>
</tr>
<tr>
<td>Псевдоним входных данных</td>
<td>Понятное имя, с помощью которого запрос задания будет ссылаться на эти входные данные.</td>
</tr>
<tr>
<td>Учетная запись хранения</td>
<td>Имя учетной записи хранения, в которой находятся большие двоичные объекты. Если учетная запись расположена в одной подписке с заданием Stream Analytics, то ее имя можно выбрать из раскрывающегося списка.</td>
</tr>
<tr>
<td>Ключ учетной записи хранения</td>
<td>Секретный ключ, связанный с учетной записью хранения. Заполняется автоматически, если учетная запись хранения расположена в одной подписке с заданием Stream Analytics.</td>
</tr>
<tr>
<td>Контейнер хранилища</td>
<td>Контейнеры обеспечивают логическую группировку BLOB-объектов, хранящихся в службе BLOB-объектов Microsoft Azure. При передаче BLOB-объекта в службу BLOB-объектов для него необходимо указать контейнер.</td>
</tr>
<tr>
<td>Шаблон пути</td>
<td>Путь, используемый для поиска больших двоичных объектов в указанном контейнере. В пути можно указать один или несколько экземпляров следующих двух переменных:<BR>{date}, {time}<BR>Пример 1: products/{date}/{time}/product-list.csv<BR>Пример 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Формат даты (необязательное свойство)</td>
<td>Если в указанном шаблоне пути использовалась переменная {date}, то из раскрывающегося списка поддерживаемых форматов можно выбрать формат даты для упорядочивания больших двоичных объектов.<BR>Например: ГГГГ/ММ/ДД, ММ/ДД/ГГГГ и т. д.</td>
</tr>
<tr>
<td>Формат времени (необязательное свойство)</td>
<td>Если в указанном шаблоне пути использовалась переменная {time}, то из раскрывающегося списка поддерживаемых форматов можно выбрать формат времени для упорядочивания больших двоичных объектов.<BR>Примеры: ЧЧ, ЧЧ/мм или ЧЧ-мм.</td>
</tr>
<tr>
<td>Формат сериализации событий</td>
<td>Чтобы запросы работали как следует, в задании Stream Analytics нужно указать, какой формат сериализации используется для потоков входящих данных. Поддерживаемые форматы для ссылочных данных: CSV и JSON.</td>
</tr>
<tr>
<td>Кодирование</td>
<td>В настоящее время единственным поддерживаемым форматом кодирования является UTF-8.</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Создание ссылочных данных по расписанию
Если ссылочные данные являются медленно изменяющимся набором данных, вы можете включить поддержку обновления ссылочных данных. Для этого укажите соответствующий шаблон пути во входной конфигурации, используя токены подстановки {date} и {time}. На основе этого свойства path pattern служба Stream Analytics будет выбирать обновленные определения ссылочных данных. Например, шаблон `sample/{date}/{time}/products.csv` с форматом даты **ГГГГ-ММ-ДД** и форматом времени **ЧЧ:ММ** указывает службе Stream Analytics выбрать обновленный большой двоичный объект `sample/2015-04-16/17-30/products.csv` в 17:30 16 апреля 2015 г. в часовом поясе UTC.

> [!NOTE]
> В настоящее время задания Stream Analytics ищут обновления больших двоичных объектов, только если время, закодированное в имени большого двоичного объекта, отстает от времени компьютера. Например, задание будет искать `sample/2015-04-16/17-30/products.csv` как можно раньше, но не ранее 17:30 16 апреля 2015 г. в часовом поясе UTC. Оно *никогда* не будет искать большой двоичный объект, закодированное имя которого опережает время в имени последнего обнаруженного большого двоичного объекта.
> 
> (например, Когда задание находит большой двоичный объект `sample/2015-04-16/17-30/products.csv`, оно игнорирует любые файлы, в именах которых закодирована дата, предшествующая 17:30 16 апреля 2015 г. Поэтому, если в этом же контейнере большой двоичный объект `sample/2015-04-16/17-25/products.csv` создается позже, задание не будет его использовать.
> 
> Аналогичным образом, если `sample/2015-04-16/17-30/products.csv` создается в 22:03 16 апреля 2015 г., но в контейнере нет большого двоичного объекта с более ранней датой, задание будет использовать этот файл начиная с 22:03 16 апреля 2015 г., а до этого времени будет использовать ссылочные данные за прошедшее время.
> 
> Исключение составляют случаи, когда заданию необходимо повторно обработать данные за прошлые периоды или когда задание запускается впервые. В начале выполнения задание ищет самый новый большой двоичный объект, созданный до указанного времени запуска задания. Это позволяет обеспечить наличие **непустого** набора ссылочных данных на момент начала задания. Если его не удалось найти, задание будет показывать следующие данные диагностики: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Фабрика данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) может использоваться для управления заданием по созданию обновленных больших двоичных объектов, необходимых службе Stream Analytics для обновления определений ссылочных данных. Фабрика данных представляет собой облачную службу интеграции информации, которая организует и автоматизирует перемещение и преобразование данных. Фабрика данных позволяет [подключаться к большому количеству облачных и локальных хранилищ данных](../data-factory/copy-activity-overview.md), а также легко перемещать данные по заданному расписанию. Дополнительные сведения и пошаговые инструкции, с помощью которых можно настроить конвейер фабрики данных и создать ссылочные данные для службы Stream Analytics, обновляемые по заданному расписанию, см. в этом [примере на сайте GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Советы по обновлению ссылочных данных
1. Перезапись больших двоичных объектов ссылочных данных не вызывает перезагрузку большого двоичного объекта в Stream Analytics, но может привести к сбою задания. Для изменения ссылочных данных рекомендуется добавить новый большой двоичный объект, используя контейнер и шаблон пути, указанные во входных данных задания, и указав **более позднее** время и данные, чем в последнем большом двоичном объекте последовательности.
2. Большие двоичные объекты ссылочных данных упорядочиваются **не** по времени их последнего изменения, а по времени и дате, указанным в имени большого двоичного объекта с помощью подстановок {date} и {time}.
3. Чтобы не отобразилось слишком большое количество больших двоичных объектов, попробуйте удалить очень старые большие двоичные объекты, которые больше не будут обрабатываться. Обратите внимание на то, что ASA может быть понадобиться повторно обработать несколько больших двоичных объектов в таких сценариях, как перезагрузка.

## <a name="next-steps"></a>Дополнительная информация
> [!div class="nextstepaction"]
> [Краткое руководство по созданию задания Stream Analytics с помощью портала Azure](stream-analytics-quick-create-portal.md)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
