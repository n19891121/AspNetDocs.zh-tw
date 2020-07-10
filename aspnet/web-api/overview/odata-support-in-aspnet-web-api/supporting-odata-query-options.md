---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: 支援 ASP.NET Web API 2-ASP.NET 4.x 中的 OData 查詢選項
author: MikeWasson
description: 使用程式碼範例的總覽顯示 ASP.NET 4.x 的 ASP.NET Web API 2 中支援的 OData 查詢選項。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188609"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a><span data-ttu-id="00469-103">支援 ASP.NET Web API 2 中的 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-103">Supporting OData Query Options in ASP.NET Web API 2</span></span>

<span data-ttu-id="00469-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="00469-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="00469-105">此總覽與程式碼範例示範 ASP.NET 4.x 的 ASP.NET Web API 2 中支援的 OData 查詢選項。</span><span class="sxs-lookup"><span data-stu-id="00469-105">This overview with code examples demonstrates the supporting OData Query Options in ASP.NET Web API 2 for ASP.NET 4.x.</span></span> 

<span data-ttu-id="00469-106">OData 定義可用於修改 OData 查詢的參數。</span><span class="sxs-lookup"><span data-stu-id="00469-106">OData defines parameters that can be used to modify an OData query.</span></span> <span data-ttu-id="00469-107">用戶端會在要求 URI 的查詢字串中傳送這些參數。</span><span class="sxs-lookup"><span data-stu-id="00469-107">The client sends these parameters in the query string of the request URI.</span></span> <span data-ttu-id="00469-108">例如，若要排序結果，用戶端會使用 $orderby 參數：</span><span class="sxs-lookup"><span data-stu-id="00469-108">For example, to sort the results, a client uses the $orderby parameter:</span></span>

`http://localhost/Products?$orderby=Name`

<span data-ttu-id="00469-109">OData 規格會呼叫這些參數*查詢選項*。</span><span class="sxs-lookup"><span data-stu-id="00469-109">The OData specification calls these parameters *query options*.</span></span> <span data-ttu-id="00469-110">您可以為專案中的任何 Web API 控制器啟用 OData 查詢選項 &#8212; 控制器不需要是 OData 端點。</span><span class="sxs-lookup"><span data-stu-id="00469-110">You can enable OData query options for any Web API controller in your project &#8212; the controller does not need to be an OData endpoint.</span></span> <span data-ttu-id="00469-111">這可讓您輕鬆地在任何 Web API 應用程式中新增功能，例如篩選和排序。</span><span class="sxs-lookup"><span data-stu-id="00469-111">This gives you a convenient way to add features such as filtering and sorting to any Web API application.</span></span>

<span data-ttu-id="00469-112">啟用查詢選項之前，請先閱讀[OData 安全性指引](odata-security-guidance.md)主題。</span><span class="sxs-lookup"><span data-stu-id="00469-112">Before enabling query options, please read the topic [OData Security Guidance](odata-security-guidance.md).</span></span>

- [<span data-ttu-id="00469-113">啟用 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-113">Enabling OData Query Options</span></span>](#enable)
- [<span data-ttu-id="00469-114">範例查詢</span><span class="sxs-lookup"><span data-stu-id="00469-114">Example Queries</span></span>](#examples)
- [<span data-ttu-id="00469-115">伺服器導向的分頁</span><span class="sxs-lookup"><span data-stu-id="00469-115">Server-Driven Paging</span></span>](#server-paging)
- [<span data-ttu-id="00469-116">限制查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-116">Limiting the Query Options</span></span>](#limiting_query_options)
- [<span data-ttu-id="00469-117">直接叫用查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-117">Invoking Query Options Directly</span></span>](#ODataQueryOptions)
- [<span data-ttu-id="00469-118">查詢驗證</span><span class="sxs-lookup"><span data-stu-id="00469-118">Query Validation</span></span>](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a><span data-ttu-id="00469-119">啟用 OData 查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-119">Enabling OData Query Options</span></span>

<span data-ttu-id="00469-120">Web API 支援下列 OData 查詢選項：</span><span class="sxs-lookup"><span data-stu-id="00469-120">Web API supports the following OData query options:</span></span>

| <span data-ttu-id="00469-121">選項</span><span class="sxs-lookup"><span data-stu-id="00469-121">Option</span></span> | <span data-ttu-id="00469-122">描述</span><span class="sxs-lookup"><span data-stu-id="00469-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00469-123">$expand</span><span class="sxs-lookup"><span data-stu-id="00469-123">$expand</span></span> | <span data-ttu-id="00469-124">以內嵌方式展開相關的實體。</span><span class="sxs-lookup"><span data-stu-id="00469-124">Expands related entities inline.</span></span> |
| <span data-ttu-id="00469-125">$filter</span><span class="sxs-lookup"><span data-stu-id="00469-125">$filter</span></span> | <span data-ttu-id="00469-126">根據布林值條件來篩選結果。</span><span class="sxs-lookup"><span data-stu-id="00469-126">Filters the results, based on a Boolean condition.</span></span> |
| <span data-ttu-id="00469-127">$inlinecount</span><span class="sxs-lookup"><span data-stu-id="00469-127">$inlinecount</span></span> | <span data-ttu-id="00469-128">告訴伺服器在回應中包含相符實體的總計數。</span><span class="sxs-lookup"><span data-stu-id="00469-128">Tells the server to include the total count of matching entities in the response.</span></span> <span data-ttu-id="00469-129"> (適用于伺服器端分頁。 ) </span><span class="sxs-lookup"><span data-stu-id="00469-129">(Useful for server-side paging.)</span></span> |
| <span data-ttu-id="00469-130">$orderby</span><span class="sxs-lookup"><span data-stu-id="00469-130">$orderby</span></span> | <span data-ttu-id="00469-131">排序結果。</span><span class="sxs-lookup"><span data-stu-id="00469-131">Sorts the results.</span></span> |
| <span data-ttu-id="00469-132">$select</span><span class="sxs-lookup"><span data-stu-id="00469-132">$select</span></span> | <span data-ttu-id="00469-133">選取要包含在回應中的屬性。</span><span class="sxs-lookup"><span data-stu-id="00469-133">Selects which properties to include in the response.</span></span> |
| <span data-ttu-id="00469-134">$skip</span><span class="sxs-lookup"><span data-stu-id="00469-134">$skip</span></span> | <span data-ttu-id="00469-135">略過前 n 個結果。</span><span class="sxs-lookup"><span data-stu-id="00469-135">Skips the first n results.</span></span> |
| <span data-ttu-id="00469-136">$top</span><span class="sxs-lookup"><span data-stu-id="00469-136">$top</span></span> | <span data-ttu-id="00469-137">只傳回前 n 個結果。</span><span class="sxs-lookup"><span data-stu-id="00469-137">Returns only the first n the results.</span></span> |

<span data-ttu-id="00469-138">若要使用 OData 查詢選項，您必須明確加以啟用。</span><span class="sxs-lookup"><span data-stu-id="00469-138">To use OData query options, you must enable them explicitly.</span></span> <span data-ttu-id="00469-139">您可以針對整個應用程式全域啟用它們，或針對特定控制器或特定動作啟用它們。</span><span class="sxs-lookup"><span data-stu-id="00469-139">You can enable them globally for the entire application, or enable them for specific controllers or specific actions.</span></span>

<span data-ttu-id="00469-140">若要全域啟用 OData 查詢選項，請在啟動時呼叫**HttpConfiguration**類別上的**EnableQuerySupport** ：</span><span class="sxs-lookup"><span data-stu-id="00469-140">To enable OData query options globally, call **EnableQuerySupport** on the **HttpConfiguration** class at startup:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

<span data-ttu-id="00469-141">**EnableQuerySupport**方法會針對傳回**IQueryable**類型的任何控制器動作，全域啟用查詢選項。</span><span class="sxs-lookup"><span data-stu-id="00469-141">The **EnableQuerySupport** method enables query options globally for any controller action that returns an **IQueryable** type.</span></span> <span data-ttu-id="00469-142">如果您不想要針對整個應用程式啟用查詢選項，可以藉由將 **[可查詢]** 屬性新增至動作方法，針對特定的控制器動作啟用它們。</span><span class="sxs-lookup"><span data-stu-id="00469-142">If you don't want query options enabled for the entire application, you can enable them for specific controller actions by adding the **[Queryable]** attribute to the action method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a><span data-ttu-id="00469-143">查詢範例</span><span class="sxs-lookup"><span data-stu-id="00469-143">Example Queries</span></span>

<span data-ttu-id="00469-144">本節顯示使用 OData 查詢選項時可能發生的查詢類型。</span><span class="sxs-lookup"><span data-stu-id="00469-144">This section shows the types of queries that are possible using the OData query options.</span></span> <span data-ttu-id="00469-145">如需查詢選項的特定詳細資料，請參閱 OData 檔，網址為[www.odata.org](http://www.odata.org/)。</span><span class="sxs-lookup"><span data-stu-id="00469-145">For specific details about the query options, refer to the OData documentation at [www.odata.org](http://www.odata.org/).</span></span>

<span data-ttu-id="00469-146">如需 $expand 和 $select 的詳細資訊，請參閱[在 $Value OData 中使用 $select、$expand 和 ASP.NET Web API](using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="00469-146">For information about $expand and $select, see [Using $select, $expand, and $value in ASP.NET Web API OData](using-select-expand-and-value.md).</span></span>

<span data-ttu-id="00469-147">**用戶端導向的分頁**</span><span class="sxs-lookup"><span data-stu-id="00469-147">**Client-Driven Paging**</span></span>

<span data-ttu-id="00469-148">對於大型實體集，用戶端可能會想要限制結果的數目。</span><span class="sxs-lookup"><span data-stu-id="00469-148">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="00469-149">例如，用戶端可能會一次顯示10個專案，其中包含「下一步」連結以取得下一個頁面的結果。</span><span class="sxs-lookup"><span data-stu-id="00469-149">For example, a client might show 10 entries at a time, with "next" links to get the next page of results.</span></span> <span data-ttu-id="00469-150">若要這樣做，用戶端會使用 $top 和 $skip 選項。</span><span class="sxs-lookup"><span data-stu-id="00469-150">To do this, the client uses the $top and $skip options.</span></span>

`http://localhost/Products?$top=10&$skip=20`

<span data-ttu-id="00469-151">[$Top] 選項會提供要傳回的最大專案數，而 [$skip] 選項則會提供要略過的專案數。</span><span class="sxs-lookup"><span data-stu-id="00469-151">The $top option gives the maximum number of entries to return, and the $skip option gives the number of entries to skip.</span></span> <span data-ttu-id="00469-152">上一個範例會提取專案21到30。</span><span class="sxs-lookup"><span data-stu-id="00469-152">The previous example fetches entries 21 through 30.</span></span>

<span data-ttu-id="00469-153">**篩選**</span><span class="sxs-lookup"><span data-stu-id="00469-153">**Filtering**</span></span>

<span data-ttu-id="00469-154">[$Filter] 選項可讓用戶端套用布林運算式來篩選結果。</span><span class="sxs-lookup"><span data-stu-id="00469-154">The $filter option lets a client filter the results by applying a Boolean expression.</span></span> <span data-ttu-id="00469-155">篩選運算式非常強大;其中包括邏輯和算術運算子、字串函數和日期函數。</span><span class="sxs-lookup"><span data-stu-id="00469-155">The filter expressions are quite powerful; they include logical and arithmetic operators, string functions, and date functions.</span></span>

| <span data-ttu-id="00469-156">傳回類別目錄等於「玩具」的所有產品。</span><span class="sxs-lookup"><span data-stu-id="00469-156">Return all products with category equal to "Toys".</span></span> | <span data-ttu-id="00469-157">`http://localhost/Products?$filter=Category`eq ' 玩具 '</span><span class="sxs-lookup"><span data-stu-id="00469-157">`http://localhost/Products?$filter=Category` eq 'Toys'</span></span> |
| --- | --- |
| <span data-ttu-id="00469-158">傳回價格小於10的所有產品。</span><span class="sxs-lookup"><span data-stu-id="00469-158">Return all products with price less than 10.</span></span> | <span data-ttu-id="00469-159">`http://localhost/Products?$filter=Price`lt 10</span><span class="sxs-lookup"><span data-stu-id="00469-159">`http://localhost/Products?$filter=Price` lt 10</span></span> |
| <span data-ttu-id="00469-160">邏輯運算子：傳回價格 >= 5 且價格 <= 15 的所有產品。</span><span class="sxs-lookup"><span data-stu-id="00469-160">Logical operators: Return all products where price >= 5 and price <= 15.</span></span> | <span data-ttu-id="00469-161">`http://localhost/Products?$filter=Price`ge 5 和價格 le 15</span><span class="sxs-lookup"><span data-stu-id="00469-161">`http://localhost/Products?$filter=Price` ge 5 and Price le 15</span></span> |
| <span data-ttu-id="00469-162">字串函數：傳回名稱中有 "zz" 的所有產品。</span><span class="sxs-lookup"><span data-stu-id="00469-162">String functions: Return all products with "zz" in the name.</span></span> | `http://localhost/Products?$filter=substringof('zz',Name)` |
| <span data-ttu-id="00469-163">日期函數：傳回2005之後的所有產品 ReleaseDate。</span><span class="sxs-lookup"><span data-stu-id="00469-163">Date functions: Return all products with ReleaseDate after 2005.</span></span> | <span data-ttu-id="00469-164">`http://localhost/Products?$filter=year(ReleaseDate)`gt 2005</span><span class="sxs-lookup"><span data-stu-id="00469-164">`http://localhost/Products?$filter=year(ReleaseDate)` gt 2005</span></span> |

<span data-ttu-id="00469-165">**排序**</span><span class="sxs-lookup"><span data-stu-id="00469-165">**Sorting**</span></span>

<span data-ttu-id="00469-166">若要排序結果，請使用 [$orderby] 篩選準則。</span><span class="sxs-lookup"><span data-stu-id="00469-166">To sort the results, use the $orderby filter.</span></span>

| <span data-ttu-id="00469-167">依價格排序。</span><span class="sxs-lookup"><span data-stu-id="00469-167">Sort by price.</span></span> | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| <span data-ttu-id="00469-168">依價格以遞減順序排序 (最高到最低) 。</span><span class="sxs-lookup"><span data-stu-id="00469-168">Sort by price in descending order (highest to lowest).</span></span> | `http://localhost/Products?$orderby=Price desc` |
| <span data-ttu-id="00469-169">依分類排序，然後依價格遞減分類內的遞增順序排序。</span><span class="sxs-lookup"><span data-stu-id="00469-169">Sort by category, then sort by price in descending order within categories.</span></span> | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a><span data-ttu-id="00469-170">伺服器導向的分頁</span><span class="sxs-lookup"><span data-stu-id="00469-170">Server-Driven Paging</span></span>

<span data-ttu-id="00469-171">如果您的資料庫包含數百萬筆記錄，您就不會想要在一個承載中全部傳送。</span><span class="sxs-lookup"><span data-stu-id="00469-171">If your database contains millions of records, you don't want to send them all in one payload.</span></span> <span data-ttu-id="00469-172">為了避免這種情況，伺服器可能會限制在單一回應中傳送的專案數。</span><span class="sxs-lookup"><span data-stu-id="00469-172">To prevent this, the server can limit the number of entries that it sends in a single response.</span></span> <span data-ttu-id="00469-173">若要啟用伺服器分頁，請在可**查詢**的屬性中設定**PageSize**屬性。</span><span class="sxs-lookup"><span data-stu-id="00469-173">To enable server paging, set the **PageSize** property in the **Queryable** attribute.</span></span> <span data-ttu-id="00469-174">值是要傳回的最大專案數。</span><span class="sxs-lookup"><span data-stu-id="00469-174">The value is the maximum number of entries to return.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

<span data-ttu-id="00469-175">如果您的控制器傳回 OData 格式，回應主體會包含下一頁數據的連結：</span><span class="sxs-lookup"><span data-stu-id="00469-175">If your controller returns OData format, the response body will contain a link to the next page of data:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

<span data-ttu-id="00469-176">用戶端可以使用此連結來提取下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="00469-176">The client can use this link to fetch the next page.</span></span> <span data-ttu-id="00469-177">若要瞭解結果集中的總專案數，用戶端可以使用 "allpages 提出要求" 值來設定 $inlinecount 查詢選項。</span><span class="sxs-lookup"><span data-stu-id="00469-177">To learn the total number of entries in the result set, the client can set the $inlinecount query option with the value "allpages".</span></span>

`http://localhost/Products?$inlinecount=allpages`

<span data-ttu-id="00469-178">值 "allpages 提出要求" 會告訴伺服器將總計數包含在回應中：</span><span class="sxs-lookup"><span data-stu-id="00469-178">The value "allpages" tells the server to include the total count in the response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> <span data-ttu-id="00469-179">下一個頁面連結和內嵌計數都需要 OData 格式。</span><span class="sxs-lookup"><span data-stu-id="00469-179">Next-page links and inline count both require OData format.</span></span> <span data-ttu-id="00469-180">原因是 OData 會在回應主體中定義特殊欄位，以保存連結和計數。</span><span class="sxs-lookup"><span data-stu-id="00469-180">The reason is that OData defines special fields in the response body to hold the link and count.</span></span>

<span data-ttu-id="00469-181">對於非 OData 格式，仍然可以支援下一頁連結和內嵌計數，方法是將查詢結果包裝在\*\*PageResult &lt; T &gt; \*\*物件中。</span><span class="sxs-lookup"><span data-stu-id="00469-181">For non-OData formats, it is still possible to support next-page links and inline count, by wrapping the query results in a **PageResult&lt;T&gt;** object.</span></span> <span data-ttu-id="00469-182">不過，它需要更多的程式碼。</span><span class="sxs-lookup"><span data-stu-id="00469-182">However, it requires a bit more code.</span></span> <span data-ttu-id="00469-183">範例如下：</span><span class="sxs-lookup"><span data-stu-id="00469-183">Here is an example:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

<span data-ttu-id="00469-184">以下是範例 JSON 回應：</span><span class="sxs-lookup"><span data-stu-id="00469-184">Here is an example JSON response:</span></span>

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a><span data-ttu-id="00469-185">限制查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-185">Limiting the Query Options</span></span>

<span data-ttu-id="00469-186">查詢選項可讓用戶端對在伺服器上執行的查詢有很大的控制權。</span><span class="sxs-lookup"><span data-stu-id="00469-186">The query options give the client a lot of control over the query that is run on the server.</span></span> <span data-ttu-id="00469-187">在某些情況下，您可能會想要基於安全性或效能的考慮，限制可用的選項。</span><span class="sxs-lookup"><span data-stu-id="00469-187">In some cases, you might want to limit the available options for security or performance reasons.</span></span> <span data-ttu-id="00469-188">**[可查詢]** 屬性具有這個的一些內建屬性。</span><span class="sxs-lookup"><span data-stu-id="00469-188">The **[Queryable]** attribute has some built in properties for this.</span></span> <span data-ttu-id="00469-189">以下是一些範例。</span><span class="sxs-lookup"><span data-stu-id="00469-189">Here are some examples.</span></span>

<span data-ttu-id="00469-190">僅允許 $skip 和 $top，以支援分頁和其他任何動作：</span><span class="sxs-lookup"><span data-stu-id="00469-190">Allow only $skip and $top, to support paging and nothing else:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

<span data-ttu-id="00469-191">只允許特定屬性進行排序，以防止對資料庫中未編制索引的屬性進行排序：</span><span class="sxs-lookup"><span data-stu-id="00469-191">Allow ordering only by certain properties, to prevent sorting on properties that are not indexed in the database:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

<span data-ttu-id="00469-192">允許 "eq" 邏輯函式，但沒有其他邏輯函數：</span><span class="sxs-lookup"><span data-stu-id="00469-192">Allow the "eq" logical function but no other logical functions:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

<span data-ttu-id="00469-193">不允許任何算術運算子：</span><span class="sxs-lookup"><span data-stu-id="00469-193">Do not allow any arithmetic operators:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

<span data-ttu-id="00469-194">您可以藉由建立**QueryableAttribute**實例，並將它傳遞至**EnableQuerySupport**函式，來全域限制選項：</span><span class="sxs-lookup"><span data-stu-id="00469-194">You can restrict options globally by constructing a **QueryableAttribute** instance and passing it to the **EnableQuerySupport** function:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a><span data-ttu-id="00469-195">直接叫用查詢選項</span><span class="sxs-lookup"><span data-stu-id="00469-195">Invoking Query Options Directly</span></span>

<span data-ttu-id="00469-196">您可以直接在控制器中叫用查詢選項，而不是使用 **[可查詢]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="00469-196">Instead of using the **[Queryable]** attribute, you can invoke the query options directly in your controller.</span></span> <span data-ttu-id="00469-197">若要這麼做，請將**ODataQueryOptions**參數新增至控制器方法。</span><span class="sxs-lookup"><span data-stu-id="00469-197">To do so, add an **ODataQueryOptions** parameter to the controller method.</span></span> <span data-ttu-id="00469-198">在此情況下，您不需要 **[可查詢]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="00469-198">In this case, you don't need the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

<span data-ttu-id="00469-199">Web API 會從 URI 查詢字串填入**ODataQueryOptions** 。</span><span class="sxs-lookup"><span data-stu-id="00469-199">Web API populates the **ODataQueryOptions** from the URI query string.</span></span> <span data-ttu-id="00469-200">若要套用查詢，請將**IQueryable**傳遞至**ApplyTo**方法。</span><span class="sxs-lookup"><span data-stu-id="00469-200">To apply the query, pass an **IQueryable** to the **ApplyTo** method.</span></span> <span data-ttu-id="00469-201">方法會傳回另一個**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="00469-201">The method returns another **IQueryable**.</span></span>

<span data-ttu-id="00469-202">針對先進的案例，如果您沒有**IQueryable**查詢提供者，您可以檢查**ODataQueryOptions** ，並將查詢選項轉譯成另一個表單。</span><span class="sxs-lookup"><span data-stu-id="00469-202">For advanced scenarios, if you do not have an **IQueryable** query provider, you can examine the **ODataQueryOptions** and translate the query options into another form.</span></span> <span data-ttu-id="00469-203"> (例如，請參閱 RaghuRam Nadiminti 的 blog 文章[將 OData 查詢翻譯為 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中也包含[範例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。 ) </span><span class="sxs-lookup"><span data-stu-id="00469-203">(For example, see RaghuRam Nadiminti's blog post [Translating OData queries to HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx), which also includes a [sample](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt).)</span></span>

<a id="query-validation"></a>
## <a name="query-validation"></a><span data-ttu-id="00469-204">查詢驗證</span><span class="sxs-lookup"><span data-stu-id="00469-204">Query Validation</span></span>

<span data-ttu-id="00469-205">**[可查詢]** 屬性會在執行查詢之前進行驗證。</span><span class="sxs-lookup"><span data-stu-id="00469-205">The **[Queryable]** attribute validates the query before executing it.</span></span> <span data-ttu-id="00469-206">驗證步驟會在**QueryableAttribute. ValidateQuery**方法中執行。</span><span class="sxs-lookup"><span data-stu-id="00469-206">The validation step is performed in the **QueryableAttribute.ValidateQuery** method.</span></span> <span data-ttu-id="00469-207">您也可以自訂驗證程式。</span><span class="sxs-lookup"><span data-stu-id="00469-207">You can also customize the validation process.</span></span>

<span data-ttu-id="00469-208">另請參閱[OData 安全性指引](odata-security-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="00469-208">Also see [OData Security Guidance](odata-security-guidance.md).</span></span>

<span data-ttu-id="00469-209">首先，覆寫在**web.config**命名空間中定義的其中一個驗證程式類別。</span><span class="sxs-lookup"><span data-stu-id="00469-209">First, override one of the validator classes that is defined in the **Web.Http.OData.Query.Validators** namespace.</span></span> <span data-ttu-id="00469-210">例如，下列驗證程式類別會停用 $orderby 選項的 ' desc ' 選項。</span><span class="sxs-lookup"><span data-stu-id="00469-210">For example, the following validator class disables the 'desc' option for the $orderby option.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

<span data-ttu-id="00469-211">子類別化 **[可查詢]** 屬性來覆寫**ValidateQuery**方法。</span><span class="sxs-lookup"><span data-stu-id="00469-211">Subclass the **[Queryable]** attribute to override the **ValidateQuery** method.</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

<span data-ttu-id="00469-212">然後，將您的自訂屬性設定為全域或每個控制器：</span><span class="sxs-lookup"><span data-stu-id="00469-212">Then set your custom attribute either globally or per-controller:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

<span data-ttu-id="00469-213">如果您直接使用**ODataQueryOptions** ，請在選項上設定驗證程式：</span><span class="sxs-lookup"><span data-stu-id="00469-213">If you are using **ODataQueryOptions** directly, set the validator on the options:</span></span>

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
