---
title: 'CA1301: Избегайте дублирования ускорителей | Документация Майкрософт'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1301
- AvoidDuplicateAccelerators
helpviewer_keywords:
- CA1301
- AvoidDuplicateAccelerators
ms.assetid: 20570a00-864b-459c-a1fa-a6e9db5f1001
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 647fef2968971cddb6a14cc19e53eed979b9c151
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661521"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301: не следует допускать повторяющихся сочетаний клавиш быстрого доступа
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|Категория|Microsoft. Globalization|
|Критическое изменение|Не критическое|

## <a name="cause"></a>Причина
 Тип расширяет <xref:System.Windows.Forms.Control?displayProperty=fullName> и содержит два или более элементов управления верхнего уровня, имеющих одинаковые ключи доступа, которые хранятся в файле ресурсов.

## <a name="rule-description"></a>Описание правила
 Клавиша доступа, также называемая клавишей быстрого доступа, обеспечивает клавиатурный доступ к элементу управления с помощью клавиши ALT. Если несколько элементов управления имеют дублирующиеся клавиши доступа, поведение клавиши доступа определено нечетко. Возможно, пользователь не сможет получить доступ к предполагаемому элементу управления с помощью ключа доступа, а элемент управления, отличный от предполагаемого, может быть включен.

 Текущая реализация этого правила не учитывает пункты меню. Однако пункты меню в одном подменю не должны иметь одинаковые ключи доступа.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение этого правила, Определите уникальные ключи доступа для всех элементов управления.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Для этого правила отключать вывод предупреждений не следует.

## <a name="example"></a>Пример
 В следующем примере показана минимальная форма, содержащая два элемента управления с одинаковыми ключами доступа. Ключи хранятся в файле ресурсов, который не отображается. Однако их значения отображаются в `checkBox.Text` строках с комментариями. Поведение повторяющихся сочетаний клавиш можно проверить, переменив строки `checkBox.Text` на их аналоги с комментариями. Однако в этом случае предупреждение не будет создано в примере.

 [!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.AvoidDuplicateAccels/cs/FxCop.Globalization.AvoidDuplicateAccels.cs#1)]

## <a name="see-also"></a>См. также раздел
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [ресурсов в классических приложениях](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
