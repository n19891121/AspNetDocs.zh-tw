---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 路由和 ASP.NET Web API 中的動作選項 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: ce54181996376cb5dde3b91c10c16f33b3c6a570
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058915"
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="50586-102">路由和 ASP.NET Web API 中的動作選取</span><span class="sxs-lookup"><span data-stu-id="50586-102">Routing and Action Selection in ASP.NET Web API</span></span>
====================
<span data-ttu-id="50586-103">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="50586-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="50586-104">這篇文章說明 ASP.NET Web API 將 HTTP 要求路由至特定動作的控制站上的方式。</span><span class="sxs-lookup"><span data-stu-id="50586-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="50586-105">路由的高階概觀，請參閱 < [ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="50586-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>


<span data-ttu-id="50586-106">這篇文章探討路由的處理程序的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="50586-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="50586-107">如果您建立 Web API 專案時，發現其中某些要求不會路由傳送您預期的方式，希望這篇文章會幫助。</span><span class="sxs-lookup"><span data-stu-id="50586-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="50586-108">路由有三個主要階段：</span><span class="sxs-lookup"><span data-stu-id="50586-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="50586-109">比對路由範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="50586-110">選取控制站。</span><span class="sxs-lookup"><span data-stu-id="50586-110">Selecting a controller.</span></span>
3. <span data-ttu-id="50586-111">選取一個動作。</span><span class="sxs-lookup"><span data-stu-id="50586-111">Selecting an action.</span></span>

<span data-ttu-id="50586-112">您可以將程序的某些部分取代您自己的自訂行為。</span><span class="sxs-lookup"><span data-stu-id="50586-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="50586-113">在本文中，我會說明的預設行為。</span><span class="sxs-lookup"><span data-stu-id="50586-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="50586-114">在結束時，我會說明您可以在此自訂行為的地方。</span><span class="sxs-lookup"><span data-stu-id="50586-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="50586-115">路由範本</span><span class="sxs-lookup"><span data-stu-id="50586-115">Route Templates</span></span>

<span data-ttu-id="50586-116">路由範本看起來類似的 URI 路徑，但它可以有預留位置值，以大括號：</span><span class="sxs-lookup"><span data-stu-id="50586-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="50586-117">當您建立路由時，您可以針對部分或全部的預留位置來提供預設值：</span><span class="sxs-lookup"><span data-stu-id="50586-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="50586-118">您也可以提供條件約束，限制如何 URI 區段可以比對的預留位置：</span><span class="sxs-lookup"><span data-stu-id="50586-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="50586-119">此架構會嘗試比對中範本的 URI 路徑的區段。</span><span class="sxs-lookup"><span data-stu-id="50586-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="50586-120">在範本中的常值必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="50586-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="50586-121">預留位置會符合任何值，除非您指定的條件約束。</span><span class="sxs-lookup"><span data-stu-id="50586-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="50586-122">此架構不符合的 URI，例如主機名稱或查詢參數的其他部分。</span><span class="sxs-lookup"><span data-stu-id="50586-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="50586-123">Framework 會選取符合 URI 的路由表中的第一個路由。</span><span class="sxs-lookup"><span data-stu-id="50586-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="50586-124">有兩個特殊的預留位置:"{controller}"和"{action}"。</span><span class="sxs-lookup"><span data-stu-id="50586-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="50586-125">"{controller}"提供的控制器名稱。</span><span class="sxs-lookup"><span data-stu-id="50586-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="50586-126">"{action}"提供動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="50586-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="50586-127">在 Web API 中，一般的慣例是省略"{action}"。</span><span class="sxs-lookup"><span data-stu-id="50586-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="50586-128">預設值</span><span class="sxs-lookup"><span data-stu-id="50586-128">Defaults</span></span>

<span data-ttu-id="50586-129">如果您提供預設值時，路由會符合缺少這些區段的 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="50586-130">例如: </span><span class="sxs-lookup"><span data-stu-id="50586-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="50586-131">Uri`http://localhost/api/products/all`和`http://localhost/api/products`符合上述的路由。</span><span class="sxs-lookup"><span data-stu-id="50586-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="50586-132">在後者的 URI、 遺漏`{category}`區段會指派預設值`all`。</span><span class="sxs-lookup"><span data-stu-id="50586-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="50586-133">路由字典</span><span class="sxs-lookup"><span data-stu-id="50586-133">Route Dictionary</span></span>

<span data-ttu-id="50586-134">如果架構找到相符項目 uri，它會建立字典，其中包含每個預留位置的值。</span><span class="sxs-lookup"><span data-stu-id="50586-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="50586-135">索引鍵是預留位置名稱，不包含大括號。</span><span class="sxs-lookup"><span data-stu-id="50586-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="50586-136">值取自 URI 的路徑或預設值。</span><span class="sxs-lookup"><span data-stu-id="50586-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="50586-137">字典會儲存在**IHttpRouteData**物件。</span><span class="sxs-lookup"><span data-stu-id="50586-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="50586-138">在此路由比對 」 階段中，特殊"{controller}"和"{action}"預留位置的處理就像其他版面配置。</span><span class="sxs-lookup"><span data-stu-id="50586-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="50586-139">它們只會儲存在其他值的字典。</span><span class="sxs-lookup"><span data-stu-id="50586-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="50586-140">預設值可以有特殊值**RouteParameter.Optional**。</span><span class="sxs-lookup"><span data-stu-id="50586-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="50586-141">預留位置會指派此值，如果值不會加入至路由字典。</span><span class="sxs-lookup"><span data-stu-id="50586-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="50586-142">例如: </span><span class="sxs-lookup"><span data-stu-id="50586-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="50586-143">URI 路徑 「 api/產品 」 中，將會包含路由字典：</span><span class="sxs-lookup"><span data-stu-id="50586-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="50586-144">控制站: 「 產品 」</span><span class="sxs-lookup"><span data-stu-id="50586-144">controller: "products"</span></span>
- <span data-ttu-id="50586-145">類別目錄: [全部]</span><span class="sxs-lookup"><span data-stu-id="50586-145">category: "all"</span></span>

<span data-ttu-id="50586-146">"Api/產品/toys/123"，不過，路由字典會包含：</span><span class="sxs-lookup"><span data-stu-id="50586-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="50586-147">控制站: 「 產品 」</span><span class="sxs-lookup"><span data-stu-id="50586-147">controller: "products"</span></span>
- <span data-ttu-id="50586-148">類別: 「 玩具 」</span><span class="sxs-lookup"><span data-stu-id="50586-148">category: "toys"</span></span>
- <span data-ttu-id="50586-149">識別碼："123"</span><span class="sxs-lookup"><span data-stu-id="50586-149">id: "123"</span></span>

<span data-ttu-id="50586-150">預設值也可以在路由範本中包含值，不會不出現在任何地方。</span><span class="sxs-lookup"><span data-stu-id="50586-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="50586-151">如果路由符合，該值會儲存在字典中。</span><span class="sxs-lookup"><span data-stu-id="50586-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="50586-152">例如: </span><span class="sxs-lookup"><span data-stu-id="50586-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="50586-153">如果 URI 的路徑是"api/root/8"，字典會包含兩個值：</span><span class="sxs-lookup"><span data-stu-id="50586-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="50586-154">控制站: 「 客戶 」</span><span class="sxs-lookup"><span data-stu-id="50586-154">controller: "customers"</span></span>
- <span data-ttu-id="50586-155">識別碼："8"</span><span class="sxs-lookup"><span data-stu-id="50586-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="50586-156">選取控制站</span><span class="sxs-lookup"><span data-stu-id="50586-156">Selecting a Controller</span></span>

<span data-ttu-id="50586-157">控制器選取項目由**IHttpControllerSelector.SelectController**方法。</span><span class="sxs-lookup"><span data-stu-id="50586-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="50586-158">這個方法會採用**HttpRequestMessage**執行個體，並傳回**HttpControllerDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="50586-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="50586-159">預設實作由提供**DefaultHttpControllerSelector**類別。</span><span class="sxs-lookup"><span data-stu-id="50586-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="50586-160">這個類別會使用簡單的演算法：</span><span class="sxs-lookup"><span data-stu-id="50586-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="50586-161">查看路由字典的索引鍵"controller"。</span><span class="sxs-lookup"><span data-stu-id="50586-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="50586-162">此索引鍵的值，並附加 「 控制器 」 以取得控制器的型別名稱的字串。</span><span class="sxs-lookup"><span data-stu-id="50586-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="50586-163">使用此型別名稱的 Web API 控制器的外觀。</span><span class="sxs-lookup"><span data-stu-id="50586-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="50586-164">比方說，如果路由字典包含索引鍵 / 值組"controller"= 「 產品 」，則控制器類型是"ProductsController 」。</span><span class="sxs-lookup"><span data-stu-id="50586-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="50586-165">如果沒有任何相符的類型或多個相符項目，架構就會傳回錯誤給用戶端。</span><span class="sxs-lookup"><span data-stu-id="50586-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="50586-166">步驟 3 中，如**DefaultHttpControllerSelector**會使用**IHttpControllerTypeResolver**介面，以取得 Web API 控制器型別的清單。</span><span class="sxs-lookup"><span data-stu-id="50586-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="50586-167">預設實作**IHttpControllerTypeResolver** （a） 實作會傳回所有公用類別**IHttpController**，（b） 都不抽象，且 （c） 中"Controller"結尾的名稱。</span><span class="sxs-lookup"><span data-stu-id="50586-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="50586-168">動作選取</span><span class="sxs-lookup"><span data-stu-id="50586-168">Action Selection</span></span>

<span data-ttu-id="50586-169">選取控制站之後, 此架構，請選取藉由呼叫的動作**IHttpActionSelector.SelectAction**方法。</span><span class="sxs-lookup"><span data-stu-id="50586-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="50586-170">這個方法會採用**HttpControllerContext** ，然後傳回**HttpActionDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="50586-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="50586-171">預設實作由提供**ApiControllerActionSelector**類別。</span><span class="sxs-lookup"><span data-stu-id="50586-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="50586-172">若要選取的動作，它會查看下列：</span><span class="sxs-lookup"><span data-stu-id="50586-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="50586-173">要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="50586-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="50586-174">在路由範本中，如果有的話"{action}"預留位置。</span><span class="sxs-lookup"><span data-stu-id="50586-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="50586-175">在控制器上的動作參數。</span><span class="sxs-lookup"><span data-stu-id="50586-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="50586-176">之前查看選取演算法，我們必須了解有關控制器動作的一些事項。</span><span class="sxs-lookup"><span data-stu-id="50586-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="50586-177">**在控制器上的方法會視為 「 動作 」？**</span><span class="sxs-lookup"><span data-stu-id="50586-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="50586-178">當選取一個動作，架構只查看公用執行個體方法的控制站上。</span><span class="sxs-lookup"><span data-stu-id="50586-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="50586-179">此外，它會排除[「 特殊名稱 」](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) （建構函式、 事件、 運算子多載，等等） 的方法和方法繼承自**ApiController**類別。</span><span class="sxs-lookup"><span data-stu-id="50586-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="50586-180">**HTTP 方法。**</span><span class="sxs-lookup"><span data-stu-id="50586-180">**HTTP Methods.**</span></span> <span data-ttu-id="50586-181">架構只會選擇符合要求的 HTTP 方法，取決於下列動作：</span><span class="sxs-lookup"><span data-stu-id="50586-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="50586-182">您可以使用屬性來指定 HTTP 方法：**AcceptVerbs**， **HttpDelete**， **HttpGet**， **HttpHead**， **HttpOptions**， **HttpPatch**， **HttpPost**，或**HttpPut**。</span><span class="sxs-lookup"><span data-stu-id="50586-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="50586-183">否則，如果以"Get"、"Post"、"Put"、"Delete"、"Head"、 [選項] 或 「 修補 」 開頭的控制器方法的名稱，然後依照慣例動作支援該 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="50586-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="50586-184">如果以上皆非，方法支援 POST。</span><span class="sxs-lookup"><span data-stu-id="50586-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="50586-185">**參數繫結。**</span><span class="sxs-lookup"><span data-stu-id="50586-185">**Parameter Bindings.**</span></span> <span data-ttu-id="50586-186">參數繫結是 Web API 建立參數的值的方式。</span><span class="sxs-lookup"><span data-stu-id="50586-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="50586-187">以下是參數繫結的預設規則：</span><span class="sxs-lookup"><span data-stu-id="50586-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="50586-188">簡單型別取自 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="50586-189">複雜型別會從要求主體。</span><span class="sxs-lookup"><span data-stu-id="50586-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="50586-190">簡單的型別包含的所有[.NET Framework 基本型別](https://msdn.microsoft.com/library/system.type.isprimitive)，再加上**DateTime**，**十進位**， **Guid**，**字串**，並**TimeSpan**。</span><span class="sxs-lookup"><span data-stu-id="50586-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="50586-191">針對每個動作中，最多一個參數可以讀取的要求主體。</span><span class="sxs-lookup"><span data-stu-id="50586-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="50586-192">可以覆寫預設繫結規則。</span><span class="sxs-lookup"><span data-stu-id="50586-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="50586-193">請參閱[WebAPI 參數繫結，在幕後](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)。</span><span class="sxs-lookup"><span data-stu-id="50586-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>


<span data-ttu-id="50586-194">有了此背景，以下是動作選取演算法。</span><span class="sxs-lookup"><span data-stu-id="50586-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="50586-195">符合 HTTP 要求方法的控制站上建立之所有動作的清單。</span><span class="sxs-lookup"><span data-stu-id="50586-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="50586-196">如果路由字典中有 「 動作 」 項目，將移除其名稱不符合此值的動作。</span><span class="sxs-lookup"><span data-stu-id="50586-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="50586-197">嘗試比對 URI、 動作參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="50586-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="50586-198">針對每個動作中，取得一份是簡單型別，其中會將繫結參數來自 URI 的參數。</span><span class="sxs-lookup"><span data-stu-id="50586-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="50586-199">排除的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="50586-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="50586-200">從這份清單中，嘗試尋找名稱相符的每個參數，在路由字典或 URI 查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="50586-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="50586-201">相符項目不區分大小寫和參數的順序無關。</span><span class="sxs-lookup"><span data-stu-id="50586-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="50586-202">選取清單中的每個參數具有相符項目之 URI 中的其中一個動作。</span><span class="sxs-lookup"><span data-stu-id="50586-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="50586-203">如果更該動作符合這些準則，挑選其中的大部分參數相符項目。</span><span class="sxs-lookup"><span data-stu-id="50586-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="50586-204">忽略動作 **[NonAction]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="50586-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="50586-205">步驟 #3 是可能最容易造成混淆。</span><span class="sxs-lookup"><span data-stu-id="50586-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="50586-206">基本概念是來自 URI，從要求主體中，或是從自訂繫結參數可取得其值。</span><span class="sxs-lookup"><span data-stu-id="50586-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="50586-207">對於來自 URI 的參數，我們想要確定該 URI 實際上包含該參數，在 （透過路由字典） 的路徑或查詢字串中的值。</span><span class="sxs-lookup"><span data-stu-id="50586-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="50586-208">例如，請考慮下列動作：</span><span class="sxs-lookup"><span data-stu-id="50586-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="50586-209">*識別碼*參數繫結至的 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="50586-210">因此，此動作可以只比對 URI，其中包含 「 識別碼 」，在 路由字典或查詢字串中的值。</span><span class="sxs-lookup"><span data-stu-id="50586-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="50586-211">選擇性參數會是例外狀況，因為它們是選擇性。</span><span class="sxs-lookup"><span data-stu-id="50586-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="50586-212">選擇性參數，就可以繫結無法從 URI 取得的值。</span><span class="sxs-lookup"><span data-stu-id="50586-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="50586-213">複雜型別會因其他原因的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="50586-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="50586-214">透過自訂繫結的複雜型別只能繫結至的 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="50586-215">但在此情況下，架構無法事先知道參數會繫結至特定的 URI。</span><span class="sxs-lookup"><span data-stu-id="50586-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="50586-216">若要了解，它必須叫用繫結。</span><span class="sxs-lookup"><span data-stu-id="50586-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="50586-217">選擇演算法的目標是靜態的描述，然後再叫用任何繫結從選取的動作。</span><span class="sxs-lookup"><span data-stu-id="50586-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="50586-218">因此，複雜型別會排除比對演算法。</span><span class="sxs-lookup"><span data-stu-id="50586-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="50586-219">選取動作之後，會叫用所有的參數繫結。</span><span class="sxs-lookup"><span data-stu-id="50586-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="50586-220">摘要: </span><span class="sxs-lookup"><span data-stu-id="50586-220">Summary:</span></span>

- <span data-ttu-id="50586-221">Action 必須符合要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="50586-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="50586-222">動作名稱必須符合 「 動作 」 中的項目路由字典，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="50586-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="50586-223">每個參數的動作，如果參數取自 URI，然後參數名稱必須找到路由字典或 URI 查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="50586-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="50586-224">（選擇性參數，而且具有複雜類型的參數會排除。）</span><span class="sxs-lookup"><span data-stu-id="50586-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="50586-225">嘗試比對參數最大數目。</span><span class="sxs-lookup"><span data-stu-id="50586-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="50586-226">最符合項目可能不含任何參數的方法。</span><span class="sxs-lookup"><span data-stu-id="50586-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="50586-227">延伸的範例</span><span class="sxs-lookup"><span data-stu-id="50586-227">Extended Example</span></span>

<span data-ttu-id="50586-228">路由：</span><span class="sxs-lookup"><span data-stu-id="50586-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="50586-229">控制器: </span><span class="sxs-lookup"><span data-stu-id="50586-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="50586-230">HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="50586-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="50586-231">路由相符</span><span class="sxs-lookup"><span data-stu-id="50586-231">Route Matching</span></span>

<span data-ttu-id="50586-232">URI 比對名為"DefaultApi"的路由。</span><span class="sxs-lookup"><span data-stu-id="50586-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="50586-233">路由字典包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="50586-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="50586-234">控制站: 「 產品 」</span><span class="sxs-lookup"><span data-stu-id="50586-234">controller: "products"</span></span>
- <span data-ttu-id="50586-235">識別碼："1"</span><span class="sxs-lookup"><span data-stu-id="50586-235">id: "1"</span></span>

<span data-ttu-id="50586-236">路由字典不包含查詢字串參數，"version"和"details"，但這些仍然會被視為動作選取的期間。</span><span class="sxs-lookup"><span data-stu-id="50586-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="50586-237">控制器選取項目</span><span class="sxs-lookup"><span data-stu-id="50586-237">Controller Selection</span></span>

<span data-ttu-id="50586-238">從路由字典中的 「 控制器 」 項目，是控制器類型`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="50586-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="50586-239">動作選取</span><span class="sxs-lookup"><span data-stu-id="50586-239">Action Selection</span></span>

<span data-ttu-id="50586-240">HTTP 要求是 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="50586-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="50586-241">支援 GET 的控制器動作`GetAll`， `GetById`，和`FindProductsByName`。</span><span class="sxs-lookup"><span data-stu-id="50586-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="50586-242">路由字典不包含 「 動作 」，項目，因此我們不需要的動作名稱相符。</span><span class="sxs-lookup"><span data-stu-id="50586-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="50586-243">接下來，我們嘗試比對的動作，參數名稱顯見光看 GET 動作。</span><span class="sxs-lookup"><span data-stu-id="50586-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="50586-244">動作</span><span class="sxs-lookup"><span data-stu-id="50586-244">Action</span></span> | <span data-ttu-id="50586-245">要比對參數</span><span class="sxs-lookup"><span data-stu-id="50586-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="50586-246">none</span><span class="sxs-lookup"><span data-stu-id="50586-246">none</span></span> |
| `GetById` | <span data-ttu-id="50586-247">"id"</span><span class="sxs-lookup"><span data-stu-id="50586-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="50586-248">"name"</span><span class="sxs-lookup"><span data-stu-id="50586-248">"name"</span></span> |

<span data-ttu-id="50586-249">請注意，*版本*參數`GetById`不是，因為它是選擇性的參數。</span><span class="sxs-lookup"><span data-stu-id="50586-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="50586-250">`GetAll`方法符合透過極簡方式。</span><span class="sxs-lookup"><span data-stu-id="50586-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="50586-251">`GetById`方法也會比對，因為路由字典包含 「 識別碼 」。</span><span class="sxs-lookup"><span data-stu-id="50586-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="50586-252">`FindProductsByName`方法不符。</span><span class="sxs-lookup"><span data-stu-id="50586-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="50586-253">`GetById` Wins 方法，因為它會比對一個參數，也沒有參數與`GetAll`。</span><span class="sxs-lookup"><span data-stu-id="50586-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="50586-254">叫用方法時，使用下列參數值：</span><span class="sxs-lookup"><span data-stu-id="50586-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="50586-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="50586-255">*id* = 1</span></span>
- <span data-ttu-id="50586-256">*版本*= 1.5</span><span class="sxs-lookup"><span data-stu-id="50586-256">*version* = 1.5</span></span>

<span data-ttu-id="50586-257">請注意，即使*版本*未使用在選取演算法參數的值來自 URI 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="50586-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="50586-258">擴充點</span><span class="sxs-lookup"><span data-stu-id="50586-258">Extension Points</span></span>

<span data-ttu-id="50586-259">Web API 路由的處理程序的某些部分來提供擴充點。</span><span class="sxs-lookup"><span data-stu-id="50586-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="50586-260">介面</span><span class="sxs-lookup"><span data-stu-id="50586-260">Interface</span></span> | <span data-ttu-id="50586-261">描述</span><span class="sxs-lookup"><span data-stu-id="50586-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50586-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="50586-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="50586-263">選取的控制器。</span><span class="sxs-lookup"><span data-stu-id="50586-263">Selects the controller.</span></span> |
| <span data-ttu-id="50586-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="50586-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="50586-265">取得控制器型別的清單。</span><span class="sxs-lookup"><span data-stu-id="50586-265">Gets the list of controller types.</span></span> <span data-ttu-id="50586-266">**DefaultHttpControllerSelector**從這份清單中選擇 控制器類型。</span><span class="sxs-lookup"><span data-stu-id="50586-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="50586-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="50586-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="50586-268">取得專案的組件清單。</span><span class="sxs-lookup"><span data-stu-id="50586-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="50586-269">**IHttpControllerTypeResolver**介面使用這份清單來尋找控制器類型。</span><span class="sxs-lookup"><span data-stu-id="50586-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="50586-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="50586-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="50586-271">建立新的控制器執行個體。</span><span class="sxs-lookup"><span data-stu-id="50586-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="50586-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="50586-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="50586-273">選取的動作。</span><span class="sxs-lookup"><span data-stu-id="50586-273">Selects the action.</span></span> |
| <span data-ttu-id="50586-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="50586-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="50586-275">叫用動作。</span><span class="sxs-lookup"><span data-stu-id="50586-275">Invokes the action.</span></span> |

<span data-ttu-id="50586-276">若要提供您自己的實作這些介面，使用**Services**收集**HttpConfiguration**物件：</span><span class="sxs-lookup"><span data-stu-id="50586-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
