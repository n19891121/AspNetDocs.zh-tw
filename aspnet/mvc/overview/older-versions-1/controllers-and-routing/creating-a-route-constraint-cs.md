---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 建立路由條件約束 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會示範如何控制瀏覽器使用規則運算式中建立路由條件約束所要求的相符項目路由。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51d76248a59968e1d6befd5d5404f7bf6c2878e4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049615"
---
<a name="creating-a-route-constraint-c"></a>建立路由條件約束 (C#)
====================
藉由[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 會示範如何控制瀏覽器使用規則運算式中建立路由條件約束所要求的相符項目路由。


您可以使用路由條件約束來限制瀏覽器會要求符合特定的路由。 您可以使用規則運算式來指定路由條件約束。

例如，假設您已定義的路由清單 1 在 Global.asax 檔案中。

**列表 1-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

列表 1 包含名為 Product 的路由。 您可以使用產品路由以將瀏覽器要求對應至 列表 2 中所包含的 ProductController。

**Listing 2 - Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

請注意，Product 控制器所公開的 Details() 動作會接受名為 productId 的單一參數。 這個參數是一個整數參數。

在 列表 1 中定義的路由會符合任何下列 url:

- /Product/23
- /Product/7

不幸的是，路由也會比對下列 Url:

- / 產品/blah
- /Product/apple

由於 Details() 動作預期整數參數，提出要求，其中包含整數值以外的項目會造成錯誤。 比方說，如果您的瀏覽器中輸入 URL /Product/apple 然後就會出現錯誤頁面 [圖 1] 中。


[![[新增專案] 對話方塊](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**圖 01**:看到頁面，explode ([按一下以檢視完整大小的影像](creating-a-route-constraint-cs/_static/image2.png))


您真的要做什麼是只比對包含適當的整數 productId 的 Url。 可以使用條件約束定義的路由時，來限制路由相符的 Url。 修改的產品路由列表 3 中包含的規則運算式條件約束，只會比對整數。

**列表 3-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

規則運算式 \d+ 比對一個或多個整數。 此條件約束會造成產品路由，以符合下列 Url:

- /Product/3
- /Product/8999

但下列 Url:

- /Product/apple
- /Product

- 這些瀏覽器要求交由另一個路由或，如果不有任何相符的路由*找不到資源*便會傳回錯誤。

> [!div class="step-by-step"]
> [上一頁](creating-custom-routes-cs.md)
> [下一頁](creating-a-custom-route-constraint-cs.md)
