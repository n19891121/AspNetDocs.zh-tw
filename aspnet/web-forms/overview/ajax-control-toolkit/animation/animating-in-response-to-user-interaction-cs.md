---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 以動畫顯示以回應使用者互動 (C#) |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫可以星級...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: c0e2888207e4fa0363fc3b357ae00108ffe817f5
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415215"
---
# <a name="animating-in-response-to-user-interaction-c"></a>根據使用者互動繪製動畫 (C#)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫可以自動啟動，或可能會觸發使用者互動，例如按一下滑鼠。


## <a name="overview"></a>總覽

動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫可以自動啟動，或可能會觸發使用者互動，例如按一下滑鼠。

## <a name="steps"></a>步驟

首先，包括`ScriptManager`單元頁面; 然後，ASP.NET AJAX 程式庫載入，因此能夠使用控制項工具組：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

動畫將會套用至面板的文字看起來像這樣：

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

在 [面板] 中相關聯的 CSS 類別，定義好用的背景色彩和也設定面板的固定的寬度：

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

然後，新增`AnimationExtender` 頁面上，以提供`ID`，則`TargetControlID`屬性和必要`runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

內`<Animations>`節點，有五種方式可以開始透過使用者互動的動畫 (遺漏的項目是`<OnLoad>`來執行整個頁面完全載入後):

- `<OnClick>` （滑鼠按一下控制項）
- `<OnHoverOut>` （滑鼠離開控制項）
- `<OnHoverOver>` (滑鼠停留在控制項，停止`<OnHoverOut>`動畫)
- `<OnMouseOut>` （滑鼠離開控制項）
- `<OnMouseOver>` (滑鼠停留在控制項，不會 」 停止`<OnMouseOut>`動畫)

在此案例中，`<OnClick>`用。 當使用者按一下 [面板] 中時，它會重新調整大小，並在同一時間淡出。

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]


[![A 按下滑鼠開始動畫](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

按下滑鼠開始動畫 ([按一下以檢視完整大小的影像](animating-in-response-to-user-interaction-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一頁](picking-one-animation-out-of-a-list-cs.md)
> [下一頁](disabling-actions-during-animation-cs.md)
