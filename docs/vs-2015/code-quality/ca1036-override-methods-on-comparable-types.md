---
title: 'CA1036: переопределяйте методы в сравнимых типах | Документация Майкрософт'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 779e6258f9c5be256a7973a5d917045507fc82e6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661831"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036: переопределяйте методы в сравнимых типах
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|Категория|Microsoft. Design|
|Критическое изменение|Не критическое|

## <a name="cause"></a>Причина
 Открытый или защищенный тип реализует интерфейс <xref:System.IComparable?displayProperty=fullName> и не переопределяет <xref:System.Object.Equals%2A?displayProperty=fullName> или не перегружает зависящий от языка оператор на равенство, неравенство, меньше или больше. Правило не сообщает о нарушении, если тип наследует только реализацию интерфейса.

## <a name="rule-description"></a>Описание правила
 Типы, определяющие пользовательский порядок сортировки, реализуют интерфейс <xref:System.IComparable>. Метод <xref:System.IComparable.CompareTo%2A> возвращает целочисленное значение, указывающее правильный порядок сортировки для двух экземпляров типа. Это правило определяет типы, которые задают порядок сортировки. Это означает, что обычные значения равенства, неравенства, меньше и больше не применяются. При предоставлении реализации <xref:System.IComparable> необходимо также переопределить <xref:System.Object.Equals%2A>, чтобы она возвращала значения, которые соответствуют <xref:System.IComparable.CompareTo%2A>. При переопределении <xref:System.Object.Equals%2A> и написании кода на языке, поддерживающем перегрузки операторов, следует также предоставить операторы, которые соответствуют <xref:System.Object.Equals%2A>.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение этого правила, переопределите <xref:System.Object.Equals%2A>. Если ваш язык программирования поддерживает перегрузку операторов, укажите следующие операторы:

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  В C#для представления этих операторов используются следующие токены: = =,! =, \< и >.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Предупреждение о нарушении этого правила можно отключить, если нарушение вызвано отсутствием операторов, а язык программирования не поддерживает перегрузку операторов, как в случае с Visual Basic .NET. Также можно отключить вывод предупреждений для этого правила, когда оно срабатывает для операторов равенства, отличных от op_Equality, если вы определили, что реализация операторов не имеет смысла в контексте приложения. Однако при переопределении Object. Equals всегда следует op_Equality и оператор = =.

## <a name="example"></a>Пример
 В следующем примере содержится тип, который правильно реализует <xref:System.IComparable>. Комментарии к коду определяют методы, которые соответствуют различным правилам, связанным с <xref:System.Object.Equals%2A> и интерфейсом <xref:System.IComparable>.

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>Пример
 Следующее приложение проверяет поведение реализации <xref:System.IComparable>, которая была показана ранее.

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>См. также раздел
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [Операторы равенства](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
