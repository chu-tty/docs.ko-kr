---
title: 진단 기호 저장소 인터페이스
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- diagnostics symbol store interfaces [.NET Framework]
- interfaces [.NET Framework], diagnostics symbol store
- unmanaged interfaces [.NET Framework], diagnostics symbol store
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: f96987d5-e6a5-478b-ac5e-302e16545cce
ms.openlocfilehash: bdb691570a9a2bf7bd2bb21af500b06c10b0bc53
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448531"
---
# <a name="diagnostics-symbol-store-interfaces"></a>진단 기호 저장소 인터페이스
이 항목에서는 컴파일러가 디버거에서 사용할 기호 정보를 생성할 수 있도록 하는 관리 되지 않는 인터페이스에 대해 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [IBindingDisplay 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/ibindingdisplay-interface.md)  
 실행 중인 응용 프로그램에 대 한 현재 바인딩 정보를 표시 하는 메서드를 제공 합니다.  
  
 [IDebugAutoAttach 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/idebugautoattach-interface.md)  
 서버에서 호출 하는 디버거 자동 연결에 대 한 인터페이스를 정의 합니다.  
  
 [INotifyConnection2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifyconnection2-interface.md)  
 연결 알림 소스를 등록 및 등록 취소 하는 메서드를 선언 합니다.  
  
 [INotifySink2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifysink2-interface.md)  
 싱크 알림에 대 한 메서드를 선언 합니다.  
  
 [INotifySource2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifysource2-interface.md)  
 알림 필터를 설정 하는 메서드를 선언 합니다.  
  
 [ISymENCUnmanagedMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)  
 편집 하며 계속 하기 기능에 대 한 정보를 제공 합니다.  
  
 [ISymUnmanagedAsyncMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethod-interface.md)  
 이 인터페이스는 [ISymUnmanagedAsyncMethodPropertiesWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md)에 대 한 읽기 보수입니다.  
  
 [ISymUnmanagedAsyncMethodPropertiesWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md)  
 메서드 기호 당 선택적 비동기 메서드 정보를 정의할 수 있습니다. 는 열린 메서드와 함께 사용 해야 합니다. 즉, [Openmethod 메서드와](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openmethod-method.md) [closemethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closemethod-method.md)호출 사이에는를 사용 해야 합니다.  
  
 [ISymUnmanagedBinder 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder-interface.md)  
 비관리 코드에 대 한 기호 바인더를 나타냅니다.  
  
 [ISymUnmanagedBinder2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder2-interface.md)  
 비관리 코드에 대 한 기호 바인더를 나타내며 `ISymUnmanagedBinder` 인터페이스를 확장 합니다.  
  
 [ISymUnmanagedBinder3 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder3-interface.md)  
 비관리 코드에 대 한 기호 바인더를 나타내며 `ISymUnmanagedBinder` 인터페이스를 확장 합니다.  
  
 [ISymUnmanagedConstant 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-interface.md)  
 관리 되지 않는 상수에 대 한 액세스를 제공 합니다.  
  
 [ISymUnmanagedDispose 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddispose-interface.md)  
 관리 되지 않는 리소스를 삭제 합니다.  
  
 [ISymUnmanagedDocument 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)  
 기호 저장소가 참조하는 문서를 나타냅니다.  
  
 [ISymUnmanagedDocumentWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocumentwriter-interface.md)  
 기호 저장소가 참조하는 문서에 쓰기 위한 메서드를 제공합니다.  
  
 [ISymUnmanagedENCUpdate 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedencupdate-interface.md)  
 편집 하며 계속 하기 기능을 위한 메서드를 제공 합니다.  
  
 [ISymUnmanagedMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)  
 기호 저장소 내의 메서드를 나타냅니다.  
  
 [ISymUnmanagedNamespace 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagednamespace-interface.md)  
 네임 스페이스를 나타냅니다.  
  
 [ISymUnmanagedReader 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)  
 기호 저장소 내의 문서, 메서드 및 변수에 대 한 액세스를 제공 하는 기호 판독기를 나타냅니다.  
  
 [ISymUnmanagedReader2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader2-interface.md)  
 메서드 토큰과 편집 및 복사 버전 번호를 지정 하 여 기호 판독기 메서드를 가져옵니다.  
  
 [ISymUnmanagedReaderSymbolSearchInfo 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreadersymbolsearchinfo-interface.md)  
 기호 검색 정보를 가져오는 메서드를 제공 합니다.  
  
 [ISymUnmanagedScope 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope-interface.md)  
 메서드 내의 어휘 범위를 나타냅니다.  
  
 [ISymUnmanagedScope2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope2-interface.md)  
 메서드 내의 어휘 범위를 나타내고, 범위 내에 정의 된 상수에 대 한 정보를 가져오는 메서드로 `ISymUnmanagedScope` 인터페이스를 확장 합니다.  
  
 [ISymUnmanagedSourceServerModule 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsourceservermodule-interface.md)  
 모듈에 대 한 소스 서버 데이터를 제공 합니다.  
  
 [ISymUnmanagedSymbolSearchInfo 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-interface.md)  
 검색 경로에 대 한 정보를 가져오는 메서드를 제공 합니다.  
  
 [ISymUnmanagedVariable 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-interface.md)  
 매개 변수, 지역 변수 또는 필드와 같은 변수를 나타냅니다.  
  
 [ISymUnmanagedWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)  
 기호 작성기를 나타내며 문서, 시퀀스 위치, 어휘 범위 및 변수를 정의 하는 메서드를 제공 합니다.  
  
 [ISymUnmanagedWriter2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter2-interface.md)  
 기호 작성기를 나타내며 문서, 시퀀스 위치, 어휘 범위 및 변수를 정의 하는 메서드를 제공 합니다. `ISymUnmanagedWriter` 인터페이스를 확장 합니다.  
  
 [ISymUnmanagedWriter3 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)  
 기호 작성기를 나타내며 문서, 시퀀스 위치, 어휘 범위 및 변수를 정의 하는 메서드를 제공 합니다. `ISymUnmanagedWriter` 인터페이스를 확장 합니다.  
  
 [ISymUnmanagedWriter4 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter4-interface.md)  
 ISymUnmanagedWriter4 인터페이스입니다.  
  
 [ISymUnmanagedWriter5 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter5-interface.md)  
 ISymUnmanagedWriter5 인터페이스입니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [진단 기호 저장소 열거형](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-enumerations.md)  
  
 [진단 기호 저장소 구조체](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-structures.md)  
  
 [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
