---
title: Выбор между облаком и сервером Azure MFA | Документация Майкрософт
description: Выберите подходящее решение многофакторной проверки подлинности, выяснив, что является объектом защиты и где находятся пользователи.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: get-started-article
ms.date: 10/02/2017
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.openlocfilehash: 8314d72aa2cc6787d3f65dd48cd693a0ac332c0a
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
---
# <a name="choose-the-azure-multi-factor-authentication-solution-for-you"></a>Выберите для себя решение "Многофакторная идентификация Microsoft Azure".
Так как существует несколько вариантов использования службы Многофакторной идентификации Azure (MFA), для определения наиболее подходящей версии следует ответить на некоторые вопросы.  Эти вопросы приведены ниже.

* [Что я пытаюсь защитить?](#what-am-i-trying-to-secure)
* [Где находятся пользователи?](#where-are-the-users-located)
* [Какие функции мне нужны?](#what-features-do-i-need)

В разделах этой статьи представлены рекомендации, которые помогут найти ответы на эти вопросы.

## <a name="what-am-i-trying-to-secure"></a>Что я пытаюсь защитить
Чтобы выяснить, какой из вариантов двухфакторной проверки подлинности вам нужен, сначала определите, что вы пытаетесь защитить с помощью второго метода проверки подлинности.  Это приложение в службе Azure?  Или в системе удаленного доступа?  Определив объект, который необходимо защитить, мы будем знать, где именно нужно активировать многофакторную проверку подлинности.  

| Что вы пытаетесь защитить | MFA в облаке | Сервер MFA |
| --- |:---:|:---:|
| Приложения Майкрософт, получающие данные напрямую из источника |● |● |
| Приложения SaaS в коллекции приложений |● |  |
| Веб-приложения, опубликованные через прокси приложения Azure AD |● |  |
| Приложения IIS, опубликованные не через прокси приложения Azure AD | |● |
| Удаленный доступ, например VPN или RDG | ● | ● |

## <a name="where-are-the-users-located"></a>Где находятся пользователи?
В зависимости от местонахождения пользователей можно определить, какое решение нам нужно для использования сервера MFA — облачное или локальное.

| Местонахождение пользователей | MFA в облаке | Сервер MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD и локальная служба AD с использованием федерации в AD FS |● |● |
| Azure AD и локальная служба AD с использованием DirSync, Azure AD Sync, Azure AD Connect без синхронизации хэшей паролей или сквозной аутентификации |● |● |
| Azure AD и локальная служба AD с использованием DirSync, Azure AD Sync, Azure AD Connect с синхронизации хэшей паролей или сквозной аутентификацией |● | |
| Локальная служба Active Directory | |● |

## <a name="what-features-do-i-need"></a>Какие функции мне нужны?
В приведенной ниже таблице сравниваются возможности облачной службы Многофакторной идентификации Azure и сервера Многофакторной идентификации.

| Функция | MFA в облаке | Сервер MFA |
| --- |:---:|:---:|
| Уведомление от мобильного приложения в качестве второго фактора | ● | ● |
| Код подтверждения мобильного приложения в качестве второго фактора | ● | ● |
| Телефонный вызов в качестве второго фактора | ● | ● |
| Одностороннее SMS в качестве второго фактора | ● | ● |
| Двустороннее SMS в качестве второго фактора | | ●  (Не рекомендуется)| 
| Маркеры оборудования в качестве второго фактора | | ● |
| Пароли приложений для клиентов Office 365, которые не поддерживают MFA | ● | |
| Администраторский контроль над методами проверки подлинности | ● | ● |
| Режим ПИН-кода | | ● |
| Предупреждение о мошенничестве |● | ● |
| Отчеты службы "Многофакторная идентификация Microsoft Azure" |● | ● |
| Разовый обход | | ● |
| Настраиваемые приветствия для телефонных вызовов | ● | ● |
| Настройка идентификатора вызывающей стороны для телефонных звонков | ● | ● |
| Надежные IP-адреса | ● | ● |
| Запоминание данных MFA для доверенных устройств | ● | |
| Условный доступ | ● | ● |
| Кэш |  | ● |

## <a name="next-steps"></a>Дополнительная информация

Теперь, когда вы имеете представление о различиях в возможностях службы "Многофакторная идентификация Azure" в облаке и на локальном сервере, можно приступать к настройке и использованию службы. **Выберите значок, соответствующий вашему сценарию.**

<center>

[![MFA в облаке](./media/concept-mfa-whichversion/cloud2.png)](howto-mfa-getstarted.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [![Сервер MFA](./media/concept-mfa-whichversion/server2.png)](howto-mfaserver-deploy.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
