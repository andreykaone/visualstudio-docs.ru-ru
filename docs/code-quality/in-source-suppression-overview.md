---
title: Подавлять предупреждения анализа кода
ms.date: 12/01/2018
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 67bb0d7ca38d4312dc2a1f1e7a8f50d0102a328a
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78408718"
---
# <a name="suppress-code-analysis-warnings"></a>Подавлять предупреждения анализа кода

Часто бывает полезно указать, что предупреждение неприменимо. Это указывает членам команды, что код был проверен, и что предупреждение можно подавлять. Подавление в исходном источнике (ISS) использует атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> для подавления предупреждения. Атрибут можно поместить ближе к сегменту кода, вызвавшему предупреждение. Можно добавить атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> в исходный файл, введя его в, или можно использовать контекстное меню для предупреждения в **Список ошибок** , чтобы добавить его автоматически.

Атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> является условным атрибутом, включенным в метаданные IL сборки управляемого кода, только если во время компиляции определен символ компиляции CODE_ANALYSIS.

В C++/CLI используйте ЦС макросов\_отключить\_сообщение или ЦС\_глобальный\_SUPPRESS_MESSAGE в файле заголовка, чтобы добавить атрибут.

> [!NOTE]
> Не следует использовать подавления в исходном виде в сборках выпуска, чтобы предотвратить случайное пересылку метаданных подавления в исходном источнике. Кроме того, из-за затрат на обработку подавления в исходном коде производительность приложения может снизиться.

::: moniker range="vs-2017"

> [!NOTE]
> Если вы переносите проект в Visual Studio 2017, вы можете внезапно столкнуться с большим количеством предупреждений анализа кода. Если вы не готовы устранить предупреждения, их можно отключить, выбрав **анализ** > **запустить анализ кода и отключить активные проблемы**.
>
> ![Выполнение анализа кода и отключение проблем в Visual Studio](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> Если вы переносите проект в Visual Studio 2019, вы можете внезапно столкнуться с большим количеством предупреждений анализа кода. Если вы не готовы устранить предупреждения, их можно отключить, выбрав **анализ** > **Сборка и подавлять активные проблемы**.

::: moniker-end

## <a name="suppressmessage-attribute"></a>SuppressMessage - атрибут

При нажатии кнопки **подавлять** в контекстном меню или щелчке правой кнопкой мыши предупреждения анализа кода в **Список ошибок**атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> добавляется либо в код, либо в глобальный файл подавления проекта.

Атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> имеет следующий формат:

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

К свойствам атрибута относятся:

- **Category** — Категория, в которой определено правило. Дополнительные сведения о категориях правил анализа кода см. в разделе [предупреждения управляемого кода](../code-quality/code-analysis-for-managed-code-warnings.md).

- **CheckId** — идентификатор правила. Поддержка включает короткое и длинное имя для идентификатора правила. Короткое имя — КАКСКСКСКС; длинное имя — КАКСКСКСКС: Фриендлитипенаме.

- **Обоснование** — текст, который используется для документирования причины подавления сообщения.

- **MessageId** — уникальный идентификатор проблемы для каждого сообщения.

- **Scope** — целевой объект, в котором предупреждение подавляется. Если целевой объект не указан, ему присваивается значение целевого объекта атрибута. В число поддерживаемых [областей](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) входят следующие.

  - [`module`](#module-suppression-scope) — эта область подавляет предупреждения для сборки. Это глобальное подавление, которое применяется ко всему проекту.

  - `resource`-(только для[устаревших FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md) ). Эта область подавляет предупреждения в диагностических сведениях, записываемых в файлы ресурсов, которые являются частью модуля (сборки). Эта область не считывается и не учитывается C#в компиляторах/VB для диагностики анализатора Roslyn, которая анализирует только исходные файлы.

  - `type` — эта область подавляет предупреждения для типа.

  - `member` — эта область подавляет предупреждения для члена.

  - `namespace` — эта область подавляет предупреждения относительно пространства имен. Он не отключает предупреждения для типов в пространстве имен.

  - `namespaceanddescendants`-(требуется компилятор версии 3. x или выше и Visual Studio 2019) Эта область подавляет предупреждения в пространстве имен и всех его потомках. Значение `namespaceanddescendants` игнорируется устаревшим анализом.

- **Target** — идентификатор, который используется для указания целевого объекта, в котором предупреждение подавляется. Он должен содержать полное имя элемента.

При появлении предупреждений в Visual Studio можно просмотреть примеры `SuppressMessage`, [добавив подавление в файл глобального подавления](../code-quality/use-roslyn-analyzers.md#suppress-violations). Атрибут подавления и его обязательные свойства отображаются в окне предварительного просмотра.

## <a name="suppressmessage-usage"></a>Использование SuppressMessage

Предупреждения анализа кода подавляются на уровне, к которому применяется атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>. Например, атрибут можно применить на уровне сборки, модуля, типа, члена или параметра. Целью этого является тесное связывание информации о подавлении с кодом, в котором происходит нарушение.

Общая форма подавления включает категорию правила и идентификатор правила, который содержит необязательное удобное для восприятия представление имени правила. Например:

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

При наличии достаточной производительности для минимизации метаданных подавления в исходном виде имя правила можно опустить. Категория правила и идентификатор его правила вместе составляют достаточно уникальный идентификатор правила. Например:

`[SuppressMessage("Microsoft.Design", "CA1039")]`

В целях удобства обслуживания не рекомендуется указывать имя правила.

## <a name="suppress-selective-violations-within-a-method-body"></a>Подавлять выборочные нарушения внутри тела метода

К методу могут применяться атрибуты подавления, но они не могут быть внедрены в тело метода. Это означает, что все нарушения конкретного правила подавляются, если добавить к методу атрибут <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>.

В некоторых случаях может потребоваться отключить определенный экземпляр нарушения, например таким образом, чтобы будущий код не выводился автоматически из правила анализа кода. Некоторые правила анализа кода позволяют сделать это с помощью свойства `MessageId` атрибута <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>. В общем случае устаревшие правила для нарушений в конкретном символе (локальная переменная или параметр) учитывают свойство `MessageId`. [CA1500: вариабленамесшаулднотматчфиелднамес](../code-quality/ca1500.md) — это пример такого правила. Однако устаревшие правила нарушения работы исполняемого кода (не символа) не учитывают свойство `MessageId`. Кроме того, .NET Compiler Platform ("Roslyn") анализаторы не учитывают свойство `MessageId`.

Чтобы отключить определенное нарушение правил, укажите имя символа для свойства `MessageId` атрибута <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>. В следующем примере показан код с двумя нарушениями [CA1500: вариабленамесшаулднотматчфиелднамес](../code-quality/ca1500.md)&mdash;один для `name` переменной и один для `age` переменной. Подавляется только нарушение `age` символа.

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

## <a name="global-level-suppressions"></a>Подавления на глобальном уровне

Средство анализа управляемого кода проверяет `SuppressMessage` атрибуты, которые применяются на уровне сборки, модуля, типа, члена или параметра. Он также вызывает нарушения для ресурсов и пространств имен. Эти нарушения должны применяться на глобальном уровне, а их область и Целевая. Например, следующее сообщение подавляет нарушение пространства имен:

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> При подавлении предупреждения с `namespace`ной областью предупреждение подавляется по самому пространству имен. Предупреждение не подавляется по типам в пространстве имен.

Все подавления можно выразить, указав явную область. Эти подавления должны находиться на глобальном уровне. Подавление на уровне члена нельзя указать путем оформления типа.

Запреты глобального уровня — это единственный способ отключить сообщения, ссылающиеся на созданный компилятором код, который не сопоставлен с явно предоставленным источником пользователя. Например, следующий код подавляет нарушение в конструкторе, созданном компилятором:

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` всегда содержит полное имя элемента.

### <a name="global-suppression-file"></a>Файл глобального подавления

В глобальном файле подавления хранятся подавленные подавления или подавления на глобальном уровне, не указывающие цель. Например, подавление для нарушений уровня сборки хранится в этом файле. Кроме того, некоторые подавления ASP.NET хранятся в этом файле, так как параметры уровня проекта недоступны для кода, который находится под формой. Файл глобального подавления создается и добавляется в проект при первом выборе параметра **в файле подавления проекта** команды **подавлять** в окне **Список ошибок** .

### <a name="module-suppression-scope"></a>Область подавления модуля

Нарушения качества кода для всей сборки можно отключить с помощью области **модуля** .

Например, следующий атрибут в файле проекта _глобалсуппрессионс_ будет подавлять нарушение ConfigureAwait для проекта ASP.NET Core:

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

## <a name="generated-code"></a>Созданный код

Компиляторы управляемого кода и некоторые сторонние средства создают код для упрощения разработки кода. Созданный компилятором код, который отображается в исходных файлах, обычно отмечается атрибутом `GeneratedCodeAttribute`.

Для анализа исходного кода (FxCop Analyzer) можно подавлять сообщения в созданном коде с помощью файла [. editorconfig](../code-quality/configure-fxcop-analyzers.md) в корне проекта или решения. Используйте шаблон файла для сопоставления с созданным кодом. Например, чтобы исключить предупреждения CS1591 в файлах * *. Designer.CS* , используйте его в файле конфигурации.

``` cmd
[*.designer.cs]
dotnet_diagnostic.CS1591.severity = none
```

Для традиционного анализа кода можно выбрать, следует ли подавлять предупреждения и ошибки анализа кода для созданного кода. Сведения о подавлении таких предупреждений и ошибок см. [в разделе как отключить предупреждения для созданного кода](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md).

> [!NOTE]
> Анализ кода игнорирует `GeneratedCodeAttribute`, когда он применяется к целой сборке или одному параметру.

## <a name="see-also"></a>См. также:

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [Использование анализаторов кода](../code-quality/use-roslyn-analyzers.md)
