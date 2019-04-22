---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: 使用 HTML5 與 jQuery UI Datepicker 快顯行事曆搭配 ASP.NET MVC-第 1 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將教導您如何使用編輯器範本、 顯示範本與 jQuery UI datepicker 快顯行事曆，ASP.NET MV 中的基本概念...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: 31a01f250e4f5473e954f040e1a506dbaf61be76
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59393576"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a><span data-ttu-id="95200-103">ASP.NET MVC： 第 1 部分中使用 HTML5 與 jQuery UI Datepicker 快顯行事曆</span><span class="sxs-lookup"><span data-stu-id="95200-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 1</span></span>

<span data-ttu-id="95200-104">藉由[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="95200-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="95200-105">本教學課程將教導您如何使用編輯器範本、 顯示範本與 jQuery UI datepicker 快顯行事曆，ASP.NET MVC Web 應用程式中的基本概念。</span><span class="sxs-lookup"><span data-stu-id="95200-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>


<span data-ttu-id="95200-106">本教學課程將教導您如何使用編輯器範本、 顯示範本和 jQuery 的基本概念[UI datepicker 快顯行事曆](http://plugins.jquery.com/project/datepicker)ASP.NET MVC Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="95200-106">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery [UI datepicker popup calendar](http://plugins.jquery.com/project/datepicker) in an ASP.NET MVC Web application.</span></span> <span data-ttu-id="95200-107">本教學課程中，您可以使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;)，這是免費版本的 Microsoft Visual Studio，或如果您已具備，您可以使用 Visual Studio 2010 SP1。</span><span class="sxs-lookup"><span data-stu-id="95200-107">For this tutorial, you can use Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;), which is a free version of Microsoft Visual Studio, or you can use Visual Studio 2010 SP1 if you already have that.</span></span>

<span data-ttu-id="95200-108">在開始之前，請確定您已安裝符合下列先決條件。</span><span class="sxs-lookup"><span data-stu-id="95200-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="95200-109">您可以安裝所有人都按下列連結：[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="95200-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="95200-110">或者，您可以個別安裝所需的軟體，使用下列連結：</span><span class="sxs-lookup"><span data-stu-id="95200-110">Alternatively, you can individually install the required software using the following links:</span></span>

- [<span data-ttu-id="95200-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="95200-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="95200-112">ASP.NET MVC 3 Tools Update</span><span class="sxs-lookup"><span data-stu-id="95200-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="95200-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行階段 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="95200-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="95200-114">如果您使用 Visual Studio 2010 而不 Visual Web Developer 中，請按一下下列連結安裝必要條件：[Visual Studio 2010 的必要元件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="95200-114">If you're using Visual Studio 2010 instead of Visual Web Developer, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="95200-115">本教學課程假設您已完成[Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程中，或您已熟悉 ASP.NET MVC 開發。</span><span class="sxs-lookup"><span data-stu-id="95200-115">This tutorial assumes you have completed the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial or that you're familiar with ASP.NET MVC development.</span></span> <span data-ttu-id="95200-116">本教學課程開頭中完成的專案[Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="95200-116">This tutorial starts with the completed project from the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span>

<span data-ttu-id="95200-117">本教學課程會示範在 C# 程式碼。</span><span class="sxs-lookup"><span data-stu-id="95200-117">This tutorial shows code in C#.</span></span> <span data-ttu-id="95200-118">不過，[入門專案](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)和已完成的專案也會提供在 Visual Basic 中。</span><span class="sxs-lookup"><span data-stu-id="95200-118">However, the [starter project](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) and completed project are also available in Visual Basic.</span></span>

<span data-ttu-id="95200-119">Visual Studio 專案使用C#和 Visual Basic 原始程式碼位於本主題隨附了：[下載](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)。</span><span class="sxs-lookup"><span data-stu-id="95200-119">A Visual Studio project with C# and Visual Basic source code is available to accompany this topic: [Download](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).</span></span>

### <a name="what-youll-build"></a><span data-ttu-id="95200-120">您將建置</span><span class="sxs-lookup"><span data-stu-id="95200-120">What You'll Build</span></span>

<span data-ttu-id="95200-121">您將新增範本 （具體而言，編輯和顯示範本） 中建立簡單的電影清單應用程式[Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="95200-121">You'll add templates (specifically, edit and display templates) to the simple movie-listing application that was created in the [Getting Started with MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) tutorial.</span></span> <span data-ttu-id="95200-122">您也會加入[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)簡化程序的輸入日期的快顯行事曆。</span><span class="sxs-lookup"><span data-stu-id="95200-122">You will also add a [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to simplify the process of entering dates.</span></span> <span data-ttu-id="95200-123">下列螢幕擷取畫面會顯示與 jQuery UI datepicker 快顯行事曆顯示修改過的應用程式。</span><span class="sxs-lookup"><span data-stu-id="95200-123">The following screenshot shows the modified application with the jQuery UI datepicker popup calendar displayed.</span></span>

![已完成的 jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="95200-125">您將學習到的技能</span><span class="sxs-lookup"><span data-stu-id="95200-125">Skills You'll Learn</span></span>

<span data-ttu-id="95200-126">以下是您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="95200-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="95200-127">如何使用屬性從[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)來控制資料的格式，顯示時，並處於編輯模式的命名空間。</span><span class="sxs-lookup"><span data-stu-id="95200-127">How to use attributes from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace to control the format of data when it's displayed and when it's in edit mode.</span></span>
- <span data-ttu-id="95200-128">如何建立範本 （編輯和顯示範本） 來控制資料的格式。</span><span class="sxs-lookup"><span data-stu-id="95200-128">How to create templates (edit and display templates) to control the formatting of data.</span></span>
- <span data-ttu-id="95200-129">如何新增[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)做為輸入的日期欄位的方式。</span><span class="sxs-lookup"><span data-stu-id="95200-129">How to add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) as a way to enter date fields.</span></span>

### <a name="getting-started"></a><span data-ttu-id="95200-130">快速入門</span><span class="sxs-lookup"><span data-stu-id="95200-130">Getting Started</span></span>

<span data-ttu-id="95200-131">如果您還沒有將入門專案的電影清單應用程式，下載：</span><span class="sxs-lookup"><span data-stu-id="95200-131">If you don't already have the movie-listing application from the starter project, download it:</span></span> 

* <span data-ttu-id="95200-132">[下載](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="95200-132">[Download](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span>
* <span data-ttu-id="95200-133">在 Windows 檔案總管中，以滑鼠右鍵按一下*MvcMovie.zip*檔案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="95200-133">In Windows Explorer, right-click the *MvcMovie.zip* file and select **Properties**.</span></span> 
* <span data-ttu-id="95200-134">在  **MvcMovie.zip 屬性**對話方塊中，選取**解除封鎖**。</span><span class="sxs-lookup"><span data-stu-id="95200-134">In the **MvcMovie.zip Properties** dialog box, select **Unblock**.</span></span> <span data-ttu-id="95200-135">(解除封鎖可避免安全性警告，當您嘗試使用時，就會發生 *.zip*您已經從 web 下載的檔案。)</span><span class="sxs-lookup"><span data-stu-id="95200-135">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

<span data-ttu-id="95200-136">以滑鼠右鍵按一下*MvcMovie.zip*檔案，然後選取**全部解壓縮**來解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="95200-136">Right-click the *MvcMovie.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="95200-137">在 Visual Web Developer] 或 [Visual Studio 2010 中，開啟*MvcMovieCS\_TU.sln*檔案。</span><span class="sxs-lookup"><span data-stu-id="95200-137">In Visual Web Developer or Visual Studio 2010, open the *MvcMovieCS\_TU.sln* file.</span></span>

<span data-ttu-id="95200-138">在 [**方案總管] 中**，按兩下*Views\Shared\\_Layout.cshtml*加以開啟。</span><span class="sxs-lookup"><span data-stu-id="95200-138">In **Solution Explorer**, double-click the *Views\Shared\\_Layout.cshtml* to open it.</span></span> <span data-ttu-id="95200-139">變更`H1`標頭**MVC 電影應用程式**要**電影 jQuery**。</span><span class="sxs-lookup"><span data-stu-id="95200-139">Change the `H1` header from **MVC Movie App** to **Movie jQuery**.</span></span> <span data-ttu-id="95200-140">按 CTRL + F5 執行應用程式，然後按一下**首頁**索引標籤上，會帶您前往`Index`電影控制器方法。</span><span class="sxs-lookup"><span data-stu-id="95200-140">Press CTRL+F5 to run the application and click the **Home** tab, which takes you to the `Index` method of the movie controller.</span></span> <span data-ttu-id="95200-141">若要試用應用程式，請選取**編輯**連結並**詳細資料**電影的其中一個連結。</span><span class="sxs-lookup"><span data-stu-id="95200-141">To try out the application, select the **Edit** link and the **Details** link for one of the movies.</span></span> <span data-ttu-id="95200-142">請注意，在索引中，編輯，並適當格式化的詳細資料檢視、 發行日期和價格：</span><span class="sxs-lookup"><span data-stu-id="95200-142">Notice that in the Index, Edit, and Details views, the release date and price are nicely formatted:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

<span data-ttu-id="95200-143">格式化的日期和價格是使用結果[Displayformat.{0](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)上的內容屬性`Movie`類別。</span><span class="sxs-lookup"><span data-stu-id="95200-143">The formatting for the date and the price is the result of using the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute on properties of the `Movie` class.</span></span>

<span data-ttu-id="95200-144">開啟*Movie.cs*檔案，並標記為註解`DisplayFormat`屬性`ReleaseDate`和`Price`屬性。</span><span class="sxs-lookup"><span data-stu-id="95200-144">Open the *Movie.cs* file and comment out the `DisplayFormat` attribute on the `ReleaseDate` and `Price` properties.</span></span> <span data-ttu-id="95200-145">產生`Movie`類別看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="95200-145">The resulting `Movie` class looks like this:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

<span data-ttu-id="95200-146">按 CTRL + F5 以執行應用程式，然後選取**首頁**索引標籤，檢視的電影清單。</span><span class="sxs-lookup"><span data-stu-id="95200-146">Press CTRL+F5 again to run the application and select the **Home** tab to view the movie list.</span></span> <span data-ttu-id="95200-147">這次發行日期顯示日期和時間，以及 [價格] 欄位不會再顯示貨幣符號。</span><span class="sxs-lookup"><span data-stu-id="95200-147">This time the release date shows the date and time, and the price field no longer shows the currency symbol.</span></span> <span data-ttu-id="95200-148">在您變更`Movie`類別已復原不錯的格式，您稍早所見，但您將在稍後修正該問題。</span><span class="sxs-lookup"><span data-stu-id="95200-148">Your change in the `Movie` class has undone the nice formatting that you saw earlier, but you'll fix that in a moment.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a><span data-ttu-id="95200-149">使用 DataAnnotations DataType 屬性來指定資料類型</span><span class="sxs-lookup"><span data-stu-id="95200-149">Using the DataAnnotations DataType Attribute to Specify the Data Type</span></span>

<span data-ttu-id="95200-150">取代標記為註解`DisplayFormat`屬性`ReleaseDate`屬性[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性，使用`Date`列舉型別。</span><span class="sxs-lookup"><span data-stu-id="95200-150">Replace the commented-out `DisplayFormat` attribute for the `ReleaseDate` property with the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute, using the `Date` enumeration.</span></span> <span data-ttu-id="95200-151">取代`DisplayFormat`屬性`Price`屬性[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性同樣地，這次使用`Currency`列舉型別。</span><span class="sxs-lookup"><span data-stu-id="95200-151">Replace the `DisplayFormat` attribute for the `Price` property with the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute again, this time using the `Currency` enumeration.</span></span> <span data-ttu-id="95200-152">這是完整的程式碼看起來像：</span><span class="sxs-lookup"><span data-stu-id="95200-152">This is what the completed code looks like:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

<span data-ttu-id="95200-153">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="95200-153">Run the application.</span></span> <span data-ttu-id="95200-154">現在在發行日期和價格屬性的格式正確 （也就利用適當的日期和貨幣格式）。</span><span class="sxs-lookup"><span data-stu-id="95200-154">Now the release date and the price properties are formatted correctly (that is, using appropriate date and currency formats).</span></span> <span data-ttu-id="95200-155">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性提供型別中繼資料內建的 ASP.NET MVC 範本，以便呈現格式正確的欄位。</span><span class="sxs-lookup"><span data-stu-id="95200-155">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute provides type metadata for the built-in ASP.NET MVC templates so that the fields render in the correct format.</span></span> <span data-ttu-id="95200-156">使用`DataType`屬性時，最好使用`DisplayFormat`屬性，因為原本是在程式碼的`DataType`屬性可讓模型更簡潔且更有彈性國際化等用途。</span><span class="sxs-lookup"><span data-stu-id="95200-156">Using the `DataType` attribute is preferable to using the `DisplayFormat` attribute that was originally in the code, because the `DataType` attribute makes the model cleaner and more flexible for purposes like internationalization.</span></span>

<span data-ttu-id="95200-157">下一節中，您會看到如何進行自訂的範本，來顯示日期欄位。</span><span class="sxs-lookup"><span data-stu-id="95200-157">In the next section you'll see how to make custom templates to display date fields.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="95200-158">下一步</span><span class="sxs-lookup"><span data-stu-id="95200-158">Next</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
