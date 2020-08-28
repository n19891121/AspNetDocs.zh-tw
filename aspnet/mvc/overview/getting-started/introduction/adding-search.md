---
uid: mvc/overview/getting-started/introduction/adding-search
title: 搜尋 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044838"
---
# <a name="search"></a><span data-ttu-id="6d09b-102">搜尋</span><span class="sxs-lookup"><span data-stu-id="6d09b-102">Search</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="6d09b-103">新增搜尋方法和搜尋視圖</span><span class="sxs-lookup"><span data-stu-id="6d09b-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="6d09b-104">在本節中，您會將搜尋功能新增至 `Index` 動作方法，讓您依據內容類型或名稱來搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="6d09b-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d09b-105">先決條件</span><span class="sxs-lookup"><span data-stu-id="6d09b-105">Prerequisites</span></span>

<span data-ttu-id="6d09b-106">若要比對此區段的螢幕擷取畫面，您必須 (F5) 執行應用程式，並將下列電影新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="6d09b-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="6d09b-107">標題</span><span class="sxs-lookup"><span data-stu-id="6d09b-107">Title</span></span> | <span data-ttu-id="6d09b-108">發行日期</span><span class="sxs-lookup"><span data-stu-id="6d09b-108">Release Date</span></span> | <span data-ttu-id="6d09b-109">Genre</span><span class="sxs-lookup"><span data-stu-id="6d09b-109">Genre</span></span> | <span data-ttu-id="6d09b-110">價格</span><span class="sxs-lookup"><span data-stu-id="6d09b-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="6d09b-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="6d09b-111">Ghostbusters</span></span> | <span data-ttu-id="6d09b-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="6d09b-112">6/8/1984</span></span> | <span data-ttu-id="6d09b-113">喜劇</span><span class="sxs-lookup"><span data-stu-id="6d09b-113">Comedy</span></span> | <span data-ttu-id="6d09b-114">6.99</span><span class="sxs-lookup"><span data-stu-id="6d09b-114">6.99</span></span> |
| <span data-ttu-id="6d09b-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="6d09b-115">Ghostbusters II</span></span> | <span data-ttu-id="6d09b-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="6d09b-116">6/16/1989</span></span> | <span data-ttu-id="6d09b-117">喜劇</span><span class="sxs-lookup"><span data-stu-id="6d09b-117">Comedy</span></span> | <span data-ttu-id="6d09b-118">6.99</span><span class="sxs-lookup"><span data-stu-id="6d09b-118">6.99</span></span> |
| <span data-ttu-id="6d09b-119">Apes 的地球</span><span class="sxs-lookup"><span data-stu-id="6d09b-119">Planet of the Apes</span></span> | <span data-ttu-id="6d09b-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="6d09b-120">3/27/1986</span></span> | <span data-ttu-id="6d09b-121">動作</span><span class="sxs-lookup"><span data-stu-id="6d09b-121">Action</span></span> | <span data-ttu-id="6d09b-122">5.99</span><span class="sxs-lookup"><span data-stu-id="6d09b-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="6d09b-123">更新索引表單</span><span class="sxs-lookup"><span data-stu-id="6d09b-123">Updating the Index Form</span></span>

<span data-ttu-id="6d09b-124">首先，將 `Index` 動作方法更新為現有的 `MoviesController` 類別。</span><span class="sxs-lookup"><span data-stu-id="6d09b-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="6d09b-125">此程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="6d09b-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="6d09b-126">方法的第一行會 `Index` 建立下列 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 查詢來選取電影：</span><span class="sxs-lookup"><span data-stu-id="6d09b-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="6d09b-127">此查詢已在此時定義，但尚未針對資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="6d09b-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="6d09b-128">如果 `searchString` 參數包含字串，則會使用下列程式碼修改電影查詢來篩選搜尋字串的值：</span><span class="sxs-lookup"><span data-stu-id="6d09b-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="6d09b-129">上述 `s => s.Title` 程式碼是 [Lambda 運算式](https://msdn.microsoft.com/library/bb397687.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d09b-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="6d09b-130">在以方法為基礎的 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 查詢中，lambda 會用來作為標準查詢運算子方法的引數，例如在上述程式碼中使用的 [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="6d09b-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="6d09b-131">當 LINQ 查詢定義時，或藉由呼叫方法（例如或）進行修改時，不會執行 LINQ 查詢 `Where` `OrderBy` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="6d09b-132">相反地，查詢執行會延後，這表示運算式的評估會延遲，直到實際反覆運算其實現值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 呼叫方法為止。</span><span class="sxs-lookup"><span data-stu-id="6d09b-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="6d09b-133">在此 `Search` 範例中，查詢會在 *Index. cshtml* 視圖中執行。</span><span class="sxs-lookup"><span data-stu-id="6d09b-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="6d09b-134">如需延後查詢執行的詳細資訊，請參閱[查詢執行](https://msdn.microsoft.com/library/bb738633.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d09b-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6d09b-135">[Contains](https://msdn.microsoft.com/library/bb155125.aspx)方法是在資料庫上執行，而不是上述的 c # 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6d09b-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="6d09b-136">在資料庫上，[包含](https://msdn.microsoft.com/library/bb155125.aspx)[類似 SQL](https://msdn.microsoft.com/library/ms179859.aspx)的對應，它不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6d09b-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="6d09b-137">現在您可以更新 `Index` 將向使用者顯示表單的視圖。</span><span class="sxs-lookup"><span data-stu-id="6d09b-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="6d09b-138">執行應用程式，並流覽至 */Movies/Index*。</span><span class="sxs-lookup"><span data-stu-id="6d09b-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="6d09b-139">將查詢字串 (例如 `?searchString=ghost`) 附加至 URL。</span><span class="sxs-lookup"><span data-stu-id="6d09b-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="6d09b-140">隨即顯示篩選過的電影。</span><span class="sxs-lookup"><span data-stu-id="6d09b-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="6d09b-142">如果您將方法的簽章變更 `Index` 為具有名為的參數 `id` ， `id` 參數將符合 `{id}` *應用程式 \_ Start\RouteConfig.cs* 檔中所設定之預設路由的預留位置。</span><span class="sxs-lookup"><span data-stu-id="6d09b-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.txt)]

<span data-ttu-id="6d09b-143">原始的 `Index` 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d09b-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="6d09b-144">修改後的 `Index` 方法看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="6d09b-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="6d09b-145">您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="6d09b-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="6d09b-146">但是，您不能期望使用者在每次想要搜尋電影時修改 URL。</span><span class="sxs-lookup"><span data-stu-id="6d09b-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="6d09b-147">因此，現在您將新增可協助他們篩選電影的 UI。</span><span class="sxs-lookup"><span data-stu-id="6d09b-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="6d09b-148">如果您變更方法的簽章 `Index` 以測試如何傳遞路由系結識別碼參數，請將其變更回，讓您的 `Index` 方法接受名為的字串參數 `searchString` ：</span><span class="sxs-lookup"><span data-stu-id="6d09b-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="6d09b-149">開啟 *Views\Movies\Index.cshtml* 檔案，並在之後 `@Html.ActionLink("Create New", "Create")` 新增下列反白顯示的表單標記：</span><span class="sxs-lookup"><span data-stu-id="6d09b-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="6d09b-150">`Html.BeginForm`Helper 會建立開頭 `<form>` 標記。</span><span class="sxs-lookup"><span data-stu-id="6d09b-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="6d09b-151">`Html.BeginForm`當使用者按一下 [**篩選**] 按鈕來提交表單時，helper 會讓表單張貼至本身。</span><span class="sxs-lookup"><span data-stu-id="6d09b-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="6d09b-152">在顯示和編輯檢視檔案時，Visual Studio 2013 會有很好的改進。</span><span class="sxs-lookup"><span data-stu-id="6d09b-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="6d09b-153">當您執行應用程式並開啟 view 檔案時，Visual Studio 2013 會叫用正確的控制器動作方法來顯示視圖。</span><span class="sxs-lookup"><span data-stu-id="6d09b-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="6d09b-154">在 Visual Studio 中開啟索引視圖， (如上圖所示) 中，請按一下 Ctr F5 或 F5 來執行應用程式，然後嘗試搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="6d09b-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="6d09b-155">沒有方法的多載 `HttpPost` `Index` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="6d09b-156">您不需要它，因為方法不會變更應用程式的狀態，而只是篩選資料。</span><span class="sxs-lookup"><span data-stu-id="6d09b-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="6d09b-157">您可以新增下列 `HttpPost Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="6d09b-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="6d09b-158">在此情況下，動作啟動程式會符合 `HttpPost Index` 方法，而 `HttpPost Index` 方法會如下圖所示執行。</span><span class="sxs-lookup"><span data-stu-id="6d09b-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="6d09b-160">不過，即使您新增這個 `HttpPost` 版本的 `Index` 方法，在如何全部實作此方法方面仍然有其限制。</span><span class="sxs-lookup"><span data-stu-id="6d09b-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="6d09b-161">假設您想要將特定的搜尋加為書籤，或者想要傳送連結給朋友，讓他們可以點選來查看相同的電影篩選清單。</span><span class="sxs-lookup"><span data-stu-id="6d09b-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="6d09b-162">請注意，HTTP POST 要求的 URL 與 GET 要求的 URL 相同 (localhost： xxxxx/電影/Index) --URL 本身沒有搜尋資訊。</span><span class="sxs-lookup"><span data-stu-id="6d09b-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="6d09b-163">現在，搜尋字串資訊會以表單欄位值的形式傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="6d09b-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="6d09b-164">這表示您無法在 URL 中捕獲該搜尋資訊以將其加入書簽或傳送給朋友。</span><span class="sxs-lookup"><span data-stu-id="6d09b-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="6d09b-165">解決方案是使用的多載 `BeginForm` ，指定 POST 要求應將搜尋資訊新增至 URL，而且應該將它路由傳送至 `HttpGet` 方法的版本 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="6d09b-166">以下列標記取代現有的無參數 `BeginForm` 方法：</span><span class="sxs-lookup"><span data-stu-id="6d09b-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="6d09b-168">現在當您提交搜尋時，URL 會包含搜尋查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6d09b-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="6d09b-169">即使您有 `HttpPost Index` 方法，搜尋也會移至 `HttpGet Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="6d09b-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="6d09b-171">依內容類型新增搜尋</span><span class="sxs-lookup"><span data-stu-id="6d09b-171">Adding Search by Genre</span></span>

<span data-ttu-id="6d09b-172">如果您已新增 `HttpPost` 方法的版本 `Index` ，請立即將其刪除。</span><span class="sxs-lookup"><span data-stu-id="6d09b-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="6d09b-173">接下來，您將新增功能，讓使用者依內容類型搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="6d09b-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="6d09b-174">以下列程式碼取代 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="6d09b-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="6d09b-175">此版本的 `Index` 方法會採用額外的參數，亦即 `movieGenre` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="6d09b-176">前幾行程式碼會建立一個 `List` 物件來保存資料庫中的電影內容。</span><span class="sxs-lookup"><span data-stu-id="6d09b-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="6d09b-177">下列程式碼是一種 LINQ 查詢，其會從資料庫中擷取所有的內容類型。</span><span class="sxs-lookup"><span data-stu-id="6d09b-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="6d09b-178">程式碼會使用 `AddRange` 泛型集合的方法 `List` ，將所有相異的內容加入至清單。</span><span class="sxs-lookup"><span data-stu-id="6d09b-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="6d09b-179"> (不含 `Distinct` 修飾詞，就會加入重複的內容，例如，喜劇會在我們的範例) 中加入兩次。</span><span class="sxs-lookup"><span data-stu-id="6d09b-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="6d09b-180">然後，程式碼會將內容清單儲存在 `ViewBag.MovieGenre` 物件中。</span><span class="sxs-lookup"><span data-stu-id="6d09b-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="6d09b-181">將類別目錄資料 (這類電影內容) 做為中的 [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 物件 `ViewBag` ，然後在下拉式清單方塊中存取類別資料是 MVC 應用程式的一般方法。</span><span class="sxs-lookup"><span data-stu-id="6d09b-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="6d09b-182">下列程式碼顯示如何檢查 `movieGenre` 參數。</span><span class="sxs-lookup"><span data-stu-id="6d09b-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="6d09b-183">如果不是空的，則程式碼會進一步限制電影查詢，將選取的電影限制為指定的類型。</span><span class="sxs-lookup"><span data-stu-id="6d09b-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="6d09b-184">如先前所述，在動作方法傳回) 之後，查詢就不會在資料庫上執行，直到電影清單反復查看在視圖中發生的 (為止 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="6d09b-185">將標記新增至索引視圖，以支援依內容類型搜尋</span><span class="sxs-lookup"><span data-stu-id="6d09b-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="6d09b-186">在 Views\Movies\Index.cshtml 檔案中加入 helper 之前的協助程式 `Html.DropDownList` *Views\Movies\Index.cshtml* `TextBox` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="6d09b-187">完成的標記如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d09b-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="6d09b-188">在下列程式碼中：</span><span class="sxs-lookup"><span data-stu-id="6d09b-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="6d09b-189">參數 "MovieGenre" 會提供 `DropDownList` helper 在中尋找的索引鍵 `IEnumerable<SelectListItem>` `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="6d09b-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="6d09b-190">`ViewBag`已在動作方法中填入：</span><span class="sxs-lookup"><span data-stu-id="6d09b-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="6d09b-191">"All" 參數提供選項標籤。</span><span class="sxs-lookup"><span data-stu-id="6d09b-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="6d09b-192">如果您在瀏覽器中檢查該選擇，將會看到其 "value" 屬性是空的。</span><span class="sxs-lookup"><span data-stu-id="6d09b-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="6d09b-193">因為我們的控制器只 `if` 會篩選字串不是 `null` 或空白，所以提交空白值以 `movieGenre` 顯示所有內容。</span><span class="sxs-lookup"><span data-stu-id="6d09b-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="6d09b-194">您也可以設定預設選取的選項。</span><span class="sxs-lookup"><span data-stu-id="6d09b-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="6d09b-195">如果您想要將 "喜劇" 作為預設選項，您可以變更控制器中的程式碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d09b-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="6d09b-196">執行應用程式，並流覽至 */Movies/Index*。</span><span class="sxs-lookup"><span data-stu-id="6d09b-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="6d09b-197">依內容類型、電影名稱，以及這兩個準則來嘗試搜尋。</span><span class="sxs-lookup"><span data-stu-id="6d09b-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="6d09b-198">在本節中，您建立了搜尋動作方法和視圖，讓使用者依電影標題和內容類型進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="6d09b-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="6d09b-199">在下一節中，您將瞭解如何將屬性加入至 `Movie` 模型，以及如何加入會自動建立測試資料庫的初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="6d09b-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6d09b-200">[上一個](examining-the-edit-methods-and-edit-view.md) 
> [下一步](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="6d09b-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
