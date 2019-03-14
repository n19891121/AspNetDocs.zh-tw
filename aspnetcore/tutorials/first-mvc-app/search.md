---
title: 將搜尋新增至 ASP.NET Core MVC 應用程式
author: rick-anderson
description: 示範如何將搜尋新增至基本 ASP.NET Core MVC 應用程式
ms.author: riande
ms.date: 12/13/2018
uid: tutorials/first-mvc-app/search
ms.openlocfilehash: e5dce35b60080ef752f8e6c6004158219015cbf5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029725"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="8f4ac-103">將搜尋新增至 ASP.NET Core MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="8f4ac-103">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="8f4ac-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8f4ac-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="8f4ac-105">在本節中，您會將搜尋功能新增至 `Index` 動作方法，讓您依據「內容類型」或「名稱」搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-105">In this section, you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="8f4ac-106">以下列程式碼更新 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-106">Update the `Index` method with the following code:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="8f4ac-107">`Index` 動作方法的第一行會建立 [LINQ](/dotnet/standard/using-linq) 查詢，以選取電影：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-107">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="8f4ac-108">查詢｢只｣會在此時定義，它尚**未**對資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-108">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="8f4ac-109">如果 `searchString` 參數包含字串，則會修改電影查詢來篩選搜尋字串的值：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-109">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="8f4ac-110">上述 `s => s.Title.Contains()` 程式碼是 [Lambda 運算式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-110">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="8f4ac-111">在以方法為基礎的 [LINQ](/dotnet/standard/using-linq) 查詢中，Lambda 會用來作為標準查詢運算子方法的引數，例如 [Where](/dotnet/api/system.linq.enumerable.where) 方法或 `Contains` (用於上述程式碼)。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-111">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="8f4ac-112">定義 LINQ 查詢或藉由呼叫像是 `Where`、`Contains` 或 `OrderBy` 等方法進行修改時，並不會執行查詢。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-112">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`, or `OrderBy`.</span></span> <span data-ttu-id="8f4ac-113">而會延後執行查詢。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-113">Rather, query execution is deferred.</span></span>  <span data-ttu-id="8f4ac-114">這是指延遲評估運算式，直到實際反覆運算其實現值或呼叫 `ToListAsync` 方法為止。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-114">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="8f4ac-115">如需延後查詢執行的詳細資訊，請參閱[查詢執行](/dotnet/framework/data/adonet/ef/language-reference/query-execution)。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-115">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="8f4ac-116">注意:[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法是在資料庫上執行，而不是在上方顯示的 C# 程式碼中執行。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-116">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="8f4ac-117">查詢是否區分大小寫取決於資料庫和定序。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-117">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="8f4ac-118">在 SQL Server 上，[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 對應至 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)，因此不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-118">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="8f4ac-119">在 SQLlite 中，由於使用預設定序，它會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-119">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="8f4ac-120">巡覽至 `/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-120">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="8f4ac-121">將查詢字串 (例如 `?searchString=Ghost`) 附加至 URL。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-121">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="8f4ac-122">隨即顯示篩選過的電影。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-122">The filtered movies are displayed.</span></span>

![索引檢視](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="8f4ac-124">如果您將 `Index` 方法的簽章變更為包含名為 `id` 的參數，則 `id` 參數會比對 *Startup.cs* 中所設定之預設路由的選擇性 `{id}` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-124">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]

<span data-ttu-id="8f4ac-125">將參數變更為 `id`，並將所有出現的 `searchString` 變更為 `id`。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-125">Change the parameter to `id` and all occurrences of `searchString` change to `id`.</span></span>

<span data-ttu-id="8f4ac-126">前一個 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-126">The previous `Index` method:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_1stSearch)]

<span data-ttu-id="8f4ac-127">含有 `id` 參數的已更新 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-127">The updated `Index` method with `id` parameter:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_SearchID)]

<span data-ttu-id="8f4ac-128">您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-128">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![已將 ghost 一詞新增至 URL，而傳回的電影清單包含 Ghostbusters 和 Ghostbusters 2 兩個電影的 Index 檢視](~/tutorials/first-mvc-app/search/_static/g2.png)

<span data-ttu-id="8f4ac-130">但是，您不能期望使用者在每次想要搜尋電影時修改 URL。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-130">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="8f4ac-131">因此，現在您將新增可協助他們篩選電影的 UI 項目。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-131">So now you'll add UI elements to help them filter movies.</span></span> <span data-ttu-id="8f4ac-132">如果您已變更 `Index` 方法的簽章來測試如何傳遞路由繫結的 `ID` 參數，請將其變更回採用一個名為 `searchString` 參數：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-132">If you changed the signature of the `Index` method to test how to pass the route-bound `ID` parameter, change it back so that it takes a parameter named `searchString`:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1,6,8&name=snippet_1stSearch)]

<span data-ttu-id="8f4ac-133">開啟 *Views/Movies/Index.cshtml* 檔案，並新增下面強調顯示的 `<form>` 標記：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-133">Open the *Views/Movies/Index.cshtml* file, and add the `<form>` markup highlighted below:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexForm1.cshtml?highlight=10-16&range=4-21)]

<span data-ttu-id="8f4ac-134">HTML `<form>` 標記使用[表單標記協助程式](xref:mvc/views/working-with-forms)，因此當您提交表單時，篩選條件字串會張貼至電影控制器的 `Index` 動作。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-134">The HTML `<form>` tag uses the [Form Tag Helper](xref:mvc/views/working-with-forms), so when you submit the form, the filter string is posted to the `Index` action of the movies controller.</span></span> <span data-ttu-id="8f4ac-135">儲存變更，然後測試篩選條件。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-135">Save your changes and then test the filter.</span></span>

![已將 ghost 一詞輸入 [標題] 篩選條件文字方塊的 Index 檢視](~/tutorials/first-mvc-app/search/_static/filter.png)

<span data-ttu-id="8f4ac-137">沒有您可能期望的 `Index` 方法的 `[HttpPost]` 多載。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-137">There's no `[HttpPost]` overload of the `Index` method as you might expect.</span></span> <span data-ttu-id="8f4ac-138">您不需要它，因為方法不會變更應用程式的狀態，而只會篩選資料。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-138">You don't need it, because the method isn't changing the state of the app, just filtering data.</span></span>

<span data-ttu-id="8f4ac-139">您可以新增下列 `[HttpPost] Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-139">You could add the following `[HttpPost] Index` method.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?highlight=1&name=snippet_SearchPost)]

<span data-ttu-id="8f4ac-140">`notUsed` 參數用來建立 `Index` 方法的多載。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-140">The `notUsed` parameter is used to create an overload for the `Index` method.</span></span> <span data-ttu-id="8f4ac-141">我們稍後將在本教學課程中加以討論。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-141">We'll talk about that later in the tutorial.</span></span>

<span data-ttu-id="8f4ac-142">如果您新增此方法，動作啟動程式會比對 `[HttpPost] Index` 方法，而 `[HttpPost] Index` 方法會如下列影像所示執行。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-142">If you add this method, the action invoker would match the `[HttpPost] Index` method, and the `[HttpPost] Index` method would run as shown in the image below.</span></span>

![應用程式回應為 "From HttpPost Index: filter on ghost" 的瀏覽器視窗](~/tutorials/first-mvc-app/search/_static/fo.png)

<span data-ttu-id="8f4ac-144">不過，即使您新增這個 `[HttpPost]` 版本的 `Index` 方法，在如何全部實作此方法方面仍然有其限制。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-144">However, even if you add this `[HttpPost]` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="8f4ac-145">假設您想要將特定的搜尋加為書籤，或者想要傳送連結給朋友，讓他們可以點選來查看相同的電影篩選清單。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-145">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="8f4ac-146">請注意，HTTP POST 要求的 URL 與 GET 要求的 URL (localhost:xxxxx/Movies/Index) 相同 -- 在 URL 中沒有搜尋資訊。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-146">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL.</span></span> <span data-ttu-id="8f4ac-147">搜尋字串資訊會以[表單欄位值](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data)的形式傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-147">The search string information is sent to the server as a [form field value](https://developer.mozilla.org/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data).</span></span> <span data-ttu-id="8f4ac-148">您可以使用瀏覽器開發人員工具或絕佳的 [Fiddler 工具](http://www.telerik.com/fiddler)來進行確認。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-148">You can verify that with the browser Developer tools or the excellent [Fiddler tool](http://www.telerik.com/fiddler).</span></span> <span data-ttu-id="8f4ac-149">下圖顯示 Chrome 瀏覽器開發人員工具：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-149">The image below shows the Chrome browser Developer tools:</span></span>

![顯示 searchString 值為 ghost 之要求本文的 Microsoft Edge 開發人員工具的 [網路] 索引標籤](~/tutorials/first-mvc-app/search/_static/f12_rb.png)

<span data-ttu-id="8f4ac-151">您可以在要求本文中看到搜尋參數和 [XSRF](xref:security/anti-request-forgery) 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-151">You can see the search parameter and [XSRF](xref:security/anti-request-forgery) token in the request body.</span></span> <span data-ttu-id="8f4ac-152">請注意，如先前的教學課程中所述，[表單標記協助程式](xref:mvc/views/working-with-forms)會產生 [XSRF](xref:security/anti-request-forgery) 防偽語彙基元。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-152">Note, as mentioned in the previous tutorial, the [Form Tag Helper](xref:mvc/views/working-with-forms) generates an [XSRF](xref:security/anti-request-forgery) anti-forgery token.</span></span> <span data-ttu-id="8f4ac-153">我們不會修改資料，因此不需要驗證控制器方法中的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-153">We're not modifying data, so we don't need to validate the token in the controller method.</span></span>

<span data-ttu-id="8f4ac-154">由於搜尋參數是在要求本文而不是 URL 中，因此您無法擷取該搜尋資訊以加為書籤或與其他人共用。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-154">Because the search parameter is in the request body and not the URL, you can't capture that search information to bookmark or share with others.</span></span> <span data-ttu-id="8f4ac-155">請指定要求應該是 `HTTP GET` 來修正此問題：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-155">Fix this by specifying the request should be `HTTP GET`:</span></span>

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexGet.cshtml?highlight=12&range=1-23)]

<span data-ttu-id="8f4ac-156">現在當您提交搜尋時，URL 中會包含搜尋查詢字串。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-156">Now when you submit a search, the URL contains the search query string.</span></span> <span data-ttu-id="8f4ac-157">即使您有 `HttpPost Index` 方法，搜尋也會移至 `HttpGet Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-157">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![顯示 URL 中 searchString=ghost 且傳回的電影 Ghostbusters 和 Ghostbusters 2 包含 ghost 一詞的瀏覽器視窗](~/tutorials/first-mvc-app/search/_static/search_get.png)

<span data-ttu-id="8f4ac-159">下列標記顯示 `form` 標記的變更：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-159">The following markup shows the change to the `form` tag:</span></span>

```html
<form asp-controller="Movies" asp-action="Index" method="get">
   ```

## <a name="add-search-by-genre"></a><span data-ttu-id="8f4ac-160">新增依內容類型搜尋</span><span class="sxs-lookup"><span data-stu-id="8f4ac-160">Add Search by genre</span></span>

<span data-ttu-id="8f4ac-161">將下列 `MovieGenreViewModel` 類別新增至 *Models* 資料夾：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-161">Add the following `MovieGenreViewModel` class to the *Models* folder:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieGenreViewModel.cs)]

<span data-ttu-id="8f4ac-162">電影內容類型檢視模型將包含：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-162">The movie-genre view model will contain:</span></span>

   * <span data-ttu-id="8f4ac-163">電影清單。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-163">A list of movies.</span></span>
   * <span data-ttu-id="8f4ac-164">包含內容類型清單的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-164">A `SelectList` containing the list of genres.</span></span> <span data-ttu-id="8f4ac-165">這可讓使用者從清單中選取內容類型。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-165">This allows the user to select a genre from the list.</span></span>
   * <span data-ttu-id="8f4ac-166">包含所選取內容類型的 `MovieGenre`。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-166">`MovieGenre`, which contains the selected genre.</span></span>
   * <span data-ttu-id="8f4ac-167">`SearchString`，其中包含使用者在搜尋文字方塊中輸入的文字。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-167">`SearchString`, which contains the text users enter in the search text box.</span></span>

<span data-ttu-id="8f4ac-168">以下列程式碼取代 `MoviesController.cs` 中的 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-168">Replace the `Index` method in `MoviesController.cs` with the following code:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_SearchGenre)]

<span data-ttu-id="8f4ac-169">下列程式碼是從資料庫中擷取所有內容類型的 `LINQ` 查詢。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-169">The following code is a `LINQ` query that retrieves all the genres from the database.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MoviesController.cs?name=snippet_LINQ)]

<span data-ttu-id="8f4ac-170">藉由投射不同的內容類型來建立內容類型的 `SelectList` (我們不希望選取清單中有重複的內容類型)。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-170">The `SelectList` of genres is created by projecting the distinct genres (we don't want our select list to have duplicate genres).</span></span>

<span data-ttu-id="8f4ac-171">當使用者搜尋項目時，搜尋的值會保留在搜尋方塊中。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-171">When the user searches for the item, the search value is retained in the search box.</span></span>

## <a name="add-search-by-genre-to-the-index-view"></a><span data-ttu-id="8f4ac-172">將依內容類型搜尋新增至 Index 檢視</span><span class="sxs-lookup"><span data-stu-id="8f4ac-172">Add search by genre to the Index view</span></span>

<span data-ttu-id="8f4ac-173">如下所示更新 `Index.cshtml`：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-173">Update `Index.cshtml` as follows:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexFormGenreNoRating.cshtml?highlight=1,15,16,17,28,31,34,37,43)]

<span data-ttu-id="8f4ac-174">檢查下列 HTML 協助程式中使用的 Lambda 運算式：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-174">Examine the lambda expression used in the following HTML Helper:</span></span>

`@Html.DisplayNameFor(model => model.Movies[0].Title)`

<span data-ttu-id="8f4ac-175">在上述程式碼中，`DisplayNameFor` HTML 協助程式會檢查 Lambda 運算式中參考的 `Title` 屬性來判斷顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-175">In the preceding code, the `DisplayNameFor` HTML Helper inspects the `Title` property referenced in the lambda expression to determine the display name.</span></span> <span data-ttu-id="8f4ac-176">由於 Lambda 運算式是檢查而不是評估，因此您在 `model`、`model.Movies` 或 `model.Movies[0]` 是 `null` 或空白時，不會收到存取違規。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-176">Since the lambda expression is inspected rather than evaluated, you don't receive an access violation when `model`, `model.Movies`, or `model.Movies[0]` are `null` or empty.</span></span> <span data-ttu-id="8f4ac-177">在評估 Lambda 運算式時 (例如，`@Html.DisplayFor(modelItem => item.Title)`)，會評估模型的屬性值。</span><span class="sxs-lookup"><span data-stu-id="8f4ac-177">When the lambda expression is evaluated (for example, `@Html.DisplayFor(modelItem => item.Title)`), the model's property values are evaluated.</span></span>

<span data-ttu-id="8f4ac-178">依據內容類型、電影標題和這兩者進行搜尋，藉以測試應用程式：</span><span class="sxs-lookup"><span data-stu-id="8f4ac-178">Test the app by searching by genre, by movie title, and by both:</span></span>

![顯示 https://localhost:5001/Movies?MovieGenre=Comedy&SearchString=2 結果的瀏覽器視窗](~/tutorials/first-mvc-app/search/_static/s2.png)

> [!div class="step-by-step"]
> <span data-ttu-id="8f4ac-180">[上一頁](controller-methods-views.md)
> [下一頁](new-field.md)</span><span class="sxs-lookup"><span data-stu-id="8f4ac-180">[Previous](controller-methods-views.md)
[Next](new-field.md)</span></span>  
