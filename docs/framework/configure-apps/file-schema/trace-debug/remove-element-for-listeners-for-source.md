---
title: <source>의 <listeners>에 대 한 <remove> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/remove
helpviewer_keywords:
- remove element for <listeners> for <source>
- <remove> element for <listeners> for <source>
ms.assetid: 3ff6b578-273d-407f-b07f-8251f1f9f5d0
ms.openlocfilehash: 75db45d4e868ce88e030ec6a43c8bdaf788a1102
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74088848"
---
# <a name="remove-element-for-listeners-for-source"></a>\<원본에 대해 \<수신기 >에 대 한 > 요소를 제거 \<
추적 소스의 `Listeners` 컬렉션에서 수신기를 제거합니다.  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;[ **\<&nbsp;진단 >** ](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;\<[**원본**](sources-element.md) >
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<원본 >** ](source-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<수신기 >** ](listeners-element-for-source.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **&nbsp;&nbsp;\<** >

## <a name="syntax"></a>구문  
  
```xml  
<remove name="listenerName" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`name`|필수 특성입니다.<br /><br /> `Listeners` 컬렉션에서 제거할 수신기의 이름입니다.|  
  
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
 `<remove>` 요소는 추적 소스에 대 한 `Listeners` 컬렉션에서 지정 된 수신기를 제거 합니다.  
  
 <xref:System.Diagnostics.TraceSource> 인스턴스의 <xref:System.Diagnostics.TraceSource.Listeners%2A> 속성에서 <xref:System.Diagnostics.TraceListenerCollection.Remove%2A> 메서드를 호출 하 여 프로그래밍 방식으로 추적 소스에 대 한 `Listeners` 컬렉션에서 요소를 제거할 수 있습니다.  
  
 이 요소는 컴퓨터 구성 파일 (machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<add>` 요소를 사용 하 여 추적 소스 `TraceSourceApp`에 대 한 `Listeners` 컬렉션에 수신기 `console`를 추가 하기 전에 `<remove>` 요소를 사용 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch" >  
         <listeners>  
           <remove name="Default"/>  
           <add name="console"   
             type="System.Diagnostics.ConsoleTraceListener" />  
         </listeners>  
      </source>  
    </sources>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.TraceSource.Listeners%2A>
- <xref:System.Diagnostics.TraceSource>
- [추적 및 디버그 설정 스키마](index.md)
- [\<clear>](clear-element-for-listeners-for-source.md)
- [추적 수신기](../../../debug-trace-profile/trace-listeners.md)
