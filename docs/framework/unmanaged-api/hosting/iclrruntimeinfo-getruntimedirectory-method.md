---
title: ICLRRuntimeInfo::GetRuntimeDirectory 메서드
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetRuntimeDirectory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetRuntimeDirectory
helpviewer_keywords:
- GetRuntimeDirectory method [.NET Framework hosting]
- ICLRRuntimeInfo::GetRuntimeDirectory method [.NET Framework hosting]
ms.assetid: 4401546e-4d48-453f-a1fb-b2ebda54df5c
topic_type:
- apiref
ms.openlocfilehash: b0a2e5f259fe1ee566f9cc25152b2d2a1f740bea
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2019
ms.locfileid: "73120335"
---
# <a name="iclrruntimeinfogetruntimedirectory-method"></a>ICLRRuntimeInfo::GetRuntimeDirectory 메서드
이 인터페이스와 연결 된 CLR (공용 언어 런타임)의 설치 디렉터리를 가져옵니다.  
  
 이 메서드는 .NET Framework 버전 2.0, 3.0 및 3.5에 제공 된 [GetCORSystemDirectory](../../../../docs/framework/unmanaged-api/hosting/getcorsystemdirectory-function.md) 함수를 대체 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRuntimeDirectory(  
[out, size_is(*pcchBuffer)] LPWSTR pwzBuffer,  
[in, out]  DWORD *pcchBuffer);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pwzBuffer`  
 제한이 CLR 설치 디렉터리를 반환 합니다. 설치 경로가 정규화 되어 있습니다. 예를 들면 "c:\windows\microsoft.net\framework\v1.0.3705\\"입니다.  
  
 `pchBuffer`  
 [in, out] 버퍼 오버런을 방지 하기 위해 `pwzBuffer`의 크기를 지정 합니다. `pwzBuffer`가 null 이면 `pchBuffer` `pwzBuffer`의 필수 크기를 반환 합니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.  
  
|HRESULT|설명|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다.|  
|E_POINTER|`pwzBuffer` 또는 `pchBuffer`가 null입니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** MetaHost  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참조

- [ICLRRuntimeInfo 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
