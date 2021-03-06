---
ms.openlocfilehash: 8adac174fbc78778e7154a205088fb9e9a57ae4a
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2020
ms.locfileid: "68143521"
---

1. На компьютере, где открыт проект ASP.NET в Visual Studio, щелкните правой кнопкой мыши этот проект в обозревателе решений и выберите **Опубликовать**.

1. Если ранее вы настроили какие-либо профили публикации, появится панель **Опубликовать**. Выберите команду **Создать новый профиль**.

1. В открывшемся диалоговом окне **Выбрать целевой объект для публикации** выберите **Импортировать профиль**.

    ![Выбор команды Опубликовать](../../deployment/media/tutorial-publish-tool-import-profile.png)

1. Перейдите в расположение файла параметров публикации, созданного в предыдущем разделе.

1. В диалоговом окне **Импортировать файл параметров публикации** перейдите к профилю, созданному в предыдущем разделе, выберите его и нажмите кнопку **Открыть**.

    Visual Studio начинает процесс развертывания, а в окне вывода отображаются ход выполнения и результаты.

    При появлении любых ошибок развертывания щелкните **Параметры** для изменения параметров. Измените параметры и нажмите кнопку **Проверить** для тестирования новых параметров. Если имя узла не найдено, попробуйте указать IP-адрес вместо имени узла в полях **Сервер** и **Целевой URL-адрес**.

    ![Изменение параметров в средстве публикации](../../deployment/media/tutorial-configure-publish-settings-in-tool.png)
