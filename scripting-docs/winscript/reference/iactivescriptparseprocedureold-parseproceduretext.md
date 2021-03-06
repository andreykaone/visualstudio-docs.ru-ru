---
title: Иактивескриптпарсепроцедуреолд::P Арсепроцедуретекст | Документация Майкрософт
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParseProcedureOld.ParseProcedureText
apilocation:
- jscript.dll
helpviewer_keywords:
- IActiveScriptParseProcedureOld::ParseProcedureText
ms.assetid: 21a21313-35ce-432d-b9a6-7999065f19ac
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 116cbc7fac0d53b55c9766945d56ecebd27b6785
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577447"
---
# <a name="iactivescriptparseprocedureoldparseproceduretext"></a>IActiveScriptParseProcedureOld::ParseProcedureText
Анализирует данную процедуру кода и добавляет анонимную процедуру в пространство имен.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp
HRESULT ParseProcedureText(  
   LPCOLESTR    pstrCode,  
   LPCOLESTR    pstrFormalParams,  
   LPCOLESTR    pstrItemName,  
   IUnknown*    punkContext,  
   LPCOLESTR    pstrDelimiter,  
   DWORD_PTR    dwSourceContextCookie,  
   ULONG        ulStartingLineNumber,  
   DWORD        dwFlags,  
   IDispatch**  ppdisp  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `pstrCode`  
 окне Текст процедуры для вычисления. Интерпретация этой строки зависит от языка сценариев.  
  
 `pstrFormalParams`  
 окне Формальные имена параметров для процедуры. Имена параметров должны быть разделены соответствующими разделителями для обработчика скриптов. Имена не должны заключаться в круглые скобки.  
  
 `pstrItemName`  
 окне Имя именованного элемента, предоставляющего контекст, в котором должна быть вычислена процедура. Если этот параметр имеет значение `NULL`, код вычисляется в глобальном контексте обработчика скриптов.  
  
 `punkContext`  
 окне Контекстный объект. Этот объект зарезервирован для использования в среде отладки, где такой контекст может быть предоставлен отладчиком для представления активного контекста времени выполнения. Если этот параметр имеет значение `NULL`, подсистема использует `pstrItemName` для задания контекста.  
  
 `pstrDelimiter`  
 окне Разделитель в конце процедуры. Когда `pstrCode` анализируется из потока текста, узел обычно использует разделитель, например две одинарные кавычки (' '), для обнаружения конца процедуры. Этот параметр задает разделитель, используемый узлом, позволяя обработчику скриптов предоставить некоторую условную предварительную обработку (например, заменить одинарную кавычку ['] с двумя одинарными кавычками для использования в качестве разделителя). Точно то, как (и если) обработчик скриптов использует эти сведения, зависит от обработчика скриптов. Задайте для этого параметра значение `NULL`, если узел не использовал разделитель для обозначения конца процедуры.  
  
 `dwSourceContextCookie`  
 окне Определяемое приложением значение, используемое в целях отладки.  
  
 `ulStartingLineNumber`  
 окне Отсчитываемое от нуля значение, указывающее, в какой строке начинается синтаксический анализ.  
  
 `dwFlags`  
 окне Флаги, связанные с процедурой. Может быть сочетанием этих значений.  
  
|Константа|значения|Смысл|  
|--------------|-----------|-------------|  
|SCRIPTPROC_ISEXPRESSION|0x00000020|Указывает, что код в `pstrCode` является выражением, представляющим возвращаемое значение процедуры.|  
|SCRIPTPROC_IMPLICIT_THIS|0x00000100|Указывает, что указатель `this` включен в область действия процедуры.|  
|SCRIPTPROC_IMPLICIT_PARENTS|0x00000200|Указывает, что родительские элементы указателя `this` включены в область действия процедуры.|  
  
 `ppdisp`  
 заполняет Возвращает оболочку диспетчеризации, в которой метод по умолчанию является процедурой, проанализированной этим методом.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Метод возвращает `HRESULT`. Допустимые значения включают, но не ограничиваются, значения, приведенные в следующей таблице.  
  
|значения|Описание|  
|-----------|-----------------|  
|`S_OK`|Метод успешно выполнен.|  
|`E_INVALIDARG`|Недопустимый аргумент.|  
|`E_POINTER`|Указан недопустимый указатель.|  
|`E_NOTIMPL`|Этот метод не поддерживается. Обработчик скриптов не поддерживает добавление процедур в пространство имен во время выполнения.|  
|`E_UNEXPECTED`|Вызов не ожидался (например, обработчик скриптов находится в неинициализированном или закрытом состоянии).|  
|`OLESCRIPT_E_SYNTAX`|В процедуре произошла неопределенная синтаксическая ошибка.|  
|`S_FALSE`|Обработчик скриптов не поддерживает объект диспетчеризации; для `ppdisp`parameter задано значение `NULL`.|  
  
## <a name="remarks"></a>Заметки  
 Во время этого вызова не вычисляется код скрипта; Вместо этого процедура компилируется в метод в `ppdisp`, где он может быть вызван сценарием позже.  
  
 Этот интерфейс не рекомендуется использовать в качестве предпочтительного интерфейса `IActiveScriptParseProcedure`. Метод `IActiveScriptParseProcedure::ParseProcedureText` аналогичен этому методу, но позволяет указать имя процедуры. Во всех обстоятельствах следует использовать `IActiveScriptParseProcedure::ParseProcedureText`.  
  
## <a name="see-also"></a>См. также  
 @No__t_1 [интерфейса иактивескриптпарсепроцедуреолд](../../winscript/reference/iactivescriptparseprocedureold-interface.md)  
 [IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)