---
title: ASP.NET Core 中 Razor 頁面的篩選條件方法
author: Rick-Anderson
description: 了解如何在 ASP.NET Core 中建立 Razor 頁面的篩選條件方法。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 04/05/2018
uid: razor-pages/filter
ms.openlocfilehash: 5b233d95c9fbab09c64072377b85b40b127df7b7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063425"
---
# <a name="filter-methods-for-razor-pages-in-aspnet-core"></a><span data-ttu-id="6b563-103">ASP.NET Core 中 Razor 頁面的篩選條件方法</span><span class="sxs-lookup"><span data-stu-id="6b563-103">Filter methods for Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="6b563-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6b563-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="6b563-105">Razor 頁面篩選條件 [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter?view=aspnetcore-2.0) 和 [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter?view=aspnetcore-2.0) 可讓 Razor 頁面在 Razor 頁面處理常式執行之前和之後執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b563-105">Razor Page filters [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter?view=aspnetcore-2.0) and [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter?view=aspnetcore-2.0) allow Razor Pages to run code before and after a Razor Page handler is run.</span></span> <span data-ttu-id="6b563-106">Razor 頁面篩選條件類似於 [ASP.NET Core MVC 動作篩選條件](xref:mvc/controllers/filters#action-filters)，但它們無法套用至個別的頁面處理常式方法。</span><span class="sxs-lookup"><span data-stu-id="6b563-106">Razor Page filters are similar to [ASP.NET Core MVC action filters](xref:mvc/controllers/filters#action-filters), except they can't be applied to individual page handler methods.</span></span> 

<span data-ttu-id="6b563-107">Razor 頁面篩選條件：</span><span class="sxs-lookup"><span data-stu-id="6b563-107">Razor Page filters:</span></span>

* <span data-ttu-id="6b563-108">在選取處理常式方法之後，但在進行模型繫結之前執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b563-108">Run code after a handler method has been selected, but before model binding occurs.</span></span>
* <span data-ttu-id="6b563-109">在執行處理常式方法之前，並在完成模型繫結之後執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b563-109">Run code before the handler method executes, after model binding is complete.</span></span>
* <span data-ttu-id="6b563-110">在執行處理常式方法之後執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6b563-110">Run code after the handler method executes.</span></span>
* <span data-ttu-id="6b563-111">可以在某個頁面或全域實作。</span><span class="sxs-lookup"><span data-stu-id="6b563-111">Can be implemented on a page or globally.</span></span>
* <span data-ttu-id="6b563-112">無法套用至特定頁面處理常式方法。</span><span class="sxs-lookup"><span data-stu-id="6b563-112">Cannot be applied to specific page handler methods.</span></span>

<span data-ttu-id="6b563-113">程式碼可以使用頁面的建構函式或中介軟體在執行處理常式方法之前執行，但只有 Razor 頁面篩選條件可以存取 [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_HttpContext)。</span><span class="sxs-lookup"><span data-stu-id="6b563-113">Code can be run before a handler method executes using the page constructor or middleware, but only Razor Page filters have access to [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_HttpContext).</span></span> <span data-ttu-id="6b563-114">篩選條件具有 [FilterContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.filtercontext?view=aspnetcore-2.0) 衍生參數，可提供對 `HttpContext` 的存取。</span><span class="sxs-lookup"><span data-stu-id="6b563-114">Filters have a [FilterContext](/dotnet/api/microsoft.aspnetcore.mvc.filters.filtercontext?view=aspnetcore-2.0) derived parameter, which provides access to `HttpContext`.</span></span> <span data-ttu-id="6b563-115">例如，[實作篩選條件屬性](#ifa)範例會將標頭新增至回應，這是無法使用建構函式或中介軟體完成的作業。</span><span class="sxs-lookup"><span data-stu-id="6b563-115">For example, the [Implement a filter attribute](#ifa) sample adds a header to the response, something that can't be done with constructors or middleware.</span></span>

<span data-ttu-id="6b563-116">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/filter/sample/PageFilter) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6b563-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-pages/filter/sample/PageFilter) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="6b563-117">Razor 頁面篩選條件提供下列方法，可在全域或頁面層級套用：</span><span class="sxs-lookup"><span data-stu-id="6b563-117">Razor Page filters provide the following methods, which can be applied globally or at the page level:</span></span>

* <span data-ttu-id="6b563-118">同步方法：</span><span class="sxs-lookup"><span data-stu-id="6b563-118">Synchronous methods:</span></span>

    * <span data-ttu-id="6b563-119">[OnPageHandlerSelected](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerselected?view=aspnetcore-2.0) :呼叫之後，已選取的處理常式方法，但模型之前發生繫結。</span><span class="sxs-lookup"><span data-stu-id="6b563-119">[OnPageHandlerSelected](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerselected?view=aspnetcore-2.0) : Called after a handler method has been selected, but before model binding occurs.</span></span>
    * <span data-ttu-id="6b563-120">[OnPageHandlerExecuting](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuting?view=aspnetcore-2.0) :執行處理常式方法，模型繫結後完成之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="6b563-120">[OnPageHandlerExecuting](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuting?view=aspnetcore-2.0) : Called before the handler method executes, after model binding is complete.</span></span>
    * <span data-ttu-id="6b563-121">[OnPageHandlerExecuted](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuted?view=aspnetcore-2.0) :之前的動作結果的處理常式方法執行之後呼叫。</span><span class="sxs-lookup"><span data-stu-id="6b563-121">[OnPageHandlerExecuted](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter.onpagehandlerexecuted?view=aspnetcore-2.0) : Called after the handler method executes, before the action result.</span></span>

* <span data-ttu-id="6b563-122">非同步方法：</span><span class="sxs-lookup"><span data-stu-id="6b563-122">Asynchronous methods:</span></span>

    * <span data-ttu-id="6b563-123">[OnPageHandlerSelectionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerselectionasync?view=aspnetcore-2.0) :在選取的處理常式方法之後，但模型繫結之前，請呼叫以非同步的方式。</span><span class="sxs-lookup"><span data-stu-id="6b563-123">[OnPageHandlerSelectionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerselectionasync?view=aspnetcore-2.0) : Called asynchronously after the handler method has been selected, but before model binding occurs.</span></span>
    * <span data-ttu-id="6b563-124">[OnPageHandlerExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerexecutionasync?view=aspnetcore-2.0) :之前的處理常式方法會叫用，模型繫結完成之後，請呼叫以非同步的方式。</span><span class="sxs-lookup"><span data-stu-id="6b563-124">[OnPageHandlerExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter.onpagehandlerexecutionasync?view=aspnetcore-2.0) : Called asynchronously before the handler method is invoked, after model binding is complete.</span></span>

> [!NOTE]
> <span data-ttu-id="6b563-125">請實作同步**或**非同步版本的篩選條件介面，但不要兩者同時實作。</span><span class="sxs-lookup"><span data-stu-id="6b563-125">Implement **either** the synchronous or the async version of a filter interface, not both.</span></span> <span data-ttu-id="6b563-126">架構會先檢查以查看篩選條件是否實作非同步介面，如果是的話，便呼叫該介面。</span><span class="sxs-lookup"><span data-stu-id="6b563-126">The framework checks first to see if the filter implements the async interface, and if so, it calls that.</span></span> <span data-ttu-id="6b563-127">如果沒有，它會呼叫同步介面的方法。</span><span class="sxs-lookup"><span data-stu-id="6b563-127">If not, it calls the synchronous interface's method(s).</span></span> <span data-ttu-id="6b563-128">如果實作了這兩個介面，則只會呼叫非同步方法。</span><span class="sxs-lookup"><span data-stu-id="6b563-128">If both interfaces are implemented, only the async methods are be called.</span></span> <span data-ttu-id="6b563-129">相同的規則會套用至頁面中的覆寫，實作覆寫的同步或非同步版本，但不能同時實作。</span><span class="sxs-lookup"><span data-stu-id="6b563-129">The same rule applies to overrides in pages, implement the synchronous or the async version of the override, not both.</span></span>

## <a name="implement-razor-page-filters-globally"></a><span data-ttu-id="6b563-130">全域實作 Razor 頁面篩選條件</span><span class="sxs-lookup"><span data-stu-id="6b563-130">Implement Razor Page filters globally</span></span>

<span data-ttu-id="6b563-131">下列程式碼會實作 `IAsyncPageFilter`：</span><span class="sxs-lookup"><span data-stu-id="6b563-131">The following code implements `IAsyncPageFilter`:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Filters/SampleAsyncPageFilter.cs?name=snippet1)]

<span data-ttu-id="6b563-132">在上述程式碼中，[ILogger](/dotnet/api/microsoft.extensions.logging.ilogger?view=aspnetcore-2.0) 並非必要。</span><span class="sxs-lookup"><span data-stu-id="6b563-132">In the preceding code, [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger?view=aspnetcore-2.0) is not required.</span></span> <span data-ttu-id="6b563-133">它在範例中用來提供應用程式的追蹤資訊。</span><span class="sxs-lookup"><span data-stu-id="6b563-133">It's used in the sample to provide trace information for the application.</span></span>

<span data-ttu-id="6b563-134">下列程式碼會啟用 `Startup` 類別中的 `SampleAsyncPageFilter`：</span><span class="sxs-lookup"><span data-stu-id="6b563-134">The following code enables the `SampleAsyncPageFilter` in the `Startup` class:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Startup.cs?name=snippet2&highlight=11)]

<span data-ttu-id="6b563-135">下列程式碼顯示完整的 `Startup` 類別：</span><span class="sxs-lookup"><span data-stu-id="6b563-135">The following code shows the complete `Startup` class:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Startup.cs?name=snippet1)]

<span data-ttu-id="6b563-136">下列程式碼會呼叫 `AddFolderApplicationModelConvention`，只將 `SampleAsyncPageFilter` 套用至 */subFolder* 中的頁面：</span><span class="sxs-lookup"><span data-stu-id="6b563-136">The following code calls `AddFolderApplicationModelConvention` to apply the `SampleAsyncPageFilter` to only pages in */subFolder*:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Startup2.cs?name=snippet2)]

<span data-ttu-id="6b563-137">下例程式碼會實作同步的 `IPageFilter`：</span><span class="sxs-lookup"><span data-stu-id="6b563-137">The following code implements the synchronous `IPageFilter`:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Filters/SamplePageFilter.cs?name=snippet1)]

<span data-ttu-id="6b563-138">下列程式碼會啟用 `SamplePageFilter`：</span><span class="sxs-lookup"><span data-stu-id="6b563-138">The following code enables the `SamplePageFilter`:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/StartupSync.cs?name=snippet2&highlight=11)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implement-razor-page-filters-by-overriding-filter-methods"></a><span data-ttu-id="6b563-139">覆寫篩選條件方法來實作 Razor 頁面篩選條件</span><span class="sxs-lookup"><span data-stu-id="6b563-139">Implement Razor Page filters by overriding filter methods</span></span>

<span data-ttu-id="6b563-140">下列程式碼會覆寫同步的 Razor 頁面篩選條件：</span><span class="sxs-lookup"><span data-stu-id="6b563-140">The following code overrides the synchronous Razor Page filters:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Pages/Index.cshtml.cs)]

::: moniker-end

<a name="ifa"></a>
## <a name="implement-a-filter-attribute"></a><span data-ttu-id="6b563-141">實作篩選條件屬性</span><span class="sxs-lookup"><span data-stu-id="6b563-141">Implement a filter attribute</span></span>

<span data-ttu-id="6b563-142">以內建屬性為基礎的篩選條件 [OnResultExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncresultfilter.onresultexecutionasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Filters_IAsyncResultFilter_OnResultExecutionAsync_Microsoft_AspNetCore_Mvc_Filters_ResultExecutingContext_Microsoft_AspNetCore_Mvc_Filters_ResultExecutionDelegate_) 可以進行子類別化。</span><span class="sxs-lookup"><span data-stu-id="6b563-142">The built-in attribute-based filter [OnResultExecutionAsync](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncresultfilter.onresultexecutionasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Filters_IAsyncResultFilter_OnResultExecutionAsync_Microsoft_AspNetCore_Mvc_Filters_ResultExecutingContext_Microsoft_AspNetCore_Mvc_Filters_ResultExecutionDelegate_) filter can be subclassed.</span></span> <span data-ttu-id="6b563-143">下列篩選條件會將標頭新增至回應：</span><span class="sxs-lookup"><span data-stu-id="6b563-143">The following filter adds a header to the response:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Filters/AddHeaderAttribute.cs)]

<span data-ttu-id="6b563-144">下列程式碼會套用 `AddHeader` 屬性：</span><span class="sxs-lookup"><span data-stu-id="6b563-144">The following code applies the `AddHeader` attribute:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Pages/Contact.cshtml.cs?name=snippet1)]

<span data-ttu-id="6b563-145">如需覆寫順序的指示，請參閱[覆寫預設順序](xref:mvc/controllers/filters#overriding-the-default-order)。</span><span class="sxs-lookup"><span data-stu-id="6b563-145">See [Overriding the default order](xref:mvc/controllers/filters#overriding-the-default-order) for instructions on overriding the order.</span></span>

<span data-ttu-id="6b563-146">如需從篩選條件縮短篩選管線的指示，請參閱[取消和縮短](xref:mvc/controllers/filters#cancellation-and-short-circuiting)。</span><span class="sxs-lookup"><span data-stu-id="6b563-146">See [Cancellation and short circuiting](xref:mvc/controllers/filters#cancellation-and-short-circuiting) for instructions to short-circuit the filter pipeline from a filter.</span></span> 

<a name="auth"></a>
## <a name="authorize-filter-attribute"></a><span data-ttu-id="6b563-147">授權篩選條件屬性</span><span class="sxs-lookup"><span data-stu-id="6b563-147">Authorize filter attribute</span></span>

<span data-ttu-id="6b563-148">[Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute?view=aspnetcore-2.0) 屬性可以套用至 `PageModel`：</span><span class="sxs-lookup"><span data-stu-id="6b563-148">The [Authorize](/dotnet/api/microsoft.aspnetcore.authorization.authorizeattribute?view=aspnetcore-2.0) attribute can be applied to a `PageModel`:</span></span>

[!code-csharp[Main](filter/sample/PageFilter/Pages/ModelWithAuthFilter.cshtml.cs?highlight=7)]
