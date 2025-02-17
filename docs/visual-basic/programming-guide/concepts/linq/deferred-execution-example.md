---
title: 지연 된 실행 예제 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 9a22bea1-c755-4aac-800a-fcd9e5107ace
ms.openlocfilehash: e0bb7f3d125cc48607a534e2c24cbf7083353945
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583324"
---
# <a name="deferred-execution-example-visual-basic"></a>지연 된 실행 예제 (Visual Basic)

이 항목에서는 지연된 실행과 지연 계산이 LINQ to XML 쿼리의 실행에 미치는 영향을 보여 줍니다.

## <a name="example"></a>예제

다음 예제에서는 지연된 실행을 사용하는 확장 메서드를 사용하는 경우의 실행 순서를 보여 줍니다. 이 예제에서는 세 문자열의 배열을 선언한 다음 `ConvertCollectionToUpperCase`에서 반환하는 컬렉션을 반복합니다.

```vb
Imports System.Runtime.CompilerServices

Module Module1

    <Extension()>
    Private Iterator Function ConvertCollectionToUpperCase(
    ByVal source As IEnumerable(Of String)) _
    As IEnumerable(Of String)
        For Each str As String In source
            Console.WriteLine("ToUpper: source {0}", str)
            Yield str.ToUpper()
        Next
    End Function

    Sub Main()
        Dim stringArray = New String() {"abc", "def", "ghi"}

        Dim q = From str In stringArray.ConvertCollectionToUpperCase()
                Select str

        For Each Str As String In q
            Console.WriteLine("Main: str {0}", Str)
        Next
    End Sub

End Module
```

이 예제는 다음과 같은 출력을 생성합니다.

```console
ToUpper: source abc
Main: str ABC
ToUpper: source def
Main: str DEF
ToUpper: source ghi
Main: str GHI
```

`ConvertCollectionToUpperCase`에서 반환하는 컬렉션을 반복할 때 각 항목이 소스 문자열 배열에서 검색되어 대문자로 변환된 후 다음 항목이 소스 문자열 배열에서 검색됩니다.

반환된 컬렉션의 각 항목이 `foreach`의 `Main` 루프에서 처리되기 전에는 문자열의 전체 배열이 대문자로 변환되지 않는 것을 확인할 수 있습니다.

## <a name="see-also"></a>참조

- [자습서: 지연 된 실행 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/tutorial-deferred-execution.md)
