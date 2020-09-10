---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: 在 ASP.NET MVC 中使用 Page Inspector |Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的網頁程式開發工具。 選取整合式瀏覽器中的任何元素，然後 Page Inspector 我 .。。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 42d5683ce75467a159c9d13edf302bd6bf24a11d
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643694"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="58a6b-104">在 ASP.NET MVC 中使用 Page Inspector</span><span class="sxs-lookup"><span data-stu-id="58a6b-104">Using Page Inspector in ASP.NET MVC</span></span>

<span data-ttu-id="58a6b-105">由 Tim Ammann</span><span class="sxs-lookup"><span data-stu-id="58a6b-105">by Tim Ammann</span></span>

> <span data-ttu-id="58a6b-106">Visual Studio 2012 中的 Page Inspector 是具有整合式瀏覽器的網頁程式開發工具。</span><span class="sxs-lookup"><span data-stu-id="58a6b-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="58a6b-107">在整合式瀏覽器中選取任何專案，Page Inspector 立即反白顯示元素的來源和 CSS。</span><span class="sxs-lookup"><span data-stu-id="58a6b-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="58a6b-108">您可以流覽任何 MVC 視圖、快速找出轉譯標記的來源，以及直接在 Visual Studio 環境中使用瀏覽器工具。</span><span class="sxs-lookup"><span data-stu-id="58a6b-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="58a6b-109">觀賞影片</span><span class="sxs-lookup"><span data-stu-id="58a6b-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="58a6b-110">本教學課程會示範如何啟用檢查模式，然後在 Web 專案中快速找出並編輯標記和 CSS。</span><span class="sxs-lookup"><span data-stu-id="58a6b-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="58a6b-111">本教學課程使用 MVC 專案，但是您也可以使用 Page Inspector 來 [Web Form](https://go.microsoft.com/?linkid=9802001) 和其他 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="58a6b-112">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="58a6b-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="58a6b-113">先決條件</span><span class="sxs-lookup"><span data-stu-id="58a6b-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="58a6b-114">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="58a6b-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="58a6b-115">使用 Page Inspector 流覽至視圖</span><span class="sxs-lookup"><span data-stu-id="58a6b-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="58a6b-116">啟用檢查模式</span><span class="sxs-lookup"><span data-stu-id="58a6b-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="58a6b-117">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="58a6b-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="58a6b-118">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="58a6b-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - <span data-ttu-id="58a6b-119">[在 [樣式] 視窗中預覽 CSS 變更](#_7_previewing_css)</span><span class="sxs-lookup"><span data-stu-id="58a6b-119">[Preview CSS Changes in the Styles window](#_7_previewing_css)</span></span>
> - [<span data-ttu-id="58a6b-120">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="58a6b-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="58a6b-121">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="58a6b-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="58a6b-122">將動態頁面元素對應至 JavaScript</span><span class="sxs-lookup"><span data-stu-id="58a6b-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="58a6b-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="58a6b-123">Prerequisites</span></span>

- <span data-ttu-id="58a6b-124">[適用于 Web 的](https://www.microsoft.com/visualstudio/11/downloads#express-web) [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)或 Visual Studio Express 2012。</span><span class="sxs-lookup"><span data-stu-id="58a6b-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="58a6b-125">若要取得 Page Inspector 的最新版本，請使用 [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) 來安裝 WINDOWS Azure SDK for .net 2.0。</span><span class="sxs-lookup"><span data-stu-id="58a6b-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>

<span data-ttu-id="58a6b-126">Page Inspector 與 Microsoft Web Developer Tools 配套。</span><span class="sxs-lookup"><span data-stu-id="58a6b-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="58a6b-127">最新版本是1.3。</span><span class="sxs-lookup"><span data-stu-id="58a6b-127">The latest version is 1.3.</span></span> <span data-ttu-id="58a6b-128">若要檢查您擁有的版本，請執行 Visual Studio，然後**從 [說明**] 功能表選取 [關於] **Microsoft Visual Studio** 。</span><span class="sxs-lookup"><span data-stu-id="58a6b-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="58a6b-129">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="58a6b-129">Create a Web Application</span></span>

<span data-ttu-id="58a6b-130">首先，建立您將與 Page Inspector 搭配使用的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="58a6b-131">在 Visual Studio 中，選擇 [檔案]**[新增專案]** &gt; \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="58a6b-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="58a6b-132">展開左側的 [ **Visual c #**]，選取 [ **web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![新的 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="58a6b-134">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="58a6b-134">Click **OK**.</span></span>

<span data-ttu-id="58a6b-135">在 [ **新增 ASP.NET MVC 4 專案** ] 對話方塊中，選取 [ **網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="58a6b-136">將 **Razor** 保留為預設的 view engine。</span><span class="sxs-lookup"><span data-stu-id="58a6b-136">Leave **Razor** as the default view engine.</span></span>

![新的 ASP.NET MVC 專案-網際網路應用程式](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="58a6b-138">應用程式會在 **原始** 檔視圖中開啟。</span><span class="sxs-lookup"><span data-stu-id="58a6b-138">The application opens in **Source** view.</span></span>

![來源視圖中的新 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="58a6b-140">現在您已經有要使用的應用程式，您可以使用 Page Inspector 來檢查和修改它。</span><span class="sxs-lookup"><span data-stu-id="58a6b-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="58a6b-141">使用 Page Inspector 流覽至視圖</span><span class="sxs-lookup"><span data-stu-id="58a6b-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="58a6b-142">在 Visual Studio 2012 中，您可以用滑鼠右鍵按一下專案中的任何視圖、選取 [ **在 Page Inspector 中查看**]，Page Inspector 會找出路線並顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="58a6b-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="58a6b-143">在 **方案總管**中，依序展開 [ **Views** ] 資料夾和 [ **主** 資料夾] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="58a6b-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="58a6b-144">以滑鼠右鍵按一下 [Index]，然後選擇 [ **View in Page Inspector**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![Page Inspector 中的 View Index. cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="58a6b-146">根據預設，Page Inspector 會停駐在 Visual Studio 環境左邊的視窗。</span><span class="sxs-lookup"><span data-stu-id="58a6b-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="58a6b-147">如果您想要的話，可以將它停駐在其他位置，或取消停駐視窗。</span><span class="sxs-lookup"><span data-stu-id="58a6b-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="58a6b-148">請參閱 [如何：排列和停駐視窗](https://msdn.microsoft.com/library/z4y0hsax.aspx)。</span><span class="sxs-lookup"><span data-stu-id="58a6b-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="58a6b-149">Page Inspector 視窗的上方窗格會在瀏覽器視窗中顯示目前的頁面。</span><span class="sxs-lookup"><span data-stu-id="58a6b-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="58a6b-150">下方窗格會顯示 HTML 標籤中的頁面，以及可讓您檢查頁面不同層面的一些索引標籤。</span><span class="sxs-lookup"><span data-stu-id="58a6b-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="58a6b-151">下方窗格與 Internet Explorer 中的 [F12 開發人員工具](https://msdn.microsoft.com/ie/aa740478) 類似。</span><span class="sxs-lookup"><span data-stu-id="58a6b-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![Page Inspector 中的 ASP.NET MVC 應用程式](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="58a6b-153">在本教學課程中，您將使用 [ **HTML** ] 和 [ **樣式** ] 索引標籤，快速流覽並對應用程式進行變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="58a6b-154">EnableInspection 模式</span><span class="sxs-lookup"><span data-stu-id="58a6b-154">EnableInspection Mode</span></span>

<span data-ttu-id="58a6b-155">若要將 Page Inspector 放入檢查模式，請按一下 [ **檢查** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="58a6b-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="58a6b-156">在檢查模式中，當您將滑鼠指標放在轉譯頁面的任何部分時，就會反白顯示對應的來源標記或程式碼。</span><span class="sxs-lookup"><span data-stu-id="58a6b-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![切換檢查模式](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="58a6b-158">現在將滑鼠移到 Page Inspector 內頁面的不同部分。</span><span class="sxs-lookup"><span data-stu-id="58a6b-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="58a6b-159">當您這樣做時，滑鼠指標會變成大型加號，而下的元素則會反白顯示：</span><span class="sxs-lookup"><span data-stu-id="58a6b-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![將滑鼠停留在 div 上方。內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="58a6b-161">當您移動滑鼠指標時，Visual Studio 會反白顯示來源檔案中對應的 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="58a6b-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="58a6b-162">如果 HTML 元素來自另一個原始檔，Visual Studio 會自動開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="58a6b-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="58a6b-163">在 Page Inspector 中，[ **html** ] 索引標籤會顯示從 Razor 語法產生的 html。</span><span class="sxs-lookup"><span data-stu-id="58a6b-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="58a6b-164">當您移動滑鼠指標時，HTML 元素會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="58a6b-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="58a6b-165">[ **樣式** ] 索引標籤會顯示元素的 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="58a6b-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="58a6b-166">使用 Page Inspector 對標記進行變更</span><span class="sxs-lookup"><span data-stu-id="58a6b-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="58a6b-167">Page Inspector 可讓您尋找位置可能不明顯的標記。</span><span class="sxs-lookup"><span data-stu-id="58a6b-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="58a6b-168">然後，您可以修改標記並查看所產生的變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="58a6b-169">若要查看此情況，請按一下 [ **檢查** ]，然後在 [Page Inspector] 視窗中，將它滾動到頁面底部。</span><span class="sxs-lookup"><span data-stu-id="58a6b-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="58a6b-170">當您將滑鼠指標移至頁尾區域時，Page Inspector 會開啟設定檔案，並反白 \_ 顯示您所選取之版面配置頁面的區段。</span><span class="sxs-lookup"><span data-stu-id="58a6b-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="58a6b-171">如您所見，頁尾區域是在版面配置檔案中定義，而不是在 view 本身。</span><span class="sxs-lookup"><span data-stu-id="58a6b-171">As you can see, the footer area is defined in the layout file, and not the view itself.</span></span>

![頁尾](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="58a6b-173">現在請將滑鼠指標移至具有著作權標示的行上 <a id="a"></a> 。</span><span class="sxs-lookup"><span data-stu-id="58a6b-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="58a6b-174">在 [ \_ 版面配置] 頁面中，會反白顯示對應的行。</span><span class="sxs-lookup"><span data-stu-id="58a6b-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![已反白顯示頁尾著作權線](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="58a6b-176">在配置 cshtml 檔案中的行尾加入一些文字 \_ 。</span><span class="sxs-lookup"><span data-stu-id="58a6b-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="58a6b-177">&lt;p &gt; &amp; copy; @DateTime.Now.Year -My ASP.NET MVC Application Rocks！ &lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="58a6b-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="58a6b-178">現在，按 Ctrl + Alt + Enter 或按一下更新列，以在 Page Inspector 瀏覽器視窗中查看結果。</span><span class="sxs-lookup"><span data-stu-id="58a6b-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![我的 ASP.NET 應用程式 Rocks！](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="58a6b-180">您可能認為頁尾定義在 Index. cshtml 中，但是它是在 Layout 中， \_ 並 Page Inspector 為您找到。</span><span class="sxs-lookup"><span data-stu-id="58a6b-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="58a6b-181">檢查模式和 HTML 視窗</span><span class="sxs-lookup"><span data-stu-id="58a6b-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="58a6b-182">接下來，您將快速查看 HTML 視窗，以及它如何為您對應元素。</span><span class="sxs-lookup"><span data-stu-id="58a6b-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="58a6b-183">按一下 [ **檢查** ]，將 Page Inspector 放入檢查模式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="58a6b-184">按一下頁面的上半部，指出「您的標誌在這裡」。</span><span class="sxs-lookup"><span data-stu-id="58a6b-184">Click the top part of the page that says "Your logo here".</span></span> <span data-ttu-id="58a6b-185">您將更詳細地檢查特定元素，因此當您移動滑鼠指標時，瀏覽器視窗中的顯示將不再變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="58a6b-186">現在將滑鼠指標移至 **HTML** 視窗。</span><span class="sxs-lookup"><span data-stu-id="58a6b-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="58a6b-187">當您移動滑鼠指標時，Page Inspector 會列出 **HTML** 視窗內的元素，並在瀏覽器視窗中反白顯示對應的元素。</span><span class="sxs-lookup"><span data-stu-id="58a6b-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 視窗](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="58a6b-189">如同之前一樣，Page Inspector 會在暫存索引標籤中為您開啟配置檔。請 \_ 按一下 [配置 \_ ] 暫時索引標籤，然後在 [ &lt; 標頭] 區段中為您反白顯示對應的標記 &gt; ：</span><span class="sxs-lookup"><span data-stu-id="58a6b-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![反白顯示標記](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="58a6b-191">在 [樣式] 視窗中預覽 CSS 變更</span><span class="sxs-lookup"><span data-stu-id="58a6b-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="58a6b-192">接下來，您將使用 [Page Inspector **樣式** ] 視窗來預覽 CSS 的變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="58a6b-193">按一下 [ **檢查** ]，將 Page Inspector 放入檢查模式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="58a6b-194">在 Page Inspector 瀏覽器視窗中，將滑鼠指標移到 [首頁] 區段上方，直到出現 [ **div. 內容包裝函式** ] 標籤。</span><span class="sxs-lookup"><span data-stu-id="58a6b-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![將滑鼠停留在 div 上方。內容包裝函式](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="58a6b-196">在 [內容包裝函式] 區段內按一下，然後將滑鼠指標移至 [ **樣式** ] 視窗。</span><span class="sxs-lookup"><span data-stu-id="58a6b-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="58a6b-197">[ **樣式** ] 視窗會顯示此元素的所有 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="58a6b-197">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="58a6b-198">向下滾動以尋找「內容包裝函式」類別選取器。</span><span class="sxs-lookup"><span data-stu-id="58a6b-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="58a6b-199">現在清除背景色彩屬性的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="58a6b-199">Now clear the checkbox for the background-color property.</span></span>

![清除背景色彩](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="58a6b-201">請注意變更在 Page Inspector 瀏覽器視窗中的立即預覽。</span><span class="sxs-lookup"><span data-stu-id="58a6b-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="58a6b-202">再次選取該核取方塊，然後按兩下屬性值並將它變更為紅色。</span><span class="sxs-lookup"><span data-stu-id="58a6b-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="58a6b-203">變更會立即顯示：</span><span class="sxs-lookup"><span data-stu-id="58a6b-203">The change shows immediately:</span></span>

![紅色背景色彩](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="58a6b-205">在您認可樣式表單本身的變更之前，[ **樣式** ] 視窗可讓您輕鬆地測試和預覽 CSS 變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="58a6b-206">CSS 自動同步處理</span><span class="sxs-lookup"><span data-stu-id="58a6b-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="58a6b-207">這項功能需要1.3 版的 Page Inspector。</span><span class="sxs-lookup"><span data-stu-id="58a6b-207">This feature requires version 1.3 of Page Inspector.</span></span>

<span data-ttu-id="58a6b-208">CSS 自動同步處理功能可讓您直接編輯 CSS 檔案，並立即在 Page Inspector 瀏覽器中查看變更。</span><span class="sxs-lookup"><span data-stu-id="58a6b-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="58a6b-209">按一下 [ **檢查** ]，將 Page Inspector 放入檢查模式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="58a6b-210">在 Page Inspector 瀏覽器中，將滑鼠指標移到 [首頁] 區段上方，直到出現 [ **div. 內容包裝函式** ] 標籤。</span><span class="sxs-lookup"><span data-stu-id="58a6b-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="58a6b-211">按一下 [一次]，選取此元素。</span><span class="sxs-lookup"><span data-stu-id="58a6b-211">Click once to select this element.</span></span>

<span data-ttu-id="58a6b-212">[ **樣式** ] 視窗會顯示此元素的所有 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="58a6b-212">The **Styles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="58a6b-213">向下滾動以尋找「內容包裝函式」類別選取器。</span><span class="sxs-lookup"><span data-stu-id="58a6b-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="58a6b-214">按一下 [內容包裝函式]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="58a6b-215">Page Inspector 會開啟定義此樣式 (.css) 的 CSS 檔案，並反白顯示對應的 CSS 樣式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="58a6b-216">現在將的值變更 `background-color` 為 "red"。</span><span class="sxs-lookup"><span data-stu-id="58a6b-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="58a6b-217">變更會立即出現在 Page Inspector 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="58a6b-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="58a6b-218">使用 CSS 色彩選擇器</span><span class="sxs-lookup"><span data-stu-id="58a6b-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="58a6b-219">Visual Studio 2012 中的 CSS 編輯器具有色彩選擇器，可讓您輕鬆地選擇和插入色彩。</span><span class="sxs-lookup"><span data-stu-id="58a6b-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="58a6b-220">色彩選擇器包含色彩的標準調色板、支援標準色彩名稱、雜湊碼、RGB、RGBA、HSL 和 HSLA 色彩，以及維護您最近在檔中使用的色彩清單。</span><span class="sxs-lookup"><span data-stu-id="58a6b-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="58a6b-221">在上一節中，您已變更屬性的值 `background-color` 。</span><span class="sxs-lookup"><span data-stu-id="58a6b-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="58a6b-222">若要叫用色彩選擇器，請將插入點放在屬性名稱和類型 **#** 或 **rgb (** 之後。</span><span class="sxs-lookup"><span data-stu-id="58a6b-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 色彩選擇器列](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="58a6b-224">按一下以選取色彩，或按向下鍵，然後使用向左鍵和向右鍵來跨越色彩。</span><span class="sxs-lookup"><span data-stu-id="58a6b-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="58a6b-225">當您流覽色彩時，會預覽對應的十六進位值：</span><span class="sxs-lookup"><span data-stu-id="58a6b-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![預覽的背景色彩屬性值](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="58a6b-227">如果色軸沒有您想要的確切色彩，您可以使用色彩選擇器快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="58a6b-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="58a6b-228">若要開啟它，請按一下色軸右端的雙箭號，或在鍵盤上按下箭號或兩次。</span><span class="sxs-lookup"><span data-stu-id="58a6b-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 色彩選擇器快顯視窗](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="58a6b-230">按一下右側分隔號中的色彩。</span><span class="sxs-lookup"><span data-stu-id="58a6b-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="58a6b-231">這會顯示主視窗中該色彩的漸層。</span><span class="sxs-lookup"><span data-stu-id="58a6b-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="58a6b-232">按下 Enter，直接從分隔號中選擇色彩，或按一下主視窗中的任何點以選擇較高的精確度。</span><span class="sxs-lookup"><span data-stu-id="58a6b-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="58a6b-233">如果您想要使用的電腦螢幕上有一種色彩 (它不一定要在 Visual Studio 使用者介面) 內，您可以使用右下方的滴管工具來捕捉其值。</span><span class="sxs-lookup"><span data-stu-id="58a6b-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="58a6b-234">您也可以移動色彩選擇器底部的滑杆，來變更色彩的不透明度。</span><span class="sxs-lookup"><span data-stu-id="58a6b-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="58a6b-235">這樣做會將色彩值變更為 RGBA 值，因為 RGBA 格式可能代表不透明度。</span><span class="sxs-lookup"><span data-stu-id="58a6b-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="58a6b-236">選擇色彩之後，請按 Enter 鍵，然後輸入分號來完成 *.css* 檔案中的背景色彩專案。</span><span class="sxs-lookup"><span data-stu-id="58a6b-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="58a6b-237">Page Inspector 更新列</span><span class="sxs-lookup"><span data-stu-id="58a6b-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="58a6b-238">Page Inspector 立即偵測到 *網站 .css* 檔案的變更，並在更新列中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="58a6b-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![Update Bar](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="58a6b-240">若要儲存所有檔案並重新整理 Page Inspector 瀏覽器，請按 Ctrl + Alt + Enter 或按一下更新列。</span><span class="sxs-lookup"><span data-stu-id="58a6b-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="58a6b-241">醒目提示色彩的變更會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="58a6b-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="58a6b-242">將動態頁面元素對應至 JavaScript</span><span class="sxs-lookup"><span data-stu-id="58a6b-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="58a6b-243">在新式的 web 應用程式中，頁面中的元素通常會以 JavaScript 動態產生。</span><span class="sxs-lookup"><span data-stu-id="58a6b-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="58a6b-244">這表示沒有任何靜態標記 (對應至這些頁面元素的 HTML 或 Razor) 。</span><span class="sxs-lookup"><span data-stu-id="58a6b-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="58a6b-245">使用1.3 版時，Page Inspector 現在可以將動態新增至頁面的專案對應回對應的 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="58a6b-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="58a6b-246">為了示範這項功能，我們將使用 [單一頁面應用程式 (SPA) 範本](../../../single-page-application/overview/introduction/knockoutjs-template.md)。</span><span class="sxs-lookup"><span data-stu-id="58a6b-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="58a6b-247">SPA 範本需要 [ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 更新。</span><span class="sxs-lookup"><span data-stu-id="58a6b-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>

<span data-ttu-id="58a6b-248">在 Visual Studio 中，選擇 [檔案]**[新增專案]** &gt; \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="58a6b-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="58a6b-249">展開左側的 [ **Visual c #**]，選取 [ **web**]，然後選取 [ **ASP.NET MVC4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="58a6b-250">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="58a6b-250">Click **OK**.</span></span>

<span data-ttu-id="58a6b-251">在 [ **新增 ASP.NET MVC 4 專案** ] 對話方塊中，選取 [ **單一頁面應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="58a6b-252">在方案總管中，依序展開 [ **Views** ] 資料夾和 [ **主** 資料夾] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="58a6b-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="58a6b-253">以滑鼠右鍵按一下 [Index]，然後選擇 [ **View in Page Inspector**]。</span><span class="sxs-lookup"><span data-stu-id="58a6b-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="58a6b-254">Page Inspector 瀏覽器中顯示的第一件事是登入頁面。</span><span class="sxs-lookup"><span data-stu-id="58a6b-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="58a6b-255">按一下 [註冊]，並建立使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="58a6b-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="58a6b-256">一旦您註冊之後，應用程式就會將您登入，並使用一些範例專案來建立待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="58a6b-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="58a6b-257">按一下 [ **檢查** ]，將 Page Inspector 放入檢查模式。</span><span class="sxs-lookup"><span data-stu-id="58a6b-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="58a6b-258">在 Page Inspector 瀏覽器中，按一下其中一個待辦事項專案。</span><span class="sxs-lookup"><span data-stu-id="58a6b-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="58a6b-259">請注意，此元素不會以藍色反白顯示，而是以橙色醒目提示元素，並在專案名稱旁邊加上 "JS"。</span><span class="sxs-lookup"><span data-stu-id="58a6b-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="58a6b-260">這表示已透過腳本動態建立元素。</span><span class="sxs-lookup"><span data-stu-id="58a6b-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="58a6b-261">此外，[ **呼叫堆疊** ] 索引標籤上會出現橙色的底線。這表示 [ **呼叫堆疊** ] 窗格具有元素的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="58a6b-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="58a6b-262">按一下 [ **呼叫堆疊** ] 索引標籤。[ **呼叫堆疊** ] 窗格會顯示建立元素之 JavaScript 呼叫的呼叫堆疊。</span><span class="sxs-lookup"><span data-stu-id="58a6b-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="58a6b-263">對外部程式庫（例如 jQuery）的呼叫會折迭，如此您就可以輕鬆地查看應用程式腳本的呼叫。</span><span class="sxs-lookup"><span data-stu-id="58a6b-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="58a6b-264">若要查看完整堆疊（包括呼叫外部程式庫），您可以展開標示為「外部程式庫」的節點：</span><span class="sxs-lookup"><span data-stu-id="58a6b-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="58a6b-265">如果您按一下 [呼叫堆疊] 中的專案，Visual Studio 會開啟程式碼檔案，並反白顯示對應的腳本。</span><span class="sxs-lookup"><span data-stu-id="58a6b-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="58a6b-266">另請參閱</span><span class="sxs-lookup"><span data-stu-id="58a6b-266">See Also</span></span>

<span data-ttu-id="58a6b-267">[ASP.NET 具有 Visual Studio (ASP.net 網站) 的 MVC 4 簡介](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)</span><span class="sxs-lookup"><span data-stu-id="58a6b-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="58a6b-268">[Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 影片簡介) </span><span class="sxs-lookup"><span data-stu-id="58a6b-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="58a6b-269">Page Inspector (MSDN) 的[錯誤訊息](https://go.microsoft.com/?linkid=9813062)</span><span class="sxs-lookup"><span data-stu-id="58a6b-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
