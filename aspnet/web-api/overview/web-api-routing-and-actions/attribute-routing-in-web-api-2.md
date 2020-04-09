---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的屬性路由 |微軟文件
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675390"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="2411e-102">ASP.NET Web API 2 中的屬性路由</span><span class="sxs-lookup"><span data-stu-id="2411e-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="2411e-103">由[邁克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2411e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2411e-104">*路由*是 Web API 將 URI 與操作匹配的方式。</span><span class="sxs-lookup"><span data-stu-id="2411e-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="2411e-105">Web API 2 支援一種稱為*屬性路由*的新型路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="2411e-106">顧名思義,屬性路由使用屬性來定義路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="2411e-107">屬性路由使您能夠對 Web API 中的 URI 進行更多控制。</span><span class="sxs-lookup"><span data-stu-id="2411e-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="2411e-108">例如,您可以輕鬆地創建描述資源層次結構的 URI。</span><span class="sxs-lookup"><span data-stu-id="2411e-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="2411e-109">早期路由樣式(稱為基於約定的路由)仍完全支援。</span><span class="sxs-lookup"><span data-stu-id="2411e-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="2411e-110">事實上,您可以將這兩種技術合併到同一專案中。</span><span class="sxs-lookup"><span data-stu-id="2411e-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="2411e-111">本主題演示如何啟用屬性路由,並介紹屬性路由的各種選項。</span><span class="sxs-lookup"><span data-stu-id="2411e-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="2411e-112">有關使用屬性路由的端到端教程,請參閱[在 Web API 2 中使用屬性路由創建 REST API。](create-a-rest-api-with-attribute-routing.md)</span><span class="sxs-lookup"><span data-stu-id="2411e-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2411e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2411e-113">Prerequisites</span></span>

<span data-ttu-id="2411e-114">[視覺工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區版、專業版或企業版</span><span class="sxs-lookup"><span data-stu-id="2411e-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="2411e-115">或者,使用 NuGet 包管理器安裝必要的包。</span><span class="sxs-lookup"><span data-stu-id="2411e-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="2411e-116">從 Visual Studio 中的 **「工具**」功能表中,選擇**NuGet 套件管理器**,然後選擇 **「包管理器控制台**」。</span><span class="sxs-lookup"><span data-stu-id="2411e-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2411e-117">在套件管理員主控台視窗中輸入以下指令:</span><span class="sxs-lookup"><span data-stu-id="2411e-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="2411e-118">為什麼選擇屬性路由?</span><span class="sxs-lookup"><span data-stu-id="2411e-118">Why Attribute Routing?</span></span>

<span data-ttu-id="2411e-119">Web API 的第一個版本使用了*基於約定的*路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="2411e-120">在這種類型的路由中,定義一個或多個路由範本,這些範本基本上是參數化字串。</span><span class="sxs-lookup"><span data-stu-id="2411e-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="2411e-121">當框架收到請求時,它將URI與路由範本匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="2411e-122">有關基於約定的路由的詳細資訊,請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2411e-122">For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="2411e-123">基於約定的路由的一個優點是範本在一個位置定義,並且路由規則在所有控制器之間一致應用。</span><span class="sxs-lookup"><span data-stu-id="2411e-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="2411e-124">遺憾的是,基於約定的路由很難支援 RESTful API 中常見的某些 URI 模式。</span><span class="sxs-lookup"><span data-stu-id="2411e-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="2411e-125">例如,資源通常包含子資源:客戶有訂單,電影有演員,書籍有作者,等等。</span><span class="sxs-lookup"><span data-stu-id="2411e-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="2411e-126">建立反映這些關係的 URI 是很自然的:</span><span class="sxs-lookup"><span data-stu-id="2411e-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="2411e-127">這種類型的URI很難使用基於約定的路由創建。</span><span class="sxs-lookup"><span data-stu-id="2411e-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="2411e-128">儘管可以做到這一點,但如果您有許多控制器或資源類型,則結果不會很好地擴展。</span><span class="sxs-lookup"><span data-stu-id="2411e-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="2411e-129">使用屬性路由,為此URI定義路由非常簡單。</span><span class="sxs-lookup"><span data-stu-id="2411e-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="2411e-130">只需向控制器操作新增屬性:</span><span class="sxs-lookup"><span data-stu-id="2411e-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="2411e-131">下面是一些其他模式,屬性路由使容易。</span><span class="sxs-lookup"><span data-stu-id="2411e-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="2411e-132">**API 版本控制**</span><span class="sxs-lookup"><span data-stu-id="2411e-132">**API versioning**</span></span>

<span data-ttu-id="2411e-133">在此示例中,"/api/v1/產品"將路由到與"/api/v2/產品"不同的控制器。</span><span class="sxs-lookup"><span data-stu-id="2411e-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="2411e-134">**重載 URI 段**</span><span class="sxs-lookup"><span data-stu-id="2411e-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="2411e-135">在此示例中,「1」是訂單號,但「掛起」映射到集合。</span><span class="sxs-lookup"><span data-stu-id="2411e-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="2411e-136">**多種參數類型**</span><span class="sxs-lookup"><span data-stu-id="2411e-136">**Multiple parameter types**</span></span>

<span data-ttu-id="2411e-137">在此示例中,"1"是訂單號,但"2013/06/16"指定日期。</span><span class="sxs-lookup"><span data-stu-id="2411e-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="2411e-138">開啟屬性路由</span><span class="sxs-lookup"><span data-stu-id="2411e-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="2411e-139">要啟用屬性路由,請在配置期間調用**MapHttpAttributeRoutes。**</span><span class="sxs-lookup"><span data-stu-id="2411e-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="2411e-140">此擴充方法在**System.Web.http.HTTP:設定擴充**套件中定義。</span><span class="sxs-lookup"><span data-stu-id="2411e-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="2411e-141">屬性路由可以與[基於約定的](routing-in-aspnet-web-api.md)路由組合使用。</span><span class="sxs-lookup"><span data-stu-id="2411e-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="2411e-142">要定義基於約定的路由,請調用**MapHTTPRoute**方法。</span><span class="sxs-lookup"><span data-stu-id="2411e-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="2411e-143">有關設定 Web API 的詳細資訊,請參閱[設定 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2411e-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="2411e-144">注意:從 Web API 1 移轉</span><span class="sxs-lookup"><span data-stu-id="2411e-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="2411e-145">在 Web API 2 之前,Web API 專案樣本產生了如下所示的代碼:</span><span class="sxs-lookup"><span data-stu-id="2411e-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="2411e-146">如果啟用了屬性路由,則此代碼將引發異常。</span><span class="sxs-lookup"><span data-stu-id="2411e-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="2411e-147">如果將現有 Web API 專案升級為使用屬性路由,請確保將此設定代碼更新為以下內容:</span><span class="sxs-lookup"><span data-stu-id="2411e-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="2411e-148">有關詳細資訊,請參閱[使用託管ASP.NET配置 Web API。](../advanced/configuring-aspnet-web-api.md#webhost)</span><span class="sxs-lookup"><span data-stu-id="2411e-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="2411e-149">新增路由屬性</span><span class="sxs-lookup"><span data-stu-id="2411e-149">Adding Route Attributes</span></span>

<span data-ttu-id="2411e-150">下面是使用屬性定義的路由的範例:</span><span class="sxs-lookup"><span data-stu-id="2411e-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="2411e-151">字串&quot;客戶/[客戶 Id]/&quot;訂單 是路由的 URI 範本。</span><span class="sxs-lookup"><span data-stu-id="2411e-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="2411e-152">Web API 嘗試將請求 URI 與範本匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="2411e-153">在此示例中,"客戶"和"訂單"是文本段,"[客戶Id]"是一個變數參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="2411e-154">以下 URI 將符合此樣本:</span><span class="sxs-lookup"><span data-stu-id="2411e-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="2411e-155">您可以使用[約束](#constraints)來限制匹配,本主題稍後將介紹。</span><span class="sxs-lookup"><span data-stu-id="2411e-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="2411e-156">請注意,&quot;製程路線樣本中的&quot;{customerId} 參數與 方法中的*customerId*參數的名稱匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="2411e-157">當 Web API 呼叫控制器操作時,它嘗試綁定路由參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="2411e-158">例如,如果 URI`http://example.com/customers/1/orders`是 ,Web API 會嘗試在操作中將值「1」綁定到*customerId*參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="2411e-159">URI 樣本可以具有多個參數:</span><span class="sxs-lookup"><span data-stu-id="2411e-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="2411e-160">沒有任何路由屬性的控制器方法都使用基於約定的路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="2411e-161">這樣,可以將兩種類型的路由合併到同一專案中。</span><span class="sxs-lookup"><span data-stu-id="2411e-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2411e-162">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="2411e-162">HTTP Methods</span></span>

<span data-ttu-id="2411e-163">Web API 還根據請求的 HTTP 方法(GET、POST 等)選擇操作。</span><span class="sxs-lookup"><span data-stu-id="2411e-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="2411e-164">默認情況下,Web API 查找與控制器方法名稱開頭不區分大小寫的匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="2411e-165">例如,名為的`PutCustomers`控制器方法與 HTTP PUT 請求匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="2411e-166">您可以通過使用以下任何屬性修飾方法來重寫此約定:</span><span class="sxs-lookup"><span data-stu-id="2411e-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="2411e-167">**[ HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="2411e-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="2411e-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="2411e-168">**[HttpGet]**</span></span>
- <span data-ttu-id="2411e-169">**[HTTPHead]**</span><span class="sxs-lookup"><span data-stu-id="2411e-169">**[HttpHead]**</span></span>
- <span data-ttu-id="2411e-170">**【 HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="2411e-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="2411e-171">**[HTTPPatch]**</span><span class="sxs-lookup"><span data-stu-id="2411e-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="2411e-172">**[ HTTPPost]**</span><span class="sxs-lookup"><span data-stu-id="2411e-172">**[HttpPost]**</span></span>
- <span data-ttu-id="2411e-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="2411e-173">**[HttpPut]**</span></span>

<span data-ttu-id="2411e-174">下面的範例將 CreateBook 方法映射到 HTTP POST 請求。</span><span class="sxs-lookup"><span data-stu-id="2411e-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="2411e-175">對於所有其他 HTTP 方法(包括非標準方法),請使用**AcceptVerbs**屬性,該屬性採用 HTTP 方法的清單。</span><span class="sxs-lookup"><span data-stu-id="2411e-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="2411e-176">路由前置碼</span><span class="sxs-lookup"><span data-stu-id="2411e-176">Route Prefixes</span></span>

<span data-ttu-id="2411e-177">通常,控制器中的路由都以相同的首碼開頭。</span><span class="sxs-lookup"><span data-stu-id="2411e-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="2411e-178">例如：</span><span class="sxs-lookup"><span data-stu-id="2411e-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="2411e-179">您可以使用 **[RoutePrefix]** 屬性為整個控制器設定公共前置前置字串:</span><span class="sxs-lookup"><span data-stu-id="2411e-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="2411e-180">在方法屬性上使用波浪線 (\*) 來覆蓋路由首碼:</span><span class="sxs-lookup"><span data-stu-id="2411e-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="2411e-181">路由前置字串可以包含參數:</span><span class="sxs-lookup"><span data-stu-id="2411e-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="2411e-182">路由約束</span><span class="sxs-lookup"><span data-stu-id="2411e-182">Route Constraints</span></span>

<span data-ttu-id="2411e-183">通過路由約束,您可以限制路由範本中的參數的匹配方式。</span><span class="sxs-lookup"><span data-stu-id="2411e-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="2411e-184">一般語法是&quot;[參數:&quot;約束 ] 。</span><span class="sxs-lookup"><span data-stu-id="2411e-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="2411e-185">例如：</span><span class="sxs-lookup"><span data-stu-id="2411e-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="2411e-186">此處,僅當URI的ID&quot;&quot;段是整數時,才會選擇第一個路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="2411e-187">否則,將選擇第二個路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="2411e-188">下表列出了支援的約束。</span><span class="sxs-lookup"><span data-stu-id="2411e-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="2411e-189">條件約束</span><span class="sxs-lookup"><span data-stu-id="2411e-189">Constraint</span></span> | <span data-ttu-id="2411e-190">描述</span><span class="sxs-lookup"><span data-stu-id="2411e-190">Description</span></span> | <span data-ttu-id="2411e-191">範例</span><span class="sxs-lookup"><span data-stu-id="2411e-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2411e-192">alpha</span><span class="sxs-lookup"><span data-stu-id="2411e-192">alpha</span></span> | <span data-ttu-id="2411e-193">符合大寫或小寫拉丁字母字元(a-z,A-Z)</span><span class="sxs-lookup"><span data-stu-id="2411e-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="2411e-194">[x:阿爾法]</span><span class="sxs-lookup"><span data-stu-id="2411e-194">{x:alpha}</span></span> |
| <span data-ttu-id="2411e-195">bool</span><span class="sxs-lookup"><span data-stu-id="2411e-195">bool</span></span> | <span data-ttu-id="2411e-196">匹配布爾值。</span><span class="sxs-lookup"><span data-stu-id="2411e-196">Matches a Boolean value.</span></span> | <span data-ttu-id="2411e-197">{x:布爾]</span><span class="sxs-lookup"><span data-stu-id="2411e-197">{x:bool}</span></span> |
| <span data-ttu-id="2411e-198">Datetime</span><span class="sxs-lookup"><span data-stu-id="2411e-198">datetime</span></span> | <span data-ttu-id="2411e-199">匹配**日期時間**值。</span><span class="sxs-lookup"><span data-stu-id="2411e-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="2411e-200">[x:日期時間]</span><span class="sxs-lookup"><span data-stu-id="2411e-200">{x:datetime}</span></span> |
| <span data-ttu-id="2411e-201">decimal</span><span class="sxs-lookup"><span data-stu-id="2411e-201">decimal</span></span> | <span data-ttu-id="2411e-202">匹配十進位值。</span><span class="sxs-lookup"><span data-stu-id="2411e-202">Matches a decimal value.</span></span> | <span data-ttu-id="2411e-203">[x:十進位]</span><span class="sxs-lookup"><span data-stu-id="2411e-203">{x:decimal}</span></span> |
| <span data-ttu-id="2411e-204">double</span><span class="sxs-lookup"><span data-stu-id="2411e-204">double</span></span> | <span data-ttu-id="2411e-205">匹配64位浮點值。</span><span class="sxs-lookup"><span data-stu-id="2411e-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="2411e-206">[x:雙]</span><span class="sxs-lookup"><span data-stu-id="2411e-206">{x:double}</span></span> |
| <span data-ttu-id="2411e-207">FLOAT</span><span class="sxs-lookup"><span data-stu-id="2411e-207">float</span></span> | <span data-ttu-id="2411e-208">匹配 32 位浮點值。</span><span class="sxs-lookup"><span data-stu-id="2411e-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="2411e-209">[x:浮動]</span><span class="sxs-lookup"><span data-stu-id="2411e-209">{x:float}</span></span> |
| <span data-ttu-id="2411e-210">guid</span><span class="sxs-lookup"><span data-stu-id="2411e-210">guid</span></span> | <span data-ttu-id="2411e-211">匹配 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="2411e-211">Matches a GUID value.</span></span> | <span data-ttu-id="2411e-212">{x:吉德]</span><span class="sxs-lookup"><span data-stu-id="2411e-212">{x:guid}</span></span> |
| <span data-ttu-id="2411e-213">int</span><span class="sxs-lookup"><span data-stu-id="2411e-213">int</span></span> | <span data-ttu-id="2411e-214">匹配 32 位整數值。</span><span class="sxs-lookup"><span data-stu-id="2411e-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="2411e-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="2411e-215">{x:int}</span></span> |
| <span data-ttu-id="2411e-216">長度</span><span class="sxs-lookup"><span data-stu-id="2411e-216">length</span></span> | <span data-ttu-id="2411e-217">將字串與指定長度或指定長度範圍內的字串匹配。</span><span class="sxs-lookup"><span data-stu-id="2411e-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="2411e-218">[x:長度(6)][x:長度(1,20)]</span><span class="sxs-lookup"><span data-stu-id="2411e-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="2411e-219">long</span><span class="sxs-lookup"><span data-stu-id="2411e-219">long</span></span> | <span data-ttu-id="2411e-220">匹配64位整數值。</span><span class="sxs-lookup"><span data-stu-id="2411e-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="2411e-221">[x:長]</span><span class="sxs-lookup"><span data-stu-id="2411e-221">{x:long}</span></span> |
| <span data-ttu-id="2411e-222">max</span><span class="sxs-lookup"><span data-stu-id="2411e-222">max</span></span> | <span data-ttu-id="2411e-223">匹配具有最大值的整數。</span><span class="sxs-lookup"><span data-stu-id="2411e-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="2411e-224">{x:最大(10)]</span><span class="sxs-lookup"><span data-stu-id="2411e-224">{x:max(10)}</span></span> |
| <span data-ttu-id="2411e-225">最大長度</span><span class="sxs-lookup"><span data-stu-id="2411e-225">maxlength</span></span> | <span data-ttu-id="2411e-226">匹配具有最大長度的字串。</span><span class="sxs-lookup"><span data-stu-id="2411e-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="2411e-227">{x:最大長度(10)]</span><span class="sxs-lookup"><span data-stu-id="2411e-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="2411e-228">Min</span><span class="sxs-lookup"><span data-stu-id="2411e-228">min</span></span> | <span data-ttu-id="2411e-229">匹配具有最小值的整數。</span><span class="sxs-lookup"><span data-stu-id="2411e-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="2411e-230">{x:min(10)]</span><span class="sxs-lookup"><span data-stu-id="2411e-230">{x:min(10)}</span></span> |
| <span data-ttu-id="2411e-231">最小長度</span><span class="sxs-lookup"><span data-stu-id="2411e-231">minlength</span></span> | <span data-ttu-id="2411e-232">匹配長度最小的字串。</span><span class="sxs-lookup"><span data-stu-id="2411e-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="2411e-233">{x:最小長度(10)]</span><span class="sxs-lookup"><span data-stu-id="2411e-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="2411e-234">range</span><span class="sxs-lookup"><span data-stu-id="2411e-234">range</span></span> | <span data-ttu-id="2411e-235">匹配值範圍內的整數。</span><span class="sxs-lookup"><span data-stu-id="2411e-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="2411e-236">[x:範圍(10,50)]</span><span class="sxs-lookup"><span data-stu-id="2411e-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="2411e-237">RegEx</span><span class="sxs-lookup"><span data-stu-id="2411e-237">regex</span></span> | <span data-ttu-id="2411e-238">匹配正則表達式。</span><span class="sxs-lookup"><span data-stu-id="2411e-238">Matches a regular expression.</span></span> | <span data-ttu-id="2411e-239">{x:regex(\d{3}-d{3}-\d{4}$)]</span><span class="sxs-lookup"><span data-stu-id="2411e-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="2411e-240">請注意,某些約束(如&quot;最小&quot;值)在括弧中採用參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="2411e-241">您可以將多個約束應用於參數,由冒號分隔。</span><span class="sxs-lookup"><span data-stu-id="2411e-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="2411e-242">自訂路由限制式</span><span class="sxs-lookup"><span data-stu-id="2411e-242">Custom Route Constraints</span></span>

<span data-ttu-id="2411e-243">您可以通過實現**IHTTPRoute 約束**介面來創建自訂路由約束。</span><span class="sxs-lookup"><span data-stu-id="2411e-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="2411e-244">例如,以下約束將參數限制為非零整數值。</span><span class="sxs-lookup"><span data-stu-id="2411e-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="2411e-245">以下代碼展示如何註冊約束:</span><span class="sxs-lookup"><span data-stu-id="2411e-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="2411e-246">現在,您可以在路由中應用約束:</span><span class="sxs-lookup"><span data-stu-id="2411e-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="2411e-247">您還可以通過實現**IInline 約束解析器**介面來替換整個**預設內聯約束解析器**類。</span><span class="sxs-lookup"><span data-stu-id="2411e-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="2411e-248">這樣做將替換所有內置約束,除非您的**IInline 約束解析器**的實現專門添加它們。</span><span class="sxs-lookup"><span data-stu-id="2411e-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="2411e-249">選擇的 URI 參數與預設值</span><span class="sxs-lookup"><span data-stu-id="2411e-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="2411e-250">您可以通過向路由參數添加問號來使 URI 參數成為可選參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="2411e-251">如果路由參數是可選的,則必須為方法參數定義預設值。</span><span class="sxs-lookup"><span data-stu-id="2411e-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="2411e-252">在此範例中,`/api/books/locale/1033``/api/books/locale`並傳回相同的資源。</span><span class="sxs-lookup"><span data-stu-id="2411e-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="2411e-253">或者,您可以在工藝路線範本中指定預設值,如下所示:</span><span class="sxs-lookup"><span data-stu-id="2411e-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="2411e-254">這幾乎與前一個示例相同,但在應用預設值時,行為有細微差異。</span><span class="sxs-lookup"><span data-stu-id="2411e-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="2411e-255">在第一個示例("{lcid:int?}")中,默認值 1033 直接分配給方法參數,因此參數將具有此精確值。</span><span class="sxs-lookup"><span data-stu-id="2411e-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="2411e-256">在第二個示例("{lcid:int=1033})中,"1033"的默認值通過模型綁定過程。</span><span class="sxs-lookup"><span data-stu-id="2411e-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="2411e-257">預設模型綁定器將「1033」轉換為數值 1033。</span><span class="sxs-lookup"><span data-stu-id="2411e-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="2411e-258">但是,您可以插入自定義模型活頁夾,這可能執行不同操作。</span><span class="sxs-lookup"><span data-stu-id="2411e-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="2411e-259">(在大多數情況下,除非您管道中有自定義模型綁定器,否則這兩個窗體將等效。</span><span class="sxs-lookup"><span data-stu-id="2411e-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="2411e-260">路由名稱</span><span class="sxs-lookup"><span data-stu-id="2411e-260">Route Names</span></span>

<span data-ttu-id="2411e-261">在 Web API 中,每個路由都有一個名稱。</span><span class="sxs-lookup"><span data-stu-id="2411e-261">In Web API, every route has a name.</span></span> <span data-ttu-id="2411e-262">路由名稱可用於生成連結,因此您可以在 HTTP 回應中包含連結。</span><span class="sxs-lookup"><span data-stu-id="2411e-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="2411e-263">要指定路由名稱,請在屬性上設定**Name**屬性。</span><span class="sxs-lookup"><span data-stu-id="2411e-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="2411e-264">下面的範例示範如何設置路由名稱,以及生成連結時如何使用路由名稱。</span><span class="sxs-lookup"><span data-stu-id="2411e-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="2411e-265">路線訂單</span><span class="sxs-lookup"><span data-stu-id="2411e-265">Route Order</span></span>

<span data-ttu-id="2411e-266">當框架嘗試將URI與路由匹配時,它會按特定順序評估路由。</span><span class="sxs-lookup"><span data-stu-id="2411e-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="2411e-267">要指定訂單,請在工藝路線屬性上設置**Order**屬性。</span><span class="sxs-lookup"><span data-stu-id="2411e-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="2411e-268">首先計算較低的值。</span><span class="sxs-lookup"><span data-stu-id="2411e-268">Lower values are evaluated first.</span></span> <span data-ttu-id="2411e-269">默認訂單值為零。</span><span class="sxs-lookup"><span data-stu-id="2411e-269">The default order value is zero.</span></span>

<span data-ttu-id="2411e-270">以下是確定總排序的方式:</span><span class="sxs-lookup"><span data-stu-id="2411e-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="2411e-271">比較工藝路線屬性的**Order**屬性。</span><span class="sxs-lookup"><span data-stu-id="2411e-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="2411e-272">查看工藝路線範本中的每個 URI 段。</span><span class="sxs-lookup"><span data-stu-id="2411e-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="2411e-273">對於每個段,順序如下:</span><span class="sxs-lookup"><span data-stu-id="2411e-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="2411e-274">欄位。</span><span class="sxs-lookup"><span data-stu-id="2411e-274">Literal segments.</span></span>
    2. <span data-ttu-id="2411e-275">具有約束的路由參數。</span><span class="sxs-lookup"><span data-stu-id="2411e-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="2411e-276">路由參數沒有約束。</span><span class="sxs-lookup"><span data-stu-id="2411e-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="2411e-277">具有約束的通配符參數段。</span><span class="sxs-lookup"><span data-stu-id="2411e-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="2411e-278">通配符參數段沒有約束。</span><span class="sxs-lookup"><span data-stu-id="2411e-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="2411e-279">在連接的情況下,路由由路由範本的區分大小寫序字串比較[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)排序。</span><span class="sxs-lookup"><span data-stu-id="2411e-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="2411e-280">範例如下。</span><span class="sxs-lookup"><span data-stu-id="2411e-280">Here is an example.</span></span> <span data-ttu-id="2411e-281">假設您定義以下控制器:</span><span class="sxs-lookup"><span data-stu-id="2411e-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="2411e-282">這些路線按如下方式排序。</span><span class="sxs-lookup"><span data-stu-id="2411e-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="2411e-283">訂單/詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2411e-283">orders/details</span></span>
2. <span data-ttu-id="2411e-284">訂單/{id}</span><span class="sxs-lookup"><span data-stu-id="2411e-284">orders/{id}</span></span>
3. <span data-ttu-id="2411e-285">訂單/[客戶名稱]</span><span class="sxs-lookup"><span data-stu-id="2411e-285">orders/{customerName}</span></span>
4. <span data-ttu-id="2411e-286">訂單/*\*日期*</span><span class="sxs-lookup"><span data-stu-id="2411e-286">orders/{\*date}</span></span>
5. <span data-ttu-id="2411e-287">訂單/待定</span><span class="sxs-lookup"><span data-stu-id="2411e-287">orders/pending</span></span>

<span data-ttu-id="2411e-288">請注意,"詳細資訊"是文本段,出現在"{id}"之前,但"掛起"顯示最後,因為**Order**屬性為 1。</span><span class="sxs-lookup"><span data-stu-id="2411e-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="2411e-289">(此示例假定沒有名為"詳細資訊"或"掛起"的客戶。</span><span class="sxs-lookup"><span data-stu-id="2411e-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="2411e-290">通常,盡量避免不明確的路線。</span><span class="sxs-lookup"><span data-stu-id="2411e-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="2411e-291">在此示例中,更好的`GetByCustomer`路由範本是"客戶/[客戶名稱]"</span><span class="sxs-lookup"><span data-stu-id="2411e-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
