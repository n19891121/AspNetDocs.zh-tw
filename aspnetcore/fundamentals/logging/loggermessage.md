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
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a><span data-ttu-id="c8a86-103">在 ASP.NET Core 中使用 LoggerMessage 進行高效能記錄</span><span class="sxs-lookup"><span data-stu-id="c8a86-103">High-performance logging with LoggerMessage in ASP.NET Core</span></span>

<span data-ttu-id="c8a86-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="c8a86-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="c8a86-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 功能會建立可快取的委派，比起[記錄器擴充方法](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions) (例如 `LogInformation`、`LogDebug` 和 `LogError`)，其需要的物件配置較少且計算額外負荷較小。</span><span class="sxs-lookup"><span data-stu-id="c8a86-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) features create cacheable delegates that require fewer object allocations and reduced computational overhead compared to [logger extension methods](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), such as `LogInformation`, `LogDebug`, and `LogError`.</span></span> <span data-ttu-id="c8a86-106">對於高效能記錄的案例，請使用 `LoggerMessage` 模式。</span><span class="sxs-lookup"><span data-stu-id="c8a86-106">For high-performance logging scenarios, use the `LoggerMessage` pattern.</span></span>

<span data-ttu-id="c8a86-107">相較於記錄器擴充方法，`LoggerMessage` 提供下列效能優勢：</span><span class="sxs-lookup"><span data-stu-id="c8a86-107">`LoggerMessage` provides the following performance advantages over Logger extension methods:</span></span>

* <span data-ttu-id="c8a86-108">記錄器擴充方法需要 "boxing" (轉換) 實值型別，例如將 `int` 轉換為 `object`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-108">Logger extension methods require "boxing" (converting) value types, such as `int`, into `object`.</span></span> <span data-ttu-id="c8a86-109">`LoggerMessage` 模式可使用靜態 `Action` 欄位和擴充方法搭配強型別參數來避免 boxing。</span><span class="sxs-lookup"><span data-stu-id="c8a86-109">The `LoggerMessage` pattern avoids boxing by using static `Action` fields and extension methods with strongly-typed parameters.</span></span>
* <span data-ttu-id="c8a86-110">記錄器擴充方法在每次寫入記錄訊息時，都必須剖析訊息範本 (具名格式字串)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-110">Logger extension methods must parse the message template (named format string) every time a log message is written.</span></span> <span data-ttu-id="c8a86-111">`LoggerMessage` 只需在定義訊息時剖析範本一次。</span><span class="sxs-lookup"><span data-stu-id="c8a86-111">`LoggerMessage` only requires parsing a template once when the message is defined.</span></span>

<span data-ttu-id="c8a86-112">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="c8a86-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="c8a86-113">範例應用程式以一個基本引述追蹤系統示範 `LoggerMessage` 功能。</span><span class="sxs-lookup"><span data-stu-id="c8a86-113">The sample app demonstrates `LoggerMessage` features with a basic quote tracking system.</span></span> <span data-ttu-id="c8a86-114">該應用程式使用記憶體內部資料庫來新增和刪除引述。</span><span class="sxs-lookup"><span data-stu-id="c8a86-114">The app adds and deletes quotes using an in-memory database.</span></span> <span data-ttu-id="c8a86-115">在進行這些作業時，將會使用 `LoggerMessage` 模式來產生記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="c8a86-115">As these operations occur, log messages are generated using the `LoggerMessage` pattern.</span></span>

## <a name="loggermessagedefine"></a><span data-ttu-id="c8a86-116">LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="c8a86-116">LoggerMessage.Define</span></span>

<span data-ttu-id="c8a86-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) 建立記錄訊息的 `Action` 委派。</span><span class="sxs-lookup"><span data-stu-id="c8a86-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) creates an `Action` delegate for logging a message.</span></span> <span data-ttu-id="c8a86-118">`Define` 多載允許最多將六個型別參數傳遞至具名格式字串 (範本)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-118">`Define` overloads permit passing up to six type parameters to a named format string (template).</span></span>

<span data-ttu-id="c8a86-119">提供給 `Define` 方法的字串是範本，而不是內插字串。</span><span class="sxs-lookup"><span data-stu-id="c8a86-119">The string provided to the `Define` method is a template and not an interpolated string.</span></span> <span data-ttu-id="c8a86-120">預留位置會依照指定類型的順序填入。</span><span class="sxs-lookup"><span data-stu-id="c8a86-120">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="c8a86-121">範本中的預留位置名稱應該是描述性名稱，而且在範本之間應該保持一致。</span><span class="sxs-lookup"><span data-stu-id="c8a86-121">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="c8a86-122">它們將作為結構化記錄資料內的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="c8a86-122">They serve as property names within structured log data.</span></span> <span data-ttu-id="c8a86-123">建議您針對預留位置名稱使用 [Pascal 大小寫](/dotnet/standard/design-guidelines/capitalization-conventions)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-123">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="c8a86-124">例如，`{Count}`、`{FirstName}`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-124">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="c8a86-125">每個記錄訊息都是 `LoggerMessage.Define` 所建立之靜態欄位中保存的 `Action`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-125">Each log message is an `Action` held in a static field created by `LoggerMessage.Define`.</span></span> <span data-ttu-id="c8a86-126">例如，範例應用程式會建立一個欄位來描述 Index 頁面之 GET 要求的記錄訊息 (*Internal/LoggerExtensions.cs*)：</span><span class="sxs-lookup"><span data-stu-id="c8a86-126">For example, the sample app creates a field to describe a log message for a GET request for the Index page (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

<span data-ttu-id="c8a86-127">針對 `Action`，請指定：</span><span class="sxs-lookup"><span data-stu-id="c8a86-127">For the `Action`, specify:</span></span>

* <span data-ttu-id="c8a86-128">記錄層級。</span><span class="sxs-lookup"><span data-stu-id="c8a86-128">The log level.</span></span>
* <span data-ttu-id="c8a86-129">含有靜態擴充方法名稱的唯一事件識別碼 ([EventId](/dotnet/api/microsoft.extensions.logging.eventid))。</span><span class="sxs-lookup"><span data-stu-id="c8a86-129">A unique event identifier ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) with the name of the static extension method.</span></span>
* <span data-ttu-id="c8a86-130">訊息範本 (具名格式字串)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-130">The message template (named format string).</span></span> 

<span data-ttu-id="c8a86-131">範例應用程式之 Index 頁面的要求會：</span><span class="sxs-lookup"><span data-stu-id="c8a86-131">A request for the Index page of the sample app sets the:</span></span>

* <span data-ttu-id="c8a86-132">將記錄層級設定為 `Information`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-132">Log level to `Information`.</span></span>
* <span data-ttu-id="c8a86-133">將事件識別碼設定為含有 `IndexPageRequested` 方法名稱的 `1`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-133">Event id to `1` with the name of the `IndexPageRequested` method.</span></span>
* <span data-ttu-id="c8a86-134">將訊息範本 (具名格式字串) 設定為字串。</span><span class="sxs-lookup"><span data-stu-id="c8a86-134">Message template (named format string) to a string.</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

<span data-ttu-id="c8a86-135">結構化的記錄存放區提供事件識別碼來加強記錄時，可以使用事件名稱。</span><span class="sxs-lookup"><span data-stu-id="c8a86-135">Structured logging stores may use the event name when it's supplied with the event id to enrich logging.</span></span> <span data-ttu-id="c8a86-136">例如，[Serilog](https://github.com/serilog/serilog-extensions-logging) 會使用事件名稱。</span><span class="sxs-lookup"><span data-stu-id="c8a86-136">For example, [Serilog](https://github.com/serilog/serilog-extensions-logging) uses the event name.</span></span>

<span data-ttu-id="c8a86-137">`Action` 是透過強型別擴充方法叫用。</span><span class="sxs-lookup"><span data-stu-id="c8a86-137">The `Action` is invoked through a strongly-typed extension method.</span></span> <span data-ttu-id="c8a86-138">`IndexPageRequested` 方法會在範例應用程式中針對 Index 頁面的 GET 要求記錄一則訊息：</span><span class="sxs-lookup"><span data-stu-id="c8a86-138">The `IndexPageRequested` method logs a message for an Index page GET request in the sample app:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

<span data-ttu-id="c8a86-139">`IndexPageRequested` 會在 *Pages/Index.cshtml.cs* 中 `OnGetAsync` 方法的記錄器上呼叫：</span><span class="sxs-lookup"><span data-stu-id="c8a86-139">`IndexPageRequested` is called on the logger in the `OnGetAsync` method in *Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

<span data-ttu-id="c8a86-140">檢查應用程式的主控台輸出：</span><span class="sxs-lookup"><span data-stu-id="c8a86-140">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

<span data-ttu-id="c8a86-141">若要將參數傳遞至記錄訊息，請在建立靜態欄位時定義最多六個型別。</span><span class="sxs-lookup"><span data-stu-id="c8a86-141">To pass parameters to a log message, define up to six types when creating the static field.</span></span> <span data-ttu-id="c8a86-142">透過為 `Action` 欄位定義 `string` 類型來新增引述時，範例應用程式會記錄字串：</span><span class="sxs-lookup"><span data-stu-id="c8a86-142">The sample app logs a string when adding a quote by defining a `string` type for the `Action` field:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

<span data-ttu-id="c8a86-143">委派的記錄訊息範本會從所提供的類型接收其預留位置值。</span><span class="sxs-lookup"><span data-stu-id="c8a86-143">The delegate's log message template receives its placeholder values from the types provided.</span></span> <span data-ttu-id="c8a86-144">範例應用程式會定義新增引述的委派，其中的引述參數是 `string`：</span><span class="sxs-lookup"><span data-stu-id="c8a86-144">The sample app defines a delegate for adding a quote where the quote parameter is a `string`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

<span data-ttu-id="c8a86-145">新增引述的靜態擴充方法 `QuoteAdded` 會接引述引數值，並將其傳遞至 `Action` 委派：</span><span class="sxs-lookup"><span data-stu-id="c8a86-145">The static extension method for adding a quote, `QuoteAdded`, receives the quote argument value and passes it to the `Action` delegate:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

<span data-ttu-id="c8a86-146">在 Index 頁面的頁面模型 (*Pages/Index.cshtml.cs*) 中，會呼叫 `QuoteAdded` 來記錄訊息：</span><span class="sxs-lookup"><span data-stu-id="c8a86-146">In the Index page's page model (*Pages/Index.cshtml.cs*), `QuoteAdded` is called to log the message:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

<span data-ttu-id="c8a86-147">檢查應用程式的主控台輸出：</span><span class="sxs-lookup"><span data-stu-id="c8a86-147">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

<span data-ttu-id="c8a86-148">範例應用程式會實作用於刪除引述的 `try`&ndash;`catch` 模式。</span><span class="sxs-lookup"><span data-stu-id="c8a86-148">The sample app implements a `try`&ndash;`catch` pattern for quote deletion.</span></span> <span data-ttu-id="c8a86-149">成功的刪除作業會記錄告知性訊息。</span><span class="sxs-lookup"><span data-stu-id="c8a86-149">An informational message is logged for a successful delete operation.</span></span> <span data-ttu-id="c8a86-150">如果擲回例外狀況，則會針對刪除作業記錄一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c8a86-150">An error message is logged for a delete operation when an exception is thrown.</span></span> <span data-ttu-id="c8a86-151">失敗刪除作業的記錄訊息包含例外狀況堆疊追蹤 (*Internal/LoggerExtensions.cs*)：</span><span class="sxs-lookup"><span data-stu-id="c8a86-151">The log message for the unsuccessful delete operation includes the exception stack trace (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

<span data-ttu-id="c8a86-152">請注意例外狀況如何傳遞至 `QuoteDeleteFailed` 中的委派：</span><span class="sxs-lookup"><span data-stu-id="c8a86-152">Note how the exception is passed to the delegate in `QuoteDeleteFailed`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

<span data-ttu-id="c8a86-153">在 Index 頁面的頁面模型中，成功的引述刪除會在記錄器上呼叫 `QuoteDeleted` 方法。</span><span class="sxs-lookup"><span data-stu-id="c8a86-153">In the page model for the Index page, a successful quote deletion calls the `QuoteDeleted` method on the logger.</span></span> <span data-ttu-id="c8a86-154">找不到要刪除的引述時，就會擲回 `ArgumentNullException`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-154">When a quote isn't found for deletion, an `ArgumentNullException` is thrown.</span></span> <span data-ttu-id="c8a86-155">例外狀況是由 `try` &ndash; `catch` 陳述式加以攔截，並透過在 `catch` 區塊的記錄器上呼叫 `QuoteDeleteFailed` 方法來進行記錄 (*Pages/Index.cshtml.cs*)：</span><span class="sxs-lookup"><span data-stu-id="c8a86-155">The exception is trapped by the `try`&ndash;`catch` statement and logged by calling the `QuoteDeleteFailed` method on the logger in the `catch` block (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

<span data-ttu-id="c8a86-156">成功刪除引述時，請檢查應用程式的主控台輸出：</span><span class="sxs-lookup"><span data-stu-id="c8a86-156">When a quote is successfully deleted, inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

<span data-ttu-id="c8a86-157">引述刪除失敗時，請檢查應用程式的主控台輸出。</span><span class="sxs-lookup"><span data-stu-id="c8a86-157">When quote deletion fails, inspect the app's console output.</span></span> <span data-ttu-id="c8a86-158">請注意，例外狀況會包含在記錄訊息中：</span><span class="sxs-lookup"><span data-stu-id="c8a86-158">Note that the exception is included in the log message:</span></span>

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

## <a name="loggermessagedefinescope"></a><span data-ttu-id="c8a86-159">LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="c8a86-159">LoggerMessage.DefineScope</span></span>

<span data-ttu-id="c8a86-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 建立定義[記錄範圍](xref:fundamentals/logging/index#log-scopes)的 `Func` 委派。</span><span class="sxs-lookup"><span data-stu-id="c8a86-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) creates a `Func` delegate for defining a [log scope](xref:fundamentals/logging/index#log-scopes).</span></span> <span data-ttu-id="c8a86-161">`DefineScope` 多載允許最多將三個型別參數傳遞至具名格式字串 (範本)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-161">`DefineScope` overloads permit passing up to three type parameters to a named format string (template).</span></span>

<span data-ttu-id="c8a86-162">就像 `Define` 方法的情況一樣，提供給 `DefineScope` 方法的字串是範本，而不是內插字串。</span><span class="sxs-lookup"><span data-stu-id="c8a86-162">As is the case with the `Define` method, the string provided to the `DefineScope` method is a template and not an interpolated string.</span></span> <span data-ttu-id="c8a86-163">預留位置會依照指定類型的順序填入。</span><span class="sxs-lookup"><span data-stu-id="c8a86-163">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="c8a86-164">範本中的預留位置名稱應該是描述性名稱，而且在範本之間應該保持一致。</span><span class="sxs-lookup"><span data-stu-id="c8a86-164">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="c8a86-165">它們將作為結構化記錄資料內的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="c8a86-165">They serve as property names within structured log data.</span></span> <span data-ttu-id="c8a86-166">建議您針對預留位置名稱使用 [Pascal 大小寫](/dotnet/standard/design-guidelines/capitalization-conventions)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-166">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="c8a86-167">例如，`{Count}`、`{FirstName}`。</span><span class="sxs-lookup"><span data-stu-id="c8a86-167">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="c8a86-168">使用 [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 方法，定義要套用至一系列記錄訊息的[記錄範圍](xref:fundamentals/logging/index#log-scopes)。</span><span class="sxs-lookup"><span data-stu-id="c8a86-168">Define a [log scope](xref:fundamentals/logging/index#log-scopes) to apply to a series of log messages using the [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) method.</span></span>

<span data-ttu-id="c8a86-169">範例應用程式具有 [全部清除] 按鈕，可用來刪除資料庫中的所有引述。</span><span class="sxs-lookup"><span data-stu-id="c8a86-169">The sample app has a **Clear All** button for deleting all of the quotes in the database.</span></span> <span data-ttu-id="c8a86-170">也可透過逐一移除引述來刪除它們。</span><span class="sxs-lookup"><span data-stu-id="c8a86-170">The quotes are deleted by removing them one at a time.</span></span> <span data-ttu-id="c8a86-171">每次刪除引述時，就會在記錄器上呼叫 `QuoteDeleted` 方法。</span><span class="sxs-lookup"><span data-stu-id="c8a86-171">Each time a quote is deleted, the `QuoteDeleted` method is called on the logger.</span></span> <span data-ttu-id="c8a86-172">記錄範圍會新增至這些記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="c8a86-172">A log scope is added to these log messages.</span></span>

<span data-ttu-id="c8a86-173">在 *appsettings.json* 的主控台記錄器區段中啟用 `IncludeScopes`：</span><span class="sxs-lookup"><span data-stu-id="c8a86-173">Enable `IncludeScopes` in the console logger section of *appsettings.json*:</span></span>

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

<span data-ttu-id="c8a86-174">若要建立記錄範圍，請新增欄位以保留該範圍的 `Func` 委派。</span><span class="sxs-lookup"><span data-stu-id="c8a86-174">To create a log scope, add a field to hold a `Func` delegate for the scope.</span></span> <span data-ttu-id="c8a86-175">範例應用程式會建立稱為 `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*) 的欄位：</span><span class="sxs-lookup"><span data-stu-id="c8a86-175">The sample app creates a field called `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

<span data-ttu-id="c8a86-176">請使用 `DefineScope` 來建立委派。</span><span class="sxs-lookup"><span data-stu-id="c8a86-176">Use `DefineScope` to create the delegate.</span></span> <span data-ttu-id="c8a86-177">叫用委派時，最多可以指定三種類型作為範本引數。</span><span class="sxs-lookup"><span data-stu-id="c8a86-177">Up to three types can be specified for use as template arguments when the delegate is invoked.</span></span> <span data-ttu-id="c8a86-178">範例應用程式會使用包含已刪除引述數目 (`int` 類型) 的訊息範本：</span><span class="sxs-lookup"><span data-stu-id="c8a86-178">The sample app uses a message template that includes the number of deleted quotes (an `int` type):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

<span data-ttu-id="c8a86-179">提供記錄訊息的靜態擴充方法。</span><span class="sxs-lookup"><span data-stu-id="c8a86-179">Provide a static extension method for the log message.</span></span> <span data-ttu-id="c8a86-180">包含訊息範本中出現之具名屬性的任何型別參數。</span><span class="sxs-lookup"><span data-stu-id="c8a86-180">Include any type parameters for named properties that appear in the message template.</span></span> <span data-ttu-id="c8a86-181">範例應用程式會帶入要刪除之引述的 `count`，然後傳回 `_allQuotesDeletedScope`：</span><span class="sxs-lookup"><span data-stu-id="c8a86-181">The sample app takes in a `count` of quotes to delete and returns `_allQuotesDeletedScope`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

<span data-ttu-id="c8a86-182">此範圍會將記錄擴充呼叫包裝在 `using` 區塊中：</span><span class="sxs-lookup"><span data-stu-id="c8a86-182">The scope wraps the logging extension calls in a `using` block:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

<span data-ttu-id="c8a86-183">檢查應用程式主控台輸出中的記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="c8a86-183">Inspect the log messages in the app's console output.</span></span> <span data-ttu-id="c8a86-184">下列結果顯示包含記錄範圍訊息的三個刪除引述：</span><span class="sxs-lookup"><span data-stu-id="c8a86-184">The following result shows three quotes deleted with the log scope message included:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="c8a86-185">其他資源</span><span class="sxs-lookup"><span data-stu-id="c8a86-185">Additional resources</span></span>

* [<span data-ttu-id="c8a86-186">記錄</span><span class="sxs-lookup"><span data-stu-id="c8a86-186">Logging</span></span>](xref:fundamentals/logging/index)
