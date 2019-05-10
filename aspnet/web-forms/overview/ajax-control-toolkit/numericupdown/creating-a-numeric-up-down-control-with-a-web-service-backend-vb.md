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
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>使用 Web 服務後端建立數值向上/向下控制項 (VB)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 而不是讓使用者核取方塊中輸入值，數值上下按鈕控制項 （也就存在於 Windows 和其他作業系統） 可以證明越多習慣。 根據預設，NumericUpDown 控制項一律會增加或減少值 1，但 web 服務證明更大的彈性。

## <a name="overview"></a>總覽

而不是讓使用者核取方塊中輸入值，數值上下按鈕控制項 （也就存在於 Windows 和其他作業系統） 可以證明越多習慣。 根據預設，`NumericUpDown`控制項一律會增加或減少值 1，但 web 服務證明更大的彈性。

## <a name="steps"></a>步驟

ASP.NET AJAX Control Toolkit 包含`NumericUpDown`擴充項會自動將兩個按鈕加入至文字方塊：一個用於增加其價值，一個用於減少。 不過控制項也支援 web 服務呼叫 （或頁面方法呼叫）。 每當向上或向下按鈕按下時的 JavaScript 程式碼會連線到 web 伺服器，並執行的方法。 方法簽章是下列其中一個：

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current`引數是在文字方塊中，目前的值`tag`屬性是可設定為屬性的其他內容資料`NumericUpDown`擴充項 （但並非必要）。

此範例中，數值向上/向下控制項都應該只允許 2 乘冪的值：1、 2、 4、 8、 16、 32、 64，依此類推。 因此，當使用者想要增加的值時執行的方法必須兩倍的舊的值;另一種方法必須將值除以兩個。 因此，以下是完整的 web 服務：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

最後，建立新的 ASP.NET 網頁。 像往常一樣，您需要`ScriptManager`控制`TextBox`控制項和`NumericUpDownExtender`控制項。 對於後者，您必須提供 web 服務的資訊：

- `ServiceDownMethod` web 方法，或頁面方法的清單名稱
- `ServiceDownPath` 向下的服務方法; web 服務的路徑如果您使用頁面方法，請省略
- `ServiceUpMethod` 名稱最多的 web 方法，或頁面方法
- `ServiceUpPath` 最新的服務方法; web 服務的路徑如果您使用頁面方法，請省略

以下是完整的標記頁面：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

如果您執行頁面時，請注意如何在文字方塊中的值一律會加倍當您按一下上方的按鈕，並當您按一下下方的按鈕減半。

[![只是 2 的乘冪的數字才會出現](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

只是 2 的乘冪的數字才會出現 ([按一下以檢視完整大小的影像](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一步](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
