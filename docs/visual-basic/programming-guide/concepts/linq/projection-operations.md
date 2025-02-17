---
title: 프로젝션 작업 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: b8d38e6d-21cf-4619-8dbb-94476f4badc7
ms.openlocfilehash: 9db8284d59baa764a5509b1acef0c4d315fb28a7
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72524096"
---
# <a name="projection-operations-visual-basic"></a>프로젝션 작업 (Visual Basic)

프로젝션은 주로 이후에 사용할 속성으로만 구성된 새 양식으로 개체를 변환하는 작업을 가리킵니다. 프로젝션을 사용하면 각 개체를 기반으로 만들어지는 새 형식을 생성할 수 있습니다. 속성을 프로젝션하고 속성에서 수학 함수를 수행할 수 있습니다. 원래 개체를 변경하지 않고 프로젝션할 수도 있습니다.

다음 섹션에는 프로젝션을 수행하는 표준 쿼리 연산자 메서드가 나와 있습니다.

## <a name="methods"></a>메서드

|메서드 이름|설명|Visual Basic 쿼리 식 구문|추가 정보|
|-----------------|-----------------|------------------------------------------|----------------------|
|셀렉트 버전|변환 함수를 기반으로 하는 값을 프로젝션합니다.|`Select`|<xref:System.Linq.Enumerable.Select%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Select%2A?displayProperty=nameWithType>|
|SelectMany|변환 함수를 기반으로 하는 값의 시퀀스를 프로젝션한 다음 하나의 시퀀스로 평면화합니다.|여러 `From` 절 사용|<xref:System.Linq.Enumerable.SelectMany%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SelectMany%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-examples"></a>쿼리 식 구문 예제

### <a name="select"></a>셀렉트 버전

다음 예제에서는 `Select` 절을 사용하여 문자열 목록의 각 문자열에서 첫 글자를 프로젝션합니다.

```vb
Dim words = New List(Of String) From {"an", "apple", "a", "day"}

Dim query = From word In words
            Select word.Substring(0, 1)

Dim sb As New System.Text.StringBuilder()
For Each letter As String In query
    sb.AppendLine(letter)
Next

' Display the output.
MsgBox(sb.ToString())

' This code produces the following output:

' a
' a
' a
' d
```

### <a name="selectmany"></a>SelectMany

다음 예에서는 여러 개의 `From` 절을 사용 하 여 문자열 목록의 각 문자열에서 각 단어를 프로젝션 합니다.

```vb
Dim phrases = New List(Of String) From {"an apple a day", "the quick brown fox"}

Dim query = From phrase In phrases
            From word In phrase.Split(" "c)
            Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In query
    sb.AppendLine(str)
Next

' Display the output.
MsgBox(sb.ToString())

' This code produces the following output:

' an
' apple
' a
' day
' the
' quick
' brown
' fox
```

## <a name="select-versus-selectmany"></a>Select 및 SelectMany

`Select()` 및 `SelectMany()` 둘 다의 작업은 소스 값에서 결과 값을 생성하는 것입니다. `Select()`는 모든 소스 값에 대해 하나의 결과 값을 생성합니다. 따라서 전체 결과는 소스 컬렉션과 동일한 개수의 요소가 들어 있는 컬렉션입니다. 반면, `SelectMany()`는 각 소스 값에서 연결된 하위 컬렉션을 포함하는 하나의 전체 결과를 생성합니다. `SelectMany()`에 대한 인수로 전달되는 변환 함수는 각 소스 값에 대해 열거 가능한 값 시퀀스를 반환해야 합니다. 이러한 열거 가능한 시퀀스는 `SelectMany()`에 의해 연결되어 하나의 큰 시퀀스를 만듭니다.

다음 두 그림은 이러한 두 메서드의 작업 간에 개념적 차이를 보여 줍니다. 각각의 경우에서 선택기(변환) 함수는 각 소스 값에서 꽃의 배열을 선택한다고 가정합니다.

이 그림은 `Select()`에서 소스 컬렉션과 동일한 개수의 요소가 들어 있는 컬렉션을 반환하는 방법을 보여 줍니다.

![Select() 작업을 보여주는 그래픽](./media/projection-operations/select-action-graphic.png)

이 그림은 `SelectMany()`에서 배열의 중간 시퀀스를 각 중간 배열의 각 값이 포함된 하나의 최종 결과 값으로 연결하는 방법을 보여 줍니다.

![SelectMany() 작업을 보여주는 그래픽](./media/projection-operations/select-many-action-graphic.png )

### <a name="code-example"></a>코드 예제

다음 예제에서는 `Select()` 및 `SelectMany()`의 동작을 비교합니다. 코드는 소스 컬렉션의 각 꽃 이름 목록에서 처음 두 항목을 사용하여 꽃 "부케"를 만듭니다. 이 예제에서 변환 함수 <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>가 사용하는 “단일 값”은 값 컬렉션입니다. 이 경우 각 하위 시퀀스의 각 문자열을 열거하기 위해 `For Each` 루프가 추가로 필요합니다.

```vb
Class Bouquet
    Public Flowers As List(Of String)
End Class

Sub SelectVsSelectMany()
    Dim bouquets = New List(Of Bouquet) From {
        New Bouquet With {.Flowers = New List(Of String)(New String() {"sunflower", "daisy", "daffodil", "larkspur"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"tulip", "rose", "orchid"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"gladiolis", "lily", "snapdragon", "aster", "protea"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"larkspur", "lilac", "iris", "dahlia"})}}

    Dim output As New System.Text.StringBuilder

    ' Select()
    Dim query1 = bouquets.Select(Function(b) b.Flowers)

    output.AppendLine("Using Select():")
    For Each flowerList In query1
        For Each str As String In flowerList
            output.AppendLine(str)
        Next
    Next

    ' SelectMany()
    Dim query2 = bouquets.SelectMany(Function(b) b.Flowers)

    output.AppendLine(vbCrLf & "Using SelectMany():")
    For Each str As String In query2
        output.AppendLine(str)
    Next

    ' Display the output
    MsgBox(output.ToString())

    ' This code produces the following output:
    '
    ' Using Select():
    ' sunflower
    ' daisy
    ' daffodil
    ' larkspur
    ' tulip
    ' rose
    ' orchid
    ' gladiolis
    ' lily
    ' snapdragon
    ' aster
    ' protea
    ' larkspur
    ' lilac
    ' iris
    ' dahlia

    ' Using SelectMany()
    ' sunflower
    ' daisy
    ' daffodil
    ' larkspur
    ' tulip
    ' rose
    ' orchid
    ' gladiolis
    ' lily
    ' snapdragon
    ' aster
    ' protea
    ' larkspur
    ' lilac
    ' iris
    ' dahlia

End Sub
```

## <a name="see-also"></a>참조

- <xref:System.Linq>
- [표준 쿼리 연산자 개요(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Select 절](../../../../visual-basic/language-reference/queries/select-clause.md)
- [방법: 조인을 사용하여 데이터 결합](../../../../visual-basic/programming-guide/language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)
- [방법: 여러 소스로 개체 컬렉션 채우기 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)
- [방법: LINQ 쿼리 결과를 특정 형식으로 반환](../../../../visual-basic/programming-guide/language-features/linq/how-to-return-a-linq-query-result-as-a-specific-type.md)
- [방법: 그룹을 사용 하 여 파일을 여러 파일로 분할 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-split-a-file-into-many-files-by-using-groups-linq.md)
