---
title: IDebugComPlusSymbolProvider::IsFunctionDeleted Документы Майкрософт
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::IsFunctionDeleted
ms.assetid: b276bd25-6658-4898-bc36-04ecdf92aa2f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7dd8b5b86b6b8c89d11326b817f2718a3ee4ad3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733702"
---
# <a name="idebugcomplussymbolproviderisfunctiondeleted"></a>IDebugComPlusSymbolProvider::IsFunctionDeleted
Определяет, что функция по указанному адресу отладки удалена.

## <a name="syntax"></a>Синтаксис

```cpp
HRESULT IsFunctionDeleted(
    IDebugAddress* pAddress
);
```

```csharp
int IsFunctionDeleted(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>Параметры
`pAddress`\
(в) Адрес отладки, представленный интерфейсом [IDebugAddress.](../../../extensibility/debugger/reference/idebugaddress.md) Этот адрес должен быть METHOD_ADDRESS.

## <a name="return-value"></a>Возвращаемое значение
Если функция удалена, `S_OK`возвращается . Если функция существует, `S_FALSE`возвращается .

## <a name="example"></a>Пример
В следующем примере показано, как реализовать этот метод для объекта **CDebugSymbolProvider,** который предоставляет интерфейс [IDebugComPlusSymbolProvider.](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)

```cpp
HRESULT CDebugSymbolProvider::IsFunctionDeleted(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pAddress, IDebugAddress));

    METHOD_ENTRY( CDebugSymbolProvider::IsFunctionDeleted );

    IfFalseGo( pAddress, S_FALSE );
    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->IsFunctionDeleted( address.addr.addr.addrMethod.tokMethod,
                                     address.addr.addr.addrMethod.dwVersion,
                                     address.addr.addr.addrMethod.dwOffset ))
    {

        // S_FALSE indicates the function is not deleted

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::IsFunctionDeleted, hr );

    if (!SUCCEEDED(hr))
    {
        hr = S_FALSE;
    }

    return hr;
}
```

## <a name="see-also"></a>См. также
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
