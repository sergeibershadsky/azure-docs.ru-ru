---
title: "Предоставление сведений о контактных лицах по вопросам безопасности в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе показано, как указать сведения о контактных лицах по вопросам безопасности в центре безопасности Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/15/2017
ms.author: terrylan
ms.openlocfilehash: 726b59c45e2eb18eebe28a180db23336ae141408
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Предоставление сведений о контактных лицах по вопросам безопасности в центре безопасности Azure
Центр безопасности Azure порекомендует вам предоставить сведения о контактных лицах по вопросам безопасности для подписки Azure, если это еще не сделано. Корпорация Майкрософт будет использовать эту информацию для связи с вами, если центр Microsoft Security Response Center (MSRC) обнаружит, что к вашим пользовательским данным был получен незаконный или несанкционированный доступ. Центр Microsoft Security Response Center (MSRC) осуществляет выборочный мониторинг безопасности сети и инфраструктуры Azure, а также получает аналитические данные об угрозах и жалобы о нарушениях от третьих лиц.

Уведомление по электронной почте отправляется для первого за день оповещения и только тогда, когда у него высокий уровень серьезности. Параметры электронной почты можно настроить только для политик подписки. Группы ресурсов в подписке унаследуют эти параметры.

> [!NOTE]
> В документе приводится обзор службы с помощью примера развертывания.  Он не является пошаговым руководством.
>
>

## <a name="implement-the-recommendation"></a>Выполнение рекомендаций
1. В колонке **Рекомендации** выберите **Указать сведения о контактных лицах по вопросам безопасности**.
   ![Предоставление сведений о контактных лицах по вопросам безопасности][1]
2. Выберите подписку Azure для предоставления контактных данных.
3. Откроется раздел **Политика безопасности — уведомление по электронной почте**.

   ![Предоставление сведений о контактном лице по вопросам безопасности][2]

   * Введите адрес или разделенные запятыми адреса электронной почты контактных лиц по вопросам безопасности. Можно ввести неограниченное количество адресов электронной почты.
   * Введите один международный телефонный номер контактного лица по вопросам безопасности.
   * Чтобы получать по электронной почте оповещения с высоким уровнем серьезности, включите параметр **Send me emails about alerts**(Отправлять мне электронные сообщения об оповещениях).
   * В будущем появится возможность отправлять уведомления по электронной почте владельцам подписок. В настоящее время соответствующий параметр неактивен.
   * Нажмите кнопку **Сохранить**, чтобы применить сведения о контактных лицах по вопросам безопасности к своей подписке.

## <a name="see-also"></a>См. также
Дополнительные сведения о Центре безопасности см. в следующих статьях:

* [Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.
* [Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.
* [Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.
* [Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — последние новости и информация об обеспечении безопасности в Azure.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
