---
title: Общие сведения о ленте
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, multiple Ribbons
- Ribbon [Office development in Visual Studio], about Ribbon
- toolbars [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], multiple Ribbons
- toolbars [Office development in Visual Studio]
- custom Ribbon, multiple Ribbons
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 668517705caa7ba6baef0b85305bf4470bc3b26b
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985616"
---
# <a name="ribbon-overview"></a>Общие сведения о ленте
  Лента — это способ организации связанных команд, чтобы их было проще найти. Команды отображаются в виде элементов управления на ленте. Элементы управления организованы в *группы* вдоль горизонтальной полосы в верхнем углу окна приложения. Связанные группы расположены на вкладках.

 Доступ к большинству функций, доступ к которым осуществлялся с помощью меню и панелей инструментов в более ранних версиях Microsoft Office системы, теперь можно получить с помощью ленты. Дополнительные сведения см. в обзоре технических статей для [разработчиков пользовательского интерфейса для системы 2007 Microsoft Office](/previous-versions/office/developer/office-2007/aa338198(v=office.12)).

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="customize-the-microsoft-office-ribbon"></a>Настройка ленты Microsoft Office
 Чтобы настроить ленту, добавьте в проект Office один из следующих элементов ленты:

- **Лента (визуальный конструктор)**

- **Лента (XML)**

  Например, для настройки ленты Excel добавьте элемент ленты в проект надстройки VSTO для Excel.

### <a name="ribbon-visual-designer-item"></a>Элемент "Лента (визуальный конструктор)"
 Элемент **Лента (визуальный конструктор)** предоставляет расширенные средства, упрощающие проектирование и разработку настраиваемой ленты. Используйте элемент **Лента (визуальный конструктор)** для настройки ленты следующими способами.

- Добавление пользовательских или встроенных вкладок на ленту.

- Добавление пользовательских групп на встроенную или пользовательскую вкладку на ленте.

  > [!NOTE]
  > Встроенная вкладка или группа уже существует на ленте Microsoft Office приложении. Например, вкладка « **данные** » является встроенной вкладкой Excel. Группа **подключения** — это встроенная группа на вкладке **данные** .

- Добавление пользовательских элементов в пользовательскую группу.

- Добавление пользовательских элементов управления в представление Backstage.

  Дополнительные сведения о настройке ленты с помощью элемента " **Лента (визуальный конструктор)** " см. в разделе [конструктор лент](../vsto/ribbon-designer.md).

### <a name="ribbon-xml-item"></a>Элемент ленты (XML)
 Используйте элемент **Лента (XML)** , если требуется настроить ленту способом, который не поддерживается элементом **Лента (визуальный конструктор)** . Используйте элемент **Лента (XML)** для настройки ленты следующими способами.

- Добавьте *встроенные* группы на пользовательскую вкладку или на встроенную вкладку.

- Добавление встроенных элементов управления в пользовательскую группу.

- Добавление пользовательского кода для переопределения обработчиков событий встроенных элементов управления.

- Настройка панели быстрого доступа.

- Совместное использование настройки ленты между надстройками VSTO с помощью полного идентификатора.

  Дополнительные сведения о настройке ленты с помощью элемента **Лента (XML)** см. в разделе [Ribbon XML](../vsto/ribbon-xml.md).

## <a name="export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>Экспорт ленты из конструктора ленты в XML-ленту
 Если создать ленту с помощью конструктора лент, а затем решить, что необходимо настроить ленту таким образом, чтобы элемент **ленты (визуальный конструктор)** не поддерживался, можно экспортировать ленту в XML.

 Visual Studio автоматически создает элемент **Ribbon (XML)** и заполняет XML-файл ленты элементами и атрибутами для каждого элемента управления на ленте.

 Не все свойства, которые находятся в окне **Свойства** конструктора ленты, передаются в XML-файл ленты.  Например, Visual Studio не экспортирует значение свойства **Image** или **Text** . Это связано с тем, что необходимо создать метод обратного вызова в файле кода ленты экспортированного проекта, чтобы указать изображение или текст элемента управления. Visual Studio не создает методы обратного вызова автоматически в процессе экспорта.

 Кроме того, все неизмененные значения свойств по умолчанию не отображаются в полученном файле XML-ленты.

 Дополнительные сведения о том, как экспортировать ленту в XML, см. в разделе [как экспортировать ленту из конструктора лент в XML-ленту](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md).

### <a name="update-the-code"></a>Обновление кода
 В **Обозреватель решений**добавляется новый файл кода ленты. Он содержит класс XML ленты. Вам необходимо создать методы обратного вызова в области `Ribbon Callbacks` этого класса для обработки действий пользователя, таких как нажатие кнопки. Переместите свой код из обработчиков событий в методы обратного вызова и модифицируйте этот код, чтобы работать с моделью программирования расширения ленты (RibbonX). Дополнительные сведения см. в разделе [Ribbon XML](../vsto/ribbon-xml.md).

 Вы также должны добавить код в класс `ThisAddIn`, `ThisWorkbook` или `ThisDocument`, который переопределяет метод `CreateRibbonExtensibilityObject` и возвращает XML-класс ленты в приложение Office.

 Дополнительные сведения см. в разделе [Ribbon XML](../vsto/ribbon-xml.md).

## <a name="add-multiple-ribbon-items-to-a-project"></a>Добавление нескольких элементов ленты в проект
 В один проект можно добавить несколько лент. Это полезно, если вам необходимо выполнить одно из следующих действий.

- Создание лент для *инспекторов*Outlook. Дополнительные сведения см. [в разделе Настройка ленты для Outlook](../vsto/customizing-a-ribbon-for-outlook.md).

    > [!NOTE]
    > Инспектор — это окно, которое открывается при выполнении пользователем определенных задач, таких как создание электронного сообщения.

- Выберите ленту, отображаемую во время выполнения.

### <a name="select-which-ribbons-to-display-at-run-time"></a>Выбор лент для показа во время выполнения
 Поскольку проект может содержать более одной ленты, можно выбрать, какую ленту следует отображать во время выполнения.

 Чтобы выбрать ленту для отображения во время выполнения, переопределите метод `CreateRibbonExtensibilityObject` в классе `ThisAddin`, `ThisWorkbook`или `ThisDocument` проекта и верните ленту, которую требуется отобразить. В следующем примере проверяется значение поля с именем `myCondition` и возвращается соответствующая лента.

> [!NOTE]
> Синтаксис, используемый в этом примере, возвращает ленту, созданную с помощью элемента **Лента (визуальный конструктор)** . Синтаксис возврата ленты, созданной с помощью элемента **ленты (XML)** , немного отличается. Дополнительные сведения о возврате элемента **ленты (XML)** см. в разделе [Ribbon XML](../vsto/ribbon-xml.md).

 Добавьте следующий код:

 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_Ribbon_choose_Ribbon_4/ThisWorkbook.cs#1)]

### <a name="related-topics"></a>См. также

|Заголовок|Описание|
|-----------|-----------------|
|[Как приступить к настройке ленты](../vsto/how-to-get-started-customizing-the-ribbon.md)|Здесь показано, как настроить ленту Microsoft Office приложения, добавить в проект Office элемент **Лента (визуальный конструктор)** или **Лента (XML)** .|
|[Конструктор ленты](../vsto/ribbon-designer.md)|Описывает, как можно использовать конструктор ленты для добавления пользовательских вкладок, групп и элементов управления на ленту Microsoft Office приложения.|
|[Пошаговое руководство. Создание настраиваемой вкладки с помощью конструктора лент](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Здесь показано, как создать настраиваемую вкладку ленты с помощью конструктора лент. Конструктор лент позволяет добавлять и размещать элементы управления на настраиваемой вкладке.|
|[Общие сведения об объектной модели ленты](../vsto/ribbon-object-model-overview.md)|Общие сведения о строго типизированной объектной модели, которую можно использовать для получения и установки свойств элементов управления ленты во время выполнения.|
|[Пошаговое руководство. Обновление элементов управления на ленте во время выполнения](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|Демонстрируется, как использовать объектную модель ленты для обновления элементов управления на ленте после ее загрузки в приложение Office.|
|[Настройка ленты для Outlook](../vsto/customizing-a-ribbon-for-outlook.md)|Содержит рекомендации по настройке ленты в Microsoft Office Outlook.|
|[Настройка ленты для InfoPath](../vsto/customizing-a-ribbon-for-infopath.md)|Содержит рекомендации по настройке ленты в Microsoft Office InfoPath.|
|[Доступ к ленте во время выполнения](../vsto/accessing-the-ribbon-at-run-time.md)|Показывает, как отображать, скрывать и изменять ленту, а также позволять пользователям запускать код из элементов управления в настраиваемой области задач, панели действий или в области формы Outlook.|
|[Как изменить позицию вкладки на ленте](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|Показывает, как изменить порядок вкладок на ленте.|
|[Как настроить встроенную вкладку](../vsto/how-to-customize-a-built-in-tab.md)|Здесь показано, как добавить группы и элементы управления на встроенную вкладку.|
|[Как добавить элементы управления в представление Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)|Показывает, как добавить элементы управления в меню, которое открывается при щелчке **файла**.|
|[Как добавить средство запуска диалогового окна в группу ленты](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|Показывает, как добавить средство запуска диалогового окна в любую группу на ленте.|
|[Как экспортировать ленту из конструктора лент в XML-ленту](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|Показывает, как настроить ленту в расширенном порядке, экспортировав ленту из конструктора в XML-ленту.|
|[XML-ленты](../vsto/ribbon-xml.md)|Объясняет, как можно настроить ленту с помощью XML-ленты.|
|[Пошаговое руководство. Создание настраиваемой вкладки с помощью конструктора лент](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|Демонстрирует создание настраиваемой вкладки ленты с помощью элемента **Лента (XML)** .|
