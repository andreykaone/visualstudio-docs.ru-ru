---
title: Свойства соединителей | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
ms.assetid: b1f24e8d-cdd7-4a5d-af37-1038f43b45c7
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1ea629e504c3ba74d35f3ad8aa89bc22cfae30df
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652042"
---
# <a name="properties-of-connectors"></a>Свойства соединителей
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Соединители представляют доменные отношения в созданном конструкторе.

 Дополнительные сведения см. [в разделе Определение доменного языка](../modeling/how-to-define-a-domain-specific-language.md). Дополнительные сведения об использовании этих свойств см. [в разделе Настройка и расширение предметно-](../modeling/customizing-and-extending-a-domain-specific-language.md)ориентированного языка.

 У соединителей есть свойства, перечисленные в следующей таблице.

|свойство;|Описание|Значение по умолчанию|
|--------------|-----------------|-------------|
|Цвет|Цвет этого соединителя.|Черный|
|Тип штриха|Стиль штриха для линии этого соединителя ("Сплошная", "тире", "точка", "Дашдот", "Дашдотдот" или "Настраиваемая").|Сплошная|
|Конечный стиль источника|Конечный стиль источника для этого соединителя (HollowArrow, EmptyArrow, FilledArrow, EmptyDiamond, FilledDiamond или None).|Отсутствуют|
|Конечный конечный стиль|Целевой конечный стиль для этого соединителя (HollowArrow, EmptyArrow, FilledArrow, EmptyDiamond, FilledDiamond или None).|Отсутствуют|
|Цвет текста|Цвет, используемый для декораторов текста, связанных с этим соединителем.|Черный|
|Thickness|Толщина линии для этого соединителя, измеряемая в дюймах.|0,03125|
|Модификатор доступа|Уровень доступа класса (`public` или `internal`).|Public|
|Настраиваемые атрибуты|Используется для добавления атрибутов в класс исходного кода, созданного из этого соединителя.|\<none>|
|Создает двойное производное|Если `True`, будет сформирован как базовый класс, так и разделяемый класс (для поддержки настройки с помощью переопределений). Дополнительные сведения см. [в разделе Переопределение и расширение созданных классов](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Имеет настраиваемый конструктор|Если `True`, в исходном коде будет предоставлен пользовательский конструктор. Дополнительные сведения см. [в разделе Переопределение и расширение созданных классов](../modeling/overriding-and-extending-the-generated-classes.md).|False|
|Модификатор наследования|Описывает тип наследования класса исходного кода, созданного из соединителя (`none`, `abstract` или `sealed`).|Нет|
|Базовый соединитель|Базовый класс этого соединителя.|(нет)|
|Название|Имя этого соединителя.|Текущее имя|
|Пространство имен|Пространство имен, связанное с этим соединителем.|Текущее пространство имен|
|Тип подсказки|Как определена подсказка (фиксированная, переменная или нет). Если параметр является фиксированным, то в качестве подсказки используется значение свойства `Fixed Tooltip Text`. Если переменная, то подсказка определяется в пользовательском коде.|\<none>|
|Примечания|Неформальные примечания, связанные с этим соединителем.|\<none>|
|Стиль маршрутизации|Стиль, используемый для маршрутизации соединителя. Соединитель `Rectilinear` разворачивается по правому краю по мере необходимости; соединитель `Straight` не поддерживает.|Rectilinear|
|Представленный цвет как свойство<br /><br /> Предоставленный стиль штриха как свойство<br /><br /> Доступная толщина как свойство<br /><br /> Отображение цвета текста|Если `True`, пользователь может задать указанное свойство фигуры. Чтобы установить это, щелкните правой кнопкой мыши определение фигуры и выберите пункт **добавить предоставленный**.|False|
|Описание|Используется для документирования созданного конструктора.|\<none>|
|Отображаемое имя|Имя, которое будет отображаться в созданном конструкторе для этого соединителя.|\<none>|
|Исправлен текст подсказки|Текст, используемый для фиксированной подсказки.|\<none>|
|Ключевое слово Help|Ключевое слово, используемое для индексации справки F1 для этого элемента.|\<none>|

## <a name="see-also"></a>См. также раздел
 [Глоссарий средств предметно-ориентированных языков](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
