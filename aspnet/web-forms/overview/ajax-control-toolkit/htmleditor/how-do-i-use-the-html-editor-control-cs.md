---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何使用 HTML 編輯器控制項? (C#) |微軟文件
author: rick-anderson
description: HTMLEditor 是 ASP.NET AJAX 控制件,允許您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: eb3a87f914c24ada52ebb5a315a7e242e96158f7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543115"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>如何使用 HTML 編輯器控制項? (C#)

由[微軟](https://github.com/microsoft)

> HTMLEditor 是 ASP.NET AJAX 控制件,允許您透過工具列中的按鈕輕鬆建立和編輯 HTML 內容。

本教學的目標是為您提供 AJAX 控制工具套件中包含的 HTML 編輯器控制項的概述。 HTML 編輯器包括用於更改字型大小、選擇字型、更改背景顏色、修改前景顏色、添加連結、添加圖像、更改文本對齊以及執行剪切、複製和粘貼操作的選項(參見圖 1)。

[![HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**圖 01**: HTML 編輯器([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image2.png))

HTML 編輯器允許您使用設計模式輸入內容,也可以直接輸入 HTML。 此外,您還可以提供預覽 HTML 內容的選項(參見圖 2)。

[![設計、HTML 和預覽按鈕](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**圖 02**:設計、HTML 和預覽按鈕([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image4.png))

在本教學中,您將瞭解如何顯示 HTML 編輯器、如何自訂 HTML 編輯器中顯示的工具列按鈕以及如何避免跨網站腳稿攻擊。

## <a name="displaying-the-html-editor"></a>顯示 HTML 編輯器

在ASP.NET頁中使用 HTML 編輯器之前,必須先向該頁添加文本管理器控制項。 文稿管理器控制件位於可視化工作室/可視化 Web 開發人員快速工具箱中的 AJAX 擴充選項卡下方。

您應該在頁面的任何其他控制項之前將腳本管理器控制件放在頁面頂部。 例如,您可以將它放在打開的伺服器端&lt;窗&gt;體 標記的下方。

HTML 編輯器控制件與 AJAX 控制件工具套件控制件的其餘部分一起位於工具箱中。 它被命名為編輯器控制件(參見圖 3)。

[![HTML 編輯器控制項](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**圖 03**: HTML 編輯器控制件([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image6.png))

將 HTML 編輯器拖到頁面上後,可以在屬性表中設置其屬性。 例如,您通常要設置"寬度"和"高度"屬性。 清單 1 包含包含 HTML 編輯器的 ASP.NET 頁的來源。

**清單 1 - 簡單編輯器.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

清單1中的頁面包含 HTML 編輯器控制件、按鈕控制項和文字控制元件。 按下這個按鈕時,HTML 編輯器的內容將顯示在「文字」控制件中(參見圖 4)。

[![使用 HTML 編輯器提交表單](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**圖 04**: 提交含有 HTML 編輯器的表單([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image8.png))

HTML 編輯器內容屬性用於檢索輸入到 HTML 編輯器中的 HTML 內容。 請注意,此 HTML 內容可能包含 JavaScript。 在下一節中,我們將討論如何防止 JAVAScript 注入攻擊。

## <a name="customizing-the-html-editor-toolbar"></a>自訂 HTML 編輯器工具列

您可以準確自定義編輯器中顯示的按鈕。 例如,您可能希望刪除 HTML 選項卡,以防止使用者將 HTML 編輯器切換到 HTML 模式。 或者,您可能希望刪除字體大小下拉清單,以防止使用者在論壇消息帖子中創建過大的文本(參見圖 5)。

[![自訂 HTML 編輯器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**圖 05**: 自訂 HTML 編輯器([按下以檢視全尺寸影像](how-do-i-use-the-html-editor-control-cs/_static/image10.png))

通過從基本編輯器類派生新的 HTML 編輯器來自定義工具列按鈕。 例如,清單 2 中的自定義編輯器僅包含粗體和斜體工具列按鈕。 所有其他工具列按鈕已被刪除。 此外,HTML 選項卡已從編輯器的底部刪除(但"設計和預覽"選項卡仍然存在)。

**清單2\_- 應用程式代碼_自訂編輯器.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

您必須將清單 2 中的類新增\_到應用程式碼資料夾,以便自動編譯該類。 如果網站中\_不存在應用代碼資料夾,則只需添加該資料夾即可。

創建自訂編輯器後,可以將其添加到ASP.NET頁,其方式與添加普通 HTML 編輯器的方式相同(請參閱清單 3)。

**清單3 - 顯示自訂編輯器.aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>避免跨網站文稿 (XSS) 攻擊

每當您接受使用者的輸入,並在網站上重新顯示該輸入時,您都有可能將網站打開以進行跨網站腳本 (XSS) 攻擊。 理論上,惡意駭客可以提交 JAVAScript 代碼,這些代碼在重新顯示輸入時將執行。 JavaScript 可用於竊取使用者密碼或其他敏感資訊。

通常,在網頁中顯示之前,可以通過 HTML 編碼從使用者檢索的任何輸入來擊敗 XSS 攻擊。 但是,HTML 編碼 HTML 編輯器的輸出不僅&lt;會編&gt;碼 文本標記,還會對所有 HTML 標記進行編碼。 換句話說,您將丟失所有格式,如字型類型、字體大小和背景顏色。

如果要從使用者收集敏感資訊(如密碼、信用卡號碼和社會保險號),則不應顯示使用 HTML 編輯器從使用者檢索的未編碼內容。 僅當您未重新播放 HTML 內容或受信任方向您的網站提交 HTML 內容的情況時,才應使用 HTML 編輯器。

例如,假設您正在創建一個博客應用程式。 在這種情況下,在撰寫部落格文章時使用 HTML 編輯器是有意義的。 您是唯一提交博客文章的人,而且,大概,您可以相信自己不會提交惡意的 JavaScript。 但是,在允許匿名使用者發表評論時,使用 HTML 編輯器是沒有意義的。 在使用者提交敏感資訊(如密碼)時,應特別小心。 惡意使用者可能會發佈包含用於竊取密碼的 JavaScript 的註釋。

## <a name="summary"></a>總結

在本教學中,您得到了 AJAX 控制工具套件中包含的 HTML 編輯器控制項的簡要概述。 您學習了如何使用 HTML 編輯器從使用者那裡接受豐富內容並將內容提交到伺服器。 我們還討論了如何自定義 HTML 編輯器顯示的工具列按鈕。 最後,您學習了在使用 HTML 編輯器接受潛在的惡意輸入時,如何避免跨網站腳本攻擊。

> [!div class="step-by-step"]
> [下一步](how-do-i-use-the-html-editor-control-vb.md)
