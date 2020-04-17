---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
title: 將數據傳遞到查看母版頁 (C#) |微軟文件
author: rick-anderson
description: 本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。 我們檢查將資料傳遞到檢視的兩種策略...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 5fee879b-8bde-42a9-a434-60ba6b1cf747
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a934f93d89e6530becc114fe455c8b3ab2968de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542478"
---
# <a name="passing-data-to-view-master-pages-c"></a><span data-ttu-id="d4237-104">將資料傳遞至檢視主版頁面 (C#)</span><span class="sxs-lookup"><span data-stu-id="d4237-104">Passing Data to View Master Pages (C#)</span></span>

<span data-ttu-id="d4237-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d4237-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d4237-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="d4237-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_CS.pdf)

> <span data-ttu-id="d4237-107">本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。</span><span class="sxs-lookup"><span data-stu-id="d4237-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="d4237-108">我們檢查將數據傳遞到檢視母版頁的兩種策略。</span><span class="sxs-lookup"><span data-stu-id="d4237-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="d4237-109">首先,我們討論一個簡單的解決方案,該解決方案會導致應用程式難以維護。</span><span class="sxs-lookup"><span data-stu-id="d4237-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="d4237-110">接下來,我們將研究一個更好的解決方案,它需要更多的初始工作,但會產生一個更可維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4237-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="d4237-111">將資料傳遞到檢視母版頁</span><span class="sxs-lookup"><span data-stu-id="d4237-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="d4237-112">本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。</span><span class="sxs-lookup"><span data-stu-id="d4237-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="d4237-113">我們檢查將數據傳遞到檢視母版頁的兩種策略。</span><span class="sxs-lookup"><span data-stu-id="d4237-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="d4237-114">首先,我們討論一個簡單的解決方案,該解決方案會導致應用程式難以維護。</span><span class="sxs-lookup"><span data-stu-id="d4237-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="d4237-115">接下來,我們將研究一個更好的解決方案,它需要更多的初始工作,但會產生一個更可維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d4237-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="d4237-116">問題</span><span class="sxs-lookup"><span data-stu-id="d4237-116">The Problem</span></span>

<span data-ttu-id="d4237-117">假設您正在建構影片資料庫應用程式,並且您想要在應用程式的每一頁上顯示影片類別清單(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="d4237-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="d4237-118">此外,假設影片類別清單存儲在資料庫表中。</span><span class="sxs-lookup"><span data-stu-id="d4237-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="d4237-119">在這種情況下,從資料庫中檢索類別並在視圖母版頁中呈現影片類別清單是有意義的。</span><span class="sxs-lookup"><span data-stu-id="d4237-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>

<span data-ttu-id="d4237-120">[![在檢視母版頁中顯示影片類別](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d4237-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-cs/_static/image2.png)](passing-data-to-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="d4237-121">**圖 01**: 在檢視母版頁中顯示影片類別 ([按下以檢視全尺寸影像](passing-data-to-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d4237-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="d4237-122">這就是問題所在。</span><span class="sxs-lookup"><span data-stu-id="d4237-122">Here's the problem.</span></span> <span data-ttu-id="d4237-123">如何檢索母版頁中的電影類別清單?</span><span class="sxs-lookup"><span data-stu-id="d4237-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="d4237-124">在母版頁中直接調用模型類的方法是很有誘惑力的。</span><span class="sxs-lookup"><span data-stu-id="d4237-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="d4237-125">換句話說,最好在母版頁中包含從資料庫檢索數據的代碼。</span><span class="sxs-lookup"><span data-stu-id="d4237-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="d4237-126">但是,繞過 MVC 控制器訪問資料庫將違反完全分離問題是構建 MVC 應用程式的主要好處之一。</span><span class="sxs-lookup"><span data-stu-id="d4237-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="d4237-127">在 MVC 應用程式中,您希望 MVC 視圖和 MVC 模型之間的所有互動都由 MVC 控制器處理。</span><span class="sxs-lookup"><span data-stu-id="d4237-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="d4237-128">這種關注點的分離產生了更可維護、適應性強和可測試的應用。</span><span class="sxs-lookup"><span data-stu-id="d4237-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="d4237-129">在 MVC 應用程式中,傳遞給檢視的所有數據(包括檢視母版頁)都應通過控制器操作傳遞到檢視。</span><span class="sxs-lookup"><span data-stu-id="d4237-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="d4237-130">此外,數據應利用視圖數據傳遞。</span><span class="sxs-lookup"><span data-stu-id="d4237-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="d4237-131">在本教程的其餘部分中,我將檢查將視圖數據傳遞到視圖母版頁的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="d4237-132">簡單解決方案</span><span class="sxs-lookup"><span data-stu-id="d4237-132">The Simple Solution</span></span>

<span data-ttu-id="d4237-133">讓我們從將檢視數據從控制器傳遞到視圖母版頁的最簡單的解決方案開始。</span><span class="sxs-lookup"><span data-stu-id="d4237-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="d4237-134">最簡單的解決方案是在每個控制器操作中傳遞母版頁的檢視數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="d4237-135">考慮清單 1 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="d4237-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="d4237-136">它公開名為`Index()`和`Details()`的兩個操作。</span><span class="sxs-lookup"><span data-stu-id="d4237-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="d4237-137">操作`Index()`方法返回「影片」資料庫表中的每個影片。</span><span class="sxs-lookup"><span data-stu-id="d4237-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="d4237-138">操作`Details()`方法返回特定影片類別中的每部電影。</span><span class="sxs-lookup"><span data-stu-id="d4237-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="d4237-139">**清單1 |`Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="d4237-139">**Listing 1 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample1.cs)]

<span data-ttu-id="d4237-140">請注意,Index() 和詳細資訊()操作都會添加兩個項來查看數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-140">Notice that both the Index() and the Details() actions add two items to view data.</span></span> <span data-ttu-id="d4237-141">索引() 操作添加了兩個鍵:類別和影片。</span><span class="sxs-lookup"><span data-stu-id="d4237-141">The Index() action adds two keys: categories and movies.</span></span> <span data-ttu-id="d4237-142">類別鍵表示檢視母版頁顯示的電影類別清單。</span><span class="sxs-lookup"><span data-stu-id="d4237-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="d4237-143">影片鍵表示「索引」檢視頁顯示的影片清單。</span><span class="sxs-lookup"><span data-stu-id="d4237-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="d4237-144">"詳細資訊"操作還添加了兩個名為類別和影片的鍵。</span><span class="sxs-lookup"><span data-stu-id="d4237-144">The Details() action also adds two keys named categories and movies.</span></span> <span data-ttu-id="d4237-145">類別鍵再次表示檢視母版頁顯示的電影類別清單。</span><span class="sxs-lookup"><span data-stu-id="d4237-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="d4237-146">影片鍵表示「詳細資訊」檢視頁顯示的特定類別中的電影清單(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="d4237-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>

<span data-ttu-id="d4237-147">[!["詳細資訊"檢視](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d4237-147">[![The Details view](passing-data-to-view-master-pages-cs/_static/image5.png)](passing-data-to-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="d4237-148">**圖 02**: 「詳細資訊」檢視 ([按下以檢視全尺寸影像](passing-data-to-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d4237-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-cs/_static/image6.png))</span></span>

<span data-ttu-id="d4237-149">索引檢視包含在清單 2 中。</span><span class="sxs-lookup"><span data-stu-id="d4237-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="d4237-150">它只是遍達視圖數據中由影片項表示的電影清單。</span><span class="sxs-lookup"><span data-stu-id="d4237-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="d4237-151">**清單2 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="d4237-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="d4237-152">視圖母版頁包含在清單 3 中。</span><span class="sxs-lookup"><span data-stu-id="d4237-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="d4237-153">視圖母版頁從檢視數據中參數地表示並呈現類別項表示的所有影片類別。</span><span class="sxs-lookup"><span data-stu-id="d4237-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="d4237-154">**清單3 |`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="d4237-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="d4237-155">所有數據都通過檢視數據傳遞到視圖和視圖母版頁。</span><span class="sxs-lookup"><span data-stu-id="d4237-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="d4237-156">這是將數據傳遞到母版頁的正確方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="d4237-157">那麼,這個解決方案有什麼問題呢?</span><span class="sxs-lookup"><span data-stu-id="d4237-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="d4237-158">問題是,此解決方案違反了DRY(不要重複自己)原則。</span><span class="sxs-lookup"><span data-stu-id="d4237-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="d4237-159">每個控制器操作都必須添加完全相同的影片類別清單才能查看數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="d4237-160">應用程式中具有重複的代碼會使應用程式更難維護、調整和修改。</span><span class="sxs-lookup"><span data-stu-id="d4237-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="d4237-161">良好的解決方案</span><span class="sxs-lookup"><span data-stu-id="d4237-161">The Good Solution</span></span>

<span data-ttu-id="d4237-162">在本節中,我們將檢查將數據從控制器操作傳遞到視圖母版頁的替代方法和更好的解決方案。</span><span class="sxs-lookup"><span data-stu-id="d4237-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="d4237-163">我們不是在每個控制器操作中添加母版頁的影片類別,而是僅將影片類別添加到視圖數據一次。</span><span class="sxs-lookup"><span data-stu-id="d4237-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="d4237-164">檢視母版頁使用的所有檢視數據都添加到應用程式控制器中。</span><span class="sxs-lookup"><span data-stu-id="d4237-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="d4237-165">應用程式控制器類包含在清單 4 中。</span><span class="sxs-lookup"><span data-stu-id="d4237-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="d4237-166">**清單4 |`Controllers\ApplicationController.cs`**</span><span class="sxs-lookup"><span data-stu-id="d4237-166">**Listing 4 – `Controllers\ApplicationController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample4.cs)]

<span data-ttu-id="d4237-167">關於清單4中的應用程式控制器,您應該注意三件事。</span><span class="sxs-lookup"><span data-stu-id="d4237-167">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="d4237-168">首先,請注意,類從基 System.Web.Mvc.Controller 類繼承。</span><span class="sxs-lookup"><span data-stu-id="d4237-168">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="d4237-169">應用程式控制器是控制器類。</span><span class="sxs-lookup"><span data-stu-id="d4237-169">The Application controller is a controller class.</span></span>

<span data-ttu-id="d4237-170">其次,請注意應用程式控制器類是一個抽象類。</span><span class="sxs-lookup"><span data-stu-id="d4237-170">Second, notice that the Application controller class is an abstract class.</span></span> <span data-ttu-id="d4237-171">抽象類是必須由具體類實現的類。</span><span class="sxs-lookup"><span data-stu-id="d4237-171">An abstract class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="d4237-172">由於應用程式控制器是抽象類,因此不能直接調用類中定義的任何方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-172">Because the Application controller is an abstract class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="d4237-173">如果嘗試直接調用應用程式類,則會收到"找不到資源"錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="d4237-173">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="d4237-174">第三,請注意,應用程式控制器包含一個構造函數,該構造函數添加要查看數據的影片類別清單。</span><span class="sxs-lookup"><span data-stu-id="d4237-174">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="d4237-175">從應用程式控制器繼承的每個控制器類都會自動調用應用程式控制器的建構函數。</span><span class="sxs-lookup"><span data-stu-id="d4237-175">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="d4237-176">每當對從應用程式控制器繼承的任何控制器調用任何操作時,影片類別將自動包含在視圖數據中。</span><span class="sxs-lookup"><span data-stu-id="d4237-176">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="d4237-177">清單 5 中的影片控制器從應用程式控制器繼承。</span><span class="sxs-lookup"><span data-stu-id="d4237-177">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="d4237-178">**清單5 |`Controllers\MoviesController.cs`**</span><span class="sxs-lookup"><span data-stu-id="d4237-178">**Listing 5 – `Controllers\MoviesController.cs`**</span></span>

[!code-csharp[Main](passing-data-to-view-master-pages-cs/samples/sample5.cs)]

<span data-ttu-id="d4237-179">與上一節中討論的「家庭控制器」一樣,電影控制器公開了名為`Index()`和`Details()`的兩種操作方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-179">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="d4237-180">請注意,檢視母版頁顯示的影片類別清單不會添加以查看 或`Index()``Details()`方法中的數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-180">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="d4237-181">由於「影片」控制器從應用程式控制器繼承,因此將添加影片類別清單以自動查看數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-181">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="d4237-182">請注意,此為視圖母版頁添加視圖數據的解決方案並不違反 DRY(不要重複自己)原則。</span><span class="sxs-lookup"><span data-stu-id="d4237-182">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="d4237-183">添加要查看數據的影片類別清單的代碼僅包含在一個位置:應用程式控制器的構造函數。</span><span class="sxs-lookup"><span data-stu-id="d4237-183">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="d4237-184">總結</span><span class="sxs-lookup"><span data-stu-id="d4237-184">Summary</span></span>

<span data-ttu-id="d4237-185">在本教程中,我們討論了將視圖數據從控制器傳遞到視圖母版頁的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-185">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="d4237-186">首先,我們研究了一種簡單但難以維持的方法。</span><span class="sxs-lookup"><span data-stu-id="d4237-186">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="d4237-187">在第一部分中,我們討論了如何在應用程式中的每個控制器操作中為視圖母版頁添加視圖數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-187">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="d4237-188">我們的結論是,這是一個糟糕的方法,因為它違反了DRY(不要重複自己)的原則。</span><span class="sxs-lookup"><span data-stu-id="d4237-188">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="d4237-189">接下來,我們研究了添加視圖母版頁所需的數據以查看數據更好的策略。</span><span class="sxs-lookup"><span data-stu-id="d4237-189">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="d4237-190">我們不是在每個控制器操作中添加檢視數據,而是在應用程式控制器中只添加一次視圖數據。</span><span class="sxs-lookup"><span data-stu-id="d4237-190">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="d4237-191">這樣,當將數據傳遞到ASP.NET MVC 應用程式中的檢視母版頁時,可以避免重複的代碼。</span><span class="sxs-lookup"><span data-stu-id="d4237-191">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d4237-192">[前一個](creating-page-layouts-with-view-master-pages-cs.md)
> [下一個](asp-net-mvc-views-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d4237-192">[Previous](creating-page-layouts-with-view-master-pages-cs.md)
[Next](asp-net-mvc-views-overview-vb.md)</span></span>
