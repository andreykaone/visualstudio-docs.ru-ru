---
title: IDebugEngine2::RemoveSetException Документы Майкрософт
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveSetException
helpviewer_keywords:
- IDebugEngine2::RemoveSetException
ms.assetid: bdd25097-0e9d-4218-b417-0497ea48d2e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e811ce2e387c299ff3655799bf35185c1d2029b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730924"
---
# <a name="idebugengine2removesetexception"></a>IDebugEngine2::RemoveSetException
Удаляет указанное исключение, чтобы оно больше не обрабатывалось движком отладки.

## <a name="syntax"></a>Синтаксис

```cpp
HRESULT RemoveSetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int RemoveSetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>Параметры
`pException`\
(в) [Структура EXCEPTION_INFO,](../../../extensibility/debugger/reference/exception-info.md) описывающая исключение, которое должно быть удалено.

## <a name="return-value"></a>Возвращаемое значение
 Возвращает значение `S_OK`, если выполнение прошло успешно; в противном случае возвращает код ошибки.

## <a name="remarks"></a>Примечания
 Удаление исключения должно быть ранее установлено более ранним вызовом методу [SetException.](../../../extensibility/debugger/reference/idebugengine2-setexception.md)

 Чтобы удалить все замыктые исключения сразу, позвоните в метод [RemoveAllSetExceptions.](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)

## <a name="see-also"></a>См. также
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
