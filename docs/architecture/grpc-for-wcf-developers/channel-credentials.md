---
title: 채널 자격 증명-WCF 개발자를 위한 gRPC
description: ASP.NET Core 3.0에서 gRPC 채널 자격 증명을 구현 하 고 사용 하는 방법입니다.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 61141dc4143f36f9ac511c3369c3fde668c9d703
ms.sourcegitcommit: 337bdc5a463875daf2cc6883e5a2da97d56f5000
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2019
ms.locfileid: "73841668"
---
# <a name="channel-credentials"></a><span data-ttu-id="b050b-103">채널 자격 증명</span><span class="sxs-lookup"><span data-stu-id="b050b-103">Channel credentials</span></span>

<span data-ttu-id="b050b-104">이름에서 알 수 있듯이 채널 자격 증명은 기본 gRPC 채널에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-104">As the name implies, channel credentials are attached to the underlying gRPC channel.</span></span> <span data-ttu-id="b050b-105">채널 자격 증명의 표준 형식은 클라이언트 인증서 인증을 사용 합니다. 여기서 클라이언트는 연결을 만들 때 TLS 인증서를 제공 합니다 .이 인증을 사용 하면 호출을 허용 하기 전에 서버에서이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-105">The standard form of channel credentials uses Client Certificate authentication, where the client provides a TLS certificate when it's making the connection, which is verified by the server before allowing any calls to be made.</span></span>

<span data-ttu-id="b050b-106">채널 자격 증명을 통화 자격 증명과 결합 하 여 gRPC 서비스에 대 한 포괄적인 보안을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-106">Channel credentials can be combined with call credentials to provide comprehensive security for a gRPC service.</span></span> <span data-ttu-id="b050b-107">채널 자격 증명은 클라이언트 응용 프로그램에서 서비스에 액세스할 수 있음을 입증 하 고 호출 자격 증명은 클라이언트 응용 프로그램을 사용 하는 사용자에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-107">The channel credentials prove that the client application is allowed to access the service, and the call credentials provide information about the person using the client application.</span></span>

<span data-ttu-id="b050b-108">클라이언트 인증서 인증은 ASP.NET Core에 대해 작동 하는 것과 동일한 방식으로 gRPC에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-108">Client certificate authentication works for gRPC the same way it works for ASP.NET Core.</span></span> <span data-ttu-id="b050b-109">구성 프로세스는 여기에 요약 되어 있습니다. 자세한 내용은 [ASP.NET Core에서 인증서 인증 구성](https://docs.microsoft.com/aspnet/core/security/authentication/certauth?view=aspnetcore-3.0) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b050b-109">The configuration process will be summarized here, but more information is available in the [Configure certificate authentication in ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authentication/certauth?view=aspnetcore-3.0) article.</span></span>

<span data-ttu-id="b050b-110">개발 목적으로 자체 서명 된 인증서를 사용할 수 있지만 프로덕션의 경우 신뢰할 수 있는 기관에서 서명 된 적절 한 HTTPS 인증서를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-110">For development purposes you can use a self-signed certificate, but for production you should use a proper HTTPS certificate signed by a trusted authority.</span></span>

## <a name="adding-certificate-authentication-to-the-server"></a><span data-ttu-id="b050b-111">서버에 인증서 인증 추가</span><span class="sxs-lookup"><span data-stu-id="b050b-111">Adding certificate authentication to the server</span></span>

<span data-ttu-id="b050b-112">호스트 수준에서 인증서 인증을 구성 해야 합니다. 예를 들어 Kestrel 서버 및 ASP.NET Core 파이프라인에서 인증서 인증을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-112">You need to configure certificate authentication both at the host level, for example on the Kestrel server, and in the ASP.NET Core pipeline.</span></span>

### <a name="configuring-certificate-validation-on-kestrel"></a><span data-ttu-id="b050b-113">Kestrel에서 인증서 유효성 검사 구성</span><span class="sxs-lookup"><span data-stu-id="b050b-113">Configuring certificate validation on Kestrel</span></span>

<span data-ttu-id="b050b-114">클라이언트 인증서를 요구 하도록 Kestrel (ASP.NET Core HTTP 서버)을 구성 하 고, 들어오는 연결을 허용 하기 전에 제공 된 인증서의 일부 유효성 검사를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-114">You can configure Kestrel (the ASP.NET Core HTTP server) to require a client certificate, and optionally to carry out some validation of the supplied certificate before accepting incoming connections.</span></span> <span data-ttu-id="b050b-115">이 구성은 `Startup`아닌 `Program` 클래스의 `CreateWebHostBuilder` 메서드에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-115">This configuration is done in the `CreateWebHostBuilder` method of the `Program` class, rather than in `Startup`.</span></span>

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            var serverCert = ObtainServerCertificate();
            webBuilder.UseStartup<Startup>()
                .ConfigureKestrel(kestrelServerOptions => {
                    kestrelServerOptions.ConfigureHttpsDefaults(opt =>
                    {
                        opt.ClientCertificateMode = ClientCertificateMode.RequireCertificate;

                        // Verify that client certificate was issued by same CA as server certificate
                        opt.ClientCertificateValidation = (certificate, chain, errors) =>
                            certificate.Issuer == serverCert.Issuer;
                    });
                });
        });

```

<span data-ttu-id="b050b-116">`ClientCertificateMode.RequireCertificate` 설정에 의해 Kestrel은 클라이언트 인증서를 제공 하지 않는 연결 요청을 즉시 거부 하지만 인증서의 유효성은 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-116">The `ClientCertificateMode.RequireCertificate` setting will cause Kestrel to immediately reject any connection request that doesn't provide a client certificate, but it won't validate the certificate.</span></span> <span data-ttu-id="b050b-117">`ClientCertificateValidation` 콜백을 추가 하면 ASP.NET Core 파이프라인이 사용 되기 전에 Kestrel에서 클라이언트 인증서의 유효성을 검사할 수 있습니다 (이 경우 서버 인증서와 동일한 *인증 기관* 에서 발급 되었는지 확인).</span><span class="sxs-lookup"><span data-stu-id="b050b-117">Adding the `ClientCertificateValidation` callback enables Kestrel to validate the client certificate (in this case, ensuring that it was issued by the same *Certificate Authority* as the server certificate) at the point the connection is made, before the ASP.NET Core pipeline is engaged.</span></span>

### <a name="adding-aspnet-core-certificate-authentication"></a><span data-ttu-id="b050b-118">ASP.NET Core 인증서 인증 추가</span><span class="sxs-lookup"><span data-stu-id="b050b-118">Adding ASP.NET Core certificate authentication</span></span>

<span data-ttu-id="b050b-119">인증서 인증은 [AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) NuGet 패키지에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-119">Certificate authentication is provided by the [Microsoft.AspNetCore.Authentication.Certificate](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) NuGet package.</span></span>

<span data-ttu-id="b050b-120">`ConfigureServices` 메서드에서 인증서 인증 서비스를 추가 하 고 `Configure` 메서드에서 ASP.NET Core 파이프라인에 인증 및 권한 부여를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-120">Add the certificate authentication service in the `ConfigureServices` method, and add authentication and authorization to the ASP.NET Core pipeline in the `Configure` method.</span></span>

```csharp
public class Startup
{
    private readonly bool _isDevelopment;

    public Startup(IWebHostEnvironment env)
    {
        _isDevelopment = env.IsDevelopment();
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(CertificateAuthenticationDefaults.AuthenticationScheme)
            .AddCertificate(options =>
            {
                if (_isDevelopment)
                {
                    // DO NOT DO THIS IN PRODUCTION!
                    options.RevocationMode = X509RevocationMode.NoCheck;
                }
            });
        services.AddAuthorization();
        services.AddGrpc();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseRouting();

        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints => { endpoints.MapGrpcService<GreeterService>(); });
    }
}
```

## <a name="providing-channel-credentials-in-the-client-application"></a><span data-ttu-id="b050b-121">클라이언트 응용 프로그램에서 채널 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="b050b-121">Providing channel credentials in the client application</span></span>

<span data-ttu-id="b050b-122">`Grpc.Net.Client` 패키지를 사용 하면 연결에 사용 되는 `GrpcChannel`에 제공 되는 <xref:System.Net.Http.HttpClient> 인스턴스에 인증서가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-122">With the `Grpc.Net.Client` package, certificates are configured on an <xref:System.Net.Http.HttpClient> instance that is provided to the `GrpcChannel` used for the connection.</span></span>

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        // Assume path to a client .pfx file and password are passed from command line
        // On Windows this would probably be a reference to the Certificate Store
        var cert = new X509Certificate2(args[0], args[1]);

        var handler = new HttpClientHandler();
        handler.ClientCertificates.Add(cert);
        var httpClient = new HttpClient(handler);

        var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
        {
            HttpClient = httpClient
        });

        var grpc = new Greeter.GreeterClient(channel);
        var response = await grpc.SayHelloAsync(new HelloRequest { Name = "Bob" });
        System.Console.WriteLine(response.Message);
    }
}
```

## <a name="combining-channelcredentials-and-callcredentials"></a><span data-ttu-id="b050b-123">ChannelCredentials 및 CallCredentials 결합</span><span class="sxs-lookup"><span data-stu-id="b050b-123">Combining ChannelCredentials and CallCredentials</span></span>

<span data-ttu-id="b050b-124">인증서 변경 내용을 Kestrel 서버에 적용 하 고 ASP.NET Core JWT 전달자 미들웨어를 사용 하 여 서버에서 인증서와 토큰 인증을 모두 사용 하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-124">You can configure your server to use both certificate and token authentication by applying the certificate changes to the Kestrel server and using the JWT bearer middleware in ASP.NET Core.</span></span>

<span data-ttu-id="b050b-125">클라이언트에 ChannelCredentials와 CallCredentials를 모두 제공 하려면 `ChannelCredentials.Create` 메서드를 사용 하 여 호출 자격 증명을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-125">To provide both ChannelCredentials and CallCredentials on the client, use the `ChannelCredentials.Create` method to apply the call credentials.</span></span> <span data-ttu-id="b050b-126"><xref:System.Net.Http.HttpClient> 인스턴스를 사용 하 여 인증서 인증을 적용 해야 합니다. `SslCredentials` 생성자에 인수를 전달 하면 내부 클라이언트 코드에서 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-126">Certificate authentication still needs to be applied using the <xref:System.Net.Http.HttpClient> instance: if you pass any arguments to the `SslCredentials` constructor, the internal client code throws an exception.</span></span> <span data-ttu-id="b050b-127">`SslCredentials` 매개 변수는 `Grpc.Core` 패키지와의 호환성을 유지 하기 위해 `Grpc.Net.Client` 패키지의 `Create` 메서드에만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-127">The `SslCredentials` parameter is only included in the `Grpc.Net.Client` package's `Create` method to maintain compatibility with the `Grpc.Core` package.</span></span>

```csharp
var handler = new HttpClientHandler();
handler.ClientCertificates.Add(cert);

var httpClient = new HttpClient(handler);

var callCredentials = CallCredentials.FromInterceptor(((context, metadata) =>
    {
        metadata.Add("Authorization", $"Bearer {_token}");
    }));

var channelCredentials = ChannelCredentials.Create(new SslCredentials(), callCredentials);

var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
{
    HttpClient = httpClient,
    Credentials = channelCredentials
});

var grpc = new Portfolios.PortfoliosClient(channel);
```

> [!TIP]
> <span data-ttu-id="b050b-128">인증서 인증 없이 클라이언트에 대 한 `ChannelCredentials.Create` 메서드를 사용 하 여 채널에 대 한 모든 호출로 토큰 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-128">You can use the `ChannelCredentials.Create` method for a client without certificate authentication, as a useful way to pass token credentials with every call made on the channel.</span></span>

<span data-ttu-id="b050b-129">[인증서 인증을 추가한 FullStockTicker 샘플 gRPC 응용 프로그램](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker) 의 버전은 GitHub에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b050b-129">A version of the [FullStockTicker sample gRPC application with certificate authentication added](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker) is on GitHub.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="b050b-130">[이전](call-credentials.md)
>[다음](encryption.md)</span><span class="sxs-lookup"><span data-stu-id="b050b-130">[Previous](call-credentials.md)
[Next](encryption.md)</span></span>