---
title: ASP.NET Core 中的區域
author: rick-anderson
description: 了解其為 ASP.NET MVC 功能的區域，如何用來將相關功能組織成群組，作為個別命名空間 (適用於路由) 和資料夾結構 (適用於檢視)。
ms.author: riande
ms.date: 02/14/2019
uid: mvc/controllers/areas
ms.openlocfilehash: c21eed04ea68512515da262b6b6895dc1a821039
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061705"
---
# <a name="areas-in-aspnet-core"></a><span data-ttu-id="706f4-103">ASP.NET Core 中的區域</span><span class="sxs-lookup"><span data-stu-id="706f4-103">Areas in ASP.NET Core</span></span>

<span data-ttu-id="706f4-104">作者：[Dhananjay Kumar](https://twitter.com/debug_mode) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="706f4-104">By [Dhananjay Kumar](https://twitter.com/debug_mode) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="706f4-105">區域是 ASP.NET 功能，可用來將相關功能組織為群組，以作為個別的命名空間 (適用於路由) 和資料夾結構 (適用於檢視)。</span><span class="sxs-lookup"><span data-stu-id="706f4-105">Areas are an ASP.NET feature used to organize related functionality into a group as a separate namespace (for routing) and folder structure (for views).</span></span> <span data-ttu-id="706f4-106">使用區域可基於路由的目的，藉由將另一個路由參數 `area` 新增至 `controller` 和 `action` 或 Razor 頁面 `page` 來建立階層。</span><span class="sxs-lookup"><span data-stu-id="706f4-106">Using areas creates a hierarchy for the purpose of routing by adding another route parameter, `area`, to `controller` and `action` or a Razor Page `page`.</span></span>

<span data-ttu-id="706f4-107">區域可提供一種方式來將 ASP.NET Core Web 應用程式分割成較小的功能群組，每個都有一組自己的 Razor Pages、控制器、檢視和模型。</span><span class="sxs-lookup"><span data-stu-id="706f4-107">Areas provide a way to partition an ASP.NET Core Web app into smaller functional groups, each  with its own set of Razor Pages, controllers, views, and models.</span></span> <span data-ttu-id="706f4-108">一個區域基本上是應用程式內的一個結構。</span><span class="sxs-lookup"><span data-stu-id="706f4-108">An area is effectively a structure inside an app.</span></span> <span data-ttu-id="706f4-109">在 ASP.NET Core Web 專案中，Pages、模型、控制器和檢視等邏輯元件都會保留在不同的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="706f4-109">In an ASP.NET Core web project, logical components like Pages, Model, Controller, and View are kept in different folders.</span></span> <span data-ttu-id="706f4-110">ASP.NET Core 執行階段會使用命名慣例來建立這些元件之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="706f4-110">The ASP.NET Core runtime uses naming conventions to create the relationship between these components.</span></span> <span data-ttu-id="706f4-111">針對大型應用程式，將應用程式分割成個別高功能層級區域可能較有利。</span><span class="sxs-lookup"><span data-stu-id="706f4-111">For a large app, it may be advantageous to partition the app into separate high level areas of functionality.</span></span> <span data-ttu-id="706f4-112">舉例來說，一個電子商務應用程式可具有多個業務單位，例如結帳、計費和搜尋。</span><span class="sxs-lookup"><span data-stu-id="706f4-112">For instance, an e-commerce app with multiple business units, such as checkout, billing, and search.</span></span> <span data-ttu-id="706f4-113">這其中的每個單位都有自己的區域，以包含檢視、控制器、Razor Pages 和模型。</span><span class="sxs-lookup"><span data-stu-id="706f4-113">Each of these units have their own area to contain views, controllers, Razor Pages, and models.</span></span>

<span data-ttu-id="706f4-114">處於下列情況時，請考慮在專案中使用區域：</span><span class="sxs-lookup"><span data-stu-id="706f4-114">Consider using Areas in an project when:</span></span>

* <span data-ttu-id="706f4-115">應用程式是由可以邏輯方式區隔的多個高階功能性元件所組成的。</span><span class="sxs-lookup"><span data-stu-id="706f4-115">The app is made of multiple high-level functional components that can be logically separated.</span></span>
* <span data-ttu-id="706f4-116">您想要分割應用程式，讓每個功能區域都可獨立運作。</span><span class="sxs-lookup"><span data-stu-id="706f4-116">You want to partition the app so that each functional area can be worked on independently.</span></span>

<span data-ttu-id="706f4-117">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) ([如何下載](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="706f4-117">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="706f4-118">下載範例提供基本的應用程式來測試區域。</span><span class="sxs-lookup"><span data-stu-id="706f4-118">The download sample provides a basic app for testing areas.</span></span>

## <a name="areas-for-controllers-with-views"></a><span data-ttu-id="706f4-119">適用於控制器與檢視的區域</span><span class="sxs-lookup"><span data-stu-id="706f4-119">Areas for controllers with views</span></span>

<span data-ttu-id="706f4-120">使用區域、控制器及檢視的典型 ASP.NET Core Web 應用程式包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="706f4-120">A typical ASP.NET Core web app using areas, controllers, and views contains the following:</span></span>

* <span data-ttu-id="706f4-121">一個[區域資料夾結構](#area-folder-structure)。</span><span class="sxs-lookup"><span data-stu-id="706f4-121">An [Area folder structure](#area-folder-structure).</span></span>
* <span data-ttu-id="706f4-122">使用 [&lbrack;Area&rbrack;](#attribute) 屬性裝飾的控制器可使控制器與區域產生關聯：[!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?name=snippet2)]</span><span class="sxs-lookup"><span data-stu-id="706f4-122">Controllers decorated with the [&lbrack;Area&rbrack;](#attribute) attribute to associate the controller with the area: [!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?name=snippet2)]</span></span>
* <span data-ttu-id="706f4-123">[已新增至啟動的區域路由](#add-area-route)：[!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet2&highlight=3-6)]</span><span class="sxs-lookup"><span data-stu-id="706f4-123">The [area route added to startup](#add-area-route): [!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet2&highlight=3-6)]</span></span>

## <a name="area-folder-structure"></a><span data-ttu-id="706f4-124">區域資料夾結構</span><span class="sxs-lookup"><span data-stu-id="706f4-124">Area folder structure</span></span>
<span data-ttu-id="706f4-125">假設應用程式具有兩個邏輯群組：「產品」和「服務」。</span><span class="sxs-lookup"><span data-stu-id="706f4-125">Consider an app that has two logical groups, *Products* and *Services*.</span></span> <span data-ttu-id="706f4-126">使用區域，資料夾結構應該如下：</span><span class="sxs-lookup"><span data-stu-id="706f4-126">Using areas, the folder structure would be similar to the following:</span></span>

* <span data-ttu-id="706f4-127">Project name</span><span class="sxs-lookup"><span data-stu-id="706f4-127">Project name</span></span>
  * <span data-ttu-id="706f4-128">區域</span><span class="sxs-lookup"><span data-stu-id="706f4-128">Areas</span></span>
    * <span data-ttu-id="706f4-129">產品</span><span class="sxs-lookup"><span data-stu-id="706f4-129">Products</span></span>
      * <span data-ttu-id="706f4-130">Controllers</span><span class="sxs-lookup"><span data-stu-id="706f4-130">Controllers</span></span>
        * <span data-ttu-id="706f4-131">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="706f4-131">HomeController.cs</span></span>
        * <span data-ttu-id="706f4-132">ManageController.cs</span><span class="sxs-lookup"><span data-stu-id="706f4-132">ManageController.cs</span></span>
      * <span data-ttu-id="706f4-133">檢視</span><span class="sxs-lookup"><span data-stu-id="706f4-133">Views</span></span>
        * <span data-ttu-id="706f4-134">首頁</span><span class="sxs-lookup"><span data-stu-id="706f4-134">Home</span></span>
          * <span data-ttu-id="706f4-135">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="706f4-135">Index.cshtml</span></span>
        * <span data-ttu-id="706f4-136">管理</span><span class="sxs-lookup"><span data-stu-id="706f4-136">Manage</span></span>
          * <span data-ttu-id="706f4-137">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="706f4-137">Index.cshtml</span></span>
          * <span data-ttu-id="706f4-138">About.cshtml</span><span class="sxs-lookup"><span data-stu-id="706f4-138">About.cshtml</span></span>
    * <span data-ttu-id="706f4-139">服務</span><span class="sxs-lookup"><span data-stu-id="706f4-139">Services</span></span>
      * <span data-ttu-id="706f4-140">Controllers</span><span class="sxs-lookup"><span data-stu-id="706f4-140">Controllers</span></span>
        * <span data-ttu-id="706f4-141">HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="706f4-141">HomeController.cs</span></span>
      * <span data-ttu-id="706f4-142">檢視</span><span class="sxs-lookup"><span data-stu-id="706f4-142">Views</span></span>
        * <span data-ttu-id="706f4-143">首頁</span><span class="sxs-lookup"><span data-stu-id="706f4-143">Home</span></span>
          * <span data-ttu-id="706f4-144">Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="706f4-144">Index.cshtml</span></span>

<span data-ttu-id="706f4-145">儘管上述配置通常會在使用區域時使用，但是只需有檢視檔案，就能使用此資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="706f4-145">While the preceding layout is typical when using Areas, only the view files are required to use this folder structure.</span></span> <span data-ttu-id="706f4-146">檢視探索會依下列順序搜尋相符的區域檢視檔案：</span><span class="sxs-lookup"><span data-stu-id="706f4-146">View discovery searches for a matching area view file in the following order:</span></span>

```text
/Areas/<Area-Name>/Views/<Controller-Name>/<Action-Name>.cshtml
/Areas/<Area-Name>/Views/Shared/<Action-Name>.cshtml
/Views/Shared/<Action-Name>.cshtml
/Pages/Shared/<Action-Name>.cshtml
   ```

<span data-ttu-id="706f4-147">非檢視資料夾的位置 (例如「控制站」和「模型」) 並**不**重要。</span><span class="sxs-lookup"><span data-stu-id="706f4-147">The location of non-view folders like *Controllers* and *Models* does **not** matter.</span></span> <span data-ttu-id="706f4-148">例如，「控制站」和「模型」資料夾並非必要項。</span><span class="sxs-lookup"><span data-stu-id="706f4-148">For example, the *Controllers* and *Models* folder are not required.</span></span> <span data-ttu-id="706f4-149">「控制器」和「模型」的內容都是要編譯為 .dll 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="706f4-149">The content of *Controllers* and *Models* is code which gets compiled into a .dll.</span></span> <span data-ttu-id="706f4-150">「檢視」的內容要在向該檢視發出要求之後才會編譯。</span><span class="sxs-lookup"><span data-stu-id="706f4-150">The content of the *Views* isn't compiled until a request to that view has been made.</span></span>

<!-- TODO review:
The content of the *Views* isn't compiled until a request to that view has been made.

What about precompiled views? 
 -->
<a name="attribute"></a>

### <a name="associate-the-controller-with-an-area"></a><span data-ttu-id="706f4-151">使控制器與區域產生關聯</span><span class="sxs-lookup"><span data-stu-id="706f4-151">Associate the controller with an Area</span></span>

<span data-ttu-id="706f4-152">區域控制器會透過 [&lbrack;Area&rbrack;](xref:Microsoft.AspNetCore.Mvc.AreaAttribute) 屬性來指定：</span><span class="sxs-lookup"><span data-stu-id="706f4-152">Area controllers are designated with the [&lbrack;Area&rbrack;](xref:Microsoft.AspNetCore.Mvc.AreaAttribute) attribute:</span></span>

[!code-csharp[](areas/samples/MVCareas/Areas/Products/Controllers/ManageController.cs?highlight=5&name=snippet)]

### <a name="add-area-route"></a><span data-ttu-id="706f4-153">新增區域路由</span><span class="sxs-lookup"><span data-stu-id="706f4-153">Add Area route</span></span>

<span data-ttu-id="706f4-154">區域路由通常會使用慣例路由，而非屬性路由。</span><span class="sxs-lookup"><span data-stu-id="706f4-154">Area routes typically use conventional routing rather than attribute routing.</span></span> <span data-ttu-id="706f4-155">慣例路由與順序息息相關。</span><span class="sxs-lookup"><span data-stu-id="706f4-155">Conventional routing is order-dependent.</span></span> <span data-ttu-id="706f4-156">一般而言，具有區域的路由應該放在路由表前面，因為這些路由比沒有區域的路由更明確。</span><span class="sxs-lookup"><span data-stu-id="706f4-156">In general, routes with areas should be placed earlier in the route table as they're more specific than routes without an area.</span></span>

<span data-ttu-id="706f4-157">如果 URL 空間在所有區域中都是統一的，則可使用 `{area:...}` 作為路由範本中的語彙基元：</span><span class="sxs-lookup"><span data-stu-id="706f4-157">`{area:...}` can be used as a token in route templates if url space is uniform across all areas:</span></span>

[!code-csharp[](areas/samples/MVCareas/Startup.cs?name=snippet&highlight=18-21)]

<span data-ttu-id="706f4-158">在上述程式碼中，`exists` 會套用路由必須與區域相符的條件約束。</span><span class="sxs-lookup"><span data-stu-id="706f4-158">In the preceding code, `exists` applies a constraint that the route must match an area.</span></span> <span data-ttu-id="706f4-159">若要將路由新增至區域，使用 `{area:...}` 是最簡單的機制。</span><span class="sxs-lookup"><span data-stu-id="706f4-159">Using `{area:...}` is the least complicated mechanism to adding routing to areas.</span></span>

<span data-ttu-id="706f4-160">下列程式碼會使用 <xref:Microsoft.AspNetCore.Builder.MvcAreaRouteBuilderExtensions.MapAreaRoute*> 來建立兩個具名的區域路由：</span><span class="sxs-lookup"><span data-stu-id="706f4-160">The following code uses <xref:Microsoft.AspNetCore.Builder.MvcAreaRouteBuilderExtensions.MapAreaRoute*> to create two named area routes:</span></span>

[!code-csharp[](areas/samples/MVCareas/StartupMapAreaRoute.cs?name=snippet&highlight=18-27)]

<span data-ttu-id="706f4-161">搭配 ASP.NET Core 2.2 使用 `MapAreaRoute` 時，請參閱[這個 GitHub 問題](https://github.com/aspnet/AspNetCore/issues/7772) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="706f4-161">When using `MapAreaRoute` with ASP.NET Core 2.2, see [this GitHub issue](https://github.com/aspnet/AspNetCore/issues/7772).</span></span>

<span data-ttu-id="706f4-162">如需詳細資訊，請參閱[區域路由](xref:mvc/controllers/routing#areas)。</span><span class="sxs-lookup"><span data-stu-id="706f4-162">For more information, see [Area routing](xref:mvc/controllers/routing#areas).</span></span>

### <a name="link-generation-with-areas"></a><span data-ttu-id="706f4-163">使用區域產生連結</span><span class="sxs-lookup"><span data-stu-id="706f4-163">Link Generation with Areas</span></span>

<span data-ttu-id="706f4-164">以下來自[範例下載](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples)的程式碼會顯示使用指定的區域來產生連結：</span><span class="sxs-lookup"><span data-stu-id="706f4-164">The following code from the [sample download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/areas/samples) shows link generation with the area specified:</span></span>

[!code-cshtml[](areas/samples/MVCareas/Views/Shared/_testLinksPartial.cshtml?name=snippet)]

<span data-ttu-id="706f4-165">使用上述程式碼產生的連結，在應用程式中的任何位置都是有效的。</span><span class="sxs-lookup"><span data-stu-id="706f4-165">The links generated with the preceding code are valid anywhere in the app.</span></span>

<span data-ttu-id="706f4-166">範例下載包括[部分檢視](xref:mvc/views/partial)，其中可在未指定區域的情況下包含上述連結和相同連結。</span><span class="sxs-lookup"><span data-stu-id="706f4-166">The sample download includes a [partial view](xref:mvc/views/partial) that contains the preceding links and the same links without specifying the area.</span></span> <span data-ttu-id="706f4-167">部分檢視會在[配置檔案]()中進行參考，因此，應用程式中的每個頁面都會顯示產生的連結。</span><span class="sxs-lookup"><span data-stu-id="706f4-167">The partial view is referenced in the [layout file](), so every page in the app displays the generated links.</span></span> <span data-ttu-id="706f4-168">在未指定區域的情況下產生的連結，只有在從相同區域與控制器中的頁面進行參考時才有效。</span><span class="sxs-lookup"><span data-stu-id="706f4-168">The links generated without specifying the area are only valid when referenced from a page in the same area and controller.</span></span>

<span data-ttu-id="706f4-169">未指定區域或控制站時，路由即會取決於「環境」值。</span><span class="sxs-lookup"><span data-stu-id="706f4-169">When the area or controller is not specified, routing depends on the *ambient* values.</span></span> <span data-ttu-id="706f4-170">目前要求的目前路由值被視為用於連結產生的環境值。</span><span class="sxs-lookup"><span data-stu-id="706f4-170">The current route values of the current request are considered ambient values for link generation.</span></span> <span data-ttu-id="706f4-171">在許多適用於範例應用程式的案例中，使用環境值會產生不正確的連結。</span><span class="sxs-lookup"><span data-stu-id="706f4-171">In many cases for the sample app, using the ambient values generates incorrect links.</span></span>

<span data-ttu-id="706f4-172">如需詳細資訊，請參閱[路由至控制器動作](xref:mvc/controllers/routing)。</span><span class="sxs-lookup"><span data-stu-id="706f4-172">For more information, see [Routing to controller actions](xref:mvc/controllers/routing).</span></span>

### <a name="shared-layout-for-areas-using-the-viewstartcshtml-file"></a><span data-ttu-id="706f4-173">使用 _ViewStart.cshtml 檔案共用區域的配置</span><span class="sxs-lookup"><span data-stu-id="706f4-173">Shared layout for Areas using the _ViewStart.cshtml file</span></span>

<span data-ttu-id="706f4-174">若要針對整個應用程式共用通用的配置，請將 *_ViewStart.cshtml* 移至應用程式根資料夾。</span><span class="sxs-lookup"><span data-stu-id="706f4-174">To share a common layout for the entire app, move the *_ViewStart.cshtml* to the application root folder.</span></span>

<!-- This section will be completed after https://github.com/aspnet/Docs/pull/10978 is merged.
<a name="arp"></a>

## Areas for Razor Pages
-->
<a name="rename"></a>

### <a name="change-default-area-folder-where-views-are-stored"></a><span data-ttu-id="706f4-175">變更檢視儲存所在的預設區域資料夾</span><span class="sxs-lookup"><span data-stu-id="706f4-175">Change default area folder where views are stored</span></span>

<span data-ttu-id="706f4-176">下列程式碼會將預設的區域資料夾從 `"Areas"` 變更為 `"MyAreas"`：</span><span class="sxs-lookup"><span data-stu-id="706f4-176">The following code changes the default area folder from `"Areas"` to `"MyAreas"`:</span></span>

[!code-csharp[](areas/samples/MVCareas/Startup2.cs?name=snippet)]

<!-- TODO review - can we delete this. Areas doesn't change publishing - right? -->
### <a name="publishing-areas"></a><span data-ttu-id="706f4-177">發行區域</span><span class="sxs-lookup"><span data-stu-id="706f4-177">Publishing Areas</span></span>

<span data-ttu-id="706f4-178">*.csproj* 檔案中包含 `<Project Sdk="Microsoft.NET.Sdk.Web">` 時，所有 `*.cshtml` 和 `wwwroot/**` 檔案都會發行至輸出。</span><span class="sxs-lookup"><span data-stu-id="706f4-178">All `*.cshtml` and `wwwroot/**` files are published to output when `<Project Sdk="Microsoft.NET.Sdk.Web">` is included in the *.csproj* file.</span></span>
