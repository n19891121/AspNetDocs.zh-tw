---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |微軟文件
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676129"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="cd58a-102">ASP.NET Web API 中的路由</span><span class="sxs-lookup"><span data-stu-id="cd58a-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="cd58a-103">由[邁克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="cd58a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="cd58a-104">本文介紹ASP.NET Web API 如何將 HTTP 請求路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="cd58a-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="cd58a-105">如果您熟悉ASP.NET MVC,則Web API路由與MVC路由非常相似。</span><span class="sxs-lookup"><span data-stu-id="cd58a-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="cd58a-106">主要區別是 Web API 使用 HTTP 謂詞(而不是 URI 路徑)來選擇操作。</span><span class="sxs-lookup"><span data-stu-id="cd58a-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="cd58a-107">您還可以在 Web API 中使用 MVC 樣式路由。</span><span class="sxs-lookup"><span data-stu-id="cd58a-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="cd58a-108">本文不假定任何有關ASP.NET MVC 的知識。</span><span class="sxs-lookup"><span data-stu-id="cd58a-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="cd58a-109">路由表</span><span class="sxs-lookup"><span data-stu-id="cd58a-109">Routing Tables</span></span>

<span data-ttu-id="cd58a-110">在 Web API ASP.NET,*控制器*是處理 HTTP 請求的類。</span><span class="sxs-lookup"><span data-stu-id="cd58a-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="cd58a-111">控制器的公共方法稱為*管理程式*或簡單的*操作*。</span><span class="sxs-lookup"><span data-stu-id="cd58a-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="cd58a-112">當 Web API 框架收到請求時,它將請求路由到操作。</span><span class="sxs-lookup"><span data-stu-id="cd58a-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="cd58a-113">要決定要呼叫的操作,框架使用*路由表*格 。</span><span class="sxs-lookup"><span data-stu-id="cd58a-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="cd58a-114">Web API 的視覺化工作室專案樣本建立預設路由:</span><span class="sxs-lookup"><span data-stu-id="cd58a-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="cd58a-115">此路由在*WebApiConfig.cs*檔案中定義,該檔案放置在 *「\_應用開始」* 目錄中:</span><span class="sxs-lookup"><span data-stu-id="cd58a-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="cd58a-116">有關該類別的詳細資訊,`WebApiConfig`請參考[設定 ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cd58a-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="cd58a-117">如果自承載 Web API,則必須`HttpSelfHostConfiguration`直接在 物件上設置路由表。</span><span class="sxs-lookup"><span data-stu-id="cd58a-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="cd58a-118">有關詳細資訊,請參閱[自主機 Web API](../older-versions/self-host-a-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cd58a-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="cd58a-119">路由表中的每個項目都包含*一個路由樣本*。</span><span class="sxs-lookup"><span data-stu-id="cd58a-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="cd58a-120">Web API 的預設路由&quot;範本 是 api/{控制器}/{id}。&quot;</span><span class="sxs-lookup"><span data-stu-id="cd58a-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="cd58a-121">在此範本中&quot;,api&quot;是文字路徑段,[控制器] 和 {id} 是占位符變數。</span><span class="sxs-lookup"><span data-stu-id="cd58a-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="cd58a-122">當 Web API 框架收到 HTTP 請求時,它會嘗試將 URI 與路由表中的路由範本之一匹配。</span><span class="sxs-lookup"><span data-stu-id="cd58a-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="cd58a-123">如果沒有路由匹配,用戶端將收到 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="cd58a-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="cd58a-124">例如,以下 URI 與預設路由符合:</span><span class="sxs-lookup"><span data-stu-id="cd58a-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="cd58a-125">/api/觸點</span><span class="sxs-lookup"><span data-stu-id="cd58a-125">/api/contacts</span></span>
- <span data-ttu-id="cd58a-126">/api/觸點/1</span><span class="sxs-lookup"><span data-stu-id="cd58a-126">/api/contacts/1</span></span>
- <span data-ttu-id="cd58a-127">/api/產品/gizmo1</span><span class="sxs-lookup"><span data-stu-id="cd58a-127">/api/products/gizmo1</span></span>

<span data-ttu-id="cd58a-128">但是,以下 URI 不匹配,因為&quot;它缺少&quot;api 段:</span><span class="sxs-lookup"><span data-stu-id="cd58a-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="cd58a-129">/觸點/1</span><span class="sxs-lookup"><span data-stu-id="cd58a-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="cd58a-130">在路由中使用「api」的原因是為了避免與ASP.NET MVC 路由發生衝突。</span><span class="sxs-lookup"><span data-stu-id="cd58a-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="cd58a-131">這樣&quot;,您可以讓 /&quot;聯繫人 轉到 MVC 控制器&quot;,/api/ 聯繫人&quot;轉到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="cd58a-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="cd58a-132">當然,如果您不喜歡此約定,則可以更改預設路由表。</span><span class="sxs-lookup"><span data-stu-id="cd58a-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="cd58a-133">找到符合路由後,Web API 將選擇控制器和操作:</span><span class="sxs-lookup"><span data-stu-id="cd58a-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="cd58a-134">要查找控制器,Web&quot;API&quot;將控制器添加到 *[控制器]* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="cd58a-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="cd58a-135">要查找操作,Web API 將查看 HTTP 謂詞,然後查找名稱以該 HTTP 謂詞名稱開頭的操作。</span><span class="sxs-lookup"><span data-stu-id="cd58a-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="cd58a-136">例如,對於 GET 請求&quot;,Web API 會&quot;查找使用&quot;Get&quot;預&quot;置的操作&quot;,例如獲取 連絡人或獲取 所有連絡人。</span><span class="sxs-lookup"><span data-stu-id="cd58a-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="cd58a-137">此約定僅適用於 GET、POST、PUT、DELETE、頭、選項和 PATCH 謂詞。</span><span class="sxs-lookup"><span data-stu-id="cd58a-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="cd58a-138">您可以使用控制器上的屬性啟用其他 HTTP 謂詞。</span><span class="sxs-lookup"><span data-stu-id="cd58a-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="cd58a-139">稍後我們將看到示例。</span><span class="sxs-lookup"><span data-stu-id="cd58a-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="cd58a-140">製程路線樣本中的其他占位符變數(如 *{id})* 映射到操作參數。</span><span class="sxs-lookup"><span data-stu-id="cd58a-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="cd58a-141">讓我們看看以下範例。</span><span class="sxs-lookup"><span data-stu-id="cd58a-141">Let's look at an example.</span></span> <span data-ttu-id="cd58a-142">假設您定義以下控制器:</span><span class="sxs-lookup"><span data-stu-id="cd58a-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="cd58a-143">下面是一些可能的 HTTP 請求,以及為每個請求呼叫的操作:</span><span class="sxs-lookup"><span data-stu-id="cd58a-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="cd58a-144">HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="cd58a-144">HTTP Verb</span></span> | <span data-ttu-id="cd58a-145">URI 路徑</span><span class="sxs-lookup"><span data-stu-id="cd58a-145">URI Path</span></span> | <span data-ttu-id="cd58a-146">動作</span><span class="sxs-lookup"><span data-stu-id="cd58a-146">Action</span></span> | <span data-ttu-id="cd58a-147">參數</span><span class="sxs-lookup"><span data-stu-id="cd58a-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cd58a-148">GET</span><span class="sxs-lookup"><span data-stu-id="cd58a-148">GET</span></span> | <span data-ttu-id="cd58a-149">api/產品</span><span class="sxs-lookup"><span data-stu-id="cd58a-149">api/products</span></span> | <span data-ttu-id="cd58a-150">取得所有產品</span><span class="sxs-lookup"><span data-stu-id="cd58a-150">GetAllProducts</span></span> | <span data-ttu-id="cd58a-151">*(無)*</span><span class="sxs-lookup"><span data-stu-id="cd58a-151">*(none)*</span></span> |
| <span data-ttu-id="cd58a-152">GET</span><span class="sxs-lookup"><span data-stu-id="cd58a-152">GET</span></span> | <span data-ttu-id="cd58a-153">api/產品/4</span><span class="sxs-lookup"><span data-stu-id="cd58a-153">api/products/4</span></span> | <span data-ttu-id="cd58a-154">取得產品 ById</span><span class="sxs-lookup"><span data-stu-id="cd58a-154">GetProductById</span></span> | <span data-ttu-id="cd58a-155">4</span><span class="sxs-lookup"><span data-stu-id="cd58a-155">4</span></span> |
| <span data-ttu-id="cd58a-156">刪除</span><span class="sxs-lookup"><span data-stu-id="cd58a-156">DELETE</span></span> | <span data-ttu-id="cd58a-157">api/產品/4</span><span class="sxs-lookup"><span data-stu-id="cd58a-157">api/products/4</span></span> | <span data-ttu-id="cd58a-158">移除產品</span><span class="sxs-lookup"><span data-stu-id="cd58a-158">DeleteProduct</span></span> | <span data-ttu-id="cd58a-159">4</span><span class="sxs-lookup"><span data-stu-id="cd58a-159">4</span></span> |
| <span data-ttu-id="cd58a-160">POST</span><span class="sxs-lookup"><span data-stu-id="cd58a-160">POST</span></span> | <span data-ttu-id="cd58a-161">api/產品</span><span class="sxs-lookup"><span data-stu-id="cd58a-161">api/products</span></span> | <span data-ttu-id="cd58a-162">*( 不符合 )*</span><span class="sxs-lookup"><span data-stu-id="cd58a-162">*(no match)*</span></span> |  |

<span data-ttu-id="cd58a-163">請注意,URI 的 *[id]* 段(如果存在)映射到操作的*id*參數。</span><span class="sxs-lookup"><span data-stu-id="cd58a-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="cd58a-164">在此示例中,控制器定義了兩個 GET 方法,一個使用*id*參數,另一個沒有參數。</span><span class="sxs-lookup"><span data-stu-id="cd58a-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="cd58a-165">此外,請注意,POST 請求將失敗,因為控制器未&quot;定義 Post...&quot;方法。</span><span class="sxs-lookup"><span data-stu-id="cd58a-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="cd58a-166">路由變體</span><span class="sxs-lookup"><span data-stu-id="cd58a-166">Routing Variations</span></span>

<span data-ttu-id="cd58a-167">上一節介紹了ASP.NET Web API 的基本路由機制。</span><span class="sxs-lookup"><span data-stu-id="cd58a-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="cd58a-168">本節介紹一些變體。</span><span class="sxs-lookup"><span data-stu-id="cd58a-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="cd58a-169">HTTP 動詞</span><span class="sxs-lookup"><span data-stu-id="cd58a-169">HTTP verbs</span></span>

<span data-ttu-id="cd58a-170">無需對 HTTP 謂詞使用命名約定,還可以通過使用以下屬性之一來修飾操作方法之一,顯式指定操作的 HTTP 謂詞:</span><span class="sxs-lookup"><span data-stu-id="cd58a-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="cd58a-171">在下面的範例中,`FindProduct`該方法映射到 GET 請求:</span><span class="sxs-lookup"><span data-stu-id="cd58a-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="cd58a-172">要允許多個 HTTP 謂詞用於某個操作,或允許除 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP`[AcceptVerbs]`謂詞,請使用該屬性,該屬性採用 HTTP 謂詞的清單。</span><span class="sxs-lookup"><span data-stu-id="cd58a-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="cd58a-173">依操作名稱路由</span><span class="sxs-lookup"><span data-stu-id="cd58a-173">Routing by Action Name</span></span>

<span data-ttu-id="cd58a-174">使用預設路由範本,Web API 使用 HTTP 謂詞選擇操作。</span><span class="sxs-lookup"><span data-stu-id="cd58a-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="cd58a-175">但是,您還可以創建一個路由,其中操作名稱包含在 URI 中:</span><span class="sxs-lookup"><span data-stu-id="cd58a-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="cd58a-176">在此路由範本中 *,[操作]* 參數在控制器上命名操作方法。</span><span class="sxs-lookup"><span data-stu-id="cd58a-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="cd58a-177">使用此路由樣式,使用屬性指定允許的 HTTP 謂詞。</span><span class="sxs-lookup"><span data-stu-id="cd58a-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="cd58a-178">例如,假設您的控制器具有以下方法:</span><span class="sxs-lookup"><span data-stu-id="cd58a-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="cd58a-179">在這種情況下,GET 請求的"api/產品/詳細資訊/1"將映射`Details`到 該方法。</span><span class="sxs-lookup"><span data-stu-id="cd58a-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="cd58a-180">這種路由樣式類似於 mVC ASP.NET,可能適用於 RPC 樣式的 API。</span><span class="sxs-lookup"><span data-stu-id="cd58a-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="cd58a-181">可以使用 屬性重寫操作`[ActionName]`名稱 。</span><span class="sxs-lookup"><span data-stu-id="cd58a-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="cd58a-182">在下面的範例中,有兩個操作映射到&quot;api/產品/縮略圖/*id*。一個支援 GET,另一個支援 POST:</span><span class="sxs-lookup"><span data-stu-id="cd58a-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="cd58a-183">非操作</span><span class="sxs-lookup"><span data-stu-id="cd58a-183">Non-Actions</span></span>

<span data-ttu-id="cd58a-184">要防止將方法作為操作呼叫,請使用`[NonAction]`屬性 。</span><span class="sxs-lookup"><span data-stu-id="cd58a-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="cd58a-185">這向框架發出信號,說明該方法不是操作,即使它以其他方式與路由規則匹配也是如此。</span><span class="sxs-lookup"><span data-stu-id="cd58a-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="cd58a-186">進階閱讀</span><span class="sxs-lookup"><span data-stu-id="cd58a-186">Further Reading</span></span>

<span data-ttu-id="cd58a-187">本主題提供了路由的高級視圖。</span><span class="sxs-lookup"><span data-stu-id="cd58a-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="cd58a-188">有關詳細資訊,請參閱[路由和操作選擇](routing-and-action-selection.md),它準確描述框架如何將 URI 與路由匹配,選擇控制器,然後選擇要調用的操作。</span><span class="sxs-lookup"><span data-stu-id="cd58a-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
