---
title: Управление доступом к ресурсам Azure с помощью Azure Active Directory
description: Узнайте о методах управления доступом к ресурсам Azure с помощью различных возможностей Azure Active Directory.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: skwan
ms.assetid: f66abf54-3809-436c-92b6-018e1179780e
ms.service: role-based-access-control
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/05/2017
ms.author: rolyon
ms.reviewer: skwan
ms.openlocfilehash: 55bd18b127fea8a06e58f14873a584f0b5849906
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
---
# <a name="manage-access-to-azure-resources-with-azure-active-directory"></a>Управление доступом к ресурсам Azure с помощью Azure Active Directory

Управление удостоверениями и доступом в облачных ресурсах является критической функцией в любой организации, использующей облако. Azure Active Directory (Azure AD) — это система идентификации и доступа в Microsoft Azure.  

Прежде чем приступить к изучению функциональных областей, поддерживаемых Azure AD, просмотрите видео Locking down access to the Azure Cloud using SSO, Roles Based Access Control, and Conditional (Блокирование доступа к облаку Azure с помощью единого входа, управления доступом на основе ролей и условного доступа). Из этого видео вы узнаете:

- как настраивать единый вход на портал Azure с помощью локальной службы Active Directory;
- как использовать Azure RBAC для детального управления доступом к ресурсам в подписке;
- как применять правила строгой аутентификации, используя условный доступ Azure AD;
- как использовать удостоверения управляемой службы, которые позволяют ресурсам Azure автоматически выполнять аутентификацию в службах Azure, а разработчикам — не использовать ключи API или секреты.

> [!VIDEO https://www.youtube.com/embed/FKBoWWKRnvI]

## <a name="feature-areas"></a>Функциональные области
Azure AD предоставляет следующие возможности управления доступом к ресурсам Azure:

|||
|---|---|
| [Связь между клиентами и подписками Azure AD](rbac-and-directory-admin-roles.md) | Узнайте, как настроить Azure AD в качестве доверенного источника пользователей и групп для подписки Azure. |
| [Управление доступом на основе ролей (RBAC)](overview.md) | Точное управление доступом с помощью ролей, присвоенных пользователям, группам или субъектам-службам. |
| [Управление привилегированными пользователями с помощью RBAC](pim-azure-resource.md) | Управление привилегированным доступом за счет присвоения привилегированных ролей JIT. |
| [Условный доступ для управления Azure](conditional-access-azure-management.md) | Настройка политики условного доступа для разрешения или запрета доступа к конечным точкам управления Azure. |
| [Управляемые удостоверения службы (MSI)](../active-directory/pp/msi-overview.md) | Назначение ресурсам Azure, таким как виртуальные машины, собственных удостоверений, чтобы не вводить учетные данные в код. |

 