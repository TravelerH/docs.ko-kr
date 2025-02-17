---
title: 기존 웹앱 및 단일 페이지 앱 중에서 선택
description: 웹 애플리케이션을 구축하는 경우 기존 웹 앱과 SPA(단일 페이지 애플리케이션) 중에서 선택하는 방법을 알아봅니다.
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: d68c167dce791a31eeb5ca5729b50ec22c64f9b0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675480"
---
# <a name="choose-between-traditional-web-apps-and-single-page-apps-spas"></a>기존 웹앱 및 SPA(단일 페이지 앱) 중에서 선택

> "Atwood의 법칙: JavaScript로 작성할 수 있는 모든 애플리케이션은 결국 JavaScript로 작성됩니다."  
> _\- Jeff Atwood_

오늘날 웹 애플리케이션을 빌드하는 방법은 일반적으로 두 가지가 있습니다. 서버에서 대부분의 애플리케이션 논리를 수행하는 기존 웹 애플리케이션과 웹 브라우저에서 대부분의 사용자 인터페이스 논리를 수행하며 기본적으로 웹 API를 사용하여 웹 서버와 통신하는 SPA(단일 페이지 애플리케이션)가 바로 그것입니다. 혼합 방식도 가능합니다. 가장 간단한 방법은 더 큰 기존 웹 애플리케이션 내에서 하나 이상의 풍부한 SPA와 같은 하위 애플리케이션을 호스트하는 것입니다.

다음과 같은 경우 기존 웹 애플리케이션을 사용해야 합니다.

- 애플리케이션의 클라이언트 쪽 요구 사항이 단순하거나 읽기 전용인 경우

- JavaScript를 지원하지 않는 브라우저에서 애플리케이션이 작동해야 하는 경우

- 팀이 JavaScript 또는 TypeScript 개발 기술에 익숙하지 않은 경우

다음과 같은 경우 SPA를 사용해야 합니다.

- 애플리케이션이 다양한 기능을 갖춘 풍부한 사용자 인터페이스를 노출해야 하는 경우

- 팀이 JavaScript 및/또는 TypeScript 개발에 익숙한 경우

- 애플리케이션이 다른(내부 또는 공용) 클라이언트용 API를 이미 노출해야 하는 경우

또한 SPA 프레임워크에는 보다 큰 아키텍처 및 보안 전문 지식이 필요합니다. 기존 웹 애플리케이션보다 잦은 업데이트 및 새 프레임워크로 인한 큰 변동이 있을 수 있습니다. 자동화된 빌드 및 배포 프로세스를 구성하고 컨테이너와 같은 배포 옵션을 활용하는 방법은 기존 웹앱보다 SPA 애플리케이션이 더 어렵습니다.

SPA 모델 덕분에 향상된 사용자 경험을 이러한 고려 사항과 비교해서 검토해야 합니다.

## <a name="blazor"></a>Blazor

ASP.NET Core 3.0에서는 Blazor라는 풍부하고 구성 가능한 대화형 UI를 빌드하는 새 모델을 제공합니다. 서버 측 Blazor를 사용하면 개발자가 서버에서 Razor를 사용하여 UI를 빌드하고, 이 코드를 브라우저에 전달하여 WebAssembly라는 JavaScript 라이브러리를 사용하여 클라이언트 쪽에서 실행되게 할 수 있습니다. ASP.NET Core 3.0은 아직 개발 중이지만 이 eBook의 3.0 업데이트에서 이 기술에 대해 자세히 확인해야 합니다. Blazor에 대한 자세한 내용은 [Blazor 시작](https://blazor.net/docs/get-started.html)을 참조하세요.

## <a name="when-to-choose-traditional-web-apps"></a>기존 웹앱을 선택하는 경우

다음에서는 이전에 설명한 기존 웹 애플리케이션을 선택해야 하는 이유를 좀 더 자세히 설명합니다.

**애플리케이션에 간단한 읽기 전용 클라이언트 쪽 요구 사항이 있는 경우**

많은 웹 애플리케이션은 대부분의 사용자에게 주로 읽기 전용 방식으로 사용됩니다. 읽기 전용(또는 대부분 읽기 전용인) 애플리케이션은 다양한 상태를 유지하고 조작하는 애플리케이션보다 훨씬 더 간단한 경우가 많습니다. 예를 들어 검색 엔진은 텍스트 상자가 있는 단일 진입점과 검색 결과를 표시하는 두 번째 페이지로 구성될 수 있습니다. 익명 사용자가 손쉽게 요청을 수행할 수 있으며 클라이언트 쪽 논리가 거의 필요하지 않습니다. 마찬가지로, 블로그 또는 콘텐츠 관리 시스템의 공용 애플리케이션은 일반적으로 클라이언트 쪽 동작이 거의 없는 콘텐츠로 주로 구성됩니다. 이러한 애플리케이션은 웹 서버에서 논리를 수행하고 브라우저에 표시되는 HTML을 렌더링하는 기존 서버 기반 웹 애플리케이션으로 손쉽게 빌드할 수 있습니다. 사이트의 각 고유 페이지에 검색 엔진에서 책갈피에 추가하고 인덱싱할 수 있는 자체 URL이 있다는 사실(기본적으로 이를 애플리케이션의 별도 기능으로 추가할 필요 없음)은 이러한 시나리오에서 분명한 이점으로 작용합니다.

**JavaScript를 지원하지 않는 브라우저에서 애플리케이션이 작동해야 하는 경우**

JavaScript 지원이 제한적이거나 없는 브라우저에서 작동해야 하는 웹 애플리케이션은 기존 웹앱 워크플로를 사용하여 작성해야 합니다(또는 최소한 이러한 동작으로 대체할 수 있어야 함). SPA가 작동하려면 클라이언트 쪽 JavaScript가 필요합니다. 사용할 수 없다면 SPA가 좋은 선택이 아닙니다.

**팀이 JavaScript 또는 TypeScript 개발 기술에 익숙하지 않은 경우**

팀이 JavaScript 또는 TypeScript에 익숙하지 않지만 서버 쪽 웹 애플리케이션 개발에 익숙하다면 기존 웹앱을 SPA보다 더 빨리 제공할 수 있을 것입니다. SPA를 프로그래밍하는 방법을 배우는 것이 목표이거나 SPA가 제공하는 사용자 경험이 필요한 경우가 아니라면 기존 웹앱 빌드가 이미 익숙한 팀에게 기존 웹앱은 더 생산적인 선택입니다.

## <a name="when-to-choose-spas"></a>SPA를 선택하는 경우

다음은 웹앱 개발의 단일 페이지 애플리케이션 스타일을 선택하는 경우에 대한 자세한 설명입니다.

**애플리케이션이 다양한 기능을 갖춘 풍부한 사용자 인터페이스를 노출해야 하는 경우**

SPA는 사용자가 작업을 수행하거나 앱의 영역 간에 이동할 때 페이지를 다시 로드할 필요가 없는 다양한 클라이언트 쪽 기능을 지원할 수 있습니다. SPA는 백그라운드에서 데이터를 페치해서 더 빨리 로드할 수 있으며, 전체 페이지를 다시 로드하는 경우가 드물기 때문에 개별 사용자 작업의 반응성이 더욱 빨라집니다. SPA는 사용자가 단추를 클릭하여 양식을 제출할 필요 없이 부분적으로 완료된 양식이나 문서를 저장하는 증분 업데이트를 지원할 수 있습니다. SPA는 끌어서 놓기와 같은 다양한 클라이언트 쪽 동작을 기존 애플리케이션보다 훨씬 쉽게 지원할 수 있습니다. SPA는 연결이 끊긴 모드에서 실행되도록 설계할 수 있습니다. 그러면 연결이 다시 설정된 후 클라이언트 쪽 모델이 업데이트되어 결국 서버로 다시 동기화됩니다. 앱의 요구 사항에 일반적인 HTML 형식이 제공하는 것 이상의 다양한 기능을 포함된 경우, SPA 스타일 애플리케이션을 선택해야 합니다.

SPA는 주소 표시줄에 의미 있는 URL을 표시하여 현재 작업을 반영하고 사용자가 이 URL을 책갈피에 추가하거나 딥 링크하여 돌아가도록 허용하는 등 기존 웹앱에 빌드된 기능을 구현해야 하는 경우가 자주 있습니다. 또한 SPA는 사용자가 결과 페이지에서 브라우저의 뒤로 및 앞으로 단추를 사용할 수 있게 하여 당황하지 않도록 해야 합니다.

**팀이 JavaScript 및/또는 TypeScript 개발에 익숙한 경우**

SPA를 작성하려면 JavaScript 및/또는 TypeScript와 클라이언트 쪽 프로그래밍 기술 및 라이브러리에 익숙해야 합니다. 팀은 Angular와 같은 SPA 프레임워크를 사용하여 최신 JavaScript를 작성하는 데 능숙해야 합니다.

> ### <a name="references--spa-frameworks"></a>참조 - SPA 프레임워크
>
> - **Angular**  
>   <https://angular.io>
> - **JavaScript 프레임워크 비교**  
>   <https://jsreport.io/the-ultimate-guide-to-javascript-frameworks/>

**애플리케이션이 다른(내부 또는 공용) 클라이언트용 API를 이미 노출해야 하는 경우**

다른 클라이언트에서 사용할 웹 API가 이미 지원되는 경우, 서버 쪽 양식의 논리를 재현하는 대신 이러한 API를 활용하는 SPA 구현을 만드는 데 필요한 노력이 줄어들 수 있습니다. SPA는 사용자가 애플리케이션과 상호 작용할 때 웹 API를 광범위하게 사용하여 데이터를 쿼리하고 업데이트합니다.

## <a name="decision-table--traditional-web-or-spa"></a>의사 결정 테이블 – 기존 웹 또는 SPA

다음 의사 결정 테이블에는 기존 웹 애플리케이션과 SPA 중에 하나를 선택할 때 고려해야 할 기본 요소 몇 가지가 요약되어 있습니다.

| **요소**                                           | **기존 웹앱** | **단일 페이지 애플리케이션** |
| ---------------------------------------------------- | ----------------------- | --------------------------- |
| 팀의 JavaScript/TypeScript 숙련도 요구 사항 | **최소**             | **필수**                |
| 스크립팅 없이 브라우저 지원                   | **지원됨**           | **지원 안 됨**           |
| 최소한의 클라이언트 쪽 애플리케이션 동작             | **적합**         | **과도**                |
| 다양하고 복잡한 사용자 인터페이스 요구 사항            | **제한적**             | **적합**             |

>[!div class="step-by-step"]
>[이전](modern-web-applications-characteristics.md)
>[다음](architectural-principles.md)
