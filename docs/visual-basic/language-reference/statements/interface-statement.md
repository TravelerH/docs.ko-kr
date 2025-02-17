---
title: Interface 문(Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Interface
helpviewer_keywords:
- interface statement [Visual Basic]
- interfaces [Visual Basic], interface definition
ms.assetid: 8997af73-bda3-4f79-bd41-ca396b610260
ms.openlocfilehash: 68590702835e47e5f0f2e0380bc0fe4017d5eb15
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582664"
---
# <a name="interface-statement-visual-basic"></a>Interface 문(Visual Basic)
인터페이스 이름을 선언 하 고 인터페이스에서 구성 하는 멤버의 정의를 소개 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] _  
Interface name [ ( Of typelist ) ]  
    [ Inherits interfacenames ]  
    [ [ modifiers ] Property membername ]  
    [ [ modifiers ] Function membername ]  
    [ [ modifiers ] Sub membername ]  
    [ [ modifiers ] Event membername ]  
    [ [ modifiers ] Interface membername ]  
    [ [ modifiers ] Class membername ]  
    [ [ modifiers ] Structure membername ]  
End Interface  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`attributelist`|(선택 사항) [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)을 참조 하십시오.|  
|`accessmodifier`|(선택 사항) 다음 중 하나일 수 있습니다.<br /><br /> [공용](../../../visual-basic/language-reference/modifiers/public.md) -   <br />-   [보호](../../../visual-basic/language-reference/modifiers/protected.md) 됨<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [개인](../../../visual-basic/language-reference/modifiers/private.md)<br />-  [보호 된 Friend](../../language-reference/modifiers/protected-friend.md)<br/>- [개인 보호](../../language-reference/modifiers/private-protected.md) 됨<br /><br /> [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.|  
|`Shadows`|(선택 사항) [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)를 참조 하세요.|  
|`name`|필수 요소. 이 인터페이스의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.|  
|`Of`|(선택 사항) 제네릭 인터페이스 임을 지정 합니다.|  
|`typelist`|[Of](../../../visual-basic/language-reference/statements/of-clause.md) 키워드를 사용 하는 경우 필수 사항입니다. 이 인터페이스의 형식 매개 변수 목록입니다. 필요에 따라 `In` 및 `Out` 제네릭 한정자를 사용 하 여 각 형식 매개 변수를 variant로 선언할 수 있습니다. [형식 목록](../../../visual-basic/language-reference/statements/type-list.md)을 참조 하십시오.|  
|`Inherits`|(선택 사항) 이 인터페이스가 다른 인터페이스나 인터페이스의 특성 및 멤버를 상속 함을 나타냅니다. [Inherits 문](../../../visual-basic/language-reference/statements/inherits-statement.md)을 참조 하세요.|  
|`interfacenames`|@No__t_0 문을 사용 하는 경우 필요 합니다. 이 인터페이스가 파생 되는 인터페이스의 이름입니다.|  
|`modifiers`|(선택 사항) 정의 되는 인터페이스 멤버에 대 한 적절 한 한정자입니다.|  
|`Property`|(선택 사항) 인터페이스의 멤버인 속성을 정의 합니다.|  
|`Function`|(선택 사항) 인터페이스의 멤버인 `Function` 프로시저를 정의 합니다.|  
|`Sub`|(선택 사항) 인터페이스의 멤버인 `Sub` 프로시저를 정의 합니다.|  
|`Event`|(선택 사항) 인터페이스의 멤버인 이벤트를 정의 합니다.|  
|`Interface`|(선택 사항) 이 인터페이스 내에 중첩 된 인터페이스를 정의 합니다. 중첩 된 인터페이스 정의는 `End Interface` 문으로 종료 해야 합니다.|  
|`Class`|(선택 사항) 인터페이스의 멤버인 클래스를 정의 합니다. 멤버 클래스 정의는 `End Class` 문으로 끝나야 합니다.|  
|`Structure`|(선택 사항) 인터페이스의 멤버인 구조체를 정의 합니다. 멤버 구조 정의는 `End Structure` 문으로 종료 해야 합니다.|  
|`membername`|인터페이스의 멤버로 정의 된 각 속성, 프로시저, 이벤트, 인터페이스, 클래스 또는 구조체에 필요 합니다. 멤버의 이름입니다.|  
|`End Interface`|@No__t_0 정의를 종료 합니다.|  
  
## <a name="remarks"></a>주의  
 *인터페이스* 는 클래스와 구조체에서 구현할 수 있는 속성, 프로시저 등의 멤버 집합을 정의 합니다. 인터페이스는 내부 동작이 아니라 멤버의 서명만 정의 합니다.  
  
 클래스 또는 구조체는 인터페이스에서 정의 된 모든 멤버에 코드를 제공 하 여 인터페이스를 구현 합니다. 마지막으로, 응용 프로그램이 해당 클래스 또는 구조에서 인스턴스를 만들 때 개체가 존재 하 고 메모리에서 실행 됩니다. 자세한 내용은 [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) 및 [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)를 참조 하세요.  
  
 @No__t_0는 네임 스페이스 또는 모듈 수준 에서만 사용할 수 있습니다. 즉, 인터페이스의 *선언 컨텍스트* 는 소스 파일, 네임 스페이스, 클래스, 구조체, 모듈 또는 인터페이스 여야 하며 프로시저 또는 블록일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 인터페이스의 기본값은 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 액세스입니다. 액세스 한정자를 사용 하 여 액세스 수준을 조정할 수 있습니다. 자세한 내용은 [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
## <a name="rules"></a>규칙  
  
- **인터페이스를 중첩 합니다.** 다른 인터페이스 내에서 인터페이스 하나를 정의할 수 있습니다. 외부 인터페이스를 *포함 하는 인터페이스*라고 하 고 내부 인터페이스를 *중첩 된 인터페이스*라고 합니다.  
  
- **멤버 선언입니다.** 속성 또는 프로시저를 인터페이스의 멤버로 선언 하는 경우 해당 속성 또는 프로시저의 *서명만* 정의 합니다. 여기에는 요소 형식 (속성 또는 프로시저), 해당 매개 변수 및 매개 변수 형식 및 반환 형식이 포함 됩니다. 이로 인해 멤버 정의는 한 줄의 코드만 사용 하 고 `End Function` 또는 `End Property` 같은 종료 문은 인터페이스에서 유효 하지 않습니다.  
  
     반면, 열거형 또는 구조체 또는 중첩 된 클래스나 인터페이스를 정의 하는 경우에는 해당 데이터 멤버를 포함 해야 합니다.  
  
- **멤버 한정자입니다.** 모듈 멤버를 정의할 때 액세스 한정자를 사용할 수 없으며 [오버 로드](../../../visual-basic/language-reference/modifiers/overloads.md)를 제외한 [Shared](../../../visual-basic/language-reference/modifiers/shared.md) 또는 procedure 한정자를 지정할 수도 없습니다. [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)를 사용 하 여 모든 멤버를 선언 하 고, [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md) 또는 [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)뿐만 아니라 속성을 정의 하는 경우 [기본값](../../../visual-basic/language-reference/modifiers/default.md) 을 사용할 수 있습니다.  
  
- **상속.** 인터페이스가 [Inherits 문을](../../../visual-basic/language-reference/statements/inherits-statement.md)사용 하는 경우 하나 이상의 기본 인터페이스를 지정할 수 있습니다. 두 인터페이스가 동일한 이름의 멤버를 정의 하는 경우에도 두 인터페이스에서 상속할 수 있습니다. 이렇게 하려면 구현 하는 코드에서 구현 중인 멤버를 지정 하는 데 이름 한정을 사용 해야 합니다.  
  
     인터페이스는 더 제한적인 액세스 수준으로 다른 인터페이스에서 상속할 수 없습니다. 예를 들어 `Public` 인터페이스는 `Friend` 인터페이스에서 상속할 수 없습니다.  
  
     인터페이스는 그 안에 중첩 된 인터페이스에서 상속할 수 없습니다.  
  
- **구현이.** 클래스가 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md) 문을 사용 하 여이 인터페이스를 구현 하는 경우 인터페이스 내에 정의 된 모든 멤버를 구현 해야 합니다. 또한 구현 하는 코드의 각 서명은이 인터페이스에 정의 된 해당 시그니처와 정확히 일치 해야 합니다. 그러나 구현 하는 코드에서 멤버의 이름은 인터페이스에 정의 된 멤버 이름과 일치 하지 않아도 됩니다.  
  
     클래스가 프로시저를 구현 하는 경우 프로시저를 `Shared`으로 지정할 수 없습니다.  
  
- **기본 속성입니다.** 인터페이스는 속성 이름을 사용 하지 않고 참조할 수 있는 *기본 속성*으로 최대 하나의 속성을 지정할 수 있습니다. 이러한 속성을 [Default](../../../visual-basic/language-reference/modifiers/default.md) 한정자로 선언 하 여 지정 합니다.  
  
     이는 인터페이스가 none을 상속 하는 경우에만 기본 속성을 정의할 수 있음을 의미 합니다.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 모든 인터페이스 멤버는 암시적으로 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스를 가집니다. 멤버를 정의할 때 액세스 한정자를 사용할 수 없습니다. 그러나 인터페이스를 구현 하는 클래스는 구현 된 각 멤버에 대 한 액세스 수준을 선언할 수 있습니다.  
  
     클래스 인스턴스를 변수에 할당 하는 경우 해당 멤버의 액세스 수준은 변수의 데이터 형식이 기본 인터페이스 인지 아니면 구현 클래스 인지에 따라 달라질 수 있습니다. 다음은 이에 대한 예입니다.  
  
     [!code-vb[VbVbalrStatements#39](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#39)]  
  
     @No__t_0를 통해 클래스 멤버에 액세스 하는 경우 모든 사용자에 게 공용 액세스 권한이 있습니다. 그러나 `varAsClass`를 통해 멤버에 액세스 하는 경우 `Sub` 프로시저 `doSomething`에 전용 액세스 권한이 있습니다.  
  
- **범위.** 인터페이스는 네임 스페이스, 클래스, 구조체 또는 모듈 전체의 범위에 있습니다.  
  
     모든 인터페이스 멤버의 범위는 전체 인터페이스입니다.  
  
- **수명.** 인터페이스 자체는 수명이 나 해당 멤버를 포함 하지 않습니다. 클래스가 인터페이스를 구현 하 고 해당 클래스의 인스턴스로 개체가 만들어지는 경우 개체는 실행 중인 응용 프로그램 내에서 수명을 가집니다. 자세한 내용은 [클래스 문의](../../../visual-basic/language-reference/statements/class-statement.md)"수명"을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Interface` 문을 사용 하 여 `thisInterface` 이라는 인터페이스를 정의 합니다 .이 인터페이스는 `Property` 문과 `Function` 문으로 구현 되어야 합니다.  
  
 [!code-vb[VbVbalrStatements#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#40)]  
  
 @No__t_0 및 `Function` 문은 인터페이스 내에서 `End Property` 및 `End Function`로 끝나는 블록을 제공 하지 않습니다. 인터페이스는 해당 멤버의 서명만 정의 합니다. 전체 `Property` 및 `Function` 블록은 `thisInterface`를 구현 하는 클래스에 나타납니다.  
  
## <a name="see-also"></a>참조

- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Generic Types in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [제네릭 인터페이스의 가변성](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)
- [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
