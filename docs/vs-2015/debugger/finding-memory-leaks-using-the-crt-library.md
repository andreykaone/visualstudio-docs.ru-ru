---
title: Обнаружение утечек памяти, с помощью библиотеки CRT | Документация Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- breakpoints, on memory allocation
- _CrtMemState
- _CrtMemCheckpoint
- memory leaks
- _CrtMemDifference
- memory leaks, detecting and isolating
- _CrtDumpMemoryLeaks
- _CrtSetBreakAlloc
- _crtBreakAlloc
- _CrtSetReportMode
- memory, debugging
- _CrtMemDumpStatistics
- debugging memory leaks
- _CRTDBG_MAP_ALLOC
- _CrtSetDbgFlag
ms.assetid: cf6dc7a6-cd12-4283-b1b6-ea53915f7ed1
caps.latest.revision: 33
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c102bba09901e55e9ec6196009965b912f8be967
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47573277"
---
# <a name="finding-memory-leaks-using-the-crt-library"></a>Обнаружение утечек памяти с помощью библиотеки CRT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [поиск памяти утечек с помощью CRT библиотеки](https://docs.microsoft.com/visualstudio/debugger/finding-memory-leaks-using-the-crt-library).  
  
Утечки памяти, определяемые как сбой при освобождении ранее выделенной памяти, — это одна из наиболее трудно обнаруживаемых ошибок в приложениях C/C++. Небольшая утечка памяти сначала может остаться незамеченной, но постепенно нарастающая утечка памяти может приводить к различным симптомам, от снижения производительности до аварийного завершения приложения из-за нехватки памяти. Более того, приложение, в котором происходит утечка памяти, может использовать всю доступную память и привести к аварийному завершению другого приложения, в результате чего может быть непонятно, какое приложение отвечает за сбой. Даже безобидная на первый взгляд утечка памяти может быть признаком других проблем, требующих устранения.  
  
 Отладчик [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] и библиотеки времени выполнения C (CRT) предоставляют средства для обнаружения утечек памяти.  
  
## <a name="enabling-memory-leak-detection"></a>Включение обнаружения утечек памяти  
 Основным средством для обнаружения утечек памяти является отладчик и отладочные функции кучи библиотеки времени выполнения C (CRT).  
  
 Чтобы включить отладочные функции кучи, вставьте в программу следующие операторы:  
  
```  
#define _CRTDBG_MAP_ALLOC  
#include <stdlib.h>  
#include <crtdbg.h>  
```  
  
 Для правильной работы функций CRT операторы `#include` должны следовать в приведенном здесь порядке.  
  
 Включение заголовочного файла crtdbg.h сопоставляет `malloc` и [бесплатный](http://msdn.microsoft.com/library/74ded9cf-1863-432e-9306-327a42080bb8) функций с их отладочными версиями [_malloc_dbg](http://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb) и `free`, которые отслеживают выделение и освобождение памяти. Это сопоставление используется только в отладочных построениях, в которых определен `_DEBUG`. В окончательных построениях используются первоначальные функции `malloc` и `free` .  
  
 Оператор `#define` сопоставляет базовые версии функций кучи CRT соответствующим отладочным версиям. Если оператор `#define` не используется, дамп утечки памяти будет менее подробным.  
  
 После того как с помощью этих операторов будут включены отладочные функции кучи, можно поместить вызов `_CrtDumpMemoryLeaks` перед точкой выхода приложения для отображения отчета об утечке памяти перед завершением работы приложения:  
  
```  
_CrtDumpMemoryLeaks();  
```  
  
 Если приложение имеет несколько точек выхода, не требуется вручную размещать вызов [_CrtDumpMemoryLeaks](http://msdn.microsoft.com/library/71b2eab4-7f55-44e8-a55a-bfea4f32d34c) в каждой точке выхода. Вызов функции `_CrtSetDbgFlag` в начале приложения приведет к автоматическому вызову функции `_CrtDumpMemoryLeaks` в каждой точке выхода. Необходимо установить два показанных здесь битовых поля:  
  
```  
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );  
```  
  
 По умолчанию `_CrtDumpMemoryLeaks` выводит отчет об утечке памяти в область **Отладка** окна **Вывод** . `_CrtSetReportMode` можно использовать для перенаправления отчета в другое расположение.  
  
 Если используется библиотека, она может переустановить вывод в другое расположение. В этом случае можно вернуть вывод обратно в окно **Вывод** , как показано ниже:  
  
```  
_CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );  
```  
  
## <a name="interpreting-the-memory-leak-report"></a>Интерпретация отчета об утечке памяти  
 Если приложение не определяет `_CRTDBG_MAP_ALLOC`, [_CrtDumpMemoryLeaks](http://msdn.microsoft.com/library/71b2eab4-7f55-44e8-a55a-bfea4f32d34c) отображает отчет об утечке памяти, выглядящий следующим образом:  
  
```  
Detected memory leaks!  
Dumping objects ->  
{18} normal block at 0x00780E80, 64 bytes long.  
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD  
Object dump complete.  
```  
  
 Если приложение определяет `_CRTDBG_MAP_ALLOC`, отчет об утечке памяти выглядит следующим образом:  
  
```  
Detected memory leaks!  
Dumping objects ->  
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}   
 normal block at 0x00780E80, 64 bytes long.  
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD  
Object dump complete.  
```  
  
 Разница заключается в том, что во втором отчете отображается имя файла и номер строки, в которой впервые было произведено выделение утекающей памяти.  
  
 Независимо от определения `_CRTDBG_MAP_ALLOC` , в отчете об утечке памяти отображаются следующие сведения:  
  
-   Номер выделения памяти, в этом примере — `18` .  
  
-   [Тип блока](http://msdn.microsoft.com/en-us/e2f42faf-0687-49e7-aa1f-916038354f97), в этом примере — `normal` .  
  
-   Расположение памяти в шестнадцатеричном формате, в этом примере — `0x00780E80` .  
  
-   Размер блока, в этом примере — `64 bytes` .  
  
-   Первые 16 байт данных в блоке, в шестнадцатеричном формате.  
  
 В отчете об утечке памяти блок памяти может определяться как обычный, клиентский или CRT. *Обычный блок* — это обыкновенная память, выделенная программой. *Клиентский блок* — особый тип блока памяти, используемой программами MFC для объектов, для которых требуется деструктор. Оператор `new` в MFC создает либо обычный, либо клиентский блок, в соответствии с создаваемым объектом. *Блок CRT* — это блок памяти, выделенной библиотекой CRT для внутреннего использования. Освобождение этих блоков производится библиотекой CRT. Поэтому маловероятно увидеть их в отчете об утечке памяти — разумеется, если не возникнет серьезный сбой, например повреждение библиотеки CRT.  
  
 Существуют два других типа блоков памяти, которые никогда не отображаются в отчетах об утечке памяти. *Свободный блок* — это блок памяти, которая была освобождена. Это по определению означает, что она не имеет отношения к утечкам. *Пропускаемый блок* — это память, специально помеченная для исключения из отчета об утечке памяти.  
  
 Эти способы работают для памяти, выделенной с помощью стандартной функции `malloc` библиотеки CRT. Если программа выделяет память с помощью C++ `new` оператор, однако вы можете увидеть только имя файла и номер строки где реализация глобального `operator new` вызовы `_malloc_dbg` в отчете об утечке памяти. Так как это поведение не очень полезен, можно изменить его для передачи данных строку, которая предоставляется выделение посредством макросом, который выглядит следующим образом: 
 
```cpp  
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```  
  
Теперь вы можете заменить `new` оператора с помощью `DBG_NEW` макрос в коде. В отладочных сборках, это используется перегруженная версия глобального `operator new` , принимает дополнительные параметры для типа блока, файла и номер строки. Эта перегрузка `new` вызовы `_malloc_dbg` для записи дополнительных сведений. При использовании `DBG_NEW`, утечки памяти сообщает, Показать имя файла и номер строки, где были выделены потерянные объекты. В окончательных сборках, используется значение по умолчанию `new`. (Не рекомендуется создать макрос препроцессора с именем `new`, или другие ключевое слово языка.) Ниже приведен пример этого метода:  
  
```cpp  
// debug_new.cpp
// compile by using: cl /EHsc /W4 /D_DEBUG /MDd debug_new.cpp
#define _CRTDBG_MAP_ALLOC
#include <cstdlib>
#include <crtdbg.h>

#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif

struct Pod {
    int x;
};

void main() {
    Pod* pPod = DBG_NEW Pod;
    pPod = DBG_NEW Pod; // Oops, leaked the original pPod!
    delete pPod;

    _CrtDumpMemoryLeaks();
}
```  
  
При выполнении этого кода в отладчике в Visual Studio, вызов `_CrtDumpMemoryLeaks` создает отчет в **вывода** окно, которое выглядит примерно так:  
  
```Output  
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD 
Object dump complete.
```  
  
Это означает, что утечка выделение было предназначено в строке 20 debug_new.cpp.  
  
## <a name="setting-breakpoints-on-a-memory-allocation-number"></a>Задание точек останова для номера выделения памяти  
 Номер выделения памяти сообщает, когда был выделен утекающий блок памяти. Например, блок с номером выделения памяти 18 — это 18-й блок памяти, выделенный во время выполнения программы. В отчете CRT учитываются все выделения блоков памяти во время выполнения. Сюда входят выделения, произведенные библиотекой CRT и другими библиотеками, такими как MFC. Поэтому блок с номером выделения памяти 18 может не быть 18-м блоком памяти, выделенным вашим кодов. Как правило, не будет.  
  
 Номер выделения можно использовать для того, чтобы задать точку останова в том месте, где выделяется память.  
  
#### <a name="to-set-a-memory-allocation-breakpoint-using-the-watch-window"></a>Установка точки останова для выделения памяти с помощью окна контрольных значений  
  
1.  Задайте точку останова недалеко от начала приложения, затем запустите приложение.  
  
2.  Когда выполнение приложения остановится в точке останова, откройте окно **Контрольные значения** .  
  
3.  В окне **Контрольные значения** введите `_crtBreakAlloc` в столбце **Имя** .  
  
     Если используется многопоточная версия DLL библиотеки CRT (параметр /MD), добавьте контекстный оператор: `{,,ucrtbased.dll}_crtBreakAlloc`.  
  
4.  Нажмите клавишу **ВВОД**.  
  
     Отладчик выполнит оценку вызова и поместит результат в столбец **Значение** . Это значение будет равно -1, если в местах выделения памяти не задано ни одной точки останова.  
  
5.  В столбце **Значение** замените отображаемое значение номером выделения памяти, на котором нужно приостановить выполнение.  
  
 После задания точки останова для номера выделения памяти можно продолжить отладку. Проследите за тем, чтобы программа была запущена в таких же условиях, как и в предыдущий раз, чтобы порядок выделения памяти не изменился. Когда выполнение программы будет приостановлено на заданном выделении памяти, с помощью окна **Стек вызовов** и других окон отладчика определите условия выделения памяти. Затем можно продолжить выполнение программы и проследить, что происходит с этим объектом и почему выделенная ему память освобождается неправильно.  
  
 Иногда может быть полезно задать точку останова по данным на самом объекте. Для получения дополнительной информации см. [Using Breakpoints](../debugger/using-breakpoints.md).  
  
 Точки останова для выделения памяти можно также задать в коде. Это можно сделать двумя способами.  
  
```  
_crtBreakAlloc = 18;  
```  
  
 или  
  
```  
_CrtSetBreakAlloc(18);  
```  
  
## <a name="comparing-memory-states"></a>Сравнение состояний памяти  
 Другая технология для обнаружения утечек памяти включает получение "снимков" состояния памяти приложения в ключевых точках. Чтобы получить снимок состояния памяти в заданной точке приложения, создайте структуру **_CrtMemState** и передайте ее функции `_CrtMemCheckpoint` . Функция поместит в структуру снимок текущего состояния памяти:  
  
```  
_CrtMemState s1;  
_CrtMemCheckpoint( &s1 );  
  
```  
  
 Функция`_CrtMemCheckpoint` поместит в структуру снимок текущего состояния памяти.  
  
 Чтобы вывести содержимое структуры **_CrtMemState** , передайте ее функции `_ CrtMemDumpStatistics` :  
  
```  
_CrtMemDumpStatistics( &s1 );  
  
```  
  
 Функция`_ CrtMemDumpStatistics` выводит дамп состояния памяти, который выглядит примерно таким образом:  
  
```  
0 bytes in 0 Free Blocks.  
0 bytes in 0 Normal Blocks.  
3071 bytes in 16 CRT Blocks.  
0 bytes in 0 Ignore Blocks.  
0 bytes in 0 Client Blocks.  
Largest number used: 3071 bytes.  
Total allocations: 3764 bytes.  
  
```  
  
 Чтобы определить, произошла ли утечка памяти на отрезке кода, можно сделать снимок состояния памяти перед ним и после него, а затем сравнить оба состояния с помощью функции `_ CrtMemDifference` :  
  
```  
_CrtMemCheckpoint( &s1 );  
// memory allocations take place here  
_CrtMemCheckpoint( &s2 );  
  
if ( _CrtMemDifference( &s3, &s1, &s2) )  
   _CrtMemDumpStatistics( &s3 );  
```  
  
 Функция`_CrtMemDifference` сравнивает состояния памяти `s1` и `s2` и returns a result in (`s3`), представляющий собой разницу `s1` и `s2`.  
  
 Еще один способ поиска утечек памяти заключается в размещении вызовов `_CrtMemCheckpoint` в начале и конце программы с последующим использованием `_CrtMemDifference` для сравнения результатов. Если `_CrtMemDifference` показывает утечку памяти, можно добавить дополнительные вызовы функции `_CrtMemCheckpoint` , чтобы разделить программу с помощью двоичного поиска, пока не будет найден источник утечки.  
  
## <a name="false-positives"></a>Ложные срабатывания  
 В некоторых случаях `_CrtDumpMemoryLeaks` может ошибочно диагностировать утечку памяти. Это может произойти в случае использования библиотеки, в которой внутренние выделения отмечены как _NORMAL_BLOCK вместо `_CRT_BLOCK`или `_CLIENT_BLOCK`. В таком случае функция `_CrtDumpMemoryLeaks` не может различать пользовательские выделения и внутренние выделения библиотеки. Если глобальные деструкторы для выделений библиотеки выполняются после точки вызова функции `_CrtDumpMemoryLeaks`, каждое внутреннее выделение библиотеки принимается за утечку памяти. Предыдущие версии библиотеки стандартных шаблонов, предшествовавшие Visual Studio .NET, приводили к тому, что функция `_CrtDumpMemoryLeaks` сообщала о таких ложных утечках, но в последних выпусках это было исправлено.  
  
## <a name="see-also"></a>См. также  
 [Сведения о куче отладки CRT](../debugger/crt-debug-heap-details.md)   
 [Безопасность отладчика](../debugger/debugger-security.md)   
 [Отладка машинного кода](../debugger/debugging-native-code.md)


