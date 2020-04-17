---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 建立操作 (VB) :微軟文件
author: rick-anderson
description: 瞭解如何向ASP.NET MVC 控制器添加新操作。 瞭解方法為操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: dd651155bdb931cb8358d369b3c0c2c98abb86b2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542244"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="b0003-104">建立動作 (VB)</span><span class="sxs-lookup"><span data-stu-id="b0003-104">Creating an Action (VB)</span></span>

<span data-ttu-id="b0003-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b0003-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b0003-106">瞭解如何向ASP.NET MVC 控制器添加新操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="b0003-107">瞭解方法為操作的要求。</span><span class="sxs-lookup"><span data-stu-id="b0003-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="b0003-108">本教學的目的是解釋如何創建新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="b0003-109">瞭解操作方法的要求。</span><span class="sxs-lookup"><span data-stu-id="b0003-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="b0003-110">您還學習如何防止方法作為操作公開。</span><span class="sxs-lookup"><span data-stu-id="b0003-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="b0003-111">新增控制器</span><span class="sxs-lookup"><span data-stu-id="b0003-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="b0003-112">通過將新方法添加到控制器,向控制器添加新操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="b0003-113">例如,清單 1 中的控制器包含名為 Index() 的操作和名為 SayHello() 的操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="b0003-114">這兩種方法都公開為操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="b0003-115">**清單1 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="b0003-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="b0003-116">為了作為一種行動暴露在宇宙中,一種方法必須滿足某些要求:</span><span class="sxs-lookup"><span data-stu-id="b0003-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="b0003-117">該方法必須為公共。</span><span class="sxs-lookup"><span data-stu-id="b0003-117">The method must be public.</span></span>
- <span data-ttu-id="b0003-118">該方法不能是靜態方法。</span><span class="sxs-lookup"><span data-stu-id="b0003-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="b0003-119">該方法不能是擴充方法。</span><span class="sxs-lookup"><span data-stu-id="b0003-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="b0003-120">該方法不能是構造函數、getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="b0003-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="b0003-121">該方法不能具有打開的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="b0003-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="b0003-122">該方法不是控制器基類的方法。</span><span class="sxs-lookup"><span data-stu-id="b0003-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="b0003-123">該方法不能包含**ref**或**out**參數。</span><span class="sxs-lookup"><span data-stu-id="b0003-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="b0003-124">請注意,對控制器操作的返回類型沒有限制。</span><span class="sxs-lookup"><span data-stu-id="b0003-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="b0003-125">控制器操作可以返回字串、DateTime、Random 類的實例或 void。</span><span class="sxs-lookup"><span data-stu-id="b0003-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="b0003-126">ASP.NET MVC 框架將任何不是操作結果的傳回類型轉換為字串,並將字串呈現給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="b0003-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="b0003-127">將不違反這些要求的任何方法添加到控制器時,該方法將作為控制器操作公開。</span><span class="sxs-lookup"><span data-stu-id="b0003-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="b0003-128">這裡要小心。</span><span class="sxs-lookup"><span data-stu-id="b0003-128">Be careful here.</span></span> <span data-ttu-id="b0003-129">連接到 Internet 的任何人都可以調用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="b0003-130">例如,不要創建"刪除My網站"控制器操作。</span><span class="sxs-lookup"><span data-stu-id="b0003-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="b0003-131">防止呼叫公共方法</span><span class="sxs-lookup"><span data-stu-id="b0003-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="b0003-132">如果需要在控制器類中創建公共方法,並且不希望將該方法公開為控制器操作,則可以使用&lt;NonAction&gt;屬性阻止調用該方法。</span><span class="sxs-lookup"><span data-stu-id="b0003-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="b0003-133">例如,清單 2 中的控制器包含一個名為「公司機密()」的公共方法,該&lt;方法使用&gt;非操作 屬性進行修飾。</span><span class="sxs-lookup"><span data-stu-id="b0003-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="b0003-134">**清單2 - 控制器\工作控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="b0003-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="b0003-135">如果您嘗試透過在瀏覽器的位址列中鍵入 /Work/公司機密來呼叫公司機密() 控制器操作,則會收到圖 1 中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b0003-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="b0003-136">[![呼叫非操作方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b0003-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="b0003-137">**圖 01**:呼叫非操作方法([按下以檢視全尺寸影像](creating-an-action-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b0003-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b0003-138">[前一個](creating-a-controller-vb.md)
> [下一個](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b0003-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
