---
title: Как настроить кэш Redis для Azure | Документация Майкрософт
description: Обзор конфигурации Redis по умолчанию для кэша Redis для Azure и описание способов настройки экземпляров кэша Redis для Azure
services: redis-cache
documentationcenter: na
author: wesmc7777
manager: cfowler
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: wesmc
ms.openlocfilehash: 0cd21c0367a95d3e866137797ac32fc5bdd196c0
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-configure-azure-redis-cache"></a>Настройка кэша Redis для Azure
В этом разделе описаны конфигурации, доступные для экземпляров кэша Redis для Azure. В этом разделе также описывается конфигурация сервера Redis по умолчанию для экземпляров кэша Redis для Azure.

> [!NOTE]
> Дополнительные сведения о настройке и использовании функций кэша уровня "Премиум" см. в статьях [Настройка постоянного хранения для кэша Redis для Azure уровня Премиум](cache-how-to-premium-persistence.md), [Настройка кластеризации для кэша Redis для Azure уровня Премиум](cache-how-to-premium-clustering.md) и [Настройка поддержки виртуальной сети для кэша Redis для Azure уровня Премиум](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Настройка параметров кэша Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Параметры кэша Redis для Azure можно просмотреть и настроить в колонке **Кэш Redis** с помощью **меню ресурсов**.

![Параметры кэша Redis](./media/cache-configure/redis-cache-settings.png)

Просмотреть и настроить следующие параметры можно с помощью **меню ресурсов**.

* [Обзор](#overview)
* [Журнал действий](#activity-log)
* [Управление доступом (IAM)](#access-control-iam)
* [Теги](#tags)
* [Диагностика и решение проблем](#diagnose-and-solve-problems)
* [Параметры](#settings)
    * [Ключи доступа](#access-keys)
    * [Дополнительные параметры](#advanced-settings)
    * [Помощник по кэшу Redis](#redis-cache-advisor)
    * [Масштабирование](#scale)
    * [Размер кластера Redis](#cluster-size)
    * [Сохраняемость данных Redis](#redis-data-persistence)
    * [Планирование обновлений](#schedule-updates)
    * [Георепликация](#geo-replication)
    * [Виртуальная сеть](#virtual-network)
    * [Брандмауэр](#firewall)
    * [Свойства](#properties)
    * [Блокировки](#locks)
    * [Сценарий автоматизации](#automation-script)
* [Администрирование](#administration)
    * [Импорт данных](#importexport)
    * [Экспорт данных](#importexport)
    * [Reboot](#reboot)
* [Мониторинг](#monitoring)
    * [Метрики Redis](#redis-metrics)
    * [Правила оповещения](#alert-rules)
    * [Диагностика](#diagnostics)
* [Настройки поддержки и устранения неполадок](#support-amp-troubleshooting-settings)
    * [Работоспособность ресурса](#resource-health)
    * [Новый запрос в службу поддержки](#new-support-request)


## <a name="overview"></a>Обзор

В разделе **Обзор** содержатся основные сведения о кэше, такие как имя, порты, ценовая категория, и выбранные метрики кэша.

### <a name="activity-log"></a>Журнал действий

Щелкните **Журнал действий**, чтобы просмотреть выполненные с кэшем действия. Также можно использовать фильтрацию, чтобы развернуть это представление, включив в него другие ресурсы. Дополнительные сведения об использовании журналов аудита см. в статье [Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md). Дополнительные сведения о мониторинге событий кэша Redis для Azure см. в разделе [Операции и оповещения](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Управление доступом (IAM)

В разделе **Управление доступом (IAM)** обеспечивается поддержка управления доступом на основе ролей (RBAC) на портале Azure. Эта конфигурация помогает организациям просто и точно выполнять требования к управлению доступом. Дополнительные сведения см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](../role-based-access-control/role-assignments-portal.md).

### <a name="tags"></a>Теги

В разделе **Теги** вы можете упорядочить свои ресурсы. Дополнительные сведения см. в статье [Использование тегов для организации ресурсов в Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Диагностика и решение проблем

Щелкните **Диагностика и решение проблем** , чтобы узнать об основных проблемах и способах их устранения.



## <a name="settings"></a>Параметры
В разделе **Параметры** можно открыть и настроить следующие параметры кэша.

* [Ключи доступа](#access-keys)
* [Дополнительные параметры](#advanced-settings)
* [Помощник по кэшу Redis](#redis-cache-advisor)
* [Масштабирование](#scale)
* [Размер кластера Redis](#cluster-size)
* [Сохраняемость данных Redis](#redis-data-persistence)
* [Планирование обновлений](#schedule-updates)
* [Георепликация](#geo-replication)
* [Виртуальная сеть](#virtual-network)
* [Брандмауэр](#firewall)
* [Свойства](#properties)
* [Блокировки](#locks)
* [Сценарий автоматизации](#automation-script)



### <a name="access-keys"></a>Ключи доступа
Щелкните **Ключи доступа** для отображения или повторного создания ключей доступа для кэша. Эти ключи используются клиентами, которые подключаются к кэшу.

![Ключи доступа кэша Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Дополнительные параметры
Приведенные ниже параметры доступны в колонке **Дополнительные параметры**.

* [Порты доступа](#access-ports)
* [Политики памяти](#memory-policies)
* [Уведомления пространства ключей (дополнительные параметры)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Порты доступа
Для новых кэшей без SSL порт по умолчанию отключен. Чтобы включить порт, не использующий протокол SSL, в колонке **Дополнительные параметры** для параметра **Разрешить доступ только по SSL** нажмите кнопку **Нет**, а затем щелкните **Сохранить**.

![Порты доступа кэша Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Политики памяти
Параметры **Политика максимальной памяти**, **maxmemory-reserved** и **maxfragmentationmemory-reserved** в колонке **Дополнительные параметры** позволяют настроить политики памяти для кэша.

![Политика максимальной памяти кэша Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Политика максимальной памяти** используется для настройки политики вытеснения для кэша и позволяет выбрать следующие политики вытеснения:

* `volatile-lru` — это политика вытеснения по умолчанию.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Дополнительные сведения о политиках `maxmemory` см. в разделе [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Политики вытеснения) на сайте Redis.

Параметр **maxmemory-reserved** определяет объем памяти в мегабайтах, зарезервированный для операций, не связанных с кэшем, например для репликации при отработке отказа. Установка этого значения обеспечивает более согласованную работу сервера Redis при изменении нагрузки. Это значение должно быть выше при рабочих нагрузках с преобладанием записи. При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.

Параметр **maxfragmentationmemory-reserved** используется для настройки объема памяти в МБ, который зарезервирован для размещения при фрагментации памяти. Установка этого значения дает возможность более согласованно использовать сервер Redis, когда кэш заполнен или почти заполнен, а также при высоком соотношении фрагментации. При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.

При выборе нового значения резервирования памяти (**maxmemory-reserved** или **maxfragmentationmemory-reserved**) также необходимо учитывать, как это изменение может повлиять на кэш, в котором уже выполняется обработка больших объемов данных. Например, если в кэше емкостью 53 ГБ находится 49 ГБ данных, а вы измените значение параметра резервирования на 8 ГБ, то максимальный объем доступной памяти для системы будет снижен до 45 ГБ. Если текущие значения `used_memory` или `used_memory_rss` выше, чем новое ограничение в 45 ГБ, то системе придется вытеснять данные до тех пор, пока оба значения `used_memory` и `used_memory_rss` не станут меньше 45 ГБ. Вытеснение может увеличить нагрузку на сервер и фрагментацию памяти. Дополнительные сведения о доступных метриках кэша, таких как `used_memory` и `used_memory_rss`, см. в разделе [Доступные метрики и интервалы отчетности](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Параметры **maxmemory-reserved** и **maxfragmentationmemory-reserved** доступны только для кэшей уровней "Стандартный" и "Премиум".
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Уведомления пространства ключей (дополнительные параметры)
В колонке **Дополнительные параметры** можно настроить уведомления пространства ключей Redis. Уведомления пространства ключей позволяют клиентам получать уведомления при возникновении определенных событий.

![Дополнительные параметры кэша Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Уведомления пространства ключей и параметр **notify-keyspace-events** доступны только для кэшей уровней Standard и Premium.
> 
> 

Дополнительные сведения см. в статье [Redis Keyspace Notifications](http://redis.io/topics/notifications) (Уведомления пространства ключей Redis). Пример кода см. в файле [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) в примере [Здравствуй, мир!](https://github.com/rustd/RedisSamples/tree/master/HelloWorld).


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Помощник по кэшу Redis
В колонке **Помощник по кэшу Redis** отображаются рекомендации для кэша. Во время обычной работы не отображается никаких рекомендаций. 

![Рекомендации](./media/cache-configure/redis-cache-no-recommendations.png)

При возникновении во время работы кэша любого из таких условий, как интенсивное использование памяти, пропускной способности сети или сервера, в колонке **Кэш Redis** отображается предупреждение.

![Рекомендации](./media/cache-configure/redis-cache-recommendations-alert.png)

Дополнительные сведения можно найти в колонке **Рекомендации** .

![Рекомендации](./media/cache-configure/redis-cache-recommendations.png)

Эти метрики можно отслеживать в колонке **Кэш Redis** в разделах [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) (Диаграммы мониторинга) и [Usage charts](cache-how-to-monitor.md#usage-charts) (Диаграммы использования).

Каждая ценовая категория имеет различные ограничения для количества клиентских подключений, памяти и пропускной способности. Если в течение продолжительного периода времени кэш приближается к максимальной емкости для этих метрик, создается рекомендация. Дополнительные сведения о метриках и ограничениях, используемых инструментом **Рекомендации**, см. в следующей таблице:

| Метрика "Кэш Redis" | Дополнительные сведения |
| --- | --- |
| Пропускная способность сети |[Производительность кэша — доступная пропускная способность](cache-faq.md#cache-performance) |
| Подключенные клиенты |[Конфигурация сервера Redis по умолчанию — максимальное количество клиентов](#maxclients) |
| Загрузка сервера |[Диаграммы использования — загрузка сервера Redis](cache-how-to-monitor.md#usage-charts) |
| Использование памяти |[Производительность кэша — размер](cache-faq.md#cache-performance) |

Чтобы обновить кэш, нажмите кнопку **Обновить сейчас**. При этом будут изменены ценовая категория и [размер](#scale) кэша. Дополнительные сведения о выборе ценовой категории кэша см. в разделе [Какое предложение и размер кэша Redis мне следует использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Масштаб
Щелкните **Масштаб**, чтобы просмотреть или изменить ценовую категорию для кэша. Дополнительные сведения о масштабировании см. в статье [Масштабирование кэша Redis для Azure](cache-how-to-scale.md).

![Ценовая категория кэша Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Размер кластера Redis
Щелкните **Размер кластера Redis (предварительная версия)** , чтобы добавить или удалить сегменты работающего кэша категории "Премиум" с включенной кластеризацией.

> [!NOTE]
> Обратите внимание, что хотя кэш Redis для Azure категории «Премиум» выпущен для общего доступа, сейчас функция изменения размера кластера Redis находится на этапе предварительной версии.
> 
> 

![Размер кластера Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

Чтобы изменить размер кластера, воспользуйтесь ползунком или введите число от 1 до 10 в текстовом поле **Shard count** (Количество сегментов), а затем нажмите кнопку **ОК** для сохранения изменений.

> [!IMPORTANT]
> Кластеризация Redis доступна только для кэша категории «Премиум». Дополнительные сведения см. в статье [Настройка кластеризации для кэша Redis для Azure уровня Премиум](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Сохраняемость данных Redis
Щелкните **Сохраняемость данных Redis** , чтобы включить, отключить или настроить сохраняемость данных кэша категории «Премиум». Кэш Redis для Azure обеспечивает сохраняемость Redis на основе [RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) или [AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Дополнительные сведения см. в статье [Настройка постоянного хранения для кэша Redis для Azure уровня Премиум](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> Сохраняемость данных Redis доступна только для кэшей категории «Премиум». 
> 
> 

### <a name="schedule-updates"></a>запланировать обновления
В колонке **Schedule updates** (Планирование обновлений) можно указать период обслуживания для обновления сервера кэша Redis. 

> [!IMPORTANT]
> Данный период обслуживания относится только к обновлениям сервера Redis, а не ко всем обновлениям Azure или операционной системы виртуальных машин, на которых размещен кэш.
> 
> 

![запланировать обновления](./media/cache-configure/redis-schedule-updates.png)

Чтобы задать период обслуживания, отметьте необходимые дни и укажите, когда будет начинаться период обслуживания в каждый из дней, а затем нажмите кнопку **ОК**. Обратите внимание, что время периода обслуживания указывается в формате UTC. 

> [!IMPORTANT]
> Функция **планирования обновлений** доступна только для кэшей категории "Премиум". Дополнительные сведения и указания см. в разделе о [планировании обновлений](cache-administration.md#schedule-updates) статьи, посвященной администрированию кэша Redis для Azure.
> 
> 

### <a name="geo-replication"></a>Георепликация

Колонка **Георепликация** предоставляет механизм связывания двух экземпляров кэша Redis для Azure категории "Премиум". Один кэш используется в качестве основного связанного кэша, а другой — как дополнительный связанный кэш. Дополнительный связанный кэш становится доступным только для чтения, и в него реплицируются данные, записанные в основной кэш. Эту функцию можно использовать для репликации кэша в разные регионы Azure.

> [!IMPORTANT]
> **Георепликация** доступна только для кэшей категории "Премиум". Дополнительные сведения и инструкции см. в статье [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md) (Как настроить георепликацию для кэша Redis для Azure).
> 
> 

### <a name="virtual-network"></a>Виртуальная сеть
В разделе **Виртуальная сеть** можно настроить параметры виртуальной сети для кэша. Дополнительные сведения о создании кэша уровня Премиум с поддержкой виртуальной сети и обновлении ее параметров см. в статье [Настройка поддержки виртуальной сети для кэша Redis для Azure уровня Премиум](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Параметры виртуальной сети доступны только для кэшей уровня Премиум, которые были настроены с поддержкой виртуальной сети во время создания кэша. 
> 
> 

### <a name="firewall"></a>Брандмауэр

Настройка правил брандмауэра доступна для всех уровней кэша Redis для Azure.

Щелкните **Брандмауэр**, чтобы просмотреть и настроить правила брандмауэра для кэша.

![Брандмауэр](./media/cache-configure/redis-firewall-rules.png)

В правилах брандмауэра можно указать начало и конец диапазона IP-адресов. Когда правила брандмауэра будут настроены, подключения к кэшу будут доступны только для клиентов из указанного диапазона IP-адресов. После сохранения правила брандмауэра существует небольшая задержка, прежде чем правило начинает действовать. Обычно эта задержка не длится более одной минуты.

> [!IMPORTANT]
> Подключения из систем мониторинга кэша Redis для Azure всегда разрешены, даже если настроены правила брандмауэра.
> 
> 

### <a name="properties"></a>properties
Щелкните **Свойства** , чтобы отобразить сведения о кэше, включая конечную точку и порты кэша.

![Свойства кэша Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Блокировки
Раздел **Блокировки** позволяет заблокировать подписку, ресурс или группу ресурсов, чтобы другие пользователи в организации не могли случайно удалить или изменить критически важные ресурсы. Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Сценарий автоматизации

Щелкните **Сценарий автоматизации**, чтобы создать и экспортировать шаблон развернутых ресурсов для использования в будущих развертываниях. Дополнительные сведения о работе с шаблонами см. в статье [Развертывание ресурсов с использованием шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Параметры администрирования
Параметры в разделе **Администрирование** позволяют выполнить следующие задачи администрирования для кэша. 

![Администрирование](./media/cache-configure/redis-cache-administration.png)

* [Импорт данных](#importexport)
* [Экспорт данных](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Импорт и экспорт
Функция импорта/экспорта является операцией управления данными в кэше Redis для Azure, которая позволяет импортировать данные в кэш и экспортировать их оттуда путем импорта и экспорта моментального снимка базы данных кэша Redis (RDB) из кэша уровня "Премиум" в страничный BLOB-объект в учетной записи хранения Azure. Функция импорта/экспорта дает возможность переключаться между различными экземплярами кэша Redis для Azure или заполнять кэш данными перед использованием.

Импорт можно использовать для переноса RDB-файлов, совместимых с Redis, с сервера Redis, запущенного в любом облаке или любой среде, включая Redis в Linux, Windows, или у любого поставщика облачных служб, такого как Amazon Web Services или другого. Импорт данных позволяет легко создать кэш, предварительно заполненный данными. Во время импорта кэш Redis для Azure загружает RDB-файлы из службы хранилища Azure в память, а затем вставляет в кэш ключи.

Экспорт позволяет экспортировать данные, хранящиеся в кэше Redis для Azure, в RDB-файлы, совместимые с Redis. Эту функцию можно использовать для перемещения данных из одного экземпляра кэша Redis для Azure в другой или на другой сервер Redis. Во время экспорта на виртуальной машине, где размещается экземпляр сервера кэша Redis для Azure, создается временный файл, который отправляется в заданную учетную запись хранения. После успешного или неудачного завершения операции экспорта этот временный файл удаляется.

> [!IMPORTANT]
> Функция импорта и экспорта доступна только для кэшей категории "Премиум". Дополнительные сведения и указания см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Колонка **Перезагрузка** позволяет перезагрузить узлы кэша. Функция перезагрузки дает возможность протестировать приложение на устойчивость в случае сбоя узла кэша.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

Если у вас кэш уровня "Премиум" с включенной кластеризацией, то вы можете выбрать сегменты кэша для перезагрузки.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

Чтобы перезагрузить один или несколько узлов кэша, выберите необходимые узлы и нажмите кнопку **Перезагрузить**. Если у вас кэш уровня "Премиум" с включенной кластеризацией, выберите сегменты для перезагрузки и нажмите кнопку **Перезагрузить**. Через несколько минут выбранные узлы перезагрузятся, а еще через несколько минут — возобновят работу.

> [!IMPORTANT]
> Перезагрузка теперь доступна для всех ценовых категорий. Дополнительные сведения и указания см. в разделе о [перезагрузке](cache-administration.md#reboot) статьи, посвященной администрированию кэша Redis для Azure.
> 
> 


## <a name="monitoring"></a>Мониторинг

В разделе **Мониторинг** можно настроить диагностику и мониторинг для кэша Redis. Дополнительные сведения о мониторинге и диагностике кэша Redis для Azure см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md).

![Диагностика](./media/cache-configure/redis-cache-diagnostics.png)

* [Метрики Redis](#redis-metrics)
* [Правила оповещения](#alert-rules)
* [Диагностика](#diagnostics)

### <a name="redis-metrics"></a>Метрики Redis
Щелкните **Метрики Redis**, чтобы [просмотреть метрики](cache-how-to-monitor.md#view-cache-metrics) кэша.

### <a name="alert-rules"></a>правила оповещений.

Щелкните **Правила оповещения**, чтобы настроить оповещения на основе метрик кэша Redis. Дополнительные сведения см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Диагностика

По умолчанию в Azure Monitor метрики кэша [хранятся в течение 30 дней](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), а затем удаляются. Чтобы сохранить метрики кэша дольше, чем на 30 дней, щелкните **Диагностика**, чтобы [настроить учетную запись хранения](cache-how-to-monitor.md#export-cache-metrics), используемую для хранения диагностических данных кэша.

>[!NOTE]
>В дополнение к архивированию метрик кэша в хранилище вы можете настроить для них [потоковую передачу в концентратор событий или отправку в журнал Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Настройки поддержки и устранения неполадок
Параметры в разделе **Поддержка и устранение неполадок** дают возможности для устранения проблем с кэшем.

![Поддержка и устранение неполадок](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Работоспособность ресурса](#resource-health)
* [Новый запрос в службу поддержки](#new-support-request)

### <a name="resource-health"></a>Работоспособность ресурса
Служба **работоспособности ресурсов** отслеживает ресурс и сообщает, работает ли он как ожидалось. Дополнительные сведения о службе работоспособности ресурсов Azure см. [здесь](../resource-health/resource-health-overview.md).

> [!NOTE]
> В настоящее время служба работоспособности ресурсов не поддерживает отправку сведений о работоспособности экземпляров кэша Redis для Azure, размещенных в виртуальной сети. Дополнительные сведения см. в разделе [Все ли функции кэша работают, когда он размещен в виртуальной сети?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet).
> 
> 

### <a name="new-support-request"></a>Новый запрос на техническую поддержку
Щелкните **Новый запрос на получение поддержки** , чтобы создать запрос по своему кэшу.





## <a name="default-redis-server-configuration"></a>Конфигурация сервера Redis по умолчанию
Новые экземпляры кэша Redis для Azure имеют следующие значения конфигурации Redis по умолчанию.

> [!NOTE]
> Параметры в этом разделе не удастся изменить с помощью метода `StackExchange.Redis.IServer.ConfigSet`. При вызове этого метода одной из команд в данном разделе, выдается исключение, аналогичное приведенному ниже примеру.  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Все настраиваемые значения, такие как **max-memory-policy**, настраиваются на портале Azure или с помощью программ командной строки, таких как Azure CLI или PowerShell.
> 
> 

| Параметр | Значение по умолчанию | ОПИСАНИЕ |
| --- | --- | --- |
| `databases` |16 |Количество баз данных по умолчанию — 16. Тем не менее можно указать другое количество в зависимости от ценовой категории<sup>1</sup>. По умолчанию используется база данных DB 0. Вы можете выбрать другую базу данных для отдельных подключений с помощью `connection.GetDatabase(dbid)`, где `dbid` — это число от `0` до `databases - 1`. |
| `maxclients` |Зависит от ценовой категории.<sup>2</sup> |Это значение представляет собой максимально допустимое количество одновременно подключенных клиентов. После достижения предела Redis закрывает все новые подключения, возвращая сообщение об ошибке "max number of clients reached" (достигнуто максимальное количество клиентов). |
| `maxmemory-policy` |`volatile-lru` |Политика максимальной памяти — это параметр, определяющий то, как Redis выбирает, что следует удалить при достижении `maxmemory` (размера кэша, выбранного вами при создании кэша). В случае с кэшем Redis для Azure значением по умолчанию является `volatile-lru`, когда удаляются ключи со сроком действия, устанавливаемым посредством алгоритма LRU. Этот параметр можно настроить на портале Azure. Дополнительные сведения см. в разделе [Политики памяти](#memory-policies). |
| `maxmemory-samples` |3 |Для экономии памяти алгоритмы LRU и минимальный TTL являются не точными, а аппроксимированными алгоритмами. По умолчанию Redis проверяет три ключа и выбирает один, использовавшийся наиболее давно. |
| `lua-time-limit` |5 000 |Максимальное время выполнения сценария Lua в миллисекундах. При достижении максимального времени выполнения Redis делает запись в журнале о нахождении данного сценария в процессе выполнения по истечении максимально допустимого времени и начинает отвечать на запросы ошибкой. |
| `lua-event-limit` |500 |Максимальный размер очереди событий сценариев. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Ограничения буферов вывода клиентов можно использовать для принудительного отключения клиентов, по каким-либо причинам недостаточно быстро считывающим данные с сервера (распространенной причиной является неспособность клиента Pub/Sub поглощать сообщения так же быстро, как их производит издатель). Дополнительные сведения можно найти по адресу [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup> Для различных ценовых категорий кэша Redis для Azure предельное значение `databases` будет разным. Его можно указать при создании кэша. Если при создании кэша значение `databases` не указано, то используется значение по умолчанию — 16.

* Кэши уровней Basic и Standard
  * кэш C0 (250 МБ) — до 16 баз данных;
  * кэш C1 (1 ГБ) — до 16 баз данных;
  * кэш C2 (2,5 ГБ) — до 16 баз данных;
  * кэш C3 (6 ГБ) — до 16 баз данных;
  * кэш C4 (13 ГБ) — до 32 баз данных;
  * кэш C5 (26 ГБ) — до 48 баз данных;
  * кэш C6 (53 ГБ) — до 64 баз данных.
* Кэши уровня Premium
  * кэш P1 (6–60 ГБ) — до 16 баз данных;
  * кэш P2 (13–130 ГБ) — до 32 баз данных;
  * кэш P3 (26–260 ГБ) — до 48 баз данных;
  * кэш P4 (53–530 ГБ) — до 64 баз данных.
  * Для всех кэшей уровня Премиум включен кластер Redis. Он поддерживает только базу данных 0, поэтому предельное значение `databases` для любого кэша уровня Премиум с включенным кластером Redis равно 1, а использование команды [Select](http://redis.io/commands/select) не допускается. Дополнительные сведения см. в разделе [Нужно ли вносить изменения в клиентское приложение, чтобы использовать кластеризацию?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering).

Дополнительные сведения о базах данных см. в разделе [Что такое базы данных Redis?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Параметр `databases` можно настроить только во время создания кэша и только с помощью PowerShell, интерфейса командной строки или других клиентов управления. Пример настройки `databases` во время создания кэша с помощью PowerShell см. в разделе о командлете [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup>`maxclients` отличается для каждой ценовой категории кэша Redis для Azure.

* Кэши уровней Basic и Standard
  * кэш C0 (250 МБ) — до 256 подключений;
  * кэш C1 (1 ГБ) — до 1000 подключений;
  * кэш C2 (2.5 ГБ) — до 2000 подключений;
  * кэш C3 (6 ГБ) — до 5000 подключений;
  * кэш C4 (13 ГБ) — до 10 000 подключений;
  * кэш C5 (26 ГБ) — до 15 000 подключений;
  * кэш C6 (53 ГБ) — до 20 000 подключений.
* Кэши уровня Premium
  * P1 (6–60 ГБ): до 7500 подключений
  * P2 (13–130 ГБ): до 15 000 подключений
  * P3 (26–260 ГБ): до 30 000 подключений
  * P4 (53–530 ГБ): до 40 000 подключений

> [!NOTE]
> Хотя каждый размер кэша *допускает* определенное число подключений, с каждым подключением к Redis связаны накладные расходы. Примером таких накладных расходов могут служить загрузка ЦП и использование памяти в результате шифрования TLS/SSL. Максимальное число подключений для данного размера кэша предполагает низкую загрузку кэша. Если *суммарная* нагрузка, связанная с подключениями и клиентскими операциями, превышает емкость системы, могут возникнуть проблемы с работой кэша, даже если максимальное число подключений для его текущего размера не превышено.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Команды Redis не поддерживаются в кэше Redis для Azure
> [!IMPORTANT]
> Поскольку настройка и управление экземплярами кэша Redis для Azure осуществляется Майкрософт, следующие команды отключены. При попытке их вызвать появляется сообщение об ошибке примерно следующего содержания: `"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Сохранить
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER — команды записи для кластера отключены, однако допускается использование кластерных команд только для чтения.
> 
> 

Дополнительные сведения о командах Redis см здесь: [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Консоль Redis
В экземплярах кэша Redis для Azure можно безопасно выполнять команды с помощью **консоли Redis**, доступной на портале Azure для всех категорий кэшей.

> [!IMPORTANT]
> - Консоль Redis не работает с [VNET](cache-how-to-premium-vnet.md). Если кэш является частью виртуальной сети, то к нему могут обращаться только клиенты в этой виртуальной сети. Так как консоль Redis работает в локальном браузере вне виртуальной сети, она не может подключиться к кэшу.
> - В кэше Redis для Azure поддерживаются не все команды Redis. Список команд Redis, отключенных в кэше Redis для Azure, см. в предыдущем разделе [Команды Redis, не поддерживаемые в кэше Redis для Azure](#redis-commands-not-supported-in-azure-redis-cache). Дополнительные сведения о командах Redis см здесь: [http://redis.io/commands](http://redis.io/commands).
> 
> 

Чтобы иметь доступ к консоли Redis, в колонке **Кэш Redis** щелкните **Консоль**.

![Консоль Redis](./media/cache-configure/redis-console-menu.png)

Чтобы выполнить команду в своем экземпляре кэша, просто введите нужную команду в консоль.

![Консоль Redis](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a>Использование консоли Redis с кластеризированным кэшем категории "Премиум"

При использовании консоли Redis с кластеризированным кэшем категории "Премиум" можно выполнять команды для одного сегмента кэша. Чтобы выполнить команду для конкретного сегмента, сначала подключитесь к нужному сегменту, щелкнув его в окне выбора сегментов.

![Консоль Redis](./media/cache-configure/redis-console-premium-cluster.png)

При попытке получить доступ к ключу, который хранится в другом сегменте, вы получите следующее сообщение об ошибке.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

В предыдущем примере выбран сегмент 1, но `myKey` находится в сегменте 0, как указано в части `(shard 0)` сообщения об ошибке. В этом примере для доступа к `myKey` выберите сегмент 0 с помощью средства выбора сегментов, а затем выполните необходимую команду.


## <a name="move-your-cache-to-a-new-subscription"></a>Перемещение кэша в новую подписку
Для перемещения кэша в новую подписку щелкните **Переместить**.

![Перемещение кэша Redis](./media/cache-configure/redis-cache-move.png)

Сведения о перемещении ресурсов из одной группы ресурсов в другую, а также из одной подписки в другую см. в статье [Перемещение ресурсов в новую группу ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Дополнительная информация
* Дополнительные сведения о работе с командами Redis см. в разделе [Как выполнять команды Redis?](cache-faq.md#how-can-i-run-redis-commands)

