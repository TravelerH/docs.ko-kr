---
title: 비관리 코드에 대한 보안 코딩 지침
ms.date: 03/30/2017
helpviewer_keywords:
- code security, unmanaged code
- unmanaged code, securing
- security [.NET Framework], unmanaged code
- secure coding, unmanaged code
ms.assetid: a8d15139-d368-4c9c-a747-ba757781117c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 867157b329218b79c8cc1255b2158bbe83666531
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045362"
---
# <a name="secure-coding-guidelines-for-unmanaged-code"></a>비관리 코드에 대한 보안 코딩 지침
일부 라이브러리 코드는 비관리 코드(예: Win32와 같은 네이티브 코드 API)를 호출해야 합니다. 이는 관리 코드에 대한 보안 경계를 벗어나야 함을 의미하므로 주의해야 합니다. 코드가 보안 중립적인 경우 코드와 코드를 호출하는 다른 코드 둘 다에 비관리 코드 권한(<xref:System.Security.Permissions.SecurityPermission> 플래그가 지정된 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> )이 있어야 합니다.  
  
 그러나 호출자가 이러한 강력한 권한을 갖는 것은 부적절한 경우가 많습니다. 이러한 경우 [래퍼 코드 보안](../misc/securing-wrapper-code.md)에 설명된 관리되는 래퍼 또는 라이브러리 코드와 마찬가지로 신뢰할 수 있는 코드가 중개자가 될 수 있습니다. 내부 비관리 코드 기능이 완전히 안전한 경우 직접 노출할 수 있지만, 그러지 않은 경우 먼저 적절한 권한 검사(요구)가 필요합니다.  
  
 코드에서 비관리 코드를 호출하지만 호출자에게 비관리 코드에 액세스할 수 있는 권한을 요구하지 않으려는 경우 해당 권한을 어설션해야 합니다. 어설션은 프레임에서 스택 워크를 차단합니다. 이 프로세스에서 보안 허점을 만들지 않도록 주의해야 합니다. 일반적으로 이 경우 호출자에게 적절한 권한을 요구한 다음 비관리 코드를 사용하여 해당 권한이 허용하는 작업만 수행하고 다른 작업을 수행하지 않도록 해야 합니다. 경우에 따라(예: 시간 가져오기 함수) 보안 검사 없이 비관리 코드를 호출자에게 직접 노출할 수 있습니다. 어떤 경우든 어설션되는 코드가 보안에 대한 책임을 져야 합니다.  
  
 네이티브 코드에 대한 코드 경로를 제공하는 관리 코드는 악성 코드의 잠재적 대상이므로 안전하게 사용할 수 있는 비관리 코드 및 사용 방법을 결정할 때는 주의해야 합니다. 일반적으로 비관리 코드는 부분적으로 신뢰할 수 있는 호출자에게 직접 노출하면 안 됩니다. 부분적으로 신뢰할 수 있는 코드에서 호출될 수 있는 라이브러리의 비관리 코드 사용 안전성을 평가하는 경우 다음 두 가지 주요 고려 사항이 있습니다.  
  
- **기능**. 관리되지 않는 API에서 호출자가 잠재적으로 위험한 작업을 수행할 수 있도록 허용하지 않는 기능을 제공하나요? 코드 액세스 보안은 권한을 사용하여 리소스에 대한 액세스를 적용하므로 API에서 파일, 사용자 인터페이스 또는 스레딩을 사용하는지 여부나 보호된 정보를 노출하는지 여부를 고려합니다. 노출하는 경우 관리 코드 래핑에서 진입을 허용하기 전에 필요한 권한을 요구해야 합니다. 또한 권한으로 보호되지 않는 동안 메모리 액세스를 엄격한 형식 안전성으로 제한해야 합니다.  
  
- **매개 변수 검사**. 일반적인 공격은 사양을 벗어나서 작동하도록 노출된 비관리 코드 API 메서드에 예기치 않은 매개 변수를 전달합니다. 내부 코드의 버그를 이용할 수 있는 모든 매개 변수와 마찬가지로 범위를 벗어난 인덱스 또는 오프셋 값을 사용한 버퍼 오버런은 이러한 공격 유형의 일반적인 예입니다. 따라서 비관리 코드 API의 기능이 필요한 요구 후에 부분적으로 신뢰할 수 있는 호출자에 대해 안전한 경우에도 관리 코드에서 매개 변수 유효성을 철저하게 검사하여 악성 코드에서 관리 코드 래퍼 계층을 통해 의도되지 않은 호출을 수행할 수 없도록 해야 합니다.  
  
## <a name="using-suppressunmanagedcodesecurityattribute"></a>SuppressUnmanagedCodeSecurityAttribute 사용  
 비관리 코드를 어설션한 다음 호출하는 경우 성능에 영향을 줍니다. 이러한 모든 호출에 대해 보안 시스템에서 자동으로 비관리 코드 권한을 요구하므로 매번 스택 워크가 발생합니다. 비관리 코드를 어설션한 다음 즉시 호출하는 경우 스택 워크가 무의미할 수 있습니다. 스택 워크는 어설션 및 비관리 코드 호출로 구성됩니다.  
  
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 라는 사용자 지정 특성을 비관리 코드 진입점에 적용하여 <xref:System.Security.Permissions.SecurityPermission> 권한이 지정된 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode> 을 요구하는 일반적인 보안 검사를 사용하지 않도록 설정할 수 있습니다. 이 경우 런타임 보안 검사 없이 비관리 코드에 액세스할 수 있게 되므로 항상 주의해야 합니다. **SuppressUnmanagedCodeSecurityAttribute** 가 적용된 경우에도 JIT(Just-In-Time) 컴파일에 발생하는 일회성 보안 검사가 있습니다. 이 보안 검사는 직접 실행 호출자에게 비관리 코드를 호출할 수 있는 권한이 있는지 확인합니다.  
  
 **SuppressUnmanagedCodeSecurityAttribute**를 사용하는 경우 다음 사항을 확인합니다.  
  
- 비관리 코드 진입점을 내부로 설정하거나, 코드 외부에서 액세스할 수 없도록 설정합니다.  
  
- 모든 비관리 코드 호출은 잠재적인 보안 허점입니다. 코드가 악성 코드에서 비관리 코드를 간접적으로 호출하고 보안 검사를 피하기 위한 포털이 아닌지 확인합니다. 해당하는 경우 권한을 요구합니다.  
  
- 아래 섹션에 설명된 대로 명명 규칙을 사용하여 비관리 코드에 대한 위험한 경로를 만드는 경우를 명시적으로 식별합니다.  
  
## <a name="naming-convention-for-unmanaged-code-methods"></a>비관리 코드 메서드의 명명 규칙  
 비관리 코드 메서드의 이름 지정을 위해 유용한 권장 규칙이 설정되었습니다. 모든 비관리 코드 메서드는 **safe**, **native**및 **unsafe**의 세 범주로 구분됩니다. 이러한 키워드를 클래스 이름으로 사용하고, 각 클래스 이름 내에 다양한 유형의 비관리 코드 진입점을 정의할 수 있습니다. 소스 코드에서 이러한 키워드를 클래스 이름에 추가해야 합니다(예: `Safe.GetTimeOfDay`, `Native.Xyz`또는 `Unsafe.DangerousAPI`). 다음 표에 설명된 것처럼 각 키워드는 해당 클래스를 사용하는 개발자에게 유용한 보안 정보를 제공합니다.  
  
|키워드|보안 고려 사항|  
|-------------|-----------------------------|  
|**safe**|악성 코드를 포함하여 모든 코드가 호출해도 완전히 무해합니다. 다른 관리 코드처럼 사용할 수 있습니다. 예를 들어 시간을 가져오는 함수는 일반적으로 안전합니다.|  
|**native**|보안 중립적입니다. 즉, 호출하려면 비관리 코드 권한이 필요한 비관리 코드입니다. 보안이 검사되고 권한이 없는 호출자를 중지합니다.|  
|**unsafe**|보안이 사용되지 않는 잠재적으로 위험한 비관리 코드 진입점입니다. 개발자는 이러한 비관리 코드를 사용할 경우 각별히 주의해야 하며 다른 보호를 통해 보안 취약성을 방지해야 합니다. 이 키워드는 보안 시스템을 재정의하기 때문에 개발자가 책임을 져야 합니다.|  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
