---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用彩選器控制器 (VB) |微軟文件
author: rick-anderson
description: ColorPicker 是 ASP.NET AJAX 擴充器,在彈出視窗控制項中提供客戶端選色功能和 UI。 它可以附加到任何ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542842"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>使用彩選擇器控制器 (VB)

由[微軟](https://github.com/microsoft)

> ColorPicker 是 ASP.NET AJAX 擴充器,在彈出視窗控制項中提供客戶端選色功能和 UI。 它可以附加到任何ASP.NET文本框控件。 它。

本教學的目的是解釋如何使用 AJAX 控制項工具套件 ColorPicker 控制件延伸器。 ColorPicker 控制元件延伸器顯示一個彈出對話框,讓您能夠選擇顏色。 當您要為使用者提供直觀的使用者介面以選擇顏色時,ColorPicker 非常有用。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>使用彩選擇器控制器延伸器延伸文字框控制項

例如,假設您想要創建一個網站,使訪問者能夠創建自定義的名片。 存取者可以輸入名片的文字並選擇顏色。 清單1中的ASP.NET頁包含兩個名為 txtCardText 和 txtCardColor 的 TextBox 控制項。 提交表單時,將顯示所選值(參見圖 1)。

[![建立名片的簡單表單](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**圖01:** 建立名片的簡單表單([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image2.png))

**清單 1 - 建立卡.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

清單1中的表單有效,但它不能提供出色的用戶體驗。 使用者必須鍵入文字框中的顏色。 如果使用者想要專用顏色(例如,只是豌豆綠色的正確陰影),則用戶必須在沒有任何幫助的情況下找出 HTML 顏色代碼。

您可以使用 ColorPicker 控制元件擴充器來創建更好的使用者體驗。 將焦點移至 TextBox 控制件時,顏色選取器將顯示顏色對話框(參見圖 2)。

[![彩工控制延伸器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**圖 02**: 彩選擇器控制元件延伸器 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image4.png))

您需要完成兩個步驟才能將 ColorPicker 控制元件延伸器與清單 1 中的表單一起使用:

1. 將文稿管理員加入頁面
2. 將彩選擇器控制器

使用 ColorPicker 之前,必須向頁面加入文稿管理員。 添加文本管理器的好地方就在打開的伺服器端&lt;表&gt;單 標記的正下方。 您可以將文稿管理器從工具箱拖到頁面上(文稿管理器位於 AJAX 擴展選項卡下)。 或者,您可以在開啟伺服器端表單標籤下的源檢視中鍵入以下標記:

&lt;asp:文稿管理員 ID="文稿管理員1"運行 at="伺服器" /&gt;

將 ColorPicker 控制元件擴展器添加到頁面的最簡單方法是在「設計檢視」 中。 如果將滑鼠懸停在 txtCardColor TextBox 上,將顯示一個智慧任務選項,使您能夠添加擴展器(參見圖 3)。 如果選擇此選項,將顯示擴展器嚮導(參見圖 4)。

[![新增延伸器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**圖 03**: 新增延伸器 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image6.png))

[![使用延伸器精靈選擇控制器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**圖 04**:使用延伸器精靈選擇控制元件延伸器([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image8.png))

您可以選擇顏色選取器延伸器,以便使用顏色選取器延伸器延伸 txtCardColor 文字盒。 按一下 [確定] 關閉對話方塊。

進行這些更改後,頁面的源類似於清單 2。

**清單2 - CreateCard.aspx(含彩選器)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

請注意,該頁面現在包含一個顏色選取器擴展器控制件,該控件直接顯示在 txtCardColor 文字盒控制項的正下方。 顏色選取器延伸器控制項延伸 txtCardColor 控制項,以便顯示顏色選取器對話方塊。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>使用按鈕啟動顏色選擇器對話框

色彩選擇器延伸器支援以下屬性:

- 彈出ButtonId - 頁面上導致顏色選取器對話框顯示的按鈕的 ID。
- 彈出位置 - 顏色選取器對話框相對於目標控制項的位置。 可能的值是「絕對」、「中心」、「左下」、「右下角」、「左上」、「右」、「左」(預設值為」左下」。
- 範例控制代碼 - 顯示選取的顏色的控制項的識別碼。
- 選擇顏色 - 顏色選擇器選擇的初始顏色。

您可以使用這些屬性自定義顏色選取器對話框的顯示方式以及選取顏色的顯示方式。 清單3中的頁面說明瞭如何使用其中幾個屬性。

**清單3 - 建立卡按鈕.aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

清單3中的頁面包括「選取顏色」按鈕(參見圖 5)。 按下此按鈕時,顏色選取器對話框將顯示在 TextBox 上方。 如果從對話框中選擇顏色,則選取顏色將顯示為 lblSample 標籤控制項的背景顏色。

"顏色選擇器彈出按鈕ID"屬性用於將"拾取顏色"按鈕與"顏色選取器"擴充器相關聯。 當您提供 PopupButtonID 屬性的值時,當目標控制項具有焦點時,顏色選取器對話方塊將不再顯示。 您必須按下這個按鈕才能顯示對話框。

SampleControlID 屬性用於將顯示所選顏色的控制項與顏色選取器相關聯。 顏色選擇器將此控制的背景顏色改變為目前選擇的顏色。

[![使用按鈕顯示顏色選擇器對話框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**圖 05**: 使用按鈕顯示顏色選擇器對話框 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image10.png))

## <a name="summary"></a>總結

在本教學中,您學習了如何使用 ColorPicker 控制元件擴展器來顯示彈出顏色選取器對話框。 首先,我們檢查了在焦點移動到 TextBox 控件時如何顯示對話方塊。 接下來,您學習了如何在按一下該按鈕時創建顯示顏色選取器對話框的按鈕。

> [!div class="step-by-step"]
> [上一步](using-the-colorpicker-control-extender-cs.md)
