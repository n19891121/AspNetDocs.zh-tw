---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: ae3258872df798f52d8e031dc8ebf01b4f0a7358
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045126"
---
# <a name="adding-a-controller"></a><span data-ttu-id="bdbce-102">新增控制器</span><span class="sxs-lookup"><span data-stu-id="bdbce-102">Adding a Controller</span></span>

<span data-ttu-id="bdbce-103">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bdbce-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="bdbce-104">MVC 代表 *模型-視圖控制器*。</span><span class="sxs-lookup"><span data-stu-id="bdbce-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="bdbce-105">MVC 是一種模式，用來開發妥善架構、可測試且容易維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbce-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="bdbce-106">以 MVC 為基礎的應用程式包含：</span><span class="sxs-lookup"><span data-stu-id="bdbce-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="bdbce-107">**M** ) ：代表應用程式資料的類別，以及使用驗證邏輯來強制執行該資料之商務規則的類別。</span><span class="sxs-lookup"><span data-stu-id="bdbce-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="bdbce-108">**V** >v) ：您的應用程式用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="bdbce-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="bdbce-109">**C** ) ：處理傳入瀏覽器要求的類別、取出模型資料，然後指定將回應傳回給瀏覽器的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="bdbce-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="bdbce-110">我們將在本教學課程系列中涵蓋這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbce-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="bdbce-111">讓我們從建立控制器類別開始。</span><span class="sxs-lookup"><span data-stu-id="bdbce-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="bdbce-112">在 **方案總管**中，以滑鼠右鍵按一下 [ *控制器* ] 資料夾，然後按一下 [ **新增**]，然後按一下 [ **控制器**]。</span><span class="sxs-lookup"><span data-stu-id="bdbce-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="bdbce-113">在 [ **新增 Scaffold** ] 對話方塊中，按一下 [ **MVC 5 控制器-空白**]，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="bdbce-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="bdbce-114">將新控制器命名為 ">helloworldcontroller.cs"，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="bdbce-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![新增控制器](adding-a-controller/_static/image3.png)

<span data-ttu-id="bdbce-116">請注意， **方案總管** 已建立名為 *HelloWorldController.cs* 的新檔案和新的資料夾 *Views\HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="bdbce-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="bdbce-117">控制器已在 IDE 中開啟。</span><span class="sxs-lookup"><span data-stu-id="bdbce-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="bdbce-118">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="bdbce-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="bdbce-119">控制器方法會傳回 HTML 字串作為範例。</span><span class="sxs-lookup"><span data-stu-id="bdbce-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="bdbce-120">控制器命名為 `HelloWorldController` ，第一個方法名為 `Index` 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="bdbce-121">讓我們從瀏覽器叫用它。</span><span class="sxs-lookup"><span data-stu-id="bdbce-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="bdbce-122">執行應用程式 (按 F5 或 Ctrl + F5) 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="bdbce-123">在瀏覽器中，將 &quot; HelloWorld 附加 &quot; 至網址列中的路徑。</span><span class="sxs-lookup"><span data-stu-id="bdbce-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="bdbce-124"> (例如，在下圖中， `http://localhost:1234/HelloWorld.`) 瀏覽器中的頁面看起來會像下列螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="bdbce-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="bdbce-125">在上述方法中，程式碼會直接傳回字串。</span><span class="sxs-lookup"><span data-stu-id="bdbce-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="bdbce-126">您已告訴系統只傳回一些 HTML，而且的確是！</span><span class="sxs-lookup"><span data-stu-id="bdbce-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="bdbce-127">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別 (以及它們內的不同動作方法) 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="bdbce-128">ASP.NET MVC 使用的預設 URL 路由邏輯會使用如下的格式來判斷要叫用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="bdbce-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="bdbce-129">您可以在 *應用程式 \_ 啟動/>start\routeconfig.cs .cs* 檔案中設定路由的格式。</span><span class="sxs-lookup"><span data-stu-id="bdbce-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="bdbce-130">當您執行應用程式但未提供任何 URL 區段時，它會預設為在上述程式碼的 [預設值] 區段中指定的 "Home" 控制器和 "Index" 動作方法。</span><span class="sxs-lookup"><span data-stu-id="bdbce-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="bdbce-131">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="bdbce-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="bdbce-132">因此， */HelloWorld* 會對應到 `HelloWorldController` 類別。</span><span class="sxs-lookup"><span data-stu-id="bdbce-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="bdbce-133">URL 的第二個部分會決定要執行之類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="bdbce-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="bdbce-134">因此， */HelloWorld/Index* 會讓 `Index` 類別的方法 `HelloWorldController` 執行。</span><span class="sxs-lookup"><span data-stu-id="bdbce-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="bdbce-135">請注意，我們只需要流覽至 */HelloWorld* ，而且 `Index` 預設會使用方法。</span><span class="sxs-lookup"><span data-stu-id="bdbce-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="bdbce-136">這是因為名為的方法 `Index` 是預設方法，如果未明確指定，就會在控制器上呼叫它。</span><span class="sxs-lookup"><span data-stu-id="bdbce-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="bdbce-137">URL 區段的第三個部分 (`Parameters`) 是路由資料。</span><span class="sxs-lookup"><span data-stu-id="bdbce-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="bdbce-138">我們稍後會在本教學課程中看到路由資料。</span><span class="sxs-lookup"><span data-stu-id="bdbce-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="bdbce-139">瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="bdbce-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="bdbce-140">`Welcome`方法會執行並傳回字串， &quot; 此為歡迎動作方法 ... &quot; 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="bdbce-141">預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]` 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="bdbce-142">在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。</span><span class="sxs-lookup"><span data-stu-id="bdbce-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="bdbce-143">您尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="bdbce-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="bdbce-144">讓我們稍微修改範例，讓您可以將 URL 中的一些參數資訊傳遞給控制器 (例如， */HelloWorld/Welcome？ name = Scott &amp; numtimes is = 4*) 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="bdbce-145">變更您的 `Welcome` 方法以包含兩個參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="bdbce-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="bdbce-146">請注意，程式碼會使用 c # 選擇性參數功能，指出 `numTimes` 如果沒有針對該參數傳遞任何值，參數應該預設為1。</span><span class="sxs-lookup"><span data-stu-id="bdbce-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="bdbce-147">安全性注意事項：上述程式碼會使用 [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) 來保護應用程式免于遭受惡意輸入 (亦即 JavaScript) 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="bdbce-148">如需詳細資訊，請參閱 [如何：將 HTML 編碼套用至字串，以防止 Web 應用程式中的腳本](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)惡意探索。</span><span class="sxs-lookup"><span data-stu-id="bdbce-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="bdbce-149">執行您的應用程式，並流覽至範例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="bdbce-150">您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。</span><span class="sxs-lookup"><span data-stu-id="bdbce-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="bdbce-151">[ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會將指定的參數從網址列中的查詢字串，自動對應到您方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="bdbce-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="bdbce-152">在上述範例中， `Parameters` 不會使用 URL 區段 () ， `name` 而且會將和 `numTimes` 參數當做 [查詢字串](http://en.wikipedia.org/wiki/Query_string)傳遞。</span><span class="sxs-lookup"><span data-stu-id="bdbce-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="bdbce-153">？</span><span class="sxs-lookup"><span data-stu-id="bdbce-153">The ?</span></span> <span data-ttu-id="bdbce-154">上述 URL 中的 (問號) 是分隔符號，而查詢字串接下來。</span><span class="sxs-lookup"><span data-stu-id="bdbce-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="bdbce-155">&amp; 字元可分隔查詢字串。</span><span class="sxs-lookup"><span data-stu-id="bdbce-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="bdbce-156">以下列程式碼取代歡迎方法：</span><span class="sxs-lookup"><span data-stu-id="bdbce-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="bdbce-157">執行應用程式，並輸入下列 URL： `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="bdbce-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="bdbce-158">這一次，第三個 URL 區段符合路由參數， `ID.` `Welcome` 動作方法包含的參數 (`ID`) 符合方法中的 URL 規格 `RegisterRoutes` 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="bdbce-159">在 ASP.NET MVC 應用程式中，以路由資料的形式傳遞參數更為常見， (像我們在) 以上的識別碼，而不是將它們當作查詢字串傳遞。</span><span class="sxs-lookup"><span data-stu-id="bdbce-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="bdbce-160">您也可以新增路由，以將 `name` 和 `numtimes` in 參數傳遞為 URL 中的路由資料。</span><span class="sxs-lookup"><span data-stu-id="bdbce-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="bdbce-161">在 *應用程式 \_ Start\RouteConfig.cs* 檔中，新增 "Hello" 路由：</span><span class="sxs-lookup"><span data-stu-id="bdbce-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="bdbce-162">執行應用程式，並流覽至 `/localhost:XXX/HelloWorld/Welcome/Scott/3` 。</span><span class="sxs-lookup"><span data-stu-id="bdbce-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="bdbce-163">對於許多 MVC 應用程式來說，預設路由會正常運作。</span><span class="sxs-lookup"><span data-stu-id="bdbce-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="bdbce-164">您稍後會在本教學課程中瞭解如何使用模型系結器來傳遞資料，而您不需要修改該的預設路由。</span><span class="sxs-lookup"><span data-stu-id="bdbce-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="bdbce-165">在這些範例中，控制器已執行 &quot; MVC 的 VC &quot; 部分（也就是，view 和 controller 工作）。</span><span class="sxs-lookup"><span data-stu-id="bdbce-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="bdbce-166">控制器會直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="bdbce-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="bdbce-167">一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。</span><span class="sxs-lookup"><span data-stu-id="bdbce-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="bdbce-168">相反地，我們通常會使用個別的 view 範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="bdbce-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="bdbce-169">接下來讓我們來看看如何進行。</span><span class="sxs-lookup"><span data-stu-id="bdbce-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bdbce-170">[上一個](getting-started.md) 
> [下一步](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="bdbce-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
