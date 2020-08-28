---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: 使用 AJAX 控制項工具組控制項和控制項擴充項 (VB) |Microsoft Docs
author: rick-anderson
description: 瞭解如何將 AJAX 控制項工具組控制項和擴充項加入至 ASP.NET 網頁。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 416ee0d4931a3850c1e9bb4ba28db43f5e1647bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044359"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>使用 AJAX Control Toolkit 控制項及控制項擴充項 (VB)

由 [Microsoft](https://github.com/microsoft)

> 瞭解如何將 AJAX 控制項工具組控制項和擴充項加入至 ASP.NET 網頁。

AJAX 控制項工具組包含一組控制項和控制項擴充項。 在這個簡短的教學課程中，您將瞭解如何將控制項和控制項擴充項加入至 ASP.NET 網頁。

> [!NOTE] 
> 
> 如需有關如何安裝 AJAX 控制項工具組，以及將 AJAX 控制項工具組新增至 Visual Studio/Visual Web Developer 工具箱的指示，請參閱教學課程開始中的 [Ajax 控制項工具](get-started-with-the-ajax-control-toolkit-vb.md)組。

## <a name="using-ajax-control-toolkit-controls"></a>使用 AJAX 控制項工具組控制項

AJAX 控制項工具組控制項的運作方式就像一般的 ASP.NET 控制項一樣。 您可以將控制項從 [工具箱] 拖曳至 ASP.NET 網頁。 您可以在設計檢視或來源視圖的頁面中加入控制項。

使用 AJAX 控制項工具組中的控制項時，有一項特殊需求。 頁面必須包含 ScriptManager 控制項。 ScriptManager 控制項負責包含 AJAX 控制項工具組控制項所需的所有必要 JavaScript。

例如，[AJAX 控制項工具組] 索引標籤包含一個名為 Editor 控制項的控制項。 此控制項會顯示豐富的 HTML 編輯器。 遵循下列步驟將編輯器控制項新增至頁面：

1. 建立新的 ASP.NET 網頁，名為 ShowEditor .aspx
2. 從 [工具箱] 的 [AJAX 擴充功能] 索引標籤底下選取 ScriptManager 控制項，然後將控制項拖曳到頁面上。
3. 從 [工具箱] 的 [AJAX 控制項工具組] 索引標籤底下選取編輯器控制項，然後將控制項拖曳到頁面上 (見 [圖 1]) 。 設計工具看起來應該如圖2所示。
4. 選取功能表選項 [ **Debug]、[開始** ] 或按 F5 鍵，以執行網站。
5. 您應該會看到 [圖 3] 中的頁面。

[![選取 HTML 編輯器控制項](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**圖 01**：選取 HTML 編輯器控制項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png)) 

[![使用 ScriptManager 和編輯控制項 Visual Studio 設計工具](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**圖 02**：使用 ScriptManager 和編輯控制項 Visual Studio 設計工具 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png)) 

[![DisplayEditor .aspx 頁面](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**圖 03**： DisplayEditor .aspx 頁面 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png)) 

## <a name="using-ajax-control-toolkit-control-extenders"></a>使用 AJAX 控制項工具組控制項擴充項

AJAX 控制項工具組也包含控制項擴充項。 如其名所示，控制項擴充項會擴充現有控制項的功能。 例如，項 confirmbutton 控制項擴充項會擴充標準 ASP.NET 按鈕控制項。 擴充項會變更按鈕控制項的行為，如此當您按一下按鈕時，按鈕就會顯示確認對話方塊。

控制項擴充項和 AJAX 控制項工具組控制項一樣，都需要 ScriptManager 控制項。 在頁面中開始使用控制項擴充項之前，您必須先將 ScriptManager 控制項加入頁面中。

遵循下列步驟以使用項 confirmbutton 控制項擴充項：

1. 建立新的 ASP.NET 網頁，名為 ShowConfirmButton .aspx
2. 從 [AJAX 擴充功能] 索引標籤底下，將控制項拖曳至頁面上，以將 ScriptManager 控制項加入至頁面。
3. 將 [標準] 按鈕控制項從 [工具箱] 中的 [標準] 索引標籤下拖曳至設計工具介面，以將其加入至頁面。
4. 按一下 [ **加入** 擴充項工作] 選項 (參閱 [圖 4]) 。
5. 在 [選擇擴充項] 對話方塊中，選取 [ConfirmButtonExtender (參閱 [圖 5]) 然後按一下 [確定] 按鈕。
6. 選取設計工具中的 [Button] 控制項，然後展開屬性視窗中的 [Button1]、[Button1 \_ ConfirmButtonExtender] 節點 (看到 [圖 6]) 。 指派值 *' 真的？ '* ConfirmText 屬性。
7. 選取功能表選項 [Debug]、[ **開始** ] 或按 F5 鍵來執行頁面。

[![新增擴充項工作選項](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**圖 04**： [加入擴充項工作] 選項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png)) 

[![選取項 confirmbutton 控制項擴充項](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**圖 05**：選取項 confirmbutton 控制項擴充項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png)) 

[![設定項 confirmbutton 屬性](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**圖 06**：設定項 confirmbutton 屬性 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png)) 

當頁面開啟時，您應該會看到一個按鈕。 當您按一下按鈕時，您會在 [圖 7] 中看到確認對話方塊。

[![顯示確認對話方塊](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**圖 07**：顯示確認對話方塊 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png)) 

請注意，您通常不會將控制項擴充項拖曳到頁面上。 相反地，您可以使用 [ **加入** 擴充項工作] 選項，將擴充項加入至已加入至頁面的控制項。 另外也請注意，您可以藉由開啟要擴充之控制項的屬性工作表來設定控制項擴充項屬性。

單一 ASP.NET 控制項可以由多個控制項擴充項延伸。 要擴充之控制項的屬性工作表將會列出與控制項相關聯的所有控制項擴充項。

> [!div class="step-by-step"]
> [上一個](get-started-with-the-ajax-control-toolkit-vb.md) 
> [下一步](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
