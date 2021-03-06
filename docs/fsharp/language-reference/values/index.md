---
title: 값
description: 의 F# 값이 특정 형식을 갖는 수량을 확인 하는 방법에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: ed7a5b069a5a47aacf0cce4cfa754ded46f6e84a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630793"
---
# <a name="values"></a>값

F#의 값은 특정 형식을 가진 수량이며, 값은 정수 또는 부동 소수점 숫자, 문자 또는 텍스트, 목록, 시퀀스, 배열, 튜플, 구분된 공용 구조체, 레코드, 클래스 형식 또는 함수 값이 될 수 있습니다.

## <a name="binding-a-value"></a>값 바인딩

*바인딩*이란 용어는 이름과 정의를 연결하는 것을 의미합니다. `let` 키워드는 다음 예제와 같이 값을 바인딩합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet601.fs)]

특정 값의 형식은 정의에서 유추됩니다. 정수 또는 부동 소수점 숫자와 같은 기본 형식의 경우 형식은 리터럴 형식에서 결정됩니다. 따라서 앞의 예제에서 컴파일러는 `b`의 형식을 `unsigned int`로 유추하는 반면 컴파일러는 `a`의 형식을 `int`로 유추합니다. 함수 값의 형식은 함수 본문의 반환 값에서 결정됩니다. 함수 값 형식에 대한 자세한 내용은 [함수](../functions/index.md)를 참조하세요. 리터럴 형식에 대한 자세한 내용은 [리터럴](../literals.md)을 참조하세요.

컴파일러는 기본적으로 사용 되지 않는 바인딩에 대 한 진단을 실행 하지 않습니다. 이러한 메시지를 받으려면 컴파일러를 호출할 때 또는 프로젝트 파일에서 경고 1182를 사용 하도록 설정 합니다 `--warnon` ( [컴파일러 옵션](../compiler-options.md)아래 참조).

## <a name="why-immutable"></a>변경할 수 없는 이유

변경할 수 없는 값은 프로그램의 실행 과정에서 변경할 수 없는 값입니다. C++, Visual Basic, C# 등의 언어를 사용하는 경우, 프로그램의 실행 과정에서 F#이 새 값을 할당할 수 있는 변수보다 변경할 수 없는 값에 우선 순위를 두는 것이 낯설게 여겨질 수 있습니다. 변경 불가능한 데이터는 함수형 프로그래밍의 중요한 요소입니다. 다중 스레드 환경에서 여러 다양한 스레드에 의해 변경될 수 있는 공유 가변 변수는 관리하기가 어렵습니다. 또한 변경 가능한 변수를 사용할 경우 다른 함수에 전달되는 변수를 변경할 수 있는지 여부를 구분하는 것이 때로 어렵습니다.

순수 함수형 언어에서는, 변수가 없으며 함수는 수학 함수로 엄격하게 동작합니다. 프로시저 언어의 코드는 변수 할당을 사용하여 값을 변경하는 경우, 함수형 언어의 해당하는 코드에는 변경할 수 없는 값(입력), 변경할 수 없는 함수 및 여러 변경할 수 없는 값(출력)이 있습니다. 이러한 수학적 엄격성은 프로그램의 동작에 대한 트리거 추론을 허용합니다. 이러한 트리거 추론이 바로 컴파일러에서 코드를 보다 엄격하게 확인하고 보다 효과적으로 최적화할 수 있는 요인이며, 이를 통해 개발자는 올바른 코드를 쉽게 이해하고 작성할 수 있습니다. 따라서 함수형 코드는 일반적인 프로시저 코드보다 디버깅하기 쉬울 수 있습니다.

F#은 순수 함수형 언어가 아니지만 함수형 프로그래밍을 완전하게 지원합니다. 변경할 수 없는 값을 사용하면 코드가 함수형 프로그래밍의 중요한 측면에서 이점을 얻을 수 있으므로 그렇게 하는 것이 좋습니다.

## <a name="mutable-variables"></a>변경 가능한 변수

`mutable` 키워드를 사용하여 변경할 수 있는 변수를 지정할 수 있습니다. F#의 변경 가능한 변수에는 일반적으로 특정 형식의 필드로 또는 로컬 값의 제한된 범위가 있어야 합니다. 제한된 범위의 변경 가능한 변수는 더 쉽게 제어할 수 있으므로 잘못된 방법으로 수정하는 경우가 더 적습니다.

값을 정의할 때와 동일한 방식으로 `let` 키워드를 사용하여 변경 가능한 변수에 초기 값을 할당할 수 있습니다. 그러나 다음 예제와 같이, 이후에 `<-` 연산자를 사용하여 변경 가능한 변수에 새 값을 할당할 수 있다는 점이 다릅니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet602.fs)]

표시 `mutable` 된 값은 작성기와 `seq` 같이 `'a ref` 클로저를 만드는 폼을 포함 하 여 클로저로 캡처한 경우 자동으로로 승격 될 수 있습니다. 이 문제가 발생 하는 경우 알리도록 하려면 프로젝트 파일에서 또는 컴파일러를 호출할 때 경고 3180을 사용 하도록 설정 합니다.

## <a name="related-topics"></a>관련 항목

|제목|Description|
|-----|-----------|
|[let 바인딩](../functions/let-bindings.md)|`let` 키워드를 사용 하 여 이름을 값 및 함수에 바인딩하는 방법에 대 한 정보를 제공 합니다.|
|[함수](../functions/index.md)|F#의 함수를 간략하게 설명합니다.|

## <a name="see-also"></a>참고자료

- [Null 값](null-Values.md)
- [F# 언어 참조](../index.md)
