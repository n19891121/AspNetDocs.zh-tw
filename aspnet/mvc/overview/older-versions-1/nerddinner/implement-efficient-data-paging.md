---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 實現高效的數據分頁 |微軟文件
author: rick-anderson
description: 步驟 8 演示如何向 /Dinners URL 添加尋呼支援,以便我們一次不顯示 1000 份晚餐,我們僅在...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541321"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="dc723-103">實作有效率的資料分頁</span><span class="sxs-lookup"><span data-stu-id="dc723-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="dc723-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dc723-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="dc723-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="dc723-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="dc723-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第8步,該教程示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc723-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="dc723-107">步驟 8 演示如何向我們的 /Dinners URL 添加尋呼支援,以便我們一次只顯示 10 份即將舉辦的晚餐,並且允許最終使用者以 SEO 友好的方式回傳整個清單。</span><span class="sxs-lookup"><span data-stu-id="dc723-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="dc723-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="dc723-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="dc723-109">神經晚餐步驟 8: 尋呼支援</span><span class="sxs-lookup"><span data-stu-id="dc723-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="dc723-110">如果我們的網站成功,它將有成千上萬的即將到來的晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc723-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="dc723-111">我們需要確保我們的 UI 擴展以處理所有這些晚餐,並允許用戶瀏覽它們。</span><span class="sxs-lookup"><span data-stu-id="dc723-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="dc723-112">為了啟用這一點,我們將添加分頁支援到我們的 */Dinners* URL,以便我們不是一次顯示 1000 份晚餐,而是一次只顯示 10 份即將舉辦的晚餐 -並允許最終使用者以 SEO 友好的方式回傳和轉發整個清單。</span><span class="sxs-lookup"><span data-stu-id="dc723-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="dc723-113">索引() 操作方法回顧</span><span class="sxs-lookup"><span data-stu-id="dc723-113">Index() Action Method Recap</span></span>

<span data-ttu-id="dc723-114">我們的 DinnersController 類別中的 Index() 操作方法目前所示:</span><span class="sxs-lookup"><span data-stu-id="dc723-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="dc723-115">當對 */Dinners* URL 發出請求時,它會檢索所有即將舉辦的晚宴的清單,然後呈現所有這些晚宴的清單:</span><span class="sxs-lookup"><span data-stu-id="dc723-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="dc723-116">瞭解可&lt;查詢 T&gt;</span><span class="sxs-lookup"><span data-stu-id="dc723-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="dc723-117">*IQuery&lt;&gt;T*是 LINQ 作為 .NET 3.5 的一部分引入的介面。</span><span class="sxs-lookup"><span data-stu-id="dc723-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="dc723-118">它支持強大的"延遲執行"方案,我們可以利用這些場景來實現分頁支援。</span><span class="sxs-lookup"><span data-stu-id="dc723-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="dc723-119">在我們的晚餐存儲庫中,我們將從我們的「查找晚餐&lt;&gt;」 方法返回一個可查詢的晚餐序列:</span><span class="sxs-lookup"><span data-stu-id="dc723-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="dc723-120">我們的 Find&lt;&gt;對托 晚餐() 方法傳回的 I 可查詢晚餐物件封裝了一個查詢,以便使用 LINQ 從我們的資料庫中檢索 Dinner 物件,使用 LINQ 到 SQL。</span><span class="sxs-lookup"><span data-stu-id="dc723-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="dc723-121">重要的是,在我們嘗試訪問/反覆運算查詢中的數據之前,或者直到我們調用查詢上的 ToList() 方法之前,它不會對資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="dc723-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="dc723-122">調用我們的 Find 對興晚餐() 方法的代碼可以選擇在執行查詢之前向&lt;IQuery Dinner&gt;物件添加其他「連結」操作/篩選器。</span><span class="sxs-lookup"><span data-stu-id="dc723-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="dc723-123">然後,LINQ 到 SQL 足夠智慧,在請求數據時對資料庫執行組合查詢。</span><span class="sxs-lookup"><span data-stu-id="dc723-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="dc723-124">為了實現分頁邏輯,我們可以更新我們的 DinnersController Index() 操作方法,以便它在調用 ToList() 之前,將其他「&lt;跳&gt;過」和「 獲取 」運算元應用於返回的可查詢晚餐序列:</span><span class="sxs-lookup"><span data-stu-id="dc723-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="dc723-125">上述代碼跳過資料庫中即將進行的 10 份晚餐,然後返回 20 份晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc723-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="dc723-126">LINQ 到 SQL 足夠智慧,可以建構最佳化的 SQL 查詢,該查詢在 SQL 資料庫中執行此跳過邏輯,而不是在 Web 伺服器中執行此跳過邏輯。</span><span class="sxs-lookup"><span data-stu-id="dc723-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="dc723-127">這意味著,即使我們資料庫中有數百萬個即將推出的 Dinner,也只能檢索我們想要的 10 個,作為此請求的一部分(使其高效且可擴展)。</span><span class="sxs-lookup"><span data-stu-id="dc723-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="dc723-128">新增頁面的頁面值</span><span class="sxs-lookup"><span data-stu-id="dc723-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="dc723-129">我們希望我們的 URL 包含一個「頁面」參數,指示使用者請求的「晚餐範圍」,而不是對特定頁面範圍進行硬編碼。</span><span class="sxs-lookup"><span data-stu-id="dc723-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="dc723-130">使用查詢字串值</span><span class="sxs-lookup"><span data-stu-id="dc723-130">Using a Querystring value</span></span>

<span data-ttu-id="dc723-131">下面的程式碼展示如何更新我們的 Index() 操作方法以支援查詢字串參數,並啟用 URL,如 */Dinners page_2*:</span><span class="sxs-lookup"><span data-stu-id="dc723-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="dc723-132">上面的 Index() 操作方法具有名為「頁」的參數。</span><span class="sxs-lookup"><span data-stu-id="dc723-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="dc723-133">參數聲明為空整數(即 int? 指示)。</span><span class="sxs-lookup"><span data-stu-id="dc723-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="dc723-134">這意味著 */Dinners?page_2* URL將導致將值"2"作為參數值傳遞。</span><span class="sxs-lookup"><span data-stu-id="dc723-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="dc723-135">*/Dinners* URL(沒有查詢字串值)將導致傳遞空值。</span><span class="sxs-lookup"><span data-stu-id="dc723-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="dc723-136">我們將頁面值乘以頁面大小(本例中為 10 行),以確定要跳過的晚餐數。</span><span class="sxs-lookup"><span data-stu-id="dc723-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="dc723-137">我們使用[C# null"合併「運算符 (?),](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)在處理可無類型時非常有用。</span><span class="sxs-lookup"><span data-stu-id="dc723-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="dc723-138">如果頁面參數為空,上述代碼將值為 0 分配給頁。</span><span class="sxs-lookup"><span data-stu-id="dc723-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="dc723-139">使用嵌入式網址值</span><span class="sxs-lookup"><span data-stu-id="dc723-139">Using Embedded URL values</span></span>

<span data-ttu-id="dc723-140">使用查詢字串值的替代方法是將頁面參數嵌入到實際 URL 本身中。</span><span class="sxs-lookup"><span data-stu-id="dc723-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="dc723-141">例如 *:/晚餐/頁/2*或 */Dinner/2*。</span><span class="sxs-lookup"><span data-stu-id="dc723-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="dc723-142">ASP.NET MVC 包含強大的 URL 路由引擎,便於支援類似方案。</span><span class="sxs-lookup"><span data-stu-id="dc723-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="dc723-143">我們可以註冊自定義路由規則,將任何傳入 URL 或 URL 格式映射到所需的任何控制器類或操作方法。</span><span class="sxs-lookup"><span data-stu-id="dc723-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="dc723-144">我們只需要在我們的項目中打開 Global.asax 檔:</span><span class="sxs-lookup"><span data-stu-id="dc723-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="dc723-145">然後使用 MapRoute() 幫助器方法註冊新的映射規則,如對路由的第一次調用。地圖路線() 如下:</span><span class="sxs-lookup"><span data-stu-id="dc723-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="dc723-146">上圖,我們正在註冊一個名為"即將推出的晚餐"的新路由規則。</span><span class="sxs-lookup"><span data-stu-id="dc723-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="dc723-147">我們指示它有 URL 格式"Dinners/page/{頁面}" - 其中 [頁面] 是嵌入在 URL 中的參數值。</span><span class="sxs-lookup"><span data-stu-id="dc723-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="dc723-148">MapRoute() 方法的第三個參數指示我們應該映射此格式與 DinnersController 類上的 Index() 操作方法相匹配的 URL。</span><span class="sxs-lookup"><span data-stu-id="dc723-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="dc723-149">我們可以在查詢字串方案中使用我們以前完全相同的 Index() 代碼,除非現在我們的「頁面」參數將來自 URL 而不是查詢字串:</span><span class="sxs-lookup"><span data-stu-id="dc723-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="dc723-150">現在,當我們運行應用程式並輸入 */Dinner 時*,我們將看到前 10 場即將舉辦的晚宴:</span><span class="sxs-lookup"><span data-stu-id="dc723-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="dc723-151">當我們輸入 */Dinner/Page/1*時,我們將看到晚餐的下一頁:</span><span class="sxs-lookup"><span data-stu-id="dc723-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="dc723-152">新增網頁瀏覽 UI</span><span class="sxs-lookup"><span data-stu-id="dc723-152">Adding page navigation UI</span></span>

<span data-ttu-id="dc723-153">完成尋呼方案的最後一步是在我們的視圖範本中實現「下一步」和「上一個」導航 UI,以便用戶輕鬆跳過 Dinner 數據。</span><span class="sxs-lookup"><span data-stu-id="dc723-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="dc723-154">要正確實現這一點,我們需要知道資料庫中的 Dinner 的總數,以及它轉換為的數據頁數。</span><span class="sxs-lookup"><span data-stu-id="dc723-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="dc723-155">然後,我們需要計算當前請求的「頁面」值是在數據開頭還是結尾,並相應地顯示或隱藏「上一個」 和「下一個」 的 UI。</span><span class="sxs-lookup"><span data-stu-id="dc723-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="dc723-156">我們可以在 Index() 操作方法中實現此邏輯。</span><span class="sxs-lookup"><span data-stu-id="dc723-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="dc723-157">或者,我們可以向專案添加幫助器類,以更可重用的方式封裝此邏輯。</span><span class="sxs-lookup"><span data-stu-id="dc723-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="dc723-158">下面是一個簡單的"分頁清單"幫助器類,派生自內置於 .NET&lt;&gt;框架中的清單 T 集合類。</span><span class="sxs-lookup"><span data-stu-id="dc723-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="dc723-159">它實現了一個可重用的集合類,可用於分頁任何 IQuery 數據序列。</span><span class="sxs-lookup"><span data-stu-id="dc723-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="dc723-160">&lt;在我們的 NerdDinner 應用程式中,我們將針對 IQuery Dinner&gt;結果進行工作,但它在其他應用程式方案中可以同樣&lt;輕鬆&gt;地用於&lt;I&gt;可查詢 產品或可 查詢客戶 結果:</span><span class="sxs-lookup"><span data-stu-id="dc723-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="dc723-161">請注意,它如何計算,然後公開屬性,如"頁面索引","頁面大小","總計數"和"總頁"。</span><span class="sxs-lookup"><span data-stu-id="dc723-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="dc723-162">然後,它還公開兩個幫助屬性"Has上頁"和"HasNextPage",指示集合中的數據頁是原始序列的開頭還是結尾。</span><span class="sxs-lookup"><span data-stu-id="dc723-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="dc723-163">上述代碼將導致運行兩個 SQL 查詢 - 第一個查詢檢索 Dinner 物件總數的計數(這不會返回物件- 而是執行返回整數的"SELECT COUNT"語句),第二個代碼將僅從資料庫中檢索當前數據頁所需的數據行。</span><span class="sxs-lookup"><span data-stu-id="dc723-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="dc723-164">然後,我們可以更新我們的晚餐控制器.Index() 説明方法,從我們的晚餐存儲庫創建一&lt;&gt;個 PaginatedList 晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc723-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="dc723-165">然後,我們可以更新 [Views_Dinners_Index.aspx 視圖範本》,&lt;以便從ViewPage NerdDinner.Helpers.PaginatedList&lt;&gt;&gt;&lt;晚餐&lt;&gt;&gt;而不是ViewPage IE500s 晚宴上繼承,然後將以下代碼添加到視圖範本的底部,以顯示或隱藏下一個和以前的導航 UI:</span><span class="sxs-lookup"><span data-stu-id="dc723-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="dc723-166">請注意,我們使用 Html.RouteLink() 説明器方法生成超連結的方式。</span><span class="sxs-lookup"><span data-stu-id="dc723-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="dc723-167">此方法類似於我們以前使用過的 Html.ActionLink() 説明程式方法。</span><span class="sxs-lookup"><span data-stu-id="dc723-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="dc723-168">區別在於,我們使用在 Global.asax 檔中設置的"即將到達的晚餐"路由規則生成 URL。</span><span class="sxs-lookup"><span data-stu-id="dc723-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="dc723-169">這可確保我們將生成索引() 操作方法的 URL,該方法的格式為 *:/Dinners/page/{page}* - 其中 [page] 值是我們基於當前 PageIndex 提供上述變數。</span><span class="sxs-lookup"><span data-stu-id="dc723-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="dc723-170">現在,當我們再次運行應用程式時,我們將在瀏覽器中一次看到 10 份晚餐:</span><span class="sxs-lookup"><span data-stu-id="dc723-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="dc723-171">我們還在頁面&lt;&lt;&lt;&gt;&gt;底部&gt;具有和導航 UI,允許我們使用搜尋引擎可存取的網址 向前和向後跳過資料:</span><span class="sxs-lookup"><span data-stu-id="dc723-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="dc723-172">**側主題:瞭解可&lt;查詢 T 的含義&gt;**</span><span class="sxs-lookup"><span data-stu-id="dc723-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="dc723-173">IQueryable&lt; &gt; T 是一個非常強大的功能,支援各種有趣的延遲執行方案(如分頁和基於合成的查詢)。</span><span class="sxs-lookup"><span data-stu-id="dc723-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="dc723-174">與所有強大的功能一樣,您希望小心如何使用它,並確保它不受濫用。</span><span class="sxs-lookup"><span data-stu-id="dc723-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="dc723-175">請務必認識到,從存儲庫返回 IQuery&lt;&gt;可查詢 T 結果可以調用代碼來追加到它上的鏈式運算符方法,從而參與最終查詢執行。</span><span class="sxs-lookup"><span data-stu-id="dc723-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="dc723-176">如果不想提供此能力的調用代碼,則應&lt;傳回 IList T&gt;或&lt;IE55ble T&gt;結果 - 其中包含已執行的查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="dc723-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="dc723-177">對於分頁方案,這將要求您將實際數據暫停邏輯推送到被調用的存儲庫方法中。</span><span class="sxs-lookup"><span data-stu-id="dc723-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="dc723-178">在此方案中,我們可能會更新我們的 Find對價晚餐() 查找方法,以有一個簽名,該簽名要麼返回一個分&lt;&gt;頁清單&lt;:paginatedList 晚餐查找要約晚餐(int pageIndex,int page_info=2>)=或返回 IList 晚餐&gt;,並使用&lt;"&gt;總計數"外參數返回晚餐的 總數 :Ilist 晚餐查找要約晚餐(int 頁索引,int 頁大小)</span><span class="sxs-lookup"><span data-stu-id="dc723-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="dc723-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc723-179">Next Step</span></span>

<span data-ttu-id="dc723-180">現在,讓我們來看看如何向應用程式添加身份驗證和授權支援。</span><span class="sxs-lookup"><span data-stu-id="dc723-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dc723-181">[前一個](re-use-ui-using-master-pages-and-partials.md)
> [下一個](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="dc723-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
