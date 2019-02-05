---
title: "\"Параметры\", \"Текстовый редактор\", \"HTML (веб-формы)\", \"Проверка\""
ms.date: 1/15/2019
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.HTML.Validation
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7f629a0b8d9f149ee10f7a35c75e351a6c3abfd3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2019
ms.locfileid: "55031777"
---
# <a name="options-text-editor-html-web-forms-validation"></a>"Параметры", "Текстовый редактор", "HTML (веб-формы)", "Проверка"

Чтобы настроить проверку синтаксиса HTML-разметки в редакторе для текущего файла, перейдите на страницу параметров **Проверка**. Чтобы открыть эту страницу, выберите в строке меню **Инструменты** > **Параметры** и перейдите к разделу **Текстовый редактор** > **HTML (веб-формы)** > **Проверка**.

## <a name="validation"></a>Проверка

- **Использовать тип документа для определения схемы проверки**

   Схема позволяет определить, какие элементы, атрибуты и регистр текста допустимы в выбранной схеме. Кроме того, вы можете определить теги и атрибуты, доступные в IntelliSense.

   Выберите этот параметр, если в Visual Studio нужно использовать объявление **<!DOCTYPE>** и элемент **html** в содержимом страницы, чтобы определить схему. Например, если вы выбрали этот параметр, а страница содержит объявление `<!DOCTYPE html>`, Visual Studio использует схему HTML5. Но если тег **html** имеет атрибут **xmlns**, такой как `<html xmlns="http://www.w3.org/1999/xhtml">`, в Visual Studio используется схема XHTML5.

- **Target when no doctype found** (Выбрать целевую схему, если тип документа не найден)

   Выберите схему для проверки, если элемент **<!DOCTYPE>** не объявлен на странице.

  - **Показать ошибки**

     Установите этот флажок, чтобы включить проверку. Если флажок снят, редактор не будет выделять ошибки при проверке.

     Остальные флажки позволяют выполнить точную настройку проверки, указав отдельные типы ошибок, которые редактор должен отмечать.

     > [!NOTE]
     > Некоторые схемы не предоставляют параметры для пометки отдельных типов ошибок. Например, при выборе **XHTML 1.1** в качестве схемы целевого объекта все флажки параметров будут сняты. В этом случае выделяются все типы ошибок.

## <a name="see-also"></a>См. также

- [Страница "Общие", папка "Среда", диалоговое окно "Параметры"](../../ide/reference/general-environment-options-dialog-box.md)