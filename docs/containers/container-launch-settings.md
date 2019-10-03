---
title: Параметры запуска инструментов Visual Studio для работы с контейнерами
author: ghogen
description: Обзор процесса сборки с помощью инструментов для работы с контейнерами
ms.author: ghogen
ms.date: 08/15/2019
ms.technology: vs-azure
ms.topic: conceptual
ms.openlocfilehash: e039e862040036f3d96729c3bdf48caafe092136
ms.sourcegitcommit: 3cda0d58c5cf1985122b8977b33a171c7359f324
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2019
ms.locfileid: "71126055"
---
# <a name="container-tools-launch-settings"></a>Параметры запуска инструментов для работы с контейнерами

В папке *Properties* проекта ASP.NET Core есть файл launchSettings.json, который содержит параметры, управляющие запуском веб-приложения на компьютере разработки. Подробные сведения об использовании этого файла при разработке проектов ASP.NET см. в статье [Использование нескольких сред в ASP.NET Core](/aspnet/core/fundamentals/environments?view=aspnetcore-2.2). В файле *launchSettings.json* параметры в разделе **Docker** определяют то, как Visual Studio работает с контейнерными приложениями.

::: moniker range="vs-2017"
```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}"
    }
```

::: moniker-end
::: moniker range=">=vs-2019"

```json
    "Docker": {
      "commandName": "Docker",
      "launchBrowser": true,
      "launchUrl": "{Scheme}://{ServiceHost}:{ServicePort}",
      "environmentVariables": {
        "ASPNETCORE_URLS": "https://+:443;http://+:80",
        "ASPNETCORE_HTTPS_PORT": "44360"
      },
      "httpPort": 51803,
      "useSSL": true,
      "sslPort": 44360
    }
```

::: moniker-end

Параметр commandName указывает, что этот раздел относится к инструментам для работы с контейнерами. В таблице ниже приведены свойства, которые можно задать в этом разделе.

::: moniker range="vs-2017"
|Имя параметра|Пример|ОПИСАНИЕ|
|------------|-------|-------|---------------|
|launchBrowser|Visual Studio 2017|"launchBrowser": true|Указывает, следует ли запускать браузер после успешного запуска проекта.|
|launchUrl|Visual Studio 2017|"launchUrl": "\<схема>://\<узел_службы>:\<порт_службы>"|Этот URL-адрес используется при запуске браузера.  Поддерживаемые токены замены для этой строки:<br>   \<схема> — заменяется на "http" или "https" в зависимости от того, используется ли протокол SSL.<br>   \<узел_службы> — обычно заменяется на "localhost". Однако если контейнеры Windows предназначены для Windows 10 RS3 или более ранних версий, то этот токен заменяется на IP-адрес контейнера.<br>   \<порт_службы> — обычно заменяется на sslPort или httpPort в зависимости от того, используется ли протокол SSL.  Однако если контейнеры Windows предназначены для Windows 10 RS3 или более ранних версий, то этот токен заменяется на "443" или "80" в зависимости от того, используется ли протокол SSL.|
::: moniker-end
::: moniker range=">=vs-2019"
|Имя параметра|Пример|ОПИСАНИЕ|
|------------|-------|-------|---------------|
|commandLineArgs|"commandLineArgs": "--mysetting myvalue"|Эти аргументы командной строки используются при запуске проекта в контейнере.|
|environmentVariables|"environmentVariables": {<br>    "ASPNETCORE_URLS": "https://+:443; http://+:80",<br>    "ASPNETCORE_HTTPS_PORT": "44381"<br>}|Значения этих переменных среды передаются процессу при его запуске в контейнере.|
|httpPort|"httpPort": 24051|Этот порт узла сопоставляется с портом 80 контейнера при запуске контейнера.  Если значение не указано, оно берется из iisSettings.|
|launchBrowser|"launchBrowser": true|Указывает, следует ли запускать браузер после успешного запуска проекта.|
|launchUrl|"launchUrl": "\<схема>://\<узел_службы>:\<порт_службы>"|Этот URL-адрес используется при запуске браузера.  Поддерживаемые токены замены для этой строки:<br>   \<схема> — заменяется на "http" или "https" в зависимости от того, используется ли протокол SSL.<br>   \<узел_службы> — обычно заменяется на "localhost". Однако если контейнеры Windows предназначены для Windows 10 RS3 или более ранних версий, то этот токен заменяется на IP-адрес контейнера.<br>   \<порт_службы> — обычно заменяется на sslPort или httpPort в зависимости от того, используется ли протокол SSL.  Однако если контейнеры Windows предназначены для Windows 10 RS3 или более ранних версий, то этот токен заменяется на "443" или "80" в зависимости от того, используется ли протокол SSL.|
|sslPort|"sslPort": 44381|Этот порт узла сопоставляется с портом 443 контейнера при запуске контейнера.  Если значение не указано, оно берется из iisSettings.|
|useSSL|"useSSL": true|Указывает, следует ли использовать протокол SSL при запуске проекта.  Если свойство useSSL не задано, протокол SSL используется при значении sslPort > 0.
::: moniker-end

## <a name="next-steps"></a>Следующие шаги

Настройте проект, задав [свойства сборки с помощью инструментов для работы с контейнерами](container-msbuild-properties.md).

## <a name="see-also"></a>См. также

[Свойства сборки Docker Compose](docker-compose-properties.md)