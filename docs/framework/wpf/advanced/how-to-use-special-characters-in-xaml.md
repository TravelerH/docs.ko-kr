---
title: '방법: XAML에서 특수 문자 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- Unicode UTF-8 file format
- UTF-8 file format
- characters [WPF], special
- typography [WPF], special characters
- special characters [WPF]
ms.assetid: a57776d1-f353-4794-afa0-bfa3c712ed1c
ms.openlocfilehash: 27f2b18593d075b54eb8c3351bbb84415700cfd4
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72395798"
---
# <a name="how-to-use-special-characters-in-xaml"></a>방법: XAML에서 특수 문자 사용
@No__t-0에서 만든 태그 파일은 유니코드 UTF-8 파일 형식으로 자동 저장 됩니다. 즉, 대부분의 특수 문자 (예: 악센트 표시)가 올바르게 인코딩됩니다. 그러나 다르게 처리되는 일반적으로 사용되는 특수 문자 집합이 있습니다. 이러한 특수 문자는 인코딩에 [!INCLUDE[TLA#tla_w3c](../../../../includes/tlasharptla-w3c-md.md)] [!INCLUDE[TL A#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 표준을 따릅니다.  
  
 다음 표는 이 특수 문자 집합을 인코딩하는 구문을 보여 줍니다.  
  
|문자|구문|설명|  
|---------------|------------|-----------------|  
|<|`&lt;`|보다 작음 기호|  
|>|`&gt;`|보다 큼 기호|  
|&|`&amp;`|앰퍼샌드 기호|  
|"|`&quot;`|큰따옴표 기호|  
  
> [!NOTE]
> Windows 메모장과 같은 텍스트 편집기를 사용 하 여 태그 파일을 만드는 경우 인코딩된 특수 문자를 유지 하기 위해 파일을 유니코드 UTF-8 파일 형식으로 저장 해야 합니다.  
  
 다음 예제에서는 태그를 만들 때 텍스트에 특수 문자를 사용하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[SpecialCharsSnippets#SpecialCharsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/SpecialCharsSnippets/CS/Window1.xaml#specialcharssnippet1)]
