---
title: Как связать подписку Azure с клиентом Azure AD B2C | Документы Майкрософт
description: Пошаговое руководство по настройке выставления счетов для клиента Azure AD B2C в подписке Azure.
services: active-directory-b2c
documentationcenter: dev-center-name
author: davidmu1
manager: mtillman
editor: ''
ms.service: active-directory-b2c
ms.topic: article
ms.workload: identity
ms.date: 12/05/2017
ms.author: davidmu
ms.openlocfilehash: bb9324b01bb810ba15994612bac2ff20dc83ab82
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
# <a name="linking-an-azure-subscription-to-an-azure-ad-b2c-tenant"></a>Связывание подписки Azure с клиентом Azure B2C

> [!IMPORTANT]
> Последние сведения о выставлении счетов за использование, а также о ценах на Azure AD B2C см. на [этой странице](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

Счета за использование Azure AD B2C выставляются для подписки Azure. Администратор созданного клиента Azure AD B2C должен явным образом связать созданный клиент Azure AD B2C с подпиской Azure. В этой статье показано, как это сделать.

> [!NOTE]
> Подписку, связанную с клиентом Azure AD B2C, можно использовать только для выставления счетов за использование Azure AD B2C. Она не позволяет добавлять другие службы Azure или лицензии Office 365 *в клиенте Azure AD B2C*.

 Чтобы реализовать такую связь, следует создать ресурс Azure AD B2C в целевой подписке Azure. В одной подписке Azure можно создать несколько клиентов B2C наряду с другими ресурсами Azure (такими как виртуальные машины, хранилища данных, приложения логики). Чтобы увидеть все ресурсы, размещенные в подписке, перейдите к клиенту Azure AD, с которым связана эта подписка.

Для работы с руководством требуется действующая подписка Azure.

## <a name="create-an-azure-ad-b2c-tenant"></a>Создание клиента Azure AD B2C

Прежде всего [создайте клиент Azure AD B2C](active-directory-b2c-get-started.md), который вы намерены связать с подпиской. Пропустите этот шаг, если у вас уже есть клиент Azure AD B2C.

## <a name="open-azure-portal-in-the-azure-ad-tenant-that-shows-your-azure-subscription"></a>Открытие портала Azure для клиента Azure AD с отображаемой подпиской Azure

Перейдите к клиенту Azure AD, в котором отображается нужная подписка Azure Откройте [Портал Azure](https://portal.azure.com) и перейдите к клиенту Azure AD, в котором отображается подписка Azure, которую вы намерены использовать.

![Переход к нужному клиенту Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="find-azure-ad-b2c-in-the-azure-marketplace"></a>Поиск Azure AD B2C в Azure Marketplace

Нажмите кнопку **Создать ресурс**. В поле **Поиск по Marketplace** введите `B2C`.

![Выделенная кнопка добавления и поле поиска по Marketplace с текстом Azure Active Directory B2C](../../includes/media/active-directory-b2c-create-tenant/find-azure-ad-b2c.png)

В списке результатов выберите **Azure AD B2C**.

![Служба Azure AD B2C, выбранная в списке результатов](../../includes/media/active-directory-b2c-create-tenant/find-azure-ad-b2c-result.png)

Отобразятся сведения об Azure AD B2C. Нажмите кнопку **Создать**, чтобы начать настройку нового клиента Azure Active Directory B2C.

В окне создания ресурса выберите **Связывание существующего B2C-клиента Azure AD с вашей подпиской Azure**.

## <a name="create-an-azure-ad-b2c-resource-within-the-azure-subscription"></a>Создание ресурса Azure AD B2C в подписке Azure

В диалоговом окне создания ресурса выберите в раскрывающемся списке клиент Azure AD B2C. Вы увидите полный список клиентов, для которых вы являетесь глобальным администратором и которые еще не связаны с подпиской.

Имя ресурса Azure AD B2C устанавливается автоматически и совпадает с доменным именем клиента Azure AD B2C.

В поле "Подписка" выберите активную подписку Azure, для которой вы являетесь администратором.

Выберите группу ресурсов и расположение группы ресурсов. Этот выбор не оказывает влияния на расположение, производительность и статус оплаты для этого клиента B2C.

![Создание ресурса B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="manage-your-azure-ad-b2c-tenant-resources"></a>Управление ресурсами клиента Azure AD B2C

Когда создание ресурса Azure AD в подписке Azure успешно завершится, вы увидите новый ресурс типа "Клиент B2C" рядом с другими ресурсами Azure.

Этот ресурс можно использовать в следующих целях:

- для перехода к подписке, где можно просмотреть сведения о выставлении счетов;
- для перехода к клиенту Azure AD B2C;
- Отправить запрос на техническую поддержку.
- для перемещения ресурса "Клиент B2C" в другую подписку Azure или в другую группу ресурсов.

![Параметры ресурсов B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Известные проблемы

### <a name="csp-subscriptions"></a>Подписки CSP

Сейчас клиент Azure AD B2C **нельзя** связать с подпиской CSP.

### <a name="self-imposed-restrictions"></a>Самоназначенные ограничения

Пользователь может установить региональное ограничение на создание ресурсов Azure. Такие ограничения могут помешать созданию ресурса Azure AD B2C. Для устранения проблемы снимите это ограничение.

## <a name="next-steps"></a>Дополнительная информация

Когда вы выполните эти шаги для каждого клиента Azure AD B2C, в выбранной подписке Azure начнется выставление счетов в соответствии с используемым соглашением Azure Direct или Enterprise.

Сведения об использовании и выставлении счетов вы можете просмотреть в выбранной подписке Azure. Также можно просмотреть подробные ежедневные отчеты об использовании с помощью [API отчетов об использовании](active-directory-b2c-reference-usage-reporting-api.md).
