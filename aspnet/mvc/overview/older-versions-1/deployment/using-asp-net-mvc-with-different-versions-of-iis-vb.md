---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 使用 ASP.NET MVC 與不同版本的 IIS (VB) |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將了解如何使用不同版本的 Internet Information Services 中的 ASP.NET MVC 和 URL 路由。 您了解不同的策略...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 0446a125845134d2fad869094a540c960f6b0a25
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59406466"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a><span data-ttu-id="bdb0f-104">使用 ASP.NET MVC 與不同版本的 IIS (VB)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-104">Using ASP.NET MVC with Different Versions of IIS (VB)</span></span>

<span data-ttu-id="bdb0f-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="bdb0f-106">在本教學課程中，您將了解如何使用不同版本的 Internet Information Services 中的 ASP.NET MVC 和 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="bdb0f-107">您將了解不同的策略來使用 IIS 7.0 （傳統模式）、 IIS 6.0 和舊版 IIS 的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>


<span data-ttu-id="bdb0f-108">ASP.NET MVC 架構而定 ASP.NET 路由將瀏覽器要求路由傳送至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="bdb0f-109">若要充分利用 ASP.NET 路由，您可能在您的 web 伺服器上執行其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="bdb0f-110">它完全取決於 Internet Information Services (IIS) 和要求處理模式，您的應用程式的版本。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="bdb0f-111">以下是不同的 IIS 版本的摘要：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="bdb0f-112">IIS 的 7.0 （整合模式）-使用 ASP.NET 路由所需的任何特殊設定。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="bdb0f-113">IIS 7.0 （傳統模式）-您需要執行特殊的設定，以使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="bdb0f-114">IIS 6.0 或以下-您需要執行特殊的設定，以使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="bdb0f-115">最新的 IIS 版本是版本 7.5 （Win7)。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="bdb0f-116">IIS 7 的 IIS 是包含與 Windows Server 2008 與 VISTA SP1 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="bdb0f-117">您也可以安裝 IIS 7.0 在 Vista 作業系統，Home Basic 除外的任何版本上 (請參閱[ https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx ](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx))。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="bdb0f-118">IIS 7.0 支援兩種模式來處理要求。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="bdb0f-119">您可以使用整合式的模式或傳統模式。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="bdb0f-120">您不需要執行任何特殊組態步驟，使用 IIS 7.0 整合模式中時。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="bdb0f-121">不過，您需要使用傳統模式中的 IIS 7.0 時執行其他設定。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="bdb0f-122">Microsoft Windows Server 2003 包含 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="bdb0f-123">使用 Windows Server 2003 作業系統時，您就無法升級至 IIS 7.0 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="bdb0f-124">使用 IIS 6.0 時，您必須執行其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="bdb0f-125">Microsoft Windows XP Professional 包含 IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="bdb0f-126">當使用 IIS 5.1，您必須執行其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="bdb0f-127">最後，Microsoft Windows 2000 和 Microsoft Windows 2000 Professional 包含 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="bdb0f-128">使用 IIS 5.0 時，您必須執行其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="bdb0f-129">與傳統模式整合</span><span class="sxs-lookup"><span data-stu-id="bdb0f-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="bdb0f-130">IIS 7.0 可處理要求使用兩種不同的要求處理模式： 整合和傳統。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="bdb0f-131">整合模式下提供較佳的效能和更多功能。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="bdb0f-132">傳統模式是適用於處理回溯相容性與較早版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="bdb0f-133">要求處理模式取決於應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="bdb0f-134">您可以判斷特定的 web 應用程式正在使用哪一個處理模式藉由判斷應用程式相關聯的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="bdb0f-135">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-135">Follow these steps:</span></span>

1. <span data-ttu-id="bdb0f-136">啟動 Internet Information Services 管理員</span><span class="sxs-lookup"><span data-stu-id="bdb0f-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="bdb0f-137">在 連線 視窗中，選取 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdb0f-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="bdb0f-138">在 動作 視窗中，按一下**基本設定**連結以開啟 編輯應用程式 對話方塊 （請參閱 圖 1）</span><span class="sxs-lookup"><span data-stu-id="bdb0f-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="bdb0f-139">記下所選取的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="bdb0f-140">根據預設，IIS 會設定為支援兩個應用程式集區：**DefaultAppPool**並**傳統.NET AppPool**。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="bdb0f-141">如果選取 [DefaultAppPool]，在整合式的要求處理模式中執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="bdb0f-142">如果已選取傳統.NET 應用程式集區，您的應用程式以傳統的要求處理模式中執行。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>


<span data-ttu-id="bdb0f-143">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span></span>

<span data-ttu-id="bdb0f-144">**圖 1**:偵測要求處理模式 ([按一下以檢視完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="bdb0f-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span></span>


<span data-ttu-id="bdb0f-145">請注意，您可以修改要求處理模式中編輯應用程式 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="bdb0f-146">按一下 [選取] 按鈕，並變更應用程式相關聯的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="bdb0f-147">請注意，相容性問題時沒有從傳統變更 ASP.NET 應用程式，以整合模式。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="bdb0f-148">如需詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="bdb0f-149">升級至 Windows Vista 和 Windows Server 2008 上，IIS 7.0 的 ASP.NET 1.1 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>

- <span data-ttu-id="bdb0f-150">與 IIS 7.0-ASP.NET 整合 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>


<span data-ttu-id="bdb0f-151">如果 ASP.NET 應用程式使用 「 DefaultAppPool 」，您不需要執行任何額外的步驟，以取得 ASP.NET 路由，因此 ASP.NET MVC） 運作。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="bdb0f-152">不過，如果 ASP.NET 應用程式設定成使用傳統.NET 應用程式時，會將集區，然後繼續閱讀，您會有更多工作來執行。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="bdb0f-153">使用 ASP.NET MVC 與較舊版本的 IIS</span><span class="sxs-lookup"><span data-stu-id="bdb0f-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="bdb0f-154">如果您需要使用較舊版本比 IIS 7.0 之 IIS 的 ASP.NET MVC，或您需要使用傳統模式中的 IIS 7.0，您會有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="bdb0f-155">首先，您可以修改的路由表，來使用檔案的副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="bdb0f-156">比方說，而不是要求 /Store/Details 之類的 URL，您便可以要求 /Store.aspx/Details 之類的 URL。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="bdb0f-157">第二個選項是建立所謂*萬用字元指令碼對應*。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="bdb0f-158">萬用字元指令碼對應可讓您將每個要求對應至 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="bdb0f-159">如果您不需要存取您的網頁伺服器 (例如，您的 ASP.NET MVC 應用程式由網際網路服務提供者裝載) 將會需要使用第一個選項。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="bdb0f-160">如果您不想要修改您的 Url 的外觀，而且您可以存取您的 web 伺服器，您可以使用第二個選項。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="bdb0f-161">我們將探討下列章節詳細說明每個選項。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="bdb0f-162">路由表中加入擴充功能</span><span class="sxs-lookup"><span data-stu-id="bdb0f-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="bdb0f-163">取得 ASP.NET 路由傳送至舊版 IIS 所使用的最簡單方式是修改您在 Global.asax 檔案中的路由表。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="bdb0f-164">預設值，並在 列表 1 中的未修改的 Global.asax 檔案設定一個名為預設路由的路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="bdb0f-165">**列表 1-Global.asax （未經修改）**</span><span class="sxs-lookup"><span data-stu-id="bdb0f-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

<span data-ttu-id="bdb0f-166">在 列表 1 中設定的預設路由可讓您看起來像這樣的路由 Url:</span><span class="sxs-lookup"><span data-stu-id="bdb0f-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="bdb0f-167">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="bdb0f-167">/Home/Index</span></span>

<span data-ttu-id="bdb0f-168">/ 產品/詳細資料/3</span><span class="sxs-lookup"><span data-stu-id="bdb0f-168">/Product/Details/3</span></span>

<span data-ttu-id="bdb0f-169">/Product</span><span class="sxs-lookup"><span data-stu-id="bdb0f-169">/Product</span></span>

<span data-ttu-id="bdb0f-170">不幸的是，舊版 IIS 將不會將這些要求傳遞給 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="bdb0f-171">因此，這些要求將不會路由至控制器。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="bdb0f-172">例如，如果您的瀏覽器要求對 URL /Home/索引然後得到錯誤頁面 [圖 2] 中。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>


<span data-ttu-id="bdb0f-173">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span></span>

<span data-ttu-id="bdb0f-174">**圖 2**:收到 404 找不到的錯誤 ([按一下以檢視完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="bdb0f-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span></span>


<span data-ttu-id="bdb0f-175">舊版 IIS 只會對應至 ASP.NET framework 的特定要求。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="bdb0f-176">要求必須是正確的檔案副檔名的 URL。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="bdb0f-177">比方說，/SomePage.aspx 要求取得對應至 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="bdb0f-178">不過，/SomePage.htm 的要求則否。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="bdb0f-179">因此，若要取得 ASP.NET 路由傳送至工作，我們必須修改預設路由使其包含對應至 ASP.NET framework 的副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="bdb0f-180">這是使用名為指令碼`registermvc.wsf`。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="bdb0f-181">它是隨附在中的 ASP.NET MVC 1 發行`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`，但 ASP.NET 2 此指令碼已移至 ASP.NET Futures 網址[ http://aspnet.codeplex.com/releases/view/39978 ](http://aspnet.codeplex.com/releases/view/39978)。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="bdb0f-182">執行此指令碼，是在 IIS 中向新的.mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="bdb0f-183">將.mvc 副檔名登錄在之後，您可以修改您 Global.asax 檔案中的路由，以便路由使用.mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="bdb0f-184">修改的 Global.asax 檔案列表 2 中的運作方式與較舊版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="bdb0f-185">**列表 2-Global.asax （使用擴充功能修改）**</span><span class="sxs-lookup"><span data-stu-id="bdb0f-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]


<span data-ttu-id="bdb0f-186">重要事項： 請記得在變更 Global.asax 檔案之後，再次建置您的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-186">Important: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>


<span data-ttu-id="bdb0f-187">有兩個重要的變更，以列表 2 中的 Global.asax 檔。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="bdb0f-188">現在有兩個 Global.asax 中所定義的路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="bdb0f-189">預設路由，而第一個路由的 URL 模式現在看起來像：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="bdb0f-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="bdb0f-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="bdb0f-191">新增.mvc 副檔名會變更 ASP.NET 路由模組攔截的檔案的類型。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="bdb0f-192">透過這項變更，ASP.NET MVC 應用程式現在將路由傳送要求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="bdb0f-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="bdb0f-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="bdb0f-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="bdb0f-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="bdb0f-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="bdb0f-195">/Product.mvc/</span></span>

<span data-ttu-id="bdb0f-196">第二個路由，也就是根路由，是新功能。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="bdb0f-197">此根路由的 URL 模式為空字串。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="bdb0f-198">此路由是必要的比對要求對應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="bdb0f-199">例如，根路由會比對的要求，看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="bdb0f-200">之後進行這些修改以您的路由表，您必須確定所有應用程式中的連結會使用這些新的 URL 模式相容。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="bdb0f-201">換句話說，請確定所有的連結包含.mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="bdb0f-202">如果您使用 Html.ActionLink() helper 方法來產生您的連結，然後您應該不需要進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>


<span data-ttu-id="bdb0f-203">而不是使用 registermvc.wcf 指令碼，您可以將新的延伸模組加入以手動方式對應至 ASP.NET framework 的 IIS。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="bdb0f-204">當自行新增新的延伸模組，請確定核取方塊標示**確認該檔案已經存在**就不會檢查。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>


## <a name="hosted-server"></a><span data-ttu-id="bdb0f-205">託管的伺服器</span><span class="sxs-lookup"><span data-stu-id="bdb0f-205">Hosted Server</span></span>

<span data-ttu-id="bdb0f-206">您永遠不能存取到您的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-206">You don't always have access to your web server.</span></span> <span data-ttu-id="bdb0f-207">比方說，如果您裝載使用網際網路裝載提供者的 ASP.NET MVC 應用程式，接著您不一定可存取 iis。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="bdb0f-208">在此情況下，您應該使用其中一個現有的檔案副檔名對應到 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="bdb0f-209">副檔名對應到 ASP.NET 的範例包括.aspx、.axd 和.ashx 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="bdb0f-210">比方說，修改過的 Global.asax 檔案列表 3 中會使用.aspx 擴充功能，而非.mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="bdb0f-211">**列表 3-Global.asax （使用.aspx 擴充功能修改）**</span><span class="sxs-lookup"><span data-stu-id="bdb0f-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

<span data-ttu-id="bdb0f-212">列表 3 中的 Global.asax 檔正是與先前的 Global.asax 檔案，除了它使用.aspx 擴充功能，而非.mvc 副檔名相同。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="bdb0f-213">您沒有使用副檔名.aspx 遠端網頁伺服器上執行任何設定。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="bdb0f-214">建立萬用字元指令碼對應</span><span class="sxs-lookup"><span data-stu-id="bdb0f-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="bdb0f-215">如果您不想要修改的 ASP.NET MVC 應用程式的 Url，而且您可以存取您的 web 伺服器，您會有額外的選項。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="bdb0f-216">您可以建立萬用字元指令碼對應將所有的要求對應至 ASP.NET framework web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="bdb0f-217">如此一來，您可以使用預設 ASP.NET MVC 路由表 （以傳統模式） 的 IIS 7.0 或 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="bdb0f-218">請注意，此選項可讓 IIS 以攔截對網頁伺服器提出的每個要求。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="bdb0f-219">這包括影像、 傳統 ASP 網頁和 HTML 網頁的要求。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="bdb0f-220">因此，啟用萬用字元指令碼對應至 ASP.NET 沒有影響效能。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="bdb0f-221">以下是如何啟用萬用字元指令碼對應的 IIS 7.0:</span><span class="sxs-lookup"><span data-stu-id="bdb0f-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="bdb0f-222">在 [連線] 視窗中選取您的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdb0f-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="bdb0f-223">請確定**功能**選取檢視</span><span class="sxs-lookup"><span data-stu-id="bdb0f-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="bdb0f-224">按兩下**處理常式對應**按鈕</span><span class="sxs-lookup"><span data-stu-id="bdb0f-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="bdb0f-225">按一下 **新增萬用字元指令碼對應**連結 （請參閱 圖 3）</span><span class="sxs-lookup"><span data-stu-id="bdb0f-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="bdb0f-226">輸入的路徑 aspnet\_isapi.dll 檔案 （您可以從 Pagehandlerfactory-isapi 指令碼對應複製這個路徑）</span><span class="sxs-lookup"><span data-stu-id="bdb0f-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="bdb0f-227">輸入名稱 MVC</span><span class="sxs-lookup"><span data-stu-id="bdb0f-227">Enter the name MVC</span></span>
7. <span data-ttu-id="bdb0f-228">按一下 **確定**按鈕</span><span class="sxs-lookup"><span data-stu-id="bdb0f-228">Click the **OK** button</span></span>


<span data-ttu-id="bdb0f-229">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span></span>

<span data-ttu-id="bdb0f-230">**圖 3**:使用 IIS 7.0 建立萬用字元指令碼對應 ([按一下以檢視完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="bdb0f-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span></span>


<span data-ttu-id="bdb0f-231">請遵循下列步驟來建立與 IIS 6.0 的萬用字元指令碼對應：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="bdb0f-232">以滑鼠右鍵按一下網站，然後選取 屬性</span><span class="sxs-lookup"><span data-stu-id="bdb0f-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="bdb0f-233">選取 [**主目錄**] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="bdb0f-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="bdb0f-234">按一下 **組態**按鈕</span><span class="sxs-lookup"><span data-stu-id="bdb0f-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="bdb0f-235">選取 [**對應**] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="bdb0f-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="bdb0f-236">按一下 **插入**按鈕 （請參閱 圖 4）</span><span class="sxs-lookup"><span data-stu-id="bdb0f-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="bdb0f-237">貼上路徑 aspnet\_isapi.dll 到可執行檔的欄位 （您可以從指令碼對應.aspx 檔案複製這個路徑）</span><span class="sxs-lookup"><span data-stu-id="bdb0f-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="bdb0f-238">標示的核取方塊取消核取 **確認該檔案已經存在**</span><span class="sxs-lookup"><span data-stu-id="bdb0f-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="bdb0f-239">按一下 **確定**按鈕</span><span class="sxs-lookup"><span data-stu-id="bdb0f-239">Click the **OK** button</span></span>


<span data-ttu-id="bdb0f-240">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span></span>

<span data-ttu-id="bdb0f-241">**圖 4**:使用 IIS 6.0 建立萬用字元指令碼對應 ([按一下以檢視完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="bdb0f-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span></span>


<span data-ttu-id="bdb0f-242">啟用萬用字元指令碼對應之後，您需要修改 Global.asax 檔案中的路由表，使其包含根路由。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="bdb0f-243">否則，您會得到錯誤頁面圖 5 中，提出您的應用程式的根頁面的要求時。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="bdb0f-244">您可以使用修改過的 Global.asax 檔案中列出的 4。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-244">You can use the modified Global.asax file in Listing 4.</span></span>


<span data-ttu-id="bdb0f-245">[![[新增專案] 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="bdb0f-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span></span>

<span data-ttu-id="bdb0f-246">**圖 5**:遺漏根路由錯誤 ([按一下以檢視完整大小的影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="bdb0f-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span></span>


<span data-ttu-id="bdb0f-247">**列表 4-Global.asax （根路由與修改）**</span><span class="sxs-lookup"><span data-stu-id="bdb0f-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

<span data-ttu-id="bdb0f-248">IIS 7.0 或 IIS 6.0 中啟用萬用字元指令碼對應之後，您可以建立使用預設路由表，看起來像這樣的要求：</span><span class="sxs-lookup"><span data-stu-id="bdb0f-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="bdb0f-249">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="bdb0f-249">/Home/Index</span></span>

<span data-ttu-id="bdb0f-250">/ 產品/詳細資料/3</span><span class="sxs-lookup"><span data-stu-id="bdb0f-250">/Product/Details/3</span></span>

<span data-ttu-id="bdb0f-251">/Product</span><span class="sxs-lookup"><span data-stu-id="bdb0f-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="bdb0f-252">總結</span><span class="sxs-lookup"><span data-stu-id="bdb0f-252">Summary</span></span>

<span data-ttu-id="bdb0f-253">本教學課程的目標是要說明如何使用 ASP.NET MVC，使用較舊版本的 IIS （或傳統模式中的 IIS 7.0） 時。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="bdb0f-254">我們將討論兩種方法可以取得 ASP.NET 路由傳送至舊版 IIS 的工作：修改預設路由表，或建立萬用字元指令碼對應。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="bdb0f-255">第一個選項需要您修改您的 ASP.NET MVC 應用程式中使用的 Url。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="bdb0f-256">這個第一個選項的其中一個非常重要的優點是，您不需要 web 伺服器的存取權才能修改路由表。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="bdb0f-257">這表示，您就可以使用此第一個選項，即使裝載 ASP.NET MVC 應用程式使用網際網路主機服務公司。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="bdb0f-258">第二個選項是建立萬用字元指令碼對應。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="bdb0f-259">此第二個選項的優點是您不需要修改您的 Url。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="bdb0f-260">此第二個選項的缺點是，它可能會影響您的 ASP.NET MVC 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="bdb0f-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="bdb0f-261">上一步</span><span class="sxs-lookup"><span data-stu-id="bdb0f-261">Previous</span></span>](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
