---
title: ICorDebugVirtualUnwinder 인터페이스
ms.date: 03/30/2017
ms.assetid: a09e9ccc-0b37-43e3-95c1-bc5fa7ee5f42
ms.openlocfilehash: 532052aa4f869861fbdb40ba0126bfd800eba942
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73121871"
---
# <a name="icordebugvirtualunwinder-interface"></a>ICorDebugVirtualUnwinder 인터페이스
스택 해제에 도움이 되는 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|name|  
|------------|----------|  
|[GetContext 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugvirtualunwinder-getcontext-method.md)|이 해제기의 현재 컨텍스트를 가져옵니다.|  
|[Next 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugvirtualunwinder-next-method.md)|호출자의 컨텍스트로 이동합니다.|  
  
## <a name="remarks"></a>주의  
 `ICorDebugVirtualUnwinder` 인터페이스의 멤버는 스택 해제에 도움이 되도록 디버거에 의해 구현됩니다.  
  
> [!NOTE]
> 이 인터페이스는 .NET 네이티브에서만 사용할 수 있습니다. .NET 네이티브 외부의 ICorDebug 시나리오에 대해 이 인터페이스를 구현하는 경우 공용 언어 런타임에서 이 인터페이스를 무시합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>참조

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
