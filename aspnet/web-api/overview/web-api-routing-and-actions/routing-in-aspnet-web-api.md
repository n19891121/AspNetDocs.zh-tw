---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345194"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="3fb34-102">ASP.NET Web API 中的路由</span><span class="sxs-lookup"><span data-stu-id="3fb34-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="3fb34-103">由 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3fb34-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3fb34-104">本文說明 ASP.NET Web API 如何將 HTTP 要求路由至控制器。</span><span class="sxs-lookup"><span data-stu-id="3fb34-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="3fb34-105">如果您熟悉 ASP.NET MVC，Web API 路由與 MVC 路由非常類似。</span><span class="sxs-lookup"><span data-stu-id="3fb34-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="3fb34-106">主要的差異在於，Web API 會使用 HTTP 動詞命令（而非 URI 路徑）來選取動作。</span><span class="sxs-lookup"><span data-stu-id="3fb34-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="3fb34-107">您也可以在 Web API 中使用 MVC 樣式的路由。</span><span class="sxs-lookup"><span data-stu-id="3fb34-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="3fb34-108">本文並不假設任何 ASP.NET MVC 的知識。</span><span class="sxs-lookup"><span data-stu-id="3fb34-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="3fb34-109">路由表</span><span class="sxs-lookup"><span data-stu-id="3fb34-109">Routing Tables</span></span>

<span data-ttu-id="3fb34-110">在 ASP.NET Web API 中， *控制器* 是處理 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="3fb34-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="3fb34-111">控制器的公用方法稱為 *動作方法* 或單純的 *動作*。</span><span class="sxs-lookup"><span data-stu-id="3fb34-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="3fb34-112">當 Web API 架構收到要求時，它會將要求路由傳送至動作。</span><span class="sxs-lookup"><span data-stu-id="3fb34-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="3fb34-113">為了判斷要叫用的動作，架構會使用 *路由表*。</span><span class="sxs-lookup"><span data-stu-id="3fb34-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="3fb34-114">Web API 的 Visual Studio 專案範本會建立預設路由：</span><span class="sxs-lookup"><span data-stu-id="3fb34-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="3fb34-115">此路由定義于 *WebApiConfig.cs* 檔案中，該檔案位於 *應用程式 \_ 啟動* 目錄中：</span><span class="sxs-lookup"><span data-stu-id="3fb34-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="3fb34-116">如需類別的詳細資訊 `WebApiConfig` ，請參閱設定 [ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="3fb34-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="3fb34-117">如果您自我裝載 Web API，您必須直接在物件上設定路由表 `HttpSelfHostConfiguration` 。</span><span class="sxs-lookup"><span data-stu-id="3fb34-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="3fb34-118">如需詳細資訊，請參閱 [自我裝載 WEB API](../older-versions/self-host-a-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="3fb34-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="3fb34-119">路由表中的每個專案都包含 *路由範本*。</span><span class="sxs-lookup"><span data-stu-id="3fb34-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="3fb34-120">Web API 的預設路由範本是 &quot; API/{controller}/{id} &quot; 。</span><span class="sxs-lookup"><span data-stu-id="3fb34-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="3fb34-121">在此範本中， &quot; api &quot; 是常值路徑區段，而 {控制器} 和 {id} 是預留位置變數。</span><span class="sxs-lookup"><span data-stu-id="3fb34-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="3fb34-122">當 Web API 架構收到 HTTP 要求時，它會嘗試比對 URI 與路由表中的其中一個路由範本。</span><span class="sxs-lookup"><span data-stu-id="3fb34-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="3fb34-123">如果沒有符合的路由，用戶端會收到404錯誤。</span><span class="sxs-lookup"><span data-stu-id="3fb34-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="3fb34-124">例如，下列 Uri 符合預設路由：</span><span class="sxs-lookup"><span data-stu-id="3fb34-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="3fb34-125">/api/contacts</span><span class="sxs-lookup"><span data-stu-id="3fb34-125">/api/contacts</span></span>
- <span data-ttu-id="3fb34-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="3fb34-126">/api/contacts/1</span></span>
- <span data-ttu-id="3fb34-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="3fb34-127">/api/products/gizmo1</span></span>

<span data-ttu-id="3fb34-128">但是，下列 URI 不相符，因為它缺少 &quot; api &quot; 區段：</span><span class="sxs-lookup"><span data-stu-id="3fb34-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="3fb34-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="3fb34-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="3fb34-130">在路由中使用 "api" 的原因是為了避免與 ASP.NET MVC 路由發生衝突。</span><span class="sxs-lookup"><span data-stu-id="3fb34-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="3fb34-131">如此一來，您可以讓 &quot; /contacts &quot; 前往 MVC 控制器， &quot; /Api/contacts 移至 &quot; Web api 控制器。</span><span class="sxs-lookup"><span data-stu-id="3fb34-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="3fb34-132">當然，如果您不喜歡這種慣例，可以變更預設路由表。</span><span class="sxs-lookup"><span data-stu-id="3fb34-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="3fb34-133">一旦找到相符的路由之後，Web API 就會選取控制器和動作：</span><span class="sxs-lookup"><span data-stu-id="3fb34-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="3fb34-134">為了尋找控制器，Web API 會將 &quot; 控制器新增 &quot; 至 *{controller}* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="3fb34-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="3fb34-135">若要尋找動作，Web API 會查看 HTTP 動詞命令，然後尋找名稱開頭為該 HTTP 動詞命令名稱的動作。</span><span class="sxs-lookup"><span data-stu-id="3fb34-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="3fb34-136">例如，透過 GET 要求，Web API 會尋找首碼為 get 的動作 &quot; &quot; ，例如 &quot; GetContact &quot; 或 &quot; GetAllContacts &quot; 。</span><span class="sxs-lookup"><span data-stu-id="3fb34-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="3fb34-137">此慣例僅適用于 GET、POST、PUT、DELETE、HEAD、OPTIONS 和 PATCH 動詞。</span><span class="sxs-lookup"><span data-stu-id="3fb34-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="3fb34-138">您可以使用控制器上的屬性來啟用其他 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="3fb34-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="3fb34-139">我們稍後會看到一個範例。</span><span class="sxs-lookup"><span data-stu-id="3fb34-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="3fb34-140">路由範本中的其他預留位置變數（例如 *{id}）* 會對應至動作參數。</span><span class="sxs-lookup"><span data-stu-id="3fb34-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="3fb34-141">以下舉例說明。</span><span class="sxs-lookup"><span data-stu-id="3fb34-141">Let's look at an example.</span></span> <span data-ttu-id="3fb34-142">假設您定義了下列控制器：</span><span class="sxs-lookup"><span data-stu-id="3fb34-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="3fb34-143">以下是一些可能的 HTTP 要求，以及針對每個要求叫用的動作：</span><span class="sxs-lookup"><span data-stu-id="3fb34-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="3fb34-144">HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="3fb34-144">HTTP Verb</span></span> | <span data-ttu-id="3fb34-145">URI 路徑</span><span class="sxs-lookup"><span data-stu-id="3fb34-145">URI Path</span></span> | <span data-ttu-id="3fb34-146">動作</span><span class="sxs-lookup"><span data-stu-id="3fb34-146">Action</span></span> | <span data-ttu-id="3fb34-147">參數</span><span class="sxs-lookup"><span data-stu-id="3fb34-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3fb34-148">GET</span><span class="sxs-lookup"><span data-stu-id="3fb34-148">GET</span></span> | <span data-ttu-id="3fb34-149">api/產品</span><span class="sxs-lookup"><span data-stu-id="3fb34-149">api/products</span></span> | <span data-ttu-id="3fb34-150">Getallproductswithcategories</span><span class="sxs-lookup"><span data-stu-id="3fb34-150">GetAllProducts</span></span> | <span data-ttu-id="3fb34-151">\* (無) \*</span><span class="sxs-lookup"><span data-stu-id="3fb34-151">*(none)*</span></span> |
| <span data-ttu-id="3fb34-152">GET</span><span class="sxs-lookup"><span data-stu-id="3fb34-152">GET</span></span> | <span data-ttu-id="3fb34-153">api/products/4</span><span class="sxs-lookup"><span data-stu-id="3fb34-153">api/products/4</span></span> | <span data-ttu-id="3fb34-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="3fb34-154">GetProductById</span></span> | <span data-ttu-id="3fb34-155">4</span><span class="sxs-lookup"><span data-stu-id="3fb34-155">4</span></span> |
| <span data-ttu-id="3fb34-156">DELETE</span><span class="sxs-lookup"><span data-stu-id="3fb34-156">DELETE</span></span> | <span data-ttu-id="3fb34-157">api/products/4</span><span class="sxs-lookup"><span data-stu-id="3fb34-157">api/products/4</span></span> | <span data-ttu-id="3fb34-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="3fb34-158">DeleteProduct</span></span> | <span data-ttu-id="3fb34-159">4</span><span class="sxs-lookup"><span data-stu-id="3fb34-159">4</span></span> |
| <span data-ttu-id="3fb34-160">POST</span><span class="sxs-lookup"><span data-stu-id="3fb34-160">POST</span></span> | <span data-ttu-id="3fb34-161">api/產品</span><span class="sxs-lookup"><span data-stu-id="3fb34-161">api/products</span></span> | <span data-ttu-id="3fb34-162">\* (沒有相符) \*</span><span class="sxs-lookup"><span data-stu-id="3fb34-162">*(no match)*</span></span> |  |

<span data-ttu-id="3fb34-163">請注意，URI 的 *{id}* 區段（如果有的話）會對應到動作的 *id* 參數。</span><span class="sxs-lookup"><span data-stu-id="3fb34-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="3fb34-164">在此範例中，控制器會定義兩個 GET 方法，一個具有 *id* 參數，另一個沒有參數。</span><span class="sxs-lookup"><span data-stu-id="3fb34-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="3fb34-165">此外，請注意 POST 要求將會失敗，因為控制器不會定義 &quot; post ... &quot; 方法。</span><span class="sxs-lookup"><span data-stu-id="3fb34-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="3fb34-166">路由變化</span><span class="sxs-lookup"><span data-stu-id="3fb34-166">Routing Variations</span></span>

<span data-ttu-id="3fb34-167">上一節描述 ASP.NET Web API 的基本路由機制。</span><span class="sxs-lookup"><span data-stu-id="3fb34-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="3fb34-168">本節說明一些變化。</span><span class="sxs-lookup"><span data-stu-id="3fb34-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="3fb34-169">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="3fb34-169">HTTP verbs</span></span>

<span data-ttu-id="3fb34-170">您可以使用下列其中一個屬性來裝飾動作方法，以明確指定動作的 HTTP 動詞命令，而不是使用 HTTP 動詞命令的命名慣例：</span><span class="sxs-lookup"><span data-stu-id="3fb34-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="3fb34-171">在下列範例中， `FindProduct` 方法會對應至 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="3fb34-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="3fb34-172">若要允許某個動作的多個 HTTP 動詞命令，或允許 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP 動詞命令，請使用 `[AcceptVerbs]` 屬性，此屬性會接受 HTTP 指令動詞清單。</span><span class="sxs-lookup"><span data-stu-id="3fb34-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="3fb34-173">依動作名稱路由傳送</span><span class="sxs-lookup"><span data-stu-id="3fb34-173">Routing by Action Name</span></span>

<span data-ttu-id="3fb34-174">使用預設路由範本，Web API 會使用 HTTP 動詞命令來選取動作。</span><span class="sxs-lookup"><span data-stu-id="3fb34-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="3fb34-175">不過，您也可以建立路由，其中動作名稱包含在 URI 中：</span><span class="sxs-lookup"><span data-stu-id="3fb34-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="3fb34-176">在此路由範本中， *{action}* 參數會命名控制器上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="3fb34-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="3fb34-177">使用這種路由樣式，請使用屬性來指定允許的 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="3fb34-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="3fb34-178">例如，假設您的控制器有下列方法：</span><span class="sxs-lookup"><span data-stu-id="3fb34-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="3fb34-179">在此情況下，「api/products/details/1」的 GET 要求會對應至 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="3fb34-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="3fb34-180">這種路由樣式與 ASP.NET MVC 類似，而且可能適用于 RPC 樣式的 API。</span><span class="sxs-lookup"><span data-stu-id="3fb34-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="3fb34-181">您可以使用屬性來覆寫動作名稱 `[ActionName]` 。</span><span class="sxs-lookup"><span data-stu-id="3fb34-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="3fb34-182">在下列範例中，有兩個動作對應至 &quot; api/產品/縮圖/*識別碼*。其中一個支援 GET，另一個支援 POST：</span><span class="sxs-lookup"><span data-stu-id="3fb34-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="3fb34-183">非動作</span><span class="sxs-lookup"><span data-stu-id="3fb34-183">Non-Actions</span></span>

<span data-ttu-id="3fb34-184">若要防止方法被叫用為動作，請使用 `[NonAction]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3fb34-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="3fb34-185">這會向架構表示方法不是動作，即使它會符合路由規則也一樣。</span><span class="sxs-lookup"><span data-stu-id="3fb34-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="3fb34-186">深入閱讀</span><span class="sxs-lookup"><span data-stu-id="3fb34-186">Further Reading</span></span>

<span data-ttu-id="3fb34-187">本主題提供路由的高階觀點。</span><span class="sxs-lookup"><span data-stu-id="3fb34-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="3fb34-188">如需詳細資訊，請參閱 [路由和動作選取專案](routing-and-action-selection.md)，其中描述架構與路由的 URI 相符的方式、選取控制器，然後選取要叫用的動作。</span><span class="sxs-lookup"><span data-stu-id="3fb34-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
