---
title: IEnumDebugModules2::Пропустить Документы Майкрософт
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Skip
helpviewer_keywords:
- IEnumDebugModules2::Skip
ms.assetid: 61dc42f4-8544-45bb-8da0-fb22cccec7da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02111475e7757eb91b1d55963e6175208747806f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716466"
---
# <a name="ienumdebugmodules2skip"></a>IEnumDebugModules2::Skip
Пропускает заданное число элементов.

## <a name="syntax"></a>Синтаксис

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>Параметры
`celt`\
[in] Число пропускаемых элементов.

## <a name="return-value"></a>Возвращаемое значение
 В случае успеха возвращает `S_OK`. `S_FALSE` Возвращает, `celt` если больше, чем число оставшихся элементов; в противном случае возвращает код ошибки.

## <a name="remarks"></a>Примечания
 Если `celt` указывается значение, превышающее количество оставшихся элементов, перечисление устанавливается до конца и `S_FALSE` возвращается.

## <a name="see-also"></a>См. также
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
