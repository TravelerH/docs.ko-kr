---
title: Inherits 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Inherits
- Inherits
helpviewer_keywords:
- Inherits statement [Visual Basic]
- Inherits statement [Visual Basic], syntax
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
ms.openlocfilehash: e92e12908c89bb7a0bf385a2122b0c8f1eb8a6f7
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72581748"
---
# <a name="inherits-statement"></a>Inherits Statement
현재 클래스 또는 인터페이스가 다른 클래스나 인터페이스 집합에서 특성, 변수, 속성, 프로시저 및 이벤트를 상속 하도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Inherits basetypenames  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`basetypenames`|필수 요소. 이 클래스가 파생 되는 클래스의 이름입니다.<br /><br /> 또는<br /><br /> 이 인터페이스가 파생 되는 인터페이스의 이름입니다. 여러 이름을 구분 하려면 쉼표를 사용 합니다.|  
  
## <a name="remarks"></a>주의  
 사용 되는 경우 `Inherits` 문은 클래스 또는 인터페이스 정의에서 공백이 아닌 첫 번째 줄 이어야 합니다. @No__t_0 또는 `Interface` 문 바로 뒤에와 야 합니다.  
  
 @No__t_0는 클래스 또는 인터페이스 에서만 사용할 수 있습니다. 즉, 상속의 선언 컨텍스트는 소스 파일, 네임 스페이스, 구조체, 모듈, 프로시저 또는 블록이 될 수 없습니다.  
  
## <a name="rules"></a>규칙  
  
- **클래스 상속.** 클래스가 `Inherits` 문을 사용 하는 경우 하나의 기본 클래스만 지정할 수 있습니다.  
  
     클래스는 그 안에 중첩 된 클래스에서 상속할 수 없습니다.  
  
- **인터페이스 상속.** 인터페이스에서 `Inherits` 문을 사용 하는 경우 하나 이상의 기본 인터페이스를 지정할 수 있습니다. 두 인터페이스가 동일한 이름의 멤버를 정의 하는 경우에도 두 인터페이스에서 상속할 수 있습니다. 이렇게 하려면 구현 하는 코드에서 구현 중인 멤버를 지정 하는 데 이름 한정을 사용 해야 합니다.  
  
     인터페이스는 더 제한적인 액세스 수준으로 다른 인터페이스에서 상속할 수 없습니다. 예를 들어 `Public` 인터페이스는 `Friend` 인터페이스에서 상속할 수 없습니다.  
  
     인터페이스는 그 안에 중첩 된 인터페이스에서 상속할 수 없습니다.  
  
 .NET Framework의 클래스 상속 예제는 <xref:System.SystemException> 클래스에서 상속 되는 <xref:System.ArgumentException> 클래스입니다. 이를 통해 <xref:System.Exception.Message%2A> 속성 및 <xref:System.Exception.ToString%2A> 메서드와 같이 시스템 예외에 필요한 미리 정의 된 모든 속성 및 프로시저를 <xref:System.ArgumentException> 수 있습니다.  
  
 .NET Framework의 인터페이스 상속 예는 <xref:System.Collections.IEnumerable> 인터페이스에서 상속 하는 <xref:System.Collections.ICollection> 인터페이스입니다. 이로 인해 <xref:System.Collections.ICollection>는 컬렉션을 트래버스하는 데 필요한 열거자의 정의를 상속 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Inherits` 문을 사용 하 `thisClass` 클래스 `anotherClass` 기본 클래스의 모든 멤버를 상속할 수 있는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrStatements#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#37)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 여러 인터페이스의 상속을 보여 줍니다.  
  
 [!code-vb[VbVbalrStatements#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#38)]  
  
 이제 `thisInterface` 이라는 인터페이스에는 상속 된 멤버가 두 개체의 유형별 비교를 위해 각각 제공 하는 <xref:System.IComparable>, <xref:System.IDisposable> 및 <xref:System.IFormattable> 인터페이스의 모든 정의와 할당 된 리소스를 해제 하 고 값이 포함 됩니다. `String` 개체입니다. @No__t_0를 구현 하는 클래스는 모든 기본 인터페이스의 모든 멤버를 구현 해야 합니다.  
  
## <a name="see-also"></a>참조

- [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)
- [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
