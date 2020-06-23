---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 開始使用 | Microsoft Docs
author: Rick-Anderson
description: 不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。 使用 Visual Studio 或 Visual Studio Code。 本指導方針 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240752"
---
# <a name="getting-started"></a><span data-ttu-id="4a65d-105">開始使用</span><span class="sxs-lookup"><span data-stu-id="4a65d-105">Getting Started</span></span>

<span data-ttu-id="4a65d-106"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4a65d-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="4a65d-107">不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="4a65d-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="4a65d-108">使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="4a65d-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="4a65d-109">本指引和應用程式可讓您大致瞭解 ASP.NET Web Pages （第2版或更新版本）和 Razor 語法，這是建立動態網站的輕量架構。</span><span class="sxs-lookup"><span data-stu-id="4a65d-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="4a65d-110">它也引進了 WebMatrix，這是用來建立頁面和網站的工具。</span><span class="sxs-lookup"><span data-stu-id="4a65d-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="4a65d-111">**層級**： ASP.NET Web Pages 的新。</span><span class="sxs-lookup"><span data-stu-id="4a65d-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="4a65d-112">**假設的技能**： HTML、基本級聯樣式表（CSS）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="4a65d-113">您將在第一組教學課程中瞭解的內容：</span><span class="sxs-lookup"><span data-stu-id="4a65d-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="4a65d-114">什麼是 ASP.NET Web Pages 技術及其用途。</span><span class="sxs-lookup"><span data-stu-id="4a65d-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="4a65d-115">WebMatrix 是什麼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="4a65d-116">如何安裝所有專案。</span><span class="sxs-lookup"><span data-stu-id="4a65d-116">How to install everything.</span></span>
> - <span data-ttu-id="4a65d-117">如何使用 WebMatrix 建立網站。</span><span class="sxs-lookup"><span data-stu-id="4a65d-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="4a65d-118">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="4a65d-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="4a65d-119">Microsoft Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="4a65d-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="4a65d-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="4a65d-120">WebMatrix.</span></span>
> - <span data-ttu-id="4a65d-121">*cshtml*頁面</span><span class="sxs-lookup"><span data-stu-id="4a65d-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="4a65d-122">Mike Pope 原本寫了本教學課程。</span><span class="sxs-lookup"><span data-stu-id="4a65d-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="4a65d-123">Tom FitzMacken 已針對 Microsoft WebMatrix 3 進行更新。</span><span class="sxs-lookup"><span data-stu-id="4a65d-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4a65d-124">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="4a65d-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4a65d-125">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="4a65d-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="4a65d-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="4a65d-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="4a65d-127">您應該知道什麼？</span><span class="sxs-lookup"><span data-stu-id="4a65d-127">What Should You Know?</span></span>

<span data-ttu-id="4a65d-128">我們假設您已經熟悉：</span><span class="sxs-lookup"><span data-stu-id="4a65d-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="4a65d-129">**HTML**。</span><span class="sxs-lookup"><span data-stu-id="4a65d-129">**HTML**.</span></span> <span data-ttu-id="4a65d-130">不需要深入的專業知識。</span><span class="sxs-lookup"><span data-stu-id="4a65d-130">No in-depth expertise is required.</span></span> <span data-ttu-id="4a65d-131">我們不會說明 HTML，但我們也不會使用任何複雜的專案。</span><span class="sxs-lookup"><span data-stu-id="4a65d-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="4a65d-132">我們會提供 HTML 教學課程的連結，我們認為這些是有用的。</span><span class="sxs-lookup"><span data-stu-id="4a65d-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="4a65d-133">**級聯樣式表（CSS）**。</span><span class="sxs-lookup"><span data-stu-id="4a65d-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="4a65d-134">與 HTML 相同。</span><span class="sxs-lookup"><span data-stu-id="4a65d-134">Same as with HTML.</span></span>
- <span data-ttu-id="4a65d-135">**基本資料庫的想法**。</span><span class="sxs-lookup"><span data-stu-id="4a65d-135">**Basic database ideas**.</span></span> <span data-ttu-id="4a65d-136">如果您使用試算表來儲存資料，並將資料排序和篩選，這就是我們通常會在本教學課程中假設的專業知識層級。</span><span class="sxs-lookup"><span data-stu-id="4a65d-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="4a65d-137">我們也假設您有興趣學習基本程式設計。</span><span class="sxs-lookup"><span data-stu-id="4a65d-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="4a65d-138">ASP.NET Web Pages 使用稱為 c # 的程式設計語言。</span><span class="sxs-lookup"><span data-stu-id="4a65d-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="4a65d-139">您不需要在程式設計中擁有任何背景，只是其中的重點。</span><span class="sxs-lookup"><span data-stu-id="4a65d-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="4a65d-140">如果您之前曾在網頁中撰寫過任何 JavaScript，就有許多背景。</span><span class="sxs-lookup"><span data-stu-id="4a65d-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="4a65d-141">請注意，如果您熟悉程式設計，您可能會發現，本教學課程最初的設定速度會變慢，而我們會讓新的程式開發人員加快速度。</span><span class="sxs-lookup"><span data-stu-id="4a65d-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="4a65d-142">不過，我們在過去的幾個教學課程中，將會有較少的基本程式設計，而且會以更快速的剪輯來移動專案。</span><span class="sxs-lookup"><span data-stu-id="4a65d-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="4a65d-143">您需要什麼？</span><span class="sxs-lookup"><span data-stu-id="4a65d-143">What Do You Need?</span></span>

<span data-ttu-id="4a65d-144">以下是您需要的內容：</span><span class="sxs-lookup"><span data-stu-id="4a65d-144">Here's what you'll need:</span></span>

- <span data-ttu-id="4a65d-145">執行 Windows 8、Windows 7、Windows Server 2008 或 Windows Server 2012 的電腦。</span><span class="sxs-lookup"><span data-stu-id="4a65d-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="4a65d-146">即時網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="4a65d-146">A live internet connection.</span></span>
- <span data-ttu-id="4a65d-147">系統管理員許可權（安裝程式所需）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="4a65d-148">什麼是 ASP.NET Web Pages？</span><span class="sxs-lookup"><span data-stu-id="4a65d-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="4a65d-149">ASP.NET Web Pages 是一種架構，可讓您用來建立動態網頁。</span><span class="sxs-lookup"><span data-stu-id="4a65d-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="4a65d-150">簡單的 HTML 網頁是靜態的;其內容取決於頁面中的固定 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="4a65d-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="4a65d-151">像您使用 ASP.NET Web Pages 建立的動態頁面，可讓您使用程式碼，即時建立網頁內容。</span><span class="sxs-lookup"><span data-stu-id="4a65d-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="4a65d-152">動態頁面可讓您執行各種動作。</span><span class="sxs-lookup"><span data-stu-id="4a65d-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="4a65d-153">您可以使用表單來要求使用者輸入，然後變更頁面所顯示的內容或外觀。</span><span class="sxs-lookup"><span data-stu-id="4a65d-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="4a65d-154">您可以從使用者中取出資訊，將它儲存在資料庫中，然後稍後再列出。</span><span class="sxs-lookup"><span data-stu-id="4a65d-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="4a65d-155">您可以從您的網站傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="4a65d-155">You can send email from your site.</span></span> <span data-ttu-id="4a65d-156">您可以與網路上的其他服務（例如，對應服務）互動，並產生可整合來自這些來源之資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="4a65d-157">什麼是 WebMatrix？</span><span class="sxs-lookup"><span data-stu-id="4a65d-157">What is WebMatrix?</span></span>

<span data-ttu-id="4a65d-158">WebMatrix 是一種工具，可整合網頁編輯器、資料庫公用程式、測試頁面的 web 伺服器，以及將您的網站發佈至網際網路的功能。</span><span class="sxs-lookup"><span data-stu-id="4a65d-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="4a65d-159">WebMatrix 是免費的，而且容易安裝且便於使用。</span><span class="sxs-lookup"><span data-stu-id="4a65d-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="4a65d-160">（它也適用于純 HTML 網頁，以及其他像是 PHP 的技術）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="4a65d-161">您實際上不*需要*使用 WebMatrix 來處理 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="4a65d-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="4a65d-162">例如，您可以使用文字編輯器來建立頁面，並使用您可以存取的網頁伺服器來測試頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="4a65d-163">不過，WebMatrix 讓它變得非常簡單，因此這些教學課程會在整個過程中使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4a65d-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="4a65d-164">關於這些教學課程</span><span class="sxs-lookup"><span data-stu-id="4a65d-164">About These Tutorials</span></span>

<span data-ttu-id="4a65d-165">本教學課程集是如何使用 ASP.NET Web Pages 的簡介。</span><span class="sxs-lookup"><span data-stu-id="4a65d-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="4a65d-166">本簡介教學課程集中有9個教學課程總計。</span><span class="sxs-lookup"><span data-stu-id="4a65d-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="4a65d-167">它是一系列教學課程集合的一部分，可讓您從 ASP.NET Web Pages 新手，建立真正、專業型式的網站。</span><span class="sxs-lookup"><span data-stu-id="4a65d-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="4a65d-168">第一個教學課程設定著重于說明如何使用 ASP.NET Web Pages 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="4a65d-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="4a65d-169">當您完成時，您可以使用其他教學課程集合，以取得此端點的結尾，並深入探索網頁。</span><span class="sxs-lookup"><span data-stu-id="4a65d-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="4a65d-170">我們刻意開始簡單的說明。</span><span class="sxs-lookup"><span data-stu-id="4a65d-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="4a65d-171">當我們顯示某個專案時，在本教學課程中設定我們一定會選擇最容易瞭解的方式。</span><span class="sxs-lookup"><span data-stu-id="4a65d-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="4a65d-172">稍後的教學課程集會更深入探討，並顯示更有效率或更有彈性的方法（也更有趣）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="4a65d-173">但這些教學課程需要您先瞭解基本概念。</span><span class="sxs-lookup"><span data-stu-id="4a65d-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="4a65d-174">您剛開始的教學課程集涵蓋了 ASP.NET Web Pages 的下列功能：</span><span class="sxs-lookup"><span data-stu-id="4a65d-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="4a65d-175">簡介並讓所有專案都已安裝。</span><span class="sxs-lookup"><span data-stu-id="4a65d-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="4a65d-176">（這是在您所閱讀的教學課程中）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="4a65d-177">ASP.NET Web Pages 程式設計的基本概念。</span><span class="sxs-lookup"><span data-stu-id="4a65d-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="4a65d-178">建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="4a65d-178">Creating a database.</span></span>
- <span data-ttu-id="4a65d-179">建立和處理使用者輸入表單。</span><span class="sxs-lookup"><span data-stu-id="4a65d-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="4a65d-180">加入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="4a65d-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="4a65d-181">您會建立什麼？</span><span class="sxs-lookup"><span data-stu-id="4a65d-181">What Will You Create?</span></span>

<span data-ttu-id="4a65d-182">本教學課程的設定和後續工作會在網站上進行，您可以在其中列出您喜歡的電影。</span><span class="sxs-lookup"><span data-stu-id="4a65d-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="4a65d-183">您將能夠輸入電影、加以編輯並列出它們。</span><span class="sxs-lookup"><span data-stu-id="4a65d-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="4a65d-184">以下是您將在本教學課程中建立的幾個頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="4a65d-185">第一個範例會顯示您將建立的電影清單頁面：</span><span class="sxs-lookup"><span data-stu-id="4a65d-185">The first one shows the movie listing page that you'll create:</span></span>

![顯示電影清單的完成電影應用程式](getting-started/_static/image1.png)

<span data-ttu-id="4a65d-187">以下是可讓您將新電影資訊新增至網站的頁面：</span><span class="sxs-lookup"><span data-stu-id="4a65d-187">And here's the page that lets you add new movie information to your site:</span></span>

![顯示 [新增電影] 頁面的已完成電影應用程式](getting-started/_static/image2.png)

<span data-ttu-id="4a65d-189">後續的教學課程會在此集合上設定組建，並新增更多功能，例如上傳圖片、讓使用者登入、傳送電子郵件，以及與社交媒體整合。</span><span class="sxs-lookup"><span data-stu-id="4a65d-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="4a65d-190">請參閱此應用程式在 Azure 上執行</span><span class="sxs-lookup"><span data-stu-id="4a65d-190">See this App Running on Azure</span></span>

<span data-ttu-id="4a65d-191">您是否想要查看已完成的網站以即時 web 應用程式的形式執行？</span><span class="sxs-lookup"><span data-stu-id="4a65d-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="4a65d-192">只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a65d-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="4a65d-193">您需要 Azure 帳戶，才能將此解決方案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4a65d-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="4a65d-194">如果您還沒有帳戶，您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="4a65d-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="4a65d-195">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4a65d-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="4a65d-196">[啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="4a65d-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="4a65d-197">安裝所有專案</span><span class="sxs-lookup"><span data-stu-id="4a65d-197">Installing Everything</span></span>

<span data-ttu-id="4a65d-198">您可以使用 Microsoft 的 Web Platform Installer 來安裝所有專案。</span><span class="sxs-lookup"><span data-stu-id="4a65d-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="4a65d-199">實際上，您會安裝安裝程式，然後使用它來安裝其他專案。</span><span class="sxs-lookup"><span data-stu-id="4a65d-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="4a65d-200">若要使用網頁，您至少必須安裝 Windows XP 含 SP3，或 Windows Server 2008 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4a65d-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="4a65d-201">在 ASP.NET 網站的 [ [Web Pages] 頁面](../../../index.md)上，按一下 [**安裝**]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![顯示 [ &quot; 安裝 WebMatrix] 按鈕的 ASP.NET 網站 &quot;](getting-started/_static/image3.png)

<span data-ttu-id="4a65d-203">在安裝 WebMatrix 之前，系統會要求您接受授權條款和隱私權聲明。</span><span class="sxs-lookup"><span data-stu-id="4a65d-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![接受詞彙以開始安裝](getting-started/_static/image4.png)

<span data-ttu-id="4a65d-205">按一下 [**執行**] 開始安裝。</span><span class="sxs-lookup"><span data-stu-id="4a65d-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="4a65d-206">（如果您想要儲存安裝程式，請按一下 [**儲存**]，然後從儲存的資料夾執行安裝程式）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="4a65d-207">隨即顯示 Web Platform Installer，準備好安裝 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4a65d-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="4a65d-208">按一下 [Install] 。</span><span class="sxs-lookup"><span data-stu-id="4a65d-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="4a65d-209">安裝程式會找出它必須安裝在您電腦上的內容，並開始處理。</span><span class="sxs-lookup"><span data-stu-id="4a65d-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="4a65d-210">視必須安裝的內容而定，此程式可能需要數分鐘到數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4a65d-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="4a65d-211">選取 [**我接受**] 以接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="4a65d-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="4a65d-212">您好，WebMatrix</span><span class="sxs-lookup"><span data-stu-id="4a65d-212">Hello, WebMatrix</span></span>

<span data-ttu-id="4a65d-213">完成後，安裝程式就可以自動啟動 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4a65d-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="4a65d-214">如果沒有，請在 Windows 中，從 [**開始**] 功能表啟動**Microsoft WebMatrix**。</span><span class="sxs-lookup"><span data-stu-id="4a65d-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="4a65d-215">當您第一次啟動 WebMatrix 時，您有機會使用您的 Microsoft 帳戶登入 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="4a65d-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="4a65d-216">藉由登入，您將可透過 Azure 獲得10個免費的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a65d-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="4a65d-217">這些免費的 web 應用程式提供便利的方式來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a65d-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="4a65d-218">如果您還沒有 Azure 帳戶，但是有 MSDN 訂閱，則可以[啟用您的 msdn 訂閱權益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="4a65d-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="4a65d-219">否則，您只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a65d-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4a65d-220">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="4a65d-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

<span data-ttu-id="4a65d-221">您不需要立即登入，即可繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="4a65d-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="4a65d-222">如果您目前未登入，您仍然可以選擇稍後再登入。</span><span class="sxs-lookup"><span data-stu-id="4a65d-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="4a65d-223">本教學課程系列中的最後一個[主題](publishing.md)涵蓋如何將您的網站部署至 Azure;因此，您必須登入才能完成該主題。</span><span class="sxs-lookup"><span data-stu-id="4a65d-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="4a65d-224">此時，請使用您的 Microsoft 帳戶登入，或選取右下角的 [**不是現在**]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![Sign In](getting-started/_static/image7.png)

<span data-ttu-id="4a65d-226">首先，您將建立空白網站並新增頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="4a65d-227">在此集合稍後的教學課程中，您將會使用其中一個內建網站範本來播放。</span><span class="sxs-lookup"><span data-stu-id="4a65d-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="4a65d-228">在 [開始] 視窗中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-228">In the start window, click **New**.</span></span>

![WebMatrix 啟動畫面](getting-started/_static/image8.png)

<span data-ttu-id="4a65d-230">範本是針對不同類型的網站預先建立的檔案和頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="4a65d-231">若要查看預設可用的所有範本，請選取 [範本資源庫] 選項。</span><span class="sxs-lookup"><span data-stu-id="4a65d-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![選取範本庫](getting-started/_static/image9.png)

<span data-ttu-id="4a65d-233">在 [**快速入門**] 視窗中，從 [ **ASP.NET** ] 群組選取 [**空白網站**]，並將新網站命名為 "WebPagesMovies"。</span><span class="sxs-lookup"><span data-stu-id="4a65d-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![已選取空白網站範本的 WebMatrix [快速入門] 視窗](getting-started/_static/image10.png)

<span data-ttu-id="4a65d-235">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4a65d-235">Click **Next**.</span></span>

<span data-ttu-id="4a65d-236">如果您已登入 Microsoft 帳戶，系統會提供您在 Azure 上建立網站的機會。</span><span class="sxs-lookup"><span data-stu-id="4a65d-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="4a65d-237">根據您的網站名稱，建議**WebPagesMovies.azurewebsites.net**的預設名稱。不過，驚嘆號表示此名稱無法在 Windows Azure 上使用。</span><span class="sxs-lookup"><span data-stu-id="4a65d-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="4a65d-238">為求簡化，請選取 [**跳過**]，立即略過在 Azure 上建立網站。</span><span class="sxs-lookup"><span data-stu-id="4a65d-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="4a65d-239">稍後在此系列中，我們會將網站發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4a65d-239">Later in this series, we will publish the site to Azure.</span></span>

![建立 azure 網站](getting-started/_static/image11.png)

<span data-ttu-id="4a65d-241">WebMatrix 會建立並開啟網站：</span><span class="sxs-lookup"><span data-stu-id="4a65d-241">WebMatrix creates and opens the site:</span></span>

![在 WebMatrix 中開啟新的 WebPagesMovies 網站](getting-started/_static/image12.png)

<span data-ttu-id="4a65d-243">在頂端，有一個快速存取工具列和一個功能區。</span><span class="sxs-lookup"><span data-stu-id="4a65d-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="4a65d-244">在左下方，您會看到工作區選取**器，您**可以在其中切換工作（**網站**、檔案、**資料庫**、**報表**）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="4a65d-245">右邊是編輯器和報表的內容窗格。</span><span class="sxs-lookup"><span data-stu-id="4a65d-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="4a65d-246">而在底部，您偶爾會看到訊息的通知列。</span><span class="sxs-lookup"><span data-stu-id="4a65d-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="4a65d-247">當您完成這些教學課程時，您將會深入瞭解 WebMatrix 及其功能。</span><span class="sxs-lookup"><span data-stu-id="4a65d-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="4a65d-248">建立網頁</span><span class="sxs-lookup"><span data-stu-id="4a65d-248">Creating a Web Page</span></span>

<span data-ttu-id="4a65d-249">若要熟悉 WebMatrix 和 ASP.NET Web Pages，您將建立簡單的頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="4a65d-250">在工作區選取器中，選取 [檔案 **] 工作區**。</span><span class="sxs-lookup"><span data-stu-id="4a65d-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="4a65d-251">此工作區可讓您使用檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="4a65d-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="4a65d-252">左窗格會顯示您網站的檔案結構。</span><span class="sxs-lookup"><span data-stu-id="4a65d-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="4a65d-253">功能區會變更以顯示檔案相關的工作。</span><span class="sxs-lookup"><span data-stu-id="4a65d-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix 中的檔案工作區](getting-started/_static/image13.png)

<span data-ttu-id="4a65d-255">在功能區中，按一下 [**新增**] 底下的箭號，然後按一下 [**新增**檔案]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![使用 &quot; 功能區中的 [新增] &quot; 命令來建立新檔案](getting-started/_static/image14.png)

<span data-ttu-id="4a65d-257">WebMatrix 會顯示檔案類型的清單。</span><span class="sxs-lookup"><span data-stu-id="4a65d-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="4a65d-258">選取 [ **CSHTML**]，然後在 [**名稱**] 方塊中輸入 "HelloWorld"。</span><span class="sxs-lookup"><span data-stu-id="4a65d-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="4a65d-259">CSHTML 頁面是 ASP.NET Web Pages 頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![建立名為 HelloWorld 的新 CSHTML 頁面](getting-started/_static/image15.png)

<span data-ttu-id="4a65d-261">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-261">Click **OK**.</span></span>

<span data-ttu-id="4a65d-262">WebMatrix 會建立頁面，並在編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="4a65d-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 編輯器中的新 HelloWorld 頁面](getting-started/_static/image16.png)

<span data-ttu-id="4a65d-264">如您所見，此頁面大多包含一般的 HTML 標籤，但頂端的區塊除外，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4a65d-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="4a65d-265">這是為了新增程式碼，您很快就會看到。</span><span class="sxs-lookup"><span data-stu-id="4a65d-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="4a65d-266">請注意，頁面的不同部分（專案 &mdash; 名稱、屬性和文字，以及頂端的區塊）都是不同的色彩。</span><span class="sxs-lookup"><span data-stu-id="4a65d-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="4a65d-267">這稱為語法反白*顯示*，可讓您更輕鬆地保持所有專案的清晰。</span><span class="sxs-lookup"><span data-stu-id="4a65d-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="4a65d-268">它是可讓您在 WebMatrix 中輕鬆使用網頁的其中一項功能。</span><span class="sxs-lookup"><span data-stu-id="4a65d-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="4a65d-269">加入和元素的內容， `<head>` `<body>` 如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4a65d-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="4a65d-270">（如有需要，您可以只複製下列區塊，並將整個現有的頁面取代為此程式碼）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="4a65d-271">在 [快速存取] 工具列或 [檔案 **] 功能表中**，按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix 快速存取工具列中的 [儲存] 按鈕](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="4a65d-273">測試頁面</span><span class="sxs-lookup"><span data-stu-id="4a65d-273">Testing the Page</span></span>

<span data-ttu-id="4a65d-274">在 [檔案 **] 工作區**中，以滑鼠右鍵按一下 [ *HelloWorld* ] 頁面，然後按一下 [**在瀏覽器中啟動**]。</span><span class="sxs-lookup"><span data-stu-id="4a65d-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![使用 WebMatrix 功能區中的 [執行] 按鈕執行頁面](getting-started/_static/image18.png)

<span data-ttu-id="4a65d-276">WebMatrix 啟動內建的網頁伺服器（IIS Express），您可以用來測試電腦上的頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="4a65d-277">（不 IIS Express 在 WebMatrix 中，您必須先將頁面發佈到 web 伺服器，然後才能進行測試）。頁面會顯示在您的預設瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="4a65d-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;&quot;在瀏覽器中執行 Hello World 頁面](getting-started/_static/image19.png)

<span data-ttu-id="4a65d-279">請注意，當您在 WebMatrix 中測試頁面時，瀏覽器中的 URL 會是 `http://localhost:33651/HelloWorld.cshtml.` 名稱*localhost*參照本機伺服器，這表示網頁是由自己電腦上的網頁伺服器所提供。</span><span class="sxs-lookup"><span data-stu-id="4a65d-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="4a65d-280">如先前所述，WebMatrix 包含名為 IIS Express 的 web 伺服器程式，會在您啟動頁面時執行。</span><span class="sxs-lookup"><span data-stu-id="4a65d-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="4a65d-281">*Localhost*之後的數位（例如， *localhost： 33651*）會參考您電腦上的*埠號碼*。</span><span class="sxs-lookup"><span data-stu-id="4a65d-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="4a65d-282">這是 IIS Express 用於此特定網站的「通道」數目。</span><span class="sxs-lookup"><span data-stu-id="4a65d-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="4a65d-283">當您建立網站時，會從範圍1024到65536隨機選取埠號碼，而且您建立的每個網站都有不同的通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="4a65d-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="4a65d-284">（當您測試自己的網站時，埠號碼幾乎一定會與33561不同）。藉由對每個網站使用不同的埠，IIS Express 可以將其與您的網站進行直接的溝通。</span><span class="sxs-lookup"><span data-stu-id="4a65d-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="4a65d-285">稍後當您將網站發佈至公用 web 伺服器時，URL 中就不會再看到*localhost* 。</span><span class="sxs-lookup"><span data-stu-id="4a65d-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="4a65d-286">此時，您會看到較典型的 URL，例如 `http://myhostingsite/mywebsite/HelloWorld.cshtml` 或頁面是什麼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="4a65d-287">您稍後會在本教學課程系列中深入瞭解如何發佈網站。</span><span class="sxs-lookup"><span data-stu-id="4a65d-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="4a65d-288">新增一些伺服器端程式碼</span><span class="sxs-lookup"><span data-stu-id="4a65d-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="4a65d-289">關閉瀏覽器並返回 WebMatrix 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="4a65d-290">在程式碼區塊中新增一行，使其看起來像下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4a65d-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="4a65d-291">這有點 Razor 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="4a65d-292">這可能會清楚地取得目前的日期和時間，並將該值放入名為的*變數*中 `currentDateTime` 。</span><span class="sxs-lookup"><span data-stu-id="4a65d-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="4a65d-293">您將在下一個教學課程中深入瞭解 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="4a65d-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="4a65d-294">在頁面主體中，于 `<p>Hello World!</p>` 元素後面新增下列專案：</span><span class="sxs-lookup"><span data-stu-id="4a65d-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="4a65d-295">此程式碼會取得您放入 `currentDateTime` 變數頂端的值，並將它插入至頁面的標記中。</span><span class="sxs-lookup"><span data-stu-id="4a65d-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="4a65d-296">`@`字元會標示頁面中的 ASP.NET Web Pages 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="4a65d-297">再次執行頁面（WebMatrix 會在執行頁面之前為您儲存變更）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="4a65d-298">這次您會在頁面中看到日期和時間。</span><span class="sxs-lookup"><span data-stu-id="4a65d-298">This time you see the date and time in the page.</span></span>

![&quot;以 &quot; 動態方式產生的時間顯示，在瀏覽器中執行的 Hello World 頁面](getting-started/_static/image20.png)

<span data-ttu-id="4a65d-300">請稍候片刻，然後在瀏覽器中重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="4a65d-301">日期和時間顯示會更新。</span><span class="sxs-lookup"><span data-stu-id="4a65d-301">The date and time display is updated.</span></span>

<span data-ttu-id="4a65d-302">在瀏覽器中，查看頁面來源。</span><span class="sxs-lookup"><span data-stu-id="4a65d-302">In the browser, look at the page source.</span></span> <span data-ttu-id="4a65d-303">它看起來會像下面這樣的標記：</span><span class="sxs-lookup"><span data-stu-id="4a65d-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="4a65d-304">請注意， `@{ }` 頂端的區塊不存在。</span><span class="sxs-lookup"><span data-stu-id="4a65d-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="4a65d-305">另請注意，日期和時間顯示會顯示實際的字元字串（ `1/18/2012 2:49:50 PM` 或任何內容），而不 `@currentDateTime` 像您在*cshtml*頁面中的一樣。</span><span class="sxs-lookup"><span data-stu-id="4a65d-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="4a65d-306">這裡發生的情況是，當您執行頁面時，ASP.NET 已處理標記為的所有程式碼（在此案例中很少） `@` 。</span><span class="sxs-lookup"><span data-stu-id="4a65d-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="4a65d-307">程式碼會產生輸出，並將該輸出插入頁面中。</span><span class="sxs-lookup"><span data-stu-id="4a65d-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="4a65d-308">這就是 ASP.NET Web Pages 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="4a65d-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="4a65d-309">當您閱讀該 ASP.NET Web Pages 會產生動態 Web 內容時，您在這裡看到的就是這個概念。</span><span class="sxs-lookup"><span data-stu-id="4a65d-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="4a65d-310">您剛才建立的頁面包含您之前看到的相同 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="4a65d-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="4a65d-311">它也可以包含可執行各種工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="4a65d-312">在此範例中，它執行的是取得目前日期和時間的簡單工作。</span><span class="sxs-lookup"><span data-stu-id="4a65d-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="4a65d-313">如您所見，您可以使用 HTML 來散置程式碼，以在頁面中產生輸出。</span><span class="sxs-lookup"><span data-stu-id="4a65d-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="4a65d-314">當有人在瀏覽器中要求 [ *cshtml* ] 頁面時，ASP.NET 會在網頁伺服器仍在手中時處理該頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="4a65d-315">ASP.NET 會將程式碼的輸出（如果有的話）插入頁面中做為 HTML。</span><span class="sxs-lookup"><span data-stu-id="4a65d-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="4a65d-316">當程式碼處理完成時，ASP.NET 會將產生的頁面傳送到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4a65d-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="4a65d-317">所有瀏覽器都是 HTML。</span><span class="sxs-lookup"><span data-stu-id="4a65d-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="4a65d-318">圖表如下：</span><span class="sxs-lookup"><span data-stu-id="4a65d-318">Here's a diagram:</span></span>

![ASP.NET 如何動態產生 HTML 的概念流程](getting-started/_static/image21.png)

<span data-ttu-id="4a65d-320">概念很簡單，但程式碼可以執行許多有趣的工作，而且有很多有趣的方式可讓您將 HTML 內容動態新增至頁面。</span><span class="sxs-lookup"><span data-stu-id="4a65d-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="4a65d-321">而 ASP.NET *，* 如同任何 HTML 網頁，也可以包含在瀏覽器本身（JavaScript 和 jQuery 程式碼）中執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4a65d-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="4a65d-322">在本教學課程中，您將會探索所有這些專案，並在後續設定。</span><span class="sxs-lookup"><span data-stu-id="4a65d-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="4a65d-323">下一步</span><span class="sxs-lookup"><span data-stu-id="4a65d-323">Coming Up Next</span></span>

<span data-ttu-id="4a65d-324">在此系列的下一個教學課程中，您將深入探索 ASP.NET Web Pages 程式設計。</span><span class="sxs-lookup"><span data-stu-id="4a65d-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a65d-325">其他資源</span><span class="sxs-lookup"><span data-stu-id="4a65d-325">Additional Resources</span></span>

<span data-ttu-id="4a65d-326">[從頭開始建立 ASP.NET 網站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="4a65d-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="4a65d-327">本教學課程特別說明如何使用 WebMatrix （不 ASP.NET Web Pages）。</span><span class="sxs-lookup"><span data-stu-id="4a65d-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="4a65d-328">另外還有一些關於 WebMatrix 的其他功能，我們將不會在本教學課程中討論到的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4a65d-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4a65d-329">下一步</span><span class="sxs-lookup"><span data-stu-id="4a65d-329">Next</span></span>](intro-to-web-pages-programming.md)
