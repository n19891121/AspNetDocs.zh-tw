---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX Control Toolkit 控制項及控制項擴充項 (C#) |Microsoft Docs
author: microsoft
description: 了解如何將 AJAX Control Toolkit 控制項及擴充項新增至您的 ASP.NET 網頁。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 82fae91e40ec2f1508fe5c82992eeef4abc4e19a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59419219"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>使用 AJAX Control Toolkit 控制項及控制項擴充項 (C#)

by [Microsoft](https://github.com/microsoft)

> 了解如何將 AJAX Control Toolkit 控制項及擴充項新增至您的 ASP.NET 網頁。


AJAX Control Toolkit 包含一組控制項及控制項擴充項。 在這個簡短的教學課程中，您會學習如何將控制項及控制項擴充項新增至 ASP.NET 網頁。

> [!NOTE] 
> 
> 如需安裝 AJAX Control Toolkit，然後加入 Visual Studio/Visual Web Developer 工具箱中，將 AJAX Control Toolkit 中的指示，請參閱本教學課程[開始使用 AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md)。


## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX Control Toolkit 控制項

未 AJAX Control Toolkit 控制項的運作方式就像一般的 ASP.NET 控制項一樣。 您可以將控制項從 [工具箱] 拖曳到 ASP.NET 頁面。 您可以將控制項新增至 設計檢視 或 原始碼檢視中的頁面。

使用 AJAX Control Toolkit 控制項時，沒有一項特殊的需求。 頁面必須包含 ScriptManager 控制項。 ScriptManager 控制項負責包括所有必要的 JavaScript AJAX Control Toolkit 控制項所需。

比方說，AJAX Control Toolkit 索引標籤會包含名為編輯器控制項的控制項。 此控制項會顯示豐富的 HTML 編輯器。 請遵循下列步驟來新增至網頁的編輯器控制項：

1. 建立新的 ASP.NET 頁面，名為 ShowEditor.aspx
2. 在 [工具箱] 選取 [AJAX 延伸模組] 索引標籤來 ScriptManager 控制項，並將控制項拖曳到頁面。
3. 工具箱] 中選取編輯器控制項，來 [AJAX Control Toolkit] 索引標籤，然後將控制項拖曳到頁面 （請參閱 [圖 1）。 設計工具看起來應該如 圖 2。
4. 透過選取功能表選項來執行網站**偵錯，請啟動偵錯**或按下 F5 鍵。
5. 您應該會看到 圖 3 中的頁面。


[![選取 HTML 編輯器控制項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**圖 01**:選取 HTML 編輯器控制項 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))


[![使用 ScriptManager 和 編輯控制項的 visual Studio 設計工具](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**圖 02**:使用 ScriptManager] 和 [編輯控制項的 visual Studio 設計工具 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))


[![DisplayEditor.aspx 頁面](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**圖 03**:DisplayEditor.aspx 頁面 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控制項 Toolkit 控制項擴充項

AJAX Control Toolkit 也會包含控制項擴充項。 正如其名，控制擴充項會擴充現有控制項的功能。 比方說，ConfirmButton 控制項擴充項會擴充標準的 ASP.NET 按鈕控制項。 擴充項變更的按鈕控制項的行為，使按鈕會顯示確認對話方塊中，當您按一下它。

控制項擴充項，就像未 AJAX Control Toolkit 控制項中，需要 ScriptManager 控制項。 開始使用網頁中的控制項擴充項之前您必須加入頁面的 ScriptManager 控制項。

請遵循下列步驟使用 ConfirmButton 控制項擴充項：

1. 建立新的 ASP.NET 頁面，名為 ShowConfirmButton.aspx
2. 藉由將控制項拖曳到頁面 [AJAX 延伸模組] 索引標籤來加入網頁的 ScriptManager 控制項。
3. 在工具箱 拖曳至設計工具介面上拖曳按鈕，一般 索引標籤來加入頁面的標準按鈕控制項。
4. 按一下 **加入擴充項**工作選項 （請參閱 圖 4）。
5. 在 選擇擴充性 對話方塊中，選取 ConfirmButtonExtender （請參閱 圖 5），然後按一下 確定 按鈕。
6. 在設計工具選取按鈕控制項，並展開擴充項，Button1\_ConfirmButtonExtender 節點，在 屬性 視窗中的 （請參閱 圖 6）。 將值指派*真的？* ConfirmText 屬性。
7. 選取功能表選項來執行網頁**偵錯，請啟動偵錯**或按下 F5 鍵。


[![[新增 Extender] 工作選項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**圖 04**:[新增 Extender] 工作選項 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))


[![選取 ConfirmButton 控制項擴充項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**圖 05**:選取 ConfirmButton 控制項擴充項 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))


[![設定 ConfirmButton 屬性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**圖 06**:設定 ConfirmButton 屬性 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))


當頁面開啟時，您應該會看到一個按鈕。 當您按一下按鈕時，您會取得確認對話方塊中，[圖 7] 中。


[![顯示 [確認] 對話方塊](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**圖 07**:顯示確認對話方塊中 ([按一下以檢視完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))


請注意，您通常執行不將控制項擴充項拖曳至頁面。 相反地，您使用**加入擴充項**工作選項，將擴充項新增至已加入至頁面的控制項。 此外，請注意，您設定控制項擴充項屬性藉由開啟所擴充控制項的屬性工作表。

在單一的 ASP.NET 控制項可以由多個控制項擴充項擴充。 所擴充控制項的屬性工作表會列出所有與控制項關聯的控制項擴充項。

> [!div class="step-by-step"]
> [上一頁](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一頁](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
