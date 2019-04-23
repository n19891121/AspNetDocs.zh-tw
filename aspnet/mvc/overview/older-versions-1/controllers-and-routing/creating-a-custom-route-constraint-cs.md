---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: 建立自訂的路由條件約束 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會示範如何建立自訂路由條件約束。 我們會實作簡單的自訂條件約束可以防止路由比對 w...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 5d8a40b03a1997904a2736a339dbf6b4003ae7bd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59410639"
---
# <a name="creating-a-custom-route-constraint-c"></a>建立自訂的路由條件約束 (C#)

藉由[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 會示範如何建立自訂路由條件約束。 我們會實作簡單的自訂條件約束，可防止瀏覽器要求從遠端電腦時要比對路由。


本教學課程的目的在於示範如何建立自訂路由條件約束。 自訂路由條件約束可讓您防止某些自訂的條件會比對，除非符合路由。

在本教學課程中，我們會建立 Localhost 的路由條件約束。 Localhost 路由條件約束只會比對從本機電腦所提出的要求。 從遠端在網際網路上的要求不符。

您可以實作 IRouteConstraint 介面，以實作自訂路由條件約束。 這是非常簡單的介面描述單一方法：

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

方法會傳回布林值。 如果傳回 false，則含有條件約束相關聯的路由不會符合瀏覽器要求。

列表 1 中包含的 Localhost 條件約束。

**列表 1-LocalhostConstraint.cs**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

列表 1 中的條件約束會利用 HttpRequest 類別所公開的 IsLocal 屬性。 當要求的 IP 位址是任一 127.0.0.1 或要求的 IP 是伺服器的 IP 位址相同，則這個屬性會傳回 true。

您使用自訂的條件約束內 Global.asax 檔案中定義的路由。 列表 2 中的 Global.asax 檔會使用 Localhost 條件約束，防止任何人要求系統管理員 頁面，除非它們從本機伺服器提出要求。 例如，從遠端伺服器時，將會失敗 /Admin/DeleteAll 的要求。

**Listing 2 - Global.asax**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

管理路由的定義所用的 Localhost 條件約束。 此路由不會比對遠端瀏覽器要求。 不過，要注意的是，其他 Global.asax 中所定義的路由可能會符合相同的要求。 請務必了解條件約束可防止特定路由相符的要求，而且並非所有的路由定義於 Global.asax 檔案。

請注意，預設路由具有已標記為註解列表 2 中的 Global.asax 檔中。 如果您包含預設路由時，預設路由會比對系統管理員控制站的要求。 在此情況下，遠端使用者可能仍然叫用動作的系統管理控制站即使其要求不符合管理路由。

> [!div class="step-by-step"]
> [上一頁](creating-a-route-constraint-cs.md)
> [下一頁](asp-net-mvc-controller-overview-vb.md)
