---
title: Функция SccRunScc | Документация Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SccRunScc
helpviewer_keywords:
- SccRunScc function
ms.assetid: bbe7c931-b17a-4779-9cf6-59e5f9f0c172
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e3baaf2fb58720d34dfa3dc2cac7cf3b44d7f1c7
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47572929"
---
# <a name="sccrunscc-function"></a>Функция SccRunScc
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [функция SccRunScc](https://docs.microsoft.com/visualstudio/extensibility/sccrunscc-function).  
  
Эта функция вызывает инструментом администрирования системы управления версиями.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp#  
SCCRTN SccRunScc(  
   LPVOID  pvContext,  
   HWND    hWnd,  
   LONG    nFiles,  
   LPCSTR* lpFileNames  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 pvContext  
 [in] Структура подключаемого модуля контекста исходного элемента управления.  
  
 hWnd  
 [in] Дескриптор окна интегрированной среды разработки, подключаемый модуль системы управления версиями можно использовать в качестве родительского для любой диалоговых окон, которые он предоставляет.  
  
 nFiles  
 [in] Число файлов, указанных в `lpFileNames` массива.  
  
 lpFileNames  
 [in] Массив имен выбранного файла.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Подключаемый модуль реализации элемента управления источника этой функции должен возвращать одно из следующих значений:  
  
|Значение|Описание|  
|-----------|-----------------|  
|SCC_OK|Инструментом администрирования системы управления версиями успешно вызвана.|  
|SCC_I_OPERATIONCANCELED|Операция была отменена.|  
|SCC_E_INITIALIZEFAILED|Не удалось инициализировать системы управления версиями.|  
|SCC_E_ACCESSFAILURE|Возникла проблема с доступом к системе управления версиями, возможно, из-за проблемы с сетью или конфликтов.|  
|SCC_E_CONNECTIONFAILURE|Не удалось подключиться к системе управления версиями.|  
|SCC_E_FILENOTCONTROLLED|Выбранный файл не существует в системе управления версиями.|  
|SCC_E_NONSPECIFICERROR|Обнаружена неспецифическая ошибка.|  
  
## <a name="remarks"></a>Примечания  
 Эта функция позволяет вызывающему объекту доступ к полному набору функций системы управления версиями через инструментом внешних администрирования. Если нет пользовательского интерфейса системы управления версиями, подключаемый модуль системы управления версиями можно реализовать интерфейс для выполнения функций необходимости администрирования.  
  
 Эта функция вызывается с числом и массив имен файлов для выбранных файлов. Если ее поддерживает средство администрирования, список файлов, можно использовать для предварительного выбора файлов в интерфейсе администрирования; в противном случае можно игнорировать списка.  
  
 Эта функция обычно вызывается, когда пользователь выбирает **запуска \<сервера системы управления версиями >** из **файл** -> **системы управления версиями** меню. Это **запуска** пункт меню можно всегда отключен или даже скрыть, установив параметр реестра. См. в разделе [как: установить подключаемый модуль системы управления источника](../extensibility/internals/how-to-install-a-source-control-plug-in.md) подробные сведения. Эта функция вызывается только в том случае, если [SccInitialize](../extensibility/sccinitialize-function.md) возвращает `SCC_CAP_RUNSCC` бит функции (см. в разделе [флаги возможностей](../extensibility/capability-flags.md) Дополнительные сведения об этом и других биты возможностей).  
  
## <a name="see-also"></a>См. также  
 [Функции API подключаемого модуля управления источника](../extensibility/source-control-plug-in-api-functions.md)   
 [Как: установить подключаемый модуль системы управления версиями](../extensibility/internals/how-to-install-a-source-control-plug-in.md)   
 [Флаги возможностей](../extensibility/capability-flags.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)
