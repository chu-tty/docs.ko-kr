---
title: CorDebugIntercept 열거형
ms.date: 03/30/2017
api_name:
- CorDebugIntercept
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugIntercept
helpviewer_keywords:
- CorDebugIntercept enumeration [.NET Framework debugging]
ms.assetid: 3d5b642e-7ef2-428b-a5ae-509c35ed461a
topic_type:
- apiref
ms.openlocfilehash: 144bdb1b4e479c1e75f89911ad5002e2650e405d
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73098119"
---
# <a name="cordebugintercept-enumeration"></a>CorDebugIntercept 열거형
가로챌 수 있는(즉, 한 단계씩 실행할 수 있는) 코드 형식을 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorDebugIntercept {  
    INTERCEPT_NONE                = 0x0,  
    INTERCEPT_CLASS_INIT          = 0x01,  
    INTERCEPT_EXCEPTION_FILTER    = 0x02,  
    INTERCEPT_SECURITY            = 0x04,  
    INTERCEPT_CONTEXT_POLICY      = 0x08,  
    INTERCEPT_INTERCEPTION        = 0x10,  
    INTERCEPT_ALL                 = 0xffff  
} CorDebugIntercept;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`INTERCEPT_NONE`|코드를 가로챌 수 없습니다.|  
|`INTERCEPT_CLASS_INIT`|생성자를 가로챌 수 있습니다.|  
|`INTERCEPT_EXCEPTION_FILTER`|예외 필터를 가로챌 수 있습니다.|  
|`INTERCEPT_SECURITY`|보안을 적용 하는 코드를 가로챌 수 있습니다.|  
|`INTERCEPT_CONTEXT_POLICY`|컨텍스트 정책을 가로챌 수 있습니다.|  
|`INTERCEPT_INTERCEPTION`|사용되지 않습니다.|  
|`INTERCEPT_ALL`|모든 코드를 가로챌 수 있습니다.|  
  
## <a name="remarks"></a>주의  
 [ICorDebugStepper:: SetInterceptMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setinterceptmask-method.md) 메서드를 사용 하 여 가로챌 수 있는 코드의 형식을 설정 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참조

- [디버깅 열거형](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
