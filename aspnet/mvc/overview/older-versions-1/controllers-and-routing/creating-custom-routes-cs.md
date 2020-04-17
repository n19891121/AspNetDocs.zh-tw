---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 建立自定義路由 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何向ASP.NET MVC 應用程式添加自定義路由。 在本教學中,您將瞭解如何修改 Global.asax 檔中的預設路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: b66ccc5e0cd4f6d7e5884394c2b7555b76382d3d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542751"
---
# <a name="creating-custom-routes-c"></a>建立自訂路由 (C#)

由[微軟](https://github.com/microsoft)

> 瞭解如何向ASP.NET MVC 應用程式添加自定義路由。 在本教學中,您將瞭解如何修改 Global.asax 檔中的預設路由表。

在本教學中,您將瞭解如何向ASP.NET MVC 應用程式添加自定義路由。 您將瞭解如何使用自訂路由修改 Global.asax 檔中的預設路由表。

對於許多簡單的ASP.NET MVC 應用程式,預設路由表將工作正常。 但是,您可能會發現您有專門的路由需求。 在這種情況下,您可以創建自定義路由。

例如,假設您正在構建一個博客應用程式。 您可能需要處理以下所示的傳入請求:

/存檔/12-25-2009

當使用者輸入此請求時,您希望返回與日期 12/25/2009 對應的博客條目。 為了處理這種類型的請求,您需要創建自定義路由。

清單1中的 Global.asax 檔包含名為 Blog 的新自訂路由,它處理看起來像 /存檔/*條目日期*的請求。

**清單 1 - 全域.asax(含自訂路由)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

添加到工藝路線表的路由的順序很重要。 我們新的自定義博客路由在現有預設路由之前添加。 如果顛倒了訂單,則預設路由將始終被調用,而不是自定義路由。

自定義博客路由匹配以 /存檔/開頭的任何請求。 因此,它與以下網址匹配:

- /存檔/12-25-2009

- /存檔/10-6-2004

- /存檔/蘋果

自定義路由將傳入請求映射到名為「存檔」的控制器,並調用 Entry() 操作。 調用 entry() 方法時,條目日期將作為名為 entryDate 的參數傳遞。

您可以將博客自定義路由與清單 2 中的控制器一起使用。

**清單2 - ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

請注意,清單 2 中的 entry() 方法接受 DateTime 類型的參數。 MVC 框架足夠智慧,可以自動將 URL 的輸入日期轉換為 DateTime 值。 如果 URL 中的輸入日期參數無法轉換為 DateTime,則引發錯誤(參見圖 1)。

**圖 1 - 轉換參數時發生錯誤**

[![[New Project] \(新增專案\) 對話方塊](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**圖 01**: 轉換參數時發生錯誤 ([按下以檢視全尺寸影像](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>總結

本教學的目的是示範如何創建自定義路由。 您學習了如何在表示部落格條目的 Global.asax 檔中向路由表添加自訂路由。 我們討論了如何將部落格條目的請求映射到名為 ArchiveController 的控制器和名為 entry() 的控制器操作。

> [!div class="step-by-step"]
> [前一個](aspnet-mvc-controllers-overview-cs.md)
> [下一個](creating-a-route-constraint-cs.md)
