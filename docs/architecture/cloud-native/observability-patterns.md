---
title: 가시성 패턴
description: 클라우드 네이티브 응용 프로그램에 대 한 관찰성 패턴
ms.date: 09/23/2019
ms.openlocfilehash: 23320144c03278d631b8a1fcc1d1c0954e907296
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "73841068"
---
# <a name="observability-patterns"></a><span data-ttu-id="2aaf7-103">가시성 패턴</span><span class="sxs-lookup"><span data-stu-id="2aaf7-103">Observability patterns</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="2aaf7-104">응용 프로그램에서 코드 레이아웃을 지원 하기 위해 패턴을 개발 하는 것 처럼 신뢰할 수 있는 방식으로 운영 응용 프로그램에 대 한 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-104">Just as patterns have been developed to aid in the layout of code in applications, there are patterns for operating applications in a reliable way.</span></span> <span data-ttu-id="2aaf7-105">응용 프로그램 유지 관리에 대 한 세 가지 유용한 패턴 (로깅, 모니터링 및 경고)이 등장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-105">Three useful patterns in maintaining applications have emerged: logging, monitoring, and alerts.</span></span>

## <a name="when-to-use-logging"></a><span data-ttu-id="2aaf7-106">로깅을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="2aaf7-106">When to use logging</span></span>

<span data-ttu-id="2aaf7-107">아무리 신중 하 게 생각 해도 응용 프로그램은 거의 대부분 프로덕션에서 예기치 않은 방식으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-107">No matter how careful we are, applications almost always behave in unexpected ways in production.</span></span> <span data-ttu-id="2aaf7-108">사용자가 응용 프로그램에 대 한 문제를 보고할 때 문제가 발생 했을 때 응용 프로그램에서 어떤 일이 발생 했는지 확인할 수 있으면 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-108">When users report problems with an application, it's extremely useful to be able to see what was going on with the app when the problem occurred.</span></span> <span data-ttu-id="2aaf7-109">응용 프로그램이 실행 되는 동안 수행 되는 작업에 대 한 정보를 캡처하는 가장 많은 시도와 진정한 방법 중 하나는 응용 프로그램에서 수행 하는 작업을 기록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-109">One of the most tried and true ways of capturing information about what an application is doing while it's running is to have the application write down what it's doing.</span></span> <span data-ttu-id="2aaf7-110">이 프로세스를 로깅 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-110">This process is known as logging.</span></span> <span data-ttu-id="2aaf7-111">프로덕션 환경에서 오류 또는 문제가 발생 하는 경우에는 프로덕션 환경이 아닌 환경에서 오류가 발생 한 조건을 재현 하는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-111">Anytime failures or problems occur in production, the goal should be to reproduce the conditions under which the failures occurred, in a non-production environment.</span></span> <span data-ttu-id="2aaf7-112">적절 한 로깅은 테스트 하 고 실험 수 있는 환경에서 문제를 복제 하기 위해 수행할 수 있는 로드맵을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-112">Having good logging in place provides a roadmap for developers to follow in order to duplicate problems in an environment that can be tested and experimented with.</span></span>

### <a name="logging-in-cloud-native-applications"></a><span data-ttu-id="2aaf7-113">클라우드 네이티브 응용 프로그램의 로깅</span><span class="sxs-lookup"><span data-stu-id="2aaf7-113">Logging in cloud-native applications</span></span>

<span data-ttu-id="2aaf7-114">모든 프로그래밍 언어에는 로그 쓰기를 허용 하는 도구가 있으며 일반적으로 이러한 로그 작성에 대 한 오버 헤드가 적습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-114">Every programming language has tooling that permits writing logs, and typically the overhead for writing these logs is low.</span></span> <span data-ttu-id="2aaf7-115">대부분의 로깅 라이브러리는 런타임에 튜닝할 수 있는 다양 한 종류의 criticalities 로깅 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-115">Many of the logging libraries provide logging different kinds of criticalities, which can be tuned at run time.</span></span> <span data-ttu-id="2aaf7-116">예를 들어 Serilog library는 다음과 같은 로깅 수준을 제공 하는 .NET 용으로 널리 사용 되는 구조화 된 로깅 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-116">For instance, the Serilog library is a popular structured logging library for .NET that provides the following logging levels</span></span>

* <span data-ttu-id="2aaf7-117">자세히</span><span class="sxs-lookup"><span data-stu-id="2aaf7-117">Verbose</span></span>
* <span data-ttu-id="2aaf7-118">Debug</span><span class="sxs-lookup"><span data-stu-id="2aaf7-118">Debug</span></span>
* <span data-ttu-id="2aaf7-119">Information</span><span class="sxs-lookup"><span data-stu-id="2aaf7-119">Information</span></span>
* <span data-ttu-id="2aaf7-120">경고</span><span class="sxs-lookup"><span data-stu-id="2aaf7-120">Warning</span></span>
* <span data-ttu-id="2aaf7-121">Error</span><span class="sxs-lookup"><span data-stu-id="2aaf7-121">Error</span></span>
* <span data-ttu-id="2aaf7-122">심각한</span><span class="sxs-lookup"><span data-stu-id="2aaf7-122">Fatal</span></span>

<span data-ttu-id="2aaf7-123">이러한 서로 다른 로그 수준은 로깅의 세분성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-123">These different log levels provide granularity in logging.</span></span> <span data-ttu-id="2aaf7-124">응용 프로그램이 프로덕션 환경에서 제대로 작동 하는 경우 중요 한 메시지만 기록 하도록 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-124">When the application is functioning properly in production, it may be configured to only log important messages.</span></span> <span data-ttu-id="2aaf7-125">응용 프로그램이 오동작 경우 로그 수준을 늘려 자세한 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-125">When the application is misbehaving, then the log level can be increased so more verbose logs are gathered.</span></span> <span data-ttu-id="2aaf7-126">이렇게 하면 디버깅의 용이성과 비교 하 여 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-126">This balances performance against ease of debugging.</span></span>

<span data-ttu-id="2aaf7-127">로깅 도구의 고성능 및 자세한 정도는 개발자가 자주 로깅할 수 있도록 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-127">The high performance of logging tools and the tunability of verbosity should encourage developers to log frequently.</span></span> <span data-ttu-id="2aaf7-128">대부분의 경우 각 메서드의 진입 및 종료에 대 한 로깅 패턴을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-128">Many favor a pattern of logging the entry and exit of each method.</span></span> <span data-ttu-id="2aaf7-129">이 접근 방식은 과도 한 것 처럼 들리지만 개발자가 더 적은 로깅을 원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-129">This approach may sound like overkill, but it's infrequent that developers will wish for less logging.</span></span> <span data-ttu-id="2aaf7-130">실제로 문제를 해결 하는 방법에 대 한 로깅 추가 목적 으로만 배포를 수행 하는 것은 드문 일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-130">In fact, it's not uncommon to perform deployments for the sole purpose of adding logging around a problematic method.</span></span> <span data-ttu-id="2aaf7-131">너무 많은 로깅에 대 한 측면에서 오류는 너무 적습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-131">Err on the side of too much logging and not on too little.</span></span> <span data-ttu-id="2aaf7-132">일부 도구는 이러한 종류의 로깅을 자동으로 제공 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-132">Note that some tools can be used to automatically provide this kind of logging.</span></span>

<span data-ttu-id="2aaf7-133">기존 응용 프로그램에서 로그 파일은 일반적으로 로컬 컴퓨터에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-133">In traditional applications, log files were typically stored on the local machine.</span></span> <span data-ttu-id="2aaf7-134">실제로 Unix와 비슷한 운영 체제에서는 모든 로그를 저장 하도록 정의 된 폴더 구조, 즉 일반적으로 `/var/log`합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-134">In fact, on Unix-like operating systems, there's a folder structure defined to hold any logs, typically under `/var/log`.</span></span> <span data-ttu-id="2aaf7-135">단일 컴퓨터의 플랫 파일에 대 한 로그인의 유용성은 클라우드 환경에서 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-135">The usefulness of logging to a flat file on a single machine is vastly reduced in a cloud environment.</span></span> <span data-ttu-id="2aaf7-136">로그를 생성 하는 응용 프로그램은 로컬 디스크에 대 한 액세스 권한이 없을 수 있습니다. 또는 로컬 디스크는 물리적 컴퓨터에 섞은 컨테이너 이기 때문에 매우 일시적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-136">Applications producing logs may not have access to the local disk or the local disk may be highly transient as containers are shuffled around physical machines.</span></span>

<span data-ttu-id="2aaf7-137">마이크로 서비스 아키텍처를 사용 하 여 개발 된 클라우드 네이티브 응용 프로그램 에서도 파일 기반로 거에 대 한 몇 가지 문제를 야기 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-137">Cloud-native applications developed using a microservices architecture also pose some challenges for file-based loggers.</span></span> <span data-ttu-id="2aaf7-138">이제 사용자 요청은 서로 다른 컴퓨터에서 실행 되는 여러 서비스에 걸쳐 있을 수 있으며 로컬 파일 시스템에 대 한 액세스 권한이 없는 서버 리스 함수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-138">User requests may now span multiple services that are run on different machines, and may include serverless functions with no access to a local file system at all.</span></span> <span data-ttu-id="2aaf7-139">이러한 많은 서비스 및 컴퓨터에서 사용자 또는 세션의 로그를 상호 연결 하는 것은 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-139">It would be very challenging to correlate the logs from a user or a session across these many services and machines.</span></span>

<span data-ttu-id="2aaf7-140">마지막으로, 일부 클라우드 네이티브 응용 프로그램의 사용자 수가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-140">Finally, the number of users in some cloud-native applications is high.</span></span> <span data-ttu-id="2aaf7-141">각 사용자가 응용 프로그램에 로그인 할 때 100 줄의 로그 메시지를 생성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-141">Imagine that each user generates a hundred lines of log messages when they log into an application.</span></span> <span data-ttu-id="2aaf7-142">격리 되는 것은 관리 가능 하지만, 10만 사용자 및 로그의 양에 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-142">In isolation, that is manageable, but multiply that over 100,000 users and the volume of logs becomes large.</span></span>

<span data-ttu-id="2aaf7-143">다행히 파일 시스템 기반 로깅을 사용 하는 방법에 대 한 훌륭한 대안이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-143">Fortunately, there are some fantastic alternatives to using file system-based logging.</span></span> <span data-ttu-id="2aaf7-144">모든 로그가 전송 되는 중앙 집중식 로그 서버는 이러한 모든 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-144">A centralized log server to which all logs are sent, fixes all these problems.</span></span> <span data-ttu-id="2aaf7-145">로그는 응용 프로그램에 의해 수집 되 고 로그를 인덱싱하고 저장 하는 중앙 로깅 응용 프로그램에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-145">Logs are collected by the applications and shipped to a central logging application which indexes and stores the logs.</span></span> <span data-ttu-id="2aaf7-146">이 시스템 클래스는 매일 수십 기가바이트의 로그를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-146">This class of system can ingest tens of gigabytes of logs every day.</span></span>

<span data-ttu-id="2aaf7-147">여러 서비스에 걸쳐 있는 로깅을 빌드할 때 몇 가지 표준 사례를 따르는 것도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-147">It's also helpful to follow some standard practices when building logging that spans many services.</span></span> <span data-ttu-id="2aaf7-148">예를 들어 긴 상호 작용을 시작할 때 [상관 관계 ID](https://blog.rapid7.com/2016/12/23/the-value-of-correlation-ids/) 를 생성 한 다음 해당 상호 작용과 관련 된 각 메시지에 기록 하면 관련 된 모든 메시지를 더 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-148">For instance, generating a [correlation ID](https://blog.rapid7.com/2016/12/23/the-value-of-correlation-ids/) at the start of a lengthy interaction, and then logging it in each message that is related to that interaction, makes it easier to search for all related messages.</span></span> <span data-ttu-id="2aaf7-149">단일 메시지만 찾고 상관 관계 ID를 추출 하 여 관련 메시지를 모두 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-149">One need only find a single message and extract the correlation ID to find all the related messages.</span></span> <span data-ttu-id="2aaf7-150">또 다른 예는 모든 서비스에 대해 로그 형식이 동일한 지 확인 하는 것입니다 .이는 사용 하는 언어나 로깅 라이브러리에 상관 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-150">Another example is ensuring that the log format is the same for every service, whatever the language or logging library it uses.</span></span> <span data-ttu-id="2aaf7-151">이 표준화를 사용 하면 로그를 훨씬 더 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-151">This standardization makes reading logs much easier.</span></span> <span data-ttu-id="2aaf7-152">그림 7-1에서는 마이크로 서비스 아키텍처가 워크플로의 일부로 중앙화 된 로깅을 활용할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-152">Figure 7-1 demonstrates how a microservices architecture can leverage centralized logging as part of its workflow.</span></span>

<span data-ttu-id="2aaf7-153">다양 한 원본에서 ![로그는 중앙 집중식 로그 저장소로 수집 됩니다. **그림 7-1**을](./media/centralized-logging.png)
합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-153">![Logs from various sources are ingested into a centralized log store.](./media/centralized-logging.png)
**Figure 7-1**.</span></span> <span data-ttu-id="2aaf7-154">다양 한 원본의 로그는 중앙 집중식 로그 저장소로 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-154">Logs from various sources are ingested into a centralized log store.</span></span>

## <a name="when-to-use-monitoring"></a><span data-ttu-id="2aaf7-155">모니터링을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="2aaf7-155">When to use monitoring</span></span>

<span data-ttu-id="2aaf7-156">일부 응용 프로그램은 중요 업무용이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-156">Some applications aren't mission-critical.</span></span> <span data-ttu-id="2aaf7-157">이는 내부적 으로만 사용 되 고 문제가 발생 하는 경우 사용자가 팀에 연락 하 여 응용 프로그램을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-157">Maybe they're only used internally, and when a problem occurs, the user can contact the team responsible and the application can be restarted.</span></span> <span data-ttu-id="2aaf7-158">그러나 고객이 소비 하는 응용 프로그램에 대 한 기대 수준이 높은 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-158">However, customers often have higher expectations for the applications they consume.</span></span> <span data-ttu-id="2aaf7-159">사용자가 또는 사용자에 게 알리기 *전에 응용 프로그램* 에서 문제가 발생 하는 경우를 알고 있어야 하는 경우 현재 상태를 모니터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-159">If you need to know when problems occur with your application *before* users do, or before users notify you, you need to monitor its current state.</span></span> <span data-ttu-id="2aaf7-160">제대로 구현 된 모니터링을 사용 하면 문제를 야기 하는 조건을 알 수 있으므로 사용자에 게 영향을 미치기 전에 기본 조건을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-160">Implemented properly, monitoring can let you know about conditions that will lead to problems, letting you address underlying conditions before they result in any user impact.</span></span>

## <a name="monitoring-considerations"></a><span data-ttu-id="2aaf7-161">모니터링 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2aaf7-161">Monitoring considerations</span></span>

<span data-ttu-id="2aaf7-162">일부 중앙 집중식 로깅 시스템은 순수 로그 외부에서 원격 분석을 수집 하는 추가 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-162">Some centralized logging systems take on an additional role of collecting telemetry outside of pure logs.</span></span> <span data-ttu-id="2aaf7-163">데이터베이스 쿼리를 실행 하는 시간, 웹 서버의 평균 응답 시간, 운영 체제에서 보고 한 CPU 로드 평균 및 메모리 압력 등의 메트릭을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-163">They can collect metrics, such as time to run a database query, average response time from a web server, and even CPU load averages and memory pressure as reported by the operating system.</span></span> <span data-ttu-id="2aaf7-164">로그와 함께 이러한 시스템은 시스템 및 응용 프로그램 전체에서 노드의 상태에 대 한 전체적인 뷰를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-164">In conjunction with the logs, these systems can provide a holistic view of the health of nodes in the system and the application as a whole.</span></span>

<span data-ttu-id="2aaf7-165">모니터링 도구의 메트릭 수집 기능은 응용 프로그램 내에서 수동으로 공급할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-165">The metric gathering capabilities of the monitoring tools can also be fed manually from within the application.</span></span> <span data-ttu-id="2aaf7-166">새 사용자 등록 또는 배치 되는 주문과 같은 특정 관심이 있는 비즈니스 흐름은 중앙 모니터링 시스템에서 카운터를 증가 하도록 계측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-166">Business flows that are of particular interest such as new users signing up or orders being placed, may be instrumented such that they increment a counter in the central monitoring system.</span></span> <span data-ttu-id="2aaf7-167">이는 응용 프로그램의 상태를 모니터링할 뿐만 아니라 비즈니스의 상태를 모니터링할 수 있도록 모니터링 도구의 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-167">This unlocks the monitoring tools to not only monitor the health of the application but the health of the business.</span></span>

<span data-ttu-id="2aaf7-168">로그 집계 도구에서 쿼리를 생성 하 여 특정 통계 나 패턴을 찾을 수 있습니다. 그러면 사용자 지정 대시보드에서 그래픽 형태로 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-168">Queries can be constructed in the log aggregation tools to look for certain statistics or patterns, which can then be displayed in graphical form, on custom dashboards.</span></span> <span data-ttu-id="2aaf7-169">팀은 응용 프로그램과 관련 된 통계를 통해 회전 하는 크고 벽 장착식 디스플레이에 투자 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-169">Frequently, teams will invest in large, wall-mounted displays that rotate through the statistics related to an application.</span></span> <span data-ttu-id="2aaf7-170">이런 방식으로 문제가 발생할 때 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-170">This way, it's simple to see the problems as they occur.</span></span>

## <a name="when-to-use-alerts"></a><span data-ttu-id="2aaf7-171">경고를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="2aaf7-171">When to use alerts</span></span>

<span data-ttu-id="2aaf7-172">응용 프로그램의 문제에 대응 해야 하는 경우 적절 한 직원에 게 경고할 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-172">If you need to react to problems with your application, you need some way to alert the right personnel.</span></span> <span data-ttu-id="2aaf7-173">이는 세 번째 클라우드 네이티브 응용 프로그램 관찰성 패턴으로, 로깅 및 모니터링에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-173">This is the third cloud-native application observability pattern, and depends on logging and monitoring.</span></span> <span data-ttu-id="2aaf7-174">응용 프로그램에는 문제를 진단할 수 있도록 응용 프로그램을 준비 하 고, 경우에 따라 모니터링 도구에 공급 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-174">Your application needs to have logging in place to allow problems to be diagnosed, and in some cases to feed into monitoring tools.</span></span> <span data-ttu-id="2aaf7-175">응용 프로그램 메트릭 및 상태 데이터를 한 곳에서 집계 하려면 모니터링이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-175">It needs monitoring to aggregate application metrics and health data in one place.</span></span> <span data-ttu-id="2aaf7-176">이 설정이 완료 되 면 특정 메트릭이 허용 수준 외부에 있을 때 경고를 트리거하는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-176">Once this has been established, rules can be created that will trigger alerts when certain metrics fall outside of acceptable levels.</span></span>

## <a name="alerts"></a><span data-ttu-id="2aaf7-177">경고</span><span class="sxs-lookup"><span data-stu-id="2aaf7-177">Alerts</span></span>

<span data-ttu-id="2aaf7-178">모니터링 도구에 대해 쿼리를 작성 하 여 알려진 오류 조건을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-178">You can craft queries against the monitoring tools to look for known failure conditions.</span></span> <span data-ttu-id="2aaf7-179">예를 들어 쿼리는 HTTP 상태 코드 500 (웹 서버에서 문제를 나타냄)의 표시에 대해 들어오는 로그를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-179">For instance, queries could search through the incoming logs for indications of HTTP status code 500, which indicates a problem on a web server.</span></span> <span data-ttu-id="2aaf7-180">이러한 방법 중 하나가 감지 되 면 조사를 시작할 수 있는 원래 서비스의 소유자에 게 전자 메일 또는 SMS를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-180">As soon as one of these is detected, then an e-mail or an SMS could be sent to the owner of the originating service who can begin to investigate.</span></span>

<span data-ttu-id="2aaf7-181">일반적으로 500 오류가 발생 한 경우에는 문제가 발생 한 것을 확인 하기에 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-181">Typically though, a single 500 error isn't sufficient to determine that a problem has occurred.</span></span> <span data-ttu-id="2aaf7-182">사용자가 암호를 잘못 입력 하거나 일부 잘못 된 데이터를 입력 한 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-182">It could mean that a user mistyped their password or entered some malformed data.</span></span> <span data-ttu-id="2aaf7-183">500 오류가 발생 한 평균 수를 초과 하는 경우에만 발생 하도록 경고 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-183">The alert queries can be crafted to only fire when a larger than average number of 500 errors are detected.</span></span>

<span data-ttu-id="2aaf7-184">가장 손상 된 경고 패턴 중 하나는 사람이 조사할 수 있는 경고를 너무 많이 발생 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-184">One of the most damaging patterns in alerting is to fire too many alerts for humans to investigate.</span></span> <span data-ttu-id="2aaf7-185">서비스 소유자는 이전에 조사 했 고 심각 하지 않은 오류를 신속 하 게 desensitized 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-185">Service owners will rapidly become desensitized to errors that they've previously investigated and found to be benign.</span></span> <span data-ttu-id="2aaf7-186">True 오류가 발생 하면 수백 개의 거짓 긍정의 노이즈가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-186">When true errors occur then they'll be lost in the noise of hundreds of false positives.</span></span> <span data-ttu-id="2aaf7-187">늑대를 제대로 하는 [소년](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf) 은이 매우 위험에 대 한 경고를 표시 하는 어린이에 게 자주 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-187">The parable of the [Boy Who Cried Wolf](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf) is frequently told to children to warn them of this very danger.</span></span> <span data-ttu-id="2aaf7-188">발생 하는 경고는 실제 문제를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2aaf7-188">It's important to ensure that the alerts that do fire are indicative of a real problem.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="2aaf7-189">[이전](monitoring-health.md)
>[다음](logging-with-elastic-stack.md)</span><span class="sxs-lookup"><span data-stu-id="2aaf7-189">[Previous](monitoring-health.md)
[Next](logging-with-elastic-stack.md)</span></span>