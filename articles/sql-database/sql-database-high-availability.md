---
title: Высокая доступность службы базы данных SQL Azure | Документация Майкрософт
description: Узнайте о возможностях и функциях высокой доступности службы базы данных SQL Azure
services: sql-database
author: anosov1960
manager: craigg
ms.service: sql-database
ms.topic: article
ms.date: 04/24/2018
ms.author: sashan
ms.reviewer: carlrab
ms.openlocfilehash: e541513890d357587e5c1e792165123c2beb5d96
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32777028"
---
# <a name="high-availability-and-azure-sql-database"></a>Высокая доступность и база данных SQL Azure
С момента появления предложения PaaS Базы данных SQL Azure корпорация Майкрософт пообещала клиентам, что обеспечит высокую доступность в рамках этой службы и клиентам не придется управлять высокой доступностью, добавлять специальную логику для ее обеспечения или же принимать связанные с ней решения. Корпорация Майкрософт предлагает клиентам Соглашения об уровне обслуживания и полностью управляет конфигурацией и работой системы обеспечения высокой доступности. Соглашение об уровне обслуживания, предусматривающее высокий уровень доступности, применяется к Базе данных SQL в регионе и не обеспечивает защиту в случае регионального сбоя, вызванного форс-мажорными обстоятельствами, неподконтрольными корпорации Майкрософт (например, стихийное бедствие, война, гражданские беспорядки, действия государственного органа, терроризм или сбои сети или устройств, внешних по отношению к центрам обработки данных Майкрософт, в том числе со стороны клиента или между стороной клиента и центром обработки данных Майкрософт).

Для упрощения понятия высокой доступности корпорация Майкрософт использует следующие предположения:
1.  Аппаратные и программные сбои неизбежны.
2.  Рабочий персонал допускает ошибки, приводящие к сбоям.
3.  Операции запланированного обслуживания вызывают простои. 

Отдельные события случаются не часто, но в масштабах облака они происходят еженедельно и даже ежедневно. 

## <a name="fault-tolerant-sql-databases"></a>Отказоустойчивые базы данных SQL
Клиентов больше всего интересует отказоустойчивость собственных баз данных и в меньшей степени отказоустойчивость службы "База данных SQL" в целом. Непрерывная работа службы в течение 99,99 % времени не имеет смысла, если собственная база данных попадает в эти 0,01 % недоступных баз данных. Каждая база данных должна быть отказоустойчивой, а устранение сбоев никогда не должно приводить к потере совершенной транзакции. 

Для хранения данных База данных SQL использует локальное хранилище на непосредственно подключенных дисках или и виртуальных дисках (VHD) и удаленное хранилище на основе страничных BLOB-объектов в хранилище Azure класса Premium. 
- Локальное хранилище используется в базах данных и эластичных пулах уровня "Премиум" или "Критически важный для бизнеса" (предварительная версия), которые предназначены для критически важных приложений OLTP с высокими требованиями к числу операций ввода-вывода в секунду. 
- Удаленное хранилище используется для уровней обслуживания "Базовый", "Стандартный" и "Общего назначения", предназначенных для бюджетных рабочих нагрузок, которым требуется независимое масштабирование ресурсов хранилища и вычислительных ресурсов. Они используют одностраничные BLOB-объекты для файлов базы данных и журналов, а также встроенную репликацию хранилищ и механизмы отказоустойчивости.

В обоих случаях механизмы репликации, обнаружение сбоев и восстановление базы данных SQL после них полностью автоматизированы и работают без вмешательства человека. Эта архитектура предотвращает потерю зафиксированных данных и обеспечивает наивысший приоритет защиты данных.

Основные преимущества:
- Клиенты получают максимальную выгоду от реплицированных баз данных без необходимости настраивать или поддерживать сложные аппаратные средства, программное обеспечение, операционную систему или среду виртуализации.
- Все свойства ACID реляционных баз данных поддерживаются системой.
- Отработка отказа автоматизирована и исключает потерю каких-либо зафиксированных данных.
- Маршрутизация подключения к основной реплике динамически управляется службой без необходимости использования логики приложения.
- Высокий уровень автоматизированного обеспечения избыточности предоставляется без дополнительной оплаты.

> [!NOTE]
> Описанная архитектура высокой доступности может быть изменена без предварительного уведомления. 

## <a name="data-redundancy"></a>Избыточность данных

Решение с высоким уровнем доступности в Базе данных SQL основано на технологии [групп доступности AlwaysON](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) SQL Server и позволяет работать с локальными и удаленными базами данных с минимальными различиями. В локальной конфигурации технология "Группа доступности AlwaysOn" используется для сохранения, а в удаленной — для обеспечения доступности (низкое целевое время восстановления (RTO) за счет активной георепликации). 

## <a name="local-storage-configuration"></a>Конфигурация локального хранилища

В этой конфигурации каждая база данных подключается к сети службой управления внутри круга управления. Одна первичная реплика и по меньшей мере две вторичные (набор кворума) расположены внутри области клиента, охватывающей три независимые физические подсистемы в одном и том же центре обработки данных. Шлюз отправляет все операции чтения и записи в основную реплику. Операции записи асинхронно реплицируются во вторичные реплики. База данных SQL использует схему фиксации на основе кворума, при которой данные записываются в первичную и одну вторичную реплику, прежде чем транзакция фиксируется.

Система отработки отказа [Service Fabric](../service-fabric/service-fabric-overview.md) автоматически восстанавливает реплики по мере сбоя узлов и поддерживает членство в кворуме, когда узлы выбывают из системы и присоединяются к ней. Плановое обслуживание тщательно координируется, чтобы обеспечить сохранение минимального числа реплик в наборе кворума (обычно 2). Эта модель хорошо подходит для баз данных уровня "Премиум" или "Критически важный для бизнеса" (предварительная версия), но требует избыточности вычислительных ресурсов и ресурсов хранения и стоит дороже.

## <a name="remote-storage-configuration"></a>Конфигурация удаленного хранилища

Для конфигураций удаленных хранилищ (уровни "Базовый", "Стандартный" или "Общего назначения") в удаленном хранилище BLOB-объектов хранится ровно одна копия, что позволяет использовать возможности систем хранения для обеспечения долговечности, избыточности и обнаружения повреждения данных. 

На следующей схеме показана архитектура с высоким уровнем доступности.
 
![Архитектура с высоким уровнем доступности](./media/sql-database-high-availability/high-availability-architecture.png)

## <a name="failure-detection-and-recovery"></a>Обнаружение сбоев и восстановление 
Крупномасштабная распределенная система нуждается в высоконадежной системе обнаружения отказов, которая может надежно, быстро и максимально точно обнаруживать сбои. Для Базы данных SQL это система на базе Azure Service Fabric. 

Очевидно, когда в первичной реплике происходит сбой, работа не сможет продолжаться, потому что сначала все операции записи и чтения выполняются на первичной реплике. Этот процесс повышения уровня вторичной реплики до статуса первичной имеет целевое время восстановления (RTO), которое равно 30 секундам, и целевую точку восстановления (RPO) равную 0. Чтобы уменьшить влияние 30-секундного RTO, лучше всего попытаться повторно подключиться несколько раз с меньшим временем ожидания попыток неудачного соединения.

В случае сбоя вторичной реплики база данных имеет минимальный набор кворума без резервов. Service Fabric инициирует процесс реконфигурации, аналогичный процессу, который следует за сбоем первичной реплики, поэтому после короткого периода, в течение которого определяется, является ли сбой постоянным, создается другая вторичная реплика. В случае временного сбоя, такого как сбой операционной системы или обновление, новая реплика не создается немедленно, а вместо этого перезапускается узел со сбоем. 

Для конфигураций удаленных хранилищ База данных SQL использует функцию AlwaysOn, чтобы выполнять отработку отказа баз данных во время обновлений. Для этого заранее создается экземпляр SQL в ходе запланированного обновления, в рамках которого подключается и восстанавливается файл базы данных из удаленного хранилища. В случае сбоев процесса или других незапланированных событий Windows Fabric управляет доступностью экземпляра и подключает удаленный файл базы данных (в качестве последнего этапа восстановления).

## <a name="zone-redundant-configuration-preview"></a>Конфигурация с избыточностью в пределах зоны (предварительная версия)

По умолчанию реплики набора кворума для конфигураций локальных хранилищ создаются в одном центре обработки данных. С введением [зон доступности Azure](../availability-zones/az-overview.md) появилась возможность разместить разные реплики в наборах кворума в разных зонах доступности в одном регионе. Чтобы исключить единую точку сбоя, круг управления также дублируется в нескольких зонах в виде трех кругов шлюзов. Маршрутизацией для конкретного круга шлюза управляет [диспетчер трафика Azure](../traffic-manager/traffic-manager-overview.md) (ATM). Так как конфигурация с избыточностью в пределах зоны не обеспечивает дополнительную избыточность баз данных, использование зон доступности на уровне служб "Премиум" или "Критически важный для бизнеса" (предварительная версия) не требует дополнительных затрат. Выбрав базу данных, избыточную в пределах зоны, можно сделать базы данных уровня "Премиум" или "Критически важный для бизнеса" (предварительная версия) устойчивыми ко множеству сбоев, включая крупные аварии в центрах обработки данных, без изменения логики приложения. Можно также преобразовать любые существующие базы данных или пулы уровня "Премиум" или "Критически важный для бизнеса" (предварительная версия) в конфигурацию с избыточностью в пределах зоны.

Так как наборы кворума с избыточностью в пределах зоны содержат реплики в разных центрах обработки данных, которые удалены на некоторое расстояние друг от друга, задержка сети может увеличить время фиксации и тем самым повлиять на производительность некоторых рабочих нагрузок OLTP. Вы всегда можете вернуться к конфигурации с одной зоной, отключив параметр избыточности в пределах зоны. Это процесс масштаба операции с данными, и он аналогичен регулярному обновлению цели уровня обслуживания (SLO). В конце этого процесса база данных или пул переносится из круга с избыточностью в пределах зоны в круг с одной зоной, или наоборот.

> [!IMPORTANT]
> Базы данных с избыточностью в пределах зоны и эластичные пулы поддерживаются только на уровне служб "Премиум" или "Критически важный для бизнеса" (предварительная версия). На этапе общедоступной предварительной версии резервные копии и записи аудита хранятся в хранилище RA-GRS, поэтому они могут не оказаться автоматически доступны в случае сбоя всей зоны. 

На следующей схеме показана версия архитектуры с высоким уровнем доступности и избыточностью в пределах зоны.
 
![Архитектура с высоким уровнем доступности и избыточностью в пределах зоны](./media/sql-database-high-availability/high-availability-architecture-zone-redundant.png)

## <a name="read-scale-out"></a>Горизонтальное масштабирование для чтения
Как описано выше, уровни служб "Премиум" и "Критически важный для бизнеса" (предварительная версия) используют наборы кворума и технологию AlwaysOn для обеспечения высокой доступности в однозонных конфигурациях и конфигурациях с избыточностью в пределах зоны. Одним из преимуществ AlwasyOn является то, что реплики всегда находятся в состоянии транзакционной согласованности. Так как реплики имеют тот же уровень производительности, что и источник, приложение может использовать дополнительную производительность для обработки рабочих нагрузок только для чтения без дополнительных затрат (горизонтальное масштабирование для чтения). Таким образом запросы только на чтение изолируются от главных рабочих нагрузок чтения и записи и не влияют на производительность приложения. Функция горизонтального масштабирования для чтения предназначена для приложений, в которые включены такие логические разделенные рабочие нагрузки только для чтения, как аналитика, и поэтому они могут использовать эту дополнительную производительность без подключения к источнику. 

Чтобы использовать масштабирование для чтения с определенной базой данных, его следует явно включить в момент создания базы данных. Эту функцию также можно включить позже путем изменения ее конфигурации с помощью PowerShell, вызвав командлет [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) или [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase), или путем использования метода [создания или обновления базы данных](/rest/api/sql/databases/createorupdate) в REST API Azure Resource Manager.

Когда для базы данных будет включена функция горизонтального масштабирования для чтения, приложения, которые подключаются к ней, будут перенаправлены к реплике для чтения и записи или к реплике только для чтения текущей базы данных в соответствии со свойством `ApplicationIntent`, настроенным в строке подключения приложения. Дополнительные сведения о свойстве `ApplicationIntent` см. в разделе об [указании назначения приложения](https://docs.microsoft.com/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery#specifying-application-intent). 

Если масштабирование для чтения отключено или установлено свойство ReadScale на уровне служб, который не поддерживается, то все подключения направляются к реплике для чтения и записи независимо от свойства `ApplicationIntent`.  

> [!NOTE]
> Можно активировать масштабирование для чтения для базы данных уровня "Стандартный" или "Общего назначения", хотя это не приведет к перенаправлению сеанса только для чтения к отдельной реплике. Это делается для поддержки существующих приложений, масштаб которых меняется между уровнями "Стандартный" или "Общего назначения" и "Премиум" или "Критически важный для бизнеса".  

Функция горизонтального масштабирования для чтения поддерживает согласованность на уровне сеанса. Если сеанс только для чтения будет повторно подключаться после ошибки соединения, которая была вызвана недоступностью реплики, он может быть перенаправлен в другую реплику. Хотя это маловероятно, но это может привести к обработке устаревшего набора данных. Аналогичным образом, если приложение записывает данные с помощью сеанса чтения и записи и сразу же считывает их с помощью сеанса только для чтения, возможно, что новые данные не будут отображены немедленно.

## <a name="conclusion"></a>Заключение
База данных SQL Azure тесно интегрирована с платформой Azure и в значительной мере зависит от Service Fabric для обнаружения сбоев и восстановления данных, а также от больших двоичных объектов службы хранилища Azure для защиты данных и от зон доступности для повышения отказоустойчивости. В то же время База данных Azure SQL использует все возможности технологии AlwaysOn из готового продукта SQL Server для репликации и отработки отказа. Сочетание этих технологий позволяет приложениям полностью реализовать преимущества смешанной модели хранения и поддерживать самые требовательные Соглашения об уровне обслуживания. 

## <a name="next-steps"></a>Дополнительная информация

- Узнайте больше о [зонах доступности Azure](../availability-zones/az-overview.md).
- Дополнительные сведения о [Service Fabric](../service-fabric/service-fabric-overview.md).
- Дополнительные сведения о [диспетчере трафика Azure](../traffic-manager/traffic-manager-overview.md). 
