---
title: ICorProfilerCallback::ObjectsAllocatedByClass 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ObjectsAllocatedByClass
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectsAllocatedByClass
helpviewer_keywords:
- ObjectsAllocatedByClass method [.NET Framework profiling]
- ICorProfilerCallback::ObjectsAllocatedByClass method [.NET Framework profiling]
ms.assetid: 91d688f3-a80e-419d-9755-ff94bc04188a
topic_type:
- apiref
ms.openlocfilehash: 9ba021ec223d00e57081567b76f70f59768e6b9a
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74445863"
---
# <a name="icorprofilercallbackobjectsallocatedbyclass-method"></a>ICorProfilerCallback::ObjectsAllocatedByClass 메서드
가장 최근 가비지 수집 이후 생성 된 각 지정 된 클래스의 인스턴스 수에 대해 프로파일러에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ObjectsAllocatedByClass(  
    [in] ULONG   cClassCount,  
    [in, size_is(cClassCount)] ClassID classIds[] ,  
    [in, size_is(cClassCount)] ULONG   cObjects[] );  
```  
  
## <a name="parameters"></a>매개 변수  
 `cClassCount`  
 진행 `classIds` 및 `cObjects` 배열의 크기입니다.  
  
 `classIds`  
 진행 각 ID가 하나 이상의 인스턴스를 포함 하는 클래스를 지정 하는 클래스 Id의 배열입니다.  
  
 `cObjects`  
 진행 정수 배열로, 각 정수는 `classIds` 배열의 해당 클래스에 대 한 인스턴스 수를 지정 합니다.  
  
## <a name="remarks"></a>주의  
 `classIds` 및 `cObjects` 배열은 병렬 배열입니다. 예를 들어 `classIds[i]` 및 `cObjects[i]`는 동일한 클래스를 참조 합니다. 이전 가비지 수집 이후 클래스의 인스턴스를 만들지 않은 경우에는 클래스가 생략 됩니다. `ObjectsAllocatedByClass` 콜백은 대량 개체 힙에 할당 된 개체를 보고 하지 않습니다.  
  
 `ObjectsAllocatedByClass`에서 보고 하는 숫자는 단지 추정치입니다. 정확한 개수에 대해 [ICorProfilerCallback:: ObjectAllocated](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectallocated-method.md)을 사용 합니다.  
  
 해당 `cObjects` 배열의 형식이 언로드되고 있으면 `classIds` 배열에 하나 이상의 null 항목이 포함 될 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [ICorProfilerCallback 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
