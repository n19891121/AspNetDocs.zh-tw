---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (包括 2011 年 4 月工具更新)ASP.NET MVC 3 是一個框架,用於使用成熟的設計模式建譯可擴充的、基於標準的 Web 應用程式...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675144"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="e2c2e-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="e2c2e-103">ASP.NET MVC 3</span></span>

> <span data-ttu-id="e2c2e-104">*(包括 2011 年 4 月工具更新)*</span><span class="sxs-lookup"><span data-stu-id="e2c2e-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="e2c2e-105">ASP.NET MVC 3 是一個框架,用於使用成熟的設計模式以及 ASP.NET 和 .NET 框架的強大功能建構可擴展的、基於標準的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="e2c2e-106">它與mVC ASP.NET並行安裝,所以立即開始使用它!</span><span class="sxs-lookup"><span data-stu-id="e2c2e-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="e2c2e-107">在此處下載[安裝程式](https://microsoft.com/download/details.aspx?id=4211)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-107">Download the [installer here](https://microsoft.com/download/details.aspx?id=4211)</span></span>

## <a name="top-features"></a><span data-ttu-id="e2c2e-108">熱門功能</span><span class="sxs-lookup"><span data-stu-id="e2c2e-108">Top Features</span></span>

- <span data-ttu-id="e2c2e-109">整合式腳手架系統可透過 NuGet 進行擴充</span><span class="sxs-lookup"><span data-stu-id="e2c2e-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="e2c2e-110">開啟 HTML 5 的項目樣本</span><span class="sxs-lookup"><span data-stu-id="e2c2e-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="e2c2e-111">表現性檢視,包括新的剃刀檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="e2c2e-112">具有相依項碼和全域操作篩選器的強大掛鉤</span><span class="sxs-lookup"><span data-stu-id="e2c2e-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="e2c2e-113">具有不顯眼的 JavaScript、jQuery 驗證和 JSON 綁定的豐富 JAvaScript 支援</span><span class="sxs-lookup"><span data-stu-id="e2c2e-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="e2c2e-114">*閱讀[下面的](#overview)完整功能清單*</span><span class="sxs-lookup"><span data-stu-id="e2c2e-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="e2c2e-115">熱門連結</span><span class="sxs-lookup"><span data-stu-id="e2c2e-115">Top Links</span></span>

<span data-ttu-id="e2c2e-116">ASP.NET MVC 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e2c2e-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="e2c2e-117">菲爾·哈克[:ASP.NET MVC 3 發佈](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="e2c2e-118">斯科特·漢塞爾曼[:ASP.NET MVC3、WebMatrix、NuGet、IIS 快遞和果園發佈 - 微軟 1 月 Web 發布上下文](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="e2c2e-119">斯科特·古斯裡:[宣佈發佈ASP.NET MVC 3,IIS 快遞,SQL CE 4,網路農場框架,果園,WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="e2c2e-120">ASP.NET MVC 3 的發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="e2c2e-121">安裝並説明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-121">Installation and Help</span></span>

- <span data-ttu-id="e2c2e-122">使用 Web 平台安裝程式安裝 ASP.NET MVC [3(建議)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="e2c2e-123">使用[安裝程式執行檔](https://go.microsoft.com/fwlink/?LinkID=208140)安裝ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="e2c2e-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="e2c2e-124">安裝[ASP.NET MVC 3 用於視覺化工作室 11 開發人員預覽](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="e2c2e-125">閱讀[簡介以ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="e2c2e-126">在[論壇](https://forums.asp.net/1146.aspx)中獲取有關 MVC 3 ASP.NET幫助和討論</span><span class="sxs-lookup"><span data-stu-id="e2c2e-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="e2c2e-127">ASP.NET MVC 3 概觀 (英文)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="e2c2e-128">ASP.NET MVC 3 建立在 ASP.NET MVC 1 和 2 的基礎上,增加了既簡化了代碼又允許更深度擴展性的偉大功能。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="e2c2e-129">本主題概述了此版本中包括的許多新功能,這些功能分為以下各節:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="e2c2e-130">透過 Mvc Scaffold 整合式延伸腳手架</span><span class="sxs-lookup"><span data-stu-id="e2c2e-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="e2c2e-131">開啟 HTML 5 的項目樣本</span><span class="sxs-lookup"><span data-stu-id="e2c2e-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="e2c2e-132">剃刀檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="e2c2e-133">支援多檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="e2c2e-134">控制器改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="e2c2e-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="e2c2e-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="e2c2e-136">模型驗證改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="e2c2e-137">相依項改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="e2c2e-138">其他新功能</span><span class="sxs-lookup"><span data-stu-id="e2c2e-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="e2c2e-139">透過 Mvc Scaffold 整合式延伸腳手架</span><span class="sxs-lookup"><span data-stu-id="e2c2e-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="e2c2e-140">新的 Scaffoldsing 系統使您能夠更輕鬆地拿起並開始高效使用,如果您是框架的完全新,並且如果您經驗豐富且已經知道正在做什麼,則自動執行常見開發任務。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="e2c2e-141">這是由新的NuGet*腳手架*包支援,稱為**Mvc 腳手架**。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="e2c2e-142">許多軟體技術使用術語「Scaffolding」表示「快速生成軟體的基本大綱,然後您可以編輯和自定義」。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="e2c2e-143">我們為ASP.NET MVC 創建的腳手架包在幾個方案中非常有用:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="e2c2e-144">**如果你第一次學習ASP.NETMVC,** 因為它為您提供了一種快速的方式來獲得一些有用的工作代碼,然後你可以根據您的需要進行編輯和調整。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="e2c2e-145">它為您從看著空白頁面的創傷中拯救,並且不知道從哪裡開始!</span><span class="sxs-lookup"><span data-stu-id="e2c2e-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="e2c2e-146">**如果您對 MVC ASP.NET非常瞭解,並且正在探索一些新的附加技術**,如對象關係映射器、視圖引擎、測試庫等,因為該技術的創建者可能也為它創建了一個基架包。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="e2c2e-147">**如果工作涉及重複創建類似類或某種檔**,因為您可以創建自定義基架,以輸出測試夾具、部署腳本或其他任何需要。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="e2c2e-148">團隊中的每個人都可以使用自定義腳手架。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="e2c2e-149">MvcScaffoldsing 中的其他功能包括:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="e2c2e-150">支援 C# 與 VB 專案</span><span class="sxs-lookup"><span data-stu-id="e2c2e-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="e2c2e-151">支援剃刀與 ASPX 檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="e2c2e-152">支援將腳手架放入ASP.NET MVC 區域並使用自訂檢視佈局/主機</span><span class="sxs-lookup"><span data-stu-id="e2c2e-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="e2c2e-153">您可以透過編輯 T4 樣本輕鬆自訂輸出</span><span class="sxs-lookup"><span data-stu-id="e2c2e-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="e2c2e-154">您可以使用自定義 PowerShell 邏輯和自訂 T4 範本添加全新的基架。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="e2c2e-155">這些參數(以及您提供給它們的任何自定義參數)會自動顯示在控制台選項卡完成清單中。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="e2c2e-156">您可以取得包含不同技術的其他基架支架的 NuGet 套件(例如,現在 LINQ 到 SQL 都有一個概念驗證套件),並將它們混合並符合在一起</span><span class="sxs-lookup"><span data-stu-id="e2c2e-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="e2c2e-157">ASP.NET MVC 3 工具更新包括針對此基架系統的巨大 Visual Studio 支援,例如:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="e2c2e-158">新增控制器對話框現在支援建立、讀取、更新和刪除控制器操作和相應檢視的完整自動基架。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="e2c2e-159">預設情況下,此基架數據存取代碼使用 EF 代碼優先。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="e2c2e-160">新增控制器對話框支援透過 NuGet 套件(如*MvcScaffold)\*\*進行擴充基架*。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="e2c2e-161">這允許將自定義基架插入對話框中,這樣,如果您傾向於的話,您可以為其他數據訪問技術(如 NHibernate)創建基架,甚至使用 ODBCDirect 的 JET!</span><span class="sxs-lookup"><span data-stu-id="e2c2e-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="e2c2e-162">有關 ASP.NET MVC 3 中的基架的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="e2c2e-163">史蒂夫·桑德森的系列帖子,包括:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="e2c2e-164">簡介: 使用 MvcScaffoldss 封裝,ASP.NET MVC 3 專案腳手架</span><span class="sxs-lookup"><span data-stu-id="e2c2e-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="e2c2e-165">標準用法:典型用例和選項</span><span class="sxs-lookup"><span data-stu-id="e2c2e-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="e2c2e-166">一對多關係</span><span class="sxs-lookup"><span data-stu-id="e2c2e-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="e2c2e-167">文手架操作和單元測試</span><span class="sxs-lookup"><span data-stu-id="e2c2e-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="e2c2e-168">覆寫 T4 樣本</span><span class="sxs-lookup"><span data-stu-id="e2c2e-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="e2c2e-169">這篇文章:建立自訂腳手架</span><span class="sxs-lookup"><span data-stu-id="e2c2e-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="e2c2e-170">斯科特·漢塞爾曼的帖子從他的PDC 2010會話[建立博客與微軟"未命名的網络愛包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="e2c2e-171">MVC 3 發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="e2c2e-172">HTML 5 專案範本</span><span class="sxs-lookup"><span data-stu-id="e2c2e-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="e2c2e-173">"新項目"對話框包括一個複選框,該複選框啟用 HTML 5 版本的項目範本。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="e2c2e-174">這些樣本利用 Modernizr 1.7 在低級瀏覽器中為 HTML 5 和 CSS 3 提供相容性支援。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="e2c2e-175">剃刀檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-175">The Razor View Engine</span></span>

<span data-ttu-id="e2c2e-176">ASP.NET MVC 3 附帶了名為 Razor 的新檢視引擎,具有以下優點:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="e2c2e-177">剃刀語法簡潔簡潔,需要最少的擊鍵次數。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="e2c2e-178">Razor 易於學習,部分原因在於它基於現有語言(如 C# 和 Visual Basic)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="e2c2e-179">可視化工作室包括用於 Razor 語法的 IntelliSense 和代碼著色。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="e2c2e-180">Razor 檢視可以進行單元測試,而無需運行應用程式或啟動 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="e2c2e-181">一些新的 Razor 功能包括:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="e2c2e-182">`@model`用於指定傳遞給檢視的類型的語法。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="e2c2e-183">`@* *@`註釋語法。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="e2c2e-184">為整個網站指定預設值(如`layoutpage`) 一次的能力。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="e2c2e-185">顯示`Html.Raw`文字而不進行 HTML 編碼的方法。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="e2c2e-186">支援在多個檢視之間共享代碼(*\_檢視 start.cshtml*或*\_viewstart.vbhtml*檔案)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="e2c2e-187">Razor 還包括新的 HTML 說明器,如下所示:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="e2c2e-188">`Chart`.</span><span class="sxs-lookup"><span data-stu-id="e2c2e-188">`Chart`.</span></span> <span data-ttu-id="e2c2e-189">渲染圖表,提供與 ASP.NET 4 中的圖表控件相同的要素。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="e2c2e-190">`WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="e2c2e-190">`WebGrid`.</span></span> <span data-ttu-id="e2c2e-191">渲染數據網格,完成分頁和排序功能。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="e2c2e-192">`Crypto`.</span><span class="sxs-lookup"><span data-stu-id="e2c2e-192">`Crypto`.</span></span> <span data-ttu-id="e2c2e-193">使用哈希演演演算法創建正確加鹽和哈希密碼。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="e2c2e-194">`WebImage`.</span><span class="sxs-lookup"><span data-stu-id="e2c2e-194">`WebImage`.</span></span> <span data-ttu-id="e2c2e-195">渲染圖像。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-195">Renders an image.</span></span>
- <span data-ttu-id="e2c2e-196">`WebMail`.</span><span class="sxs-lookup"><span data-stu-id="e2c2e-196">`WebMail`.</span></span> <span data-ttu-id="e2c2e-197">傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-197">Sends an email message.</span></span>

<span data-ttu-id="e2c2e-198">有關 Razor 的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="e2c2e-199">斯科特·古斯裡的博客文章介紹剃刀</span><span class="sxs-lookup"><span data-stu-id="e2c2e-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="e2c2e-200">斯科特·古斯裡的博客文章介紹關鍵字@model</span><span class="sxs-lookup"><span data-stu-id="e2c2e-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="e2c2e-201">斯科特·古斯裡的博客文章介紹剃刀佈局</span><span class="sxs-lookup"><span data-stu-id="e2c2e-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="e2c2e-202">剃刀 API 快速參考</span><span class="sxs-lookup"><span data-stu-id="e2c2e-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="e2c2e-203">MVC 3 發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="e2c2e-204">支援多檢視引擎</span><span class="sxs-lookup"><span data-stu-id="e2c2e-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="e2c2e-205">ASP.NET MVC 3 中的 **「新增檢視」** 對話框允許您選擇要使用的檢視引擎,而 **「新專案**」對話框允許您為專案指定預設檢視引擎。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="e2c2e-206">您可以選擇 Web 窗體檢視引擎 (ASPX)、Razor 或開源檢視引擎(如[Spark、NHaml](https://code.google.com/p/nhaml/)或[Spark](http://sparkviewengine.com/)[NDjango)。](http://ndjango.org/)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="e2c2e-207">控制器改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="e2c2e-208">全域操作篩選器</span><span class="sxs-lookup"><span data-stu-id="e2c2e-208">Global Action Filters</span></span>

<span data-ttu-id="e2c2e-209">有時,您希望在操作方法運行之前或操作方法運行之前執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="e2c2e-210">為了支援這一點,ASP.NET MVC 2 提供了操作篩選器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="e2c2e-211">操作篩選器是自定義屬性,提供聲明性方法,將操作前和操作後行為添加到特定的控制器操作方法。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="e2c2e-212">但是,在某些情況下,您可能希望指定適用於所有操作方法的操作前或行動後行為。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="e2c2e-213">MVC 3 允許您通過將全域篩選器添加`GlobalFilters`到 集合來指定全域篩選器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="e2c2e-214">有關全域操作篩選器的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="e2c2e-215">斯科特·古斯裡在MVC 3預覽的博客</span><span class="sxs-lookup"><span data-stu-id="e2c2e-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="e2c2e-216">[ASP.NET MVC 中的篩選](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="e2c2e-217">新的「檢視袋」屬性</span><span class="sxs-lookup"><span data-stu-id="e2c2e-217">New "ViewBag" Property</span></span>

<span data-ttu-id="e2c2e-218">MVC 2`ViewData`控制器 支援一個屬性,該屬性使您能夠使用後期綁定字典 API 將數據傳遞到檢視範本。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="e2c2e-219">在 MVC 3 中,還可以對屬性`ViewBag`使用更簡單 的語法來實現相同的目的。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="e2c2e-220">例如,可以寫入`ViewData["Message"]="text"`而不是`ViewBag.Message="text"`寫入 。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="e2c2e-221">不需要定義任何強型態類別使用`ViewBag`屬性 。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="e2c2e-222">因為它是動態屬性,因此只需獲取或設置屬性,它將在運行時動態解析它們。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="e2c2e-223">在內部`ViewBag`,屬性`ViewData`在字典中存儲為名稱/值對。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="e2c2e-224">(注意:在大多數預發行版本的 MVC 3`ViewBag`中, 屬性`ViewModel`被命名為屬性 。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="e2c2e-225">新的「動作結果」類型</span><span class="sxs-lookup"><span data-stu-id="e2c2e-225">New "ActionResult" Types</span></span>

<span data-ttu-id="e2c2e-226">以下`ActionResult`類型與相應的說明器方法在 MVC 3 中是新的或增強的:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="e2c2e-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="e2c2e-228">將 404 HTTP 狀態代碼返回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="e2c2e-229">[重定向結果](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="e2c2e-230">返回臨時重定向 (HTTP 302 狀態代碼) 或永久重定向 (HTTP 301 狀態代碼),具體取決於布爾參數。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="e2c2e-231">結合此變更[,Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)類別現在有三種執行永久重定向的方法`RedirectPermanent``RedirectToRoutePermanent`:、 和`RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="e2c2e-232">這些方法返回`RedirectResult``Permanent`屬性設置`true`為 的實例。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="e2c2e-233">[HTTPStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span><span class="sxs-lookup"><span data-stu-id="e2c2e-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="e2c2e-234">返回使用者指定的 HTTP 狀態代碼。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="e2c2e-235">JavaScript 和 Ajax 改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="e2c2e-236">默認情況下,MVC 3 中的 Ajax 和驗證説明程式使用不顯眼的 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="e2c2e-237">不顯眼的 JavaScript 避免將內聯 JAvaScript 注入 HTML。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="e2c2e-238">這使得您的 HTML 更小且不太混亂,並且更易於交換或自定義 JavaScript 庫。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="e2c2e-239">默認情況下,MVC `jQueryValidate` 3 中的驗證説明程式也使用該外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="e2c2e-240">如果需要 MVC 2 行為,可以使用*Web.config*檔設置禁用不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="e2c2e-241">有關 JavaScript 和 Ajax 改進的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="e2c2e-242">維琪百科網站上不顯眼的JAVAScript的基本介紹</span><span class="sxs-lookup"><span data-stu-id="e2c2e-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="e2c2e-243">布拉德·威爾遜的《不顯眼的JAVAScript》帖子</span><span class="sxs-lookup"><span data-stu-id="e2c2e-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="e2c2e-244">布拉德·威爾遜的《不顯眼的JAVA腳本驗證帖》</span><span class="sxs-lookup"><span data-stu-id="e2c2e-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="e2c2e-245">[使用 Razor 與不顯眼的 JavaScript 建立 MVC 3 應用程式](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)(ASP.NET網站上的教程)</span><span class="sxs-lookup"><span data-stu-id="e2c2e-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="e2c2e-246">MVC 3 發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="e2c2e-247">預設使用客戶端驗證</span><span class="sxs-lookup"><span data-stu-id="e2c2e-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="e2c2e-248">在早期版本的 MVC 中,需要從檢視中顯式調`Html.EnableClientValidation`用方法,以便啟用客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="e2c2e-249">在 MVC 3 中,這不再需要,因為默認情況下啟用客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="e2c2e-250">(您可以使用*Web.config*檔中的設定禁用此功能。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="e2c2e-251">為了使客戶端驗證正常工作,您仍然需要引用網站中相應的 jQuery 和 jQuery 驗證庫。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="e2c2e-252">您可以在自己的伺服器上託管這些庫,也可以從內容交付網路 (CDN)(如 Microsoft 或 Google 的 CDN)中引用它們。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="e2c2e-253">遠端驗證器</span><span class="sxs-lookup"><span data-stu-id="e2c2e-253">Remote Validator</span></span>

<span data-ttu-id="e2c2e-254">ASP.NET MVC 3 支援新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)類,使您能夠利用 jQuery 驗證外掛程式的遠端驗證器支援。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="e2c2e-255">這使客戶端驗證庫能夠自動呼叫您在伺服器上定義的自訂方法,以便執行只能執行伺服器端的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="e2c2e-256">`Remote`在下面的範例中,該屬性指定客戶端驗證將調`UserNameAvailable``UsersController`用 類上命名的操作以`UserName`驗證該 欄位。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="e2c2e-257">下面的示例顯示了相應的控制器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="e2c2e-258">有關如何使用`Remote`該屬性的詳細資訊,請參閱如何:在 MSDN 函式庫中[ASP.NET MVC 中實現遠端驗證](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="e2c2e-259">JSON 繫結支援</span><span class="sxs-lookup"><span data-stu-id="e2c2e-259">JSON Binding Support</span></span>

<span data-ttu-id="e2c2e-260">ASP.NET MVC 3 包括內建的 JSON 綁定支援,使操作方法能夠接收 JSON 編碼的數據,並將其模型綁定到操作方法參數。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="e2c2e-261">此功能在涉及用戶端範本和數據綁定的方案中非常有用。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="e2c2e-262">(用戶端範本使您能夠使用在用戶端上執行的範本格式化和顯示單個資料項或資料項集。MVC 3 使您能夠輕鬆地將用戶端範本與發送和接收 JSON 數據的伺服器上的操作方法連接。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="e2c2e-263">有關 JSON 綁定支援的詳細資訊,請參閱[Scott Guthrie 的 MVC 3 預覽部落格文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript 和 AJAX 改進**部分。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="e2c2e-264">模型驗證改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="e2c2e-265">「資料註解」中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="e2c2e-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="e2c2e-266">ASP.NET MVC `DataAnnotations` 3`DisplayAttribute`支援中繼資料屬性,如 。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="e2c2e-267">『驗證屬性』類別</span><span class="sxs-lookup"><span data-stu-id="e2c2e-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="e2c2e-268">在`ValidationAttribute`.NET 框架 4 中`IsValid`改進了該類,以支援新的重載,該重載提供有關當前驗證上下文的詳細資訊,例如正在驗證的物件。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="e2c2e-269">這支援更豐富的方案,您可以在其中根據模型的另一個屬性驗證當前值。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="e2c2e-270">例如,新`CompareAttribute`屬性允許您比較模型的兩個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="e2c2e-271">在下面的範例中,`ComparePassword`屬性必須`Password`符合 該欄位才能有效。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="e2c2e-272">驗證介面</span><span class="sxs-lookup"><span data-stu-id="e2c2e-272">Validation Interfaces</span></span>

<span data-ttu-id="e2c2e-273">[IValidaobject 介面](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)使您能夠執行模型級驗證,並且它使您能夠提供特定於整個模型狀態的驗證錯誤消息,或在模型中的兩個屬性之間。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="e2c2e-274">MVC 3`IValidatableObject`現在從 模型綁定時從介面檢索錯誤,並使用內置的 HTML 表單説明器自動標記或突出顯示視圖中受影響的欄位。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="e2c2e-275">[IClientValidaa 可介面](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)使ASP.NET MVC 能夠在運行時發現驗證器是否支援客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="e2c2e-276">此介面的設計使其可以與各種驗證框架集成。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="e2c2e-277">有關驗證介面的詳細資訊,請參閱[Scott Guthrie 的 MVC 3 預覽部落格文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)**模型驗證改進**部分。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="e2c2e-278">(但是,請注意,博客中對"IValidateObject"的引用應為"IValidaaobject"。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="e2c2e-279">相依項改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="e2c2e-280">ASP.NET MVC 3 為應用依賴項注入 (DI) 和與依賴項注入或控制反轉 (IOC) 容器集成提供更好的支援。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="e2c2e-281">在以下領域新增了對 DI 的支援:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="e2c2e-282">控制器(註冊和注入控制器工廠,注入控制器)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="e2c2e-283">視圖(註冊和注入視圖引擎,將依賴項注入視圖頁)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="e2c2e-284">操作篩選器(定位和注入篩檢程式)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="e2c2e-285">模型活頁夾(註冊和注入)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="e2c2e-286">模型驗證提供程式(註冊和注入)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="e2c2e-287">建模元數據提供程式(註冊和注入)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="e2c2e-288">價值提供者(註冊和注入)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="e2c2e-289">MVC 3 支援[通用服務定位器](https://github.com/unitycontainer/commonservicelocator)庫`IServiceLocator`和支援該庫 介面的任何 DI 容器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="e2c2e-290">它還支援一個新的`IDependencyResolver`介面,使集成 DI 框架變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="e2c2e-291">有關 MVC 3 中的 DI 的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="e2c2e-292">布拉德·威爾遜關於服務地點的一系列博客文章</span><span class="sxs-lookup"><span data-stu-id="e2c2e-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="e2c2e-293">MVC 3 發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="e2c2e-294">其他新功能</span><span class="sxs-lookup"><span data-stu-id="e2c2e-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="e2c2e-295">NuGet 整合</span><span class="sxs-lookup"><span data-stu-id="e2c2e-295">NuGet Integration</span></span>

<span data-ttu-id="e2c2e-296">ASP.NET MVC 3 自動安裝並啟用 NuGet 作為其設置的一部分。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="e2c2e-297">NuGet 是免費的開源套件管理員,可讓您在專案中輕鬆搜尋、安裝和使用.NET庫和工具。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="e2c2e-298">它適用於所有 Visual Studio 專案類型(包括ASP.NET Web 窗體和ASP.NET MVC)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="e2c2e-299">NuGet 使維護開源專案的開發人員(例如,像 Moq、NHibernate、Ninject、結構映射、NUnit、溫莎、RhinoMocks 和 Elmah)的專案)能夠打包其庫並將其註冊到線上庫中。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="e2c2e-300">然後,想要使用這些庫之一的 .NET 開發人員可以輕鬆查找包並將其安裝在他們正在處理的專案中。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="e2c2e-301">通過ASP.NET 3 工具更新,專案範本包括預安裝的 NuGet 包的 JavaScript 庫,因此它們可以通過 NuGet 進行更新。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="e2c2e-302">實體框架代碼優先也預裝為 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="e2c2e-303">如需 NuGet 的詳細資訊，請參閱 [NuGet 文件](https://docs.microsoft.com/nuget/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="e2c2e-304">部份頁面輸出快取</span><span class="sxs-lookup"><span data-stu-id="e2c2e-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="e2c2e-305">自版本 1 以來ASP.NET MVC 都支援整頁回應的輸出緩存。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="e2c2e-306">MVC 3 還支援部分頁面輸出緩存,這允許您輕鬆緩存回應的區域或片段。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="e2c2e-307">有關緩存的詳細資訊,請參閱[Scott Guthrie 在 MVC 3 版本候選版和 MVC](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) [3 發行說明](../whitepapers/mvc3-release-notes.md)的 **「子操作輸出緩存**」部分部分頁面**輸出緩存**部分。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="e2c2e-308">對要求驗證的精細控制</span><span class="sxs-lookup"><span data-stu-id="e2c2e-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="e2c2e-309">ASP.NET MVC 具有內置請求驗證,可自動幫助抵禦 XSS 和 HTML 注入攻擊。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="e2c2e-310">但是,有時您希望顯式禁用請求驗證,例如,如果您希望允許使用者發佈 HTML 內容(例如,在部落格條目或 CMS 內容中)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="e2c2e-311">現在,您可以將[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)屬性添加到模型或視圖模型,以便在模型綁定期間禁用基於每個屬性的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="e2c2e-312">有關請求驗證的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="e2c2e-313">[斯科特·古斯裡關於MVC 3版本候選的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 **「不顯眼的JavaScript和驗證**」部分。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="e2c2e-314">MVC 3 發行說明</span><span class="sxs-lookup"><span data-stu-id="e2c2e-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="e2c2e-315">可擴充的「新項目」對話框</span><span class="sxs-lookup"><span data-stu-id="e2c2e-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="e2c2e-316">在 mVC 3 ASP.NET,您可以將專案範本、檢視引擎和單元測試專案框架添加到 **「新項目**」對話框中。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="e2c2e-317">樣本基架改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="e2c2e-318">ASP.NET MVC 3 基架範本比早期版本的 MVC 更好地識別模型上的主鍵屬性並適當地處理它們。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="e2c2e-319">(例如,基架範本現在確保主鍵不是基架作為可編輯的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="e2c2e-320">默認情況下,"創建和編輯"基架現在使用`Html.EditorFor`幫助器而不是`Html.TextBoxFor`幫助程式。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="e2c2e-321">這在 **「添加檢視」** 對話框生成檢視時,改進了對模型上以數據註釋屬性形式對元數據的支援。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="e2c2e-322">"Html.Labelfor"和"Html.LabelFormodel"的新重載</span><span class="sxs-lookup"><span data-stu-id="e2c2e-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="e2c2e-323">已為`LabelFor`和`LabelForModel`幫助器方法添加了新方法重載。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="e2c2e-324">新的重載讓您能夠指定或覆蓋分頁文本。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="e2c2e-325">無工作階段控制器支援</span><span class="sxs-lookup"><span data-stu-id="e2c2e-325">Sessionless Controller Support</span></span>

<span data-ttu-id="e2c2e-326">在 mVC 3 ASP.NET 中,可以指示是否希望控制器類使用會話狀態,如果是,會話狀態應是讀/寫還是只讀。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="e2c2e-327">有關無會話控制器支援的詳細資訊,請參閱[MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="e2c2e-328">新的「附加元資料屬性」 類別</span><span class="sxs-lookup"><span data-stu-id="e2c2e-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="e2c2e-329">可以使用[「附加元數據」](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)屬性填充模型`ModelMetadata.AdditionalValues`屬性的 字典。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="e2c2e-330">例如,如果檢視模型具有僅應向管理員顯示的屬性,則可以對該屬性進行加帶,如以下示例所示:</span><span class="sxs-lookup"><span data-stu-id="e2c2e-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="e2c2e-331">呈現產品檢視模型時,此元數據可用於任何顯示或編輯器範本。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="e2c2e-332">由您解釋元數據資訊。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="e2c2e-333">帳號控制器改進</span><span class="sxs-lookup"><span data-stu-id="e2c2e-333">AccountController improvements</span></span>

<span data-ttu-id="e2c2e-334">互聯網專案範本中的帳戶控制器已大為改善。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="e2c2e-335">新的內聯網項目範本</span><span class="sxs-lookup"><span data-stu-id="e2c2e-335">New Intranet Project Template</span></span>

<span data-ttu-id="e2c2e-336">包含新的 Intranet 專案樣本,該範本啟用 Windows 身份驗證並刪除帳戶控制器。</span><span class="sxs-lookup"><span data-stu-id="e2c2e-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>
