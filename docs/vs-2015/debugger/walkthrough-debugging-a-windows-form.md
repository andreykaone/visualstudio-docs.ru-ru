---
title: 'Пошаговое руководство: Отладка в Windows Forms | Документация Майкрософт'
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
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- debugging managed code, Windows Forms
- debugging [Visual Studio], Windows Forms
- Attach to Process dialog box
- debugger, attaching to programs
- Attach to Process dialog box, walkthroughs
- Windows Forms, debugging
- debugging Windows Forms, walkthroughs
ms.assetid: 529db1e2-d9ea-482a-b6a0-7c543d17f114
caps.latest.revision: 31
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7cf2fd93c76d4be7c032518148acad27b4937f3a
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47570357"
---
# <a name="walkthrough-debugging-a-windows-form"></a>Пример. Отладка в Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [Пошаговое руководство: отладка в Windows Forms](https://docs.microsoft.com/visualstudio/debugger/walkthrough-debugging-a-windows-form).  
  
Форма Windows Forms — один из наиболее распространенных вариантов управляемых приложений. На основе формы Windows Forms создается стандартное приложение Windows. Можно реализовать данный примере на Visual Basic, C# или C++.  
  
 Для начала необходимо закрыть и открыть решения.  
  
### <a name="to-prepare-for-this-walkthrough"></a>Чтобы подготовиться к выполнению данного пошагового руководства  
  
-   Если какое–либо решение уже открыто, закройте его. (На **файл** меню, выберите **закрыть решение**.)  
  
## <a name="create-a-new-windows-form"></a>Создание новой формы Windows Forms.  
 Далее нам предстоит создать новую форму Windows Forms.  
  
#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>Чтобы создать форму Windows Forms для данного примера  
  
1.  На **файл** меню, выберите **New** и нажмите кнопку **проекта**.  
  
     Откроется диалоговое окно **Новый проект** .  
  
2.  В области типов проектов, откройте **Visual Basic**, **Visual C#**, или **Visual C++** узел, затем  
  
    1.  Для Visual Basic или Visual C#, выберите **Windows** узел, затем выберите **приложение Windows Form** в **шаблоны** области.  
  
    2.  Visual C++ выберите **CLR** узел, затем выберите **приложение Windows Form** в **шаблоны** области...  
  
3.  В **шаблоны** области выберите **приложения Windows**.  
  
4.  В **имя** окне укажите уникальное имя (например, Walkthrough_SimpleDebug) проекта.  
  
5.  Нажмите кнопку **ОК**.  
  
     Visual Studio создаст новый проект и откроет новую форму в конструкторе Windows Forms. Дополнительные сведения см. в разделе [конструктор Windows Forms](http://msdn.microsoft.com/en-us/3c3d61f8-f36c-4d41-b9c3-398376fabb15).  
  
6.  На **представление** меню, выберите **элементов**.  
  
     Откроется Панель элементов. См. дополнительные сведения о [панели элементов](../ide/reference/toolbox.md).  
  
7.  В области элементов щелкните **кнопку** управления и перетащите его на поверхность разработки формы. Сбросьте кнопку в форму.  
  
8.  В области элементов щелкните **TextBox** управления и перетащите его на поверхность разработки формы. DROP **TextBox** в форме.  
  
9. На поверхности разработки формы дважды щелкните кнопку.  
  
     Появится страница кода. Курсор должен находиться в тексте `button1_Click`  
  
10. В функции `button1_Click` добавьте следующий код:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
11. В меню **Сборка** выберите команду **Собрать решение**.  
  
     Проект должен быть построен без ошибок.  
  
## <a name="debug-your-form"></a>Отладка формы  
 Теперь все готово для того, чтобы начать отладку.  
  
#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>Чтобы выполнить отладку формы Windows Forms, созданной для данного примера  
  
1.  В окне исходного кода щелкните левое поле на той же строке, в которую добавляется текст:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
     Появится красная точка, и текст строки будет выделен красным цветом. Красная точка представляет точку останова. Дополнительные сведения см. в разделе [точки останова](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583). Если приложение запускается из отладчика, выполнение этого приложения будет приостановлено отладчиком на строке с помеченным кодом. После этого можно просмотреть состояние приложения и произвести его отладку.  
  
    > [!NOTE]
    >  Щелкните правой кнопкой мыши любую строку кода, пункты **точки останова**, а затем нажмите кнопку **вставить точку останова** добавьте точку останова в этой строке.  
  
2.  ON **Отладка** меню, выберите **запустить**.  
  
     Запустится форма Windows Forms.  
  
3.  В форме Windows Forms щелкните добавленную кнопку.  
  
     После этого в Visual Studio приложение остановится на той строке, где была задана точка останова на странице кода. Эта строка будет выделена желтым цветом. Теперь можно просматривать переменные в приложении и управлять его выполнением. В этот момент приложение остановит свое выполнение и будет ожидать действий со стороны пользователя.  
  
4.  На **Отладка** меню, выберите **Windows**, затем **Watch**и нажмите кнопку **Контрольные значения 1**.  
  
5.  В **Контрольные значения 1** окно, щелкните пустую строку. В **имя** столбец, тип `textBox1.Text` (Если вы используете Visual Basic, Visual C# или J#) или `textBox1->Text` (если используется C++), затем нажмите клавишу ВВОД.  
  
     **Контрольные значения 1** окно показывает значение этой переменной в двойных кавычках, как:  
  
    ```  
    ""  
    ```  
  
6.  На **Отладка** меню, выберите **шаг с заходом**.  
  
     Значение textBox1.Text в **Контрольные значения 1**окно, чтобы:  
  
    ```  
    Button was clicked!  
    ```  
  
7.  На **Отладка** меню, выберите **Продолжить** для возобновления отладки программы.  
  
8.  В форме Windows Forms снова нажмите кнопку.  
  
     Visual Studio снова приостановит выполнение программы.  
  
9. Щелкните красную точка, представляющую точка останова.  
  
     Это действие удалит точка останова из кода программы.  
  
10. На **Отладка** меню, выберите **остановить отладку**.  
  
## <a name="attach-to-your-windows-form-application-for-debugging"></a>Присоединение к приложению Windows Form для отладки  
 В [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] можно присоединить отладчик к выполняющемуся процессу. Если используется экспресс-выпуск, эта возможность не поддерживается.  
  
#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>Присоединение к приложению Windows Form для отладки  
  
1.  В созданном ранее проекте щелкните левое поле, чтобы еще раз установить точка останова на добавленной строке:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!"  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
2.  На **Отладка** меню, выберите **Запуск без отладки**.  
  
     Форма Windows Forms запустится из Windows, как и при двойном щелчке исполняемого файла. Отладчик не будет присоединен.  
  
3.  На **Отладка** меню, выберите **присоединение к процессу**. (Эта команда также доступна на **средства** меню.)  
  
     Откроется диалоговое окно **Присоединение к процессу** .  
  
4.  В **доступные процессы** области, найдите имя процесса (Walkthrough_SimpleDebug.exe) в **процесс** столбец и щелкните его.  
  
5.  Нажмите кнопку **Attach** кнопки.  
  
6.  В форме Windows Forms нажмите единственную кнопку.  
  
     Отладчик прервет выполнение формы Windows Forms на точке останова.  
  
## <a name="see-also"></a>См. также  
 [Отладка управляемого кода](../debugger/debugging-managed-code.md)   
 [Безопасность отладчика](../debugger/debugger-security.md)


