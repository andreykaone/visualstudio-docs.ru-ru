---
title: Регистрация и отбор (Источник управления VSPackage) Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 973eb19916a737dfa775fe79ee62cb3d11fe0123
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705723"
---
# <a name="registration-and-selection-source-control-vspackage"></a>Регистрация и выбор (пакет VSPackage системы управления версиями)
Контроль источника VSPackage должен быть зарегистрирован, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]чтобы подвергнуть его . Если зарегистрировано несколько источников управления VSPackage, пользователь может выбрать, какой VSPackage загрузить в соответствующее время. Более подробную информацию о VSPackages и о том, как их зарегистрировать, можно найти на [VSPackages.](../../extensibility/internals/vspackages.md)

## <a name="registering-a-source-control-package"></a>Регистрация пакета управления источниками
 Пакет управления исходным ресурсом [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] зарегистрирован таким образом, чтобы среда смогли найти его и запросить поддерживаемые функции. Это соответствует схеме задержки загрузки, в которой экземпляр пакета создается только тогда, когда требуются его функции или команды или запрашиваются явно.

 VSPackages место информации в версии конкретного реестра ключ,\\HKEY_LOCAL_MACHINE»SOFTWARE-Microsoft-VisualStudio*X.Y*, где *X* является основным номером версии и *Y* является второстепенным номером версии. Эта практика обеспечивает возможность поддержки боковой установки [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]нескольких версий.

 Пользовательский [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] интерфейс (UI) поддерживает выбор из нескольких установленных плагинов управления исходным элементом (через пакет адаптера управления исходным управлением), а также управления исходным управлением VSPackages. Там может быть только один активный плагин управления исходным источником или VSPackage одновременно. Однако, как описано ниже, IDE позволяет переключаться между плагинами управления исходным управлением и VSPackages через автоматический механизм замены пакетов на основе решений. Есть некоторые требования со стороны управления исходом VSPackage, чтобы этот механизм отбора.

### <a name="registry-entries"></a>Записи реестра
 Пакет управления источниками нуждается в трех частных GUID:

- Пакет GUID: Это основной GUID для пакета, который содержит реализацию управления исходным управлением (называемый ID_Package в этом разделе).

- GUID управления исходным элементом: Это GUID для управления исходным управлением VSPackage, используемый для регистрации в Visual Studio Source Control Stub, а также используется в качестве контекста интерфейса управления интерфейсом. Служба управления источниками GUID зарегистрирована под контролем источника GUID. В этом примере GUID управления исходным источником называется ID_SccProvider.

- Служба управления источниками GUID: Это частная услуга GUID, используемая Visual Studio (называемая SID_SccPkgService в этом разделе). В дополнение к этому, пакет управления исходным источником должен определить другие GUIDдля для VSPackages, окна инструментов, и так далее.

  Следующие записи реестра должны быть сделаны элементом управления источником VSPackage:

| Имя ключа | Записи |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (по умолчанию) rg_sz: ID_SccProvider |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | (по умолчанию)\<- rg_sz: Дружественное название пакета><br /><br /> Обслуживание и rg_sz: (SID_SccPkgService) |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | (по умолчанию)\<- rg_sz: идентификатор ресурсов для локализованных имен><br /><br /> Пакет и rg_sz: (ID_Package) |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (Обратите внимание, что `SourceCodeControl`ключевое имя, уже используется [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] и \<не доступно в качестве выбора для PackageName>.) | (по умолчанию) rg_sz ID_Package: |

## <a name="selecting-a-source-control-package"></a>Выбор пакета управления исходным ресурсом
 Одновременно могут быть зарегистрированы несколько плагинов на основе API на основе API и управления исходным управлением VSPackages. Процесс выбора плагина управления исходным элементом или [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage должен гарантировать, что плагин или VSPackage загружается в соответствующее время, и может отложить загрузку ненужных компонентов, пока они не потребуются. Кроме того, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] необходимо удалить все uI из других неактивных VSPackages, включая пункты меню, диалоговые поля и панели инструментов, а также отобразить uI для активного VSPackage.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]загружает элемент управления VSPackage при выполнении любой из следующих операций:

- Решение открывается (когда решение находится под контролем источника).

   При открытии решения или проекта под контролем источника IDE вызывает загрузку управления исходным элементом VSPackage, предназначенного для загрузки этого решения.

- Все команды меню управления исходным элементом VSPackage выполняются.

  Управление источником VSPackage должно загружать все компоненты, которые ему нужны, только тогда, когда они будут использованы (иначе известный как задержка загрузки).

### <a name="automatic-solution-based-vspackage-swapping"></a>Автоматическое решение на основе VSPackage Swapping
 Вы можете вручную поменять управление [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] исходом VSPackages через диалоговую коробку **Options** в категории **Управления источниками.** Автоматическая замена пакетов на основе решений означает, что пакет управления исходным источником, назначенный для конкретного решения, автоматически настроен на активную работу при открытии этого решения. Каждый пакет управления <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>источниками должен реализовывать и . [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]обрабатывает коммутатор между плагинами управления исходным кодом (реализация API-кода управления исходным управлением) и vsPackages управления исходным кодом.

 Пакет адаптера управления исходным кодом используется для переключения на любой плагин на основе API-наосновения Source Control. Процесс перехода на промежуточный пакет адаптера управления исходным элементом и определения того, какой плагин управления исходным элементом должен быть настроен на активный или неактивный, является прозрачным для пользователя. Пакет Adapter всегда активен, когда активен любой плагин управления исходным источником. Переключение между двумя плагинами управления исходным источником означает просто загрузку и разгрузку плагина DLL. Переключение на управление исходным управлением VSPackage, однако, включает взаимодействие с IDE для загрузки соответствующего VSPackage.

 Контроль источника VSPackage вызывается, когда любое решение открыто, и ключ реестра для VSPackage находится в файле решения. Когда решение открыто, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] находит значение реестра и загружает соответствующий элемент управления исходом VSPackage. Все элементы управления источниками VSPackages должны иметь записи реестра, описанные выше. Решение, находясь под контролем источника, помечается как связанное с определенным элементом управления исходным элементом VSPackage. Управление источником VSPackages <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> должны реализовать для автоматического решения на основе VSPackage замены.

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>Визуальный развитель студии для выбора и переключения пакетов
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]обеспечивает uI для управления исходным управлением VSPackage и выбор плагинов в диалоговом поле **Options** в категории **Управления исходным управлением.** Это позволяет пользователю выбрать активный плагин управления исходным элементом или VSPackage. Список выпадающих списков включает в себя:

- Все установленные пакеты управления исходом

- Все установленные плагины управления исходным элементом

- Опция "нет", которая отключает управление исходным кодом

  Виден только uI для активного выбора управления исходом. Выбор VSPackage скрывает uI для предыдущего VSPackage и показывает uI для нового. Активный VSPackage выбирается на основе пользователя. Если пользователь имеет несколько [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] копий открытых одновременно, каждый из них потенциально может использовать различные активные VSPackage. Если несколько пользователей вошли в систему на один и [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] тот же компьютер, каждый пользователь может иметь отдельные экземпляры открытых, каждый из которых имеет различные активные VSPackage. Когда несколько [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] экземпляров закрыты пользователем, управление исходным кодом VSPackage, который был активен для последнего открытого решения, становится контролем источника по умолчанию VSPackage, который будет активен при перезагрузке.

  В отличие [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]от предыдущих версий, перезагрузка IDE больше не единственный способ переключить управление исходным кодом VSPackages. Выбор VSPackage происходит автоматически. Для переключения пакетов требуются привилегии пользователя Windows (не администратор или пользователь питания).

## <a name="see-also"></a>См. также
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [Компоненты](../../extensibility/internals/source-control-vspackage-features.md)
- [Создание подключаемого модуля системы управления версиями](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [Пакеты VSPackage](../../extensibility/internals/vspackages.md)
