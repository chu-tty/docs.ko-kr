---
title: ISymUnmanagedVariable::GetSignature 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetSignature
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetSignature
helpviewer_keywords:
- GetSignature method, ISymUnmanagedVariable interface [.NET Framework debugging]
- ISymUnmanagedVariable::GetSignature method [.NET Framework debugging]
ms.assetid: 78c1ba28-a410-4360-805c-23a95408964a
topic_type:
- apiref
ms.openlocfilehash: 2939d9cf3991a9e0b8f93bb301925b1092eca50e
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74446038"
---
# <a name="isymunmanagedvariablegetsignature-method"></a>ISymUnmanagedVariable::GetSignature 메서드
이 변수의 시그니처를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetSignature(  
    [in]  ULONG32  cSig,  
    [out] ULONG32  *pcSig,  
    [out, size_is(cSig),  
        length_is(*pcSig)] BYTE sig[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cSig`  
 진행 `sig` 매개 변수가 가리키는 버퍼의 길이입니다.  
  
 `pcSig`  
 제한이 서명을 포함 하는 데 필요한 버퍼의 크기 (문자 수)를 수신 하는 `ULONG32`에 대 한 포인터입니다.  
  
 `sig`  
 제한이 서명을 저장 하는 버퍼입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면이 고, 그렇지 않으면 S_OK입니다. 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym, CorSym  
  
## <a name="see-also"></a>참고 항목

- [ISymUnmanagedVariable 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-interface.md)
