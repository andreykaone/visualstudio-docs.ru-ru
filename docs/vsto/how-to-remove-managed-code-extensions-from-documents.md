---
title: Руководство. Удаление расширений управляемого кода из документов
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0832f0e404331e68fe88dfc990c51ed699eca263
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985798"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>Руководство. Удаление расширений управляемого кода из документов
  Сборку настройки можно программным образом удалить из документа или книги, которая является частью настройки уровня документа для Microsoft Office Word или Microsoft Office Excel. Пользователи могут открывать документы и просматривать содержимое, но любой настраиваемый пользовательский интерфейс (UI), добавляемый в документы, не будет отображаться, и код не будет выполняться.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Сборку настройки можно удалить с помощью одного из `RemoveCustomization` методов, предоставляемых [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Используемый метод зависит от того, требуется ли удалить настройку во время выполнения (т. е. путем запуска кода в настройке во время открытия документа Word или книги Excel) или удалить настройку из закрытого документа или документа, который я на сервере, на котором не установлен Microsoft Office.

## <a name="to-remove-the-customization-assembly-at-run-time"></a>Удаление сборки настройки во время выполнения

1. В коде настройки вызовите метод <xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> (для Word) или метод <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> (для Excel). Этот метод следует вызывать только после того, как настройка больше не нужна.

     Место вызова этого метода в коде зависит от того, как используется настройка. Например, если клиенты используют функции настройки до тех пор, пока они не будут готовы отправить документ другим клиентам, которым требуется только сам документ (а не Настройка), можно предоставить некоторый пользовательский интерфейс, вызывающий `RemoveCustomization`, когда пользователь щелкнет его. Кроме того, если ваша Настройка заполняет документ данными при первом открытии, но настройка не предоставляет другие функции, доступ к которым осуществляется напрямую клиентами, то можно вызвать Ремовекустомизатион сразу же после настройки. Завершает инициализацию документа.

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>Удаление сборки настройки из закрытого документа или документа на сервере

1. В проекте, который не требует Microsoft Office, например консольное приложение или проект Windows Forms, добавьте ссылку на сборку *Microsoft. VisualStudio. Tools. Applications. ServerDocument. dll* .

2. Добавьте следующий оператор **Imports** или **using** в начало файла кода.

     [!code-csharp[Trin_VstcoreDeployment#1](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#1)]
     [!code-vb[Trin_VstcoreDeployment#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#1)]

3. Вызовите статический метод <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> класса <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> и укажите путь к документу решения для параметра.

     В следующем примере кода предполагается, что вы удаляете настройку из документа с именем *WordDocument1. docx* , который находится на рабочем столе.

     [!code-csharp[Trin_VstcoreDeployment#2](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#2)]
     [!code-vb[Trin_VstcoreDeployment#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#2)]

4. Выполните сборку проекта и запустите приложение на компьютере, на котором нужно удалить настройку. На компьютере должна быть установлена среда выполнения средств Visual Studio 2010 для Office.

## <a name="see-also"></a>См. также
- [Управление документами на сервере с помощью класса ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [Как присоединить расширения управляемого кода к документам](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
