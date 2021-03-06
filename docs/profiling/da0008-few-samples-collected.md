---
title: DA0008. Собрано мало выборок | Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DATooFewSamples
- vs.performance.8
- vs.performance.DA0008
- vs.performance.rules.DA0008
ms.assetid: 8a5b78aa-7b3d-476c-a47d-abfaff3fae7c
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 15f8eeb370a3f1e61981e0e936704d33f6b44bbd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779445"
---
# <a name="da0008-few-samples-collected"></a>DA0008. Собрано несколько образцов

|||
|-|-|
|Идентификатор правила|DA0008|
|Категория|Использование средств профилирования|
|Способ профилирования|Выборка|
|Сообщение|Собрано небольшое число выборок. Для получения значительных результатов рекомендуется использовать более высокую частоту выборки или более долгий запуск.|
|Тип правила|Сведения|

## <a name="cause"></a>Причина
 В сеансе профилирования было собрано небольшое число выборок.

## <a name="rule-description"></a>Описание правила
 При использовании метода выборки следует собрать статистически значимое число выборок, чтобы данные отражали фактическое поведение программы. Чтобы свести к минимуму ошибки выборки, нужно собрать по крайней мере 1000 выборок данных по выполнению инструкции программы. Недостаточное количество выборок может привести к неправильным выводам при анализе данных профилирования.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Для получения статистически значимых результатов рекомендуется дольше выполнять процедуру профилирования приложения или увеличить частоту выборки. Дополнительные сведения об изменении частоты выборки в интегрированной среде разработки Visual Studio см. в разделе [Практическое руководство. Выбор событий выборки](../profiling/how-to-choose-sampling-events.md). Дополнительные сведения об изменении частоты выборки при использовании командной строки средств профилирования см. в разделе [Таймер](../profiling/timer.md) руководства [VSPerfCmd](../profiling/vsperfcmd.md).
