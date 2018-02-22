---
title: "Рефакторинг для перемещения типа в соответствующий файл в Visual Studio | Документы Майкрософт"
ms.custom: 
ms.date: 01/26/2018
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: ghogen
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 62187c88fa2d2cf7ecf1b358fa0c03416be449a8
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2018
---
# <a name="move-a-type-to-a-matching-file-refactoring"></a>Рефакторинг для перемещения типа в соответствующий файл

Область применения этого рефакторинга:

- C#

- Visual Basic

**Что?** Вы можете переместить выбранный тип в отдельный файл с таким же именем.

**Когда?** При наличии нескольких классов, структур, интерфейсов и пр. в одном файле, который нужно разделить.

**Зачем?** Размещение нескольких типов в одном файле может усложнить поиск этих типов. Перемещение типов в файлы с таким же именем улучшает читаемость кода и упрощает навигацию по нему.

## <a name="how-to"></a>Практические советы

1. Выделите имя типа, который требуется переместить, или поместите в него текстовый курсор.

   - C#:

    ![Выделенный код — C#](media/movetype-highlight-cs.png)

   - Visual Basic:

    ![Выделенный код — Visual Basic](media/movetype-highlight-vb.png)

1. Затем выполните одно из следующих действий:

   - **Клавиатура**
     - Нажмите клавиши **CTRL + .**, чтобы активировать меню **Быстрые действия и рефакторинг**. Затем во всплывающем окне предварительного просмотра выберите пункт **Переместить тип в *имя_типа*.cs**, где *имя_типа* — это имя выбранного вами типа.
   - **Мышь**
     - Щелкните код правой кнопкой мыши и выберите меню **Быстрые действия и рефакторинг**. Затем во всплывающем окне предварительного просмотра выберите пункт **Переместить тип в *имя_типа*.cs**, где *имя_типа* — это имя выбранного вами типа.

   Тип перемещается в новый файл с таким же именем в решении.

   - C#:

    ![Встроенный результат — C#](media/movetype-result-cs.png)

   - Visual Basic:

    ![Встроенный результат — Visual Basic](media/movetype-result-vb.png)

## <a name="see-also"></a>См. также

[Рефакторинг](../refactoring-in-visual-studio.md)