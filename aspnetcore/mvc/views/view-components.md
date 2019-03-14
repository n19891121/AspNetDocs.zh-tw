---
title: 檢視 ASP.NET Core 中的元件
author: rick-anderson
description: 了解如何檢視 ASP.NET Core 中使用的元件，以及如何將這些元件新增到應用程式。
ms.author: riande
ms.date: 1/30/2019
uid: mvc/views/view-components
ms.openlocfilehash: d979c9480f7bffff993f0ea526bdc231b940baa2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049875"
---
# <a name="view-components-in-aspnet-core"></a><span data-ttu-id="0f211-103">檢視 ASP.NET Core 中的元件</span><span class="sxs-lookup"><span data-stu-id="0f211-103">View components in ASP.NET Core</span></span>

<span data-ttu-id="0f211-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0f211-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0f211-105">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="0f211-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="view-components"></a><span data-ttu-id="0f211-106">檢視元件</span><span class="sxs-lookup"><span data-stu-id="0f211-106">View components</span></span>

<span data-ttu-id="0f211-107">檢視元件與部分檢視類似，但功能更強大。</span><span class="sxs-lookup"><span data-stu-id="0f211-107">View components are similar to partial views, but they're much more powerful.</span></span> <span data-ttu-id="0f211-108">檢視元件不會使用模型繫結，並且只取決於呼叫它時所提供的資料。</span><span class="sxs-lookup"><span data-stu-id="0f211-108">View components don't use model binding, and only depend on the data provided when calling into it.</span></span> <span data-ttu-id="0f211-109">此文章是使用控制器與檢視所撰寫，但檢視元件也能搭配 Razor Pages 使用。</span><span class="sxs-lookup"><span data-stu-id="0f211-109">This article was written using controllers and views, but view components also work with Razor Pages.</span></span>

<span data-ttu-id="0f211-110">檢視元件：</span><span class="sxs-lookup"><span data-stu-id="0f211-110">A view component:</span></span>

* <span data-ttu-id="0f211-111">轉譯區塊，而不是整個回應。</span><span class="sxs-lookup"><span data-stu-id="0f211-111">Renders a chunk rather than a whole response.</span></span>
* <span data-ttu-id="0f211-112">包含控制器與檢視之間的相同關注點分離和可測試性優點。</span><span class="sxs-lookup"><span data-stu-id="0f211-112">Includes the same separation-of-concerns and testability benefits found between a controller and view.</span></span>
* <span data-ttu-id="0f211-113">可以有參數和商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="0f211-113">Can have parameters and business logic.</span></span>
* <span data-ttu-id="0f211-114">它通常是從配置頁面叫用。</span><span class="sxs-lookup"><span data-stu-id="0f211-114">Is typically invoked from a layout page.</span></span>

<span data-ttu-id="0f211-115">如果您的可重複使用轉譯邏輯對於部分檢視而言太過複雜，則檢視元件是處理它的預定位置，例如：</span><span class="sxs-lookup"><span data-stu-id="0f211-115">View components are intended anywhere you have reusable rendering logic that's too complex for a partial view, such as:</span></span>

* <span data-ttu-id="0f211-116">動態導覽功能表</span><span class="sxs-lookup"><span data-stu-id="0f211-116">Dynamic navigation menus</span></span>
* <span data-ttu-id="0f211-117">標籤雲端 (可在其中查詢資料庫)</span><span class="sxs-lookup"><span data-stu-id="0f211-117">Tag cloud (where it queries the database)</span></span>
* <span data-ttu-id="0f211-118">登入面板</span><span class="sxs-lookup"><span data-stu-id="0f211-118">Login panel</span></span>
* <span data-ttu-id="0f211-119">購物車</span><span class="sxs-lookup"><span data-stu-id="0f211-119">Shopping cart</span></span>
* <span data-ttu-id="0f211-120">最近發行的文章</span><span class="sxs-lookup"><span data-stu-id="0f211-120">Recently published articles</span></span>
* <span data-ttu-id="0f211-121">一般部落格上的資訊看板內容</span><span class="sxs-lookup"><span data-stu-id="0f211-121">Sidebar content on a typical blog</span></span>
* <span data-ttu-id="0f211-122">登入面板，將在每個頁面上轉譯並根據使用者登入狀態來示範登出或登入連結</span><span class="sxs-lookup"><span data-stu-id="0f211-122">A login panel that would be rendered on every page and show either the links to log out or log in, depending on the log in state of the user</span></span>

<span data-ttu-id="0f211-123">檢視元件是由兩個部分所組成：類別 (通常衍生自 [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) 以及它所傳回的結果 (通常是檢視)。</span><span class="sxs-lookup"><span data-stu-id="0f211-123">A view component consists of two parts: the class (typically derived from [ViewComponent](/dotnet/api/microsoft.aspnetcore.mvc.viewcomponent)) and the result it returns (typically a view).</span></span> <span data-ttu-id="0f211-124">與控制器類似，檢視元件可以是 POCO，但大部分開發人員會想要利用透過衍生自 `ViewComponent` 而取得的方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="0f211-124">Like controllers, a view component can be a POCO, but most developers will want to take advantage of the methods and properties available by deriving from `ViewComponent`.</span></span>

## <a name="creating-a-view-component"></a><span data-ttu-id="0f211-125">建立檢視元件</span><span class="sxs-lookup"><span data-stu-id="0f211-125">Creating a view component</span></span>

<span data-ttu-id="0f211-126">本節包含建立檢視元件的高階需求。</span><span class="sxs-lookup"><span data-stu-id="0f211-126">This section contains the high-level requirements to create a view component.</span></span> <span data-ttu-id="0f211-127">在本文稍後，我們會詳細檢查每個步驟，並建立檢視元件。</span><span class="sxs-lookup"><span data-stu-id="0f211-127">Later in the article, we'll examine each step in detail and create a view component.</span></span>

### <a name="the-view-component-class"></a><span data-ttu-id="0f211-128">檢視元件類別</span><span class="sxs-lookup"><span data-stu-id="0f211-128">The view component class</span></span>

<span data-ttu-id="0f211-129">您可以透過下列任一項來建立檢視元件類別：</span><span class="sxs-lookup"><span data-stu-id="0f211-129">A view component class can be created by any of the following:</span></span>

* <span data-ttu-id="0f211-130">衍生自 *ViewComponent*</span><span class="sxs-lookup"><span data-stu-id="0f211-130">Deriving from *ViewComponent*</span></span>
* <span data-ttu-id="0f211-131">以 `[ViewComponent]` 屬性裝飾類別，或衍生自具有 `[ViewComponent]` 屬性的類別</span><span class="sxs-lookup"><span data-stu-id="0f211-131">Decorating a class with the `[ViewComponent]` attribute, or deriving from a class with the `[ViewComponent]` attribute</span></span>
* <span data-ttu-id="0f211-132">建立名稱結尾為尾碼 *ViewComponent* 的類別</span><span class="sxs-lookup"><span data-stu-id="0f211-132">Creating a class where the name ends with the suffix *ViewComponent*</span></span>

<span data-ttu-id="0f211-133">與控制器類似，檢視元件必須是公用、非巢狀和非抽象類別。</span><span class="sxs-lookup"><span data-stu-id="0f211-133">Like controllers, view components must be public, non-nested, and non-abstract classes.</span></span> <span data-ttu-id="0f211-134">檢視元件名稱是移除 "ViewComponent" 尾碼的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-134">The view component name is the class name with the "ViewComponent" suffix removed.</span></span> <span data-ttu-id="0f211-135">它也可以使用 `ViewComponentAttribute.Name` 屬性明確地指定。</span><span class="sxs-lookup"><span data-stu-id="0f211-135">It can also be explicitly specified using the `ViewComponentAttribute.Name` property.</span></span>

<span data-ttu-id="0f211-136">檢視元件類別：</span><span class="sxs-lookup"><span data-stu-id="0f211-136">A view component class:</span></span>

* <span data-ttu-id="0f211-137">完全支援建構函式[相依性插入](../../fundamentals/dependency-injection.md)</span><span class="sxs-lookup"><span data-stu-id="0f211-137">Fully supports constructor [dependency injection](../../fundamentals/dependency-injection.md)</span></span>

* <span data-ttu-id="0f211-138">不參與控制器生命週期，這表示您無法在檢視元件中使用[篩選](../controllers/filters.md)</span><span class="sxs-lookup"><span data-stu-id="0f211-138">Doesn't take part in the controller lifecycle, which means you can't use [filters](../controllers/filters.md) in a view component</span></span>

### <a name="view-component-methods"></a><span data-ttu-id="0f211-139">檢視元件方法</span><span class="sxs-lookup"><span data-stu-id="0f211-139">View component methods</span></span>

<span data-ttu-id="0f211-140">檢視元件會在傳回 `Task<IViewComponentResult>` 的 `InvokeAsync` 方法或傳回 `IViewComponentResult` 的同步 `Invoke` 方法中定義其邏輯。</span><span class="sxs-lookup"><span data-stu-id="0f211-140">A view component defines its logic in an `InvokeAsync` method that returns a `Task<IViewComponentResult>` or in a synchronous `Invoke` method that returns an `IViewComponentResult`.</span></span> <span data-ttu-id="0f211-141">參數直接來自檢視元件的引動過程，而不是來自模型繫結。</span><span class="sxs-lookup"><span data-stu-id="0f211-141">Parameters come directly from invocation of the view component, not from model binding.</span></span> <span data-ttu-id="0f211-142">檢視元件絕不會直接處理要求。</span><span class="sxs-lookup"><span data-stu-id="0f211-142">A view component never directly handles a request.</span></span> <span data-ttu-id="0f211-143">通常，檢視元件會初始化模型，並呼叫 `View` 方法將其傳遞至檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-143">Typically, a view component initializes a model and passes it to a view by calling the `View` method.</span></span> <span data-ttu-id="0f211-144">簡要來說，檢視元件方法：</span><span class="sxs-lookup"><span data-stu-id="0f211-144">In summary, view component methods:</span></span>

* <span data-ttu-id="0f211-145">定義傳回 `Task<IViewComponentResult>` 的 `InvokeAsync` 方法或傳回 `IViewComponentResult` 的同步 `Invoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="0f211-145">Define an `InvokeAsync` method that returns a `Task<IViewComponentResult>` or a synchronous `Invoke` method that returns an `IViewComponentResult`.</span></span>
* <span data-ttu-id="0f211-146">通常會初始化模型，並呼叫 `ViewComponent` `View` 方法將其傳遞至檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-146">Typically initializes a model and passes it to a view by calling the `ViewComponent` `View` method.</span></span>
* <span data-ttu-id="0f211-147">參數來自呼叫端方法，而非 HTTP。</span><span class="sxs-lookup"><span data-stu-id="0f211-147">Parameters come from the calling method, not HTTP.</span></span> <span data-ttu-id="0f211-148">沒有模型繫結。</span><span class="sxs-lookup"><span data-stu-id="0f211-148">There's no model binding.</span></span>
* <span data-ttu-id="0f211-149">無法直接當成 HTTP 端點連接。</span><span class="sxs-lookup"><span data-stu-id="0f211-149">Are not reachable directly as an HTTP endpoint.</span></span> <span data-ttu-id="0f211-150">它們是透過您的程式碼所叫用 (通常是在檢視中)。</span><span class="sxs-lookup"><span data-stu-id="0f211-150">They're invoked from your code (usually in a view).</span></span> <span data-ttu-id="0f211-151">檢視元件絕不會處理要求。</span><span class="sxs-lookup"><span data-stu-id="0f211-151">A view component never handles a request.</span></span>
* <span data-ttu-id="0f211-152">已多載在簽章上，而非目前 HTTP 要求中的任何詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f211-152">Are overloaded on the signature rather than any details from the current HTTP request.</span></span>

### <a name="view-search-path"></a><span data-ttu-id="0f211-153">檢視搜尋路徑</span><span class="sxs-lookup"><span data-stu-id="0f211-153">View search path</span></span>

<span data-ttu-id="0f211-154">執行階段會搜尋下列路徑中的檢視：</span><span class="sxs-lookup"><span data-stu-id="0f211-154">The runtime searches for the view in the following paths:</span></span>

* <span data-ttu-id="0f211-155">/Views/{控制器名稱}/Components/{檢視元件名稱}/{檢視名稱}</span><span class="sxs-lookup"><span data-stu-id="0f211-155">/Views/{Controller Name}/Components/{View Component Name}/{View Name}</span></span>
* <span data-ttu-id="0f211-156">/Views/Shared/Components/{檢視元件名稱}/{檢視名稱}</span><span class="sxs-lookup"><span data-stu-id="0f211-156">/Views/Shared/Components/{View Component Name}/{View Name}</span></span>
* <span data-ttu-id="0f211-157">/Pages/Shared/Components/{檢視元件名稱}/{檢視名稱}</span><span class="sxs-lookup"><span data-stu-id="0f211-157">/Pages/Shared/Components/{View Component Name}/{View Name}</span></span>

<span data-ttu-id="0f211-158">搜尋路徑適用於使用控制器 + 檢視和 Razor Pages 的專案。</span><span class="sxs-lookup"><span data-stu-id="0f211-158">The search path applies to projects using controllers + views and Razor Pages.</span></span>

<span data-ttu-id="0f211-159">檢視元件的預設檢視名稱是 *Default*，這表示您的檢視檔案通常會命名為 *Default.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="0f211-159">The default view name for a view component is *Default*, which means your view file will typically be named *Default.cshtml*.</span></span> <span data-ttu-id="0f211-160">建立檢視元件結果時，或呼叫 `View` 方法時，可以指定不同的檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-160">You can specify a different view name when creating the view component result or when calling the `View` method.</span></span>

<span data-ttu-id="0f211-161">建議您將檢視檔案命名為 *Default.cshtml*，並使用 *Views/Shared/Components/{View Component Name}/{View Name}* 路徑。</span><span class="sxs-lookup"><span data-stu-id="0f211-161">We recommend you name the view file *Default.cshtml* and use the *Views/Shared/Components/{View Component Name}/{View Name}* path.</span></span> <span data-ttu-id="0f211-162">此範例中所使用的 `PriorityList` 檢視元件會將 *Views/Shared/Components/PriorityList/Default.cshtml* 用於檢視元件檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-162">The `PriorityList` view component used in this sample uses *Views/Shared/Components/PriorityList/Default.cshtml* for the view component view.</span></span>

## <a name="invoking-a-view-component"></a><span data-ttu-id="0f211-163">叫用檢視元件</span><span class="sxs-lookup"><span data-stu-id="0f211-163">Invoking a view component</span></span>

<span data-ttu-id="0f211-164">若要使用檢視元件，請在檢視內呼叫下列項目：</span><span class="sxs-lookup"><span data-stu-id="0f211-164">To use the view component, call the following inside a view:</span></span>

```cshtml
@await Component.InvokeAsync("Name of view component", {Anonymous Type Containing Parameters})
```

<span data-ttu-id="0f211-165">參數將傳遞給 `InvokeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="0f211-165">The parameters will be passed to the `InvokeAsync` method.</span></span> <span data-ttu-id="0f211-166">本文中所開發的 `PriorityList` 檢視元件是透過 *Views/ToDO/Index.cshtml* 檢視檔案所叫用。</span><span class="sxs-lookup"><span data-stu-id="0f211-166">The `PriorityList` view component developed in the article is invoked from the *Views/ToDo/Index.cshtml* view file.</span></span> <span data-ttu-id="0f211-167">在下列範例中，`InvokeAsync` 方法是使用兩個參數所呼叫：</span><span class="sxs-lookup"><span data-stu-id="0f211-167">In the following, the `InvokeAsync` method is called with two parameters:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

::: moniker range=">= aspnetcore-1.1"

## <a name="invoking-a-view-component-as-a-tag-helper"></a><span data-ttu-id="0f211-168">叫用檢視元件作為標籤協助程式</span><span class="sxs-lookup"><span data-stu-id="0f211-168">Invoking a view component as a Tag Helper</span></span>

<span data-ttu-id="0f211-169">針對 ASP.NET Core 1.1 和更新版本，您可以叫用檢視元件作為[標籤協助程式](xref:mvc/views/tag-helpers/intro)：</span><span class="sxs-lookup"><span data-stu-id="0f211-169">For ASP.NET Core 1.1 and higher, you can invoke a view component as a [Tag Helper](xref:mvc/views/tag-helpers/intro):</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="0f211-170">標籤協助程式依照 Pascal 命名法大小寫慣例的類別和方法參數會轉譯成其 [Kebab 字體](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101)。</span><span class="sxs-lookup"><span data-stu-id="0f211-170">Pascal-cased class and method parameters for Tag Helpers are translated into their [kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="0f211-171">用來叫用檢視元件的標籤協助程式會使用 `<vc></vc>` 項目。</span><span class="sxs-lookup"><span data-stu-id="0f211-171">The Tag Helper to invoke a view component uses the `<vc></vc>` element.</span></span> <span data-ttu-id="0f211-172">檢視元件指定如下：</span><span class="sxs-lookup"><span data-stu-id="0f211-172">The view component is specified as follows:</span></span>

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

<span data-ttu-id="0f211-173">若要使用檢視元件作為標籤協助程式，請使用 `@addTagHelper` 指示詞註冊包含檢視元件的組件。</span><span class="sxs-lookup"><span data-stu-id="0f211-173">To use a view component as a Tag Helper, register the assembly containing the view component using the `@addTagHelper` directive.</span></span> <span data-ttu-id="0f211-174">如果檢視元件位於稱為 `MyWebApp` 的組件中，則請將下列指示詞新增至 *_ViewImports.cshtml* 檔案：</span><span class="sxs-lookup"><span data-stu-id="0f211-174">If your view component is in an assembly called `MyWebApp`, add the following directive to the *_ViewImports.cshtml* file:</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="0f211-175">您可以將檢視元件註冊為任何參考檢視元件的檔案標籤協助程式。</span><span class="sxs-lookup"><span data-stu-id="0f211-175">You can register a view component as a Tag Helper to any file that references the view component.</span></span> <span data-ttu-id="0f211-176">如需如何註冊標籤協助程式的詳細資訊，請參閱[管理標籤協助程式範圍](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope)。</span><span class="sxs-lookup"><span data-stu-id="0f211-176">See [Managing Tag Helper Scope](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) for more information on how to register Tag Helpers.</span></span>

<span data-ttu-id="0f211-177">本教學課程中使用的 `InvokeAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="0f211-177">The `InvokeAsync` method used in this tutorial:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="0f211-178">在標籤 (tag) 協助程式標籤 (markup) 中：</span><span class="sxs-lookup"><span data-stu-id="0f211-178">In Tag Helper markup:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="0f211-179">在上述範例中，`PriorityList` 檢視元件會變成 `priority-list`。</span><span class="sxs-lookup"><span data-stu-id="0f211-179">In the sample above, the `PriorityList` view component becomes `priority-list`.</span></span> <span data-ttu-id="0f211-180">檢視元件的參數會以 Kebab 字體傳遞為屬性。</span><span class="sxs-lookup"><span data-stu-id="0f211-180">The parameters to the view component are passed as attributes in kebab case.</span></span>

::: moniker-end

### <a name="invoking-a-view-component-directly-from-a-controller"></a><span data-ttu-id="0f211-181">直接從控制器叫用檢視元件</span><span class="sxs-lookup"><span data-stu-id="0f211-181">Invoking a view component directly from a controller</span></span>

<span data-ttu-id="0f211-182">檢視元件通常是從檢視中進行叫用，但您可以直接從控制器方法叫用它們。</span><span class="sxs-lookup"><span data-stu-id="0f211-182">View components are typically invoked from a view, but you can invoke them directly from a controller method.</span></span> <span data-ttu-id="0f211-183">雖然檢視元件不會定義控制器這類端點，但您可以輕鬆地實作控制器動作，以傳回 `ViewComponentResult` 的內容。</span><span class="sxs-lookup"><span data-stu-id="0f211-183">While view components don't define endpoints like controllers, you can easily implement a controller action that returns the content of a `ViewComponentResult`.</span></span>

<span data-ttu-id="0f211-184">在此範例中，是直接從控制器呼叫檢視元件：</span><span class="sxs-lookup"><span data-stu-id="0f211-184">In this example, the view component is called directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a><span data-ttu-id="0f211-185">逐步解說：建立簡單的檢視元件</span><span class="sxs-lookup"><span data-stu-id="0f211-185">Walkthrough: Creating a simple view component</span></span>

<span data-ttu-id="0f211-186">[下載](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample)、建置和測試起始程式碼。</span><span class="sxs-lookup"><span data-stu-id="0f211-186">[Download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), build and test the starter code.</span></span> <span data-ttu-id="0f211-187">它是具有 `ToDo` 控制器的簡單專案，而此控制器顯示 *ToDO* 項目清單。</span><span class="sxs-lookup"><span data-stu-id="0f211-187">It's a simple project with a `ToDo` controller that displays a list of *ToDo* items.</span></span>

![ToDos 清單](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a><span data-ttu-id="0f211-189">新增 ViewComponent 類別</span><span class="sxs-lookup"><span data-stu-id="0f211-189">Add a ViewComponent class</span></span>

<span data-ttu-id="0f211-190">建立 *ViewComponents* 資料夾，並新增下列 `PriorityListViewComponent` 類別：</span><span class="sxs-lookup"><span data-stu-id="0f211-190">Create a *ViewComponents* folder and add the following `PriorityListViewComponent` class:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

<span data-ttu-id="0f211-191">程式碼的注意事項：</span><span class="sxs-lookup"><span data-stu-id="0f211-191">Notes on the code:</span></span>

* <span data-ttu-id="0f211-192">檢視元件類別可以包含在專案的**任何**資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0f211-192">View component classes can be contained in **any** folder in the project.</span></span>
* <span data-ttu-id="0f211-193">因為類別名稱 PriorityList**ViewComponent** 結尾為尾碼 **ViewComponent**，所以從檢視參考類別元件時，執行階段會使用字串 "PriorityList"。</span><span class="sxs-lookup"><span data-stu-id="0f211-193">Because the class name PriorityList**ViewComponent** ends with the suffix **ViewComponent**, the runtime will use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="0f211-194">我稍後將更詳細地進行說明。</span><span class="sxs-lookup"><span data-stu-id="0f211-194">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="0f211-195">`[ViewComponent]` 屬性可以變更用來參考檢視元件的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-195">The `[ViewComponent]` attribute can change the name used to reference a view component.</span></span> <span data-ttu-id="0f211-196">例如，我們無法將類別命名為 `XYZ` 以及套用 `ViewComponent` 屬性：</span><span class="sxs-lookup"><span data-stu-id="0f211-196">For example, we could've named the class `XYZ` and applied the `ViewComponent` attribute:</span></span>

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* <span data-ttu-id="0f211-197">上面的 `[ViewComponent]` 屬性會告知檢視元件選取器在尋找與元件建立關聯的檢視時使用名稱 `PriorityList`，以及在從檢視參考類別元件時使用字串 "PriorityList"。</span><span class="sxs-lookup"><span data-stu-id="0f211-197">The `[ViewComponent]` attribute above tells the view component selector to use the name `PriorityList` when looking for the views associated with the component, and to use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="0f211-198">我稍後將更詳細地進行說明。</span><span class="sxs-lookup"><span data-stu-id="0f211-198">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="0f211-199">元件會使用[相依性插入](../../fundamentals/dependency-injection.md)，讓資料內容可供使用。</span><span class="sxs-lookup"><span data-stu-id="0f211-199">The component uses [dependency injection](../../fundamentals/dependency-injection.md) to make the data context available.</span></span>
* <span data-ttu-id="0f211-200">`InvokeAsync` 會公開可以從檢視中呼叫的方法，而且可以採用任意數目的引數。</span><span class="sxs-lookup"><span data-stu-id="0f211-200">`InvokeAsync` exposes a method which can be called from a view, and it can take an arbitrary number of arguments.</span></span>
* <span data-ttu-id="0f211-201">`InvokeAsync` 方法會傳回一組符合 `isDone` 和 `maxPriority` 參數的 `ToDo` 項目。</span><span class="sxs-lookup"><span data-stu-id="0f211-201">The `InvokeAsync` method returns the set of `ToDo` items that satisfy the `isDone` and `maxPriority` parameters.</span></span>

### <a name="create-the-view-component-razor-view"></a><span data-ttu-id="0f211-202">建立檢視元件 Razor 檢視</span><span class="sxs-lookup"><span data-stu-id="0f211-202">Create the view component Razor view</span></span>

* <span data-ttu-id="0f211-203">建立 *Views/Shared/Components* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f211-203">Create the *Views/Shared/Components* folder.</span></span> <span data-ttu-id="0f211-204">此資料夾**必須**命名為 *Components*。</span><span class="sxs-lookup"><span data-stu-id="0f211-204">This folder **must** be named *Components*.</span></span>

* <span data-ttu-id="0f211-205">建立 *Views/Shared/Components/PriorityList* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f211-205">Create the *Views/Shared/Components/PriorityList* folder.</span></span> <span data-ttu-id="0f211-206">此資料夾名稱必須符合檢視元件類別的名稱，或去掉尾碼的類別名稱 (如果我們遵循慣例，並在類別名稱中使用 *ViewComponent* 尾碼)。</span><span class="sxs-lookup"><span data-stu-id="0f211-206">This folder name must match the name of the view component class, or the name of the class minus the suffix (if we followed convention and used the *ViewComponent* suffix in the class name).</span></span> <span data-ttu-id="0f211-207">如果您已使用 `ViewComponent` 屬性，則類別名稱需要符合屬性指定。</span><span class="sxs-lookup"><span data-stu-id="0f211-207">If you used the `ViewComponent` attribute, the class name would need to match the attribute designation.</span></span>

* <span data-ttu-id="0f211-208">建立 *Views/Shared/Components/PriorityList/Default.cshtml* Razor 檢視：[!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="0f211-208">Create a *Views/Shared/Components/PriorityList/Default.cshtml* Razor view: [!code-cshtml[](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span></span>

   <span data-ttu-id="0f211-209">Razor 檢視採用 `TodoItem` 清單，並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="0f211-209">The Razor view takes a list of `TodoItem` and displays them.</span></span> <span data-ttu-id="0f211-210">如果檢視元件 `InvokeAsync` 方法未傳遞檢視名稱 (如我們的範例所示)，則依照慣例會使用 *Default* 作為檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-210">If the view component `InvokeAsync` method doesn't pass the name of the view (as in our sample), *Default* is used for the view name by convention.</span></span> <span data-ttu-id="0f211-211">在教學課程稍後，我將示範如何傳遞檢視的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-211">Later in the tutorial, I'll show you how to pass the name of the view.</span></span> <span data-ttu-id="0f211-212">若要覆寫特定控制器的預設樣式，請在控制器特定檢視資料夾中新增檢視 (例如 *Views/ToDO/Components/PriorityList/Default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="0f211-212">To override the default styling for a specific controller, add a view to the controller-specific view folder (for example *Views/ToDo/Components/PriorityList/Default.cshtml)*.</span></span>

    <span data-ttu-id="0f211-213">如果檢視元件是控制器特有的，則可以將它新增至控制器特定資料夾 (*Views/ToDO/Components/PriorityList/Default.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="0f211-213">If the view component is controller-specific, you can add it to the controller-specific folder (*Views/ToDo/Components/PriorityList/Default.cshtml*).</span></span>

* <span data-ttu-id="0f211-214">將包含優先順序清單元件呼叫的 `div` 新增至 *Views/ToDO/index.cshtml* 檔案底端：</span><span class="sxs-lookup"><span data-stu-id="0f211-214">Add a `div` containing a call to the priority list component to the bottom of the *Views/ToDo/index.cshtml* file:</span></span>

    [!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFirst.cshtml?range=34-38)]

<span data-ttu-id="0f211-215">`@await Component.InvokeAsync` 標記顯示呼叫檢視元件的語法。</span><span class="sxs-lookup"><span data-stu-id="0f211-215">The markup `@await Component.InvokeAsync` shows the syntax for calling view components.</span></span> <span data-ttu-id="0f211-216">第一個引數是我們想要叫用或呼叫之元件的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-216">The first argument is the name of the component we want to invoke or call.</span></span> <span data-ttu-id="0f211-217">後續參數會傳遞至元件。</span><span class="sxs-lookup"><span data-stu-id="0f211-217">Subsequent parameters are passed to the component.</span></span> <span data-ttu-id="0f211-218">`InvokeAsync` 可以採用任意數目的引數。</span><span class="sxs-lookup"><span data-stu-id="0f211-218">`InvokeAsync` can take an arbitrary number of arguments.</span></span>

<span data-ttu-id="0f211-219">測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f211-219">Test the app.</span></span> <span data-ttu-id="0f211-220">下圖顯示 ToDo 清單和優先順序項目：</span><span class="sxs-lookup"><span data-stu-id="0f211-220">The following image shows the ToDo list and the priority items:</span></span>

![ToDo 清單和優先順序項目](view-components/_static/pi.png)

<span data-ttu-id="0f211-222">您也可以直接從控制器呼叫檢視元件：</span><span class="sxs-lookup"><span data-stu-id="0f211-222">You can also call the view component directly from the controller:</span></span>

[!code-csharp[](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![IndexVC 動作中的優先順序項目](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a><span data-ttu-id="0f211-224">指定檢視名稱</span><span class="sxs-lookup"><span data-stu-id="0f211-224">Specifying a view name</span></span>

<span data-ttu-id="0f211-225">在某些情況下，可能需要複雜的檢視元件，才能指定非預設檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-225">A complex view component might need to specify a non-default view under some conditions.</span></span> <span data-ttu-id="0f211-226">下列程式碼示範如何從 `InvokeAsync` 方法指定 "PVC" 檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-226">The following code shows how to specify the "PVC" view  from the `InvokeAsync` method.</span></span> <span data-ttu-id="0f211-227">更新 `PriorityListViewComponent` 類別中的 `InvokeAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="0f211-227">Update the `InvokeAsync` method in the `PriorityListViewComponent` class.</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

<span data-ttu-id="0f211-228">將 *Views/Shared/Components/PriorityList/Default.cshtml* 檔案複製至名為 *Views/Shared/Components/PriorityList/PVC.cshtml* 的檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-228">Copy the *Views/Shared/Components/PriorityList/Default.cshtml* file to a view named *Views/Shared/Components/PriorityList/PVC.cshtml*.</span></span> <span data-ttu-id="0f211-229">新增標題，以指出正在使用 PVC 檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-229">Add a heading to indicate the PVC view is being used.</span></span>

[!code-cshtml[](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

<span data-ttu-id="0f211-230">更新 *Views/ToDO/Index.cshtml*：</span><span class="sxs-lookup"><span data-stu-id="0f211-230">Update *Views/ToDo/Index.cshtml*:</span></span>

<!-- Views/ToDo/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="0f211-231">執行應用程式，並驗證 PVC 檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-231">Run the app and verify PVC view.</span></span>

![設定檢視元件優先順序](view-components/_static/pvc.png)

<span data-ttu-id="0f211-233">如果未轉譯 PVC 檢視，請驗證您要呼叫的檢視元件優先順序為 4 或以上。</span><span class="sxs-lookup"><span data-stu-id="0f211-233">If the PVC view isn't rendered, verify you are calling the view component with a priority of 4 or higher.</span></span>

### <a name="examine-the-view-path"></a><span data-ttu-id="0f211-234">檢查檢視路徑</span><span class="sxs-lookup"><span data-stu-id="0f211-234">Examine the view path</span></span>

* <span data-ttu-id="0f211-235">將優先順序參數變更為 3 或更小，以不傳回優先順序檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-235">Change the priority parameter to three or less so the priority view isn't returned.</span></span>
* <span data-ttu-id="0f211-236">將 *Views/ToDO/Components/PriorityList/Default.cshtml* 暫時重新命名為 *1Default.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="0f211-236">Temporarily rename the *Views/ToDo/Components/PriorityList/Default.cshtml* to *1Default.cshtml*.</span></span>
* <span data-ttu-id="0f211-237">測試應用程式，您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="0f211-237">Test the app, you'll get the following error:</span></span>

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' wasn't found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* <span data-ttu-id="0f211-238">將 *Views/ToDO/Components/PriorityList/1Default.cshtml* 複製至 *Views/Shared/Components/PriorityList/Default.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="0f211-238">Copy *Views/ToDo/Components/PriorityList/1Default.cshtml* to *Views/Shared/Components/PriorityList/Default.cshtml*.</span></span>
* <span data-ttu-id="0f211-239">將某個標記新增至 *Shared* ToDO 檢視元件檢視，指出檢視來自 *Shared* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0f211-239">Add some markup to the *Shared* ToDo view component view to indicate the view is from the *Shared* folder.</span></span>
* <span data-ttu-id="0f211-240">測試 **Shared** 元件檢視。</span><span class="sxs-lookup"><span data-stu-id="0f211-240">Test the **Shared** component view.</span></span>

![含 Shared 元件檢視的 ToDo 輸出](view-components/_static/shared.png)

### <a name="avoiding-hard-coded-strings"></a><span data-ttu-id="0f211-242">避免硬式編碼的字串</span><span class="sxs-lookup"><span data-stu-id="0f211-242">Avoiding hard-coded strings</span></span>

<span data-ttu-id="0f211-243">如果您想要編譯時間安全，則可以將寫在程式碼中的檢視元件名稱取代為類別名稱。</span><span class="sxs-lookup"><span data-stu-id="0f211-243">If you want compile time safety, you can replace the hard-coded view component name with the class name.</span></span> <span data-ttu-id="0f211-244">建立不含 "ViewComponent" 尾碼的檢視元件：</span><span class="sxs-lookup"><span data-stu-id="0f211-244">Create the view component without the "ViewComponent" suffix:</span></span>

[!code-csharp[](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

<span data-ttu-id="0f211-245">將 `using` 陳述式新增至 Razor 檢視檔案，並使用 `nameof` 運算子：</span><span class="sxs-lookup"><span data-stu-id="0f211-245">Add a `using` statement to your Razor view file, and use the `nameof` operator:</span></span>

[!code-cshtml[](view-components/sample/ViewCompFinal/Views/ToDo/IndexNameof.cshtml?range=1-6,35-)]

## <a name="perform-synchronous-work"></a><span data-ttu-id="0f211-246">執行同步工作</span><span class="sxs-lookup"><span data-stu-id="0f211-246">Perform synchronous work</span></span>

<span data-ttu-id="0f211-247">如果您不需要執行非同步工作，架構會處理叫用同步 `Invoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="0f211-247">The framework handles invoking a synchronous `Invoke` method if you don't need to perform asynchronous work.</span></span> <span data-ttu-id="0f211-248">下列方法會建立同步 `Invoke` 檢視元件：</span><span class="sxs-lookup"><span data-stu-id="0f211-248">The following method creates a synchronous `Invoke` view component:</span></span>

```csharp
public class PriorityList : ViewComponent
{
    public IViewComponentResult Invoke(int maxPriority, bool isDone)
    {
        var items = new List<string> { $"maxPriority: {maxPriority}", $"isDone: {isDone}" };
        return View(items);
    }
}
```

<span data-ttu-id="0f211-249">檢視元件的 Razor 檔案，會列出傳遞至 `Invoke` 方法 (*Views/Home/Components/PriorityList/Default.cshtml*) 的字串：</span><span class="sxs-lookup"><span data-stu-id="0f211-249">The view component's Razor file lists the strings passed to the `Invoke` method (*Views/Home/Components/PriorityList/Default.cshtml*):</span></span>

```cshtml
@model List<string>

<h3>Priority Items</h3>
<ul>
    @foreach (var item in Model)
    {
        <li>@item</li>
    }
</ul>
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="0f211-250">使用下列其中一項方式，在 Razor 檔案中叫用檢視元件 (例如 *Views/Home/Index.cshtml*)：</span><span class="sxs-lookup"><span data-stu-id="0f211-250">The view component is invoked in a Razor file (for example, *Views/Home/Index.cshtml*) using one of the following approaches:</span></span>

* <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>
* [<span data-ttu-id="0f211-251">標籤協助程式</span><span class="sxs-lookup"><span data-stu-id="0f211-251">Tag Helper</span></span>](xref:mvc/views/tag-helpers/intro)

<span data-ttu-id="0f211-252">若要使用 <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper> 方法，請呼叫 `Component.InvokeAsync`：</span><span class="sxs-lookup"><span data-stu-id="0f211-252">To use the <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper> approach, call `Component.InvokeAsync`:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-1.1"

<span data-ttu-id="0f211-253">使用 <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper> 在 Razor 檔案中叫用檢視元件 (例如 *Views/Home/Index.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="0f211-253">The view component is invoked in a Razor file (for example, *Views/Home/Index.cshtml*) with <xref:Microsoft.AspNetCore.Mvc.IViewComponentHelper>.</span></span>

<span data-ttu-id="0f211-254">呼叫 `Component.InvokeAsync`：</span><span class="sxs-lookup"><span data-stu-id="0f211-254">Call `Component.InvokeAsync`:</span></span>

::: moniker-end

```cshtml
@await Component.InvokeAsync(nameof(PriorityList), new { maxPriority = 4, isDone = true })
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="0f211-255">若要使用標籤協助程式，請使用 `@addTagHelper` 指示詞註冊包含檢視元件的組件 (檢視元件位於稱為 `MyWebApp` 的組件中)：</span><span class="sxs-lookup"><span data-stu-id="0f211-255">To use the Tag Helper, register the assembly containing the View Component using the `@addTagHelper` directive (the view component is in an assembly called `MyWebApp`):</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="0f211-256">使用 Razor 標記檔案中的檢視元件標籤協助程式：</span><span class="sxs-lookup"><span data-stu-id="0f211-256">Use the view component Tag Helper in the Razor markup file:</span></span>

```cshtml
<vc:priority-list max-priority="999" is-done="false">
</vc:priority-list>
```
::: moniker-end

<span data-ttu-id="0f211-257">`PriorityList.Invoke` 的方法簽章為同步，但 Razor 會在標記檔案中找到並使用 `Component.InvokeAsync` 呼叫該方法。</span><span class="sxs-lookup"><span data-stu-id="0f211-257">The method signature of `PriorityList.Invoke` is synchronous, but Razor finds and calls the method with `Component.InvokeAsync` in the markup file.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f211-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="0f211-258">Additional resources</span></span>

* [<span data-ttu-id="0f211-259">在檢視中插入相依性</span><span class="sxs-lookup"><span data-stu-id="0f211-259">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
