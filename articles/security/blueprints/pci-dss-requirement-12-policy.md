---
title: 'План обработки платежей Azure: требования к политике'
description: Требование 12 (стандарт PCI DSS)
services: security
documentationcenter: na
author: jomolesk
manager: mbaldwin
editor: tomsh
ms.assetid: a79d59d8-20e3-4efe-8686-c8f4ed80e220
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/15/2017
ms.author: jomolesk
ms.openlocfilehash: 2fb238e9b95180d6156159c87ec008a71943e698
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
---
# <a name="policy-requirements-for-pci-dss-compliant-environments"></a>Требования к политике для сред, соответствующих стандарту PCI DSS  
## <a name="pci-dss-requirement-12"></a>Требование 12 (стандарт PCI DSS)

**Установка политики, регулирующей информационную безопасность для всего персонала**

> [!NOTE]
> Эти требования определены [Советом по стандартам безопасности индустрии платежных карт (Payment Card Industry Security Standards Council, PCI SSC)](https://www.pcisecuritystandards.org/pci_security/) в [стандарте PCI DSS версии 3.2](https://www.pcisecuritystandards.org/document_library?category=pcidss&document=pci_dss). Сведения о процедурах тестирования и рекомендации по каждому требованию см. в документации стандарта PCI DSS.

Политика усиленной безопасности задает тон безопасности для всей сущности и уведомляет сотрудников, что от них ожидается. Персоналу следует знать о конфиденциальной природе данных и свои обязанности в отношении защиты этих данных. В рамках требования 12 к "персоналу" относятся сотрудники на условиях полной и частичной занятости, временные сотрудники, подрядчики и консультанты, постоянно находящиеся на сайте организации или иным способом имеющие доступ к среде данных владельца карты.

## <a name="pci-dss-requirement-121"></a>Требование 12.1 (стандарт PCI DSS)

**12.1**. Установка, публикация, обслуживание и распространение политики безопасности.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за установку и обслуживание политики информационной безопасности.|



### <a name="pci-dss-requirement-1211"></a>Требование 12.1.1 (стандарт PCI DSS)

**12.1.1**. Проверка политики безопасности по крайней мере один раз в год и ее обновление при изменениях в среде.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты должны обновлять свою политику информационной безопасности как минимум один раз в год или при изменениях в среде данных владельца карты (CDE).|



## <a name="pci-dss-requirement-122"></a>Требование 12.2 (стандарт PCI DSS)

**12.2**. Реализация процесса оценки рисков, который:
- выполняется по крайней мере один раз в год, а также при наличии значительных изменений в среде (например, приобретения, слияния, перемещения и т. д.);
- идентифицирует критически важные ресурсы, угрозы и уязвимости;
- приводит к формальному, документально подтвержденному анализу риска.
- > Примеры методик анализа рисков включают, помимо прочих: OCTAVE, ISO 27005 и NIST SP 800-30.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за реализацию процесса оценки рисков, который охватывает все угрозы, перечисленные в требовании 12.2.|



## <a name="pci-dss-requirement-123"></a>Требование 12.3 (стандарт PCI DSS)

**12.3**. Разработка политик использования для критически важных технологий и определение соответствующего использования этих технологий.

> [!NOTE]
> Примеры важных технологий включают, помимо прочего, следующие: технологии удаленного доступа и беспроводные технологии, использование ноутбуков, планшетов, съемных электронных носителей, электронной почты и Интернета.
Эти политики использования должны включать следующие требования.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1231"></a>Требование 12.3.1 (стандарт PCI DSS)

**12.3.1**. Явное подтверждение уполномоченными сторонами.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1232"></a>Требование 12.3.2 (стандарт PCI DSS)

**12.3.2**. Проверка подлинности для использования технологии.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1233"></a>Требование 12.3.3 (стандарт PCI DSS)

**12.3.3**. Список всех таких устройств и сотрудников, у которых есть доступ.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1234"></a>Требование 12.3.4 (стандарт PCI DSS)

**12.3.4**. Метод точного и простого определения владельца, контактных данных и цели (например, назначение меток, кодирования и инвентаризации устройств).

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1235"></a>Требование 12.3.5 (стандарт PCI DSS)

**12.3.5**. Приемлемое использование технологии.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1236"></a>Требование 12.3.6 (стандарт PCI DSS)

**12.3.6**. Допустимые сетевые расположения для технологий.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за определение допустимых сетевых расположений для облачных виртуальных машин, хранилища и вспомогательных служб.|



### <a name="pci-dss-requirement-1237"></a>Требование 12.3.7 (стандарт PCI DSS)

**12.3.7**. Список продуктов, утвержденных организацией.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за определение допустимых сетевых расположений для облачных виртуальных машин, хранилища и вспомогательных служб.|



### <a name="pci-dss-requirement-1238"></a>Требование 12.3.8 (стандарт PCI DSS)

**12.3.8**. Автоматическое отключение сеансов для технологий удаленного доступа через определенный период бездействия.

**Обязанности:&nbsp;&nbsp;`Shared`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Microsoft Azure использует функцию блокировки корпоративного сеанса AD Microsoft, которая блокирует сеанс через определенный период бездействия. Сетевые подключения завершаются после 30 минут бездействия. |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1239"></a>Требование 12.3.9 (стандарт PCI DSS)

**12.3.9**. Активация технологий удаленного доступа для поставщиков и бизнес-партнеров только при соответствующей для них необходимости с немедленной деактивацией по завершении использования этих технологий.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-12310"></a>Требование 12.3.10 (стандарт PCI DSS)

**12.3.10**. Сотрудникам, у которых есть доступ к данным владельца карты через технологии удаленного доступа, запрещается копировать, перемещать и сохранять данные владельца карты на локальные жесткие диски и съемные электронные носители, за исключением случаев предоставления явного разрешения в рамках определенной бизнес-задачи.
В последнем случае в соответствии с требованиями политик использования данные должны быть защищены согласно всем применимым требованиям PCI DSS.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за то, чтобы сотрудники, у которых есть доступ к данным владельца карты через технологии удаленного доступа, соблюдали положения о запрете копирования, перемещения и сохранения данных владельца карты на локальные жесткие диски и съемные электронные носители, за исключением случаев предоставления явного разрешения в рамках определенной бизнес-задачи.|



## <a name="pci-dss-requirement-124"></a>Требование 12.4 (стандарт PCI DSS)

**12.4**. Процедуры и политика безопасности должны четко определять обязанности в отношении информационной безопасности для всего персонала.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1241"></a>Требование 12.4.1 (стандарт PCI DSS)

**12.4.1**. Дополнительные требования только для поставщиков услуг. Руководство компании обязуется установить ответственность в отношении защиты данных владельца карты и программу соответствия требованиям PCI DSS, которая будет охватывать следующее:
- общую ответственность за обеспечение требований соответствия PCI DSS;
- определение учредительного документа для программы соответствия требованиям PCI DSS и взаимодействие с руководством. 

> [!NOTE]
> Это рекомендуется сделать до 31 января 2018 года. После этой даты это нужно сделать обязательно.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты, которые являются поставщиками услуг, несут ответственность за создание документации по их программе соответствия требованиям PCI.|



## <a name="pci-dss-requirement-125"></a>Требование 12.5 (стандарт PCI DSS)

**12.5**. Назначение следующих обязанностей в отношении управления информационной безопасностью отдельным пользователям или группе.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за определение и назначение сотрудникам обязанностей в отношении информационной безопасности.|



### <a name="pci-dss-requirement-1251"></a>Требование 12.5.1 (стандарт PCI DSS)

**12.5.1**. Установка, документирование и распространение процедур и политик безопасности.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за определение и назначение сотрудникам обязанностей в отношении информационной безопасности.|



### <a name="pci-dss-requirement-1252"></a>Требование 12.5.2 (стандарт PCI DSS)

**12.5.2**. Мониторинг и анализ сведений и оповещений о безопасности, а также их передача соответствующим сотрудникам.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за определение и назначение сотрудникам обязанностей в отношении информационной безопасности.|



### <a name="pci-dss-requirement-1253"></a>Требование 12.5.3 (стандарт PCI DSS)

**12.5.3**. Устанавливайте, создавайте документацию и распространяйте политику реагирования на инциденты безопасности и процедуры эскалации для своевременной и эффективной обработки всех случаев.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1254"></a>Требование 12.5.4 (стандарт PCI DSS)

**12.5.4**. Управляйте учетными записями пользователей, включая возможности добавления, удаления и изменения.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1255"></a>Требование 12.5.5 (стандарт PCI DSS)

**12.5.5**. Отслеживайте и контролируйте любой доступ к данным.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик, регулирующих соответствующее использование, реализацию и проверку подлинности критически важных технологий в среде данных владельца карты (CDE).|



## <a name="pci-dss-requirement-126"></a>Требование 12.6 (стандарт PCI DSS)

**12.6**. Создайте формальную ознакомительную программу безопасности, чтобы проинформировать всех сотрудников о важности процедур и политики безопасности в отношении данных владельца карты.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за создание и обслуживание политик в отношении осведомленности о безопасности для персонала, у которого есть доступ к среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1261"></a>Требование 12.6.1 (стандарт PCI DSS)

**12.6.1**. Проводите обучающие программы для сотрудников при приеме на работу и не реже раза в год. 

> [!NOTE]
> Методы могут различаться в зависимости от роли сотрудника и его уровня доступа к данным владельца карты.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за ознакомление персонала со сведениями о безопасности, а также за проведение ознакомительного обучения в отношении требований PCI-DSS не реже раза в год.|



### <a name="pci-dss-requirement-1262"></a>Требование 12.6.2 (стандарт PCI DSS)

**12.6.2**. Не реже раза в год персонал обязуется подтверждать свое знакомство с процедурами и политикой безопасности, а также понимание этих процедур и политики.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за ознакомление персонала со сведениями о безопасности, а также за проведение ознакомительного обучения в отношении требований PCI-DSS не реже раза в год.|



## <a name="pci-dss-requirement-127"></a>Требование 12.7 (стандарт PCI DSS)

**12.7**. Проверяйте потенциальных сотрудников до непосредственного приема на работу, чтобы свести к минимуму риски атак из внутренних источников. (Примеры такой проверки включают анализ предыдущих мест работы, отсутствие уголовного прошлого, кредитную репутацию и проверку рекомендаций и послужного списка.) 

> [!NOTE]
> В отношении тех потенциальных сотрудников, которые претендуют на такие должности, как кассир-операционист, у которого на момент выполнения транзакции есть доступ только к одному коду карточки за один раз, это требование представляет собой только рекомендацию.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за проверку биографических данных сотрудников, у которых есть доступ к CDE.|



## <a name="pci-dss-requirement-128"></a>Требование 12.8 (стандарт PCI DSS)

**12.8**. Создайте и применяйте политики и процедуры для контроля поставщиков услуг, у которых есть доступ к данным владельца карты или которые могут повлиять на безопасность этих данных, как показано ниже.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за мониторинг соответствия требованиям PCI для поставщиков услуг, у которых есть доступ к данным владельца карты или которые могут повлиять на безопасность CDE. Клиенты должны вести список всех поставщиков услуг, задействованных в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1281"></a>Требование 12.8.1 (стандарт PCI DSS)

**12.8.1**. Ведите список поставщиков услуг, включая описание предоставляемой услуги.


**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за мониторинг соответствия требованиям PCI для поставщиков услуг, у которых есть доступ к данным владельца карты или которые могут повлиять на безопасность CDE. Клиенты должны вести список всех поставщиков услуг, задействованных в среде данных владельца карты (CDE).|



### <a name="pci-dss-requirement-1282"></a>Требование 12.8.2 (стандарт PCI DSS)

**12.8.2**. Составьте письменное соглашение, включающее подтверждение, что поставщики услуг отвечают за безопасность данных владельца карты, которыми эти поставщики владеют, иным образом их хранят, обрабатывают, передают от имени клиента или используют в той мере, которая может повлиять на безопасность среды данных владельца карты клиента. 

> [!NOTE]
> Точная формулировка подтверждения будет зависеть от соглашения между двумя сторонами, сведений о предоставляемой услуге и обязанностей, назначенных каждой стороне. Подтверждение не должно включать точную формулировку, используемую в этом требовании.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за хранение письменных соглашений, заключенных с поставщиками услуг, где они подтверждают свою ответственность за обеспечение безопасности данных владельцев карт.|



### <a name="pci-dss-requirement-1283"></a>Требование 12.8.3 (стандарт PCI DSS)

**12.8.3**. Требуется установленный процесс привлечения поставщиков услуг, включая соответствующую комплексную проверку перед их непосредственным вовлечением.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за наличие установленного процесса для привлечения поставщиков услуг, включая соответствующую комплексную проверку перед их непосредственным вовлечением.|



### <a name="pci-dss-requirement-1284"></a>Требование 12.8.4 (стандарт PCI DSS)

**12.8.4**. Организуйте программу для мониторинга состояния соответствия требованиям PCI DSS поставщиков услуг не реже раза в год.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты отвечают за организацию программы для мониторинга состояния соответствия требованиям PCI DSS поставщиков услуг не реже раза в год.|



### <a name="pci-dss-requirement-1285"></a>Требование 12.8.5 (стандарт PCI DSS)

**12.8.5**. Сохраняйте сведения о том, какими требованиями PCI DSS управляет каждый поставщик услуг и организация.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за сохранение копии [итоговой таблицы ответственности](https://aka.ms/pciblueprintcrm32), в которой изложены требования PCI DSS, за которые отвечает заказчик, и те, за которые отвечает Microsoft Azure.|



## <a name="pci-dss-requirement-129"></a>Требование 12.9 (стандарт PCI DSS)

**12.9**. Дополнительное требование только для поставщиков услуг. Поставщики услуг подтверждают в письменной форме и предоставляют это подтверждение клиентам, что они отвечают за безопасность данных владельца карты, которыми эти поставщики владеют, иным образом хранят, обрабатывают или передают от имени клиента или используют в той мере, которая может повлиять на безопасность среды данных владельца карты клиента. 

> [!NOTE]
> Точная формулировка подтверждения будет зависеть от соглашения между двумя сторонами, сведений о предоставляемой услуге и обязанностей, назначенных каждой стороне. Подтверждение не должно включать точную формулировку, используемую в этом требовании.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты, которые являются поставщиками услуг, несут ответственность за подтверждение своих обязанностей в отношении обеспечения соответствия требованиям PCI. |



## <a name="pci-dss-requirement-1210"></a>Требование 12.10 (стандарт PCI DSS)

**12.10**. Составьте план реагирования на инциденты. Будьте готовы к незамедлительному реагированию на инциденты в системе безопасности.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12101"></a>Требование 12.10.1 (стандарт PCI DSS)

**12.10.1**. Создайте план реагирования на инциденты для выполнения в случае инцидентов в системе безопасности. Как минимум план должен охватывать следующее:
- роли, обязанности и стратегии обмена данными и взаимодействия в случае компрометации, включая по крайней мере уведомление платежных операторов;
- определенные процедуры реагирования на инцидент;
- процедуры восстановления и непрерывности бизнес-процессов;
- процессы резервного копирования данных;
- анализ нормативных требований для создания отчетов о компрометации;
- реагирование всех критических системных компонентов;
- обращение к процедурам реагирования на инцидент, применяемым платежными операторами, или задействование этих процедур.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12102"></a>Требование 12.10.2 (стандарт PCI DSS)

**12.10.2**. Не реже раза в год просматривайте и тестируйте план, включая все элементы в списке требования 12.10.1.


**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12103"></a>Требование 12.10.3 (стандарт PCI DSS)

**12.10.3**. Обеспечьте круглосуточную поддержку (назначьте определенных сотрудников), чтобы своевременно реагировать на инциденты.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12104"></a>Требование 12.10.4 (стандарт PCI DSS)

**12.10.4**. Проведите соответствующее обучение сотрудников, которым назначены обязанности реагирования на бреши в системе безопасности.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12105"></a>Требование 12.10.5 (стандарт PCI DSS)

**12.10.5**. Настройте оповещения в системах мониторинга безопасности, включая, помимо прочего, следующие: системы мониторинга целостности файлов, брандмауэры, системы обнаружения или предотвращения вторжений.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



### <a name="pci-dss-requirement-12106"></a>Требование 12.10.6 (стандарт PCI DSS)

**12.10.6**. Разработайте процесс для изменения и развития плана реагирования на инциденты в соответствии с выводами, полученными при разрешении случившихся инцидентов, и отраслевыми нововведениями и тенденциями.

**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты несут ответственность за разработку IR-планов и тестирование в отношении любого средства управления клиента, связанного с общими точками контакта, и любых клиентских приложений, использующих инфраструктуру Azure. Клиент несет ответственность за предоставление точных контактных данных Azure в случае, когда необходимо сообщить об инциденте, который может повлиять на данные или приложение.|



## <a name="pci-dss-requirement-1211"></a>Требование 12.11 (стандарт PCI DSS)

**12.11**. **Дополнительное требование только для поставщиков услуг.** Проверяйте (как минимум ежеквартально) соблюдение сотрудниками политик безопасности и операционных процедур.
Проверки должны включать в себя следующие процессы:
- ежедневные проверки журнала;
- проверки набора правил брандмауэра;
- применение стандартов конфигурации к новым системам;
- Реагирование на оповещения системы безопасности
- процессы управления изменениями. 

> [!NOTE]
> Это рекомендуется сделать до 31 января 2018 года. После этой даты это нужно сделать обязательно.


**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты, которые являются поставщиками услуг, несут ответственность за создание документации о проверках процессов в отношении соблюдения требований PCI.|



### <a name="pci-dss-requirement-12111"></a>Требование 12.11.1 (стандарт PCI DSS)

**12.11.1**. Дополнительное требование только для поставщиков услуг. Ведите документацию о ежеквартальных проверках, включая:
- документирование результатов проверок;
- просмотр и заверение результатов подписью сотрудника, ответственного за программы соблюдения соответствия требованиям PCI DSS. 

> [!NOTE]
> До 31 января 2018 года это является рекомендацией. Затем станет требованием.


**Обязанности:&nbsp;&nbsp;`Customer Only`**

|||
|---|---|
| **Поставщик<br />(Microsoft&nbsp;Azure)** | Не применяется |
| **Клиент<br />(план PCI-DSS&nbsp;)** | Клиенты, которые являются поставщиками услуг, несут ответственность за создание документации о проверках процессов в отношении соблюдения требований PCI.|




