---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 建立自訂 HTML 說明器 (C#) |微軟文件
author: rick-anderson
description: 本教學的目標是示範如何建立自訂 HTML 幫助器,您可以在 MVC 檢視中使用。 透過使用 HTML 說明程式...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 82e4118fd404051b891489b62d531169e83f450d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542556"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="498f1-104">建立自訂的 HTML 協助程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="498f1-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="498f1-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="498f1-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="498f1-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="498f1-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="498f1-107">本教學的目標是示範如何建立自訂 HTML 幫助器,您可以在 MVC 檢視中使用。</span><span class="sxs-lookup"><span data-stu-id="498f1-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="498f1-108">通過使用 HTML 說明器,可以減少創建標準 HTML 頁必須執行的繁瑣鍵入 HTML 標記的數量。</span><span class="sxs-lookup"><span data-stu-id="498f1-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="498f1-109">本教學的目標是示範如何建立自訂 HTML 幫助器,您可以在 MVC 檢視中使用。</span><span class="sxs-lookup"><span data-stu-id="498f1-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="498f1-110">通過使用 HTML 說明器,可以減少創建標準 HTML 頁必須執行的繁瑣鍵入 HTML 標記的數量。</span><span class="sxs-lookup"><span data-stu-id="498f1-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="498f1-111">在本教學的第一部分中,我描述了 ASP.NET MVC 框架中包含的一些現有 HTML 幫助器。</span><span class="sxs-lookup"><span data-stu-id="498f1-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="498f1-112">接下來,我描述了創建自定義 HTML 幫助器的兩種方法:我解釋如何通過創建靜態方法和創建擴展方法來創建自定義 HTML 説明程式。</span><span class="sxs-lookup"><span data-stu-id="498f1-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="498f1-113">瞭解 HTML 說明器</span><span class="sxs-lookup"><span data-stu-id="498f1-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="498f1-114">HTML 說明程式只是傳回字串的方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="498f1-115">字串可以表示所需的任何類型的內容。</span><span class="sxs-lookup"><span data-stu-id="498f1-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="498f1-116">例如,可以使用 HTML 幫助器呈現標準 HTML`<input>``<img>`標記(如 HTML 和標記)。</span><span class="sxs-lookup"><span data-stu-id="498f1-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="498f1-117">您還可以使用 HTML 說明器呈現更複雜的內容,如選項卡條或資料庫資料的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="498f1-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="498f1-118">mVC 框架ASP.NET包括以下一組標準 HTML 說明器(這不是完整的清單):</span><span class="sxs-lookup"><span data-stu-id="498f1-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="498f1-119">Html.操作連結()</span><span class="sxs-lookup"><span data-stu-id="498f1-119">Html.ActionLink()</span></span>
- <span data-ttu-id="498f1-120">Html.開始形式()</span><span class="sxs-lookup"><span data-stu-id="498f1-120">Html.BeginForm()</span></span>
- <span data-ttu-id="498f1-121">Html.選擇方塊()</span><span class="sxs-lookup"><span data-stu-id="498f1-121">Html.CheckBox()</span></span>
- <span data-ttu-id="498f1-122">Html.下拉清單()</span><span class="sxs-lookup"><span data-stu-id="498f1-122">Html.DropDownList()</span></span>
- <span data-ttu-id="498f1-123">Html.結束形式()</span><span class="sxs-lookup"><span data-stu-id="498f1-123">Html.EndForm()</span></span>
- <span data-ttu-id="498f1-124">Html.隱藏()</span><span class="sxs-lookup"><span data-stu-id="498f1-124">Html.Hidden()</span></span>
- <span data-ttu-id="498f1-125">Html.列表框()</span><span class="sxs-lookup"><span data-stu-id="498f1-125">Html.ListBox()</span></span>
- <span data-ttu-id="498f1-126">Html.密碼()</span><span class="sxs-lookup"><span data-stu-id="498f1-126">Html.Password()</span></span>
- <span data-ttu-id="498f1-127">Html.收音機按鈕()</span><span class="sxs-lookup"><span data-stu-id="498f1-127">Html.RadioButton()</span></span>
- <span data-ttu-id="498f1-128">Html.文字區域()</span><span class="sxs-lookup"><span data-stu-id="498f1-128">Html.TextArea()</span></span>
- <span data-ttu-id="498f1-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="498f1-129">Html.TextBox()</span></span>

<span data-ttu-id="498f1-130">例如,請考慮清單 1 中的表單。</span><span class="sxs-lookup"><span data-stu-id="498f1-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="498f1-131">此表單是在兩個標準 HTML 幫助器的説明下呈現的(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="498f1-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="498f1-132">此表單使用`Html.BeginForm()`與`Html.TextBox()`說明器方法呈現簡單的 HTML 窗體。</span><span class="sxs-lookup"><span data-stu-id="498f1-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="498f1-133">[![使用 HTML 說明器呈現的頁面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="498f1-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="498f1-134">**圖 01**: 使用 HTML 說明器呈現的頁面 ([按下以檢視全尺寸影像](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="498f1-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="498f1-135">**清單1 |`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="498f1-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="498f1-136">Html.BeginForm() 說明器方法用於建立打開和關閉`<form>`HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="498f1-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="498f1-137">請注意,該方法`Html.BeginForm()`是在 using 語句中調用的。</span><span class="sxs-lookup"><span data-stu-id="498f1-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="498f1-138">using 語句可確保標記`<form>`在 using 塊的末尾關閉。</span><span class="sxs-lookup"><span data-stu-id="498f1-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="498f1-139">如果您願意,可以調用 Html.EndForm() 説明器方法`<form>`來關閉 標記,而不是創建 using 塊。</span><span class="sxs-lookup"><span data-stu-id="498f1-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="498f1-140">使用任何方法創建您最直觀的開始和結束`<form>`標記。</span><span class="sxs-lookup"><span data-stu-id="498f1-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="498f1-141">在`Html.TextBox()`清單1中使用幫助器方法來呈現`<input>`HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="498f1-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="498f1-142">如果在瀏覽器中選擇視圖源,則會在清單 2 中看到 HTML 源。</span><span class="sxs-lookup"><span data-stu-id="498f1-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="498f1-143">請注意,來源包含標準 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="498f1-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="498f1-144">請注意 -HTML`Html.TextBox()`幫助`<%= %>`程式使用`<% %>`標記而不是 標記呈現。</span><span class="sxs-lookup"><span data-stu-id="498f1-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="498f1-145">如果未包含等號,則不會向瀏覽器呈現任何內容。</span><span class="sxs-lookup"><span data-stu-id="498f1-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="498f1-146">mVC ASP.NET框架包含一小組幫助器。</span><span class="sxs-lookup"><span data-stu-id="498f1-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="498f1-147">最有可能的是,您需要使用自訂 HTML 幫助程式擴展 MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="498f1-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="498f1-148">在本教學的其餘部分中,您將學習建立自定義 HTML 幫助器的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="498f1-149">**清單2 |`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="498f1-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="498f1-150">使用靜態方法建立 HTML 說明器</span><span class="sxs-lookup"><span data-stu-id="498f1-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="498f1-151">建立新 HTML 說明器的最簡單方法是建立傳回字串的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="498f1-152">例如,假設您決定創建一個呈現`<label>`HTML 標記的新 HTML 説明程式。</span><span class="sxs-lookup"><span data-stu-id="498f1-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="498f1-153">可以使用清單 2 中的類別呈現`<label>`。</span><span class="sxs-lookup"><span data-stu-id="498f1-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="498f1-154">**清單2 |`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="498f1-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="498f1-155">清單2中的類沒有什麼特別之處。</span><span class="sxs-lookup"><span data-stu-id="498f1-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="498f1-156">該方法`Label()`只需返回一個字串。</span><span class="sxs-lookup"><span data-stu-id="498f1-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="498f1-157">清單3中修改後的索引檢視使用`LabelHelper`來呈現`<label>`HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="498f1-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="498f1-158">請注意,檢視包含導入命名`<%@ imports %>`空間的`Application1.Helpers`指令。</span><span class="sxs-lookup"><span data-stu-id="498f1-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="498f1-159">**清單2 |`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="498f1-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="498f1-160">使用延伸方法建立 HTML 說明程式</span><span class="sxs-lookup"><span data-stu-id="498f1-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="498f1-161">如果要建立與 ASP.NET mVC 框架中包含的標準 HTML 説明程式相同的 HTML 説明程式,則需要創建擴充方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="498f1-162">擴展方法使您能夠向現有類添加新方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="498f1-163">建立 HTML 說明器方法時,向由檢視的 Html 屬性表示的 HtmlHelper 類添加新方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="498f1-164">清單3中的類向名為`HtmlHelper``Label()`的 類添加了擴充方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="498f1-165">關於這個類,你應該注意一些事情。</span><span class="sxs-lookup"><span data-stu-id="498f1-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="498f1-166">首先,請注意類是靜態類。</span><span class="sxs-lookup"><span data-stu-id="498f1-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="498f1-167">必須使用靜態類定義擴展方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="498f1-168">其次,請注意,`Label()`方法的第一個參數前面是關鍵`this`字 。</span><span class="sxs-lookup"><span data-stu-id="498f1-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="498f1-169">擴展方法的第一個參數指示擴展方法擴展的類。</span><span class="sxs-lookup"><span data-stu-id="498f1-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="498f1-170">**清單3 |`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="498f1-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="498f1-171">創建擴充方法並成功建構應用程式後,擴充方法與類的所有其他方法一樣顯示在 Visual Studio Intellisense 中(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="498f1-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="498f1-172">唯一的區別是擴展方法旁邊出現一個特殊符號(向下箭頭的圖示)。</span><span class="sxs-lookup"><span data-stu-id="498f1-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="498f1-173">[![使用 Html.label() 擴充方法](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="498f1-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="498f1-174">**圖 02**: 使用 Html.label() 延伸方法 ([按下以檢視全尺寸影像](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="498f1-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="498f1-175">清單4中修改後的索引檢視使用 Html.label() 擴充方法`<label>`呈現其所有 標記。</span><span class="sxs-lookup"><span data-stu-id="498f1-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="498f1-176">**清單4 |`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="498f1-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="498f1-177">總結</span><span class="sxs-lookup"><span data-stu-id="498f1-177">Summary</span></span>

<span data-ttu-id="498f1-178">在本教學中,您學習了創建自定義 HTML 幫助器的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="498f1-179">首先,您學習了如何通過創建返回字串`Label()`的靜態方法來創建自定義 HTML 説明程式。</span><span class="sxs-lookup"><span data-stu-id="498f1-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="498f1-180">接下來,您學習了如何通過在`Label()``HtmlHelper`類上創建擴展方法來創建自定義 HTML 幫助器方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="498f1-181">在本教學中,我重點討論了建構一個非常簡單的 HTML 幫助器方法。</span><span class="sxs-lookup"><span data-stu-id="498f1-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="498f1-182">意識到 HTML 説明程式可能非常複雜。</span><span class="sxs-lookup"><span data-stu-id="498f1-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="498f1-183">可以生成 HTML 說明程式,這些幫助程式呈現豐富的內容,如樹檢視、功能表或資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="498f1-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="498f1-184">[前一個](asp-net-mvc-views-overview-cs.md)
> [下一個](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="498f1-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
