---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX 控制工具套件控制並控制延伸器 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何將 AJAX 控制工具套件控制項和擴展器添加到ASP.NET頁。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543713"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>使用 AJAX Control Toolkit 控制項及控制項擴充項 (C#)

由[微軟](https://github.com/microsoft)

> 瞭解如何將 AJAX 控制工具套件控制項和擴展器添加到ASP.NET頁。

AJAX 控制工具套件包含一元件和控制擴展器。 在本教學中,您將瞭解如何將控制器和控制擴展器添加到ASP.NET頁。

> [!NOTE] 
> 
> 有關安裝 AJAX 控制工具組並將 AJAX 控制工具套件添加到可視化工作室/可視化 Web 開發人員工具組的說明,請參閱[有關 AJAX 控制項工具組入門](get-started-with-the-ajax-control-toolkit-cs.md)教學。

## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX 控制工具套件控制項

AJAX 控制工具套件控制項的工作方式與普通ASP.NET控件類似。 您可以將控制式從工具匣拖到ASP.NET頁上。 您可以在「設計」檢視或「源」檢視中將控制件添加到頁面。

使用 AJAX 控制工具套件中的控制件時有一個特殊要求。 該頁必須包含腳本管理器控制項。 文稿管理器控制項負責包括 AJAX 控制工具套件控制件所需的所有 JavaScript。

例如,AJAX 控制件工具組選項卡包括名為編輯器控制項的控制項。 此控制項顯示豐富的 HTML 編輯器。 依以下步驟將編輯器控制項

1. 建立新ASP.NET頁面名為 ShowEditor.aspx
2. 從工具箱中的 AJAX 擴展選項卡下方選擇腳本管理器控制項,並將該控制項拖到頁面上。
3. 從工具箱中的 AJAX 控制工具組選項卡下方選擇編輯器控制件,並將控制項拖到頁面上(參見圖 1)。 設計器應如圖 2 所示。
4. 通過選擇功能表選項 **「除錯、「開始除錯**」或點擊 F5 鍵來運行網站。
5. 您應該會看到圖 3 中的頁面。

[![選擇 HTML 編輯器控制項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**圖 01**:選擇 HTML 編輯器控制件([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[![具有文稿管理員及編輯控制項的視覺化工作室設計器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**圖 02**: 具有文稿管理員與編輯控制項的視覺化工作室設計器([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[![顯示編輯器.aspx 頁面](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**圖 03**: 顯示編輯器.aspx 頁面([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控制工具套件控制擴充器

AJAX 控制工具組還包含控制擴展器。 顧名思義,控件擴展器擴展了現有控制項的功能。 例如,「確認按鈕」控制器擴展器擴展了標準ASP.NET按鈕控制項。 擴展程式更改按鈕控制件的行為,以便按一下按鈕時顯示確認對話方塊。

控制項延伸器(與 AJAX 控制項工具套件控制件一樣)需要文稿管理器控制項。 在開始使用頁面中的控制器之前,必須將文稿管理器控制項添加到頁面。

依以下步驟使用確認按鈕控制元件延伸器:

1. 創建新ASP.NET頁面名為"顯示確認按鈕.aspx"
2. 通過將控制項從 AJAX 擴充選項卡下方拖曳到頁面上,將文本管理器控制件添加到頁面。
3. 通過將「按鈕」從工具箱中的「標準」選項卡下方拖動到「設計器」圖面,將標準按鈕控制項添加到頁面。
4. 按下 **「新增延伸器**」工作選項(參見圖 4)。
5. 在「選擇擴展器」對話框中,選擇「確認按鈕擴展器」(參見圖 5),然後單擊"確定"按鈕。
6. 選擇設計器中的「按鈕」控制器並展開「屬性」視窗中的\_Button1 確認按鈕擴展器節點(參見圖 6)。 將值 *「真的?"* 分配給」確認文本"
7. 通過選擇功能表選項 **「調試」、「開始調試」** 或點擊 F5 鍵來運行頁面。

[![新增擴充器工作選項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**圖 04**: 新增延伸器工作選項([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[![選擇確認按鍵控制延伸器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**圖 05**: 選擇確認按鈕控制元件延伸器([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))

[![設定確認按鈕屬性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**圖 06**: 設定確認按鈕屬性([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))

打開頁面時,應看到一個按鈕。 按下這個按鈕時,您將獲得圖 7 中的確認對話框。

[![顯示確認對話框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**圖 07**: 顯示確認對話框([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

請注意,您通常不會將控制器拖動到頁面上。 相反,您可以使用 **「新增延伸器**」工作選項將擴展器添加到已添加到頁面的控制項。 此外,請注意,通過打開要擴展的控制項的屬性表來設置控制元件擴展器屬性。

單個ASP.NET控件可以通過多個控制元件擴展器進行擴展。 要擴展的控制項的屬性表將列出與控制項關聯的所有控制元件擴展器。

> [!div class="step-by-step"]
> [前一個](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一個](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
