---
title: 'CA1809: Избегайте чрезмерного использования локальных переменных | Документация Майкрософт'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d23d9cc6006997c82451ac061e3ee0353e59b1b9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671487"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809: избегайте чрезмерного использования локальных переменных
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidExcessiveLocals|
|CheckId|CA1809|
|Категория|Microsoft. Performance|
|Критическое изменение|Не критическое|

## <a name="cause"></a>Причина
 Элемент содержит более 64 локальных переменных, некоторые из которых могут создаваться компилятором.

## <a name="rule-description"></a>Описание правила
 Распространенная оптимизация производительности заключается в хранении значения в регистре процессора, а не в памяти, которое называется *регистрирует* значением. Среда CLR считает до 64 локальных переменных для енрегистратион. Переменные, которые не енрегистеред, помещаются в стек и должны быть перемещены в регистр перед манипуляцией. Чтобы обеспечить возможность получения енрегистеред всеми локальными переменными, ограничьте число локальных переменных до 64.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение этого правила, выполните рефакторинг реализации, чтобы использовать не более 64 локальных переменных.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Можно отключить вывод предупреждения из этого правила или отключать правило, если производительность не является проблемой.

## <a name="related-rules"></a>Связанные правила
 [CA1804: удалите неиспользуемые локальные переменные](../code-quality/ca1804-remove-unused-locals.md)
