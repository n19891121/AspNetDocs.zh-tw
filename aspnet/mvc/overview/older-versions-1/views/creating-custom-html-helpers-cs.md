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
# <a name="creating-custom-html-helpers-c"></a>建立自訂的 HTML 協助程式 (C#)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> 本教學的目標是示範如何建立自訂 HTML 幫助器,您可以在 MVC 檢視中使用。 通過使用 HTML 說明器,可以減少創建標準 HTML 頁必須執行的繁瑣鍵入 HTML 標記的數量。

本教學的目標是示範如何建立自訂 HTML 幫助器,您可以在 MVC 檢視中使用。 通過使用 HTML 說明器,可以減少創建標準 HTML 頁必須執行的繁瑣鍵入 HTML 標記的數量。

在本教學的第一部分中,我描述了 ASP.NET MVC 框架中包含的一些現有 HTML 幫助器。 接下來,我描述了創建自定義 HTML 幫助器的兩種方法:我解釋如何通過創建靜態方法和創建擴展方法來創建自定義 HTML 説明程式。

## <a name="understanding-html-helpers"></a>瞭解 HTML 說明器

HTML 說明程式只是傳回字串的方法。 字串可以表示所需的任何類型的內容。 例如,可以使用 HTML 幫助器呈現標準 HTML`<input>``<img>`標記(如 HTML 和標記)。 您還可以使用 HTML 說明器呈現更複雜的內容,如選項卡條或資料庫資料的 HTML 表。

mVC 框架ASP.NET包括以下一組標準 HTML 說明器(這不是完整的清單):

- Html.操作連結()
- Html.開始形式()
- Html.選擇方塊()
- Html.下拉清單()
- Html.結束形式()
- Html.隱藏()
- Html.列表框()
- Html.密碼()
- Html.收音機按鈕()
- Html.文字區域()
- Html.TextBox()

例如,請考慮清單 1 中的表單。 此表單是在兩個標準 HTML 幫助器的説明下呈現的(參見圖 1)。 此表單使用`Html.BeginForm()`與`Html.TextBox()`說明器方法呈現簡單的 HTML 窗體。

[![使用 HTML 說明器呈現的頁面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**圖 01**: 使用 HTML 說明器呈現的頁面 ([按下以檢視全尺寸影像](creating-custom-html-helpers-cs/_static/image3.png))

**清單1 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html.BeginForm() 說明器方法用於建立打開和關閉`<form>`HTML 標記。 請注意,該方法`Html.BeginForm()`是在 using 語句中調用的。 using 語句可確保標記`<form>`在 using 塊的末尾關閉。

如果您願意,可以調用 Html.EndForm() 説明器方法`<form>`來關閉 標記,而不是創建 using 塊。 使用任何方法創建您最直觀的開始和結束`<form>`標記。

在`Html.TextBox()`清單1中使用幫助器方法來呈現`<input>`HTML 標記。 如果在瀏覽器中選擇視圖源,則會在清單 2 中看到 HTML 源。 請注意,來源包含標準 HTML 標籤。

> [!IMPORTANT]
> 請注意 -HTML`Html.TextBox()`幫助`<%= %>`程式使用`<% %>`標記而不是 標記呈現。 如果未包含等號,則不會向瀏覽器呈現任何內容。

mVC ASP.NET框架包含一小組幫助器。 最有可能的是,您需要使用自訂 HTML 幫助程式擴展 MVC 框架。 在本教學的其餘部分中,您將學習建立自定義 HTML 幫助器的兩種方法。

**清單2 |`Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>使用靜態方法建立 HTML 說明器

建立新 HTML 說明器的最簡單方法是建立傳回字串的靜態方法。 例如,假設您決定創建一個呈現`<label>`HTML 標記的新 HTML 説明程式。 可以使用清單 2 中的類別呈現`<label>`。

**清單2 |`Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

清單2中的類沒有什麼特別之處。 該方法`Label()`只需返回一個字串。

清單3中修改後的索引檢視使用`LabelHelper`來呈現`<label>`HTML 標記。 請注意,檢視包含導入命名`<%@ imports %>`空間的`Application1.Helpers`指令。

**清單2 |`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>使用延伸方法建立 HTML 說明程式

如果要建立與 ASP.NET mVC 框架中包含的標準 HTML 説明程式相同的 HTML 説明程式,則需要創建擴充方法。 擴展方法使您能夠向現有類添加新方法。 建立 HTML 說明器方法時,向由檢視的 Html 屬性表示的 HtmlHelper 類添加新方法。

清單3中的類向名為`HtmlHelper``Label()`的 類添加了擴充方法。 關於這個類,你應該注意一些事情。 首先,請注意類是靜態類。 必須使用靜態類定義擴展方法。

其次,請注意,`Label()`方法的第一個參數前面是關鍵`this`字 。 擴展方法的第一個參數指示擴展方法擴展的類。

**清單3 |`Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

創建擴充方法並成功建構應用程式後,擴充方法與類的所有其他方法一樣顯示在 Visual Studio Intellisense 中(參見圖 2)。 唯一的區別是擴展方法旁邊出現一個特殊符號(向下箭頭的圖示)。

[![使用 Html.label() 擴充方法](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**圖 02**: 使用 Html.label() 延伸方法 ([按下以檢視全尺寸影像](creating-custom-html-helpers-cs/_static/image6.png))

清單4中修改後的索引檢視使用 Html.label() 擴充方法`<label>`呈現其所有 標記。

**清單4 |`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>總結

在本教學中,您學習了創建自定義 HTML 幫助器的兩種方法。 首先,您學習了如何通過創建返回字串`Label()`的靜態方法來創建自定義 HTML 説明程式。 接下來,您學習了如何通過在`Label()``HtmlHelper`類上創建擴展方法來創建自定義 HTML 幫助器方法。

在本教學中,我重點討論了建構一個非常簡單的 HTML 幫助器方法。 意識到 HTML 説明程式可能非常複雜。 可以生成 HTML 說明程式,這些幫助程式呈現豐富的內容,如樹檢視、功能表或資料庫資料表。

> [!div class="step-by-step"]
> [前一個](asp-net-mvc-views-overview-cs.md)
> [下一個](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
