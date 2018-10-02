---
title: 'Практическое: вызвать отладчик рабочего процесса | Документация Майкрософт'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 34c592af-f4f6-4d02-99f6-63a94698e48b
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 6142e12da9a32ccb325c6a8a199f67599c7228c8
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47558483"
---
# <a name="how-to-invoke-the-workflow-debugger"></a>Как вызвать отладчик рабочего процесса
Как правило, отладка рабочих процессов похожа на отладку программ, написанных на других языках программирования Visual Studio. Запуск отладчика рабочих процессов:  
  
-   Выберите **присоединение к процессу** на **Отладка** меню, чтобы выбрать выполняющийся рабочий процесс для экземпляра рабочего процесса. Эта процедура совпадает с процедурой прикрепления к хост-процессу в управляемом коде.  
  
-   Нажмите клавишу **F5** Чтобы запустить выполнение экземпляра рабочего процесса или продолжить выполнение после попадания точки останова.  
  
-   Используйте удаленную отладку. Сведения об использовании удаленной отладки, см. в разделе [как: Включение удаленной отладки](http://go.microsoft.com/fwlink/?LinkId=196257).  
  
    > [!NOTE]
    >  Если приложение рабочего процесса предназначено x86 архитектуры и размещается на компьютере под управлением 64-разрядной операционной системы, удаленная отладка не будет работать без [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] установлен на удаленном компьютере или цель приложения рабочего процесса изменена на **Любой ЦП**.  
  
### <a name="stepping-through-code"></a>Пошаговая отладка  
  
-   **Шаг с заходом**: можно выполнить пошаговую отладку действия с помощью **F11**. Отладчик выполняет пошаговую отладку всех заданных обработчиков. Если обработчики не заданы, то действие пропускается, а в случае составного действия, которое содержит другие действия, выполняется вход в первое выполняющееся действие.  
  
-   **Шаг с выходом:** вы можете шаг с выходом из действия, использующего **Shift-F11**. Выход из пошаговой отладки действия запускает текущее действие и все родственные действия на выполнение до завершения. Далее отладчик прерывается на текущем родительском объекте действия. При выходе из пошаговой отладки из кода обработчика, отладчик прерывается на действии, с которым связан обработчик.  
  
-   **Шаг с обходом**: можно пропустить действия, использующего **F10**. При обходе составного действия отладчик прерывается на первом исполняемом дочернем объекте составного действия. При обходе несоставного действия, например, действия <xref:System.Activities.Statements.Assign>, отладчик выполняет действие и связанные с ним обработчики и прерывается на следующем действии. Если выполняемое действие является последним дочерним действием в составном действии, то после выполнения отладчик прерывается на родительском действии.  
  
### <a name="debugging-with-f5"></a>Отладка по клавише F5  
  
-   Если вы создаете проект консольного приложения рабочего процесса, просто нажмите **F5** чтобы начать отладку приложения и рабочего процесса. При создании отдельной библиотеки действий необходимо в качестве начального проекта подготовить исполняемое хост-приложение. Чтобы установить запускаемый проект **обозревателе решений**, щелкните правой кнопкой мыши имя проекта узла и выберите **Назначить запускаемым проектом**.  
  
## <a name="see-also"></a>См. также  
 [Практическое: задайте точки останова в рабочих процессах](../workflow-designer/how-to-set-breakpoints-in-workflows.md)   
 [Отладка рабочих процессов с помощью конструктора рабочих процессов](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)