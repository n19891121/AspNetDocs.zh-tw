---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 建立自定義路由 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何向ASP.NET MVC 應用程式添加自定義路由。 在本教學中,您將瞭解如何修改 Global.asax 檔中的預設路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542751"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="b3fdf-104">建立自訂路由 (C#)</span><span class="sxs-lookup"><span data-stu-id="b3fdf-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="b3fdf-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b3fdf-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b3fdf-106">瞭解如何向ASP.NET MVC 應用程式添加自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="b3fdf-107">在本教學中,您將瞭解如何修改 Global.asax 檔中的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="b3fdf-108">在本教學中,您將瞭解如何向ASP.NET MVC 應用程式添加自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="b3fdf-109">您將瞭解如何使用自訂路由修改 Global.asax 檔中的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="b3fdf-110">對於許多簡單的ASP.NET MVC 應用程式,預設路由表將工作正常。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="b3fdf-111">但是,您可能會發現您有專門的路由需求。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="b3fdf-112">在這種情況下,您可以創建自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="b3fdf-113">例如,假設您正在構建一個博客應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="b3fdf-114">您可能需要處理以下所示的傳入請求:</span><span class="sxs-lookup"><span data-stu-id="b3fdf-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="b3fdf-115">/存檔/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="b3fdf-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="b3fdf-116">當使用者輸入此請求時,您希望返回與日期 12/25/2009 對應的博客條目。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="b3fdf-117">為了處理這種類型的請求,您需要創建自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="b3fdf-118">清單1中的 Global.asax 檔包含名為 Blog 的新自訂路由,它處理看起來像 /存檔/*條目日期*的請求。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="b3fdf-119">**清單 1 - 全域.asax(含自訂路由)**</span><span class="sxs-lookup"><span data-stu-id="b3fdf-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="b3fdf-120">添加到工藝路線表的路由的順序很重要。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="b3fdf-121">我們新的自定義博客路由在現有預設路由之前添加。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="b3fdf-122">如果顛倒了訂單,則預設路由將始終被調用,而不是自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="b3fdf-123">自定義博客路由匹配以 /存檔/開頭的任何請求。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="b3fdf-124">因此,它與以下網址匹配:</span><span class="sxs-lookup"><span data-stu-id="b3fdf-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="b3fdf-125">/存檔/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="b3fdf-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="b3fdf-126">/存檔/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="b3fdf-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="b3fdf-127">/存檔/蘋果</span><span class="sxs-lookup"><span data-stu-id="b3fdf-127">/Archive/apple</span></span>

<span data-ttu-id="b3fdf-128">自定義路由將傳入請求映射到名為「存檔」的控制器,並調用 Entry() 操作。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="b3fdf-129">調用 entry() 方法時,條目日期將作為名為 entryDate 的參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="b3fdf-130">您可以將博客自定義路由與清單 2 中的控制器一起使用。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="b3fdf-131">**清單2 - ArchiveController.cs**</span><span class="sxs-lookup"><span data-stu-id="b3fdf-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="b3fdf-132">請注意,清單 2 中的 entry() 方法接受 DateTime 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="b3fdf-133">MVC 框架足夠智慧,可以自動將 URL 的輸入日期轉換為 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="b3fdf-134">如果 URL 中的輸入日期參數無法轉換為 DateTime,則引發錯誤(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="b3fdf-135">**圖 1 - 轉換參數時發生錯誤**</span><span class="sxs-lookup"><span data-stu-id="b3fdf-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="b3fdf-136">[![[New Project] \(新增專案\) 對話方塊](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b3fdf-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="b3fdf-137">**圖 01**: 轉換參數時發生錯誤 ([按下以檢視全尺寸影像](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b3fdf-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="b3fdf-138">總結</span><span class="sxs-lookup"><span data-stu-id="b3fdf-138">Summary</span></span>

<span data-ttu-id="b3fdf-139">本教學的目的是示範如何創建自定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="b3fdf-140">您學習了如何在表示部落格條目的 Global.asax 檔中向路由表添加自訂路由。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="b3fdf-141">我們討論了如何將部落格條目的請求映射到名為 ArchiveController 的控制器和名為 entry() 的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b3fdf-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3fdf-142">[前一個](aspnet-mvc-controllers-overview-cs.md)
> [下一個](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b3fdf-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
