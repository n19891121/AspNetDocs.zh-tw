---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: 簡介 ASP.NET Web Pages 使用 WebMatrix 發佈網站 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程是教學課程集中的最後一篇介紹 ASP.NET Web Pages 和 Microsoft WebMatrix 的文章。 它會討論如何發佈您的網站 t .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240590"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a><span data-ttu-id="8a982-104">簡介 ASP.NET Web Pages 使用 WebMatrix 發佈網站</span><span class="sxs-lookup"><span data-stu-id="8a982-104">Introducing ASP.NET Web Pages - Publishing a Site by Using WebMatrix</span></span>

<span data-ttu-id="8a982-105"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8a982-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8a982-106">本教學課程是教學課程集中的最後一篇介紹 ASP.NET Web Pages 和 Microsoft WebMatrix 的文章。</span><span class="sxs-lookup"><span data-stu-id="8a982-106">This tutorial is the final installment in the tutorial set that introduces ASP.NET Web Pages and Microsoft WebMatrix.</span></span> <span data-ttu-id="8a982-107">它會討論如何將您的網站發佈至網際網路，讓其他人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="8a982-107">It discusses how to publish your site to the Internet so that others can work with it.</span></span> <span data-ttu-id="8a982-108">它假設您已完成[建立 ASP.NET Web Pages 網站一致外觀](https://go.microsoft.com/fwlink/?LinkId=251585)的系列。</span><span class="sxs-lookup"><span data-stu-id="8a982-108">It assumes you have completed the series through [Creating a Consistent Look for ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=251585).</span></span>
> 
> <span data-ttu-id="8a982-109">您將瞭解如何使用發佈您的網站：</span><span class="sxs-lookup"><span data-stu-id="8a982-109">You'll learn how to publish your site using:</span></span>
> 
> - <span data-ttu-id="8a982-110">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8a982-110">Microsoft Azure</span></span>
> - <span data-ttu-id="8a982-111">Web 主控公司</span><span class="sxs-lookup"><span data-stu-id="8a982-111">Web Hosting Company</span></span>

## <a name="about-publishing-your-site"></a><span data-ttu-id="8a982-112">關於發佈您的網站</span><span class="sxs-lookup"><span data-stu-id="8a982-112">About Publishing Your Site</span></span>

<span data-ttu-id="8a982-113">到目前為止，您已在本機電腦上完成所有工作，包括測試您的頁面。</span><span class="sxs-lookup"><span data-stu-id="8a982-113">Up to now, you've done all your work on a local computer, including testing your pages.</span></span> <span data-ttu-id="8a982-114">若要執行您的<em>cshtml</em>頁面，您已使用內建于 WebMatrix 的 web 伺服器，也就是 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="8a982-114">To run your<em>.cshtml</em> pages, you've used the web server that's built into WebMatrix, namely IIS Express.</span></span> <span data-ttu-id="8a982-115">但當然，沒有人可以看到您所建立的網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-115">But of course no one can see the site you've created except you.</span></span> <span data-ttu-id="8a982-116">若要讓其他人可以使用您的網站，您必須將它發佈到網際網路。</span><span class="sxs-lookup"><span data-stu-id="8a982-116">To let others work with your site, you have to publish it to the Internet.</span></span>

<span data-ttu-id="8a982-117">除非您已經有公用 web 伺服器的存取權，否則發佈表示您必須擁有具有*雲端平臺*或*主機服務提供者*的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a982-117">Unless you have access to a public web server already, publishing means that you have to have an account with a *cloud platform* or a *hosting provider*.</span></span> <span data-ttu-id="8a982-118">雲端平臺（例如 Microsoft Azure）會為您的應用程式提供隨選基礎結構。</span><span class="sxs-lookup"><span data-stu-id="8a982-118">A cloud platform, such as Microsoft Azure, provides on-demand infrastructure for your applications.</span></span> <span data-ttu-id="8a982-119">主機服務提供者是擁有可公開存取之網頁伺服器的公司，可出租您網站的空間。</span><span class="sxs-lookup"><span data-stu-id="8a982-119">A hosting provider is a company that owns publicly accessible web servers and that will rent you space for your site.</span></span> <span data-ttu-id="8a982-120">針對高容量的商業網站，主控方案會從數個月（或甚至免費）到每個月數百美元的小型網站執行。</span><span class="sxs-lookup"><span data-stu-id="8a982-120">Hosting plans run from a few dollars a month (or even free) for small sites to many hundreds of dollars a month for high-volume commercial websites.</span></span>

> [!NOTE]
> <span data-ttu-id="8a982-121">您可以透過網際網路服務提供者（ISP）存取公用 web 伺服器，以供家裡取得網際網路服務。</span><span class="sxs-lookup"><span data-stu-id="8a982-121">You might have access to a public web server via the internet service provider (ISP) that you use to get internet service at home.</span></span> <span data-ttu-id="8a982-122">不過，您的主控提供者必須支援 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="8a982-122">However, your hosting provider must support ASP.NET Web Pages.</span></span> <span data-ttu-id="8a982-123">許多 Isp 都不這麼做，但還是值得一次檢查。</span><span class="sxs-lookup"><span data-stu-id="8a982-123">Many ISPs don't, but it's always worth checking.</span></span>

<span data-ttu-id="8a982-124">在本教學課程中，我們將概述如何發佈。</span><span class="sxs-lookup"><span data-stu-id="8a982-124">In this tutorial, we'll give you an overview of how to publish.</span></span> <span data-ttu-id="8a982-125">提供所有專案的確切詳細資料並不實用，因為每個主機服務提供者的進程會有所不同。</span><span class="sxs-lookup"><span data-stu-id="8a982-125">It's not practical to provide exact details for everything, because the process differs a bit for every hosting provider.</span></span> <span data-ttu-id="8a982-126">但是，您將能瞭解此程式的運作方式。</span><span class="sxs-lookup"><span data-stu-id="8a982-126">But you'll get a good idea of how the process works.</span></span>

<span data-ttu-id="8a982-127">本教學課程包含四個區段：</span><span class="sxs-lookup"><span data-stu-id="8a982-127">This tutorial contains four sections:</span></span>

1. [<span data-ttu-id="8a982-128">設定預設頁面</span><span class="sxs-lookup"><span data-stu-id="8a982-128">Setting up the default page</span></span>](#defaultpage)
2. <span data-ttu-id="8a982-129">發行（選擇下列其中一項）</span><span class="sxs-lookup"><span data-stu-id="8a982-129">Publishing (choose one of the following)</span></span>  
 <span data-ttu-id="8a982-130">a.</span><span class="sxs-lookup"><span data-stu-id="8a982-130">a.</span></span> [<span data-ttu-id="8a982-131">將您的網站發佈至 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8a982-131">Publishing Your Site to Microsoft Azure</span></span>](#azure)  
 <span data-ttu-id="8a982-132">b.</span><span class="sxs-lookup"><span data-stu-id="8a982-132">b.</span></span> [<span data-ttu-id="8a982-133">將您的網站發佈至虛擬主機公司</span><span class="sxs-lookup"><span data-stu-id="8a982-133">Publishing Your Site to a Web Hosting Company</span></span>](#host)
3. [<span data-ttu-id="8a982-134">更新即時網站：重新發佈</span><span class="sxs-lookup"><span data-stu-id="8a982-134">Updating the Live Site: Republishing</span></span>](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a><span data-ttu-id="8a982-135">設定預設頁面</span><span class="sxs-lookup"><span data-stu-id="8a982-135">Setting up the default page</span></span>

<span data-ttu-id="8a982-136">當使用者流覽至您網站的基底位址時，會向使用者顯示網站的預設頁面。</span><span class="sxs-lookup"><span data-stu-id="8a982-136">When a user navigates to the base address for your web site, the default page for your site is displayed to the user.</span></span> <span data-ttu-id="8a982-137">例如，當*Default.htm*設定為網站的預設頁面時 `www.contoso.com` ，流覽至與 `www.contoso.com` 流覽至相同 `www.contoso.com/Default.htm` 。</span><span class="sxs-lookup"><span data-stu-id="8a982-137">For example, when *Default.htm* is set as the default page for the site at `www.contoso.com`, then navigating to `www.contoso.com` is the same as navigating to `www.contoso.com/Default.htm`.</span></span>

<span data-ttu-id="8a982-138">目前，您的網站會使用**預設的. cshtml**做為預設頁面。</span><span class="sxs-lookup"><span data-stu-id="8a982-138">Currently, your site uses **Default.cshtml** as the default page.</span></span> <span data-ttu-id="8a982-139">此頁面適用于您的預設頁面，但在本教學課程中，您尚未將任何內容新增至該頁面，因此會顯示空白頁面。</span><span class="sxs-lookup"><span data-stu-id="8a982-139">This page is fine for your default page, but in this tutorial you have not added any content to that page so it would display a blank page.</span></span> <span data-ttu-id="8a982-140">開啟 Default. cshtml，並以下列程式碼取代內容。</span><span class="sxs-lookup"><span data-stu-id="8a982-140">Open Default.cshtml and replace the content with the following code.</span></span>

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

<span data-ttu-id="8a982-141">現在您的網站已準備好發行。</span><span class="sxs-lookup"><span data-stu-id="8a982-141">Now your site is ready for publication.</span></span> <span data-ttu-id="8a982-142">首先，您將瞭解如何將網站部署至 Azure，以及如何將其部署至虛擬主機公司。</span><span class="sxs-lookup"><span data-stu-id="8a982-142">First, you will see how to deploy the site to Azure, and then how to deploy it to a web hosting company.</span></span> <span data-ttu-id="8a982-143">其中一個選項適用于您的網站，而您只需要遵循其中一個部署選項。</span><span class="sxs-lookup"><span data-stu-id="8a982-143">Either option works for your web site, and you only need to follow one of the deployment options.</span></span>

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a><span data-ttu-id="8a982-144">將您的網站發佈至 Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8a982-144">Publishing Your Site to Microsoft Azure</span></span>

<span data-ttu-id="8a982-145">本教學課程會先示範如何將您的網站部署至 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="8a982-145">This tutorial will first show you how to deploy your site to Microsoft Azure.</span></span> <span data-ttu-id="8a982-146">藉由使用 Microsoft 帳戶登入，您可以在 Azure 上建立多達10個免費網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-146">By signing in with a Microsoft account, you can create up to 10 free sites on Azure.</span></span> <span data-ttu-id="8a982-147">這些免費網站提供便利的方式來測試您的網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-147">These free sites provide a convenient way to test your sites.</span></span> <span data-ttu-id="8a982-148">您稍後可以隨時刪除此範例網站，以避免使用您所有的免費網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-148">You can always delete this example site later to avoid using all of your free sites.</span></span> <span data-ttu-id="8a982-149">只需要幾分鐘的時間，您就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a982-149">You can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8a982-150">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="8a982-150">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="8a982-151">在 [WebMatrix] 功能區中，按一下 [**發佈**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a982-151">In the WebMatrix ribbon, click the **Publish** button.</span></span>

![WebMatrix 功能區中的 [發佈] 按鈕](publishing/_static/image1.png)

<span data-ttu-id="8a982-153">[**發佈您的網站**] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="8a982-153">The **Publish Your Site** dialog box is displayed.</span></span> <span data-ttu-id="8a982-154">如果您尚未登入您的 Microsoft 帳戶，對話方塊會包含**開始使用 Azure**連結。</span><span class="sxs-lookup"><span data-stu-id="8a982-154">If you have not signed in to your Microsoft account, the dialog box will contain a **Get started with Azure** link.</span></span> <span data-ttu-id="8a982-155">按一下此連結。</span><span class="sxs-lookup"><span data-stu-id="8a982-155">Click this link.</span></span>

![發佈您的網站](publishing/_static/image2.png)

<span data-ttu-id="8a982-157">如果您尚未登入 Microsoft 帳戶，系統會再次提供您登入的機會。</span><span class="sxs-lookup"><span data-stu-id="8a982-157">If you have not signed in to a Microsoft account, you are again given the opportunity to sign in.</span></span> <span data-ttu-id="8a982-158">您必須登入 Microsoft 帳戶，才能在 Azure 上發佈您的網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-158">You must sign in to a Microsoft account to publish your site on Azure.</span></span>

![Sign In](publishing/_static/image3.png)

<span data-ttu-id="8a982-160">登入您的 Microsoft 帳戶之後，對話方塊中會包含在 Azure 上建立新網站或連線至 Azure 上的其中一個現有網站的連結。</span><span class="sxs-lookup"><span data-stu-id="8a982-160">After signing in to your Microsoft account, the dialog box contains links to create a new site on Azure or connect to one of your existing sites on Azure.</span></span>

![建立新網站](publishing/_static/image4.png)

<span data-ttu-id="8a982-162">選取 [**建立新網站**]。</span><span class="sxs-lookup"><span data-stu-id="8a982-162">Select **Create a new site**.</span></span>

<span data-ttu-id="8a982-163">如果您將專案命名為**WebPagesMovies**，您網站的預設名稱將會是**webpagesmovies.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="8a982-163">If you named your project **WebPagesMovies**, the default name for your site will be **webpagesmovies.azurewebsites.net**.</span></span> <span data-ttu-id="8a982-164">此預設名稱很可能無法使用，如紅色驚嘆號所示。</span><span class="sxs-lookup"><span data-stu-id="8a982-164">This default name is most likely not available, as indicated by the red exclamation mark.</span></span>

![預設的網站名稱](publishing/_static/image5.png)

<span data-ttu-id="8a982-166">將網站名稱變更為可用的專案，然後選取靠近您的位置的位置。</span><span class="sxs-lookup"><span data-stu-id="8a982-166">Change the site name to something that is available, and select a location that is close to your location.</span></span>

![變更的網站名稱](publishing/_static/image6.png)

<span data-ttu-id="8a982-168">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8a982-168">Click **OK**.</span></span>

<span data-ttu-id="8a982-169">WebMatrix 會 performss 測試以判斷伺服器是否與您的網站相容。</span><span class="sxs-lookup"><span data-stu-id="8a982-169">WebMatrix performss a test to determine if the server is compatible with your site.</span></span>

![相容性測試](publishing/_static/image7.png)

<span data-ttu-id="8a982-171">選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="8a982-171">Select **Continue**.</span></span>

<span data-ttu-id="8a982-172">即會顯示相容性測試的結果。</span><span class="sxs-lookup"><span data-stu-id="8a982-172">The results of the compatibility test are displayed.</span></span>

![相容性結果](publishing/_static/image8.png)

<span data-ttu-id="8a982-174">選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="8a982-174">Select **Continue**.</span></span>

<span data-ttu-id="8a982-175">WebMatrix 會顯示要發佈至網站的檔案和資料庫。</span><span class="sxs-lookup"><span data-stu-id="8a982-175">WebMatrix displays the files and databases that will be published to the site.</span></span> <span data-ttu-id="8a982-176">由於這是您第一次發佈網站，因此會列出所有檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-176">Since this is the first time you are publishing the site, all of the files are listed.</span></span> <span data-ttu-id="8a982-177">您可以取消選取尚未準備好要發行的檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-177">You can uncheck a file that is not ready to be published.</span></span> <span data-ttu-id="8a982-178">在後續的發行集中，只會顯示已變更的檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-178">In the subsequent publications, only the files that have changed will be displayed.</span></span> <span data-ttu-id="8a982-179">請參閱[更新即時網站：重新發佈](#update)。</span><span class="sxs-lookup"><span data-stu-id="8a982-179">See [Updating the Live Site: Republishing](#update).</span></span>

![publish preview](publishing/_static/image9.png)

<span data-ttu-id="8a982-181">選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="8a982-181">Select **Continue**.</span></span>

<span data-ttu-id="8a982-182">網站部署至 Azure 之後，會顯示一則訊息，指出部署已完成。</span><span class="sxs-lookup"><span data-stu-id="8a982-182">After the site has been deployed to Azure, a message is displayed that indicates the deployment has completed.</span></span>

![publish complete](publishing/_static/image10.png)

<span data-ttu-id="8a982-184">您的網站和資料庫已發佈至 Azure，且現已開放給公眾使用。</span><span class="sxs-lookup"><span data-stu-id="8a982-184">Your site and database have been published to Azure, and are now available to the public.</span></span> <span data-ttu-id="8a982-185">按一下指出發行已完成的訊息中的連結，您現在會看到已部署的網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-185">Click the link in the message indicating publishing has completed, and you will now see your deployed site.</span></span> <span data-ttu-id="8a982-186">您或具有網際網路存取權的任何人都可以新增或修改資料庫中的記錄。</span><span class="sxs-lookup"><span data-stu-id="8a982-186">You or anyone with Internet access can add or modify records in the database.</span></span>

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a><span data-ttu-id="8a982-187">將您的網站發佈至虛擬主機公司</span><span class="sxs-lookup"><span data-stu-id="8a982-187">Publishing Your Site to a Web Hosting Company</span></span>

<span data-ttu-id="8a982-188">如果您決定不要發佈至 Azure，您可以改為將您的網站發佈至虛擬主機公司。</span><span class="sxs-lookup"><span data-stu-id="8a982-188">If you decide to not publish to Azure, you can instead publish your site to a web hosting company.</span></span>

<span data-ttu-id="8a982-189">按一下 [**尋找 web 裝載**] 連結。</span><span class="sxs-lookup"><span data-stu-id="8a982-189">Click the **Find web hosting** link.</span></span>

![[發行設定] 對話方塊中的 [尋找 web 裝載] 按鈕](publishing/_static/image12.png)

<span data-ttu-id="8a982-191">您會前往 Microsoft 網站上的頁面，其中列出支援 ASP.NET 的主控提供者。</span><span class="sxs-lookup"><span data-stu-id="8a982-191">You go to a page on the Microsoft site that lists hosting providers that support ASP.NET.</span></span>

![列出主控提供者的 Microsoft 網站頁面](publishing/_static/image13.png)

<span data-ttu-id="8a982-193">很明顯地，現在可能很難以得知您長期所需要的裝載功能。</span><span class="sxs-lookup"><span data-stu-id="8a982-193">Obviously, it can be difficult to know now exactly what hosting features you might require over the long term.</span></span> <span data-ttu-id="8a982-194">以下是幾個要考慮的事項：</span><span class="sxs-lookup"><span data-stu-id="8a982-194">Here are a couple of things to consider:</span></span>

- <span data-ttu-id="8a982-195">基於 WebPagesMovies 網站的目的，您不需要有個別的 SQL Server 附加元件，這通常會產生額外的成本。</span><span class="sxs-lookup"><span data-stu-id="8a982-195">For purposes of the WebPagesMovies site, you don't have to have a separate add-on for SQL Server, which often costs extra.</span></span> <span data-ttu-id="8a982-196">在您的網站中，您使用的是獨立的 SQL Server Compact Edition。</span><span class="sxs-lookup"><span data-stu-id="8a982-196">In your site, you're using SQL Server Compact Edition, which is self-contained.</span></span> <span data-ttu-id="8a982-197">不過，您可能需要 SQL Server 存取權，才能進行某些未來的網站工作。</span><span class="sxs-lookup"><span data-stu-id="8a982-197">However, you might need SQL Server access for some future website work you do.</span></span> <span data-ttu-id="8a982-198">如果您認為可能的話，請確定您可以在稍後新增 SQL Server 功能。</span><span class="sxs-lookup"><span data-stu-id="8a982-198">If you think you might, make sure that you can add SQL Server capability later.</span></span>
- <span data-ttu-id="8a982-199">檢查主控提供者是否支援 Web Deploy 發佈通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8a982-199">Check whether the hosting provider supports the Web Deploy publishing protocol.</span></span> <span data-ttu-id="8a982-200">您可以使用 FTP 通訊協定來發行，但使用 Web Deploy 會比較方便。</span><span class="sxs-lookup"><span data-stu-id="8a982-200">You can publish by using FTP protocol, but it's more convenient to use Web Deploy.</span></span>

<span data-ttu-id="8a982-201">有些網站提供免費的試用期限。</span><span class="sxs-lookup"><span data-stu-id="8a982-201">Some sites offer a free trial period.</span></span> <span data-ttu-id="8a982-202">當您仍在試驗 WebMatrix 和 ASP.NET Web Pages 時，免費試用是嘗試發佈和裝載的好方法。</span><span class="sxs-lookup"><span data-stu-id="8a982-202">A free trial is a good way to try publishing and hosting while you're still experimenting with WebMatrix and ASP.NET Web Pages.</span></span>

<span data-ttu-id="8a982-203">挑選您想要的一個。</span><span class="sxs-lookup"><span data-stu-id="8a982-203">Pick one that you like.</span></span> <span data-ttu-id="8a982-204">在本教學課程中，我們選取了 [DiscountASP.NET]，因為我們在建立教學課程時，該公司已有促銷活動，可讓人們免費裝載網站數個月。</span><span class="sxs-lookup"><span data-stu-id="8a982-204">For this tutorial, we selected DiscountASP.NET, because while we were creating the tutorial, that company had a promotion that let people host a site free for a few months.</span></span>

> [!NOTE]
> <span data-ttu-id="8a982-205">我們在本教學課程中選擇的主機服務提供者，不應被視為該公司對其他人的背書。</span><span class="sxs-lookup"><span data-stu-id="8a982-205">Our choice of a hosting provider for this tutorial shouldn't be interpreted as an endorsement of that company over any other.</span></span> <span data-ttu-id="8a982-206">但我們必須挑選一個來說明，而 DiscountASP.NET 是支援 ASP.NET Web Pages 的眾多公司，以及用於發佈的 Web Deploy 通訊協定之一。</span><span class="sxs-lookup"><span data-stu-id="8a982-206">But we had to pick one for illustration, and DiscountASP.NET is one of the many companies that supports ASP.NET Web Pages and the Web Deploy protocol for publishing.</span></span>

<span data-ttu-id="8a982-207">一般而言，在您註冊主控提供者之後，公司會傳送電子郵件給您，其中包含使用者名稱和密碼、網頁伺服器的 URL 等等。</span><span class="sxs-lookup"><span data-stu-id="8a982-207">Typically, after you've signed up with the hosting provider, the company sends you an email that contains a user name and password, the URL of the web server, and so on.</span></span> <span data-ttu-id="8a982-208">如果主控公司支援 Web Deploy 通訊協定，他們可能會將包含發佈設定的檔案傳送給您，或讓您下載一個檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-208">If the hosting company supports Web Deploy protocol, they might send you a file that contains publish settings, or let you download one.</span></span> <span data-ttu-id="8a982-209">發行設定檔案可簡化您的程式。</span><span class="sxs-lookup"><span data-stu-id="8a982-209">A publish settings file simplifies the process for you.</span></span>

<span data-ttu-id="8a982-210">當您已註冊並準備好發佈時，請按一下 [WebMatrix] 功能區中的 [**發佈**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a982-210">When you've signed up and are ready to publish, click the **Publish** button in the WebMatrix ribbon.</span></span> <span data-ttu-id="8a982-211">[**發行設定**] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="8a982-211">The **Publish Settings** dialog box is displayed.</span></span>

<span data-ttu-id="8a982-212">如果主機服務提供者將發佈設定檔案傳送給您，請按一下 [匯**入發行設定**] 連結並匯入檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-212">If the hosting provider sent you a publish settings file, click the **Import publish settings** link and import the file.</span></span> <span data-ttu-id="8a982-213">如果您沒有發佈設定檔案，請使用主控公司在電子郵件中傳送給您的值來填入欄位。</span><span class="sxs-lookup"><span data-stu-id="8a982-213">If you don't have a publish settings file, fill in the fields by using the values that the hosting company sent you in email.</span></span> <span data-ttu-id="8a982-214">當您完成時，[**發行設定**] 對話方塊看起來可能會像這樣：</span><span class="sxs-lookup"><span data-stu-id="8a982-214">Here's what the **Publish Settings** dialog box might look like when you're done:</span></span>

![在 [發行設定] 對話方塊中填入的發行設定](publishing/_static/image14.png)

<span data-ttu-id="8a982-216">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="8a982-216">Click **Validate Connection**.</span></span> <span data-ttu-id="8a982-217">如果一切都沒問題，對話方塊會報告 [已**成功連線**]，這表示它可以與主控提供者的伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="8a982-217">If everything is ok, the dialog box reports **Connected successfully**, which means it can communicate with the hosting provider's server.</span></span>

![如果發行設定正確，則為成功訊息](publishing/_static/image15.png)

<span data-ttu-id="8a982-219">如果發生問題，WebMatrix 會盡力告訴您問題的原因：</span><span class="sxs-lookup"><span data-stu-id="8a982-219">If there's a problem, WebMatrix does its best to tell you what the problem is:</span></span>

![如果發行設定發生問題，則會出現錯誤訊息](publishing/_static/image16.png)

<span data-ttu-id="8a982-221">按一下 [Save] \*\*\*\* 儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="8a982-221">Click **Save** to save your settings.</span></span> <span data-ttu-id="8a982-222">WebMatrix 提供來執行測試，以確保它可以與主控網站正確通訊：</span><span class="sxs-lookup"><span data-stu-id="8a982-222">WebMatrix offers to perform a test to make sure that it can communicate correctly with the hosting site:</span></span>

![用來執行發佈程式測試的訊息供應專案](publishing/_static/image17.png)

<span data-ttu-id="8a982-224">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="8a982-224">Click **Yes**.</span></span> <span data-ttu-id="8a982-225">WebMatrix 將一些範例檔案上傳到主控提供者。</span><span class="sxs-lookup"><span data-stu-id="8a982-225">WebMatrix uploads some sample files to the hosting provider.</span></span> <span data-ttu-id="8a982-226">當相容性測試完成時，WebMatrix 會報告結果：</span><span class="sxs-lookup"><span data-stu-id="8a982-226">When the compatibility test is done, WebMatrix reports the results:</span></span>

![發佈測試的結果](publishing/_static/image18.png)

<span data-ttu-id="8a982-228">如果您已經準備好開始進行，請繼續進行，然後按一下 [**繼續**] 來啟動實際的發佈程式。</span><span class="sxs-lookup"><span data-stu-id="8a982-228">If you're ready to go, go ahead and click **Continue** to start the publish process for real.</span></span> <span data-ttu-id="8a982-229">WebMatrix 會找出您的網站中已有哪些檔案，而且已經在主機伺服器上（現在就是無），並提供您發佈程式的預覽：</span><span class="sxs-lookup"><span data-stu-id="8a982-229">WebMatrix figures out what files are in your site and are already on the host server (right now, none) and gives you a preview of the publish process:</span></span>

![預覽發佈程式將要上傳的檔案](publishing/_static/image19.png)

<span data-ttu-id="8a982-231">要發佈的檔案清單包含您建立的網頁，如 [*電影*]。</span><span class="sxs-lookup"><span data-stu-id="8a982-231">The list of files to publish includes the web pages that you've created like *Movies.cshtml*.</span></span> <span data-ttu-id="8a982-232">此清單也包含您已安裝之協助程式的檔案、要針對您的資料庫 SQL Server Compact 版本執行的檔案等等。</span><span class="sxs-lookup"><span data-stu-id="8a982-232">The list also includes files for helpers that you've installed, the files to run SQL Server Compact Edition for your database, and so on.</span></span> <span data-ttu-id="8a982-233">因此，初始發佈程式可能很可觀。</span><span class="sxs-lookup"><span data-stu-id="8a982-233">As a result, the initial publish process can be substantial.</span></span>

<span data-ttu-id="8a982-234">按一下 **[繼續]** 。</span><span class="sxs-lookup"><span data-stu-id="8a982-234">Click **Continue**.</span></span> <span data-ttu-id="8a982-235">WebMatrix 會將您的檔案複製到主控提供者的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8a982-235">WebMatrix copies your files to the hosting provider's server.</span></span> <span data-ttu-id="8a982-236">完成時，會在狀態列中報告結果：</span><span class="sxs-lookup"><span data-stu-id="8a982-236">When it's done, the results are reported in the status bar:</span></span>

![當發行程式成功完成時的狀態列訊息](publishing/_static/image20.png)

<span data-ttu-id="8a982-238">若要查看您的即時網站，請按一下狀態列中的連結。</span><span class="sxs-lookup"><span data-stu-id="8a982-238">To see your live site, click the link in the status bar.</span></span> <span data-ttu-id="8a982-239">將*電影*新增至 URL，您會看到您所建立的*電影. cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="8a982-239">Add *Movies* to the URL, and you'll see the *Movies.cshtml* file that you created:</span></span>

![顯示 [電影] 頁面的即時網站](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a><span data-ttu-id="8a982-241">更新即時網站：重新發佈</span><span class="sxs-lookup"><span data-stu-id="8a982-241">Updating the Live Site: Republishing</span></span>

<span data-ttu-id="8a982-242">一旦您發佈網站（至 Azure 或虛擬主機公司）之後，您的電腦上會有兩個版本， &mdash; 以及服務提供者上的版本。</span><span class="sxs-lookup"><span data-stu-id="8a982-242">Once you've published your site (to either Azure or a web hosting company), there are two copies of it &mdash; the version on your computer and the version on the service provider.</span></span> <span data-ttu-id="8a982-243">您可能會想要繼續開發網站（如果沒有其他，則是下一個教學課程集的一部分）。</span><span class="sxs-lookup"><span data-stu-id="8a982-243">You'll probably want to continue developing the site (if nothing else, as part of the next tutorial set).</span></span> <span data-ttu-id="8a982-244">當您這麼做時，必須重新發佈網站，才能將變更從電腦複製到服務提供者。</span><span class="sxs-lookup"><span data-stu-id="8a982-244">When you do, you have to republish your site in order to copy changes from your computer to the service provider.</span></span> <span data-ttu-id="8a982-245">WebMatrix 中的發佈程式可判斷您的網站上有哪些檔案已變更，並只發行那些檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-245">The publish process in WebMatrix can determine what files have changed on your site and publish just those files.</span></span>

<span data-ttu-id="8a982-246">若要查看重新發行的運作方式，請開啟 [*電影*] 網站，進行一些小變更，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-246">To see how republishing works, open the *Movies.cshtml* site, make some small change, and then save the file.</span></span> <span data-ttu-id="8a982-247">例如，將標題變更為 `Movies - Updated` 。</span><span class="sxs-lookup"><span data-stu-id="8a982-247">For example, change the title to `Movies - Updated`.</span></span>

<span data-ttu-id="8a982-248">按一下功能區中的 [**發佈**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a982-248">Click the **Publish** button in the ribbon.</span></span> <span data-ttu-id="8a982-249">WebMatrix 會決定已變更的內容，並顯示其將發佈之檔案的預覽。</span><span class="sxs-lookup"><span data-stu-id="8a982-249">WebMatrix determines what's changed and shows you a preview of the files it will publish.</span></span>

![[發行] 對話方塊顯示已變更的檔案準備好重新發行](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> <span data-ttu-id="8a982-251">根據預設，WebMatrix 只會在您第一次發行網站時發行您的資料庫（*.sdf*檔案）。</span><span class="sxs-lookup"><span data-stu-id="8a982-251">By default, WebMatrix publishes your database (*.sdf* file) only the first time you publish the site.</span></span> <span data-ttu-id="8a982-252">一旦您的網站發佈，而人們與網站互動之後，即時網站上的資料庫通常會有網站的實際資料。</span><span class="sxs-lookup"><span data-stu-id="8a982-252">Once your site is published and people are interacting with the website, the database on the live site typically has the site's real data.</span></span> <span data-ttu-id="8a982-253">您必須小心不要使用電腦上的 *.sdf*檔案來覆寫即時資料庫，這通常只包含測試資料。</span><span class="sxs-lookup"><span data-stu-id="8a982-253">You have to be very careful not to overwrite the live database with the *.sdf* file that's on your computer, which usually contains only test data.</span></span> <span data-ttu-id="8a982-254">這就是為什麼您會看到警告**發佈會覆寫任何遠端資料庫**，以及為什麼預設會清除*WebPagesMovies*的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="8a982-254">That's why you see the warning **Publishing will overwrite any remote databases**, and why the check box for *WebPagesMovies.sdf* is cleared by default.</span></span>

<span data-ttu-id="8a982-255">按一下 **[繼續]** 。</span><span class="sxs-lookup"><span data-stu-id="8a982-255">Click **Continue**.</span></span> <span data-ttu-id="8a982-256">WebMatrix 會發佈變更的檔案，並顯示成功的訊息，就像您第一次發佈一樣。</span><span class="sxs-lookup"><span data-stu-id="8a982-256">WebMatrix publishes the changed files and shows you a success message, like it did the first time you published.</span></span>

<span data-ttu-id="8a982-257">前往即時網站（如果仍顯示，您可以按一下成功訊息中的連結），並確認您的變更已發佈。</span><span class="sxs-lookup"><span data-stu-id="8a982-257">Go to the live site (you can click the link in the success message if it's still showing) and verify that your change has been published.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="8a982-258">**從遠端編輯檔案**</span><span class="sxs-lookup"><span data-stu-id="8a982-258">**Editing Files Remotely**</span></span>
> 
> <span data-ttu-id="8a982-259">除了變更您的網站再重新發行以外，您也可以直接在 WebMatrix 中編輯遠端檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-259">As an alternative to changing your site and then republishing, you can edit remote files directly in WebMatrix.</span></span> <span data-ttu-id="8a982-260">在此案例中，您會開啟服務提供者上的檔案，而 WebMatrix 會下載該檔案的複本供您編輯。</span><span class="sxs-lookup"><span data-stu-id="8a982-260">In this scenario, you open a file that's on the service provider, and WebMatrix downloads a copy of it for you to edit.</span></span> <span data-ttu-id="8a982-261">每次您儲存檔案時，WebMatrix 都會將變更傳送至網站。</span><span class="sxs-lookup"><span data-stu-id="8a982-261">Every time you save the file, WebMatrix sends the changes to the site.</span></span>
> 
> <span data-ttu-id="8a982-262">遠端編輯是對您的即時網站進行變更的簡單方式。</span><span class="sxs-lookup"><span data-stu-id="8a982-262">Remote editing is an easy way to make changes to your live site.</span></span> <span data-ttu-id="8a982-263">不過，您以這種方式進行的變更不會與本機網站中的檔案同步處理。</span><span class="sxs-lookup"><span data-stu-id="8a982-263">However, the changes you make this way aren't synchronized with the files in your local site.</span></span> <span data-ttu-id="8a982-264">若要將本機檔案與遠端網站同步處理，您可以下載遠端檔案。</span><span class="sxs-lookup"><span data-stu-id="8a982-264">To synchronize the local files with the remote site, you can download the remote files.</span></span> <span data-ttu-id="8a982-265">此程式的運作方式非常類似發行，但相反。</span><span class="sxs-lookup"><span data-stu-id="8a982-265">This process works much like publishing, except in reverse.</span></span>
> 
> <span data-ttu-id="8a982-266">我們不會在這裡詳細說明 WebMatrix 的遠端編輯和遠端下載功能。</span><span class="sxs-lookup"><span data-stu-id="8a982-266">We won't describe more about the remote-editing and remote-download facilities of WebMatrix here.</span></span> <span data-ttu-id="8a982-267">如果多人必須在不同電腦上的相同網站上工作，它們就很有用。</span><span class="sxs-lookup"><span data-stu-id="8a982-267">They're quite useful if multiple people have to work on the same site on different computers.</span></span> <span data-ttu-id="8a982-268">如需詳細資訊，請參閱[使用 WebMatrix 2 Beta 發佈和編輯遠端網站](https://go.microsoft.com/fwlink/?LinkId=251591)。</span><span class="sxs-lookup"><span data-stu-id="8a982-268">For more information, see [Publish and Edit a Remote Site with WebMatrix 2 Beta](https://go.microsoft.com/fwlink/?LinkId=251591).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a982-269">其他資源</span><span class="sxs-lookup"><span data-stu-id="8a982-269">Additional Resources</span></span>

- <span data-ttu-id="8a982-270">[ASP.NET WebMatrix ASP.NET Web Pages 論壇](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)，這是張貼問題和獲得解答的絕佳地方。</span><span class="sxs-lookup"><span data-stu-id="8a982-270">[ASP.NET WebMatrix ASP.NET Web Pages forum](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), a great place to post questions and get answers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8a982-271">上一步</span><span class="sxs-lookup"><span data-stu-id="8a982-271">Previous</span></span>](layouts.md)
