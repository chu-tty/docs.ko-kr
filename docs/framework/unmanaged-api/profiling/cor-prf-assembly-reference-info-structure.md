---
title: COR_PRF_ASSEMBLY_REFERENCE_INFO 구조
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: c8c1d916-8d1a-4f82-8128-9fd3732383fc
ms.openlocfilehash: ac7ddeed5694ad0ae6ef3d4a11fcb1fb23755b8e
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73123223"
---
# <a name="cor_prf_assembly_reference_info-structure"></a>COR_PRF_ASSEMBLY_REFERENCE_INFO 구조
[.NET Framework 4.5.2 이상 버전에서 지원됨]  
  
 어셈블리 참조 closure 워커를 수행할 때 고려해야 하는 어셈블리 참조에 대한 정보를 공용 언어 런타임에 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _COR_PRF_ASSEMBLY_REFERENCE_INFO {  
    void* pbPublicKeyOrToken;  
    ULONG cbPublicKeyOrToken;  
    LPCWSTR szName;  
    ASSEMBLYMETADATA* pMetaData;  
    void* pbHashValue;  
    ULONG cbHashValue;  
    DWORD dwAssemblyRefFlags;  
} COR_PRF_EX_CLAUSE_INFO;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`pbPublicKeyOrToken`|어셈블리의 공개 키 또는 토큰에 대한 포인터입니다.|  
|`cbPublicKeyOrToken`|공개 키 또는 토큰의 바이트 수입니다.|  
|`szName`|참조되는 어셈블리의 이름입니다.|  
|`pMetaData`|어셈블리의 메타데이터에 대한 포인터입니다.|  
|`pbHashValue`|해시 BLOB(Binary Large Object)에 대한 포인터입니다.|  
|`cbHashValue`|해시 BLOB의 바이트 수입니다.|  
|`dwAssemblyRefFlags`|어셈블리의 플래그입니다.|  
  
## <a name="remarks"></a>주의  
 프로파일러는 어셈블리 참조 closure 워커를 수행할 때 공용 언어 런타임이 고려해야 하는 추가 어셈블리 참조를 선언할 때 `COR_PRF_EX_CLAUSE_INFO` 구조체를 채웁니다.  
  
 프로파일러가 [ICorProfilerCallback6:: GetAssemblyReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) 콜백 메서드를 등록 하는 경우 런타임은 로드 될 어셈블리의 경로와 이름 및 [ICorProfilerAssemblyReferenceProvider](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-interface.md) 에 대 한 포인터를 전달 합니다. 해당 메서드에 대 한 인터페이스 개체입니다. 그런 다음 프로파일러는 ICorProfilerCallback6::에 지정 된 어셈블리에서 참조 하려는 각 대상 어셈블리에 대해 `COR_PRF_ASSEMBLY_REFERENCE_INFO` 개체를 사용 하 여 [ICorProfilerAssemblyReferenceProvider:: AddAssemblyReference](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md) 메서드를 호출할 수 있습니다. [ GetAssemblyReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) 콜백입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>참조

- [프로파일링 구조체](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)
- [GetAssemblyReferences 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md)
- [AddAssemblyReference 메서드](../../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)
