---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 動態與 強型別視圖 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702942"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="c688a-103">動態與</span><span class="sxs-lookup"><span data-stu-id="c688a-103">Dynamic v.</span></span> <span data-ttu-id="c688a-104">強型別檢視</span><span class="sxs-lookup"><span data-stu-id="c688a-104">Strongly Typed Views</span></span>

<span data-ttu-id="c688a-105">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c688a-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c688a-106">有三種方式可將資訊從控制器傳遞至 ASP.NET MVC 3 中的觀點：</span><span class="sxs-lookup"><span data-stu-id="c688a-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="c688a-107">做為強型別模型物件。</span><span class="sxs-lookup"><span data-stu-id="c688a-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="c688a-108">作為動態類型 (使用 @model 動態) </span><span class="sxs-lookup"><span data-stu-id="c688a-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="c688a-109">使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="c688a-109">Using the ViewBag</span></span>

<span data-ttu-id="c688a-110">我撰寫了簡單的 MVC 3 熱門 Blog 應用程式，以比較和對比動態和強型別的觀點。</span><span class="sxs-lookup"><span data-stu-id="c688a-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="c688a-111">控制器會從簡單的 blog 清單開始：</span><span class="sxs-lookup"><span data-stu-id="c688a-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="c688a-112">以滑鼠右鍵按一下 IndexNotStonglyTyped ( # A1 方法，並新增 Razor view。</span><span class="sxs-lookup"><span data-stu-id="c688a-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="c688a-113">[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c688a-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="c688a-114">請確定未核取 [ **建立強型** 別] 視圖框。</span><span class="sxs-lookup"><span data-stu-id="c688a-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="c688a-115">產生的視圖不包含太多：</span><span class="sxs-lookup"><span data-stu-id="c688a-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="c688a-116">由於我們使用的是動態的，而不是強型別視圖，因此 intellisense 不會協助我們。</span><span class="sxs-lookup"><span data-stu-id="c688a-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="c688a-117">完成的程式碼如下所示：</span><span class="sxs-lookup"><span data-stu-id="c688a-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="c688a-118">[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c688a-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="c688a-119">現在我們要新增強型別視圖。</span><span class="sxs-lookup"><span data-stu-id="c688a-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="c688a-120">將下列程式碼新增至控制器：</span><span class="sxs-lookup"><span data-stu-id="c688a-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="c688a-121">請注意， (topBlogs) ;以非強型別視圖的形式呼叫。</span><span class="sxs-lookup"><span data-stu-id="c688a-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="c688a-122">以滑鼠右鍵按一下 \*StonglyTypedIndex ( # B1 \* 內，然後選取 [ **加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="c688a-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="c688a-123">這次請選取 [ **Blog** ] 模型類別，然後選取 [ **清單** ] 作為 Scaffold 範本。</span><span class="sxs-lookup"><span data-stu-id="c688a-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="c688a-124">[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c688a-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="c688a-125">在新的 view 範本中，我們會取得 intellisense 支援。</span><span class="sxs-lookup"><span data-stu-id="c688a-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="c688a-126">[![7002。 IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c688a-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>
