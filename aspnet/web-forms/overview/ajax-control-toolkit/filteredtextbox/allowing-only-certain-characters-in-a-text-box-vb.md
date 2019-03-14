---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: 只允許特定字元在文字方塊中 (VB) |Microsoft Docs
author: wenz
description: ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。 不過這仍無法防止使用者輸入不正確...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: aec5a3af98cf40e460f4164fb8950e8029002937
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028545"
---
<a name="allowing-only-certain-characters-in-a-text-box-vb"></a>文字方塊中只允許特定字元 (VB)
====================
藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip)或[下載 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。 不過這仍不會防止使用者輸入無效的字元，並嘗試送出表單。


## <a name="overview"></a>總覽

ASP.NET 驗證控制項可以確保只有特定字元允許在使用者輸入。 不過這仍不會防止使用者輸入無效的字元，並嘗試送出表單。

## <a name="steps"></a>步驟

ASP.NET AJAX Control Toolkit 包含`FilteredTextBox`擴充文字方塊控制項。 一旦啟動後，只有特定的一組字元可能會輸入欄位。

針對此目的，我們必須先如往常般 ASP.NET AJAX`ScriptManager`載入也會由 ASP.NET AJAX Control Toolkit 中的 JavaScript 程式庫：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

然後，我們需要在文字方塊中：

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

最後，`FilteredTextBoxExtender`控制項負責限制允許使用者輸入的字元。 首先，設定`TargetControlID`屬性設定為`ID`的`TextBox`控制項。 然後，選擇其中一個可用`FilterType`值：

- `Custom` 預設值;您必須提供一份有效的字元
- `LowercaseLetters` 只有小寫字母
- `Numbers` 只有數字
- `UppercaseLetters` 大寫英文字母

如果`Custom FilterType`使用時，`ValidChars`屬性必須設定，並提供一份可能輸入的字元。 順便一提： 如果您嘗試將文字貼到文字方塊中，會移除所有無效的字元。

以下是標記`FilteredTextBoxExtender`只允許數字的控制項 (也會使用的項目`FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

執行頁面並嘗試輸入字母，如果已啟用 JavaScript，它將無法運作;數字，不過會出現在頁面上。 不過請注意，保護`FilteredTextBox`提供不是項目符號的使用期限：如果已啟用 JavaScript，任何資料可能會在文字方塊中輸入，因此您必須使用額外的驗證方法，也就是 ASP。NET 的驗證控制項。


[![可能會輸入只有數字](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

可能會輸入只有數字 ([按一下以檢視完整大小的影像](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))

> [!div class="step-by-step"]
> [上一步](allowing-only-certain-characters-in-a-text-box-cs.md)
