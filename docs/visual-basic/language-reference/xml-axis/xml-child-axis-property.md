---
title: XML 자식 축 속성(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyChildAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
ms.openlocfilehash: 88d0b1f315bc1bb9dc474604d222a8ebcc1e40aa
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582235"
---
# <a name="xml-child-axis-property-visual-basic"></a>XML 자식 축 속성(Visual Basic)
<xref:System.Xml.Linq.XElement> 개체, <xref:System.Xml.Linq.XDocument> 개체, <xref:System.Xml.Linq.XElement> 개체 컬렉션 또는 <xref:System.Xml.Linq.XDocument> 개체 컬렉션 중 하나의 자식에 액세스할 수 있도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
object.<child>  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`object`|필수 요소. <xref:System.Xml.Linq.XElement> 개체, <xref:System.Xml.Linq.XDocument> 개체, <xref:System.Xml.Linq.XElement> 개체의 컬렉션 또는 <xref:System.Xml.Linq.XDocument> 개체의 컬렉션입니다.|  
|. <|필수 요소. 자식 축 속성의 시작을 나타냅니다.|  
|`child`|필수 요소. [@No__t_0 형식으로 액세스할 자식 노드의 이름입니다.<br /><br /> -    `Prefix`-선택 사항입니다. 자식 노드에 대한 XML 네임스페이스 접두사입니다. `Imports` 문으로 정의되는 전역 XML 네임스페이스여야 합니다.<br />-    `Name`-필수 항목입니다. 로컬 자식 노드 이름입니다. [선언 된 XML 요소 및 특성의 이름](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)을 참조 하세요.|  
|>|필수 요소. 자식 축 속성의 끝을 나타냅니다.|  
  
## <a name="return-value"></a>반환 값  
 <xref:System.Xml.Linq.XElement> 개체의 컬렉션입니다.  
  
## <a name="remarks"></a>주의  
 XML 자식 축 속성을 사용하여 <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체, <xref:System.Xml.Linq.XElement> 또는 <xref:System.Xml.Linq.XDocument> 개체 모음에서 이름을 기준으로 자식 노드에 액세스할 수 있습니다. XML을 `Value` 속성을 사용하여 반환 모음에 있는 첫 번째 자식 노드의 값에 액세스합니다. 자세한 내용은 [XML Value 속성](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)을 참조 하세요.  
  
 Visual Basic 컴파일러는 자식 축 속성을 <xref:System.Xml.Linq.XContainer.Elements%2A> 메서드에 대 한 호출로 변환 합니다.  
  
## <a name="xml-namespaces"></a>XML 네임스페이스  
 자식 축 속성의 이름은 `Imports` 문을 사용해 전역적으로 선언된 XML 네임스페이스 접두사만 사용할 수 있습니다. XML 요소 리터럴 내에서 로컬로 선언된 XML 네임스페이스 접두사를 사용할 수 없습니다. 자세한 내용은 [Imports 문 (XML 네임 스페이스)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `contact` 개체에서 이름이 `phone`인 자식 노드에 액세스하는 방법을 보여 줍니다.  
  
 [!code-vb[VbXMLSamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#17)]  
  
 이 코드의 텍스트는 다음과 같습니다.  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>예제  
 다음 예제에서는 `contacts` 개체의 `contact` 자식 축 속성에서 반환된 컬렉션에서 이름이 `phone`인 자식 노드에 액세스하는 방법을 보여 줍니다.  
  
 [!code-vb[VbXMLSamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#18)]  
  
 이 코드의 텍스트는 다음과 같습니다.  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>예제  
 다음 예제에서는 `ns`를 XML 네임스페이스 접두사로 선언한 다음 네임스페이스의 접두사를 사용하여 XML 리터럴을 만들고 정규화된 이름 `ns:name`을 가진 첫 번째 자식 노드에 액세스합니다.  
  
 [!code-vb[VbXMLSamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples8.vb#19)]  
  
 이 코드의 텍스트는 다음과 같습니다.  
  
 `Patrick Hines`  
  
## <a name="see-also"></a>참조

- <xref:System.Xml.Linq.XElement>
- [XML 축 속성](../../../visual-basic/language-reference/xml-axis/index.md)
- [XML 리터럴](../../../visual-basic/language-reference/xml-literals/index.md)
- [Visual Basic에서 XML 만들기](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [선언된 XML 요소 및 특성의 이름](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
