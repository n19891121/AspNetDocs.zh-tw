---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用視覺化工作室程式設計ASP.NET網頁 (Razor) |微軟文件
author: Rick-Anderson
description: 本附錄說明如何使用 Visual Studio 2010 或可視化 Web 開發人員 2010 Express 使用 Razor 語法對 ASP.NET 網頁進行程式設計。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542894"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="74a9b-103">使用視覺化工作室ASP.NET網頁 (Razor) 程式設計</span><span class="sxs-lookup"><span data-stu-id="74a9b-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="74a9b-104"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="74a9b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="74a9b-105">本文介紹如何使用可視化工作室或可視化 Web 開發人員快速程式 ASP.NET 網頁 (Razor) 網站。</span><span class="sxs-lookup"><span data-stu-id="74a9b-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="74a9b-106">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="74a9b-106">What you'll learn</span></span>
>
> - <span data-ttu-id="74a9b-107">您需要安裝的內容(如果有的話)才能在 Visual Studio 版本中使用 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="74a9b-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="74a9b-108">如何向視覺化 Web 開發人員 2010 Express 添加對ASP.NET網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="74a9b-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="74a9b-109">如何使用 Visual Studio 中的功能使用 ASP.NET Razor 頁面,包括 IntelliSense 和調試器。</span><span class="sxs-lookup"><span data-stu-id="74a9b-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="74a9b-110">本教學中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="74a9b-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="74a9b-111">ASP.NET網頁 (剃鬚刀) 3</span><span class="sxs-lookup"><span data-stu-id="74a9b-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="74a9b-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="74a9b-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="74a9b-113">Web矩陣 3</span><span class="sxs-lookup"><span data-stu-id="74a9b-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="74a9b-114">本教學還適用於ASP.NET網頁 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。</span><span class="sxs-lookup"><span data-stu-id="74a9b-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="74a9b-115">您可以使用 WebMatrix 或許多其他程式碼編輯器使用 Razor 語法對 ASP.NET 網頁進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="74a9b-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="74a9b-116">您還可以使用 Microsoft Visual Studio,這是一個功能齊全的集成開發環境 (IDE),它提供了一組功能強大的工具來創建多種類型的應用程式(而不僅僅是網站)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="74a9b-117">要使用ASP.NET Razor 頁面,您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="74a9b-118">Visual Studio 為使用 ASP.NET Razor 網頁進行程式設計提供的兩個特別有用的功能是:</span><span class="sxs-lookup"><span data-stu-id="74a9b-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="74a9b-119">*內泰利感知*。</span><span class="sxs-lookup"><span data-stu-id="74a9b-119">*IntelliSense*.</span></span> <span data-ttu-id="74a9b-120">視覺工作室內置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更為全面。</span><span class="sxs-lookup"><span data-stu-id="74a9b-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="74a9b-121">*除錯器*。</span><span class="sxs-lookup"><span data-stu-id="74a9b-121">*Debugger*.</span></span> <span data-ttu-id="74a9b-122">除錯器允許您在程式執行時停止程式、檢查變數和逐行執行代碼,從而對代碼進行故障排除。</span><span class="sxs-lookup"><span data-stu-id="74a9b-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="74a9b-123">將視覺工作室與不同版本的ASP.NET網頁使用</span><span class="sxs-lookup"><span data-stu-id="74a9b-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="74a9b-124">要在 Visual Studio 2017 中開發ASP.NET Web 應用,請安裝**ASP.NET和 Web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="74a9b-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="74a9b-125">Visual Studio 2012 和 Visual Studio 2013 包括對ASP.NET網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="74a9b-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="74a9b-126">(安裝 Visual Studio 時,將安裝支援ASP.NET網頁所需的套件。</span><span class="sxs-lookup"><span data-stu-id="74a9b-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="74a9b-127">默認情況下,Visual Studio 2010 不包括對 ASP.NET 網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="74a9b-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="74a9b-128">要將 ASP.NET 網頁與 Visual Studio 2010 一起使用,您必須安裝 ASP.NET MVC 套件。</span><span class="sxs-lookup"><span data-stu-id="74a9b-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="74a9b-129">要取得 ASP.NET 網頁 2,請安裝ASP.NET MVC 4。</span><span class="sxs-lookup"><span data-stu-id="74a9b-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="74a9b-130">下表總結了不同版本的 Visual Studio 中對 ASP.NET 網頁的支援。</span><span class="sxs-lookup"><span data-stu-id="74a9b-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="74a9b-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="74a9b-131">Visual Studio 2010</span></span> | <span data-ttu-id="74a9b-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="74a9b-132">Visual Studio 2012</span></span> | <span data-ttu-id="74a9b-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="74a9b-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="74a9b-134">**ASP.NET Web Pages 2**</span><span class="sxs-lookup"><span data-stu-id="74a9b-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="74a9b-135">安裝ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="74a9b-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="74a9b-136">(包括)</span><span class="sxs-lookup"><span data-stu-id="74a9b-136">(Included)</span></span> | <span data-ttu-id="74a9b-137">(包括)</span><span class="sxs-lookup"><span data-stu-id="74a9b-137">(Included)</span></span> |
| <span data-ttu-id="74a9b-138">**ASP.NET Web Pages 3**</span><span class="sxs-lookup"><span data-stu-id="74a9b-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="74a9b-139">透過 NuGet 更新到ASP.NET網頁 3</span><span class="sxs-lookup"><span data-stu-id="74a9b-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="74a9b-140">(包括)</span><span class="sxs-lookup"><span data-stu-id="74a9b-140">(Included)</span></span> |

<span data-ttu-id="74a9b-141">要使用 Visual Studio 2010,請參閱[在 Visual Studio 2010 中安裝支援 ASP.NET 網頁](#vs2010support)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="74a9b-142">從 WebMatrix 啟動視覺化工作室</span><span class="sxs-lookup"><span data-stu-id="74a9b-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="74a9b-143">如果您在 WebMatrix 中啟動了一個專案,並希望切換到 Visual Studio,WebMatrix 提供了一個按鈕,用於在 Visual Studio 中輕鬆打開專案。</span><span class="sxs-lookup"><span data-stu-id="74a9b-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="74a9b-144">您必須在電腦上安裝 Visual Studio 才能啟用此按鈕。</span><span class="sxs-lookup"><span data-stu-id="74a9b-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="74a9b-145">下圖顯示了 WebMatrix 中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="74a9b-145">The following image shows the button in WebMatrix.</span></span>

![啟動視覺工作室](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="74a9b-147">單擊該按鈕時,專案在可視化工作室中打開。</span><span class="sxs-lookup"><span data-stu-id="74a9b-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="74a9b-148">您可以在 WebMatrix 和 Visual Studio 之間來回切換,沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="74a9b-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="74a9b-149">如果其他環境中的任何檔已更改,需要重新載入以獲取最新更改,您將收到通知。</span><span class="sxs-lookup"><span data-stu-id="74a9b-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="74a9b-150">在視覺工作室建立ASP.NET剃刀網站</span><span class="sxs-lookup"><span data-stu-id="74a9b-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="74a9b-151">要在視覺工作室中創建ASP.NET剃刀網站:</span><span class="sxs-lookup"><span data-stu-id="74a9b-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="74a9b-152">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="74a9b-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="74a9b-153">在 **「檔案**」選單中,按下 **「新建網站**」 。。</span><span class="sxs-lookup"><span data-stu-id="74a9b-153">In the **File** menu, click **New Web Site**.</span></span>

    ![建立新網站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="74a9b-155">在 **"新建網站'** 對話框中,選擇要使用的語言(可視 C# 或可視基本)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="74a9b-156">選擇**ASP.NET網站(Razor)** 範本。</span><span class="sxs-lookup"><span data-stu-id="74a9b-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![剃鬚刀網站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="74a9b-158">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="74a9b-158">Click **OK**.</span></span>

<span data-ttu-id="74a9b-159">新專案存在,並且填充了一些默認網頁,以説明您入門。</span><span class="sxs-lookup"><span data-stu-id="74a9b-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="74a9b-160">Using IntelliSense</span><span class="sxs-lookup"><span data-stu-id="74a9b-160">Using IntelliSense</span></span>

<span data-ttu-id="74a9b-161">現在,您已經創建了一個網站,您可以看到 IntelliSense 在視覺工作室中是如何工作的。</span><span class="sxs-lookup"><span data-stu-id="74a9b-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="74a9b-162">在您剛剛創建的網站中,打開*Default.cshtml*頁面。</span><span class="sxs-lookup"><span data-stu-id="74a9b-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="74a9b-163">在頁面`<h3>`中的標記之後,鍵`@ServerInfo.`入 (包括點)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="74a9b-164">請注意 IntelliSense 如何在下拉清單`ServerInfo`中顯示 説明程式的可用方法。</span><span class="sxs-lookup"><span data-stu-id="74a9b-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="74a9b-166">從`GetHtml`清單中選擇方法,然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="74a9b-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="74a9b-167">IntelliSense 會自動填充該方法。</span><span class="sxs-lookup"><span data-stu-id="74a9b-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="74a9b-168">(與 C# 中的任何方法一樣,`()`必須在 方法之後添加字元。方法的`GetHtml`已完成代碼類似於以下範例:</span><span class="sxs-lookup"><span data-stu-id="74a9b-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="74a9b-169">按 Ctrl+F5 以運行該頁。</span><span class="sxs-lookup"><span data-stu-id="74a9b-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="74a9b-170">這是頁面在瀏覽器中顯示時的外觀:</span><span class="sxs-lookup"><span data-stu-id="74a9b-170">This is what the page looks like when displayed in a browser:</span></span>

    ![瀏覽器中的預設頁面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="74a9b-172">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="74a9b-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="74a9b-173">使用除錯器</span><span class="sxs-lookup"><span data-stu-id="74a9b-173">Using the Debugger</span></span>

1. <span data-ttu-id="74a9b-174">在*Default.cshtml*頁面的頂部`Page.Title`,以 開頭的行後添加以下代碼行:</span><span class="sxs-lookup"><span data-stu-id="74a9b-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="74a9b-175">在片段左側編輯器的灰色邊距中,按一次新行的旁邊以新增*斷點*。</span><span class="sxs-lookup"><span data-stu-id="74a9b-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="74a9b-176">斷點是一個標記,它告訴調試器在此時停止運行程式,以便您可以看到發生了什麼。</span><span class="sxs-lookup"><span data-stu-id="74a9b-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![設定中斷點](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="74a9b-178">刪除對 方法`ServerInfo.GetHtml`的 調用,並將調用`@myTime`添加到 變數的位置。</span><span class="sxs-lookup"><span data-stu-id="74a9b-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="74a9b-179">此調用顯示新代碼行返回的當前時間值。</span><span class="sxs-lookup"><span data-stu-id="74a9b-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="74a9b-180">按 F5 以在調試器中運行頁面。</span><span class="sxs-lookup"><span data-stu-id="74a9b-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="74a9b-181">頁面在您設置的斷點上停止。</span><span class="sxs-lookup"><span data-stu-id="74a9b-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="74a9b-182">下圖顯示了具有斷點(黃色)的編輯器中頁面的外觀。</span><span class="sxs-lookup"><span data-stu-id="74a9b-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![除錯中斷點](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="74a9b-184">在「調試」工具列中,按下 **「進入」** 按鈕(或按 F11)以執行下一行代碼。</span><span class="sxs-lookup"><span data-stu-id="74a9b-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="74a9b-185">每次按下此按鈕時,都會將執行提前到下一行代碼。</span><span class="sxs-lookup"><span data-stu-id="74a9b-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![單步進入按鈕](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="74a9b-187">通過將滑鼠指標放在變數`myTime`上或透過檢查 **「局部變數**」和 **「調用堆疊**」視窗中顯示的值來檢查變數的值。</span><span class="sxs-lookup"><span data-stu-id="74a9b-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="74a9b-188">可視化工作室顯示變數的值。</span><span class="sxs-lookup"><span data-stu-id="74a9b-188">Visual Studio display the value of the variable.</span></span>

    ![顯示時間值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="74a9b-190">檢查完變數並單步執行代碼後,按 F5 繼續運行頁面,而無需在每行停止。</span><span class="sxs-lookup"><span data-stu-id="74a9b-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="74a9b-191">完成所有代碼後,瀏覽器將顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="74a9b-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="74a9b-192">要瞭解有關除錯器以及如何在 Visual Studio 中除錯程式碼的資訊,請參閱[演練:在視覺化 Web 開發人員中除錯網頁](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="74a9b-193">使用 Razor 在 ASP.NET MVC 專案中使用 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74a9b-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="74a9b-194">Razor 語法還廣泛用於ASP.NET MVC 專案中。</span><span class="sxs-lookup"><span data-stu-id="74a9b-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="74a9b-195">MVC 是構建動態網站的強大、基於模式的方法。</span><span class="sxs-lookup"><span data-stu-id="74a9b-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="74a9b-196">如果ASP.NET網頁網站變得難以維護,您可能需要考慮將其轉換為ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="74a9b-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="74a9b-197">有關建立 MVC 應用程式的範例,請參閱[使用 mVC 5 ASP.NET 入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="74a9b-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="74a9b-198">2010 年在可視化工作室安裝對 ASP.NET 網頁的支援</span><span class="sxs-lookup"><span data-stu-id="74a9b-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="74a9b-199">本節演示如何安裝 Visual Web 開發人員 Express 2010 和可視化工作室的ASP.NET網頁工具。</span><span class="sxs-lookup"><span data-stu-id="74a9b-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="74a9b-200">如果您尚未網路平台安裝程式,請從以下網址下載它:</span><span class="sxs-lookup"><span data-stu-id="74a9b-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="74a9b-201">運行 Web 平臺安裝程式。</span><span class="sxs-lookup"><span data-stu-id="74a9b-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="74a9b-202">按**下產品**「選項卡。</span><span class="sxs-lookup"><span data-stu-id="74a9b-202">Click the **Products** tab.</span></span>

    ![WebPI 產品選項卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="74a9b-204">搜索**ASP.NET MVC 4(ASP.NET**網頁 2),然後按下「**添加**」。。</span><span class="sxs-lookup"><span data-stu-id="74a9b-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="74a9b-205">這些產品包括用於構建ASP.NET Razor 網站的視覺工作室工具。</span><span class="sxs-lookup"><span data-stu-id="74a9b-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![WebPi 安裝選項](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="74a9b-207">單擊「**安裝**」以完成安裝。</span><span class="sxs-lookup"><span data-stu-id="74a9b-207">Click **Install** to complete the installation.</span></span>
