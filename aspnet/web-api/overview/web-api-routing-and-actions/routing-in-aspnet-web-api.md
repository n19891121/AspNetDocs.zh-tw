---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |微軟文件
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676129"
---
# <a name="routing-in-aspnet-web-api"></a>ASP.NET Web API 中的路由

由[邁克·瓦森](https://github.com/MikeWasson)

本文介紹ASP.NET Web API 如何將 HTTP 請求路由到控制器。

> [!NOTE]
> 如果您熟悉ASP.NET MVC,則Web API路由與MVC路由非常相似。 主要區別是 Web API 使用 HTTP 謂詞(而不是 URI 路徑)來選擇操作。 您還可以在 Web API 中使用 MVC 樣式路由。 本文不假定任何有關ASP.NET MVC 的知識。

## <a name="routing-tables"></a>路由表

在 Web API ASP.NET,*控制器*是處理 HTTP 請求的類。 控制器的公共方法稱為*管理程式*或簡單的*操作*。 當 Web API 框架收到請求時,它將請求路由到操作。

要決定要呼叫的操作,框架使用*路由表*格 。 Web API 的視覺化工作室專案樣本建立預設路由:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

此路由在*WebApiConfig.cs*檔案中定義,該檔案放置在 *「\_應用開始」* 目錄中:

![](routing-in-aspnet-web-api/_static/image1.png)

有關該類別的詳細資訊,`WebApiConfig`請參考[設定 ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。

如果自承載 Web API,則必須`HttpSelfHostConfiguration`直接在 物件上設置路由表。 有關詳細資訊,請參閱[自主機 Web API](../older-versions/self-host-a-web-api.md)。

路由表中的每個項目都包含*一個路由樣本*。 Web API 的預設路由&quot;範本 是 api/{控制器}/{id}。&quot; 在此範本中&quot;,api&quot;是文字路徑段,[控制器] 和 {id} 是占位符變數。

當 Web API 框架收到 HTTP 請求時,它會嘗試將 URI 與路由表中的路由範本之一匹配。 如果沒有路由匹配,用戶端將收到 404 錯誤。 例如,以下 URI 與預設路由符合:

- /api/觸點
- /api/觸點/1
- /api/產品/gizmo1

但是,以下 URI 不匹配,因為&quot;它缺少&quot;api 段:

- /觸點/1

> [!NOTE]
> 在路由中使用「api」的原因是為了避免與ASP.NET MVC 路由發生衝突。 這樣&quot;,您可以讓 /&quot;聯繫人 轉到 MVC 控制器&quot;,/api/ 聯繫人&quot;轉到 Web API 控制器。 當然,如果您不喜歡此約定,則可以更改預設路由表。

找到符合路由後,Web API 將選擇控制器和操作:

- 要查找控制器,Web&quot;API&quot;將控制器添加到 *[控制器]* 變數的值。
- 要查找操作,Web API 將查看 HTTP 謂詞,然後查找名稱以該 HTTP 謂詞名稱開頭的操作。 例如,對於 GET 請求&quot;,Web API 會&quot;查找使用&quot;Get&quot;預&quot;置的操作&quot;,例如獲取 連絡人或獲取 所有連絡人。 此約定僅適用於 GET、POST、PUT、DELETE、頭、選項和 PATCH 謂詞。 您可以使用控制器上的屬性啟用其他 HTTP 謂詞。 稍後我們將看到示例。
- 製程路線樣本中的其他占位符變數(如 *{id})* 映射到操作參數。

讓我們看看以下範例。 假設您定義以下控制器:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

下面是一些可能的 HTTP 請求,以及為每個請求呼叫的操作:

| HTTP 指令動詞 | URI 路徑 | 動作 | 參數 |
| --- | --- | --- | --- |
| GET | api/產品 | 取得所有產品 | *(無)* |
| GET | api/產品/4 | 取得產品 ById | 4 |
| 刪除 | api/產品/4 | 移除產品 | 4 |
| POST | api/產品 | *( 不符合 )* |  |

請注意,URI 的 *[id]* 段(如果存在)映射到操作的*id*參數。 在此示例中,控制器定義了兩個 GET 方法,一個使用*id*參數,另一個沒有參數。

此外,請注意,POST 請求將失敗,因為控制器未&quot;定義 Post...&quot;方法。

## <a name="routing-variations"></a>路由變體

上一節介紹了ASP.NET Web API 的基本路由機制。 本節介紹一些變體。

### <a name="http-verbs"></a>HTTP 動詞

無需對 HTTP 謂詞使用命名約定,還可以通過使用以下屬性之一來修飾操作方法之一,顯式指定操作的 HTTP 謂詞:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

在下面的範例中,`FindProduct`該方法映射到 GET 請求:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

要允許多個 HTTP 謂詞用於某個操作,或允許除 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP`[AcceptVerbs]`謂詞,請使用該屬性,該屬性採用 HTTP 謂詞的清單。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>依操作名稱路由

使用預設路由範本,Web API 使用 HTTP 謂詞選擇操作。 但是,您還可以創建一個路由,其中操作名稱包含在 URI 中:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

在此路由範本中 *,[操作]* 參數在控制器上命名操作方法。 使用此路由樣式,使用屬性指定允許的 HTTP 謂詞。 例如,假設您的控制器具有以下方法:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

在這種情況下,GET 請求的"api/產品/詳細資訊/1"將映射`Details`到 該方法。 這種路由樣式類似於 mVC ASP.NET,可能適用於 RPC 樣式的 API。

可以使用 屬性重寫操作`[ActionName]`名稱 。 在下面的範例中,有兩個操作映射到&quot;api/產品/縮略圖/*id*。一個支援 GET,另一個支援 POST:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>非操作

要防止將方法作為操作呼叫,請使用`[NonAction]`屬性 。 這向框架發出信號,說明該方法不是操作,即使它以其他方式與路由規則匹配也是如此。

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>進階閱讀

本主題提供了路由的高級視圖。 有關詳細資訊,請參閱[路由和操作選擇](routing-and-action-selection.md),它準確描述框架如何將 URI 與路由匹配,選擇控制器,然後選擇要調用的操作。
