---
title: 배열 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [Visual Basic], converting type
- type conversion [Visual Basic], arrays
- conversions [Visual Basic], type
- arrays [Visual Basic], data types
- conversions [Visual Basic], data type
- object arrays [Visual Basic], converting type
- data type conversion [Visual Basic], array conversions
- conversions [Visual Basic], array types
- object arrays
ms.assetid: fceff7d2-a1b7-44c7-b9aa-8bd831d8a444
ms.openlocfilehash: 475f3f5357f7c989a30ca9e6c5d32b8cc989436f
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72581855"
---
# <a name="array-conversions-visual-basic"></a>배열 변환(Visual Basic)
다음 조건을 충족 하는 경우 배열 형식을 다른 배열 형식으로 변환할 수 있습니다.  
  
- **같은 순위입니다.** 두 배열의 순위는 동일 해야 합니다. 즉, 동일한 수의 차수를 가져야 합니다. 그러나 각 차원의 길이는 같을 필요가 없습니다.  
  
- **요소 데이터 형식입니다.** 두 배열 요소의 데이터 형식은 모두 참조 형식 이어야 합니다. 하나 이상의 값 형식이 관련 되어 있으므로 `Integer` 배열을 `Long` 배열 또는 `Object` 배열로 변환할 수 없습니다. 자세한 내용은 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)을 참조하세요.  
  
- **Convertibility.** 확대 또는 축소의 변환은 두 배열의 요소 형식 간에 가능 해야 합니다. 이 요구 사항에 실패 하는 예제는 `String` 배열과 <xref:System.Attribute?displayProperty=nameWithType>에서 파생 된 클래스의 배열 사이에서 시도 된 변환입니다. 이러한 두 형식에는 공통 된 것이 없으며 두 형식 사이에는 어떠한 종류의 변환만 존재 하지 않습니다.  
  
 한 배열 형식을 다른 형식으로 변환 하는 것은 각 요소의 변환이 확대 또는 축소 인지에 따라 확대 또는 축소 됩니다. 자세한 내용은 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)을 참조하세요.  
  
## <a name="conversion-to-an-object-array"></a>개체 배열로 변환  
 @No__t_0 배열을 초기화 하지 않고 선언 하는 경우 요소 형식은 초기화 되지 않은 상태로 유지 되는 동안 `Object` 됩니다. 특정 클래스의 배열로 설정 하면 해당 클래스의 형식을 사용 합니다. 그러나 해당 기본 형식은 여전히 `Object` 되며 이후에는 관련 없는 클래스의 다른 배열로 설정할 수 있습니다. 모든 클래스는 `Object`에서 파생 되므로 모든 클래스에서 다른 클래스로 배열의 요소 형식을 변경할 수 있습니다.  
  
 다음 예에서는 형식 `student`와 `String` 간에 변환이 없지만 둘 다 `Object`에서 파생 되므로 모든 할당이 유효 합니다.  
  
```vb  
' Assume student has already been defined as a class.  
Dim testArray() As Object  
' testArray is still an Object array at this point.  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
testArray = New student(3) {}  
' testArray is now of type student().  
testArray = names  
' testArray is now a String array.  
```  
  
### <a name="underlying-type-of-an-array"></a>배열의 내부 형식  
 원래 특정 클래스를 사용 하 여 배열을 선언 하는 경우 해당 기본 요소 형식은 해당 클래스입니다. 이후에 다른 클래스의 배열로 설정 하는 경우 두 클래스 사이에 변환이 있어야 합니다.  
  
 다음 예제에서 `students`은 `student` 배열입니다. @No__t_0와 `student` 간에 변환이 존재 하지 않으므로 마지막 문이 실패 합니다.  
  
```vb  
Dim students() As student  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
students = New Student(3) {}  
' The following statement fails at compile time.  
students = names  
```  
  
## <a name="see-also"></a>참조

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Visual Basic 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [암시적 변환과 명시적 변환](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [문자열과 다른 형식 사이의 변환](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [방법: Visual Basic에서 개체를 다른 형식으로 변환](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
