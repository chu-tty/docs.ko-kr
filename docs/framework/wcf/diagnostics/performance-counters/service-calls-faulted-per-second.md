---
title: '서비스: Calls Faulted Per Second'
ms.date: 03/30/2017
ms.assetid: 94247356-2b29-4b50-b639-91ca8c1cf3a9
ms.openlocfilehash: 85c38f12c4d9bacf08597d465d831cf73e907cab
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72321443"
---
# <a name="service-calls-faulted-per-second"></a>서비스: Calls Faulted Per Second
카운터 이름: Calls Faulted Per Second  
  
## <a name="description"></a>설명  
 이 서비스에 오류를 반환한 초당 호출 수입니다.  
  
 이 카운터는 다음 수식을 사용 하 여 값을 계산 하는 성능 카운터 형식 [PERF_COUNTER_COUNTER](https://go.microsoft.com/fwlink/?LinkID=94649)입니다.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)  
  
 WCF (Windows Communication Foundation) 응용 프로그램에서 서비스 메서드는 SOAP 오류 메시지를 사용 하 여 처리 오류 정보를 전달 합니다. SOAP 오류는 서비스 작업의 메타데이터에 포함된 메시지 유형이므로 클라이언트가 실행을 더욱 견고하게 만들거나 대화형으로 만드는 데 사용할 수 있는 오류 계약을 만듭니다. SOAP 오류는 XML 형식으로 클라이언트에 표현되므로 상호 운용성이 매우 높습니다.  
  
## <a name="see-also"></a>참조

- [계약 및 서비스에서 오류 지정 및 처리](../../specifying-and-handling-faults-in-contracts-and-services.md)
