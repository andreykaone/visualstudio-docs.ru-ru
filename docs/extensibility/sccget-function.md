---
title: Функция SccGet (англ.) Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2d69308d2f569fc2e0d72dcf64c762687955d4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700892"
---
# <a name="sccget-function"></a>Функция SccGet
Эта функция получает копию одного или нескольких файлов для просмотра и компиляции, но не для редактирования. В большинстве систем файлы помечаются как только для чтения.

## <a name="syntax"></a>Синтаксис

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Параметры
 pvКонтекст

(в) Структура контекста плагина управления исходным элементом.

 Hwnd

(в) Ручка к окну IDE, которую плагин управления исходным элементом может использоваться в качестве родительского элемента для любых диалоговых коробок, которые она предоставляет.

 nФайлы

(в) Количество файлов, указанных в массиве. `lpFileNames`

 lpFileNames

(в) Массив полностью квалифицированных имен файлов, которые необходимо получить.

 fВарианты

(в) Флаги`SCC_GET_ALL`командования `SCC_GET_RECURSIVE`(, ).

 pvOptions

(в) Опции управления исходным управлением.

## <a name="return-value"></a>Возвращаемое значение
 Ожидается, что внедрение этой функции элемента управления исходным элементом вернет одно из следующих значений:

|Значение|Описание|
|-----------|-----------------|
|SCC_OK|Успех операции.|
|SCC_E_FILENOTCONTROLLED|Файл не находится в системе управления версиями.|
|SCC_E_OPNOTSUPPORTED|Система управления исходным источником не поддерживает эту операцию.|
|SCC_E_FILEISCHECKEDOUT|Не удается получить файл, который пользователь в настоящее время проверил.|
|SCC_E_ACCESSFAILURE|Возникла проблема с доступом к системе управления исходным кодом, вероятно, из-за проблем с сетью или раздором. Рекомендуется повторная попытка.|
|SCC_E_NOSPECIFIEDVERSION|Указана недействительная версия или дата/время.|
|SCC_E_NONSPECIFICERROR|Неспецифический сбой; файл не был синхронизирован.|
|SCC_I_OPERATIONCANCELED|Операция отменена до завершения.|
|SCC_E_NOTAUTHORIZED|У пользователя нет разрешений на выполнение этой операции.|

## <a name="remarks"></a>Примечания
 Эта функция вызывается с подсчетом и массивом имен файлов, которые необходимо получить. Если IDE проходит `SCC_GET_ALL`флаг, это означает, `lpFileNames` что элементы в не файлы, но каталоги, и что все файлы под контролем источника в данных каталогах должны быть извлечены.

 Флаг `SCC_GET_ALL` можно комбинировать `SCC_GET_RECURSIVE` с флагом, чтобы получить все файлы в данных каталогах и во всех субдиректорах.

> [!NOTE]
> `SCC_GET_RECURSIVE`никогда не `SCC_GET_ALL`должны быть переданы без . Кроме того, обратите внимание, что если каталоги *C: 'A* и *C: 'A'B* оба передаются на рекурсивный получить, *C: ЗАЗБ* и все его субдиректоров на самом деле будут извлечены в два раза. Это ответственность IDE, а не плагин управления исходным элементом, чтобы убедиться, что дубликаты, подобные этому, не доходят до массива.

 Наконец, даже если плагин управления `SCC_CAP_GET_NOUI` исходным источником указал флаг на инициализацию, указав, что у него нет пользовательского интерфейса для команды Get, эта функция все равно может быть вызвана IDE для извлечения файлов. Флаг просто означает, что IDE не отображает элемент меню Get и что плагин не должен предоставлять какой-либо ui.

## <a name="rename-files-and-sccget"></a>Переименование файлов и SccGet
 Ситуация: пользователь проверяет файл, например, *a.txt,* и изменяет его. Перед регистрацией *a.txt* второй пользователь переименовывает *a.txt* в *b.txt* в базе данных управления исходным управлением, проверяет *b.txt,* вносит некоторые изменения в файл и проверяет файл. Первый пользователь хочет, чтобы изменения, внесенные вторым пользователем, чтобы первый пользователь переименовывали свою локальную версию файла *a.txt* на *b.txt* и сделал попасть в файл. Однако локальный кэш, отслеживающий номера версий, по-прежнему считает, что первая версия *a.txt* хранится локально, поэтому элемент управления источниками не может разрешить различия.

 Существует два способа разрешения этой ситуации, когда локальный кэш версий управления исходным источником не синхронизируется с базой данных управления исходным источником:

1. Не допускайте переименования файла в базу данных управления исходным источником, которая в настоящее время проверяется.

2. Сделайте эквивалент "удалить старый", а затем "добавить новый". Следующий алгоритм является одним из способов достижения этой цели.

    1. Позвоните в функцию [Scc'ru,](../extensibility/sccquerychanges-function.md) чтобы узнать о переименовании *a.txt* в *b.txt* в базе данных управления исходным источником.

    2. Переименуйте местный *a.txt* в *b.txt*.

    3. Позвоните `SccGet` в функцию для *a.txt* и *b.txt.*

    4. Поскольку *a.txt* не существует в базе данных управления исходным элементом, кэш локальной версии очищается от отсутствующих данных версии *a.txt.*

    5. Проверяемый файл *b.txt* сливается с содержимым локального файла *b.txt.*

    6. Обновленный файл *b.txt* теперь можно регистрировать.

## <a name="see-also"></a>См. также
- [Функции API управления исходным элементом](../extensibility/source-control-plug-in-api-functions.md)
- [Битфлаги, используемые определенными командами](../extensibility/bitflags-used-by-specific-commands.md)
