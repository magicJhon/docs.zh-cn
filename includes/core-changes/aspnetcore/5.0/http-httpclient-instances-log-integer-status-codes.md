---
ms.openlocfilehash: 44d33fb28e66e590e4604c6dd2c73616e4c5e943
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728297"
---
### <a name="http-httpclient-instances-created-by-ihttpclientfactory-log-integer-status-codes"></a><span data-ttu-id="b2687-101">HTTP：IHttpClientFactory 创建的 HttpClient 实例记录整数状态代码</span><span class="sxs-lookup"><span data-stu-id="b2687-101">HTTP: HttpClient instances created by IHttpClientFactory log integer status codes</span></span>

<span data-ttu-id="b2687-102"><xref:System.Net.Http.IHttpClientFactory> 创建的 <xref:System.Net.Http.HttpClient> 实例将 HTTP 状态代码记录为整数而不是状态代码名称。</span><span class="sxs-lookup"><span data-stu-id="b2687-102"><xref:System.Net.Http.HttpClient> instances created by <xref:System.Net.Http.IHttpClientFactory> log HTTP status codes as integers instead of with status code names.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="b2687-103">引入的版本</span><span class="sxs-lookup"><span data-stu-id="b2687-103">Version introduced</span></span>

<span data-ttu-id="b2687-104">5.0 预览版 1</span><span class="sxs-lookup"><span data-stu-id="b2687-104">5.0 Preview 1</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="b2687-105">旧行为</span><span class="sxs-lookup"><span data-stu-id="b2687-105">Old behavior</span></span>

<span data-ttu-id="b2687-106">日志记录使用 HTTP 状态代码的文本说明。</span><span class="sxs-lookup"><span data-stu-id="b2687-106">Logging uses the textual descriptions of HTTP status codes.</span></span> <span data-ttu-id="b2687-107">考虑以下日志消息：</span><span class="sxs-lookup"><span data-stu-id="b2687-107">Consider the following log messages:</span></span>

```
Received HTTP response after 56.0044ms - OK
End processing HTTP request after 70.0862ms - OK
```

#### <a name="new-behavior"></a><span data-ttu-id="b2687-108">新行为</span><span class="sxs-lookup"><span data-stu-id="b2687-108">New behavior</span></span>

<span data-ttu-id="b2687-109">日志记录使用 HTTP 状态代码的整数值。</span><span class="sxs-lookup"><span data-stu-id="b2687-109">Logging uses the integer values of HTTP status codes.</span></span> <span data-ttu-id="b2687-110">考虑以下日志消息：</span><span class="sxs-lookup"><span data-stu-id="b2687-110">Consider the following log messages:</span></span>

```
Received HTTP response after 56.0044ms - 200
End processing HTTP request after 70.0862ms - 200
```

#### <a name="reason-for-change"></a><span data-ttu-id="b2687-111">更改原因</span><span class="sxs-lookup"><span data-stu-id="b2687-111">Reason for change</span></span>

<span data-ttu-id="b2687-112">此日志记录的原始行为与始终使用整数值的 ASP.NET Core 的其他部分不一致。</span><span class="sxs-lookup"><span data-stu-id="b2687-112">The original behavior of this logging is inconsistent with other parts of ASP.NET Core that have always used integer values.</span></span> <span data-ttu-id="b2687-113">不一致使通过结构化日志记录系统（如 [Elasticsearch](https://www.elastic.co/elasticsearch/)）查询日志变得困难。</span><span class="sxs-lookup"><span data-stu-id="b2687-113">The inconsistency makes logs difficult to query via structured logging systems such as [Elasticsearch](https://www.elastic.co/elasticsearch/).</span></span> <span data-ttu-id="b2687-114">有关详细信息，请参阅 [dotnet/extensions#1549](https://github.com/dotnet/extensions/issues/1549)。</span><span class="sxs-lookup"><span data-stu-id="b2687-114">For more context, see [dotnet/extensions#1549](https://github.com/dotnet/extensions/issues/1549).</span></span>

<span data-ttu-id="b2687-115">使用整数值比文本更灵活，因为它允许对值范围进行查询。</span><span class="sxs-lookup"><span data-stu-id="b2687-115">Using integer values is more flexible than text because it allows queries on ranges of values.</span></span>

<span data-ttu-id="b2687-116">考虑添加另一个日志值来捕获整数状态代码。</span><span class="sxs-lookup"><span data-stu-id="b2687-116">Adding another log value to capture the integer status code was considered.</span></span> <span data-ttu-id="b2687-117">遗憾的是，这样做会导致与 ASP.NET Core 的其余部分不一致。</span><span class="sxs-lookup"><span data-stu-id="b2687-117">Unfortunately, doing so would introduce another inconsistency with the rest of ASP.NET Core.</span></span> <span data-ttu-id="b2687-118">HttpClient 日志记录和 HTTP 服务器/托管日志记录使用相同的 `StatusCode` 密钥名称。</span><span class="sxs-lookup"><span data-stu-id="b2687-118">HttpClient logging and HTTP server/hosting logging use the same `StatusCode` key name already.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="b2687-119">建议操作</span><span class="sxs-lookup"><span data-stu-id="b2687-119">Recommended action</span></span>

<span data-ttu-id="b2687-120">最佳选择是更新日志记录查询，以使用状态代码的整数值。</span><span class="sxs-lookup"><span data-stu-id="b2687-120">The best option is to update logging queries to use the integer values of status codes.</span></span> <span data-ttu-id="b2687-121">这种方式可能会导致跨多个 ASP.NET Core 版本编写查询时遇到一些困难。</span><span class="sxs-lookup"><span data-stu-id="b2687-121">This option may cause some difficulty writing queries across multiple ASP.NET Core versions.</span></span> <span data-ttu-id="b2687-122">但是出于此目的使用整数查询日志会更加灵活。</span><span class="sxs-lookup"><span data-stu-id="b2687-122">However, using integers for this purpose is much more flexible for querying logs.</span></span>

<span data-ttu-id="b2687-123">如果需要强制与旧行为兼容并使用文本状态代码，请将 `IHttpClientFactory` 日志记录替换为你自己的日志记录：</span><span class="sxs-lookup"><span data-stu-id="b2687-123">If you need to force compatibility with the old behavior and use textual status codes, replace the `IHttpClientFactory` logging with your own:</span></span>

1. <span data-ttu-id="b2687-124">将以下类的 .NET Core 3.1 版本复制到项目中：</span><span class="sxs-lookup"><span data-stu-id="b2687-124">Copy the .NET Core 3.1 versions of the following classes into your project:</span></span>

    * [<span data-ttu-id="b2687-125">LoggingHttpMessageHandlerBuilderFilter</span><span class="sxs-lookup"><span data-stu-id="b2687-125">LoggingHttpMessageHandlerBuilderFilter</span></span>](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandlerBuilderFilter.cs)
    * [<span data-ttu-id="b2687-126">LoggingHttpMessageHandler</span><span class="sxs-lookup"><span data-stu-id="b2687-126">LoggingHttpMessageHandler</span></span>](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingHttpMessageHandler.cs)
    * [<span data-ttu-id="b2687-127">LoggingScopeHttpMessageHandler</span><span class="sxs-lookup"><span data-stu-id="b2687-127">LoggingScopeHttpMessageHandler</span></span>](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/LoggingScopeHttpMessageHandler.cs)
    * [<span data-ttu-id="b2687-128">HttpHeadersLogValue</span><span class="sxs-lookup"><span data-stu-id="b2687-128">HttpHeadersLogValue</span></span>](https://github.com/dotnet/extensions/blob/release/3.1/src/HttpClientFactory/Http/src/Logging/HttpHeadersLogValue.cs)

1. <span data-ttu-id="b2687-129">重命名类，以避免与 [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http) NuGet 包中的公共类型发生冲突。</span><span class="sxs-lookup"><span data-stu-id="b2687-129">Rename the classes to avoid conflicts with public types in the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http) NuGet package.</span></span>

1. <span data-ttu-id="b2687-130">在项目的 `Startup.ConfigureServices` 方法中，将 `LoggingHttpMessageHandlerBuilderFilter` 的内置实现替换为自己的实现。</span><span class="sxs-lookup"><span data-stu-id="b2687-130">Replace the built-in implementation of `LoggingHttpMessageHandlerBuilderFilter` with your own in the project's `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="b2687-131">例如：</span><span class="sxs-lookup"><span data-stu-id="b2687-131">For example:</span></span>

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        // Other service registrations go first. Code omitted for brevity.

        // Place the following after all AddHttpClient registrations.
        var descriptors = services.Where(
            s => s.ServiceType == typeof(IHttpMessageHandlerBuilderFilter));
        foreach (var descriptor in descriptors)
        {
            services.Remove(descriptor);
        }

        services.AddSingleton<IHttpMessageHandlerBuilderFilter,
                              MyLoggingHttpMessageHandlerBuilderFilter>();
    }
    ```

#### <a name="category"></a><span data-ttu-id="b2687-132">类别</span><span class="sxs-lookup"><span data-stu-id="b2687-132">Category</span></span>

<span data-ttu-id="b2687-133">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b2687-133">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="b2687-134">受影响的 API</span><span class="sxs-lookup"><span data-stu-id="b2687-134">Affected APIs</span></span>

<xref:System.Net.Http.HttpClient?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:System.Net.Http.HttpClient`

-->