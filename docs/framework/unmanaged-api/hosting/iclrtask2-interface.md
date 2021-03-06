---
title: ICLRTask2 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRTask2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask2
helpviewer_keywords:
- ICLRTask2 interface [.NET Framework hosting]
ms.assetid: b5a22ebc-0582-49de-91f9-97a3d9789290
topic_type:
- apiref
ms.openlocfilehash: 47c6dd9045636bcfbe07c909fec3fda515d28ee8
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73124518"
---
# <a name="iclrtask2-interface"></a>ICLRTask2 인터페이스
는 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인터페이스의 모든 기능을 제공 합니다. 또한는 현재 스레드에서 스레드 중단이 지연 될 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[BeginPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-beginpreventasyncabort-method.md)|현재 스레드에서 새 스레드 중단 요청을 지연 시킵니다.|  
|[EndPreventAsyncAbort 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrtask2-endpreventasyncabort-method.md)|새 스레드 또는 보류 중인 스레드 중단 요청을 허용 하 여 현재 스레드에 대 한 스레드 중단을 발생 시킬 수 있습니다.|  
  
## <a name="remarks"></a>주의  
 `ICLRTask2` 인터페이스는 `ICLRTask` 인터페이스를 상속 하 고 호스트가 스레드 중단을 지연 하지 않아야 하는 코드 영역을 보호할 수 있도록 하는 메서드를 추가 합니다. `BeginPreventAsyncAbort`를 호출 하면 현재 스레드에 대 한 지연 스레드 중단 카운터가 증가 하 고 `EndPreventAsyncAbort`를 호출 하면 해당 카운터가 감소 합니다. `BeginPreventAsyncAbort` 및 `EndPreventAsyncAbort`에 대 한 호출은 중첩할 수 있습니다. 카운터가 0 보다 큰 경우 현재 스레드에 대 한 스레드 중단이 지연 됩니다.  
  
 `BeginPreventAsyncAbort` 및 `EndPreventAsyncAbort`에 대 한 호출이 페어링 되지 않은 경우 현재 스레드에 스레드 중단을 전달할 수 없는 상태에 도달할 수 있습니다.  
  
 자체를 중단 하는 스레드에는 지연이 적용 되지 않습니다.  
  
 이 기능에 의해 노출 되는 기능은 VM (가상 컴퓨터)에서 내부적으로 사용 됩니다. 이러한 메서드를 잘못 지정 하면 VM에서 지정 되지 않은 동작이 발생할 수 있습니다. 예를 들어 먼저 `BeginPreventAsyncAbort`를 호출 하지 않고 `EndPreventAsyncAbort`를 호출 하면 VM이 이전에 증가 한 경우 카운터를 0으로 설정할 수 있습니다. 마찬가지로 내부 카운터는 오버플로를 검사 하지 않습니다. 호스트와 VM이 모두 증가 하 여 정수 한도를 초과 하는 경우 결과 동작은 지정 되지 않습니다.  
  
 `ICLRTask`에서 상속 된 멤버와이 인터페이스의 다른 용도에 대 한 자세한 내용은 [ICLRTask](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md) 인터페이스를 참조 하세요.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICLRTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)
- [ICLRTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)
- [IHostTask 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)
- [IHostTaskManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
