---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 控制器總覽（VB） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會介紹如何 ASP.NET MVC 控制器。 您將瞭解如何建立新的控制器，並傳回不同類型的動作 res 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601560"
---
# <a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="7a0c5-104">ASP.NET MVC 控制器概觀 (VB)</span><span class="sxs-lookup"><span data-stu-id="7a0c5-104">ASP.NET MVC Controller Overview (VB)</span></span>

<span data-ttu-id="7a0c5-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="7a0c5-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="7a0c5-106">在本教學課程中，Stephen Walther 會介紹如何 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="7a0c5-107">您將瞭解如何建立新的控制器，並傳回不同類型的動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-107">You learn how to create new controllers and return different types of action results.</span></span>

<span data-ttu-id="7a0c5-108">本教學課程會探索 ASP.NET MVC 控制器、控制器動作和動作結果的主題。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="7a0c5-109">完成本教學課程之後，您將瞭解如何使用控制器來控制造訪者與 ASP.NET MVC 網站互動的方式。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="7a0c5-110">瞭解控制器</span><span class="sxs-lookup"><span data-stu-id="7a0c5-110">Understanding Controllers</span></span>

<span data-ttu-id="7a0c5-111">MVC 控制器負責回應對 ASP.NET MVC 網站提出的要求。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="7a0c5-112">每個瀏覽器要求都會對應到特定的控制器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="7a0c5-113">例如，假設您在瀏覽器的網址列中輸入下列 URL：</span><span class="sxs-lookup"><span data-stu-id="7a0c5-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="7a0c5-114">在此情況下，會叫用名為 ProductController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="7a0c5-115">ProductController 會負責產生瀏覽器要求的回應。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="7a0c5-116">例如，控制器可能會將特定的視圖傳回給瀏覽器，或控制器可能會將使用者重新導向至另一個控制器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="7a0c5-117">[清單 1] 包含名為 ProductController 的簡單控制器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="7a0c5-118">**Listing1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="7a0c5-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="7a0c5-119">如 [清單 1] 所示，控制器只是一個類別（一個 Visual Basic 的 .NET 或C#類別）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="7a0c5-120">「控制器」（controller）是衍生自基底 System.web. Controller 類別的類別。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="7a0c5-121">由於控制器繼承自這個基類，因此控制器會繼承數個有用的方法（我們稍後會討論這些方法）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="7a0c5-122">瞭解控制器動作</span><span class="sxs-lookup"><span data-stu-id="7a0c5-122">Understanding Controller Actions</span></span>

<span data-ttu-id="7a0c5-123">控制器會公開控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-123">A controller exposes controller actions.</span></span> <span data-ttu-id="7a0c5-124">動作是控制器上的方法，當您在瀏覽器的網址列中輸入特定 URL 時，會呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="7a0c5-125">例如，假設您提出下列 URL 的要求：</span><span class="sxs-lookup"><span data-stu-id="7a0c5-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="7a0c5-126">在此情況下，會在 ProductController 類別上呼叫 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="7a0c5-127">Index （）方法是控制器動作的範例。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="7a0c5-128">控制器動作必須是控制器類別的公用方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="7a0c5-129">根據預設，Visual Basic.NET 方法是公用方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="7a0c5-130">請注意，您新增至控制器類別的任何公用方法都會自動公開為控制器動作（您必須特別小心，因為只要在瀏覽器網址列中輸入正確的 URL，就可以讓 universe 中的任何人叫用控制器動作）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="7a0c5-131">控制器動作必須滿足一些額外的需求。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="7a0c5-132">做為控制器動作使用的方法無法多載。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="7a0c5-133">此外，控制器動作不可以是靜態方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="7a0c5-134">另一方面，您可以使用任何方法做為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="7a0c5-135">瞭解動作結果</span><span class="sxs-lookup"><span data-stu-id="7a0c5-135">Understanding Action Results</span></span>

<span data-ttu-id="7a0c5-136">控制器動作會傳回稱為*動作結果*的內容。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="7a0c5-137">動作結果是控制器動作為了回應瀏覽器要求所傳回的內容。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="7a0c5-138">ASP.NET MVC 架構支援數種類型的動作結果，包括：</span><span class="sxs-lookup"><span data-stu-id="7a0c5-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="7a0c5-139">ViewResult-表示 HTML 和標記。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="7a0c5-140">EmptyResult-不代表任何結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="7a0c5-141">RedirectResult-代表重新導向至新的 URL。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="7a0c5-142">JsonResult-代表可在 AJAX 應用程式中使用的 JavaScript 物件標記法結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="7a0c5-143">JavaScriptResult-代表 JavaScript 腳本。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="7a0c5-144">ContentResult-代表文字結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="7a0c5-145">FileContentResult-代表可下載的檔案（包含二進位內容）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="7a0c5-146">FilePathResult-代表可下載的檔案（具有路徑）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="7a0c5-147">FileStreamResult-代表可下載的檔案（含檔案資料流程）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="7a0c5-148">所有這些動作結果都是繼承自基底 ActionResult 類別。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="7a0c5-149">在大部分情況下，控制器動作會傳回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="7a0c5-150">例如，[清單 2] 中的索引控制器動作會傳回 ViewResult。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="7a0c5-151">**清單 2-Controllers\BookController.vb**</span><span class="sxs-lookup"><span data-stu-id="7a0c5-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="7a0c5-152">當動作傳回 ViewResult 時，會將 HTML 傳回到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="7a0c5-153">[清單 2] 中的 Index （）方法會將名為 Index 的視圖傳回給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="7a0c5-154">請注意，[清單 2] 中的 Index （）動作並不會傳回 ViewResult （）。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="7a0c5-155">相反地，會呼叫控制器基類的 View （）方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="7a0c5-156">一般來說，您不會直接傳回動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="7a0c5-157">相反地，您會呼叫控制器基類的下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="7a0c5-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="7a0c5-158">View-傳回 ViewResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="7a0c5-159">重新導向-傳回 RedirectResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="7a0c5-160">RedirectToAction-傳回 RedirectToRouteResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="7a0c5-161">RedirectToRoute-傳回 RedirectToRouteResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="7a0c5-162">Json-傳回 JsonResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="7a0c5-163">JavaScriptResult-傳回 JavaScriptResult。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="7a0c5-164">Content-傳回 ContentResult 動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="7a0c5-165">File-根據傳遞至方法的參數，傳回 FileContentResult、FilePathResult 或 FileStreamResult。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="7a0c5-166">因此，如果您想要將視圖傳回給瀏覽器，請呼叫 View （）方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="7a0c5-167">如果您想要將使用者從一個控制器動作重新導向到另一個，您可以呼叫 RedirectToAction （）方法。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="7a0c5-168">例如，[清單 3] 中的 [詳細資料] （）動作會顯示一個視圖，或將使用者重新導向至 [索引] （）動作，這取決於識別碼參數是否具有值。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="7a0c5-169">**清單 3-CustomerController .vb**</span><span class="sxs-lookup"><span data-stu-id="7a0c5-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="7a0c5-170">ContentResult 動作結果是特殊的。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-170">The ContentResult action result is special.</span></span> <span data-ttu-id="7a0c5-171">您可以使用 ContentResult 動作結果，以純文字傳回動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="7a0c5-172">例如，[清單 4] 中的 Index （）方法會傳回純文字格式的訊息，而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="7a0c5-173">**清單 4-Controllers\StatusController.vb**</span><span class="sxs-lookup"><span data-stu-id="7a0c5-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="7a0c5-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="7a0c5-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="7a0c5-175">System.web. Mvc. 控制器</span><span class="sxs-lookup"><span data-stu-id="7a0c5-175">System.Web.Mvc.Controller</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="7a0c5-176">叫用 StatusController （）動作時，不會傳回 view。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="7a0c5-177">相反地，原始文字 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="7a0c5-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="7a0c5-178">會傳回至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-178">is returned to the browser.</span></span>

<span data-ttu-id="7a0c5-179">如果控制器動作傳回的結果不是動作結果，例如日期或整數，則會自動將結果包裝在 ContentResult 中。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="7a0c5-180">例如，當叫用清單5中 WorkController 的 Index （）動作時，會自動以 ContentResult 的形式傳回日期。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="7a0c5-181">**清單 5-WorkController .vb**</span><span class="sxs-lookup"><span data-stu-id="7a0c5-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="7a0c5-182">[清單 5] 中的 Index （）動作會傳回 DateTime 物件。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="7a0c5-183">ASP.NET MVC 架構會將 DateTime 物件轉換成字串，並自動將 DateTime 值包裝在 ContentResult 中。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="7a0c5-184">瀏覽器會以純文字的形式接收日期和時間。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="7a0c5-185">總結</span><span class="sxs-lookup"><span data-stu-id="7a0c5-185">Summary</span></span>

<span data-ttu-id="7a0c5-186">本教學課程的目的是要為您介紹 ASP.NET MVC 控制器、控制器動作和控制器動作結果的概念。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="7a0c5-187">在第一節中，您已瞭解如何將新的控制器新增至 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="7a0c5-188">接下來，您已瞭解如何將控制器的公用方法公開至 universe 做為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="7a0c5-189">最後，我們討論了可從控制器動作傳回的不同類型動作結果。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="7a0c5-190">特別是，我們討論了如何從控制器動作傳回 ViewResult、RedirectToActionResult 和 ContentResult。</span><span class="sxs-lookup"><span data-stu-id="7a0c5-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7a0c5-191">[上一頁](creating-a-custom-route-constraint-cs.md)
> [下一頁](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7a0c5-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
