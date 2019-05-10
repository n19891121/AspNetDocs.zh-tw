---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
title: 繪製 UpdatePanel 控制項 (C#) 的動畫 |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 內容...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e57f8c7c-3940-4bc0-9468-3a0ca69158ea
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-cs
msc.type: authoredcontent
ms.openlocfilehash: c403cddd1e3eb5b66f795a2e4032fae63fdb26ca
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130737"
---
# <a name="animating-an-updatepanel-control-c"></a>繪製 UpdatePanel 控制項的動畫 (C#)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.cs.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1CS.pdf)

> 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 UpdatePanel 的內容，特殊的擴充項會存在，依賴動畫架構：UpdatePanelAnimation。 本教學課程會示範如何設定這類動畫的 UpdatePanel。

## <a name="overview"></a>總覽

動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 內容`UpdatePanel`，特殊的擴充性已存在，而且依賴動畫架構： `UpdatePanelAnimation`。 本教學課程示範如何設定這類的動畫`UpdatePanel`。

## <a name="steps"></a>步驟

如往常般的第一個步驟是加入`ScriptManager`頁面中，讓 ASP.NET AJAX 程式庫已載入，並控制工具組可以用於：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample1.aspx)]

在此案例中的動畫將會套用到 ASP.NET`Wizard`中的 web 控制項`UpdatePanel`。 （任意） 的三個步驟會提供足夠的選項，以觸發回傳：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample2.aspx)]

所需的標記`UpdatePanelAnimationExtender`控制項是用來標記十分類似`AnimationExtender`。 在 `TargetControlID`我們提供的屬性`ID`的`UpdatePanel`以動畫顯示; 內`UpdatePanelAnimationExtender`控制項，`<Animations>`項目會保存 animation(s) 的 XML 標記。 不過是其中一項差異：事件和事件處理常式的數量僅限於在相`AnimationExtender`。 針對`UpdatePanels`只有兩個，其中存在：

- `<OnUpdated>` 當已更新 UpdatePanel
- `<OnUpdating>` 開始更新 UpdatePanel

在此案例中，新的內容`UpdatePanel`（之後回傳） 應該會淡入。 這是必要的標記：

[!code-aspx[Main](animating-an-updatepanel-control-cs/samples/sample3.aspx)]

現在每次回傳發生時在 UpdatePanel 中，新的內容面板的淡入順暢。

[![下一個步驟中，精靈會淡入](animating-an-updatepanel-control-cs/_static/image2.png)](animating-an-updatepanel-control-cs/_static/image1.png)

下一個步驟中，精靈會淡入 ([按一下以檢視完整大小的影像](animating-an-updatepanel-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [上一頁](changing-an-animation-using-client-side-code-cs.md)
> [下一頁](dynamically-controlling-updatepanel-animations-cs.md)
