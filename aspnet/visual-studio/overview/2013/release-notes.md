---
uid: visual-studio/overview/2013/release-notes
title: 視覺工作室ASP.NET和網络工具 2013 發行說明 |微軟文件
author: rick-anderson
description: 本文檔介紹了 2013 年可視化工作室的 ASP.NET 和網路工具的發布。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543492"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="9b6a6-103">適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具版本資訊</span><span class="sxs-lookup"><span data-stu-id="9b6a6-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="9b6a6-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9b6a6-105">本文檔介紹了 2013 年可視化工作室的 ASP.NET 和網路工具的發布。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="9b6a6-106">內容</span><span class="sxs-lookup"><span data-stu-id="9b6a6-106">Contents</span></span>

- [<span data-ttu-id="9b6a6-107">安裝說明</span><span class="sxs-lookup"><span data-stu-id="9b6a6-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="9b6a6-108">文件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="9b6a6-109">軟體要求</span><span class="sxs-lookup"><span data-stu-id="9b6a6-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="9b6a6-110">2013年可視化工作室ASP.NET和網路工具的新功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="9b6a6-111">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b6a6-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="9b6a6-112">新的 Web 專案體驗</span><span class="sxs-lookup"><span data-stu-id="9b6a6-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="9b6a6-113">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="9b6a6-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="9b6a6-114">瀏覽器連結</span><span class="sxs-lookup"><span data-stu-id="9b6a6-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="9b6a6-115">視覺化工作室 Web 編輯器增強功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="9b6a6-116">Visual Studio 中的 Azure 應用服務 Web 應用支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="9b6a6-117">Web 發佈增強功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="9b6a6-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="9b6a6-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="9b6a6-119">ASP.NET Web 表單</span><span class="sxs-lookup"><span data-stu-id="9b6a6-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="9b6a6-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="9b6a6-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="9b6a6-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="9b6a6-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="9b6a6-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="9b6a6-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="9b6a6-123">ASP.NET身份</span><span class="sxs-lookup"><span data-stu-id="9b6a6-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="9b6a6-124">Microsoft OWIN 元件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="9b6a6-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9b6a6-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="9b6a6-126">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="9b6a6-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="9b6a6-127">ASP.NET應用程式掛起</span><span class="sxs-lookup"><span data-stu-id="9b6a6-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="9b6a6-128">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="9b6a6-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="9b6a6-129">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="9b6a6-129">Installation Notes</span></span>

<span data-ttu-id="9b6a6-130">ASP.NET和Web工具為可視化工作室2013捆綁在主安裝程式,可以[在這裡](https://www.asp.net/downloads)下載。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="9b6a6-131">文件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-131">Documentation</span></span>

<span data-ttu-id="9b6a6-132">有關 visual Studio 2013 的 ASP.NET 和 Web 工具的教程和其他資訊可從[ASP.NET 網站](https://www.asp.net/)獲得。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="9b6a6-133">軟體需求</span><span class="sxs-lookup"><span data-stu-id="9b6a6-133">Software Requirements</span></span>

<span data-ttu-id="9b6a6-134">ASP.NET和網路工具需要可視化工作室 2013。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="9b6a6-135">2013年可視化工作室ASP.NET和網路工具的新功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="9b6a6-136">以下各節介紹版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="9b6a6-137">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b6a6-137">One ASP.NET</span></span>

<span data-ttu-id="9b6a6-138">隨著 Visual Studio 2013 的發表,我們朝著統一使用 ASP.NET 技術的經驗邁出了一步,以便您可以輕鬆混合和匹配所需的技術。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="9b6a6-139">例如,可以使用 MVC 啟動專案,並在以後輕鬆地將 Web 窗體頁添加到專案,或在 Web 窗體專案中基架 Web API 中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="9b6a6-140">一ASP.NET就是讓你作為開發人員更容易在ASP.NET中做你喜歡的事情。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="9b6a6-141">無論您選擇何種技術,您都可以確信自己正在構建"一ASP.NET"的可信底層框架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="9b6a6-142">新的 Web 專案體驗</span><span class="sxs-lookup"><span data-stu-id="9b6a6-142">New Web Project Experience</span></span>

<span data-ttu-id="9b6a6-143">我們在 Visual Studio 2013 中增強了創建新 Web 專案的經驗。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="9b6a6-144">在 **「新建ASP.NET Web 專案**」對話框中,您可以選擇所需的項目類型、配置任何技術組合(Web 窗體、MVC、Web API)、設定身份驗證選項以及添加單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![新ASP.NET專案](release-notes/_static/image1.png)

<span data-ttu-id="9b6a6-146">新的對話框使您能夠更改許多範本的預設身份驗證選項。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="9b6a6-147">例如,在建立ASP.NET Web 窗體專案時,您可以選擇以下任一選項:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="9b6a6-148">不需要驗證</span><span class="sxs-lookup"><span data-stu-id="9b6a6-148">No Authentication</span></span>
- <span data-ttu-id="9b6a6-149">個人使用者帳戶(ASP.NET會員身份或社交提供者登入)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="9b6a6-150">組織帳號 (網路應用程式中的活動目錄)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="9b6a6-151">Windows 驗證(Intranet 應用程式中的活動目錄)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![驗證選項](release-notes/_static/image2.png)

<span data-ttu-id="9b6a6-153">有關建立 Web 專案的新流程的詳細資訊,請參閱在[Visual Studio 2013 建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="9b6a6-154">關於新身份驗證選項的詳細資訊,請參考此文件後面的[ASP.NET 識別](#TOC8)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="9b6a6-155">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="9b6a6-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="9b6a6-156">ASP.NET基架是ASP.NET Web 應用程式的代碼生成框架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="9b6a6-157">它可以輕鬆地向與數據模型交互的專案添加樣板代碼。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="9b6a6-158">在 Visual Studio 的早期版本中,基架僅限於 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="9b6a6-159">借助 Visual Studio 2013,您現在可以對任何 ASP.NET 專案(包括 Web 窗體)使用基架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="9b6a6-160">Visual Studio 2013 目前不支援為 Web 窗體專案生成頁面,但您仍可以通過向專案添加 MVC 依賴項來使用 Web 窗體的腳手架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="9b6a6-161">將在將來的更新中添加對生成 Web 窗體頁面的支援。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="9b6a6-162">使用基架時,我們確保在專案中安裝了所有必需的依賴項。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="9b6a6-163">例如,如果從ASP.NET Web 窗體專案開始,然後使用基架添加 Web API 控制器,則所需的 NuGet 包和引用將自動添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="9b6a6-164">要將 MVC 基架加入 Web 窗體專案,請新增**新的文手架,** 並在對話框視窗中選擇**MVC 5 相依項 。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="9b6a6-165">基架 MVC 有兩個選項;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="9b6a6-166">如果選擇「最小」,則只有 ASP.NET MVC 的 NuGet 包和引用添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="9b6a6-167">如果選擇"完整"選項,則添加最小依賴項以及 MVC 專案所需的內容檔。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="9b6a6-168">支援基架非同步控制器使用實體框架6中的新異步功能。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="9b6a6-169">有關詳細資訊和教程,請參閱[ASP.NET 腳手架概述](aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="9b6a6-170">瀏覽器連結 + 瀏覽器和視覺化工作室之間的訊號R通道</span><span class="sxs-lookup"><span data-stu-id="9b6a6-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="9b6a6-171">新的[瀏覽器連結](using-browser-link.md)功能允許您將多個瀏覽器連接到 Visual Studio,並透過單擊工具列中的按鈕刷新所有瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="9b6a6-172">您可以將多個瀏覽器連接到開發網站(包括移動模擬程式),然後單擊刷新以同時刷新所有瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="9b6a6-173">瀏覽器連結還公開 API,使開發人員能夠編寫瀏覽器連結擴展。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="9b6a6-174">通過使開發人員能夠利用瀏覽器連結 API,可以創建非常高級的方案,這些方案跨越 Visual Studio 和任何已連接的瀏覽器之間的邊界。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="9b6a6-175">Web Essentials 利用 API 在 Visual Studio 和瀏覽器的開發人員工具、遠端控制行動模擬器等之間創建整合體驗。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="9b6a6-176">視覺化工作室 Web 編輯器增強功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="9b6a6-177">Visual Studio 2013 包括用於 Web 應用程式中 Razor 檔案和 HTML 檔案的新 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="9b6a6-178">新的 HTML 編輯器提供基於 HTML5 的單一架構。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="9b6a6-179">它有自動大括弧完成,jQuery UI和AngularJS屬性IntelliSense,屬性IntelliSense分組,ID和類名Intellisense,和其他改進,包括更好的性能,格式和智慧標籤。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="9b6a6-180">以下螢幕截圖示範如何在 HTML 編輯器中使用 Bootstrap 屬性 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 編輯器中的感知](release-notes/_static/image4.png)

<span data-ttu-id="9b6a6-182">Visual Studio 2013 還附帶了內置的咖啡腳本和 LESS 編輯器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="9b6a6-183">LESS 編輯器附帶了 CSS 編輯器中的所有很酷的功能,@import並具有針對鏈中所有 LESS 文件中的變數和混合值的特定 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="9b6a6-184">Visual Studio 中的 Azure 應用服務 Web 應用支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="9b6a6-185">在 Visual Studio 2013 中,使用用於 .NET 2.2 的 Azure SDK,可以使用**伺服器資源管理器**直接與遠端 Web 應用進行交互。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="9b6a6-186">您可以登錄到 Azure 帳戶、創建新的 Web 應用、配置應用、查看即時日誌等。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="9b6a6-187">SDK 2.2 發佈後不久,您將能夠在 Azure 中遠端在調試模式下運行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="9b6a6-188">安裝 .NET 的 Azure SDK 當前版本時,Azure 應用服務 Web 應用的大多數新功能在 Visual Studio 2012 中也起作用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="9b6a6-189">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="9b6a6-190">在 Azure 應用服務中建立ASP.NET Web 應用</span><span class="sxs-lookup"><span data-stu-id="9b6a6-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="9b6a6-191">使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9b6a6-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="9b6a6-192">Web 發佈增強功能</span><span class="sxs-lookup"><span data-stu-id="9b6a6-192">Web Publish Enhancements</span></span>

<span data-ttu-id="9b6a6-193">Visual Studio 2013 包括新的和增強的 Web 發佈功能。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="9b6a6-194">以下提供其中一些範例：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-194">Here are a few of them:</span></span>

- <span data-ttu-id="9b6a6-195">輕鬆[自動進行 Web.config 檔案加密](https://go.microsoft.com/fwlink/?LinkId=325529)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="9b6a6-196">(此連結和以下兩個指向 MSDN 上的文檔,這些文檔可能直到 10 月 17 日深夜才可用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="9b6a6-197">在[部署期間輕鬆自動讓應用程式離線](https://go.microsoft.com/fwlink/?LinkId=325530)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="9b6a6-198">將 Web 部署設定為[使用檔案校驗和,而不是上次更改的日期](https://go.microsoft.com/fwlink/?LinkId=325531),以確定應複製到伺服器的檔。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="9b6a6-199">使用 FTP 或檔案系統發佈方法以及 Web 部署時,快速發表單個選定檔(包括 Web.config)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="9b6a6-200">有關ASP.NET Web 部署的詳細資訊,請參閱[ASP.NET網站](https://go.microsoft.com/fwlink/?LinkId=322027)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="9b6a6-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="9b6a6-201">NuGet 2.7</span></span>

<span data-ttu-id="9b6a6-202">NuGet 2.7 包含一組豐富的新功能,在[NuGet 2.7 發行說明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中對此進行了詳細介紹。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="9b6a6-203">此版本的 NuGet 還無需為 NuGet 的包還原功能提供下載包的明確同意。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="9b6a6-204">現在透過安裝 NuGet 授予同意(以及 NuGet 首選項對話方塊中的關聯複選框)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="9b6a6-205">現在,默認情況下,包還原只是工作。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="9b6a6-206">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="9b6a6-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="9b6a6-207">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b6a6-207">One ASP.NET</span></span>

<span data-ttu-id="9b6a6-208">Web 窗體專案範本與新 one ASP.NET 體驗無縫集成。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="9b6a6-209">您可以將 MVC 和 Web API 支援添加到 Web 窗體專案中,並且可以使用「一ASP.NET專案創建嚮導設定身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="9b6a6-210">有關詳細資訊,請參閱在[Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="9b6a6-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9b6a6-211">ASP.NET Identity</span></span>

<span data-ttu-id="9b6a6-212">Web 表單樣專案樣本支援新的ASP.NET識別架構。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="9b6a6-213">此外,範本現在支援創建 Web 窗體 Intranet 專案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="9b6a6-214">有關詳細資訊,請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案的**[認證方法](creating-web-projects-in-visual-studio.md#auth)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="9b6a6-215">啟動程序</span><span class="sxs-lookup"><span data-stu-id="9b6a6-215">Bootstrap</span></span>

<span data-ttu-id="9b6a6-216">Web 表單表板使用[Bootstrap](http://twitter.github.io/bootstrap/)提供時尚且回應迅速的外觀,讓您輕鬆自定義。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="9b6a6-217">有關詳細資訊,請參閱[Visual Studio 2013 Web 專案範本中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="9b6a6-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="9b6a6-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="9b6a6-219">一ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b6a6-219">One ASP.NET</span></span>

<span data-ttu-id="9b6a6-220">Web MVC 專案範本與新一ASP.NET體驗無縫整合。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="9b6a6-221">您可以使用「一ASP.NET項目創建嚮導自定義 MVC 專案並設定身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="9b6a6-222">ASP.NET MVC 5 的入門教程可以在[ASP.NET MVC 5 入門](../../../mvc/overview/getting-started/introduction/getting-started.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="9b6a6-223">有關將 MVC 4 專案升級到 MVC 5 的資訊,請參閱[如何將 ASP.NET MVC 4 和 Web API 專案升級到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="9b6a6-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9b6a6-224">ASP.NET Identity</span></span>

<span data-ttu-id="9b6a6-225">MVC 專案範本已更新,用於ASP.NET標識進行身份驗證和標識管理。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="9b6a6-226">一個教程,包括Facebook和谷歌認證和新的會員API可以在[創建ASP.NETMVC 5應用程式與Facebook和谷歌OAuth2和OpenID登錄](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md),[並建立ASP.NETMVC應用程式與auth和SQL DB,並部署到Azure應用程式服務](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="9b6a6-227">啟動程序</span><span class="sxs-lookup"><span data-stu-id="9b6a6-227">Bootstrap</span></span>

<span data-ttu-id="9b6a6-228">MVC 專案範本已更新,可使用[Bootstrap](http://getbootstrap.com/)提供時尚且回應迅速的外觀,讓您輕鬆自定義。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="9b6a6-229">有關詳細資訊,請參閱[Visual Studio 2013 Web 專案範本中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="9b6a6-230">驗證篩選器</span><span class="sxs-lookup"><span data-stu-id="9b6a6-230">Authentication filters</span></span>

<span data-ttu-id="9b6a6-231">身份驗證篩選器是 ASP.NET MVC 中一種新型篩選器,在 ASP.NET MVC 管道中的授權篩選器之前運行,允許您為所有控制器指定每個操作、每個控制器或全域的身份驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="9b6a6-232">身份驗證篩選器處理請求中的憑據並提供相應的主體。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="9b6a6-233">身份驗證篩選器還可以添加身份驗證質詢以回應未經授權的請求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="9b6a6-234">篩選器覆寫</span><span class="sxs-lookup"><span data-stu-id="9b6a6-234">Filter overrides</span></span>

<span data-ttu-id="9b6a6-235">現在,可以通過指定覆蓋篩選器來覆蓋應用於給定操作方法或控制器的篩選器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="9b6a6-236">覆蓋篩選器指定一組不應為給定作用域(操作或控制器)運行的篩選器類型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="9b6a6-237">這允許您配置全域應用的篩選器,但隨後排除某些全域篩選器應用於特定操作或控制器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="9b6a6-238">屬性路由</span><span class="sxs-lookup"><span data-stu-id="9b6a6-238">Attribute routing</span></span>

<span data-ttu-id="9b6a6-239">ASP.NET MVC 現在支援屬性路由,這要歸[http://attributerouting.net](http://attributerouting.net)功於 Tim McCall(作者)的貢獻。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="9b6a6-240">使用屬性路由,您可以通過對操作和控制器進行說明來指定路由。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="9b6a6-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="9b6a6-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="9b6a6-242">屬性路由</span><span class="sxs-lookup"><span data-stu-id="9b6a6-242">Attribute routing</span></span>

<span data-ttu-id="9b6a6-243">ASP.NET Web API 現在支援屬性路由,這要[http://attributerouting.net](http://attributerouting.net)歸功於 Tim McCall(作者)的貢獻。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="9b6a6-244">使用屬性路由,您可以通過指定操作和控制器來指定 Web API 路由,如下所示:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="9b6a6-245">屬性路由使您能夠對 Web API 中的 URI 進行更多控制。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="9b6a6-246">例如,您可以使用單個 API 控制器輕鬆定義資源層次結構:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="9b6a6-247">屬性路由還提供用於指定可選參數、預設值和路由約束的便捷語法:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="9b6a6-248">有關屬性路由的詳細資訊,請參閱[Web API 2 中的屬性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="9b6a6-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="9b6a6-249">OAuth 2.0</span></span>

<span data-ttu-id="9b6a6-250">Web API 和單頁應用程式專案範本現在支援使用 OAuth 2.0 進行授權。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="9b6a6-251">OAuth 2.0 是一個用於授權客戶端訪問受保護資源的框架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="9b6a6-252">它適用於各種用戶端,包括瀏覽器和行動裝置。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="9b6a6-253">對 OAuth 2.0 的支援基於 Microsoft OWIN 元件為承載身份驗證和實現授權伺服器角色而提供的新安全中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="9b6a6-254">或者,可以使用組織授權伺服器(如 Windows Server 2012 R2 中的 Azure 活動目錄或 ADFS)授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="9b6a6-255">O 資料改進</span><span class="sxs-lookup"><span data-stu-id="9b6a6-255">OData Improvements</span></span>

<span data-ttu-id="9b6a6-256">**支援$select、$expand、$batch和$value**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="9b6a6-257">ASP.NET Web API OData 現在完全支援$select、$expand和$value。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="9b6a6-258">您還可以使用$batch請求批處理和處理更改集。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="9b6a6-259">$select和$expand選項允許您更改從 OData 終結點傳回的數據的形狀。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="9b6a6-260">有關詳細資訊,請參閱在[Web API OData 中介紹$select 和$expand支援](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="9b6a6-261">**提高可擴充性**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-261">**Improved extensibility**</span></span>

<span data-ttu-id="9b6a6-262">OData for 物質現在可擴展。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="9b6a6-263">您可以添加 Atom 條目元數據、支援命名串流和媒體連結項目、添加實例註釋以及自訂連結的生成方式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="9b6a6-264">**沒有類型支援**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-264">**Type-less support**</span></span>

<span data-ttu-id="9b6a6-265">現在,您可以構建 OData 服務,而無需為實體類型定義 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="9b6a6-266">相反,您的 OData 控制器可以獲取或返回**IEdmObject**的實例 ,這是用於序列化/反序列化的 OData 實例。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="9b6a6-267">**重用現有模型**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-267">**Reuse an existing model**</span></span>

<span data-ttu-id="9b6a6-268">如果您已有現有的實體數據模型 (EDM),現在可以直接重用它,而不必構建新的實體數據模型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="9b6a6-269">例如,如果您使用的是實體框架,則可以使用 EF 為您生成的 EDM。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="9b6a6-270">要求處理</span><span class="sxs-lookup"><span data-stu-id="9b6a6-270">Request Batching</span></span>

<span data-ttu-id="9b6a6-271">請求批處理將多個操作合併到單個 HTTP POST 請求中,以減少網路流量並提供更順暢、更不健談的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="9b6a6-272">ASP.NET Web API 現在支援幾種要求批次處理策略:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="9b6a6-273">使用 OData 服務$batch終結點。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="9b6a6-274">將多個請求打包到單個 MIME 多部分請求中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="9b6a6-275">使用自定義批處理格式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-275">Use a custom batching format.</span></span>

<span data-ttu-id="9b6a6-276">要啟用要求批次處理,只需將具有批次處理處理程式的路由新增到 Web API 設定中:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="9b6a6-277">您還可以控制請求或按順序執行,還是按任何順序執行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="9b6a6-278">可移植ASP.NET Web API 用戶端</span><span class="sxs-lookup"><span data-stu-id="9b6a6-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="9b6a6-279">現在,可以使用ASP.NET Web API 用戶端創建跨 Windows 應用商店和 Windows Phone 8 應用程式的便攜式類庫。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="9b6a6-280">您還可以創建可在用戶端和伺服器之間共用的可移植的要件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="9b6a6-281">提高可測試性</span><span class="sxs-lookup"><span data-stu-id="9b6a6-281">Improved Testability</span></span>

<span data-ttu-id="9b6a6-282">Web API 2 使單元測試 API 控制器變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="9b6a6-283">只需使用請求消息和配置實例化 API 控制器,然後調用要測試的操作方法。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="9b6a6-284">對於執行連結生成的操作方法,也很容易類比**UrlHelper**類。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="9b6a6-285">IHTTPAction 結果</span><span class="sxs-lookup"><span data-stu-id="9b6a6-285">IHttpActionResult</span></span>

<span data-ttu-id="9b6a6-286">現在,您可以實現 IHttpActionResult 來封裝 Web API 操作方法的結果。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="9b6a6-287">從 Web API 操作方法傳回的 IHttpActionResult 由 ASP.NET Web API 執行時執行,以生成產生的回應消息。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="9b6a6-288">可以從任何 Web API 操作傳回 IHttpActionResult,以簡化 Web API 實現單元測試。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="9b6a6-289">為方便起見,一些IHttpActionResult實現在開箱即用,包括用於返回特定狀態代碼、格式化內容或內容協商回應的結果。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="9b6a6-290">HTTPRequestContext</span><span class="sxs-lookup"><span data-stu-id="9b6a6-290">HttpRequestContext</span></span>

<span data-ttu-id="9b6a6-291">新的**HttpRequestContext**追蹤與請求關聯的任何狀態,但無法立即從請求中獲取。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="9b6a6-292">例如,可以使用**HttpRequestContext**獲取路由資料、與請求關聯的主體、用戶端證書 **、UrlHelper**和虛擬路徑根。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="9b6a6-293">您可以輕鬆地為單元測試目的創建**HTTPRequestContext。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="9b6a6-294">由於請求的主體隨請求一起流動,而不是依賴於**Thread.CurrentThe,** 因此主體現在在請求在 Web API 管道中時在請求的整個生存期內可用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="9b6a6-295">CORS</span><span class="sxs-lookup"><span data-stu-id="9b6a6-295">CORS</span></span>

<span data-ttu-id="9b6a6-296">多虧了布羅克·艾倫的另一個巨大貢獻,ASP.NET現在完全支援跨原請求共用 (CORS)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="9b6a6-297">瀏覽器安全性可防止網頁對另一個網域提出 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="9b6a6-298">[CORS](http://www.w3.org/TR/cors/)是一種 W3C 標準,允許伺服器放鬆同源策略。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="9b6a6-299">使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="9b6a6-300">Web API 2 現在支援 CORS,包括自動處理預檢請求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="9b6a6-301">如需詳細資訊，請參閱 [在 ASP.NET Web API 中啟用跨原始來源要求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="9b6a6-302">驗證篩選器</span><span class="sxs-lookup"><span data-stu-id="9b6a6-302">Authentication Filters</span></span>

<span data-ttu-id="9b6a6-303">驗證篩選器是 web API 中 ASP.NET 一種新型篩選器,在 ASP.NET Web API 管道中授權篩選器之前運行,允許您為所有控制器指定每個操作、每個控制器或全域的身份驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="9b6a6-304">身份驗證篩選器處理請求中的憑據並提供相應的主體。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="9b6a6-305">身份驗證篩選器還可以添加身份驗證質詢以回應未經授權的請求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="9b6a6-306">篩選器覆寫</span><span class="sxs-lookup"><span data-stu-id="9b6a6-306">Filter Overrides</span></span>

<span data-ttu-id="9b6a6-307">現在,可以通過指定重寫篩選器來覆蓋應用於給定操作方法或控制器的篩選器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="9b6a6-308">覆蓋篩選器指定一組不應為給定作用域(操作或控制器)運行的篩選器類型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="9b6a6-309">這允許您添加全域篩選器,但隨後從特定操作或控制器中排除某些篩選器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="9b6a6-310">OWIN 整合</span><span class="sxs-lookup"><span data-stu-id="9b6a6-310">OWIN Integration</span></span>

<span data-ttu-id="9b6a6-311">ASP.NET Web API 現在完全支援 OWIN,可以在任何支援 OWIN 的主機上運行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="9b6a6-312">還包括一個**主機身份驗證篩選器**,它提供與 OWIN 身份驗證系統的集成。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="9b6a6-313">通過 OWIN 整合,您可以與其他 OWIN 中間件(如 SignalR)一起,在您自己的進程中自行託管 Web API。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="9b6a6-314">有關詳細資訊,請參閱使用[OWIN ASP.NET Web API 進行自託管](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="9b6a6-315">ASP.NET信號R 2.0</span><span class="sxs-lookup"><span data-stu-id="9b6a6-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="9b6a6-316">以下各節介紹 SignalR 2.0 的功能。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="9b6a6-317">基於 OWIN 建譯</span><span class="sxs-lookup"><span data-stu-id="9b6a6-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="9b6a6-318">地圖集線與地圖連線現在是對應訊號</span><span class="sxs-lookup"><span data-stu-id="9b6a6-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="9b6a6-319">跨域支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="9b6a6-320">透過單點觸控和單體機器人支援 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="9b6a6-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="9b6a6-321">可攜式 .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="9b6a6-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="9b6a6-322">新的自主機包</span><span class="sxs-lookup"><span data-stu-id="9b6a6-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="9b6a6-323">向後相容的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="9b6a6-324">已移除此.NET 4.0 的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="9b6a6-325">將訊息傳送到客戶端及群組清單</span><span class="sxs-lookup"><span data-stu-id="9b6a6-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="9b6a6-326">傳送使用者傳送訊息</span><span class="sxs-lookup"><span data-stu-id="9b6a6-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="9b6a6-327">更好的錯誤處理支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="9b6a6-328">更簡便的集線器單元測試</span><span class="sxs-lookup"><span data-stu-id="9b6a6-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="9b6a6-329">JavaScript 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="9b6a6-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="9b6a6-330">有關如何將現有的 1.x 專案升級到 SignalR 2.0 的範例,請參閱[升級 SignalR 1.x 專案](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="9b6a6-331">基於 OWIN 建譯</span><span class="sxs-lookup"><span data-stu-id="9b6a6-331">Built on OWIN</span></span>

<span data-ttu-id="9b6a6-332">SignalR 2.0 完全基於[OWIN(.NET 的開放 Web 介面)](http://owin.org/)構建。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="9b6a6-333">此更改使 SignalR 的設定過程在 Web 託管和自託管 SignalR 應用程式之間更加一致,但還需要多次 API 更改。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="9b6a6-334">地圖集線與地圖連線現在是對應訊號</span><span class="sxs-lookup"><span data-stu-id="9b6a6-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="9b6a6-335">為了與 OWIN 標準相容,這些方法已重新`MapSignalR`命名為 。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="9b6a6-336">`MapSignalR`在沒有參數的情況下調用將映射所有中心(如`MapHubs`版本1.x);映射單個**持久連接**物件,將連接類型指定為類型參數,並將連接的 URL 擴展作為第一個參數。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="9b6a6-337">該方法`MapSignalR`在 Owin 啟動類中調用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="9b6a6-338">Visual Studio 2013 包含 Owin 啟動類的新範本;要使用此樣本,請使用以下操作:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="9b6a6-339">右鍵單擊項目</span><span class="sxs-lookup"><span data-stu-id="9b6a6-339">Right-click on the project</span></span>
2. <span data-ttu-id="9b6a6-340">選擇 **'新增\*\*\*\*',新專案...**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="9b6a6-341">選擇**Owin 啟動類別**。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="9b6a6-342">Startup.cs命名**新類。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="9b6a6-343">在**Web 應用程式中,**`MapSignalR`包含該方法 的 Owin 啟動類別後使用 Web.Config 檔的應用程式設定節點中的條目添加到 Owin 的啟動過程中,如下所示。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="9b6a6-344">在**自託管應用程式中**,啟動類作為`WebApp.Start`方法的類型參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="9b6a6-345">**映射 SignalR 1.x 中的集線器與連線(來自 Web 應用程式中的全域應用程式檔案):**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="9b6a6-346">**映射 SignalR 2.0 中的集線器與連線(來自 Owin 啟動類別):**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="9b6a6-347">在**自託管應用程式中**,啟動類`WebApp.Start`作為 方法的類型參數傳遞,如下所示。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="9b6a6-348">跨域支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-348">Cross-Domain Support</span></span>

<span data-ttu-id="9b6a6-349">在 SignalR 1.x 中,跨域請求由單個啟用 CrossDomain 標誌控制。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="9b6a6-350">此標誌同時控制 JSONP 和 CORS 請求。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="9b6a6-351">為了更靈活,所有 CORS 支援都從 SignalR 的伺服器元件中刪除(如果檢測到瀏覽器支援它,JAVAScript 用戶端仍通常使用 CORS),並且新的 OWIN 中間件已可用於支援這些方案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="9b6a6-352">在 SignalR 2.0 中,如果用戶端上需要 JSONP(以支援舊瀏覽器中的跨域請求),`EnableJSONP``HubConfiguration`則`true`需要通過在 物件 上設置為 (如下所示)顯式啟用它。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="9b6a6-353">默認情況下禁用 JSONP,因為它的安全性低於 CORS。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="9b6a6-354">要在 SignalR 2.0 中添加`Microsoft.Owin.Cors`新的 CORS 中間件,`UseCors`請將庫添加到 專案中,並在 SignalR 中間件之前調用,如下節所示。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="9b6a6-355">**將 Microsoft.Owin.Cors 新增到您的專案**:要安裝此庫,請在套件管理員控制台中執行以下指令:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="9b6a6-356">此命令會將包的 2.0.0 版本添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="9b6a6-357">**呼叫使用參數**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-357">**Calling UseCors**</span></span>

<span data-ttu-id="9b6a6-358">以下代碼段演示如何在 SignalR 1.x 和 2.0 中實現跨域連接。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="9b6a6-359">**在 SignalR 1.x 中實現跨網域要求 (來自全域應用程式檔案)**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="9b6a6-360">**在 SignalR 2.0 中實現跨網域要求 (來自 C# 代碼檔案)**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="9b6a6-361">以下代碼展示如何在 SignalR 2.0 專案中啟用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="9b6a6-362">此代碼示例使用`Map``RunSignalR``MapSignalR`而不是 ,以便 CORS 中間件僅運行需要 CORS 支援的 SignalR 請求(而不是針對中`MapSignalR`指定的路徑上的所有流量)。`Map`還可用於需要為特定 URL 首碼運行的任何其他中間件,而不是整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="9b6a6-363">透過單點觸控和單體機器人支援 iOS 和 Android</span><span class="sxs-lookup"><span data-stu-id="9b6a6-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="9b6a6-364">已使用[Xamarin 庫中](https://xamarin.com/)的 MonoTouch 和 MonoDroid 元件為 iOS 和 Android 用戶端添加了支援。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="9b6a6-365">有關如何使用它們的詳細資訊,請參閱[使用 Xamarin 元件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="9b6a6-366">當 SignalR RTW 版本可用時,這些元件將在[Xamarin 儲存](https://store.xamarin.com/)中可用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="9b6a6-367">• 可移植 .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="9b6a6-367">### Portable .NET client</span></span>

<span data-ttu-id="9b6a6-368">為了更好地促進跨平台開發,Silverlight、WinRT 和 Windows Phone 用戶端已替換為支援以下平臺的單個可攜式 .NET 用戶端:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="9b6a6-369">淨 4.5</span><span class="sxs-lookup"><span data-stu-id="9b6a6-369">NET 4.5</span></span>
- <span data-ttu-id="9b6a6-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="9b6a6-370">Silverlight 5</span></span>
- <span data-ttu-id="9b6a6-371">WinRT (.NET 用於 Windows 應用商店應用)</span><span class="sxs-lookup"><span data-stu-id="9b6a6-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="9b6a6-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9b6a6-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="9b6a6-373">新的自主機包</span><span class="sxs-lookup"><span data-stu-id="9b6a6-373">New Self-Host Package</span></span>

<span data-ttu-id="9b6a6-374">現在有一個 NuGet 套件,以便更輕鬆地開始使用 SignalR 自主機(託管在行程或其他應用程式中的 SignalR 應用程式,而不是託管在 Web 伺服器中)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="9b6a6-375">要升級使用 SignalR 1.x 構建的自主機專案,請刪除 Microsoft.AspNet.SignalR.Owin 包,然後添加 Microsoft.AspNet.SignalR.SelfHost 包。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="9b6a6-376">有關開始使用自主機包的詳細資訊,請參閱[教程:SignalR 自主機](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="9b6a6-377">向後相容的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-377">Backward-compatible server support</span></span>

<span data-ttu-id="9b6a6-378">在早期版本的 SignalR 中,用戶端和伺服器中使用的 SignalR 套件版本需要相同。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="9b6a6-379">為了支援難以更新的粗用戶端應用程式,SignalR 2.0 現在支援使用較新的伺服器版本與較舊的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="9b6a6-380">**注意:SignalR 2.0 不支援使用較舊版本的較舊用戶端構建的伺服器。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="9b6a6-381">已移除此.NET 4.0 的伺服器支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="9b6a6-382">SignalR 2.0 已放棄對伺服器與 .NET 4.0 的互通性的支援。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="9b6a6-383">.NET 4.5 必須與 SignalR 2.0 伺服器一起使用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="9b6a6-384">信號R 2.0 仍有 .NET 4.0 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="9b6a6-385">將訊息傳送到客戶端及群組清單</span><span class="sxs-lookup"><span data-stu-id="9b6a6-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="9b6a6-386">在 SignalR 2.0 中,可以使用用戶端和組 IT 的清單發送消息。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="9b6a6-387">以下代碼段演示如何執行此操作。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="9b6a6-388">**使用持久連線將訊息傳送到客戶端及群組清單**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="9b6a6-389">**使用中心向客戶端及群組清單傳送訊息**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="9b6a6-390">傳送使用者傳送訊息</span><span class="sxs-lookup"><span data-stu-id="9b6a6-390">Sending a message to a specific user</span></span>

<span data-ttu-id="9b6a6-391">此功能允許使用者透過新介面 IUserIdProvider 指定使用者 Id 基於 IRequest 的內容:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="9b6a6-392">**IUserId 提供者介面**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="9b6a6-393">默認情況下,將有一個使用使用者IPrincipal.Identity.Name作為使用者名的實現。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="9b6a6-394">在集線器中,您可以透過新的 API 向這些使用者傳送訊息:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="9b6a6-395">**使用用戶端.使用者 API**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="9b6a6-396">更好的錯誤處理支援</span><span class="sxs-lookup"><span data-stu-id="9b6a6-396">Better Error Handling Support</span></span>

<span data-ttu-id="9b6a6-397">用戶現在可以從任何中心調用中引發**HubException。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="9b6a6-398">**HubException**的建構函數可以獲取字串訊息和物件額外的錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="9b6a6-399">SignalR 將自動序列化異常並將其發送到用戶端,其中它將用於拒絕/拒絕中心方法調用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="9b6a6-400">**顯示詳細的集線器異常**設置與**HubException**被發送回客戶端無關;它總是發送。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="9b6a6-401">**顯示傳送到客戶端傳送 Hubexception 的伺服器端碼**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="9b6a6-402">**顯示回應從伺服器傳送的 HubException 的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="9b6a6-403">**.NET 用戶端代碼,用於回應從伺服器傳送的 HubException**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="9b6a6-404">更簡便的集線器單元測試</span><span class="sxs-lookup"><span data-stu-id="9b6a6-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="9b6a6-405">SignalR 2.0`IHubCallerConnectionContext`包括一 個在集線器上調用的介面,該介面使創建類比用戶端調用變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="9b6a6-406">以下程式碼段展示使用此介面與流行的測試工具[xUnit.net](https://github.com/xunit/xunit)與[moq](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="9b6a6-407">**帶xUnit.net的單元測試訊號R**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="9b6a6-408">**使用 moq 進行單元測試訊號R**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="9b6a6-409">JavaScript 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="9b6a6-409">JavaScript error handling</span></span>

<span data-ttu-id="9b6a6-410">在 SignalR 2.0 中,所有 JavaScript 錯誤處理回調返回 JavaScript 錯誤物件,而不是原始字串。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="9b6a6-411">這允許 SignalR 將更豐富的資訊流向錯誤處理程式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="9b6a6-412">可以從錯誤的`source`屬性中獲取內部異常。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="9b6a6-413">**處理 Start.Fail 異常的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="9b6a6-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="9b6a6-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="9b6a6-415">新的ASP.NET會員制</span><span class="sxs-lookup"><span data-stu-id="9b6a6-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="9b6a6-416">ASP.NET身份是ASP.NET應用程式的新成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="9b6a6-417">ASP.NET識別使用戶特定的配置檔數據與應用程序資料整合變得容易。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="9b6a6-418">ASP.NET識別還允許您為應用程式中的使用者配置檔選擇持久性模型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="9b6a6-419">您可以將資料儲存在 SQL Server 資料庫或其他資料存放區中，包括 NoSQL 資料存放區 (例如 Azure 儲存體資料表)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="9b6a6-420">有關詳細資訊,請參閱**可視化工作室 2013 中創建ASP.NET Web 專案的**[單個使用者帳戶](creating-web-projects-in-visual-studio.md#indauth)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="9b6a6-421">宣告架構驗證</span><span class="sxs-lookup"><span data-stu-id="9b6a6-421">Claims-based authentication</span></span>

<span data-ttu-id="9b6a6-422">ASP.NET現在支援基於聲明的身份驗證,其中使用者的身份表示為來自受信任頒發者的一組聲明。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="9b6a6-423">使用者可以使用應用程式資料庫中維護的使用者名稱和密碼進行身份驗證,或使用社交身份提供者(例如:微軟帳戶、Facebook、Google、Twitter),或者透過 Azure 活動目錄或活動目錄聯合服務 (ADFS) 使用組織帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="9b6a6-424">與 Azure 的目錄與 Windows 伺服器活動目錄整合</span><span class="sxs-lookup"><span data-stu-id="9b6a6-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="9b6a6-425">現在,您可以創建ASP.NET使用Azure活動目錄或Windows伺服器活動目錄 (AD) 進行身份驗證的專案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="9b6a6-426">有關詳細資訊,請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案的**[組織帳戶](creating-web-projects-in-visual-studio.md#orgauth)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="9b6a6-427">OWIN 整合</span><span class="sxs-lookup"><span data-stu-id="9b6a6-427">OWIN Integration</span></span>

<span data-ttu-id="9b6a6-428">ASP.NET身份驗證現在基於OWIN中間件,可用於任何基於OWIN的主機。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="9b6a6-429">有關 OWIN 的詳細資訊,請參閱以下[Microsoft OWIN 元件](#TOC7)部分。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="9b6a6-430">Microsoft OWIN 元件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="9b6a6-431">[.NET](http://owin.org/) (OWIN) 的開放 Web 介面定義 .NET Web 伺服器和 Web 應用程式之間的抽象。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="9b6a6-432">OWIN 將 Web 應用程式與伺服器分離,使 Web 應用程式與主機無關。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="9b6a6-433">例如,您可以在 IIS 中託管基於 OWIN 的 Web 應用程式,也可以在自訂進程中自承載它。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="9b6a6-434">Microsoft OWIN 元件(也稱為 Katana 專案)中引入的更改包括新的伺服器和主機組件、新的幫助器庫和中間件以及新的身份驗證中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="9b6a6-435">有關 OWIN 和卡塔納的更多資訊,請參閱[OWIN 和卡塔納中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="9b6a6-436">**注意[:OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式無法在 IIS 經典模式下運行;它們必須在集成模式下運行。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="9b6a6-437">**注意[:OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式必須完全信任地運行。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="9b6a6-438">新伺服器和主機</span><span class="sxs-lookup"><span data-stu-id="9b6a6-438">New Servers and Hosts</span></span>

<span data-ttu-id="9b6a6-439">使用此版本,添加了新的元件以啟用自承載方案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="9b6a6-440">這些元件包括以下 NuGet 套件:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="9b6a6-441">**微軟.Owin.Host.HTTPListener**.</span><span class="sxs-lookup"><span data-stu-id="9b6a6-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="9b6a6-442">提供一個 OWIN 伺服器,該伺服器使用**HttpListener**偵聽 HTTP 請求並將其定向到 OWIN 管道中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="9b6a6-443">**Microsoft.Owin.Hosting**為希望在自定義進程中自承載 OWIN 管道(如控制台應用程式或 Windows 服務)的開發人員提供一個庫。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="9b6a6-444">**奧溫霍斯**。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-444">**OwinHost**.</span></span> <span data-ttu-id="9b6a6-445">提供一個獨立的可執行檔,用於包裝`Microsoft.Owin.Hosting`並允許您自承載 OWIN 管道,而無需編寫自定義主機應用程式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="9b6a6-446">此外,`Microsoft.Owin.Host.SystemWeb`該包現在使中間件能夠向**SystemWeb**伺服器提供提示,指示應在特定的 ASP.NET 管道階段調用中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="9b6a6-447">此功能對於身份驗證中間件特別有用,該中間件應在ASP.NET管道中早期運行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="9b6a6-448">說明庫和中間件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="9b6a6-449">儘管只能使用 OWIN 規範中的函數和類型定義編寫 OWIN 元件`Microsoft.Owin`,但新 包提供了一組更使用者友好的抽象。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="9b6a6-450">此包將幾個較早的包(例如 ,)`Owin.Extensions``Owin.Types`合併到單個結構良好的物件模型中,然後其他 OWIN 元件可以輕鬆地使用該模型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="9b6a6-451">事實上,大多數 Microsoft OWIN 元件現在都使用此包。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="9b6a6-452">[OWIN](http://www.owin.org)應用程式無法在IIS經典模式下運行;它們必須在集成模式下運行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="9b6a6-453">[OWIN](http://www.owin.org)應用程式必須完全信任地運行。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="9b6a6-454">此版本還包括 Microsoft.Owin.診斷包,其中包括用於驗證正在運行的 OWIN 應用程式的中間件,以及幫助調查故障的錯誤頁中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="9b6a6-455">驗證元件</span><span class="sxs-lookup"><span data-stu-id="9b6a6-455">Authentication Components</span></span>

<span data-ttu-id="9b6a6-456">以下身份驗證元件可用。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-456">The following authentication components are available.</span></span>

- <span data-ttu-id="9b6a6-457">**微軟.Owin.安全.主動目錄**.</span><span class="sxs-lookup"><span data-stu-id="9b6a6-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="9b6a6-458">使用內部部署或基於雲端的目錄服務啟用身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="9b6a6-459">**微軟.Owin.Security.cookies**支援使用Cookie進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="9b6a6-460">此套件以前命名為`Microsoft.Owin.Security.Forms`。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="9b6a6-461">**微軟.Owin.Security.Facebook**使用Facebook基於OAuth的服務啟用身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="9b6a6-462">**微軟.Owin.Security.谷歌**使用谷歌基於OpenID的服務啟用身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="9b6a6-463">**微軟.Owin.Security.Jwt**啟用使用 JWT 令牌的身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="9b6a6-464">**微軟.Owin.Security.微軟帳戶**啟用使用微軟帳戶進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="9b6a6-465">**微軟.奧溫.安全.奧烏斯**.</span><span class="sxs-lookup"><span data-stu-id="9b6a6-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="9b6a6-466">提供 OAuth 授權伺服器以及用於驗證無記名權杖的中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="9b6a6-467">**微軟.Owin.Security.Twitter**使用Twitter基於OAuth的服務進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="9b6a6-468">此版本還包括包`Microsoft.Owin.Cors`,其中包含用於處理跨源 HTTP 請求的中間件。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="9b6a6-469">在 Visual Studio 2013 的最終版本中刪除了對 JWT 簽名的支援。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="9b6a6-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="9b6a6-470">Entity Framework 6</span></span>

<span data-ttu-id="9b6a6-471">有關實體框架 6 中的新功能和其他更改的清單,請參閱[實體框架版本歷史記錄](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="9b6a6-472">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="9b6a6-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="9b6a6-473">ASP.NET Razor 3 包括以下新功能:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="9b6a6-474">支援選項卡編輯。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-474">Support for Tab editing.</span></span> <span data-ttu-id="9b6a6-475">以前,使用「**保留選項卡**」選項時,Visual Studio 中的 **「格式文檔**」指令、自動縮進和自動格式設定無法正常工作。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="9b6a6-476">此更改糾正了用於選項卡格式的 Razor 代碼的可視化工作室格式。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="9b6a6-477">生成連結時支援 URL 重寫規則。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="9b6a6-478">刪除安全透明屬性。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="9b6a6-479">這是一個重大更改,使 Razor 3 與 MVC4 和更早版本不相容,而 Razor 2 與 MVC5 或針對 MVC5 編譯的程式集不相容。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="9b6a6-480">Razor 3 問題修復在 Visual Studio 2013 從預發行版本可以[在這裡](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到.</span><span class="sxs-lookup"><span data-stu-id="9b6a6-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="9b6a6-481">ASP.NET應用程式掛起</span><span class="sxs-lookup"><span data-stu-id="9b6a6-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="9b6a6-482">ASP.NET應用程式掛起是 .NET Framework 4.5.1 中的一項改變遊戲規則的功能,它從根本上改變了在一台電腦上託管大量ASP.NET網站的使用者體驗和經濟模型。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="9b6a6-483">有關詳細資訊,請參閱[ASP.NET 應用程式掛起 – 回應式共用 .NET Web 託管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="9b6a6-484">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="9b6a6-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="9b6a6-485">本節介紹視覺工作室 2013 ASP.NET和 Web 工具中的已知問題和重大更改。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="9b6a6-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="9b6a6-486">NuGet</span></span>

- <span data-ttu-id="9b6a6-487">[使用 SLN 檔時,新包還原在 Mono 上不起作用](https://nuget.codeplex.com/workitem/3596), 將在即將進行的 nuget.exe 下載和[NuGet.CommandLine 套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修復。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="9b6a6-488">[新的包還原與 Wix 專案不起作用](https://nuget.codeplex.com/workitem/3598)- 將在即將進行的 nuget.exe 下載和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修復。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="9b6a6-489">[自動包還原在解決方案資料夾下的專案不起作用](https://nuget.codeplex.com/workitem/3625), 將在 NuGet 2.8 中修復。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="9b6a6-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="9b6a6-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="9b6a6-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`不會總是返回`IQueryable<T>`,因為我們添加了`$select``$expand`對和的支援。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="9b6a6-492">我們以前的樣本`ODataQueryOptions<T>`總是將傳回值`ApplyTo`從`IQueryable<T>`轉換為 。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="9b6a6-493">這在早期`$filter`起作用,因為我們支援之前的查詢選項 (、、、、)`$orderby``$skip``$top`不會更改查詢的形狀。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="9b6a6-494">`$select`現在,我們支援`$expand`,並`ApplyTo`從返回值`IQueryable<T>`將 並不總是。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="9b6a6-495">如果使用之前的範例代碼,則如果用戶端未發送`$select`和`$expand`,它將繼續工作。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="9b6a6-496">但是,如果您希望支援`$select`,`$expand`並且必須將該代碼更改為此代碼。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="9b6a6-497">**要求.網址或要求上下文.網址在批次處理請求期間為空**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="9b6a6-498">在批次處理方案中 **,UrlHelper**從**請求.Url**或**請求上下文.網址**存取時為空。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="9b6a6-499">此問題目前在此處追蹤[:BatchRequestContext.網址 對於批次處理請求為空](http://aspnetwebstack.codeplex.com/workitem/1301)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="9b6a6-500">此問題的解決方法是建立**UrlHelper**的新實體,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="9b6a6-501">**建立 UrlHelper 的新實體**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="9b6a6-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="9b6a6-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="9b6a6-503">使用 MVC5 與 OrgAuth 時,如果您有執行 AntiForgerToken 驗證的檢視,則當您將資料發布到檢視時,可能會遇到以下錯誤:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="9b6a6-504">**錯誤**：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-504">**Error**:</span></span>

    <span data-ttu-id="9b6a6-505">*'/' 應用程式中有伺服器錯誤。*</span><span class="sxs-lookup"><span data-stu-id="9b6a6-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="9b6a6-506"><em>所提供的索賠身份上不存在<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>類型"<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>或""的索賠。要使用基於聲明的身份驗證啟用反偽造權杖支援,請驗證已配置的聲明提供者是否在它生成的聲明標識實例上同時提供這兩種聲明。如果配置的聲明提供者使用不同的聲明類型作為唯一識別碼,則可以透過設定靜態屬性 AntiForgeryConfig.唯一ClaimType標識符來配置它。</em></span><span class="sxs-lookup"><span data-stu-id="9b6a6-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="9b6a6-507">**因應措施**：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-507">**Workaround**:</span></span>

    <span data-ttu-id="9b6a6-508">在 Global.asax 中新增以下行以修復它:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="9b6a6-509">這將在下一個版本中修復。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="9b6a6-510">將 MVC4 應用升級到 MVC5 後,生成解決方案並啟動它。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="9b6a6-511">您應該會看到以下錯誤:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-511">You should see the following error:</span></span>

    <span data-ttu-id="9b6a6-512">[A]系統.Web.WebPages.Razor.配置.Host節不能強制轉換為 [B_system.Web.Web.WebPages.Razor.配置.主機節。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="9b6a6-513">類型 A 源自 "系統.Web.WebPages.Razor" 版本=2.0.0.0,區域性=中性,PublicKeyToken=31bf3856ad364e35"在上下文\_"預設"的位置 "C:_windows.Net_大會_GAC MSIL_System.WebPages.Razor_v4.0.0\_\_\_31bf3856ad36e35_系統.WebPages.剃鬚刀.剃鬚刀。"</span><span class="sxs-lookup"><span data-stu-id="9b6a6-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="9b6a6-514">類型 B 源自 'System.Web.WebPages.Razor, 版本=3.0.0.0, 區域性= 中性, PublicKeyToken_31bf3856ad364e35"在上下文"預設"的位置"C:_Windows_Microsoft.NET_Framework_v4.0.30319\臨時ASP.NET檔\root_6d 05bbd0_e8b5908e_assembly_dl3_c9cbca63_f8910382\_6273ce01_System.WebPages.Razor.dll'。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="9b6a6-515">要修復上述錯誤,請開啟項目中*的所有*Web.config 檔(包括"檢視'資料夾中的檔案),並執行以下操作:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="9b6a6-516">將"System.Web.Mvc"版本"4.0.0.0"的所有匹配項更新為"5.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="9b6a6-517">更新&quot;系統.Web.Helpers"、系統.Web.WebPages&quot;和&quot;系統.Web.WebPages.Razor&quot;到"3.0.0.0"版本的所有匹配項</span><span class="sxs-lookup"><span data-stu-id="9b6a6-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="9b6a6-518">例如,在進行上述更改後,程式集綁定應如下所示:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="9b6a6-519">有關將 MVC 4 專案升級到 MVC 5 的資訊,請參閱[如何將 ASP.NET MVC 4 和 Web API 專案升級到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="9b6a6-520">當將客戶端驗證與 jQuery 不顯眼驗證一起使用時,對於類型="數位"的 HTML 輸入元素,驗證消息有時不正確。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="9b6a6-521">輸入無效號碼時將顯示所需值的驗證錯誤("需要"年齡欄位),而不是需要有效編號的正確消息。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="9b6a6-522">在"創建"和"編輯"檢視中具有整數屬性的模型的腳手架代碼通常會產生此問題。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="9b6a6-523">要解決此問題,從以下方面更改編輯器説明程式:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="9b6a6-524">變更為：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="9b6a6-525">ASP.NET MVC 5 不再支援部分信任。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="9b6a6-526">連結到 MVC 或 WebAPI 二進位檔案的專案應刪除[安全透明](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)屬性和[「允許部分受信任的呼叫者」](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="9b6a6-527">刪除這些屬性將消除編譯器錯誤,如下所示。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="9b6a6-528">請注意,作為副作用,您不能在同一應用程式中使用 4.0 和 5.0 程式集。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="9b6a6-529">您需要將所有它們更新為 5.0。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="9b6a6-530">具有 Facebook 授權的 SPA 樣本可能會導致 IE 不穩定,而網站託管在 Intranet 區域中</span><span class="sxs-lookup"><span data-stu-id="9b6a6-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="9b6a6-531">SPA 模板提供帶 Facebook 的外部登錄。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="9b6a6-532">當使用範本創建的專案在本地運行時,登錄可能會導致 IE 崩潰。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="9b6a6-533">解決方案：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-533">Solution:</span></span>

1. <span data-ttu-id="9b6a6-534">在互聯網區域託管網站;或</span><span class="sxs-lookup"><span data-stu-id="9b6a6-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="9b6a6-535">在 IE 以外的瀏覽器中測試方案。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="9b6a6-536">Web Forms Scaffolding</span><span class="sxs-lookup"><span data-stu-id="9b6a6-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="9b6a6-537">Web 窗體基架已從 VS2013 中刪除,將來將更新為 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="9b6a6-538">但是,您仍可以通過添加 MVC 依賴項和生成 MVC 基架來在 Web 窗體專案中使用基架。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="9b6a6-539">您的專案將包含 Web 窗體和 MVC 的組合。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="9b6a6-540">要將 MVC 新增到 Web 窗體專案,請新增新的文手架項目,然後選擇**MVC 5 相依項 。**</span><span class="sxs-lookup"><span data-stu-id="9b6a6-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="9b6a6-541">根據是否需要所有內容檔(如腳本)選擇"最小"或"完整"</span><span class="sxs-lookup"><span data-stu-id="9b6a6-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="9b6a6-542">然後,為 MVC 添加一個基架項,這將在專案中創建檢視和控制器。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="9b6a6-543">MVC 與 Web API 基架 - HTTP 404,找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="9b6a6-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="9b6a6-544">如果在向專案添加基架項時遇到錯誤,則專案可能會處於不一致狀態。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="9b6a6-545">對基架所做的一些更改將回滾,但其他更改(如已安裝的 NuGet 包)將不會回滾。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="9b6a6-546">如果路由配置更改回滾,則使用者在導航到基架專案時將收到 HTTP 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="9b6a6-547">因應措施：</span><span class="sxs-lookup"><span data-stu-id="9b6a6-547">Workaround:</span></span>

- <span data-ttu-id="9b6a6-548">要修復 MVC 的此錯誤,請添加新的腳手架項並選擇 MVC 5 依賴項(最小或完整)。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="9b6a6-549">此過程將添加專案所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="9b6a6-550">要修復 Web API 的此錯誤,本文:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="9b6a6-551">將 WebApiConfig 類添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="9b6a6-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="9b6a6-552">在 Global.asax\_中的應用程式 啟動方法中設定 WebApiConfig.註冊,如下所示:</span><span class="sxs-lookup"><span data-stu-id="9b6a6-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
