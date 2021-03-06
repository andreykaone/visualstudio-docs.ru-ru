---
title: Команды, меню и панели инструментов Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2be2f719d0f123328d5c518c08e30df2185e2a19
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709506"
---
# <a name="commands-menus-and-toolbars"></a>Команды, меню и панели инструментов
Меню и панели инструментов - это способ доступа пользователей к командам в вашем VSPackage. Команды — это функции, которые выполняют задачи, например печать документа, обновление представления или создание нового файла. Меню и панели инструментов — это удобные графические способы представления команд пользователям. Обычно связанные команды группируются в одном меню или на одной панели инструментов.

- Меню обычно отображаются в виде строк из одного слова, сгруппированных в строке в верхней части интегрированной среды разработки (IDE) или окна инструментов. Меню также могут отображаться после щелчка правой кнопкой мыши — в этом случае они называются контекстными меню. После щелчка меню раскрываются и отображают одну или несколько команд. После щелчка команды могут выполняться задачи или открываться подменю с дополнительными командами. Некоторые известные имена меню **файл,** **отсвативайте,** **Просмотр**, и **окно**. Для получения дополнительной [информации см.](../../extensibility/extending-menus-and-commands.md)

- Панели инструментов обычно являются строками кнопок и других элементов управления, таких как поля со списком, списки, текстовые поля и контроллеры меню. Все элементы управления панели инструментов связаны с командами. При нажатии кнопки панели инструментов активируется ее связанная команда. Кнопки панели инструментов обычно содержат значки, которые предлагают базовые команды, например принтер для команды "Печать". В раскрывающемся списке каждый элемент в списке связывается с другой командой. Контроллер меню — это гибрид, в котором одна часть элемента управления — кнопка панели инструментов, а другая — стрелка вниз, которая отображает дополнительные команды при щелчке. Для получения дополнительной информации [см.](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)

- При создании команды необходимо также создать для нее обработчик событий. Обработчик событий определяет, когда команда видна или включена, позволяет изменить ее текст и гарантирует, что команда отвечает соответствующим образом ("маршрутизируется") при активации. В большинстве экземпляров среда IDE обрабатывает команды с помощью интерфейса <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>. Команды в маршруте [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] указаны в виде иерархии, начиная с корневого контекста команды на основе локального выбора и до внешнего контекста на основе глобального выделения. Команды, добавленные в главное меню, становятся сразу доступными для использования в сценариях. Для получения дополнительной информации [см. MenuCommands против OleMenuCommands](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015) и [объектов контекста выбора](../../extensibility/internals/selection-context-objects.md).

  Чтобы определить новые меню и панели инструментов, необходимо описать их в таблице команд Visual Studio *(.vsct)* файл. Шаблон пакета Visual Studio создает этот файл для вас, а также необходимые элементы для поддержки любых команд, панелей инструментов и редакторов, выбранных в шаблоне. Кроме того, вы можете написать свой собственный файл *.vsct,* используя схему XML, описанную здесь: ссылка на [схему VSCT XML.](../../extensibility/vsct-xml-schema-reference.md)

  Для получения дополнительной информации о работе [Visual Studio command table (.vsct) files](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)с *файлами .vsct* см.

  Темы в этом разделе объясняют, как команды, меню и панели инструментов работают в VSPackages.

## <a name="in-this-section"></a>В этом разделе
- [Как VSPackages добавляют элементы пользовательского интерфейса](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 Подробное описание спецификации формата командной таблицы.

- [Таблица команд Visual Studio (.vsct) файлов](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 Описывает синтаксис на основе XML и компилятор для командных таблиц.

- [Размещение команд, групп и панели инструментов по умолчанию](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 Описывает предопределенные команды, группы, меню и панели инструментов.

- [Команды, меню и группы, определяемые IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 Определяем предопределенные меню, команды и командные группы, доступные [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] для использования IDE.

- [Командный дизайн](../../extensibility/internals/command-design.md)

 Объясняет, как проектировать команды.

- [Оптимизация меню и команд панели инструментов](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 Дает рекомендации для команд.

- [Сделать команды доступными](../../extensibility/internals/making-commands-available.md)

 Объясняет, как сделать команды доступными для Visual Studio.

- [Команды и меню, в которые используются межопомнеесборки](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 Объясняет, как реализовать команды, которые используют межопомнеев.

## <a name="related-sections"></a>См. также
- [Командная размытая в VSPackages](../../extensibility/internals/command-routing-in-vspackages.md)

 Объясняет сяраут команд в VSPackages.
