---
title: 在 ASP.NET Core 中使用 LoggerMessage 進行高效能記錄
author: guardrex
description: 了解如何使用 LoggerMessage 來建立可快取的委派，其對於高效能記錄案例需要較少的物件配置。
ms.author: riande
ms.date: 11/03/2017
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: a0080a20fed2d8fc295e55822c11d5731c6910ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048615"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a>在 ASP.NET Core 中使用 LoggerMessage 進行高效能記錄

作者：[Luke Latham](https://github.com/guardrex)

[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 功能會建立可快取的委派，比起[記錄器擴充方法](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions) (例如 `LogInformation`、`LogDebug` 和 `LogError`)，其需要的物件配置較少且計算額外負荷較小。 對於高效能記錄的案例，請使用 `LoggerMessage` 模式。

相較於記錄器擴充方法，`LoggerMessage` 提供下列效能優勢：

* 記錄器擴充方法需要 "boxing" (轉換) 實值型別，例如將 `int` 轉換為 `object`。 `LoggerMessage` 模式可使用靜態 `Action` 欄位和擴充方法搭配強型別參數來避免 boxing。
* 記錄器擴充方法在每次寫入記錄訊息時，都必須剖析訊息範本 (具名格式字串)。 `LoggerMessage` 只需在定義訊息時剖析範本一次。

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

範例應用程式以一個基本引述追蹤系統示範 `LoggerMessage` 功能。 該應用程式使用記憶體內部資料庫來新增和刪除引述。 在進行這些作業時，將會使用 `LoggerMessage` 模式來產生記錄訊息。

## <a name="loggermessagedefine"></a>LoggerMessage.Define

[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) 建立記錄訊息的 `Action` 委派。 `Define` 多載允許最多將六個型別參數傳遞至具名格式字串 (範本)。

提供給 `Define` 方法的字串是範本，而不是內插字串。 預留位置會依照指定類型的順序填入。 範本中的預留位置名稱應該是描述性名稱，而且在範本之間應該保持一致。 它們將作為結構化記錄資料內的屬性名稱。 建議您針對預留位置名稱使用 [Pascal 大小寫](/dotnet/standard/design-guidelines/capitalization-conventions)。 例如，`{Count}`、`{FirstName}`。

每個記錄訊息都是 `LoggerMessage.Define` 所建立之靜態欄位中保存的 `Action`。 例如，範例應用程式會建立一個欄位來描述 Index 頁面之 GET 要求的記錄訊息 (*Internal/LoggerExtensions.cs*)：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

針對 `Action`，請指定：

* 記錄層級。
* 含有靜態擴充方法名稱的唯一事件識別碼 ([EventId](/dotnet/api/microsoft.extensions.logging.eventid))。
* 訊息範本 (具名格式字串)。 

範例應用程式之 Index 頁面的要求會：

* 將記錄層級設定為 `Information`。
* 將事件識別碼設定為含有 `IndexPageRequested` 方法名稱的 `1`。
* 將訊息範本 (具名格式字串) 設定為字串。

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

結構化的記錄存放區提供事件識別碼來加強記錄時，可以使用事件名稱。 例如，[Serilog](https://github.com/serilog/serilog-extensions-logging) 會使用事件名稱。

`Action` 是透過強型別擴充方法叫用。 `IndexPageRequested` 方法會在範例應用程式中針對 Index 頁面的 GET 要求記錄一則訊息：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested` 會在 *Pages/Index.cshtml.cs* 中 `OnGetAsync` 方法的記錄器上呼叫：

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

檢查應用程式的主控台輸出：

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

若要將參數傳遞至記錄訊息，請在建立靜態欄位時定義最多六個型別。 透過為 `Action` 欄位定義 `string` 類型來新增引述時，範例應用程式會記錄字串：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

委派的記錄訊息範本會從所提供的類型接收其預留位置值。 範例應用程式會定義新增引述的委派，其中的引述參數是 `string`：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

新增引述的靜態擴充方法 `QuoteAdded` 會接引述引數值，並將其傳遞至 `Action` 委派：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

在 Index 頁面的頁面模型 (*Pages/Index.cshtml.cs*) 中，會呼叫 `QuoteAdded` 來記錄訊息：

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

檢查應用程式的主控台輸出：

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

範例應用程式會實作用於刪除引述的 `try`&ndash;`catch` 模式。 成功的刪除作業會記錄告知性訊息。 如果擲回例外狀況，則會針對刪除作業記錄一則錯誤訊息。 失敗刪除作業的記錄訊息包含例外狀況堆疊追蹤 (*Internal/LoggerExtensions.cs*)：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

請注意例外狀況如何傳遞至 `QuoteDeleteFailed` 中的委派：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

在 Index 頁面的頁面模型中，成功的引述刪除會在記錄器上呼叫 `QuoteDeleted` 方法。 找不到要刪除的引述時，就會擲回 `ArgumentNullException`。 例外狀況是由 `try` &ndash; `catch` 陳述式加以攔截，並透過在 `catch` 區塊的記錄器上呼叫 `QuoteDeleteFailed` 方法來進行記錄 (*Pages/Index.cshtml.cs*)：

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

成功刪除引述時，請檢查應用程式的主控台輸出：

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

引述刪除失敗時，請檢查應用程式的主控台輸出。 請注意，例外狀況會包含在記錄訊息中：

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a>LoggerMessage.DefineScope

[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 建立定義[記錄範圍](xref:fundamentals/logging/index#log-scopes)的 `Func` 委派。 `DefineScope` 多載允許最多將三個型別參數傳遞至具名格式字串 (範本)。

就像 `Define` 方法的情況一樣，提供給 `DefineScope` 方法的字串是範本，而不是內插字串。 預留位置會依照指定類型的順序填入。 範本中的預留位置名稱應該是描述性名稱，而且在範本之間應該保持一致。 它們將作為結構化記錄資料內的屬性名稱。 建議您針對預留位置名稱使用 [Pascal 大小寫](/dotnet/standard/design-guidelines/capitalization-conventions)。 例如，`{Count}`、`{FirstName}`。

使用 [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 方法，定義要套用至一系列記錄訊息的[記錄範圍](xref:fundamentals/logging/index#log-scopes)。

範例應用程式具有 [全部清除] 按鈕，可用來刪除資料庫中的所有引述。 也可透過逐一移除引述來刪除它們。 每次刪除引述時，就會在記錄器上呼叫 `QuoteDeleted` 方法。 記錄範圍會新增至這些記錄訊息。

在 *appsettings.json* 的主控台記錄器區段中啟用 `IncludeScopes`：

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

若要建立記錄範圍，請新增欄位以保留該範圍的 `Func` 委派。 範例應用程式會建立稱為 `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*) 的欄位：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

請使用 `DefineScope` 來建立委派。 叫用委派時，最多可以指定三種類型作為範本引數。 範例應用程式會使用包含已刪除引述數目 (`int` 類型) 的訊息範本：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

提供記錄訊息的靜態擴充方法。 包含訊息範本中出現之具名屬性的任何型別參數。 範例應用程式會帶入要刪除之引述的 `count`，然後傳回 `_allQuotesDeletedScope`：

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

此範圍會將記錄擴充呼叫包裝在 `using` 區塊中：

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

檢查應用程式主控台輸出中的記錄訊息。 下列結果顯示包含記錄範圍訊息的三個刪除引述：

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="additional-resources"></a>其他資源

* [記錄](xref:fundamentals/logging/index)
