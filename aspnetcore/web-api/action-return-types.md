---
title: ASP.NET Core Web API 中的控制器動作傳回型別
author: scottaddie
description: 了解在 ASP.NET Core Web API 中使用各種控制器動作方法傳回型別。
ms.author: scaddie
ms.custom: mvc
ms.date: 01/04/2019
uid: web-api/action-return-types
ms.openlocfilehash: 98d70e0379d353cff98a6d7a13f2dd00eb4da206
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047495"
---
# <a name="controller-action-return-types-in-aspnet-core-web-api"></a>ASP.NET Core Web API 中的控制器動作傳回型別

作者：[Scott Addie](https://github.com/scottaddie)

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/web-api/action-return-types/samples) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

ASP.NET Core 提供下列 Web API 控制器動作傳回型別選項：

::: moniker range=">= aspnetcore-2.1"

* [特定類型](#specific-type)
* [IActionResult](#iactionresult-type)
* [ActionResult\<T>](#actionresultt-type)

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* [特定類型](#specific-type)
* [IActionResult](#iactionresult-type)

::: moniker-end

本文件說明使用每個傳回型別的最適時機。

## <a name="specific-type"></a>特定類型

最簡單的動作傳回基本或複雜的資料類型 (例如，`string` 或自訂物件類型)。 請考慮下列動作，它會傳回自訂 `Product` 物件的集合：

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_Get)]

無已知條件，無法確保在動作執行期間能滿足傳回特定類型。 上述動作不接受任何參數，因此不需要驗證參數條件約束。

當動作需要計入已知情況時，會引入多個傳回路徑。 在此情況下，通常會混合 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 傳回型別和基本或複雜的傳回型別。 [IActionResult](#iactionresult-type) 或 [ActionResult\<T>](#actionresultt-type) 是容納此動作類型的必要項目。

## <a name="iactionresult-type"></a>IActionResult 類型

當動作中可能有多個 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 傳回型別時，適合使用 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult) 傳回型別。 `ActionResult` 類型代表各種 HTTP 狀態碼。 某些落在這個類別的常見傳回型別是 [BadRequestResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestresult) (400)、[NotFoundResult](/dotnet/api/microsoft.aspnetcore.mvc.notfoundresult) (404) 和 [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult) (200)。

因為動作中有多個傳回型別和路徑，所以有必要隨意使用 [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute.-ctor) 屬性。 此屬性會產生由 [Swagger](/aspnet/core/tutorials/web-api-help-pages-using-swagger) 等工具所產生之 API 說明頁面的更具體描述回應詳細資料。 `[ProducesResponseType]` 表示已知類型和 HTTP 狀態碼要由動作傳回。

### <a name="synchronous-action"></a>同步動作

請考慮下列有兩個可能傳回型別的同步動作：

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

在上述動作中，當基礎資料存放區中無 `id` 所代表的產品時，會傳回 404 狀態碼。 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) helper 方法會當成 `return new NotFoundResult();` 的捷徑叫用。 如果產品不存在，就會傳回代表承載的 `Product` 物件，狀態碼為 200。 [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) 協助程式方法會當成 `return new OkObjectResult(product);` 的縮寫形式叫用。

### <a name="asynchronous-action"></a>非同步動作

請考慮下列有兩個可能傳回型別的同步動作：

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.Pre21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

在上述程式碼中：

* 當產品描述包含 "XYZ Widget" 時，ASP.NET Core 執行階段會傳回 400 狀態碼 ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*))。
* 當建立產品時，[CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) 方法會產生 201 狀態碼。 在此程式碼路徑中，會傳回 `Product` 物件。

例如，下列模型指出要求必須包含 `Name` 和 `Description` 屬性。 因此，若無法在要求中提供 `Name` 和 `Description`，就會導致模型驗證失敗。

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.DataAccess/Models/Product.cs?name=snippet_ProductClass&highlight=5-6,8-9)]

::: moniker range=">= aspnetcore-2.1"

如果套用 ASP.NET Core 2.1 或更新版本中的 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 屬性，則模型驗證錯誤會導致產生 400 狀態碼。 如需詳細資訊，請參閱[自動 HTTP 400 回應](xref:web-api/index#automatic-http-400-responses)。

## <a name="actionresultt-type"></a>ActionResult\<T> 類型

ASP.NET Core 2.1 為 Web API 控制器動作引入了 [ActionResult\<T>](/dotnet/api/microsoft.aspnetcore.mvc.actionresult-1) 傳回型別。 它可讓您傳回衍生自 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult) 的類型或傳回[特定類型](#specific-type)。 `ActionResult<T>` 透過 [IActionResult 類型](#iactionresult-type)提供下列優點：

* [[ProducesResponseType]](/dotnet/api/microsoft.aspnetcore.mvc.producesresponsetypeattribute) 屬性的 `Type` 屬性可被排除。 例如，`[ProducesResponseType(200, Type = typeof(Product))]` 簡化為 `[ProducesResponseType(200)]`。 該動作的預期傳回型別會改為從 `ActionResult<T>` 中的 `T` 推斷。
* [隱含轉型運算子](/dotnet/csharp/language-reference/keywords/implicit)支援 `T` 和 `ActionResult` 轉換成 `ActionResult<T>`。 `T` 轉換成 [ObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.objectresult)，這表示 `return new ObjectResult(T);` 已簡化成 `return T;`。

C# 不支援介面上的隱含轉換運算子。 因此，必須將介面轉換為具象型別才能使用 `ActionResult<T>`。 例如，在下列範例中使用 `IEnumerable` 將無法運作：

```csharp
[HttpGet]
public ActionResult<IEnumerable<Product>> Get()
{
    return _repository.GetProducts();
}
```

修正上述程式碼的其中一個選項是傳回 `_repository.GetProducts().ToList();`。

大部分的動作都有特定的傳回型別。 如果在動作執行期間發生非預期的狀況，就不會傳回特定的類型。 例如，動作的輸入參數可能無法驗證模型。 在此情況下，通常會傳回適當的 `ActionResult` 類型而不是特定的類型。

### <a name="synchronous-action"></a>同步動作

請考慮有兩個可能傳回型別的同步動作：

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_GetById&highlight=8,11)]

在上述程式碼中，當資料庫中無產品時，會傳回 404 狀態碼。 如果產品不存在，就會傳回對應的 `Product` 物件。 ASP.NET Core 2.1 前的 `return product;` 行可能是 `return Ok(product);`。

> [!TIP]
> 自 ASP.NET Core 2.1 開始，使用 `[ApiController]` 屬性裝飾控制器類別時，會啟用動作參數繫結來源推斷。 使用要求路由資料自動繫結在路由範本中比對名稱的參數名稱。 因此，不會以 [[FromRoute]](/dotnet/api/microsoft.aspnetcore.mvc.fromrouteattribute) 屬性明確標註上述動作的 `id` 參數。

### <a name="asynchronous-action"></a>非同步動作

請考慮有兩個可能傳回型別的非同步動作：

[!code-csharp[](../web-api/action-return-types/samples/WebApiSample.Api.21/Controllers/ProductsController.cs?name=snippet_CreateAsync&highlight=8,13)]

在上述程式碼中：

* 在下列情況下，ASP.NET Core 執行階段會傳回 400 狀態碼 ([BadRequest](xref:Microsoft.AspNetCore.Mvc.ControllerBase.BadRequest*))：
  * 已套用 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 屬性，而模型驗證失敗。
  * 產品描述包含 "XYZ Widget"。
* 當建立產品時，[CreatedAtAction](xref:Microsoft.AspNetCore.Mvc.ControllerBase.CreatedAtAction*) 方法會產生 201 狀態碼。 在此程式碼路徑中，會傳回 `Product` 物件。

> [!TIP]
> 自 ASP.NET Core 2.1 開始，使用 `[ApiController]` 屬性裝飾控制器類別時，會啟用動作參數繫結來源推斷。 複雜類型參數會使用要求本文自動繫結。 因此，不會以 [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 屬性明確標註上述動作的 `product` 參數。

::: moniker-end

## <a name="additional-resources"></a>其他資源

* <xref:mvc/controllers/actions>
* <xref:mvc/models/validation>
* <xref:tutorials/web-api-help-pages-using-swagger>
