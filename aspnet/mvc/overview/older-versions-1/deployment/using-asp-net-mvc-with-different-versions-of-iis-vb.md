---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: 將ASP.NET MVC 與不同版本的 IIS (VB) 使用 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何使用ASP.NET MVC 和 URL 路由,以及不同版本的 Internet 資訊服務。 你學習不同的原則...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 5e04ae14026e6d5dd1e603be6c52ff6876a468cf
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541997"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a><span data-ttu-id="5c801-104">使用 ASP.NET MVC 與不同版本的 IIS (VB)</span><span class="sxs-lookup"><span data-stu-id="5c801-104">Using ASP.NET MVC with Different Versions of IIS (VB)</span></span>

<span data-ttu-id="5c801-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5c801-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5c801-106">在本教學中,您將瞭解如何使用ASP.NET MVC 和 URL 路由,以及不同版本的 Internet 資訊服務。</span><span class="sxs-lookup"><span data-stu-id="5c801-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="5c801-107">您將學習將 ASP.NET MVC 與 IIS 7.0(經典模式)、IIS 6.0 和早期版本的 IIS 使用的不同策略。</span><span class="sxs-lookup"><span data-stu-id="5c801-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>

<span data-ttu-id="5c801-108">ASP.NET MVC 框架依賴於 ASP.NET 路由來將瀏覽器請求路由到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="5c801-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="5c801-109">為了利用ASP.NET路由,您可能需要在Web伺服器上執行其他配置步驟。</span><span class="sxs-lookup"><span data-stu-id="5c801-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="5c801-110">這完全取決於互聯網資訊服務 (IIS) 的版本和應用程式的請求處理模式。</span><span class="sxs-lookup"><span data-stu-id="5c801-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="5c801-111">以下是不同版本的 IIS 的摘要:</span><span class="sxs-lookup"><span data-stu-id="5c801-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="5c801-112">IIS 7.0(整合模式) - 無需特殊配置ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="5c801-113">IIS 7.0(經典模式) - 您需要執行特殊配置才能使用ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="5c801-114">IIS 6.0 或以下 - 您需要執行特殊配置才能使用ASP.NET路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="5c801-115">最新版本的IIS版本為7.5版本(在Win7上)。</span><span class="sxs-lookup"><span data-stu-id="5c801-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="5c801-116">IIS 7 的 IIS 包含在 Windows 伺服器 2008 和 VISTA/SP1 及更高版本中。</span><span class="sxs-lookup"><span data-stu-id="5c801-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="5c801-117">您還可以在 Vista 作業系統的任何版本上安裝 IIS 7.0,但家庭[https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)基本版除外 (參見 )。</span><span class="sxs-lookup"><span data-stu-id="5c801-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="5c801-118">IIS 7.0 支援兩種處理請求的模式。</span><span class="sxs-lookup"><span data-stu-id="5c801-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="5c801-119">您可以使用整合模式或傳統模式。</span><span class="sxs-lookup"><span data-stu-id="5c801-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="5c801-120">在整合模式下使用IIS 7.0時,無需執行任何特殊配置步驟。</span><span class="sxs-lookup"><span data-stu-id="5c801-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="5c801-121">但是,在經典模式下使用IIS 7.0時,您確實需要執行其他配置。</span><span class="sxs-lookup"><span data-stu-id="5c801-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="5c801-122">微軟 Windows 伺服器 2003 包括 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="5c801-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="5c801-123">使用 Windows Server 2003 作業系統時,無法將 IIS 6.0 升級到 IIS 7.0。</span><span class="sxs-lookup"><span data-stu-id="5c801-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="5c801-124">使用IIS 6.0時,必須執行其他配置步驟。</span><span class="sxs-lookup"><span data-stu-id="5c801-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="5c801-125">微軟視窗XP專業版包括IIS 5.1。</span><span class="sxs-lookup"><span data-stu-id="5c801-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="5c801-126">使用IIS 5.1時,必須執行其他配置步驟。</span><span class="sxs-lookup"><span data-stu-id="5c801-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="5c801-127">最後,微軟 Windows 2000 和微軟 Windows 2000 專業版包括 IIS 5.0。</span><span class="sxs-lookup"><span data-stu-id="5c801-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="5c801-128">使用IIS 5.0時,必須執行其他配置步驟。</span><span class="sxs-lookup"><span data-stu-id="5c801-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="5c801-129">整合模式與傳統模式</span><span class="sxs-lookup"><span data-stu-id="5c801-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="5c801-130">IIS 7.0 可以使用兩種不同的請求處理模式處理請求:集成和經典。</span><span class="sxs-lookup"><span data-stu-id="5c801-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="5c801-131">集成模式提供更好的性能和更多功能。</span><span class="sxs-lookup"><span data-stu-id="5c801-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="5c801-132">經典模式包括向後相容早期版本的IIS。</span><span class="sxs-lookup"><span data-stu-id="5c801-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="5c801-133">請求處理模式由應用程式池確定。</span><span class="sxs-lookup"><span data-stu-id="5c801-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="5c801-134">通過確定與應用程式關聯的應用程式池,可以確定特定 Web 應用程式正在使用哪種處理模式。</span><span class="sxs-lookup"><span data-stu-id="5c801-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="5c801-135">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c801-135">Follow these steps:</span></span>

1. <span data-ttu-id="5c801-136">推出網際網路資訊服務管理員</span><span class="sxs-lookup"><span data-stu-id="5c801-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="5c801-137">在「連線」視窗中,選擇應用程式</span><span class="sxs-lookup"><span data-stu-id="5c801-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="5c801-138">在「操作」視窗中,按下 **「基本設定」** 連結以開啟「編輯應用程式」對話框(參見圖 1)</span><span class="sxs-lookup"><span data-stu-id="5c801-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="5c801-139">請注意所選的應用程式池。</span><span class="sxs-lookup"><span data-stu-id="5c801-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="5c801-140">預設情況下,IIS 設定為支援兩個應用程式池:**預設 AppPool**和**經典 .NET AppPool**。</span><span class="sxs-lookup"><span data-stu-id="5c801-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="5c801-141">如果選擇了預設AppPool,則應用程式以整合的請求處理模式運行。</span><span class="sxs-lookup"><span data-stu-id="5c801-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="5c801-142">如果選擇了經典 .NET AppPool,則應用程式以經典請求處理模式運行。</span><span class="sxs-lookup"><span data-stu-id="5c801-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>

<span data-ttu-id="5c801-143">[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5c801-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span></span>

<span data-ttu-id="5c801-144">**圖1:** 偵測要求處理模式([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5c801-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span></span>

<span data-ttu-id="5c801-145">請注意,您可以在"編輯應用程式"對話框中修改請求處理模式。</span><span class="sxs-lookup"><span data-stu-id="5c801-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="5c801-146">按下「選擇」按鈕並更改與應用程式關聯的應用程式池。</span><span class="sxs-lookup"><span data-stu-id="5c801-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="5c801-147">請注意,將ASP.NET應用程式從經典模式更改為集成模式時存在相容性問題。</span><span class="sxs-lookup"><span data-stu-id="5c801-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="5c801-148">如需詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="5c801-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="5c801-149">將 ASP.NET 1.1 升級到 Windows Vista 和 Windows 伺服器 2008 上的 IIS 7.0 --[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="5c801-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>

- <span data-ttu-id="5c801-150">ASP.NET與 IIS 7.0 整合 -[https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="5c801-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>

<span data-ttu-id="5c801-151">如果ASP.NET應用程式正在使用 DefaultAppPool,則無需執行任何其他步驟,就可以使ASP.NET路由(因此ASP.NET MVC)正常工作。</span><span class="sxs-lookup"><span data-stu-id="5c801-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="5c801-152">但是,如果ASP.NET應用程式配置為使用經典 .NET AppPool,然後繼續閱讀,您還有更多工作要做。</span><span class="sxs-lookup"><span data-stu-id="5c801-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="5c801-153">將ASP.NET MVC 與舊版本的 IIS 一起使用</span><span class="sxs-lookup"><span data-stu-id="5c801-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="5c801-154">如果您需要將 IIS 版本早於 IIS 7.0 的舊版本 ASP.NET MVC 使用,或者需要在傳統模式下使用 IIS 7.0,則有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="5c801-155">首先,您可以修改路由表以使用文件副檔名。</span><span class="sxs-lookup"><span data-stu-id="5c801-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="5c801-156">例如,您請求的 URL 不是 /Store/詳細資訊,而是請求 URL,如 /Store.aspx/詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5c801-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="5c801-157">第二個選項是創建稱為*通配符腳本映射*的內容。</span><span class="sxs-lookup"><span data-stu-id="5c801-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="5c801-158">通配符文稿對應讓您能夠將每個請求映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="5c801-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="5c801-159">如果您無法存取 Web 伺服器(例如,您的 ASP.NET MVC 應用程式由 Internet 服務提供者託管),則需要使用第一個選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="5c801-160">如果不想修改 URL 的外觀,並且可以訪問 Web 伺服器,則可以使用第二個選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="5c801-161">我們將在以下部分中詳細介紹每個選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="5c801-162">新增於表新增延伸</span><span class="sxs-lookup"><span data-stu-id="5c801-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="5c801-163">獲取ASP.NET路由以使用舊版本的IIS的最簡單方法是修改Global.asax檔中的路由表。</span><span class="sxs-lookup"><span data-stu-id="5c801-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="5c801-164">清單1中的預設和未修改的 Global.asax 檔配置了一個名為"預設路由"的路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="5c801-165">**清單1 - 全域.asax(未修改)**</span><span class="sxs-lookup"><span data-stu-id="5c801-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

<span data-ttu-id="5c801-166">通過清單 1 中設定的預設路由,您可以路由如下所示的 URL:</span><span class="sxs-lookup"><span data-stu-id="5c801-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="5c801-167">/首頁/索引</span><span class="sxs-lookup"><span data-stu-id="5c801-167">/Home/Index</span></span>

<span data-ttu-id="5c801-168">/產品/詳細資訊/3</span><span class="sxs-lookup"><span data-stu-id="5c801-168">/Product/Details/3</span></span>

<span data-ttu-id="5c801-169">/Product</span><span class="sxs-lookup"><span data-stu-id="5c801-169">/Product</span></span>

<span data-ttu-id="5c801-170">遺憾的是,舊版本的IIS不會將這些請求傳遞給ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="5c801-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="5c801-171">因此,這些請求不會路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="5c801-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="5c801-172">例如,如果您對 URL/Home/Index 發出瀏覽器請求,則將在圖 2 中獲取錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="5c801-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>

<span data-ttu-id="5c801-173">[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5c801-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span></span>

<span data-ttu-id="5c801-174">**圖2**: 收到 404 找不到錯誤([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5c801-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span></span>

<span data-ttu-id="5c801-175">較舊版本的IIS僅將某些請求映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="5c801-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="5c801-176">請求必須針對具有正確檔副檔名的 URL。</span><span class="sxs-lookup"><span data-stu-id="5c801-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="5c801-177">例如,對 /SomePage.aspx 的請求將映射到ASP.NET框架。</span><span class="sxs-lookup"><span data-stu-id="5c801-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="5c801-178">但是,對 /SomePage.htm 的請求沒有。</span><span class="sxs-lookup"><span data-stu-id="5c801-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="5c801-179">因此,要使ASP.NET路由正常工作,我們必須修改預設路由,以便它包含映射到ASP.NET框架的檔擴展名。</span><span class="sxs-lookup"><span data-stu-id="5c801-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="5c801-180">這是使用名為`registermvc.wsf`的腳本完成的。</span><span class="sxs-lookup"><span data-stu-id="5c801-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="5c801-181">它包含在 ASP.NET MVC`C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`1 版本中 ,但截至 ASP.NET 2,此文本[http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)已移動到 ASP.NET 期貨,可在 。</span><span class="sxs-lookup"><span data-stu-id="5c801-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="5c801-182">執行此文本會使用IIS註冊新的.mvc擴展。</span><span class="sxs-lookup"><span data-stu-id="5c801-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="5c801-183">註冊 .mvc 副檔名後,您可以在 Global.asax 檔中修改路由,以便路由使用 .mvc 擴展名。</span><span class="sxs-lookup"><span data-stu-id="5c801-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="5c801-184">清單2中修改後的 Global.asax 檔適用於舊版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="5c801-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="5c801-185">**清單 2 - 全域.asax(使用延伸修改)**</span><span class="sxs-lookup"><span data-stu-id="5c801-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]

<span data-ttu-id="5c801-186">重要提示:請記住在更改 Global.asax 檔後再次建構ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c801-186">Important: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>

<span data-ttu-id="5c801-187">清單2中全域.asax 檔有兩個重要更改。</span><span class="sxs-lookup"><span data-stu-id="5c801-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="5c801-188">現在,全域.asax 中定義了兩個路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="5c801-189">預設路由(第一個路由)的 URL 模式現在如下所示:</span><span class="sxs-lookup"><span data-stu-id="5c801-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="5c801-190">{控制器}.mvc/{操作}/{id}</span><span class="sxs-lookup"><span data-stu-id="5c801-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="5c801-191">.mvc 副檔名的添加會更改ASP.NET路由模組截獲的文件類型。</span><span class="sxs-lookup"><span data-stu-id="5c801-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="5c801-192">透過此變更,ASP.NET MVC 應用程式現在路由如下所示的請求:</span><span class="sxs-lookup"><span data-stu-id="5c801-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="5c801-193">/Home.mvc/指數/</span><span class="sxs-lookup"><span data-stu-id="5c801-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="5c801-194">/產品.mvc/細節/3</span><span class="sxs-lookup"><span data-stu-id="5c801-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="5c801-195">/產品.mvc/</span><span class="sxs-lookup"><span data-stu-id="5c801-195">/Product.mvc/</span></span>

<span data-ttu-id="5c801-196">第二個路由,根路由,是新的。</span><span class="sxs-lookup"><span data-stu-id="5c801-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="5c801-197">根路由的此 URL 模式是一個空字串。</span><span class="sxs-lookup"><span data-stu-id="5c801-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="5c801-198">對於匹配針對應用程式根發出的請求,此路由是必需的。</span><span class="sxs-lookup"><span data-stu-id="5c801-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="5c801-199">例如,根路由將匹配如下所示的請求:</span><span class="sxs-lookup"><span data-stu-id="5c801-199">For example, the Root route will match a request that looks like this:</span></span>

[http://www.YourApplication.com/](http://www.YourApplication.com/)

<span data-ttu-id="5c801-200">對路由表進行這些修改後,需要確保應用程式中的所有連結都與這些新 URL 模式相容。</span><span class="sxs-lookup"><span data-stu-id="5c801-200">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="5c801-201">換句話說,請確保所有連結都包含 .mvc 擴展。</span><span class="sxs-lookup"><span data-stu-id="5c801-201">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="5c801-202">如果使用 Html.ActionLink() 説明器方法產生連結,則不需要進行任何更改。</span><span class="sxs-lookup"><span data-stu-id="5c801-202">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>

<span data-ttu-id="5c801-203">您可以手動向 iIS 添加新擴展 ASP.NET,而不是使用 registermvc.wcf 腳本。</span><span class="sxs-lookup"><span data-stu-id="5c801-203">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="5c801-204">自行新增新副檔名時,請確保未選取的標記為 **「驗證該檔存在」 選單 。**</span><span class="sxs-lookup"><span data-stu-id="5c801-204">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>

## <a name="hosted-server"></a><span data-ttu-id="5c801-205">託管伺服器</span><span class="sxs-lookup"><span data-stu-id="5c801-205">Hosted Server</span></span>

<span data-ttu-id="5c801-206">您並不總是有權訪問 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5c801-206">You don't always have access to your web server.</span></span> <span data-ttu-id="5c801-207">例如,如果您使用 Internet 託管供應商託管 ASP.NET MVC 應用程式,則不一定有權訪問 IIS。</span><span class="sxs-lookup"><span data-stu-id="5c801-207">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="5c801-208">在這種情況下,應使用映射到ASP.NET框架的現有文件副檔名之一。</span><span class="sxs-lookup"><span data-stu-id="5c801-208">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="5c801-209">映射到ASP.NET的檔副檔名的範例包括 .aspx、.axd 和 .ashx 副檔名。</span><span class="sxs-lookup"><span data-stu-id="5c801-209">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="5c801-210">例如,清單 3 中修改的 Global.asax 檔使用 .aspx 擴展名而不是 .mvc 擴展名。</span><span class="sxs-lookup"><span data-stu-id="5c801-210">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="5c801-211">**清單 3 - 全域.asax(使用 .aspx 擴展修改)**</span><span class="sxs-lookup"><span data-stu-id="5c801-211">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

<span data-ttu-id="5c801-212">清單3中的 Global.asax 檔與以前的 Global.asax 檔案完全相同,只是它使用 .aspx 擴展名而不是 .mvc 副檔名。</span><span class="sxs-lookup"><span data-stu-id="5c801-212">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="5c801-213">您不必在遠端 Web 伺服器上執行任何設定才能使用 .aspx 擴展。</span><span class="sxs-lookup"><span data-stu-id="5c801-213">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="5c801-214">建立通配符文稿對應</span><span class="sxs-lookup"><span data-stu-id="5c801-214">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="5c801-215">如果您不想修改ASP.NET MVC 應用程式的 URL,並且可以造訪 Web 伺服器,則有其他選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-215">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="5c801-216">您可以建立通配符文本映射,將所有請求映射到 Web 伺服器 ASP.NET 框架。</span><span class="sxs-lookup"><span data-stu-id="5c801-216">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="5c801-217">這樣,您可以使用預設ASP.NET MVC 路由表與IIS 7.0(經典模式)或IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="5c801-217">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="5c801-218">請注意,此選項會導致IIS攔截針對Web伺服器的每個請求。</span><span class="sxs-lookup"><span data-stu-id="5c801-218">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="5c801-219">這包括對圖像、經典 ASP 頁面和 HTML 頁面的請求。</span><span class="sxs-lookup"><span data-stu-id="5c801-219">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="5c801-220">因此,將通配符腳本映射啟用ASP.NET確實會影響性能。</span><span class="sxs-lookup"><span data-stu-id="5c801-220">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="5c801-221">以下是為 IIS 7.0 啟用通配符文稿對應的方式:</span><span class="sxs-lookup"><span data-stu-id="5c801-221">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="5c801-222">在「連線」視窗中選擇應用程式</span><span class="sxs-lookup"><span data-stu-id="5c801-222">Select your application in the Connections window</span></span>
2. <span data-ttu-id="5c801-223">確保選擇**了 「功能」** 檢視</span><span class="sxs-lookup"><span data-stu-id="5c801-223">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="5c801-224">雙擊 **「處理程式映射」** 按鈕</span><span class="sxs-lookup"><span data-stu-id="5c801-224">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="5c801-225">按下 **「新增通配符文稿映射」** 連結(參見圖 3) 3</span><span class="sxs-lookup"><span data-stu-id="5c801-225">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="5c801-226">輸入 aspnet\_isapi.dll 檔案的路徑 (可以從 PageHandlerFactory 文稿映射複製此路徑)</span><span class="sxs-lookup"><span data-stu-id="5c801-226">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="5c801-227">輸入名稱 MVC</span><span class="sxs-lookup"><span data-stu-id="5c801-227">Enter the name MVC</span></span>
7. <span data-ttu-id="5c801-228">點選 **「確定」** 按鈕</span><span class="sxs-lookup"><span data-stu-id="5c801-228">Click the **OK** button</span></span>

<span data-ttu-id="5c801-229">[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5c801-229">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span></span>

<span data-ttu-id="5c801-230">**圖 3**: 使用 IIS 7.0 建立通配符文稿映射([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5c801-230">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span></span>

<span data-ttu-id="5c801-231">依以下步驟建立具有 IIS 6.0 的通配符文稿映射:</span><span class="sxs-lookup"><span data-stu-id="5c801-231">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="5c801-232">右鍵按一下網站並選擇"屬性"</span><span class="sxs-lookup"><span data-stu-id="5c801-232">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="5c801-233">選擇**家目錄**選項卡</span><span class="sxs-lookup"><span data-stu-id="5c801-233">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="5c801-234">點選 **「設定」** 按鈕</span><span class="sxs-lookup"><span data-stu-id="5c801-234">Click the **Configuration** button</span></span>
4. <span data-ttu-id="5c801-235">選擇**映射選項**卡</span><span class="sxs-lookup"><span data-stu-id="5c801-235">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="5c801-236">點選 **「插入」** 按鈕(參見圖 4)</span><span class="sxs-lookup"><span data-stu-id="5c801-236">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="5c801-237">將 aspnet\_isapi.dll 的路徑貼上為可執行欄位(可以從 .aspx 檔案的文稿映射中複製此路徑)</span><span class="sxs-lookup"><span data-stu-id="5c801-237">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="5c801-238">取消選擇標籤為 **「驗證檔案存在」複選框**</span><span class="sxs-lookup"><span data-stu-id="5c801-238">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="5c801-239">點選 **「確定」** 按鈕</span><span class="sxs-lookup"><span data-stu-id="5c801-239">Click the **OK** button</span></span>

<span data-ttu-id="5c801-240">[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5c801-240">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span></span>

<span data-ttu-id="5c801-241">**圖 4**: 使用 IIS 6.0 建立通配符文稿映射([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5c801-241">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span></span>

<span data-ttu-id="5c801-242">啟用通配符文本映射後,需要修改 Global.asax 檔中的路由表,以便它包含根路由。</span><span class="sxs-lookup"><span data-stu-id="5c801-242">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="5c801-243">否則,當您請求應用程式的根頁時,您將獲得圖 5 中的錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="5c801-243">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="5c801-244">您可以使用清單 4 中修改的 Global.asax 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c801-244">You can use the modified Global.asax file in Listing 4.</span></span>

<span data-ttu-id="5c801-245">[![[New Project] \(新增專案\) 對話方塊](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5c801-245">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span></span>

<span data-ttu-id="5c801-246">**圖 5**: 缺少根路由錯誤([按下以檢視全尺寸影像](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5c801-246">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span></span>

<span data-ttu-id="5c801-247">**清單 4 - 全域.asax(使用根路由修改)**</span><span class="sxs-lookup"><span data-stu-id="5c801-247">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

<span data-ttu-id="5c801-248">為 IIS 7.0 或 IIS 6.0 啟用通配符文本映射後,可以發出適用於預設路由表的請求,如下所示:</span><span class="sxs-lookup"><span data-stu-id="5c801-248">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="5c801-249">/首頁/索引</span><span class="sxs-lookup"><span data-stu-id="5c801-249">/Home/Index</span></span>

<span data-ttu-id="5c801-250">/產品/詳細資訊/3</span><span class="sxs-lookup"><span data-stu-id="5c801-250">/Product/Details/3</span></span>

<span data-ttu-id="5c801-251">/Product</span><span class="sxs-lookup"><span data-stu-id="5c801-251">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="5c801-252">總結</span><span class="sxs-lookup"><span data-stu-id="5c801-252">Summary</span></span>

<span data-ttu-id="5c801-253">本教學的目的是解釋在使用舊版本的 IIS(或經典模式下的 IIS 7.0)時如何使用ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="5c801-253">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="5c801-254">我們討論了使ASP.NET路由與舊版本的IIS配合使用的方法:修改預設路由表或創建通配符腳本映射。</span><span class="sxs-lookup"><span data-stu-id="5c801-254">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="5c801-255">第一個選項要求您修改ASP.NET MVC 應用程式中使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="5c801-255">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="5c801-256">第一個選項的一個顯著優點是,您不需要訪問 Web 伺服器來修改路由表。</span><span class="sxs-lookup"><span data-stu-id="5c801-256">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="5c801-257">這意味著,即使使用 internet 託管公司託管 ASP.NET MVC 應用程式,您也可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="5c801-257">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="5c801-258">第二個選項是創建通配符腳本映射。</span><span class="sxs-lookup"><span data-stu-id="5c801-258">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="5c801-259">第二個選項的優點是不需要修改 URL。</span><span class="sxs-lookup"><span data-stu-id="5c801-259">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="5c801-260">第二個選項的缺點是它會影響ASP.NET MVC 應用程式的性能。</span><span class="sxs-lookup"><span data-stu-id="5c801-260">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5c801-261">上一步</span><span class="sxs-lookup"><span data-stu-id="5c801-261">Previous</span></span>](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
