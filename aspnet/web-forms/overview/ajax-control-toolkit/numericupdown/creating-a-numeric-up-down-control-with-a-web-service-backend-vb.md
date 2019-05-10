---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 使用 (VB) 的 Web 服務後端建立數值向上/向下控制項 |Microsoft Docs
author: wenz
description: 而不是讓使用者核取方塊中輸入值，數值向上/向下控制項 （也就存在於 Windows 和其他作業系統） 可以證明越多 c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: fffa670134d5b9aa3523603c60accb4e887747c8
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132536"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a><span data-ttu-id="9d4d6-103">使用 Web 服務後端建立數值向上/向下控制項 (VB)</span><span class="sxs-lookup"><span data-stu-id="9d4d6-103">Creating a Numeric Up/Down Control with a Web Service Backend (VB)</span></span>

<span data-ttu-id="9d4d6-104">藉由[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9d4d6-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9d4d6-105">[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="9d4d6-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)</span></span>

> <span data-ttu-id="9d4d6-106">而不是讓使用者核取方塊中輸入值，數值上下按鈕控制項 （也就存在於 Windows 和其他作業系統） 可以證明越多習慣。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="9d4d6-107">根據預設，NumericUpDown 控制項一律會增加或減少值 1，但 web 服務證明更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="overview"></a><span data-ttu-id="9d4d6-108">總覽</span><span class="sxs-lookup"><span data-stu-id="9d4d6-108">Overview</span></span>

<span data-ttu-id="9d4d6-109">而不是讓使用者核取方塊中輸入值，數值上下按鈕控制項 （也就存在於 Windows 和其他作業系統） 可以證明越多習慣。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="9d4d6-110">根據預設，`NumericUpDown`控制項一律會增加或減少值 1，但 web 服務證明更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="9d4d6-111">步驟</span><span class="sxs-lookup"><span data-stu-id="9d4d6-111">Steps</span></span>

<span data-ttu-id="9d4d6-112">ASP.NET AJAX Control Toolkit 包含`NumericUpDown`擴充項會自動將兩個按鈕加入至文字方塊：一個用於增加其價值，一個用於減少。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="9d4d6-113">不過控制項也支援 web 服務呼叫 （或頁面方法呼叫）。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="9d4d6-114">每當向上或向下按鈕按下時的 JavaScript 程式碼會連線到 web 伺服器，並執行的方法。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="9d4d6-115">方法簽章是下列其中一個：</span><span class="sxs-lookup"><span data-stu-id="9d4d6-115">The method signature is the following one:</span></span>

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

<span data-ttu-id="9d4d6-116">`current`引數是在文字方塊中，目前的值`tag`屬性是可設定為屬性的其他內容資料`NumericUpDown`擴充項 （但並非必要）。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="9d4d6-117">此範例中，數值向上/向下控制項都應該只允許 2 乘冪的值：1、 2、 4、 8、 16、 32、 64，依此類推。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="9d4d6-118">因此，當使用者想要增加的值時執行的方法必須兩倍的舊的值;另一種方法必須將值除以兩個。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="9d4d6-119">因此，以下是完整的 web 服務：</span><span class="sxs-lookup"><span data-stu-id="9d4d6-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

<span data-ttu-id="9d4d6-120">最後，建立新的 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="9d4d6-121">像往常一樣，您需要`ScriptManager`控制`TextBox`控制項和`NumericUpDownExtender`控制項。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="9d4d6-122">對於後者，您必須提供 web 服務的資訊：</span><span class="sxs-lookup"><span data-stu-id="9d4d6-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="9d4d6-123">`ServiceDownMethod` web 方法，或頁面方法的清單名稱</span><span class="sxs-lookup"><span data-stu-id="9d4d6-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="9d4d6-124">`ServiceDownPath` 向下的服務方法; web 服務的路徑如果您使用頁面方法，請省略</span><span class="sxs-lookup"><span data-stu-id="9d4d6-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="9d4d6-125">`ServiceUpMethod` 名稱最多的 web 方法，或頁面方法</span><span class="sxs-lookup"><span data-stu-id="9d4d6-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="9d4d6-126">`ServiceUpPath` 最新的服務方法; web 服務的路徑如果您使用頁面方法，請省略</span><span class="sxs-lookup"><span data-stu-id="9d4d6-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="9d4d6-127">以下是完整的標記頁面：</span><span class="sxs-lookup"><span data-stu-id="9d4d6-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

<span data-ttu-id="9d4d6-128">如果您執行頁面時，請注意如何在文字方塊中的值一律會加倍當您按一下上方的按鈕，並當您按一下下方的按鈕減半。</span><span class="sxs-lookup"><span data-stu-id="9d4d6-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>

<span data-ttu-id="9d4d6-129">[![只是 2 的乘冪的數字才會出現](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9d4d6-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)</span></span>

<span data-ttu-id="9d4d6-130">只是 2 的乘冪的數字才會出現 ([按一下以檢視完整大小的影像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9d4d6-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="9d4d6-131">上一步</span><span class="sxs-lookup"><span data-stu-id="9d4d6-131">Previous</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
