---
title: Найти и заменить в файлах
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.findreplace.replaceinfiles
- vs.replaceinfiles
helpviewer_keywords:
- text searches, replacing text
- find and replace
- replace in files
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dddd55714e53516ba1ccd8a11c99761a4db7136a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585630"
---
# <a name="replace-in-files"></a>Замена в файлах

Функция **Заменить в файлах** позволяет осуществлять поиск строки или выражения в заданном наборе файлов и заменять все или некоторые из найденных совпадений. Найденные совпадения и предпринятые действия перечисляются в окне **Результаты поиска**, выбранном в разделе **Параметры результатов**.

> [!NOTE]
> Отображаемые диалоговые окна и команды меню могут отличаться от описанных в **справке** в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, например на **Общие** или **Visual C++** , выберите **Сервис** > **Импорт и экспорт параметров**, а затем щелкните **Сбросить все параметры**.

Для отображения функции **Заменить в файлах** в окне **Поиск и замена** можно использовать любой из следующих методов.

## <a name="to-display-replace-in-files"></a>Отображение окна "Заменить в файлах"

1. В меню **Правка** разверните узел **Поиск и замена**.

2. Выберите **Заменить в файлах**.

   — или —

   Если окно **Поиск и замена** уже открыто, на панели инструментов выберите **Заменить в файлах**.

## <a name="find-what"></a>Найти

Чтобы найти новую текстовую строку или выражение, введите их в поле. Для поиска любой из 20 строк, которые вы искали недавно, откройте раскрывающийся список и выберите нужную строку. Нажмите расположенную рядом кнопку **Построитель выражений**, чтобы использовать в строке поиска одно или несколько регулярных выражений. Дополнительные сведения см. в статье [Использование регулярных выражений в Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

> [!NOTE]
> Кнопка **Построитель выражений** будет включена, только если вы выбрали **Использовать регулярные выражения** в области **Параметры поиска**.

## <a name="replace-with"></a>Заменить на

Чтобы заменить экземпляры строки в поле **Образец** другой строкой, введите заменяющую строку в поле **Заменить на**. Чтобы удалить экземпляры строки в поле **Образец**, оставьте это поле пустым. Откройте список для отображения последних 20 строк, поиск которых выполнялся недавно. Нажмите расположенную рядом кнопку **Построитель выражений**, чтобы использовать в заменяющей строке одно или несколько регулярных выражений. Дополнительные сведения см. в статье [Использование регулярных выражений в Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

## <a name="look-in"></a>Искать в

Параметр, выбранный в раскрывающемся списке **Искать в** , определяет, будет ли функция **Замена в файлах** осуществлять поиск только в файлах, активных в текущий момент, или во всех файлах, хранимых в определенных папках. Выберите область поиска в списке или нажмите кнопку **Обзор (...)** , чтобы открыть диалоговое окно **Выбор папок поиска** и выбрать набор папок, в которых будет выполняться поиск. Можно также ввести путь непосредственно в поле **Область поиска**.

> [!NOTE]
> Если после выбора варианта **Область поиска** начинается поиск в файле, извлеченном из системы управления исходным кодом, поиск производится только в версии файла, скачанной на локальный компьютер.

## <a name="find-options"></a>Параметры поиска

Вы можете развернуть или свернуть раздел **Параметры поиска**. Можно установить или снять следующие флажки.

**Учитывать регистр**

Если этот флажок установлен, в окне **Результаты поиска** будут отображаться только те экземпляры строки **Образец**, которые соответствуют заданному содержанию и регистру. Например, поиск строки MyObject **с учетом регистра** будет возвращать MyObject, но не myobject или MYOBJECT.

**Слово целиком**

Если этот флажок установлен, в окне **Результаты поиска** будут отображаться только те экземпляры строки **Образец**, которые точно соответствуют введенным словам. Например, поиск строки MyObject будет возвращать MyObject, но не CMyObject или MyObjectC.

**Использование регулярных выражений**

Если этот флажок установлен, вы можете использовать специальные обозначения, чтобы определить шаблоны текста в текстовых полях **Образец** или **Заменить на**. Список этих обозначений см. в статье [Использование регулярных выражений в Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

**Искать в файлах указанных типов**

Этот список указывает типы файлов для поиска в каталогах **Область поиска**. Если оставить это поле пустым, поиск будет выполняться во всех файлах в каталогах **Область поиска**. Выберите любой элемент в списке, чтобы ввести заранее заданную строку для поиска указанных типов файлов.

## <a name="result-options"></a>Параметры результатов

Вы можете развернуть или свернуть раздел **Параметры результатов**. Можно установить или снять следующие флажки.

Окно **Результаты поиска 1**

Если выбран этот параметр, результаты текущего поиска заменяют содержимое окна **Результаты поиска 1**. Это окно открывается автоматически и отображает результаты поиска. Чтобы открыть окно вручную, выберите **Другие окна** в меню **Вид** и выберите **Результаты поиска 1**.

Окно **Результаты поиска 2**

Если выбран этот параметр, результаты текущего поиска заменяют содержимое окна **Результаты поиска 2**. Это окно открывается автоматически и отображает результаты поиска. Чтобы открыть окно вручную, выберите **Другие окна** в меню **Вид** и выберите **Результаты поиска 2**.

**Отображать только имена файлов**

Если этот флажок установлен, то в окнах **Результаты поиска** выводится список полных имен и путей для всех файлов, содержащих строку поиска. Но результаты не включают строку кода, в которой содержится заданная строка. Этот флажок доступен только для функции **Найти в файлах**.

**Оставить измененные файлы открытыми после выполнения команды «Заменить все»**

Если этот флажок установлен, все файлы, в которых были произведены замены, останутся открытыми, так что изменения можно будет сохранить или отменить. Объем доступной памяти может ограничить число файлов, которые останутся открытыми после операции замены.

> [!CAUTION]
> Команда **Откат** может использоваться только для файлов, которые остались открытыми для редактирования. Если этот параметр не установлен, файлы, которые не были до этого открыты для редактирования, останутся закрытыми, а команда **Откат** не будет для них доступна.

## <a name="see-also"></a>См. также раздел

- [Поиск и замена текста](../ide/finding-and-replacing-text.md)
- [Поиск в файлах](../ide/find-in-files.md)
- [Команды Visual Studio](../ide/reference/visual-studio-commands.md)
