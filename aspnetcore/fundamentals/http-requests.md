---
title: 在 ASP.NET Core 中使用 IHttpClientFactory 發出 HTTP 要求
author: stevejgordon
description: 深入了解在 ASP.NET Core 中使用 IHttpClientFactory 介面來管理邏輯 HttpClient 執行個體。
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 01/25/2019
uid: fundamentals/http-requests
ms.openlocfilehash: a4026addaa55d463c41aadd0a7a39606c88fcb84
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024545"
---
# <a name="make-http-requests-using-ihttpclientfactory-in-aspnet-core"></a>在 ASP.NET Core 中使用 IHttpClientFactory 發出 HTTP 要求

作者：[Glenn Condron](https://github.com/glennc)、[Ryan Nowak](https://github.com/rynowak) 和 [Steve Gordon](https://github.com/stevejgordon)

<xref:System.Net.Http.IHttpClientFactory> 可以註冊及用來在應用程式中設定和建立 <xref:System.Net.Http.HttpClient> 執行個體。 它提供下列優點：

* 提供一個集中位置以便命名和設定邏輯 `HttpClient` 執行個體。 例如，您可以註冊 *github* 並設定用戶端以存取 GitHub。 預設用戶端可以註冊用於其他用途。
* 透過委派 `HttpClient` 中的處理常式來撰寫外寄中介軟體的概念，並提供延伸模組以便 Polly 架構中介軟體利用外寄中介軟體。
* 管理基礎 `HttpClientMessageHandler` 執行個體的共用和存留期，以避免在手動管理 `HttpClient` 存留期時，發生的常見 DNS 問題。
* 針對透過處理站所建立之用戶端傳送的所有要求，新增可設定的記錄體驗 (透過 `ILogger`)。

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/http-requests/samples) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

## <a name="prerequisites"></a>必要條件

以 .NET Framework 為目標的專案，需要安裝 [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) NuGet 套件。 以 .NET Core 為目標且參考 [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) 的專案，已包含 `Microsoft.Extensions.Http` 套件。

## <a name="consumption-patterns"></a>耗用模式

有數種方式可將 `IHttpClientFactory` 用於應用程式：

* [基本使用方式](#basic-usage)
* [具名用戶端](#named-clients)
* [具型別用戶端](#typed-clients)
* [產生的用戶端](#generated-clients)

它們全都不會嚴格優先於另一個。 最好的方法取決於應用程式的條件約束。

### <a name="basic-usage"></a>基本使用方式

`IHttpClientFactory` 可以藉由在 `Startup.ConfigureServices` 方法內的 `IServiceCollection` 上呼叫 `AddHttpClient` 擴充方法來註冊。

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet1)]

註冊之後，程式碼可以在可使用[相依性插入 (DI)](xref:fundamentals/dependency-injection) 插入服務的任何位置，接受 `IHttpClientFactory`。 `IHttpClientFactory` 可以用來建立 `HttpClient` 執行個體：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/BasicUsage.cshtml.cs?name=snippet1&highlight=9-12,21)]

以這種方式使用 `IHttpClientFactory` 是重構現有應用程式的好方法。 它對 `HttpClient` 的使用方式沒有任何影響。 在目前建立 `HttpClient` 執行個體的位置，將那些項目取代為呼叫 <xref:System.Net.Http.IHttpClientFactory.CreateClient*>。

### <a name="named-clients"></a>具名用戶端

如果應用程式需要使用多個不同的 `HttpClient`，且每個都有不同的設定，可以選擇使用**具名用戶端**。 具名 `HttpClient` 的組態可以在 `Startup.ConfigureServices` 中註冊時指定。

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet2)]

在上述程式碼中，會呼叫 `AddHttpClient` 並提供名稱 *github*。 此用戶端已套用一些預設組態&mdash;即使用 GitHub API 所需的基底位址和兩個標頭。

每次呼叫 `CreateClient` 時，會建立 `HttpClient` 的新執行個體並呼叫組態動作。

若要使用具名用戶端，可以傳遞字串參數至 `CreateClient`。 指定要建立之用戶端的名稱：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/NamedClient.cshtml.cs?name=snippet1&highlight=21)]

在上述程式碼中，要求不需要指定主機名稱。 它可以只傳遞路徑，因為已使用為用戶端設定的基底位址。

### <a name="typed-clients"></a>具型別用戶端

具型別用戶端提供與具名用戶端相同的功能，而不需要使用字串作為索引鍵。 具型別用戶端方法在使用用戶端時提供 IntelliSense 和編譯器說明。 它們提供單一位置來設定特定 `HttpClient` 並與其互動。 例如，單一的具型別用戶端可能用於單一的後端端點，並封裝處理該端點的所有邏輯。 另一個優點是它們使用 DI 且可以在應用程式中需要之處插入。

具型別用戶端在其建構函式中接受 `HttpClient` 參數：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/GitHub/GitHubService.cs?name=snippet1&highlight=5)]

在上述程式碼中，組態會移到具型別用戶端。 `HttpClient` 物件會公開為公用屬性。 您可定義 API 特定的方法，其公開 `HttpClient` 功能。 `GetAspNetDocsIssues` 方法會封裝從 GitHub 存放庫查詢和剖析最新開啟問題所需的程式碼。

若要註冊具型別用戶端，泛型 <xref:Microsoft.Extensions.DependencyInjection.HttpClientFactoryServiceCollectionExtensions.AddHttpClient*> 擴充方法可用於 `Startup.ConfigureServices` 內，並指定具型別用戶端類別：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet3)]

具型別用戶端會向 DI 註冊為暫時性。 具型別用戶端可以直接插入並使用：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Pages/TypedClient.cshtml.cs?name=snippet1&highlight=11-14,20)]

想要的話，具型別用戶端的組態可以在 `Startup.ConfigureServices` 中註冊時指定，而不是在具型別用戶端的建構函式中：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet4)]

可以將 `HttpClient` 完全封裝在具型別用戶端內。 可以提供在內部呼叫 `HttpClient` 執行個體的公用方法，而不將它公開為屬性。

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/GitHub/RepoService.cs?name=snippet1&highlight=4)]

在上述程式碼，`HttpClient` 儲存為私用欄位。 進行外部呼叫的所有存取都會經歷 `GetRepos` 方法。

### <a name="generated-clients"></a>產生的用戶端

`IHttpClientFactory` 可和其他協力廠商程式庫一起使用，例如 [Refit](https://github.com/paulcbetts/refit)。 Refit 是適用於 .NET 的 REST 程式庫。 它將 REST API 轉換為即時介面。 介面的實作由 `RestService` 動態產生，並使用 `HttpClient` 進行外部 HTTP 呼叫。

定義介面及回覆來代表外部 API 和其回應：

```csharp
public interface IHelloClient
{
    [Get("/helloworld")]
    Task<Reply> GetMessageAsync();
}

public class Reply
{
    public string Message { get; set; }
}
```

可以新增具型別用戶端，使用 Refit 產生實作：

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddHttpClient("hello", c =>
    {
        c.BaseAddress = new Uri("http://localhost:5000");
    })
    .AddTypedClient(c => Refit.RestService.For<IHelloClient>(c));

    services.AddMvc();
}
```

定義的介面可在需要時使用，並搭配 DI 與 Refit 所提供的實作：

```csharp
[ApiController]
public class ValuesController : ControllerBase
{
    private readonly IHelloClient _client;

    public ValuesController(IHelloClient client)
    {
        _client = client;
    }

    [HttpGet("/")]
    public async Task<ActionResult<Reply>> Index()
    {
        return await _client.GetMessageAsync();
    }
}
```

## <a name="outgoing-request-middleware"></a>外寄要求中介軟體

`HttpClient` 已經有委派可針對外寄 HTTP 要求連結在一起的處理常式的概念。 `IHttpClientFactory` 可讓您輕鬆地定義要套用於每個具名用戶端的處理常式。 它支援註冊和鏈結多個處理常式，以建置外寄要求中介軟體管線。 這些處理常式每個都可以在外寄要求之前和之後執行工作。 此模式與 ASP.NET Core 中的輸入中介軟體管線相似。 模式提供一個機制來管理 HTTP 要求的跨領域關注，包括快取、錯誤處理、序列化和記錄。

若要建立處理常式，請定義衍生自 <xref:System.Net.Http.DelegatingHandler> 的類別。 覆寫 `SendAsync` 方法，以在將要求傳遞至管線中的下一個處理常式之前執行程式碼：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Handlers/ValidateHeaderHandler.cs?name=snippet1)]

上述程式碼定義一個基本處理常式。 它會檢查以查看要求上是否已包含 `X-API-KEY` 標頭。 如果遺漏標頭，它可以避免 HTTP 呼叫，並傳回適當的回應。

在註冊期間，可以新增一或多個處理常式至 `HttpClient` 的組態。 這項工作是透過 <xref:Microsoft.Extensions.DependencyInjection.IHttpClientBuilder> 上的擴充方法完成。

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet5)]

::: moniker range=">= aspnetcore-2.2"

在上述程式碼，`ValidateHeaderHandler` 已向 DI 註冊。 `IHttpClientFactory` 會為每個處理常式建立個別的 DI 範圍。 處理常式可相依於任何範圍的服務。 處置處理常式時，會處置處理常式所相依的服務。

註冊之後，便可以呼叫 <xref:Microsoft.Extensions.DependencyInjection.HttpClientBuilderExtensions.AddHttpMessageHandler*>，並傳入處理常式的類型。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

在上述程式碼，`ValidateHeaderHandler` 已向 DI 註冊。 處理常式**必須**在 DI 中註冊為暫時性服務，無限定範圍。 若處理常式已註冊為具範圍服務，而且已處置處理常式所相依的任何服務，可在處理常式移出範圍之前處置處理常式的服務，這會導致處理常式失敗。

註冊之後，便可以呼叫 <xref:Microsoft.Extensions.DependencyInjection.HttpClientBuilderExtensions.AddHttpMessageHandler*>，並傳入處理常式類型。

::: moniker-end

可以遵循應該執行的順序來註冊多個處理常式。 每個處理常式會包裝下一個處理常式，直到最終 `HttpClientHandler` 執行要求：

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet6)]

使用下列其中一種方式來與訊息處理常式共用個別要求狀態：

* 使用 `HttpRequestMessage.Properties` 將資料傳遞到處理常式。
* 使用 `IHttpContextAccessor` 來存取目前的要求。
* 建立自訂 `AsyncLocal` 儲存體物件以傳遞資料。

## <a name="use-polly-based-handlers"></a>使用 Polly 為基礎的處理常式

`IHttpClientFactory` 整合受歡迎的協力廠商程式庫，稱為 [Polly](https://github.com/App-vNext/Polly)。 Polly 是適用於 .NET 的完整恢復功能和暫時性錯誤處理程式庫。 它可讓開發人員以流暢且執行緒安全的方式表達原則，例如重試、斷路器、逾時、艙隔離與後援。

提供擴充方法來啟用使用 Polly 原則搭配設定的 `HttpClient` 執行個體。 Polly 延伸模組提供於 [Microsoft.Extensions.Http.Polly](https://www.nuget.org/packages/Microsoft.Extensions.Http.Polly/) NuGet 套件中。 [Microsoft.AspNetCore.App 中繼套件](xref:fundamentals/metapackage-app)未包含此套件。 若要使用延伸模組，專案中應該要包含明確的 `<PackageReference />`。

[!code-csharp[](http-requests/samples/2.x/HttpClientFactorySample/HttpClientFactorySample.csproj?highlight=9)]

在還原此套件之後，擴充方法可用來支援將 Polly 為基礎的處理常式新增至用戶端。

### <a name="handle-transient-faults"></a>處理暫時性錯誤

大部分的錯誤發生在外部 HTTP 呼叫是暫時性的時候。 包含一個便利的擴充方法，稱為 `AddTransientHttpErrorPolicy`，它可允許定義原則來處理暫時性錯誤。 使用此延伸模組方法設定的原則，會處理 `HttpRequestException`、HTTP 5xx 回應和 HTTP 408 回應。

`AddTransientHttpErrorPolicy` 延伸模組可用於 `Startup.ConfigureServices` 內。 延伸模組能提供 `PolicyBuilder` 物件的存取，該物件已設定來處理代表可能暫時性錯誤的錯誤：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet7)]

在上述程式碼，已定義了 `WaitAndRetryAsync` 原則。 失敗的要求會重試最多三次，並且在嘗試之間會有 600 毫秒的延遲時間。

### <a name="dynamically-select-policies"></a>動態選取原則

有額外的擴充方法可用來新增 Polly 為基礎的處理常式。 其中一個這類延伸模組是 `AddPolicyHandler`，它有多個多載。 一個多載可讓您在定義要套用的原則時，檢查要求：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet8)]

在上述程式碼中，如果外寄要求是 GET，就會套用 10 秒逾時。 任何其他 HTTP 方法會使用 30 秒逾時。

### <a name="add-multiple-polly-handlers"></a>新增多個 Polly 處理常式

通常會建立巢狀 Polly 原則，以提供增強的功能：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet9)]

在上述範例中，會新增兩個處理常式。 第一個使用 `AddTransientHttpErrorPolicy` 延伸模組來新增重試原則。 失敗的要求會重試最多三次。 第二個 `AddTransientHttpErrorPolicy` 呼叫會新增斷路器原則。 如果循序發生五次失敗的嘗試，進一步的外部要求會遭到封鎖 30 秒。 斷路器原則可設定狀態。 透過此用戶端的所有呼叫都會共用相同的線路狀態。

### <a name="add-policies-from-the-polly-registry"></a>從 Polly 登錄新增原則

管理定期使用原則的一個方法是定義一次，並向 `PolicyRegistry` 註冊它們。 提供了擴充方法，可以使用來自登錄的原則新增處理常式：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet10)]

在上述程式碼中，當 `PolicyRegistry` 新增至 `ServiceCollection` 時，註冊了兩個原則。 為了使用來自登錄的原則，使用了 `AddPolicyHandlerFromRegistry` 方法，並傳遞要套用的原則名稱。

關於 `IHttpClientFactory` Polly 整合的詳細資訊，可以在 [Polly Wiki](https://github.com/App-vNext/Polly/wiki/Polly-and-HttpClientFactory) 上找到。

## <a name="httpclient-and-lifetime-management"></a>HttpClient 和存留期管理

每次在 `IHttpClientFactory` 上呼叫 `CreateClient` 時，都會傳回新的 `HttpClient` 執行個體。 每個具名用戶端都有一個 <xref:System.Net.Http.HttpMessageHandler>。 處理站會管理 `HttpMessageHandler` 執行個體的存留期。

`IHttpClientFactory` 會將處理站所建立的 `HttpMessageHandler` 執行個體放入集區以減少資源耗用量。 建立新的 `HttpClient` 執行個體時，如果其存留期間尚未過期，`HttpMessageHandler` 執行個體可從集區重複使用。

將處理常式放入集區非常實用，因為處理常式通常會管理自己專屬的底層 HTTP 連線。 建立比所需數目更多的處理常式，可能會導致連線延遲。 有些處理常式也會保持連線無限期地開啟，這可能導致處理常式無法對 DNS 變更回應。

預設處理常式存留時間為兩分鐘。 可以針對每個具名用戶端覆寫預設值。 若要覆寫它，請在建立用戶端時所傳回的 `IHttpClientBuilder` 上呼叫 <xref:Microsoft.Extensions.DependencyInjection.HttpClientBuilderExtensions.SetHandlerLifetime*>：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet11)]

不需要處置用戶端。 處置會取消傳出的要求，並保證指定的 `HttpClient` 執行個體在呼叫 <xref:System.IDisposable.Dispose*> 之後無法使用。 `IHttpClientFactory` 會追蹤並處置 `HttpClient` 執行個體使用的資源。 `HttpClient` 執行個體通常可視為 .NET 物件，不需要處置。

在開始使用 `IHttpClientFactory` 之前，讓單一 `HttpClient` 執行個體維持一段較長的時間，是很常使用的模式。 在移轉到 `IHttpClientFactory` 之後，就不再需要此模式。

## <a name="logging"></a>記錄

透過 `IHttpClientFactory` 建立的用戶端會記錄所有要求的記錄訊息。 在記錄設定中啟用適當的資訊層級，以查看預設記錄檔訊息。 額外的記錄功能，例如要求標頭的記錄，只會包含在追蹤層級。

用於每個用戶端的記錄檔分類包含用戶端的名稱。 例如，名為 *MyNamedClient* 的用戶端會記錄分類為 `System.Net.Http.HttpClient.MyNamedClient.LogicalHandler` 的訊息。 後面加上 *LogicalHandler* 的訊息發生在要求處理常式管線之外。 在要求中，訊息會在管線中任何其他處理常式處理它之前就記錄。 在回應中，訊息會在任何其他管線處理常式收到回應之後記錄。

記錄也會發生在要求處理常式管線之內。 在 *MyNamedClient* 範例中，那些訊息是針對記錄檔分類 `System.Net.Http.HttpClient.MyNamedClient.ClientHandler` 而記錄。 對於要求，這是發生在所有其他處理常式都已執行之後，並且緊接在網路上傳送要求之前。 在回應中，此記錄會包含回應傳回通過處理常式管線之前的狀態。

在管線內外啟用記錄，可讓您檢查其他管線處理常式所做的變更。 例如，這可能包括要求標頭的變更，或是回應狀態碼的變更。

在記錄分類中包含用戶端的名稱，可讓您在需要時進行特定具名用戶端的記錄檔篩選。

## <a name="configure-the-httpmessagehandler"></a>設定 HttpMessageHandler

可能需要控制用戶端使用之內部 `HttpMessageHandler` 的組態。

新增具名或具型別用戶端時，會傳回 `IHttpClientBuilder`。 <xref:Microsoft.Extensions.DependencyInjection.HttpClientBuilderExtensions.ConfigurePrimaryHttpMessageHandler*> 擴充方法可以用來定義委派。 委派是用來建立及設定該用戶端所使用的主要 `HttpMessageHandler`：

[!code-csharp[Main](http-requests/samples/2.x/HttpClientFactorySample/Startup.cs?name=snippet12)]

## <a name="additional-resources"></a>其他資源

* [使用 HttpClientFactory 實作復原 HTTP 要求](/dotnet/standard/microservices-architecture/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)
* [使用 HttpClientFactory 和 Polly 原則以指數輪詢實作 HTTP 呼叫重試](/dotnet/standard/microservices-architecture/implement-resilient-applications/implement-http-call-retries-exponential-backoff-polly)
* [實作斷路器模式](/dotnet/standard/microservices-architecture/implement-resilient-applications/implement-circuit-breaker-pattern)