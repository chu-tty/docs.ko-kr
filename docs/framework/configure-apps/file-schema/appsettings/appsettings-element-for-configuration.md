---
title: <appSettings>에 대한 <configuration> 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings
helpviewer_keywords:
- appSettings Element
- <appSettings> Element
ms.assetid: 39694cc4-6b84-45a6-9329-385a0d8b48fe
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6112d87afcca8b2f54508d03d3ea4c0781d7e475
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73119278"
---
# <a name="appsettings-element-for-configuration"></a>\<구성에 대 한 \<appSettings > 요소 >

사용자 지정 응용 프로그램 설정을 포함 합니다. .NET Framework에서 제공 하는 미리 정의 된 구성 섹션입니다.

[ **\<configuration>** ](../configuration-element.md)   
&nbsp;&nbsp; **\<appSettings>**

## <a name="syntax"></a>구문

```xml
<appSettings>
  <!-- Elements to add, clear, or remove configuration settings -->
</appSettings>
```

## <a name="attribute"></a>특성

|           | Description |
| --------- | ----------- |
| **file**  | 선택적 특성입니다.<br><br>사용자 지정 응용 프로그램 구성 설정이 포함 된 외부 파일에 대 한 상대 경로를 지정 합니다. 지정 된 파일에는 **> 추가\<** 에 지정 된 것과 동일한 종류의 설정이 포함 되어 있습니다. **>\<제거**하 고 **\<요소를 삭제 하 고 해당** 요소와 동일한 키/값 쌍 형식을 사용 합니다.<br><br>지정 된 경로는 기본 구성 파일을 기준으로 합니다. Windows Forms 응용 프로그램의 경우이 폴더는 응용 프로그램 구성 파일의 위치가 아니라 */so/debug*와 같은 이진 폴더입니다. Web Forms 응용 프로그램의 경우 경로는 *web.config* 파일이 있는 응용 프로그램 루트를 기준으로 합니다.<br><br>지정 된 파일을 찾을 수 없는 경우 런타임은 특성을 무시 합니다. |

## <a name="parent-element"></a>부모 요소

|     | Description |
| --- | ----------- |
| [ **\<구성 >** 요소인](../configuration-element.md) | 공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다. |

## <a name="child-elements"></a>자식 요소

|     | Description |
| --- | ----------- |
| [ **\<add>** ](add-element-for-appsettings.md) | 사용자 지정 응용 프로그램 설정을 추가 합니다. |
| [ **\<clear>** ](clear-element-for-appsettings.md) | 이전에 정의 된 모든 응용 프로그램 설정을 지웁니다. |
| [ **\<remove>** ](remove-element-for-appsettings.md) | 이전에 정의 된 응용 프로그램 설정을 제거 합니다. |

## <a name="remarks"></a>주의

**\<appSettings >** 요소는 데이터베이스 연결 문자열, 파일 경로, XML Web services url 또는 응용 프로그램에 대 한 기타 사용자 지정 구성 정보와 같은 사용자 지정 응용 프로그램 구성 정보를 저장 합니다. **\<appSettings >** 요소에 지정 된 키/값 쌍은 <xref:System.Configuration.ConfigurationSettings> 클래스를 사용 하 여 코드에서 액세스 됩니다.

*Web.config 및 응용* 프로그램 구성 파일의 **\<appSettings >** 요소에서 **file** 특성을 사용할 수 있습니다. 이 특성은 추가 설정을 제공 하거나 **\<appSettings >** 요소에 지정 된 설정을 재정의 하는 구성 파일을 지정 합니다. 사용자가 응용 프로그램 구성 파일에 지정 된 프로젝트 설정을 재정의 하려는 경우와 같이 소스 제어 팀 개발 시나리오에서 **file** 특성을 사용할 수 있습니다.

**File** 특성에 지정 된 구성 파일에는 **\<구성 >** 아닌 **\<appSettings >** 의 루트 노드가 있어야 합니다.

## <a name="example"></a>예제

다음 예제에서는 사용자 지정 애플리케이션 설정을 정의하는 외부 애플리케이션 설정 파일(*custom.config*)을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<appSettings>
  <add key="MyCustomSetting" value="MyCustomSettingValue" />
</appSettings>
```

다음 예제에서는 외부 설정 파일의 설정을 사용하고 자체의 애플리케이션 설정을 지정하는 애플리케이션 구성 파일을 보여 줍니다.

```xml
<configuration>
  <appSettings file="custom.config">
    <add key="ApplicationName" value="MyApplication" />
  </appSettings>
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일 *, 컴퓨터 구성 파일 (machine.config*) 및 응용 프로그램 디렉터리 수준에 없는 *web.config 파일* 에서 사용할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [.NET Framework에 대 한 구성 파일 스키마](../index.md)
