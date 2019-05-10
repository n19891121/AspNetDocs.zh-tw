---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: 繪製 UpdatePanel 控制項 (VB) 的動畫 |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 內容...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: b44dfd284ac1ed94e92bd52f4ca426a36bf86825
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130752"
---
# <a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="620e1-104">繪製 UpdatePanel 控制項的動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="620e1-104">Animating an UpdatePanel Control (VB)</span></span>

<span data-ttu-id="620e1-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="620e1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="620e1-106">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="620e1-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="620e1-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="620e1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="620e1-108">UpdatePanel 的內容，特殊的擴充項會存在，依賴動畫架構：UpdatePanelAnimation。</span><span class="sxs-lookup"><span data-stu-id="620e1-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="620e1-109">本教學課程會示範如何設定這類動畫的 UpdatePanel。</span><span class="sxs-lookup"><span data-stu-id="620e1-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>

## <a name="overview"></a><span data-ttu-id="620e1-110">總覽</span><span class="sxs-lookup"><span data-stu-id="620e1-110">Overview</span></span>

<span data-ttu-id="620e1-111">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="620e1-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="620e1-112">內容`UpdatePanel`，特殊的擴充性已存在，而且依賴動畫架構： `UpdatePanelAnimation`。</span><span class="sxs-lookup"><span data-stu-id="620e1-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="620e1-113">本教學課程示範如何設定這類的動畫`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="620e1-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="620e1-114">步驟</span><span class="sxs-lookup"><span data-stu-id="620e1-114">Steps</span></span>

<span data-ttu-id="620e1-115">如往常般的第一個步驟是加入`ScriptManager`頁面中，讓 ASP.NET AJAX 程式庫已載入，並控制工具組可以用於：</span><span class="sxs-lookup"><span data-stu-id="620e1-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="620e1-116">在此案例中的動畫將會套用到 ASP.NET`Wizard`中的 web 控制項`UpdatePanel`。</span><span class="sxs-lookup"><span data-stu-id="620e1-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="620e1-117">（任意） 的三個步驟會提供足夠的選項，以觸發回傳：</span><span class="sxs-lookup"><span data-stu-id="620e1-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="620e1-118">所需的標記`UpdatePanelAnimationExtender`控制項是用來標記十分類似`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="620e1-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="620e1-119">在 `TargetControlID`我們提供的屬性`ID`的`UpdatePanel`以動畫顯示; 內`UpdatePanelAnimationExtender`控制項，`<Animations>`項目會保存 animation(s) 的 XML 標記。</span><span class="sxs-lookup"><span data-stu-id="620e1-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="620e1-120">不過是其中一項差異：事件和事件處理常式的數量僅限於在相`AnimationExtender`。</span><span class="sxs-lookup"><span data-stu-id="620e1-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="620e1-121">針對`UpdatePanels`只有兩個，其中存在：</span><span class="sxs-lookup"><span data-stu-id="620e1-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="620e1-122">`<OnUpdated>` 當已更新 UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="620e1-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="620e1-123">`<OnUpdating>` 開始更新 UpdatePanel</span><span class="sxs-lookup"><span data-stu-id="620e1-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="620e1-124">在此案例中，新的內容`UpdatePanel`（之後回傳） 應該會淡入。</span><span class="sxs-lookup"><span data-stu-id="620e1-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="620e1-125">這是必要的標記：</span><span class="sxs-lookup"><span data-stu-id="620e1-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="620e1-126">現在每次回傳發生時在 UpdatePanel 中，新的內容面板的淡入順暢。</span><span class="sxs-lookup"><span data-stu-id="620e1-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>

<span data-ttu-id="620e1-127">[![下一個步驟中，精靈會淡入](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="620e1-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="620e1-128">下一個步驟中，精靈會淡入 ([按一下以檢視完整大小的影像](animating-an-updatepanel-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="620e1-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="620e1-129">[上一頁](changing-an-animation-using-client-side-code-vb.md)
> [下一頁](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="620e1-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
