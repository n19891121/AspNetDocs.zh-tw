---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: 支援 OData 查詢選項在 ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: 概觀與程式碼範例顯示 ASP.NET Web API 2 中支援的 OData 查詢選項，asp.net 4.x。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 428e4942e42436585049c1e84cd7b07a4a79c0d1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59411562"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="39a48-103">ASP.NET Web API 2 中支援 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="39a48-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="39a48-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="39a48-105">本概觀的程式碼範例示範支援的 OData 查詢選項，ASP.NET Web API 2 中 asp.net 4.x。</span><span class="sxs-lookup"><span data-stu-id="39a48-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="39a48-106">OData 會定義可用來修改 OData 查詢的參數。</span><span class="sxs-lookup"><span data-stu-id="39a48-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="39a48-107">用戶端在要求 URI 查詢字串中傳送這些參數。</span><span class="sxs-lookup"><span data-stu-id="39a48-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="39a48-108">例如，若要排序的結果，用戶端會使用 $orderby 參數：</span><span class="sxs-lookup"><span data-stu-id="39a48-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="39a48-109">OData 規格會呼叫這些參數*查詢選項*。</span><span class="sxs-lookup"><span data-stu-id="39a48-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="39a48-110">您可以啟用您專案中的任何 Web API 控制器的 OData 查詢選項&#8212;控制器不需要是 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="39a48-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="39a48-111">這會讓您加入功能，例如篩選和排序任何 Web API 應用程式的便利方式。</span><span class="sxs-lookup"><span data-stu-id="39a48-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="39a48-112">啟用查詢選項，請參閱本主題之前[OData 安全性指導](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="39a48-113">啟用 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="39a48-114">範例查詢</span><span class="sxs-lookup"><span data-stu-id="39a48-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="39a48-115">Server-Driven Paging</span><span class="sxs-lookup"><span data-stu-id="39a48-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="39a48-116">限制的查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="39a48-117">直接叫用查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="39a48-118">查詢驗證</span><span class="sxs-lookup"><span data-stu-id="39a48-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="39a48-119">啟用 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-119">Enabling OData Query Options</span></span>

<span data-ttu-id="39a48-120">Web API 支援下列 OData 查詢選項：</span><span class="sxs-lookup"><span data-stu-id="39a48-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="39a48-121">選項</span><span class="sxs-lookup"><span data-stu-id="39a48-121">Option</span></span> | <span data-ttu-id="39a48-122">描述</span><span class="sxs-lookup"><span data-stu-id="39a48-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="39a48-123">$expand</span><span class="sxs-lookup"><span data-stu-id="39a48-123">$expand</span></span> | <span data-ttu-id="39a48-124">展開相關的實體內嵌。</span><span class="sxs-lookup"><span data-stu-id="39a48-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="39a48-125">$filter</span><span class="sxs-lookup"><span data-stu-id="39a48-125">$filter</span></span> | <span data-ttu-id="39a48-126">篩選結果，根據布林條件。</span><span class="sxs-lookup"><span data-stu-id="39a48-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="39a48-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="39a48-127">$inlinecount</span></span> | <span data-ttu-id="39a48-128">告知伺服器應回應中包含的相符實體總計數。</span><span class="sxs-lookup"><span data-stu-id="39a48-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="39a48-129">（適用於伺服器端分頁。）</span><span class="sxs-lookup"><span data-stu-id="39a48-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="39a48-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="39a48-130">$orderby</span></span> | <span data-ttu-id="39a48-131">排序結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-131">Sorts the results.</span></span> |
| <span data-ttu-id="39a48-132">$select</span><span class="sxs-lookup"><span data-stu-id="39a48-132">$select</span></span> | <span data-ttu-id="39a48-133">選取要包含在回應中的屬性。</span><span class="sxs-lookup"><span data-stu-id="39a48-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="39a48-134">$skip</span><span class="sxs-lookup"><span data-stu-id="39a48-134">$skip</span></span> | <span data-ttu-id="39a48-135">略過前 n 個結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-135">Skips the first n results.</span></span> |
| <span data-ttu-id="39a48-136">$top</span><span class="sxs-lookup"><span data-stu-id="39a48-136">$top</span></span> | <span data-ttu-id="39a48-137">傳回前 n 個結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="39a48-138">若要使用的 OData 查詢選項，您必須明確啟用它們。</span><span class="sxs-lookup"><span data-stu-id="39a48-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="39a48-139">您可以全域啟用整個應用程式，或針對特定控制器或特定的動作啟用它們。</span><span class="sxs-lookup"><span data-stu-id="39a48-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="39a48-140">若要全域啟用 OData 查詢選項，請呼叫**EnableQuerySupport**上**HttpConfiguration**在啟動類別：</span><span class="sxs-lookup"><span data-stu-id="39a48-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="39a48-141">**EnableQuerySupport**方法可讓查詢選項，會傳回任何控制器動作的全域**IQueryable**型別。</span><span class="sxs-lookup"><span data-stu-id="39a48-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="39a48-142">如果您不想啟用整個應用程式的查詢選項，您可以讓它們適用於特定的控制器動作加 **[Queryable]** 屬性加入動作方法。</span><span class="sxs-lookup"><span data-stu-id="39a48-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="39a48-143">範例查詢</span><span class="sxs-lookup"><span data-stu-id="39a48-143">Example Queries</span></span>

<span data-ttu-id="39a48-144">本節說明是可能使用的 OData 查詢選項的查詢的類型。</span><span class="sxs-lookup"><span data-stu-id="39a48-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="39a48-145">如特定的查詢選項的詳細資訊，請參閱 OData 文件，網址[www.odata.org](http://www.odata.org/)。</span><span class="sxs-lookup"><span data-stu-id="39a48-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="39a48-146">如需 $展開和 $select，請參閱[使用 $select，$expand、 和 ASP.NET Web API OData 中的 $value](using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="39a48-147">**Client-Driven Paging**</span><span class="sxs-lookup"><span data-stu-id="39a48-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="39a48-148">為大型實體集，用戶端可能會想要限制結果數目。</span><span class="sxs-lookup"><span data-stu-id="39a48-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="39a48-149">例如，用戶端可能會顯示 10 個項目一次 下一步 」 的連結，來取得下一頁的結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="39a48-150">若要這樣做，用戶端會使用 $top] 和 [$skip 選項。</span><span class="sxs-lookup"><span data-stu-id="39a48-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="39a48-151">$Top 選項提供項目，以傳回，最大數目，以及 $skip 選項以略過的項目數。</span><span class="sxs-lookup"><span data-stu-id="39a48-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="39a48-152">前一個範例會擷取項目 21 到 30。</span><span class="sxs-lookup"><span data-stu-id="39a48-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="39a48-153">**篩選**</span><span class="sxs-lookup"><span data-stu-id="39a48-153">**Filtering**</span></span>

<span data-ttu-id="39a48-154">$Filter 選項可讓用戶端所套用的布林運算式篩選結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="39a48-155">篩選條件運算式是相當強大;其中包括邏輯和算術運算子、 字串函數，以及日期函式。</span><span class="sxs-lookup"><span data-stu-id="39a48-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="39a48-156">會傳回等於 「 玩具 」 類別的所有產品。</span><span class="sxs-lookup"><span data-stu-id="39a48-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="39a48-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span><span class="sxs-lookup"><span data-stu-id="39a48-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="39a48-158">會傳回標價小於 10 的所有產品。</span><span class="sxs-lookup"><span data-stu-id="39a48-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="39a48-159">`http://localhost/Products?$filter=Price` l 10</span><span class="sxs-lookup"><span data-stu-id="39a48-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="39a48-160">邏輯運算子：傳回所有產品，價格 > = 5 且價格 < = 15。</span><span class="sxs-lookup"><span data-stu-id="39a48-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="39a48-161">`http://localhost/Products?$filter=Price` ge 5 和價格 le 15</span><span class="sxs-lookup"><span data-stu-id="39a48-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="39a48-162">字串函數：傳回與"zz"的所有產品名稱中。</span><span class="sxs-lookup"><span data-stu-id="39a48-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="39a48-163">日期函數：傳回所有產品 ReleaseDate 2005 之後。</span><span class="sxs-lookup"><span data-stu-id="39a48-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="39a48-164">`http://localhost/Products?$filter=year(ReleaseDate)` t 2005</span><span class="sxs-lookup"><span data-stu-id="39a48-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="39a48-165">**排序**</span><span class="sxs-lookup"><span data-stu-id="39a48-165">**Sorting**</span></span>

<span data-ttu-id="39a48-166">若要排序的結果，請使用 $orderby 篩選。</span><span class="sxs-lookup"><span data-stu-id="39a48-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="39a48-167">價格依排序。</span><span class="sxs-lookup"><span data-stu-id="39a48-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="39a48-168">排序依據以遞減順序 （最高到最低） 的價格。</span><span class="sxs-lookup"><span data-stu-id="39a48-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="39a48-169">依類別排序，然後依價格遞減類別內的順序排序。</span><span class="sxs-lookup"><span data-stu-id="39a48-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="39a48-170">伺服器驅動型分頁</span><span class="sxs-lookup"><span data-stu-id="39a48-170">Server-Driven Paging</span></span>

<span data-ttu-id="39a48-171">如果您的資料庫包含數百萬筆記錄，您不想傳送這些全都放在一個裝載。</span><span class="sxs-lookup"><span data-stu-id="39a48-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="39a48-172">若要避免這個問題，伺服器可以限制單一回應中傳送的項目數。</span><span class="sxs-lookup"><span data-stu-id="39a48-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="39a48-173">若要啟用伺服器分頁，將**PageSize**中的屬性**Queryable**屬性。</span><span class="sxs-lookup"><span data-stu-id="39a48-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="39a48-174">值是要傳回的項目數目上限。</span><span class="sxs-lookup"><span data-stu-id="39a48-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="39a48-175">如果您的控制器傳回 OData 格式時，回應主體會包含下一頁資料的連結：</span><span class="sxs-lookup"><span data-stu-id="39a48-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="39a48-176">用戶端可以使用此連結，以擷取下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="39a48-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="39a48-177">若要了解結果集中的項目總數，用戶端可以設定 $inlinecount 查詢選項的值"allpages 」。</span><span class="sxs-lookup"><span data-stu-id="39a48-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="39a48-178">值"allpages 」 會要求伺服器在回應中包含的總數：</span><span class="sxs-lookup"><span data-stu-id="39a48-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="39a48-179">下一頁連結和內嵌計數都需要 OData 格式。</span><span class="sxs-lookup"><span data-stu-id="39a48-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="39a48-180">原因是，OData 會定義特殊欄位來保存的連結和計數的回應主體中。</span><span class="sxs-lookup"><span data-stu-id="39a48-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>


<span data-ttu-id="39a48-181">對於非 OData 格式，就仍然可以支援藉由包裝的查詢結果中的下一頁連結和內嵌計數**PageResult&lt;T&gt;** 物件。</span><span class="sxs-lookup"><span data-stu-id="39a48-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="39a48-182">不過，它需要更多的程式碼。</span><span class="sxs-lookup"><span data-stu-id="39a48-182">However, it requires a bit more code.</span></span> <span data-ttu-id="39a48-183">請看以下範例：</span><span class="sxs-lookup"><span data-stu-id="39a48-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="39a48-184">以下是範例 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="39a48-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="39a48-185">限制的查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-185">Limiting the Query Options</span></span>

<span data-ttu-id="39a48-186">查詢選項會導致在用戶端控制伺服器執行的查詢很多。</span><span class="sxs-lookup"><span data-stu-id="39a48-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="39a48-187">在某些情況下，您可能想要限制可用的選項，基於安全性或效能的考量。</span><span class="sxs-lookup"><span data-stu-id="39a48-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="39a48-188">**[Queryable]** 屬性有部分內建屬性的。</span><span class="sxs-lookup"><span data-stu-id="39a48-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="39a48-189">以下是一些範例。</span><span class="sxs-lookup"><span data-stu-id="39a48-189">Here are some examples.</span></span>

<span data-ttu-id="39a48-190">僅允許 $skip 和 $top，以支援分頁並沒有其他項目：</span><span class="sxs-lookup"><span data-stu-id="39a48-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="39a48-191">若要避免在資料庫中建立索引的屬性上的排序順序只能由特定的屬性，可讓：</span><span class="sxs-lookup"><span data-stu-id="39a48-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="39a48-192">允許"eq"的邏輯函式，但沒有其他的邏輯函數：</span><span class="sxs-lookup"><span data-stu-id="39a48-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="39a48-193">不允許任何的算術運算子：</span><span class="sxs-lookup"><span data-stu-id="39a48-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="39a48-194">您可以藉由建構，全域限制選項**QueryableAttribute**執行個體，並將其傳遞給**EnableQuerySupport**函式：</span><span class="sxs-lookup"><span data-stu-id="39a48-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="39a48-195">直接叫用查詢選項</span><span class="sxs-lookup"><span data-stu-id="39a48-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="39a48-196">而不是使用 **[Queryable]** 屬性，您可以直接在您的控制器中叫用的查詢選項。</span><span class="sxs-lookup"><span data-stu-id="39a48-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="39a48-197">若要這樣做，請新增**ODataQueryOptions**控制器方法的參數。</span><span class="sxs-lookup"><span data-stu-id="39a48-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="39a48-198">在此情況下，您不需要 **[Queryable]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="39a48-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="39a48-199">Web API 會填入**ODataQueryOptions**從 URI 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="39a48-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="39a48-200">若要套用查詢，請傳遞**IQueryable**要**ApplyTo**方法。</span><span class="sxs-lookup"><span data-stu-id="39a48-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="39a48-201">此方法會傳回另一個**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="39a48-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="39a48-202">對於進階案例，如果您不需要**IQueryable**查詢提供者，您可以檢查**ODataQueryOptions**並轉譯成另一種形式的查詢選項。</span><span class="sxs-lookup"><span data-stu-id="39a48-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="39a48-203">(例如，請參閱 RaghuRam Nadiminti 部落格文章[轉譯的 OData 查詢，為 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中也包括[範例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。)</span><span class="sxs-lookup"><span data-stu-id="39a48-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="39a48-204">查詢驗證</span><span class="sxs-lookup"><span data-stu-id="39a48-204">Query Validation</span></span>

<span data-ttu-id="39a48-205">**[Queryable]** 屬性驗證的查詢，然後再執行它。</span><span class="sxs-lookup"><span data-stu-id="39a48-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="39a48-206">驗證步驟在中執行**QueryableAttribute.ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="39a48-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="39a48-207">您也可以自訂驗證程序。</span><span class="sxs-lookup"><span data-stu-id="39a48-207">You can also customize the validation process.</span></span>

<span data-ttu-id="39a48-208">另請參閱[OData 安全性指導](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="39a48-209">覆寫其中一個驗證程式也就是類別定義中的第一次， **Web.Http.OData.Query.Validators**命名空間。</span><span class="sxs-lookup"><span data-stu-id="39a48-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="39a48-210">例如，下列的驗證程式類別會停用 $orderby 選項的 'desc' 選項。</span><span class="sxs-lookup"><span data-stu-id="39a48-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="39a48-211">子類別 **[Queryable]** 屬性來覆寫**ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="39a48-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="39a48-212">然後設定您的自訂屬性是全域或每個控制站：</span><span class="sxs-lookup"><span data-stu-id="39a48-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="39a48-213">如果您使用**ODataQueryOptions**直接設定選項中的 驗證程式：</span><span class="sxs-lookup"><span data-stu-id="39a48-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
