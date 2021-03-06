---
title: Добавление ссылок с использованием NuGet или расширения SDK
ms.date: 08/02/2019
ms.topic: conceptual
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad7fc9132647988aee46a2bb07e992505109d33c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702431"
---
# <a name="nuget-versus-sdk-as-a-project-reference"></a>NuGet против SDK в качестве ссылки на проект

Эта статья разработана, чтобы помочь разработчикам выбрать, следует ли упаковать свое программное обеспечение в пакет NuGet или в комплект разработки программного обеспечения (SDK). В частности, он обсуждает различия между ними, когда они упоминаются в проекте Visual Studio.

- [NuGet](/nuget) — это система управления пакетами с открытым исходным кодом, которая упрощает процесс включения библиотек в проект. Для .NET (включая .NET Core) NuGet является поддерживаемым корпорацией Майкрософт механизмом обмена кодом. NuGet определяет, как создаются, размещаются и потребляются пакеты для .NET, и предоставляет инструменты для каждой из этих ролей. В Visual Studio вы добавляете пакеты NuGet в проект с помощью пользовательского интерфейса [Package Manager.](/nuget/consume-packages/install-use-packages-visual-studio)

- [SDK](../extensibility/creating-a-software-development-kit.md) представляет собой набор файлов, которые Visual Studio рассматривает как единый справочный элемент. В диалоговом окне справочного менеджера в Visual Studio перечислены все SDK, имеющие отношение к текущему проекту при выборе **добавления справки.** При добавлении SDK в проект можно получить доступ ко всему содержимому этого SDK через IntelliSense, окно Toolbox, конструкторов, Object Browser, MSBuild, развертывание, отладку и упаковку.

## <a name="which-mechanism-should-i-use"></a>Какой механизм следует использовать?

В следующей таблице приводится сравнение ссылочных функций пакета SDK и NuGet.

| Компонент | Поддержка пакета SDK | Примечания для пакета SDK | Поддержка NuGet | Примечания для NuGet |
| - | - | - |---------------| - |
| Механизм ссылается на одну сущность, после чего становятся доступны все файлы и функциональные возможности. | Да | Для добавления пакета SDK используется диалоговое окно **Диспетчер ссылок**, и все файлы и функциональные возможности будут доступны во время рабочего процесса разработки. | Да | |
| MSBuild автоматически использует сборки и файлы метаданных Windows (*WINMD-файлы*). | Да | Ссылки в пакете SDK автоматически передаются в компилятор. | Да | |
| MSBuild автоматически использует H- или LIB-файлы. | Да | Файл *имя_пакета_SDKN.props* указывает Visual Studio, как настроить каталог Visual C++ и т. д. для автоматического использования *H-файлов* или *LIB-файлов*. | Нет | |
| MSBuild автоматически использует *JS-файла* или *CSS-файлы*. | Да | В **обозревателе решений** можно развернуть узел ссылки на пакет SDK для JavaScript для отображения отдельных *JS-файлов* или *CSS-файлов*, затем создать теги `<source include/>` путем перетаскивания этих файлов в их исходные файлы. Пакет SDK поддерживает функциональность клавиши F5 и автоматическую установку пакетов. | Да | |
| MSBuild автоматически добавляет элемент управления на **панель элементов**. | Да | **Панель элементов** может использовать пакеты SDK и отображать элементы управления на указанных вкладках. | Нет | |
| Механизм поддерживает установщик Visual Studio для расширений (VSIX). | Да | VSIX располагает специальным манифестом и логикой для создания пакетов SDK. | Да | VSIX можно внедрить в другую программу установки. |
| **Обозреватель объектов** перечисляет ссылки. | Да | **Обозреватель объектов** автоматически получает список ссылок в пакете SDK и перечисляет их. | Нет | |
| Файлы и ссылки автоматически добавляются в диалоговое окно **Диспетчер ссылок** (ссылки на справку, автозаполнение и т. д). | Да | В диалоговом окне **Диспетчер ссылок** автоматически перечисляются пакеты SDK, а также ссылки на справку и список зависимостей пакета SDK. | Нет | NuGet предоставляет собственное диалоговое окно **Управление пакетами NuGet**. |
| Механизм поддерживает несколько архитектур. | Да | Пакеты SDK могут предоставлять несколько конфигураций. MSBuild использует соответствующие файлы для каждой конфигурации проекта. | Нет | |
| Механизм поддерживает несколько конфигураций. | Да | Пакеты SDK могут предоставлять несколько конфигураций. В зависимости от архитектуры проекта MSBuild использует для каждой архитектуры соответствующие файлы. | Нет | |
| Механизм может запретить копирование файлов. | Да | В зависимости от папки размещения файлов (*\redist* или *\designtime*) можно контролировать, какие файлы следует копировать в пакет работающего приложения. | Нет | Файлы, предназначенные для копирования, объявляются в манифесте пакета. |
| Содержимое отображается в локализованных файлах. | Да | Локализованные XML-документы в пакетах SDK автоматически включаются для повышения эффективности процесса разработки. | Нет | |
| MSBuild поддерживает одновременное использование нескольких версий пакета SDK. | Да | Пакет SDK поддерживает одновременное использование нескольких версий. | Нет | Ссылки отсутствуют. В проекте не может быть несколько версий файлов NuGet одновременно. |
| Механизм поддерживает указание соответствующих целевых платформ, версий Visual Studio и типов проектов. | Да | В диалоговом окне **Диспетчер ссылок** и на **панели элементов** отображаются только пакеты SDK, применимые к проекту, чтобы пользователи могли без труда выбирать соответствующие пакеты SDK. | Да (частично) | Целевой рабочей средой является сводная среда. Фильтрация в пользовательском интерфейсе отсутствует. Во время установки может быть возвращена ошибка. |
| Механизм поддерживает указание сведений о регистрации собственных WINMD-файлов. | Да | Можно указать взаимосвязь между WINMD-файлами и DLL-файлами в *SDKManifest.xml*. | Нет | |
| Механизм поддерживает указание зависимостей от других пакетов SDK. | Да | Пакет SDK только уведомляет пользователя. Пользователь по-прежнему должен устанавливать их и ссылаться на них вручную. | Да | NuGet извлекает их автоматически. Пользователь не получает уведомления. |
| Механизм интегрируется с такими компонентами [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)], как манифест приложения и идентификатор платформы. | Да | Пакет SDK должен поддерживать основные принципы [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)], чтобы обеспечить правильную работу функций упаковки и F5 с пакетами SDK, которые доступны в [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)]. | Нет | |
| Механизм интегрируется с конвейером отладки приложений для приложений [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]. | Да | Пакет SDK должен поддерживать основные принципы [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)], чтобы обеспечить правильную работу функций упаковки и F5 с пакетами SDK, которые доступны в [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)]. | Да | Содержимое NuGet становится частью проекта. Особых указания относительно использования F5 отсутствуют. |
| Механизм интегрируется с манифестами приложений. | Да | Пакет SDK должен поддерживать основные принципы [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)], чтобы обеспечить правильную работу функций упаковки и F5 с пакетами SDK, которые доступны в [!INCLUDE[win8_appstore_short](../ide/includes/win8_appstore_short_md.md)]. | Да | Содержимое NuGet становится частью проекта. Особых указания относительно использования F5 отсутствуют. |
| Механизм развертывает файлы без ссылок (например, развертывание платформы тестирования, на которой будут тестироваться приложения [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]). | Да | Файлы, помещаемые в папку *\redist*, развертываются автоматически. | Да | |
| Механизм автоматически добавляет пакеты SDK для платформы в интегрированную среду разработки Visual Studio. | Да | Если поместить пакет SDK для [!INCLUDE[win8](../debugger/includes/win8_md.md)] или пакета SDK для Windows Phone в определенное место с определенной структурой, он автоматически интегрируется с помощью функций Visual Studio. | Нет | |
| Механизм поддерживает компьютер для разработки без установленных программ. (Это значит, что устанавливать ничего не требуется — действуют только принципы простого извлечения из системы управления версиями.) | Нет | Поскольку вы ссылаетесь на пакет SDK, необходимо отдельно вернуть решение и пакет SDK. Пакет SDK можно вернуть из двух расположений по умолчанию вне реестра, из которых MSBuild выполняет итерацию по пакетам SDK (дополнительные сведения см. в статье [Creating a Software Development Kit](../extensibility/creating-a-software-development-kit.md) (Создание пакета средств разработки программного обеспечения)). Или если пользовательское расположение состоит из пакетов SDK, можно указать следующий код в файле проекта:<br /><br />`<PropertyGroup>`<br />&nbsp;&nbsp;`<SDKReferenceDirectoryRoot>`<br />&nbsp;&nbsp;`C:\MySDKs`<br />&nbsp;&nbsp;`</SDKReferenceDirectoryRoot>`<br />`</PropertyGroup>`<br /><br /> Затем верните пакеты SDK в это расположение. | Да | Можно извлечь решение, и Visual Studio немедленно распознает файлы и обработает их. |
| Вы можете войти в крупное существующее сообщество создателей пакетов. | Недоступно | Сообщество является новой организацией. | Да | |
| Вы можете войти в крупное существующее сообщество потребителей пакетов. | Недоступно | Сообщество является новой организацией. | Да | |
| Вы можете присоединиться к экосистеме партнеров (пользовательские коллекции, репозиторий и т. д.). | Недоступно | Доступные репозитории включают: Visual Studio Marketplace, Центр загрузки Майкрософт и [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]. | Да | |
| Механизм интегрируется с серверами построения непрерывной интеграции как для создания, так и для использования пакетов. | Да | Пакет SDK должен передать возвращенное расположение (свойство SDKReferenceDirectoryRoot) с помощью командной строки в MSBuild. | Да | |
| Механизм поддерживает основную и предварительную версии пакетов. | Да | Пакет SDK поддерживает добавление ссылок на несколько версий. | Да | |
| Механизм поддерживает автоматическое обновление установленных пакетов. | Да | Если пакет SDK поставляется в виде VSIX или в составе автоматических обновлений Visual Studio, он предоставляет автоматические уведомления. | Да | |
| Механизм содержит автономный *EXE-файл* для создания и использования пакетов. | Да | Пакет SDK содержит *MSBuild.exe*. | Да | |
| Пакеты можно возвращать в систему управления версиями. | Да | Нельзя выполнять запись после изменения в объекты вне узла "Документы". Это значит, что пакеты SDK могут быть не возвращены. Расширение SDK может иметь большой размер. | Да | |
| Для создания и потребления пакетов можно использовать интерфейс PowerShell. | Да (потребление), Нет (создание) | Инструментарий для создания пакета SDK отсутствует. При потреблении MSBuild выполняется в командной строке. | Да | |
| Для поддержки отладки можно использовать пакет символов. | Да | *PDB-файлы*, размещаемые в пакете SDK, выбираются автоматически. | Да | |
| Механизм поддерживает автообновление диспетчера пакетов. | Недоступно | Пакет SDK обновляется с помощью MSBuild. | Да | |
| Механизм поддерживает упрощенный формат манифеста. | Да | *SDKManifest.xml* поддерживает много атрибутов, однако обычно требуется их небольшая часть. | Да | |
| Механизм доступен для всех выпусков Visual Studio. | Да | Пакет SDK поддерживает все выпуски Visual Studio. | Да | NuGet поддерживает все выпуски Visual Studio. |

## <a name="see-also"></a>См. также

- [Управление ссылками в проекте](../ide/managing-references-in-a-project.md)
- [Управление ссылками в проекте (Visual Studio для Mac)](/visualstudio/mac/managing-references-in-a-project)
