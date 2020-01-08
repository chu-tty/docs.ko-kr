---
title: 사용자 지정 SQLite 버전
ms.date: 12/13/2019
description: 기본 SQLite 라이브러리의 사용자 지정 버전을 사용 하는 방법에 대해 알아봅니다.
ms.openlocfilehash: 8a2646138ea9dbecf412a2e8e0e347e2d71a5b0b
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450389"
---
# <a name="custom-sqlite-versions"></a><span data-ttu-id="667ef-103">사용자 지정 SQLite 버전</span><span class="sxs-lookup"><span data-stu-id="667ef-103">Custom SQLite versions</span></span>

<span data-ttu-id="667ef-104">SQLitePCLRaw을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-104">Microsoft.Data.Sqlite is built on top of SQLitePCLRaw.</span></span> <span data-ttu-id="667ef-105">번들을 사용 하거나 SQLitePCLRaw 공급자를 구성 하 여 기본 SQLite 라이브러리의 사용자 지정 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-105">You can use custom versions of the native SQLite library by using a bundle or by configuring a SQLitePCLRaw provider.</span></span>

## <a name="bundles"></a><span data-ttu-id="667ef-106">번들</span><span class="sxs-lookup"><span data-stu-id="667ef-106">Bundles</span></span>

<span data-ttu-id="667ef-107">SQLitePCLRaw는 다양 한 플랫폼에서 적절 한 종속성을 쉽게 가져올 수 있도록 번들 패키지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-107">SQLitePCLRaw provides bundle packages that make it easy to bring in the right dependencies across different platforms.</span></span>

<span data-ttu-id="667ef-108">기본적으로 bundle_e_sqlite3 SQLitePCLRaw는 주 Microsoft. Sqlite 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-108">The main Microsoft.Data.Sqlite package brings in SQLitePCLRaw.bundle_e_sqlite3 by default.</span></span>

<span data-ttu-id="667ef-109">다른 번들을 사용 하려면 사용 하려는 번들 패키지와 함께 `Microsoft.Data.Sqlite.Core` 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-109">To use a different bundle, install the `Microsoft.Data.Sqlite.Core` package instead along with the bundle package you want to use.</span></span> <span data-ttu-id="667ef-110">번들은 Microsoft. Data. Sqlite에 의해 자동으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-110">Bundles are automatically initialized by Microsoft.Data.Sqlite.</span></span>

| <span data-ttu-id="667ef-111">번들</span><span class="sxs-lookup"><span data-stu-id="667ef-111">Bundle</span></span> | <span data-ttu-id="667ef-112">설명</span><span class="sxs-lookup"><span data-stu-id="667ef-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="667ef-113">SQLitePCLRaw bundle_e_sqlite3</span><span class="sxs-lookup"><span data-stu-id="667ef-113">SQLitePCLRaw.bundle_e_sqlite3</span></span> | <span data-ttu-id="667ef-114">모든 플랫폼에서 SQLite의 일관 된 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-114">Provides a consistent version of SQLite on all platforms.</span></span> <span data-ttu-id="667ef-115">FTS4, FTS5, JSON1 및를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-115">Includes the FTS4, FTS5, JSON1, and</span></span> | <span data-ttu-id="667ef-116">R \* 트리 확장</span><span class="sxs-lookup"><span data-stu-id="667ef-116">R\*Tree extensions.</span></span> <span data-ttu-id="667ef-117">이것이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-117">This is the default.</span></span> |
| <span data-ttu-id="667ef-118">SQLitePCLRaw bundle_green</span><span class="sxs-lookup"><span data-stu-id="667ef-118">SQLitePCLRaw.bundle_green</span></span> | <span data-ttu-id="667ef-119">시스템 SQLite 라이브러리를 사용 하는 iOS를 제외 하 고 bundle_e_sqlite3와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-119">Same as bundle_e_sqlite3, except on iOS where it uses the system SQLite library.</span></span> |
| <span data-ttu-id="667ef-120">SQLitePCLRaw bundle_zetetic</span><span class="sxs-lookup"><span data-stu-id="667ef-120">SQLitePCLRaw.bundle_zetetic</span></span> | <span data-ttu-id="667ef-121">Zetetic의 공식 SQLCipher 빌드를 사용 합니다 (포함 되지 않음).</span><span class="sxs-lookup"><span data-stu-id="667ef-121">Uses the official SQLCipher builds from Zetetic (not included).</span></span> |
| <span data-ttu-id="667ef-122">SQLitePCLRaw bundle_winsqlite3</span><span class="sxs-lookup"><span data-stu-id="667ef-122">SQLitePCLRaw.bundle_winsqlite3</span></span> | <span data-ttu-id="667ef-123">Windows 10의 시스템 SQLite 라이브러리인 winsqlite3를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-123">Uses winsqlite3.dll, the system SQLite library on Windows 10.</span></span> |
| <span data-ttu-id="667ef-124">SQLitePCLRaw bundle_e_sqlcipher</span><span class="sxs-lookup"><span data-stu-id="667ef-124">SQLitePCLRaw.bundle_e_sqlcipher</span></span> | <span data-ttu-id="667ef-125">SQLCipher의 비공식 오픈 소스 빌드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-125">Provides an unofficial, open-source build of SQLCipher.</span></span> |

<span data-ttu-id="667ef-126">예를 들어, 비공식적으로 오픈 소스 SQLCipher 빌드를 사용 하려면 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-126">For example, to use the unofficial, open-source build of SQLCipher use the following commands.</span></span>

### <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="667ef-127">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="667ef-127">.NET Core CLI</span></span>](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite.Core
dotnet add package SQLitePCLRaw.bundle_e_sqlcipher
```

### <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="667ef-128">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="667ef-128">Visual Studio</span></span>](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite.Core
Install-Package SQLitePCLRaw.bundle_e_sqlcipher
```

---

## <a name="sqlitepclraw-providers"></a><span data-ttu-id="667ef-129">SQLitePCLRaw 공급자</span><span class="sxs-lookup"><span data-stu-id="667ef-129">SQLitePCLRaw providers</span></span>

<span data-ttu-id="667ef-130">`SQLitePCLRaw.provider.dynamic_cdecl` 패키지를 활용 하 여 SQLite의 고유한 빌드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-130">You can use your own build of SQLite by leveraging the `SQLitePCLRaw.provider.dynamic_cdecl` package.</span></span> <span data-ttu-id="667ef-131">이 경우 네이티브 라이브러리를 앱과 함께 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-131">In this case, you're responsible for deploying the native library with your app.</span></span> <span data-ttu-id="667ef-132">앱을 사용 하 여 네이티브 라이브러리를 배포 하는 방법에 대 한 세부 정보는 사용 중인 .NET 플랫폼과 런타임에 따라 크게 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-132">Note, the details of deploying native libraries with your app vary considerably depending on which .NET platform and runtime you're using.</span></span>

<span data-ttu-id="667ef-133">먼저 IGetFunctionPointer를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-133">First, you'll need to implement IGetFunctionPointer.</span></span> <span data-ttu-id="667ef-134">구현은 .NET Core에서 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-134">The implementation is fairly trivial on .NET Core.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_NativeLibraryAdapter)]

<span data-ttu-id="667ef-135">그런 다음 SQLitePCLRaw 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-135">Next, configure the SQLitePCLRaw provider.</span></span> <span data-ttu-id="667ef-136">이 작업은 앱에서 사용 하기 전에 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-136">Ensure this is done before Microsoft.Data.Sqlite is used in your app.</span></span> <span data-ttu-id="667ef-137">또한 공급자를 재정의할 수 있는 SQLitePCLRaw 번들 패키지를 사용 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="667ef-137">Also, avoid using a SQLitePCLRaw bundle package which might override your provider.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/SystemLibrarySample/Program.cs?name=snippet_SetProvider)]