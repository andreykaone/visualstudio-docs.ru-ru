---
title: Выбор интерпретатора и окружения Python для проекта
description: Вы можете отдельно выбрать окружение Python, включая Anaconda и виртуальные среды, для применения к конкретному проекту.
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 34ceb2ec7cc923f6642977cf4c70fbfae07bf523
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307085"
---
# <a name="how-to-select-a-python-environment-for-a-project"></a>Выбор окружения Python для проекта

Весь код в проекте Python выполняется в контексте определенного окружения, например в глобальном окружении Python, окружении Anaconda, виртуальном окружении или окружении Conda. Visual Studio использует это же окружение для отладки, импорта, автозавершения элементов, проверки синтаксиса и других задач, требующих языковые службы, которые характерны для данной версии Python и набора установленных пакетов.

Для всех новых проектов Python в Visual Studio настраивается глобальное окружение по умолчанию, которое указано в узле **Окружения Python** в **обозревателе решений**:

![Глобальное окружение Python по умолчанию, отображаемое в обозревателе решений](media/environments/environments-project.png)

::: moniker range="vs-2017"
Чтобы изменить окружение для проекта, щелкните правой кнопкой мыши узел **Окружения Python** и выберите **Добавление и удаление окружений Python**. В появившемся списке глобальных, виртуальных окружений и окружений Conda выберите все окружения, которые должны отображаться в узле **Окружения Python**:

![Диалоговое окно добавления и удаления сред Python](media/environments/environments-add-remove.png)

Когда вы щелкнете **ОК**, все выбранные окружения отобразятся в узле **Окружения Python**. Полужирным шрифтом здесь выделено окружение, которое сейчас активно:

![Несколько окружений Python отображаются в обозревателе решений](media/environments/environments-project-multiple.png)

Чтобы быстро активировать другое окружение, щелкните его имя правой кнопкой мыши и выберите команду **Активировать окружение**. Ваш выбор сохраняется в проекте, и выбранное окружение применяется при каждом последующем открытии проекта. Если вы снимете все флажки в диалоговом окне **Добавление и удаление окружений Python**, в Visual Studio будет активировано глобальное окружение по умолчанию.

В контекстном меню узла **Окружения Python** также доступны дополнительные команды:

| Команда | Описание |
| --- | --- |
| **Добавить виртуальное окружение** | Запускает процесс создания виртуального окружения в проекте. Дополнительные сведения см. в разделе [Создание виртуального окружения](#create-a-virtual-environment). |
| **Добавить существующее виртуальное окружение** | Выводит запрос на выбор папки, содержащей виртуальное окружение, и добавляет окружение в список в узле **Окружения Python**, но не активирует его. См. дополнительные сведения об [активации существующего виртуального окружения](#activate-an-existing-virtual-environment). |
| **Создать окружение Conda** | Переключается в *окно* **Окружения Python**, в котором нужно ввести имя окружения и указать для него базовый интерпретатор. См. [Окружения Conda](managing-python-environments-in-visual-studio.md#conda-environments). |
::: moniker-end

::: moniker range=">=vs-2019"
Чтобы изменить окружение для проекта, щелкните правой кнопкой мыши узел **Окружения Python** и выберите **Добавить окружение** или выберите **Добавить окружение** из раскрывающегося списка окружений на панели инструментов Python.

Когда откроется диалоговое окно **Добавление окружения**, перейдите на вкладку **Существующее окружение** и выберите новое окружение из раскрывающегося списка **Окружения**:

![Выбор окружения проекта в диалоговом окне "Добавление окружений"](media/environments/environments-project-2019.png)

Если вы уже добавили в проект окружение, отличное от стандартного глобального окружения, для него может потребоваться активация. Щелкните окружение правой кнопкой мыши в узле **Окружения Python** и выберите действие **Активировать окружение**. Чтобы удалить из проекта окружение, выберите действие **Удалить**.

![Активация и удаление окружения проекта](media/environments/environments-project-add-remove-2019.png)
::: moniker-end

## <a name="use-virtual-environments"></a>Использование виртуальных окружений

Виртуальное окружение — это уникальное сочетание интерпретатора Python и набора библиотек, которое не повторяется в других глобальных окружениях и окружениях Conda. Виртуальное окружение предназначено для конкретного проекта, и данные о нем хранятся в папке проекта. В этой папке содержатся установленные библиотеки окружения и файл *pyvenv.cfg*, в котором указан путь к *базовому интерпретатору*, расположенному в другом месте файловой системы. То есть в виртуальном окружении нет копии интерпретатора, а только ссылка на него.

Преимуществом виртуального окружения является то, что в нем по мере разработки проекта всегда будут отражаться точные зависимости проекта. (С другой стороны, в общем глобальном окружении можно хранить любое число библиотек, используемых или неиспользуемых в проекте.) В виртуальном окружении можно легко создать файл *requirements.txt*, который будет использоваться для переустановки этих зависимостей на другой рабочий компьютер или компьютер разработки. Дополнительные сведения см. в руководстве по [управлению необходимыми пакетами с помощью requirements.txt](managing-required-packages-with-requirements-txt.md).

Если в Visual Studio открыть проект, который содержит файл *requirements.txt*, Visual Studio автоматически позволит воссоздать виртуальное окружение. На тех компьютерах, где не установлена среда Visual Studio, можно восстанавливать пакеты с помощью команды `pip install -r requirements.txt`.

Учитывая то, что в виртуальном окружении жестко запрограммирован путь к базовому интерпретатору и можно воссоздать окружение с помощью файла *requirements.txt*, обычно вся папка виртуального окружения не указывается в системе управления версиями.

В следующих разделах объясняется, как активировать существующее виртуальное окружение в проекте и создать новое виртуальное окружение.

В Visual Studio виртуальное окружение для проекта активируется так же, как и любое другое окружение: с помощью узла **Окружения Python** в **обозревателе решений**.

Если виртуальное окружение добавлено в проект, оно появится в окне **Окружения Python**. После этого вы сможете активировать его, как и любое другое окружение, и управлять его пакетами.

::: moniker range="vs-2017"
### <a name="create-a-virtual-environment"></a>Создание виртуального окружения

Виртуальное окружение можно создать напрямую в Visual Studio, выполнив следующие действия.

1. В **обозревателе решений** выберите **Добавить виртуальное окружение**, щелкнув правой кнопкой мыши **Окружения Python**. Откроется следующее диалоговое окно:

    ![Создание виртуальной среды](media/environments/environments-add-virtual-1.png)

1. В поле **Расположение виртуального окружения** укажите путь к виртуальному окружению. Если вы укажете только имя, для виртуального окружения в текущем проекте создается вложенная папка с таким же именем.

1. Выберите среду в качестве базового интерпретатора и щелкните **Создать**. В Visual Studio отобразится индикатор выполнения, который позволяет отслеживать процесс настройки окружения и скачивания необходимых пакетов. После завершения процесса виртуальное окружение отобразится в окне **Окружения Python** для проекта, в котором оно размещено.

1. Виртуальное окружение не активируется по умолчанию. Чтобы активировать окружение для проекта, щелкните его правой кнопкой мыши и выберите **Активировать окружение**.

> [!Note]
> Если указан путь к расположению существующего виртуального окружения, Visual Studio автоматически обнаруживает базовый интерпретатор (для этого используется файл *orig-prefix.txt* в каталоге окружения *lib*). Вместо кнопки **Создать** отобразится кнопка **Добавить**.
>
> Если в добавляемом виртуальном окружении уже есть файл *requirements.txt*, в диалоговом окне **Добавление виртуального окружения** отображается запрос на автоматическую установку пакетов. Этот механизм упрощает восстановление окружения на другом компьютере:
>
> ![Создание виртуальной среды при наличии файла requirements.txt](media/environments/environments-requirements-txt.png)
>
> В любом случае результат будет такой же, как и при **добавлении существующего виртуального окружения**.

### <a name="activate-an-existing-virtual-environment"></a>Активация существующего виртуального окружения

Если у вас уже есть виртуальное окружение, его можно активировать для проекта следующим образом:

1. В **обозревателе решений** выберите **Добавить существующее виртуальное окружение**, щелкнув правой кнопкой мыши **Окружения Python**.

1. Откроется диалоговое окно **Обзор**. Найдите и выберите здесь папку с виртуальным окружением, а затем нажмите кнопку **ОК**. Если Visual Studio обнаружит в этом окружении файл *requirements.txt*, появится запрос на установку обнаруженных пакетов.

1. Через несколько секунд виртуальное окружение появится в узле **Окружения Python** **обозревателя решений**. Виртуальное окружение не активируется по умолчанию, поэтому щелкните его правой кнопкой мыши и выберите действие **Активировать окружение**.
::: moniker-end

::: moniker range=">=vs-2019"
### <a name="create-a-virtual-environment"></a>Создание виртуального окружения

Виртуальное окружение можно создать напрямую в Visual Studio, выполнив следующие действия.

1. Чтобы изменить окружение для проекта, щелкните правой кнопкой мыши узел **Окружения Python** в **обозревателе решений** и выберите **Добавить окружение** или выберите **Добавить окружение** из раскрывающегося списка окружений на панели инструментов Python. В открывшемся диалоговом окне **Добавление окружения** выберите вкладку **Виртуальное окружение**:

    ![Вкладка виртуального окружения в диалоговом окне "Добавление окружения"](media/environments/environments-add-virtual-1-2019.png)

1. Укажите имя виртуального окружения, выберите базовый интерпретатор и проверьте его расположение. В разделе **Install packages from file** (Устанавливать пакеты из файла) укажите путь к файлу *requirements.txt*, если нужно.

1. Проверьте другие параметры в диалоговом окне.

    | Параметр | Описание |
    | --- | --- |
    | Set as current environment (Установить в качестве текущего окружения) | После создания окружения активирует его в выбранном проекте. |
    | Set as default environment for new projects (Установить в качестве окружения по умолчанию для новых проектов) | Автоматически устанавливает окружение и активирует его во всех новых проектах, которые создаются в Visual Studio. При использовании этого варианта виртуальное окружение следует размещать за пределами конкретных проектов.  |
    | View in Python Environments window (Просмотреть в окне окружений Python) | Указывает, нужно ли открывать окно **Окружения Python** после создания окружения. |
    | Make this environment available globally (Сделать это окружение доступным глобально) | Указывает, нужно ли сделать это виртуальное окружение глобальным. При использовании этого варианта виртуальное окружение следует размещать за пределами конкретных проектов. |

1. Выберите **Создать**, чтобы завершить создание виртуального окружения. В Visual Studio отобразится индикатор выполнения, который позволяет отслеживать процесс настройки окружения и скачивания необходимых пакетов. После завершения процесса виртуальное окружение активируется и отображается в узле **Окружения Python** в **обозревателе решений** и в окне **Окружения Python** для проекта, в который оно включено.

### <a name="activate-an-existing-virtual-environment"></a>Активация существующего виртуального окружения

Если у вас уже есть виртуальное окружение, его можно активировать для проекта следующим образом:

1. В **обозревателе решений** щелкните правой кнопкой мыши **Окружения Python** и выберите **Добавить окружение**.

1. Откроется диалоговое окно **Обзор**. Найдите и выберите здесь папку с виртуальным окружением, а затем нажмите кнопку **ОК**. Если Visual Studio обнаружит в этом окружении файл *requirements.txt*, появится запрос на установку обнаруженных пакетов.

1. Через несколько секунд виртуальное окружение появится в узле **Окружения Python** **обозревателя решений**. Виртуальное окружение не активируется по умолчанию, поэтому щелкните его правой кнопкой мыши и выберите действие **Активировать окружение**.
::: moniker-end

### <a name="remove-a-virtual-environment"></a>Удаление виртуального окружения

1. В **обозревателе решений** щелкните правой кнопкой мыши виртуальное окружение и выберите **Удалить**.

1. В Visual Studio вам будет предложено выбрать нужное действие (убрать или удалить виртуальное окружение). Вариант **Убрать** означает, что окружение исчезнет из проекта, но сохранится в файловой системе. Если выбрать **Удалить**, окружение убирается из проекта и все его файлы удаляются из файловой системы. Это действие не затрагивает базовый интерпретатор.

## <a name="view-installed-packages"></a>Просмотр установленных пакетов

В обозревателе решений можно развернуть узел любого окружения, чтобы быстро просмотреть установленные в нем пакеты (то есть те, которые можно импортировать и применять в коде, когда активно это окружение):

![Пакеты Python для среды в обозревателе решений](media/environments/environments-installed-packages.png)

::: moniker range="vs-2017"
Чтобы установить пакеты, щелкните окружение правой кнопкой мыши и выберите действие **Установить пакет Python**. В окне **Окружения Python** откроется соответствующая вкладка **Пакеты**. Введите условие поиска (лучше всего имя пакета), и в Visual Studio отобразятся все подходящие пакеты.
::: moniker-end
::: moniker range=">=vs-2019"
Чтобы установить новые пакеты, щелкните окружение правой кнопкой мыши и выберите действие **Manage Python Packages** (Управление пакетами Python). В окне **Окружения Python** откроется соответствующая вкладка **Пакеты**. На вкладке **Пакеты** введите условие поиска (обычно это имя пакета), и Visual Studio отобразит все подходящие пакеты.
::: moniker-end

Пакеты (и зависимости) в Visual Studio для большинства окружений скачиваются из репозитория [Python Package Index (PyPI)](https://pypi.org). В нем же вы можете искать доступные пакеты. В строке состояния Visual Studio и окне вывода отображаются сведения об установке. Чтобы удалить пакет, щелкните его правой кнопкой мыши и выберите **Удалить**.

Обычно диспетчер пакетов conda по умолчанию использует канал `https://repo.continuum.io/pkgs/`, но доступны и другие каналы. Дополнительные сведения см. в статье [об управлении каналами](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-channels.html) (docs.conda.io).

Не забывайте, что отображаемые записи могут быть неточными, а задания установки и удаления — ненадежными или недоступными. Visual Studio использует диспетчер пакетов pip, если он доступен, и при необходимости скачивает и устанавливает его. Visual Studio также может использовать диспетчер пакетов простой установки (easy_install). Здесь же отображаются пакеты, установленные с помощью команд `pip` или `easy_install` из командной строки.

Обратите внимание, что сейчас Visual Studio не позволяет использовать `conda` для установки пакетов в окружении Conda. Вместо этого используйте `conda` из командной строки.

> [!Tip]
> Если пакет содержит исходный код собственных компонентов в файлах *\*.pyd*, попытка pip установить пакет завершается сбоем. Если необходимая версия Visual Studio не установлена, pip не может скомпилировать эти компоненты. В этом случае отображается сообщение об ошибке: **Ошибка: не удалось найти vcvarsall.bat**. Как правило, диспетчер `easy_install` может скачать предварительно скомпилированные двоичные файлы. Подходящий компилятор для более старых версий Python можно скачать по адресу [https://www.microsoft.com/download/details.aspx?id=44266](https://www.microsoft.com/download/details.aspx?id=44266). Дополнительные сведения см. в записи блога команды разработчиков Python [How to deal with the pain of “unable to find vcvarsall.bat”](https://devblogs.microsoft.com/python/unable-to-find-vcvarsall-bat/) (Что делать в случае возникновения ошибки "Не удалось найти vcvarsall.bat").

## <a name="see-also"></a>См. также

- [Управление окружениями Python в Visual Studio](managing-python-environments-in-visual-studio.md)
- [Использование файла requirements.txt для зависимостей](managing-required-packages-with-requirements-txt.md)
- [Пути поиска](search-paths.md)
- [Справочная информация по окну "Окружения Python"](python-environments-window-tab-reference.md)
