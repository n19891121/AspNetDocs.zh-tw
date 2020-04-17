---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 瞭解ASP.NET MVC 執行流程 |微軟文件
author: rick-anderson
description: 瞭解ASP.NET MVC 框架如何逐步處理瀏覽器請求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541022"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="80bd7-103">了解 ASP.NET MVC 執行程序</span><span class="sxs-lookup"><span data-stu-id="80bd7-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="80bd7-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="80bd7-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="80bd7-105">瞭解ASP.NET MVC 框架如何逐步處理瀏覽器請求。</span><span class="sxs-lookup"><span data-stu-id="80bd7-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="80bd7-106">對基於ASP.NET MVC 的 Web 應用程式的請求首先透過**UrlRoutingModule**物件,該物件是一個 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="80bd7-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="80bd7-107">此模組會剖析該要求並執行路由選取。</span><span class="sxs-lookup"><span data-stu-id="80bd7-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="80bd7-108">**UrlRoutingModule**物件選擇與當前請求匹配的第一個路由物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="80bd7-109">(路由對像是實現**RouteBase**的類,通常是**路由**類的實例。如果沒有路由匹配 **,UrlRoutingModule**物件將不執行任何操作,並讓請求回退到常規ASP.NET或 IIS 請求處理。</span><span class="sxs-lookup"><span data-stu-id="80bd7-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="80bd7-110">從選取的**路由**物件中 **,UrlRouteModule**物件獲取與**路由**物件關聯的**IRouteHandler**物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="80bd7-111">通常,在 MVC 應用程式中,這將是**MvcRouteHandler**的實例。</span><span class="sxs-lookup"><span data-stu-id="80bd7-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="80bd7-112">**IRouteHandler**實例創建一個**IHTTPHandler**物件,並將其傳遞給**IHttpContext**物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="80bd7-113">默認情況下,MVC 的**IHTTPHandler**實例是**MvcHandler**物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="80bd7-114">**然後,MvcHandler**物件選擇最終將處理請求的控制器。</span><span class="sxs-lookup"><span data-stu-id="80bd7-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="80bd7-115">當 ASP.NET MVC Web 應用程式在 IIS 7.0 中執行時，MVC 專案不需要副檔名。</span><span class="sxs-lookup"><span data-stu-id="80bd7-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="80bd7-116">然而，在 IIS 6.0 中，處理常式需要您將 .mvc 副檔名對應至 ASP.NET ISAPI DLL。</span><span class="sxs-lookup"><span data-stu-id="80bd7-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="80bd7-117">模組和處理程式是 mVC 框架 ASP.NET 的入口點。</span><span class="sxs-lookup"><span data-stu-id="80bd7-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="80bd7-118">它們會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="80bd7-118">They perform the following actions:</span></span>

- <span data-ttu-id="80bd7-119">選取 MVC Web 應用程式中適當的控制器。</span><span class="sxs-lookup"><span data-stu-id="80bd7-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="80bd7-120">取得特定控制器執行個體。</span><span class="sxs-lookup"><span data-stu-id="80bd7-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="80bd7-121">呼叫**控制器的執行方法**。</span><span class="sxs-lookup"><span data-stu-id="80bd7-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="80bd7-122">下面列出了 MVC Web 專案的執行階段:</span><span class="sxs-lookup"><span data-stu-id="80bd7-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="80bd7-123">接收應用程式的第一個要求</span><span class="sxs-lookup"><span data-stu-id="80bd7-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="80bd7-124">在 Global.asax 檔中,**路由**物件將添加到**RouteTable**物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="80bd7-125">執行路由</span><span class="sxs-lookup"><span data-stu-id="80bd7-125">Perform routing</span></span> 

    - <span data-ttu-id="80bd7-126">**UrlRoutingModule 模組**使用**RouteTable**集合中的第一個匹配**路由**物件來創建**RouteData**物件,然後使用它創建**請求上下文**(**IHTTPContext**) 物件。</span><span class="sxs-lookup"><span data-stu-id="80bd7-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="80bd7-127">建立 MVC 要求處理常式</span><span class="sxs-lookup"><span data-stu-id="80bd7-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="80bd7-128">**MvcRouteHandler**物件創建**MvcHandler**類的實例,並將其傳遞給**請求上下文**實例。</span><span class="sxs-lookup"><span data-stu-id="80bd7-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="80bd7-129">建立控制器</span><span class="sxs-lookup"><span data-stu-id="80bd7-129">Create controller</span></span> 

    - <span data-ttu-id="80bd7-130">**MvcHandler**物件使用**RequestContext**實例來識別**IControllerFactory**物件(通常是**默認控制器工廠**類的實例)來使用來創建控制器實例。</span><span class="sxs-lookup"><span data-stu-id="80bd7-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="80bd7-131">執行控制器 - **MvcHandler**實體呼叫控制器**的執行方法**。</span><span class="sxs-lookup"><span data-stu-id="80bd7-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="80bd7-132">叫用動作</span><span class="sxs-lookup"><span data-stu-id="80bd7-132">Invoke action</span></span> 

    - <span data-ttu-id="80bd7-133">大多數控制器從**控制器**基類繼承。</span><span class="sxs-lookup"><span data-stu-id="80bd7-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="80bd7-134">對於這樣做的控制器,與控制器關聯的**ControllerActionInvoker**物件確定要呼叫的控制器類的操作方法,然後調用該方法。</span><span class="sxs-lookup"><span data-stu-id="80bd7-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="80bd7-135">執行結果</span><span class="sxs-lookup"><span data-stu-id="80bd7-135">Execute result</span></span> 

    - <span data-ttu-id="80bd7-136">典型的操作方法可能會接收使用者輸入、準備適當的回應數據,然後通過返回結果類型來執行結果。</span><span class="sxs-lookup"><span data-stu-id="80bd7-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="80bd7-137">可以執行的內建結果類型包括 **:ViewResult(** 呈現檢視,是最常用的結果類型,**重定向到路由結果**,**重定向結果**,**內容結果\*\*\*\*,JsonResult**和**空結果**。</span><span class="sxs-lookup"><span data-stu-id="80bd7-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
