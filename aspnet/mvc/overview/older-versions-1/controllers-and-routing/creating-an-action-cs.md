---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 建立操作 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何向ASP.NET MVC 控制器添加新操作。 瞭解方法為操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c1edfbab41afa58c7cb2c0d306995e9fe491c90
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542270"
---
# <a name="creating-an-action-c"></a>建立動作 (C#)

由[微軟](https://github.com/microsoft)

> 瞭解如何向ASP.NET MVC 控制器添加新操作。 瞭解方法為操作的要求。

本教學的目的是解釋如何創建新的控制器操作。 瞭解操作方法的要求。 您還學習如何防止方法作為操作公開。

## <a name="adding-an-action-to-a-controller"></a>新增控制器

通過將新方法添加到控制器,向控制器添加新操作。 例如,清單 1 中的控制器包含名為 Index() 的操作和名為 SayHello() 的操作。 這兩種方法都公開為操作。

**清單1 - 控制器\主控制器.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

為了作為一種行動暴露在宇宙中,一種方法必須滿足某些要求:

- 該方法必須為公共。
- 該方法不能是靜態方法。
- 該方法不能是擴充方法。
- 該方法不能是構造函數、getter 或 setter。
- 該方法不能具有打開的泛型類型。
- 該方法不是控制器基類的方法。
- 該方法不能包含**ref**或**out**參數。

請注意,對控制器操作的返回類型沒有限制。 控制器操作可以返回字串、DateTime、Random 類的實例或 void。 ASP.NET MVC 框架將任何不是操作結果的傳回類型轉換為字串,並將字串呈現給瀏覽器。

將不違反這些要求的任何方法添加到控制器時,該方法將作為控制器操作公開。 這裡要小心。 連接到 Internet 的任何人都可以調用控制器操作。 例如,不要創建"刪除My網站"控制器操作。

## <a name="preventing-a-public-method-from-being-invoked"></a>防止呼叫公共方法

如果需要在控制器類中創建公共方法,並且不希望將該方法公開為控制器操作,則可以通過使用 [NonAction] 屬性阻止調用該方法。 例如,清單 2 中的控制器包含一種名為"公司機密()"的公共方法,該方法使用 [非操作] 屬性進行修飾。

**清單2 - 控制器_工作控制器.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

如果您嘗試透過在瀏覽器的位址列中鍵入 /Work/公司機密來呼叫公司機密() 控制器操作,則會收到圖 1 中的錯誤訊息。

[![呼叫非操作方法](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**圖 01**:呼叫非操作方法([按下以檢視全尺寸影像](creating-an-action-cs/_static/image2.png))

> [!div class="step-by-step"]
> [前一個](creating-a-controller-cs.md)
> [下一個](asp-net-mvc-routing-overview-vb.md)
