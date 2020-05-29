---
uid: web-api/overview/advanced/calling-a-web-api-from-a-net-client
title: '從 .NET 用戶端呼叫 Web API （c #）-ASP.NET 4。x'
author: MikeWasson
description: 本教學課程說明如何從 .NET 4.x 應用程式呼叫 Web API。
ms.author: riande
ms.date: 11/24/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/advanced/calling-a-web-api-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 484d927eeb0ba49f5f00d476f4658ebc081d0a4a
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84172935"
---
# <a name="call-a-web-api-from-a-net-client-c"></a>從 .NET 用戶端呼叫 Web API （c #）

由[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)

[下載已完成的專案](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。 [下載指示](/aspnet/core/tutorials/#how-to-download-a-sample)。 

本教學課程說明如何使用 HttpClient，從 .NET 應用程式呼叫 Web API [。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)

在本教學課程中，會寫入使用下列 Web API 的用戶端應用程式：

| 動作 | HTTP method | 相對 URI |
| --- | --- | --- |
| 依照識別碼取得產品 | GET | /api/products/*識別碼* |
| 建立新的產品 | POST | /api/products |
| 更新產品 | PUT | /api/products/*識別碼* |
| 刪除產品 | 刪除 | /api/products/*識別碼* |

若要瞭解如何使用 ASP.NET Web API 來執行此 API，請參閱[建立支援 CRUD 作業的 WEB api](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。

為了簡單起見，本教學課程中的用戶端應用程式是 Windows 主控台應用程式。 Windows Phone 和 Windows Store 應用程式也支援**HttpClient** 。 如需詳細資訊，請參閱[使用便攜程式庫撰寫適用于多個平臺的 WEB API 用戶端程式代碼](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)

**注意：** 如果您將基底 Url 和相對 Uri 傳遞為硬式編碼值，請注意使用 API 的規則 `HttpClient` 。 `HttpClient.BaseAddress`屬性應設定為尾端斜線（）的位址 `/` 。 例如，將硬式編碼的資源 Uri 傳遞給 `HttpClient.GetAsync` 方法時，請勿包含前置正斜線。 若要 `Product` 依識別碼取得：

1. 設定`client.BaseAddress = new Uri("https://localhost:5001/");`
1. 要求 `Product` 。 例如 `client.GetAsync<Product>("api/products/4");`。

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a>建立主控台應用程式

在 Visual Studio 中，建立名為**HttpClientSample**的新 Windows 主控台應用程式，並貼上下列程式碼：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

上述程式碼是完整的用戶端應用程式。

`RunAsync`會執行並封鎖，直到完成為止。 大部分的**HttpClient**方法都是非同步，因為它們會執行網路 i/o。 所有非同步工作都是在內部完成 `RunAsync` 。 應用程式通常不會封鎖主執行緒，但此應用程式不允許任何互動。

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a>安裝 Web API 用戶端程式庫

使用 NuGet 套件管理員來安裝 Web API 用戶端程式庫套件。

從 [工具]**** 功能表中，選取 [NuGet 封裝管理員]**** > [封裝管理員主控台]****。 在 [套件管理員主控台] （PMC）中，輸入下列命令：

`Install-Package Microsoft.AspNet.WebApi.Client`

上述命令會將下列 NuGet 套件新增至專案：

* WebApi。用戶端
* Newtonsoft.Json

Netwonsoft （也稱為 Json.NET）是適用于 .NET 的熱門高效能 JSON 架構。

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a>新增模型類別

檢查 `Product` 類別：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

這個類別符合 Web API 所使用的資料模型。 應用程式可以使用**HttpClient** `Product` 從 HTTP 回應讀取實例。 應用程式不需要撰寫任何還原序列化程式碼。

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a>建立和初始化 HttpClient

檢查靜態**HttpClient**屬性：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

**HttpClient**的目的是要具現化一次，並在應用程式的整個生命週期中重複使用。 下列情況可能會導致**SocketException**錯誤：

* 針對每個要求建立新的**HttpClient**實例。
* 負載過重的伺服器。

針對每個要求建立新的**HttpClient**實例可能會耗盡可用的通訊端。

下列程式碼會初始化**HttpClient**實例：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

上述程式碼：

* 設定 HTTP 要求的基底 URI。 將埠號碼變更為伺服器應用程式中所使用的埠。 除非使用伺服器應用程式的埠，否則應用程式將無法使用。
* 將 Accept 標頭設定為 "application/json"。 設定此標頭會告訴伺服器以 JSON 格式傳送資料。

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a>傳送 GET 要求以取得資源

下列程式碼會傳送產品的 GET 要求：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

**GetAsync**方法會傳送 HTTP GET 要求。 當方法完成時，它會傳回包含 HTTP 回應的**HttpResponseMessage** 。 如果回應中的狀態碼是成功的程式碼，回應主體會包含產品的 JSON 標記法。 呼叫**ReadAsAsync**將 JSON 承載還原序列化為 `Product` 實例。 **ReadAsAsync**方法是非同步，因為回應主體可以任意大。

當 HTTP 回應包含錯誤代碼時， **HttpClient**不會擲回例外狀況。 相反地，如果狀態為錯誤碼，則 **.issuccessstatuscode**屬性為**false** 。 如果您想要將 HTTP 錯誤碼視為例外狀況，請在回應物件上呼叫[HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 。 `EnsureSuccessStatusCode`如果狀態碼落在 200 299 的範圍外，則擲回例外狀況 &ndash; 。 請注意， **HttpClient**可能會因其他原因而擲回例外狀況 &mdash; ，例如，如果要求超時。

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a>要還原序列化的媒體類型格式器

呼叫不含任何參數的**ReadAsAsync**時，會使用一組預設的*媒體*格式器來讀取回應主體。 預設的格式器支援 JSON、XML 和表單 url 編碼的資料。

除了使用預設的格式器之外，您還可以提供格式器清單給**ReadAsAsync**方法。  如果您有自訂的媒體類型格式器，使用格式器清單會很有用：

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

如需詳細資訊，請參閱[ASP.NET Web API 2 中的媒體](../formats-and-model-binding/media-formatters.md)格式器

## <a name="sending-a-post-request-to-create-a-resource"></a>傳送 POST 要求以建立資源

下列程式碼會傳送 POST 要求，其中包含 `Product` JSON 格式的實例：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

**PostAsJsonAsync**方法：

* 將物件序列化為 JSON。
* 在 POST 要求中傳送 JSON 承載。

如果要求成功：

* 它應該會傳回201（已建立）的回應。
* 回應應包含位置標頭中所建立資源的 URL。

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a>傳送 PUT 要求以更新資源

下列程式碼會傳送 PUT 要求來更新產品：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

**PutAsJsonAsync**方法的運作方式類似**PostAsJsonAsync**，不同之處在于它會傳送 PUT 要求，而不是 POST。

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a>傳送刪除要求以刪除資源

下列程式碼會傳送刪除要求以刪除產品：

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

就像 GET 一樣，刪除要求沒有要求主體。 您不需要使用 DELETE 來指定 JSON 或 XML 格式。

## <a name="test-the-sample"></a>測試範例

若要測試用戶端應用程式：

1. [下載](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)並執行伺服器應用程式。 [下載指示](/aspnet/core/#how-to-download-a-sample)。 確認伺服器應用程式正在運作。 例如， `http://localhost:64195/api/products` 應該會傳回產品清單。
2. 設定 HTTP 要求的基底 URI。 將埠號碼變更為伺服器應用程式中所使用的埠。
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. 執行用戶端應用程式。 會產生下列輸出：

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
