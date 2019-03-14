---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: 測試密碼強度的 (C#) |Microsoft Docs
author: wenz
description: 因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。 在此 ASP 中 PasswordStrength 控制項。N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: b71744df46f8b8d20efafa333a10370397c37d2f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048405"
---
<a name="testing-the-strength-of-a-password-c"></a>測試密碼強度 (C#)
====================
藉由[Christian Wenz](https://github.com/wenz)

[下載程式碼](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip)或[下載 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> 因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。 PasswordStrength 控制項在 ASP.NET AJAX Control Toolkit 可以檢查是好的密碼。


## <a name="overview"></a>總覽

因此，延遲使用者通常會選擇簡單的密碼，也就是輕而易舉地突破，則幾乎任何地方，需要密碼。 `PasswordStrength` ASP.NET AJAX Control Toolkit 中的控制項可以檢查是好的密碼。

## <a name="steps"></a>步驟

`PasswordStrength`擴充文字方塊控制項，並檢查密碼是否夠好。 它提供豐富的屬性，透過的選項以下是只是某些：

- `MinimumNumericCharacters` 密碼所需的數字字元的最小數目
- `MinimumSymbolCharacters` 密碼所需的符號字元 （不字母和數字） 最小的數目
- `PreferredPasswordLength` 最小密碼長度
- `RequiresUpperAndLowerCaseCharacters` 密碼是否必須使用大寫和小寫字元

`StrengthIndicatorType`提供的資訊如何呈現的強度的密碼，以文字 (值`"Text"`) 或為類型的進度列 (值`"BarIndicator"`)。 在 `DisplayPosition`屬性，您將設定資訊出現的位置。 以下是完整的範例，包括 ASP.NET AJAX`ScriptManager`控制項，`PasswordStrength`控制項，當然還有使用者可以在其中輸入密碼 文字方塊。 為了示範，後者的表單欄位是規則的文字欄位並不是密碼欄位，讓您可以查看在開發期間您輸入的內容。

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

執行此頁面，並立即輸入：只輸入小寫字母、 大寫字母、 數字和符號之後，密碼已被視為為永不中斷。


[![現在是 （挺） 好用的密碼](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

現在，密碼是 （挺） 好用的 ([按一下以檢視完整大小的影像](testing-the-strength-of-a-password-cs/_static/image3.png))

> [!div class="step-by-step"]
> [下一步](testing-the-strength-of-a-password-vb.md)
