---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 建立自訂路由 (C#) |Microsoft Docs
author: microsoft
description: 了解如何將自訂的路由新增至 ASP.NET MVC 應用程式。 在本教學課程中，您將了解如何修改 Global.asax 檔案中的預設路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 7b7324c9e0518697c0978b96b0123cb44133722b
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418933"
---
# <a name="creating-custom-routes-c"></a><span data-ttu-id="42e92-104">建立自訂路由 (C#)</span><span class="sxs-lookup"><span data-stu-id="42e92-104">Creating Custom Routes (C#)</span></span>

<span data-ttu-id="42e92-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="42e92-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="42e92-106">了解如何將自訂的路由新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e92-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="42e92-107">在本教學課程中，您將了解如何修改 Global.asax 檔案中的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="42e92-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="42e92-108">在本教學課程中，您將了解如何將自訂的路由新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e92-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="42e92-109">您了解如何修改預設的路由表，在 Global.asax 檔案中，以自訂路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="42e92-110">對於許多簡單的 ASP.NET MVC 應用程式，預設路由表將正常運作。</span><span class="sxs-lookup"><span data-stu-id="42e92-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="42e92-111">不過，您可能會發現您專用的路由需求。</span><span class="sxs-lookup"><span data-stu-id="42e92-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="42e92-112">在此情況下，您可以建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="42e92-113">例如，假設您要建置的部落格應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e92-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="42e92-114">您可能想要處理傳入的要求看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="42e92-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="42e92-115">/ 封存/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="42e92-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="42e92-116">當使用者輸入此要求時，您想要的日期傳回與相對應的部落格項目 2009 年 12 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="42e92-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="42e92-117">為了處理這種類型的要求，您需要建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="42e92-118">列表 1 中的 Global.asax 檔包含新的自訂路由，名為部落格，哪一個處理要求，看起來像 /Archive/*項目日期*。</span><span class="sxs-lookup"><span data-stu-id="42e92-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

**<span data-ttu-id="42e92-119">列表 1-Global.asax （具有自訂路由）</span><span class="sxs-lookup"><span data-stu-id="42e92-119">Listing 1 - Global.asax (with custom route)</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="42e92-120">您將新增至路由表路由的順序很重要。</span><span class="sxs-lookup"><span data-stu-id="42e92-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="42e92-121">現有的預設路由前面會加上我們新的自訂部落格路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="42e92-122">如果您反轉順序，則預設路由一律會取得呼叫而不是自訂的路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="42e92-123">自訂的部落格路由比對開頭為/封存/任何要求。</span><span class="sxs-lookup"><span data-stu-id="42e92-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="42e92-124">因此，它會符合所有下列 Url:</span><span class="sxs-lookup"><span data-stu-id="42e92-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="42e92-125">/ 封存/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="42e92-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="42e92-126">日封存/10-6-2004 年</span><span class="sxs-lookup"><span data-stu-id="42e92-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="42e92-127">/ 封存/apple</span><span class="sxs-lookup"><span data-stu-id="42e92-127">/Archive/apple</span></span>

<span data-ttu-id="42e92-128">自訂的路由將內送的要求對應至名為 Archive 的控制站，並叫用 Entry() 動作。</span><span class="sxs-lookup"><span data-stu-id="42e92-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="42e92-129">Entry() 方法呼叫時，就會將項目日期傳遞做為參數命名為 entryDate 中。</span><span class="sxs-lookup"><span data-stu-id="42e92-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="42e92-130">您可以使用列表 2 中的控制站的部落格的自訂路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

**<span data-ttu-id="42e92-131">列表 2-ArchiveController.cs</span><span class="sxs-lookup"><span data-stu-id="42e92-131">Listing 2 - ArchiveController.cs</span></span>**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="42e92-132">請注意，在 列表 2 Entry() 方法接受 DateTime 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="42e92-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="42e92-133">MVC 架構是夠聰明，無法從 URL 中將項目日期轉換成 DateTime 值時，自動的。</span><span class="sxs-lookup"><span data-stu-id="42e92-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="42e92-134">如果 URL 中的項目日期參數無法轉換成日期時間，就會引發錯誤 （請參閱 圖 1）。</span><span class="sxs-lookup"><span data-stu-id="42e92-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

**<span data-ttu-id="42e92-135">圖 1-轉換參數時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="42e92-135">Figure 1 - Error from converting parameter</span></span>**


[![T<span data-ttu-id="42e92-136">他 [新增專案] 對話方塊中]</span><span class="sxs-lookup"><span data-stu-id="42e92-136">he New Project dialog box]</span></span>(creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

<span data-ttu-id="42e92-137">**圖 01**:轉換參數時發生錯誤 ([按一下以檢視完整大小的影像](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="42e92-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="42e92-138">總結</span><span class="sxs-lookup"><span data-stu-id="42e92-138">Summary</span></span>

<span data-ttu-id="42e92-139">本教學課程的目標是要示範如何建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="42e92-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="42e92-140">您已了解如何將自訂路由加入至 Global.asax 檔案表示部落格文章中的路由表。</span><span class="sxs-lookup"><span data-stu-id="42e92-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="42e92-141">我們會討論如何將要求的部落格項目對應至名為 ArchiveController 控制器和名為 Entry() 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="42e92-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="42e92-142">[上一頁](aspnet-mvc-controllers-overview-cs.md)
> [下一頁](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="42e92-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
