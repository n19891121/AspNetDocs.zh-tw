---
title: 使用資料流在 ASP.NET Core SignalR
author: bradygaster
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/14/2018
uid: signalr/streaming
ms.openlocfilehash: ade2d6fb6e799d53ff3aaa69c641d0088acdee95
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036645"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a>使用資料流在 ASP.NET Core SignalR

由[brennan Conroy](https://github.com/BrennanConroy)提供

ASP.NET Core SignalR 支援資料流的伺服器方法的傳回值。 這是適用於其中的資料片段會在一段時間的案例。 時傳回的值串流處理到用戶端，每個片段會傳送至用戶端，它會變成可用，而不是等待變成可用的所有資料。

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

## <a name="set-up-the-hub"></a>設定中樞

中樞的方法會自動變成資料流處理的中樞方法傳回時`ChannelReader<T>`或`Task<ChannelReader<T>>`。 以下是此範例示範的資料串流到用戶端的基本概念。 每當物件寫入`ChannelReader`該物件會立即傳送至用戶端。 在結束時，`ChannelReader`完成告知用戶端的資料流已關閉。

> [!NOTE]
> * 寫入`ChannelReader`在背景執行緒，然後傳回`ChannelReader`儘速。 其他中樞引動過程將會遭到封鎖，直到`ChannelReader`會傳回。
> * 包裝您的邏輯中`try ... catch`並完成`Channel`在 catch 和外部 catch 以確保中樞方法叫用正確地完成。

::: moniker range="= aspnetcore-2.1"

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.aspnetcore21.cs?name=snippet1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?name=snippet1)]

在 ASP.NET Core 2.2 或更新版本，串流處理中樞方法可以接受`CancellationToken`從資料流的用戶端取消訂閱時，會觸發的參數。 若要停止伺服器作業，並釋放任何資源，如果用戶端中斷連線的資料流結束前使用此權杖。

::: moniker-end

## <a name="net-client"></a>.NET 用戶端

`StreamAsChannelAsync`方法`HubConnection`用來叫用的資料流的方法。 將中樞方法的名稱和定義中的中樞方法的引數傳遞`StreamAsChannelAsync`。 泛型參數上的`StreamAsChannelAsync<T>`指定的資料流的方法所傳回的物件類型。 A`ChannelReader<T>`傳回的資料流引動過程，和代表用戶端上的資料流。 若要讀取資料，常見的模式是迴圈`WaitToReadAsync`並呼叫`TryRead`可用資料時。 資料流已關閉伺服器，或取消語彙基元傳遞至時，將會結束迴圈`StreamAsChannelAsync`已取消。

::: moniker range=">= aspnetcore-2.2"

```csharp
// Call "Cancel" on this CancellationTokenSource to send a cancellation message to 
// the server, which will trigger the corresponding token in the Hub method.
var cancellationTokenSource = new CancellationTokenSource();
var channel = await hubConnection.StreamAsChannelAsync<int>(
    "Counter", 10, 500, cancellationTokenSource.Token);

// Wait asynchronously for data to become available
while (await channel.WaitToReadAsync())
{
    // Read all currently available data synchronously, before waiting for more data
    while (channel.TryRead(out var count))
    {
        Console.WriteLine($"{count}");
    }
}

Console.WriteLine("Streaming completed");
```

::: moniker-end

::: moniker range="= aspnetcore-2.1"

```csharp
var channel = await hubConnection
    .StreamAsChannelAsync<int>("Counter", 10, 500, CancellationToken.None);

// Wait asynchronously for data to become available
while (await channel.WaitToReadAsync())
{
    // Read all currently available data synchronously, before waiting for more data
    while (channel.TryRead(out var count))
    {
        Console.WriteLine($"{count}");
    }
}

Console.WriteLine("Streaming completed");
```

::: moniker-end

## <a name="javascript-client"></a>JavaScript 用戶端

JavaScript 用戶端呼叫中樞上資料流的方法，使用`connection.stream`。 `stream` 方法接受兩個引數：

* 中樞方法的名稱。 下列範例中，在中樞方法名稱是`Counter`。
* 中樞的方法中定義的引數。 在下列範例中，引數是： 資料流項目，若要接收，以及資料流項目之間的延遲數目的計數。

`connection.stream` 會傳回`IStreamResult`其中包含`subscribe`方法。 傳遞`IStreamSubscriber`要`subscribe`並設定`next`， `error`，和`complete`若要取得通知的回呼`stream`引動過程。

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

::: moniker range="= aspnetcore-2.1"

若要結束用戶端從資料流，呼叫`dispose`方法`ISubscription`傳回`subscribe`方法。

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

若要結束用戶端從資料流，呼叫`dispose`方法`ISubscription`傳回`subscribe`方法。 呼叫這個方法會造成`CancellationToken`參數 （如果您提供一個） 之中樞方法的取消。

::: moniker-end

## <a name="related-resources"></a>相關資源

* [中樞](xref:signalr/hubs)
* [.NET 用戶端](xref:signalr/dotnet-client)
* [JavaScript 用戶端](xref:signalr/javascript-client)
* [發佈至 Azure](xref:signalr/publish-to-azure-web-app)
