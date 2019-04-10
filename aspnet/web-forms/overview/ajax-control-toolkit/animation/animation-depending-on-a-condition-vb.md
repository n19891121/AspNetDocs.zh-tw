---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 依據條件 (VB) 的動畫 |Microsoft Docs
author: wenz
description: 動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。 動畫是否是...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: 78140f56184e88fb4dbe29f234aebd5732b69ad9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418868"
---
# <a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="7edad-104">依據條件的動畫 (VB)</span><span class="sxs-lookup"><span data-stu-id="7edad-104">Animation Depending On a Condition (VB)</span></span>

<span data-ttu-id="7edad-105">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7edad-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7edad-106">[下載程式碼](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip)或[下載 PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7edad-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="7edad-107">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="7edad-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7edad-108">動畫執行時是否也取決於一些 JavaScript 程式碼的表單中的條件。</span><span class="sxs-lookup"><span data-stu-id="7edad-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="7edad-109">總覽</span><span class="sxs-lookup"><span data-stu-id="7edad-109">Overview</span></span>

<span data-ttu-id="7edad-110">動畫控制項在 ASP.NET AJAX Control Toolkit 中不只是控制項，但若要將動畫加入至控制項的整個架構。</span><span class="sxs-lookup"><span data-stu-id="7edad-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7edad-111">動畫執行時是否也取決於一些 JavaScript 程式碼的表單中的條件。</span><span class="sxs-lookup"><span data-stu-id="7edad-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="7edad-112">步驟</span><span class="sxs-lookup"><span data-stu-id="7edad-112">Steps</span></span>

<span data-ttu-id="7edad-113">首先，包括`ScriptManager`單元頁面; 然後，ASP.NET AJAX 程式庫載入，因此能夠使用控制項工具組：</span><span class="sxs-lookup"><span data-stu-id="7edad-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="7edad-114">動畫將會套用至面板的文字看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="7edad-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="7edad-115">在 [面板] 中相關聯的 CSS 類別，定義好用的背景色彩和也設定面板的固定的寬度：</span><span class="sxs-lookup"><span data-stu-id="7edad-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="7edad-116">然後，新增`AnimationExtender` 頁面上，以提供`ID`，則`TargetControlID`屬性和必要</span><span class="sxs-lookup"><span data-stu-id="7edad-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory</span></span> `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="7edad-117">內`<Animations>`節點，請使用`<OnLoad>`頁面完全載入後，執行動畫。</span><span class="sxs-lookup"><span data-stu-id="7edad-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="7edad-118">而不是一個一般的動畫，`<Condition>`元素派上用場。</span><span class="sxs-lookup"><span data-stu-id="7edad-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="7edad-119">提供的值為 JavaScript 程式碼`ConditionScript`屬性會在執行階段執行。</span><span class="sxs-lookup"><span data-stu-id="7edad-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="7edad-120">如果評估為 true，動畫會執行，否則不。</span><span class="sxs-lookup"><span data-stu-id="7edad-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="7edad-121">下列標記會提供兩個動畫，每個正在執行 50%的隨機時的案例。</span><span class="sxs-lookup"><span data-stu-id="7edad-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="7edad-122">因為只能有一張動畫內`<OnLoad>`，這兩個`<Condition>`動畫會聯結在一起使用`<Sequence>`項目：</span><span class="sxs-lookup"><span data-stu-id="7edad-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="7edad-123">請注意，為小於符號 (`<`) 中`ConditionScript`屬性必須逸出 （）。</span><span class="sxs-lookup"><span data-stu-id="7edad-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="7edad-124">當您執行此指令碼，可能是沒有動畫執行時，或兩者的其中一個存在，或兩個的作用。</span><span class="sxs-lookup"><span data-stu-id="7edad-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


[![T<span data-ttu-id="7edad-125">他面板漸淡但不調整大小，因此未在第二個動畫執行後的第一個]</span><span class="sxs-lookup"><span data-stu-id="7edad-125">he panel is fading out without resizing, so the second animation runs, the first one didn't]</span></span>(animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

<span data-ttu-id="7edad-126">面板淡出但不調整大小，因此未在第二個動畫執行後的第一個 ([按一下以檢視完整大小的影像](animation-depending-on-a-condition-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7edad-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7edad-127">[上一頁](executing-several-animations-after-each-other-vb.md)
> [下一頁](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7edad-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
