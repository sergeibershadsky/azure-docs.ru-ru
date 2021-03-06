---
title: Миграция из мобильных служб в мобильное приложение службы приложений
description: Простая миграция приложения мобильных служб в мобильное приложение службы приложений
services: app-service\mobile
documentationcenter: ''
author: conceptdev
manager: crdun
editor: ''
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: crdun
ms.openlocfilehash: 5001704f47af0c7b07744f1dceb7aa58bdb6448c
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2018
---
# <a name="article-top"></a>Перенос существующей мобильной службы Azure в службу приложений Azure
Благодаря [общей доступности службы приложений Azure]сайты мобильных служб Azure можно легко переносить на месте, что позволяет пользоваться преимуществами всех компонентов службы приложений Azure.  В этом документе объясняется, что происходит во время переноса сайта из мобильных служб Azure в службу приложений Azure.

## <a name="what-does-migration-do"></a>Что происходит с сайтом во время переноса
При переносе мобильная служба Azure преобразуется в приложение [службы приложений Azure]. При этом ее код не изменяется.  Центры уведомлений, подключение данных SQL, параметры проверки подлинности, запланированные задания и имя домена также останутся без изменений.  Мобильные клиенты, использующие мобильную службу Azure, будут работать в обычном режиме.  После переноса в службу приложений Azure ваша служба будет перезапущена.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Зачем переносить сайт
Корпорация Майкрософт рекомендует перенести мобильную службу Azure, чтобы воспользоваться следующими преимуществами компонентов службы приложений Azure:

* Новые компоненты узла, включая [веб-задания] и [пользовательские доменные имена].
* мониторинг и устранение неполадок с помощью [Application Insights];
* Встроенные средства DevOps, включая [промежуточных слотов], откат и тестирование в рабочей среде.
* [Автоматическое масштабирование], балансировка нагрузки и [мониторинг производительности].

Дополнительные сведения о преимуществах службы приложений Azure см. в статье, посвященной [сравнению мобильных служб и службы приложений].

## <a name="before-you-begin"></a>Перед началом работы
Перед выполнением основных операций на сайте необходимо создать резервную копию мобильной службы и базы данных SQL.

## <a name="migrating-site"></a>Перенос сайтов
В ходе этого процесса будут перенесены все сайты в пределах одного региона Azure.

Чтобы перенести сайт, выполните следующие действия:

1. Войдите на [классическом портале Azure].
2. В регионе выберите мобильную службу для переноса.
3. Нажмите кнопку **Перенести в службу приложений**.

   ![Кнопка «Перенести»][0]
4. Откроется диалоговое окно «Перенос в службу приложений».
5. Введите имя своей мобильной службы в соответствующее поле.  Например, если используется имя домена contoso.azure-mobile.net, введите в соответствующее поле *contoso*.
6. Нажмите кнопку с галочкой.

Мониторинг состояния миграции в мониторе активности На классическом портале Azure ваш сайт отображается в состоянии *миграции*.

  ![Монитор активности переноса][1]

Каждый перенос мобильной службы может длиться от 3 до 15 минут.  Сайт остается доступным во время миграции.
По завершении миграции сайт будет перезапущен,  и в это время он будет недоступен. Это может длиться несколько секунд.

## <a name="finalizing-migration"></a>Завершение переноса
Необходимо запланировать тестирование сайта с мобильного клиента по завершении переноса.  Убедитесь, что вы можете выполнять все стандартные действия клиента, не внося изменения в мобильный клиент.  

### <a name="update-app-service-tier"></a>Выбор соответствующей ценовой категории службы приложений
После переноса службы приложений Azure вы получаете дополнительную свободу в выборе цены.

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню "Параметры" щелкните **План служб приложений**.
5. Щелкните плитку **Ценовая категория**.
6. Щелкните плитку, которая отвечает вашим требованиям, а затем нажмите кнопку **Выбрать**.  Чтобы просмотреть доступные ценовые категории, нажмите кнопку **Просмотреть все**.

Для начала мы рекомендуем следующие категории:

| Ценовая категория мобильной службы | Ценовая категория службы приложений |
|:--- |:--- |
| Free |Бесплатный F1 |
| базовая; |Базовая B1 |
| Стандартная |Стандартный S1 |

Вы можете подобрать подходящую ценовую категорию для своего приложения.  Дополнительные сведения см. на странице [Цены службы приложений].

> [!TIP]
> Категория службы приложений "Стандартный" предусматривает доступ к разным функциям и компонентам, которые могут вам понадобиться, включая [промежуточных слотов], автоматическое резервное копирование и автомасштабирование.  Заодно ознакомьтесь с новыми возможностями.
>
>

### <a name="review-migration-scheduler-jobs"></a>Просмотр перенесенных заданий планировщика
Задания планировщика не будут отображаться в течение примерно 30 минут после переноса.  Запланированные задания будут выполняться в фоновом режиме.
Чтобы просмотреть запланированные задания, которые снова стали видимыми, сделайте следующее.

1. Войдите на [портале Azure].
2. Щелкните **Обзор**, введите **Расписание** в поле *Фильтр*, а затем выберите **Коллекции планировщика**.

После переноса будет доступно ограниченное количество бесплатных заданий планировщика.  Просмотрите сведения об использовании заданий и [планы планировщика Azure].

### <a name="configure-cors"></a>Настройка CORS при необходимости
Общий доступ к ресурсам независимо от источника — это способ предоставления веб-сайту доступа к веб-API на другом домене.  Если вы используете мобильные службы Azure со связанным веб-сайтом, вам понадобится настроить CORS как часть переноса.  Если вы обращаетесь к мобильным службам Azure только с мобильных устройств, в большинстве случаев вам не нужно настраивать CORS.

Перенесенные параметры CORS доступны в параметре приложения **MS_CrossDomainWhitelist**.  Чтобы перенести сайт в средство CORS службы приложений, выполните следующие действия:

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню API щелкните **CORS**.
5. Введите в появившееся поле разрешенные источники, нажимая клавишу ВВОД после ввода каждого источника.
6. Создав список разрешенных источников, нажмите кнопку "Сохранить".

> [!TIP]
> Одно из преимуществ использования службы приложений Azure заключается в том, что ваш веб-сайт и мобильная служба работают на одном сайте.  Дополнительные сведения см. в разделе [Дальнейшие действия](#next-steps).
>
>

### <a name="download-publish-profile"></a>Загрузка нового профиля публикации
Профиль публикации сайта изменяется при переходе на службу приложений Azure.  Если вы собираетесь опубликовать свой сайт из среды Visual Studio, вам потребуется новый профиль публикации.  Загрузка нового профиля публикации

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. Щелкните **Скачать профиль публикации**.

Файл PublishSettings будет скачан на ваш компьютер.  Обычно он называется так: *имя_сайта*.PublishSettings.  Затем вы можете импортировать параметры публикации в существующий проект.

1. Откройте Visual Studio и проект мобильной службы Azure.
2. Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать**.
3. Щелкните **Импорт**.
4. Нажмите кнопку **Обзор** и выберите скачанный файл параметров публикации.  Щелкните **ОК**
5. Щелкните **Проверить подключение**, чтобы проверить параметры публикации.
6. Щелкните **Опубликовать**, чтобы опубликовать сайт.

## <a name="working-with-your-site"></a>Работа с сайтом после переноса
После переноса вы будете работать с новой службой приложений на [портале Azure].  Ниже приведены некоторые пояснения к конкретным операциям, которые вы обычно выполняли на [классическом портале Azure], а также к их эквивалентам в службе приложений.

### <a name="publishing-your-site"></a>Загрузка и публикация перенесенного сайта
Вы можете получить доступ к своему сайту через GIT или FTP и повторно опубликовать его с помощью разных средств, включая WebDeploy, TFS, Mercurial, GitHub и FTP.  Учетные данные развертывания переносятся со всеми остальными данными сайта.  Если вы не настроили учетные данные развертывания, вы можете сбросить их.

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню "Публикация" щелкните **Учетные данные развертывания**.
5. Введите новые учетные данные развертывания в соответствующие поля, а затем нажмите кнопку "Сохранить".

Вы можете использовать эти учетные данные, чтобы клонировать сайт с помощью GIT или настроить автоматическое развертывание из GitHub, TFS или Mercurial.  Дополнительные сведения см. в [документации по развертыванию службы приложений Azure].

### <a name="appsettings"></a>Параметры приложения
Большинство параметров перенесенной мобильной службы доступны в разделе «Параметры приложения».  Вы можете получить список параметров приложения на [портале Azure].
Чтобы просмотреть или изменить параметры приложения, выполните следующие действия:

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню "Общие" щелкните **Параметры приложения** .
5. Прокрутите страницу вниз до раздела «Параметры приложения» и найдите параметры своего приложения.
6. Щелкните значение параметра приложения, чтобы изменить его.  Нажмите кнопку **Сохранить**, чтобы сохранить значение.

Одновременно можно обновить несколько параметров приложения.

> [!TIP]
> Например, есть два параметра приложения с одинаковым значением:  *ApplicationKey* и *MS\_ApplicationKey*.  Обновите значения двух этих параметров одновременно.
>
>

### <a name="authentication"></a>Проверка подлинности
На перенесенном сайте все параметры проверки подлинности доступны как параметры приложения.  Чтобы обновить параметры проверки подлинности, необходимо сначала изменить параметры соответствующего приложения.  В таблице ниже приведены правильные параметры приложения для поставщика проверки подлинности.

| Поставщик | Идентификатор клиента | Секрет клиента | Другие параметры |
|:--- |:--- |:--- |:--- |
| Учетная запись Майкрософт |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Примечание. Параметр **MS\_AadTenants** сохраняется как разделенный запятыми список доменов клиента (поля "Разрешенные клиенты" на портале мобильных служб).

> [!WARNING]
> **Не используйте механизмы проверки подлинности в меню «Параметры».**
>
> В службе приложений Azure реализована отдельная система проверки подлинности и авторизации без кода. Доступ к ней можно получить из меню "Параметры" в разделе *Проверка подлинности и авторизация* (а также из устаревшего параметра *Проверка подлинности мобильного приложения*).  Эти параметры несовместимы с перенесенной мобильной службой Azure.  Вы можете [обновить свой сайт](app-service-mobile-net-upgrading-from-mobile-services.md), чтобы пользоваться преимуществами проверки подлинности службы приложений Azure.
>
>

### <a name="easytables"></a>Данные
На портале Azure вкладка *Данные* в мобильных службах заменена элементом *Простые таблицы*.  Для доступа к элементу «Простые таблицы» выполните следующие действия:

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню "Мобильные устройства" щелкните **Простые таблицы**.

Вы можете добавить новую таблицу, нажав кнопку **Добавить**, или открыть существующую, щелкнув ее имя.  В этой колонке можно выполнять разные операции, включая:

* изменение разрешений таблицы;
* редактирование рабочих сценариев;
* управление схемой таблицы;
* удаление таблицы;
* очистка содержимого таблицы;
* удаление определенных строк таблицы.

### <a name="easyapis"></a>API
На портале Azure вкладка *API* в мобильных службах заменена элементом *Простые API*.  Для доступа к элементу «Простые API» выполните следующие действия:

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню "Мобильные устройства" щелкните **Простые API**.

Перенесенные API-интерфейсы отобразятся в колонке.  Кроме того, в этой колонке можно добавить новый API.  Чтобы управлять определенным API, щелкните его.
В новой колонке можно настроить разрешения и изменить сценарии для API.

### <a name="on-demand-jobs"></a>Задания планировщика
Все задания планировщика доступны в разделе коллекций заданий планировщика.  Чтобы перейти к заданиям планировщика, выполните следующие действия.

1. Войдите на [портале Azure].
2. Щелкните **Обзор**, введите **Расписание** в поле *Фильтр*, а затем выберите **Коллекции планировщика**.
3. Выберите коллекцию заданий для сайта.  Она называется *имя_сайта*-Jobs.
4. Щелкните **Параметры**.
5. В разделе "Управление" щелкните **Задания планировщика**.

Отобразится список запланированных заданий с частотой, указанной перед переносом.  Задания по требованию будут отключены.  Чтобы запустить задания по требованию, выполните следующие действия.

1. Выберите нужное задание.
2. При необходимости щелкните **Включить**, чтобы включить задание.
3. Щелкните **Параметры**, а затем — **Расписание**.
4. Выберите для повторения значение **Один раз**, а затем нажмите кнопку **Сохранить**.

Ваши задания по требованию находятся в папке `App_Data/config/scripts/scheduler post-migration`.  Мы рекомендуем преобразовывать все задания по требованию в [веб-задания] или [функции].  Новые задания планировщика необходимо записывать как [веб-задания] или [функции].

### <a name="notification-hubs"></a>Центры уведомлений
Мобильные службы используют центры уведомлений для push-уведомлений.  Следующие параметры приложений используются для связывания центра уведомлений с мобильной службой после переноса.

| Параметр приложения | ОПИСАНИЕ |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Пространство имен центра уведомлений |
| **MS\_NotificationHubName** |Имя центра уведомлений |
| **MS\_NotificationHubConnectionString** |Строка подключения к центру уведомлений |
| **MS\_NamespaceName** |Псевдоним для MS_PushEntityNamespace |

Вы можете управлять своим центром уведомлений с помощью [портале Azure].  Запишите имя центра уведомлений (его можно найти с помощью параметров приложения).

1. Войдите на [портале Azure].
2. Щелкните **Обзор**, а затем выберите **Центры уведомлений**.
3. Щелкните имя центра уведомлений, связанного с мобильной службой.

> [!NOTE]
> Если центр уведомлений представлен смешанным типом, он не будет отображаться.  «Смешанные» центры уведомлений используют как компоненты центров уведомлений, так и устаревшие компоненты служебной шины.  Прежде чем продолжать, вам нужно [преобразовать смешанные пространства имен].  После завершения преобразования центр уведомлений отобразится на [портале Azure].
>
>

Дополнительную информацию см. в документации по [центрам уведомлений].

> [!TIP]
> Компоненты управления центрами уведомлений на [портале Azure] все еще доступны в режиме предварительной версии.  [классическом портале Azure] остается доступным для управления всеми центрами уведомлений.
>
>

### <a name="legacy-push"></a>Параметры отправки push-уведомлений устаревшего типа
Если вы настроили отправку push-уведомлений в мобильной службе до выхода центров уведомлений, значит вы используете *отправку push-уведомлений устаревшего типа*.  Если вы используете push-уведомления и не видите центр уведомлений в конфигурации, скорее всего, вы используете *отправку push-уведомлений устаревшего типа*.  Перенос этой функции выполняется вместе с другими компонентами.  Тем не менее после переноса рекомендуется обновить центры уведомлений.

До этого времени все параметры отправки push-уведомлений (исключением является сертификат APN) остаются доступными в окне параметров приложения.  Чтобы обновить сертификат APNS, замените соответствующий файл в файловой системе.

### <a name="app-settings"></a>Другие параметры приложения
Из мобильной службы перенесены приведенные ниже дополнительные параметры приложения. Они доступны в разделе *Параметры* > *Параметры приложения*.

| Параметр приложения | ОПИСАНИЕ |
|:--- |:--- |
| **MS\_MobileServiceName** |Имя приложения |
| **MS\_MobileServiceDomainSuffix** |Префикс домена. Например, azure-mobile.net. |
| **MS\_ApplicationKey** |Ключ приложения |
| **MS\_MasterKey** |Главный ключ приложения |

Ключ и главный ключ приложения должны совпадать с ключами приложения в исходной мобильной службе.  В частности, ключ приложения отправляется мобильными клиентами для проверки использования ими мобильного API.

### <a name="cliequivalents"></a>Эквиваленты командной строки
Команду *azure mobile* больше нельзя использовать для управления сайтом мобильных служб Azure.  Вместо этой команды многие функции выполняет команда *azure site*.  В следующей таблице приведены эквиваленты часто используемых команд.

| Команда *Azure Mobile* | Эквивалентная команда *Azure Site* |
|:--- |:--- |
| mobile locations |site location list |
| mobile list |site list |
| mobile show *имя* |site show *имя* |
| mobile restart *имя* |site restart *имя* |
| mobile redeploy *имя* |site deployment redeploy *иденификатор_фиксации* *имя* |
| mobile key set *имя* *тип* *значение* |site appsetting delete *ключ* *значение* <br/> site appsetting add *ключ*=*значение* *имя* |
| mobile config list *имя* |site appsetting list *имя* |
| mobile config get *имя* *ключ* |site appsetting show *ключ* *имя* |
| mobile config set *имя* *ключ* |site appsetting delete *ключ* *значение* <br/> site appsetting add *ключ*=*значение* *имя* |
| mobile domain list *имя* |site domain list *имя* |
| mobile domain add *имя* *домен* |site domain add *домен* *имя* |
| mobile domain delete *имя* |site domain delete *домен* *имя* |
| mobile scale show *имя* |site show *имя* |
| mobile scale change *имя* |site scale mode *режим* *имя* <br /> site scale instances *экземпляры* *имя* |
| mobile appsetting list *имя* |site appsetting list *имя* |
| mobile appsetting add *имя* *ключ* *значение* |site appsetting add *ключ*=*значение* *имя* |
| mobile appsetting delete *name* *key* |site appsetting delete *ключ* *значение* |
| mobile appsetting show *имя* *ключ* |site appsetting delete *ключ* *значение* |

Обновите параметры проверки подлинности или push-уведомлений, обновив соответствующие параметры приложения.
Измените файлы и опубликуйте сайт с помощью FTP или GIT.

### <a name="diagnostics"></a>Диагностика и ведение журналов
В службе приложений Azure ведение журналов диагностики обычно отключено.  Чтобы включить ведение журналов диагностики, выполните следующие действия.

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. По умолчанию откроется колонка "Параметры".
4. В меню «Компоненты» выберите элемент **Журналы диагностики** .
5. Щелкните **Вкл.** для следующих журналов: **Ведение журналов приложения (файловая система)**, **Подробные сообщения об ошибках** и **Трассировка неудачно завершенных запросов**.
6. Щелкните элемент **Файловая система** , чтобы включить ведение журналов веб-сервера.
7. Нажмите кнопку **Сохранить**

Чтобы просмотреть журналы, выполните следующие действия:

1. Войдите на [портале Azure].
2. Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя перенесенной мобильной службы.
3. Нажмите кнопку **Средства**.
4. В меню «Наблюдение» выберите пункт **Поток журнала** .

Создаваемые журналы будут отображаться в окне.  Кроме того, вы можете скачать журналы для последующего анализа с помощью учетных данных развертывания. Дополнительные сведения см. в документации по [ведению журналов].

## <a name="known-issues"></a>Известные проблемы
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>Удаление перенесенного клона мобильного приложения приводит к недоступности сайта
Если клонировать перенесенную мобильную службу с помощью Azure PowerShell, а затем удалить клон, запись DNS для рабочей службы будет удалена.  В результате сайт будет недоступен из Интернета.  

Решение. Если вы хотите клонировать сайт, сделайте это на портале.

### <a name="changing-webconfig-does-not-work"></a>Изменение Web.config не поддерживается
При наличии сайта ASP.NET изменить файл `Web.config` нельзя.  Во время запуска служба приложений Azure создает подходящий файл `Web.config` для поддержки среды выполнения мобильных служб.  Некоторые параметры (например, пользовательские заголовки) можно переопределить с помощью файла преобразования XML.  Создайте файл с именем `applicationHost.xdt`; он должен располагаться в каталоге `D:\home\site` службы Azure.  Загрузите файл `applicationHost.xdt`, используя пользовательский скрипт развертывания, или непосредственно с помощью Kudu.  Ниже приведен пример документа.

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Дополнительные сведения см. в документации с [примерами преобразования XDT] на сайте GitHub.

### <a name="migrated-mobile-services-cannot-be-added-to-traffic-manager"></a>Перенесенные мобильные службы нельзя добавить в диспетчер трафика
При создании профиля диспетчера трафика нельзя напрямую выбрать для профиля перенесенную мобильную службу.  Необходимо использовать внешнюю конечную точку.  Внешнюю конечную точку можно добавить только через PowerShell.  Дополнительные сведения см. в [руководстве по диспетчеру трафика](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Дальнейшие действия
После переноса приложения в службу приложений вы сможете использовать дополнительные функции.

* Развертывание [промежуточных слотов] позволяет поэтапно вносить изменения в сайт и выполнять A/B-тестирование.
* [Веб-задания] заменяют запланированные задания по требованию.
* Вы можете [непрерывно развертывать] свой сайт, связав его с GitHub, TFS или Mercurial.
* Для мониторинга сайта можно использовать [Application Insights] .
* Обслуживайте веб-сайт и мобильный API, используя один и тот же код.

### <a name="upgrading-your-site"></a>Обновление сайта мобильных служб до пакета SDK для мобильных приложений Azure
* Для проектов серверов на основе Node.js новый [пакет SDK Node.js для мобильных приложений] предусматривает ряд новых возможностей. Например, теперь можно осуществлять локальную разработку и отладку, использовать любую версию Node.js выше 0.10 и выполнять настройку с любой версией ПО промежуточного слоя Express.js.
* Для проектов серверов на основе .NET новый [пакет SDK NuGet для мобильных приложений](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) предусматривает гибкие возможности использования зависимостей NuGet.  Эти пакеты поддерживают проверку подлинности новой службы приложений и использование с любым проектом ASP.NET. Дополнительные сведения об обновлении см. в статье [Обновление существующего приложения мобильной службы Azure .NET до службы приложений](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Цены службы приложений]: https://azure.microsoft.com/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Автоматическое масштабирование]: ../app-service/web-sites-scale.md
[службы приложений Azure]: ../app-service/app-service-web-overview.md
[классическом портале Azure]: https://manage.windowsazure.com
[портале Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/regions/
[планы планировщика Azure]: ../scheduler/scheduler-plans-billing.md
[непрерывно развертывать]: ../app-service/app-service-continuous-deployment.md
[преобразовать смешанные пространства имен]: https://azure.microsoft.com/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[пользовательские доменные имена]: ../app-service/app-service-web-tutorial-custom-domain.md
[Fiddler]: http://www.telerik.com/fiddler
[общей доступности службы приложений Azure]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[Hybrid Connections]: ../app-service/app-service-hybrid-connections.md
[ведению журналов]: ../app-service/web-sites-enable-diagnostic-log.md
[пакет SDK Node.js для мобильных приложений]: https://github.com/azure/azure-mobile-apps-node
[сравнению мобильных служб и службы приложений]: app-service-mobile-value-prop-migration-from-mobile-services.md
[центрам уведомлений]: ../notification-hubs/notification-hubs-push-notification-overview.md
[мониторинг производительности]: ../app-service/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[промежуточных слотов]: ../app-service/web-sites-staged-publishing.md
[VNet]: ../app-service/web-sites-integrate-with-vnet.md
[примерами преобразования XDT]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[функции]: ../azure-functions/functions-overview.md
