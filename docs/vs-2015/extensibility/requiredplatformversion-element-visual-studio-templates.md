---
title: Элемент RequiredPlatformVersion (шаблоны Visual Studio) | Документация Майкрософт
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5fb35bfefeb7722c3ec488a1f9caf63cd49202dd
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/22/2018
ms.locfileid: "47564130"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>RequiredPlatformVersion - элемент (шаблоны Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Последнюю версию этого раздела можно найти в [элемент RequiredPlatformVersion (шаблоны Visual Studio)](https://docs.microsoft.com/visualstudio/extensibility/requiredplatformversion-element-visual-studio-templates).  
  
Указывает минимальную версию операционной системы, шаблон проекта необходима для правильной работы. Этот элемент используется для шаблонов проектов, которые создают [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] приложений.  
  
 `RequiredPlatformVersion` Значение сравнивается непосредственно с версией операционной системы. Если `RequiredPlatformVersion` выше, чем версия операционной системы, шаблон не отображается в **новый проект** диалоговое окно. Для указания шаблона для [!INCLUDE[win8](../includes/win8-md.md)] или более поздней версии, задайте `RequiredPlatformVersion` для 6.2.0. Для указания шаблона для [!INCLUDE[win81](../includes/win81-md.md)] или более поздней версии, задайте RequiredPlatformVersion для 6.3.0.  
  
 Шаблоны, которые указывают `RequiredPlatformVersion`= 8, совместимы с предыдущей клиента [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] шаблонов.  
  
 VSTemplate  
TemplateData  
... TargetPlatformName  
RequiredPlatformVersion  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 Отсутствует.  
  
### <a name="attributes"></a>Атрибуты  
 Отсутствует.  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[TemplatePlatformName](../extensibility/templatedata-element-visual-studio-templates.md)|Задает платформу, для которой предназначен шаблон проекта.|  
  
## <a name="text-value"></a>Текстовое значение  
 Текстовое значение является обязательным.  
  
## <a name="remarks"></a>Примечания  
 Данный текст задает минимальную версию операционной системы для шаблона.  
  
## <a name="example"></a>Пример  
 В этом примере указывает, что предназначен шаблон проекта [!INCLUDE[win8](../includes/win8-md.md)] или более поздней версии.  
  
```xml  
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <TargetPlatformName>Windows</TargetPlatformName>  
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>  
  
    </TemplateData>  
    <TemplateContent>  
  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>См. также  
 [Элемент TargetPlatformName (шаблоны Visual Studio)](../extensibility/targetplatformname-element-visual-studio-templates.md)   
 [Создание шаблонов проектов и элементов](../ide/creating-project-and-item-templates.md)   
 [Справочник по схеме шаблонов Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
