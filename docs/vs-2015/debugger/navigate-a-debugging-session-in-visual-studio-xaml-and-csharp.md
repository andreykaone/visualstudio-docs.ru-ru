---
title: Навигация по сеансу отладки в Visual Studio (Xaml и C#) | Документация Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 1da33203-333f-4a05-b4e2-8d407c497233
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8c9aed98b7f2649aa5c62e930e1833b80d58b7ba
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47568935"
---
# <a name="navigate-a-debugging-session-in-visual-studio-xaml-and-c"></a>Навигация по сеансу отладки в Visual Studio (XAML и C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [Навигация по сеансу отладки в Visual Studio (Xaml и C#)](https://docs.microsoft.com/visualstudio/debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp).  
  
В этом кратком руководстве описана процедура навигации по сеансам отладки, а также способы просмотра и изменения состояния программы в сеансе.  
  
 Это краткое руководство предназначено для разработчиков, которые не знакомы с методами отладки с помощью Visual Studio, и для разработчиков, которые хотят узнать больше о навигации по сеансу отладки Visual Studio. Оно не предназначено для обучения самому искусству отладки. Методы, содержащиеся в образце кода, предназначены исключительно для того, чтобы продемонстрировать процедуры отладки, описанные в данном разделе. При создании этих методов не применяются рекомендации по проектированию приложения или функций. На самом деле вы быстро поймете, что и методы, и само приложение практически ничего не делают.  
  
 Разделы данного краткого руководства были запланированы как абсолютно независимые, поэтому вы можете пропустить любой раздел, содержащий уже знакомую вам информацию. Также не требуется создавать пример приложения; однако это рекомендуется сделать, и мы постарались максимально упростить процесс.  
  
 **Сочетания клавиш отладчика.** Навигация по отладчику Visual Studio оптимизирована для работы и с мышью, и с клавиатурой. Для многих действий, описанных в этом разделе, в скобках указаны клавиши или сочетания клавиш для быстрого доступа. Например, примечание (клавиша F5) указывает, что нажатие клавиши F5 приводит к запуску или продолжению выполнения кода отладчиком.  
  
## <a name="in-this-topic"></a>Содержание раздела  
 Вы научитесь:  
  
-   [Создание примера приложения](#BKMK_CreateTheApplication)  
  
-   [Задайте точку останова, выполните код до этой точки, выполните шаг с заходом в метод и проверьте данные программы.](#BKMK_StepInto)  
  
-   [Шаг с заходом, с обходом и c выходом из метода](#BKMK_StepIntoOverOut)  
  
-   [Задайте условную точку останова, выполните до текущей позиции и визуализируйте переменную.](#BKMK_ConditionCursorVisualize)  
  
-   [Измените и продолжите, исправьте исключение.](#BKMK_EditContinueRecoverExceptions)  
  
##  <a name="BKMK_CreateTheApplication"></a> Создание примера приложения  
 Отладка связана с кодом, поэтому в примере приложения платформа для приложений для Магазина Windows используется исключительно в целях создания исходного файла, в котором можно увидеть, каким образом выполняется навигация по сеансу отладки и как можно проанализировать и изменить состояние программы. Весь код вызывается из конструктора главной страницы; элементы управления не добавляются, и события не обрабатываются.  
  
 **Создайте стандартное приложение C# для Магазина Windows.** Запустите Visual Studio. На домашней странице выберите ссылку **Новый проект** . В диалоговом окне «Новый проект» выберите **Visual C#** в списке **Установленные** , а затем выберите **Магазин Windows**. В списке шаблонов проектов выберите **Приложение**. Visual Studio создает новое решение и проект и отображает конструктор MainPage.xaml и редактор кода XAML.  
  
 **Откройте исходный файл MainPage.xaml.cs.** Щелкните правой кнопкой мыши в любом месте редактора XML и выберите пункт **Просмотреть код**. Отображается файл кода программной части MainPage.xaml.cs. Обратите внимание, что в файле указан только один метод (конструктор `MainPage()` ).  
  
 **Замените конструктор MainPage образцом кода.** Удалите метод MainPage(). Перейдите по этой ссылке: [Навигация отладчика в примере кода (Xaml и C#)](../debugger/debugger-navigation-sample-code-xaml-and-csharp.md), а затем скопируйте код, приведенный в разделе C# в буфер обмена. (Выберите **обратно** в браузере или окне справки, чтобы вернуться на эту страницу быстрого запуска.) В редакторе Visual Studio вставьте код в блок `partial class MainPage`. Нажмите сочетание клавиш CTRL + s, чтобы сохранить файл.  
  
 После этого можно выполнить примеры, приведенные в этом разделе.  
  
##  <a name="BKMK_StepInto"></a> Задайте точку останова, выполните код до этой точки, выполните шаг с заходом в метод и проверьте данные программы.  
 Наиболее распространенным способом начала сеанса отладки является выбор функции **Начать отладку** в меню **Отладки** (клавиша F5). Начинается выполнение, которое продолжается до достижения точки останова, приостановления выполнения вручную, возникновения исключения или завершения приложения.  
  
 При приостановке выполнения в отладчике можно просмотреть значение активной переменной в подсказке, которая отображается при наведении указателя мыши на переменную. Можно также открыть окна «Локальные» и «Видимые» для просмотра списка активных переменных и их текущих значений. Добавление одной или нескольких переменных в окно контрольных значений позволяет сосредоточиться на значениях переменных в ходе выполнения приложения.  
  
 После приостановки выполнения приложения (что также называется остановом отладчика) можно контролировать способ выполнения остальной части программного кода. Можно продолжить выполнение построчно, перемещаться из вызова метода в сам метод или выполнить вызываемый метод за один шаг. Эти процедуры называются пошаговым выполнением приложения. Также можно возобновить стандартное выполнение приложения до следующей заданной точки останова или до строки, в которой размещен курсор. Сеанс отладки можно остановить в любой момент. Отладчик выполняет необходимые операции очистки и завершает выполнение.  
  
### <a name="example-1"></a>Пример 1  
 В этом примере вы задаете точку останова в конструкторе MainPage файла MainPage.xaml.cs, выполняете шаг с заходом в первый метод, просматриваете значения переменных, а затем останавливаете отладку.  
  
 **Задайте точку останова.** Задайте точку останова в операторе `methodTrack = "Main Page";` в конструкторе MainPage. Выберите строку на затененном переплете редактора исходного кода (клавиатура: поместите курсор на строку и нажмите клавишу F9).  
  
 ![Шаг с заходом](../debugger/media/dbg-basics-stepinto.png "DBG_Basics_StepInto")  
  
 На переплете отобразится значок точки останова.  
  
 **Выполните код до точки останова.** Запустите сеанс отладки, выбрав **Начать отладку** on the **Отладка** (F5).  
  
 Начинается выполнение приложения. Выполнение приостанавливается непосредственно перед оператором, для которого задана точка останова. Значок текущей строки на переплете определяет расположение, а текущий оператор выделяется.  
  
 ![Установите точку останова](../debugger/media/dbg-basics-setbreakpoint.png "DBG_Basics_SetBreakpoint")  
  
 Теперь вы можете контролировать выполнение приложения и проверять состояние программы при пошаговом выполнении операторов.  
  
 **Выполните шаг с заходом метода.** On the **Отладки** выберите команду **Шаг с заходом** (клавиша F11).  
  
 ![Текущая строка](../debugger/media/dbg-basics-currentline.png "DBG_Basics_CurrentLine")  
  
 Обратите внимание, что отладчик переходит на следующую строку, которая представляет собой вызов метода Example1. Снова выберите шаг с заходом. Отладчик перемещается на точку входа метода Example1. Это означает, что метод был загружен в стеке вызовов и была выделена память для локальных переменных.  
  
 При заходе в строку кода отладчик выполняет одно из следующих действий.  
  
-   Если следующий оператор не является вызовом функции в вашем решении, отладчик выполняет оператор, переходит к следующему оператору, а затем приостанавливает выполнение.  
  
-   Если следующий оператор является вызовом функции в вашем решении, отладчик переходит к точке входа вызываемой функции, а затем приостанавливает выполнение.  
  
 Продолжайте пошаговую отладку операторов Example1 до достижения точки выхода. Отладчик выделяет закрывающую фигурную скобку метода.  
  
 **Просмотр значений переменных в подсказках по данным.** При наведении указателя мыши на имя переменной в подсказке отображается имя, значение и тип переменной.  
  
 ![Подсказок по данным отладчика](../debugger/media/dbg-basics-datatip.png "DBG_Basics_DataTip")  
  
 Наведите указатель мыши на переменную `a`. Обратите внимание на имя, значение и тип данных. Наведите указатель мыши на переменную `methodTrack`. И снова обратите внимание на имя, значение и тип данных.  
  
 **Проверьте значения переменных в окне «Локальные».** В диалоговом окне **Отладка** выберите пункт **Окна**и затем щелкните **Локальные**. (Клавиатура: Alt + 4).  
  
 ![Окно "Локальные"](../debugger/media/dbg-basics-localswindow.png "DBG_Basics_LocalsWindow")  
  
 Окно «Локальные» — это древовидное представление параметров и переменных функции. Свойства переменной объекта являются дочерними узлами самого объекта. Переменная `this` является скрытым параметром в каждом методе объекта, который представляет сам объект. В этом случае он представляет класс MainPage. Поскольку `methodTrack` является членом класса MainPage, его значение и тип данных указаны в строке под `this`. Разверните узел `this` , чтобы просмотреть сведения `methodTrack` .  
  
 **Добавьте контрольное значение для переменной methodTrack.** Переменная `methodWatch` используется на протяжении быстрого запуска для отображения методов, вызываемых в примерах. Чтобы упростить просмотр значения переменной, добавьте его в окно контрольных значений. Щелкните правой кнопкой мыши имя переменной в окне «Локальные», а затем выберите **Добавить контрольное значение**.  
  
 ![Окно контрольных значений](../debugger/media/dbg-basics-watchwindow.png "DBG_Basics_WatchWindow")  
  
 В окне контрольных значений можно отслеживать несколько переменных. Значения контролируемых переменных, например значения локальных переменных и значения в окнах подсказок, обновляются при каждой приостановке выполнения. Можно также добавить переменные в окно контрольного значения из редактора кода. Выберите переменную для контроля, щелкните правой кнопкой мыши и выберите **Добавить контрольное значение**.  
  
##  <a name="BKMK_StepIntoOverOut"></a> Шаг с заходом, с обходом и c выходом из метода  
 В отличие от шага с заходом в метод, вызываемый родительским методом, шаг с обходом метода выполняет дочерний метод, а затем приостанавливает выполнение в вызывающем методе при возобновлении родительского метода. Метод можно обойти, если вам известно, как работает этот метод, и вы уверены, что его выполнение не повлияет на анализируемую проблему.  
  
 Шаг с обходом строки кода, которая не включает вызов метода, выполняет строку таким же образом, как и шаг с заходом в строку.  
  
 Шаг с выходом из дочернего метода продолжает выполнение метода и затем приостанавливает выполнение после возврата метода в вызывающий метод. Вы можете выполнить шаг с выходом из функции long, если определено, что остальная часть функции не имеет значения.  
  
 И шаг с обходом, и шаг с выходом из функции приводит к выполнению функции.  
  
 ![Шаг с заходом, с обходом и c выходом из метода](../debugger/media/dbg-basics-stepintooverout.png "DBG_Basics_StepIntoOverOut")  
  
### <a name="example-2"></a>Пример 2  
 В этом примере вы выполните шаг с заходом, с обходом и c выходом из методов.  
  
 **Вызовите метод Example2 в конструкторе MainPage.** Измените конструктор MainPage и замените строку, следующую за `methodTrack = String.Empty;` , строкой `Example2();`.  
  
 ![Вызов метода Example2 из метода Demo](../debugger/media/dbg-basics-callexample2.png "DBG_Basics_CallExample2")  
  
 **Выполните код до точки останова.** Запустите сеанс отладки, выбрав **Начать отладку** on the **Отладка** (F5). Отладчик приостанавливает выполнение в точке останова.  
  
 **Выполните шаг с обходом строки кода.** В диалоговом окне **Отладка** выберите команду **Шаг с обходом** (клавиша F10). Отладчик выполняет оператор `methodTrack = "MainPage";` таким же образом, как шаг с заходом в оператор.  
  
 **Выполните шаг с заходом в Example2 и Example2_A.** Нажмите клавишу F11, чтобы выполнить шаг с заходом в метод Example 2. Продолжайте выполнение шага с заходом в операторы Example2, пока не достигнете строки `int x = Example2_A();`. Снова выполните шаг с заходом в эту строку, чтобы переместить точку входа Example2_A. Продолжайте выполнение шага с заходов в каждый оператор Example2_A, пока не вернетесь к Example2.  
  
 ![Example2](../debugger/media/dbg-basics-example2.png "DBG_Basics_Example2")  
  
 **Выполните шаг с обходом функции.** Обратите внимание, что следующая строка в Example2 ( `int y = Example2_A();` ), по сути, совпадает с предыдущей строкой. Можно спокойно пропустить эту строку. Нажмите клавишу F10 для перемещения из точки возобновления Example2 второго вызова в Example2_A. Выберите F10, чтобы обойти этот метод. Обратите внимание: в строке `methodTrack` указано, что метод Example2_A был выполнен дважды. Вы также заметите, что отладчик немедленно перейдет к следующей строке. Выполнение в точке возобновления Example2 не приостанавливается.  
  
 **Выполните шаг с выходом из функции.** Нажмите клавишу F11, чтобы выполнить шаг с заходом в метод Example2_B. Обратите внимание, что Example2_B не слишком отличается от Example2_A. Чтобы выполнить шаг с выходом из метода, выберите **Шаг с выходом** в меню **Отладка** (клавиши Shift + F11). Обратите внимание, что переменная `methodTrack` указывает, что Example2_B был выполнен и отладчик вернулся в точку возобновления Example2.  
  
 **Остановите отладку.** Выберите «Остановить отладку» в меню «Отладка» (клавиатура: Shift + F5). Это приведет к завершению сеанса отладки.  
  
##  <a name="BKMK_ConditionCursorVisualize"></a> Задайте условную точку останова, выполните до текущей позиции и визуализируйте переменную.  
 Условные точки останова задают условие, которое приводит к приостановке выполнения отладчиком. Условие задается любым выражением кода, которое может обрабатываться как true или false. Например, можно использовать условную точку останова для проверки состояния программы в часто вызываемом методе только тогда, когда переменная достигает определенного значения.  
  
 Выполнение до текущей позиции аналогично заданию однократной точки останова. При приостановке выполнения можно выбрать строку в исходном коде и возобновить выполнение до достижения выбранной строки. Например, можно пошагово выполнить цикл в методе и определить, что данный код в цикле выполняется правильно. Вместо того чтобы применять пошаговое выполнение каждой итерации цикла, можно запустить выполнение до текущей позиции курсора, заданной после выполнения цикла.  
  
 Иногда трудно просмотреть значение переменной в строке подсказки или окна переменной. Отладчик может отображать строки, HTML и Xml в средстве визуализации текста, в котором отображается отформатированное представление значения в окне с возможностью прокрутки.  
  
### <a name="example-3"></a>Пример 3  
 В этом примере вы задаете условную точку останова для прерывания выполнения на определенной итерации цикла с последующим выполнением до текущей позиции курсора, заданной после цикла. Можно также просмотреть значение переменной в средстве визуализации текста.  
  
 **Вызовите метод Example3 в конструкторе MainPage.** Измените конструктор MainPage и замените строку, следующую за `methodTrack = String.Empty;` , строкой `Example3();`.  
  
 ![Вызов метода Example3 из метода Demo](../debugger/media/dbg-basics-callexample3.png "DBG_Basics_CallExample3")  
  
 **Выполните код до точки останова.** Запустите сеанс отладки, выбрав **Начать отладку** on the **Отладка** (F5). Отладчик приостанавливает выполнение в точке останова в методе MainPage.  
  
 **Выполните шаг с заходом в метод Example3.** Выберите **Шаг с заходом** в меню **Отладки** (клавиша F11) для перемещения в точку входа метода Example3. Продолжайте пошаговое выполнение с заходом в метод, пока не будет выполнена итерация одного или двух циклов блока `for` . Обратите внимание, что пошаговое выполнение всех 1000 итераций заняло бы много времени.  
  
 **Задайте условную точку останова.** В левом поле окна кода щелкните правой кнопкой мыши строку `x += i;` и выберите **Условие**. Установите флажок **Условие** , а затем введите `i == 500;` в текстовом поле. Выберите параметр **Верно** и выберите **ОК**. Точка останова позволяет проверить значение в 500-й итерации цикла `for` .  
  
 ![Диалоговое окно Условие точки останова](../debugger/media/dbg-basics-breakpointcondition.png "DBG_Basics_BreakpointCondition")  
  
 Для определения значка условной точки останова используется белое перекрестие.  
  
 ![Условную точку останова](../debugger/media/dbg-basics-conditionalbreakpoint.png "DBG_Basics_ConditionalBreakpoint")  
  
 **Выполните код до точки останова.** В меню «Отладка» выберите команду «Продолжить» (клавиша F5). В окне «Локальные» убедитесь, что для `i` задано значение 500. Обратите внимание, что переменная `s` представлена в виде одной строки и гораздо длиннее окна.  
  
 **Визуализируйте строковую переменную.** Щелкните значок лупы в столбце **Значение** строки `s`.  
  
 Появится окно средства визуализации текста, и значение строки будет представлено в виде многострочного текста.  
  
 **Выполните код до позиции курсора.** Щелкните правой кнопкой мыши строку `methodTrack += "->Example3";` и выберите **Выполнить до курсора** (клавиатура: переместите курсор на строку; CTRL + F10). Отладчик завершает итерации цикла и затем приостанавливает выполнение в строке.  
  
 **Остановите отладку.** Выберите «Остановить отладку» в меню «Отладка» (клавиатура: Shift + F5). Это приведет к завершению сеанса отладки.  
  
##  <a name="BKMK_EditContinueRecoverExceptions"></a> Измените и продолжите, исправьте исключение.  
 В некоторых случаях при приостановке выполнения кода в отладчике Visual Studio существует возможность изменения значений переменных и даже логики операторов. Эта функция называется изменением и продолжением.  
  
 Функция изменения и продолжения может быть особенно полезной при остановке на позиции исключения. Вместо остановки и перезапуска отладки длинной и связанной процедуры, чтобы избежать вызова исключения, можно «очистить» исключение, чтобы переместить выполнение в точку непосредственно перед моментом, где возникло исключение, а затем изменить неправильную переменную или оператор и продолжить текущий сеанс отладки в состоянии без создания исключения.  
  
 Хотя функцию изменения и продолжения можно использовать в разнообразных ситуациях, сложно указать определенные условия, которые не поддерживают данную функцию, поскольку условия зависят от языка программирования, текущего состояния стека программы и возможности отладчика изменять состояние без прерывания процесса. Чтобы определить, поддерживается ли изменение редактирования, лучше всего просто попробовать воспользоваться этой функцией; отладчик незамедлительно уведомит вас в том случае, если изменение не поддерживается.  
  
### <a name="example-4"></a>Пример 4  
 В этом примере вы выполните отладчик до исключения, перемотаете исключение, исправите логику метода и затем измените значение переменной, чтобы можно было продолжить выполнение метода.  
  
 **Вызовите метод Example4 в конструкторе MainPage.** Измените конструктор MainPage() и замените строку, следующую за `methodTrack = String.Empty;` , строкой `Example4();`.  
  
 ![Вызов метода Example4 из метода Demo](../debugger/media/dbg-basics-callexample4.png "DBG_Basics_CallExample4")  
  
 **Выполните код до исключения.** Запустите сеанс отладки, выбрав **Начать отладку** on the **Отладка** (F5). Нажмите клавишу F5, чтобы возобновить выполнение. Отладчик приостанавливает выполнение в точке исключения в методе Example4 и выводит диалоговое окно исключения.  
  
 ![Диалоговое окно исключения](../debugger/media/dbg-basics-exceptiondlg.png "DBG_Basics_ExceptionDlg")  
  
 **Измените логику программы.** Очевидно, что ошибка находится в условии `if` : значение `x` должно быть изменено при `x` , равном 0, а не при `x` , не равном нулю. Выберите **Прервать** , чтобы исправить логику метода. При попытке изменения строки отображается другое диалоговое окно.  
  
 ![Изменить и продолжить-диалоговое окно](../debugger/media/dbg-basics-editandcontinuedlg.png "DBG_Basics_EditAndContinueDlg")  
  
 Выберите **Изменить** , а затем замените строку `if (x != 0)` на `if (x == 0)`. Отладчик сохраняет изменения логики программы в исходный файл.  
  
 **Измените значение переменной.** Проверьте значение `x` в подсказке или в окне локальных переменных. Оно по-прежнему равно 0 (нулю). При попытке выполнить инструкцию, которая вызвала исходное исключение, исключение возникнет снова. Значение `x`можно изменить. В окне «Локальные» дважды щелкните столбец **Значение** строки **x** . Измените значение с 0 на 1.  
  
 ![Изменение значения в окне "Локальные"](../debugger/media/dbg-basics-editandcontinuefix.png "DBG_Basics_EditAndContinueFix")  
  
 Нажмите клавишу F11, чтобы выполнить шаг с заходом в оператор, который ранее вызвал исключение. Обратите внимание, что строка выполняется без ошибок. Снова нажмите F11.  
  
 **Остановите отладку.** On the **Отладки** выберите команду **Отладка** (клавиатура: Shift + F5). Это приведет к завершению сеанса отладки.  
  
## <a name="see-also"></a>См. также  
 [Запуск сеанса отладки (VB, C#, C++ и XAML)](../debugger/start-a-debugging-session-for-a-store-app-in-visual-studio-vb-csharp-cpp-and-xaml.md)   
 [Активировать приостановки, возобновления и фоновых событий для Windows Store)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)   
 [Отладка приложений в Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)


