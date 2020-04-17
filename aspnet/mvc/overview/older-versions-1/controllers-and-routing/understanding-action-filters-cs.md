---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 瞭解操作篩選器 (C#) |微軟文件
author: rick-anderson
description: 本教學的目的是解釋操作篩選器。 操作篩選器是屬性,您可以套用控制器操作或整個控制器...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 75ba7b1dce280a45cd092de97c464eade5f49838
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542179"
---
# <a name="understanding-action-filters-c"></a>了解動作篩選 (C#)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 本教學的目的是解釋操作篩選器。 操作篩選器是一個屬性,您可以應用於控制器操作(或整個控制器),該屬性修改操作的執行方式。

## <a name="understanding-action-filters"></a>瞭解操作篩選器

本教學的目的是解釋操作篩選器。 操作篩選器是一個屬性,您可以應用於控制器操作(或整個控制器),該屬性修改操作的執行方式。 ASP.NET MVC 框架包括多個操作篩選器:

- 輸出快取 - 此操作篩選器快取控制器操作的輸出,以指定的時間進行。
- 句柄錯誤 - 此操作篩選器處理執行控制器操作時引發的錯誤。
- 授權 – 此操作篩選器使您能夠限制對特定使用者或角色的訪問。

您還可以創建自己的自定義操作篩選器。 例如,您可能希望創建自定義操作篩選器以實現自定義身份驗證系統。 或者,您可能希望創建一個操作篩選器,用於修改控制器操作返回的檢視數據。

在本教學中,您將瞭解如何從開始構建操作篩選器。 我們創建一個 Log 操作篩選器,將操作處理的不同階段記錄到可視化工作室輸出視窗。

### <a name="using-an-action-filter"></a>使用操作篩選器

操作篩選器是屬性。 您可以將大多數操作篩選器應用於單個控制器操作或整個控制器。

例如,清單 1 中的數據控制器`Index()`公開名為 返回當前時間的操作。 此操作使用`OutputCache`操作篩選器進行修飾。 此篩選器會導致將操作返回的值緩存 10 秒。

**清單1 |`Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

如果透過網址/`Index()`資料/索引輸入瀏覽器的位址列並多次點擊「刷新」按鈕來重複呼叫該操作,則您將在 10 秒內看到相同的時間。 操作的`Index()`輸出緩存 10 秒(參見圖 1)。

[![快取時間](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**圖 01**: 快取時間 ([按下以檢視全尺寸影像](understanding-action-filters-cs/_static/image3.png))

在清單 1 中,單個操作`OutputCache`篩選器 (操作篩選器`Index()`)應用於 該方法。 如果需要,可以將多個操作篩選器應用於同一操作。 例如,您可能希望將和`OutputCache``HandleError`操作篩選器應用於同一操作。

在清單`OutputCache`1 中,操作篩選器套`Index()`用於操作 。 您還可以將此屬性應用於`DataController`類本身。 在這種情況下,控制器公開的任何操作返回的結果將被緩存 10 秒。

### <a name="the-different-types-of-filters"></a>不同類型的過濾器

ASP.NET MVC 框架支援四種不同類型的篩選器:

1. 授權篩選器 =`IAuthorizationFilter`實現 屬性。
2. 操作篩選器 =`IActionFilter`實現 屬性。
3. 結果篩選器 =`IResultFilter`實現 屬性。
4. 異常篩選器 =`IExceptionFilter`實現 屬性。

篩選器按上面列出的順序執行。 例如,授權篩選器始終在操作篩選器和異常篩選器始終在每一種其他類型的篩選器之後執行。

授權篩選器用於實現控制器操作的身份驗證和授權。 例如,"授權"篩選器是授權篩選器的範例。

操作篩選器包含在控制器操作執行之前和之後執行的邏輯。 例如,可以使用操作篩選器修改控制器操作返回的檢視數據。

結果篩選器包含在執行檢視結果之前和之後執行的邏輯。 例如,您可能希望在檢視呈現給瀏覽器之前修改視圖結果。

異常篩選器是要運行的最後一種篩選器類型。 可以使用異常篩選器來處理控制器操作或控制器操作結果引發的錯誤。 您還可以使用異常篩選器來記錄錯誤。

每種不同類型的篩選器都按特定順序執行。 如果要控制執行相同類型的篩選器的順序,則可以設置篩選器的 Order 屬性。

所有操作篩選器的基類別是類別`System.Web.Mvc.FilterAttribute`。 如果要實現特定類型的篩選器,則需要創建從基本篩選器類繼承的類,並實現一個或多個`IAuthorizationFilter`、`IActionFilter`或`IResultFilter``IExceptionFilter`介面。

### <a name="the-base-actionfilterattribute-class"></a>基本操作篩選器屬性類別

為了更輕鬆地實現自定義操作篩選器,ASP.NET MVC 框架`ActionFilterAttribute`包括一個基本類。 此類實現`IActionFilter``IResultFilter`和介面並`Filter`從 類繼承。

此處的術語並不完全一致。 從技術上講,從 ActionFilterAttribute 類繼承的類既是操作篩選器,也是結果篩選器。 但是,在鬆散的意義上,單詞操作篩選器用於引用 mVC 框架中的任何類型的篩選器ASP.NET。

基`ActionFilterAttribute`類別有您可以重寫的以下方法:

- OnAction 執行 – 在執行控制器操作之前呼叫此方法。
- 執行執行時 ─ 在執行控制器操作後呼叫此方法。
- OnResult 執行 – 在執行控制器操作結果之前呼叫此方法。
- OnResult 執行 - 在執行控制器操作結果後呼叫此方法。

在下一節中,我們將瞭解如何實現每種不同方法。

### <a name="creating-a-log-action-filter"></a>建立紀錄操作篩選器

為了說明如何構建自定義操作篩選器,我們將創建一個自定義操作篩選器,將處理控制器操作的各個階段記錄到 Visual Studio 輸出視窗。 我們的`LogActionFilter`包含在清單2中。

**清單2 |`ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

在清單`OnActionExecuting()`2`OnActionExecuted()``OnResultExecuting()``OnResultExecuted()`中 ,、、`Log()`和 方法都 調用 方法。 方法的名稱與目前路由資料會傳遞給方法`Log()`。 該方法`Log()`將消息寫入可視化工作室輸出視窗(參見圖 2)。

[![寫入視覺化工作室輸出視窗](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**圖 02**: 寫入視覺化工作室輸出視窗 ([按下以檢視全尺寸影像](understanding-action-filters-cs/_static/image6.png))

清單3中的主控制器說明了如何將 Log 操作篩選器應用於整個控制器類。 每當呼叫主控制器公開的任何操作(`Index()`方法或`About()`方法),處理操作的各個階段都會記錄到 Visual Studio 輸出視窗。

**清單3 |`Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>總結

在本教學中,您將被介紹到ASP.NET MVC 操作篩選器。 您瞭解了四種不同類型的篩選器:授權篩選器、操作篩選器、結果篩選器和異常篩選器。 您還瞭解了基`ActionFilterAttribute`類。

最後,您學習了如何實現簡單的操作篩選器。 我們創建了一個 Log 操作篩選器,將處理控制器操作的各個階段記錄到可視化工作室輸出視窗。

> [!div class="step-by-step"]
> [前一個](asp-net-mvc-routing-overview-cs.md)
> [下一個](improving-performance-with-output-caching-cs.md)
