---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: 視覺工作室改進 2005 |微軟文件
author: rick-anderson
description: Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542972"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="ccedc-103">Visual Studio 2005 中的改善</span><span class="sxs-lookup"><span data-stu-id="ccedc-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="ccedc-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ccedc-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ccedc-105">Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。</span><span class="sxs-lookup"><span data-stu-id="ccedc-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="ccedc-106">Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。</span><span class="sxs-lookup"><span data-stu-id="ccedc-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="ccedc-107">與 Visual Studio .NET 2002 和 2003 一樣強大,但處理 Web 專案的方式也有很多投訴。</span><span class="sxs-lookup"><span data-stu-id="ccedc-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="ccedc-108">Visual Studio 2005 增加了大量新功能,以解決這些投訴。</span><span class="sxs-lookup"><span data-stu-id="ccedc-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="ccedc-109">對於那些喜歡 Visual Studio .NET 2003 處理 Web 應用程式編譯的方式的使用者,請參閱[Web 應用程式專案](https://go.microsoft.com/fwlink/?LinkId=57870)。</span><span class="sxs-lookup"><span data-stu-id="ccedc-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="ccedc-110">在本模組中,很好地涵蓋了 Web 專案創建、管理和開發方面的改進。</span><span class="sxs-lookup"><span data-stu-id="ccedc-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="ccedc-111">在後面的模組中,很好地涵蓋了構建 Web 專案並部署它們的改進。</span><span class="sxs-lookup"><span data-stu-id="ccedc-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="ccedc-112">首頁伺服器延伸</span><span class="sxs-lookup"><span data-stu-id="ccedc-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="ccedc-113">Visual Studio .NET 2002 和 2003 需要框上的 FrontPage 伺服器擴展,以便創建或生成 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="ccedc-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="ccedc-114">開發人員在兩種不同的訪問模式(FrontPage 伺服器擴展名或文件存取模式)之間進行選擇,這兩種模式都使用 FrontPage 伺服器擴展程式執行諸如在 IIS 中設置應用程式根等任務。</span><span class="sxs-lookup"><span data-stu-id="ccedc-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="ccedc-115">Visual Studio 2005 消除了對本地專案 FrontPage 伺服器擴展的依賴。</span><span class="sxs-lookup"><span data-stu-id="ccedc-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="ccedc-116">Visual Studio 2005 現在直接存取IIS元庫,而不是使用FrontPage伺服器擴展。</span><span class="sxs-lookup"><span data-stu-id="ccedc-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="ccedc-117">Visual Studio 2005 還添加了對 FTP 的支援,該支援允許遠端項目訪問,而無需 FrontPage 伺服器擴展。</span><span class="sxs-lookup"><span data-stu-id="ccedc-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="ccedc-118">對於那些想要在其專案中使用 FrontPage 伺服器擴展的開發人員,該選項仍然可用。</span><span class="sxs-lookup"><span data-stu-id="ccedc-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="ccedc-119">但是,根據ASP.NET開發人員社區的強烈反饋,這不是一項要求。</span><span class="sxs-lookup"><span data-stu-id="ccedc-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-120">遠端項目創建、打開等仍然需要 FrontPage 伺服器擴展。</span><span class="sxs-lookup"><span data-stu-id="ccedc-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="ccedc-121">ASP.NET 程式開發伺服器</span><span class="sxs-lookup"><span data-stu-id="ccedc-121">ASP.NET Development Server</span></span>

<span data-ttu-id="ccedc-122">Visual Studio 2005 附帶了一個名為ASP.NET開發伺服器的新 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="ccedc-123">(此 Web 伺服器以前稱為卡西尼。</span><span class="sxs-lookup"><span data-stu-id="ccedc-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="ccedc-124">ASP.NET開發伺服器有幾個好處。</span><span class="sxs-lookup"><span data-stu-id="ccedc-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="ccedc-125">現在,非管理員可以針對 Web 伺服器開發和調試。</span><span class="sxs-lookup"><span data-stu-id="ccedc-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="ccedc-126">ASP.NET開發伺服器動態地將虛擬目錄映射到檔案系統中的任何位置,從而允許靈活的專案位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="ccedc-127">Windows XP 專業版上已經使用 IIS 的使用者現在將能夠創建新的 Web 應用程式,這些應用程式不會影響其在 IIS 中的預設網站的檔案或資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="ccedc-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="ccedc-128">無需特殊配置即可利用ASP.NET開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="ccedc-129">當檔案系統上託管的 Web 專案被調試或流覽時,Visual Studio 2005 將自動啟動隨機埠上的 ASP.NET 開發伺服器的實例來為請求提供服務。</span><span class="sxs-lookup"><span data-stu-id="ccedc-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="ccedc-130">本模組稍後將介紹ASP.NET開發伺服器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="ccedc-131">改進的檔案管理</span><span class="sxs-lookup"><span data-stu-id="ccedc-131">Improved File Management</span></span>

<span data-ttu-id="ccedc-132">在 Visual Studio 2002 和 2003 中,一個專案檔(VB.NET.vbproj 和 .csproj 表示 C#)儲存了 Web 應用程式中所有檔案的資訊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="ccedc-133">解決方案資源管理員顯示基於專案檔中的檔資訊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="ccedc-134">因此,在使用外部編輯器的情況下,解決方案資源管理器通常會顯示不準確的資訊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="ccedc-135">Visual Studio 2002 和 2003 通常會覆蓋檔更改或不顯示最新版本的檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="ccedc-136">Visual Studio 2005 不需要使用專案檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="ccedc-137">相反,它直接從磁碟讀取檔和資料夾資訊,從而準確顯示專案中的檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="ccedc-138">由於 Visual Studio 2002 和 2003 中的「引用」資料夾不表示 Web 應用程式中的實際資料夾,因此 Visual Studio 2005 還會從解決方案資源管理器中刪除"引用"資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="ccedc-139">要造訪 Visual Studio 2005 中的專案的引用,應使用專案的屬性頁。</span><span class="sxs-lookup"><span data-stu-id="ccedc-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="ccedc-140">建立 Web 專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-140">Creating Web Projects</span></span>

<span data-ttu-id="ccedc-141">Web 開發人員在 Visual Studio 2005 中有許多可用於專案創建的新選項。</span><span class="sxs-lookup"><span data-stu-id="ccedc-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="ccedc-142">網站現在可以在檔案系統的任意位置創建,然後可以使用新的ASP.NET開發伺服器進行調試或流覽。</span><span class="sxs-lookup"><span data-stu-id="ccedc-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="ccedc-143">開發人員還可以使用 FTP 創建新的網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="ccedc-144">按一下此處查看 Visual Studio 2005 中創建 Web 專案的影片演練。</span><span class="sxs-lookup"><span data-stu-id="ccedc-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="ccedc-145">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="ccedc-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="ccedc-146">檔案系統專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-146">File System Projects</span></span>

<span data-ttu-id="ccedc-147">正如您在影片演練中所看到的,您可以選擇透過檔共享在檔案系統上或在遠端位置創建網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="ccedc-148">使用ASP.NET開發伺服器瀏覽和除錯在檔案系統上創建的網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-149">ASP.NET開發伺服器可能會給客戶帶來一些混亂。</span><span class="sxs-lookup"><span data-stu-id="ccedc-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="ccedc-150">如果在 IS 目錄結構(即 c:/inetpub/wwwroot)的檔案系統上創建了 Web 專案,則從 Visual Studio 2005 內部啟動時,該網站仍將通過 ASP.NET 開發伺服器進行流覽。</span><span class="sxs-lookup"><span data-stu-id="ccedc-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="ccedc-151">因此,任何IIS配置(即身份驗證方法)都不適用。</span><span class="sxs-lookup"><span data-stu-id="ccedc-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="ccedc-152">默認 Web 專案還僅包括 Default.aspx 頁、default.cs 檔和 App/_Data 資料夾,從而刪除了大量開銷。</span><span class="sxs-lookup"><span data-stu-id="ccedc-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="ccedc-153">根據需要添加 Web.config 和特殊資料夾(即應用/_code)。</span><span class="sxs-lookup"><span data-stu-id="ccedc-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="ccedc-154">您的 Web 專案僅包括所需的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="ccedc-155">HTTP 專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-155">HTTP Projects</span></span>

<span data-ttu-id="ccedc-156">HTTP 專案可以是在本地 IIS 網站或遠端網站上創建的專案。</span><span class="sxs-lookup"><span data-stu-id="ccedc-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="ccedc-157">預設項目位置為`http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="ccedc-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="ccedc-158">如果按下「瀏覽」按鈕,則有兩個 HTTP 選項:本地 IIS 和遠端網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="ccedc-159">這兩個選項的主要區別是在"選擇位置"對話框中顯示網站資訊的方法以及檔案複製到 Web 伺服器的方式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="ccedc-160">"本地 IIS"選項從本地電腦上的中式庫讀取網站資訊,並使用檔案系統複製檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="ccedc-161">遠端站點選項使用 FrontPage 伺服器擴展名,網站資訊和檔使用 HTTP 和 FrontPage 伺服器擴展程式 RPC 呼叫進行複製。</span><span class="sxs-lookup"><span data-stu-id="ccedc-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-162">vs_/_tmp.htm 檔和 get/_aspx/_ver.aspx 不再用於確定版本資訊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="ccedc-163">默認 HTTP 選項為本地 IIS。</span><span class="sxs-lookup"><span data-stu-id="ccedc-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="ccedc-164">此選項讀取 IIS 中庫以確定哪些網站可用以及創建內容的位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="ccedc-165">您可以透過在樹檢視中選擇其他資料夾或虛擬目錄來選擇它。</span><span class="sxs-lookup"><span data-stu-id="ccedc-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="ccedc-166">您還可以創建新的虛擬目錄、將資料夾標記為應用程式,以及從此對話框中刪除現有的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="ccedc-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

![選擇位置對話框](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="ccedc-168">**圖 1**: 選擇位置對話框</span><span class="sxs-lookup"><span data-stu-id="ccedc-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="ccedc-169">與早期版本的 Visual Studio 不同,如果選中 **「使用安全套接字層」** 複選框,並且 SSL 證書與您正在流覽的 URL 不匹配,則將顯示一個安全警報對話框,詢問您是否要繼續。</span><span class="sxs-lookup"><span data-stu-id="ccedc-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="ccedc-170">使用 Visual Studio .NET 2003,如果證書不是匹配的,則創建項目將失敗。</span><span class="sxs-lookup"><span data-stu-id="ccedc-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![有關 SSL 憑證的安全警示](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="ccedc-172">**圖 2**: 有關 SSL 憑證的安全警示</span><span class="sxs-lookup"><span data-stu-id="ccedc-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="ccedc-173">主機標題上的註解</span><span class="sxs-lookup"><span data-stu-id="ccedc-173">Note on Host Headers</span></span>

<span data-ttu-id="ccedc-174">如果要在綁定到特定 IP 的站台上創建 Web 應用程式,則需要確保配置主機標頭。</span><span class="sxs-lookup"><span data-stu-id="ccedc-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="ccedc-175">否則,Visual Studio`http://localhost`將在中創建網站,但當從 IDE 內部流覽或調試網站時,IP 位址將無法正確解析。</span><span class="sxs-lookup"><span data-stu-id="ccedc-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="ccedc-176">如果選擇「遠端網站」選項,則對話框將更改以允許您輸入新網站的目標 URL。</span><span class="sxs-lookup"><span data-stu-id="ccedc-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="ccedc-177">此 URL 必須位於已啟用了 FrontPage 伺服器擴展名的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="ccedc-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="ccedc-178">如果要使用 FrontPage 伺服器擴展程式使用本地 Web 伺服器,可以使用「遠端網站」選項並指定本地網址。</span><span class="sxs-lookup"><span data-stu-id="ccedc-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![在遠端伺服器上建立網站](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="ccedc-180">**圖 3**: 在遠端伺服器上建立網站</span><span class="sxs-lookup"><span data-stu-id="ccedc-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="ccedc-181">通過 SSL 在遠端網站上創建應用程式時,如果 SSL 證書不匹配,則確認對話方塊與使用本地 IIS 選項時顯示的對話方塊略有不同。</span><span class="sxs-lookup"><span data-stu-id="ccedc-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![遠端網站安全警報](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="ccedc-183">**圖 4**: 遠端站台安全警示</span><span class="sxs-lookup"><span data-stu-id="ccedc-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="ccedc-184">FTP</span><span class="sxs-lookup"><span data-stu-id="ccedc-184">FTP</span></span>

<span data-ttu-id="ccedc-185">Visual Studio 2005 引入了透過 FTP 創建網站的選項。</span><span class="sxs-lookup"><span data-stu-id="ccedc-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="ccedc-186">使用此選項時,IDE 會在使用者臨時資料夾中在本地創建檔案,然後使用 FTP 將檔案移動到 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-187">暫存資料夾位置為 c:/文件與&lt;設定&gt;/ 使用者 /本地設定/Temp/VWDWebCache/&lt;伺服器&gt;/=&lt;應用程式名稱&gt;</span><span class="sxs-lookup"><span data-stu-id="ccedc-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="ccedc-188">使用 FTP 選項時,將顯示「選擇位置」對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="ccedc-189">在此對話框中輸入所需的 FTP 連接資訊,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP 選擇位置對話框](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="ccedc-191">**圖 5**: FTP 的"選擇位置對話方塊"</span><span class="sxs-lookup"><span data-stu-id="ccedc-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="ccedc-192">實驗室:設定 FTP 網站並建立專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="ccedc-193">以下步驟配置 FTP 網站,以便使用者具有只有他們才能通過 FTP 上載到的位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="ccedc-194">安裝 FTP 服務</span><span class="sxs-lookup"><span data-stu-id="ccedc-194">Install the FTP Service</span></span>

1. <span data-ttu-id="ccedc-195">打開"添加刪除程式",選擇"添加/刪除 Windows 元件"</span><span class="sxs-lookup"><span data-stu-id="ccedc-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="ccedc-196">選擇互聯網資訊服務(Windows 2003 上的應用程式伺服器),然後單擊 **「詳細資訊**」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="ccedc-197">檢查**檔案傳輸協定 (FTP) 服務**,然後按一下 **「確定**」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="ccedc-198">按下 **「下一步**」以安裝 FTP 服務。</span><span class="sxs-lookup"><span data-stu-id="ccedc-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="ccedc-199">建立新資料夾</span><span class="sxs-lookup"><span data-stu-id="ccedc-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="ccedc-200">在 Windows 資源管理器中,在 c:/inetpub/wwwroot 內部創建名為**User1**的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="ccedc-201">配置資料夾和資料夾的許可權。</span><span class="sxs-lookup"><span data-stu-id="ccedc-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="ccedc-202">從管理工具打開互聯網資訊服務快照。</span><span class="sxs-lookup"><span data-stu-id="ccedc-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="ccedc-203">現在,您的電腦名稱節點下將有一個 FTP Sites 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="ccedc-204">延伸**FTP 網站**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="ccedc-205">右鍵按一下**預設 FTP 網站**,選擇 **"新建**",然後按一下 **「\*\*\*\*下一步**」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="ccedc-206">輸入虛擬目錄名稱**的使用者 1,** 然後按下 **「下一步**」 。</span><span class="sxs-lookup"><span data-stu-id="ccedc-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="ccedc-207">輸入**路徑的 c:/inetpub/wwwroot/User1,** 然後單擊 **"下一步**"。</span><span class="sxs-lookup"><span data-stu-id="ccedc-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="ccedc-208">按下 **「下一步\*\*\*\*」,然後單擊"完成"** 以完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="ccedc-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="ccedc-209">右鍵按這裏預設 FTP 網站下的**User1**虛擬目錄,然後選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="ccedc-210">選中 **「寫入」** 複選框,然後按下 **「 確定」** 以關閉對話框。</span><span class="sxs-lookup"><span data-stu-id="ccedc-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="ccedc-211">右鍵按下**預設 FTP 網站**並選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="ccedc-212">在「**安全帳戶」** 選項卡上,取消選中 **「允許匿名連接**」。。</span><span class="sxs-lookup"><span data-stu-id="ccedc-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="ccedc-213">在對話框中按下 **「是**」,詢問是否要繼續。</span><span class="sxs-lookup"><span data-stu-id="ccedc-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="ccedc-214">按一下 **[確定]** 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="ccedc-215">在 **「網站」** 節點下展開**預設網站**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="ccedc-216">右鍵單擊**User1**目錄並選擇 **"屬性"**</span><span class="sxs-lookup"><span data-stu-id="ccedc-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="ccedc-217">在「**應用程式設定」** 部分中,按一下「**創建**」 將資料夾標記為應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="ccedc-218">按一下 **[確定]** 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccedc-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="ccedc-219">關閉互聯網資訊服務卡入。</span><span class="sxs-lookup"><span data-stu-id="ccedc-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="ccedc-220">建立 Web 專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-220">Create web project</span></span>

1. <span data-ttu-id="ccedc-221">開放視覺工作室 2005.</span><span class="sxs-lookup"><span data-stu-id="ccedc-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="ccedc-222">在 **「檔案」** 選單中,選擇 **「新建網站**」 。。</span><span class="sxs-lookup"><span data-stu-id="ccedc-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="ccedc-223">在 **'位置**' 下拉下清單中, 選擇**FTP**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="ccedc-224">按一下 [瀏覽]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="ccedc-224">Click **Browse**.</span></span>
5. <span data-ttu-id="ccedc-225">輸入**本地**端的伺服器文字盒中輸入**本地端主機**。</span><span class="sxs-lookup"><span data-stu-id="ccedc-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="ccedc-226">在「目錄」文字框中輸入**使用者 1。**</span><span class="sxs-lookup"><span data-stu-id="ccedc-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="ccedc-227">按一下 [開啟]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="ccedc-227">Click **Open**.</span></span> <span data-ttu-id="ccedc-228">FTP 位置將輸入到"新建網站"對話框中。</span><span class="sxs-lookup"><span data-stu-id="ccedc-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="ccedc-229">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="ccedc-229">Click **OK**.</span></span>
9. <span data-ttu-id="ccedc-230">取消在 FTP 登入對話方塊中**打開匿名登錄**,輸入認證,然後單擊「**確定**」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="ccedc-231">專案的 URL 是什麼?</span><span class="sxs-lookup"><span data-stu-id="ccedc-231">What is the URL for the project?</span></span> <span data-ttu-id="ccedc-232">(專案的網址將顯示在解決方案資源管理員中。</span><span class="sxs-lookup"><span data-stu-id="ccedc-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="ccedc-233">在 **「生成」** 選單中,選擇 **「生成網站**」或 **「生成解決方案**」 。</span><span class="sxs-lookup"><span data-stu-id="ccedc-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="ccedc-234">右鍵單擊解決方案資源管理器中的 Default.aspx,然後選擇 **「瀏覽器中的檢視**」。。</span><span class="sxs-lookup"><span data-stu-id="ccedc-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="ccedc-235">在「網站網址必需」對話框中,`http://localhost/user1`輸入 URL 並按一下「**確定**」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-236">如果收到指示無法載入類型 /_Default的錯誤,請確保在 Web 網站上運行 ASP.NET 2.0,而不是早期版本。</span><span class="sxs-lookup"><span data-stu-id="ccedc-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="ccedc-237">您可以在「互聯網資訊服務」 中的 ASP.NET 選項卡上執行此操作。</span><span class="sxs-lookup"><span data-stu-id="ccedc-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="ccedc-238">開啟網頁專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-238">Opening Web Projects</span></span>

<span data-ttu-id="ccedc-239">打開 Web 專案類似於建立專案。</span><span class="sxs-lookup"><span data-stu-id="ccedc-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="ccedc-240">以下各節會標註在IDE中工作時注意的區域。</span><span class="sxs-lookup"><span data-stu-id="ccedc-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="ccedc-241">它還涵蓋使用 HTTP 和 FTP 處理 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="ccedc-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="ccedc-242">要打開 Web 專案,請從「檔」功能表中選擇「打開網站」。</span><span class="sxs-lookup"><span data-stu-id="ccedc-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="ccedc-243">系統、本地 IIS、FTP 和遠端網站,系統將提示您使用以前介紹的相同"選擇位置"對話框,並且有相同的四個選項可供您使用。</span><span class="sxs-lookup"><span data-stu-id="ccedc-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="ccedc-244">檔案系統</span><span class="sxs-lookup"><span data-stu-id="ccedc-244">File System</span></span>

<span data-ttu-id="ccedc-245">如本模組前面所述,Visual Studio 不再使用專案檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="ccedc-246">因此,如果您選擇從檔案系統打開網站,則實際上可以選擇任何希望選擇的資料夾,即使您選擇的資料夾最初未在 Visual Studio 中作為 Web 專案創建。</span><span class="sxs-lookup"><span data-stu-id="ccedc-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="ccedc-247">例如,您可以選擇以網站身份打開"我的文檔"資料夾,Visual Studio 將愉快地打開該資料夾並顯示您的檔,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![我的文件作為網站開啟](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="ccedc-249">**圖 6**:*我的文件*作為網站開啟</span><span class="sxs-lookup"><span data-stu-id="ccedc-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="ccedc-250">由於 Visual Studio 僅在必要時創建其他檔和資料夾,因此不會將其他檔案或資料夾添加到您打開的位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="ccedc-251">此體系結構的副作用是,它可以防止您在文件系統上嵌套網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="ccedc-252">例如,請考慮以下目錄結構。</span><span class="sxs-lookup"><span data-stu-id="ccedc-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="ccedc-253">C:/我的Web網站網路專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="ccedc-254">C:/MyWebSite/嵌套的另一個 Web 專案</span><span class="sxs-lookup"><span data-stu-id="ccedc-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="ccedc-255">當您在 c:/MyWebSite 打開網站時,「嵌套」資料夾將顯示為該應用程式的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="ccedc-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="ccedc-256">HTTP</span></span>

<span data-ttu-id="ccedc-257">通過 HTTP 打開網站時,可以從 IIS 中庫(本地 IIS)或使用 FrontPage 伺服器擴展(遠端網站)讀取設置。如果有嵌套 Web 應用程式,則這些應用程式將顯示,並帶有一個圖示,用於標識它們為應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="ccedc-258">如果您熟悉在 FrontPage 中處理 Web 應用程式,則 Visual Studio 2005 中的行為類似。</span><span class="sxs-lookup"><span data-stu-id="ccedc-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="ccedc-259">即使 Visual Studio 將顯示嵌套在 IDE 中當前打開的應用程式下方的應用程式的圖示,但它也不允許擴展它們以查看其內容。</span><span class="sxs-lookup"><span data-stu-id="ccedc-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="ccedc-260">但是,您可以雙擊它們以打開它們。</span><span class="sxs-lookup"><span data-stu-id="ccedc-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="ccedc-261">執行此操作時,將顯示一個對話框,提示您打開 Web 應用程式(並取代當前打開的解決方案)或將 Web 應用程式添加到當前解決方案。</span><span class="sxs-lookup"><span data-stu-id="ccedc-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![按兩下嵌 sotcrit 的資訊標示會顯示此對話框](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="ccedc-263">**圖 7**: 雙擊嵌套應用程式圖示將為您提供此對話框</span><span class="sxs-lookup"><span data-stu-id="ccedc-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="ccedc-264">FTP 站台</span><span class="sxs-lookup"><span data-stu-id="ccedc-264">FTP Site</span></span>

<span data-ttu-id="ccedc-265">當您透過 FTP 打開網站時,這些檔都將在本地複製到暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="ccedc-266">本地儲存位置的完整路徑顯示在專案的"屬性"窗格中,並使用以下格式創建。</span><span class="sxs-lookup"><span data-stu-id="ccedc-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="ccedc-267">C:/文件與設定/&lt;&gt;使用者 /本地設定/Temp/VWDWebCache/&lt;伺服器&gt;/=&lt;應用程式名稱&gt;</span><span class="sxs-lookup"><span data-stu-id="ccedc-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="ccedc-268">使用 FTP 時,Visual Studio 需要指定專案的基本 URL,以便可以流覽它,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="ccedc-269">如果不指定基本 URL,Visual Studio 將在您首次嘗試瀏覽網站中的頁面時詢問它。</span><span class="sxs-lookup"><span data-stu-id="ccedc-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![為 FTP 網站指定基本網址](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="ccedc-271">**圖 8**: 為 FTP 網站指定基本網址</span><span class="sxs-lookup"><span data-stu-id="ccedc-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="ccedc-272">編譯的改進</span><span class="sxs-lookup"><span data-stu-id="ccedc-272">Improvements in Compilation</span></span>

<span data-ttu-id="ccedc-273">在 Visual Studio 2005 中處理 Web 應用程式的速度明顯快於以前的版本。</span><span class="sxs-lookup"><span data-stu-id="ccedc-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="ccedc-274">這在很大程度上是由於編譯體系結構的更改。</span><span class="sxs-lookup"><span data-stu-id="ccedc-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="ccedc-275">在 Visual Studio 2002 和 2003 中,Web 應用程式被編譯為駐留在 /bin 資料夾中的一個主程式集。</span><span class="sxs-lookup"><span data-stu-id="ccedc-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="ccedc-276">在 Visual Studio 2005 中,添加了一個應用/_Code資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="ccedc-277">類和其他非 UI 代碼將添加到應用/_Code資料夾。</span><span class="sxs-lookup"><span data-stu-id="ccedc-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="ccedc-278">當 Visual Studio 生成專案時,App/_Code 資料夾中的所有檔都將編譯為單個 App/_Code.dll 檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="ccedc-279">此更改的結果是後續生成比早期版本快得多。</span><span class="sxs-lookup"><span data-stu-id="ccedc-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-280">MSBuild 命令行實用程式還可用於建構ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="ccedc-281">該工具將在第 9 單元中介紹。</span><span class="sxs-lookup"><span data-stu-id="ccedc-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="ccedc-282">另一個編譯增強功能是"生成"功能表上的新"生成頁"選項。</span><span class="sxs-lookup"><span data-stu-id="ccedc-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="ccedc-283">此功能允許開發人員僅重建當前頁面(當然,以及依賴項),以便可以更快地編譯更改。</span><span class="sxs-lookup"><span data-stu-id="ccedc-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="ccedc-284">由於 C# 不提供用於更新 IntelliSense 等的背景編譯,因此它們將從此功能中獲益匪淺,因為它將允許通過僅重建單個頁面快速更新 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ccedc-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="ccedc-285">專案的生成屬性允許您設定在執行啟動頁之前發生的生成類型。</span><span class="sxs-lookup"><span data-stu-id="ccedc-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="ccedc-286">開發人員可以選擇僅生成當前頁面,以便 Visual Studio 可以在代碼更改後更快地開始調試應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

![製作頁啟動](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="ccedc-288">**圖 9**: 產生頁面開始操作</span><span class="sxs-lookup"><span data-stu-id="ccedc-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="ccedc-289">Visual Studio 和 ASP.NET架構的另一大增強是在編輯和繼續方面。</span><span class="sxs-lookup"><span data-stu-id="ccedc-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="ccedc-290">在 Visual Studio 2005 中,開發人員可以開始調試專案,並在專案上進行代碼更改,而無需分離調試器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="ccedc-291">事實上,您可以從字面上開始調試專案、添加新類、向該類添加代碼、向創建該類的新實例的頁面添加代碼以及執行類的方法,所有這些都不分離調試器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="ccedc-292">執行新代碼實際上和刷新瀏覽器一樣簡單!</span><span class="sxs-lookup"><span data-stu-id="ccedc-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="ccedc-293">按一下此處查看 Visual Studio 2005 中編輯影片演練並繼續功能。</span><span class="sxs-lookup"><span data-stu-id="ccedc-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="ccedc-294">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="ccedc-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="ccedc-295">ASP.NET 2.0 和 Visual Studio 2005 中強大的編輯和繼續功能是由於ASP.NET應用程式的體系結構更改。</span><span class="sxs-lookup"><span data-stu-id="ccedc-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="ccedc-296">在 ASP.NET 1.x 中,在 Visual Studio 2002/2003 中創建的應用程式編譯為存儲在 /bin 資料夾中的主程式集。</span><span class="sxs-lookup"><span data-stu-id="ccedc-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="ccedc-297">應用程式的所有類、頁面等都編譯到該 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="ccedc-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="ccedc-298">然後在運行時,ASP.NET將編譯頁面中的所有控制件、標記和ASP.NET代碼,並將這些DLL複製到ASP.NET臨時資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ccedc-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="ccedc-299">在使用 ASP.NET 2.0 的 Visual Studio 2005 中,上述兩個編譯模型(一個用於 Visual Studio,一個用於運行時 ASP.NET)已合併為一個通用編譯模型。</span><span class="sxs-lookup"><span data-stu-id="ccedc-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="ccedc-300">這意味著所有編譯問題現在都在開發階段而不是運行時捕獲。</span><span class="sxs-lookup"><span data-stu-id="ccedc-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="ccedc-301">它還允許設計器和 IntelliSense 支援使用者控制件和母版頁等功能。</span><span class="sxs-lookup"><span data-stu-id="ccedc-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="ccedc-302">按一次檢視設計器對使用者控制的影片演練。</span><span class="sxs-lookup"><span data-stu-id="ccedc-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="ccedc-303">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="ccedc-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="ccedc-304">從頁面中刪除使用者控制項時,@Register該指令將保留在標記中,並且應手動刪除,以避免在從網站中刪除使用者控制項時解析器錯誤。</span><span class="sxs-lookup"><span data-stu-id="ccedc-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="ccedc-305">可視化工作室編譯模型的另一個改進是發佈網站功能。</span><span class="sxs-lookup"><span data-stu-id="ccedc-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="ccedc-306">由於「發佈」功能預先編譯了網站,因此開發人員可以享受無需按需編譯任何內容的額外性能。</span><span class="sxs-lookup"><span data-stu-id="ccedc-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="ccedc-307">它還將 App/_Code 資料夾中的所有原始程式碼預編譯為 DLL,以便無需部署原始碼。</span><span class="sxs-lookup"><span data-stu-id="ccedc-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

![發布網站對話框](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="ccedc-309">**圖 10**: 發布網站對話框</span><span class="sxs-lookup"><span data-stu-id="ccedc-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-310">aspnet/_compile.exe 實用程式也可用於預編譯ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="ccedc-311">該工具將在第 9 單元中介紹。</span><span class="sxs-lookup"><span data-stu-id="ccedc-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="ccedc-312">發佈網站時,預編譯檔將存儲在臨時ASP.NET檔資料夾中,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="ccedc-313">具有 *.ssd*檔案副檔名的檔案是定義特定 DLL 依賴項的 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="ccedc-314">任何 Web 窗體或使用者控制器都編譯為以*應用 _/Web/_* 開頭的隨機 DLL。</span><span class="sxs-lookup"><span data-stu-id="ccedc-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="ccedc-315">如果選擇「*允許此預編譯網站可升級」* 複選框,則 Web 窗體和使用者控制件內的標記將不會預先編譯為 DLL,從而允許您在部署後進行更改。</span><span class="sxs-lookup"><span data-stu-id="ccedc-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="ccedc-316">如果您希望鎖定標記以不允許更改已部署的內容,請取消選中此框。</span><span class="sxs-lookup"><span data-stu-id="ccedc-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="ccedc-317">*使用固定命名和單頁程式集*複選框允許您禁用批處理編譯,以便將每個頁面編譯為固定命名的程式集。</span><span class="sxs-lookup"><span data-stu-id="ccedc-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="ccedc-318">未勾選此方塊允許您利用批次處理編譯。</span><span class="sxs-lookup"><span data-stu-id="ccedc-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="ccedc-319">*啟用預編譯程式集上的強命名*複選方塊允許您對預編譯程式集進行強名稱。</span><span class="sxs-lookup"><span data-stu-id="ccedc-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-320">在 ASP.NET 1.x 中,必須將強名稱程式集安裝到全域程式集緩存 (GAC)。</span><span class="sxs-lookup"><span data-stu-id="ccedc-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="ccedc-321">在 ASP.NET 2.0 中,您不需要在 GAC 中安裝強名稱程式集。</span><span class="sxs-lookup"><span data-stu-id="ccedc-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET應用程式預先編譯檔](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="ccedc-323">**圖11:ASP.NET**應用程式預編譯檔</span><span class="sxs-lookup"><span data-stu-id="ccedc-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-324">在上面的應用程式中,沒有 Web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="ccedc-325">如果有,它將在發佈網站過程后稱為*預編譯App.config。*</span><span class="sxs-lookup"><span data-stu-id="ccedc-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="ccedc-326">部署的改進</span><span class="sxs-lookup"><span data-stu-id="ccedc-326">Improvements in Deployment</span></span>

<span data-ttu-id="ccedc-327">與 Visual Studio 2002 和 2003 一樣,Visual Studio 2005 提供了複製專案功能。</span><span class="sxs-lookup"><span data-stu-id="ccedc-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="ccedc-328">但是,該功能已在 Visual Studio 2005 中進行了增強,現在稱為"複製網站"。</span><span class="sxs-lookup"><span data-stu-id="ccedc-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="ccedc-329">複製網站"對話框將拆分為左側框架和右框架。</span><span class="sxs-lookup"><span data-stu-id="ccedc-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="ccedc-330">左幀稱為源網站,右框架稱為遠程網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="ccedc-331">有一件事可能會令一些開發人員感到困惑,那就是顯示在正確框架中的網站不一定是遠端網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="ccedc-332">它可以是本地文件系統或IIS本地實例上的網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="ccedc-333">此外,左側框架中顯示的網站不一定是源網站,因為對話框允許您從遠端網站*發佈到*源網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="ccedc-334">如果要將專案複製到遠端網站,則該站點必須安裝 FrontPage 伺服器擴展程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="ccedc-335">如果沒有,則需要使用 FTP 進行連接。</span><span class="sxs-lookup"><span data-stu-id="ccedc-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="ccedc-336">另一方面,如果要將專案複製到本地 IIS 實例,則不需要 FrontPage 伺服器擴展。</span><span class="sxs-lookup"><span data-stu-id="ccedc-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-337">如果您嘗試在本地 IIS 實例上創建新網站,並且安裝了 FrontPage 2002 伺服器擴展程式,則會收到一條錯誤消息,告訴您在 SharePoint 伺服器上不支援創建網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="ccedc-338">在這種情況下,您可以選擇安裝 FrontPage 2000 伺服器擴展或刪除 FrontPage 伺服器擴展名。</span><span class="sxs-lookup"><span data-stu-id="ccedc-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="ccedc-339">按一下此處查看複製網站功能的視頻演練。</span><span class="sxs-lookup"><span data-stu-id="ccedc-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="ccedc-340">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="ccedc-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="ccedc-341">除錯改進</span><span class="sxs-lookup"><span data-stu-id="ccedc-341">Improvements in Debugging</span></span>

<span data-ttu-id="ccedc-342">Visual Studio 2005 中的調試有四個關鍵改進。</span><span class="sxs-lookup"><span data-stu-id="ccedc-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="ccedc-343">以非管理員身份在本地進行調試可以開箱即用。</span><span class="sxs-lookup"><span data-stu-id="ccedc-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="ccedc-344">默認情況下,編譯元素的調試屬性現在為 false。</span><span class="sxs-lookup"><span data-stu-id="ccedc-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="ccedc-345">遠端調試設置和配置比以前更容易。</span><span class="sxs-lookup"><span data-stu-id="ccedc-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="ccedc-346">現在,您可以調試通過 FTP 位置打開的網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="ccedc-347">作為非管理員進行除錯</span><span class="sxs-lookup"><span data-stu-id="ccedc-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="ccedc-348">添加ASP.NET開發伺服器允許非管理員輕鬆調試ASP.NET應用程式開箱即用。</span><span class="sxs-lookup"><span data-stu-id="ccedc-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="ccedc-349">除錯本地檔案系統上執行ASP.NET應用程式時,Visual Studio在登入使用者的上下文中啟動ASP.NET開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="ccedc-350">然後,該使用者可以調試該應用程式,而無需任何其他配置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="ccedc-351">預設情況下,除錯為 false</span><span class="sxs-lookup"><span data-stu-id="ccedc-351">Debug is False by Default</span></span>

<span data-ttu-id="ccedc-352">在 ASP.NET 1.x 中,預設情況下,Web.config 檔*編譯*元素中的*調試*屬性設置為*true。*</span><span class="sxs-lookup"><span data-stu-id="ccedc-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="ccedc-353">始終建議開發人員在將應用程式部署到生產之前將此屬性設置為*false,* 但由於大多數開發人員並不完全瞭解將調試屬性設置為 true 的後果,因此他們只是將其保留原樣。</span><span class="sxs-lookup"><span data-stu-id="ccedc-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="ccedc-354">將除錯屬性設定為 true 的最嚴重的問題是禁用 ASP.NETs 批次處理編譯模型。</span><span class="sxs-lookup"><span data-stu-id="ccedc-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="ccedc-355">因此,每個頁面都編譯成一個單獨的 DLL。</span><span class="sxs-lookup"><span data-stu-id="ccedc-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="ccedc-356">如果 Web 應用程式由數千個頁面組成(並非任何方法所聞所未聞),則這意味著該應用程式將創建數千個小型 DLL。</span><span class="sxs-lookup"><span data-stu-id="ccedc-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="ccedc-357">雖然這些 DLL 大小較小,但它們不會載入到記憶體中的任何特定位置。</span><span class="sxs-lookup"><span data-stu-id="ccedc-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="ccedc-358">因此,它們會導致系統記憶體中的碎片,並可能導致記憶體外異常事件。</span><span class="sxs-lookup"><span data-stu-id="ccedc-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="ccedc-359">在 ASP.NET 2.0 中,默認情況下調試屬性設置為 false。</span><span class="sxs-lookup"><span data-stu-id="ccedc-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="ccedc-360">正如您已經看到的那樣,當開發人員在 Visual Studio 2005 中調試ASP.NET應用程式時,系統會提示他們添加啟用調試的 Web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="ccedc-361">這樣做會產生與ASP.NET 1.x 中相同的缺點,但現在開發人員被明確警告,在將應用程式移動到生產之前,應將屬性重置為 false。</span><span class="sxs-lookup"><span data-stu-id="ccedc-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="ccedc-362">遠端除錯設定與設定</span><span class="sxs-lookup"><span data-stu-id="ccedc-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="ccedc-363">在 Visual Studio 2002/2003 中,遠端調試依賴於電腦調試管理器 (mdm.exe) 和 vs7jit.exe 過程。</span><span class="sxs-lookup"><span data-stu-id="ccedc-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="ccedc-364">因此,排除遠端調試問題的故障通常是客戶的一個黑匣子,對 PSS 通常沒有多大説明。</span><span class="sxs-lookup"><span data-stu-id="ccedc-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="ccedc-365">Visual Studio 2005 消除了對 mdm.exe 和 vs7jit.exe 進程的依賴。</span><span class="sxs-lookup"><span data-stu-id="ccedc-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="ccedc-366">相反,它現在使用遠端除錯監視器服務 (msvsmon.exe.)</span><span class="sxs-lookup"><span data-stu-id="ccedc-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="ccedc-367">Visual Studio 2005 遠程調試的要求非常簡單。</span><span class="sxs-lookup"><span data-stu-id="ccedc-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="ccedc-368">在除錯之前,您需要在遠端伺服器上執行 msvsmon.exe。</span><span class="sxs-lookup"><span data-stu-id="ccedc-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="ccedc-369">可以從 Visual Studio CD 安裝遠端除錯監視器,也可以簡單地從共享運行 msvsmon.exe,而無需在 Web 伺服器上安裝任何內容。</span><span class="sxs-lookup"><span data-stu-id="ccedc-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="ccedc-370">運行 msvsmon.exe 時,可能會抱怨埠被阻止進行遠端調試。</span><span class="sxs-lookup"><span data-stu-id="ccedc-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="ccedc-371">幸運的是,您可以在警告對話框中輕鬆取消阻止埠,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![通知 Windows 防火牆封鎖遠端除錯](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="ccedc-373">**圖 12**: 通知 Windows 防火牆封鎖遠端除錯</span><span class="sxs-lookup"><span data-stu-id="ccedc-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="ccedc-374">取消阻止調試所需的埠後,您將看到遠端調試監視器,如下所示。</span><span class="sxs-lookup"><span data-stu-id="ccedc-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="ccedc-375">通過此介面,您可以輕鬆監視連接並更改調試許可權。</span><span class="sxs-lookup"><span data-stu-id="ccedc-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![遠端除錯監視器](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="ccedc-377">**圖 13**: 遠端除錯監視器</span><span class="sxs-lookup"><span data-stu-id="ccedc-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="ccedc-378">還可以遠端除錯透過 FTP 打開的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccedc-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="ccedc-379">步驟與之前介紹的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="ccedc-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="ccedc-380">但是,您需要指定用於瀏覽本模組前面概述的 FTP 專案的基本 URL。</span><span class="sxs-lookup"><span data-stu-id="ccedc-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="ccedc-381">實驗室 2</span><span class="sxs-lookup"><span data-stu-id="ccedc-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="ccedc-382">使用視覺化工作室 2005 進行遠端除錯</span><span class="sxs-lookup"><span data-stu-id="ccedc-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="ccedc-383">本實驗將引導您透過 Visual Studio 2005 進行遠端調試。</span><span class="sxs-lookup"><span data-stu-id="ccedc-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="ccedc-384">按一下此處查看本實驗的視頻演練。</span><span class="sxs-lookup"><span data-stu-id="ccedc-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="ccedc-385">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="ccedc-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="ccedc-386">本實驗要求您擁有兩台電腦,一台運行 Visual Studio 2005,另一台運行 IIS 5 或更高。</span><span class="sxs-lookup"><span data-stu-id="ccedc-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="ccedc-387">打開 Visual Studio 2005 並在遠端伺服器上創建新的網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-388">您可以在遠端 IIS 實體上或透過 FTP 創建網站。</span><span class="sxs-lookup"><span data-stu-id="ccedc-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="ccedc-389">從遠端 Web 伺服器,使用 UNC 路徑在開發電腦上找到 msvsmon.exe 並將其執行。</span><span class="sxs-lookup"><span data-stu-id="ccedc-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="ccedc-390">msvsmon.exe 的預設位置是 //伺服器/c$/程式檔/微軟視覺工作室 8/Common7/IDE/遠端調試器/x86。</span><span class="sxs-lookup"><span data-stu-id="ccedc-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="ccedc-391">如果提示取消阻止埠進行遠端調試,則執行此操作。</span><span class="sxs-lookup"><span data-stu-id="ccedc-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="ccedc-392">從開發電腦打開 Default.aspx 的代碼後面,並在 page/_Load 方法中設置斷點。</span><span class="sxs-lookup"><span data-stu-id="ccedc-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="ccedc-393">從開發電腦開始調試。</span><span class="sxs-lookup"><span data-stu-id="ccedc-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="ccedc-394">您應該按預期命中斷點。</span><span class="sxs-lookup"><span data-stu-id="ccedc-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="ccedc-395">ASP.NET 程式開發伺服器</span><span class="sxs-lookup"><span data-stu-id="ccedc-395">ASP.NET Development Server</span></span>

<span data-ttu-id="ccedc-396">正如我們已經討論過的,Visual Studio 2005 附帶了一個名為ASP.NET開發伺服器的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="ccedc-397">(ASP.NET開發伺服器有時稱為卡西尼。此 Web 伺服器是瀏覽和除錯檔案系統執行的 Web 應用程式的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="ccedc-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="ccedc-398">ASP.NET開發伺服器是受限的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="ccedc-399">它不允許遠端連接,它不允許來自除啟動 Web 伺服器的使用者以外的任何使用者的任何請求。</span><span class="sxs-lookup"><span data-stu-id="ccedc-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="ccedc-400">它還不能為 ASP 頁提供服務。</span><span class="sxs-lookup"><span data-stu-id="ccedc-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="ccedc-401">僅提供ASP.NET資源和 HTML 資源(包括圖像、CSS 檔等)。</span><span class="sxs-lookup"><span data-stu-id="ccedc-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="ccedc-402">ASP.NET開發伺服器可以通過命令行啟動,通過運行位於 c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*的 WebDev.WebServer.exe 檔。</span><span class="sxs-lookup"><span data-stu-id="ccedc-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="ccedc-403">以下對話框顯示可用的參數。</span><span class="sxs-lookup"><span data-stu-id="ccedc-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="ccedc-404">**圖 14**</span><span class="sxs-lookup"><span data-stu-id="ccedc-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="ccedc-405">通過命令行顯式啟動時,不支援ASP.NET開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="ccedc-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
