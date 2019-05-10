---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: 調整 DropShadow (VB) 的 Z 軸索引 |Microsoft Docs
author: wenz
description: DropShadow 控制項在 AJAX Control Toolkit 擴充具有延伸陰影的面板。 不過此陰影有時會與其他控制項，如安裝衝突...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: f56087b1e94653d2a6a06f915191db6ec5e358a2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65116957"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>調整 DropShadow 的 Z 軸索引 (VB)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> DropShadow 控制項在 AJAX Control Toolkit 擴充具有延伸陰影的面板。 不過此陰影與其他控制項，例如 ASP.NET Menu 控制項中有時會發生衝突。 當功能表項目出現，它會出現在下拉式陰影後面。

## <a name="overview"></a>總覽

DropShadow 控制項在 AJAX Control Toolkit 擴充具有延伸陰影的面板。 不過此陰影與其他控制項，例如 ASP.NET Menu 控制項中有時會發生衝突。 當功能表項目出現，它會出現在下拉式陰影後面。

## <a name="steps"></a>步驟

程式碼開始面板本身，包含足夠的文字，使面板包含足夠的文字為可見的效果：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

另一個面板直接之前放置`panelShadow`面板。 它包含具有水平方向的功能表，以便透過出現的功能表項目 (或者： 在)`dropShadow`面板):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

然後，`DropShadowExtender`加入至擴充`panelShadow`面板下拉式陰影效果：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

最後，ASP.NET AJAX`ScriptManager`控制項可讓控制項工具組運作：

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

當您執行此指令碼時，則會在下方面板出現的功能表項目。 不過功能表使用的 CSS 類別`panel`您只需要定義使項目會顯示在 [其他] 面板前面的兩件事：

- 相對位置
- 正 z 軸索引

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

然後，`DropShadowExtender`控制項沒有與此功能表控制項沒事取這麼長衝突。

[![之前：看不到功能表項目](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

之前：看不到功能表項目 ([按一下以檢視完整大小的影像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))

[![之後：在出現的功能表項目](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

之後：功能表項目會出現 ([按一下以檢視完整大小的影像](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))

> [!div class="step-by-step"]
> [上一頁](manipulating-dropshadow-properties-from-client-code-cs.md)
> [下一頁](manipulating-dropshadow-properties-from-client-code-vb.md)
