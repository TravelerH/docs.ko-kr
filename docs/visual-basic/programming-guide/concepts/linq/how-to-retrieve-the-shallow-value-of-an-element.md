---
title: '방법: 요소의 단순 값 검색 (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 730a6670-fb8c-41fc-8a1b-eb97a837e432
ms.openlocfilehash: 184186a92865b022118b9989633a97c75274e7f4
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72320429"
---
# <a name="how-to-retrieve-the-shallow-value-of-an-element-visual-basic"></a>방법: 요소의 단순 값 검색 (Visual Basic)

이 항목에서는 요소의 부분 값을 가져오는 방법을 보여 줍니다. 단일 문자열로 연결된 모든 하위 요소의 값을 포함하는 상세 값과 달리 부분 값은 특정 요소의 값입니다.

캐스팅을 사용하거나 <xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType> 속성을 사용하여 요소 값을 검색하는 경우에는 상세 값이 검색됩니다. 부분 값을 검색하려면 다음 예제와 같이 `ShallowValue` 확장 메서드를 사용합니다. 요소의 내용을 기준으로 요소를 선택하려는 경우에는 부분 값을 검색하는 것이 유용합니다.

다음 예제에서는 요소의 부분 값을 검색하는 확장 메서드를 선언합니다. 그런 다음 쿼리에 해당 확장명 메서드를 사용하여 계산된 값을 포함하는 모든 요소를 나열합니다.

## <a name="example"></a>예제

아래에 있는 Report.xml 텍스트 파일은 이 예제의 소스입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Report>
  <Section>
    <Heading>
      <Column Name="CustomerId">=Customer.CustomerId.Heading</Column>
      <Column Name="Name">=Customer.Name.Heading</Column>
    </Heading>
    <Detail>
      <Column Name="CustomerId">=Customer.CustomerId</Column>
      <Column Name="Name">=Customer.Name</Column>
    </Detail>
  </Section>
</Report>
```

```vb
Module Module1
    <System.Runtime.CompilerServices.Extension()> _
    Public Function ShallowValue(ByVal xe As XElement)
        Return xe _
               .Nodes() _
               .OfType(Of XText)() _
               .Aggregate(New StringBuilder(), _
                              Function(s, c) s.Append(c), _
                              Function(s) s.ToString())
    End Function

    Sub Main()
        Dim root As XElement = XElement.Load("Report.xml")

        Dim query As IEnumerable(Of XElement) = _
            From el In root.Descendants() _
            Where (el.ShallowValue().StartsWith("=")) _
            Select el

        For Each q As XElement In query
            Console.WriteLine("{0}{1}{2}", _
                q.Name.ToString().PadRight(8), _
                q.Attribute("Name").ToString().PadRight(20), _
                q.ShallowValue())
        Next
    End Sub
End Module
```

이 예제는 다음과 같은 출력을 생성합니다.

```console
Column  Name="CustomerId"   =Customer.CustomerId.Heading
Column  Name="Name"         =Customer.Name.Heading
Column  Name="CustomerId"   =Customer.CustomerId
Column  Name="Name"         =Customer.Name
```

## <a name="see-also"></a>참조

- [LINQ to XML 축(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-axes.md)
