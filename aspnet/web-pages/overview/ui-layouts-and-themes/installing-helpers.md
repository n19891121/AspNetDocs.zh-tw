---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 安裝協助程式中 ASP.NET Web Pages (Razor) 網站 |Microsoft Docs
author: Rick-Anderson
description: 本文說明如何在 ASP.NET Web Pages (Razor) 網站安裝的協助程式。 協助程式是一種可重複使用的元件，包括程式碼和標記，以每個...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 3ffb2f88fd8d2ad32fb8ea7d476ca10fdd9ac430
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59398328"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="c592a-104">安裝 ASP.NET Web Pages (Razor) 網站中的協助程式</span><span class="sxs-lookup"><span data-stu-id="c592a-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="c592a-105">藉由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c592a-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c592a-106">本文說明如何在 ASP.NET Web Pages (Razor) 網站安裝的協助程式。</span><span class="sxs-lookup"><span data-stu-id="c592a-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="c592a-107">A*協助程式*是一種可重複使用的元件，包括程式碼和標記，以執行可能冗長或複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="c592a-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="c592a-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="c592a-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c592a-109">如何安裝網站，建立使用 WebMatrix 3 中的協助程式。</span><span class="sxs-lookup"><span data-stu-id="c592a-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c592a-110">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="c592a-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c592a-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="c592a-111">WebMatrix 3</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="c592a-112">協助程式的概觀</span><span class="sxs-lookup"><span data-stu-id="c592a-112">Overview of Helpers</span></span>

<span data-ttu-id="c592a-113">使用者通常會想要在網頁上執行某些工作需要大量的程式碼，或需要額外的知識。</span><span class="sxs-lookup"><span data-stu-id="c592a-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="c592a-114">範例包括顯示的圖表資料;將 Twitter [跟隨] 按鈕放在頁面的從您的網站; 傳送電子郵件裁剪或調整大小的影像;為您的網站使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="c592a-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="c592a-115">若要讓您輕鬆地執行這類作業，ASP.NET Web Pages 可讓您使用*協助程式*。</span><span class="sxs-lookup"><span data-stu-id="c592a-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="c592a-116">協助程式是您安裝站台，並可讓您的元件使用，只要一兩行 Razor 程式碼執行一般工作。</span><span class="sxs-lookup"><span data-stu-id="c592a-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="c592a-117">ASP.NET Web Pages 有幾個內建的協助程式。</span><span class="sxs-lookup"><span data-stu-id="c592a-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="c592a-118">不過，許多協助程式可使用 NuGet 套件管理員提供的封裝 （增益集） 中。</span><span class="sxs-lookup"><span data-stu-id="c592a-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="c592a-119">NuGet 可讓您選取要安裝的套件，然後它會負責安裝的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c592a-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="c592a-120">在 WebMatrix 3 安裝協助程式</span><span class="sxs-lookup"><span data-stu-id="c592a-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="c592a-121">在 WebMatrix 3 中，按一下**NuGet**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c592a-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![在 WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image1.png)
2. <span data-ttu-id="c592a-123">這會啟動 NuGet 套件管理員，並顯示可用的套件。</span><span class="sxs-lookup"><span data-stu-id="c592a-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="c592a-124">在 [搜尋] 方塊中，輸入您想要安裝的協助程式是關鍵字。</span><span class="sxs-lookup"><span data-stu-id="c592a-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![在 WebMatrix 中的 [NuGet 資源庫] 對話方塊](installing-helpers/_static/image2.png)
3. <span data-ttu-id="c592a-126">選取封裝，然後按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="c592a-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="c592a-127">按一下 **是**時詢問您是否要安裝套件，並指出您接受條款。</span><span class="sxs-lookup"><span data-stu-id="c592a-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="c592a-128">如果這是您已安裝的協助程式的第一次，NuGet 會在您的網站的協助程式，使您的程式碼中建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="c592a-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="c592a-129">若要解除安裝的協助程式，請按一下**資源庫**按鈕，再按一下**已安裝**索引標籤，然後挑選您想要解除安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="c592a-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="c592a-130">安裝 Twitter 協助程式</span><span class="sxs-lookup"><span data-stu-id="c592a-130">Installing the Twitter helper</span></span>

<span data-ttu-id="c592a-131">Twitter API 的最新版本不相容，與您透過 NuGet 安裝 Twitter 協助程式。</span><span class="sxs-lookup"><span data-stu-id="c592a-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="c592a-132">相反地，請參閱 <<c0> [ 使用 WebMatrix 的 Twitter Helper](twitter-helper.md)主題以取得有關如何設定 Twitter 協助程式，在您的專案中的資訊。</span><span class="sxs-lookup"><span data-stu-id="c592a-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c592a-133">其他資源</span><span class="sxs-lookup"><span data-stu-id="c592a-133">Additional Resources</span></span>


[<span data-ttu-id="c592a-134">簡介的 ASP.NET Web Pages 2-程式設計基本概念</span><span class="sxs-lookup"><span data-stu-id="c592a-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="c592a-135">使用 WebMatrix 的 twitter Helper</span><span class="sxs-lookup"><span data-stu-id="c592a-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
