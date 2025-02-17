---
title: <basicHttpBinding>
ms.date: 03/30/2017
helpviewer_keywords:
- basicHttpBinding Element
ms.assetid: 85cf1a4f-26c2-48c7-bda6-6c960d5d3fb3
ms.openlocfilehash: b9d1e231bf2274f0df784feab26bc35a34ca772b
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398253"
---
# <a name="basichttpbinding"></a>\<basicHttpBinding>
WCF(Windows Communication Foundation) 서비스가 ASMX 기반 웹 서비스 및 클라이언트, 그리고 WS-I Basic Profile 1.1을 따르는 기타 서비스와 통신할 수 있는 엔드포인트를 구성 및 노출하는 데 사용할 수 있는 바인딩을 나타냅니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<바인딩 >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<basicHttpBinding >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<basicHttpBinding>
  <binding allowCookies="Boolean"
           bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           envelopeVersion="None/Soap11/Soap12"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxReceivedMessageSize="Integer"
           messageEncoding="Text/Mtom"
           name="String"
           openTimeout="TimeSpan"
           proxyAddress="URI"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
           useDefaultWebProxy="Boolean">
    <security mode="None/Transport/Message/TransportWithMessageCredential/TransportCredentialOnly">
      <transport clientCredentialType="None/Basic/Digest/Ntlm/Windows/Certificate"
                 proxyCredentialType="None/Basic/Digest/Ntlm/Windows"
                 realm="String" />
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               clientCredentialType="UserName/Certificate" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</basicHttpBinding>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|Description|  
|---------------|-----------------|  
|`allowCookies`|클라이언트가 쿠키를 수락하고 이를 앞으로의 요청에서 전파할지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 쿠키를 사용하는 ASMX 웹 서비스와 상호 작용할 때 이 속성을 사용할 수 있습니다. 그러면 서버에서 반환된 쿠키가 해당 서비스에 대한 이후의 모든 클라이언트 요청에 자동으로 복사되도록 할 수 있습니다.|  
|`bypassProxyOnLocal`|로컬 주소에 대해 프록시 서버를 사용하지 않을 것인지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.<br /><br /> 주소가 로컬인 인터넷 리소스는 로컬 리소스입니다. 로컬 주소는 동일한 컴퓨터, 로컬 LAN 또는 인트라넷에 있는 식별 되 면 구문적으로 제공 되지 않아 Uri와 같이 마침표 (.) " http://webserver/ "및" http://localhost/ "입니다.<br /><br /> 이 특성은 BasicHttpBinding으로 구성된 끝점이 로컬 리소스 액세스 시 프록시 서버를 사용할지 여부를 결정합니다. 이 특성이 `true`이면 로컬 인터넷 리소스에 대한 요청은 프록시 서버를 사용하지 않습니다. 이 특성이 `true`로 설정된 경우 클라이언트가 동일한 시스템의 서비스와 통신할 때 프록시를 통하게 하려면 localhost 대신 호스트 이름을 사용해야 합니다<br /><br /> 이 특성이 `false`이면 모든 인터넷 요청이 프록시 서버를 통해 이루어집니다.|  
|`closeTimeout`|닫기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`envelopeVersion`|이 바인딩에서 처리한 메시지에 사용되는 SOAP 버전을 지정합니다. 유효한 값은 Soap11뿐입니다.|  
|`hostNameComparisonMode`|URI 구문 분석에 사용되는 HTTP 호스트 이름 비교 모드를 지정합니다. 이 특성은 <xref:System.ServiceModel.HostNameComparisonMode> 형식이며 URI에 대해 비교할 때 호스트 이름이 서비스에 연결하는 데 사용되는지 여부를 나타냅니다. 기본값은 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>이며 이 값은 비교 시 호스트 이름을 무시합니다.|  
|`maxBufferPoolSize`|채널에서 메시지를 수신하는 메시지 버퍼 관리자가 사용하도록 할당된 최대 메모리를 지정하는 정수 값입니다. 기본값은 524288(0x80000)바이트입니다.<br /><br /> 버퍼 관리자는 버퍼 풀을 사용하여 버퍼 사용 비용을 최소화합니다. 버퍼는 메시지가 채널에서 나올 때 서비스를 이용하여 그 메시지를 처리해야 합니다. 버퍼 풀에 메시지 로드를 처리하기에 충분한 메모리가 없는 경우 버퍼 관리자는 CLR 힙으로부터 추가 메모리를 할당해야 하며, 이로 인해 가비지 컬렉션 오버헤드가 증가합니다. CLR 가비지 힙으로부터 다량의 할당이 이루어지는 경우 버퍼 풀 크기가 너무 작은 것이므로, 이 특성으로 지정된 제한을 늘려 더 크게 할당하면 성능이 향상될 수 있습니다.|  
|`maxBufferSize`|이 바인딩으로 구성된 엔드포인트에 대해 메시지가 처리되는 동안 해당 메시지를 저장하는 버퍼의 최대 크기(바이트)를 지정하는 정수 값입니다. 기본값은 65,536바이트입니다.|  
|`maxReceivedMessageSize`|이 바인딩으로 구성된 채널에서 받을 수 있는 메시지(헤더 포함)의 최대 메시지 크기(바이트)를 정의하는 양의 정수입니다. 수신자에게 너무 큰 메시지를 보낸 발신자에게는 SOAP 오류가 발생합니다. 수신자는 메시지를 삭제하고 추적 로그에 이벤트 항목을 만듭니다. 기본값은 65,536바이트입니다.|  
|`messageEncoding`|SOAP 메시지를 인코딩하는 데 사용되는 인코더를 정의합니다. 유효한 값은 다음과 같습니다.<br /><br /> 본문 텍스트 메시지 인코더를 사용 합니다.<br />Mtom MTOM (메시지 전송 조직 메커니즘) 1.0 인코더를 사용 합니다.<br /><br /> 기본값은 Text입니다. 이 특성은 <xref:System.ServiceModel.WSMessageEncoding> 형식입니다.|  
|`name`|바인딩의 구성 이름을 포함하는 문자열입니다. 이 값은 바인딩의 ID로 사용되므로 고유해야 합니다. 각 바인딩에는 서비스의 메타데이터에서 함께 바인딩을 고유하게 식별하는 `name` 및 `namespace` 특성이 있습니다. 또한 이 이름은 동일한 형식의 바인딩 간에 고유합니다. [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.|  
|`namespace`|바인딩의 XML 네임스페이스를 지정합니다. 기본값은 "http://tempuri.org/Bindings"입니다. 각 바인딩에는 서비스의 메타데이터에서 함께 바인딩을 고유하게 식별하는 `name` 및 `namespace` 특성이 있습니다.|  
|`openTimeout`|열기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`proxyAddress`|HTTP 프록시의 주소를 포함하는 URI입니다. `useSystemWebProxy`를 `true`로 설정할 경우 이 설정은 `null`이어야 합니다. 기본값은 `null`입니다.|  
|`receiveTimeout`|받기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:10:00입니다.|  
|`sendTimeout`|보내기 작업을 완료하기 위해 제공된 시간 간격을 지정하는 <xref:System.TimeSpan> 값입니다. 이 값은 <xref:System.TimeSpan.Zero>보다 크거나 같아야 합니다. 기본값은 00:01:00입니다.|  
|`textEncoding`|바인딩에서 메시지를 내보내는 데 사용되는 문자 집합 인코딩을 설정합니다. 유효한 값은 다음과 같습니다.<br /><br /> -   BigEndianUnicode: 유니코드가 나 Endian 인코딩입니다.<br />유니코드 16 비트 인코딩입니다.<br />-   UTF8: 8 비트 인코딩<br /><br /> 기본값은 UTF8입니다. 이 특성은 <xref:System.Text.Encoding> 형식입니다.|  
|`transferMode`|메시지가 요청 또는 응답에서 버퍼링되는지 또는 스트리밍되는지를 지정하는 유효한 <xref:System.ServiceModel.TransferMode> 값입니다.|  
|`useDefaultWebProxy`|시스템의 자동 구성된 HTTP 프록시가 있는 경우 이를 사용할지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|바인딩에 대한 보안 설정을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement> 형식입니다.|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|이 바인딩으로 구성된 엔드포인트에서 처리할 수 있는 SOAP 메시지의 복잡성에 대한 제약 조건을 정의합니다. 이 요소는 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> 형식입니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|이 요소는 표준 및 사용자 지정 바인딩의 컬렉션을 보유합니다.|  
  
## <a name="remarks"></a>설명  
 BasicHttpBinding은 SOAP 1.1 메시지를 보내기 위한 전송으로 HTTP를 사용합니다. 서비스는 이 바인딩을 사용하여 ASMX 클라이언트가 사용하는 엔드포인트와 같이 WS-I BP 1.1을 따르는 엔드포인트를 노출할 수 있습니다. 마찬가지로 클라이언트는 BasicHttpBinding을 사용하여 ASMX 웹 서비스 또는 BasicHttpBinding으로 구성된 서비스와 같이 WS-I BP 1.1을 따르는 엔드포인트를 노출하는 서비스와 통신할 수 있습니다.  
  
 보안은 기본적으로 해제 되어 있지만 [ \<보안 >](security-of-basichttpbinding.md) 자식 요소의 mode 특성을 이외의 `None`값으로 설정 하 여 추가할 수 있습니다. 이 요소는 기본적으로 "텍스트" 메시지 인코딩 및 UTF-8 텍스트 인코딩을 사용합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 첫 번째 및 두 번째 세대 웹 서비스와의 HTTP 통신 및 최대 상호 운용성을 제공하는 <xref:System.ServiceModel.BasicHttpBinding>의 사용 방법을 보여 줍니다. 클라이언트 및 서비스 구성 파일에 바인딩이 지정됩니다. 바인딩 형식은 `binding` 요소의 `<endpoint>` 특성을 사용하여 지정합니다. 기본 바인딩을 구성하고 일부 설정을 변경하려면 바인딩 구성을 정의해야 합니다. 엔드포인트는 서비스에 대한 다음 구성 코드에 표시된 것처럼 `bindingConfiguration` 요소의 `<endpoint>` 특성을 사용하여 이름으로 바인딩 구성을 참조해야 합니다.  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
      <binding name="Binding1"
               hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Text"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
## <a name="example"></a>예제  
 [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)]부터는 바인딩 및 동작에 이름이 필요하지 않습니다. 이전 예제의 기능은 끝점 주소에서 bindingConfiguration을 제거 하 고 바인딩에서 이름을 제거 하 여 수행할 수 있습니다.  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="basicHttpBinding"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
      <binding hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Text"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </basicHttpBinding>
  </bindings>
</system.serviceModel>
```  
  
 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [바인딩](../../../wcf/bindings.md)
- [시스템 제공 바인딩 구성](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](../../../misc/binding.md)
