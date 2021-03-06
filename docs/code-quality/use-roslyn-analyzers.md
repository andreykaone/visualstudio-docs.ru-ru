---
title: Тяжесть и подавление правила анализатора
ms.date: 03/04/2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 67fd157ad4db24acbc1676ea0a9a1d79e9eb34f9
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431414"
---
# <a name="use-code-analyzers"></a>Использование анализаторов кода

Анализатор кода .NET Compiler Platform ("Рослин") анализирует ваш код C- или Visual Basic при вводе. Каждая *диагностика* или правило имеет состояние тяжести и подавления по умолчанию, которое может быть перезаписано для вашего проекта. Эта статья охватывает строгость правил, использование наборов правил и устранение нарушений.

## <a name="analyzers-in-solution-explorer"></a>Анализаторы в исследователе решений

Вы можете сделать большую часть настройки анализатор диагностики от **Solution Explorer**. При [установке анализаторов](../code-quality/install-roslyn-analyzers.md) в пакет NuGet узло **анализаторов** появляется под узлом **Ссылки** или **Зависимостей** в **Solution Explorer.** Если расширить **анализаторы,** а затем расширить одну из сборок анализатора, вы увидите все диагностики в сборке.

![Узла анализаторов в Solution Explorer](media/analyzers-expanded-in-solution-explorer.png)

Свойства диагностики, включая ее описание и серьезность по умолчанию, можно просмотреть в окне **Свойств.** Чтобы просмотреть свойства, нажмите правой кнопкой мыши на правило и выберите **Свойства**, или выберите правило, а затем нажмите **Alt**+**Enter**.

![Диагностические свойства в окне свойств](media/analyzer-diagnostic-properties.png)

Чтобы просмотреть онлайн-документацию для диагностики, нажмите право йнагнуть на диагностику и выберите **Помощь просмотра.**

Значки рядом с каждой диагностикой в **Solution Explorer** соответствуют значям, которые вы видите в установленном правиле при открытии в редакторе:

- "x" в круге указывает на [серьезность](#rule-severity) **ошибки**
- "!" в треугольнике указывает на [тяжесть](#rule-severity) **Предупреждения**
- "i" в круге указывает на [серьезность](#rule-severity) **информации**
- "i" в круге на светлом фоне указывает на [тяжесть](#rule-severity) **скрытых**
- нисходящая стрелка в круге указывает на то, что диагностика подавляется

![Значки диагностики в Solution Explorer](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>Важность правил

::: moniker range=">=vs-2019"

Вы можете настроить серьезность правил анализатора, или *диагностики,* если вы [установите анализаторы](../code-quality/install-roslyn-analyzers.md) в виде пакета NuGet. Начиная с визуальной студии 2019 версия 16.3, вы можете настроить серьезность правила [в файле EditorConfig](#set-rule-severity-in-an-editorconfig-file). Вы также можете изменить серьезность правила [из Solution Explorer](#set-rule-severity-from-solution-explorer) или в [файле набора правил.](#set-rule-severity-in-the-rule-set-file)

::: moniker-end

::: moniker range="vs-2017"

Вы можете настроить серьезность правил анализатора, или *диагностики,* если вы [установите анализаторы](../code-quality/install-roslyn-analyzers.md) в виде пакета NuGet. Можно изменить серьезность правила [из Solution Explorer](#set-rule-severity-from-solution-explorer) или в [файле набора правил.](#set-rule-severity-in-the-rule-set-file)

::: moniker-end

В следующей таблице показаны различные параметры серьезности:

| Тяжесть (Исследователь решений) | Тяжесть (файл EditorConfig) | Поведение времени сборки | Поведение редактора |
|-|-|-|
| Error | `error` | Нарушения отображаются как *Ошибки* в списке ошибок и в выводах сборки командной строки, и вызывают сбой в сборках.| Оскорбительный код подчеркивается красным завихрением и отмечен небольшой красной коробкой в панели прокрутки. |
| Предупреждение | `warning` | Нарушения отображаются как *Предупреждения* в списке ошибок и в выводах сборки командной строки, но не приводят к сбою в сборках. | Оскорбительный код подчеркивается зеленым завихрением и отмечен небольшой зеленой коробкой в панели прокрутки. |
| Сведения | `suggestion` | Нарушения отображаются как *Сообщения* в списке ошибок, а вовсе не в выводах сборки командной строки. | Оскорбительный код подчеркивается серым завихрением и отмечен небольшой серой коробкой в панели прокрутки. |
| Скрытый | `silent` | Невидимая для пользователя. | Невидимая для пользователя. Однако о диагностике сообщается диагностическому механизму IDE. |
| None | `none` | Подавлен полностью. | Подавлен полностью. |
| По умолчанию | `default` | Соответствует серьезности правила по умолчанию. Чтобы определить значение по умолчанию для правила, посмотрите в окне свойств свойств. | Соответствует серьезности правила по умолчанию. |

На следующем скриншоте редактора кода показаны три различных нарушения с различными нарушениями. Обратите внимание на цвет squiggle и небольшой, цветной квадрат в прокрутке бар справа.

![Ошибка, предупреждение и нарушение информации в редакторе кода](media/diagnostics-severity-colors.png)

На следующем скриншоте показаны те же три нарушения, что и в списке ошибок:

![Ошибка, предупреждение и нарушение информации в списке ошибок](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>Установите серьезность правил в файле EditorConfig

(Visual Studio 2019 версия 16.3 и более поздний)

Вы можете установить серьезность предупреждений или правил анализатора в файле EditorConfig со следующим синтаксисом:

`dotnet_diagnostic.<rule ID>.severity = <severity>`

Установка серьезности правила в файле EditorConfig имеет приоритет над любой серьезностью, установленной в наборе правил или в Solution Explorer. Вы можете [вручную](#manually-configure-rule-severity) настроить серьезность в файле EditorConfig или [автоматически](#automatically-configure-rule-severity) через лампочку, которая появляется рядом с нарушением.

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>Установите серьезность правил нескольких правил анализатора сразу в файле EditorConfig

(Visual Studio 2019 версия 16.5 и более поздний)

Вы можете установить серьезность для определенной категории правил анализатора или для всех правил анализатора с одной записью в файле EditorConfig.

- Установите серьезность правил для категории правил анализатора:

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- Установите серьезность правил для всех правил анализатора:

`dotnet_analyzer_diagnostic.severity = <severity>`

Если у вас есть несколько записей, которые применимы к определенному идентификатору правила, следующий порядок приоритета, чтобы выбрать применимую запись:

- Ввод severity для индивидуального правила ID имеет приоритет над входом серьезности для категории.
- Степень серьезности для категории имеет приоритет над входом в категорию строгости для всех правил анализатора.

Рассмотрим следующий пример EditorConfig, где [CA1822](https://docs.microsoft.com/visualstudio/code-quality/ca1822) имеет категорию "Производительность":

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

В предыдущем примере все три записи применимы к CA1822. Однако, используя указанные правила приоритета, первое правило ID на основе серьезности запись выигрывает над следующей записи. В этом примере CA1822 будет иметь эффективную тяжесть "ошибки". Все остальные правила с категорией "Производительность" будут иметь серьезность "предупреждение". Все оставшиеся правила анализатора, которые не имеют категории "Производительность", будут иметь серьезное "предложение".

#### <a name="manually-configure-rule-severity"></a>Ручная настройка серьезности правил

1. Если у вас еще нет файла EditorConfig для вашего проекта, [добавьте один](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)файл.

2. Добавьте запись для каждого правила, который вы хотите настроить под соответствующим расширением файла. Например, чтобы установить степень серьезности `error` для [CA1822](ca1822.md) для файлов C,» запись выглядит следующим образом:

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> Для анализаторов в стиле кода IDE можно также настроить их в файл EditorConfig, например, `dotnet_style_qualification_for_field = false:suggestion`с помощью другого синтаксиса. Однако, если вы установите тяжесть с помощью `dotnet_diagnostic` синтаксиса, он имеет приоритет. Для получения дополнительной [информации см.](../ide/editorconfig-language-conventions.md)

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>Преобразование существующего файла «Правила» в файл EditorConfig

Начиная с версии Visual Studio 2019 16.5, файлы сустановленными правилами унижаются в пользу файла EditorConfig для конфигурации анализатора для управляемого кода. Большая часть инструментария Visual Studio для конфигурации серьезности правил анализатора была обновлена для работы с файлами EditorConfig вместо файлов с установленными правилами. Файлы EditorConfig позволяют настроить как ограничения правил анализатора, так и параметры анализа, включая параметры стиля кода Visual Studio IDE. Настоятельно рекомендуется преобразовать существующий файл с установленным набором правил в файл EditorConfig. Также рекомендуется сохранить файл EditorConfig в корне репо или в папке решения. Используя корень папки репо или решения, вы убедитесь, что параметры серьезности из этого файла автоматически применяются ко всему репо или решению, соответственно.

Существует несколько способов преобразования существующего файла наборов правил в файл EditorConfig:

- От редактора Ruleset в Визуальной студии (требует Visual Studio 2019 16.5 или более поздней). Если ваш проект уже использует определенный `CodeAnalysisRuleSet`файл наборов правил в качестве своего, вы можете преобразовать его в эквивалентный файл EditorConfig из редактора Ruleset в Visual Studio.

    1. Дважды щелкните файл сустановленным действием правил в Solution Explorer.

       Файл «Правила» должен быть открыт в редакторе «Правила». Вы должны увидеть кликабельный **infobar** в верхней части редактора наборов правил.

       ![Преобразование установки правил в файл EditorConfig в редакторе Ruleset](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. **Нажмите** на ссылку infobar.

       Это должно открыть диалог **Save As,** который позволяет выбрать каталог, где вы хотите создать файл EditorConfig.

    3. **Нажмите** кнопку **Сохранить** для создания файла EditorConfig.

       Генерируемый EditorConfig должен открыться в редакторе. Кроме того, свойство `CodeAnalysisRuleSet` MSBuild обновляется в файле проекта, чтобы больше не ссылаться на исходный файл набора правил.

- Из командной строки.

    1. Установите пакет NuGet [Microsoft.CodeAnalysis.RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter).

    2. Выполните `RulesetToEditorconfigConverter.exe` из установленного пакета, с путями к файлу ruleset и файлом EditorConfig в качестве аргументов командной строки.

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

Вот пример файла наборов правил для преобразования:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules for ConsoleApp" Description="Code analysis rules for ConsoleApp.csproj." ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1821" Action="Warning" />
    <Rule Id="CA2213" Action="Warning" />
    <Rule Id="CA2231" Action="Warning" />
  </Rules>
</RuleSet>
```

Вот преобразованный файл EditorConfig:

```ini
# NOTE: Requires **VS2019 16.3** or later

# Rules for ConsoleApp
# Description: Code analysis rules for ConsoleApp.csproj.

# Code files
[*.{cs,vb}]


dotnet_diagnostic.CA1001.severity = warning

dotnet_diagnostic.CA1821.severity = warning

dotnet_diagnostic.CA2213.severity = warning

dotnet_diagnostic.CA2231.severity = warning
```

#### <a name="automatically-configure-rule-severity"></a>Автоматики серьезности правил

##### <a name="configure-from-light-bulb-menu"></a>Настройка из меню лампочки

Visual Studio предоставляет удобный способ настроить серьезность правила из меню лампочки [Быстрые действия.](../ide/quick-actions.md)

1. После нарушения происходит, нависте над нарушением squiggle в редакторе и открыть меню лампочки. Или, положите курсор на линию и нажмите **Ctrl**+**.** (точка).

2. Из меню лампочки выберите **Настройка или Подавите проблем** > **ы настройка идентификатора \<правила> тяжести.**

   ![Настроить серьезность правил из меню лампочки в Visual Studio](media/configure-rule-severity.png)

3. Оттуда выберите один из вариантов серьезности.

   ![Настройка серьезности правил как предложение](media/configure-rule-severity-suggestion.png)

   Visual Studio добавляет запись в файл EditorConfig, чтобы настроить правило на запрашиваемый уровень, как показано в поле предварительного просмотра.

   > [!TIP]
   > Если у вас еще нет файла EditorConfig в проекте, Visual Studio создает его для вас.

##### <a name="configure-from-error-list"></a>Настройка из списка ошибок

Visual Studio также предоставляет удобный способ настройки серьезности правила из меню контекста списка ошибок.

1. После нарушения нажмите на диагностическую запись в списке ошибок.

2. Из контекстного меню выберите **степень серьезности**набора.

   ![Настройка серьезности правил из списка ошибок в Visual Studio](media/configure-rule-severity-error-list.png)

3. Оттуда выберите один из вариантов серьезности.

   Visual Studio добавляет запись в файл EditorConfig, чтобы настроить правило на запрашиваемый уровень.

   > [!TIP]
   > Если у вас еще нет файла EditorConfig в проекте, Visual Studio создает его для вас.

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>Установите серьезность правил от Solution Explorer

1. В Solution Explorer расширьте > **анализаторы** **ссылок**(или**анализаторы** **зависимостей** > для проектов .NET Core).

2. Расширьте сборку, содержащую правило, для которого необходимо установить степень серьезности.

::: moniker range=">=vs-2019"
3. Нажмите правой кнопкой мыши правило и выберите **Установить серьезность**. В контекстном меню выберите один из вариантов серьезности.

   Visual Studio добавляет запись в файл EditorConfig, чтобы настроить правило на запрашиваемый уровень. Если проект использует файл с установленным правилами вместо файла EditorConfig, в файл набора правил добавляется запись серьезности.

   > [!TIP]
   > Если в проекте у вас еще нет файла EditorConfig или файла с установленным правилами, Visual Studio создает для вас новый файл EditorConfig.
::: moniker-end

::: moniker range="vs-2017"
3. Право нажмите правило и выберите **Set Rule Set Severity**. В контекстном меню выберите один из вариантов серьезности.

   Степень серьезности для правила сохраняется в файле набора активных правил.
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>Установите серьезность правил в файле набора правил

![Файл набора правил в исследователе решений](media/ruleset-in-solution-explorer.png)

1. Откройте файл набора активных правил, дважды нажав его в **Solution Explorer,** выбрав **Open Active Rule Set** в меню узла **анализарно-аналитического** > **Analyzers** управления ссылок Ссылок или выбрав **Страницу** свойства **анализа кода** для проекта.

   Если это первый раз, когда вы редактируете набор правил, Visual Studio делает копию файла набора правил по умолчанию, называет * \<его имя проекта>.ruleset*и добавляет его в ваш проект. Этот набор пользовательских правил также становится активным набором правил для вашего проекта.

   > [!NOTE]
   > Проекты .NET Core и .NET Standard не поддерживают команды меню для наборов правил в **Solution Explorer,** например, **Open Active Rule Set.** Чтобы указать правило без обязательств, установленное для проекта .NET Core или .NET Standard, вручную [добавьте свойство **CodeAnalysisRuleSet** ](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) в файл проекта. Вы все еще можете настроить правила в рамках правила, установленного в uI набора правил Visual Studio.

1. Просмотрите правило, расширив его содержащую сборку.

1. В столбце **«Действие»** выберите значение, чтобы открыть список выпадающих и выберите нужную степень серьезности из списка.

   ![Файл набора правил открыт в редакторе](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>Подавление нарушений

Существует несколько способов подавления нарушений правил:

::: moniker range=">=vs-2019"

- В **файле EditorConfig**

  Установите `none`тяжесть, например, `dotnet_diagnostic.CA1822.severity = none`.

- Из меню **Анализ**

  Выберите **анализ** > **сборки и подавить активные проблемы** в панели меню, чтобы подавить все текущие нарушения. Иногда это называют "базовым".

::: moniker-end

::: moniker range="vs-2017"

- Из меню **Анализ**

  Выберите **анализ** > **кода запуска и подавление активных проблем** в панели меню, чтобы подавить все текущие нарушения. Иногда это называют "базовым".

::: moniker-end

- От **исследователя решений**

  Установите серьезность правила **нет**.

- Из **редактора набора правил**

  Отоверьте поле рядом с его именем или **установите Действие** **нет.**

- От **редактора кода**

  Поместите курсор в строку кода с нарушением и нажмите **Ctrl**+**Period (.),** чтобы открыть меню **Быстрых Действий.** Выберите **Suppress CAXXXX** > **в файле Исходного/Подавления.**

  ![Подавление диагностики из меню быстрых действий](media/suppress-diagnostic-from-editor.png)

- Из **списка ошибок**

  Выберите правила, которые вы хотите подавить, а затем нажмите правой кнопкой мыши и выберите **Suppress** > **In Source/In Suppression File.**

  - При подавлении **в источнике**диалог **предварительных изменений** открывается и показывает предварительный просмотр [предупреждения #pragma](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) или визуальной базовой [директивы #Disable,](/dotnet/visual-basic/language-reference/directives/directives) добавленной в исходный код.

    ![Предварительный просмотр добавления предупреждения #pragma в файл кода](media/pragma-warning-preview.png)

  - При выборе **файла подавления**диалог **предварительных изменений** открывается <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> и показывает предварительный просмотр атрибута, добавленного в файл глобальных подавления.

    ![Предварительный просмотр добавления атрибута SuppressMessage в файл подавления](media/preview-changes-in-suppression-file.png)

  В диалоге **предварительных изменений** выберите **Apply**.

  > [!NOTE]
  > Если вы не видите опцию **меню Подавки** в **Solution Explorer,** нарушение, скорее всего, исходит от сборки, а не анализа в реальном времени. **Список ошибок** отображает диагностику или нарушения правил как из анализа кода в реальном времени, так и из сборки. Поскольку диагностика сборки может быть устаревшей, например, если вы отредактировали код для устранения нарушения, но не перестроили, вы не можете подавить эти диагнозы из **списка ошибок.** Диагностика из живого анализа, или IntelliSense, всегда актуальна с текущими источниками и может быть подавлена из **списка ошибок.** Чтобы исключить диагностику *сборки* из выбора, переключите фильтр исходного списка **ошибок** с **build и IntelliSense** на **IntelliSense.** Затем выберите диагностику, которую вы хотите подавить, и приступить, как описано ранее.
  >
  > ![Фильтр источника списка ошибок в Visual Studio](media/error-list-filter.png)

## <a name="command-line-usage"></a>Использование командной строки

При построении проекта на командной строке в выходе сборки, если выполнены следующие условия, появляются нарушения правил:

- Анализаторы устанавливаются как пакет NuGet, а не как расширение VSIX.

- В коде проекта нарушается одно или несколько правил.

- [Тяжесть](#rule-severity) нарушенного правила устанавливается либо **предупреждение,** в этом случае нарушения не вызывают сборки к сбою, или **ошибка**, в этом случае нарушения вызывают сборку к сбою.

Многословность вывода сборки не влияет на то, показаны ли нарушения правил. Даже при **тихой** многословности нарушения правил появляются в выходе сборки.

> [!TIP]
> Если вы привыкли к запуску анализа наследия из командной строки, либо с *Помощью FxCopCmd.exe,* либо через msbuild с флагом **RunCodeAnalysis,** вот как это сделать с анализаторами кода.

Чтобы увидеть нарушения анализатора на командной строке при построении проекта с помощью msbuild, запустите команду следующим образом:

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

На следующем изображении показаны выходные данные сборки из командной строки для создания проекта, содержащего нарушение правила анализа:

![Выходные данные MSBuild с нарушением правила](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>Зависимые проекты

В проекте .NET Core, если вы добавляете ссылку на проект с анализаторами NuGet, эти анализаторы автоматически добавляются и в зависимый проект. Чтобы отключить это поведение, например, если зависимый проект является проектом модульного тестирования, отметьте пакет NuGet как частный в файле *.csproj* или *.vbproj* эталонного проекта, установив атрибут **PrivateAssets:**

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>См. также раздел

- [Обзор анализаторов кода в Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [Отправить ошибку анализатора кода](https://github.com/dotnet/roslyn-analyzers/issues)
- [Использование наборов правил](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [Подавление предупреждений об анализе кода](../code-quality/in-source-suppression-overview.md)
