---
title: API 게이트웨이 패턴과 클라이언트-마이크로 서비스 간 직접 통신
description: API 게이트웨이 패턴과 클라이언트-마이크로 서비스 간 직접 통신의 차이점 및 사용법을 이해합니다.
ms.date: 01/07/2019
ms.openlocfilehash: 6b42650b2dbce093f12fe02b1605c95076dc8592
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72522954"
---
# <a name="the-api-gateway-pattern-versus-the-direct-client-to-microservice-communication"></a>API 게이트웨이 패턴과 클라이언트-마이크로 서비스 간 직접 통신

마이크로 서비스 아키텍처에서 각 마이크로 서비스는 일반적으로 미세 엔드포인트의 집합을 노출합니다. 이 사실은 이 섹션에 설명된 대로 클라이언트-마이크로 서비스 간 통신에 영향을 줄 수 있습니다.

## <a name="direct-client-to-microservice-communication"></a>클라이언트-마이크로 서비스 간 직접 통신

가능한 방법은 클라이언트-마이크로 서비스 간 직접 통신 아키텍처를 사용하는 것입니다. 이 방법에서 클라이언트 앱은 그림 4-12에 나와 있는 것처럼 일부 마이크로 서비스에 직접 요청을 만듭니다.

![클라이언트-마이크로 서비스 간 통신 아키텍처를 보여 주는 다이어그램입니다.](./media/direct-client-to-microservice-communication.png)

**그림 4-12**. 클라이언트-마이크로 서비스 간 직접 통신 아키텍처 사용

이 방식에서는 각 마이크로 서비스에 공용 엔드포인트가 있으며 경우에 따라 각 마이크로 서비스에 대해 다른 TCP 포트가 있을 수 있습니다. 특정 서비스에 대한 URL의 예는 Azure에서 다음 URL을 참조하세요.

`http://eshoponcontainers.westus.cloudapp.azure.com:88/`

클러스터에 기반한 프로덕션 환경에서는 해당 URL이 클러스터에서 사용되는 부하 분산 장치에 매핑하고, 이어서 요청을 마이크로 서비스에 분산하게 됩니다. 프로덕션 환경에서는 마이크로 서비스와 인터넷 사이에 [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction)와 같은 ADC(애플리케이션 배달 컨트롤러)를 사용할 수 있습니다. 이는 부하 분산을 수행할 뿐 아니라 SSL 종료를 제공하여 서비스를 보호하는 투명한 계층으로 작동합니다. 이는 CPU 집중적 SSL 종료 및 Azure Application Gateway로의 라우팅 듀티를 오프로딩하여 호스트의 로드를 증가시킵니다. 어떤 경우든 부하 분산 장치 및 ADC는 논리적 애플리케이션 아키텍처 관점에서 투명합니다.

클라이언트-마이크로 서비스 간 직접 통신 아키텍처는 소규모 마이크로 서비스 기반 애플리케이션에, 특히 클라이언트 앱이 ASP.NET MVC 앱과 같은 서버 쪽 웹 애플리케이션인 경우에 적합합니다. 그러나 대규모 또는 복잡한 마이크로 서비스 기반 애플리케이션을 빌드할 때(예: 마이크로 서비스 형식을 수십 번 처리하는 경우), 그리고 특히 클라이언트 앱이 원격 모바일 앱 또는 SPA 웹 애플리케이션인 경우에는 해당 방식에 몇 가지 문제가 있습니다.

마이크로 서비스 기반의 대규모 애플리케이션을 개발할 때 다음과 같은 질문을 고려합니다.

- *클라이언트 앱이 백 엔드에 대한 요청 수를 최소화하고 여러 마이크로 서비스에 대한 번거로운 통신을 줄이려면 어떻게 해야 할까요?*

여러 마이크로 서비스와 상호 작용하여 단일 UI 화면을 빌드하면 인터넷에서 왕복 수가 증가합니다. 그러면 대기 시간 및 UI 쪽 복잡성이 증가합니다. 이상적으로 응답은 서버 쪽에서 효율적으로 집계됩니다. 이렇게 하면 여러 데이터 조각이 동시에 돌아오고 일부 UI가 준비되는 즉시 데이터를 표시하기 때문에 대기 시간이 줄어듭니다.

- *권한 부여, 데이터 변환 및 동적 요청 디스패치와 같은 교차 편집 문제를 처리하려면 어떻게 해야 할까요?*

모든 마이크로 서비스의 보안 및 권한 부여와 같은 보안 및 교차 편집 문제를 구현하려면 상당한 개발 노력이 필요할 수 있습니다. 가능한 방법은 해당 서비스를 Docker 호스트 또는 내부 클러스터 내에 두는 것입니다. 이렇게 하면 외부에서 직접 마이크로 서비스에 액세스할 수 없으며 교차 편집 문제를 API 게이트웨이와 같은 한곳에서 구현할 수 있습니다.

- *클라이언트 앱이 인터넷 친화적이 아닌 프로토콜을 사용하는 서비스와 통신하려면 어떻게 해야 할까요?*

서버 쪽에서 사용되는 프로토콜(예: AMQP 또는 이진 프로토콜)은 일반적으로 클라이언트 앱에서 지원되지 않습니다. 따라서 요청은 HTTP/HTTPS와 같은 프로토콜을 통해 수행되고 나중에 다른 프로토콜로 변환해야 합니다. *메시지 가로채기(man-in-the-middle)* 방식은 이 경우 도움이 될 수 있습니다.

- *모바일 앱에 대해 특별히 만든 외관을 셰이핑하려면 어떻게 해야 할까요?*

여러 마이크로 서비스의 API는 다른 클라이언트 애플리케이션의 요구 사항에 적합하지 않게 디자인되었을 수 있습니다. 예를 들어 모바일 앱의 요구는 웹앱의 요구와 다를 수 있습니다. 모바일 앱의 경우 데이터 응답이 더 효율적일 수 있도록 더욱 최적화해야 할 수 있습니다. 이는 여러 마이크로 서비스에서 데이터를 집계하고, 단일 데이터 세트를 반환하며, 경우에 따라 모바일 앱에 필요하지 않은 응답의 모든 데이터를 제거하여 수행할 수 있습니다. 또한 물론 해당 데이터를 압축할 수도 있습니다. 다시 한 번 언급하지만, 모바일 앱과 마이크로 서비스 간 외관 또는 API는 이 시나리오에 편리할 수 있습니다.

## <a name="why-consider-api-gateways-instead-of-direct-client-to-microservice-communication"></a>클라이언트-마이크로 서비스 간 직접 통신 대신 API 게이트웨이를 고려하는 이유

마이크로 서비스 아키텍처에서 클라이언트 앱은 일반적으로 둘 이상의 마이크로 서비스에서 제공하는 기능을 사용해야 합니다. 해당 사용이 직접 실행되는 경우 클라이언트는 마이크로 서비스 엔드포인트에 대한 여러 호출을 처리해야 합니다. 애플리케이션이 개선되고 새 마이크로 서비스가 도입되었거나 기존 마이크로 서비스가 업데이트되면 어떻게 되나요? 애플리케이션에 여러 마이크로 서비스가 있는 경우 클라이언트 앱에서 많은 엔드포인트를 처리하는 것은 큰 문제일 수 있습니다. 클라이언트 앱은 해당 내부 엔드포인트에 결합되므로 나중에 마이크로 서비스가 개선되면 클라이언트 앱에 큰 영향을 줄 수 있습니다.

따라서 중간 수준 또는 간접 참조 계층(게이트웨이)을 포함하면 마이크로 서비스 기반 애플리케이션의 경우 매우 편리할 수 있습니다. API 게이트웨이가 없는 경우 클라이언트 앱은 마이크로 서비스로 직접 요청을 보내야 하는데 이 경우 다음과 같은 문제가 발생합니다.

- **결합**: API 게이트웨이 패턴이 없으면 클라이언트 앱은 내부 마이크로 서비스에 결합됩니다. 클라이언트 앱은 애플리케이션의 여러 영역이 마이크로 서비스에서 어떻게 분해되는지 알아야 합니다. 내부 마이크로 서비스를 개선하고 리팩터링할 경우 클라이언트 앱에서 내부 마이크로 서비스를 직접 참조하기 때문에 클라이언트 앱이 크게 변경되므로 해당 작업은 유지 관리에 나쁜 영향을 줍니다. 클라이언트 앱을 자주 업데이트해야 하므로 솔루션을 개선하기가 더 어렵습니다.

- **너무 많은 왕복**: 클라이언트 앱의 단일 페이지/화면에서 여러 서비스를 몇 번 호출해야 할 수 있습니다. 이로 인해 클라이언트와 서버 간에 여러 번의 네트워크 왕복이 발생할 수 있어 대기 시간이 상당히 늘어납니다. 중간 수준에서 처리되는 집계는 클라이언트 앱의 성능과 사용자 환경을 향상할 수 있습니다.

- **보안 문제**: 게이트웨이가 없으면 모든 마이크로 서비스가 "외부 세계"에 노출되어야 하므로 클라이언트 앱에서 직접 사용되지 않는 내부 마이크로 서비스를 숨길 경우보다 더 큰 공격 표면이 생성됩니다. 공격 표면이 작을수록 애플리케이션을 더 안전하게 보호할 수 있습니다.

- **교차 편집 문제**: 공개적으로 게시된 각 마이크로 서비스는 권한 부여, SSL 등의 문제를 처리해야 합니다. 대부분의 경우 이러한 문제는 단일 계층에서 처리할 수 있으므로 내부 마이크로 서비스가 간소화됩니다.

## <a name="what-is-the-api-gateway-pattern"></a>API 게이트웨이 패턴이란?

여러 클라이언트 앱이 있는 대규모 또는 복잡한 마이크로 서비스 기반 애플리케이션을 디자인하고 빌드하는 경우 [API 게이트웨이](https://microservices.io/patterns/apigateway.html)가 고려할 좋은 방법일 수 있습니다. 이는 마이크로 서비스의 특정 그룹에 단일 진입점을 제공하는 서비스입니다. 개체 지향 디자인의 [외관 패턴](https://en.wikipedia.org/wiki/Facade_pattern)과 유사하지만 이 경우에는 분산된 시스템의 일부입니다. 또한 클라이언트 앱의 요구 사항을 고려하면서 빌드하였기 때문에 API 게이트웨이 패턴을 "[BFF](https://samnewman.io/patterns/architectural/bff/)(프런트 엔드의 백 엔드)"라고도 합니다.

따라서 API 게이트웨이는 클라이언트 앱과 마이크로 서비스 사이에 위치합니다. 클라이언트에서 서비스로 요청을 라우팅하는 역방향 프록시로 사용됩니다. 또한 인증, SSL 종료 및 캐시와 같은 추가 교차 편집 기능을 제공할 수 있습니다.

그림 4-13에 사용자 지정 API 게이트웨이가 어떻게 몇몇 마이크로 서비스만 사용하여 간소화된 마이크로 서비스 기반 아키텍처에 적합한지가 나와 있습니다.

![사용자 지정 서비스로 구현된 API 게이트웨이를 보여 주는 다이어그램입니다.](./media/direct-client-to-microservice-communication-versus-the-API-Gateway-pattern/custom-service-api-gateway.png)

**그림 4-13**. 사용자 지정 서비스로 구현된 API 게이트웨이 사용

앱은 개별 마이크로 서비스에 요청을 전달하도록 구성된 단일 엔드포인트인 API 게이트웨이에 연결합니다. 이 예제에서는 API 게이트웨이가 컨테이너로 실행 중인 사용자 지정 ASP.NET Core WebHost 서비스로 구현됩니다.

해당 다이어그램에서 여러 다른 클라이언트 앱에 연결한 단일 사용자 지정 API 게이트웨이 서비스를 사용한다는 점을 강조해야 합니다. 사용자의 API 게이트웨이 서비스는 클라이언트 앱의 다양하고 많은 요구 사항을 기반으로 늘어나고 진화하므로 그러한 사실은 중요한 위험입니다. 결국 이러한 다른 요구 사항으로 인해 너무 커지면 사실상 모놀리식 애플리케이션 또는 모놀리식 서비스와 상당히 비슷할 수 있습니다. 예를 들어 API 게이트웨이를 여러 서비스 또는 더 작은 여러 API 게이트웨이로 클라이언트 앱 양식 팩터 형식당 하나씩 분할하는 것이 좋습니다.

API 게이트웨이 패턴을 구현할 때는 주의해야 합니다. 일반적으로 단일 API 게이트웨이가 애플리케이션의 모든 내부 마이크로 서비스를 집계하도록 하지 않는 것이 좋습니다. 그렇지 않으면 모놀리식 집계 또는 오케스트레이터로 동작하며 모든 마이크로 서비스를 연결하여 마이크로 서비스 자치를 위반합니다.

따라서 API 게이트웨이는 비즈니스 경계 및 클라이언트 앱을 기준으로 분리되어야 하며, 모든 내부 마이크로 서비스에서 단일 집계로 작동하지 않아야 합니다.

API 게이트웨이 계층을 여러 API 게이트웨이로 분할하면 애플리케이션에 여러 개의 클라이언트 앱이 있는 경우 해당 애플리케이션은 여러 API 게이트웨이 형식을 식별할 때 기본 피벗일 수 있으므로 각 클라이언트 앱의 요구 사항에 대해 다른 외관이 포함될 수 있습니다. 이 경우의 패턴을 [BFF](https://samnewman.io/patterns/architectural/bff/)("프런트 엔드의 백 엔드")라고 합니다. 다음 이미지에 표시된 대로 이 패턴에서 각 API 게이트웨이는 여러 내부 마이크로 서비스의 호출 아래에 있는 특정 어댑터 코드를 구현하여 클라이언트 양식 팩터를 기반으로 각 클라이언트 앱에 맞춰진 다른 API를 제공할 수 있습니다.

![여러 사용자 지정 API 게이트웨이를 보여 주는 다이어그램입니다.](./media/direct-client-to-microservice-communication-versus-the-API-Gateway-pattern/multiple-custom-api-gateways.png)

**그림 4-13.1**. 여러 사용자 지정 API 게이트웨이 사용

그림 4-13.1은 클라이언트 유형에 따라 분리되는 API 게이트웨이를 보여줍니다. 하나는 모바일 클라이언트 용이고, 다른 하나는 웹 클라이언트용입니다. 기존 웹앱은 웹 API 게이트웨이를 사용하는 MVC 마이크로 서비스에 연결합니다. 이 예제는 여러 세분화된 API 게이트웨이가 있는 간소화된 아키텍처를 나타냅니다. 이 경우에 각 API 게이트웨이에 대해 식별된 경계는 순수하게 [BFF](https://samnewman.io/patterns/architectural/bff/)("프런트 엔드의 백 엔드") 패턴을 기반으로 하므로 클라이언트 앱당 필요한 API에만 기반합니다. 그러나 더 큰 애플리케이션에서는 더 나아가 비즈니스 경계를 기반으로 추가 API 게이트웨이를 두 번째 피벗으로 만들어야 합니다.

## <a name="main-features-in-the-api-gateway-pattern"></a>API 게이트웨이 패턴의 주요 기능

API 게이트웨이는 여러 기능을 제공할 수 있습니다. 제품에 따라 더 풍부하거나 더 단순한 기능을 제공할 수 있지만 API 게이트웨이의 가장 중요하고 기본적인 기능은 다음 디자인 패턴입니다.

**역방향 프록시 또는 게이트웨이 라우팅** API 게이트웨이는 요청(계층 7 라우팅, 일반적으로 HTTP 요청)을 내부 마이크로 서비스의 엔드포인트로 리디렉션 또는 라우팅하는 역방향 프록시를 제공합니다. 게이트웨이는 클라이언트 앱에 대한 단일 엔드포인트 또는 URL을 제공한 후 내부적으로 요청을 내부 마이크로 서비스 그룹에 매핑합니다. 이 라우팅 기능은 마이크로 서비스에서 클라이언트 앱을 분리하는 데 도움이 될 뿐만 아니라, 모놀리식 API와 클라이언트 앱 사이에 API 게이트웨이를 배치하여 모놀리식 API를 현대화하는 경우 매우 편리하기도 합니다. 그런 다음, 나중에 여러 마이크로 서비스로 분할될 때까지 레거시 모놀리식 API를 계속 사용하면서 새 API를 새 마이크로 서비스로 추가할 수 있습니다. API 게이트웨이 때문에 클라이언트 앱은 사용 중인 API가 내부 마이크로 서비스 또는 모놀리식 API로 구현되는지를 인식하지 못합니다. 더 중요한 것은 모놀리식 API를 마이크로 서비스로 개선하고 리팩터링할 경우 API 게이트웨이 라우팅 덕분에 클라이언트 앱은 URI 변경 내용에 영향을 받지 않습니다.

자세한 내용은 [게이트웨이 라우팅 패턴](https://docs.microsoft.com/azure/architecture/patterns/gateway-routing)을 참조하세요.

**요청 집계** 게이트웨이 패턴의 일부로 여러 내부 마이크로 서비스를 대상으로 하는 여러 클라이언트 요청(대개 HTTP 요청)을 단일 클라이언트 요청으로 집계할 수 있습니다. 이 패턴은 특히 클라이언트 페이지/화면에 여러 마이크로 서비스의 정보가 필요할 때 편리합니다. 이 방법을 사용하면 클라이언트 앱은 여러 요청을 내부 마이크로 서비스에 디스패치한 다음, 결과를 집계하고 모든 것을 다시 클라이언트 앱에 보내는 API 게이트웨이에 단일 요청을 보냅니다. 이 디자인 패턴의 주요 이점과 목표는 클라이언트 앱과 백 엔드 API 간에 통신량을 줄이는 것이고, 이는 특히 클라이언트 원격 브라우저의 JavaScript에서 시작되는 SPA 앱에서 생성되는 요청 또는 모바일 앱처럼 마이크로 서비스가 상주하는 데이터 센터에서 생성되는 원격 앱에 중요합니다. 서버 환경(예: ASP.NET Core MVC 웹앱)에서 요청을 수행하는 일반 웹앱의 경우 대기 시간이 원격 클라이언트 앱보다 훨씬 더 작으므로 이 패턴이 중요하지 않습니다.

사용하는 API 게이트웨이 제품에 따라 이 집계를 수행할 수 있습니다. 그러나 대부분의 경우 API 게이트웨이의 범위에서 집계 마이크로 서비스를 만드는 것이 더 유연하므로 코드(즉, C# 코드)에서 집계를 정의합니다.

자세한 내용은 [게이트웨이 집계 패턴](https://docs.microsoft.com/azure/architecture/patterns/gateway-aggregation)을 참조하세요.

**교차 편집 문제 또는 게이트웨이 오프로딩** 각 API 게이트웨이 제품에서 제공하는 기능에 따라 개별 마이크로 서비스에서 게이트웨이로 기능을 오프로드하면 교차 편집 문제를 한 계층으로 통합하여 각 마이크로 서비스의 구현을 간소화할 수 있습니다. 이 방법은 특히 다음 기능과 같이 모든 내부 마이크로 서비스에서 적절하게 구현하기에 복잡할 수 있는 특수 기능에 편리합니다.

- 인증 및 권한 부여
- 서비스 검색 통합
- 응답 캐싱
- 정책, 회로 차단기 및 QoS 다시 시도
- 속도 제한
- 부하 분산
- 로깅, 추적, 상관 관계
- 헤더, 쿼리 문자열 및 청구 변환
- IP 허용 목록

자세한 내용은 [게이트웨이 오프로딩 패턴](https://docs.microsoft.com/azure/architecture/patterns/gateway-offloading)을 참조하세요.

## <a name="using-products-with-api-gateway-features"></a>API 게이트웨이 기능이 있는 제품 사용

각 구현에 따라 API 게이트웨이 제품에서 제공되는 더욱 많은 교차 편집 문제가 있을 수 있습니다. 여기에서 살펴봅니다.

- [Azure API Management](https://azure.microsoft.com/services/api-management/)
- [Ocelot](https://github.com/ThreeMammals/Ocelot)

### <a name="azure-api-management"></a>Azure API Management

그림 4-14에 표시된 대로 [Azure API Management](https://azure.microsoft.com/services/api-management/)는 API 게이트웨이 요구 사항을 해결할 뿐만 아니라 API에서 인사이트를 수집하는 등의 기능을 제공합니다. API 관리 솔루션을 사용하는 경우 API 게이트웨이는 해당 전체 API 관리 솔루션 내의 구성 요소입니다.

![Azure API Management를 API 게이트웨이로 사용하는 방법을 보여 주는 다이어그램입니다.](./media/direct-client-to-microservice-communication-versus-the-API-Gateway-pattern/api-gateway-azure-api-management.png)

**그림 4-14**. API 게이트웨이에 Azure API Management 사용

Azure API Management에서는 로깅, 보안, 계량 등 API 게이트웨이 및 관리 요구를 모두 해결합니다. 이 경우 Azure API Management와 같은 제품을 사용할 때, 단일 API 게이트웨이가 있을 수도 있다는 사실은 그리 위험하지 않습니다. 이러한 API 게이트웨이 유형은 “더 가볍기” 때문에, 즉 모놀리식 구성 요소로 진화할 수도 있는 사용자 지정 C# 코드를 구현하지 않기 때문입니다. 

API 게이트웨이 제품은 일반적으로 통신 진입을 위한 역방향 프록시와 더 비슷하게 작동합니다. 또한 여기서는 내부 마이크로 서비스에서 API를 필터링하고, 이 단일 계층에 게시된 API에 권한을 적용할 수 있습니다.

API Management 시스템에서 사용할 수 있는 정보는 API가 사용되는 방식과 수행되는 방식을 이해하는 데 유용합니다. 유사한 실시간 분석 보고서를 볼 수 있으며 비즈니스에 영향을 줄 수 있는 추세를 식별하여 이를 수행합니다. 또한 요청 및 응답 작업에 관한 로그를 향후 온라인 및 오프라인 분석을 위해 보유할 수 있습니다.

Azure API Management를 통해 키, 토큰 및 IP 필터링을 사용하여 API를 보호할 수 있습니다. 이러한 기능을 사용하면 유연하고 세분화된 할당량 및 속도 제한이 가능하며, 정책을 사용하여 API의 모양과 동작을 수정하고, 응답 캐싱을 통해 성능을 향상시킬 수 있습니다.

이 가이드 및 참조 샘플 애플리케이션(eShopOnContainers)에서 아키텍처는 Azure API Management와 같은 PaaS 제품을 사용하지 않고 일반 컨테이너에 집중할 수 있도록 더 간단하고 사용자 지정한 컨테이너화된 아키텍처로 제한됩니다. 하지만 Microsoft Azure에 배포되는 더 큰 규모의 마이크로 서비스 기반 애플리케이션의 경우 프로덕션에서 API 게이트웨이를 위한 기준으로 Azure API Management를 평가하는 것이 좋습니다.

### <a name="ocelot"></a>Ocelot

[Ocelot](https://github.com/ThreeMammals/Ocelot)은 더 간단한 방법으로 사용하는 API 게이트웨이입니다. Ocelot은 시스템에 대한 통합된 진입점이 필요한 마이크로 서비스 아키텍처용으로 특별히 만들어진 오픈 소스 .NET Core 기반 API 게이트웨이입니다. 간단하고 빠르고 확장 가능하며 다양한 기능과 함께 라우팅 및 인증을 제공합니다.

[eShopOnContainers 참조 애플리케이션](https://github.com/dotnet-architecture/eShopOnContainers)에서 Ocelot을 선택하는 주요 원인은 Ocelot이 Docker Host, Kubernetes 등의 마이크로서비스/컨테이너를 배포하는 것과 동일한 애플리케이션 배포 환경에 배포할 수 있는 .NET Core 기반의 간단한 API 게이트웨이이기 때문입니다. 또한 .NET Core를 기반으로 하므로 Linux 또는 Windows에 배포할 수 있는 플랫폼 간 API 게이트웨이입니다.

컨테이너에서 실행되는 사용자 지정 API 게이트웨이를 보여 주는 이전 다이어그램은 컨테이너 및 마이크로 서비스 기반 애플리케이션에서 Ocelot을 실행하는 방법과 동일합니다.

또한 Apigee, Kong, MuleSoft, WSO2 및 서비스 메시 수신 컨트롤러 기능을 위한 기타 제품(예: Linkerd 및 Istio)과 같이 API 게이트웨이 기능을 제공하는 다양한 제품이 출시되어 있습니다.

초기 아키텍처 및 패턴 설명 섹션 뒤에 다음 섹션에서는 [Ocelot](https://github.com/ThreeMammals/Ocelot)을 사용하여 API 게이트웨이를 구현하는 방법을 설명합니다.

## <a name="drawbacks-of-the-api-gateway-pattern"></a>API 게이트웨이 패턴의 단점

- 가장 중요한 단점은 API 게이트웨이를 구현할 때 해당 계층을 내부 마이크로 서비스와 결합한다는 것입니다. 이와 같은 결합으로 인해 애플리케이션에 심각한 문제가 발생할 수 있습니다. Azure Service Bus 팀의 아키텍트인 Clemens Vaster는 GOTO 2016의 "[메시징 및 마이크로 서비스](https://www.youtube.com/watch?v=rXi5CLjIQ9k)" 세션에서 이 잠재적 문제점을 "새로운 ESB"라고 언급했습니다.

- 마이크로 서비스 API 게이트웨이를 사용하면 가능한 추가 단일 실패 지점이 만들어집니다.

- API 게이트웨이는 추가 네트워크 호출로 인해 응답 시간 증가로 이어질 수 있습니다. 그러나 이 추가 호출은 클라이언트 인터페이스가 일반적으로 내부 마이크로 서비스를 너무 빈번하게 직접 호출하는 것보다는 적은 영향을 미칩니다.

- 제대로 스케일 아웃하지 않으면 API 게이트웨이는 병목 상태가 될 수 있습니다.

- 사용자 지정 논리 및 데이터 집계를 포함하는 경우 API 게이트웨이는 추가 개발 비용 및 향후 유지 관리가 필요합니다. 개발자는 각 마이크로 서비스의 엔드포인트를 노출하기 위해 API 게이트웨이를 업데이트해야 합니다. 또한 내부 마이크로 서비스의 구현 변경은 API 게이트웨이 수준의 코드 변경으로 이어질 수 있습니다. 그러나 API 게이트웨이가 보안, 로깅 및 버전 관리에만 적용하는 경우(Azure API Management를 사용할 때) 이 추가 개발 비용은 적용되지 않을 수 있습니다.

- API 게이트웨이가 단일 팀에서 개발된 경우 개발 병목 상태가 있을 수 있습니다. 이것이 다양한 클라이언트 요구 사항에 응답하는 세분화된 API 게이트웨이가 여러 개인 것이 더 나은 방법인 또 다른 이유입니다. 또한 내부 마이크로 서비스에서 작업 중인 다른 팀에서 소유하는 여러 영역 또는 레이어로 API 게이트웨이를 내부적으로 구분할 수도 있습니다.

## <a name="additional-resources"></a>추가 자료

- **Chris Richardson. 패턴: API 게이트웨이/프런트 엔드의 백 엔드** \
  <https://microservices.io/patterns/apigateway.html>

- **API 게이트웨이 패턴** \
  <https://docs.microsoft.com/azure/architecture/microservices/gateway>

- **집계 및 컴퍼지션 패턴** \
  <https://microservices.io/patterns/data/api-composition.html>

- **Azure API Management** \
  <https://azure.microsoft.com/services/api-management/>

- **Udi Dahan. 서비스 지향 컴퍼지션** \
  <http://udidahan.com/2014/07/30/service-oriented-composition-with-video/>

- **Clemens Vasters. GOTO 2016의 메시징 및 마이크로 서비스(비디오)**  \
  <https://www.youtube.com/watch?v=rXi5CLjIQ9k>

- **간단한 API 게이트웨이**(ASP.NET Core API 게이트웨이 자습서 시리즈) \
  <https://www.pogsdotnet.com/2018/08/api-gateway-in-nutshell.html>

>[!div class="step-by-step"]
>[이전](identify-microservice-domain-model-boundaries.md)
>[다음](communication-in-microservice-architecture.md)
