---
title: Представление "Указатели инструкций" — данные выборки | Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: c7f647bb-c5a3-4708-9f9d-33c0fd6e2e96
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 42398e044bfc06e41249b15ac9baeebcaebd19f6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "74774260"
---
# <a name="instruction-pointers-ips-view---sampling-data"></a>Представление указателей инструкций — данные выборки
В представлении "Указатели инструкций" данных выборки перечисляются данные о производительности инструкций сборки, непосредственно выполняемых во время сбора выборок в сеансе профилирования.

> [!NOTE]
> Возможности расширенной безопасности в Windows 8 и Windows Server 2012 требовали значительных изменений в способе, которым профилировщик Visual Studio собирает данные на этих платформах. Для приложений универсальной платформы Windows также требуются новые методы сбора. См. статью [Средства производительности в приложениях Windows 8 и Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

|Столбец|Description|
|------------|-----------------|
|**Идентификатор процесса**|Идентификатор процесса (PID) сеанса профилирования.|
|**Имя процесса**|Имя процесса.|
|**Имя модуля**|Имя модуля, содержащего инструкцию.|
|**Путь к модулю**|Путь к модулю, содержащему инструкцию.|
|**Исходный файл**|Исходный файл, содержащий инструкцию.|
|**Имя функции**|Имя функции, содержащей инструкцию.|
|**Номер строки функции**|Номер строки, на которой эта функция начинается в исходном файле.|
|**Адрес функции**|Начальный адрес памяти функции в загруженном двоичном коде.|
|**Начало исходной строки**|Номер начальной строки в исходном файле, с которой начинается сбор выборок.|
|**Конец исходной строки**|Номер строки в исходном файле, которой заканчивается сбор выборок.|
|**Начало исходного символа**|Смещение начального символа в строке исходного файла, с которого начинается сбор выборок.|
|**Конец исходного символа**|Смещение конечного символа в строке исходного файла, которым заканчивается сбор выборок.|
|**Адрес инструкции**|Адрес памяти инструкции в загруженном двоичном коде.|
|**Эксклюзивные выборки**|Общее количество выборок, собранных в процессе выполнения инструкции.|
|**% эксклюзивных выборок**|Процент от всех выборок в сеансе профилирования, собранных во время выполнения инструкции.|

## <a name="see-also"></a>См. также раздел
- [Представление "Указатели инструкций" — выборка](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)
