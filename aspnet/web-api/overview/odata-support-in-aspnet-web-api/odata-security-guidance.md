---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Security Guidance for ASP.NET Web API 2 OData-ASP.NET 4.x
author: MikeWasson
description: 說明在 ASP.NET 上的 ASP.NET Web API 2 中公開透過 OData 資料集時要考量的安全性問題 4.x。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59393505"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a><span data-ttu-id="590b5-103">Security Guidance for ASP.NET Web API 2 OData</span><span class="sxs-lookup"><span data-stu-id="590b5-103">Security Guidance for ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="590b5-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="590b5-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="590b5-105">本主題描述一些您應該考慮在 ASP.NET 上的 ASP.NET Web API 2 中公開透過 OData 資料集時的安全性問題 4.x。</span><span class="sxs-lookup"><span data-stu-id="590b5-105">This topic describes some of the security issues that you should consider when exposing a dataset through OData for ASP.NET Web API 2 on ASP.NET 4.x.</span></span>

## <a name="edm-security"></a><span data-ttu-id="590b5-106">EDM 安全性</span><span class="sxs-lookup"><span data-stu-id="590b5-106">EDM Security</span></span>

<span data-ttu-id="590b5-107">查詢語意根據 entity data model (EDM) 中，不基礎的模型型別。</span><span class="sxs-lookup"><span data-stu-id="590b5-107">The query semantics are based on the entity data model (EDM), not the underlying model types.</span></span> <span data-ttu-id="590b5-108">您可以排除 EDM 中的屬性，將不會顯示查詢。</span><span class="sxs-lookup"><span data-stu-id="590b5-108">You can exclude a property from the EDM and it will not be visible to the query.</span></span> <span data-ttu-id="590b5-109">例如，假設您的模型包含員工具有的型別薪資屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-109">For example, suppose your model includes an Employee type with a Salary property.</span></span> <span data-ttu-id="590b5-110">您可能想要隱藏來自用戶端在 EDM 中排除此屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-110">You might want to exclude this property from the EDM to hide it from clients.</span></span>

<span data-ttu-id="590b5-111">有兩種方式可以排除在 EDM 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-111">There are two ways to exclude a property from the EDM.</span></span> <span data-ttu-id="590b5-112">您可以設定 **[IgnoreDataMember]** 模型類別中的屬性上的屬性：</span><span class="sxs-lookup"><span data-stu-id="590b5-112">You can set the **[IgnoreDataMember]** attribute on the property in the model class:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

<span data-ttu-id="590b5-113">您也可以移除該屬性在 EDM 中以程式設計的方式：</span><span class="sxs-lookup"><span data-stu-id="590b5-113">You can also remove the property from the EDM programmatically:</span></span>

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a><span data-ttu-id="590b5-114">查詢安全性</span><span class="sxs-lookup"><span data-stu-id="590b5-114">Query Security</span></span>

<span data-ttu-id="590b5-115">惡意或單純的用戶端可以建構花很長的時間執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="590b5-115">A malicious or naive client may be able to construct a query that takes a very long time to execute.</span></span> <span data-ttu-id="590b5-116">最糟的情況中，這可能會中斷服務的存取。</span><span class="sxs-lookup"><span data-stu-id="590b5-116">In the worst case this can disrupt access to your service.</span></span>

<span data-ttu-id="590b5-117">**[Queryable]** 是動作篩選條件，以剖析、 驗證，並將查詢套用的屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-117">The **[Queryable]** attribute is an action filter that parses, validates, and applies the query.</span></span> <span data-ttu-id="590b5-118">篩選條件會將查詢選項轉換成 LINQ 運算式。</span><span class="sxs-lookup"><span data-stu-id="590b5-118">The filter converts the query options into a LINQ expression.</span></span> <span data-ttu-id="590b5-119">當 OData 控制器會傳回**IQueryable**型別**IQueryable** LINQ 提供者會將 LINQ 運算式轉換成一個查詢。</span><span class="sxs-lookup"><span data-stu-id="590b5-119">When the OData controller returns an **IQueryable** type, the **IQueryable** LINQ provider converts the LINQ expression into a query.</span></span> <span data-ttu-id="590b5-120">因此，效能取決於使用時，LINQ 提供者同時也會在您的資料集或資料庫結構描述的特定特性。</span><span class="sxs-lookup"><span data-stu-id="590b5-120">Therefore, performance depends on the LINQ provider that is used, and also on the particular characteristics of your dataset or database schema.</span></span>

<span data-ttu-id="590b5-121">如需 ASP.NET Web API 中使用 OData 查詢選項的詳細資訊，請參閱 <<c0> [ 支援的 OData 查詢選項](supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="590b5-121">For more information about using OData query options in ASP.NET Web API, see [Supporting OData Query Options](supporting-odata-query-options.md).</span></span>

<span data-ttu-id="590b5-122">如果您知道所有用戶端所信任 （例如，在企業環境中），或您的資料集很小，查詢效能可能不會有問題。</span><span class="sxs-lookup"><span data-stu-id="590b5-122">If you know that all clients are trusted (for example, in an enterprise environment), or if your dataset is small, query performance might not be an issue.</span></span> <span data-ttu-id="590b5-123">否則，您應該考慮下列建議。</span><span class="sxs-lookup"><span data-stu-id="590b5-123">Otherwise, you should consider the following recommendations.</span></span>

- <span data-ttu-id="590b5-124">測試您的服務，使用各種不同的查詢和分析資料庫。</span><span class="sxs-lookup"><span data-stu-id="590b5-124">Test your service with various queries and profile the DB.</span></span>
- <span data-ttu-id="590b5-125">啟用伺服器驅動型分頁，來避免傳回大型資料集在單一查詢中。</span><span class="sxs-lookup"><span data-stu-id="590b5-125">Enable server-driven paging, to avoid returning a large data set in one query.</span></span> <span data-ttu-id="590b5-126">如需詳細資訊，請參閱 < [Server-Driven 分頁](supporting-odata-query-options.md#server-paging)。</span><span class="sxs-lookup"><span data-stu-id="590b5-126">For more information, see [Server-Driven Paging](supporting-odata-query-options.md#server-paging).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- <span data-ttu-id="590b5-127">您需要 $filter 和 $orderby 嗎？</span><span class="sxs-lookup"><span data-stu-id="590b5-127">Do you need $filter and $orderby?</span></span> <span data-ttu-id="590b5-128">有些應用程式可能會允許用戶端分頁、 使用 $top 和 $skip，但停用其他查詢選項。</span><span class="sxs-lookup"><span data-stu-id="590b5-128">Some applications might allow client paging, using $top and $skip, but disable the other query options.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- <span data-ttu-id="590b5-129">請考慮限制 $orderby 叢集索引中的屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-129">Consider restricting $orderby to properties in a clustered index.</span></span> <span data-ttu-id="590b5-130">沒有叢集索引的大型資料的排序速度很慢。</span><span class="sxs-lookup"><span data-stu-id="590b5-130">Sorting large data without a clustered index is slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- <span data-ttu-id="590b5-131">節點計數上限：**MaxNodeCount**屬性上的 **[Queryable]** 設定 $filter 語法樹狀目錄中允許的最大數目節點。</span><span class="sxs-lookup"><span data-stu-id="590b5-131">Maximum node count: The **MaxNodeCount** property on **[Queryable]** sets the maximum number nodes allowed in the $filter syntax tree.</span></span> <span data-ttu-id="590b5-132">預設值是 100，但因為大量節點可能會慢而無法編譯，您可能想要設定較低的值。</span><span class="sxs-lookup"><span data-stu-id="590b5-132">The default value is 100, but you may want to set a lower value, because a large number of nodes can be slow to compile.</span></span> <span data-ttu-id="590b5-133">特別是如果您使用 LINQ to Objects （亦即，在記憶體中，而不使用中繼 LINQ 提供者的集合上的 LINQ 查詢）。</span><span class="sxs-lookup"><span data-stu-id="590b5-133">This is particularly true if you are using LINQ to Objects (i.e., LINQ queries on a collection in memory, without the use of an intermediate LINQ provider).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- <span data-ttu-id="590b5-134">請考慮停用的 any （） 和 all （） 函式，這些可能會很慢。</span><span class="sxs-lookup"><span data-stu-id="590b5-134">Consider disabling the any() and all() functions, as these can be slow.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- <span data-ttu-id="590b5-135">如果任何字串屬性包含大型字串&#8212;例如，產品描述或部落格文章&#8212;請考慮停用的字串函數。</span><span class="sxs-lookup"><span data-stu-id="590b5-135">If any string properties contain large strings&#8212;for example, a product description or a blog entry&#8212;consider disabling the string functions.</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- <span data-ttu-id="590b5-136">請考慮不允許的導覽屬性進行篩選。</span><span class="sxs-lookup"><span data-stu-id="590b5-136">Consider disallowing filtering on navigation properties.</span></span> <span data-ttu-id="590b5-137">導覽屬性的篩選可能會導致聯結，可能會變慢，視您的資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="590b5-137">Filtering on navigation properties can result in a join, which might be slow, depending on your database schema.</span></span> <span data-ttu-id="590b5-138">下列程式碼會顯示查詢驗證程式，以防止篩選導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="590b5-138">The following code shows a query validator that prevents filtering on navigation properties.</span></span> <span data-ttu-id="590b5-139">如需有關查詢驗證程式的詳細資訊，請參閱 <<c0> [ 查詢驗證](supporting-odata-query-options.md#query-validation)。</span><span class="sxs-lookup"><span data-stu-id="590b5-139">For more information about query validators, see [Query Validation](supporting-odata-query-options.md#query-validation).</span></span> 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- <span data-ttu-id="590b5-140">請考慮限制 $filter 查詢藉由撰寫自訂資料庫的驗證程式。</span><span class="sxs-lookup"><span data-stu-id="590b5-140">Consider restricting $filter queries by writing a validator that is customized for your database.</span></span> <span data-ttu-id="590b5-141">例如，請考慮這兩個查詢：</span><span class="sxs-lookup"><span data-stu-id="590b5-141">For example, consider these two queries:</span></span> 

  - <span data-ttu-id="590b5-142">與動作項目以 'A' 開頭的姓氏的所有影片。</span><span class="sxs-lookup"><span data-stu-id="590b5-142">All movies with actors whose last name starts with ‘A'.</span></span>
  - <span data-ttu-id="590b5-143">1994 年發行的所有影片。</span><span class="sxs-lookup"><span data-stu-id="590b5-143">All movies released in 1994.</span></span>

    <span data-ttu-id="590b5-144">除非電影會由動作項目編製索引，第一個查詢可能需要掃描整個清單的電影資料庫引擎。</span><span class="sxs-lookup"><span data-stu-id="590b5-144">Unless movies are indexed by actors, the first query might require the DB engine to scan the entire list of movies.</span></span> <span data-ttu-id="590b5-145">而第二個的查詢可能會是可接受的則假設電影會編製索引的發行年份。</span><span class="sxs-lookup"><span data-stu-id="590b5-145">Whereas the second query might be acceptable, assuming movies are indexed by release year.</span></span>

    <span data-ttu-id="590b5-146">下列程式碼顯示的驗證程式，可讓您的 「 ReleaseYear"和"Title"屬性，但沒有其他屬性的篩選。</span><span class="sxs-lookup"><span data-stu-id="590b5-146">The following code shows a validator that allows filtering on the "ReleaseYear" and "Title" properties but no other properties.</span></span>

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- <span data-ttu-id="590b5-147">一般情況下，請考慮您需要哪些 $filter 函式。</span><span class="sxs-lookup"><span data-stu-id="590b5-147">In general, consider which $filter functions you need.</span></span> <span data-ttu-id="590b5-148">如果您的用戶端不需要 $filter 完整表達，您可以限制允許的函式。</span><span class="sxs-lookup"><span data-stu-id="590b5-148">If your clients do not need the full expressiveness of $filter, you can limit the allowed functions.</span></span>
