---
title: Совместное использование классов с помощью библиотеки DSL | Документация Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 509bd96b-3e66-47f4-8642-771421d0d0d5
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 093cc277fa1cbe1915099fd9663fc1ccb797ca3a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671183"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>Совместное использование классов в различных доменных языках с помощью библиотеки доменных языков
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

В пакете SDK для визуализации и моделирования [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] можно создать неполное определение DSL, которое можно импортировать в другой домен DSL. Это позволяет разделить общие части похожих моделей.

## <a name="creating-and-using-dsl-libraries"></a>Создание и использование библиотек DSL

#### <a name="to-create-a-dsl-library"></a>Создание библиотеки DSL

1. Создайте новый проект DSL и выберите шаблон решения библиотеки DSL.

     Будет создан один проект DSL с пустой моделью.

2. Можно добавить классы предметной области, связи, фигуры и т. д.

     Элементы в библиотеке не обязательно должны образовывать одно дерево внедрения.

     Чтобы определить связь, которую могут использовать средства импорта, создайте два доменных класса и создайте связь между ними.

     Рассмотрите возможность установки **модификатора наследования** доменных классов для `Abstract`.

3. Можно добавить элементы, определенные в обозревателе DSL, такие как построители подключений.

4. Можно добавить настройки, требующие дополнительного кода, например ограничения проверки.

5. Щелкните **преобразовать все шаблоны**.

6. Выполните построение проекта.

7. При распространении DSL для использования другими пользователями необходимо предоставить скомпилированную сборку (DLL) и файл `DslDefinition.dsl`. Скомпилированную сборку можно найти в папке в разделе `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>Импорт библиотеки DSL

1. В другом определении DSL в **обозревателе DSL**щелкните правой кнопкой мыши корневой класс DSL и выберите команду **Добавить новый импорт DslLibrary**.

2. В окно свойств задайте **путь к файлу** библиотеки. Можно использовать либо относительный, либо абсолютный путь.

    Импортированная библиотека появится в обозревателе DSL в режиме только для чтения.

3. Импортированные классы можно использовать в качестве базовых классов. Создайте доменный класс в импортируемом DSL-приложении, а в окно свойств задайте в качестве **базового класса** импортированный класс.

4. Щелкните преобразовать все шаблоны.

5. Добавьте в проект DSL ссылку на сборку (DLL), созданную проектом библиотеки DSL.

6. Постройте решение.

   Библиотека DSL может импортировать другие библиотеки. При импорте библиотеки ее импорты также автоматически отображаются в обозревателе DSL.

## <a name="see-also"></a>См. также раздел
 [Определение доменного языка](../modeling/how-to-define-a-domain-specific-language.md)
