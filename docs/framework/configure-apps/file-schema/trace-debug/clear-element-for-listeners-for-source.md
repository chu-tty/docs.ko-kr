---
title: <source>의 <listeners>에 대 한 <clear> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/clear
helpviewer_keywords:
- <clear> element for <listeners> for <source>
- clear element for <listeners> for <source>
ms.assetid: 76796bb2-9c0b-4526-8135-8bf18b16d8d9
ms.openlocfilehash: 4567f236397435e89371ca4c80730ff964fddd21
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74088928"
---
# <a name="clear-element-for-listeners-for-source"></a>\<소스에 대 한 \<수신기 >에 대해 clear > 요소를 \<
추적 소스의 `Listeners` 컬렉션을 지웁니다.  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;[ **\<&nbsp;진단 >** ](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;\<[**원본**](sources-element.md) >
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<원본 >** ](source-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<수신기 >** ](listeners-element-for-source.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;\<**clear >**

## <a name="syntax"></a>구문  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음.  
  
### <a name="child-elements"></a>자식 요소  
 없음.  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|`sources`|추적 메시지를 시작하는 추적 소스가 포함되어 있습니다.|  
|`source`|추적 메시지를 시작하는 추적 소스를 지정합니다.|  
|`listeners`|메시지를 수집, 저장 및 라우팅하는 수신기를 지정 합니다.|  
  
## <a name="remarks"></a>주의  
 `<clear>` 요소는 <xref:System.Diagnostics.DefaultTraceListener>를 포함 하 여 추적 소스에 대 한 `Listeners` 컬렉션에서 모든 수신기를 제거 합니다. `<add>` 요소를 사용 하기 전에 `<clear>` 요소를 사용 하 여 컬렉션에 다른 활성 수신기가 없음을 확신할 수 있습니다.  
  
## <a name="configuration-file"></a>구성 파일  
 이 요소는 컴퓨터 구성 파일 (machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<add>` 요소를 사용 하 여 수신기 `console`를 추가 하 고 추적 소스 `Listeners`에 대 한 `TraceSourceApp`컬렉션에 `textListener`를 추가 하기 전에 `<clear>` 요소를 사용 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
       <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <clear/>  
          <add name="console"   
            type="System.Diagnostics.ConsoleTraceListener"/>  
          <add name="textListener"/>  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"   
        type="System.Diagnostics.TextWriterTraceListener"   
        initializeData="myListener.log"/>  
    </sharedListeners>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TraceListener>
- [추적 및 디버그 설정 스키마](index.md)
- [추적 수신기](../../../debug-trace-profile/trace-listeners.md)
