---
ms.openlocfilehash: acef6d7177ee5ad7e18dc8ba1e383d6f76263623
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394448"
---
### <a name="signalr-javascript-client-package-name-changed"></a>SignalR: JavaScript 클라이언트 패키지 이름이 변경됨

ASP.NET Core 3.0 Preview 7에서 SignalR JavaScript 클라이언트 패키지 이름이 `@aspnet/signalr`에서 `@microsoft/signalr`로 변경되었습니다. 이름 변경은 Azure SignalR Service 덕분에 SignalR은 ASP.NET Core 앱 이상에서만 유용하다는 사실을 반영합니다.

이 변경에 대응하려면 *package.json* 파일, `require` 문 및 ECMAScript `import` 문에서 참조를 변경합니다. 이 이름 바꾸기의 일부로 API가 변경되지 않습니다.

자세한 내용은 [aspnet/AspNetCore#11637](https://github.com/aspnet/AspNetCore/issues/11637)을 참조하세요.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="old-behavior"></a>이전 동작

클라이언트 패키지의 이름은 `@aspnet/signalr`이었습니다.

#### <a name="new-behavior"></a>새 동작

클라이언트 패키지의 이름은 `@microsoft/signalr`입니다.

#### <a name="reason-for-change"></a>변경 이유

이름 변경은 Azure SignalR Service 덕분에 SignalR은 ASP.NET Core 앱 이외에도 유용합니다.

#### <a name="recommended-action"></a>권장 작업

새 패키지 `@microsoft/signalr`로 전환합니다.

#### <a name="category"></a>범주

ASP.NET Core

#### <a name="affected-apis"></a>영향을 받는 API

없음

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
