---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和檢視實現清單/詳細資訊 UI |微軟文件
author: rick-anderson
description: 步驟 4 展示如何向應用程式添加控制器,該應用程式利用我們的模型為使用者提供數據清單/詳細資訊導航體驗...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541308"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="ba5dd-103">使用控制器和檢視來實作清單/詳細資料 UI</span><span class="sxs-lookup"><span data-stu-id="ba5dd-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="ba5dd-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ba5dd-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ba5dd-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="ba5dd-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ba5dd-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第4步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ba5dd-107">步驟 4 演示如何向應用程式添加控制器,該應用程式利用我們的模型為使用者提供在 NerdDinner 網站上晚餐的數據列表/詳細資訊導航體驗。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="ba5dd-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="ba5dd-109">神經晚餐步驟 4:控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="ba5dd-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="ba5dd-110">對於傳統的 Web 框架(經典 ASP、PHP、ASP.NET Web 窗體等),傳入 URL 通常映射到磁碟上的檔。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="ba5dd-111">例如:諸如"/Products.aspx"或"/Products.php"這樣的 URL 請求可能由"Products.aspx"或"Products.php"檔處理。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="ba5dd-112">基於 Web 的 MVC 框架以略有不同的方式將 URL 映射到伺服器代碼。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="ba5dd-113">它們不是將傳入 URL 映射到檔,而是將 URL 映射到類上的方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="ba5dd-114">這些類稱為"控制器",它們負責處理傳入的 HTTP 請求、處理使用者輸入、檢索和保存數據以及確定要發送回用戶端的回應(顯示 HTML、下載檔、重定向到其他 URL 等)。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="ba5dd-115">現在,我們已經為我們的NerdDinner應用程式建立了基本模型,我們的下一步將是向應用程式添加一個控制器,利用它為使用者提供我們網站上的 Dinner 的數據列表/詳細資訊導航體驗。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="ba5dd-116">新增晚餐控制器控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="ba5dd-117">我們將從右鍵單擊 Web 專案中的「控制器」資料夾開始,然後選擇 **「新增-&gt;控制器」** 選單命令(您也可以通過鍵入 Ctrl-M、Ctrl-C 來執行此指令):</span><span class="sxs-lookup"><span data-stu-id="ba5dd-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="ba5dd-118">這會彈出「新增控制器」對話框:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="ba5dd-119">我們將命名新的控制器「DinnersController」,然後單擊「添加」按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="ba5dd-120">然後,Visual Studio 將在我們的 @控制器目錄下添加DinnersController.cs檔:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="ba5dd-121">它還將在代碼編輯器中打開新的 DinnersController 類。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="ba5dd-122">新增一個晚餐控制器類別</span><span class="sxs-lookup"><span data-stu-id="ba5dd-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="ba5dd-123">我們希望讓使用我們的應用程式的訪問者流覽即將舉辦的晚宴清單,並允許他們點擊清單中的任何晚餐以查看有關此晚餐的具體細節。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="ba5dd-124">我們將透過發佈應用程式的以下網址執行此操作:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="ba5dd-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-125">**URL**</span></span> | <span data-ttu-id="ba5dd-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="ba5dd-127">*/晚餐/*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-127">*/Dinners/*</span></span> | <span data-ttu-id="ba5dd-128">顯示即將來臨的晚宴的 HTML 清單</span><span class="sxs-lookup"><span data-stu-id="ba5dd-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="ba5dd-129">*/晚餐/詳情/[id]*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="ba5dd-130">顯示網址 中嵌入的「id」參數指示的特定晚餐的詳細資訊, 這將與資料庫中的晚餐 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="ba5dd-131">例如:/Dinners/詳細資訊/2 將顯示一個 HTML 頁面,其中詳細介紹了晚餐 ID 值為 2 的晚餐。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="ba5dd-132">我們將通過向 DinnersController 類中添加兩種公共「操作方法」來發佈這些 URL 的初始實現,如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="ba5dd-133">然後,我們將運行NerdDinner應用程式,並使用我們的瀏覽器來調用它們。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="ba5dd-134">鍵入 *「/Dinners/」URL*將導致我們的*Index()* 方法執行,並且它將發送回以下回應:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="ba5dd-135">鍵入 *"/晚餐/詳細資訊/2"URL*將導致運行*我們的詳細資訊()* 方法,併發送回以下回應:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="ba5dd-136">您可能想知道 - ASP.NET MVC 如何知道創建我們的 DinnersController 類並調用這些方法?</span><span class="sxs-lookup"><span data-stu-id="ba5dd-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="ba5dd-137">為了理解這一點,讓我們快速瞭解路由的工作原理。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="ba5dd-138">瞭解ASP.NET MVC 路由</span><span class="sxs-lookup"><span data-stu-id="ba5dd-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="ba5dd-139">ASP.NET MVC 包含強大的 URL 路由引擎,在控制 URL 如何映射到控制器類方面提供了很大的靈活性。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="ba5dd-140">它允許我們完全自定義ASP.NET MVC 如何選擇要建立的控制器類、調用哪種方法,以及配置不同的方式,以便變數可以從 URL/Querystring 自動解析並傳遞給方法作為參數參數。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="ba5dd-141">它提供了靈活性,完全優化了SEO網站(搜尋引擎優化),以及發佈任何我們想要從應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="ba5dd-142">默認情況下,新的ASP.NET MVC 專案附帶一組已註冊的 URL 路由規則。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="ba5dd-143">這使我們能夠輕鬆啟動應用程式,而無需顯式配置任何內容。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="ba5dd-144">預設路由規則註冊可以在專案的「應用程式」類別中找到, 我們可以透過按兩下專案根目錄中的「Global.asax」檔案來開啟:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="ba5dd-145">預設ASP.NET MVC 路由規則在此類的「註冊路由」方法中註冊:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="ba5dd-146">"路線。上面的 MapRoute()方法調用註冊了一個預設路由規則,該規則使用 URL 格式將傳入 URL 映射到控制器類:"//{控制器}/{{{操作}/{id}" - 其中"控制器"是要實例化的控制器類的名稱,"操作"是要調用它的公共方法的名稱,"id"是嵌入在 URL 中的可選參數,可以作為參數傳遞給該方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="ba5dd-147">傳遞給"MapRoute()"方法調用的第三個參數是一組預設值,用於在 URL 中不存在的控制器/操作/id 值(控制器 = "Home",操作 ="索引",Id=")。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="ba5dd-148">下面是一個表,演示如何使用預設的<em>"//控制器\/{操作}/{id}"</em>路由規則映射各種 URL:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="ba5dd-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-149">**URL**</span></span> | <span data-ttu-id="ba5dd-150">**控制器類**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-150">**Controller Class**</span></span> | <span data-ttu-id="ba5dd-151">**動作方法**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-151">**Action Method**</span></span> | <span data-ttu-id="ba5dd-152">**傳遞的參數**</span><span class="sxs-lookup"><span data-stu-id="ba5dd-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba5dd-153">*/晚餐/細節/2*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="ba5dd-154">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-154">DinnersController</span></span> | <span data-ttu-id="ba5dd-155">詳細資訊(ID)</span><span class="sxs-lookup"><span data-stu-id="ba5dd-155">Details(id)</span></span> | <span data-ttu-id="ba5dd-156">id=2</span><span class="sxs-lookup"><span data-stu-id="ba5dd-156">id=2</span></span> |
| <span data-ttu-id="ba5dd-157">*/晚餐/編輯/5*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="ba5dd-158">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-158">DinnersController</span></span> | <span data-ttu-id="ba5dd-159">編輯(ID)</span><span class="sxs-lookup"><span data-stu-id="ba5dd-159">Edit(id)</span></span> | <span data-ttu-id="ba5dd-160">id=5</span><span class="sxs-lookup"><span data-stu-id="ba5dd-160">id=5</span></span> |
| <span data-ttu-id="ba5dd-161">*/晚餐/創建*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-161">*/Dinners/Create*</span></span> | <span data-ttu-id="ba5dd-162">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-162">DinnersController</span></span> | <span data-ttu-id="ba5dd-163">Create()</span><span class="sxs-lookup"><span data-stu-id="ba5dd-163">Create()</span></span> | <span data-ttu-id="ba5dd-164">N/A</span><span class="sxs-lookup"><span data-stu-id="ba5dd-164">N/A</span></span> |
| <span data-ttu-id="ba5dd-165">*/晚餐*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-165">*/Dinners*</span></span> | <span data-ttu-id="ba5dd-166">晚餐控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-166">DinnersController</span></span> | <span data-ttu-id="ba5dd-167">索引()</span><span class="sxs-lookup"><span data-stu-id="ba5dd-167">Index()</span></span> | <span data-ttu-id="ba5dd-168">N/A</span><span class="sxs-lookup"><span data-stu-id="ba5dd-168">N/A</span></span> |
| <span data-ttu-id="ba5dd-169">*/首頁*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-169">*/Home*</span></span> | <span data-ttu-id="ba5dd-170">家用控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-170">HomeController</span></span> | <span data-ttu-id="ba5dd-171">索引()</span><span class="sxs-lookup"><span data-stu-id="ba5dd-171">Index()</span></span> | <span data-ttu-id="ba5dd-172">N/A</span><span class="sxs-lookup"><span data-stu-id="ba5dd-172">N/A</span></span> |
| */* | <span data-ttu-id="ba5dd-173">家用控制器</span><span class="sxs-lookup"><span data-stu-id="ba5dd-173">HomeController</span></span> | <span data-ttu-id="ba5dd-174">索引()</span><span class="sxs-lookup"><span data-stu-id="ba5dd-174">Index()</span></span> | <span data-ttu-id="ba5dd-175">N/A</span><span class="sxs-lookup"><span data-stu-id="ba5dd-175">N/A</span></span> |

<span data-ttu-id="ba5dd-176">最後三行顯示正在使用的預設值(控制器 = 主頁、操作 + 索引、ID ="")。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="ba5dd-177">由於「Index」方法註冊為預設操作名稱(如果未指定),因此「/Dinners」和「/home」URL 會導致在其控制器類上調用 Index() 操作方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="ba5dd-178">由於"Home"控制器在未指定時註冊為預設控制器,因此"/" URL會導致創建 HomeController,並調用其上的索引() 操作方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="ba5dd-179">如果您不喜歡這些預設 URL 路由規則,好消息是它們很容易更改 - 只需在上面的註冊路由方法中編輯它們即可。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="ba5dd-180">但是,對於我們的NerdDinner應用程式,我們不會更改任何預設URL路由規則,而只是將它們作為本操作使用。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="ba5dd-181">使用我們的晚餐控制器的晚餐儲存庫</span><span class="sxs-lookup"><span data-stu-id="ba5dd-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="ba5dd-182">現在,讓我們用使用我們的模型的實現替換當前對 DinnersController Index() 和詳細資訊()操作方法的實現。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="ba5dd-183">我們將使用之前構建的 DinnerRepository 類來實現該行為。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="ba5dd-184">我們將首先添加一個"使用"語句,該語句引用"NerdDinner.Model"命名空間,然後聲明我們的 DinnerRepository 的實例作為 DinnerController 類上的字段。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="ba5dd-185">在本章的後面部分,我們將介紹"依賴注入"的概念,並展示我們的控制器獲取對 DinnerRepository 的引用的另一種方法,該存儲庫可實現更好的單元測試 -但現在,我們將創建一個類似於下面的 DinnerRepository 內聯實例。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="ba5dd-186">現在,我們準備使用檢索到的數據模型物件生成 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="ba5dd-187">將檢視與我們的控制器一起使用</span><span class="sxs-lookup"><span data-stu-id="ba5dd-187">Using Views with our Controller</span></span>

<span data-ttu-id="ba5dd-188">雖然可以在我們的操作方法中編寫代碼來組裝 HTML,然後使用*Response.Write()* 説明器方法將其發送回用戶端,但這種方法很快就會變得相當笨拙。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="ba5dd-189">更好的方法是,我們只能在 DinnersController 操作方法中執行應用程式和數據邏輯,然後將呈現 HTML 回應所需的數據傳遞給負責提供其 HTML 表示的單獨"視圖"範本。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="ba5dd-190">正如我們在一瞬間看到的,"視圖"範本是一個文字檔,通常包含 HTML 標記和嵌入呈現代碼的組合。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="ba5dd-191">將控制器邏輯與視圖渲染分離帶來了幾個大好處。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="ba5dd-192">特別是,它有助於在應用程式代碼和UI格式/呈現代碼之間強制實施明確的"關注點分離"。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="ba5dd-193">這使得與 UI 呈現邏輯隔離的單元測試應用程式邏輯變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="ba5dd-194">它便於以後修改 UI 呈現範本,而無需更改應用程式代碼。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="ba5dd-195">而且,它可以使開發人員和設計人員更輕鬆地在專案上協作。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="ba5dd-196">我們可以更新 DinnersController 類,以指示我們希望使用視圖範本發送回 HTML UI 回應,方法是將兩種操作方法的方法簽名從返回類型的"void"改為"ActionResult"。"</span><span class="sxs-lookup"><span data-stu-id="ba5dd-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="ba5dd-197">然後,我們可以調用控制器基類上的*View()* 幫助器方法返回如下所示的「ViewResult」物件:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="ba5dd-198">我們在上面使用的*View()* 説明器方法的簽名如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="ba5dd-199">*View()* 説明程式方法的第一個參數是我們要用於呈現 HTML 回應的檢視範本檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="ba5dd-200">第二個參數是一個模型物件,其中包含檢視範本為呈現 HTML 回應所需的數據。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="ba5dd-201">在我們的 Index() 操作方法中,我們調用*View()* 説明器方法,並指示我們希望使用"Index"視圖範本呈現晚餐的 HTML 清單。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="ba5dd-202">我們正在傳遞檢視範本一系列 Dinner 物件,以便從以下角度生成清單:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="ba5dd-203">在我們的「詳細資訊」操作方法中,我們嘗試使用 URL 中提供的 ID 檢索 Dinner 物件。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="ba5dd-204">如果找到有效的"晚餐",我們調用*View()* 説明器方法,指示我們要使用"詳細資訊"視圖範本來呈現檢索到的 Dinner 物件。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="ba5dd-205">如果請求無效的晚餐,我們會呈現一條有用的錯誤消息,指示使用"NotFound"視圖範本(以及僅採用範本名稱的*View()* 幫助器方法的重載版本不存在 Dinner:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="ba5dd-206">現在,讓我們實現"未找到"、"詳細資訊"和"索引"視圖範本。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="ba5dd-207">實作「未找到」檢視範本</span><span class="sxs-lookup"><span data-stu-id="ba5dd-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="ba5dd-208">我們將首先實現"NotFound"視圖範本 -它顯示一條友好的錯誤消息,指示找不到請求的晚餐。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="ba5dd-209">我們將通過在控制器操作方法中定位文本游標來創建新的檢視範本,然後右鍵按一下並選擇「新增檢視」選單命令(我們還可以通過鍵入 Ctrl-M、Ctrl-V 來執行此命令):</span><span class="sxs-lookup"><span data-stu-id="ba5dd-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="ba5dd-210">這將彈出一個"添加視圖"對話框,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="ba5dd-211">預設情況下,對話方塊將預填充創建檢視的名稱,以匹配啟動對話框時光標所採用的操作方法的名稱(在本例中為"詳細資訊")。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="ba5dd-212">由於我們想要首先實現「未找到」範本,我們將重寫此檢視名稱並將其設置為「未找到」:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="ba5dd-213">按下「添加」按鈕時,Visual Studio 將在「_Views_Dinners」目錄中為我們創建新的「NotFound.aspx」檢視範本(如果目錄不存在,它還會創建該範本):</span><span class="sxs-lookup"><span data-stu-id="ba5dd-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="ba5dd-214">它還將在代碼編輯器中打開我們新的「NotFound.aspx」檢視範本:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="ba5dd-215">默認情況下,查看範本有兩個"內容區域",我們可以在其中添加內容和代碼。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="ba5dd-216">第一個允許我們自定義發回的 HTML 頁面的"標題"</span><span class="sxs-lookup"><span data-stu-id="ba5dd-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="ba5dd-217">第二個允許我們自定義發回的 HTML 頁面的「主要內容」。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="ba5dd-218">要實現我們的「未找到」檢視範本,我們將添加一些基本內容:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="ba5dd-219">然後,我們可以在瀏覽器中試用。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-219">We can then try it out within the browser.</span></span> <span data-ttu-id="ba5dd-220">為此,讓我們請求 *"/晚餐/詳細資訊/9999"URL。*</span><span class="sxs-lookup"><span data-stu-id="ba5dd-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="ba5dd-221">這將引用資料庫中當前不存在的晚餐,並導致我們的 DinnersController.詳細資訊() 操作方法呈現我們的「未找到」檢視範本:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="ba5dd-222">在上面的螢幕截圖中,您會注意到一件事,那就是我們的基本檢視範本繼承了一堆環繞螢幕上主要內容的 HTML。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="ba5dd-223">這是因為我們的檢視範本使用「母版頁」樣本,使我們能夠在網站上的所有視圖上應用一致的佈局。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="ba5dd-224">我們將在本教程的後續部分討論母版頁如何工作。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="ba5dd-225">實作「詳細資訊」檢視範本</span><span class="sxs-lookup"><span data-stu-id="ba5dd-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="ba5dd-226">現在,讓我們實現「詳細資訊」檢視範本, 它將為單個晚餐模型生成 HTML。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="ba5dd-227">我們將通過將文字游標定位到「詳細資訊」操作方法中,然後右鍵單擊並選擇「添加檢視」選單命令(或按 Ctrl-M,Ctrl-V) 來執行此操作:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="ba5dd-228">這將彈出「添加檢視」對話框。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="ba5dd-229">我們將保留預設檢視名稱("詳細資訊")。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="ba5dd-230">我們還在對話框中選擇"創建強類型視圖"複選框,並選擇(使用組合框下拉下)我們從控制器傳遞到視圖的模型類型的名稱。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="ba5dd-231">對於此檢視,我們傳遞一個 Dinner 物件(此類型的完全限定名稱為:「NerdDinner.Model.Dinner」):</span><span class="sxs-lookup"><span data-stu-id="ba5dd-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="ba5dd-232">與之前選擇創建"空視圖"的範本不同,這次我們將選擇使用"詳細資訊"範本自動"基架"視圖。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="ba5dd-233">我們可以通過更改上面對話方塊中的「查看內容」 下拉清單來指示這一點。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="ba5dd-234">"Scaffold"將根據我們傳遞給它的 Dinner 物件生成我們詳細資訊視圖範本的初始實現。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="ba5dd-235">這為我們提供了一種快速開始視圖範本實現的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="ba5dd-236">當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「詳細資訊.aspx」檢視範本檔:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="ba5dd-237">它還將在代碼編輯器中打開我們新的"Details.aspx"視圖範本。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="ba5dd-238">它將包含基於 Dinner 模型的詳細資訊視圖的初始基架實現。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="ba5dd-239">基架引擎使用 .NET 反射來查看通過該資料庫的類上公開的公共屬性,並將根據找到的每個類型添加適當的內容:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="ba5dd-240">我們可以請求 *"/晚餐/詳細資訊/1"URL*以查看瀏覽器中此"詳細資訊"基架實現的外觀。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="ba5dd-241">使用此網址會顯示我們首次建立資料庫時手動到資料庫的晚餐之一:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="ba5dd-242">這讓我們快速啟動和運行,並為我們提供了詳細資訊.aspx 視圖的初始實現。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="ba5dd-243">然後,我們可以去調整它,以自定義 UI,以讓我們滿意。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="ba5dd-244">當我們更仔細地查看 Details.aspx 範本時,我們會發現它包含靜態 HTML 以及嵌入式呈現代碼。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="ba5dd-245">&lt;%&gt;程式碼塊在檢視樣本呈現時執行代碼&lt;,%=&gt;% 程式碼塊執行其中包含的代碼,然後將結果呈現給範本的輸出流。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="ba5dd-246">我們可以在View中編寫代碼,該代碼訪問使用強類型"Model"屬性從控制器傳遞的"Dinner"模型物件。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="ba5dd-247">Visual Studio 在編輯器中存取此「模型」屬性時,為我們提供了完整的代碼無意義:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="ba5dd-248">讓我們做一些調整,以便我們最終的詳細資訊視圖範本的源如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="ba5dd-249">當我們再次訪問 *「/晚餐/細節/1」URL*時,它現在將呈現如下:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="ba5dd-250">實現「索引」檢視範本</span><span class="sxs-lookup"><span data-stu-id="ba5dd-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="ba5dd-251">現在,讓我們實現"索引"視圖範本 - 這將生成即將推出的晚餐的清單。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="ba5dd-252">為此,我們將將文本游標定位在 Index 操作方法中,然後右鍵單擊並選擇「添加檢視」功能表命令(或按 Ctrl-M、Ctrl-V)。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="ba5dd-253">在"添加視圖"對話框中,我們將保留名為"索引"的視圖範本,並選擇"創建強類型視圖"複選框。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="ba5dd-254">這一次,我們將選擇自動生成「列表」檢視範範本,並選擇「NerdDinner.Model.Dinner」作為傳遞給檢視的模型類型(由於我們已指示我們正在創建「列表」基架將導致添加視圖對話框假定我們將一系列 Dinner 物件從控制器傳遞到視圖):</span><span class="sxs-lookup"><span data-stu-id="ba5dd-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="ba5dd-255">當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「Index.aspx」檢視範本檔。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="ba5dd-256">它將「支架」在其中的初始實現,提供我們傳遞給檢視的 Dinner 的 HTML 表清單。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="ba5dd-257">當我們運行應用程式並訪問 *「/Dinners/」URL*時,它將呈現我們的晚餐清單,如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="ba5dd-258">上面的表格解決方案為我們提供了一個網格般的佈局,我們的晚餐數據 – 這不是我們想要為我們的消費者面對晚餐上市。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="ba5dd-259">我們可以更新 Index.aspx 檢視範本並對其進行修改以列出較少的資料列,&lt;並&gt;使用 ul 元素呈現它們,而不是使用以下代碼呈現表:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="ba5dd-260">當我們迴圈展示模型中的每個晚餐時,我們使用上述"var"關鍵字。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="ba5dd-261">不熟悉 C# 3.0 的人可能會認為使用"var"意味著晚餐對像是後期綁定的。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="ba5dd-262">相反,這意味著編譯器使用針對強類型"模型"屬性的類型推理(類型為&lt;&gt;"IE500Dinner"),並將本地"Dinner"變數編譯為 Dinner 類型 - 這意味著我們在代碼塊中獲取完全的無意義和編譯時間檢查:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="ba5dd-263">當我們在瀏覽器中的 */Dinners* URL 上刷新時,我們更新的視圖現在如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="ba5dd-264">看起來更好,但還沒有完全存在。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="ba5dd-265">我們的最後一步是使最終使用者能夠點擊清單中的單個晚餐並查看有關它們的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="ba5dd-266">我們將透過呈現連結到晚餐控制器上「詳細資訊」操作方法的 HTML 超連結元素來實現此內容。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="ba5dd-267">我們可以在 Index 檢視中以兩種方式之一生成這些超連結。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="ba5dd-268">第一種是手動建立&lt;&gt;HTML 元素,如下所示,&lt;&gt;其中&gt;我們在&lt;HTML 元素內嵌入 % 區塊:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="ba5dd-269">我們可以使用的替代方法是利用 MVC 中 ASP.NET 內建的「Html.ActionLink())」幫助器方法,該方法支援以程式設計方式&lt;建立&gt;HTML 元素, 該 元素連結到控制器上的另一個操作方法:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="ba5dd-270">Html.ActionLink() 説明器方法的第一個參數是要顯示的連結文本(在本例中為 Dinner 的標題),第二個參數是我們想要將連結生成的控制器操作名稱(在本例中為詳細資訊方法),第三個參數是一組要發送到操作的參數(作為具有屬性名稱/值的匿名類型實現)。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="ba5dd-271">在這種情況下,我們指定我們要連結到的晚餐的「id」參數,並且由於 ASP.NET MVC 中的預設 URL 路由規則為 Html.ActionLink() 幫助器方法的"{控制器}/{操作}/{id}",因此 Html.ActionLink() 説明程式方法將生成以下輸出:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="ba5dd-272">對於我們的 Index.aspx 檢視,我們將使用 Html.ActionLink() 說明器方法方法,並將每個晚餐都包含到相應詳細資訊 URL 的連結中:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="ba5dd-273">現在,當我們點擊 */Dinners* URL 時,我們的晚餐清單如下所示:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="ba5dd-274">當我們按一下清單中的任何晚餐時,我們將導航以查看有關它的詳細資訊:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="ba5dd-275">基於慣例的命名與 _Views目錄結構</span><span class="sxs-lookup"><span data-stu-id="ba5dd-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="ba5dd-276">默認情況下ASP.NET MVC 應用程式在解決檢視範本時使用基於約定的目錄命名結構。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="ba5dd-277">這允許開發人員在從 Controller 類中引用檢視時避免對位置路徑進行完全限定。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="ba5dd-278">默認情況下ASP.NET MVC 將在應用程式下方的\[[視圖\*控制器名稱] 目錄中尋找檢視範本檔。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="ba5dd-279">例如,我們一直在研究 DinnersController 類,該類顯式引用三個視圖範本:「索引」、「詳細資訊」和」未找到」。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="ba5dd-280">預設情況下,ASP.NET MVC 將在應用程式根目錄下的 *[Views_Dinners]* 目錄中尋找這些檢視:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="ba5dd-281">請注意,專案中當前存在三個控制器類(DinnersController、HomeController 和 AccountController - 在創建專案時預設添加了後兩個控制器類),並且_Views 目錄中有三個子目錄(每個控制器一個)。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="ba5dd-282">從「主頁」和「帳戶」控制器引用的檢視將自動解析其檢視範本,這些範本來自相應的 *[視圖]主頁*和 *[視圖]帳戶*目錄。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="ba5dd-283">*[Views]共用*子目錄提供了一種存儲在應用程式中多個控制器中重複使用的視圖範本的方法。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="ba5dd-284">當 ASP.NET MVC 嘗試解析檢視範本時,它將首先在 *[視圖\[控制器]* 特定目錄中進行檢查,如果無法找到視圖範本,它將在 *[Views_Shared]* 目錄中查找。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="ba5dd-285">在命名單個視圖範本時,建議的指導是讓視圖範本共用與導致其呈現的操作方法相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="ba5dd-286">例如,上面的"Index"操作方法是使用"索引"視圖來呈現視圖結果,而"詳細資訊"操作方法使用"詳細資訊"視圖來呈現其結果。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="ba5dd-287">這樣,就可以輕鬆快速查看與每個操作關聯的範本。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="ba5dd-288">當檢視範本與在控制器上調用的操作方法具有相同的名稱時,開發人員不需要顯式指定視圖範本名稱。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="ba5dd-289">相反,我們可以將模型物件傳遞給"View()"幫助器方法(不指定視圖名稱),並且ASP.NET MVC 將自動推斷我們希望在磁碟上使用 *[視圖\[\[控制器名稱] 操作名稱]* 視圖範本來呈現它。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="ba5dd-290">這使我們能夠稍微清理一下控制器代碼,並避免在代碼中重複兩次名稱:</span><span class="sxs-lookup"><span data-stu-id="ba5dd-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="ba5dd-291">上述代碼是實現一個不錯的晚餐清單/細節體驗的網站所需要的一切。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="ba5dd-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba5dd-292">Next Step</span></span>

<span data-ttu-id="ba5dd-293">我們現在有一個不錯的晚餐瀏覽體驗建立。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="ba5dd-294">現在,讓我們啟用 CRUD(創建、讀取、更新、刪除)數據表單編輯支援。</span><span class="sxs-lookup"><span data-stu-id="ba5dd-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ba5dd-295">[前一個](build-a-model-with-business-rule-validations.md)
> [下一個](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="ba5dd-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
