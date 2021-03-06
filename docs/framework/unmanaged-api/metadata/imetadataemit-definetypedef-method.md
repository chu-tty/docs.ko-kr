---
title: IMetaDataEmit::DefineTypeDef 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineTypeDef
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineTypeDef
helpviewer_keywords:
- IMetaDataEmit::DefineTypeDef method [.NET Framework metadata]
- DefineTypeDef method [.NET Framework metadata]
ms.assetid: dd11c485-be95-4b97-9cd8-68679a4fb432
topic_type:
- apiref
ms.openlocfilehash: 031996813718a074eebab62ff54a2de52b898c22
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74450219"
---
# <a name="imetadataemitdefinetypedef-method"></a>IMetaDataEmit::DefineTypeDef 메서드
공용 언어 런타임 형식에 대 한 형식 정의를 만들고 해당 형식 정의에 대 한 메타 데이터 토큰을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineTypeDef (   
    [in]  LPCWSTR     szTypeDef,   
    [in]  DWORD       dwTypeDefFlags,   
    [in]  mdToken     tkExtends,   
    [in]  mdToken     rtkImplements[],   
    [out] mdTypeDef   *ptd  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szTypeDef`  
 진행 유니코드 형식의 이름입니다.  
  
 `dwTypeDefFlags`  
 [in] `TypeDef` 특성입니다. `CoreTypeAttr` 값의 비트 마스크입니다.  
  
 `tkExtends`  
 진행 기본 클래스의 토큰입니다. `mdTypeDef` 또는 `mdTypeRef` 토큰 이어야 합니다.  
  
 `rtkImplements`  
 진행 이 클래스 또는 인터페이스가 구현 하는 인터페이스를 지정 하는 토큰의 배열입니다.  
  
 `ptd`  
 제한이 할당 된 `mdTypeDef` 토큰입니다.  
  
## <a name="remarks"></a>주의  
 `dwTypeDefFlags`의 플래그는 생성 되는 형식이 공통 형식 시스템 참조 형식 (클래스 또는 인터페이스) 인지 아니면 공용 형식 시스템 값 형식 인지를 지정 합니다.  
  
 제공 된 매개 변수에 따라이 메서드는이 형식에 의해 상속 되거나 구현 되는 각 인터페이스에 대 한 `mdInterfaceImpl` 레코드를 만들 수도 있습니다. 그러나이 메서드는 이러한 `mdInterfaceImpl` 토큰을 반환 하지 않습니다. 클라이언트는 나중에 `mdInterfaceImpl` 토큰을 추가 하거나 수정 하려는 경우 `IMetaDataImport` 인터페이스를 사용 하 여이를 열거 해야 합니다. `[default]` 인터페이스의 COM 의미 체계를 사용 하려면 `rtkImplements`의 첫 번째 요소로 기본 인터페이스를 제공 해야 합니다. 클래스에 설정 된 사용자 지정 특성은 클래스에 기본 인터페이스가 있음을 나타내며이는 항상 클래스에 대해 선언 된 첫 번째 `mdInterfaceImpl` 토큰이 되는 것으로 간주 됩니다.  
  
 `rtkImplements` 배열의 각 요소는 `mdTypeDef` 또는 `mdTypeRef` 토큰을 보유 합니다. 배열의 마지막 요소는 `mdTokenNil`이어야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Cor  
  
 **라이브러리:** Mscoree.dll에서 리소스로 사용 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
