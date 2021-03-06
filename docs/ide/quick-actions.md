---
title: Быстрые действия, лампочки и отвертки
ms.date: 03/28/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2ce8ce85e027a7ed7f78d0da1f68f328c1ca103d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596961"
---
# <a name="quick-actions"></a>Быстрые действия

Быстрые действия позволяют легко создавать и изменять код, а также выполнять его рефакторинг одним действием. Быстрые действия доступны для C#, [C++](/cpp/ide/writing-and-refactoring-code-cpp) и файлов кода Visual Basic. Некоторые действия доступны только для определенного языка, тогда как другие доступны для всех языков.

Быстрые действия можно использовать для решения следующих задач:

- исправление кода при нарушениях правил [анализатора кода](../code-quality/roslyn-analyzers-overview.md);

::: moniker range=">=vs-2019"

- [игнорирование](../code-quality/use-roslyn-analyzers.md#suppress-violations) нарушений правил анализа кода или [настройка](../code-quality/use-roslyn-analyzers.md#automatically-configure-rule-severity) их уровня серьезности;

::: moniker-end

::: moniker range="vs-2017"

- [игнорирование](../code-quality/use-roslyn-analyzers.md#suppress-violations) нарушений правил анализа кода;

::: moniker-end

- применение рефакторинга (например, [встраивание временной переменной](../ide/reference/inline-temporary-variable.md));

- создание кода (например, [представление локальной переменной](../ide/reference/introduce-local-variable.md)).

> [!NOTE]
> Этот раздел относится к Visual Studio в Windows. Информацию о Visual Studio для Mac см. в статье [Рефакторинг кода (Visual Studio для Mac)](/visualstudio/mac/refactoring).

Быстрые действия можно применять, используя значок лампочки ![значок лампочки](media/light-bulb-icon.png), значок отвертки ![значок отвертки](media/screwdriver-icon.png) или сочетание клавиш **CTRL**+ **.** когда курсор находится на строке кода, для которой доступно действие. Лампочка, сигнализирующая об ошибке, ![значок лампочки ошибки](media/error-light-bulb-icon.png) отображается, если есть красная волнистая линия, указывающая на ошибку, и у Visual Studio есть решение этой ошибки.

Сторонние разработчики могут предоставить для любого языка пользовательскую диагностику и предложения, например в рамках пакета SDK, и лампочки Visual Studio будут отображаться на основе этих правил.

## <a name="icons"></a>Значки

Значок, отображающийся при доступном быстром действии, указывает на тип доступного исправления или рефакторинга. Значок *отвертки* ![значок отвертки](media/screwdriver-icon.png) указывает, что доступны действия по изменению кода, но вам не обязательно их использовать. Значок *желтой лампочки* ![значок лампочки](media/light-bulb-icon.png) указывает, что доступны действия, которые *следует* сделать для улучшения кода. Значок *лампочки с ошибкой* ![значок лампочки с ошибкой](media/error-light-bulb-icon.png) указывает, что доступны действия для исправления ошибки в коде.

## <a name="to-see-a-light-bulb-or-screwdriver"></a>Отображение лампочки и отвертки

Если доступно исправление, отображаются лампочки:

- При наведении курсора мыши на расположение ошибки.

   ![Лампочка с наведением указателя мыши](../ide/media/vs2015_lightbulb_hover.png)

- В левом поле редактора при перемещении курсора в соответствующую строку кода.

Вы также можете нажать клавиши **Ctrl**+ **.** в любом месте строки, чтобы увидеть список доступных быстрых действий и рефакторингов.

Чтобы просмотреть возможные исправления, щелкните стрелку вниз рядом с лампочкой или ссылку **Показать возможные исправления**. Отобразится список доступных быстрых действий.

![Расширенная лампочка](../ide/media/vs2015_lightbulb_hover_expanded.png)

## <a name="see-also"></a>См. также раздел

- [Создание кода в Visual Studio](../ide/code-generation-in-visual-studio.md)
- [Распространенные быстрые действия](../ide/common-quick-actions.md)
- [Стили кода и быстрые действия](../ide/code-styles-and-code-cleanup.md)
- [Написание и рефакторинг кода (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [Рефакторинг (Visual Studio для Mac)](/visualstudio/mac/refactoring)
