---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET和網络工具發行說明 2013.1 可視化工作室 2012 |微軟文件
author: rick-anderson
description: 本文件介紹了 Visual Studio 2012 的 ASP.NET 和網路工具 2013.1 的發佈。
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: d4aced4e77a150d52358c2d2513ff79e6594a9de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543570"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="5ab38-103">適用於 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1 版本資訊</span><span class="sxs-lookup"><span data-stu-id="5ab38-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="5ab38-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5ab38-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5ab38-105">本文件介紹了 Visual Studio 2012 的 ASP.NET 和網路工具 2013.1 的發佈。</span><span class="sxs-lookup"><span data-stu-id="5ab38-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="5ab38-106">內容</span><span class="sxs-lookup"><span data-stu-id="5ab38-106">Contents</span></span>

- [<span data-ttu-id="5ab38-107">安裝說明</span><span class="sxs-lookup"><span data-stu-id="5ab38-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="5ab38-108">軟體要求</span><span class="sxs-lookup"><span data-stu-id="5ab38-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="5ab38-109">視覺工作室 2012 年 ASP.NET 和網路工具 2013.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="5ab38-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="5ab38-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="5ab38-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="5ab38-111">範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="5ab38-112">ASP.NET MVC 5 樣本</span><span class="sxs-lookup"><span data-stu-id="5ab38-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="5ab38-113">ASP.NET Web API 2 範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="5ab38-114">專案範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="5ab38-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5ab38-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="5ab38-116">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="5ab38-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="5ab38-117">剃刀編輯器</span><span class="sxs-lookup"><span data-stu-id="5ab38-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="5ab38-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5ab38-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="5ab38-119">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="5ab38-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="5ab38-120">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="5ab38-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="5ab38-121">MVC 與 Web API 基架 - HTTP 404,找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="5ab38-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="5ab38-122">Visual Studio Express 2012 用於 Web 在新增文手架專案後停止工作</span><span class="sxs-lookup"><span data-stu-id="5ab38-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="5ab38-123">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="5ab38-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="5ab38-124">使用「使用」或「F5」檢視 cshtml 檔會導致伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="5ab38-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="5ab38-125">Url 重寫和蒂爾德 (\*)</span><span class="sxs-lookup"><span data-stu-id="5ab38-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="5ab38-126">範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="5ab38-127">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="5ab38-127">Installation Notes</span></span>

<span data-ttu-id="5ab38-128">[安裝](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids)ASP.NET和網路工具 2013.1 用於視覺工作室 2012。</span><span class="sxs-lookup"><span data-stu-id="5ab38-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="5ab38-129">軟體需求</span><span class="sxs-lookup"><span data-stu-id="5ab38-129">Software Requirements</span></span>

<span data-ttu-id="5ab38-130">您必須有 Visual Studio 2012 或 Visual Studio Express 2012 用於 Web。</span><span class="sxs-lookup"><span data-stu-id="5ab38-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="5ab38-131">視覺工作室 2012 年 ASP.NET 和網路工具 2013.1 中的新功能</span><span class="sxs-lookup"><span data-stu-id="5ab38-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="5ab38-132">啟動程序</span><span class="sxs-lookup"><span data-stu-id="5ab38-132">Bootstrap</span></span>

<span data-ttu-id="5ab38-133">當您文手架 MVC 5 控制器與檢視時,檢視的標記使用[Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="5ab38-134">範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="5ab38-135">ASP.NET MVC 5 樣本</span><span class="sxs-lookup"><span data-stu-id="5ab38-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="5ab38-136">我們添加了一個新的 MVC 5 範本。</span><span class="sxs-lookup"><span data-stu-id="5ab38-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="5ab38-137">它引用最新的 MVC 5 NuGet 套件,您可以使用基架添加控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="5ab38-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="5ab38-138">ASP.NET Web API 2 範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="5ab38-139">我們添加了一個新的 Web API 2 範本。</span><span class="sxs-lookup"><span data-stu-id="5ab38-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="5ab38-140">它引用最新的 Web API 2 NuGet 套件,您可以使用基架添加控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="5ab38-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="5ab38-141">項目範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-141">Item Templates</span></span>

<span data-ttu-id="5ab38-142">我們為 MVC 5 檢視、網頁 (Razor 3) 和 Web API 2 控制器添加了新的專案範本。</span><span class="sxs-lookup"><span data-stu-id="5ab38-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="5ab38-143">他們在添加新項的同時,將相關的 NuGet 包安裝到專案中。</span><span class="sxs-lookup"><span data-stu-id="5ab38-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="5ab38-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5ab38-144">Entity Framework 6</span></span>

<span data-ttu-id="5ab38-145">當您使用實體框架建構 MVC 或 Web API 控制器時,我們使用框架 6。</span><span class="sxs-lookup"><span data-stu-id="5ab38-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="5ab38-146">有關實體框架的詳細資訊,請參閱[實體框架版本歷史記錄](https://msdn.com/data/jj574253)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="5ab38-147">您還可以下載並安裝可視化工作室的實體框架 6 工具 2012。</span><span class="sxs-lookup"><span data-stu-id="5ab38-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="5ab38-148">請參考[實體框架](https://msdn.com/data/ee712906#tooling)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="5ab38-149">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="5ab38-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="5ab38-150">ASP.NET基架是ASP.NET Web 應用程式的代碼生成框架。</span><span class="sxs-lookup"><span data-stu-id="5ab38-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="5ab38-151">它可以輕鬆地向與數據模型交互的專案添加樣板代碼。</span><span class="sxs-lookup"><span data-stu-id="5ab38-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="5ab38-152">在 Visual Studio 的早期版本中,基架僅限於 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="5ab38-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="5ab38-153">使用此更新,您現在可以對任何ASP.NET專案(包括 Web 窗體)使用基架。</span><span class="sxs-lookup"><span data-stu-id="5ab38-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="5ab38-154">此更新不支援為 Web 窗體專案生成頁面,但仍可以通過向專案添加 MVC 依賴項來使用 Web 窗體的腳手架。</span><span class="sxs-lookup"><span data-stu-id="5ab38-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="5ab38-155">將在將來的更新中添加對生成 Web 窗體頁面的支援。</span><span class="sxs-lookup"><span data-stu-id="5ab38-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="5ab38-156">使用基架時,我們確保在專案中安裝了所有必需的依賴項。</span><span class="sxs-lookup"><span data-stu-id="5ab38-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="5ab38-157">例如,如果從ASP.NET Web 窗體專案開始,然後使用基架添加 Web API 控制器,則所需的 NuGet 包和引用將自動添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="5ab38-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="5ab38-158">要將 MVC 基架加入 Web 窗體專案,請新增**新的文手架,** 並在對話框視窗中選擇**MVC 5 相依項 。**</span><span class="sxs-lookup"><span data-stu-id="5ab38-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="5ab38-159">基架 MVC 有兩個選項;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="5ab38-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="5ab38-160">如果選擇「最小」,則只有 ASP.NET MVC 的 NuGet 包和引用添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="5ab38-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="5ab38-161">如果選擇"完整"選項,則添加最小依賴項以及 MVC 專案所需的內容檔。</span><span class="sxs-lookup"><span data-stu-id="5ab38-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="5ab38-162">支援基架非同步控制器使用實體框架6中的新異步功能。</span><span class="sxs-lookup"><span data-stu-id="5ab38-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="5ab38-163">有關詳細資訊和教程,請參閱[ASP.NET 腳手架概述](../2013/aspnet-scaffolding-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="5ab38-164">這些教程顯示了視覺工作室 2013 的腳手架,但它們也適用於 Visual Studio 2012 的ASP.NET和網路工具 2013.1。</span><span class="sxs-lookup"><span data-stu-id="5ab38-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="5ab38-165">剃刀編輯器</span><span class="sxs-lookup"><span data-stu-id="5ab38-165">Razor Editor</span></span>

<span data-ttu-id="5ab38-166">有了這個更新,Visual Studio 2012 現在支援 Razor 3 工具/編輯。</span><span class="sxs-lookup"><span data-stu-id="5ab38-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="5ab38-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5ab38-167">NuGet 2.7</span></span>

<span data-ttu-id="5ab38-168">NuGet 2.7 包含一組豐富的新功能,在[NuGet 2.7 發行說明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中對此進行了詳細介紹。</span><span class="sxs-lookup"><span data-stu-id="5ab38-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="5ab38-169">此版本的 NuGet 消除了使用者顯式允許 NuGet 還原缺少的包的需要。</span><span class="sxs-lookup"><span data-stu-id="5ab38-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="5ab38-170">安裝 NuGet 2.7 時,使用者隱式同意自動還原丟失的包。</span><span class="sxs-lookup"><span data-stu-id="5ab38-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="5ab38-171">使用者可以通過 Visual Studio 中的 NuGet 設定明確選擇退出包恢復。</span><span class="sxs-lookup"><span data-stu-id="5ab38-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="5ab38-172">此更改簡化了包還原的工作方式。</span><span class="sxs-lookup"><span data-stu-id="5ab38-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="5ab38-173">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="5ab38-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="5ab38-174">ASP.NET腳手架</span><span class="sxs-lookup"><span data-stu-id="5ab38-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="5ab38-175">MVC 與 Web API 基架 - HTTP 404,找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="5ab38-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="5ab38-176">如果在向專案添加基架項時遇到錯誤,則專案可能會處於不一致狀態。</span><span class="sxs-lookup"><span data-stu-id="5ab38-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="5ab38-177">對基架所做的一些更改將回滾,但其他更改(如已安裝的 NuGet 包)將不會回滾。</span><span class="sxs-lookup"><span data-stu-id="5ab38-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="5ab38-178">如果路由配置更改回滾,則使用者在導航到基架專案時將收到 HTTP 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="5ab38-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="5ab38-179">要修復 MVC 的此錯誤,請添加新的腳手架項並選擇 MVC 5 依賴項(最小或完整)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="5ab38-180">此過程將添加專案所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="5ab38-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="5ab38-181">要修復 Web API 的此錯誤,本文:</span><span class="sxs-lookup"><span data-stu-id="5ab38-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="5ab38-182">將以下 WebApiConfig 類添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="5ab38-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="5ab38-183">在 Global.asax\_中的應用程式 啟動方法中設定 WebApiConfig.註冊,如下所示:</span><span class="sxs-lookup"><span data-stu-id="5ab38-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="5ab38-184">Visual Studio Express 2012 用於 Web 在新增文手架專案後停止工作</span><span class="sxs-lookup"><span data-stu-id="5ab38-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="5ab38-185">如果 Web 的 Visual Studio Express 2012 在使用實體框架添加基架專案(例如 Web API 2 控制器具有操作的操作,使用實體框架)後停止工作,則 Visual Studio Express 可能無法載入依賴於 System.Web.擴展的程式集的本機映射。</span><span class="sxs-lookup"><span data-stu-id="5ab38-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="5ab38-186">要更正此問題,請將 Visual Studio Express 設定為使用 System.Web.擴展的 MSIL 映射:</span><span class="sxs-lookup"><span data-stu-id="5ab38-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="5ab38-187">在管理員模式下打開命令提示。</span><span class="sxs-lookup"><span data-stu-id="5ab38-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="5ab38-188">到 %程式檔案%\微軟視覺工作室 11.0_Common7_IDE 或 %程式檔 (x86)%\微軟視覺工作室 11.0_Common7_IDE (對於 64 位元視窗)。</span><span class="sxs-lookup"><span data-stu-id="5ab38-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="5ab38-189">在文字編輯器中打開 VWDExpress.exe.config。</span><span class="sxs-lookup"><span data-stu-id="5ab38-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="5ab38-190">&lt;&gt;在/&lt;設定&gt;執行時 元素下新增以下行:</span><span class="sxs-lookup"><span data-stu-id="5ab38-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="5ab38-191">重新啟動視覺化工作室快速 2012 為 Web.</span><span class="sxs-lookup"><span data-stu-id="5ab38-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="5ab38-192">ASP.NET剃刀 3</span><span class="sxs-lookup"><span data-stu-id="5ab38-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="5ab38-193">使用「使用」或「F5」檢視 cshtml 檔會導致伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="5ab38-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="5ab38-194">當您在 Visual Studio 2012 中創建 MVC 5 專案(或在 Visual Studio 2012 中打開在 Visual Studio 2013 中建立的 MVC 5 專案)並嘗試使用「瀏覽」或 F5 查看 cshtml 檔時,您將收到一個錯誤,指出 **"/' 應用程式中的伺服器錯誤**"。</span><span class="sxs-lookup"><span data-stu-id="5ab38-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="5ab38-195">伺服器試著瀏覽到`http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="5ab38-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="5ab38-196">要解決此問題,請將專案中的 **「開始操作」** 設定更改為 **「特定頁面**」 。</span><span class="sxs-lookup"><span data-stu-id="5ab38-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="5ab38-197">您無需為頁面提供值。</span><span class="sxs-lookup"><span data-stu-id="5ab38-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="5ab38-198">進行此變更後,選擇 F5 將瀏覽到應用程式`http://localhost:XXXX`的根目錄 ( 。</span><span class="sxs-lookup"><span data-stu-id="5ab38-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="5ab38-199">此行為與 Visual Studio 2013 中的 MVC 5 專案的行為不同,其中 **「當前頁面」** 設定將啟動打開頁面。</span><span class="sxs-lookup"><span data-stu-id="5ab38-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="5ab38-200">Url 重寫和蒂爾德 (\*)</span><span class="sxs-lookup"><span data-stu-id="5ab38-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="5ab38-201">升級到ASP.NET Razor 3 或 ASP.NET MVC 5 後,如果使用 URL 重寫,則波浪(\*)表示法可能不再正常工作。</span><span class="sxs-lookup"><span data-stu-id="5ab38-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="5ab38-202">URL 重寫會影響&lt;HTML 元素(如 A/、SCRIPT/、LINK/&gt;&lt;&gt;&lt;&gt;等)中的波浪線(\*)表示法,因此波浪線不再映射到根目錄。</span><span class="sxs-lookup"><span data-stu-id="5ab38-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="5ab38-203">例如,如果將**asp.net/content**請求重寫為**asp.net,**&lt;則 a href_"/內容/"中的 href 屬性將&gt;解析為 **/內容/內容/** 而不是**/**。</span><span class="sxs-lookup"><span data-stu-id="5ab38-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="5ab38-204">要禁止此更改,可以在每個網頁或 Global.asax 中的**\_應用程式 BeginRequest**中將**IIS\_WasUrl 重寫**上下文設置為 false。</span><span class="sxs-lookup"><span data-stu-id="5ab38-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="5ab38-205">範本</span><span class="sxs-lookup"><span data-stu-id="5ab38-205">Templates</span></span>

<span data-ttu-id="5ab38-206">當您在 Windows 8.1 或 Windows Server 2012 R2 上使用 Visual Studio 2012 創建 ASP.NET MVC 專案時,Visual Studio 會顯示一條錯誤消息,指出"為 ASP.NET 4.5 配置 Web [url] 失敗"。</span><span class="sxs-lookup"><span data-stu-id="5ab38-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![設定錯誤](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="5ab38-208">您會看到此錯誤,因為 Visual Studio 2012 在 Windows 這些版本上安裝時不會啟用 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="5ab38-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="5ab38-209">要啟用 ASP.NET 4.5,請執行打開[或關閉"打開"Windows 功能](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)中描述的步驟。</span><span class="sxs-lookup"><span data-stu-id="5ab38-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![開啟或關閉 Windows 功能](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="5ab38-211">或者,您可以通過命令行啟用ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="5ab38-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="5ab38-212">在管理員模式下打開命令提示。</span><span class="sxs-lookup"><span data-stu-id="5ab38-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="5ab38-213">運行以下命令以啟用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="5ab38-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
