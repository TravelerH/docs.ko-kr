---
title: <trace>에 대 한 <listeners>에 대 한 <filter> 요소 @no__t
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add/filter
helpviewer_keywords:
- initializeData attribute
- filter element for <add> for <listeners> for <trace>
- <filter> element for <add> for <listeners> for <trace>
ms.assetid: eb9c18f5-dfa8-47c5-b91b-e4b93e76e1cc
ms.openlocfilehash: f6b1ec99c5aab8e85df7f1920aca32f49a5be066
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699359"
---
# <a name="filter-element-for-add-for-listeners-for-trace"></a>@no__t에 대 한 \<filter > @no__t 요소 > @no__t에 대 한 > 추가 >-3trace
추적에 대 한 `Listeners` 컬렉션의 수신기에 필터를 추가 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<trace >** ](trace-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<listeners >** ](listeners-element-for-trace.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7[ **&nbsp;0 add >** ](add-element-for-listeners-for-trace.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 @ no__t-8 @ no__t-9 **&nbsp;1 filter >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<filter   
  type="traceFilterClassName"   
  initializeData="data" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`type`|필수 특성입니다.<br /><br /> @No__t-0 클래스에서 상속 해야 하는 필터의 유형을 지정 합니다. 형식의 네임 스페이스 정규화 된 이름을 사용할 수 있습니다 .이 이름은 형식의 <xref:System.Type.FullName%2A> 속성에 해당 하며, <xref:System.Type.AssemblyQualifiedName%2A> 속성에 해당 하는 어셈블리 정보를 포함 하 여 정규화 된 형식 이름을 사용할 수 있습니다. 정규화 된 형식 이름에 대 한 자세한 내용은 정규화 된 [형식 이름 지정](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)을 참조 하세요.|  
|`initializeData`|선택적 특성입니다.<br /><br /> 지정 된 필터 클래스의 생성자에 전달 된 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|`trace`|추적 메시지를 수집하고 저장하고 라우팅하는 수신기가 포함되어 있습니다.|  
|`listeners`|메시지를 수집, 저장 및 라우팅하는 수신기를 포함 합니다. 수신기는 추적 출력을 적절 한 대상으로 보냅니다.|  
|`add`|`Listeners` 컬렉션에 수신기를 추가합니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 요소는 [@no__t 3sharedListeners >](sharedlisteners-element.md)에 정의 된 수신기의 이름 뿐만 아니라 수신기의 형식을 지정 하는 추적 수신기의 `<add>` 요소에 포함 되어야 합니다. 수신기가 [\<sharedListeners >](sharedlisteners-element.md)에 정의 되어 있는 경우 해당 수신기의 필터를 해당 요소에 정의 해야 합니다.  
  
 이 요소는 컴퓨터 구성 파일 (machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `<filter>` 요소를 사용 하 여 추적에 대 한 `Listeners` 컬렉션의 @no__t 수신기에 필터를 추가 하 고 필터 이벤트 수준을 `Error`으로 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <add name="console"   
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"   
            initializeData="Error" />  
        </add>  
        <remove name="Default" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.TraceListener.Filter%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.TraceFilter>
- [추적 및 디버그 설정 스키마](index.md)
