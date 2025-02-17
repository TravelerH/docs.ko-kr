---
title: Erase 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Erase
helpviewer_keywords:
- Erase keyword [Visual Basic]
- Erase statement [Visual Basic]
ms.assetid: 7a8133d7-b750-4d74-8b66-ba1dd9778d4b
ms.openlocfilehash: 7dec2a859f664ee8dcbb305082ec33aeacbaccb4
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583394"
---
# <a name="erase-statement-visual-basic"></a>Erase 문(Visual Basic)
배열 변수를 해제 하 고 해당 요소에 사용 되는 메모리의 할당을 취소 하는 데 사용 됩니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Erase arraylist  
```  
  
## <a name="parts"></a>요소  
 `arraylist`  
 필수 요소. 지울 배열 변수의 목록입니다. 여러 변수는 쉼표로 구분됩니다.  
  
## <a name="remarks"></a>주의  
 @No__t_0 문은 프로시저 수준 에서만 나타날 수 있습니다. 즉, 프로시저 내에서 배열을 해제할 수 있지만 클래스 또는 모듈 수준에서는 해제할 수 없습니다.  
  
 @No__t_0 문은 각 배열 변수에 `Nothing`를 할당 하는 것과 같습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Erase` 문을 사용 하 여 두 배열을 지우고 해당 메모리 (1000 및 100 저장소 요소 각각)를 해제 합니다. 그런 다음 `ReDim` 문은 3 차원 배열에 새 배열 인스턴스를 할당 합니다.  
  
 [!code-vb[VbVbalrStatements#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#19)]  
  
## <a name="see-also"></a>참조

- [Nothing](../../../visual-basic/language-reference/nothing.md)
- [ReDim 문](../../../visual-basic/language-reference/statements/redim-statement.md)
