---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: '瞭解模型、視圖和控制器 (c # ) |Microsoft Docs'
author: StephenWalther
description: 對模型、視圖和控制器有混淆嗎？ 在本教學課程中，Stephen Walther 將為您介紹 ASP.NET MVC 應用程式的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: f4d069ddf30634dd6d632468d8e282bf5b2593d3
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045217"
---
# <a name="understanding-models-views-and-controllers-c"></a><span data-ttu-id="6f34e-104">了解模型、檢視和控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="6f34e-104">Understanding Models, Views, and Controllers (C#)</span></span>

<span data-ttu-id="6f34e-105">依 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6f34e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6f34e-106">對模型、視圖和控制器有混淆嗎？</span><span class="sxs-lookup"><span data-stu-id="6f34e-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="6f34e-107">在本教學課程中，Stephen Walther 將為您介紹 ASP.NET MVC 應用程式的不同部分。</span><span class="sxs-lookup"><span data-stu-id="6f34e-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>

<span data-ttu-id="6f34e-108">本教學課程提供 ASP.NET MVC 模型、視圖和控制器的概要說明。</span><span class="sxs-lookup"><span data-stu-id="6f34e-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="6f34e-109">換句話說，它會說明 ASP.NET MVC 中的 M '、V ' 和 C '。</span><span class="sxs-lookup"><span data-stu-id="6f34e-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="6f34e-110">閱讀本教學課程之後，您應該瞭解 ASP.NET MVC 應用程式的不同部分如何一起運作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="6f34e-111">您也應該瞭解 ASP.NET MVC 應用程式架構與 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式的差異。</span><span class="sxs-lookup"><span data-stu-id="6f34e-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="6f34e-112">範例 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f34e-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="6f34e-113">建立 ASP.NET MVC Web 應用程式的預設 Visual Studio 範本包含一個非常簡單的範例應用程式，可用來瞭解 ASP.NET MVC 應用程式的不同部分。</span><span class="sxs-lookup"><span data-stu-id="6f34e-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="6f34e-114">在本教學課程中，我們會利用這個簡單的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="6f34e-115">您可以藉由啟動 Visual Studio 2008 並選取功能表選項 [檔案]、[新增專案] (來建立包含 MVC 範本的新 ASP.NET MVC 應用程式，請參閱 [圖 1]) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="6f34e-116">在 [新增專案] 對話方塊中，從 [專案類型] 下選取您慣用的程式語言 (Visual Basic 或 c # ) 然後選取 [範本] 底下的 [ **ASP.NET MVC Web 應用程式** ]</span><span class="sxs-lookup"><span data-stu-id="6f34e-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="6f34e-117">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f34e-117">Click the OK button.</span></span>

<span data-ttu-id="6f34e-118">[![[新增專案] 對話方塊](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6f34e-118">[![New Project Dialog](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span></span>

<span data-ttu-id="6f34e-119">**圖 01**： [新增專案] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="6f34e-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image2.png))</span></span>

<span data-ttu-id="6f34e-120">當您建立新的 ASP.NET MVC 應用程式時，會出現 [ **建立單元測試專案** ] 對話方塊 (請參閱 [圖 2]) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="6f34e-121">此對話方塊可讓您在方案中建立個別的專案，以測試您的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="6f34e-122">選取選項 [ **否，不要建立單元測試專案** ]，然後按一下 [ **確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6f34e-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>

<span data-ttu-id="6f34e-123">[![[建立單元測試] 對話方塊](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6f34e-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span></span>

<span data-ttu-id="6f34e-124">**圖 02**： [建立單元測試] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="6f34e-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image4.png))</span></span>

<span data-ttu-id="6f34e-125">建立新的 ASP.NET MVC 應用程式之後。</span><span class="sxs-lookup"><span data-stu-id="6f34e-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="6f34e-126">在 [方案總管] 視窗中，您會看到數個資料夾和檔案。</span><span class="sxs-lookup"><span data-stu-id="6f34e-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="6f34e-127">特別是，您會看到三個名為「模型」、「Views」和「控制器」的資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f34e-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="6f34e-128">您可能會猜到資料夾名稱，這些資料夾包含用來執行模型、視圖和控制器的檔案。</span><span class="sxs-lookup"><span data-stu-id="6f34e-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="6f34e-129">如果您展開 [控制器] 資料夾，您應該會看到名為 AccountController.cs 的檔案，以及名為 HomeController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="6f34e-129">If you expand the Controllers folder, you should see a file named AccountController.cs and a file named HomeController.cs.</span></span> <span data-ttu-id="6f34e-130">如果您展開 Views 資料夾，您應該會看到三個名為 Account、Home 和 Shared 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f34e-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="6f34e-131">如果您展開 [主資料夾] 資料夾，您將會看到兩個名為 [關於 .aspx 和 default.aspx 的檔案 (請參閱 [圖 3]) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="6f34e-132">這些檔案會組成預設 ASP.NET MVC 範本隨附的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>

<span data-ttu-id="6f34e-133">[![方案總管視窗](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6f34e-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span></span>

<span data-ttu-id="6f34e-134">**圖 03**：方案總管視窗 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="6f34e-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image6.png))</span></span>

<span data-ttu-id="6f34e-135">您可以藉由選取 [偵錯工具]、[ **開始調試**] 來執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="6f34e-136">或者，您也可以按 F5 鍵。</span><span class="sxs-lookup"><span data-stu-id="6f34e-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="6f34e-137">當您第一次執行 ASP.NET 應用程式時，[圖 4] 中的對話方塊會出現，建議您啟用 [偵錯工具] 模式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="6f34e-138">按一下 [確定] 按鈕，應用程式就會執行。</span><span class="sxs-lookup"><span data-stu-id="6f34e-138">Click the OK button and the application will run.</span></span>

<span data-ttu-id="6f34e-139">[![未啟用 [調試] 對話方塊](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6f34e-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span></span>

<span data-ttu-id="6f34e-140">**圖 04**：未啟用 [調試] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="6f34e-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image8.png))</span></span>

<span data-ttu-id="6f34e-141">當您執行 ASP.NET MVC 應用程式時，Visual Studio 會在網頁瀏覽器中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="6f34e-142">範例應用程式只包含兩個頁面： [索引] 頁面和 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f34e-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="6f34e-143">當應用程式第一次啟動時，會出現 [索引] 頁面 (請參閱 [圖 5]) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="6f34e-144">您可以按一下應用程式右上方的功能表連結，以流覽至 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f34e-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>

<span data-ttu-id="6f34e-145">[![索引頁面](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="6f34e-145">[![The Index Page](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span></span>

<span data-ttu-id="6f34e-146">**圖 05**： [索引] 頁面 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image11.png)) </span><span class="sxs-lookup"><span data-stu-id="6f34e-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image11.png))</span></span>

<span data-ttu-id="6f34e-147">請注意瀏覽器位址列中的 Url。</span><span class="sxs-lookup"><span data-stu-id="6f34e-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="6f34e-148">例如，當您按一下 [關於] 功能表連結時，瀏覽器位址列中的 URL 會變更為 [ **/Home/About**]。</span><span class="sxs-lookup"><span data-stu-id="6f34e-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="6f34e-149">如果您關閉瀏覽器視窗，並返回 Visual Studio，您將無法找到路徑為 Home/About 的檔案。</span><span class="sxs-lookup"><span data-stu-id="6f34e-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="6f34e-150">檔案不存在。</span><span class="sxs-lookup"><span data-stu-id="6f34e-150">The files don't exist.</span></span> <span data-ttu-id="6f34e-151">這有何可能？</span><span class="sxs-lookup"><span data-stu-id="6f34e-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="6f34e-152">URL 不等於頁面</span><span class="sxs-lookup"><span data-stu-id="6f34e-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="6f34e-153">當您建立傳統的 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式時，URL 與頁面之間會有一對一的對應關係。</span><span class="sxs-lookup"><span data-stu-id="6f34e-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="6f34e-154">如果您從伺服器要求名為 SomePage 的頁面，則磁片上的頁面會是名為 SomePage .aspx。</span><span class="sxs-lookup"><span data-stu-id="6f34e-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="6f34e-155">如果 SomePage .aspx 檔案不存在，則會出現不美觀的 **404-找不到頁面** 錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f34e-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="6f34e-156">相較之下，建立 ASP.NET MVC 應用程式時，您在瀏覽器的網址列中輸入的 URL 與您在應用程式中找到的檔案之間並沒有任何對應關係。</span><span class="sxs-lookup"><span data-stu-id="6f34e-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="6f34e-157">在 ASP.NET MVC 應用程式中，URL 會對應至控制器動作，而不是磁片上的頁面。</span><span class="sxs-lookup"><span data-stu-id="6f34e-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="6f34e-158">在傳統的 ASP.NET 或 ASP 應用程式中，瀏覽器要求會對應到頁面。</span><span class="sxs-lookup"><span data-stu-id="6f34e-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="6f34e-159">相反地，在 ASP.NET MVC 應用程式中，瀏覽器要求會對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="6f34e-160">以內容為主的 ASP.NET Web Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="6f34e-161">相反地，ASP.NET MVC 應用程式是以應用程式邏輯為主。</span><span class="sxs-lookup"><span data-stu-id="6f34e-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="6f34e-162">瞭解 ASP.NET 路由</span><span class="sxs-lookup"><span data-stu-id="6f34e-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="6f34e-163">瀏覽器要求會透過稱為 *ASP.NET 路由*的 ASP.NET 架構功能，對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="6f34e-164">ASP.NET MVC framework 會使用 ASP.NET 路由將連入要求 *路由傳送* 至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="6f34e-165">ASP.NET 路由會使用路由表來處理連入要求。</span><span class="sxs-lookup"><span data-stu-id="6f34e-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="6f34e-166">當您的 web 應用程式第一次啟動時，就會建立此路由表。</span><span class="sxs-lookup"><span data-stu-id="6f34e-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="6f34e-167">路由表是在 global.asax 檔案中設定。</span><span class="sxs-lookup"><span data-stu-id="6f34e-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="6f34e-168">預設 MVC global.asax 檔案包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="6f34e-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="6f34e-169">**清單 1-global.asax**</span><span class="sxs-lookup"><span data-stu-id="6f34e-169">**Listing 1 - Global.asax**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

<span data-ttu-id="6f34e-170">ASP.NET 應用程式第一次啟動時， \_ 會呼叫應用程式啟動 ( # A1 方法。</span><span class="sxs-lookup"><span data-stu-id="6f34e-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="6f34e-171">在 [清單 1] 中，這個方法會呼叫 RegisterRoutes ( # A1 方法，而 RegisterRoutes ( # A3 方法會建立預設路由表。</span><span class="sxs-lookup"><span data-stu-id="6f34e-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="6f34e-172">預設路由表包含一個路由。</span><span class="sxs-lookup"><span data-stu-id="6f34e-172">The default route table consists of one route.</span></span> <span data-ttu-id="6f34e-173">此預設路由會將所有傳入要求分成三個區段， (URL 區段是正斜線) 之間的任何一項。</span><span class="sxs-lookup"><span data-stu-id="6f34e-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="6f34e-174">第一個區段對應到控制器名稱，第二個區段對應至動作名稱，而最後一個區段對應至傳遞給名為 Id 之動作的參數。</span><span class="sxs-lookup"><span data-stu-id="6f34e-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="6f34e-175">例如，請考慮下列 URL：</span><span class="sxs-lookup"><span data-stu-id="6f34e-175">For example, consider the following URL:</span></span>

<span data-ttu-id="6f34e-176">/Product/Details/3</span><span class="sxs-lookup"><span data-stu-id="6f34e-176">/Product/Details/3</span></span>

<span data-ttu-id="6f34e-177">此 URL 會剖析成三個參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f34e-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="6f34e-178">控制器 = 產品</span><span class="sxs-lookup"><span data-stu-id="6f34e-178">Controller = Product</span></span>

<span data-ttu-id="6f34e-179">動作 = 詳細資料</span><span class="sxs-lookup"><span data-stu-id="6f34e-179">Action = Details</span></span>

<span data-ttu-id="6f34e-180">識別碼 = 3</span><span class="sxs-lookup"><span data-stu-id="6f34e-180">Id = 3</span></span>

<span data-ttu-id="6f34e-181">Global.asax 檔案中定義的預設路由包含所有三個參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="6f34e-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="6f34e-182">預設控制器為 [首頁]，預設動作是 [索引]，而預設識別碼為空白字串。</span><span class="sxs-lookup"><span data-stu-id="6f34e-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="6f34e-183">記住這些預設值後，請考慮下列 URL 的剖析方式：</span><span class="sxs-lookup"><span data-stu-id="6f34e-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="6f34e-184">/Employee</span><span class="sxs-lookup"><span data-stu-id="6f34e-184">/Employee</span></span>

<span data-ttu-id="6f34e-185">此 URL 會剖析成三個參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f34e-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="6f34e-186">控制器 = 員工</span><span class="sxs-lookup"><span data-stu-id="6f34e-186">Controller = Employee</span></span>

<span data-ttu-id="6f34e-187">Action = Index</span><span class="sxs-lookup"><span data-stu-id="6f34e-187">Action = Index</span></span>

<span data-ttu-id="6f34e-188">識別碼 =</span><span class="sxs-lookup"><span data-stu-id="6f34e-188">Id =</span></span>

<span data-ttu-id="6f34e-189">最後，如果您開啟 ASP.NET MVC 應用程式，但未提供任何 URL (例如， `http://localhost`) 則會剖析 URL，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f34e-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="6f34e-190">控制器 = 首頁</span><span class="sxs-lookup"><span data-stu-id="6f34e-190">Controller = Home</span></span>

<span data-ttu-id="6f34e-191">Action = Index</span><span class="sxs-lookup"><span data-stu-id="6f34e-191">Action = Index</span></span>

<span data-ttu-id="6f34e-192">識別碼 =</span><span class="sxs-lookup"><span data-stu-id="6f34e-192">Id =</span></span>

<span data-ttu-id="6f34e-193">要求會路由傳送至 HomeController 類別上的索引 ( # A1 動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="6f34e-194">瞭解控制器</span><span class="sxs-lookup"><span data-stu-id="6f34e-194">Understanding Controllers</span></span>

<span data-ttu-id="6f34e-195">控制器負責控制使用者與 MVC 應用程式互動的方式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="6f34e-196">控制器包含 ASP.NET MVC 應用程式的流程式控制制邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f34e-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="6f34e-197">控制器會決定當使用者提出瀏覽器要求時，要傳回給使用者的回應。</span><span class="sxs-lookup"><span data-stu-id="6f34e-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="6f34e-198">控制器只是一個類別 (例如 Visual Basic 或 c # 類別) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="6f34e-199">範例 ASP.NET MVC 應用程式包含一個名為 HomeController.cs 的控制器，位於 [控制器] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="6f34e-199">The sample ASP.NET MVC application includes a controller named HomeController.cs located in the Controllers folder.</span></span> <span data-ttu-id="6f34e-200">HomeController.cs 檔案的內容會在 [清單 2] 中重現。</span><span class="sxs-lookup"><span data-stu-id="6f34e-200">The content of the HomeController.cs file is reproduced in Listing 2.</span></span>

<span data-ttu-id="6f34e-201">**清單 2-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="6f34e-201">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

<span data-ttu-id="6f34e-202">請注意，HomeController 有兩個名為 Index ( # A1 和 ( # A3 的方法。</span><span class="sxs-lookup"><span data-stu-id="6f34e-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="6f34e-203">這兩個方法會對應至控制器所公開的兩個動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="6f34e-204">URL/Home/Index 會叫用 HomeController， ( # A1 方法，而 URL/Home/About 會叫用 HomeController。關於 ( # A3 方法。</span><span class="sxs-lookup"><span data-stu-id="6f34e-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="6f34e-205">控制器中的任何公用方法都會公開為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="6f34e-206">您需要特別注意這一點。</span><span class="sxs-lookup"><span data-stu-id="6f34e-206">You need to be careful about this.</span></span> <span data-ttu-id="6f34e-207">這表示任何可存取網際網路的人都可以叫用包含在該控制器中的所有公用方法，方法是在瀏覽器中輸入正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="6f34e-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="6f34e-208">了解檢視</span><span class="sxs-lookup"><span data-stu-id="6f34e-208">Understanding Views</span></span>

<span data-ttu-id="6f34e-209">HomeController 類別所公開的兩個控制器動作（Index ( # A1 和 ( # A3）會傳回一個 view。</span><span class="sxs-lookup"><span data-stu-id="6f34e-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="6f34e-210">視圖包含 HTML 標籤和傳送至瀏覽器的內容。</span><span class="sxs-lookup"><span data-stu-id="6f34e-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="6f34e-211">View 相當於使用 ASP.NET MVC 應用程式時的頁面。</span><span class="sxs-lookup"><span data-stu-id="6f34e-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="6f34e-212">您必須在正確的位置建立您的視圖。</span><span class="sxs-lookup"><span data-stu-id="6f34e-212">You must create your views in the right location.</span></span> <span data-ttu-id="6f34e-213">HomeController ( # A1 動作會傳回位於下列路徑的視圖：</span><span class="sxs-lookup"><span data-stu-id="6f34e-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="6f34e-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="6f34e-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="6f34e-215">HomeController. About ( # A1 動作會傳回位於下列路徑的視圖：</span><span class="sxs-lookup"><span data-stu-id="6f34e-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="6f34e-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="6f34e-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="6f34e-217">一般情況下，如果您想要傳回控制器動作的視圖，則需要在 [Views] 資料夾中建立與控制器相同名稱的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="6f34e-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="6f34e-218">在子資料夾內，您必須建立與控制器動作相同名稱的 .aspx 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f34e-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="6f34e-219">[清單 3] 中的檔案包含有關 .aspx 的觀點。</span><span class="sxs-lookup"><span data-stu-id="6f34e-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="6f34e-220">**清單 3-關於 .aspx**</span><span class="sxs-lookup"><span data-stu-id="6f34e-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

<span data-ttu-id="6f34e-221">如果您忽略 [清單 3] 中的第一行，則大部分的視圖都是由標準 HTML 組成。</span><span class="sxs-lookup"><span data-stu-id="6f34e-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="6f34e-222">您可以在這裡輸入任何您想要的 HTML 來修改視圖的內容。</span><span class="sxs-lookup"><span data-stu-id="6f34e-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="6f34e-223">View 與 Active Server Pages 或 ASP.NET Web Forms 中的頁面非常類似。</span><span class="sxs-lookup"><span data-stu-id="6f34e-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="6f34e-224">一個視圖可以包含 HTML 內容和腳本。</span><span class="sxs-lookup"><span data-stu-id="6f34e-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="6f34e-225">您可以用您最愛的 .NET 程式設計語言撰寫腳本 (例如，c # 或 Visual Basic .NET) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="6f34e-226">您可以使用腳本來顯示動態內容，例如資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="6f34e-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="6f34e-227">瞭解模型</span><span class="sxs-lookup"><span data-stu-id="6f34e-227">Understanding Models</span></span>

<span data-ttu-id="6f34e-228">我們已討論過控制器，並已討論過這些觀點。</span><span class="sxs-lookup"><span data-stu-id="6f34e-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="6f34e-229">我們必須討論的最後一個主題是模型。</span><span class="sxs-lookup"><span data-stu-id="6f34e-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="6f34e-230">什麼是 MVC 模型？</span><span class="sxs-lookup"><span data-stu-id="6f34e-230">What is an MVC model?</span></span>

<span data-ttu-id="6f34e-231">MVC 模型包含所有不包含在視圖或控制器中的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f34e-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="6f34e-232">此模型應該包含您所有的應用程式商務邏輯、驗證邏輯和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f34e-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="6f34e-233">例如，如果您使用 Microsoft Entity Framework 來存取資料庫，則您會在 [模型] 資料夾中) 您的 .edmx 檔案 (建立 Entity Framework 類別。</span><span class="sxs-lookup"><span data-stu-id="6f34e-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="6f34e-234">視圖應該只包含與產生使用者介面相關的邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f34e-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="6f34e-235">控制器應該只包含傳回右視圖所需的最低邏輯，或將使用者重新導向至另一個動作 (流量控制) 。</span><span class="sxs-lookup"><span data-stu-id="6f34e-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="6f34e-236">其他所有專案都應該包含在模型中。</span><span class="sxs-lookup"><span data-stu-id="6f34e-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="6f34e-237">一般情況下，您應該努力進行 fat 模型和訣竅控制器。</span><span class="sxs-lookup"><span data-stu-id="6f34e-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="6f34e-238">您的控制器方法應該只包含幾行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f34e-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="6f34e-239">如果控制器動作變得太長，您應該考慮將邏輯移出 [模型] 資料夾中的新類別。</span><span class="sxs-lookup"><span data-stu-id="6f34e-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="6f34e-240">摘要</span><span class="sxs-lookup"><span data-stu-id="6f34e-240">Summary</span></span>

<span data-ttu-id="6f34e-241">本教學課程提供 ASP.NET MVC web 應用程式中不同部分的概要總覽。</span><span class="sxs-lookup"><span data-stu-id="6f34e-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="6f34e-242">您已瞭解 ASP.NET 路由如何將連入瀏覽器要求對應至特定的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="6f34e-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="6f34e-243">您已瞭解控制器如何協調將視圖傳回至瀏覽器的方式。</span><span class="sxs-lookup"><span data-stu-id="6f34e-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="6f34e-244">最後，您已瞭解模型如何包含應用程式的商務、驗證和資料庫存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f34e-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>
