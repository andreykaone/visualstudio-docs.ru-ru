---
title: Практическое руководство. Сборка с использованием нескольких конфигураций
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33cd217a08f62b4919af6d72017176c110cf5e5a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "77904091"
---
# <a name="how-to-build-multiple-configurations-simultaneously"></a>Практическое руководство. Сборка с использованием нескольких конфигураций

Большинство типов проектов можно создать с использованием нескольких или даже всех конфигураций сборки одновременно с помощью диалогового окна **Пакетная сборка**. Однако вы не можете одновременно выполнять сборку следующих типов проектов в нескольких конфигурациях сборок:

1. Приложения [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)], созданные для Windows с использованием JavaScript.

2. Все проекты Visual Basic.

Если решение содержит какие-либо проекты этих двух типов, то **Пакетная сборка** для этого решения будет недоступна. В этом случае команда не отображается в меню **Сборка**.

   Дополнительные сведения о конфигурациях сборки см. в статье [Общие сведения о конфигурациях сборки](../ide/understanding-build-configurations.md).

## <a name="to-build-a-project-in-multiple-build-configurations"></a>Сборка проекта в нескольких конфигурациях сборок

1. В строке меню выберите **Сборка** > **Пакетная сборка**. Или нажмите клавиши **Ctrl**+**Q**, чтобы открыть поле поиска, и выполните поиск `Batch Build`.

2. В столбце **Сборка** установите флажки для конфигураций, с которыми требуется выполнить сборку проекта.

    > [!TIP]
    > Если вы хотите изменить или создать конфигурацию сборки для решения, выберите **Сборка** > **Диспетчер конфигураций** в строке меню, чтобы открыть диалоговое окно **Диспетчер конфигураций**. После изменения конфигурации сборки для решения нажмите кнопку **Пересобрать** в диалоговом окне **Пакетная сборка**, чтобы обновить все конфигурации сборки для проектов в решении.

3. Нажмите кнопку **Сборка** или **Пересобрать** для сборки проекта с указанными конфигурациями.

## <a name="see-also"></a>См. также

- [Практическое руководство. Создание и изменение конфигураций](../ide/how-to-create-and-edit-configurations.md)
- [Общие сведения о конфигурациях построения](../ide/understanding-build-configurations.md)
- [Параллельная сборка нескольких проектов](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)