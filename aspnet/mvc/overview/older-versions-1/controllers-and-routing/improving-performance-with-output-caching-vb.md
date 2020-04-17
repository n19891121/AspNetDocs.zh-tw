---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 以輸出快取 (VB) 提高性能 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何利用輸出緩存來顯著提高ASP.NET MVC Web 應用程式的性能。 你。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: e18d4c5132d4dccc97f1465e7885c9c47a0edab1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542686"
---
# <a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="682d6-104">使用輸出快取改善效能 (VB)</span><span class="sxs-lookup"><span data-stu-id="682d6-104">Improving Performance with Output Caching (VB)</span></span>

<span data-ttu-id="682d6-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="682d6-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="682d6-106">在本教學中,您將瞭解如何利用輸出緩存來顯著提高ASP.NET MVC Web 應用程式的性能。</span><span class="sxs-lookup"><span data-stu-id="682d6-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="682d6-107">您將瞭解如何緩存從控制器操作返回的結果,以便在每次新用戶調用該操作時都不需要創建相同的內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>

<span data-ttu-id="682d6-108">本教學的目的是說明如何透過利用輸出緩存顯著提高ASP.NET MVC 應用程式的性能。</span><span class="sxs-lookup"><span data-stu-id="682d6-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="682d6-109">輸出緩存使您能夠快取控制器操作傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="682d6-110">這樣,每次調用相同的控制器操作時,不需要生成相同的內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="682d6-111">例如,假設您ASP.NET MVC 應用程式在名為 Index 的檢視中顯示資料庫記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="682d6-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="682d6-112">通常,每次使用者調用返回 Index 視圖的控制器操作時,必須通過執行資料庫查詢從資料庫檢索資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="682d6-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="682d6-113">另一方面,如果利用輸出緩存,則可以避免在每次任何用戶調用相同的控制器操作時執行資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="682d6-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="682d6-114">可以從緩存中檢視,而不是從控制器操作中重新生成檢視。</span><span class="sxs-lookup"><span data-stu-id="682d6-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="682d6-115">快取使您能夠避免在伺服器上執行冗餘工作。</span><span class="sxs-lookup"><span data-stu-id="682d6-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="682d6-116">開啟輸出快取</span><span class="sxs-lookup"><span data-stu-id="682d6-116">Enabling Output Caching</span></span>

<span data-ttu-id="682d6-117">通過將&lt;OutputCache&gt;屬性添加到單個控制器操作或整個控制器類來啟用輸出緩存。</span><span class="sxs-lookup"><span data-stu-id="682d6-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="682d6-118">例如,清單 1 中的控制器公開名為 Index() 的操作。</span><span class="sxs-lookup"><span data-stu-id="682d6-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="682d6-119">索引() 操作的輸出緩存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="682d6-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="682d6-120">**清單1 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="682d6-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

<span data-ttu-id="682d6-121">在 ASP.NET MVC 的 Beta 版本中,輸出[http://www.MySite.com/](http://www.mysite.com/)緩存不適用於像的 URL。</span><span class="sxs-lookup"><span data-stu-id="682d6-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="682d6-122">相反,您必須輸入像[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。</span><span class="sxs-lookup"><span data-stu-id="682d6-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>

<span data-ttu-id="682d6-123">在清單 1 中,索引() 操作的輸出緩存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="682d6-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="682d6-124">如果您願意,可以指定更長的緩存持續時間。</span><span class="sxs-lookup"><span data-stu-id="682d6-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="682d6-125">例如,如果要緩存控制器操作的輸出一天,則可以指定 86400 秒(60\*秒\*60 分鐘 24 小時)的緩存持續時間。</span><span class="sxs-lookup"><span data-stu-id="682d6-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="682d6-126">不能保證內容將在您指定的時間量內緩存。</span><span class="sxs-lookup"><span data-stu-id="682d6-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="682d6-127">當記憶體資源變低時,緩存將自動開始驅逐內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="682d6-128">清單 1 中的主控制器返回清單 2 中的索引檢視。</span><span class="sxs-lookup"><span data-stu-id="682d6-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="682d6-129">這個觀點沒有什麼特別之處。</span><span class="sxs-lookup"><span data-stu-id="682d6-129">There is nothing special about this view.</span></span> <span data-ttu-id="682d6-130">索引檢視僅顯示當前時間(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="682d6-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="682d6-131">**清單 2 = 檢視\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="682d6-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="682d6-132">**圖 1 = 快取索引檢視**</span><span class="sxs-lookup"><span data-stu-id="682d6-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="682d6-134">如果透過在瀏覽器的位址列中輸入 URL /Home/Index 並反覆點擊瀏覽器中的「刷新/重新載入」按鈕來多次調用 Index() 操作,則 Index 檢視顯示的時間在 10 秒內不會更改。</span><span class="sxs-lookup"><span data-stu-id="682d6-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="682d6-135">將顯示相同的時間,因為視圖是緩存的。</span><span class="sxs-lookup"><span data-stu-id="682d6-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="682d6-136">請務必瞭解,對於訪問應用程式的每個人,緩存相同的視圖。</span><span class="sxs-lookup"><span data-stu-id="682d6-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="682d6-137">調用 Index() 操作的任何人都可以獲得相同的索引檢視緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="682d6-138">這意味著 Web 伺服器為索引檢視提供服務而必須執行的工作量將大大減少。</span><span class="sxs-lookup"><span data-stu-id="682d6-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="682d6-139">清單2中的視圖碰巧在做一些非常簡單的事情。</span><span class="sxs-lookup"><span data-stu-id="682d6-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="682d6-140">視圖僅顯示當前時間。</span><span class="sxs-lookup"><span data-stu-id="682d6-140">The view just displays the current time.</span></span> <span data-ttu-id="682d6-141">但是,您可以同樣輕鬆地緩存顯示一組資料庫記錄的檢視。</span><span class="sxs-lookup"><span data-stu-id="682d6-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="682d6-142">在這種情況下,每次調用返回檢視的控制器操作時,就不需要從資料庫中檢索資料庫記錄集。</span><span class="sxs-lookup"><span data-stu-id="682d6-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="682d6-143">快取可以減少 Web 伺服器和資料庫伺服器必須執行的工作量。</span><span class="sxs-lookup"><span data-stu-id="682d6-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="682d6-144">不要在 MVC 檢視&lt;中 使用頁面&gt;%@ 輸出快取 % 指令。</span><span class="sxs-lookup"><span data-stu-id="682d6-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="682d6-145">此指令正在從 Web 窗體世界中出血,不應在 mVC 應用程式中 ASP.NET 中使用。</span><span class="sxs-lookup"><span data-stu-id="682d6-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="682d6-146">快取內容的位置</span><span class="sxs-lookup"><span data-stu-id="682d6-146">Where Content is Cached</span></span>

<span data-ttu-id="682d6-147">預設情況下,當您使用&lt;OutputCache&gt;屬性時,內容緩存在三個位置:Web 伺服器、任何代理伺服器和 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="682d6-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="682d6-148">您可以通過&lt;修改 OutputCache&gt;屬性的位置屬性來準確控制內容的緩存位置。</span><span class="sxs-lookup"><span data-stu-id="682d6-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="682d6-149">您可以將「位置」屬性設定為以下任一值:</span><span class="sxs-lookup"><span data-stu-id="682d6-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="682d6-150">·任何</span><span class="sxs-lookup"><span data-stu-id="682d6-150">· Any</span></span>
> 
> <span data-ttu-id="682d6-151">·客戶</span><span class="sxs-lookup"><span data-stu-id="682d6-151">· Client</span></span>
> 
> <span data-ttu-id="682d6-152">·下游</span><span class="sxs-lookup"><span data-stu-id="682d6-152">· Downstream</span></span>
> 
> <span data-ttu-id="682d6-153">·伺服器</span><span class="sxs-lookup"><span data-stu-id="682d6-153">· Server</span></span>
> 
> <span data-ttu-id="682d6-154">·沒有</span><span class="sxs-lookup"><span data-stu-id="682d6-154">· None</span></span>
> 
> <span data-ttu-id="682d6-155">·伺服器和用戶端</span><span class="sxs-lookup"><span data-stu-id="682d6-155">· ServerAndClient</span></span>

<span data-ttu-id="682d6-156">默認情況下,"位置"屬性具有"Any"的值。</span><span class="sxs-lookup"><span data-stu-id="682d6-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="682d6-157">但是,在某些情況下,您可能只想在瀏覽器或伺服器上緩存。</span><span class="sxs-lookup"><span data-stu-id="682d6-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="682d6-158">例如,如果要緩存針對每個使用者進行個人化的資訊,則不應在伺服器上緩存資訊。</span><span class="sxs-lookup"><span data-stu-id="682d6-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="682d6-159">如果要向不同的用戶顯示不同的資訊,則應僅在用戶端上緩存資訊。</span><span class="sxs-lookup"><span data-stu-id="682d6-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="682d6-160">例如,清單 3 中的控制器公開名為 GetName() 的操作,該操作傳回當前使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="682d6-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="682d6-161">如果 Jack 登錄到網站並調用 GetName() 操作,則該操作將返回字串「嗨傑克」。</span><span class="sxs-lookup"><span data-stu-id="682d6-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="682d6-162">如果,隨後,Jill登錄到網站並調用 GetName() 操作,那麼她也將得到字串「嗨傑克」。。</span><span class="sxs-lookup"><span data-stu-id="682d6-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="682d6-163">在 Jack 最初呼叫控制器操作後,字串將緩存在 Web 伺服器上,供所有使用者使用。</span><span class="sxs-lookup"><span data-stu-id="682d6-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="682d6-164">**清單3 = 控制器\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="682d6-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="682d6-165">最有可能的是,清單 3 中的控制器不能以您想要的方式工作。</span><span class="sxs-lookup"><span data-stu-id="682d6-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="682d6-166">您不想向吉爾顯示「嗨傑克」的消息。</span><span class="sxs-lookup"><span data-stu-id="682d6-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="682d6-167">不應在伺服器緩存中緩存個性化內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="682d6-168">但是,您可能希望在瀏覽器緩存中緩存個性化內容以提高性能。</span><span class="sxs-lookup"><span data-stu-id="682d6-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="682d6-169">如果在瀏覽器中緩存內容,並且使用者多次調用同一控制器操作,則可以從瀏覽器緩存而不是伺服器檢索內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="682d6-170">清單 4 中修改後的控制器快取 GetName() 操作的輸出。</span><span class="sxs-lookup"><span data-stu-id="682d6-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="682d6-171">但是,內容僅緩存在瀏覽器上,而不是伺服器上。</span><span class="sxs-lookup"><span data-stu-id="682d6-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="682d6-172">這樣,當多個使用者調用 GetName() 方法時,每個人都會獲得自己的使用者名,而不是其他人的使用者名。</span><span class="sxs-lookup"><span data-stu-id="682d6-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="682d6-173">**清單4 = 控制器\使用者控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="682d6-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="682d6-174">請注意,清單&lt;&gt;4 中的 OutputCache 屬性包括一個位置屬性,該屬性設置為值輸出緩存位置.用戶端。</span><span class="sxs-lookup"><span data-stu-id="682d6-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="682d6-175">OutputCache&lt;&gt;屬性還包括NoStore屬性。</span><span class="sxs-lookup"><span data-stu-id="682d6-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="682d6-176">NoStore 屬性用於通知代理伺服器和瀏覽器它們不應存儲緩存內容的永久副本。</span><span class="sxs-lookup"><span data-stu-id="682d6-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="682d6-177">變更輸出快取</span><span class="sxs-lookup"><span data-stu-id="682d6-177">Varying the Output Cache</span></span>

<span data-ttu-id="682d6-178">在某些情況下,您可能需要相同內容的不同緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="682d6-179">例如,假設您正在創建一個母版/詳細資訊頁。</span><span class="sxs-lookup"><span data-stu-id="682d6-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="682d6-180">母版頁顯示電影標題的清單。</span><span class="sxs-lookup"><span data-stu-id="682d6-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="682d6-181">按一下標題時,您將獲得所選影片的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="682d6-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="682d6-182">如果緩存詳細資訊頁,則無論單擊哪個影片,都會顯示同一影片的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="682d6-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="682d6-183">第一個用戶選擇的第一個影片將顯示給所有將來的使用者。</span><span class="sxs-lookup"><span data-stu-id="682d6-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="682d6-184">您可以通過&lt;利用 OutputCache&gt;屬性的 VaryByParam 屬性來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="682d6-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="682d6-185">此屬性使您能夠在表單參數或查詢字串參數不同時創建相同內容的不同快取版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="682d6-186">例如,清單 5 中的控制器公開名為 Master() 和詳細資訊() 的兩個操作。</span><span class="sxs-lookup"><span data-stu-id="682d6-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="682d6-187">Master() 操作傳回影片標題清單,詳細資訊() 操作傳回所選影片的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="682d6-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="682d6-188">**清單5 = 控制器\電影控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="682d6-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="682d6-189">Master() 操作包括一個具有值"無"的 VaryByParam 屬性。</span><span class="sxs-lookup"><span data-stu-id="682d6-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="682d6-190">調用 Master() 操作時,將返回主檢視的相同緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="682d6-191">忽略任何表單參數或查詢字串參數(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="682d6-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="682d6-192">**圖 2 = /電影/主檢視**</span><span class="sxs-lookup"><span data-stu-id="682d6-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="682d6-194">**圖 3 = /電影/詳細資訊檢視**</span><span class="sxs-lookup"><span data-stu-id="682d6-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="682d6-196">詳細資訊() 操作包括一個帶值"Id"的 VaryByParam 屬性。</span><span class="sxs-lookup"><span data-stu-id="682d6-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="682d6-197">當將 Id 參數的不同值傳遞給控制器操作時,將生成「詳細資訊」檢視的不同緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="682d6-198">請務必瞭解,使用 VaryByParam 屬性會導致緩存更多,而不是更少。</span><span class="sxs-lookup"><span data-stu-id="682d6-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="682d6-199">為 Id 參數的每個不同版本創建「詳細資訊」檢視的不同緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="682d6-200">您可以將 VaryByParam 屬性設定為以下值:</span><span class="sxs-lookup"><span data-stu-id="682d6-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="682d6-201">\*• 每當窗體或查詢字串參數發生變化時,都會創建不同的緩存版本。</span><span class="sxs-lookup"><span data-stu-id="682d6-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="682d6-202">沒有 = 從不建立不同的快取版本</span><span class="sxs-lookup"><span data-stu-id="682d6-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="682d6-203">參數的分號清單 = 每當清單中的任何窗體或查詢字串參數發生變化時,建立不同的緩存版本</span><span class="sxs-lookup"><span data-stu-id="682d6-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>

#### <a name="creating-a-cache-profile"></a><span data-ttu-id="682d6-204">建立快取設定檔</span><span class="sxs-lookup"><span data-stu-id="682d6-204">Creating a Cache Profile</span></span>

<span data-ttu-id="682d6-205">作為透過修改&lt;OutputCache&gt;屬性的屬性來設定輸出快取屬性的替代方法,您可以在 Web 設定 (Web.config) 檔案中建立快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="682d6-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="682d6-206">在 Web 設定檔中建立快取配置檔具有幾個重要優勢。</span><span class="sxs-lookup"><span data-stu-id="682d6-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="682d6-207">首先,通過在 Web 設定檔中配置輸出緩存,可以控制控制器操作如何在一個中心位置緩存內容。</span><span class="sxs-lookup"><span data-stu-id="682d6-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="682d6-208">您可以創建一個快取設定檔,並將設定檔應用於多個控制器或控制器操作。</span><span class="sxs-lookup"><span data-stu-id="682d6-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="682d6-209">其次,您可以修改 Web 配置檔,而無需重新編譯應用程式。</span><span class="sxs-lookup"><span data-stu-id="682d6-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="682d6-210">如果需要禁用已部署到生產中的應用程式的快取,則只需修改 Web 設定檔中定義的快取設定檔即可。</span><span class="sxs-lookup"><span data-stu-id="682d6-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="682d6-211">將自動檢測並應用對 Web 配置檔的任何更改。</span><span class="sxs-lookup"><span data-stu-id="682d6-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="682d6-212">例如,清單&lt;&gt;6 中的快取 Web 配置部分定義名為 Cache1Hour 的快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="682d6-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="682d6-213">&lt;快取&gt;部分必須出現在 Web&lt;設定檔的 system.web&gt;部分中。</span><span class="sxs-lookup"><span data-stu-id="682d6-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="682d6-214">**清單6 = Web.config 的快取部分**</span><span class="sxs-lookup"><span data-stu-id="682d6-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="682d6-215">清單7中的控制器說明了如何使用&lt;OutputCache&gt;屬性將Cache1Hour設定檔應用於控制器操作。</span><span class="sxs-lookup"><span data-stu-id="682d6-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="682d6-216">**清單7 = 控制器\設定檔案控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="682d6-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="682d6-217">如果調用清單 7 中控制器公開的 Index() 操作,則將返回相同的時間 1 小時。</span><span class="sxs-lookup"><span data-stu-id="682d6-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="682d6-218">總結</span><span class="sxs-lookup"><span data-stu-id="682d6-218">Summary</span></span>

<span data-ttu-id="682d6-219">輸出緩存為您提供了一種非常簡單的方法來顯著提高ASP.NET MVC 應用程式的性能。</span><span class="sxs-lookup"><span data-stu-id="682d6-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="682d6-220">在本教學中,您學習了如何使用&lt;OutputCache&gt;屬性快取控制器操作的輸出。</span><span class="sxs-lookup"><span data-stu-id="682d6-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="682d6-221">您還學習了如何修改&lt;OutputCache&gt;屬性的屬性,如持續時間和 VaryByParam 屬性,以修改內容的緩存方式。</span><span class="sxs-lookup"><span data-stu-id="682d6-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="682d6-222">最後,您學習了如何在 Web 設定檔中定義快取設定檔。</span><span class="sxs-lookup"><span data-stu-id="682d6-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="682d6-223">[前一個](understanding-action-filters-vb.md)
> [下一個](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="682d6-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
