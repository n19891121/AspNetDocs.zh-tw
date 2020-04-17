---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 瞭解操作篩選器 (VB) :微軟文件
author: rick-anderson
description: 本教學的目的是解釋操作篩選器。 操作篩選器是屬性,您可以套用控制器操作或整個控制器...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 70ab564bc1217f67874090d2ae6899d9bcd743a1
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542101"
---
# <a name="understanding-action-filters-vb"></a><span data-ttu-id="9fddb-104">了解動作篩選 (VB)</span><span class="sxs-lookup"><span data-stu-id="9fddb-104">Understanding Action Filters (VB)</span></span>

<span data-ttu-id="9fddb-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9fddb-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9fddb-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="9fddb-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> <span data-ttu-id="9fddb-107">本教學的目的是解釋操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="9fddb-108">操作篩選器是一個屬性,您可以應用於控制器操作(或整個控制器),該屬性修改操作的執行方式。</span><span class="sxs-lookup"><span data-stu-id="9fddb-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="9fddb-109">瞭解操作篩選器</span><span class="sxs-lookup"><span data-stu-id="9fddb-109">Understanding Action Filters</span></span>

<span data-ttu-id="9fddb-110">本教學的目的是解釋操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="9fddb-111">操作篩選器是一個屬性,您可以應用於控制器操作(或整個控制器),該屬性修改操作的執行方式。</span><span class="sxs-lookup"><span data-stu-id="9fddb-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="9fddb-112">ASP.NET MVC 框架包括多個操作篩選器:</span><span class="sxs-lookup"><span data-stu-id="9fddb-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="9fddb-113">輸出快取 - 此操作篩選器快取控制器操作的輸出,以指定的時間進行。</span><span class="sxs-lookup"><span data-stu-id="9fddb-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="9fddb-114">句柄錯誤 - 此操作篩選器處理執行控制器操作時引發的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9fddb-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="9fddb-115">授權 – 此操作篩選器使您能夠限制對特定使用者或角色的訪問。</span><span class="sxs-lookup"><span data-stu-id="9fddb-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="9fddb-116">您還可以創建自己的自定義操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="9fddb-117">例如,您可能希望創建自定義操作篩選器以實現自定義身份驗證系統。</span><span class="sxs-lookup"><span data-stu-id="9fddb-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="9fddb-118">或者,您可能希望創建一個操作篩選器,用於修改控制器操作返回的檢視數據。</span><span class="sxs-lookup"><span data-stu-id="9fddb-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="9fddb-119">在本教學中,您將瞭解如何從開始構建操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="9fddb-120">我們創建一個 Log 操作篩選器,將操作處理的不同階段記錄到可視化工作室輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9fddb-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="9fddb-121">使用操作篩選器</span><span class="sxs-lookup"><span data-stu-id="9fddb-121">Using an Action Filter</span></span>

<span data-ttu-id="9fddb-122">操作篩選器是屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-122">An action filter is an attribute.</span></span> <span data-ttu-id="9fddb-123">您可以將大多數操作篩選器應用於單個控制器操作或整個控制器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="9fddb-124">例如,清單 1 中的數據控制器`Index()`公開名為 返回當前時間的操作。</span><span class="sxs-lookup"><span data-stu-id="9fddb-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="9fddb-125">此操作使用`OutputCache`操作篩選器進行修飾。</span><span class="sxs-lookup"><span data-stu-id="9fddb-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="9fddb-126">此篩選器會導致將操作返回的值緩存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="9fddb-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="9fddb-127">**清單1 |`Controllers\DataController.vb`**</span><span class="sxs-lookup"><span data-stu-id="9fddb-127">**Listing 1 – `Controllers\DataController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

<span data-ttu-id="9fddb-128">如果透過網址/`Index()`資料/索引輸入瀏覽器的位址列並多次點擊「刷新」按鈕來重複呼叫該操作,則您將在 10 秒內看到相同的時間。</span><span class="sxs-lookup"><span data-stu-id="9fddb-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="9fddb-129">操作的`Index()`輸出緩存 10 秒(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="9fddb-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="9fddb-130">[![快取時間](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9fddb-130">[![Cached time](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)</span></span>

<span data-ttu-id="9fddb-131">**圖 01**: 快取時間 ([按下以檢視全尺寸影像](understanding-action-filters-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9fddb-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-vb/_static/image3.png))</span></span>

<span data-ttu-id="9fddb-132">在清單 1 中,單個操作`OutputCache`篩選器 (操作篩選器`Index()`)應用於 該方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="9fddb-133">如果需要,可以將多個操作篩選器應用於同一操作。</span><span class="sxs-lookup"><span data-stu-id="9fddb-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="9fddb-134">例如,您可能希望將和`OutputCache``HandleError`操作篩選器應用於同一操作。</span><span class="sxs-lookup"><span data-stu-id="9fddb-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="9fddb-135">在清單`OutputCache`1 中,操作篩選器套`Index()`用於操作 。</span><span class="sxs-lookup"><span data-stu-id="9fddb-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="9fddb-136">您還可以將此屬性應用於`DataController`類本身。</span><span class="sxs-lookup"><span data-stu-id="9fddb-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="9fddb-137">在這種情況下,控制器公開的任何操作返回的結果將被緩存 10 秒。</span><span class="sxs-lookup"><span data-stu-id="9fddb-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="9fddb-138">不同類型的過濾器</span><span class="sxs-lookup"><span data-stu-id="9fddb-138">The Different Types of Filters</span></span>

<span data-ttu-id="9fddb-139">ASP.NET MVC 框架支援四種不同類型的篩選器:</span><span class="sxs-lookup"><span data-stu-id="9fddb-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="9fddb-140">授權篩選器 =`IAuthorizationFilter`實現 屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="9fddb-141">操作篩選器 =`IActionFilter`實現 屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="9fddb-142">結果篩選器 =`IResultFilter`實現 屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="9fddb-143">異常篩選器 =`IExceptionFilter`實現 屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="9fddb-144">篩選器按上面列出的順序執行。</span><span class="sxs-lookup"><span data-stu-id="9fddb-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="9fddb-145">例如,授權篩選器始終在操作篩選器和異常篩選器始終在每一種其他類型的篩選器之後執行。</span><span class="sxs-lookup"><span data-stu-id="9fddb-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="9fddb-146">授權篩選器用於實現控制器操作的身份驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="9fddb-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="9fddb-147">例如,"授權"篩選器是授權篩選器的範例。</span><span class="sxs-lookup"><span data-stu-id="9fddb-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="9fddb-148">操作篩選器包含在控制器操作執行之前和之後執行的邏輯。</span><span class="sxs-lookup"><span data-stu-id="9fddb-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="9fddb-149">例如,可以使用操作篩選器修改控制器操作返回的檢視數據。</span><span class="sxs-lookup"><span data-stu-id="9fddb-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="9fddb-150">結果篩選器包含在執行檢視結果之前和之後執行的邏輯。</span><span class="sxs-lookup"><span data-stu-id="9fddb-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="9fddb-151">例如,您可能希望在檢視呈現給瀏覽器之前修改視圖結果。</span><span class="sxs-lookup"><span data-stu-id="9fddb-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="9fddb-152">異常篩選器是要運行的最後一種篩選器類型。</span><span class="sxs-lookup"><span data-stu-id="9fddb-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="9fddb-153">可以使用異常篩選器來處理控制器操作或控制器操作結果引發的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9fddb-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="9fddb-154">您還可以使用異常篩選器來記錄錯誤。</span><span class="sxs-lookup"><span data-stu-id="9fddb-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="9fddb-155">每種不同類型的篩選器都按特定順序執行。</span><span class="sxs-lookup"><span data-stu-id="9fddb-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="9fddb-156">如果要控制執行相同類型的篩選器的順序,則可以設置篩選器的 Order 屬性。</span><span class="sxs-lookup"><span data-stu-id="9fddb-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="9fddb-157">所有操作篩選器的基類別是類別`System.Web.Mvc.FilterAttribute`。</span><span class="sxs-lookup"><span data-stu-id="9fddb-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="9fddb-158">如果要實現特定類型的篩選器,則需要創建從基本篩選器類繼承的類,並實現一個或多個 I授權篩選器、IActionFilter、IResultFilter 或例外篩選器介面。</span><span class="sxs-lookup"><span data-stu-id="9fddb-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the IAuthorizationFilter, IActionFilter, IResultFilter, or ExceptionFilter interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="9fddb-159">基本操作篩選器屬性類別</span><span class="sxs-lookup"><span data-stu-id="9fddb-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="9fddb-160">為了更輕鬆地實現自定義操作篩選器,ASP.NET MVC 框架`ActionFilterAttribute`包括一個基本類。</span><span class="sxs-lookup"><span data-stu-id="9fddb-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="9fddb-161">此類實現`IActionFilter``IResultFilter`和介面並`Filter`從 類繼承。</span><span class="sxs-lookup"><span data-stu-id="9fddb-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="9fddb-162">此處的術語並不完全一致。</span><span class="sxs-lookup"><span data-stu-id="9fddb-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="9fddb-163">從技術上講,從 ActionFilterAttribute 類繼承的類既是操作篩選器,也是結果篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="9fddb-164">但是,在鬆散的意義上,單詞操作篩選器用於引用 mVC 框架中的任何類型的篩選器ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="9fddb-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="9fddb-165">基本操作篩選器屬性類別有您可以重寫的以下方法:</span><span class="sxs-lookup"><span data-stu-id="9fddb-165">The base ActionFilterAttribute class has the following methods that you can override:</span></span>

- <span data-ttu-id="9fddb-166">OnAction 執行 – 在執行控制器操作之前呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="9fddb-167">執行執行時 ─ 在執行控制器操作後呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="9fddb-168">OnResult 執行 – 在執行控制器操作結果之前呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="9fddb-169">OnResult 執行 - 在執行控制器操作結果後呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="9fddb-170">在下一節中,我們將瞭解如何實現每種不同方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="9fddb-171">建立紀錄操作篩選器</span><span class="sxs-lookup"><span data-stu-id="9fddb-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="9fddb-172">為了說明如何構建自定義操作篩選器,我們將創建一個自定義操作篩選器,將處理控制器操作的各個階段記錄到 Visual Studio 輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9fddb-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="9fddb-173">我們的`LogActionFilter`包含在清單2中。</span><span class="sxs-lookup"><span data-stu-id="9fddb-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="9fddb-174">**清單2 |`ActionFilters\LogActionFilter.vb`**</span><span class="sxs-lookup"><span data-stu-id="9fddb-174">**Listing 2 – `ActionFilters\LogActionFilter.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

<span data-ttu-id="9fddb-175">在清單`OnActionExecuting()`2`OnActionExecuted()``OnResultExecuting()``OnResultExecuted()`中 ,、、`Log()`和 方法都 調用 方法。</span><span class="sxs-lookup"><span data-stu-id="9fddb-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="9fddb-176">方法的名稱與目前路由資料會傳遞給方法`Log()`。</span><span class="sxs-lookup"><span data-stu-id="9fddb-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="9fddb-177">該方法`Log()`將消息寫入可視化工作室輸出視窗(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="9fddb-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="9fddb-178">[![寫入視覺化工作室輸出視窗](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9fddb-178">[![Writing to the Visual Studio Output window](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)</span></span>

<span data-ttu-id="9fddb-179">**圖 02**: 寫入視覺化工作室輸出視窗 ([按下以檢視全尺寸影像](understanding-action-filters-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9fddb-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-vb/_static/image6.png))</span></span>

<span data-ttu-id="9fddb-180">清單3中的主控制器說明了如何將 Log 操作篩選器應用於整個控制器類。</span><span class="sxs-lookup"><span data-stu-id="9fddb-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="9fddb-181">每當呼叫主控制器公開的任何操作(`Index()`方法或`About()`方法),處理操作的各個階段都會記錄到 Visual Studio 輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9fddb-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="9fddb-182">**清單3 |`Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="9fddb-182">**Listing 3 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a><span data-ttu-id="9fddb-183">總結</span><span class="sxs-lookup"><span data-stu-id="9fddb-183">Summary</span></span>

<span data-ttu-id="9fddb-184">在本教學中,您將被介紹到ASP.NET MVC 操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="9fddb-185">您瞭解了四種不同類型的篩選器:授權篩選器、操作篩選器、結果篩選器和異常篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="9fddb-186">您還瞭解了基`ActionFilterAttribute`類。</span><span class="sxs-lookup"><span data-stu-id="9fddb-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="9fddb-187">最後,您學習了如何實現簡單的操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="9fddb-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="9fddb-188">我們創建了一個 Log 操作篩選器,將處理控制器操作的各個階段記錄到可視化工作室輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="9fddb-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9fddb-189">[前一個](asp-net-mvc-routing-overview-vb.md)
> [下一個](improving-performance-with-output-caching-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9fddb-189">[Previous](asp-net-mvc-routing-overview-vb.md)
[Next](improving-performance-with-output-caching-vb.md)</span></span>
