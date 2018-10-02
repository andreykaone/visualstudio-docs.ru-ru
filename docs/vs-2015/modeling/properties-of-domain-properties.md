---
title: Свойства доменных свойств | Документация Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, domain properties
ms.assetid: a9471562-d6f2-46bf-9872-e0d66ba03150
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 3c1bd47ce583c790fdc90a4135184b21a932f449
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47561897"
---
# <a name="properties-of-domain-properties"></a>Свойства доменных свойств
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [свойства свойства домена](https://docs.microsoft.com/visualstudio/modeling/properties-of-domain-properties).  
  
Объект *свойства домена* — это функция элемента модели, который может содержать значение. Например, класс домена `Person` может иметь свойства `Name` и `BirthDate`. В определении доменного языка свойства домена перечислены в поле класса домена на схеме и в разделе класса домена в Обозревателе доменного языка. Дополнительные сведения см. в разделе [способ определения доменного языка](../modeling/how-to-define-a-domain-specific-language.md).  
  
> [!NOTE]
>  Слово "свойство" имеет два применения. Объект *свойства домена* — это функция, которая определяется в классе домена. В отличие от этого, многие элементы доменного языка с имеют *свойства*, перечислены в **свойства** окно в определении DSL. Например, каждое свойство домена имеет набор свойств, которые описаны в этом разделе.  
  
 Во время выполнения, когда пользователь создает экземпляры класса домена, значения свойств домена отображаются в окне "Свойства" и в фигурах.  
  
 Большинство свойств домена реализуются как обычные свойства CLR. Однако с точки зрения программирования свойства домена имеют более широкую функциональность, чем обычные программные свойства.  
  
-   Можно определять правила и события, которые отслеживают состояние свойства. Дополнительные сведения см. в разделе [реагирование на события и распространение изменений](../modeling/responding-to-and-propagating-changes.md).  
  
-   Транзакции помогают избежать нестабильных состояний. Дополнительные сведения см. в разделе [перехода и обновления модели в программном коде](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
 При выборе свойства домена в схеме или в Обозревателе доменного языка в окне "Свойства" отображаются указанные ниже элементы. Дополнительные сведения об использовании этих элементов см. в разделе [Настройка и расширение доменного языка](../modeling/customizing-and-extending-a-domain-specific-language.md).  
  
|Свойство.|Описание|Значение по умолчанию|  
|--------------|-----------------|-------------------|  
|**Описание**|Описание, которое используется для документирования пользовательского интерфейса созданного конструктора.|\<None >|  
|**Отображаемое имя**|Имя, которое будет отображаться в созданном конструкторе для этого свойства домена. Оно может включать пробелы и пунктуацию, например "Заголовок песни".|\<None >|  
|**Поставщик имени элемента**|Он применяется только если параметр `Is Element Name` имеет значение `true`. Можно написать код, который предоставляет имя для нового элемента класса домена, переопределяя поведение по умолчанию.<br /><br /> В файле кода проекта доменного языка создайте класс, производный от <xref:Microsoft.VisualStudio.Modeling.ElementNameProvider>.<br /><br /> Затем в Обозревателе доменного языка щелкните корень доменного языка правой кнопкой мыши и выберите пункт "Добавить внешний тип". Введите имя класса.<br /><br /> Снова выберите свойство домена и в раскрывающемся списке выберите имя класса.|\<None >|  
|**Модификатор доступа метода получения**|Уровень доступа класса домена (`public` или `internal`). Управляет областью, в которой код программы может получать доступ к свойству.|`public`|  
|**Ключевое слово справки**|Дополнительное слово, которое используется для индексации справки F1 для этого свойства домена.|\<None >|  
|**Могут просматривать**|Если свойство имеет значение `True`, свойство домена отображается в окне свойств, когда открыты модели данного доменного языка.<br /><br /> Если свойство имеет значение `False`, свойство домена в пользовательском интерфейсе не отображается.<br /><br /> Если вы хотите сделать свойство домена, видна, но только для чтения, задайте **только для чтения**.|`True`|  
|**Представляет имя элемента**|Если свойство имеет значение `True`, это свойство домена отображается под именем его элемента модели в Обозревателе DSL.<br /><br /> Новые элементы модели будут получать для этого свойства значение по умолчанию. Если вы хотите управлять, как создаются эти значения, задайте **поставщик имени элемента**.|`False`|  
|**Доступен пользовательский Интерфейс только для чтения**|Если свойство имеет значение `True`, значение свойства домена нельзя будет изменить с помощью пользовательского интерфейса. При этом его можно будет задать программно, и оно будет отображаться в окне "Свойства".<br /><br /> Если вы хотите скрыть свойство домена от пользователя, задайте **возможность просмотра**. Если вы хотите управлять доступом, программы, задайте **задание модификатора доступа**.|`False`|  
|**Тип**|Тип свойства домена (`Normal`, `Calculated` или `CustomStorage`). Дополнительные сведения см. в разделе [вычисляемые и пользовательские свойства хранилища](../modeling/calculated-and-custom-storage-properties.md).|`Normal`|  
|**Name**|Имя данного свойства домена. Он должен быть допустимым идентификатором, например **SongTitle**.|\<None >|  
|**Примечания**|Неофициальные примечания, связанные с данным свойством домена.|\<None >|  
|**Задание модификатора доступа**|Модификатор доступа для задания. Управляет областью, в которой код программы может задавать свойство.|`public`|  
|**Type**|Тип свойства. Чтобы добавить в список доступных типов, щелкните корень доменного языка в обозревателе DSL правой кнопкой мыши и нажмите кнопку **добавить внешний тип**.|`String`|  
  
## <a name="see-also"></a>См. также  
 [Глоссарий по средствам доменного языка работы](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)


