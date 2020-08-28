---
title: 將視圖新增至 MVC 應用程式
author: Rick-Anderson
description: 將視圖新增至 MVC 應用程式
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045009"
---
# <a name="adding-a-view"></a><span data-ttu-id="6f2a0-103">新增檢視</span><span class="sxs-lookup"><span data-stu-id="6f2a0-103">Adding a View</span></span>

<span data-ttu-id="6f2a0-104">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6f2a0-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="6f2a0-105">在這一節中，您將修改 `HelloWorldController` 類別以使用「查看範本」檔案，將產生 HTML 回應的程式完全封裝到用戶端。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="6f2a0-106">您將使用 [Razor view 引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)來建立 view 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="6f2a0-107">Razor 型視圖範本的副檔名為 *cshtml* ，並提供使用 c # 建立 HTML 輸出的簡潔方式。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="6f2a0-108">Razor 可將撰寫視圖範本時所需的字元數和按鍵次數降到最低，並啟用快速、流暢的編碼工作流程。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="6f2a0-109">目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="6f2a0-110">將 `Index` 方法變更為呼叫控制器 [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) 方法，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="6f2a0-110">Change the `Index` method to call the controllers [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) method, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="6f2a0-111">`Index`上述方法會使用 view 範本來產生瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="6f2a0-112">控制器方法 (也稱為 [動作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)) （例如 `Index` 上述方法）通常會傳回 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (或衍生自 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)) 的類別，而不是字串之類的基本類型。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="6f2a0-113">以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，然後按一下 [ **新增**]，再按一下 [ \*\*具有版面配置的 MVC 5 視圖頁面] (Razor) \*\*。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="6f2a0-114">在 [ **指定專案的名稱** ] 對話方塊中，輸入 [ *索引*]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="6f2a0-115">在 [**選取版面配置頁面**] 對話方塊中，接受預設的\*\* \_ Layout\*\* ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="6f2a0-116">在上圖中，已選取左窗格中的 [ *Views\Shared* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="6f2a0-117">如果您在另一個資料夾中有自訂的版面配置檔案，您可以選取它。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="6f2a0-118">我們稍後會在本教學課程中討論版面配置檔案</span><span class="sxs-lookup"><span data-stu-id="6f2a0-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="6f2a0-119">*MvcMovie\Views\HelloWorld\Index.cshtml*檔案會建立。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="6f2a0-120">新增下列反白顯示的標記。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="6f2a0-121">以滑鼠右鍵按一下 [ *Index* ]，然後 **在 [瀏覽器] 中**選取 [View]。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="6f2a0-123">您也可以用滑鼠右鍵按一下 [*索引*]，然後選取**Page Inspector 中**的 [View]。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="6f2a0-124">如需詳細資訊，請參閱 [Page Inspector 教學](../../views/using-page-inspector-in-aspnet-mvc.md) 課程。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="6f2a0-125">或者，執行應用程式並流覽至 `HelloWorld` 控制器 (`http://localhost:xxxx/HelloWorld`) 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="6f2a0-126">`Index`您控制器中的方法不會執行太多工作，而只是執行語句 `return View()` ，這會指定方法應該使用 view 範本檔案來呈現瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="6f2a0-127">因為您未明確指定要使用的視圖範本檔案名，ASP.NET MVC 預設為使用 \Views\HelloWorld 資料夾中的*\Views\HelloWorld*資料夾中的*Index. cshtml* view 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="6f2a0-128">下圖顯示 &quot; 來自我們的視圖範本的字串 Hello！ &quot; 在視圖中進行硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="6f2a0-129">看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-129">Looks pretty good.</span></span> <span data-ttu-id="6f2a0-130">不過請注意，瀏覽器的標題列會顯示「索引-我的 ASP.NET 應用程式」，而頁面頂端的大連結則顯示「應用程式名稱」。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-130">However, notice that the browser's title bar shows "Index - My ASP.NET Application," and the big link at the top of the page says "Application name."</span></span> <span data-ttu-id="6f2a0-131">根據您瀏覽器視窗的大小，您可能需要按一下右上方的三個橫條，才能看到 **首頁**、 **About**、 **Contact**、 **Register** 和 **登入** 連結。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="6f2a0-132">變更視圖和版面配置頁面</span><span class="sxs-lookup"><span data-stu-id="6f2a0-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="6f2a0-133">首先，您想要變更 &quot; 頁面頂端的應用程式名稱 &quot; 連結。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="6f2a0-134">該文字在每個頁面中都是通用的。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-134">That text is common to every page.</span></span> <span data-ttu-id="6f2a0-135">它其實只會在專案中的一個位置進行，即使它出現在應用程式的每個頁面上也一樣。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="6f2a0-136">移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 [配置檔] \* \_ 。\*</span><span class="sxs-lookup"><span data-stu-id="6f2a0-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="6f2a0-137">這個檔案稱為版面配置 *頁面* ，它位於所有其他頁面使用的共用資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="6f2a0-139">版面配置範本可讓您在某個位置指定網站的 HTML 容器配置，然後將它套用到網站中的多個頁面。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="6f2a0-140">找到 `@RenderBody()` 這行。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="6f2a0-141">`RenderBody` 是顯示您建立之所有檢視特定頁面的預留位置，「包裝」&quot;&quot;在版面配置頁中。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="6f2a0-142">例如，如果您選取 [ **關於** ] 連結，則會在方法內轉譯 *Views\Home\About.cshtml* view `RenderBody` 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="6f2a0-143">變更標題元素的內容。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-143">Change the contents of the title element.</span></span> <span data-ttu-id="6f2a0-144">將版面配置 [範本中的](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) [從 &quot; 應用程式名稱] 變更 &quot; 為 [ &quot; MVC 電影] &quot; ，並將控制器從變更 `Home` 為 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-144">Change the [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="6f2a0-145">完整的版面配置檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f2a0-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="6f2a0-146">執行應用程式，並注意它現在會顯示 &quot; MVC 電影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="6f2a0-147">按一下 [ **關於** ] 連結，您也會看到該頁面如何顯示 &quot; MVC 電影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="6f2a0-148">我們可以在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="6f2a0-149">當我們先建立 *Views\HelloWorld\Index.cshtml* 檔案時，它會包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f2a0-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="6f2a0-150">上述的 Razor 程式碼會明確地設定版面配置頁面。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="6f2a0-151">檢查 *Views \\ _ViewStart cshtml* 檔案，其中包含完全相同的 Razor 標記。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="6f2a0-152">*[Views \\ _ViewStart 的 views](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 檔案會定義所有視圖都將使用的一般配置，因此您可以將該程式碼從*Views\HelloWorld\Index.cshtml*檔中批註出來或移除。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="6f2a0-153">您可以使用 `Layout` 屬性來設定不同的版面配置檢視，或將它設定為 `null`，因此不會使用任何版面配置檔案。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="6f2a0-154">現在，讓我們來變更索引視圖的標題。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="6f2a0-155">開啟 *MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="6f2a0-156">有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後在第二個標頭中 (`<h2>` 元素) 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="6f2a0-157">您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="6f2a0-158">為了指出要顯示的 HTML 標題，上述程式碼會設定 `Title` 物件 (的屬性，該 `ViewBag` 物件位於 *Index. cshtml* view 範本) 中。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="6f2a0-159">請注意，配置範本 ( *Views\Shared \\ _Layout. cshtml* ) 會使用專案中的這個值， `<title>` 做為 `<head>` 我們先前修改過之 HTML 區段的一部分。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="6f2a0-160">使用這 `ViewBag` 種方法，您可以輕鬆地在您的視圖範本和版面配置檔案之間傳遞其他參數。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="6f2a0-161">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-161">Run the application.</span></span> <span data-ttu-id="6f2a0-162">請注意，瀏覽器標題、主要標題和次要標題已變更</span><span class="sxs-lookup"><span data-stu-id="6f2a0-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="6f2a0-163">(如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="6f2a0-164">在您的瀏覽器中按 Ctrl + F5，以強制載入來自伺服器的回應。 ) 瀏覽器標題是以 `ViewBag.Title` 我們在*Index. cshtml* view 範本中所設定的，以及在版面配置檔案 &quot; 中新增的其他電影應用程式所建立。 &quot;</span><span class="sxs-lookup"><span data-stu-id="6f2a0-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="6f2a0-165">另外也請注意， *Index. cshtml* view 範本中的內容如何與\* \_ Layout\* view 範本合併，並將單一 HTML 回應傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="6f2a0-166">版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="6f2a0-167">&quot;這就是我們的一些資料 &quot; (在此情況下 &quot; ，我們的視圖範本的 Hello！ &quot; message) 是硬式編碼的。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="6f2a0-168">MVC 應用程式有一個 &quot; V &quot; (view) 而且您有 &quot; C &quot; (控制器) ，但是沒有任何 &quot; M &quot; (模型) 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="6f2a0-169">不久之後，我們將逐步解說如何建立資料庫，並從中取出模型資料。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-169">Shortly, we'll walk through how to create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="6f2a0-170">將資料從控制器傳遞至檢視</span><span class="sxs-lookup"><span data-stu-id="6f2a0-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="6f2a0-171">在我們移至資料庫並討論模型之前，讓我們先討論如何從控制器將資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="6f2a0-172">系統會叫用控制器類別以回應傳入的 URL 要求。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="6f2a0-173">控制器類別可讓您撰寫程式碼來處理傳入瀏覽器要求、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="6f2a0-174">然後，您可以從控制器使用 View 範本，以產生並格式化瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="6f2a0-175">控制器會負責提供所需的資料或物件，讓「視圖」範本能夠呈現瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="6f2a0-176">最佳做法：「 **視圖」範本永遠不應該執行商務邏輯，或直接與資料庫互動**。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="6f2a0-177">相反地，「視圖」範本應該只適用于控制器提供給它的資料。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="6f2a0-178">維護這 &quot; 項考慮會 &quot; 讓您的程式碼保持乾淨、可測試且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="6f2a0-179">目前， `Welcome` 類別中的動作方法 `HelloWorldController` 會接受 `name` 和參數，然後將 `numTimes` 值直接輸出至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="6f2a0-180">讓控制器改為使用 view 範本，而不是讓控制器將此回應轉譯為字串。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="6f2a0-181">檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="6f2a0-182">若要這麼做，您可以讓控制器將動態資料放 (參數，) 視圖範本在可存取的物件中所需的資料 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="6f2a0-183">返回 *HelloWorldController.cs* 檔案並變更 `Welcome` 方法，以將 `Message` 和值加入 `NumTimes` 至 `ViewBag` 物件。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="6f2a0-184">`ViewBag` 是動態物件，這表示您可以在其中放置任何您想要的內容; `ViewBag` 除非您將某個內容放在其中，否則物件沒有定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="6f2a0-185">[ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將 (和) 的具名引數， `name` `numTimes` 從網址列中的查詢字串對應到您方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="6f2a0-186">完整的 *HelloWorldController.cs* 檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f2a0-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="6f2a0-187">現在 `ViewBag` 物件包含將會自動傳遞給視圖的資料。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="6f2a0-188">接下來，您需要一個歡迎使用的視圖範本！</span><span class="sxs-lookup"><span data-stu-id="6f2a0-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="6f2a0-189">在 [ **組建** ] 功能表中，選取 [ **組建方案** (] 或 [Ctrl + Shift + B]) 以確定專案已編譯。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="6f2a0-190">以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，然後按一下 [ **新增**]，再按一下 [ \*\*具有版面配置的 MVC 5 視圖頁面] (Razor) \*\*。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="6f2a0-191">在 [ **指定專案的名稱** ] 對話方塊中，輸入 [ *歡迎使用*]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="6f2a0-192">在 [**選取版面配置頁面**] 對話方塊中，接受預設的\*\* \_ Layout\*\* ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="6f2a0-193">*MvcMovie\Views\HelloWorld\Welcome.cshtml*檔案會建立。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="6f2a0-194">取代 *歡迎的 cshtml* 檔案中的標記。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="6f2a0-195">您將會建立一個迴圈，並以 &quot; &quot; 使用者指出的次數來顯示 Hello。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="6f2a0-196">完整的 *歡迎* 檔如下所示。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="6f2a0-197">執行應用程式，並流覽至下列 URL：</span><span class="sxs-lookup"><span data-stu-id="6f2a0-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="6f2a0-198">現在會從 URL 取得資料，並使用 [模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結器將資料傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="6f2a0-199">控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="6f2a0-200">然後，此視圖會將資料顯示為使用者的 HTML。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="6f2a0-201">在上述範例中，我們使用了 `ViewBag` 物件將資料從控制器傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="6f2a0-202">稍後在教學課程中，我們將使用檢視模型將控制器中的資料傳遞至檢視。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="6f2a0-203">傳遞資料的視圖模型方法通常比查看包方法更慣用。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="6f2a0-204">如需詳細資訊，請參閱 blog 專案 [動態型強](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 型別查看。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="6f2a0-205">這是 &quot; 模型的 M 類型 &quot; ，但不是資料庫種類。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="6f2a0-206">讓我們運用所學的內容，建立電影的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f2a0-206">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f2a0-207">[上一個](adding-a-controller.md) 
> [下一步](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="6f2a0-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
