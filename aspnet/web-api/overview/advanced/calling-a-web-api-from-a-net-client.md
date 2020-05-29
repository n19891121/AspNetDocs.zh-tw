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
# <a name="call-a-web-api-from-a-net-client-c"></a><span data-ttu-id="e3f68-103">從 .NET 用戶端呼叫 Web API （c #）</span><span class="sxs-lookup"><span data-stu-id="e3f68-103">Call a Web API From a .NET Client (C#)</span></span>

<span data-ttu-id="e3f68-104">由[Mike Wasson](https://github.com/MikeWasson)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e3f68-104">by [Mike Wasson](https://github.com/MikeWasson) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e3f68-105">[下載已完成的專案](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample)。</span><span class="sxs-lookup"><span data-stu-id="e3f68-105">[Download Completed Project](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample).</span></span> <span data-ttu-id="e3f68-106">[下載指示](/aspnet/core/tutorials/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="e3f68-106">[Download instructions](/aspnet/core/tutorials/#how-to-download-a-sample).</span></span> 

<span data-ttu-id="e3f68-107">本教學課程說明如何使用 HttpClient，從 .NET 應用程式呼叫 Web API [。](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="e3f68-107">This tutorial shows how to call a web API from a .NET application, using [System.Net.Http.HttpClient.](https://msdn.microsoft.com/library/system.net.http.httpclient(v=vs.110).aspx)</span></span>

<span data-ttu-id="e3f68-108">在本教學課程中，會寫入使用下列 Web API 的用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="e3f68-108">In this tutorial, a client app is written that consumes the following web API:</span></span>

| <span data-ttu-id="e3f68-109">動作</span><span class="sxs-lookup"><span data-stu-id="e3f68-109">Action</span></span> | <span data-ttu-id="e3f68-110">HTTP method</span><span class="sxs-lookup"><span data-stu-id="e3f68-110">HTTP method</span></span> | <span data-ttu-id="e3f68-111">相對 URI</span><span class="sxs-lookup"><span data-stu-id="e3f68-111">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3f68-112">依照識別碼取得產品</span><span class="sxs-lookup"><span data-stu-id="e3f68-112">Get a product by ID</span></span> | <span data-ttu-id="e3f68-113">GET</span><span class="sxs-lookup"><span data-stu-id="e3f68-113">GET</span></span> | <span data-ttu-id="e3f68-114">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="e3f68-114">/api/products/*id*</span></span> |
| <span data-ttu-id="e3f68-115">建立新的產品</span><span class="sxs-lookup"><span data-stu-id="e3f68-115">Create a new product</span></span> | <span data-ttu-id="e3f68-116">POST</span><span class="sxs-lookup"><span data-stu-id="e3f68-116">POST</span></span> | <span data-ttu-id="e3f68-117">/api/products</span><span class="sxs-lookup"><span data-stu-id="e3f68-117">/api/products</span></span> |
| <span data-ttu-id="e3f68-118">更新產品</span><span class="sxs-lookup"><span data-stu-id="e3f68-118">Update a product</span></span> | <span data-ttu-id="e3f68-119">PUT</span><span class="sxs-lookup"><span data-stu-id="e3f68-119">PUT</span></span> | <span data-ttu-id="e3f68-120">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="e3f68-120">/api/products/*id*</span></span> |
| <span data-ttu-id="e3f68-121">刪除產品</span><span class="sxs-lookup"><span data-stu-id="e3f68-121">Delete a product</span></span> | <span data-ttu-id="e3f68-122">刪除</span><span class="sxs-lookup"><span data-stu-id="e3f68-122">DELETE</span></span> | <span data-ttu-id="e3f68-123">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="e3f68-123">/api/products/*id*</span></span> |

<span data-ttu-id="e3f68-124">若要瞭解如何使用 ASP.NET Web API 來執行此 API，請參閱[建立支援 CRUD 作業的 WEB api](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
)。</span><span class="sxs-lookup"><span data-stu-id="e3f68-124">To learn how to implement this API with ASP.NET Web API, see [Creating a Web API that Supports CRUD Operations](xref:web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
).</span></span>

<span data-ttu-id="e3f68-125">為了簡單起見，本教學課程中的用戶端應用程式是 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3f68-125">For simplicity, the client application in this tutorial is a Windows console application.</span></span> <span data-ttu-id="e3f68-126">Windows Phone 和 Windows Store 應用程式也支援**HttpClient** 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-126">**HttpClient** is also supported for Windows Phone and Windows Store apps.</span></span> <span data-ttu-id="e3f68-127">如需詳細資訊，請參閱[使用便攜程式庫撰寫適用于多個平臺的 WEB API 用戶端程式代碼](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span><span class="sxs-lookup"><span data-stu-id="e3f68-127">For more information, see [Writing Web API Client Code for Multiple Platforms Using Portable Libraries](https://blogs.msdn.com/b/webdev/archive/2013/07/19/writing-web-api-client-code-for-multiple-platforms-using-portable-libraries.aspx)</span></span>

<span data-ttu-id="e3f68-128">**注意：** 如果您將基底 Url 和相對 Uri 傳遞為硬式編碼值，請注意使用 API 的規則 `HttpClient` 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-128">**NOTE:** If you pass base URLs and relative URIs as hard-coded values, be mindful of the rules for utilizing the `HttpClient` API.</span></span> <span data-ttu-id="e3f68-129">`HttpClient.BaseAddress`屬性應設定為尾端斜線（）的位址 `/` 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-129">The `HttpClient.BaseAddress` property should be set to an address with a trailing forward slash (`/`).</span></span> <span data-ttu-id="e3f68-130">例如，將硬式編碼的資源 Uri 傳遞給 `HttpClient.GetAsync` 方法時，請勿包含前置正斜線。</span><span class="sxs-lookup"><span data-stu-id="e3f68-130">For example, when passing hard-coded resource URIs to the `HttpClient.GetAsync` method, don't include a leading forward slash.</span></span> <span data-ttu-id="e3f68-131">若要 `Product` 依識別碼取得：</span><span class="sxs-lookup"><span data-stu-id="e3f68-131">To get a `Product` by ID:</span></span>

1. <span data-ttu-id="e3f68-132">設定`client.BaseAddress = new Uri("https://localhost:5001/");`</span><span class="sxs-lookup"><span data-stu-id="e3f68-132">Set `client.BaseAddress = new Uri("https://localhost:5001/");`</span></span>
1. <span data-ttu-id="e3f68-133">要求 `Product` 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-133">Request a `Product`.</span></span> <span data-ttu-id="e3f68-134">例如 `client.GetAsync<Product>("api/products/4");`。</span><span class="sxs-lookup"><span data-stu-id="e3f68-134">For example, `client.GetAsync<Product>("api/products/4");`.</span></span>

<a id="CreateConsoleApp"></a>
## <a name="create-the-console-application"></a><span data-ttu-id="e3f68-135">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e3f68-135">Create the Console Application</span></span>

<span data-ttu-id="e3f68-136">在 Visual Studio 中，建立名為**HttpClientSample**的新 Windows 主控台應用程式，並貼上下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="e3f68-136">In Visual Studio, create a new Windows console app named **HttpClientSample** and paste in the following code:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_all)]

<span data-ttu-id="e3f68-137">上述程式碼是完整的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3f68-137">The preceding code is the complete client app.</span></span>

<span data-ttu-id="e3f68-138">`RunAsync`會執行並封鎖，直到完成為止。</span><span class="sxs-lookup"><span data-stu-id="e3f68-138">`RunAsync` runs and blocks until it completes.</span></span> <span data-ttu-id="e3f68-139">大部分的**HttpClient**方法都是非同步，因為它們會執行網路 i/o。</span><span class="sxs-lookup"><span data-stu-id="e3f68-139">Most **HttpClient** methods are async, because they perform network I/O.</span></span> <span data-ttu-id="e3f68-140">所有非同步工作都是在內部完成 `RunAsync` 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-140">All of the async tasks are done inside `RunAsync`.</span></span> <span data-ttu-id="e3f68-141">應用程式通常不會封鎖主執行緒，但此應用程式不允許任何互動。</span><span class="sxs-lookup"><span data-stu-id="e3f68-141">Normally an app doesn't block the main thread, but this app doesn't allow any interaction.</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_run)]

<a id="InstallClientLib"></a>
## <a name="install-the-web-api-client-libraries"></a><span data-ttu-id="e3f68-142">安裝 Web API 用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e3f68-142">Install the Web API Client Libraries</span></span>

<span data-ttu-id="e3f68-143">使用 NuGet 套件管理員來安裝 Web API 用戶端程式庫套件。</span><span class="sxs-lookup"><span data-stu-id="e3f68-143">Use NuGet Package Manager to install the Web API Client Libraries package.</span></span>

<span data-ttu-id="e3f68-144">從 [工具]\*\*\*\* 功能表中，選取 [NuGet 封裝管理員]\*\*\*\* > [封裝管理員主控台]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="e3f68-144">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span> <span data-ttu-id="e3f68-145">在 [套件管理員主控台] （PMC）中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="e3f68-145">In the Package Manager Console (PMC), type the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.Client`

<span data-ttu-id="e3f68-146">上述命令會將下列 NuGet 套件新增至專案：</span><span class="sxs-lookup"><span data-stu-id="e3f68-146">The preceding command adds the following NuGet packages to the project:</span></span>

* <span data-ttu-id="e3f68-147">WebApi。用戶端</span><span class="sxs-lookup"><span data-stu-id="e3f68-147">Microsoft.AspNet.WebApi.Client</span></span>
* <span data-ttu-id="e3f68-148">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="e3f68-148">Newtonsoft.Json</span></span>

<span data-ttu-id="e3f68-149">Netwonsoft （也稱為 Json.NET）是適用于 .NET 的熱門高效能 JSON 架構。</span><span class="sxs-lookup"><span data-stu-id="e3f68-149">Netwonsoft.Json (also known as Json.NET) is a popular high-performance JSON framework for .NET.</span></span>

<a id="AddModelClass"></a>
## <a name="add-a-model-class"></a><span data-ttu-id="e3f68-150">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="e3f68-150">Add a Model Class</span></span>

<span data-ttu-id="e3f68-151">檢查 `Product` 類別：</span><span class="sxs-lookup"><span data-stu-id="e3f68-151">Examine the `Product` class:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_prod)]

<span data-ttu-id="e3f68-152">這個類別符合 Web API 所使用的資料模型。</span><span class="sxs-lookup"><span data-stu-id="e3f68-152">This class matches the data model used by the web API.</span></span> <span data-ttu-id="e3f68-153">應用程式可以使用**HttpClient** `Product` 從 HTTP 回應讀取實例。</span><span class="sxs-lookup"><span data-stu-id="e3f68-153">An app can use **HttpClient** to read a `Product` instance from an HTTP response.</span></span> <span data-ttu-id="e3f68-154">應用程式不需要撰寫任何還原序列化程式碼。</span><span class="sxs-lookup"><span data-stu-id="e3f68-154">The app doesn't have to write any deserialization code.</span></span>

<a id="InitClient"></a>
## <a name="create-and-initialize-httpclient"></a><span data-ttu-id="e3f68-155">建立和初始化 HttpClient</span><span class="sxs-lookup"><span data-stu-id="e3f68-155">Create and Initialize HttpClient</span></span>

<span data-ttu-id="e3f68-156">檢查靜態**HttpClient**屬性：</span><span class="sxs-lookup"><span data-stu-id="e3f68-156">Examine the static **HttpClient** property:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_HttpClient)]

<span data-ttu-id="e3f68-157">**HttpClient**的目的是要具現化一次，並在應用程式的整個生命週期中重複使用。</span><span class="sxs-lookup"><span data-stu-id="e3f68-157">**HttpClient** is intended to be instantiated once and reused throughout the life of an application.</span></span> <span data-ttu-id="e3f68-158">下列情況可能會導致**SocketException**錯誤：</span><span class="sxs-lookup"><span data-stu-id="e3f68-158">The following conditions can result in **SocketException** errors:</span></span>

* <span data-ttu-id="e3f68-159">針對每個要求建立新的**HttpClient**實例。</span><span class="sxs-lookup"><span data-stu-id="e3f68-159">Creating a new **HttpClient** instance per request.</span></span>
* <span data-ttu-id="e3f68-160">負載過重的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e3f68-160">Server under heavy load.</span></span>

<span data-ttu-id="e3f68-161">針對每個要求建立新的**HttpClient**實例可能會耗盡可用的通訊端。</span><span class="sxs-lookup"><span data-stu-id="e3f68-161">Creating a new **HttpClient** instance per request can exhaust the available sockets.</span></span>

<span data-ttu-id="e3f68-162">下列程式碼會初始化**HttpClient**實例：</span><span class="sxs-lookup"><span data-stu-id="e3f68-162">The following code initializes the **HttpClient** instance:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5)]

<span data-ttu-id="e3f68-163">上述程式碼：</span><span class="sxs-lookup"><span data-stu-id="e3f68-163">The preceding code:</span></span>

* <span data-ttu-id="e3f68-164">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="e3f68-164">Sets the base URI for HTTP requests.</span></span> <span data-ttu-id="e3f68-165">將埠號碼變更為伺服器應用程式中所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="e3f68-165">Change the port number to the port used in the server app.</span></span> <span data-ttu-id="e3f68-166">除非使用伺服器應用程式的埠，否則應用程式將無法使用。</span><span class="sxs-lookup"><span data-stu-id="e3f68-166">The app won't work unless port for the server app is used.</span></span>
* <span data-ttu-id="e3f68-167">將 Accept 標頭設定為 "application/json"。</span><span class="sxs-lookup"><span data-stu-id="e3f68-167">Sets the Accept header to "application/json".</span></span> <span data-ttu-id="e3f68-168">設定此標頭會告訴伺服器以 JSON 格式傳送資料。</span><span class="sxs-lookup"><span data-stu-id="e3f68-168">Setting this header tells the server to send data in JSON format.</span></span>

<a id="GettingResource"></a>
## <a name="send-a-get-request-to-retrieve-a-resource"></a><span data-ttu-id="e3f68-169">傳送 GET 要求以取得資源</span><span class="sxs-lookup"><span data-stu-id="e3f68-169">Send a GET request to retrieve a resource</span></span>

<span data-ttu-id="e3f68-170">下列程式碼會傳送產品的 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="e3f68-170">The following code sends a GET request for a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_GetProductAsync)]

<span data-ttu-id="e3f68-171">**GetAsync**方法會傳送 HTTP GET 要求。</span><span class="sxs-lookup"><span data-stu-id="e3f68-171">The **GetAsync** method sends the HTTP GET request.</span></span> <span data-ttu-id="e3f68-172">當方法完成時，它會傳回包含 HTTP 回應的**HttpResponseMessage** 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-172">When the method completes, it returns an **HttpResponseMessage** that contains the HTTP response.</span></span> <span data-ttu-id="e3f68-173">如果回應中的狀態碼是成功的程式碼，回應主體會包含產品的 JSON 標記法。</span><span class="sxs-lookup"><span data-stu-id="e3f68-173">If the status code in the response is a success code, the response body contains the JSON representation of a product.</span></span> <span data-ttu-id="e3f68-174">呼叫**ReadAsAsync**將 JSON 承載還原序列化為 `Product` 實例。</span><span class="sxs-lookup"><span data-stu-id="e3f68-174">Call **ReadAsAsync** to deserialize the JSON payload to a `Product` instance.</span></span> <span data-ttu-id="e3f68-175">**ReadAsAsync**方法是非同步，因為回應主體可以任意大。</span><span class="sxs-lookup"><span data-stu-id="e3f68-175">The **ReadAsAsync** method is asynchronous because the response body can be arbitrarily large.</span></span>

<span data-ttu-id="e3f68-176">當 HTTP 回應包含錯誤代碼時， **HttpClient**不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e3f68-176">**HttpClient** does not throw an exception when the HTTP response contains an error code.</span></span> <span data-ttu-id="e3f68-177">相反地，如果狀態為錯誤碼，則 **.issuccessstatuscode**屬性為**false** 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-177">Instead, the **IsSuccessStatusCode** property is **false** if the status is an error code.</span></span> <span data-ttu-id="e3f68-178">如果您想要將 HTTP 錯誤碼視為例外狀況，請在回應物件上呼叫[HttpResponseMessage. EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-178">If you prefer to treat HTTP error codes as exceptions, call [HttpResponseMessage.EnsureSuccessStatusCode](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.ensuresuccessstatuscode(v=vs.110).aspx) on the response object.</span></span> <span data-ttu-id="e3f68-179">`EnsureSuccessStatusCode`如果狀態碼落在 200 299 的範圍外，則擲回例外狀況 &ndash; 。</span><span class="sxs-lookup"><span data-stu-id="e3f68-179">`EnsureSuccessStatusCode` throws an exception if the status code falls outside the range 200&ndash;299.</span></span> <span data-ttu-id="e3f68-180">請注意， **HttpClient**可能會因其他原因而擲回例外狀況 &mdash; ，例如，如果要求超時。</span><span class="sxs-lookup"><span data-stu-id="e3f68-180">Note that **HttpClient** can throw exceptions for other reasons &mdash; for example, if the request times out.</span></span>

<a id="MediaTypeFormatters"></a>
### <a name="media-type-formatters-to-deserialize"></a><span data-ttu-id="e3f68-181">要還原序列化的媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="e3f68-181">Media-Type Formatters to Deserialize</span></span>

<span data-ttu-id="e3f68-182">呼叫不含任何參數的**ReadAsAsync**時，會使用一組預設的*媒體*格式器來讀取回應主體。</span><span class="sxs-lookup"><span data-stu-id="e3f68-182">When **ReadAsAsync** is called with no parameters, it uses a default set of *media formatters* to read the response body.</span></span> <span data-ttu-id="e3f68-183">預設的格式器支援 JSON、XML 和表單 url 編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="e3f68-183">The default formatters support JSON, XML, and Form-url-encoded data.</span></span>

<span data-ttu-id="e3f68-184">除了使用預設的格式器之外，您還可以提供格式器清單給**ReadAsAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="e3f68-184">Instead of using the default formatters, you can provide a list of formatters to the **ReadAsAsync** method.</span></span>  <span data-ttu-id="e3f68-185">如果您有自訂的媒體類型格式器，使用格式器清單會很有用：</span><span class="sxs-lookup"><span data-stu-id="e3f68-185">Using a list of formatters is useful if you have a custom media-type formatter:</span></span>

```csharp
var formatters = new List<MediaTypeFormatter>() {
    new MyCustomFormatter(),
    new JsonMediaTypeFormatter(),
    new XmlMediaTypeFormatter()
};
resp.Content.ReadAsAsync<IEnumerable<Product>>(formatters);
```

<span data-ttu-id="e3f68-186">如需詳細資訊，請參閱[ASP.NET Web API 2 中的媒體](../formats-and-model-binding/media-formatters.md)格式器</span><span class="sxs-lookup"><span data-stu-id="e3f68-186">For more information, see [Media Formatters in ASP.NET Web API 2](../formats-and-model-binding/media-formatters.md)</span></span>

## <a name="sending-a-post-request-to-create-a-resource"></a><span data-ttu-id="e3f68-187">傳送 POST 要求以建立資源</span><span class="sxs-lookup"><span data-stu-id="e3f68-187">Sending a POST Request to Create a Resource</span></span>

<span data-ttu-id="e3f68-188">下列程式碼會傳送 POST 要求，其中包含 `Product` JSON 格式的實例：</span><span class="sxs-lookup"><span data-stu-id="e3f68-188">The following code sends a POST request that contains a `Product` instance in JSON format:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_CreateProductAsync)]

<span data-ttu-id="e3f68-189">**PostAsJsonAsync**方法：</span><span class="sxs-lookup"><span data-stu-id="e3f68-189">The **PostAsJsonAsync** method:</span></span>

* <span data-ttu-id="e3f68-190">將物件序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="e3f68-190">Serializes an object to JSON.</span></span>
* <span data-ttu-id="e3f68-191">在 POST 要求中傳送 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="e3f68-191">Sends the JSON payload in a POST request.</span></span>

<span data-ttu-id="e3f68-192">如果要求成功：</span><span class="sxs-lookup"><span data-stu-id="e3f68-192">If the request succeeds:</span></span>

* <span data-ttu-id="e3f68-193">它應該會傳回201（已建立）的回應。</span><span class="sxs-lookup"><span data-stu-id="e3f68-193">It should return a 201 (Created) response.</span></span>
* <span data-ttu-id="e3f68-194">回應應包含位置標頭中所建立資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="e3f68-194">The response should include the URL of the created resources in the Location header.</span></span>

<a id="PuttingResource"></a>
## <a name="sending-a-put-request-to-update-a-resource"></a><span data-ttu-id="e3f68-195">傳送 PUT 要求以更新資源</span><span class="sxs-lookup"><span data-stu-id="e3f68-195">Sending a PUT Request to Update a Resource</span></span>

<span data-ttu-id="e3f68-196">下列程式碼會傳送 PUT 要求來更新產品：</span><span class="sxs-lookup"><span data-stu-id="e3f68-196">The following code sends a PUT request to update a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_UpdateProductAsync)]

<span data-ttu-id="e3f68-197">**PutAsJsonAsync**方法的運作方式類似**PostAsJsonAsync**，不同之處在于它會傳送 PUT 要求，而不是 POST。</span><span class="sxs-lookup"><span data-stu-id="e3f68-197">The **PutAsJsonAsync** method works like **PostAsJsonAsync**, except that it sends a PUT request instead of POST.</span></span>

<a id="DeletingResource"></a>
## <a name="sending-a-delete-request-to-delete-a-resource"></a><span data-ttu-id="e3f68-198">傳送刪除要求以刪除資源</span><span class="sxs-lookup"><span data-stu-id="e3f68-198">Sending a DELETE Request to Delete a Resource</span></span>

<span data-ttu-id="e3f68-199">下列程式碼會傳送刪除要求以刪除產品：</span><span class="sxs-lookup"><span data-stu-id="e3f68-199">The following code sends a DELETE request to delete a product:</span></span>

[!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet_DeleteProductAsync)]

<span data-ttu-id="e3f68-200">就像 GET 一樣，刪除要求沒有要求主體。</span><span class="sxs-lookup"><span data-stu-id="e3f68-200">Like GET, a DELETE request does not have a request body.</span></span> <span data-ttu-id="e3f68-201">您不需要使用 DELETE 來指定 JSON 或 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="e3f68-201">You don't need to specify JSON or XML format with DELETE.</span></span>

## <a name="test-the-sample"></a><span data-ttu-id="e3f68-202">測試範例</span><span class="sxs-lookup"><span data-stu-id="e3f68-202">Test the sample</span></span>

<span data-ttu-id="e3f68-203">若要測試用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="e3f68-203">To test the client app:</span></span>

1. <span data-ttu-id="e3f68-204">[下載](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server)並執行伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3f68-204">[Download](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-api/overview/advanced/calling-a-web-api-from-a-net-client/sample/server) and run the server app.</span></span> <span data-ttu-id="e3f68-205">[下載指示](/aspnet/core/#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="e3f68-205">[Download instructions](/aspnet/core/#how-to-download-a-sample).</span></span> <span data-ttu-id="e3f68-206">確認伺服器應用程式正在運作。</span><span class="sxs-lookup"><span data-stu-id="e3f68-206">Verify the server app is working.</span></span> <span data-ttu-id="e3f68-207">例如， `http://localhost:64195/api/products` 應該會傳回產品清單。</span><span class="sxs-lookup"><span data-stu-id="e3f68-207">For example, `http://localhost:64195/api/products` should return a list of products.</span></span>
2. <span data-ttu-id="e3f68-208">設定 HTTP 要求的基底 URI。</span><span class="sxs-lookup"><span data-stu-id="e3f68-208">Set the base URI for HTTP requests.</span></span> <span data-ttu-id="e3f68-209">將埠號碼變更為伺服器應用程式中所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="e3f68-209">Change the port number to the port used in the server app.</span></span>
    [!code-csharp[Main](calling-a-web-api-from-a-net-client/sample/client/Program.cs?name=snippet5&highlight=2)]

3. <span data-ttu-id="e3f68-210">執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3f68-210">Run the client app.</span></span> <span data-ttu-id="e3f68-211">會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e3f68-211">The following output is produced:</span></span>

   ```console
   Created at http://localhost:64195/api/products/4
   Name: Gizmo     Price: 100.0    Category: Widgets
   Updating price...
   Name: Gizmo     Price: 80.0     Category: Widgets
   Deleted (HTTP Status = 204)
   ```
