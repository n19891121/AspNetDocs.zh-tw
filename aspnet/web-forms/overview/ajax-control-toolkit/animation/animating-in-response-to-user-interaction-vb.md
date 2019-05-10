---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 以動畫顯示以回應使用者互動 (VB) |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫可以星級...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: fa774eecd872e79e3b05f6a6ebe177be895b8191
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65112918"
---
# <a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="985a2-104">根據使用者互動繪製動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="985a2-104">Animating in Response To User Interaction (VB)</span></span>

<span data-ttu-id="985a2-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="985a2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="985a2-106">[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="985a2-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="985a2-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="985a2-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="985a2-108">動畫可以自動啟動，或可能會觸發使用者互動，例如按一下滑鼠。</span><span class="sxs-lookup"><span data-stu-id="985a2-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="overview"></a><span data-ttu-id="985a2-109">總覽</span><span class="sxs-lookup"><span data-stu-id="985a2-109">Overview</span></span>

<span data-ttu-id="985a2-110">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="985a2-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="985a2-111">動畫可以自動啟動，或可能會觸發使用者互動，例如按一下滑鼠。</span><span class="sxs-lookup"><span data-stu-id="985a2-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="985a2-112">步驟</span><span class="sxs-lookup"><span data-stu-id="985a2-112">Steps</span></span>

<span data-ttu-id="985a2-113">首先，包括`ScriptManager`單元頁面; 然後，ASP.NET AJAX 程式庫載入，因此能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="985a2-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="985a2-114">動畫將會套用至面板的文字看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="985a2-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="985a2-115">在 [面板] 中相關聯的 CSS 類別，定義好用的背景色彩和也設定面板的固定的寬度：</span><span class="sxs-lookup"><span data-stu-id="985a2-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="985a2-116">然後，新增`AnimationExtender` 頁面上，以提供`ID`，則`TargetControlID`屬性和必要`runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="985a2-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="985a2-117">內`<Animations>`節點，有五種方式可以開始透過使用者互動的動畫 (遺漏的項目是`<OnLoad>`來執行整個頁面完全載入後):</span><span class="sxs-lookup"><span data-stu-id="985a2-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="985a2-118">`<OnClick>` （滑鼠按一下控制項）</span><span class="sxs-lookup"><span data-stu-id="985a2-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="985a2-119">`<OnHoverOut>` （滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="985a2-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="985a2-120">`<OnHoverOver>` (滑鼠停留在控制項，停止`<OnHoverOut>`動畫)</span><span class="sxs-lookup"><span data-stu-id="985a2-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="985a2-121">`<OnMouseOut>` （滑鼠離開控制項）</span><span class="sxs-lookup"><span data-stu-id="985a2-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="985a2-122">`<OnMouseOver>` (滑鼠停留在控制項，不會 」 停止`<OnMouseOut>`動畫)</span><span class="sxs-lookup"><span data-stu-id="985a2-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="985a2-123">在此案例中，`<OnClick>`用。</span><span class="sxs-lookup"><span data-stu-id="985a2-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="985a2-124">當使用者按一下 [面板] 中時，它會重新調整大小，並在同一時間淡出。</span><span class="sxs-lookup"><span data-stu-id="985a2-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

<span data-ttu-id="985a2-125">[![按下滑鼠開始動畫](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="985a2-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="985a2-126">按下滑鼠開始動畫 ([按一下以檢視完整大小的影像](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="985a2-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="985a2-127">[上一頁](picking-one-animation-out-of-a-list-vb.md)
> [下一頁](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="985a2-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
