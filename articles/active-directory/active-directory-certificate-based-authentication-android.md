---
title: Аутентификация на основе сертификата в Azure Active Directory на устройстве Android
description: Узнайте о поддерживаемых сценариях и требованиях к настройке аутентификации на основе сертификата в решениях на устройствах Android.
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: article
ms.date: 01/15/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: annaba
ms.openlocfilehash: ef58fd6c4701f367c6b8664c9cf9ee76e15fbd70
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
ms.locfileid: "33880756"
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a>Аутентификация на основе сертификата в Azure Active Directory на устройстве Android

Для устройств Android можно применять аутентификацию на основе сертификатов (CBA) в Azure Active Directory. Для этого на устройстве используется сертификат клиента при подключении к:

* мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;
* клиентам Exchange ActiveSync (EAS).

Настройка данной функции избавляет от необходимости ввода имени пользователя и пароля в определенных почтовых клиентах и приложениях Microsoft Office на мобильных устройствах.

В этой статье приведены требования и поддерживаемые сценарии для настройки CBA на устройстве iOS (Android) для пользователей клиентов в тарифных планах Office 365 корпоративный, бизнес, для образования, для государственных организаций США, Китая и Германии.

В тарифных планах Office 365 US Government Defense и Federal доступна предварительная версия этой функции.

## <a name="microsoft-mobile-applications-support"></a>Поддержка мобильных приложений Microsoft

| Приложения | Поддержка |
| --- | --- |
| Приложение Azure Information Protection |![Проверка][1] |
| Корпоративный портал Intune |![Проверка][1] |
| Microsoft Teams |![Проверка][1] |
| OneNote |![Проверка][1] |
| OneDrive |![Проверка][1] |
| Outlook |![Проверка][1] |
| Power BI |![Проверка][1] |
| Skype для бизнеса |![Проверка][1] |
| Word/Excel/PowerPoint |![Проверка][1] |
| Yammer |![Проверка][1] |

### <a name="implementation-requirements"></a>Требования к реализации

На устройстве должна быть установлена ОС Android версии 5.0 (Lollipop) и выше.

Необходимо настроить сервер федерации.

Чтобы служба Azure Active Directory могла отзывать сертификат клиента, маркер AD FS должен иметь следующие утверждения:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` (серийный номер сертификата клиента);
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` (строка для издателя сертификата клиента).

Azure Active Directory добавляет эти утверждения в маркер обновления, если они доступны в маркере AD FS (или любом другом токене SAML). Когда требуется проверить маркер обновления, эта информация используется для проверки отзыва.

Рекомендуем обновить страницы ошибок AD FS вашей организации следующими сведениями:

* требованием установки Microsoft Authenticator для Android;
* инструкциями о получении сертификата пользователя.

Дополнительные сведения см. в статье о [настройке страниц входа AD FS](https://technet.microsoft.com/library/dn280950.aspx).

Некоторые приложения Office (с поддержкой современной проверки подлинности) отправляют в Azure AD запрос с текстом *prompt=login*. По умолчанию Azure AD преобразует *prompt=login* в запросе к службам AD FS в текст *wauth=usernamepassworduri* (запрашивает у AD FS аутентификацию с помощью имени пользователя и пароля) и *wfresh=0* (указывает AD FS игнорировать состояние единого входа и выполнять аутентификацию заново). Чтобы включить проверку подлинности на основе сертификатов для этих приложений, необходимо изменить поведение Azure AD по умолчанию. Задайте для параметра *PromptLoginBehavior* в настройках федеративного домена значение *Отключено*.
Для выполнения этой задачи можно использовать командлет [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0):

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`

## <a name="exchange-activesync-clients-support"></a>Поддержка клиентов Exchange ActiveSync

Поддерживаются некоторые приложения Exchange ActiveSync, работающие на Android 5.0 (Lollipop) или более поздней версии. Чтобы определить, поддерживает ли почтовая программа эту функцию, обратитесь к разработчику приложения.

## <a name="next-steps"></a>Дополнительная информация

Чтобы настроить аутентификацию на основе сертификата в своей среде, ознакомьтесь с инструкциями в статье [Get started with certificate-based authentication in Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) (Приступая к работе с аутентификацией на основе сертификата в Azure Active Directory).

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
