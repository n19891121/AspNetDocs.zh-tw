---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: 定位 ModalPopup (VB) |Microsoft Docs
author: wenz
description: AJAX Control Toolkit 之 ModalPopup 控制項提供簡單的方式來建立使用用戶端表示強制回應快顯。 控制項不提供的不過...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: d5cfcd2ff8956b54f241ee7002aa00a0bd47469e
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65132648"
---
# <a name="positioning-a-modalpopup-vb"></a>定位 ModalPopup (VB)

藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> AJAX Control Toolkit 之 ModalPopup 控制項提供簡單的方式來建立使用用戶端表示強制回應快顯。 但是控制項不提供內建的功能，可以定位快顯視窗。

## <a name="overview"></a>總覽

AJAX Control Toolkit 之 ModalPopup 控制項提供簡單的方式來建立使用用戶端表示強制回應快顯。 但是控制項不提供內建的功能，可以定位快顯視窗。

## <a name="steps"></a>步驟

若要啟動的 ASP.NET AJAX Control Toolkit 中，功能`ScriptManager`。 控制項必須放置在任何位置上 (但在`<form>`項目):

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

接下來，加入做為強制回應快顯面板。 按鈕來關閉快顯視窗：

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

每當在快顯視窗會顯示，它應該會位於網頁的特定位置。 這項工作，會建立用戶端的 JavaScript 函式。 它會先嘗試存取面板。 如果成功，面板的位置會設定使用 CSS 和 JavaScript （在快顯視窗的位置會的變更）。 不過，`ModalPopupExtender`控制項也會嘗試快顯視窗的位置。 因此，JavaScript 程式碼重複將的快顯視窗中，而每個十分之一秒。

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

如您所見的傳回值`setTimeout()`JavaScript 方法儲存在全域變數。 若要停止重複的定位快顯視窗，視情況下，這可讓使用`clearTimeout()`方法：

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

現在剩下要執行的是讓瀏覽器呼叫在情況允許時，這些函式。 `movePanel()`觸發程序 [面板] 中，按一下此按鈕時，就必須呼叫 JavaScript 函式：

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

而`stopMoving()`函式派上用場時快顯視窗已關閉，這可能會觸發在`ModalPopupExtender`控制項：

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

[![強制回應快顯視窗會出現在指定的位置](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

強制回應快顯視窗會出現在指定的位置 ([按一下以檢視完整大小的影像](positioning-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一步](handling-postbacks-from-a-modalpopup-vb.md)
