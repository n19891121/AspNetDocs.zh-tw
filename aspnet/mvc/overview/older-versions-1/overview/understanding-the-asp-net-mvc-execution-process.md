---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 瞭解ASP.NET MVC 執行流程 |微軟文件
author: rick-anderson
description: 瞭解ASP.NET MVC 框架如何逐步處理瀏覽器請求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 48afbbe7349b80e0ed0b9bab987ae3ccda493aca
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541022"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a>了解 ASP.NET MVC 執行程序

由[微軟](https://github.com/microsoft)

> 瞭解ASP.NET MVC 框架如何逐步處理瀏覽器請求。

對基於ASP.NET MVC 的 Web 應用程式的請求首先透過**UrlRoutingModule**物件,該物件是一個 HTTP 模組。 此模組會剖析該要求並執行路由選取。 **UrlRoutingModule**物件選擇與當前請求匹配的第一個路由物件。 (路由對像是實現**RouteBase**的類,通常是**路由**類的實例。如果沒有路由匹配 **,UrlRoutingModule**物件將不執行任何操作,並讓請求回退到常規ASP.NET或 IIS 請求處理。

從選取的**路由**物件中 **,UrlRouteModule**物件獲取與**路由**物件關聯的**IRouteHandler**物件。 通常,在 MVC 應用程式中,這將是**MvcRouteHandler**的實例。 **IRouteHandler**實例創建一個**IHTTPHandler**物件,並將其傳遞給**IHttpContext**物件。 默認情況下,MVC 的**IHTTPHandler**實例是**MvcHandler**物件。 **然後,MvcHandler**物件選擇最終將處理請求的控制器。

> [!NOTE]
> 當 ASP.NET MVC Web 應用程式在 IIS 7.0 中執行時，MVC 專案不需要副檔名。 然而，在 IIS 6.0 中，處理常式需要您將 .mvc 副檔名對應至 ASP.NET ISAPI DLL。

模組和處理程式是 mVC 框架 ASP.NET 的入口點。 它們會執行下列動作：

- 選取 MVC Web 應用程式中適當的控制器。
- 取得特定控制器執行個體。
- 呼叫**控制器的執行方法**。

下面列出了 MVC Web 專案的執行階段:

- 接收應用程式的第一個要求 

    - 在 Global.asax 檔中,**路由**物件將添加到**RouteTable**物件。
- 執行路由 

    - **UrlRoutingModule 模組**使用**RouteTable**集合中的第一個匹配**路由**物件來創建**RouteData**物件,然後使用它創建**請求上下文**(**IHTTPContext**) 物件。
- 建立 MVC 要求處理常式 

    - **MvcRouteHandler**物件創建**MvcHandler**類的實例,並將其傳遞給**請求上下文**實例。
- 建立控制器 

    - **MvcHandler**物件使用**RequestContext**實例來識別**IControllerFactory**物件(通常是**默認控制器工廠**類的實例)來使用來創建控制器實例。
- 執行控制器 - **MvcHandler**實體呼叫控制器**的執行方法**。 |
- 叫用動作 

    - 大多數控制器從**控制器**基類繼承。 對於這樣做的控制器,與控制器關聯的**ControllerActionInvoker**物件確定要呼叫的控制器類的操作方法,然後調用該方法。
- 執行結果 

    - 典型的操作方法可能會接收使用者輸入、準備適當的回應數據,然後通過返回結果類型來執行結果。 可以執行的內建結果類型包括 **:ViewResult(** 呈現檢視,是最常用的結果類型,**重定向到路由結果**,**重定向結果**,**內容結果****,JsonResult**和**空結果**。
