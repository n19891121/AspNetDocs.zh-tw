---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2 中的路由慣例 Odata-ASP.NET 4.x
author: MikeWasson
description: 在 ASP.NET 4.x OData 端點會使用該 Web API 2 說明路由慣例。
ms.author: riande
ms.date: 07/31/2013
ms.custom: seoapril2019
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 8916f8b7a024636be1be055457081487f46a7936
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421624"
---
# <a name="routing-conventions-in-aspnet-web-api-2-odata"></a><span data-ttu-id="7d5cb-103">ASP.NET Web API 2 中的路由慣例 Odata</span><span class="sxs-lookup"><span data-stu-id="7d5cb-103">Routing Conventions in ASP.NET Web API 2 Odata</span></span>

<span data-ttu-id="7d5cb-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="7d5cb-105">本文章會說明在 ASP.NET 4.x OData 端點會使用該 Web API 2 的路由慣例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-105">This article describes the routing conventions that Web API 2 in ASP.NET 4.x uses for OData endpoints.</span></span>


<span data-ttu-id="7d5cb-106">當 Web API 取得 OData 要求時，它會將要求對應至控制器和動作名稱中。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-106">When Web API gets an OData request, it maps the request to a controller name and an action name.</span></span> <span data-ttu-id="7d5cb-107">對應根據 HTTP 方法和 URI。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-107">The mapping is based on the HTTP method and the URI.</span></span> <span data-ttu-id="7d5cb-108">例如，`GET /odata/Products(1)`對應至`ProductsController.GetProduct`。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-108">For example, `GET /odata/Products(1)` maps to `ProductsController.GetProduct`.</span></span>

<span data-ttu-id="7d5cb-109">在這篇文章的第 1 部分，我說明的內建的 OData 路由慣例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-109">In part 1 of this article, I describe the built-in OData routing conventions.</span></span> <span data-ttu-id="7d5cb-110">這些慣例專為 OData 端點，而且取代預設的 Web API 路由系統。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-110">These conventions are designed specifically for OData endpoints, and they replace the default Web API routing system.</span></span> <span data-ttu-id="7d5cb-111">(您呼叫時會更換**MapODataRoute**。)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-111">(The replacement happens when you call **MapODataRoute**.)</span></span>

<span data-ttu-id="7d5cb-112">在第 2 部分，我會示範如何新增自訂路由慣例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-112">In part 2, I show how to add custom routing conventions.</span></span> <span data-ttu-id="7d5cb-113">目前的內建慣例不會涵蓋整個範圍的 OData Uri，但您可以延伸它們來處理額外情況。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-113">Currently the built-in conventions do not cover the entire range of OData URIs, but you can extend them to handle additional cases.</span></span>

- [<span data-ttu-id="7d5cb-114">內建的路由慣例</span><span class="sxs-lookup"><span data-stu-id="7d5cb-114">Built-in Routing Conventions</span></span>](#conventions)
- [<span data-ttu-id="7d5cb-115">自訂路由慣例</span><span class="sxs-lookup"><span data-stu-id="7d5cb-115">Custom Routing Conventions</span></span>](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a><span data-ttu-id="7d5cb-116">內建的路由慣例</span><span class="sxs-lookup"><span data-stu-id="7d5cb-116">Built-in Routing Conventions</span></span>

<span data-ttu-id="7d5cb-117">我將說明在 Web API 中的 OData 路由慣例之前，最好先了解 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-117">Before I describe the OData routing conventions in Web API, it's helpful to understand OData URIs.</span></span> <span data-ttu-id="7d5cb-118">[OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/)所組成：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-118">An [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) consists of:</span></span>

- <span data-ttu-id="7d5cb-119">服務根目錄</span><span class="sxs-lookup"><span data-stu-id="7d5cb-119">The service root</span></span>
- <span data-ttu-id="7d5cb-120">資源路徑</span><span class="sxs-lookup"><span data-stu-id="7d5cb-120">The resource path</span></span>
- <span data-ttu-id="7d5cb-121">查詢選項</span><span class="sxs-lookup"><span data-stu-id="7d5cb-121">Query options</span></span>

![](odata-routing-conventions/_static/image1.png)

<span data-ttu-id="7d5cb-122">路由，重要的部分是資源路徑。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-122">For routing, the important part is the resource path.</span></span> <span data-ttu-id="7d5cb-123">資源路徑會分成區段。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-123">The resource path is divided into segments.</span></span> <span data-ttu-id="7d5cb-124">比方說，`/Products(1)/Supplier`有三個區段：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-124">For example, `/Products(1)/Supplier` has three segments:</span></span>

- `Products` <span data-ttu-id="7d5cb-125">指的是名為 「 產品 」 實體集。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-125">refers to an entity set named "Products".</span></span>
- `1` <span data-ttu-id="7d5cb-126">是實體索引鍵，從集合中選取單一實體。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-126">is an entity key, selecting a single entity from the set.</span></span>
- `Supplier` <span data-ttu-id="7d5cb-127">已選取 相關的實體的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-127">is a navigation property that selects a related entity.</span></span>

<span data-ttu-id="7d5cb-128">因此這個路徑會挑選出產品 1 的供應商。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-128">So this path picks out the supplier of product 1.</span></span>

> [!NOTE]
> <span data-ttu-id="7d5cb-129">OData 路徑區段未一律對應到 URI 區段。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-129">OData path segments do not always correspond to URI segments.</span></span> <span data-ttu-id="7d5cb-130">例如，"1"會被視為路徑區段。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-130">For example, "1" is considered a path segment.</span></span>


**<span data-ttu-id="7d5cb-131">控制器名稱。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-131">Controller Names.</span></span>** <span data-ttu-id="7d5cb-132">控制器名稱永遠被衍生自實體集資源路徑的根目錄中。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-132">The controller name is always derived from the entity set at the root of the resource path.</span></span> <span data-ttu-id="7d5cb-133">例如，如果資源路徑是`/Products(1)/Supplier`，Web API 會尋找名為控制器`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-133">For example, if the resource path is `/Products(1)/Supplier`, Web API looks for a controller named `ProductsController`.</span></span>

**<span data-ttu-id="7d5cb-134">動作名稱。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-134">Action Names.</span></span>** <span data-ttu-id="7d5cb-135">動作名稱被衍生自的路徑區段，再加上 entity data model (EDM) 中，下列表格所列的。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-135">Action names are derived from the path segments plus the entity data model (EDM), as listed in the following tables.</span></span> <span data-ttu-id="7d5cb-136">在某些情況下，有兩個選項的動作名稱。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-136">In some cases, you have two choices for the action name.</span></span> <span data-ttu-id="7d5cb-137">例如，"Get"或&quot;GetProducts&quot;。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-137">For example, "Get" or &quot;GetProducts&quot;.</span></span>

**<span data-ttu-id="7d5cb-138">查詢實體</span><span class="sxs-lookup"><span data-stu-id="7d5cb-138">Querying Entities</span></span>**

| <span data-ttu-id="7d5cb-139">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-139">Request</span></span> | <span data-ttu-id="7d5cb-140">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-140">Example URI</span></span> | <span data-ttu-id="7d5cb-141">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-141">Action Name</span></span> | <span data-ttu-id="7d5cb-142">範例動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-142">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7d5cb-143">取得 /entityset</span><span class="sxs-lookup"><span data-stu-id="7d5cb-143">GET /entityset</span></span> | <span data-ttu-id="7d5cb-144">/Products</span><span class="sxs-lookup"><span data-stu-id="7d5cb-144">/Products</span></span> | <span data-ttu-id="7d5cb-145">GetEntitySet 或 Get</span><span class="sxs-lookup"><span data-stu-id="7d5cb-145">GetEntitySet or Get</span></span> | <span data-ttu-id="7d5cb-146">GetProducts</span><span class="sxs-lookup"><span data-stu-id="7d5cb-146">GetProducts</span></span> |
| <span data-ttu-id="7d5cb-147">GET /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-147">GET /entityset(key)</span></span> | <span data-ttu-id="7d5cb-148">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-148">/Products(1)</span></span> | <span data-ttu-id="7d5cb-149">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="7d5cb-149">GetEntityType or Get</span></span> | <span data-ttu-id="7d5cb-150">GetProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-150">GetProduct</span></span> |
| <span data-ttu-id="7d5cb-151">GET /entityset(key)/cast</span><span class="sxs-lookup"><span data-stu-id="7d5cb-151">GET /entityset(key)/cast</span></span> | <span data-ttu-id="7d5cb-152">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="7d5cb-152">/Products(1)/Models.Book</span></span> | <span data-ttu-id="7d5cb-153">GetEntityType 或 Get</span><span class="sxs-lookup"><span data-stu-id="7d5cb-153">GetEntityType or Get</span></span> | <span data-ttu-id="7d5cb-154">GetBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-154">GetBook</span></span> |

<span data-ttu-id="7d5cb-155">如需詳細資訊，請參閱 <<c0> [ 建立唯讀的 OData 端點](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-155">For more information, see [Create a Read-Only OData Endpoint](odata-v3/creating-an-odata-endpoint.md).</span></span>

**<span data-ttu-id="7d5cb-156">建立、 更新和刪除實體</span><span class="sxs-lookup"><span data-stu-id="7d5cb-156">Creating, Updating, and Deleting Entities</span></span>**

| <span data-ttu-id="7d5cb-157">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-157">Request</span></span> | <span data-ttu-id="7d5cb-158">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-158">Example URI</span></span> | <span data-ttu-id="7d5cb-159">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-159">Action Name</span></span> | <span data-ttu-id="7d5cb-160">範例動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-160">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7d5cb-161">張貼 /entityset</span><span class="sxs-lookup"><span data-stu-id="7d5cb-161">POST /entityset</span></span> | <span data-ttu-id="7d5cb-162">/Products</span><span class="sxs-lookup"><span data-stu-id="7d5cb-162">/Products</span></span> | <span data-ttu-id="7d5cb-163">PostEntityType 或 Post</span><span class="sxs-lookup"><span data-stu-id="7d5cb-163">PostEntityType or Post</span></span> | <span data-ttu-id="7d5cb-164">PostProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-164">PostProduct</span></span> |
| <span data-ttu-id="7d5cb-165">PUT /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-165">PUT /entityset(key)</span></span> | <span data-ttu-id="7d5cb-166">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-166">/Products(1)</span></span> | <span data-ttu-id="7d5cb-167">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="7d5cb-167">PutEntityType or Put</span></span> | <span data-ttu-id="7d5cb-168">PutProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-168">PutProduct</span></span> |
| <span data-ttu-id="7d5cb-169">PUT /entityset （索引鍵）/轉換</span><span class="sxs-lookup"><span data-stu-id="7d5cb-169">PUT /entityset(key)/cast</span></span> | <span data-ttu-id="7d5cb-170">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="7d5cb-170">/Products(1)/Models.Book</span></span> | <span data-ttu-id="7d5cb-171">PutEntityType 或 Put</span><span class="sxs-lookup"><span data-stu-id="7d5cb-171">PutEntityType or Put</span></span> | <span data-ttu-id="7d5cb-172">PutBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-172">PutBook</span></span> |
| <span data-ttu-id="7d5cb-173">修補程式 /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-173">PATCH /entityset(key)</span></span> | <span data-ttu-id="7d5cb-174">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-174">/Products(1)</span></span> | <span data-ttu-id="7d5cb-175">PatchEntityType 或修補程式</span><span class="sxs-lookup"><span data-stu-id="7d5cb-175">PatchEntityType or Patch</span></span> | <span data-ttu-id="7d5cb-176">PatchProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-176">PatchProduct</span></span> |
| <span data-ttu-id="7d5cb-177">PATCH /entityset(key)/cast</span><span class="sxs-lookup"><span data-stu-id="7d5cb-177">PATCH /entityset(key)/cast</span></span> | <span data-ttu-id="7d5cb-178">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="7d5cb-178">/Products(1)/Models.Book</span></span> | <span data-ttu-id="7d5cb-179">PatchEntityType 或修補程式</span><span class="sxs-lookup"><span data-stu-id="7d5cb-179">PatchEntityType or Patch</span></span> | <span data-ttu-id="7d5cb-180">PatchBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-180">PatchBook</span></span> |
| <span data-ttu-id="7d5cb-181">DELETE /entityset(key)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-181">DELETE /entityset(key)</span></span> | <span data-ttu-id="7d5cb-182">/Products(1)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-182">/Products(1)</span></span> | <span data-ttu-id="7d5cb-183">DeleteEntityType 或 Delete</span><span class="sxs-lookup"><span data-stu-id="7d5cb-183">DeleteEntityType or Delete</span></span> | <span data-ttu-id="7d5cb-184">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-184">DeleteProduct</span></span> |
| <span data-ttu-id="7d5cb-185">DELETE /entityset(key)/cast</span><span class="sxs-lookup"><span data-stu-id="7d5cb-185">DELETE /entityset(key)/cast</span></span> | <span data-ttu-id="7d5cb-186">/Products(1)/Models.Book</span><span class="sxs-lookup"><span data-stu-id="7d5cb-186">/Products(1)/Models.Book</span></span> | <span data-ttu-id="7d5cb-187">DeleteEntityType 或 Delete</span><span class="sxs-lookup"><span data-stu-id="7d5cb-187">DeleteEntityType or Delete</span></span> | <span data-ttu-id="7d5cb-188">DeleteBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-188">DeleteBook</span></span> |

**<span data-ttu-id="7d5cb-189">查詢的導覽屬性</span><span class="sxs-lookup"><span data-stu-id="7d5cb-189">Querying a Navigation Property</span></span>**

| <span data-ttu-id="7d5cb-190">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-190">Request</span></span> | <span data-ttu-id="7d5cb-191">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-191">Example URI</span></span> | <span data-ttu-id="7d5cb-192">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-192">Action Name</span></span> | <span data-ttu-id="7d5cb-193">範例動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-193">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7d5cb-194">GET /entityset(key)/navigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-194">GET /entityset(key)/navigation</span></span> | <span data-ttu-id="7d5cb-195">/Products(1)/Supplier</span><span class="sxs-lookup"><span data-stu-id="7d5cb-195">/Products(1)/Supplier</span></span> | <span data-ttu-id="7d5cb-196">GetNavigationFromEntityType 或 GetNavigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-196">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="7d5cb-197">GetSupplierFromProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-197">GetSupplierFromProduct</span></span> |
| <span data-ttu-id="7d5cb-198">GET /entityset(key)/cast/navigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-198">GET /entityset(key)/cast/navigation</span></span> | <span data-ttu-id="7d5cb-199">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="7d5cb-199">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="7d5cb-200">GetNavigationFromEntityType 或 GetNavigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-200">GetNavigationFromEntityType or GetNavigation</span></span> | <span data-ttu-id="7d5cb-201">GetAuthorFromBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-201">GetAuthorFromBook</span></span> |

<span data-ttu-id="7d5cb-202">如需詳細資訊，請參閱 <<c0> [ 使用實體關係](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-202">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

**<span data-ttu-id="7d5cb-203">建立和刪除連結</span><span class="sxs-lookup"><span data-stu-id="7d5cb-203">Creating and Deleting Links</span></span>**

| <span data-ttu-id="7d5cb-204">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-204">Request</span></span> | <span data-ttu-id="7d5cb-205">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-205">Example URI</span></span> | <span data-ttu-id="7d5cb-206">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-206">Action Name</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d5cb-207">POST /entityset(key)/$links/navigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-207">POST /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="7d5cb-208">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="7d5cb-208">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="7d5cb-209">CreateLink</span><span class="sxs-lookup"><span data-stu-id="7d5cb-209">CreateLink</span></span> |
| <span data-ttu-id="7d5cb-210">PUT 的 /entityset （索引鍵） / $links/瀏覽</span><span class="sxs-lookup"><span data-stu-id="7d5cb-210">PUT /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="7d5cb-211">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="7d5cb-211">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="7d5cb-212">CreateLink</span><span class="sxs-lookup"><span data-stu-id="7d5cb-212">CreateLink</span></span> |
| <span data-ttu-id="7d5cb-213">DELETE /entityset(key)/$links/navigation</span><span class="sxs-lookup"><span data-stu-id="7d5cb-213">DELETE /entityset(key)/$links/navigation</span></span> | <span data-ttu-id="7d5cb-214">/Products(1)/$links/Supplier</span><span class="sxs-lookup"><span data-stu-id="7d5cb-214">/Products(1)/$links/Supplier</span></span> | <span data-ttu-id="7d5cb-215">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="7d5cb-215">DeleteLink</span></span> |
| <span data-ttu-id="7d5cb-216">DELETE /entityset(key)/$links/navigation(relatedKey)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-216">DELETE /entityset(key)/$links/navigation(relatedKey)</span></span> | <span data-ttu-id="7d5cb-217">/Products/(1)/$links/Suppliers(1)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-217">/Products/(1)/$links/Suppliers(1)</span></span> | <span data-ttu-id="7d5cb-218">DeleteLink</span><span class="sxs-lookup"><span data-stu-id="7d5cb-218">DeleteLink</span></span> |

<span data-ttu-id="7d5cb-219">如需詳細資訊，請參閱 <<c0> [ 使用實體關係](odata-v3/working-with-entity-relations.md)。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-219">For more information, see [Working with Entity Relations](odata-v3/working-with-entity-relations.md).</span></span>

**<span data-ttu-id="7d5cb-220">屬性</span><span class="sxs-lookup"><span data-stu-id="7d5cb-220">Properties</span></span>**

*<span data-ttu-id="7d5cb-221">需要 Web API 2</span><span class="sxs-lookup"><span data-stu-id="7d5cb-221">Requires Web API 2</span></span>*

| <span data-ttu-id="7d5cb-222">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-222">Request</span></span> | <span data-ttu-id="7d5cb-223">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-223">Example URI</span></span> | <span data-ttu-id="7d5cb-224">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-224">Action Name</span></span> | <span data-ttu-id="7d5cb-225">範例動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-225">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7d5cb-226">GET /entityset(key)/property</span><span class="sxs-lookup"><span data-stu-id="7d5cb-226">GET /entityset(key)/property</span></span> | <span data-ttu-id="7d5cb-227">/Products(1)/Name</span><span class="sxs-lookup"><span data-stu-id="7d5cb-227">/Products(1)/Name</span></span> | <span data-ttu-id="7d5cb-228">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="7d5cb-228">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="7d5cb-229">GetNameFromProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-229">GetNameFromProduct</span></span> |
| <span data-ttu-id="7d5cb-230">GET /entityset(key)/cast/property</span><span class="sxs-lookup"><span data-stu-id="7d5cb-230">GET /entityset(key)/cast/property</span></span> | <span data-ttu-id="7d5cb-231">/Products(1)/Models.Book/Author</span><span class="sxs-lookup"><span data-stu-id="7d5cb-231">/Products(1)/Models.Book/Author</span></span> | <span data-ttu-id="7d5cb-232">GetPropertyFromEntityType 或 GetProperty</span><span class="sxs-lookup"><span data-stu-id="7d5cb-232">GetPropertyFromEntityType or GetProperty</span></span> | <span data-ttu-id="7d5cb-233">GetTitleFromBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-233">GetTitleFromBook</span></span> |

**<span data-ttu-id="7d5cb-234">動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-234">Actions</span></span>**

| <span data-ttu-id="7d5cb-235">要求</span><span class="sxs-lookup"><span data-stu-id="7d5cb-235">Request</span></span> | <span data-ttu-id="7d5cb-236">範例 URI</span><span class="sxs-lookup"><span data-stu-id="7d5cb-236">Example URI</span></span> | <span data-ttu-id="7d5cb-237">動作名稱</span><span class="sxs-lookup"><span data-stu-id="7d5cb-237">Action Name</span></span> | <span data-ttu-id="7d5cb-238">範例動作</span><span class="sxs-lookup"><span data-stu-id="7d5cb-238">Example Action</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7d5cb-239">POST /entityset(key)/action</span><span class="sxs-lookup"><span data-stu-id="7d5cb-239">POST /entityset(key)/action</span></span> | <span data-ttu-id="7d5cb-240">/Products(1)/Rate</span><span class="sxs-lookup"><span data-stu-id="7d5cb-240">/Products(1)/Rate</span></span> | <span data-ttu-id="7d5cb-241">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="7d5cb-241">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="7d5cb-242">RateOnProduct</span><span class="sxs-lookup"><span data-stu-id="7d5cb-242">RateOnProduct</span></span> |
| <span data-ttu-id="7d5cb-243">POST /entityset(key)/cast/action</span><span class="sxs-lookup"><span data-stu-id="7d5cb-243">POST /entityset(key)/cast/action</span></span> | <span data-ttu-id="7d5cb-244">/Products(1)/Models.Book/CheckOut</span><span class="sxs-lookup"><span data-stu-id="7d5cb-244">/Products(1)/Models.Book/CheckOut</span></span> | <span data-ttu-id="7d5cb-245">ActionNameOnEntityType 或 ActionName</span><span class="sxs-lookup"><span data-stu-id="7d5cb-245">ActionNameOnEntityType or ActionName</span></span> | <span data-ttu-id="7d5cb-246">CheckOutOnBook</span><span class="sxs-lookup"><span data-stu-id="7d5cb-246">CheckOutOnBook</span></span> |

<span data-ttu-id="7d5cb-247">如需詳細資訊，請參閱 < [OData 動作](odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-247">For more information, see [OData Actions](odata-v3/odata-actions.md).</span></span>

**<span data-ttu-id="7d5cb-248">方法簽章</span><span class="sxs-lookup"><span data-stu-id="7d5cb-248">Method Signatures</span></span>**

<span data-ttu-id="7d5cb-249">以下是一些方法簽章的規則：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-249">Here are some rules for the method signatures:</span></span>

- <span data-ttu-id="7d5cb-250">如果路徑包含索引鍵，動作應該有一個名為參數*金鑰*。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-250">If the path contains a key, the action should have a parameter named *key*.</span></span>
- <span data-ttu-id="7d5cb-251">如果路徑包含索引鍵轉換為導覽屬性，動作應該有一個名為參數*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-251">If the path contains a key into a navigation property, the action should have a parameter named *relatedKey*.</span></span>
- <span data-ttu-id="7d5cb-252">裝飾*金鑰*並*relatedKey*參數搭配 **[FromODataUri]** 參數。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-252">Decorate *key* and *relatedKey* parameters with the **[FromODataUri]** parameter.</span></span>
- <span data-ttu-id="7d5cb-253">POST 和 PUT 要求需要一個實體型別的參數。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-253">POST and PUT requests take a parameter of the entity type.</span></span>
- <span data-ttu-id="7d5cb-254">PATCH 要求採用參數的型別**差異&lt;T&gt;**，其中*T*是實體類型。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-254">PATCH requests take a parameter of type **Delta&lt;T&gt;**, where *T* is the entity type.</span></span>

<span data-ttu-id="7d5cb-255">如需參考，以下是範例，並顯示每個內建的 OData 路由慣例的方法簽章。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-255">For reference, here is an example that shows method signatures for every built-in OData routing convention.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a><span data-ttu-id="7d5cb-256">自訂路由慣例</span><span class="sxs-lookup"><span data-stu-id="7d5cb-256">Custom Routing Conventions</span></span>

<span data-ttu-id="7d5cb-257">目前的內建慣例並未涵蓋所有可能的 OData Uri。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-257">Currently the built-in conventions do not cover all possible OData URIs.</span></span> <span data-ttu-id="7d5cb-258">您可以藉由實作加入新的慣例**IODataRoutingConvention**介面。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-258">You can add new conventions by implementing the **IODataRoutingConvention** interface.</span></span> <span data-ttu-id="7d5cb-259">此介面有兩種方法：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-259">This interface has two methods:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- <span data-ttu-id="7d5cb-260">**SelectController**傳回控制器的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-260">**SelectController** returns the name of the controller.</span></span>
- <span data-ttu-id="7d5cb-261">**SelectAction**傳回動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-261">**SelectAction** returns the name of the action.</span></span>

<span data-ttu-id="7d5cb-262">如需這兩個方法中，如果慣例不適用於該要求，方法應該傳回 null。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-262">For both methods, if the convention does not apply to that request, the method should return null.</span></span>

<span data-ttu-id="7d5cb-263">**ODataPath**參數代表的已剖析的 OData 資源路徑。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-263">The **ODataPath** parameter represents the parsed OData resource path.</span></span> <span data-ttu-id="7d5cb-264">它包含一份**[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 執行個體，其中每個區段的資源路徑。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-264">It contains a list of **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** instances, one for each segment of the resource path.</span></span> <span data-ttu-id="7d5cb-265">**ODataPathSegment**是抽象類別，每個區段的類型由衍生自類別**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-265">**ODataPathSegment** is an abstract class; each segment type is represented by a class that derives from **ODataPathSegment**.</span></span>

<span data-ttu-id="7d5cb-266">**ODataPath.TemplatePath**屬性是字串，表示串連所有路徑區段。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-266">The **ODataPath.TemplatePath** property is a string that represents the concatenation all of the path segments.</span></span> <span data-ttu-id="7d5cb-267">例如，URI 是否`/Products(1)/Supplier`，路徑範本&quot;~/entityset/key/navigation&quot;。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-267">For example, if the URI is `/Products(1)/Supplier`, the path template is &quot;~/entityset/key/navigation&quot;.</span></span> <span data-ttu-id="7d5cb-268">請注意，這些區段不會直接對應至 URI 區段。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-268">Notice that the segments don't correspond directly to URI segments.</span></span> <span data-ttu-id="7d5cb-269">例如，將實體索引鍵 (1) 表示為其自身**ODataPathSegment**。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-269">For example, the entity key (1) is represented as its own **ODataPathSegment**.</span></span>

<span data-ttu-id="7d5cb-270">一般而言，實作**IODataRoutingConvention**會進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-270">Typically, an implementation of **IODataRoutingConvention** does the following:</span></span>

1. <span data-ttu-id="7d5cb-271">比較以查看此慣例套用至目前要求的路徑範本。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-271">Compare the path template to see if this convention applies to the current request.</span></span> <span data-ttu-id="7d5cb-272">如果它不適用，會傳回 null。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-272">If it does not apply, return null.</span></span>
2. <span data-ttu-id="7d5cb-273">慣例會套用，如果使用的屬性**ODataPathSegment**衍生控制器和動作名稱的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-273">If the convention applies, use properties of the **ODataPathSegment** instances to derive controller and action names.</span></span>
3. <span data-ttu-id="7d5cb-274">動作，將新增至路由字典應該繫結至動作參數 （通常是實體索引鍵） 的任何值。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-274">For actions, add any values to the route dictionary that should bind to the action parameters (typically entity keys).</span></span>

<span data-ttu-id="7d5cb-275">讓我們看看一個特定的範例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-275">Let's look at a specific example.</span></span> <span data-ttu-id="7d5cb-276">內建的路由慣例不支援對巡覽集合進行索引。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-276">The built-in routing conventions do not support indexing into a navigation collection.</span></span> <span data-ttu-id="7d5cb-277">換句話說，沒有任何 Uri 慣例如下所示：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-277">In other words, there is no convention for URIs like the following:</span></span>

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

<span data-ttu-id="7d5cb-278">以下是查詢的自訂的路由慣例，來處理這種類型。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-278">Here is a custom routing convention to handle this type of query.</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

<span data-ttu-id="7d5cb-279">附註：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-279">Notes:</span></span>

1. <span data-ttu-id="7d5cb-280">我是衍生自**EntitySetRoutingConvention**，因為**SelectController**該類別中的方法是適用於這個新的路由慣例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-280">I derive from **EntitySetRoutingConvention**, because the **SelectController** method in that class is appropriate for this new routing convention.</span></span> <span data-ttu-id="7d5cb-281">這表示我不需要重新實作**SelectController**。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-281">That means I don't need to re-implement **SelectController**.</span></span>
2. <span data-ttu-id="7d5cb-282">慣例只適用於 GET 要求和路徑範本時，才&quot;~/entityset/key/navigation/key&quot;。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-282">The convention applies only to GET requests, and only when the path template is &quot;~/entityset/key/navigation/key&quot;.</span></span>
3. <span data-ttu-id="7d5cb-283">動作名稱是&quot;取得 {EntityType}&quot;，其中 *{EntityType}* 是瀏覽集合型別。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-283">The action name is &quot;Get{EntityType}&quot;, where *{EntityType}* is the type of the navigation collection.</span></span> <span data-ttu-id="7d5cb-284">例如， &quot;GetSupplier&quot;。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-284">For example, &quot;GetSupplier&quot;.</span></span> <span data-ttu-id="7d5cb-285">您可以使用任何您喜歡的命名慣例&#8212;只要確定您符合對控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-285">You can use any naming convention that you like &#8212; just make sure your controller actions match.</span></span>
4. <span data-ttu-id="7d5cb-286">動作會採用兩個參數，叫做*金鑰*並*relatedKey*。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-286">The action takes two parameters named *key* and *relatedKey*.</span></span> <span data-ttu-id="7d5cb-287">(如需一些預先定義的參數名稱的清單，請參閱 < [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="7d5cb-287">(For a list of some predefined parameter names, see [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)</span></span>

<span data-ttu-id="7d5cb-288">下一個步驟加入新的慣例路由慣例的清單。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-288">The next step is adding the new convention to the list of routing conventions.</span></span> <span data-ttu-id="7d5cb-289">發生這種情況在設定期間，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-289">This happens during configuration, as shown in the following code:</span></span>

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

<span data-ttu-id="7d5cb-290">以下是一些其他範例路由慣例，會有幫助研究：</span><span class="sxs-lookup"><span data-stu-id="7d5cb-290">Here are some other sample routing conventions that be useful to study:</span></span>

- [<span data-ttu-id="7d5cb-291">CompositeKeyRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="7d5cb-291">CompositeKeyRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [<span data-ttu-id="7d5cb-292">CustomNavigationRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="7d5cb-292">CustomNavigationRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [<span data-ttu-id="7d5cb-293">NonBindableActionRoutingConvention</span><span class="sxs-lookup"><span data-stu-id="7d5cb-293">NonBindableActionRoutingConvention</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [<span data-ttu-id="7d5cb-294">ODataVersionRouteConstraint</span><span class="sxs-lookup"><span data-stu-id="7d5cb-294">ODataVersionRouteConstraint</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

<span data-ttu-id="7d5cb-295">和 Web API 本身當然是開放原始碼，因此您所見[原始程式碼](http://aspnetwebstack.codeplex.com/)內建的路由慣例。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-295">And of course Web API itself is open-source, so you can see the [source code](http://aspnetwebstack.codeplex.com/) for the built-in routing conventions.</span></span> <span data-ttu-id="7d5cb-296">這些定義在**System.Web.Http.OData.Routing.Conventions**命名空間。</span><span class="sxs-lookup"><span data-stu-id="7d5cb-296">These are defined in the **System.Web.Http.OData.Routing.Conventions** namespace.</span></span>
