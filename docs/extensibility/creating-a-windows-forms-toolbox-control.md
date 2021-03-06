---
title: Создание системы управления инструментами Windows (ru) Документы Майкрософт
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7e7749302252c5d56f21c58de9b6ac23f898572
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739581"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Создание управления набором инструментов форм Windows

Шаблон элемента управления инструментами Windows Forms, включенный в Visual Studio Extensibility Tools (VS SDK), позволяет создавать элемент управления **Toolbox,** который автоматически добавляется при установке расширения. В этом пошаговом показании, как использовать шаблон для создания простого встречного управления, который можно распространять среди других пользователей.

## <a name="prerequisites"></a>Предварительные требования

Начиная с Visual Studio 2015, вы не устанавливаете Visual Studio SDK из центра загрузки. Он включен в качестве дополнительной функции в Visual Studio установки. Вы также можете установить VS SDK позже. Для получения дополнительной информации, [см.](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-the-toolbox-control"></a>Создание управления набором инструментов

Шаблон управления набором инструментов Форм Windows создает неопределенный пользовательский контроль и предоставляет всю функциональность, необходимую для добавления элемента управления в **Toolbox.**

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Создание расширения с помощью управления набором инструментов форм Windows

1. Создайте проект VSIX под названием `MyWinFormsControl`. Шаблон проекта VSIX можно найти в диалоге **нового проекта,** ища "vsix".

2. Когда проект откроется, добавьте шаблон **элемента управления инструментами Форм Windows** под названием. `Counter` В **Solution Explorer**, правой кнопкой мыши узла проекта и выберите **Добавить** > **новый пункт**. В диалоге **Добавить новый пункт** перейдите на **Visual C е** > **Расширительность** и выберите **управление набором инструментов для форм Windows**

3. Это добавляет элемент управления `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> пользователем, для размещения элемента управления в **Toolbox**и **запись актива Microsoft.VisualStudio.ToolboxControl** Asset в манифесте VSIX для развертывания.

### <a name="build-a-user-interface-for-the-control"></a>Создание пользовательского интерфейса для управления

Для `Counter` управления требуется два <xref:System.Windows.Forms.Label> элемента управления детьми: для отображения текущего счета и <xref:System.Windows.Forms.Button> для сбросить счет до 0. Никакие другие элементы управления детьми не требуются, потому что абоненты будут приравливывать счетчик программно.

#### <a name="to-build-the-user-interface"></a>Создание пользовательского интерфейса

1. В **Solution Explorer**, дважды нажмите *Counter.cs,* чтобы открыть его в дизайнера.

2. Удалите **Нажмите здесь !** кнопка, включенная по умолчанию при добавлении шаблона элемента управления инструментами Форм Windows.

3. От **Toolbox**перетащите `Label` элемент `Button` управления, а затем элемент управления под ним на поверхность дизайна.

4. Изопроизвить общее управление пользователем до 150, 50 пикселей и изменить размер управления кнопкой до 50, 20 пикселей.

5. В окне **Свойств** установите следующие значения для элементов управления на поверхности конструкции.

    |Control|Свойство|Значение|
    |-------------|--------------|-----------|
    |`Label1`|**Text**|""|
    |`Button1`|**имя**;|btnReset|
    |`Button1`|**Text**|Reset|

### <a name="code-the-user-control"></a>Код управления пользователем

Элемент `Counter` управления будет подвергать метод увращению счетчика, событие, которое должно быть поднято всякий раз, когда счетчик приравлен, кнопка **сброса** и три свойства для хранения текущего счета, текста дисплея, а также отображение или сокрытие кнопки **сброса.** Атрибут `ProvideToolboxControl` определяет место на **панели элементов** , в котором будет отображаться элемент управления `Counter` .

#### <a name="to-code-the-user-control"></a>Кодирование управления пользователем

1. Дважды щелкните форму, чтобы открыть обработчик событий нагрузки в окне кода.

2. Над методом обработчика событий в классе управления создайте целый ряд для хранения значения счетчика и строку для хранения текста отображения, как показано в следующем примере.

    ```csharp
    int currentValue;
    string displayText;
    ```

3. Создание следующих деклараций о государственной собственности.

    ```csharp
    public int Value {
        get { return currentValue; }
    }

    public string Message {
        get { return displayText; }
        set { displayText = value; }
    }

    public bool ShowReset {
        get { return btnReset.Visible; }
        set { btnReset.Visible = value; }
    }

    ```

    Звонящие могут получить доступ к этим свойствам, чтобы получить и установить текст отображения счетчика и показать или скрыть кнопку **сбросить.** Звонящие могут получить текущую стоимость `Value` свойства только для чтения, но они не могут установить значение непосредственно.

4. Поместите следующий `Load` код в случае для элемента управления.

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    Установка текста **меток** в <xref:System.Windows.Forms.UserControl.Load> случае позволяет целевым свойствам загружаться до их применения значений. Установка текста **метки** в конструкторе приведет к пустой **этикетке.**

5. Создайте следующий общедоступный метод для приращения счетчика.

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. Добавьте декларацию `Incremented` о событии в класс управления.

    ```csharp
    public event EventHandler Incremented;
    ```

    Звонящие могут добавлять обработчики в это событие, чтобы реагировать на изменения в значении счетчика.

7. Вернуться к представлению проектирования и дважды щелкните кнопку **Сбрать** для создания обработчика `btnReset_Click` событий, а затем заполните ее, как показано в следующем примере.

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. Непосредственно над определением класса в объявлении атрибута `ProvideToolboxControl` измените значение первого параметра с `"MyWinFormsControl.Counter"` на `"General"`. Таким образом задается имя группы элементов, в которой будет размещаться элемент управления на **панели элементов**.

    В приведенном ниже примере показаны атрибут `ProvideToolboxControl` и скорректированное определение класса.

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>Тестирование элемента управления

 Чтобы протестировать элемент управления **Toolbox,** сначала протестуйте его в среде разработки, а затем протестируете в скомпилированном приложении.

#### <a name="to-test-the-control"></a>Тестирование элемента управления

1. Нажмите **F5,** чтобы **начать отладку**.

    Эта команда создает проект и открывает второй экспериментальный экземпляр Visual Studio, который имеет контроль установлен.

2. В экспериментальном экземпляре Visual Studio создайте проект **приложения Windows Forms.**

3. В **Solution Explorer**, дважды нажмите *Form1.cs,* чтобы открыть его в дизайнер, если он еще не открыт.

4. В **наборе инструментов**элемент управления `Counter` должно отображаться в разделе **Общий.**

5. Перетащите `Counter` элемент управления в форму, а затем выберите его. Свойства `Value` `Message`и `ShowReset` свойства будут отображаться в окне **Свойств** вместе с свойствами, которые унаследованы от. <xref:System.Windows.Forms.UserControl>

6. Установите свойство `Message` в значение `Count:`.

7. Перетащите <xref:System.Windows.Forms.Button> элемент управления в форму, а затем установите свойства имени и текста кнопки. `Test`

8. Дважды нажмите кнопку, чтобы открыть *Form1.cs* в представлении кода и создать обработчик клика.

9. В обработчике `counter1.Increment()`клика позвоните .

10. В функции конструктора, после `InitializeComponent`вызова, введите, `counter1``.``Incremented +=` а затем нажмите **Вкладка** дважды.

    Visual Studio создает обработчик уровня `counter1.Incremented` формы для события.

11. Выделите `Throw` оператора в обработчике событий, введите, `mbox`а затем нажмите **Tab** дважды, чтобы создать окно сообщения из фрагмента кода mbox.

12. На следующей строке `if` / `else` добавьте следующий блок, чтобы установить видимость кнопки **сбросить.**

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. Нажмите клавишу **F5**.

    Форма открывается. Элемент `Counter` управления отображает следующий текст.

    **Количество голосов: 0**

14. Нажмите **Проверить**.

    Счетчик приращений и Visual Studio отображает окно сообщений.

15. Закройте ящик с сообщениями.

    Кнопка **сбросить** исчезает.

16. Нажмите **Тест,** пока счетчик не достигнет **5** закрытия почтовых ящиков каждый раз.

    Появляется кнопка **сбросить.**

17. Выберите **Сбросить**.

    Счетчик сбрасывает до **0**.

## <a name="next-steps"></a>Следующие шаги

При создании элемента управления **Toolbox** Visual Studio создает файл под названием *ProjectName.vsix* в папке «Бин-отладка» вашего проекта. Вы можете развернуть элемент управления, загрузив файл *.vsix* в сеть или на веб-узел. Когда пользователь открывает файл *.vsix,* элемент управления устанавливается и добавляется в **набор инструментов** Visual Studio на компьютере пользователя. Кроме того, вы можете загрузить файл *.vsix* в [Visual Studio Marketplace,](https://marketplace.visualstudio.com/) чтобы пользователи могли найти его, просматривая диалог о**расширениях и обновлениях.** **Tools** > 

## <a name="see-also"></a>См. также

- [Расширить другие части Визуальной студии](../extensibility/extending-other-parts-of-visual-studio.md)
- [Создание управления ящиком инструментов WPF](../extensibility/creating-a-wpf-toolbox-control.md)
- [Расширить другие части Визуальной студии](../extensibility/extending-other-parts-of-visual-studio.md)
- [Основы управления Windows Forms](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
