---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 中的單元測試控制器 |Microsoft Docs
author: MikeWasson
description: 本主題描述 Web API 2 中的單元測試控制器的一些特定技術。 閱讀本主題之前，您可能會想要閱讀教學課程單元 .。。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: ee933cfc736a07b91c8f7feea2c4a2c64d200942
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240648"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a><span data-ttu-id="5f746-104">ASP.NET Web API 2 中的單元測試控制器</span><span class="sxs-lookup"><span data-stu-id="5f746-104">Unit Testing Controllers in ASP.NET Web API 2</span></span>

<span data-ttu-id="5f746-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5f746-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="5f746-106">本主題描述 Web API 2 中的單元測試控制器的一些特定技術。</span><span class="sxs-lookup"><span data-stu-id="5f746-106">This topic describes some specific techniques for unit testing controllers in Web API 2.</span></span> <span data-ttu-id="5f746-107">閱讀本主題之前，您可能會想要閱讀教學課程[單元測試 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，其中顯示如何將單元測試專案加入至您的方案。</span><span class="sxs-lookup"><span data-stu-id="5f746-107">Before reading this topic, you might want to read the tutorial [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), which shows how to add a unit-test project to your solution.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5f746-108">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="5f746-108">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="5f746-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5f746-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="5f746-110">Web API 2</span><span class="sxs-lookup"><span data-stu-id="5f746-110">Web API 2</span></span>
> - <span data-ttu-id="5f746-111">[Moq](https://github.com/Moq) 4.5.30</span><span class="sxs-lookup"><span data-stu-id="5f746-111">[Moq](https://github.com/Moq) 4.5.30</span></span>

> [!NOTE]
> <span data-ttu-id="5f746-112">我使用 Moq，但相同的想法適用于任何模擬架構。</span><span class="sxs-lookup"><span data-stu-id="5f746-112">I used Moq, but the same idea applies to any mocking framework.</span></span> <span data-ttu-id="5f746-113">Moq 4.5.30 （和更新版本）支援 Visual Studio 2017、Roslyn 和 .NET 4.5 及更新版本。</span><span class="sxs-lookup"><span data-stu-id="5f746-113">Moq 4.5.30 (and later) supports Visual Studio 2017, Roslyn and .NET 4.5 and later versions.</span></span>

<span data-ttu-id="5f746-114">單元測試中的常見模式是 &quot; 排列-act-assert &quot; ：</span><span class="sxs-lookup"><span data-stu-id="5f746-114">A common pattern in unit tests is &quot;arrange-act-assert&quot;:</span></span>

- <span data-ttu-id="5f746-115">排列：設定要執行測試的任何必要條件。</span><span class="sxs-lookup"><span data-stu-id="5f746-115">Arrange: Set up any prerequisites for the test to run.</span></span>
- <span data-ttu-id="5f746-116">Act：執行測試。</span><span class="sxs-lookup"><span data-stu-id="5f746-116">Act: Perform the test.</span></span>
- <span data-ttu-id="5f746-117">判斷提示：確認測試是否成功。</span><span class="sxs-lookup"><span data-stu-id="5f746-117">Assert: Verify that the test succeeded.</span></span>

<span data-ttu-id="5f746-118">在 [排列] 步驟中，您通常會使用 mock 或 stub 物件。</span><span class="sxs-lookup"><span data-stu-id="5f746-118">In the arrange step, you will often use mock or stub objects.</span></span> <span data-ttu-id="5f746-119">這麼做可將相依性的數目降至最低，因此測試著重于測試一件事。</span><span class="sxs-lookup"><span data-stu-id="5f746-119">That minimizes the number of dependencies, so the test is focused on testing one thing.</span></span>

<span data-ttu-id="5f746-120">以下是您應該在 Web API 控制器中進行單元測試的一些事項：</span><span class="sxs-lookup"><span data-stu-id="5f746-120">Here are some things that you should unit test in your Web API controllers:</span></span>

- <span data-ttu-id="5f746-121">動作會傳回正確的回應類型。</span><span class="sxs-lookup"><span data-stu-id="5f746-121">The action returns the correct type of response.</span></span>
- <span data-ttu-id="5f746-122">不正確參數傳回正確的錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-122">Invalid parameters return the correct error response.</span></span>
- <span data-ttu-id="5f746-123">動作會呼叫儲存機制或服務層級上的正確方法。</span><span class="sxs-lookup"><span data-stu-id="5f746-123">The action calls the correct method on the repository or service layer.</span></span>
- <span data-ttu-id="5f746-124">如果回應包含領域模型，請確認模型類型。</span><span class="sxs-lookup"><span data-stu-id="5f746-124">If the response includes a domain model, verify the model type.</span></span>

<span data-ttu-id="5f746-125">這些都是要測試的一般事項，但細節取決於您的控制器的執行。</span><span class="sxs-lookup"><span data-stu-id="5f746-125">These are some of the general things to test, but the specifics depend on your controller implementation.</span></span> <span data-ttu-id="5f746-126">特別的是，不論您的控制器動作會傳回**HttpResponseMessage**或**應傳回 iHTTPactionresult**，都有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="5f746-126">In particular, it makes a big difference whether your controller actions return **HttpResponseMessage** or **IHttpActionResult**.</span></span> <span data-ttu-id="5f746-127">如需這些結果類型的詳細資訊，請參閱[Web Api 2 中的動作結果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="5f746-127">For more information about these result types, see [Action Results in Web Api 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

## <a name="testing-actions-that-return-httpresponsemessage"></a><span data-ttu-id="5f746-128">測試傳回 HttpResponseMessage 的動作</span><span class="sxs-lookup"><span data-stu-id="5f746-128">Testing Actions that Return HttpResponseMessage</span></span>

<span data-ttu-id="5f746-129">以下是其動作會傳回**HttpResponseMessage**的控制器範例。</span><span class="sxs-lookup"><span data-stu-id="5f746-129">Here is an example of a controller whose actions return **HttpResponseMessage**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

<span data-ttu-id="5f746-130">請注意，控制器會使用相依性插入來插入 `IProductRepository` 。</span><span class="sxs-lookup"><span data-stu-id="5f746-130">Notice the controller uses dependency injection to inject an `IProductRepository`.</span></span> <span data-ttu-id="5f746-131">這可讓控制器更具測試性，因為您可以插入模擬存放庫。</span><span class="sxs-lookup"><span data-stu-id="5f746-131">That makes the controller more testable, because you can inject a mock repository.</span></span> <span data-ttu-id="5f746-132">下列單元測試會驗證方法是否將 `Get` 寫入 `Product` 至回應主體。</span><span class="sxs-lookup"><span data-stu-id="5f746-132">The following unit test verifies that the `Get` method writes a `Product` to the response body.</span></span> <span data-ttu-id="5f746-133">假設 `repository` 是 mock `IProductRepository` 。</span><span class="sxs-lookup"><span data-stu-id="5f746-133">Assume that `repository` is a mock `IProductRepository`.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

<span data-ttu-id="5f746-134">請務必在**控制器上設定\*\*\*\*要求**和設定。</span><span class="sxs-lookup"><span data-stu-id="5f746-134">It's important to set **Request** and **Configuration** on the controller.</span></span> <span data-ttu-id="5f746-135">否則，測試將會失敗，並出現**system.argumentnullexception**或**InvalidOperationException**。</span><span class="sxs-lookup"><span data-stu-id="5f746-135">Otherwise, the test will fail with an **ArgumentNullException** or **InvalidOperationException**.</span></span>

## <a name="testing-link-generation"></a><span data-ttu-id="5f746-136">測試連結產生</span><span class="sxs-lookup"><span data-stu-id="5f746-136">Testing Link Generation</span></span>

<span data-ttu-id="5f746-137">`Post`方法會呼叫**UrlHelper** ，以在回應中建立連結。</span><span class="sxs-lookup"><span data-stu-id="5f746-137">The `Post` method calls **UrlHelper.Link** to create links in the response.</span></span> <span data-ttu-id="5f746-138">在單元測試中，這需要進行一些設定：</span><span class="sxs-lookup"><span data-stu-id="5f746-138">This requires a little more setup in the unit test:</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

<span data-ttu-id="5f746-139">**UrlHelper**類別需要要求 URL 和路由資料，因此測試必須設定這些的值。</span><span class="sxs-lookup"><span data-stu-id="5f746-139">The **UrlHelper** class needs the request URL and route data, so the test has to set values for these.</span></span> <span data-ttu-id="5f746-140">另一個選項是 mock 或存根**UrlHelper**。</span><span class="sxs-lookup"><span data-stu-id="5f746-140">Another option is mock or stub **UrlHelper**.</span></span> <span data-ttu-id="5f746-141">使用這種方法，您可以將[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)的預設值取代為會傳回固定值的模擬或存根版本。</span><span class="sxs-lookup"><span data-stu-id="5f746-141">With this approach, you replace the default value of [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) with a mock or stub version that returns a fixed value.</span></span>

<span data-ttu-id="5f746-142">讓我們使用[Moq](https://github.com/Moq)架構來重寫測試。</span><span class="sxs-lookup"><span data-stu-id="5f746-142">Let's rewrite the test using the [Moq](https://github.com/Moq) framework.</span></span> <span data-ttu-id="5f746-143">`Moq`在測試專案中安裝 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="5f746-143">Install the `Moq` NuGet package in the test project.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

<span data-ttu-id="5f746-144">在此版本中，您不需要設定任何路由資料，因為 mock **UrlHelper**會傳回常數位串。</span><span class="sxs-lookup"><span data-stu-id="5f746-144">In this version, you don't need to set up any route data, because the mock **UrlHelper** returns a constant string.</span></span>

## <a name="testing-actions-that-return-ihttpactionresult"></a><span data-ttu-id="5f746-145">測試傳回應傳回 iHTTPactionresult 的動作</span><span class="sxs-lookup"><span data-stu-id="5f746-145">Testing Actions that Return IHttpActionResult</span></span>

<span data-ttu-id="5f746-146">在 Web API 2 中，控制器動作可以傳回**應傳回 iHTTPactionresult**，類似于 ASP.NET MVC 中的**ActionResult** 。</span><span class="sxs-lookup"><span data-stu-id="5f746-146">In Web API 2, a controller action can return **IHttpActionResult**, which is analogous to **ActionResult** in ASP.NET MVC.</span></span> <span data-ttu-id="5f746-147">**應傳回 iHTTPactionresult**介面會定義用來建立 HTTP 回應的命令模式。</span><span class="sxs-lookup"><span data-stu-id="5f746-147">The **IHttpActionResult** interface defines a command pattern for creating HTTP responses.</span></span> <span data-ttu-id="5f746-148">控制器不會直接建立回應，而是會傳回**應傳回 iHTTPactionresult**。</span><span class="sxs-lookup"><span data-stu-id="5f746-148">Instead of creating the response directly, the controller returns an **IHttpActionResult**.</span></span> <span data-ttu-id="5f746-149">之後，管線會叫用**應傳回 iHTTPactionresult**來建立回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-149">Later, the pipeline invokes the **IHttpActionResult** to create the response.</span></span> <span data-ttu-id="5f746-150">這種方法可讓您更輕鬆地撰寫單元測試，因為您可以略過**HttpResponseMessage**所需的許多設定。</span><span class="sxs-lookup"><span data-stu-id="5f746-150">This approach makes it easier to write unit tests, because you can skip a lot of the setup that is needed for **HttpResponseMessage**.</span></span>

<span data-ttu-id="5f746-151">以下是範例控制器，其動作會傳回**應傳回 iHTTPactionresult**。</span><span class="sxs-lookup"><span data-stu-id="5f746-151">Here is an example controller whose actions return **IHttpActionResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

<span data-ttu-id="5f746-152">這個範例會顯示一些使用**應傳回 iHTTPactionresult**的常見模式。</span><span class="sxs-lookup"><span data-stu-id="5f746-152">This example shows some common patterns using **IHttpActionResult**.</span></span> <span data-ttu-id="5f746-153">讓我們來瞭解如何對其進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="5f746-153">Let's see how to unit test them.</span></span>

### <a name="action-returns-200-ok-with-a-response-body"></a><span data-ttu-id="5f746-154">動作會傳回200（確定）與回應主體</span><span class="sxs-lookup"><span data-stu-id="5f746-154">Action returns 200 (OK) with a response body</span></span>

<span data-ttu-id="5f746-155">`Get` `Ok(product)` 如果找到產品，方法會呼叫。</span><span class="sxs-lookup"><span data-stu-id="5f746-155">The `Get` method calls `Ok(product)` if the product is found.</span></span> <span data-ttu-id="5f746-156">在單元測試中，請確定傳回類型為**OkNegotiatedContentResult** ，而傳回的產品具有正確的識別碼。</span><span class="sxs-lookup"><span data-stu-id="5f746-156">In the unit test, make sure the return type is **OkNegotiatedContentResult** and the returned product has the right ID.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

<span data-ttu-id="5f746-157">請注意，單元測試不會執行動作結果。</span><span class="sxs-lookup"><span data-stu-id="5f746-157">Notice that the unit test doesn't execute the action result.</span></span> <span data-ttu-id="5f746-158">您可以假設動作結果會正確地建立 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-158">You can assume the action result creates the HTTP response correctly.</span></span> <span data-ttu-id="5f746-159">（這就是為什麼 Web API 架構有自己的單元測試！）</span><span class="sxs-lookup"><span data-stu-id="5f746-159">(That's why the Web API framework has its own unit tests!)</span></span>

### <a name="action-returns-404-not-found"></a><span data-ttu-id="5f746-160">動作傳回404（找不到）</span><span class="sxs-lookup"><span data-stu-id="5f746-160">Action returns 404 (Not Found)</span></span>

<span data-ttu-id="5f746-161">`Get` `NotFound()` 如果找不到產品，方法會呼叫。</span><span class="sxs-lookup"><span data-stu-id="5f746-161">The `Get` method calls `NotFound()` if the product is not found.</span></span> <span data-ttu-id="5f746-162">在此情況下，單元測試只會檢查傳回型別是否為**NotFoundResult**。</span><span class="sxs-lookup"><span data-stu-id="5f746-162">For this case, the unit test just checks if the return type is **NotFoundResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a><span data-ttu-id="5f746-163">動作會傳回200（確定），而不會傳迴響應主體</span><span class="sxs-lookup"><span data-stu-id="5f746-163">Action returns 200 (OK) with no response body</span></span>

<span data-ttu-id="5f746-164">`Delete`方法會呼叫 `Ok()` 以傳回空的 HTTP 200 回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-164">The `Delete` method calls `Ok()` to return an empty HTTP 200 response.</span></span> <span data-ttu-id="5f746-165">如同上述範例，單元測試會檢查傳回類型，在此案例中為**OkResult**。</span><span class="sxs-lookup"><span data-stu-id="5f746-165">Like the previous example, the unit test checks the return type, in this case **OkResult**.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a><span data-ttu-id="5f746-166">動作會傳回201（已建立）與位置標頭</span><span class="sxs-lookup"><span data-stu-id="5f746-166">Action returns 201 (Created) with a Location header</span></span>

<span data-ttu-id="5f746-167">`Post`方法會呼叫 `CreatedAtRoute` ，以在 Location 標頭中傳回具有 URI 的 HTTP 201 回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-167">The `Post` method calls `CreatedAtRoute` to return an HTTP 201 response with a URI in the Location header.</span></span> <span data-ttu-id="5f746-168">在單元測試中，確認動作是否已設定正確的路由值。</span><span class="sxs-lookup"><span data-stu-id="5f746-168">In the unit test, verify that the action sets the correct routing values.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a><span data-ttu-id="5f746-169">動作會傳回另一個具有回應主體的2xx</span><span class="sxs-lookup"><span data-stu-id="5f746-169">Action returns another 2xx with a response body</span></span>

<span data-ttu-id="5f746-170">`Put`方法會呼叫 `Content` ，以傳回包含回應主體的 HTTP 202 （接受）回應。</span><span class="sxs-lookup"><span data-stu-id="5f746-170">The `Put` method calls `Content` to return an HTTP 202 (Accepted) response with a response body.</span></span> <span data-ttu-id="5f746-171">這種情況類似于傳回200（OK），但是單元測試也應該檢查狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5f746-171">This case is similar to returning 200 (OK), but the unit test should also check the status code.</span></span>

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="5f746-172">其他資源</span><span class="sxs-lookup"><span data-stu-id="5f746-172">Additional Resources</span></span>

- [<span data-ttu-id="5f746-173">單元測試 ASP.NET Web API 2 時的模擬 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="5f746-173">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- <span data-ttu-id="5f746-174">[撰寫 ASP.NET Web API 服務的測試](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service)（Youssef Moussaoui 的 blog 文章）。</span><span class="sxs-lookup"><span data-stu-id="5f746-174">[Writing tests for an ASP.NET Web API service](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service) (blog post by Youssef Moussaoui).</span></span>
- [<span data-ttu-id="5f746-175">使用 Route Debugger 進行 ASP.NET Web API 偵錯</span><span class="sxs-lookup"><span data-stu-id="5f746-175">Debugging ASP.NET Web API with Route Debugger</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
