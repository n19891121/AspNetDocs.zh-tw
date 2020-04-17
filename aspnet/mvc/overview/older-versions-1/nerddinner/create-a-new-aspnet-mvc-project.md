---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 建立新ASP.NET MVC 專案 |微軟文件
author: rick-anderson
description: 步驟 1 演示如何將基本的 NerdDinner 應用程式結構放在原位。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541477"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="3c316-103">建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="3c316-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="3c316-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3c316-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3c316-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="3c316-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="3c316-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第 1 步,該教學示範如何使用 ASP.NET MVC 1 構建小型但完整的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c316-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="3c316-107">步驟 1 演示如何將基本的 NerdDinner 應用程式結構放在原位。</span><span class="sxs-lookup"><span data-stu-id="3c316-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="3c316-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="3c316-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="3c316-109">神經晚餐步驟 1:&gt;檔案 - 新項目</span><span class="sxs-lookup"><span data-stu-id="3c316-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="3c316-110">我們將透過在 Visual Studio 2008 或免費的可視化 Web 開發人員 2008 Express 中選擇 **「檔-&gt;新專案**」功能表項來開始我們的NerdDinner應用程式。</span><span class="sxs-lookup"><span data-stu-id="3c316-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="3c316-111">這將彈出"新專案"對話框。</span><span class="sxs-lookup"><span data-stu-id="3c316-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="3c316-112">要建立新ASP.NET MVC 應用程式,我們將選擇對話框左側的「Web」節點,然後在右側選擇「ASP.NET MVC Web 應用程式」專案範本:</span><span class="sxs-lookup"><span data-stu-id="3c316-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="3c316-113">*重要提示:請確保已下載並安裝 ASP.NET MVC - 否則它不會顯示在「新項目」對話框中。如果您尚未安裝[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)的 V2(ASP.NET MVC 在"Web 平臺-&gt;框架和運行時"部分中可用)。*</span><span class="sxs-lookup"><span data-stu-id="3c316-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="3c316-114">我們將命名要創建「NerdDinner」的新項目,然後單擊「確定」按鈕創建它。</span><span class="sxs-lookup"><span data-stu-id="3c316-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="3c316-115">當我們按下「OK」Visual Studio 時,將彈出一個附加對話框,提示我們為新應用程式選擇創建單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="3c316-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="3c316-116">此單元測試專案使我們能夠創建自動測試,以驗證應用程式的功能和行為(本教程稍後將介紹如何操作)。</span><span class="sxs-lookup"><span data-stu-id="3c316-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="3c316-117">上面對話方塊中的「測試框架」下拉清單填充了所有可用的ASP.NET MVC 單元測試專案範本安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="3c316-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="3c316-118">可以為 NUnit、MBUnit 和 XUnit 下載版本。</span><span class="sxs-lookup"><span data-stu-id="3c316-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="3c316-119">還支援內置的可視化工作室單元測試框架。</span><span class="sxs-lookup"><span data-stu-id="3c316-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="3c316-120">*注意:可視化工作室單元測試框架僅適用於 Visual Studio 2008 專業版和更高版本。如果您使用的是 VS 2008 標準版或可視化 Web 開發人員 2008 Express,則需要下載並安裝 nUnit、MBUnit 或 XUnit 擴展,以便 ASP.NET MVC 才能顯示此對話方塊。如果沒有安裝任何測試框架,將不會顯示該對話方塊。*</span><span class="sxs-lookup"><span data-stu-id="3c316-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="3c316-121">我們將為我們創建的測試專案使用預設的「NerdDinner.Test」名稱,並使用「視覺化工作室單元測試」框架選項。</span><span class="sxs-lookup"><span data-stu-id="3c316-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="3c316-122">當我們點擊「ok」按鈕 Visual Studio 將為我們建立一個解決方案,其中包含兩個專案 - 一個用於我們的 Web 應用程式,一個用於我們的單元測試:</span><span class="sxs-lookup"><span data-stu-id="3c316-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="3c316-123">檢查 NerdDinner 目錄結構</span><span class="sxs-lookup"><span data-stu-id="3c316-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="3c316-124">當您使用 Visual Studio 建立新 ASP.NET MVC 應用程式時,它會自動向專案新增許多檔案和目錄:</span><span class="sxs-lookup"><span data-stu-id="3c316-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="3c316-125">預設的項目上ASP.NET MVC 專案有六個頂級目錄:</span><span class="sxs-lookup"><span data-stu-id="3c316-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="3c316-126">**目錄**</span><span class="sxs-lookup"><span data-stu-id="3c316-126">**Directory**</span></span> | <span data-ttu-id="3c316-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="3c316-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="3c316-128">**/控制器**</span><span class="sxs-lookup"><span data-stu-id="3c316-128">**/Controllers**</span></span> | <span data-ttu-id="3c316-129">放置處理網址 要求的控制器類別的位置</span><span class="sxs-lookup"><span data-stu-id="3c316-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="3c316-130">**/型號**</span><span class="sxs-lookup"><span data-stu-id="3c316-130">**/Models**</span></span> | <span data-ttu-id="3c316-131">放置並操作資料的類別的位置</span><span class="sxs-lookup"><span data-stu-id="3c316-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="3c316-132">**/檢視**</span><span class="sxs-lookup"><span data-stu-id="3c316-132">**/Views**</span></span> | <span data-ttu-id="3c316-133">設定設定輸出的 UI 樣本檔案的位置</span><span class="sxs-lookup"><span data-stu-id="3c316-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="3c316-134">**/文稿**</span><span class="sxs-lookup"><span data-stu-id="3c316-134">**/Scripts**</span></span> | <span data-ttu-id="3c316-135">放置 JavaScript 函式庫檔案與文稿的位置 (.js)</span><span class="sxs-lookup"><span data-stu-id="3c316-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="3c316-136">**/內容**</span><span class="sxs-lookup"><span data-stu-id="3c316-136">**/Content**</span></span> | <span data-ttu-id="3c316-137">放置 CSS 與影像檔以及其他非動態/非 JavaScript 內容的位置</span><span class="sxs-lookup"><span data-stu-id="3c316-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="3c316-138">**/應用程式\_資料**</span><span class="sxs-lookup"><span data-stu-id="3c316-138">**/App\_Data**</span></span> | <span data-ttu-id="3c316-139">儲存要讀取/寫入的資料檔的位置。</span><span class="sxs-lookup"><span data-stu-id="3c316-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="3c316-140">ASP.NET MVC 不需要此結構。</span><span class="sxs-lookup"><span data-stu-id="3c316-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="3c316-141">事實上,處理大型應用程式的開發人員通常會跨多個專案對應用程式進行分區,使其更易於管理(例如:資料模型類通常位於與 Web 應用程式不同的類庫專案中)。</span><span class="sxs-lookup"><span data-stu-id="3c316-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="3c316-142">但是,默認專案結構確實提供了一個不錯的默認目錄約定,我們可以用它來保持應用程序問題清潔。</span><span class="sxs-lookup"><span data-stu-id="3c316-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="3c316-143">當我們展開 /控制器目錄時,我們會發現 Visual Studio 預設為專案添加了兩個控制器類 - 主控制器和帳戶控制器:</span><span class="sxs-lookup"><span data-stu-id="3c316-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="3c316-144">當我們展開 /Views 目錄時,我們會發現三個子目錄 - /Home,//帳戶和 /共用 - 以及其中的幾個範本檔也添加到專案中,默認情況下:</span><span class="sxs-lookup"><span data-stu-id="3c316-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="3c316-145">當我們展開 /內容和 /script 檔:</span><span class="sxs-lookup"><span data-stu-id="3c316-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="3c316-146">當我們擴展NerdDinner.測試專案時,我們將找到兩個類,其中包含控制器類的單元測試:</span><span class="sxs-lookup"><span data-stu-id="3c316-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="3c316-147">Visual Studio 添加的這些預設檔為我們提供了工作應用程式的基本結構 - 完整的主頁,關於頁面,帳戶登錄/註銷/註冊頁,和未處理的錯誤頁面(所有有線和開箱即用)。</span><span class="sxs-lookup"><span data-stu-id="3c316-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="3c316-148">執行內德晚餐應用程式</span><span class="sxs-lookup"><span data-stu-id="3c316-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="3c316-149">我們可以通過選擇**除錯&gt;- 啟動除錯**或**除錯 -&gt;不除錯選單項目**執行專案:</span><span class="sxs-lookup"><span data-stu-id="3c316-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="3c316-150">這會啟動 Visual Studio 附帶的內建ASP.NET Web 伺服器,並執行我們的應用程式:</span><span class="sxs-lookup"><span data-stu-id="3c316-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="3c316-151">以下是我們新專案的主頁(URL:"/")運行時:</span><span class="sxs-lookup"><span data-stu-id="3c316-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="3c316-152">按下「關於」選項卡將顯示一個有關頁面(URL:"/主頁/關於"):</span><span class="sxs-lookup"><span data-stu-id="3c316-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="3c316-153">按下右上角的「登錄」連結將我們帶到登錄頁面(URL:"/帳戶/登錄")</span><span class="sxs-lookup"><span data-stu-id="3c316-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="3c316-154">如果我們沒有登錄帳戶,我們可以單擊註冊連結(URL:"/帳戶/註冊")創建一個:</span><span class="sxs-lookup"><span data-stu-id="3c316-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="3c316-155">在創建新專案時,默認情況下添加了實現上述主頁、關於和註銷/寄存器功能的代碼。</span><span class="sxs-lookup"><span data-stu-id="3c316-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="3c316-156">我們將使用它作為應用程式的起點。</span><span class="sxs-lookup"><span data-stu-id="3c316-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="3c316-157">測試內德晚餐應用程式</span><span class="sxs-lookup"><span data-stu-id="3c316-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="3c316-158">如果我們使用 Visual Studio 2008 的專業版或更高版本,我們可以在 Visual Studio 中使用內置單元測試 IDE 支援來測試專案:</span><span class="sxs-lookup"><span data-stu-id="3c316-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="3c316-159">選擇上述選項之一將在 IDE 中開啟「測試結果」窗格,並在新專案中包含的 27 個單元測試中提供通過/失敗狀態,這些測試涵蓋內置功能:</span><span class="sxs-lookup"><span data-stu-id="3c316-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="3c316-160">在本教程的後面部分,我們將介紹有關自動測試的更多資訊,並添加其他單元測試,這些測試涵蓋了我們實現的應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="3c316-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="3c316-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c316-161">Next Step</span></span>

<span data-ttu-id="3c316-162">現在,我們已經有了一個基本的應用程序結構。</span><span class="sxs-lookup"><span data-stu-id="3c316-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="3c316-163">現在,讓我們[建立資料庫來儲存我們的應用程式資料](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3c316-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c316-164">[前一個](introducing-the-nerddinner-tutorial.md)
> [下一個](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="3c316-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
