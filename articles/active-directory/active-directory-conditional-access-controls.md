---
title: Элементы управления условным доступом в Azure Active Directory | Документация Майкрософт
description: Узнайте, как работают элементы управления условным доступом в Azure Active Directory.
services: active-directory
keywords: условный доступ к приложениям, условный доступ посредством Azure Active Directory, безопасный доступ к ресурсам организации, политики условного доступа
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 8271c4c88245e98fd3709c7279904d36ad009682
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
ms.locfileid: "32770729"
---
# <a name="access-controls-in-azure-active-directory-conditional-access"></a>Элементы управления условным доступом в Azure Active Directory 

С помощью [условного доступа Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md) можно контролировать доступ авторизованных пользователей к облачным приложениям. В политике условного доступа определяется реакция ("сделать это") на конкретное условие, при котором активируется политика ("в этом случае"). 

![Контроль](./media/active-directory-conditional-access-controls/10.png)


В контексте условного доступа 

- элемент "**в этом случае**" называется **условиями**;

- а "**следует сделать это**" называется **элементом управления доступом**.


Сочетание инструкции условия с элементами управления представляет собой политику условного доступа.

![Контроль](./media/active-directory-conditional-access-controls/61.png)

Каждый элемент управления определяет либо требование, которое должно быть выполнено осуществляющим вход пользователем или системой, либо ограничение действий пользователя после входа. 

Существуют два типа элементов управления. 

- **Элементы управления предоставлением прав** позволяют контролировать доступ.

- **Элементы управления сеансом** позволяют ограничить доступ в пределах сеанса.

В этом разделе описываются различные элементы управления, которые доступны для условного доступа Azure AD. 

## <a name="grant-controls"></a>Элементы управления предоставлением прав

С помощью элементов управления предоставлением прав можно полностью запретить доступ или разрешить доступ с дополнительными требованиями, выбрав необходимые элементы управления. Если указано несколько элементов управления, то можно требовать, чтобы:

- были выполнены все выбранные элементы управления (*И*); 
- был выполнен один выбранный элемент управления (*И*).

![Контроль](./media/active-directory-conditional-access-controls/17.png)



### <a name="multi-factor-authentication"></a>Многофакторная Идентификация

Этот элемент управления позволяет требовать прохождение Многофакторной идентификации для доступа к указанному облачному приложению. Данный элемент управления поддерживает следующие поставщики Многофакторной идентификации: 

- Многофакторная идентификация Azure 

- локальный поставщик многофакторной проверки подлинности, используемый совместно со службами федерации Active Directory (AD FS).
 
Многофакторная идентификация позволяет защитить ресурсы от несанкционированного входа пользователя, который получил доступ к основным учетным данным действительного пользователя.



### <a name="compliant-device"></a>Устройства, соответствующие требованиям

Политики условного доступа можно настроить на основе устройств. Цель политики условного доступа на основе устройств — предоставить доступ к настроенным ресурсам только с [управляемых устройств](active-directory-conditional-access-policy-connected-applications.md#managed-devices). Требование устройства, соответствующего требованиям, — это один из способов определения управляемого устройства. Если этот параметр выбран, то политика условного доступа разрешает попытки доступа с устройств, которые [зарегистрированы](device-management-introduction.md) в Azure Active Directory и помечены решением MDM как совместимые.

Дополнительные сведения см. в статье [Настройка политик условного доступа на основе устройств для Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

### <a name="hybrid-azure-ad-joined-device"></a>Гибридные устройства, присоединенные к Azure AD

Требование гибридного устройства, присоединенного к Azure AD, — это еще один способ настройки политики условного доступа на основе устройств. Это требование относится к настольным компьютерам, ноутбукам и корпоративным планшетам, присоединенным к локальному каталогу Active Directory. Если этот параметр выбран, то политика условного доступа разрешает попытки доступа с устройств, которые присоединены к локальному каталогу Active Directory и Azure Active Directory.  

Дополнительные сведения см. в статье [Настройка политик условного доступа на основе устройств для Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).





### <a name="approved-client-app"></a>Утвержденное клиентское приложение

Так как ваши сотрудники используют мобильные устройства как в личных целях, так и для выполнения рабочих задач, вам может потребоваться возможность защитить данные компании, предоставляемые на устройствах, даже в том случае, если вы не управляете этими устройствами.
Можно использовать [политики защиты приложений Intune](https://docs.microsoft.com/intune/app-protection-policy), чтобы защитить данные компании независимо от какого-либо решения по управлению мобильными устройствами (MDM).


Используя утвержденные клиентские приложения, можно требовать поддержку [политик защиты приложений Intune](https://docs.microsoft.com/intune/app-protection-policy) клиентским приложением, которое пытается получить доступ к вашим облачным приложениям. Например, можно ограничить доступ приложения Outlook к Exchange Online. Политика условного доступа, требующая утвержденное клиентское приложение, также называется [политикой условного доступа на основе приложений](active-directory-conditional-access-mam.md). Список поддерживаемых утвержденных клиентских приложений приведен в разделе [Требование утвержденного клиентского приложения](active-directory-conditional-access-technical-reference.md#approved-client-app-requirement).


### <a name="terms-of-use"></a>Условия использования

Вы можете потребовать от пользователя принять условия использования перед получением доступа к ресурсу. Как администратор вы можете настроить и изменить условия использования, отправив документ в формате PDF. Если пользователь находится в области этого элемента управления, то этот пользователь получит доступ к приложению только после принятия условий использования. 


### <a name="custom-controls"></a>Пользовательские элементы управления 

На странице "Условный доступ" можно создать пользовательские элементы управления, которые перенаправляют пользователей на совместимую службу для удовлетворения дальнейших требований вне Azure Active Directory. Это позволяет применять правила условного доступа с помощью многофакторной проверки подлинности и поставщиков проверки или создать собственную службу для такой проверки. В этом случае пользователь перенаправляется на внешнюю службу, выполняет все необходимые действия для собственной проверки или проверки подлинности и затем перенаправляется обратно в Azure Active Directory. Если пользователь успешно прошел собственную проверку или проверку подлинности, этот пользователь продолжает работу в потоке условного доступа. 

## <a name="custom-controls"></a>Пользовательские элементы управления

Пользовательские элементы управления являются функцией выпуска Azure Active Directory Premium P2. При использовании пользовательских элементов управления пользователи перенаправляются на совместимую службу для удовлетворения дальнейших требований вне Azure Active Directory. В этом случае пользователь перенаправляется на внешнюю службу, выполняет все необходимые действия для собственной проверки или проверки подлинности и затем перенаправляется обратно в Azure Active Directory. Azure Active Directory проверяет ответ, и если пользователь успешно прошел собственную проверку или проверку подлинности, этот пользователь продолжает работу в потоке условного доступа.

Эти элементы управления позволяют использовать определенные внешние и пользовательские службы как элементы управления условного доступа и расширить возможности условного доступа.

Сейчас поставщики включают следующие совместимые службы:

- [Duo Security](https://duo.com/docs/azure-ca)

- RSA

- [Trusona](https://www.trusona.com/docs/azure-ad-integration-guide)

Дополнительные сведения об этих службах можно получить у поставщиков служб.

### <a name="creating-custom-controls"></a>Создание пользовательских элементов управления

Чтобы создать пользовательский элемент управления, сначала обратитесь к поставщику, которым вы хотите воспользоваться. У каждого стороннего поставщика есть собственные требования и собственные процессы регистрации, подписки или иного подключения к службе, а также включения условного доступа. После выполнения этих требований поставщик предоставит вам блок данных в формате JSON. Эти данные позволят поставщику настроить условный доступ для вашего клиента, создать новый элемент управления и определить, как проверить, прошли ли пользователи проверку у поставщика, с помощью условного доступа.

Скопируйте данные JSON и вставьте их в соответствующее текстовое поле. Не изменяйте данные JSON, если точно не знаете, что делаете. Изменение данных JSON может привести к разрыву связи между поставщиком и корпорацией Майкрософт и к блокировке учетных записей ваших пользователей.

Пользовательский элемент управления можно создать в разделе **Управление** на странице **Условный доступ**.

![Контроль](./media/active-directory-conditional-access-controls/82.png)

Щелкните **Создать пользовательский элемент управления**. Откроется колонка с текстовым полем, в котором нужно указать данные JSON элемента управления.  


![Контроль](./media/active-directory-conditional-access-controls/81.png)


### <a name="deleting-custom-controls"></a>Удаление пользовательских элементов управления

Чтобы удалить пользовательский элемент управления, сначала убедитесь, что он не используется в политиках условного доступа. После завершения:

1. Перейдите к списку пользовательских элементов управления

2. Нажмите кнопку ...  

3. Нажмите кнопку **Удалить**.

### <a name="editing-custom-controls"></a>Изменение пользовательских элементов управления

Чтобы изменить пользовательский элемент управления, необходимо удалить текущий элемент управления и создать новый элемент управления с обновленными данными.




## <a name="session-controls"></a>Элементы управления сеансов

Элементы управления сеансом позволяют ограничивать возможности работы в облачном приложении. Элементы управления сеансов используются облачным приложением и зависят от дополнительных сведений, предоставляемых Azure AD в приложение о сеансе.

![Контроль](./media/active-directory-conditional-access-controls/31.png)

### <a name="use-app-enforced-restrictions"></a>Использование примененных к приложению ограничений

Этот элемент управления используется, чтобы требовать от Azure AD передачу сведений об устройстве в облачное приложение. Это позволяет облачному приложению определять, использует ли пользователь совместимое устройство или устройство в составе домена. Сейчас этот элемент управления поддерживается только для SharePoint как для облачного приложения. SharePoint использует сведения об устройствах для предоставления пользователям ограниченных или полных возможностей в зависимости от состояния устройства.
Дополнительные сведения о том, как требовать ограниченный доступ в SharePoint, см. в статье [Управление доступом с неуправляемых устройств](https://aka.ms/spolimitedaccessdocs).



## <a name="next-steps"></a>Дополнительная информация

- Если вы хотите узнать, как настроить политику условного доступа, прочитайте статью [Начало работы с условным доступом в Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

- Если вы готовы к настройке политик условного доступа для своей среды, см. статью [Рекомендации по работе с условным доступом в Azure Active Directory](active-directory-conditional-access-best-practices.md). 
