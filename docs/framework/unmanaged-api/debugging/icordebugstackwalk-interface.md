---
title: ICorDebugStackWalk 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk
helpviewer_keywords:
- ICorDebugStackWalk interface [.NET Framework debugging]
ms.assetid: 16d695e8-975d-431b-8421-e9e6c3e3f476
topic_type:
- apiref
ms.openlocfilehash: 48f1b485b6dfa8fd898f6ea00eee2d7b397deba6
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131864"
---
# <a name="icordebugstackwalk-interface"></a>ICorDebugStackWalk 인터페이스
스레드 스택에서 관리되는 메서드나 프레임을 가져오기 위한 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetContext 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-getcontext-method.md)|`ICorDebugStackWalk` 개체의 현재 프레임에 대 한 컨텍스트를 반환 합니다.|  
|[SetContext 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-setcontext-method.md)|`ICorDebugStackWalk` 개체의 현재 컨텍스트를 스레드의 올바른 컨텍스트로 설정 합니다.|  
|[Next 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-next-method.md)|`ICorDebugStackWalk` 개체를 다음 프레임으로 이동 합니다.|  
|[GetFrame 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-getframe-method.md)|`ICorDebugStackWalk` 개체의 현재 프레임을 가져옵니다.|  
  
## <a name="remarks"></a>주의  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참조

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
