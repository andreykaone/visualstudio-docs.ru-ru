---
title: Использование CTest для C++
ms.date: 01/23/2020
ms.topic: conceptual
ms.author: corob
manager: jillfra
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 78759a017575916bce3b3fff643cbce8ff303fd6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/18/2020
ms.locfileid: "76826527"
---
# <a name="how-to-use-ctest-for-c-in-visual-studio-2017-and-later"></a>Использование CTest для C++ в Visual Studio 2017 и более поздних версиях

Система CMake (которая включает в себя CTest) по умолчанию интегрирована в среду IDE Visual Studio как компонент рабочей нагрузки **Разработка классических приложений на C++** . Если вам нужно установить ее на компьютере, откройте программу Visual Studio Installer, нажмите кнопку **Разработка классических приложений на C++** , а затем выберите команду **Изменить**. Выберите **Средства CMake C++ для Windows** в списке компонентов рабочей нагрузки.

## <a name="to-write-tests"></a>Написание тестов

Поддержка CMake в Visual Studio не распространяется на систему проектов Visual Studio. Поэтому тесты CTest создаются и настраиваются так же, как в любой среде CMake. Используйте команду `enable_testing()`, чтобы включить тестирование, и команду `add_test()` или `gtest_discover_tests()`, чтобы добавить новый тест. Дополнительные сведения о CTest см. в [документации по CMake](https://gitlab.kitware.com/cmake/community/wikis/doc/ctest/Testing-With-CTest). 

Дополнительные сведения об использовании CMake в Visual Studio см. в статье о [проектах CMake в Visual Studio](/cpp/build/cmake-projects-in-visual-studio).

## <a name="to-run-tests"></a>Выполнение тестов

CTest полностью интегрирован с **обозревателем тестов** и поддерживает платформы модульного тестирования Google и Boost. Эти платформы по умолчанию включены в качестве компонентов рабочей нагрузки **Разработка классических приложений на C++** . Но если вы обновляете проект с более старой версии Visual Studio, может потребоваться установить эти платформы с помощью программы Visual Studio Installer.

На следующем рисунке показаны результаты выполнения CTest с использованием платформы Google Test.

![Выполнение CTest с помощью платформы Google Test в Visual Studio](media/ctest-test-explorer.png)

Если вы используете CTest, но не используете адаптеры Google или Boost, результаты будут доступны на уровне CTest, а не на отдельном уровне метода проверки. Вы сможете выполнять отладку и использовать пошаговый режим для исполняемых файлов CTest, но без трассировки стека для отдельных тестов.

## <a name="see-also"></a>См. также раздел

- [Написание модульных тестов для C/C++](writing-unit-tests-for-c-cpp.md)
