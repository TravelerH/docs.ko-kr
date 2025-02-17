---
title: .NET 네이티브 및 컴파일
ms.date: 03/30/2017
ms.assetid: e38ae4f3-3e3d-42c3-a4b8-db1aa9d84f85
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1a15d30ea4d6e0f4456460248e96428419117d85
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049434"
---
# <a name="net-native-and-compilation"></a>.NET 네이티브 및 컴파일

.NET Framework를 대상으로 지정하는 Windows 8.1 애플리케이션과 Windows 데스크톱 애플리케이션은 특정 프로그래밍 언어로 작성되고 IL(중간 언어)로 컴파일됩니다. 런타임에 JIT(Just-In-Time) 컴파일러는 메서드가 처음 실행되기 바로 전에 로컬 컴퓨터에 대한 네이티브 코드로 IL을 컴파일합니다. 반대로 .NET 네이티브 도구 체인은 컴파일 타임에 소스 코드를 네이티브 코드로 변환합니다. 이 항목에서는 .NET Framework 앱에 사용할 수 있는 다른 컴파일 기술과 .NET 네이티브를 비교하고 .NET 네이티브로 컴파일된 코드에서 발생하는 예외가 JIT로 컴파일된 코드에서 발생하지 않는 이유를 이해하는 데 도움이 될 수 있는 네이티브 코드를 .NET 네이티브에서 생성하는 방법에 대한 실제적인 개요를 제공합니다.

## <a name="net-native-generating-native-binaries"></a>.NET 네이티브: 네이티브 이진 파일 생성

.NET Framework를 대상으로 지정하고 .NET 네이티브 도구 체인으로 컴파일되지 않은 애플리케이션은 다음이 포함된 애플리케이션 어셈블리로 구성됩니다.

- 어셈블리, 해당 종속성, 포함된 형식, 해당 멤버를 설명하는 [메타데이터](../../standard/metadata-and-self-describing-components.md). 메타데이터는 리플렉션 및 런타임에 바인딩된 액세스에 사용되고 때때로 컴파일러 및 빌드 도구에서도 사용됩니다.

- 구현 코드. IL(중간 언어) opcodes로 구성됩니다. 런타임에 JIT(Just-In-Time) 컴파일러가 이 코드를 대상 플랫폼에 대한 네이티브 코드로 변환합니다.

 주 애플리케이션 어셈블리 이외에 앱에는 다음 항목이 있어야 합니다.

- 앱에 필요한 추가적인 클래스 라이브러리 또는 타사 어셈블리. 이들 어셈블리에도 어셈블리, 해당 형식, 해당 멤버를 설명하는 메타데이터와 모든 형식 멤버를 구현하는 IL이 포함됩니다.

- .NET Framework 클래스 라이브러리. .NET Framework 설치와 함께 로컬 시스템에 설치되는 어셈블리 컬렉션입니다. .NET Framework 클래스 라이브러리에 포함된 어셈블리에는 전체 메타데이터 및 구현 코드 집합이 들어 있습니다.

- 공용 언어 런타임. 어셈블리 로드, 메모리 관리 및 가비지 컬렉션, 예외 처리, Just-In-Time 컴파일, 원격, interop와 같은 서비스를 수행하는 동적 링크 라이브러리 컬렉션입니다. 클래스 라이브러리처럼 런타임은 로컬 시스템에 .NET Framework 설치와 함께 설치됩니다.

앱을 성공적으로 실행하려면 전체 공용 언어 런타임과 애플리케이션별 어셈블리의 모든 형식에 대한 메타데이터 및 IL, 타사 어셈블리 및 시스템 어셈블리가 있어야 합니다.

## <a name="net-native-and-just-in-time-compilation"></a>.NET 네이티브 및 Just-In-Time 컴파일

.NET 네이티브 도구 체인에 대한 입력은 C# 또는 Visual Basic 컴파일러로 빌드된 Windows 스토어 앱입니다. 즉. .NET Native 네이티브 도구 체인은 언어 컴파일러가 Windows 스토어 앱 컴파일을 마쳤을 때 실행을 시작합니다.

> [!TIP]
> .NET 네이티브에 대한 입력은 관리되는 어셈블리에 기록되는 IL 및 메타데이터이므로 빌드 전 또는 빌드 후 이벤트를 사용하거나 MSBuild 프로젝트 파일을 수정하여 사용자 지정 코드 생성 또는 기타 사용자 지정 작업을 수행할 수 있습니다.
>
> 그러나 IL을 수정하고 이에 따라 .NET 도구 체인이 앱의 IL을 분석하지 않도록 방지하는 도구 범주는 지원되지 않습니다. 난독 처리기는 이 형식의 가장 주목할 만한 도구입니다.

앱을 IL에서 네이티브 코드로 변환하는 과정에서 .NET 네이티브 도구 체인은 다음과 같은 작업을 수행합니다.

- 특정 코드 경로에서 리플렉션 및 메타데이터에 의존하는 코드를 정적 네이티브 코드로 바꿉니다. 예를 들어 값 형식이 <xref:System.ValueType.Equals%2A?displayProperty=nameWithType> 메서드를 재정의하지 않으면 기본 같음 테스트에서는 리플렉션을 사용하여 값 형식 필드를 나타내는 <xref:System.Reflection.FieldInfo> 개체를 검색하고 나서 두 인스턴스의 필드 값을 비교합니다. 네이티브 코드를 컴파일할 때 .NET 네이티브 도구 체인은 리플렉션 코드 및 메타데이터를 필드 값의 정적 비교로 바꿉니다.

- 가능할 경우 네이티브 코드는 모든 메타데이터를 제거하려고 시도합니다.

- 네이티브 코드는 실제로 앱에서 호출되는 구현 코드만 최종 앱 어셈블리에 포함합니다. 이는 특히 타사 라이브러리 및 .NET Framework 클래스 라이브러리에 있는 코드에 영향을 미칩니다. 따라서 애플리케이션은 더 이상 타사 라이브러리나 전체 .NET Framework 클래스 라이브러리에 의존하지 않고, 타사 및 .NET Framework 클래스 라이브러리의 코드는 앱에 대한 로컬 위치에 있습니다.

- 네이티브 코드는 전체 CLR을 주로 가비지 수집기를 포함하는 리팩터링된 런타임으로 바꿉니다. 리팩터링된 런타임은 앱에 대한 로컬 위치에 있는 mrt100_app.dll 라이브러리에서 찾을 수 있고 크기가 겨우 몇백 킬로바이트입니다. 정적 링크를 사용하면 공용 언어 런타임에서 수행되는 대부분 서비스가 필요하지 않으므로 이 상황이 가능합니다.

  > [!NOTE]
  > .NET 네이티브에서는 표준 공용 언어 런타임과 같은 가비지 수집기를 사용합니다. .NET 네이티브 가비지 수집기에서 백그라운드 가비지 수집은 기본적으로 사용됩니다. 가비지 수집에 대한 자세한 내용은 [가비지 수집 기본 사항](../../standard/garbage-collection/fundamentals.md)을 참조하세요.

> [!IMPORTANT]
> .NET 네이티브에서는 전체 애플리케이션을 네이티브 애플리케이션으로 컴파일합니다. 관리 코드와 독립적으로 호출될 수 있도록 클래스 라이브러리가 포함된 단일 어셈블리를 네이티브 코드로 컴파일할 수는 없습니다.

.NET 네이티브 도구 체인에서 생성되는 결과 앱은 프로젝트 디렉터리의 디버그 또는 릴리스 디렉터리에 있는 ilc.out 디렉터리에 기록됩니다. 결과 앱은 다음 파일로 구성됩니다.

- *\<appName>* .exe - 컨트롤을 *\<appName>* .dll의 특수 `Main` 내보내기에 전송하는 스텁 실행 파일.

- *\<appName&gt;* .dll - 모든 애플리케이션 코드와 종속성이 있는 .NET Framework 클래스 라이브러리 및 타사 라이브러리의 코드가 들어 있는 Windows 동적 링크 라이브러리.  Windows와 상호 운용하고 앱에서 개체를 직렬화하는 데 필요한 코드와 같은 지원 코드도 포함됩니다.

- mrt100_app.dll - 가비지 컬렉션과 같은 런타임 서비스를 제공하는 리팩터링된 런타임.

 모든 종속성은 앱의 APPX 매니페스트에 의해 캡처됩니다.  appx 패키지로 직접 번들로 제공되는 애플리케이션 exe, dll 및 mrt100_app.dll 이외에 다음 파일 두 개가 추가로 포함됩니다.

- msvcr140_app.dll - mrt100_app.dll에서 사용되는 CRT(C 런타임) 라이브러리. 이 파일은 프레임워크 참조를 통해 패키지에 포함됩니다.

- mrt100.dll. 이 라이브러리에는 라이브러리가 없어서 mrt100_app.dll 작동을 방지할 수 없더라도 mrt100_app.dll 성능을 향상할 수 있는 함수가 포함됩니다. 이 라이브러리는 로컬 컴퓨터의 system32 디렉터리에 로드됩니다(있는 경우).

.NET 네이티브 도구 체인은 앱이 실제로 구현 코드를 호출하는지를 인식하는 경우에만 해당 코드를 앱에 연결하므로 다음 시나리오에 필요한 메타데이터 또는 구현 코드가 앱에 포함되지 않을 수 있습니다.

- 리플렉션.

- 동적 또는 런타임 바인딩 호출.

- 직렬화 및 deserialization

- COM interop

런타임에 필요한 메타데이터나 구현 코드가 있으면 .NET 네이티브 런타임이 예외를 throw합니다. 런타임에 사용할 수 있어야 하는 메타데이터나 구현 코드가 포함된 프로그램 요소를 지정하고 런타임 정책을 프로그램 요소에 할당하는 XML 파일인 [런타임 지시문 파일](runtime-directives-rd-xml-configuration-file-reference.md)을 사용하여 이 예외를 방지하고 .NET 네이티브 도구 체인에 필요한 메타데이터와 구현 코드가 포함되어 있는지 확인할 수 있습니다. .NET 네이티브 도구 체인으로 컴파일된 Windows 스토어 프로젝트에 추가되는 기본 런타임 지시문 파일은 다음과 같습니다.

```xml
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">
  <Application>
    <Assembly Name="*Application*" Dynamic="Required All" />
  </Application>
</Directives>
```

이 파일을 통해 앱 패키지의 모든 어셈블리에서 모든 형식 및 모든 해당 멤버를 리플렉션하고 동적으로 호출할 수 있습니다. 그러나 .NET Framework 클래스 라이브러리 어셈블리의 형식을 리플렉션하거나 동적으로 활성화할 수는 없습니다. 대부분 경우에 이것으로 충분합니다.

## <a name="net-native-and-ngen"></a>.NET 네이티브 및 NGEN

[네이티브 이미지 생성기](../tools/ngen-exe-native-image-generator.md)(NGEN)에서는 어셈블리를 네이티브 코드로 컴파일하고 로컬 컴퓨터의 네이티브 이미지 캐시에 어셈블리를 설치합니다. 그러나 .NET 네이티브처럼 NGEN이 네이티브 코드를 생성하더라도 몇 가지 중요한 방식에서 .NET 네이티브와 다릅니다.

- 특정 메서드에 대한 네이티브 이미지를 사용할 수 없으면 NGEN이 JITing 코드로 대체됩니다. 즉, 네이티브 이미지에서는 계속해서 NGEN이 JIT 컴파일로 대체되어야 하는 이벤트에 메타데이터와 IL을 포함해야 합니다. 반대로 .NET 네이티브는 네이티브 이미지만 생성하고 JIT 컴파일로 대체되지 않습니다. 따라서 일부 리플렉션, 직렬화 및 interop 시나리오에 필요한 메타데이터만 유지되어야 합니다.

- NGEN은 어셈블리 로드, 원격, interop, 메모리 관리, 가비지 컬렉션, 필요한 경우 JIT 컴파일과 같은 서비스를 위해 계속해서 전체 공용 언어 런타임에 의존합니다. .NET 네이티브에서는 이들 서비스 대부분이 필요하지 않거나(JIT 컴파일), 빌드 타임에 해결되고 앱 어셈블리에 통합됩니다. 가장 중요한 가비지 수집을 비롯한 나머지 서비스는 훨씬 더 작은 리팩터링된 mrt100_app.dll 런타임에 포함됩니다.

- NGEN 이미지는 손상되기 쉽습니다. 예를 들어 종속성에 패치나 변경을 적용하려면 일반적으로 패치나 변경을 사용하는 어셈블리도 다시 NGEN되어야 합니다. 이는 특히 .NET Framework 클래스 라이브러리의 시스템 라이브러리에 적용됩니다. 반대로 .NET 네이티브에서는 애플리케이션을 서로 독립적으로 처리할 수 있습니다.

## <a name="see-also"></a>참고자료

- [메타데이터 및 자동 기술 구성 요소](../../standard/metadata-and-self-describing-components.md)
- [내부 .NET 네이티브 (Channel 9 비디오)](https://channel9.msdn.com/Shows/Going+Deep/Inside-NET-Native)
- [리플렉션 및 .NET 네이티브](reflection-and-net-native.md)
- [.NET 네이티브 일반 문제 해결](net-native-general-troubleshooting.md)
