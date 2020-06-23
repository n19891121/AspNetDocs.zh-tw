---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2 中的單元測試控制器 |Microsoft Docs
author: MikeWasson
description: 本主題描述 Web API 2 中的單元測試控制器的一些特定技術。 閱讀本主題之前，您可能會想要閱讀教學課程單元 .。。
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: ee933cfc736a07b91c8f7feea2c4a2c64d200942
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240648"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的單元測試控制器

由[Mike Wasson](https://github.com/MikeWasson)

> 本主題描述 Web API 2 中的單元測試控制器的一些特定技術。 閱讀本主題之前，您可能會想要閱讀教學課程[單元測試 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，其中顯示如何將單元測試專案加入至您的方案。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> 我使用 Moq，但相同的想法適用于任何模擬架構。 Moq 4.5.30 （和更新版本）支援 Visual Studio 2017、Roslyn 和 .NET 4.5 及更新版本。

單元測試中的常見模式是 &quot; 排列-act-assert &quot; ：

- 排列：設定要執行測試的任何必要條件。
- Act：執行測試。
- 判斷提示：確認測試是否成功。

在 [排列] 步驟中，您通常會使用 mock 或 stub 物件。 這麼做可將相依性的數目降至最低，因此測試著重于測試一件事。

以下是您應該在 Web API 控制器中進行單元測試的一些事項：

- 動作會傳回正確的回應類型。
- 不正確參數傳回正確的錯誤回應。
- 動作會呼叫儲存機制或服務層級上的正確方法。
- 如果回應包含領域模型，請確認模型類型。

這些都是要測試的一般事項，但細節取決於您的控制器的執行。 特別的是，不論您的控制器動作會傳回**HttpResponseMessage**或**應傳回 iHTTPactionresult**，都有很大的差異。 如需這些結果類型的詳細資訊，請參閱[Web Api 2 中的動作結果](../getting-started-with-aspnet-web-api/action-results.md)。

## <a name="testing-actions-that-return-httpresponsemessage"></a>測試傳回 HttpResponseMessage 的動作

以下是其動作會傳回**HttpResponseMessage**的控制器範例。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

請注意，控制器會使用相依性插入來插入 `IProductRepository` 。 這可讓控制器更具測試性，因為您可以插入模擬存放庫。 下列單元測試會驗證方法是否將 `Get` 寫入 `Product` 至回應主體。 假設 `repository` 是 mock `IProductRepository` 。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

請務必在**控制器上設定****要求**和設定。 否則，測試將會失敗，並出現**system.argumentnullexception**或**InvalidOperationException**。

## <a name="testing-link-generation"></a>測試連結產生

`Post`方法會呼叫**UrlHelper** ，以在回應中建立連結。 在單元測試中，這需要進行一些設定：

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**UrlHelper**類別需要要求 URL 和路由資料，因此測試必須設定這些的值。 另一個選項是 mock 或存根**UrlHelper**。 使用這種方法，您可以將[ApiController](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx)的預設值取代為會傳回固定值的模擬或存根版本。

讓我們使用[Moq](https://github.com/Moq)架構來重寫測試。 `Moq`在測試專案中安裝 NuGet 套件。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

在此版本中，您不需要設定任何路由資料，因為 mock **UrlHelper**會傳回常數位串。

## <a name="testing-actions-that-return-ihttpactionresult"></a>測試傳回應傳回 iHTTPactionresult 的動作

在 Web API 2 中，控制器動作可以傳回**應傳回 iHTTPactionresult**，類似于 ASP.NET MVC 中的**ActionResult** 。 **應傳回 iHTTPactionresult**介面會定義用來建立 HTTP 回應的命令模式。 控制器不會直接建立回應，而是會傳回**應傳回 iHTTPactionresult**。 之後，管線會叫用**應傳回 iHTTPactionresult**來建立回應。 這種方法可讓您更輕鬆地撰寫單元測試，因為您可以略過**HttpResponseMessage**所需的許多設定。

以下是範例控制器，其動作會傳回**應傳回 iHTTPactionresult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

這個範例會顯示一些使用**應傳回 iHTTPactionresult**的常見模式。 讓我們來瞭解如何對其進行單元測試。

### <a name="action-returns-200-ok-with-a-response-body"></a>動作會傳回200（確定）與回應主體

`Get` `Ok(product)` 如果找到產品，方法會呼叫。 在單元測試中，請確定傳回類型為**OkNegotiatedContentResult** ，而傳回的產品具有正確的識別碼。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

請注意，單元測試不會執行動作結果。 您可以假設動作結果會正確地建立 HTTP 回應。 （這就是為什麼 Web API 架構有自己的單元測試！）

### <a name="action-returns-404-not-found"></a>動作傳回404（找不到）

`Get` `NotFound()` 如果找不到產品，方法會呼叫。 在此情況下，單元測試只會檢查傳回型別是否為**NotFoundResult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>動作會傳回200（確定），而不會傳迴響應主體

`Delete`方法會呼叫 `Ok()` 以傳回空的 HTTP 200 回應。 如同上述範例，單元測試會檢查傳回類型，在此案例中為**OkResult**。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>動作會傳回201（已建立）與位置標頭

`Post`方法會呼叫 `CreatedAtRoute` ，以在 Location 標頭中傳回具有 URI 的 HTTP 201 回應。 在單元測試中，確認動作是否已設定正確的路由值。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>動作會傳回另一個具有回應主體的2xx

`Put`方法會呼叫 `Content` ，以傳回包含回應主體的 HTTP 202 （接受）回應。 這種情況類似于傳回200（OK），但是單元測試也應該檢查狀態碼。

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>其他資源

- [單元測試 ASP.NET Web API 2 時的模擬 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [撰寫 ASP.NET Web API 服務的測試](https://docs.microsoft.com/archive/blogs/youssefm/writing-tests-for-an-asp-net-web-api-service)（Youssef Moussaoui 的 blog 文章）。
- [使用 Route Debugger 進行 ASP.NET Web API 偵錯](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
