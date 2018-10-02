---
title: IntelliSense для Visual C# | Документы Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IntelliSense [J#]
- Visual C#, IntelliSense
- IntelliSense [C#]
ms.assetid: 79ca304d-dc1e-4dc9-a2a6-7808df2e588e
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c967bde43358c856ab4cbd16e36391cb02760391
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47557981"
---
# <a name="visual-c-intellisense"></a>IntelliSense для Visual C#
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [IntelliSense для Visual C#](https://docs.microsoft.com/visualstudio/ide/visual-csharp-intellisense).  
  
Возможности IntelliSense для Visual C# доступны при написании кода в редакторе и при отладке кода в окне команд [режима интерпретации](../ide/reference/immediate-window.md).  
  
## <a name="completion-lists"></a>Списки завершения  
 Списки завершения IntelliSense в Visual C# содержат токены из операций составления списков членов, завершения слов и других. Они обеспечивают быстрый доступ к следующим элементам:  
  
-   Члены типа или пространства имен,  
  
-   Переменные, команды и имена функций,  
  
-   [Фрагменты кода](#CodeSnippets),  
  
-   [Ключевые слова языка](#Keywords),  
  
-   [Методы расширения](#ExtensionMethods)  
  
 Список завершения в C# обладает достаточно широкими возможностями по фильтрации несоответствующих токенов и предварительному выбору токена в зависимости от контекста. Дополнительные сведения см. в разделах [Фильтрованные списки завершения в C#](../misc/filtered-completion-lists-in-csharp.md) и [Заранее выбранные элементы списков завершения в C#](../misc/pre-selected-completion-list-items-in-csharp.md).  
  
###  <a name="CodeSnippets"></a> Фрагменты кода в списках завершения  
 В Visual C# списки завершения содержат фрагменты кода, позволяющие легко вставлять предварительно определенные тела кода в программу. Фрагменты кода появляются в списке завершения в виде [элемента Shortcut (фрагменты кода Intellisense)](http://msdn.microsoft.com/en-us/052cc97a-5c70-42f8-b398-4c3adf670cfa) фрагмента.  Дополнительные сведения о фрагментах кода, доступных в Visual C# по умолчанию, см. в разделе [Фрагменты кода Visual C#](../ide/visual-csharp-code-snippets.md).  
  
###  <a name="Keywords"></a> Ключевые слова языка в списках завершения  
 Список завершения в Visual C# также содержит ключевые слова языка. Дополнительные сведения о ключевых словах языка C# см. в разделе [Ключевые слова C#](http://msdn.microsoft.com/library/e929b0f2-4b92-4d37-8060-23d323b098ad).  
  
###  <a name="ExtensionMethods"></a> Методы расширения в списках завершения  
 Список завершения в Visual C# содержит методы расширения, которые находятся в области действия.  
  
> [!NOTE]
>  В списке завершения отображаются не все методы расширения для объектов <xref:System.String>.  
  
 В методах расширения используется не такой значок, как в методах экземпляра. Значки списка перечислены в разделе [Значки представления классов и обозревателя объектов](../ide/class-view-and-object-browser-icons.md). Если метод экземпляра и метод расширения с одинаковыми именами находятся в одной области, в списке завершения отображается значок метода расширения.  
  
### <a name="filtered-completion-lists"></a>Фильтрованные списки завершения  
 IntelliSense удаляет ненужные элементы из списка завершения с помощью фильтров.  
  
 Visual C# фильтрует списки завершения по следующим элементам:  
  
-   **Интерфейсы и базовые классы** IntelliSense автоматически удаляет элементы из списков завершения интерфейсов и базовых классов, как в базе объявлений класса, так и в списках интерфейса и ограничений. Например, перечисления не отображаются в списке завершения для базовых классов, поскольку перечисления не могут использоваться для базовых классов. Список завершения для базовых классов содержит только интерфейсы и пространства имен. Если выбрать элемент в списке и ввести запятую, IntelliSense удалит базовые классы из списка завершения, поскольку Visual C# не поддерживает множественное наследование. Аналогичная логика используется и для предложений ограничения.  
  
-   **Атрибуты**. При применении атрибута к типу список завершения фильтруется таким образом, что в нем остаются только типы, которые получены из пространств имен, содержащих эти типы, например <xref:System.Attribute>.  
  
-   Операторы `as` и `is`.  
  
-   **Предложения CATCH.**  
  
-   **Инициализаторы объектов**. В списке завершения будут отображаться только те элементы, которые могут быть инициализированы.  
  
-   **Ключевое слово new**. При вводе `new` и нажатии клавиши ПРОБЕЛ появляется список завершения. Элемент в списке выбирается автоматически в зависимости от контекста в коде. Например, в списке завершения автоматически выбираются элементы для объявлений и операторов возврата в методах.  
  
-   **Операторы AS и IS**. Фильтрованный список завершения отображается автоматически при нажатии клавиши ПРОБЕЛ после ввода ключевого слова `as` или `is`.  
  
-   События. При вводе ключевого слова `event` список завершения содержит только типы делегата.  
  
-   Справочная система по параметрам автоматически производит сортировку по первой соответствующей параметрам перегрузке метода по мере их ввода. Если существует несколько перегрузок метода, можно использовать кнопки со стрелками вверх и вниз для перехода к следующей возможной перегрузке в списке.  
  
## <a name="most-recently-used-members"></a>Недавно использовавшиеся члены  
 IntelliSense запоминает последние элементы, выбранные во всплывающем окне [Список членов](../ide/using-intellisense.md) для автоматического завершения имени объекта. Когда вы откроете список членов в следующий раз, элементы, которые недавно использовались, будут показаны сверху. Журнал наиболее часто используемых членов списка очищается после завершения каждого сеанса в интегрированной среде разработки.  
  
## <a name="override"></a>override  
 Если ввести [override](http://msdn.microsoft.com/library/dd1907a8-acf8-46d3-80b9-c2ca4febada8), а затем нажать клавишу ПРОБЕЛ, IntelliSense покажет во всплывающем списке все допустимые элементы базового класса, которые можно переопределить. Если после `override` ввести тип возвращаемого значения метода, IntelliSense будет отображать только методы, возвращающие этот тип. Если IntelliSense не удается найти совпадения, будут показаны все члены базового класса.  
  
## <a name="automatic-code-generation"></a>Автоматическое генерирование кода  
  
### <a name="add-using"></a>Добавить директиву using  
 Операция IntelliSense «Добавить директиву using» позволяет сосредоточить внимание на коде, который вы пишете, и не отвлекаться на другую часть кода.  
  
 Чтобы инициировать операцию «Добавить директиву using», поместите курсор на ссылку на тип, которую не удается разрешить. Например, при создании консольного приложения и добавлении `XmlTextReader` в тело метода `Main` под крайним правым символом `XmlTextReader` появится смарт-тег, так как это ссылка на тип, которую не удается разрешить.  
  
 ![Добавить использование изображения смарт-тега](../ide/media/addusesmart.gif "AddUseSmart")  
  
 Затем можно вызвать операцию "Добавить директиву using", выбрав соответствующую команду в подменю **Разрешить** в меню **IntelliSense**, в контекстном меню либо воспользовавшись смарт-тегом. Смарт-тег отображается, только если курсор помещен на несвязанный тип или рядом с ним.  
  
 ![Добавить использование расширенного изображения смарт-тега](../ide/media/addusesmartexp.gif "AddUseSmartExp")  
  
### <a name="organize-usings"></a>Управление директивами using  
 Параметры **Управление директивами using** позволяют сортировать и удалять объявления `using` и `extern`, не меняя поведение исходного кода. Со временем исходные файлы могут стать перегруженными, и их станет трудно читать по причине ненужных и неорганизованных директив `using`. Параметры **Управление директивами using** сжимают исходный код, удаляя неиспользуемые директивы `using` и улучшая читаемость путем их сортировки.  
  
 Чтобы просмотреть доступные параметры в интегрированной среде разработки Visual Studio, в меню **Правка** выберите **IntelliSense**, а затем **Управление директивами using**. Интегрированная среда разработки предоставляет следующие параметры для организации и удаления директив `usings`:  
  
### <a name="implement-interface"></a>Реализовать интерфейс  
 Технология IntelliSense может облегчить реализацию [интерфейса](http://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba) при работе в редакторе кода. Обычно для правильной реализации интерфейса нужно создать объявление метода для каждого члена интерфейса в классе. При использовании IntelliSense после ввода имени интерфейса в объявлении класса отображается смарт-тег. Смарт-тег позволяет выбрать вариант автоматической реализации интерфейса с помощью явного или неявного именования. В случае явного именования объявления метода содержат имя интерфейса. В случае неявного именования в объявлениях метода нет указания на интерфейс, к которому они принадлежат. Доступ к явно именованному методу интерфейса может осуществляться только через экземпляр интерфейса, а не через экземпляр класса. Дополнительные сведения см. в разделе [Явная реализация интерфейса](http://msdn.microsoft.com/library/181c901f-0d4c-4f29-97fc-895079617bf2).  
  
 Функция реализации интерфейса создаст минимальное количество заглушек методов, необходимых для работы интерфейса. Если базовый класс реализует части интерфейса, эти заглушки не восстанавливаются.  
  
### <a name="implement-abstract-base-class"></a>Реализация абстрактного базового класса  
 IntelliSense предоставляет возможность автоматической реализации членов абстрактного базового класса при работе в редакторе кода. В обычном режиме для реализации членов абстрактного базового класса для каждого метода абстрактного базового класса в производном классе необходимо создать новое определение метода. При использовании IntelliSense после ввода имени абстрактного базового класса в объявлении класса появляется смарт-тег. Смарт-тег дает возможность автоматической реализации методов базового класса.  
  
 Заглушки метода, создаваемые функцией «Реализовать абстрактный базовый класс», моделируются фрагментом кода, определенным в файле MethodStub.snippet. Фрагменты кода можно изменять. Подробнее см. в разделе [Пошаговое руководство. Создание фрагмента кода](../ide/walkthrough-creating-a-code-snippet.md).  
  
### <a name="generate-from-usage"></a>Создание в результате использования  
 Возможность **Создание в результате использования** позволяет использовать классы и элементы до того, как они будут определены. Для любого класса, конструктора, метода, свойства, поля или перечисления, которое вы хотите использовать, но еще не определили, можно создать заглушку. Новые типы и члены можно создавать, не покидая текущего расположения в коде. Это сводит до минимума нарушения в рабочем процессе.  
  
 Каждый неопределенный идентификатор подчеркивается волнистой чертой. При перемещении указателя мыши на такой идентификатор в подсказке появляется сообщение об ошибке.  
  
 Для отображения нужных параметров можно выполнить одну из следующих процедур:  
  
-   Щелкните неопределенный идентификатор. Под крайним слева символом появится короткое подчеркивание. Наведите указатель мыши на это подчеркивание, чтобы появился смарт-тег (значок). Щелкните смарт-тег.  
  
-   Щелкните неопределенный идентификатор и нажмите сочетание клавиш CTRL+. (точка).  
  
-   Щелкните неопределенный идентификатор правой кнопкой мыши и выберите команду **Сформировать**.  
  
 В число появившихся параметров могут входить следующие:  
  
-   **Сформировать заглушку свойства**  
  
-   **Сформировать заглушку поля**  
  
-   **Сформировать заглушку метода**  
  
-   **Сформировать класс**  
  
-   **Сформировать новый тип** (для класса, структуры, интерфейса или перечисления)  
  
## <a name="generate-event-handlers"></a>Сформировать обработчики событий  
 В редакторе кода IntelliSense упрощает подключение методов (обработчиков событий) к полям событий.  
  
 Если ввести оператор `+=` после поля события в файле CS, IntelliSense предложит нажать клавишу TAB. В результате будет вставлен новый экземпляр делегата, который указывает на метод, обрабатывающий событие.  
  
 ![Автопривязка кнопки](../ide/media/vxautohookup.gif "vxAutoHookUp")  
  
 При нажатии клавиши TAB IntelliSense автоматически завершает оператор и отображает ссылку на обработчик событий в виде выделенного текста в редакторе кода. Для завершения автоматического подключения события IntelliSense предлагает снова нажать клавишу TAB или создать пустую заглушку для обработчика событий.  
  
 ![Генерация обработчика событий](../ide/media/vxgenerateeventhandler.gif "vxGenerateEventHandler")  
  
> [!NOTE]
>  Если новый делегат, созданный IntelliSense, ссылается на существующий обработчик событий, IntelliSense выводит эти сведения во всплывающей подсказке. Эту ссылку можно изменить — соответствующий текст уже выделен в редакторе кода. В противном случае автоматическое подключение события завершается на этом этапе.  
  
 При нажатии клавиши TAB IntelliSense заглушает метод с корректной сигнатурой и размещает указатель в теле обработчика событий.  
  
> [!NOTE]
>  Для возврата к оператору подключения события используйте команду **Назад** в меню **Вид** (CTRL+-).  
  
 В следующей задаче показано, как IntelliSense автоматически подключает обработчик событий с именем `button1_Click` к полю события с именем `button1.Click`.  
  
## <a name="see-also"></a>См. также  
 [Интегрированная среда разработки Visual Studio](../ide/visual-studio-ide.md)


