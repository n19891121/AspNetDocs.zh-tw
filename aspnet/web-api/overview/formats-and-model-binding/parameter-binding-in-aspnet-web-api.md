---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API 中的參數系結-ASP.NET 4。x
author: MikeWasson
description: 描述 Web API 如何系結參數，以及如何在 ASP.NET 4.x 中自訂系結程式。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: da79a01b8493d489aced016d46e228b7f8186127
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105256"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API 中的參數系結

由 [Mike Wasson](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

本文說明 Web API 系結參數的方式，以及如何自訂系結程式。 當 Web API 在控制器上呼叫方法時，它必須設定參數的值，也就 *是稱為系* 結的進程。

根據預設，Web API 會使用下列規則來系結參數：

- 如果參數是「簡單」類型，Web API 會嘗試從 URI 取得值。 簡單類型 [包括 .net 基本型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) 別 (**int**、 **bool**、 **double** 等等) ，加上 **TimeSpan**、 **DateTime**、 **Guid**、 **decimal** 和 **string**，以及可從字串轉換之類型轉換子 *的任何類型* 。 稍後 (詳細資訊類型轉換器。 ) 
- 針對複雜類型，Web API 會使用 [媒體類型格式](media-formatters.md)器，嘗試從訊息主體讀取值。

例如，以下是一般 Web API 控制器方法：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*Id* 參數是 &quot; 簡單 &quot; 類型，因此 Web API 會嘗試從要求 URI 取得值。 *Item* 參數是複雜類型，因此，Web API 會使用媒體類型格式器來讀取要求本文中的值。

為了從 URI 取得值，Web API 會查看路由資料和 URI 查詢字串。 當路由系統剖析 URI 並將其與路由相符時，就會填入路由資料。 如需詳細資訊，請參閱 [路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。

在本文的其餘部分，我將示範如何自訂模型系結程式。 但是針對複雜類型，請考慮盡可能使用媒體類型格式器。 HTTP 的主要原則是在訊息本文中傳送資源，並使用內容協商來指定資源的標記法。 媒體類型格式器專為此目的而設計。

## <a name="using-fromuri"></a>使用 [FromUri]

若要強制 Web API 從 URI 讀取複雜型別，請將 **[FromUri]** 屬性加入至參數。 下列範例 `GeoPoint` 會定義型別，以及可從 URI 取得的控制器方法 `GeoPoint` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

用戶端可以將緯度和經度值放在查詢字串中，而 Web API 會使用它們來建立 `GeoPoint` 。 例如：

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>使用 [FromBody]

若要強制 Web API 從要求主體讀取簡單類型，請將 **[FromBody]** 屬性新增至參數：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

在此範例中，Web API 會使用媒體類型格式器來讀取要求主體中的 *名稱* 值。 以下是範例用戶端要求。

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

當參數具有 [FromBody] 時，Web API 會使用 Content-type 標頭來選取格式器。 在此範例中，內容類型為 &quot; application/json &quot; ，而且要求主體是原始的 json 字串， (不是) 的 json 物件。

最多可以有一個參數從訊息主體讀取。 這樣就無法運作：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

這項規則的原因是要求主體可能儲存在只能讀取一次的非緩衝資料流程中。

## <a name="type-converters"></a>類型轉換器

您可以建立一個 **TypeConverter** 並提供字串轉換，讓 web api 將某個類別視為簡單類型 (如此一來，web api 就會嘗試從 URI) 系結它。

下列程式碼顯示 `GeoPoint` 表示地理點的類別，以及從字串轉換成實例的 **TypeConverter** `GeoPoint` 。 `GeoPoint`類別是以 **[TypeConverter]** 屬性裝飾，以指定類型轉換子。  (此範例是由 Mike 延遲的 blog 文章所啟發， [說明如何在 MVC/WebAPI 中系結至動作簽章中的自訂物件](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)。 ) 

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

現在 Web API 會視為 `GeoPoint` 簡單類型，這表示它會嘗試 `GeoPoint` 從 URI 系結參數。 您不需要在參數上包含 **[FromUri]** 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

用戶端可以使用如下的 URI 來叫用方法：

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>模型繫結器

比型別轉換子更有彈性的選項，就是建立自訂模型系結器。 使用模型系結器，您就可以存取來自路由資料的 HTTP 要求、動作描述和原始值等專案。

若要建立模型系結器，請執行 **IModelBinder** 介面。 此介面會定義單一方法 **BindModel**：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

以下是物件的模型系結器 `GeoPoint` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

模型系結器會從 *值提供者* 取得原始輸入值。 此設計會將兩個不同的功能分開：

- 值提供者會接受 HTTP 要求，並填入索引鍵/值組的字典。
- 模型系結器會使用此字典來填入模型。

Web API 中的預設值提供者會從路由資料和查詢字串中取得值。 例如，如果 URI 為 `http://localhost/api/values/1?location=48,-122` ，則值提供者會建立下列索引鍵/值組：

- 識別碼 = &quot; 1&quot;
- 位置 = &quot; 48、-122&quot;

 (我假設預設的路由範本，也就是 &quot; api/{controller}/{id} &quot; 。 ) 

要系結的參數名稱會儲存在 **ModelBindingCoNtext. ModelName** 屬性中。 模型系結器會在字典中尋找具有此值的索引鍵。 如果該值存在，而且可以轉換成，則模型系結器會將系結 `GeoPoint` 值指派給 **ModelBindingCoNtext 模型** 屬性。

請注意，模型系結器不限於簡單的類型轉換。 在此範例中，模型系結器會先查看已知位置的資料表，如果失敗，則會使用類型轉換。

**設定模型系結器**

有幾種方式可以設定模型系結器。 首先，您可以將 **[ModelBinder]** 屬性加入至參數。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

您也可以將 **[ModelBinder]** 屬性加入至類型。 Web API 會針對該類型的所有參數使用指定的模型系結器。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

最後，您可以將模型系結器提供者加入至 **HttpConfiguration**。 模型系結器提供者只是建立模型系結器的 factory 類別。 您可以藉由衍生自 [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) 類別來建立提供者。 但是，如果您的模型系結器會處理單一型別，則使用內建的 **SimpleModelBinderProvider** 會更容易使用，這是專為此用途所設計。 下列程式碼示範如何執行這項操作。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

使用模型系結提供者時，您仍然必須將 **[ModelBinder]** 屬性加入至參數，以告知 Web API 應該使用模型系結器，而不是媒體類型格式器。 但現在您不需要在屬性中指定模型系結器的類型：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>值提供者

我曾說過，模型系結器會從值提供者取得值。 若要撰寫自訂值提供者，請執行 **IValueProvider** 介面。 以下是從要求中的 cookie 提取值的範例：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

您也需要從 **ValueProviderFactory** 類別衍生，以建立值提供者 factory。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

將值提供者 factory 新增至 **HttpConfiguration** ，如下所示。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 會撰寫所有值提供者，因此當模型系結器呼叫 **ValueProvider** 時，模型系結器會接收第一個可產生它的值提供者的值。

或者，您可以使用 **ValueProvider** 屬性，在參數層級設定值提供者 factory，如下所示：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

這會告知 Web API 使用具有指定之值提供者 factory 的模型系結，而不使用任何其他已註冊的值提供者。

## <a name="httpparameterbinding"></a>HttpParameterBinding

模型系結器是更一般機制的特定實例。 如果您查看 **[ModelBinder]** 屬性，就會看到它衍生自抽象的 **ParameterBindingAttribute** 類別。 這個類別會定義單一方法 **getbindingexpression**，它會傳回 **HttpParameterBinding** 物件：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

**HttpParameterBinding** 負責將參數系結至值。 在 **[ModelBinder]** 的案例中，屬性會傳回使用 **IModelBinder** 來執行實際系結的 **HttpParameterBinding** 執行。 您也可以執行自己的 **HttpParameterBinding**。

例如，假設您想要從 `if-match` 要求中取得 etag 和 `if-none-match` 標頭。 我們一開始會先定義類別來代表 Etag。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

我們也會定義列舉來指出是否要從 `if-match` 標頭或 `if-none-match` 標頭取得 ETag。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

以下是從所需標頭取得 ETag 的 **HttpParameterBinding** ，並將其系結至 etag 類型的參數：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**ExecuteBindingAsync** 方法會執行系結。 在這個方法中，將系結參數值加入至 **HttpActionCoNtext** 中的 **ActionArgument** 字典。

> [!NOTE]
> 如果您的 **ExecuteBindingAsync** 方法會讀取要求訊息的本文，請覆寫 **WillReadBody** 屬性以傳回 true。 要求主體可能是未緩衝的資料流程，但只能讀取一次，因此 Web API 會強制執行一個規則，其中最多隻能有一個系結可讀取訊息主體。

若要套用自訂 **HttpParameterBinding**，您可以定義衍生自 **ParameterBindingAttribute** 的屬性。 針對 `ETagParameterBinding` ，我們會定義兩個屬性，一個用於 `if-match` 標頭，另一個用於 `if-none-match` 標頭。 兩者都衍生自抽象基類。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

以下是使用屬性的控制器方法 `[IfNoneMatch]` 。

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

除了 **ParameterBindingAttribute** 之外，還有另一個用來新增自訂 **HttpParameterBinding** 的勾點。 在 **HttpConfiguration** 物件上， **ParameterBindingRules** 屬性是類型 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**) 的匿名函式集合。 例如，您可以加入規則，讓 GET 方法上的任何 ETag 參數使用 `ETagParameterBinding` `if-none-match` ：

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

函數應該針對系結 `null` 不適用的參數傳回。

## <a name="iactionvaluebinder"></a>IActionValueBinder

整個參數系結程式是由插即用服務（ **IActionValueBinder**）所控制。 **IActionValueBinder** 的預設執行會執行下列動作：

1. 尋找參數上的 **ParameterBindingAttribute** 。 這包括 **[FromBody]**、 **[FromUri]** 和 **[ModelBinder]**，或自訂屬性。
2. 否則，請針對傳回非 null **HttpParameterBinding** 的函式查看 **HttpConfiguration. ParameterBindingRules** 。
3. 否則，請使用我先前所述的預設規則。 

    - 如果參數類型為 "simple" 或具有類型轉換器，請從 URI 系結。 這相當於在參數上放置 **[FromUri]** 屬性。
    - 否則，請嘗試從訊息主體讀取參數。 這相當於在參數上放置 **[FromBody]** 。

如果您想要的話，可以使用自訂的實作為來取代整個 **IActionValueBinder** 服務。

## <a name="additional-resources"></a>其他資源

[自訂參數系結範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Mike 停止撰寫了一系列有關 Web API 參數系結的良好 blog 文章：

- [Web API 如何進行參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API 的 MVC 樣式參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [如何在 MVC/Web API 中系結至動作簽章中的自訂物件](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [如何在 Web API 中建立自訂值提供者](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [本質上的 Web API 參數系結](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
