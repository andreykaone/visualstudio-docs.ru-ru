---
title: 'Пошаговое руководство: Отсутствие объектов вследствие неправильной настройки конвейера | Документация Майкрософт'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed8ac02d-b38f-4055-82fb-67757c2ccbb9
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b5cbe580bed0cda79a5a218109be1fd7f633f115
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47569908"
---
# <a name="walkthrough-missing-objects-due-to-misconfigured-pipeline"></a>Пошаговое руководство. Отсутствие объектов вследствие неправильной настройки конвейера
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [Пошаговое руководство: отсутствует объектов из-за неправильно конвейера](https://docs.microsoft.com/visualstudio/debugger/graphics/walkthrough-missing-objects-due-to-misconfigured-pipeline).  
  
В данном пошаговом руководстве показано, как с помощью средств диагностики графики [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] исследовать объект, который отсутствует из-за незаданного шейдера пикселей.  
  
 В данном пошаговом руководстве рассмотрены следующие задачи:  
  
-   Использование **списка событий графики** для обнаружения возможных источников проблем.  
  
-   Проверка результата вызова API Direct3D **с помощью окна** Этапы графического конвейера `DrawIndexed` .  
  
-   Проверка контекста устройства для проверки того, что этап шейдера не установлен.  
  
-   Поиск источника незаданного шейдера пикселей с помощью окна **Этапы графического конвейера** в сочетании с окном **Стек вызовов событий графики** .  
  
## <a name="scenario"></a>Сценарий  
 Отсутствие объекта в трехмерном приложении иногда бывает вызвано тем, что перед отрисовкой этого объекта не был задан один из этапов шейдера. В приложениях с простыми требованиями к отрисовке источник этой ошибки обычно находится где-либо в стеке вызовов рисования объекта. Однако в целях оптимизации некоторые приложения группируют объекты с общими программами-шейдерами, текстурами или другими данными, чтобы минимизировать расходы на смену состояний. В таких приложениях источник ошибки может находиться в глубинах системы пакетной обработки и не присутствовать в стеке вызовов рисования. В этом пошаговом руководстве рассматривается сценарий с приложением с простыми требованиями к отрисовке, поэтому источник ошибки можно найти в стеке вызовов.  
  
 В этом сценарии при запуске приложения для тестирования фон отрисовывается так, как ожидалось, однако один из объектов не отображается. С помощью диагностики графики можно записать данные о проблеме в журнал графики, чтобы можно было выполнить отладку приложения. Проблема в приложении выглядит следующим образом:  
  
 ![Объект не виден](../debugger/media/gfx-diag-demo-misconfigured-pipeline-problem.png "gfx_diag_demo_misconfigured_pipeline_problem")  
  
## <a name="investigation"></a>Исследование  
 С помощью средств диагностики графики можно загрузить документ журнала графики для проверки кадров, захваченных в ходе теста.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Анализ кадра в журнале графики  
  
1.  В [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] загрузите документ журнала графики, содержащий кадр, на котором видно, что объект отсутствует. Откроется новая вкладка журнала графики в [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. В верхней части этой вкладки находится вывод целевого объекта отрисовки для выбранного кадра. В нижней части находится **Список кадров**, в котором каждый захваченный кадр отображается как эскиз.  
  
2.  В **списке кадров**выберите кадр, который демонстрирует, что объект не отображается. Однобуферная прорисовка обновляется, и в ней отображается выбранный кадр. В этом сценарии вкладка журнала графики выглядит следующим образом:  
  
     ![Документ журнала графики в Visual Studio](../debugger/media/gfx-diag-demo-misconfigured-pipeline-step-1.png "gfx_diag_demo_misconfigured_pipeline_step_1")  
  
 После выбора кадра, который демонстрирует проблему, можно приступать к диагностике с использованием окна **Список событий графики**. **Список событий графики** содержит все вызовы API Direct3D, которые были выполнены для отрисовки активного кадра, — например, для настройки состояния устройства, для создания и обновления буферов, а также для рисования объектов, которые присутствуют в кадре. Многие типы вызовов, например вызовы Draw, Dispatch, Copy или Clear, представляют интерес, поскольку при надлежащей работе приложения часто (но не всегда) происходит соответствующее изменение в целевом объекте отрисовки. Особенно интересны вызовы Draw, поскольку каждый из них представляет геометрию, отрисованную приложением.  
  
 Поскольку вам известно, что в целевом объекте отрисовки нет отсутствующего объекта, однако нет и других ошибок, можно воспользоваться окном **Список событий графики** в сочетании с окном **Этапы графического конвейера** , чтобы определить, какой из вызовов рисования соответствует геометрии отсутствующего объекта. В окне **Этапы графического конвейера** показана геометрия, отправленная в каждый вызов Draw независимо от влияния на однобуферную прорисовку. По мере продвижения по вызовам рисования этапы конвейера обновляются для отображения геометрии, связанной с каждым вызовом при его проходе через каждый включенный этап, а вывод целевого объекта отрисовки обновляется для отображения состояния целевого объекта отрисовки по завершении вызова.  
  
#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>Поиск вызова Draw для отсутствующей геометрии  
  
1.  Откройте окно **Список событий графики** . На панели инструментов **Диагностика графики** выберите **Список событий**.  
  
2.  Откройте окно **Этапы графического конвейера** . На панели инструментов **Диагностика графики** выберите **Этапы конвейера**.  
  
3.  Просматривая вызовы Draw в окне **Список событий графики** , перейдите в окно **Этапы графического конвейера** для отсутствующего объекта. Чтобы упростить эту задачу, введите Draw в поле **Поиск** в верхнем правом углу окна **Список событий графики** . Список будет отфильтрован и будет содержать только события, в названиях которых присутствует слово «Draw».  
  
     В окне **Этапы графического конвейера** этап **Сборщик входных данных** показывает геометрию объекта перед его преобразованием, а этап **Шейдер вершин** показывает тот же объект после преобразования. Обратите внимание, что в этом сценарии в окне **Этапы графического конвейера** присутствуют этапы **Сборщик входных данных** и  **Шейдер вершин** , но не этап **Шейдер пикселей** для одного из вызовов Draw.  
  
    > [!NOTE]
    >  Если другие этапы конвейера — например, этапы шейдера поверхности, шейдера доменов или шейдера геометрии — обрабатывают объект, любой из них быть причиной проблемы. Обычно проблема связана с самым ранним этапом, в котором результат не отображается или отображается непредвиденным образом.  
  
4.  Остановитесь, когда достигнете вызова Draw, соответствующего отсутствующему объекту. В этом сценарии в окне **Этапы графического конвейера** видно, что геометрия была передана GPU (о чем говорит наличие этапа **Сборщик входных данных** ) и преобразована (о чем говорит наличие этапа **Шейдер вершин** ), однако она не отображается в целевом объекте отрисовки, поскольку нет активного шейдера пикселей (об этом говори отсутствие этапа **Шейдер пикселей** ). В этом сценарии можно даже видеть силуэт отсутствующего объекта на этапе **Средство слияния вывода** :  
  
     ![Событие DrawIndexed и его влияние на конвейере](../debugger/media/gfx-diag-demo-misconfigured-pipeline-step-2.png "gfx_diag_demo_misconfigured_pipeline_step_2")  
  
 После того как вы убедитесь, что приложение выполнило вызов рисования для геометрии отсутствующего объекта, и обнаружите, что этап шейдера пикселей был неактивен, вы можете проверить состояние устройства, чтобы подтвердить свои выводы. Для просмотра контекста устройства и других данных объектов Direct3D можно пользоваться окном **Таблица графических объектов** .  
  
#### <a name="to-examine-device-context"></a>Проверка контекста устройства  
  
1.  Откройте **контекст устройства d3d11**. В окне **Этапы графического конвейера** выберите ссылку **ID3D11DeviceContext** в составе вызова `DrawIndexed` , который отображается в верхней части окна.  
  
2.  Проверьте состояние устройства, которое отображается на вкладке **контекст устройства d3d11** , чтобы убедиться, что во время вызова рисования не было активного шейдера пикселей. В этом сценарии **общая информация о шейдере**— отображаемая под **состоянием шейдера пикселей**— показывает, что шейдер равен **NULL**:  
  
     ![Контекст устройства D3D 11 показывает состояние шейдера пикселей](../debugger/media/gfx-diag-demo-misconfigured-pipeline-step-4.png "gfx_diag_demo_misconfigured_pipeline_step_4")  
  
 После того как вы убедились, что приложение установило шейдер пикселей равным NULL в приложении, следующий шаг — найти место в исходном коде приложения, где задается шейдер пикселей. Найти это место можно с помощью окон **Список событий графики** и **Стек вызовов событий графики** .  
  
#### <a name="to-find-where-the-pixel-shader-is-set-in-your-apps-source-code"></a>Поиск места задания шейдера пикселей в исходном коде приложения  
  
1.  Найдите вызов `PSSetShader` , соответствующий отсутствующему объекту. В окне **Список событий графики** введите "Draw;PSSetShader" в поле **Поиск** , которое находится в правом верхнем углу окна **Список событий графики** . Список будет отфильтрован и будет содержать только события "PSSetShader" и события, в названиях которых присутствует слово "Draw". Выберите первый вызов `PSSetShader` , который идет перед вызовом рисования отсутствующего объекта.  
  
    > [!NOTE]
    >  `PSSetShader` не будет присутствовать в окне **Список событий графики** , если он не был задан в ходе этого кадра. Обычно это происходит, только если только один шейдер пикселей используется для всех объектов, или если вызов `PSSetShader` случайно был пропущен в ходе этого кадра. В любом случае рекомендуется выполнить поиск вызовов `PSSetShader` в исходном коде приложения и с помощью традиционных приемов отладки проанализировать поведение этих вызовов.  
  
2.  Откройте окно **Стек вызовов событий графики** . На панели инструментов **Диагностика графики** выберите **Стек вызовов событий графики**.  
  
3.  С помощью стека вызовов найдите вызов `PSSetShader` в исходном коде приложения. В окне **Стек вызовов событий графики** выберите самый верхний вызов и проверьте значение, равным которому задается шейдер пикселей. Шейдер пикселей может непосредственно быть установлен в NULL либо значение NULL может возникнуть из-за аргумента, переданного в функцию, или другого состояния. Если он не задан непосредственно, возможно, обнаружить источник значения NULL удастся где-либо выше по стеку вызовов. В этом сценарии вы обнаружите, что построитель текстуры непосредственно задан равным `nullptr` в самой верхней функции, которая называется `CubeRenderer::Render`:  
  
     ![Код, который не инициализирует шейдер пикселей](../debugger/media/gfx-diag-demo-misconfigured-pipeline-step-5.png "gfx_diag_demo_misconfigured_pipeline_step_5")  
  
    > [!NOTE]
    >  Если источник значения NULL не удается обнаружить, просто просмотрев стек вызовов, рекомендуется установить условную точку останова в вызове `PSSetShader` , чтобы приостановить выполнение программы при установке шейдера пикселей в NULL. Затем перезапустите приложение в режиме отладки и с помощью традиционных приемов отладки найдите источник значения NULL.  
  
 Чтобы устранить проблему, присвойте правильный шейдер пикселей, используя первый параметр вызова API `ID3D11DeviceContext::PSSetShader` .  
  
 ![Исправленный C&#43; &#43; исходный код](../debugger/media/gfx-diag-demo-misconfigured-pipeline-step-6.png "gfx_diag_demo_misconfigured_pipeline_step_6")  
  
 Внеся исправления в код, можно заново собрать его и еще раз запустить приложение, чтобы убедиться, что проблема с отрисовкой решена:  
  
 ![Теперь объект появился](../debugger/media/gfx-diag-demo-misconfigured-pipeline-resolution.jpg "gfx_diag_demo_misconfigured_pipeline_resolution")


