---
title: Поиск изменений кода и других журналов с помощью CodeLens | Документы Майкрософт
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: f697d7b4-704e-4cac-b13a-bc57d2ff8318
caps.latest.revision: 134
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8876a0a3c2b978443ee4bc74097dbc9fdd410b8b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656001"
---
# <a name="find-code-changes-and-other-history-with-codelens"></a>Поиск изменений кода и других журналов с помощью CodeLens
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Получайте дополнительные сведения о коде, не отрываясь от работы и не выходя из редактора. Находите ссылки на код, изменения кода, связанные ошибки, рабочие элементы, проверки кода и модульные тесты.

> [!NOTE]
> Средство CodeLens доступно только в выпусках Visual Studio Enterprise и Visual Studio Professional. Оно не доступно в выпуске Visual Studio Community.

 Посмотрите, где и как отдельные части вашего кода используются в решении.

 ![Индикаторы CodeLens в редакторе кода](../ide/media/codelensoverview.png "коделенсовервиев")

 Сообщите рабочей группе об изменениях в коде, не выходя из редактора.

 ![CodeLens &#45; . обратитесь к команде](../ide/media/codelensovervew2.png "CodeLensOvervew2")

 Чтобы выбрать, какие индикаторы должны отображаться, включить или выключить средство CodeLens, последовательно выберите пункты **Инструменты**, **Параметры**, **Текстовый редактор**, **Все языки**, **CodeLens**.

## <a name="FindReferences"></a> Поиск ссылок на код
 Требуется:

- Visual Studio Enterprise или Visual Studio Professional

- Код Visual C# .NET или Visual Basic .NET

  Выберите индикатор **ссылок** (**ALT + 2**). Если в результатах отображается **0 ссылок**, это значит, что ссылки из кода Visual C# или Visual Basic отсутствуют. Сюда не входят ссылки из других элементов, таких как XAML- и ASPX-файлы.

  ![Обозначение &#45; CodeLens выбор ссылок](../ide/media/codelensviewreferenceslist.png "коделенсвиевреференцеслист")

  Чтобы просмотреть код ссылки, наведите указатель мыши на ссылку.

  ![Ссылка &#45; для просмотра CodeLens](../ide/media/codelensviewreferencespeekreference.png "коделенсвиевреференцеспикреференце")

  Чтобы открыть файл, на который указывает ссылка, дважды щелкните эту ссылку.

  Чтобы просмотреть отношения между этим кодом и его ссылками, [создайте карту кода](../modeling/map-dependencies-across-your-solutions.md) и выберите параметр **Показать все ссылки** в контекстном меню карты кода.

  ![Ссылки &#45; CodeLens на карте кода](../ide/media/codelensmappedreferences.png "коделенсмаппедреференцес")

## <a name="FindCodeHistory"></a> Поиск журнала кода и связанных элементов
 Просмотрите журнал кода, чтобы узнать, что случилось. Можно также изучить изменения до их внедрения в ваш код, чтобы понять, как изменения в других ветвях могут повлиять на него.

 Требуется:

- Visual Studio Enterprise или Visual Studio Professional

- Team Foundation Server 2013 или более поздней версии, Visual Studio Team Services или Git

- [Lync 2010 или более поздней версии или Skype для бизнеса](https://technet.microsoft.com/lync)(для связи с коллегами, не выходя из редактора кода)

  Для кода на Visual C# .NET или Visual Basic .NET, который хранится вместе с системой управления версиями Team Foundation (TFVC) или Git, сведения CodeLens предоставляются на уровнях класса и метода (индикаторы*уровня кода элемента* ). Если репозиторий Git находится в TfGit, можно также получить ссылки на рабочие элементы TFS.

  ![Индикаторы уровня&#45;элементов кода](../ide/media/codelenselementlevelindicators.png "коделенселементлевелиндикаторс")

  Для всех других типов файлов, которые можно открыть в редакторе Visual Studio, сведения о CodeLens по всему файлу приводятся в одном месте — в нижней части окна (индикаторы*уровня файла* ).

  ![Индикаторы&#45;CodeLens на уровне файлов](../ide/media/almcodelensfilelevelindicators.png "алмкоделенсфилелевелиндикаторс")

  Чтобы выбрать индикатор с помощью клавиатуры, нажмите и удерживайте клавишу **ALT** для отображения назначенных клавиш с цифрами.

  ![Нажмите клавишу ALT, чтобы просмотреть номера доступа к клавиатуре](../ide/media/codelensaltkeyindicators.png "CodeLensAltKeyIndicators")

### <a name="find-changes-in-your-code"></a>Поиск изменений в коде
 Узнайте, кто изменил ваш код на C# или Visual Basic, и просмотрите внесенные в код изменения на индикаторах уровня кода элемента. При использовании системы управления версиями Team Foundation (TFVC) в Team Foundation Server или Visual Studio Team Services отображается следующее.

 ![CodeLens: получение журнала изменений для кода в TFVC](../ide/media/codelenscodechanges.png "коделенскодечанжес")

 Период времени по умолчанию — последние 12 месяцев. Если код хранится в Team Foundation Server, это ограничение можно изменить, выполнив [команду TFSConfig](https://msdn.microsoft.com/94424190-3b6b-4f33-a6b6-5807f4225b62) вместе с [командой CodeIndex](../ide/codeindex-command.md) и флагом **/indexHistoryPeriod** .

 Чтобы просмотреть подробный журнал всех изменений, включая сделанные более года назад, выберите параметр **Показать все изменения файла**.

 ![Показывать все изменения кода](../ide/media/codelensshowsallchanges.png "коделенсшовсаллчанжес")

 Откроется окно журнала с наборами изменений.

 ![Окно журнала для всех изменений кода](../ide/media/codelenscodechangeshistory.png "коделенскодечанжешистори")

 Если ваши файлы хранятся в репозитории Git и вы выбираете индикатор изменений на уровне элемента кода, отображается следующее:

 ![CodeLens: получение журнала изменений для кода в Git](../ide/media/codelenscodechangesgit.png "коделенскодечанжесгит")

 Просмотрите изменения для всего файла (кроме файлов C# и Visual Basic) на индикаторах уровня файла в нижней части окна.

 ![CodeLens: получение сведений о файле кода](../ide/media/codelensfilelevel.png "коделенсфилелевел")

 Чтобы получить дополнительные сведения об изменении, щелкните этот элемент правой кнопкой мыши. В зависимости от того, используется TFVC или Git, вам будут предложены варианты сравнения версий файла, просмотра сведений и отслеживания изменений, получения выбранной версии файла и уведомления автора об изменениях по электронной почте. Некоторые из этих сведений отображаются в Team Explorer.

 Также можно узнать, кто вносил изменения в код в течение определенного времени. Это поможет обнаружить закономерности во вносимых рабочей группой изменениях и оценить их влияние.

 ![CodeLens: Просмотр журнала изменений кода в виде графика](../ide/media/codelens.png "CodeLens")

#### <a name="find-changes-in-your-current-branch"></a>Поиск изменений в текущем подразделении
 Предположим, что ваша группа работает в нескольких подразделениях, основном и дочернем, для снижения риска нарушения стабильности кода:

 ![CodeLens: Поиск при создании ветви кода](../ide/media/codelensfirstbranchconceptual.png "коделенсфирстбранчконцептуал")

 Узнайте, сколько пользователей вносили изменения в код и сколько изменений было сделано в основном подразделении (**ALT + 6**):

 ![CodeLens: определение количества изменений в ветви](../ide/media/codelensbranchchanges.png "коделенсбранччанжес")

#### <a name="find-when-your-code-was-branched"></a>Поиск разветвления кода
 Перейдите к коду в дочернем подразделении, например Dev, как в этом примере. Выберите индикатор изменений (**ALT + 6**):

 ![CodeLens: Поиск при создании ветви кода](../ide/media/codelensfirstbranchscreenshot.png "коделенсфирстбранчскриншот")

#### <a name="find-incoming-changes-from-other-branches"></a>Поиск входящих изменений от других подразделений
 ![CodeLens: Поиск изменений в коде в других ветвях](../ide/media/codelensbranchchangecheckinconceptual.png "коделенсбранччанжечеккинконцептуал")

 …как это исправление ошибки в подразделении Dev:

 ![CodeLens: изменение возвращено в другую ветвь](../ide/media/codelensbranchchangedevscreenshot.png "коделенсбранччанжедевскриншот")

 Вы можете просмотреть это изменение, не покидая текущее подразделение (Main):

 ![CodeLens: Просмотр входящих изменений из другой ветви](../ide/media/codelensbranchchangemainscreenshot.png "коделенсбранччанжемаинскриншот")

#### <a name="find-when-changes-got-merged"></a>Поиск объединения изменений
 Вы можете увидеть, какие изменения были добавлены в ваше подразделение:

 ![Объединенные изменения CodeLens &#45; между ветвями](../ide/media/codelensbranchmergedconceptual.png "коделенсбранчмержедконцептуал")

 Например, код в подразделении Main теперь содержит исправление ошибки из подразделения Dev:

 ![Измененийи CodeLens &#45; , Объединенные между ветвями](../ide/media/codelensbranchmergedscreenshot.png "CodeLensBranchMergedScreenshot")

#### <a name="compare-an-incoming-change-with-your-local-version-shift--f10"></a>Сравните входящее изменение с локальной версией (SHIFT + F10).
 ![CodeLens: сравнение входящего изменения с локальным](../ide/media/codelensbranchincomingchangemenu.png "коделенсбранчинкомингчанжемену")

 Можно также дважды щелкнуть набор изменений.

#### <a name="what-do-the-icons-mean"></a>Что означают значки?

|**Значок**|**Откуда поступило изменение?**|
|--------------|-----------------------------------------|
|![Значок CodeLens: изменение с текущего ответвления](../ide/media/codelensbranchcurrenticon.png "коделенсбранчкуррентикон")|Текущее подразделение|
|![Изменение &#45; CodeLens от значка родительской ветви](../ide/media/codelensbranchparenticon.png "коделенсбранчпарентикон")|Родительское подразделение|
|![Значок CodeLens: изменение с дочерней ветви](../ide/media/codelensbranchchildicon.png "коделенсбранччилдикон")|Дочернее подразделение|
|![Значок &#45; изменения CodeLens на основе значка одноранговой ветви](../ide/media/codelensbranchpeericon.png "коделенсбранчпирикон")|Одноранговое подразделение|
|![Значок &#45; изменения CodeLens от ветви](../ide/media/codelensbranchfurtherawayicon.png "коделенсбранчфурсеравайикон")|Подразделение, отличное от родительского, дочернего или однорангового|
|![CodeLens: слияние из родительского значка](../ide/media/codelensbranchmergefromparenticon.png "коделенсбранчмержефромпарентикон")|Слияние с данными от родительского подразделения с дочерним подразделением|
|![CodeLens: значок слияния из дочерней ветви](../ide/media/codelensbranchmergefromchildicon.png "коделенсбранчмержефромчилдикон")|Слияние с данными от дочернего подразделения с родительским подразделением|
|![CodeLens: слияние из значка несвязанной ветви](../ide/media/codelensbranchmergefromunrelatedicon.png "коделенсбранчмержефромунрелатедикон")|Слияние с данными от несвязанного подразделения (слияние без базовой версии)|

### <a name="find-linked-work-items"></a>Поиск связанных рабочих элементов
 ![CodeLens &#45; Поиск рабочих элементов для конкретного кода](../ide/media/codelensworkitems.png "коделенсворкитемс")

### <a name="find-linked-code-reviews"></a>Поиск связанных проверок кода
 ![Запросы &#45; на проверку кода в представлении CodeLens](../ide/media/codelenscodereviews.png "коделенскодеревиевс")

### <a name="find-linked-bugs"></a>Поиск связанных ошибок
 ![CodeLens &#45; Поиск ошибок, связанных с наборами изменений](../ide/media/codelensbugschangesets.png "коделенсбугсчанжесетс")

### <a name="contact-the-owner-of-an-item"></a>Обращение к владельцу элемента
 ![Обращение к владельцу элемента](../ide/media/codelenscontactitemowner.png "коделенсконтактитемовнер")

 Откройте контекстное меню элемента, чтобы увидеть параметры контакта. Если на компьютере установлено приложение Lync или Skype для бизнеса, отобразятся следующие параметры:

 ![Параметры контактов для элемента](../ide/media/codelensitemcontactmenu.png "коделенситемконтактмену")

## <a name="FindRunUnitTests"></a> Поиск модульных тестов для кода
 Узнайте больше об имеющихся модульных тестах для кода, не открывая обозреватель тестов. Требуется:

- Visual Studio Enterprise или Visual Studio Professional

- Код Visual C# .NET или Visual Basic .NET

- [Проект модульного теста](../test/unit-test-your-code.md) с модульными тестами для кода приложения

1. Перейдите к коду приложения с модульными тестами.

2. Просмотрите тестовый охват для этого кода (**ALT + 3**).

     ![CodeLens &#45; выберите состояние тестирования в редакторе кода](../ide/media/codelenschoosetestindicator.png "коделенсчусетестиндикатор")

3. Если отображается значок предупреждения ![модульные тесты &#45; CodeLens еще не запущены](../ide/media/codelenstestwarningicon.png "коделенстестварнингикон"), запустите тесты.

     ![Модульные тесты представления CodeLens &#45; еще не запущены](../ide/media/codelenstestsnotyetrun.png "коделенстестснотетрун")

4. Чтобы просмотреть определение теста, откройте файл кода в редакторе, дважды щелкнув элемент теста в окне индикаторов CodeLens.

     ![CodeLens &#45; переход к определению модульного теста](../ide/media/codelensunittestdefinition.png "коделенсуниттестдефинитион")

5. Просмотрите результаты теста. Выберите индикатор состояния теста (![значок ошибки &#45; модульного теста codelens](../ide/media/codelenstestfailedicon.png "коделенстестфаиледикон") или ![значок &#45; пройденного теста единицы измерения codelens](../ide/media/codelenstestpassedicon.png "коделенстестпасседикон")) или нажмите клавиши **ALT + 1**.

     ![CodeLens &#45; см. в результатах модульного теста](../ide/media/codelensunittestresult.png "коделенсуниттестресулт")

6. Чтобы увидеть, сколько пользователей изменяло данный тест, кто именно изменял тест или сколько изменений было внесено в тест, [Поиск журнала кода и связанных элементов](#FindCodeHistory).

## <a name="QA"></a> Вопросы и ответы

### <a name="ChangeOrTurnOff"></a> Вопрос. Как включить и выключить CodeLens? Как выбрать отображаемые индикаторы?
 **Ответ.**  Включать и выключать можно все индикаторы, кроме индикатора ссылок. Откройте меню **Инструменты**и последовательно выберите пункты **Параметры**, **Текстовый редактор**, **Все языки**, **CodeLens**.

 Если индикаторы включены, параметры CodeLens можно также открыть из индикаторов.

 ![Индикаторы &#45; включения CodeLens отключены или включены](../ide/media/codelensturnoffonindicatorsfromcode.png "коделенстурноффониндикаторсфромкоде")

 Индикаторы CodeLens уровня файла включаются и отключаются с помощью значка шеврона в нижней части окна редактора.

 ![Включение и&#45;отключение индикаторов на уровне файлов](../ide/media/codelensfilelevelonandoff.png "коделенсфилелевелонандофф")

### <a name="NoIndicators"></a> Вопрос. Где находится CodeLens?
 **Ответ.** CodeLens отображается в коде Visual C# .NET и Visual Basic .NET на уровне метода, класса, индексатора и свойства. Для всех других типов файлов CodeLens отображается на уровне файла.

- Включите CodeLens. Откройте меню **Инструменты**и последовательно выберите пункты **Параметры**, **Текстовый редактор**, **Все языки**, **CodeLens**.

- Если код хранится в TFS, с помощью [команды CodeIndex](../ide/codeindex-command.md) и [команды TFS Config](https://msdn.microsoft.com/94424190-3b6b-4f33-a6b6-5807f4225b62)убедитесь, что индексирование кода включено.

- Индикаторы, связанные с TFS, отображаются, только когда рабочие элементы связаны с кодом и имеются разрешения на открытие связанных рабочих элементов. [Убедитесь в наличии разрешений члена команды.](/azure/devops/organizations/security/view-permissions)

- Индикаторы модульных тестов не отображаются, если в коде приложения отсутствуют модульные тесты. Индикаторы состояния теста отображаются автоматически в тестовых проектах. Если известно, что код приложения имеет модульные тесты, но индикаторы тестов не отображаются, попробуйте выполнить сборку решения (**CTRL + SHIFT + B**).

### <a name="q-why-dont-i-see-the-work-item-details-for-a-commit"></a>Вопрос: Почему я не вижу сведения рабочего элемента для фиксации?
 **Ответ.** Это может происходить, когда CodeLens не может найти рабочие элементы в TFS. Проверьте, что вы подключены к командному проекту, который имеет эти рабочие элементы, и что имеются разрешения для просмотра этих рабочих элементов. Это также может произойти, если описание фиксации содержит неверные сведения об идентификаторах рабочих элементов в TFS.

### <a name="NoLync"></a> Вопрос. Почему не отображаются индикаторы Lync или Skype?
 **Ответ.** Они не отображаются, если вы не вошли в службу Lync или Skype для бизнеса, не установили ни одну из них или используете неподдерживаемую конфигурацию. Однако вы по-прежнему можете отправлять почту:

 ![Владелец &#45; набора изменений контакта CodeLens по почте](../ide/media/codelenscodesendmailchangesetnolync1.png "CodeLensCodeSendMailChangesetNoLync1")

 **Какие конфигурации Lync и Skype поддерживаются?**

- Skype для бизнеса (32- или 64-разрядная версия)

- Lync 2010 или более поздняя версия отдельно (32- или 64-разрядная), но не Lync Basic 2013 с Windows 8.1

  CodeLens не поддерживает наличие нескольких установленных версий Lync или Skype. Они могут быть не локализованы для всех локализованных версий Visual Studio.

### <a name="q-how-do-i-change-the-font-and-color-for-codelens"></a>Вопрос. Как изменить шрифт и цвет CodeLens?
 **О.** Последовательно щелкните **Сервис**, **Параметры**, **Среда**, **Шрифты и цвета**.

 ![Изменение &#45; параметров шрифта и цвета в CodeLens](../ide/media/codelensoptionsfontscolorssettings.png "коделенсоптионсфонтсколорссеттингс")

 Для использования клавиатуры выполните следующие действия.

1. Нажмите клавиши **ALT + T + O** , чтобы открыть окно **Параметры** .

2. Нажмите клавишу **СТРЕЛКА ВВЕРХ** или **СТРЕЛКА ВНИЗ** , чтобы перейти к узлу **Среда** , а затем нажмите клавишу **СТРЕЛКА ВЛЕВО** , чтобы развернуть узел.

3. Нажмите клавишу **СТРЕЛКА ВНИЗ** , чтобы перейти к пункту **Шрифты и цвета**.

4. Нажмите клавишу **TAB** , чтобы перейти к списку **Параметры для** , после чего нажмите клавишу **СТРЕЛКА ВНИЗ** , чтобы выбрать **CodeLens**.

### <a name="q-can-i-move-the-codelens-heads-up-display"></a>В. Можно ли переместить HUD-элемент CodeLens?
 Ответ **.** Да, выберите ![пункт &#45; закрепить codelens в качестве окна](../ide/media/codelensdockwindow.png "коделенсдокквиндов") , чтобы закрепить CodeLens как окно.

 ![Закрепить окно индикатора CodeLens](../ide/media/codelensselectdockwindow.png "коделенсселектдокквиндов")

 ![Закрепленное окно ссылок CodeLens](../ide/media/codelensreferencesdockedwindow.png "коделенсреференцесдоккедвиндов")

### <a name="q-how-do-i-refresh-the-indicators"></a>В. Как обновить индикаторы?
 **Ответ.** Это зависит от индикатора.

- **Ссылки**: этот индикатор обновляется автоматически при изменении кода. Если этот индикатор закреплен в отдельном окне, его можно обновить вручную здесь:

     ![Закрепление CodeLens &#45; как окна](../ide/media/codelensviewreferencesdocked.png "коделенсвиевреференцесдоккед")

- **Команда**: эти индикаторы можно обновить вручную здесь:

     ![Индикаторы &#45; обновления CodeLens](../ide/media/codelensrefreshindicatorsfromcode.png "коделенсрефрешиндикаторсфромкоде")

- **Тест**: [найдите модульные тесты для кода](#FindRunUnitTests), чтобы обновить тот индикатор.

### <a name="LocalVersion"></a> Вопрос. Что такое "Локальная версия"?
 **О.** Стрелка **Локальная версия** указывает на последний набор изменений в локальной версии этого файла. Если на сервере находятся более новые наборы изменений, они отображаются над или под стрелкой **Локальная версия** в зависимости от порядка сортировки наборов изменений.

### <a name="q-can-i-manage-how-codelens-processes-code-to-show-history-and-linked-items"></a>Вопрос. Можно ли управлять тем, как CodeLens обрабатывает код для отображения журнала и связанных элементов?
 **Ответ.** Да, если код находится в TFS, используйте [команду CodeIndex](../ide/codeindex-command.md) с [командой TFS Config](https://msdn.microsoft.com/94424190-3b6b-4f33-a6b6-5807f4225b62).
