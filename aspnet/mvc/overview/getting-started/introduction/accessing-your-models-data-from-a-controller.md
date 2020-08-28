---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045165"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="a4816-102">從控制器存取模型資料</span><span class="sxs-lookup"><span data-stu-id="a4816-102">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="a4816-103">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a4816-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="a4816-104">在本節中，您將建立新的 `MoviesController` 類別，並撰寫程式碼以抓取電影資料，並使用 view 範本在瀏覽器中顯示該資料。</span><span class="sxs-lookup"><span data-stu-id="a4816-104">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="a4816-105">請先**建立應用程式**，再繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a4816-105">**Build the application** before going on to the next step.</span></span> <span data-ttu-id="a4816-106">如果您未建立應用程式，您將會在新增控制器時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a4816-106">If you don't build the application, you'll get an error adding a controller.</span></span>

<span data-ttu-id="a4816-107">在方案總管中，以滑鼠右鍵按一下 [ *控制器* ] 資料夾，然後按一下 [ **新增**]，然後按一下 [ **控制器**]。</span><span class="sxs-lookup"><span data-stu-id="a4816-107">In Solution Explorer, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="a4816-108">在 [ **新增 Scaffold** ] 對話方塊中，按一下 [ **具有 views 的 MVC 5 控制器]，使用 Entity Framework**]，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a4816-108">In the **Add Scaffold** dialog box, click **MVC 5 Controller with views, using Entity Framework**, and then click **Add**.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- <span data-ttu-id="a4816-109">選取 [ \*\*Movie (MvcMovie \*\* ] 模型類別的 [) 模型]。</span><span class="sxs-lookup"><span data-stu-id="a4816-109">Select **Movie (MvcMovie.Models)** for the Model class.</span></span>
- <span data-ttu-id="a4816-110">針對資料內容類別選取 \*\*MovieDBCoNtext (MvcMovie) \*\* 。</span><span class="sxs-lookup"><span data-stu-id="a4816-110">Select **MovieDBContext (MvcMovie.Models)** for the Data context class.</span></span>
- <span data-ttu-id="a4816-111">在 [控制器名稱] 中輸入 **moviescontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="a4816-111">For the Controller name enter **MoviesController**.</span></span>

  <span data-ttu-id="a4816-112">下圖顯示已完成的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a4816-112">The image below shows the completed dialog.</span></span>  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

<span data-ttu-id="a4816-113">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="a4816-113">Click **Add**.</span></span> <span data-ttu-id="a4816-114"> (如果您收到錯誤，可能是您在開始新增控制器之前未建立應用程式。 ) Visual Studio 會建立下列檔案和資料夾：</span><span class="sxs-lookup"><span data-stu-id="a4816-114">(If you get an error, you probably didn't build the application before starting adding the controller.) Visual Studio creates the following files and folders:</span></span>

- <span data-ttu-id="a4816-115">[*控制器*] 資料夾中*的 MoviesController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="a4816-115">*A MoviesController.cs* file in the *Controllers* folder.</span></span>
- <span data-ttu-id="a4816-116">*Views\Movies*資料夾。</span><span class="sxs-lookup"><span data-stu-id="a4816-116">A *Views\Movies* folder.</span></span>
- <span data-ttu-id="a4816-117">在新的*Views\Movies*資料夾中，*建立 cshtml、Delete、cshtml、Details*、. cshtml 和*Index. cshtml* 。</span><span class="sxs-lookup"><span data-stu-id="a4816-117">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="a4816-118">Visual Studio 自動建立 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (為您建立、讀取、更新和刪除) 動作方法和視圖 (自動建立 crud 動作方法和視圖，稱為「樣板) 」。</span><span class="sxs-lookup"><span data-stu-id="a4816-118">Visual Studio automatically created the [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="a4816-119">您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。</span><span class="sxs-lookup"><span data-stu-id="a4816-119">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="a4816-120">執行應用程式，並按一下 [ **MVC 電影** ] 連結 (或在 `Movies` 瀏覽器的網址列中，將 */Movies* 附加至 URL，以流覽至控制器) 。</span><span class="sxs-lookup"><span data-stu-id="a4816-120">Run the application and click on the **MVC Movie** link (or browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser).</span></span> <span data-ttu-id="a4816-121">由於應用程式是依賴 *應用程式 \_ Start\RouteConfig.cs* 檔中定義的預設路由 () ，因此瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至控制器的預設 `Index` 動作方法 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-121">Because the application is relying on the default routing (defined in the *App\_Start\RouteConfig.cs* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="a4816-122">換句話說，瀏覽器要求實際上與 `http://localhost:xxxxx/Movies` 瀏覽器要求相同 `http://localhost:xxxxx/Movies/Index` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-122">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="a4816-123">結果是空的電影清單，因為您還沒有加入。</span><span class="sxs-lookup"><span data-stu-id="a4816-123">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a><span data-ttu-id="a4816-124">建立電影</span><span class="sxs-lookup"><span data-stu-id="a4816-124">Creating a Movie</span></span>

<span data-ttu-id="a4816-125">選取 **Create New** 連結。</span><span class="sxs-lookup"><span data-stu-id="a4816-125">Select the **Create New** link.</span></span> <span data-ttu-id="a4816-126">輸入影片的一些詳細資料，然後按一下 [ **建立** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4816-126">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="a4816-127">您可能無法在 [價格] 欄位中輸入小數點或逗點。</span><span class="sxs-lookup"><span data-stu-id="a4816-127">You may not be able to enter decimal points or commas in the Price field.</span></span> <span data-ttu-id="a4816-128">若要支援使用逗號 (的非英文地區設定的 jQuery 驗證 &quot; 、 &quot;) 用於小數點和非英文日期格式的非英文地區設定，您必須包含 *globalize.js* 和您的特定 *文化特性/globalize.cultures.js* 檔案 (從 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 和 JavaScript 使用 `Globalize.parseFloat` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-128">To support jQuery validation for non-English locales that use a comma (&quot;,&quot;) for a decimal point, and non US-English date formats, you must include *globalize.js* and your specific *cultures/globalize.cultures.js* file(from [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) and JavaScript to use `Globalize.parseFloat`.</span></span> <span data-ttu-id="a4816-129">我將在下一個教學課程中示範如何進行這項作業。</span><span class="sxs-lookup"><span data-stu-id="a4816-129">I'll show how to do this in the next tutorial.</span></span> <span data-ttu-id="a4816-130">現在，只要輸入如 10 之類的整數。</span><span class="sxs-lookup"><span data-stu-id="a4816-130">For now, just enter whole numbers like 10.</span></span>

<span data-ttu-id="a4816-131">按一下 [ **建立** ] 按鈕，會將表單張貼至伺服器，並在其中將電影資訊儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="a4816-131">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="a4816-132">然後，系統會將您重新導向至 */Movies* URL，您可以在清單中看到新建立的電影。</span><span class="sxs-lookup"><span data-stu-id="a4816-132">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="a4816-133">建立幾個電影項目。</span><span class="sxs-lookup"><span data-stu-id="a4816-133">Create a couple more movie entries.</span></span> <span data-ttu-id="a4816-134">嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="a4816-134">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="a4816-135">檢查產生的程式碼</span><span class="sxs-lookup"><span data-stu-id="a4816-135">Examining the Generated Code</span></span>

<span data-ttu-id="a4816-136">開啟 *Controllers\MoviesController.cs* 檔案，並檢查產生的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="a4816-136">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="a4816-137">具有方法的影片控制器部分 `Index` 如下所示。</span><span class="sxs-lookup"><span data-stu-id="a4816-137">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="a4816-138">對控制器的要求會 `Movies` 傳回資料表中的所有專案 `Movies` ，然後將結果傳遞給 `Index` 視圖。</span><span class="sxs-lookup"><span data-stu-id="a4816-138">A request to the `Movies` controller returns all the entries in the `Movies` table and then passes the results to the `Index` view.</span></span> <span data-ttu-id="a4816-139">類別中的下列程式列會具現 `MoviesController` 化 movie 資料庫內容，如先前所述。</span><span class="sxs-lookup"><span data-stu-id="a4816-139">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="a4816-140">您可以使用 movie 資料庫內容來查詢、編輯和刪除電影。</span><span class="sxs-lookup"><span data-stu-id="a4816-140">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="a4816-141">強型別模型和 @model 關鍵字</span><span class="sxs-lookup"><span data-stu-id="a4816-141">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="a4816-142">稍早在本教學課程中，您已看到控制器如何使用物件將資料或物件傳遞至 view 範本 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-142">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="a4816-143">`ViewBag`是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="a4816-143">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="a4816-144">MVC 也提供將 *強* 型別物件傳遞至 view 範本的能力。</span><span class="sxs-lookup"><span data-stu-id="a4816-144">MVC also provides the ability to pass *strongly* typed objects to a view template.</span></span> <span data-ttu-id="a4816-145">這種強型別方法可讓您在 Visual Studio 編輯器中更妥善的編譯時間檢查程式碼和更豐富的 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="a4816-145">This strongly typed approach enables better compile-time checking of your code and richer [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) in the Visual Studio editor.</span></span> <span data-ttu-id="a4816-146">Visual Studio 中的樣板機制使用這種方法， (也就是在建立方法和瀏覽器時，將 *強* 型別模型) 與 `MoviesController` 類別和視圖範本一起傳遞。</span><span class="sxs-lookup"><span data-stu-id="a4816-146">The scaffolding mechanism in Visual Studio used this approach (that is, passing a *strongly* typed model) with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="a4816-147">在 *Controllers\MoviesController.cs* 檔案中檢查產生的 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="a4816-147">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="a4816-148">`Details`方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="a4816-148">The `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

<span data-ttu-id="a4816-149">`id`參數通常會以路由資料的形式傳遞，例如， `http://localhost:1234/movies/details/1` 會將控制器設定為電影控制器、將動作設定為，並將設定為 `details` `id` 1。</span><span class="sxs-lookup"><span data-stu-id="a4816-149">The `id` parameter is generally passed as route data, for example `http://localhost:1234/movies/details/1` will set the controller to the movie controller, the action to `details` and the `id` to 1.</span></span> <span data-ttu-id="a4816-150">您也可以使用查詢字串傳入識別碼，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4816-150">You could also pass in the id with a query string as follows:</span></span>

`http://localhost:1234/movies/details?id=1`

<span data-ttu-id="a4816-151">如果找到，則會將 `Movie` 模型的實例 `Movie` 傳遞至 `Details` 視圖：</span><span class="sxs-lookup"><span data-stu-id="a4816-151">If a `Movie` is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

<span data-ttu-id="a4816-152">檢查 *Views\Movies\Details.cshtml* 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="a4816-152">Examine the contents of the *Views\Movies\Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

<span data-ttu-id="a4816-153">藉由在「 `@model` 視圖」範本檔案的頂端加入語句，您可以指定該視圖預期的物件類型。</span><span class="sxs-lookup"><span data-stu-id="a4816-153">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="a4816-154">當您建立電影控制器時，Visual Studio 會在 *Details.cshtml* 檔案的最上方自動包含下列 `@model` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="a4816-154">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="a4816-155">這個 `@model` 指示詞可讓您使用強型別的 `Model` 物件，存取控制器傳遞至檢視的電影。</span><span class="sxs-lookup"><span data-stu-id="a4816-155">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="a4816-156">例如，在 [ *詳細資料* ] 範例中，程式碼會將每個 movie 欄位傳遞至 `DisplayNameFor` ，並使用強型別物件 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML helper `Model` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-156">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="a4816-157">`Create`和 `Edit` 方法和 view 範本也會傳遞 movie 模型物件。</span><span class="sxs-lookup"><span data-stu-id="a4816-157">The `Create` and `Edit` methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="a4816-158">檢查 MoviesController.cs 檔案中的*Index. cshtml* view 範本和 `Index` 方法*MoviesController.cs* 。</span><span class="sxs-lookup"><span data-stu-id="a4816-158">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="a4816-159">請注意程式碼在 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` 動作方法中呼叫 helper 方法時，如何建立物件 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-159">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="a4816-160">然後，程式碼會將此 `Movies` 清單從 `Index` 動作方法傳遞至視圖：</span><span class="sxs-lookup"><span data-stu-id="a4816-160">The code then passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

<span data-ttu-id="a4816-161">當您建立電影控制器時，Visual Studio 會自動將下列 `@model` 語句包含在 *Index. cshtml* 檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="a4816-161">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

<span data-ttu-id="a4816-162">這個指示 `@model` 詞可讓您使用強型別的物件，存取控制器傳遞給視圖的電影清單 `Model` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-162">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="a4816-163">例如，在 *Index. cshtml* 範本中，程式碼會藉由對強型別物件執行語句，以迴圈播放影片 `foreach` `Model` ：</span><span class="sxs-lookup"><span data-stu-id="a4816-163">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="a4816-164">因為 `Model` 物件是強型別 (為 `IEnumerable<Movie>` 物件) ，所以 `item` 迴圈中的每個物件都會輸入為 `Movie` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-164">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="a4816-165">除了其他優點之外，這表示您可以在程式碼編輯器中取得程式碼和完整 IntelliSense 支援的編譯時期檢查：</span><span class="sxs-lookup"><span data-stu-id="a4816-165">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="a4816-167">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="a4816-167">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="a4816-168">Entity Framework Code First 偵測到提供的資料庫連接字串已指向 `Movies` 尚未存在的資料庫，所以 Code First 自動建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a4816-168">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="a4816-169">您可以藉由查看 *應用程式 \_ 資料* 資料夾來確認它是否已建立。</span><span class="sxs-lookup"><span data-stu-id="a4816-169">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="a4816-170">如果看不到 *.mdf*檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開 [*應用程式 \_ 資料*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="a4816-170">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png)

<span data-ttu-id="a4816-171">按兩下 [ *.Mdf* ] 以開啟 [ **伺服器瀏覽器**]，然後展開 [ **資料表]** 資料夾以查看 [電影] 資料表。</span><span class="sxs-lookup"><span data-stu-id="a4816-171">Double-click *Movies.mdf* to open **SERVER EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span> <span data-ttu-id="a4816-172">請注意 [識別碼] 旁邊的按鍵圖示。</span><span class="sxs-lookup"><span data-stu-id="a4816-172">Note the key icon next to ID.</span></span> <span data-ttu-id="a4816-173">根據預設，EF 會將名為 ID 的屬性設為主鍵。</span><span class="sxs-lookup"><span data-stu-id="a4816-173">By default, EF will make a property named ID the primary key.</span></span> <span data-ttu-id="a4816-174">如需 EF 和 MVC 的詳細資訊，請參閱 Tom Dykstra 在 [MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)上的絕佳教學課程。</span><span class="sxs-lookup"><span data-stu-id="a4816-174">For more information on EF and MVC, see Tom Dykstra's excellent tutorial on [MVC and EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="a4816-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="a4816-175">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")</span></span>

<span data-ttu-id="a4816-176">以滑鼠右鍵按一下 `Movies` 資料表，然後選取 [ **顯示資料表資料** ] 以查看您所建立的資料。</span><span class="sxs-lookup"><span data-stu-id="a4816-176">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

<span data-ttu-id="a4816-177">以滑鼠右鍵按一下 `Movies` 資料表，然後選取 [ **開啟資料表定義** ]，以查看 Entity Framework Code First 為您建立的資料表結構。</span><span class="sxs-lookup"><span data-stu-id="a4816-177">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

<span data-ttu-id="a4816-178">請注意資料表的架構如何 `Movies` 對應至您稍 `Movie` 早建立的類別。</span><span class="sxs-lookup"><span data-stu-id="a4816-178">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="a4816-179">Entity Framework Code First 會根據您的類別自動建立此架構 `Movie` 。</span><span class="sxs-lookup"><span data-stu-id="a4816-179">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="a4816-180">當您完成時，請以滑鼠右鍵按一下 [ *MovieDBCoNtext* ] 並選取 [ **關閉連接**] 來關閉連接。</span><span class="sxs-lookup"><span data-stu-id="a4816-180">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="a4816-181"> (如果您未關閉連線，下次執行專案時，可能會收到錯誤) 。</span><span class="sxs-lookup"><span data-stu-id="a4816-181">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

<span data-ttu-id="a4816-182">您現在擁有一個資料庫和多個頁面，可用來顯示、編輯、更新和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="a4816-182">You now have a database and pages to display, edit, update and delete data.</span></span> <span data-ttu-id="a4816-183">在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` `SearchIndex` 可讓您在此資料庫中搜尋電影的方法和觀點。</span><span class="sxs-lookup"><span data-stu-id="a4816-183">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span> <span data-ttu-id="a4816-184">如需搭配 MVC 使用 Entity Framework 的詳細資訊，請參閱為 [ASP.NET MVC 應用程式建立 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="a4816-184">For more information on using Entity Framework with MVC, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4816-185">[上一個](creating-a-connection-string.md) 
> [下一步](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="a4816-185">[Previous](creating-a-connection-string.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
