---
title: "\"Параметры\", \"Текстовый редактор\", U-SQL, IntelliSense"
ms.date: 01/17/2019
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.U-SQL.IntelliSense
- VS.ToolsOptionsPages.Text_Editor.HQL.IntelliSense
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ff2c1e69081e6ad54abd6ba17d228aed0f0217a
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2019
ms.locfileid: "55042690"
---
# <a name="options-text-editor-u-sql-intellisense"></a>"Параметры", "Текстовый редактор", U-SQL, IntelliSense

Страница параметров **IntelliSense** позволяет изменять некоторые параметры текстового редактора для U-SQL. Для доступа к странице параметров выберите **Сервис** > **Параметры** и затем **Текстовый редактор** > **U-SQL** > **IntelliSense**.

## <a name="intellisense-settings"></a>Параметры IntelliSense

Установите флажок, чтобы включить параметр **Краткие сведения** или **Intellisense**. Если задан параметр "Краткие сведения", при наведении курсора на переменную отображается ее полное объявление.

## <a name="completion-lists"></a>Списки завершения

- **Показывать список завершения после ввода знака**

   Если этот параметр выбран, IntelliSense автоматически отображает список завершения при начале ввода. Если этот параметр не выбран, функцию завершения IntelliSense можно вызвать из меню IntelliSense или с помощью сочетания клавиш **CTRL** + **ПРОБЕЛ**.

- **Помещать ключевые слова в списки завершения**

   Если этот параметр выбран, IntelliSense добавляет ключевые слова в список завершения.

- **Помещать фрагменты кода в списки завершения**

   Если этот параметр выбран, IntelliSense добавляет фрагменты кода в список завершения.

## <a name="selection-in-completion-list"></a>Выбор в списке завершения

- **Commit by typing the following characters** (Зафиксировать при вводе следующих символов)

   В этом поле отображаются символы, которые приводят к фиксации предложения списка завершения, которое выделено. Вы можете добавлять символы в этот список и удалять их из него.

- **Зафиксировать при нажатии клавиши ПРОБЕЛ**

   Если этот параметр выбран, можно зафиксировать предложение списка завершения, которое выделено, нажав клавишу ПРОБЕЛ.

- **Добавить новую строку по нажатию клавиши ВВОД в конце полностью введенного слова**

   Если этот параметр выбран, автоматически добавляется новая строка, а курсор перемещается на новую строку, когда вы вводите все символы для предложения списка завершения.

## <a name="see-also"></a>См. также

- [Страница "Общие", папка "Среда", диалоговое окно "Параметры"](../../ide/reference/general-environment-options-dialog-box.md)
- [Использование технологии IntelliSense](../../ide/using-intellisense.md)