---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET和網络工具 2012.2 發行說明 |微軟文件
author: rick-anderson
description: ASP.NET和網路工具 2012.2 的發行說明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676304"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a><span data-ttu-id="6027e-103">ASP.NET 和 Web 工具 2012.2 版本資訊</span><span class="sxs-lookup"><span data-stu-id="6027e-103">ASP.NET and Web Tools 2012.2 Release Notes</span></span>

> <span data-ttu-id="6027e-104">本文件介紹 ASP.NET 和 Web 工具 2012.2 的發布。</span><span class="sxs-lookup"><span data-stu-id="6027e-104">This document describes the release of ASP.NET and Web Tools 2012.2.</span></span> <span data-ttu-id="6027e-105">它是可視化工作室 Web 工具和 ASP.NET 的更新。</span><span class="sxs-lookup"><span data-stu-id="6027e-105">It is an update to Visual Studio Web Tooling and ASP.NET.</span></span>

- [<span data-ttu-id="6027e-106">安裝說明</span><span class="sxs-lookup"><span data-stu-id="6027e-106">Installation Notes</span></span>](#_Installation)
- [<span data-ttu-id="6027e-107">文件</span><span class="sxs-lookup"><span data-stu-id="6027e-107">Documentation</span></span>](#_Documentation)
- [<span data-ttu-id="6027e-108">支援</span><span class="sxs-lookup"><span data-stu-id="6027e-108">Support</span></span>](#_Support)
- [<span data-ttu-id="6027e-109">軟體要求</span><span class="sxs-lookup"><span data-stu-id="6027e-109">Software Requirements</span></span>](#_Software_Requirements)
- [<span data-ttu-id="6027e-110">ASP.NET和 Web 工具中的新功能 2012.2</span><span class="sxs-lookup"><span data-stu-id="6027e-110">New Features in ASP.NET and Web Tools 2012.2</span></span>](#_New_Features_in)

    - [<span data-ttu-id="6027e-111">Tooling</span><span class="sxs-lookup"><span data-stu-id="6027e-111">Tooling</span></span>](#_Tooling)
    - [<span data-ttu-id="6027e-112">Web Publishing</span><span class="sxs-lookup"><span data-stu-id="6027e-112">Web Publishing</span></span>](#_Web_Publishing)
    - [<span data-ttu-id="6027e-113">ASP.NET MVC 樣本</span><span class="sxs-lookup"><span data-stu-id="6027e-113">ASP.NET MVC Templates</span></span>](#_Templates)
    - [<span data-ttu-id="6027e-114">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6027e-114">ASP.NET Web API</span></span>](#_ASP.NET_Web_API)

    - [<span data-ttu-id="6027e-115">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="6027e-115">ASP.NET SignalR</span></span>](#_ASP.NET_SignalR)
    - [<span data-ttu-id="6027e-116">ASP.NET 易記 URL</span><span class="sxs-lookup"><span data-stu-id="6027e-116">ASP.NET Friendly URLs</span></span>](#_ASP.NET_Friendly_URLs)
- [<span data-ttu-id="6027e-117">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="6027e-117">Known Issues and Breaking Changes</span></span>](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a><span data-ttu-id="6027e-118">安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="6027e-118">Installation Notes</span></span>

<span data-ttu-id="6027e-119">ASP.NET和Web工具2012.2為可視化工作室2012可以使用[Web平臺安裝程式](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安裝。</span><span class="sxs-lookup"><span data-stu-id="6027e-119">ASP.NET and Web Tools 2012.2 for Visual Studio 2012 can be installed using [Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).</span></span> <span data-ttu-id="6027e-120">這是 Visual Studio 2012 或 Visual Studio Express 2012 Web 的更新,這是必要的。</span><span class="sxs-lookup"><span data-stu-id="6027e-120">This is an update to Visual Studio 2012 or Visual Studio Express 2012 for Web, which is required.</span></span> <span data-ttu-id="6027e-121">如果您未安裝 Visual Studio,則將安裝適用於 Web 的 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="6027e-121">If you do not have Visual Studio installed, Visual Studio Express 2012 for Web will be installed.</span></span>

<span data-ttu-id="6027e-122">您還可以手動安裝ASP.NET和 Web 工具 2012.2。</span><span class="sxs-lookup"><span data-stu-id="6027e-122">You can also install ASP.NET and Web Tools 2012.2 manually.</span></span> <span data-ttu-id="6027e-123">您必須安裝 Visual Studio 2012 或 Visual Studio Express 2012 以安裝 Web。</span><span class="sxs-lookup"><span data-stu-id="6027e-123">You must have Visual Studio 2012 or Visual Studio Express 2012 for Web installed.</span></span> <span data-ttu-id="6027e-124">然後使用以下說明:</span><span class="sxs-lookup"><span data-stu-id="6027e-124">Then use the following instructions:</span></span> 

1. <span data-ttu-id="6027e-125">從下載中心下載[ASP.NET和 Web 框架 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6027e-125">Download [ASP.NET and Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe) installer from Download Center.</span></span>
2. <span data-ttu-id="6027e-126">當提示時,按一下「運行」。</span><span class="sxs-lookup"><span data-stu-id="6027e-126">When prompted click Run.</span></span> <span data-ttu-id="6027e-127">您還可以保存該檔以稍後運行該檔。</span><span class="sxs-lookup"><span data-stu-id="6027e-127">You can also save the file to run it later.</span></span>
3. <span data-ttu-id="6027e-128">驗證您將要更新的可視化工作室版本。</span><span class="sxs-lookup"><span data-stu-id="6027e-128">Verify the version of Visual Studio you will update.</span></span> <span data-ttu-id="6027e-129">您可以通過啟動要更新的可視化工作室來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="6027e-129">You can do this by launching the Visual Studio you wish to update.</span></span> <span data-ttu-id="6027e-130">然後單擊"幫助"功能表項。</span><span class="sxs-lookup"><span data-stu-id="6027e-130">Then click the Help menu item.</span></span>   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. <span data-ttu-id="6027e-131">如果你看到關於微軟視覺工作室&quot;2012網頁的功能表&quot;項 ,然後下載[網路開發人員工具2012.2 - Visual Studio Express 2012為Web。](https://go.microsoft.com/fwlink/?LinkID=282228)</span><span class="sxs-lookup"><span data-stu-id="6027e-131">If you see the menu item &quot;About Microsoft Visual Studio 2012 for Web&quot; then download [Web Developer Tools 2012.2 - Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span> <span data-ttu-id="6027e-132">否則下載[網路開發人員工具 2012.2 - 視覺工作室 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span><span class="sxs-lookup"><span data-stu-id="6027e-132">Otherwise download [Web Developer Tools 2012.2 - Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228).</span></span>
5. <span data-ttu-id="6027e-133">當提示時,按一下「運行」。</span><span class="sxs-lookup"><span data-stu-id="6027e-133">When prompted click Run.</span></span> <span data-ttu-id="6027e-134">您還可以保存該檔以稍後運行該檔。</span><span class="sxs-lookup"><span data-stu-id="6027e-134">You can also save the file to run it later.</span></span>

> [!NOTE]
> <span data-ttu-id="6027e-135">ASP.NET和 Web 工具 2012.2 版本不包括 SQL Server 資料工具。</span><span class="sxs-lookup"><span data-stu-id="6027e-135">ASP.NET and Web Tools 2012.2 release does not include SQL Server Data Tools.</span></span> <span data-ttu-id="6027e-136">SQL Server 和 Windows Azure SQL 資料庫提供了一組更豐富的資料庫工具,包括離線專案支援的開發、架構比較和擴增的資料庫部署功能。</span><span class="sxs-lookup"><span data-stu-id="6027e-136">SQL Server and Windows Azure SQL Databases provides a richer set of database tooling including offline project-backed development, schema comparison and enhanced database deployment capabilities.</span></span> <span data-ttu-id="6027e-137">關於詳細資訊或安裝 SQL 伺服器資料工具,[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)請造訪 。</span><span class="sxs-lookup"><span data-stu-id="6027e-137">For more information or to install SQL Server Data Tools visit [https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127).</span></span>

<a id="_Documentation"></a>
## <a name="documentation"></a><span data-ttu-id="6027e-138">文件</span><span class="sxs-lookup"><span data-stu-id="6027e-138">Documentation</span></span>

<span data-ttu-id="6027e-139">有關ASP.NET和 Web 工具 2012.2 的教程和其他資訊可從ASP.NET網站https://www.asp.net)() 獲得。</span><span class="sxs-lookup"><span data-stu-id="6027e-139">Tutorials and other information about ASP.NET and Web Tools 2012.2 are available from ASP.NET web site ( https://www.asp.net).</span></span>

<a id="_Support"></a>
## <a name="support"></a><span data-ttu-id="6027e-140">支援</span><span class="sxs-lookup"><span data-stu-id="6027e-140">Support</span></span>

<span data-ttu-id="6027e-141">ASP.NET和網路工具 2012.2 正式發佈和支援。</span><span class="sxs-lookup"><span data-stu-id="6027e-141">ASP.NET and Web Tools 2012.2 is officially released and supported.</span></span> <span data-ttu-id="6027e-142">您可以使用正常的支援通道。</span><span class="sxs-lookup"><span data-stu-id="6027e-142">You can use your normal support channel.</span></span> <span data-ttu-id="6027e-143">您還可以向ASP.NET論壇 ()[https://forums.asp.net/](https://forums.asp.net/)發佈問題,ASP.NET社區成員經常能夠提供非正式支援。</span><span class="sxs-lookup"><span data-stu-id="6027e-143">You can also post questions to the ASP.NET forums ([https://forums.asp.net/](https://forums.asp.net/)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="6027e-144">軟體需求</span><span class="sxs-lookup"><span data-stu-id="6027e-144">Software Requirements</span></span>

<span data-ttu-id="6027e-145">ASP.NET和網路工具 2012.2 要求 Visual Studio 2012 或 Visual Studio Express 2012 用於 Web。</span><span class="sxs-lookup"><span data-stu-id="6027e-145">The ASP.NET and Web Tools 2012.2 requires Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a><span data-ttu-id="6027e-146">ASP.NET和 Web 工具中的新功能 2012.2</span><span class="sxs-lookup"><span data-stu-id="6027e-146">New Features in ASP.NET and Web Tools 2012.2</span></span>

<span data-ttu-id="6027e-147">本節介紹在ASP.NET和Web工具 2012.2 版本中引入的功能。</span><span class="sxs-lookup"><span data-stu-id="6027e-147">This section describes features that have been introduced in the ASP.NET and Web Tools 2012.2 release.</span></span>

<a id="_Tooling"></a>
### <a name="tooling"></a><span data-ttu-id="6027e-148">Tooling</span><span class="sxs-lookup"><span data-stu-id="6027e-148">Tooling</span></span>

- <span data-ttu-id="6027e-149">Page Inspector</span><span class="sxs-lookup"><span data-stu-id="6027e-149">Page Inspector</span></span> 

    - <span data-ttu-id="6027e-150">支援 JavaScript 選擇映射,允許頁面檢查器將動態添加到頁面的專案映射回相應的 JavaScript 代碼。</span><span class="sxs-lookup"><span data-stu-id="6027e-150">Support JavaScript selection mapping allowing Page Inspector to map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span>
    - <span data-ttu-id="6027e-151">即時查看 CSS 更新的能力。</span><span class="sxs-lookup"><span data-stu-id="6027e-151">The ability to see CSS updates in real-time.</span></span>
    - <span data-ttu-id="6027e-152">關於詳細資訊,請閱讀[網頁檢查器 中的 CSS 自動同步與 JavaScript 選擇對應](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6027e-152">For more information, read [CSS Auto-Sync and JavaScript Selection Mapping in Page Inspector](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx).</span></span>
- <span data-ttu-id="6027e-153">編輯器</span><span class="sxs-lookup"><span data-stu-id="6027e-153">Editor</span></span> 

    - <span data-ttu-id="6027e-154">支援咖啡腳本、鬍鬚、手柄和 JsRender 的語法突出顯示。</span><span class="sxs-lookup"><span data-stu-id="6027e-154">Support syntax highlighting for CoffeeScript, Mustache, Handlebars, and JsRender.</span></span>
    - <span data-ttu-id="6027e-155">HTML 編輯器為挖空綁定提供"感知"。</span><span class="sxs-lookup"><span data-stu-id="6027e-155">The HTML editor provides Intellisense for Knockout bindings.</span></span>
    - <span data-ttu-id="6027e-156">減少編輯和編譯器支援,以便使用 LESS 構建動態 CSS。</span><span class="sxs-lookup"><span data-stu-id="6027e-156">LESS editing and compiler support to enable building dynamic CSS using LESS.</span></span>
    - <span data-ttu-id="6027e-157">將 JSON 貼上為 .NET 類。</span><span class="sxs-lookup"><span data-stu-id="6027e-157">Paste JSON as a .NET class.</span></span> <span data-ttu-id="6027e-158">使用此特殊貼上指令將 JSON 貼上到 C# 或VB.NET代碼檔中,Visual Studio 將自動生成從 JSON 推斷的 .NET 類。</span><span class="sxs-lookup"><span data-stu-id="6027e-158">Using this Special Paste command to paste JSON into a C# or VB.NET code file, and Visual Studio will automatically generate .NET classes inferred from the JSON.</span></span>
- <span data-ttu-id="6027e-159">移動模擬器支援增加了擴充性掛鉤,以便第三方模擬器可以作為 VSIX 安裝。</span><span class="sxs-lookup"><span data-stu-id="6027e-159">Mobile Emulator support adds extensibility hooks so that third-party emulators can be installed as a VSIX.</span></span> <span data-ttu-id="6027e-160">已安裝的模擬器將顯示在 F5 下拉清單中,以便開發人員可以在各種行動裝置上預覽其網站。</span><span class="sxs-lookup"><span data-stu-id="6027e-160">The installed emulators will show up in the F5 dropdown, so that developers can preview their websites on a variety of mobile devices.</span></span> <span data-ttu-id="6027e-161">閱讀更多有關此功能在斯科特漢塞爾曼的部落格目與[視覺工作室新的瀏覽器堆疊集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6027e-161">Read more about this feature in Scott Hanselman's blog entry on [the new BrowserStack integration with Visual Studio](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx).</span></span>

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a><span data-ttu-id="6027e-162">Web Publishing</span><span class="sxs-lookup"><span data-stu-id="6027e-162">Web Publishing</span></span>

- <span data-ttu-id="6027e-163">網站專案現在具有與 Web 應用程式專案相同的發表體驗,包括發表到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="6027e-163">Web site projects now have the same publishing experience as Web Application projects including publishing to Windows Azure Web Sites.</span></span>
- <span data-ttu-id="6027e-164">選擇性發佈&#8211;一個或多個檔案,您可以執行以下操作(發佈到 Web 部署終結點後):</span><span class="sxs-lookup"><span data-stu-id="6027e-164">Selective publish &#8211; for one or more files you can perform the following actions (after publishing to a Web Deploy endpoint):</span></span> 

    - <span data-ttu-id="6027e-165">發佈選定的檔。</span><span class="sxs-lookup"><span data-stu-id="6027e-165">Publish selected files.</span></span>
    - <span data-ttu-id="6027e-166">查看本地檔和遠端檔之間的區別。</span><span class="sxs-lookup"><span data-stu-id="6027e-166">See the difference between a local file and a remote file.</span></span>
    - <span data-ttu-id="6027e-167">使用遠端檔案更新本地檔案或使用本地檔案更新遠端檔案。</span><span class="sxs-lookup"><span data-stu-id="6027e-167">Update the local file with the remote file or update the remote file with the local file.</span></span>

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a><span data-ttu-id="6027e-168">ASP.NET MVC 樣本</span><span class="sxs-lookup"><span data-stu-id="6027e-168">ASP.NET MVC Templates</span></span>

- <span data-ttu-id="6027e-169">全新的 Facebook 應用程式範本可讓撰寫 Facebook Canvas 應用程式再容易不過了。</span><span class="sxs-lookup"><span data-stu-id="6027e-169">The new Facebook Application template makes writing Facebook Canvas applications easy.</span></span> <span data-ttu-id="6027e-170">只需幾個簡單的步驟，您便可建立 Facebook 應用程式，進而取得已登入使用者的資料並將資料與他的朋友進行整合。</span><span class="sxs-lookup"><span data-stu-id="6027e-170">In a few simple steps, you can create a Facebook application that gets data from a logged in user and integrates with their friends.</span></span> <span data-ttu-id="6027e-171">此範本包括一個新程式庫，處理建置 Facebook 應用程式時所涉及的所有連結，包括授權、權限、存取 Facebook 資料等等。</span><span class="sxs-lookup"><span data-stu-id="6027e-171">The template includes a new library to take care of all the plumbing involved in building a Facebook app, including authentication, permissions, accessing Facebook data and more.</span></span> <span data-ttu-id="6027e-172">有關使用 Facebook 應用程式樣本的詳細資訊,請參[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)閱 。</span><span class="sxs-lookup"><span data-stu-id="6027e-172">For more information on using the Facebook Application template see [https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921).</span></span>
- <span data-ttu-id="6027e-173">全新的單一網頁應用程式 MVC 範本可讓開發人員使用 HTML 5、CSS 3 和熱門的 Knockout 與 jQuery JavaScript 程式庫，在 ASP.NET Web API 的基礎上建置互動式用戶端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6027e-173">A new Single Page Application MVC template allows developers to build interactive client-side web apps using HTML 5, CSS 3, and the popular Knockout and jQuery JavaScript libraries, on top of ASP.NET Web API.</span></span> <span data-ttu-id="6027e-174">該範本包括一個"待辦事項"列表應用程式,該應用程式演示了構建使用 RESTful 伺服器 API 的 JavaScript HTML5 應用程式的常見做法。</span><span class="sxs-lookup"><span data-stu-id="6027e-174">The template includes a "todo" list application that demonstrates common practices for building a JavaScript HTML5 application that uses a RESTful server API.</span></span> <span data-ttu-id="6027e-175">您可以在 上閱讀更多[https://www.asp.net/single-page-application](../../../single-page-application/index.md)內容 。</span><span class="sxs-lookup"><span data-stu-id="6027e-175">You can read more at [https://www.asp.net/single-page-application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="6027e-176">您現在可以創建一個 VSIX,將新範本添加到 ASP.NET MVC 新項目對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6027e-176">You can now create a VSIX that adds new templates to the ASP.NET MVC New Project dialog.</span></span> <span data-ttu-id="6027e-177">瞭解如何在此處:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span><span class="sxs-lookup"><span data-stu-id="6027e-177">Learn how here: [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)</span></span>
- <span data-ttu-id="6027e-178">已更新 &#8211; MVC 專案樣本的固定顯示模式包,以包括新的「固定顯示模式」NuGet 包,該包包含 MVC 4 中 Bug 的解決方法。</span><span class="sxs-lookup"><span data-stu-id="6027e-178">FixedDisplayModes package &#8211; MVC project templates have been updated to include the new ‘FixedDisplayModes' NuGet package, which contains a workaround for a bug in MVC 4.</span></span> <span data-ttu-id="6027e-179">有關包中包含的修復程式的詳細資訊,請參閱 MVC 團隊的此部[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)落格文章 ( )。</span><span class="sxs-lookup"><span data-stu-id="6027e-179">For more information on the fix contained in the package, refer to this blog post ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) from the MVC team.</span></span>

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="6027e-180">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6027e-180">ASP.NET Web API</span></span>

<span data-ttu-id="6027e-181">ASP.NET Web API 已通過以下幾個新功能進行了增強:</span><span class="sxs-lookup"><span data-stu-id="6027e-181">ASP.NET Web API has been enhanced with several new features:</span></span>

- <span data-ttu-id="6027e-182">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="6027e-182">ASP.NET Web API OData</span></span>
- <span data-ttu-id="6027e-183">ASP.NET Web API 追蹤</span><span class="sxs-lookup"><span data-stu-id="6027e-183">ASP.NET Web API Tracing</span></span>
- <span data-ttu-id="6027e-184">ASP.NET Web API 說明頁</span><span class="sxs-lookup"><span data-stu-id="6027e-184">ASP.NET Web API Help Page</span></span>

#### <a name="aspnet-web-api-odata"></a><span data-ttu-id="6027e-185">ASP.NET Web API OData</span><span class="sxs-lookup"><span data-stu-id="6027e-185">ASP.NET Web API OData</span></span>

<span data-ttu-id="6027e-186">ASP.NET Web API OData 使您能夠靈活地建構具有豐富業務邏輯的 OData 終結點,而不是任何資料來源。</span><span class="sxs-lookup"><span data-stu-id="6027e-186">ASP.NET Web API OData gives you the flexibility you need to build OData endpoints with rich business logic over any data source.</span></span> <span data-ttu-id="6027e-187">使用ASP.NET Web API OData,您可以控制要公開的 OData 語意量。</span><span class="sxs-lookup"><span data-stu-id="6027e-187">With ASP.NET Web API OData you control the amount of OData semantics that you want to expose.</span></span> <span data-ttu-id="6027e-188">ASP.NET Web API OData 包含在 mVC 4ASP.NET 專案樣本[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)中,也可從 NuGet () 獲得。</span><span class="sxs-lookup"><span data-stu-id="6027e-188">ASP.NET Web API OData is included with the ASP.NET MVC 4 project templates and is also available from NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)).</span></span>

<span data-ttu-id="6027e-189">ASP.NET Web API OData 目前支援以下功能:</span><span class="sxs-lookup"><span data-stu-id="6027e-189">ASP.NET Web API OData currently supports the following features:</span></span>

- <span data-ttu-id="6027e-190">通過應用 [可查詢] 屬性啟用 OData 查詢語義。</span><span class="sxs-lookup"><span data-stu-id="6027e-190">Enable OData query semantics by applying the [Queryable] attribute.</span></span>
- <span data-ttu-id="6027e-191">輕鬆驗證 OData 查詢並限制支援的查詢選項、運算子和函數集。</span><span class="sxs-lookup"><span data-stu-id="6027e-191">Easily validate OData queries and restrict the set of supported query options, operators and functions.</span></span>
- <span data-ttu-id="6027e-192">參數直接綁定到 ODataQueryOptions,以獲得查詢的抽象語法樹表示形式,然後可以驗證並應用於可查詢或 IE500。</span><span class="sxs-lookup"><span data-stu-id="6027e-192">Parameter bind to ODataQueryOptions directly to get an abstract syntax tree representation of the query that can then be validated and applied to an IQueryable or IEnumerable.</span></span>
- <span data-ttu-id="6027e-193">通過在 [可查詢] 屬性上指定結果限制,啟用服務驅動的分頁和下一頁連結生成。</span><span class="sxs-lookup"><span data-stu-id="6027e-193">Enable service-driven paging and next page link generation by specifying result limits on [Queryable] attribute.</span></span>
- <span data-ttu-id="6027e-194">使用$inlinecount請求匹配資源總數的內聯計數。</span><span class="sxs-lookup"><span data-stu-id="6027e-194">Request an inlined count of the total number of matching resources using $inlinecount.</span></span>
- <span data-ttu-id="6027e-195">控制無效傳播。</span><span class="sxs-lookup"><span data-stu-id="6027e-195">Control null propagation.</span></span>
- <span data-ttu-id="6027e-196">$filter中的任何/所有運算符。</span><span class="sxs-lookup"><span data-stu-id="6027e-196">Any/All operators in $filter.</span></span>
- <span data-ttu-id="6027e-197">按約定推斷實體數據模型,或以類似於實體框架代碼優先的方式顯式自定義模型。</span><span class="sxs-lookup"><span data-stu-id="6027e-197">Infer an entity data model by convention or explicitly customize a model in a manner similar to Entity Framework Code-First.</span></span>
- <span data-ttu-id="6027e-198">通過從實體集控制器派生來公開實體集。</span><span class="sxs-lookup"><span data-stu-id="6027e-198">Expose entity sets by deriving from EntitySetController.</span></span>
- <span data-ttu-id="6027e-199">用於公開導航屬性、操作連結和實現 OData 操作的簡單可自定義約定。</span><span class="sxs-lookup"><span data-stu-id="6027e-199">Simple, customizable conventions for exposing navigation properties, manipulating links and implementing OData actions.</span></span>
- <span data-ttu-id="6027e-200">使用 MapODataRoute 擴充方法簡化路由。</span><span class="sxs-lookup"><span data-stu-id="6027e-200">Simplified routing using the MapODataRoute extension method.</span></span>
- <span data-ttu-id="6027e-201">通過公開多個 EDM 模型來支援版本控制。</span><span class="sxs-lookup"><span data-stu-id="6027e-201">Support for versioning by exposing multiple EDM models.</span></span>
- <span data-ttu-id="6027e-202">公開服務文檔和$metadata,以便為 Web API 生成用戶端(.NET、Windows Phone、Windows 應用商店等)。</span><span class="sxs-lookup"><span data-stu-id="6027e-202">Expose service document and $metadata so you can generate clients (.NET, Windows Phone, Windows Store, etc.) for your Web API.</span></span>
- <span data-ttu-id="6027e-203">支援 OData Atom、JSON 和 JSON 詳細格式。</span><span class="sxs-lookup"><span data-stu-id="6027e-203">Support for the OData Atom, JSON, and JSON verbose formats.</span></span>
- <span data-ttu-id="6027e-204">建立、更新、部分更新(PATCH)和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="6027e-204">Create, update, partially update (PATCH) and delete entities.</span></span>
- <span data-ttu-id="6027e-205">查詢和操作實體之間的關係。</span><span class="sxs-lookup"><span data-stu-id="6027e-205">Query and manipulate relationships between entities.</span></span>
- <span data-ttu-id="6027e-206">建立連接到您的路線的關係連結。</span><span class="sxs-lookup"><span data-stu-id="6027e-206">Create relationship links that wire up to your routes.</span></span>
- <span data-ttu-id="6027e-207">複雜類型。</span><span class="sxs-lookup"><span data-stu-id="6027e-207">Complex types.</span></span>
- <span data-ttu-id="6027e-208">實體類型繼承。</span><span class="sxs-lookup"><span data-stu-id="6027e-208">Entity Type Inheritance.</span></span>
- <span data-ttu-id="6027e-209">集合屬性。</span><span class="sxs-lookup"><span data-stu-id="6027e-209">Collection properties.</span></span>
- <span data-ttu-id="6027e-210">枚舉。</span><span class="sxs-lookup"><span data-stu-id="6027e-210">Enums.</span></span>
- <span data-ttu-id="6027e-211">OData 操作。</span><span class="sxs-lookup"><span data-stu-id="6027e-211">OData actions.</span></span>
- <span data-ttu-id="6027e-212">建立與 WCF 資料服務相同的基礎,即 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)()。</span><span class="sxs-lookup"><span data-stu-id="6027e-212">Built upon the same foundation as WCF Data Services, namely ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)).</span></span>

<span data-ttu-id="6027e-213">有關web API OData ASP.NET[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)的詳細資訊 ,請參閱。</span><span class="sxs-lookup"><span data-stu-id="6027e-213">For more information on ASP.NET Web API OData see [https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141).</span></span>

#### <a name="aspnet-web-api-tracing"></a><span data-ttu-id="6027e-214">ASP.NET Web API 追蹤</span><span class="sxs-lookup"><span data-stu-id="6027e-214">ASP.NET Web API Tracing</span></span>

<span data-ttu-id="6027e-215">ASP.NET Web API 追蹤將從 Web API 的追蹤資料整合到 .NET 追蹤中。</span><span class="sxs-lookup"><span data-stu-id="6027e-215">ASP.NET Web API Tracing integrates tracing data from your web APIs with .NET Tracing.</span></span> <span data-ttu-id="6027e-216">默認情況下,它在 Web API 專案樣本中啟用。</span><span class="sxs-lookup"><span data-stu-id="6027e-216">It is now enabled by default in the Web API project template.</span></span> <span data-ttu-id="6027e-217">Web API 的追蹤數據將發送到輸出視窗,並透過 IntelliTrace 提供。</span><span class="sxs-lookup"><span data-stu-id="6027e-217">Tracing data for your web APIs is sent to the Output window and is made available through IntelliTrace.</span></span> <span data-ttu-id="6027e-218">ASP.NET Web API 追蹤使您能夠透過與[Windows Azure 診斷](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)整合在 Windows Azure 上託管時追蹤有關 Web API 的資訊。</span><span class="sxs-lookup"><span data-stu-id="6027e-218">ASP.NET Web API Tracing enables you to trace information about your Web API when hosted on Windows Azure through integration with [Windows Azure Diagnostics](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx).</span></span> <span data-ttu-id="6027e-219">您還可以使用ASP.NET Web API 追蹤 NuGet 套件 ()[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)在任何應用程式中安裝和啟用ASP.NET Web API 追蹤。</span><span class="sxs-lookup"><span data-stu-id="6027e-219">You can also install and enable ASP.NET Web API Tracing in any application using the ASP.NET Web API Tracing NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)).</span></span>

<span data-ttu-id="6027e-220">有關設定和使用ASP.NET Web API 追蹤的詳細資訊,[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)請參閱 。</span><span class="sxs-lookup"><span data-stu-id="6027e-220">For more information on configuring and using ASP.NET Web API Tracing see [https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874).</span></span>

#### <a name="aspnet-web-api-help-page"></a><span data-ttu-id="6027e-221">ASP.NET Web API 說明頁</span><span class="sxs-lookup"><span data-stu-id="6027e-221">ASP.NET Web API Help Page</span></span>

<span data-ttu-id="6027e-222">默認情況下,Web API 幫助頁ASP.NET包含在 Web API 專案範本中。</span><span class="sxs-lookup"><span data-stu-id="6027e-222">The ASP.NET Web API Help Page is now included by default in the Web API project template.</span></span> <span data-ttu-id="6027e-223">ASP.NET Web API 協助頁面會自動為 Web API 產生文件,包括 HTTP 終結點、支援的 HTTP 方法、參數以及示例請求和回應消息負載。</span><span class="sxs-lookup"><span data-stu-id="6027e-223">The ASP.NET Web API Help Page automatically generates documentation for web APIs including the HTTP endpoints, the supported HTTP methods, parameters and example request and response message payloads.</span></span> <span data-ttu-id="6027e-224">文檔會自動從代碼中的註釋中提取。</span><span class="sxs-lookup"><span data-stu-id="6027e-224">Documentation is automatically pulled from comments in your code.</span></span> <span data-ttu-id="6027e-225">您還可以使用ASP.NET Web API 幫助頁 NuGet 套件 ()[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)將ASP.NET Web API 幫助頁添加到任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="6027e-225">You can also add the ASP.NET Web API Help Page to any application using the ASP.NET Web API Help Page NuGet package ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)).</span></span>

<span data-ttu-id="6027e-226">有關設定和自訂ASP.NET Web API 說明頁的詳細資訊,[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)請參閱 。</span><span class="sxs-lookup"><span data-stu-id="6027e-226">For more information on setting up and customizing the ASP.NET Web API Help Page see [https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140).</span></span>

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a><span data-ttu-id="6027e-227">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="6027e-227">ASP.NET SignalR</span></span>

<span data-ttu-id="6027e-228">ASP.NET SignalR 使將即時 Web 功能添加到 ASP.NET 應用程式中變得簡單,如果使用 WebSocket(如果可用),則在不可用時自動回歸到其他技術。</span><span class="sxs-lookup"><span data-stu-id="6027e-228">ASP.NET SignalR makes it simple to add real-time web capabilities to your ASP.NET application, using WebSockets if available and automatically falling back to other techniques when it isn't.</span></span>

<span data-ttu-id="6027e-229">有關使用ASP.NET訊號R的詳細資訊,請參[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)閱 。</span><span class="sxs-lookup"><span data-stu-id="6027e-229">For more information on using ASP.NET SignalR see [https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271).</span></span>

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a><span data-ttu-id="6027e-230">ASP.NET 易記 URL</span><span class="sxs-lookup"><span data-stu-id="6027e-230">ASP.NET Friendly URLs</span></span>

<span data-ttu-id="6027e-231">ASP.NET友好 URL 使 Web 表單開發人員能夠非常輕鬆地生成外觀更簡潔的 URL(沒有 .aspx 擴展)。</span><span class="sxs-lookup"><span data-stu-id="6027e-231">ASP.NET FriendlyURLs makes it very easy for web forms developers to generate cleaner looking URLs(without the .aspx extension).</span></span> <span data-ttu-id="6027e-232">它只需要很少或不需要配置,並且可用於現有的ASP.NET v4.0 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6027e-232">It requires little to no configuration and can be used with existing ASP.NET v4.0 applications.</span></span> <span data-ttu-id="6027e-233">友好 URL 功能還支援桌面檢視和行動視圖之間的切換,使開發人員能夠更輕鬆地向其應用程式添加行動支援。</span><span class="sxs-lookup"><span data-stu-id="6027e-233">The FriendlyURLs feature also makes it easier for developers to add mobile support to their applications, by supporting switching between desktop and mobile views.</span></span>

<span data-ttu-id="6027e-234">有關安裝和使用ASP.NET友好 URL 的詳細資訊,請[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)參閱 。</span><span class="sxs-lookup"><span data-stu-id="6027e-234">For more information on installing and using ASP.NET Friendly URLs see [http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx).</span></span>

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="6027e-235">已知問題和重大變更</span><span class="sxs-lookup"><span data-stu-id="6027e-235">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="6027e-236">本節介紹 ASP.NET 和 Web 工具 2012.2 版本中的已知問題和重大更改。</span><span class="sxs-lookup"><span data-stu-id="6027e-236">This section describes known issues and breaking changes that are in the ASP.NET and Web Tools 2012.2 release.</span></span>

### <a name="installation-issues"></a><span data-ttu-id="6027e-237">安裝問題</span><span class="sxs-lookup"><span data-stu-id="6027e-237">Installation Issues</span></span>

#### <a name="out-of-order-installs-of-visual-studio-2012"></a><span data-ttu-id="6027e-238">視覺工作室 2012 的有序安裝</span><span class="sxs-lookup"><span data-stu-id="6027e-238">Out of order installs of Visual Studio 2012</span></span>

<span data-ttu-id="6027e-239">安裝ASP.NET和 Web 工具 2012.2 後安裝 Visual Studio 2012 的額外 SKU 將需要修復操作。</span><span class="sxs-lookup"><span data-stu-id="6027e-239">Installing an additional SKU of Visual Studio 2012 after installing the ASP.NET and Web Tools 2012.2 will require a repair operation.</span></span> <span data-ttu-id="6027e-240">考量以下發生順序：</span><span class="sxs-lookup"><span data-stu-id="6027e-240">Consider the following sequence:</span></span>

1. <span data-ttu-id="6027e-241">安裝視覺化工作室 2012 快速網頁</span><span class="sxs-lookup"><span data-stu-id="6027e-241">Install Visual Studio 2012 Express for Web</span></span>
2. <span data-ttu-id="6027e-242">安裝ASP.NET和 Web 工具 2012.2</span><span class="sxs-lookup"><span data-stu-id="6027e-242">Install ASP.NET and Web Tools 2012.2</span></span>
3. <span data-ttu-id="6027e-243">安裝視覺工作室 2012 專業, 高級或終極</span><span class="sxs-lookup"><span data-stu-id="6027e-243">Install Visual Studio 2012 Professional, Premium or Ultimate</span></span>

<span data-ttu-id="6027e-244">步驟 2 僅會導致為 Web 安裝 Express 的更新。</span><span class="sxs-lookup"><span data-stu-id="6027e-244">Step 2 would only result in installing updates for Express for Web.</span></span> <span data-ttu-id="6027e-245">為了確保在步驟 3 中安裝的其他 SKU 包含更新,您需要修復 ASP.NET和 Web 工具 2012.2 才能安裝上次安裝的 SKU 的更新。</span><span class="sxs-lookup"><span data-stu-id="6027e-245">To ensure that the additional SKU installed during step 3 contains the update you will need to repair the ASP.NET and Web Tools 2012.2 to install the updates for the last SKU installed.</span></span> <span data-ttu-id="6027e-246">如果步驟 1 和步驟 3 中的 SKU 顛倒,則這也適用於。</span><span class="sxs-lookup"><span data-stu-id="6027e-246">This also applies if the SKUs in Step 1 and 3 are reversed.</span></span>

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a><span data-ttu-id="6027e-247">安裝微軟ASP.NET和網路工具 2012.2 當可視化工作室打開</span><span class="sxs-lookup"><span data-stu-id="6027e-247">Installing Microsoft ASP.NET and Web Tools 2012.2 when Visual Studio is open</span></span>

<span data-ttu-id="6027e-248">如果在安裝 Microsoft ASP.NET 和 Web 工具 2012.2 期間打開 VS,則 Visual Studio 可能最終處於不良狀態。</span><span class="sxs-lookup"><span data-stu-id="6027e-248">If VS is open during installation of Microsoft ASP.NET and Web Tools 2012.2, Visual Studio might end up in a bad state.</span></span> <span data-ttu-id="6027e-249">建議使用者在繼續安裝之前關閉 Visual Studio 的所有實例。</span><span class="sxs-lookup"><span data-stu-id="6027e-249">It is recommended that users close all instances of Visual Studio before proceeding with install.</span></span>

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a><span data-ttu-id="6027e-250">在安裝中取消ASP.NET和 Web 工具 2012.2 設定</span><span class="sxs-lookup"><span data-stu-id="6027e-250">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation</span></span>

<span data-ttu-id="6027e-251">取消ASP.NET和 Web 工具 2012.2 安裝將會使 Visual Studio 處於不良狀態。</span><span class="sxs-lookup"><span data-stu-id="6027e-251">Canceling ASP.NET and Web Tools 2012.2 setup in the middle of installation will leave Visual Studio in a bad state.</span></span> <span data-ttu-id="6027e-252">要解決此問題,請執行以下步驟:</span><span class="sxs-lookup"><span data-stu-id="6027e-252">To address this problem follow these steps:</span></span> 

- <span data-ttu-id="6027e-253">移至 [新增或移除程式]</span><span class="sxs-lookup"><span data-stu-id="6027e-253">Go to Add Remove Programs</span></span>
- <span data-ttu-id="6027e-254">卸載 Microsoft ASP.NET 和 Web 工具 2012.2(如果存在)。</span><span class="sxs-lookup"><span data-stu-id="6027e-254">Uninstall Microsoft ASP.NET and Web Tools 2012.2, if present.</span></span>
- <span data-ttu-id="6027e-255">重新安裝微軟ASP.NET和網路工具 2012.2</span><span class="sxs-lookup"><span data-stu-id="6027e-255">Reinstall Microsoft ASP.NET and Web Tools 2012.2</span></span>

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a><span data-ttu-id="6027e-256">卸載ASP.NET和 Web 工具 2012.2 後,缺少ASP.NET MVC 4 範本和 Razor v2 網站範本</span><span class="sxs-lookup"><span data-stu-id="6027e-256">After uninstalling ASP.NET and Web Tools 2012.2 the ASP.NET MVC 4 templates and Razor v2 Web Site templates are missing</span></span>

<span data-ttu-id="6027e-257">卸載ASP.NET和 Web 工具 2012.2 還將從 Visual Studio 2012 卸載所有ASP.NET MVC 4 和 Razor v2 網站範本。</span><span class="sxs-lookup"><span data-stu-id="6027e-257">Uninstalling ASP.NET and Web Tools 2012.2 will also uninstall all of ASP.NET MVC 4 and Razor v2 Web Site templates from Visual Studio 2012.</span></span>

<span data-ttu-id="6027e-258">解決方法是修復 Visual Studio 2012 安裝,以重新安裝ASP.NET MVC 4 和 Razor v2 網站範本。</span><span class="sxs-lookup"><span data-stu-id="6027e-258">The workaround is to repair your Visual Studio 2012 installation to reinstall ASP.NET MVC 4 and Razor v2 Web Site templates.</span></span>

### <a name="tooling-issues"></a><span data-ttu-id="6027e-259">工具問題</span><span class="sxs-lookup"><span data-stu-id="6027e-259">Tooling Issues</span></span>

#### <a name="nuget-error-reported-during-project-creation"></a><span data-ttu-id="6027e-260">專案建立期間回報的 NuGet 錯誤</span><span class="sxs-lookup"><span data-stu-id="6027e-260">NuGet error reported during project creation</span></span>

<span data-ttu-id="6027e-261">安裝ASP.NET和 Web 工具 2012.2 後,在建立 MVC 4 專案時可能會看到以下錯誤</span><span class="sxs-lookup"><span data-stu-id="6027e-261">After installing ASP.NET and Web Tools 2012.2 you may see the following error when creating an MVC 4 project</span></span>

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

<span data-ttu-id="6027e-262">ASP.NET和網路工具 2012.2 船舶 NuGet 2.1,並將升級 Visual Studio 2012 中的擴展。</span><span class="sxs-lookup"><span data-stu-id="6027e-262">The ASP.NET and Web Tools 2012.2 ships NuGet 2.1 and will upgrade the extension in Visual Studio 2012.</span></span> <span data-ttu-id="6027e-263">在某些情況下,VSIX 安裝程式將無法正確更新 VSIX。</span><span class="sxs-lookup"><span data-stu-id="6027e-263">In some cases, the VSIX installer will fail to correctly update the VSIX.</span></span> <span data-ttu-id="6027e-264">以下步驟將允許您解決此問題:</span><span class="sxs-lookup"><span data-stu-id="6027e-264">The following steps will allow you to address this problem:</span></span>

1. <span data-ttu-id="6027e-265">以管理員身份開始視覺工作室 2012</span><span class="sxs-lookup"><span data-stu-id="6027e-265">Start Visual Studio 2012 as an Administrator</span></span>
2. <span data-ttu-id="6027e-266">跳到工具&gt;- 擴充和更新,卸載 NuGet。</span><span class="sxs-lookup"><span data-stu-id="6027e-266">Go to Tools-&gt;Extensions and Updates and uninstall NuGet.</span></span>
3. <span data-ttu-id="6027e-267">關閉 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6027e-267">Close Visual Studio</span></span>
4. <span data-ttu-id="6027e-268">導覽到ASP.NET和 Web 工具 2012.2 安裝資料夾:</span><span class="sxs-lookup"><span data-stu-id="6027e-268">Navigate to the ASP.NET and Web Tools 2012.2 installation folder:</span></span>

    1. <span data-ttu-id="6027e-269">對於視覺工作室 2012:**程式檔_微軟 ASP.NET_ASP.NET 網路堆疊_視覺工作室 2012**</span><span class="sxs-lookup"><span data-stu-id="6027e-269">For Visual Studio 2012: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**</span></span>
    2. <span data-ttu-id="6027e-270">對於 Visual Studio 2012 Web 快訊:**程式檔案_微軟 ASP.NET_ASP.NET Web 堆疊_Visual Studio Express 2012 網頁**</span><span class="sxs-lookup"><span data-stu-id="6027e-270">For Visual Studio 2012 Express for Web: **Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**</span></span>
5. <span data-ttu-id="6027e-271">雙擊 NuGet.Tools.vsix 重新安裝 NuGet</span><span class="sxs-lookup"><span data-stu-id="6027e-271">Double click on the NuGet.Tools.vsix to reinstall NuGet</span></span>

### <a name="web-api-issues"></a><span data-ttu-id="6027e-272">Web API 問題</span><span class="sxs-lookup"><span data-stu-id="6027e-272">Web API Issues</span></span>

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a><span data-ttu-id="6027e-273">分析$filter和 DateTime 文字中的問題</span><span class="sxs-lookup"><span data-stu-id="6027e-273">Parsing issues in $filter and DateTime literals</span></span>

<span data-ttu-id="6027e-274">OData URI 解析器無法正確解析部分日期時間文本。</span><span class="sxs-lookup"><span data-stu-id="6027e-274">The OData URI parser fails to parse partial datetime literals properly.</span></span> <span data-ttu-id="6027e-275">例如,$filter_開始 eq 日期時間『2012-12-31T12:00』 無法正確解析。</span><span class="sxs-lookup"><span data-stu-id="6027e-275">For example, $filter=start eq datetime'2012-12-31T12:00' fails to parse properly.</span></span> <span data-ttu-id="6027e-276">解決方法是使用完整的文本,$filter_開始 eq 日期時間『2012-12-31T12:00:00』。</span><span class="sxs-lookup"><span data-stu-id="6027e-276">A workaround is to use the full literal, $filter=start eq datetime'2012-12-31T12:00:00'.</span></span>

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a><span data-ttu-id="6027e-277">OData 不支援不區分大小寫的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="6027e-277">OData doesn't support case-insensitive property names.</span></span>

<span data-ttu-id="6027e-278">OData 不支援 OData 查詢和 odata 路徑中不區分大小寫的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="6027e-278">OData doesn't support case-insensitive property names in OData queries and odata path.</span></span> <span data-ttu-id="6027e-279">請參考工作項目:</span><span class="sxs-lookup"><span data-stu-id="6027e-279">See workitems:</span></span>

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

<span data-ttu-id="6027e-280">如果使用者在 javascript 用戶端和伺服器端具有不同的大小寫,他們可能會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="6027e-280">If users have different casing on javascript client side and server side, they probably will encounter this issue.</span></span> <span data-ttu-id="6027e-281">此問題是在 odata 協定中設計的問題。</span><span class="sxs-lookup"><span data-stu-id="6027e-281">This issue is by design in odata protocol.</span></span> <span data-ttu-id="6027e-282">但是,許多用戶報告此問題。</span><span class="sxs-lookup"><span data-stu-id="6027e-282">However, many users reports this issue.</span></span> <span data-ttu-id="6027e-283">要解決此問題,用戶必須更正 URL 中的情況。</span><span class="sxs-lookup"><span data-stu-id="6027e-283">To work around it, users have to correct their cases in URL.</span></span>

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a><span data-ttu-id="6027e-284">默認 OData 路由約定不支援導航屬性上的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="6027e-284">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span>

<span data-ttu-id="6027e-285">默認 OData 路由約定不支援導航屬性上的 POST/PUT。</span><span class="sxs-lookup"><span data-stu-id="6027e-285">Default OData routing conventions doesn't support POST/PUT on navigation property.</span></span> <span data-ttu-id="6027e-286">請參考工作項目[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。</span><span class="sxs-lookup"><span data-stu-id="6027e-286">See workitem [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366).</span></span> <span data-ttu-id="6027e-287">在默認約定中,我們缺少此常用約定。</span><span class="sxs-lookup"><span data-stu-id="6027e-287">We are missing this commonly used convention in default conventions.</span></span>

<span data-ttu-id="6027e-288">要解決它,使用者需要擴展新的路由約定來支援它。</span><span class="sxs-lookup"><span data-stu-id="6027e-288">To work around it, users need to extend new routing convention to support it.</span></span>

### <a name="facebook-template-issues"></a><span data-ttu-id="6027e-289">Facebook 樣本問題</span><span class="sxs-lookup"><span data-stu-id="6027e-289">Facebook Template Issues</span></span>

#### <a name="facebook-application-template-only-works-using-net-45"></a><span data-ttu-id="6027e-290">Facebook 應用程式樣本僅適用於 .NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6027e-290">Facebook Application template only works using .NET 4.5</span></span>

<span data-ttu-id="6027e-291">您必須在"新項目"對話框的框架下拉清單中選擇 .NET 4.5,才能在 mVC 4 ASP.NET中查看 Facebook 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="6027e-291">You must select .NET 4.5 in the framework dropdown list in the New Project dialog to see the Facebook Application template in ASP.NET MVC 4.</span></span>

#### <a name="real-time-update-controller"></a><span data-ttu-id="6027e-292">即時更新控制器</span><span class="sxs-lookup"><span data-stu-id="6027e-292">Real-time Update Controller</span></span>

<span data-ttu-id="6027e-293">Facebook 應用程式樣本允許使用者輕鬆創建 Web API 控制器來處理來自 Facebook 的即時更新。</span><span class="sxs-lookup"><span data-stu-id="6027e-293">The Facebook Application template allows user easily create a Web API Controller to handle real-time updates from Facebook.</span></span> <span data-ttu-id="6027e-294">如果開發計算機位於 NAT 之後,則如果沒有進一步的網路配置,控制器可能無法工作。</span><span class="sxs-lookup"><span data-stu-id="6027e-294">If your development machine is behind NAT, your Controller may not work without further network configuration.</span></span> <span data-ttu-id="6027e-295">有關詳細資訊,請參閱此處:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span><span class="sxs-lookup"><span data-stu-id="6027e-295">See here for details: [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)</span></span>

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a><span data-ttu-id="6027e-296">查詢字串值與 Facebook OAuth 參數衝突</span><span class="sxs-lookup"><span data-stu-id="6027e-296">Query string values conflict with Facebook OAuth parameters</span></span>

<span data-ttu-id="6027e-297">以下欄位與 Facebook OAuth 對話框的回調 URL 衝突。</span><span class="sxs-lookup"><span data-stu-id="6027e-297">The following fields conflict with Facebook OAuth dialog's call back URL.</span></span> <span data-ttu-id="6027e-298">不要添加具有以下名稱的查詢字串值:代碼、錯誤、錯誤\_描述、錯誤\_原因。</span><span class="sxs-lookup"><span data-stu-id="6027e-298">Do not add your own query string values with the following names: code, error, error\_description, error\_reason.</span></span>

#### <a name="using-page-inspector-with-facebook-template"></a><span data-ttu-id="6027e-299">使用帶有 Facebook 樣本的頁面檢查器</span><span class="sxs-lookup"><span data-stu-id="6027e-299">Using Page Inspector with Facebook Template</span></span>

<span data-ttu-id="6027e-300">除錯 Facebook 應用程式時,不能在 Visual Studio 2012 中使用頁面檢查器功能。</span><span class="sxs-lookup"><span data-stu-id="6027e-300">You can't use the Page Inspector feature in Visual Studio 2012 while debugging your Facebook Application.</span></span> <span data-ttu-id="6027e-301">頁面檢查器當前不支援 iframe。</span><span class="sxs-lookup"><span data-stu-id="6027e-301">The Page Inspector does not currently support iframes.</span></span>

### <a name="single-page-application-template-issues"></a><span data-ttu-id="6027e-302">單頁應用程式樣本問題</span><span class="sxs-lookup"><span data-stu-id="6027e-302">Single Page Application Template Issues</span></span>

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a><span data-ttu-id="6027e-303">使用 JQuery 1.9/挖空 2.2.1 更新時,在運行預設 MVC SPA 專案時,新的 todo 項編輯輸入焦點事件處理不正確。</span><span class="sxs-lookup"><span data-stu-id="6027e-303">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter focus event is not handled properly.</span></span>

<span data-ttu-id="6027e-304">使用 JQuery 1.9/挖空 2.2.1 更新,在運行預設 MVC SPA 專案時,新待辦事項編輯在進入待辦事項清單的新待辦事項後不再聚焦到新的待辦事項編輯框。</span><span class="sxs-lookup"><span data-stu-id="6027e-304">With JQuery 1.9/Knockout 2.2.1 update, when running default MVC SPA project, new todo item edit enter no longer focus back to the new todo item edit box after entering the new todo item to the todo list.</span></span>

<span data-ttu-id="6027e-305">要進行解決方法引用[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html),並針對以下範例代碼進行類似的修復:</span><span class="sxs-lookup"><span data-stu-id="6027e-305">To workaround reference [http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html), and make similar fix to the following sample code:</span></span>

<span data-ttu-id="6027e-306">檔案 todo.model.js</span><span class="sxs-lookup"><span data-stu-id="6027e-306">File todo.model.js</span></span>  
 <span data-ttu-id="6027e-307">函數待辦事項(資料),添加以下內容:</span><span class="sxs-lookup"><span data-stu-id="6027e-307">function todolist(data), add following:</span></span>  
 <span data-ttu-id="6027e-308">**自我.is選定 = ko.可觀察(假);**</span><span class="sxs-lookup"><span data-stu-id="6027e-308">**self.isSelected = ko.observable(false);**</span></span>

<span data-ttu-id="6027e-309">函數 todoList.原型.addTodo,添加以下黑色文字:</span><span class="sxs-lookup"><span data-stu-id="6027e-309">function todoList.prototype.addTodo, add the following blacked text:</span></span>  
 <span data-ttu-id="6027e-310">**自我.是選擇(真);**</span><span class="sxs-lookup"><span data-stu-id="6027e-310">**self.isSelected(true);**</span></span>  
 <span data-ttu-id="6027e-311">自我.新托多標題();&quot; &quot;</span><span class="sxs-lookup"><span data-stu-id="6027e-311">self.newTodoTitle(&quot;&quot;);</span></span>

<span data-ttu-id="6027e-312">檔案索引.cshtml,新增以下黑色文字:</span><span class="sxs-lookup"><span data-stu-id="6027e-312">File index.cshtml, add the following blacked text:</span></span>  
 <span data-ttu-id="6027e-313">&lt;表單資料繫結檔&quot;檔:新增Todo&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="6027e-313">&lt;form data-bind=&quot;submit: addTodo&quot;&gt;</span></span>  
 <span data-ttu-id="6027e-314">&lt;輸入類=&quot;addTodo&quot;&quot;類型&quot;&quot;= 文字資料 綁定= 值:newTodoTitle,占位符:"在此處鍵入添加",模糊OnEnter:true,**有焦點:是選定**,事件:[模糊:添加Todo]&quot; /&gt;</span><span class="sxs-lookup"><span data-stu-id="6027e-314">&lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder: 'Type here to add', blurOnEnter: true, **hasfocus: isSelected**, event: { blur: addTodo }&quot; /&gt;</span></span>  
 <span data-ttu-id="6027e-315">&lt;/形式&gt;</span><span class="sxs-lookup"><span data-stu-id="6027e-315">&lt;/form&gt;</span></span>
