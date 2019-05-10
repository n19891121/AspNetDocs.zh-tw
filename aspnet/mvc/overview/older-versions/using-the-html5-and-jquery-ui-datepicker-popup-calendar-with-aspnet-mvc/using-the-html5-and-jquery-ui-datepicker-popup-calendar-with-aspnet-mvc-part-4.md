---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 使用 HTML5 與 jQuery UI Datepicker 快顯行事曆搭配 ASP.NET MVC-第 4 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將教導您如何使用編輯器範本、 顯示範本與 jQuery UI datepicker 快顯行事曆，ASP.NET MV 中的基本概念...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: d660fcbc561c84951c8376014e5c1902851a6caa
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65129566"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a><span data-ttu-id="a19bb-103">使用 HTML5 與 jQuery UI Datepicker 快顯行事曆搭配 ASP.NET MVC-第 4 部分</span><span class="sxs-lookup"><span data-stu-id="a19bb-103">Using the HTML5 and jQuery UI Datepicker Popup Calendar with ASP.NET MVC - Part 4</span></span>

<span data-ttu-id="a19bb-104">藉由[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="a19bb-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="a19bb-105">本教學課程將教導您如何使用編輯器範本、 顯示範本與 jQuery UI datepicker 快顯行事曆，ASP.NET MVC Web 應用程式中的基本概念。</span><span class="sxs-lookup"><span data-stu-id="a19bb-105">This tutorial will teach you the basics of how to work with editor templates, display templates, and the jQuery UI datepicker popup calendar in an ASP.NET MVC Web application.</span></span>

### <a name="adding-a-template-for-editing-dates"></a><span data-ttu-id="a19bb-106">新增範本進行編輯日期</span><span class="sxs-lookup"><span data-stu-id="a19bb-106">Adding a Template for Editing Dates</span></span>

<span data-ttu-id="a19bb-107">在本節中，您將建立範本，以進行編輯時，ASP.NET MVC 會顯示 UI，來編輯模型屬性以標記會套用的日期**日期**列舉[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="a19bb-107">In this section you'll create a template for editing dates that will be applied when ASP.NET MVC displays UI for editing model properties that are marked with the **Date** enumeration of the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) attribute.</span></span> <span data-ttu-id="a19bb-108">範本會呈現的日期;不會顯示時間。</span><span class="sxs-lookup"><span data-stu-id="a19bb-108">The template will render only the date; time will not be displayed.</span></span> <span data-ttu-id="a19bb-109">在範本中，您將使用[jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/)地編輯日期的快顯行事曆。</span><span class="sxs-lookup"><span data-stu-id="a19bb-109">In the template you'll use the [jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to provide a way to edit dates.</span></span>

<span data-ttu-id="a19bb-110">若要開始，開啟*Movie.cs*檔案，並新增[資料類型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性搭配**日期**列舉`ReleaseDate`屬性，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="a19bb-110">To begin, open the *Movie.cs* file and add the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute with the **Date** enumeration to the `ReleaseDate` property, as shown in the following code:</span></span>

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

<span data-ttu-id="a19bb-111">此程式碼會造成`ReleaseDate`的時間，以同時顯示範本，並編輯範本沒有要顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="a19bb-111">This code causes the `ReleaseDate` field to be displayed without the time in both display templates and edit templates.</span></span> <span data-ttu-id="a19bb-112">如果您的應用程式含有*date.cshtml*中的範本*Views\Shared\EditorTemplates*資料夾或*Views\Movies\EditorTemplates*資料夾中，該範本將用來呈現任何`DateTime`時編輯的屬性。</span><span class="sxs-lookup"><span data-stu-id="a19bb-112">If your application contains a *date.cshtml* template in the *Views\Shared\EditorTemplates* folder or in the *Views\Movies\EditorTemplates* folder, that template will be used to render any `DateTime` property while editing.</span></span> <span data-ttu-id="a19bb-113">否則內建的 ASP.NET 範本化系統會顯示為日期的屬性。</span><span class="sxs-lookup"><span data-stu-id="a19bb-113">Otherwise the built-in ASP.NET templating system will display the property as a date.</span></span>

<span data-ttu-id="a19bb-114">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19bb-114">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="a19bb-115">選取 [編輯] 連結來確認發行日期輸入的欄位會顯示只有表示日期。</span><span class="sxs-lookup"><span data-stu-id="a19bb-115">Select an edit link to verify that the input field for the release date is showing only the date.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

<span data-ttu-id="a19bb-116">在 [**方案總管] 中**，展開*檢視*資料夾中，展開*共用*資料夾，然後再以滑鼠右鍵按一下*Views\Shared\EditorTemplates*資料夾。</span><span class="sxs-lookup"><span data-stu-id="a19bb-116">In **Solution Explorer**, expand the *Views* folder, expand the *Shared* folder, and then right-click the *Views\Shared\EditorTemplates* folder.</span></span>

<span data-ttu-id="a19bb-117">按一下 **新增**，然後按一下**檢視**。</span><span class="sxs-lookup"><span data-stu-id="a19bb-117">Click **Add**, and then click **View**.</span></span> <span data-ttu-id="a19bb-118">**加入檢視**對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a19bb-118">The **Add View** dialog box is displayed.</span></span>

<span data-ttu-id="a19bb-119">在 **檢視表名稱**方塊中，輸入&quot;日期&quot;。</span><span class="sxs-lookup"><span data-stu-id="a19bb-119">In the **View name** box, type &quot;Date&quot;.</span></span>

<span data-ttu-id="a19bb-120">選取 **建立成局部檢視**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a19bb-120">Select the **Create as a partial view** check box.</span></span> <span data-ttu-id="a19bb-121">請確定**使用版面配置頁或主版頁面**並**建立強型別檢視**未選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a19bb-121">Make sure that the **Use a layout or master page** and **Create a strongly-typed view** check boxes are not selected.</span></span>

<span data-ttu-id="a19bb-122">按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="a19bb-122">Click **Add**.</span></span> <span data-ttu-id="a19bb-123">*Views\Shared\EditorTemplates\Date.cshtml*建立範本。</span><span class="sxs-lookup"><span data-stu-id="a19bb-123">The *Views\Shared\EditorTemplates\Date.cshtml* template is created.</span></span>

<span data-ttu-id="a19bb-124">將下列程式碼加入*Views\Shared\EditorTemplates\Date.cshtml*範本。</span><span class="sxs-lookup"><span data-stu-id="a19bb-124">Add the following code to the *Views\Shared\EditorTemplates\Date.cshtml* template.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

<span data-ttu-id="a19bb-125">第一行會宣告為模型`DateTime`型別。</span><span class="sxs-lookup"><span data-stu-id="a19bb-125">The first line declares the model to be a `DateTime` type.</span></span> <span data-ttu-id="a19bb-126">雖然您不需要編輯中的模型型別宣告，並顯示範本，它是最佳的作法，讓您取得編譯時間檢查傳遞至檢視的模型。</span><span class="sxs-lookup"><span data-stu-id="a19bb-126">Although you don't need to declare the model type in edit and display templates, it's a best practice so that you get compile-time checking of the model being passed to the view.</span></span> <span data-ttu-id="a19bb-127">（另一個優點是您再取得在 Visual Studio 中檢視模型的 IntelliSense）。如果未宣告的模型型別，ASP.NET MVC 會將它視為[動態](https://msdn.microsoft.com/library/dd264741.aspx)輸入，而且沒有任何編譯時期類型檢查。</span><span class="sxs-lookup"><span data-stu-id="a19bb-127">(Another benefit is that you then get IntelliSense for the model in the view in Visual Studio.) If the model type is not declared, ASP.NET MVC considers it a [dynamic](https://msdn.microsoft.com/library/dd264741.aspx) type and there's no compile-time type checking.</span></span> <span data-ttu-id="a19bb-128">如果您宣告模型`DateTime`型別，它會成為強型別。</span><span class="sxs-lookup"><span data-stu-id="a19bb-128">If you declare the model to be a `DateTime` type, it becomes strongly typed.</span></span>

<span data-ttu-id="a19bb-129">第二行是常值只會顯示的 HTML 標記&quot;使用的日期範本&quot;之前的日期欄位。</span><span class="sxs-lookup"><span data-stu-id="a19bb-129">The second line is just literal HTML markup that displays &quot;Using Date Template&quot; before a date field.</span></span> <span data-ttu-id="a19bb-130">您將暫時使用這一行，來確認正在使用此日期範本。</span><span class="sxs-lookup"><span data-stu-id="a19bb-130">You'll use this line temporarily to verify that this date template is being used.</span></span>

<span data-ttu-id="a19bb-131">下一行是[Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)呈現的協助程式`input`是文字方塊中的欄位。</span><span class="sxs-lookup"><span data-stu-id="a19bb-131">The next line is an [Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) helper that renders an `input` field that's a text box.</span></span> <span data-ttu-id="a19bb-132">協助程式的第三個參數會使用匿名型別來設定文字方塊中的類別`datefield`並輸入要`date`。</span><span class="sxs-lookup"><span data-stu-id="a19bb-132">The third parameter for the helper uses an anonymous type to set the class for the text box to `datefield` and the type to `date`.</span></span> <span data-ttu-id="a19bb-133">(因為`class`會保留在 C# 中，您需要使用`@`字元來逸出`class`C# 剖析器中的屬性。)</span><span class="sxs-lookup"><span data-stu-id="a19bb-133">(Because `class` is a reserved in C#, you need to use the `@` character to escape the `class` attribute in the C# parser.)</span></span>

<span data-ttu-id="a19bb-134">`date`型別是 HTML5 輸入的類型，可讓感知 HTML5 的瀏覽器來呈現 HTML5 行事曆控制項。</span><span class="sxs-lookup"><span data-stu-id="a19bb-134">The `date` type is an HTML5 input type that enables HTML5-aware browsers to render a HTML5 calendar control.</span></span> <span data-ttu-id="a19bb-135">稍後您將在其中加入一些 JavaScript，以連結到 jQuery datepicker`Html.TextBox`項目使用`datefield`類別。</span><span class="sxs-lookup"><span data-stu-id="a19bb-135">Later on you'll add some JavaScript to hook up the jQuery datepicker to the `Html.TextBox` element using the `datefield` class.</span></span>

<span data-ttu-id="a19bb-136">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19bb-136">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="a19bb-137">您可以確認`ReleaseDate`編輯檢視中的屬性使用編輯範本，因為範本會顯示&quot;使用日期範本&quot;之前`ReleaseDate`文字輸入方塊中，此映像所示：</span><span class="sxs-lookup"><span data-stu-id="a19bb-137">You can verify that the `ReleaseDate` property in the edit view is using the edit template because the template displays &quot;Using Date Template&quot; just before the `ReleaseDate` text input box, as shown in this image:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

<span data-ttu-id="a19bb-138">在瀏覽器中檢視頁面的來源。</span><span class="sxs-lookup"><span data-stu-id="a19bb-138">In your browser, view the source of the page.</span></span> <span data-ttu-id="a19bb-139">(例如，以滑鼠右鍵按一下  頁面上，並選取**檢視原始檔**。)下列範例示範一些標記頁面，說明`class`和`type`中轉譯的 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="a19bb-139">(For example, right-click the page and select **View source**.) The following example shows some of the markup for the page, illustrating the `class` and `type` attributes in the rendered HTML.</span></span>

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

<span data-ttu-id="a19bb-140">返回*Views\Shared\EditorTemplates\Date.cshtml*範本並移除&quot;使用日期範本&quot;標記。</span><span class="sxs-lookup"><span data-stu-id="a19bb-140">Return to the *Views\Shared\EditorTemplates\Date.cshtml* template and remove the &quot;Using Date Template&quot; markup.</span></span> <span data-ttu-id="a19bb-141">現在已完成的範本看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a19bb-141">Now the completed template looks like this:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a><span data-ttu-id="a19bb-142">新增 jQuery UI Datepicker 快顯行事曆使用 NuGet</span><span class="sxs-lookup"><span data-stu-id="a19bb-142">Adding a jQuery UI Datepicker Popup Calendar using NuGet</span></span>

<span data-ttu-id="a19bb-143">在本節中，您將新增[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆日期編輯範本。</span><span class="sxs-lookup"><span data-stu-id="a19bb-143">In this section you'll add the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar to the date-edit template.</span></span> <span data-ttu-id="a19bb-144">[JQuery UI](http://jqueryui.com/)動畫，進階的效果，以及可自訂的小工具程式庫提供支援。</span><span class="sxs-lookup"><span data-stu-id="a19bb-144">The [jQuery UI](http://jqueryui.com/) library provides support for animation, advanced effects, and customizable widgets.</span></span> <span data-ttu-id="a19bb-145">它是以 jQuery JavaScript 程式庫所建置的。</span><span class="sxs-lookup"><span data-stu-id="a19bb-145">It's built on top of the jQuery JavaScript library.</span></span> <span data-ttu-id="a19bb-146">Datepicker 快顯行事曆能夠以簡單且自然的輸入而不輸入字串中使用的行事曆的日期。</span><span class="sxs-lookup"><span data-stu-id="a19bb-146">The datepicker popup calendar makes it easy and natural to enter dates using a calendar instead of entering a string.</span></span> <span data-ttu-id="a19bb-147">快顯行事曆也會限制使用者合法的日期，日期的一般文字項目可讓您輸入類似`2/33/1999`(年 2 月 33rd，1999年)，但[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)快顯行事曆不允許的。</span><span class="sxs-lookup"><span data-stu-id="a19bb-147">The popup calendar also limits users to legal dates — ordinary text entry for a date would let you enter something like `2/33/1999` ( February 33rd, 1999), but the [jQuery UI datepicker](http://jqueryui.com/demos/datepicker/) popup calendar won't allow that.</span></span>

<span data-ttu-id="a19bb-148">首先，您必須安裝的 jQuery UI 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a19bb-148">First, you have to install the jQuery UI libraries.</span></span> <span data-ttu-id="a19bb-149">若要這樣做，您將使用 NuGet，也就是包含在 Visual Studio 2010 和 Visual Web Developer 的 SP1 版本的套件管理員。</span><span class="sxs-lookup"><span data-stu-id="a19bb-149">To do that, you'll use NuGet, which is a package manager that's included in SP1 versions of Visual Studio 2010 and Visual Web Developer.</span></span>

<span data-ttu-id="a19bb-150">在 Visual Web Developer 中，從**工具**功能表上，選取**NuGet 套件管理員**，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="a19bb-150">In Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

<span data-ttu-id="a19bb-151">注意:如果**工具**不會顯示功能表**NuGet 套件管理員**命令，您必須依照的指示安裝 NuGet[安裝 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)頁面NuGet 網站。</span><span class="sxs-lookup"><span data-stu-id="a19bb-151">Note: If the **Tools** menu doesn't display the **NuGet Package Manager** command, you need to install NuGet by following the instructions on the [Installing NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) page of the NuGet website.</span></span>   
  
<span data-ttu-id="a19bb-152">如果您使用 Visual Studio，而不是 Visual Web Developer 中，從**工具**功能表上，選取**NuGet 套件管理員**，然後選取**新增程式庫封裝參考**。</span><span class="sxs-lookup"><span data-stu-id="a19bb-152">If you're using Visual Studio instead of Visual Web Developer, from the **Tools** menu, select **NuGet Package Manager** and then select **Add Library Package Reference**.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

<span data-ttu-id="a19bb-153">在 [ **MVCMovie-管理 NuGet 套件**] 對話方塊中，按一下**線上**左側索引標籤，然後輸入&quot;jQuery.UI&quot;在搜尋方塊中。</span><span class="sxs-lookup"><span data-stu-id="a19bb-153">In the **MVCMovie - Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter &quot;jQuery.UI&quot; in the search box.</span></span> <span data-ttu-id="a19bb-154">選取 [j**查詢 UI Widget: Datepicker**，然後選取**安裝**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a19bb-154">Select j **Query UI Widgets:Datepicker**, then select the **Install** button.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

<span data-ttu-id="a19bb-155">NuGet 會將這些偵錯版本和縮製的版本的 jQuery UI 核心和 jQuery UI 日期選擇器新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="a19bb-155">NuGet adds these debug versions and minified versions of jQuery UI Core and the jQuery UI date picker to your project:</span></span>

- <span data-ttu-id="a19bb-156">*jquery.ui.core.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-156">*jquery.ui.core.js*</span></span>
- <span data-ttu-id="a19bb-157">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-157">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="a19bb-158">*jquery.ui.datepicker.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-158">*jquery.ui.datepicker.js*</span></span>
- <span data-ttu-id="a19bb-159">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-159">*jquery.ui.datepicker.min.js*</span></span>

<span data-ttu-id="a19bb-160">注意:偵錯版本 (不含任何檔案 *。 min.js*擴充功能) 適合進行偵錯，但在生產網站中，您會在加入縮製的版本。</span><span class="sxs-lookup"><span data-stu-id="a19bb-160">Note: The debug versions (the files without the *.min.js* extension) are useful for debugging, but in a production site, you'd include only the minified versions.</span></span>

<span data-ttu-id="a19bb-161">若要實際使用 jQuery 日期選擇器，您需要建立行事曆小工具，來編輯範本將會連結 jQuery 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a19bb-161">To actually use the jQuery date picker, you need to create a jQuery script that will hook up the calendar widget to the edit template.</span></span> <span data-ttu-id="a19bb-162">在 [**方案總管] 中**，以滑鼠右鍵按一下*指令碼*資料夾，然後選取**新增**，然後**新項目**，，然後**JScript檔案**。</span><span class="sxs-lookup"><span data-stu-id="a19bb-162">In **Solution Explorer**, right-click the *Scripts* folder and select **Add**, then **New Item**, and then **JScript File**.</span></span> <span data-ttu-id="a19bb-163">將檔案命名*DatePickerReady.js*。</span><span class="sxs-lookup"><span data-stu-id="a19bb-163">Name the file *DatePickerReady.js*.</span></span>

<span data-ttu-id="a19bb-164">將下列程式碼加入*DatePickerReady.js*檔案：</span><span class="sxs-lookup"><span data-stu-id="a19bb-164">Add the following code to the *DatePickerReady.js* file:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

<span data-ttu-id="a19bb-165">如果您不熟悉 jQuery，以下是這項功能的簡短說明： 第一行是&quot;jQuery 準備&quot;函式，在網頁中的所有 DOM 項目已都載入時呼叫。</span><span class="sxs-lookup"><span data-stu-id="a19bb-165">If you're not familiar with jQuery, here's a brief explanation of what this does: the first line is the &quot;jQuery ready&quot; function, which is called when all the DOM elements in a page have loaded.</span></span> <span data-ttu-id="a19bb-166">第二行中選取所有具有類別名稱的 DOM 項目`datefield`，然後叫用`datepicker`為每個函式。</span><span class="sxs-lookup"><span data-stu-id="a19bb-166">The second line selects all DOM elements that have the class name `datefield`, then invokes the `datepicker` function for each of them.</span></span> <span data-ttu-id="a19bb-167">(請記住，您會加入`datefield`類別，即可*Views\Shared\EditorTemplates\Date.cshtml*稍早在本教學課程中的範本。)</span><span class="sxs-lookup"><span data-stu-id="a19bb-167">(Remember that you added the `datefield` class to the *Views\Shared\EditorTemplates\Date.cshtml* template earlier in the tutorial.)</span></span>

<span data-ttu-id="a19bb-168">接下來，開啟*Views\Shared\\_Layout.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="a19bb-168">Next, open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="a19bb-169">您需要將參考加入至下列檔案，也就是所有必要的好讓您可以使用日期選擇器：</span><span class="sxs-lookup"><span data-stu-id="a19bb-169">You need to add references to the following files, which are all required so that you can use the date picker:</span></span>

- <span data-ttu-id="a19bb-170">*Content/themes/base/jquery.ui.core.css*</span><span class="sxs-lookup"><span data-stu-id="a19bb-170">*Content/themes/base/jquery.ui.core.css*</span></span>
- <span data-ttu-id="a19bb-171">*Content/themes/base/jquery.ui.datepicker.css*</span><span class="sxs-lookup"><span data-stu-id="a19bb-171">*Content/themes/base/jquery.ui.datepicker.css*</span></span>
- <span data-ttu-id="a19bb-172">*Content/themes/base/jquery.ui.theme.css*</span><span class="sxs-lookup"><span data-stu-id="a19bb-172">*Content/themes/base/jquery.ui.theme.css*</span></span>
- <span data-ttu-id="a19bb-173">*jquery.ui.core.min.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-173">*jquery.ui.core.min.js*</span></span>
- <span data-ttu-id="a19bb-174">*jquery.ui.datepicker.min.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-174">*jquery.ui.datepicker.min.js*</span></span>
- <span data-ttu-id="a19bb-175">*DatePickerReady.js*</span><span class="sxs-lookup"><span data-stu-id="a19bb-175">*DatePickerReady.js*</span></span>

<span data-ttu-id="a19bb-176">下列範例顯示的實際程式碼，您應該新增底部`head`中的項目*Views\Shared\\_Layout.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="a19bb-176">The following example shows the actual code that you should add at the bottom of the `head` element in the *Views\Shared\\_Layout.cshtml* file.</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

<span data-ttu-id="a19bb-177">完整`head`區段如下所示：</span><span class="sxs-lookup"><span data-stu-id="a19bb-177">The complete `head` section is shown here:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

<span data-ttu-id="a19bb-178">[URL 內容 helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法會將資源路徑轉換為絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="a19bb-178">The [URL content helper](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) method converts the resource path to an absolute path.</span></span> <span data-ttu-id="a19bb-179">您必須使用`@URL.Content`正確地參考這些資源在 IIS 上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19bb-179">You must use `@URL.Content` to correctly reference these resources when the application is running on IIS.</span></span>

<span data-ttu-id="a19bb-180">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19bb-180">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="a19bb-181">選取 [編輯] 連結，然後將插入點放**ReleaseDate**欄位。</span><span class="sxs-lookup"><span data-stu-id="a19bb-181">Select an edit link, then put the insertion point into the **ReleaseDate** field.</span></span> <span data-ttu-id="a19bb-182">JQuery UI 快顯行事曆會顯示。</span><span class="sxs-lookup"><span data-stu-id="a19bb-182">The jQuery UI popup calendar is displayed.</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

<span data-ttu-id="a19bb-183">大部分的 jQuery 控制項，例如 datepicker 可讓您廣泛地加以自訂。</span><span class="sxs-lookup"><span data-stu-id="a19bb-183">Like most jQuery controls, the datepicker lets you customize it extensively.</span></span> <span data-ttu-id="a19bb-184">如需資訊，請參閱[視覺自訂：設計的 jQuery UI 佈景主題](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)上[jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/)站台。</span><span class="sxs-lookup"><span data-stu-id="a19bb-184">For information, see [Visual Customization: Designing a jQuery UI theme](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) on the [jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/) site.</span></span>

### <a name="supporting-the-html5-date-input-control"></a><span data-ttu-id="a19bb-185">支援 HTML5 的日期輸入的控制項</span><span class="sxs-lookup"><span data-stu-id="a19bb-185">Supporting the HTML5 Date Input Control</span></span>

<span data-ttu-id="a19bb-186">更多瀏覽器支援 HTML5，您會想使用原生 HTML5 輸入，例如`date`輸入項目，並使用 jQuery UI 行事曆。</span><span class="sxs-lookup"><span data-stu-id="a19bb-186">As more browsers support HTML5, you'll want to use the native HTML5 input, such as the `date` input element, and not use the jQuery UI calendar.</span></span> <span data-ttu-id="a19bb-187">您可以將邏輯加入您的應用程式會自動使用 HTML5 控制項，如果瀏覽器支援它們。</span><span class="sxs-lookup"><span data-stu-id="a19bb-187">You can add logic to your application to automatically use HTML5 controls if the browser supports them.</span></span> <span data-ttu-id="a19bb-188">若要這樣做，請將取代的內容*DatePickerReady.js*以下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a19bb-188">To do this, replace the contents of the *DatePickerReady.js* file with the following:</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

<span data-ttu-id="a19bb-189">此指令碼的第一行會使用 Modernizr，確認支援 HTML5 日期輸入。</span><span class="sxs-lookup"><span data-stu-id="a19bb-189">The first line of this script uses Modernizr to verify that HTML5 date input is supported.</span></span> <span data-ttu-id="a19bb-190">如果不受支援，jQuery UI 日期選擇器會改為連結。</span><span class="sxs-lookup"><span data-stu-id="a19bb-190">If it's not supported, the jQuery UI date picker is hooked up instead.</span></span> <span data-ttu-id="a19bb-191">([Modernizr](http://www.modernizr.com/docs/)一個開放原始碼 JavaScript 程式庫，可偵測的 HTML5 和 CSS3 的原生實作的可用性。</span><span class="sxs-lookup"><span data-stu-id="a19bb-191">([Modernizr](http://www.modernizr.com/docs/) is an open-source JavaScript library that detects the availability of native implementations of HTML5 and CSS3.</span></span> <span data-ttu-id="a19bb-192">Modernizr 已隨附於您建立任何新 ASP.NET MVC 專案中）。</span><span class="sxs-lookup"><span data-stu-id="a19bb-192">Modernizr is included in any new ASP.NET MVC projects that you create.)</span></span>

<span data-ttu-id="a19bb-193">您進行這項變更之後，您可以使用瀏覽器支援 HTML5，例如 Opera 11 來進行測試。</span><span class="sxs-lookup"><span data-stu-id="a19bb-193">After you've made this change, you can test it by using a browser that supports HTML5, such as Opera 11.</span></span> <span data-ttu-id="a19bb-194">執行使用 HTML5 相容的瀏覽器的應用程式，並編輯電影項目。</span><span class="sxs-lookup"><span data-stu-id="a19bb-194">Run the application using an HTML5-compatible browser and edit a movie entry.</span></span> <span data-ttu-id="a19bb-195">會使用 HTML5 日期控制項，而不是 jQuery UI 快顯行事曆：</span><span class="sxs-lookup"><span data-stu-id="a19bb-195">The HTML5 date control is used instead of the jQuery UI popup calendar:</span></span>

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

<span data-ttu-id="a19bb-196">因為瀏覽器的新版本以累加方式實作 HTML5，現在是不錯的方法是將程式碼新增至您所能容納的 HTML5 支援各種不同的網站。</span><span class="sxs-lookup"><span data-stu-id="a19bb-196">Because new versions of browsers are implementing HTML5 incrementally, a good approach for now is to add code to your website that accommodates a wide variety of HTML5 support.</span></span> <span data-ttu-id="a19bb-197">比方說，更強固*DatePickerReady.js*指令碼如下所示，可讓您僅部分支援 HTML5 日期控制項的站台支援瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="a19bb-197">For example, a more robust *DatePickerReady.js* script is shown below that lets your site support browsers that only partially support the HTML5 date control.</span></span>

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

<span data-ttu-id="a19bb-198">此指令碼會選取 HTML5`input`類型的項目`date`未完全支援 HTML5 日期控制項。</span><span class="sxs-lookup"><span data-stu-id="a19bb-198">This script selects HTML5 `input` elements of type `date` that don't fully support the HTML5 date control.</span></span> <span data-ttu-id="a19bb-199">針對這些項目，其連結的 jQuery UI 快顯行事曆，然後變更`type`屬性從`date`至`text`。</span><span class="sxs-lookup"><span data-stu-id="a19bb-199">For those elements, it hooks up the jQuery UI popup calendar and then changes the `type` attribute from `date` to `text`.</span></span> <span data-ttu-id="a19bb-200">藉由變更`type`屬性從`date`到`text`，也會刪除 HTML5 日期的部分支援。</span><span class="sxs-lookup"><span data-stu-id="a19bb-200">By changing the `type` attribute from `date` to `text`, partial HTML5 date support is eliminated.</span></span> <span data-ttu-id="a19bb-201">更加強固*DatePickerReady.js*指令碼，請參閱[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)。</span><span class="sxs-lookup"><span data-stu-id="a19bb-201">An even more robust *DatePickerReady.js* script can be found at [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).</span></span>

### <a name="adding-nullable-dates-to-the-templates"></a><span data-ttu-id="a19bb-202">加入範本中的可為 Null 的日期</span><span class="sxs-lookup"><span data-stu-id="a19bb-202">Adding Nullable Dates to the Templates</span></span>

<span data-ttu-id="a19bb-203">如果您使用其中一個現有的日期範本，並傳遞 null 的日期，您會收到執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="a19bb-203">If you use one of the existing date templates and pass a null date, you'll get a run-time error.</span></span> <span data-ttu-id="a19bb-204">若要進行更穩固的日期範本，您會將它們來處理 null 值。</span><span class="sxs-lookup"><span data-stu-id="a19bb-204">To make the date templates more robust, you'll change them to handle null values.</span></span> <span data-ttu-id="a19bb-205">若要支援可為 null 的日期，將變更中的程式碼*Views\Shared\DisplayTemplates\DateTime.cshtml*如下：</span><span class="sxs-lookup"><span data-stu-id="a19bb-205">To support nullable dates, change the code in the *Views\Shared\DisplayTemplates\DateTime.cshtml* to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

<span data-ttu-id="a19bb-206">程式碼會傳回空字串，當模型**null**。</span><span class="sxs-lookup"><span data-stu-id="a19bb-206">The code returns an empty string when the model is **null**.</span></span>

<span data-ttu-id="a19bb-207">變更中的程式碼*Views\Shared\EditorTemplates\Date.cshtml*下列檔案：</span><span class="sxs-lookup"><span data-stu-id="a19bb-207">Change the code in the *Views\Shared\EditorTemplates\Date.cshtml* file to the following:</span></span>

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

<span data-ttu-id="a19bb-208">此程式碼執行時，該模型不是 null，如果模型的`DateTime`會使用值。</span><span class="sxs-lookup"><span data-stu-id="a19bb-208">When this code runs, if the model is not null, the model's `DateTime` value is used.</span></span> <span data-ttu-id="a19bb-209">如果模型是 null，就會改為使用目前的日期。</span><span class="sxs-lookup"><span data-stu-id="a19bb-209">If the model is null, the current date is used instead.</span></span>

### <a name="wrapup"></a><span data-ttu-id="a19bb-210">簡便</span><span class="sxs-lookup"><span data-stu-id="a19bb-210">Wrapup</span></span>

<span data-ttu-id="a19bb-211">本教學課程涵蓋 ASP.NET 樣板化 helper 的基本概念，並示範如何使用 ASP.NET MVC 應用程式中的 jQuery UI datepicker 快顯行事曆。</span><span class="sxs-lookup"><span data-stu-id="a19bb-211">This tutorial has covered the basics of ASP.NET templated helpers and shows you how to use the jQuery UI datepicker popup calendar in an ASP.NET MVC application.</span></span> <span data-ttu-id="a19bb-212">如需詳細資訊，請嘗試這些資源：</span><span class="sxs-lookup"><span data-stu-id="a19bb-212">For more information, try these resources:</span></span>

- <span data-ttu-id="a19bb-213">如需當地語系化資訊，請參閱 Rajeesh 的部落格[ASP.NET MVC 中的 JQueryUI Datepicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。</span><span class="sxs-lookup"><span data-stu-id="a19bb-213">For information on localization, see Rajeesh's blog [JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).</span></span>
- <span data-ttu-id="a19bb-214">JQuery UI 的相關資訊，請參閱[jQuery UI](http://docs.jquery.com/UI)。</span><span class="sxs-lookup"><span data-stu-id="a19bb-214">For information about jQuery UI, see [jQuery UI](http://docs.jquery.com/UI).</span></span>
- <span data-ttu-id="a19bb-215">如需如何當地語系化 datepicker 控制項的詳細資訊，請參閱[UI/Datepicker/當地語系化](http://docs.jquery.com/UI/Datepicker/Localization)。</span><span class="sxs-lookup"><span data-stu-id="a19bb-215">For information about how to localize the datepicker control, see [UI/Datepicker/Localization](http://docs.jquery.com/UI/Datepicker/Localization).</span></span>
- <span data-ttu-id="a19bb-216">如需有關 ASP.NET MVC 範本的詳細資訊，請參閱 Brad Wilson 的部落格系列[ASP.NET MVC 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="a19bb-216">For more information about the ASP.NET MVC templates, see Brad Wilson's blog series on [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="a19bb-217">雖然系列撰寫 ASP.NET MVC 2，資料仍適用於目前版本的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="a19bb-217">Although the series was written for ASP.NET MVC 2, the material still applies for the current version of ASP.NET MVC.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a19bb-218">上一步</span><span class="sxs-lookup"><span data-stu-id="a19bb-218">Previous</span></span>](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
