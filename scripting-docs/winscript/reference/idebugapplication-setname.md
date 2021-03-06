---
title: 'IDebugApplication:: SetName | Документация Майкрософт'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.SetName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::SetName
ms.assetid: 7b0ddc58-6f20-4ce3-9bdf-81a6c1d64256
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6a3e5115d4adc3fc3dfa93f10c90cb0d2b36f0e4
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571103"
---
# <a name="idebugapplicationsetname"></a>IDebugApplication::SetName
Задает имя приложения.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp
HRESULT SetName(  
   LPCOLESTR  pstrName  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `pstrName`  
 окне Имя приложения.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Метод возвращает `HRESULT`. Допустимые значения включают, но не ограничиваются, значения, приведенные в следующей таблице.  
  
|значения|Описание|  
|-----------|-----------------|  
|`S_OK`|Метод успешно выполнен.|  
  
## <a name="remarks"></a>Заметки  
 Имя, предоставленное этому методу, возвращается при последующих вызовах метода `IRemoteDebugApplication::GetName`.  
  
 Этот метод следует вызывать перед вызовом метода `IProcessDebugManager::AddApplication`.  
  
## <a name="see-also"></a>См. также  
 @No__t_1 [интерфейса IDebugApplication](../../winscript/reference/idebugapplication-interface.md)  
 [IProcessDebugManager::AddApplication](../../winscript/reference/iprocessdebugmanager-addapplication.md)