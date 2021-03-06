---
title: Настройка шаблона устройства в приложении Azure IoT Central | Документация Майкрософт
description: Узнайте, как настроить измерения, параметры, свойства, правила и панели мониторинга в шаблоне устройства.
services: iot-central
author: viv-liu
ms.author: viviali
ms.date: 04/16/2018
ms.topic: article
ms.prod: microsoft-iot-central
manager: timlt
ms.openlocfilehash: 52c6c8fe4375354d650f92b73bffc288c9a2ccfe
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34201515"
---
# <a name="set-up-a-device-template"></a>Настройка шаблона устройства

Шаблон устройства — это схема, которая определяет характеристики и поведение типа устройства, которое подключается к приложению Microsoft Azure IoT Central.

Например, конструктор может создать шаблон устройства для подключенного к Интернету вещей вентилятора, который имеет:

- измерение телеметрии температуры;

- измерение событий ошибки двигателя вентилятора;

- измерение состояния работы вентилятора;

- параметр скорости вентилятора;

- свойство расположения;

- правила отправки оповещений;

- панель мониторинга, которая обеспечивает полный обзор устройства.

На основе этого шаблона устройства можно создавать и подключать реальные вентиляторы с такими именами, как **fan-1** и **fan-2**. Все эти вентиляторы имеют измерения, параметры, свойства, правила и панель мониторинга, которые пользователи вашего приложения могут отслеживать и контролировать.

> [!NOTE]
Только администраторы и конструкторы могут создавать, изменять и удалять шаблоны устройств. Любой пользователь может создавать устройства на странице **Device Explorer** из существующих шаблонов устройств.

## <a name="create-a-new-device-template"></a>Создание шаблона нового устройства

1. Перейдите на страницу **конструктора приложений**.

1. Чтобы создать пустой шаблон, выберите **Create Device Template** (Создать шаблон устройства), а затем выберите **Пользовательский**.

1. Введите имя для нового шаблона устройства и нажмите кнопку **Создать**.

    ![Страница сведений об устройстве](./media/howto-set-up-template/devicedetailspage.png)

1. Теперь вы находитесь на странице **сведений об устройстве** нового имитированного устройства. Имитированное устройство автоматически создается при создании нового шаблона устройства. Оно передает данные и может контролироваться как реальное устройство.

Теперь взглянем на каждую из вкладок страницы **сведений об устройстве**.

## <a name="measurements"></a>Измерения

Измерения — это данные, поступающие от устройства. Можно добавить несколько измерений в шаблон устройства в зависимости от его возможностей. В настоящее время телеметрия и события являются типами поддерживаемых измерений.

- **Измерения телеметрии** — это непрерывный поток числовых данных, которые устройство собирает с течением времени. Например, температура.
- **Измерения событий** представляют собой данные определенной точки во времени, которые представляют что-то значимое, связанное с устройством. События имеют степень серьезности, представляющую уровень их важности. Например, ошибка мотора вентилятора.
- **Измерения состояния** представляют состояние устройства или его компонентов в течение определенного периода времени. Например, режим вентилятора, который может быть определен как работающий и остановленный.

### <a name="create-a-telemetry-measurement"></a>Создание измерения телеметрии
Чтобы добавить новое измерение телеметрии, нажмите кнопку **​​+ New Measurement** (+ Новое измерение), которая открывает форму для выбора типа измерения. Щелкните **Телеметрия** и введите сведения в форму **Create Telemetry** (Создание телеметрии).

> [!NOTE]
> Когда подключено реальное устройство, обратите внимание на имя измерения, которое сообщает устройство. Имя должно точно соответствовать **имени поля** измерения.

Например, можно добавить новое измерение телеметрии температуры:

![Форма измерений](./media/howto-set-up-template/measurementsform.png)

После нажатия кнопки **Сохранить** в списке измерений появится измерение **Температура**, и оператор сможет увидеть визуализацию данных о температуре, которые собирает устройство.

![График измерений](./media/howto-set-up-template/measurementsgraph.png)

### <a name="create-an-event-measurement"></a>Создание измерения событий
Чтобы добавить новое измерение событий, нажмите кнопку **​​+ New Measurement** (​​+ Новое измерение), которая открывает форму для выбора типа измерения. Щелкните **Событие** и введите сведения в форму **Create Event** (Создание события).

В этой форме укажите **отображаемое имя**, **имя поля** и **серьезность** события. Можно выбрать из трех доступных уровней серьезности — **ошибка**, **предупреждение** и **сведения**.  

Например, можно добавить новое событие "Ошибка мотора вентилятора".

![Форма измерений событий](./media/howto-set-up-template/eventmeasurementsform.png)

После нажатия кнопки **Сохранить** в списке измерений появится измерение **Ошибка мотора вентилятора**, и оператор сможет увидеть визуализацию данных о событии, которые отправляет устройство.

![Диаграмма измерения событий](./media/howto-set-up-template/eventmeasurementschart.png)

Чтобы просмотреть дополнительные сведения о событии, щелкните событие на диаграмме:

![Сведения об измерении событий](./media/howto-set-up-template/eventmeasurementsdetail.png)


### <a name="create-a-state-measurement"></a>Создание измерения состояния
Чтобы добавить новое измерение состояния, нажмите кнопку **​​+ New Measurement** (​​+ Новое измерение), которая открывает форму для выбора типа измерения. Щелкните **Состояние** и введите сведения в форму **Create State** (Создание состояния).

В этой форме укажите **отображаемое имя**, **имя поля** и возможные **значения** события. Каждое **значение** также может иметь отображаемое имя, которое будет использоваться при отображении значения в диаграммах и таблицах.

Например, вы можете добавить новое состояние "Режим вентилятора", которое имеет два возможных значения, отправляемых устройством: **Работает** и **Остановлено**.

![Форма измерений состояния](./media/howto-set-up-template/statemeasurementsform.png)

После нажатия кнопки **Сохранить** в списке измерений появится измерение **Режим вентилятора**, и оператор сможет увидеть визуализацию данных о состоянии, которые отправляет устройство.

![Диаграмма измерений состояния](./media/howto-set-up-template/statemeasurementschart.png)

В случае, если в течение небольшого периода времени количество отправленных устройством точек данных слишком велико, измерение состояния отображается с другими визуальными элементами, как показано ниже. Если вы щелкните диаграмму, то все точки данных за этот период времени будут отображаться в хронологическом порядке. Вы также можете сузить диапазон времени, чтобы увидеть измерения, нанесенные на график.

![Сведения об измерениях состояния](./media/howto-set-up-template/statemeasurementsdetail.png)


## <a name="settings"></a>Параметры

Параметры предназначены для управления устройством. Они позволяют операторам вашего приложения предоставлять входные данные для устройства. Вы можете добавить несколько параметров в шаблон устройства, которые отображаются в виде плиток на вкладке **Параметры** для использования операторами. Существует шесть видов параметров, которые вы можете добавить: номер, текст, дата, переключатель, список выбора и метка раздела.

> [!NOTE]
> Когда подключено реальное устройство, обратите внимание на имя параметра, которое сообщает устройство. Имя должно точно соответствовать **имени поля** параметра.

Параметры могут быть в одном из трех состояний. Эти состояния выводятся на устройстве.

- **Синхронизировано**: устройство изменилось с учетом значения параметра.

- **Ожидание**: устройство в настоящее время меняется в соответствии со значением параметра.

- **Ошибка**: устройство вернуло ошибку.

Например, вы можете добавить новый параметр скорости вращения вентилятора:

![Форма параметров](./media/howto-set-up-template/settingsform.png)

После нажатия кнопки **Сохранить** параметр **Fan speed** (Скорость вентилятора) появляется в виде плитки. Его можно использовать для изменения скорости вращения вентилятора устройства.

> [!NOTE]
> После создания новой плитки можно опробовать новый параметр. Во-первых, отключите режим конструктора в верхней правой части экрана:

![Плитка параметров](./media/howto-set-up-template/settingstile.png)

## <a name="properties"></a>properties

Свойства являются метаданными устройства, связанными с этим устройством (например, расположение устройства и серийный номер): Вы можете добавить несколько свойств в свой шаблон устройства, которые отображаются как плитки на вкладке **Свойства**. Оператор может указывать значения свойств при создании нового устройства, а также может редактировать эти значения в любое время. Существует шесть видов свойств, которые вы можете добавить: номер, текст, дата, переключатель, свойство устройства и метка.

Существуют два типа свойств:

- **Свойства устройства**, которые отображаются на устройстве.
- **Свойства приложения**, которые хранятся только в приложении. Устройство не имеет сведений о свойствах приложения.

> [!NOTE]
> Что касается свойств устройства, когда подключено реальное устройство, следует обратить внимание на имя свойства, которое сообщает устройство. Имя должно точно соответствовать **имени поля** свойства. Для свойств приложения имя поля может быть любым, но оно должно быть уникальным в шаблоне устройства.

Например, можно добавить местоположение устройства как новое свойство:

![Форма свойств](./media/howto-set-up-template/propertiesform.png)

После нажатия кнопки **Сохранить** местоположение устройства отображается в виде плитки:

![Плитка свойств](./media/howto-set-up-template/propertiestile.png)

> [!NOTE]
> После создания новой плитки можно изменить значение свойства. Во-первых, отключите режим конструктора в верхней правой части экрана.

## <a name="rules"></a>Правила

Правила позволяют операторам наблюдать за устройствами почти в реальном времени. Правила автоматически вызывают **действия**, такие как отправка сообщения электронной почты, когда правило срабатывает. На сегодня существует один тип правил:

- **Правило телеметрии**. Правило телеметрии срабатывает, когда данные телеметрии выбранного устройства превышают указанное пороговое значение. Дополнительные сведения см. в статье [Создание правила телеметрии и настройка уведомлений в приложении Azure IoT Central](howto-create-telemetry-rules.md).

## <a name="dashboard"></a>панель мониторинга

На панели мониторинга оператор может просмотреть сведения об устройстве. В качестве конструктора вы можете добавить на эту страницу плитки, которые помогают операторам понять, как работает устройство. В шаблон устройства можно добавить несколько плиток панели мониторинга. Существует шесть типов плиток для панели мониторинга, которые можно добавить: изображения, линии, диаграммы, гистограммы, ключевые показатели эффективности, параметры, свойства и метки.

Например, можно добавить плитку **Settings and Properties** (Параметры и свойства), чтобы показать текущие выбранные значения параметров и свойств:

![Форма сведений об устройстве на панели мониторинга](./media/howto-set-up-template/dashboardsettingsandpropertiesform.png)

Теперь, когда оператор просматривает панель управления, он может видеть плитку, на которой отображаются свойства и параметры устройства:

![Плитка на панели мониторинга](./media/howto-set-up-template/dashboardtile.png)

## <a name="next-steps"></a>Дополнительная информация

Вы узнали, как настраивать шаблон устройства в приложении Azure IoT Central, а значит вы готовы к следующему шагу.

> [!div class="nextstepaction"]
> [Создание версии шаблона нового устройства](howto-version-devicetemplate.md)
