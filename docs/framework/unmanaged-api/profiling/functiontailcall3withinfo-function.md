---
title: FunctionTailcall3WithInfo 함수
ms.date: 03/30/2017
api_name:
- FunctionTailcall3WithInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall3WithInfo
helpviewer_keywords:
- FunctionTailcall3WithInfo function [.NET Framework profiling]
ms.assetid: 46380fcc-0198-43ae-a1f5-2d4939425886
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9cd301ac9d82dd49fc9680d2724714f267ed88ae
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763292"
---
# <a name="functiontailcall3withinfo-function"></a>FunctionTailcall3WithInfo 함수
현재 실행 중인 함수를 다른 함수에 대 한 마무리 호출이 수행 하려고 하는 프로파일러에 알립니다 및 전달할 수 있는 핸들을 제공 합니다 [ICorProfilerInfo3::GetFunctionTailcall3Info 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md) 를 검색 하는 스택 프레임입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
void __stdcall FunctionTailcall3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a>매개 변수  
 `functionIDOrClientID`  
 [in] 마무리 호출을 수행 하려고 하는 현재 실행 중인 함수의 식별자입니다.  
  
 `eltInfo`  
 [in] 지정된 스택 프레임에 대한 정보를 나타내는 불투명 핸들입니다. 이 핸들이 전달 된 콜백 하는 동안에 유효 합니다.  
  
## <a name="remarks"></a>설명  
 `FunctionTailcall3WithInfo` 콜백 메서드를 사용 하 여 프로파일러가 호출 함수 처럼 프로파일러에 알립니다를 [ICorProfilerInfo3::GetFunctionTailcall3Info 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md) 스택 프레임을 검사 합니다. 스택 프레임 정보에 액세스할 수는 `COR_PRF_ENABLE_FRAME_INFO` 플래그를 설정 해야 합니다. 프로파일러를 사용할 수는 [icorprofilerinfo:: Seteventmask 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) 이벤트 플래그를 사용 하 여 합니다 [ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) 등록 프로그램 이 함수의 구현입니다.  
  
 `FunctionTailcall3WithInfo` 함수 콜백을 구현 해야 합니다. 구현을 사용 해야 합니다는 `__declspec(naked)` 저장소 클래스 특성입니다.  
  
 실행 엔진은이 함수를 호출 하기 전에 모든 레지스터를 저장 하지 않습니다.  
  
- 항목에는 부동 소수점 FPU (단위)에 포함 하 여 사용 하는 모든 레지스터를 저장 해야 합니다.  
  
- 종료 시 스택의 호출자에 의해 푸시된 모든 매개 변수에 팝 하 여 복원 해야 합니다.  
  
 구현의 `FunctionTailcall3WithInfo` 가비지 수집 지연 될 수 있으므로 차단 하지 않아야 합니다. 구현을 스택 가비지 컬렉션에 게 친숙 한 상태의 수 없을 수도 가비지 수집을 않아야 합니다. 런타임이 될 때까지 차단 됩니다 가비지 수집을 시도 하는 경우 `FunctionTailcall3WithInfo` 반환 합니다.  
  
 또한 FunctionTailcall3WithInfo 함수 해야 하지 관리 코드로 호출 하거나 어떤 방식으로 관리 되는 메모리를 할당 하면 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)
- [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)
- [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)
- [FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)
- [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)
- [SetEnterLeaveFunctionHooks3](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [SetEnterLeaveFunctionHooks3WithInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)
- [SetFunctionIDMapper2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)
- [프로파일링 전역 정적 함수](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
