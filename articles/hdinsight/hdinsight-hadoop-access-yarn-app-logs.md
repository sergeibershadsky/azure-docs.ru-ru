---
title: Программный доступ к журналам приложений Hadoop YARN в Azure | Документы Майкрософт
description: Программный доступ к журналам приложений в кластере Hadoop в HDInsight.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.devlang: na
ms.topic: conceptual
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: aab7865548c034cb550874c31977b05936dc45b9
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Доступ к журналам приложений YARN в HDInsight под управлением Windows
Из этой статьи вы узнаете, как получить доступ к журналам приложений YARN, завершивших работу в кластере Hadoop под управлением Windows в Azure HDInsight.

> [!IMPORTANT]
> Информация, содержащаяся в данном документе, относится только к кластерам HDInsight под управлением Windows. Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Сведения о доступе к журналам YARN в кластерах HDInsight под управлением Linux см. в статье [Доступ к журналам приложений YARN в HDInsight под управлением Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md).
>


### <a name="prerequisites"></a>предварительным требованиям
* Кластер HDInsight на платформе Windows См.  статью [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>Сервер временной шкалы YARN
<a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN Timeline Server</a> предоставляет общие сведения о завершенных приложениях, а также зависящие от платформы сведения о приложениях через два разных интерфейса. В частности:

* Возможность хранения и извлечения общей информации о приложениях в кластерах HDInsight появилась, начиная с версии 3.1.1.374.
* В настоящее время компонент сервера временной шкалы, предоставляющий сведения о приложениях для конкретной платформы, недоступен в кластерах HDInsight.

К общим сведениям о приложениях относятся следующие типы данных:

* уникальный идентификатор приложения;
* имя пользователя, запустившего приложение;
* информация о попытках завершить приложение;
* информация о контейнерах, которые использовались во время каждой из попыток.

В кластерах HDInsight эти сведения сохраняет Azure Resource Manager. Сведения сохраняются в стандартном хранилище кластера в хранилище журналов. Эти общие данные о завершенных приложениях можно извлечь с помощью REST API:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Приложения и журналы YARN
YARN поддерживает несколько моделей программирования, отделяя управление ресурсами от планирования и мониторинга приложений. YARN использует глобальный диспетчер *ResourceManager*, *диспетчеры узлов* на каждый рабочий узел и *диспетчеры приложений* на каждое приложение. Диспетчер приложений согласовывает ресурсы (ЦП, память, диск, сеть), необходимые для работы приложения, с диспетчером ресурсов. Диспетчер ресурсов совместно с диспетчером узлов предоставляют эти ресурсы в виде *контейнеров*. Диспетчер приложений отвечает за отслеживание хода выполнения контейнеров, назначаемых ему диспетчером ресурсов. Приложению может потребоваться много контейнеров в зависимости от характера приложения.

* Для выполнения приложения может потребоваться несколько *попыток*. 
* Контейнеры выделяются определенной попытке. 
* Контейнер предоставляет контекст для базовой единицы работы. 
* Вся работа, выполняемая в контексте контейнера, выполняется на одном рабочем узле, которому был выделен контейнер. 

Дополнительные сведения см. [здесь][YARN-concepts].

Журналы приложений (и соответствующие журналы контейнеров) крайне важны для отладки проблемных приложений Hadoop. YARN предоставляет хорошую платформу для сбора, объединения и хранения журналов приложений с функцией [объединения журналов][log-aggregation]. Функция объединения журналов делает доступ к журналам приложений более детерминированным, так как она объединяет журналы со всех контейнеров на рабочем узле и хранит их как один сводный файл журнала в файловой системе по умолчанию после завершения приложения. Ваше приложение может использовать сотни и даже тысячи контейнеров, но журналы всех контейнеров, запущенных на одном рабочем узле, объединяются в один файл. В результате на каждый рабочий узел, используемый приложением, приходится один файл журнала. Объединение журналов включено по умолчанию в кластерах HDInsight (3.0 и более поздних версий), а сводные журналы можно найти в контейнере кластера по умолчанию по следующему адресу:

    wasb:///app-logs/<user>/logs/<applicationId>

где *user* — имя пользователя, запустившего приложение, а *applicationId*— уникальный идентификатор приложения, назначенный диспетчером ресурсов YARN.

Сводные журналы не могут считываться напрямую, так как они записаны в [TFile][T-file], [двоичном формате][binary-format], индексированном контейнером. YARN предоставляет средства CLI для разгрузки этих журналов в виде обычного текста в нужные приложения или контейнеры. Вы можете просмотреть эти журналы в виде обычного текста, выполнив одну из следующих команд YARN непосредственно в узлах кластера (после подключения к нему через протокол RDP):

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>Пользовательский интерфейс YARN ResourceManager
Пользовательский интерфейс YARN ResourceManager работает на головном узле кластера. Для доступа к нему можно использовать панель мониторинга портала Azure.

1. Войдите на [портал Azure](https://portal.azure.com/).
2. В меню слева последовательно щелкните **Обзор** и **Кластеры HDInsight**, а затем выберите кластер под управлением Windows, в котором размещены нужные журналы приложений YARN.
3. В меню вверху щелкните **Панель мониторинга**. В новой вкладке браузера откроется страница **Консоль запросов HDInsight**.
4. В **консоли запросов HDInsight** щелкните **Yarn UI** (Пользовательский интерфейс Yarn).

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
