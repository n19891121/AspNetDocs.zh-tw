---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
title: 將動態內容加入快取頁面 (VB) |微軟文件
author: rick-anderson
description: 瞭解如何在同一頁中混合動態和緩存的內容。 快取後取代讓您能夠顯示動態內容,如橫幅播發。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 68acd884-fb57-4486-a1be-aaa93e380780
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 1ed022fc560becbd21722b94f2428cf7b32f2635
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542257"
---
# <a name="adding-dynamic-content-to-a-cached-page-vb"></a><span data-ttu-id="3a001-104">將動態內容新增至快取的頁面 (VB)</span><span class="sxs-lookup"><span data-stu-id="3a001-104">Adding Dynamic Content to a Cached Page (VB)</span></span>

<span data-ttu-id="3a001-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3a001-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="3a001-106">瞭解如何在同一頁中混合動態和緩存的內容。</span><span class="sxs-lookup"><span data-stu-id="3a001-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="3a001-107">快取後取代讓您能夠在已快取的頁面中顯示動態內容,如橫幅播發或新聞專案。</span><span class="sxs-lookup"><span data-stu-id="3a001-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="3a001-108">通過利用輸出緩存,您可以顯著提高ASP.NET MVC 應用程式的性能。</span><span class="sxs-lookup"><span data-stu-id="3a001-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="3a001-109">在每次請求頁面時,該頁可以生成一次,並緩存在多個使用者的記憶體中,而不是每次請求頁面時重新生成頁面。</span><span class="sxs-lookup"><span data-stu-id="3a001-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="3a001-110">但有一個問題。</span><span class="sxs-lookup"><span data-stu-id="3a001-110">But there is a problem.</span></span> <span data-ttu-id="3a001-111">如果您需要在頁面中顯示動態內容,該怎麼辦?</span><span class="sxs-lookup"><span data-stu-id="3a001-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="3a001-112">例如,假設您要在頁面中顯示橫幅廣告。</span><span class="sxs-lookup"><span data-stu-id="3a001-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="3a001-113">您不希望緩存橫幅播發,以便每個使用者看到相同的播發。</span><span class="sxs-lookup"><span data-stu-id="3a001-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="3a001-114">你不會這樣賺錢的!</span><span class="sxs-lookup"><span data-stu-id="3a001-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="3a001-115">幸運的是,有一個簡單的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3a001-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="3a001-116">您可以利用稱為*快取後取代*ASP.NET 架構的功能。</span><span class="sxs-lookup"><span data-stu-id="3a001-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="3a001-117">快取後取代讓您能夠取代已快存在記憶體中的頁面中的動態內容。</span><span class="sxs-lookup"><span data-stu-id="3a001-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="3a001-118">通常,當您使用&lt;OutputCache&gt;屬性輸出快取頁面時,該頁將緩存在伺服器和用戶端(Web 瀏覽器)上。</span><span class="sxs-lookup"><span data-stu-id="3a001-118">Normally, when you output cache a page by using the &lt;OutputCache&gt; attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="3a001-119">使用緩存後替換時,頁面僅緩存在伺服器上。</span><span class="sxs-lookup"><span data-stu-id="3a001-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="3a001-120">使用快取後取代</span><span class="sxs-lookup"><span data-stu-id="3a001-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="3a001-121">使用緩存後替換需要兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="3a001-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="3a001-122">首先,您需要定義一個方法,該方法返回表示要在緩存頁中顯示的動態內容的字串。</span><span class="sxs-lookup"><span data-stu-id="3a001-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="3a001-123">接下來,調用 HttpResponse.Write 替代() 方法將動態內容注入頁面。</span><span class="sxs-lookup"><span data-stu-id="3a001-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="3a001-124">例如,假設您要在快取的頁面中隨機顯示不同的新聞專案。</span><span class="sxs-lookup"><span data-stu-id="3a001-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="3a001-125">清單 1 中的類公開一個名為 RenderNews()的方法,該方法從三個新聞項清單中隨機返回一個新聞項。</span><span class="sxs-lookup"><span data-stu-id="3a001-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="3a001-126">**清單1 = 模型\新聞.vb**</span><span class="sxs-lookup"><span data-stu-id="3a001-126">**Listing 1 – Models\News.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample1.vb)]

<span data-ttu-id="3a001-127">要利用緩存後替換,請致電 HttpResponse.Write 替代()方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="3a001-128">Write替代()方法設置代碼,以動態內容替換緩存頁的區域。</span><span class="sxs-lookup"><span data-stu-id="3a001-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="3a001-129">Write替代()方法用於在清單2的視圖中顯示隨機新聞項。</span><span class="sxs-lookup"><span data-stu-id="3a001-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="3a001-130">**清單 2 = 檢視\home_Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="3a001-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample2.aspx)]

<span data-ttu-id="3a001-131">渲染新聞方法傳遞給寫入替換() 方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="3a001-132">請注意,不調用 RenderNews 方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-132">Notice that the RenderNews method is not called.</span></span> <span data-ttu-id="3a001-133">相反,在 AddressOf 運算子的説明下,對該方法的引用傳遞給 Write 替代()。</span><span class="sxs-lookup"><span data-stu-id="3a001-133">Instead a reference to the method is passed to WriteSubstitution() with the help of the AddressOf operator.</span></span>

<span data-ttu-id="3a001-134">已緩存索引視圖。</span><span class="sxs-lookup"><span data-stu-id="3a001-134">The Index view is cached.</span></span> <span data-ttu-id="3a001-135">視圖由清單 3 中的控制器返回。</span><span class="sxs-lookup"><span data-stu-id="3a001-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="3a001-136">請注意,Index() 操作&lt;使用 OutputCache&gt;屬性進行修飾,該屬性會導致索引視圖緩存 60 秒。</span><span class="sxs-lookup"><span data-stu-id="3a001-136">Notice that the Index() action is decorated with an &lt;OutputCache&gt; attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="3a001-137">**清單3 = 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="3a001-137">**Listing 3 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample3.vb)]

<span data-ttu-id="3a001-138">即使快取了 Index 檢視,當您請求「索引」頁時,也會顯示不同的隨機新聞項。</span><span class="sxs-lookup"><span data-stu-id="3a001-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="3a001-139">請求「索引」頁時,頁面顯示的時間在 60 秒內不會更改(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="3a001-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="3a001-140">時間不變的事實證明頁面被緩存了。</span><span class="sxs-lookup"><span data-stu-id="3a001-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="3a001-141">但是,Write替代()方法(隨機新聞項)注入的內容隨每個請求而變化。</span><span class="sxs-lookup"><span data-stu-id="3a001-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="3a001-142">**圖 1 = 在快取的頁面中注入動態新聞專案**</span><span class="sxs-lookup"><span data-stu-id="3a001-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-vb/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="3a001-144">在說明器方法使用快取時取代</span><span class="sxs-lookup"><span data-stu-id="3a001-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="3a001-145">利用緩存後替換的一種更簡單的方法是在自定義説明器方法中封裝對 Write 替代() 方法的調用。</span><span class="sxs-lookup"><span data-stu-id="3a001-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="3a001-146">清單4中的説明方法說明了此方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="3a001-147">**清單4 = 說明者\AdHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="3a001-147">**Listing 4 – Helpers\AdHelper.vb**</span></span>

[!code-vb[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample4.vb)]

<span data-ttu-id="3a001-148">清單4包含一個可視化基本模組,該模組公開了兩種方法:渲染橫幅()和渲染橫幅內部()。</span><span class="sxs-lookup"><span data-stu-id="3a001-148">Listing 4 contains a Visual Basic module that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="3a001-149">RenderBanner() 方法表示實際幫助器方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="3a001-150">此方法擴展了標準ASP.NET MVC HtmlHelper 類,以便您可以像任何其他説明器方法一樣在視圖中調用 Html.RenderBanner()。</span><span class="sxs-lookup"><span data-stu-id="3a001-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="3a001-151">renderBanner() 方法呼叫將 RenderBanner 內部() 方法傳遞給 Write 取代() 方法的 HttpResponse.Write 替換() 方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="3a001-152">RenderBanner 內部() 方法是一種私有方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="3a001-153">此方法不會作為幫助器方法公開。</span><span class="sxs-lookup"><span data-stu-id="3a001-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="3a001-154">RenderBanner 內部() 方法從三個橫幅廣告圖像清單中隨機返回一個橫幅廣告圖像。</span><span class="sxs-lookup"><span data-stu-id="3a001-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="3a001-155">清單5中修改後的索引檢視說明了如何使用 RenderBanner() 説明器方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="3a001-156">請注意,在檢視&lt;頂部包含額外的&gt;%@ 匯入 % 指令,用於匯入 MvcApplication1.Helpers 命名空間。</span><span class="sxs-lookup"><span data-stu-id="3a001-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="3a001-157">如果忽略導入此命名空間,則 RenderBanner() 方法將不會顯示為 Html 屬性上的方法。</span><span class="sxs-lookup"><span data-stu-id="3a001-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="3a001-158">**清單 5 = 檢視\home_Index.aspx(使用 RenderBanner() 方法)**</span><span class="sxs-lookup"><span data-stu-id="3a001-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-vb/samples/sample5.aspx)]

<span data-ttu-id="3a001-159">請求清單 5 中由檢視呈現的頁面時,每個請求都會顯示不同的橫幅播發(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="3a001-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="3a001-160">頁面被緩存,但橫幅播發由 RenderBanner() 幫助器方法動態注入。</span><span class="sxs-lookup"><span data-stu-id="3a001-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="3a001-161">**圖 2 = 顯示隨機橫幅播發的索引檢視**</span><span class="sxs-lookup"><span data-stu-id="3a001-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-vb/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="3a001-163">總結</span><span class="sxs-lookup"><span data-stu-id="3a001-163">Summary</span></span>

<span data-ttu-id="3a001-164">本教程介紹了如何動態更新緩存頁中的內容。</span><span class="sxs-lookup"><span data-stu-id="3a001-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="3a001-165">您學習了如何使用 HttpResponse.Write 替代() 方法,以便將動態內容注入緩存頁面。</span><span class="sxs-lookup"><span data-stu-id="3a001-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="3a001-166">您還學習了如何在 HTML 說明器方法中封裝對 Write 替代() 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="3a001-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="3a001-167">盡可能利用快取, 會對 Web 應用程式的效能產生顯著影響。</span><span class="sxs-lookup"><span data-stu-id="3a001-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="3a001-168">如本教學中所述,即使您需要在頁面中顯示動態內容,您也可以利用緩存。</span><span class="sxs-lookup"><span data-stu-id="3a001-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3a001-169">[前一個](improving-performance-with-output-caching-vb.md)
> [下一個](creating-a-controller-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3a001-169">[Previous](improving-performance-with-output-caching-vb.md)
[Next](creating-a-controller-vb.md)</span></span>
