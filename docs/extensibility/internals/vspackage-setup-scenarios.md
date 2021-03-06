---
title: VSPackage Настройка Сценарии (ru) Документы Майкрософт
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01279666642adb729d4350b8a497c42d78159120
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703975"
---
# <a name="vspackage-setup-scenarios"></a>Сценарии установки VSPackage

Важно, чтобы разработать ваш установщик VSPackage для гибкости. Например, в будущем может потребоваться выпуск патча безопасности, или это может изменить бизнес-стратегию, которая требует тщательной поддержки версий.

В [поддержку нескольких версий Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)вы можете прочитать о преимуществах и [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] проблемах поддержки бок о бок установки либо с общими или бок о бок установки вашего VSPackage. Короче говоря, бок о бок VSPackages дать вам максимальную [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]гибкость для поддержки новых функций .

Сценарии, обсуждаемые в этой теме, не являются единственным выбором, но они представлены в качестве предлагаемых рекомендаций.

## <a name="components-privacy-and-sharing"></a>Компоненты, конфиденциальность и совместное использование

### <a name="make-your-components-independent"></a>Сделайте ваши компоненты независимыми

После того как вы определите и `GUID`заселяете компонент, назначите и развернете компонент, вы не сможете изменить его состав. Если вы измените состав компонента, полученный компонент должен стать `GUID`новым компонентом с новым. С учетом этих фактов наибольшая гибкость в версиях обеспечивается за счет того, что каждый компонент становится независимым, самостоятельным подразделением. Для получения дополнительной информации о правилах, [What Happens if the Component Rules Are Broken?](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)регулирующих компоненты, [см.](/windows/desktop/Msi/changing-the-component-code)

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>Не смешивайте общие и частные ресурсы в компоненте

Подсчет ссылок происходит на уровне компонента. Следовательно, смешивание общих и частных ресурсов в одном компоненте делает невозможным обновление частных ресурсов, таких как исполняемый файл, без перезаписи общих ресурсов. Этот сценарий создает проблемы обратной совместимости и ограничивает вас от создания бок о бок возможности.

Например, значения реестра, используемые для [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] регистрации VSPackage с должны храниться в компоненте отдельно от одного используется для регистрации VSPackage с Visual Studio. Общие файлы или значения реестра переходят в еще один компонент.

## <a name="scenario-1-shared-vspackage"></a>Сценарий 1: Общий VSPackage

В этом сценарии общий VSPackage (один двоичный файл, поддерживающий несколько версий Visual Studio, поставляется в пакете установки Windows. Регистрация с каждой версией Visual Studio контролируется пользователями, которые выбираются пользователями. Это также означает, что при выделении отдельных функций, каждый компонент может быть выбран индивидуально для установки [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]или неустановки, поставив пользователя в управление интеграции VSPackage в различных версиях . (См. [Функции установки Windows](/windows/desktop/Msi/windows-installer-features) для получения дополнительной информации об использовании функций в пакетах Установки Windows.)

![VS Общий установщик VSPackage](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

Как показано на иллюстрации, общие компоненты являются частью Feat_Common функции, которая всегда устанавливается. Делая Feat_VS2002 и Feat_VS2003 функции видимыми, пользователи могут выбрать при установке времени, в какую версию Visual Studio они хотят, чтобы VSPackage интегрировать. Пользователи также могут использовать режим обслуживания установки Windows для добавления или удаления функций, которые в этом случае добавляют или удаляют регистрационную информацию VSPackage из различных версий Visual Studio.

> [!NOTE]
> Установка столбца дисплея объекта до 0 скрывает его. Низкое значение столбца уровня, например 1, гарантирует, что она всегда будет установлена. Для получения дополнительной информации [Feature Table](/windows/desktop/Msi/feature-table) [см.](/windows/desktop/Msi/installlevel)

## <a name="scenario-2-shared-vspackage-update"></a>Сценарий 2: Совместное обновление VSPackage

В этом сценарии отправляется обновленная версия установки VSPackage в сценарии 1. Для обсуждения обновление добавляет поддержку Visual Studio, но это также может быть более простой патч безопасности или пакет услуг по исправлению ошибок. Правила установки Windows для установки новых компонентов требуют, чтобы неизменные компоненты, уже намироваваемые в системе, не были восстановлены. В этом случае уже присутствуюшая система с уже присутствуют версия 1.0 перезапишет обновленный компонент Comp_MyVSPackage.dll и позволит пользователям выбрать для добавления новой функции Feat_VS2005 с ее компонентом Comp_VS2005_Reg.

> [!CAUTION]
> Всякий раз, когда VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]делится между несколькими версиями, важно, чтобы последующие релизы VSPackage поддерживать обратную совместимость с предыдущими версиями Visual Studio. В тех случаях, когда вы не можете поддерживать обратную совместимость, необходимо использовать частные VSPackage. Для получения дополнительной [информации см.](../../extensibility/supporting-multiple-versions-of-visual-studio.md)

![VS Общие VS Пакет Обновление установщик](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

Этот сценарий представляет собой новый установщик VSPackage, пользуясь поддержкой Windows Installer для незначительных обновлений. Пользователи просто установить версию 1.1 и он обновляет версию 1.0. Тем не менее, не обязательно иметь версию 1.0 в системе. Тот же установщик установит версию 1.1 на систему без версии 1.0. Преимущество, чтобы обеспечить незначительные обновления таким образом, что это не обязательно, чтобы пройти через работу по разработке обновления установки и полного продукта установки. Один установщик выполняет обе работы. Исправление безопасности или пакет услуг могут вместо этого воспользоваться исправлениями установки Windows. Для получения дополнительной информации [см.](/windows/desktop/Msi/patching-and-upgrades)

## <a name="scenario-3-side-by-side-vspackage"></a>Сценарий 3: Бок на стороне VSPackage

Этот сценарий представляет два VSPackage установщиков - по одному для каждой версии Visual Studio .NET 2003 и Visual Studio. Каждый установщик устанавливает бок о бок, или частный, VSPackage (тот, который специально построен и установлен для конкретной версии Visual Studio). Каждый VSPackage находится в своем собственном компоненте. Следовательно, каждый из них может обслуживаться индивидуально с помощью патчей или релизов технического обслуживания. Поскольку VSPackage DLL теперь специфичен для версии, можно смело включать регистрационную информацию в тот же компонент, что и DLL.

![Установщик пакета VS Side by-Side](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

Каждый установщик также включает в себя код, который разделяется между двумя установщиками. Если общий код установлен в общем месте, установка обоих файлов .msi установит общий код только один раз. Второй установщик только приращения ссылки рассчитывать на компонент. Подсчет ссылок гарантирует, что если один из VSPackages не установлен, общий код останется для другого VSPackage. Если второй VSPackage также не установлен, общий код будет удален.

## <a name="scenario-4-side-by-side-vspackage-update"></a>Сценарий 4: Бок на стороне VSPackage обновление

В этом случае ваш VSPackage для Visual Studio пострадал от уязвимости в безопасности, и вам нужно выпустить обновление. Как и в сценарии 2, можно создать новый файл .msi, который обновляет существующую установку для включения исправления безопасности, а также развертывать новые установки с исправлением безопасности уже на месте.

В этом случае VSPackage является управляемым VSPackage, установленным в глобальном кэше сборки (GAC). При восстановлении исправления безопасности необходимо изменить часть номера сборки номером номера версии. Регистрационная информация для нового номера сборки перезаписывает предыдущую версию, вызывая [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] загрузку фиксированной сборки.

![VS Бок-за боком VS Установщик пакета](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

Для получения дополнительной информации о развертывании бок о бок сборки, см [Упрощение развертывания и решения DLL Ад с .NET Framework](https://msdn.microsoft.com/library/ms973843.aspx).

## <a name="see-also"></a>См. также

- [Установщик Windows](/windows/desktop/Msi/windows-installer-portal)
- [Поддержка нескольких версий Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)
