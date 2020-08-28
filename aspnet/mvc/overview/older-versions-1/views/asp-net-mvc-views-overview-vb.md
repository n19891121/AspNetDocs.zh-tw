---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC Views 總覽 (VB) |Microsoft Docs
author: StephenWalther
description: 什麼是 ASP.NET MVC 視圖，以及它與 HTML 網頁有何不同？ 在本教學課程中，Stephen Walther 將介紹您的觀點，並示範如何進行 .。。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a07d15cb14e9ef90b62c5a8702dee53f1a0a6032
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044661"
---
# <a name="aspnet-mvc-views-overview-vb"></a>ASP.NET MVC 檢視概觀 (VB)

依 [Stephen Walther](https://github.com/StephenWalther)

> 什麼是 ASP.NET MVC 視圖，以及它與 HTML 網頁有何不同？ 在本教學課程中，Stephen Walther 將介紹您的觀點，並示範如何利用視圖內的 View Data 和 HTML helper。

本教學課程的目的是要提供您 ASP.NET MVC 視圖、查看資料和 HTML 協助程式的簡介。 在本教學課程結束時，您應該瞭解如何建立新的視圖、如何將資料從控制器傳遞至視圖，以及如何使用 HTML 協助程式來產生視圖中的內容。

## <a name="understanding-views"></a>了解檢視

不同于 ASP.NET 或 Active Server Pages，ASP.NET MVC 不包含任何直接對應至頁面的作業。 在 ASP.NET MVC 應用程式中，磁片上沒有對應至您在瀏覽器網址列中輸入之路徑的頁面。 在 ASP.NET MVC 應用程式中，最接近頁面的地方就是所謂的 *觀點*。

在 ASP.NET MVC 應用程式中，傳入的瀏覽器要求會對應至控制器動作。 控制器動作可能會傳回一個 view。 不過，控制器動作可能會執行其他類型的動作，例如將您重新導向至另一個控制器動作。

[清單 1] 包含一個名為 HomeController 的簡單控制器。 HomeController 會公開兩個控制器動作，名為 Index ( # A1 和 Details ( # A3。

**清單 1-HomeController .vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

您可以在瀏覽器網址列中輸入下列 URL，以叫用第一個動作（索引 ( # A1 動作）：

/Home/Index

您可以在瀏覽器中輸入下列位址，以叫用第二個動作（詳細資料 ( # A1 動作）：

/Home/Details

索引 ( # A1 動作會傳回一個 view。 您所建立的大部分動作都會傳回 views。 不過，動作可能會傳回其他類型的動作結果。 例如， ( # A1 動作的詳細資料會傳回將連入要求重新導向至索引的 RedirectToActionResult， ( # A3 動作。

索引 ( # A1 動作包含下列一行程式碼：

View ( # A1

這行程式碼會傳回必須位於 web 伺服器上下列路徑的視圖：

\Views\Home\Index.aspx

視圖的路徑是從控制器的名稱和控制器動作的名稱推斷而來。

如果您想要的話，您可以明確瞭解此視圖。 下面這行程式碼會傳回名為 Fred 的視圖：

View ( Fred ) 

執行這行程式碼時，會從下列路徑傳回 view：

\Views\Home\Fred.aspx

> [!NOTE] 
> 
> 如果您打算為 ASP.NET MVC 應用程式建立單元測試，則最好明確瞭解視圖名稱。 如此一來，您就可以建立單元測試來確認控制器動作是否傳回預期的視圖。

## <a name="adding-content-to-a-view"></a>將內容加入至視圖

View 是標準的 (X) HTML 檔案，可以包含腳本。 您可以使用腳本將動態內容新增到視圖中。

例如，[清單 2] 中的視圖會顯示目前的日期和時間。

**清單 2-\Views\Home\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

請注意，[清單 2] 中的 HTML 頁面主體包含下列腳本：

&lt;% Response。寫入 (的日期時間。現在) %&gt;

您可以使用腳本分隔符號 &lt; % 和% &gt; 來標記腳本的開頭和結尾。 此腳本是以 Visual basic 撰寫。 它會藉由呼叫回應來顯示目前的日期和時間。請撰寫 ( # A1 方法，將內容轉譯至瀏覽器。 您 &lt; 可以使用腳本分隔符號% 和% &gt; 來執行一或多個語句。

由於您會呼叫回應，因此，Microsoft 會為您提供呼叫回應的快捷方式。請撰寫 ( # A3 方法，以 ( # A1。 [清單 3] 中的視圖使用分隔符號 &lt; % = 和% &gt; 做為呼叫回應的快捷方式。寫入 ( # A1。

**清單 3-Views\Home\Index2.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

您可以使用任何 .NET 語言，在視圖中產生動態內容。 一般來說，您會使用 Visual Basic .NET 或 c # 來撰寫控制器和 views。

## <a name="using-html-helpers-to-generate-view-content"></a>使用 HTML helper 來產生視圖內容

為了讓您更輕鬆地將內容新增至視圖，您可以利用所謂的 *HTML Helper*。 HTML Helper 通常是產生字串的方法。 您可以使用 HTML 協助程式來產生標準 HTML 元素，例如文字方塊、連結、下拉式清單和清單方塊。

例如，[清單 4] 中的視圖會利用三個 HTML 協助程式--Html.beginform ( # A1、TextBox ( # A3 和密碼 ( # A5 協助程式--若要產生登入表單 (請參閱 [圖 1]) 。

**清單 4--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

[![[New Project] \(新增專案\) 對話方塊](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)

**圖 01**：標準登入表單 ([按一下以查看完整大小的影像](asp-net-mvc-views-overview-vb/_static/image2.png)) 

所有的 HTML helper 方法都是在視圖的 Html 屬性上呼叫。 例如，您可以藉由呼叫 Html ( # A1 方法來呈現 TextBox。

請注意，當您同時呼叫 Html 時，您會使用腳本分隔符號 &lt; % = 和% &gt; ( # A1 和 Html。密碼 ( # A3 helper。 這些協助程式只會傳回字串。 您必須呼叫回應。請撰寫 ( # A1，以便將字串轉譯至瀏覽器。

使用 HTML Helper 方法是選擇性的。 藉由減少您需要撰寫的 HTML 和腳本數量，讓您的生活更輕鬆。 [清單 5] 中的視圖會轉譯與 [清單 4] 中的外觀完全相同的表單，而不使用 HTML 協助程式。

**清單 5--\Views\Home\Login.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

您也可以選擇建立自己的 HTML helper。 例如，您可以建立 GridView ( # A1 helper 方法，此方法會自動顯示 HTML 資料表中的一組資料庫記錄。 在 **建立自訂 HTML**協助程式的教學課程中，我們將探討這個主題。

## <a name="using-view-data-to-pass-data-to-a-view"></a>使用 View Data 將資料傳遞至視圖

您可以使用 view data 將資料從控制器傳遞至 view。 您可以將視圖資料視為您透過郵件傳送的封裝。 所有從控制器傳遞至視圖的資料都必須使用此封裝來傳送。 例如，[清單 6] 中的控制器會新增訊息來查看資料。

**清單 6-ProductController .vb**

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

控制器 ViewData 屬性代表名稱和值配對的集合。 在 [清單 6] 中，索引 ( # A1 方法會將專案加入至名為 message 的 view 資料集合，其值為 Hello World！。 當 ( # A1 方法的索引傳回視圖時，會自動將視圖資料傳遞給視圖。

[清單 7] 中的視圖會從 view 資料取出訊息，並將訊息轉譯至瀏覽器。

**清單 7--\Views\Product\Index.aspx**

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

請注意，此視圖會利用 Html。轉譯訊息時， ( # A1 HTML Helper 方法的編碼方式。 Html ( # A1 HTML Helper 會將特殊字元（例如和）編碼為可 &lt; &gt; 安全顯示在網頁中的字元。 每當您轉譯使用者提交至網站的內容時，您應該將內容編碼以防止 JavaScript 插入式攻擊。

 (，因為我們會在 ProductController 中自行建立訊息，所以不需要將訊息編碼。 不過，最好是一律呼叫 Html，在顯示視圖內從 view 資料取出的內容時，編碼 ( # A1 方法。 ) 

在 [清單 7] 中，我們利用了 view data，從控制器將簡單的字串訊息傳遞給視圖。 您也可以使用 view data，將其他類型的資料（例如資料庫記錄集合）從控制器傳遞至 view。 例如，如果您想要在 view 中顯示 Products 資料庫資料表的內容，則您會在 view data 中傳遞資料庫記錄的集合。

您也可以選擇將強型別視圖資料從控制器傳遞至 view。 在教學課程中，我們將探討 **瞭解強型別 View 資料和 Views**的這個主題。

## <a name="summary"></a>摘要

本教學課程提供 ASP.NET MVC 視圖、查看資料和 HTML 協助程式的簡介。 在第一節中，您已瞭解如何將新的視圖加入至您的專案。 您已瞭解您必須在正確的資料夾中加入一個視圖，才能從特定控制器呼叫它。 接下來，我們討論過 HTML 協助程式的主題。 您已瞭解 HTML 協助程式如何讓您輕鬆地產生標準的 HTML 內容。 最後，您已瞭解如何利用 view data 來將控制器中的資料傳遞給視圖。

> [!div class="step-by-step"]
> [上一個](passing-data-to-view-master-pages-cs.md) 
> [下一步](creating-custom-html-helpers-vb.md)
