---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: 'ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (c # ) |Microsoft Docs'
author: bradygaster
description: 本檔提供在 .NET 用戶端中使用適用于 SignalR 第2版的中樞 API 的簡介，例如 Windows Store (WinRT) 、WPF、Silverlight 和缺點 .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345542"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (c # ) 

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔提供在 .NET 用戶端中使用適用于 SignalR 第2版的中樞 API 的簡介，例如 Windows Store (WinRT) 、WPF、Silverlight 和主控台應用程式。
>
> SignalR 中樞 API 可讓您進行遠端程序呼叫， (從伺服器到連線用戶端，以及從用戶端到伺服器的 Rpc) 。 在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。 在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。 SignalR 會為您處理所有用戶端對伺服器的配管。
>
> SignalR 也提供較低層級的 API，稱為「持續連線」。 如需 SignalR、中樞和持續連線的簡介，或說明如何建立完整 SignalR 應用程式的教學課程，請參閱 [SignalR-消費者入門](../getting-started/index.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。 如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [用戶端設定](#clientsetup)
- [如何建立連接](#establishconnection)

    - [Silverlight 用戶端的跨網域連接](#slcrossdomain)
- [如何設定連接](#configureconnection)

    - [如何在 WPF 用戶端中設定並行連接的最大數目](#maxconnections)
    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
    - [如何指定 HTTP 標頭](#httpheaders)
    - [如何指定用戶端憑證](#clientcertificate)
- [如何建立中樞 proxy](#proxy)
- [如何在用戶端上定義伺服器可以呼叫的方法](#callclient)

    - [沒有參數的方法](#clientmethodswithoutparms)
    - [具有參數的方法，指定參數類型](#clientmethodswithparmtypes)
    - [具有參數的方法，指定參數的動態物件](#clientmethodswithdynamparms)
    - [如何移除處理常式](#removehandler)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連接存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何啟用用戶端記錄](#logging)
- [伺服器可呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例](#wpfsl)

如需範例 .NET 用戶端專案，請參閱下列資源：

- [>gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT、Silverlight、主控台應用程式範例) 的範例。
- GitHub.com 上的[DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF 範例) 。
- [SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) GitHub.com (主控台應用程式範例) 。

如需有關如何對伺服器或 JavaScript 用戶端進行程式設計的檔，請參閱下列資源：

- [SignalR 中樞 API 指南-伺服器](hubs-api-guide-server.md)
- [SignalR 中樞 API 指南-JavaScript 用戶端](hubs-api-guide-javascript-client.md)

API 參考主題的連結是 .NET 4.5 版的 API。 如果您使用的是 .NET 4，請參閱 [.net 4 版的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

將 SignalR 安裝 (不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)封裝) 的[用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 套件。 針對 .NET 4 和 .NET 4.5，此套件支援 WinRT、Silverlight、WPF、主控台應用程式和 Windows Phone 用戶端。

如果您在用戶端上的 SignalR 版本與伺服器上的版本不同，則 SignalR 通常可以調整成差異。 例如，執行 SignalR 第2版的伺服器將支援已安裝 1.1. x 的用戶端，以及安裝了版本2的用戶端。 如果伺服器上的版本與用戶端上的版本之間的差異太大，或用戶端比伺服器更新時，SignalR 會在 `InvalidOperationException` 用戶端嘗試建立連接時擲回例外狀況。 錯誤訊息為 " `You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X` "。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連接

您必須先建立物件並建立 proxy，才能建立連線 `HubConnection` 。 若要建立連接，請 `Start` 在物件上呼叫 `HubConnection` 方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> 針對 JavaScript 用戶端，您必須先註冊至少一個事件處理常式，才能呼叫 `Start` 方法來建立連接。 .NET 用戶端不需要這項功能。 針對 JavaScript 用戶端，產生的 proxy 程式碼會自動為存在於伺服器上的所有中樞建立 proxy，並註冊處理常式，就是您指出用戶端想要使用的中樞。 但是針對 .NET 用戶端，您會以手動方式建立中樞 proxy，所以 SignalR 會假設您將使用任何建立 proxy 的中樞。

範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

`Start`方法會以非同步方式執行。 為了確保後續的程式程式碼在建立連接之後不會執行，請 `await` 在 ASP.NET 4.5 非同步方法或 `.Wait()` 同步方法中使用。 請勿 `.Wait()` 在 WinRT 用戶端中使用。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight 用戶端的跨網域連接

如需有關如何啟用 Silverlight 用戶端的跨網域連線的詳細資訊，請參閱 [讓服務可跨網域界限使用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連接

建立連接之前，您可以指定下列任何選項：

- 並行連接限制。
- 查詢字串參數。
- 傳輸方法。
- HTTP 標頭。
- 用戶端憑證。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>如何在 WPF 用戶端中設定並行連接的最大數目

在 WPF 用戶端中，您可能必須從預設值2增加並行連接的最大數目。 建議值為10。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

如需詳細資訊，請參閱 [ServicePointManager. >servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果您想要在用戶端連接時將資料傳送至伺服器，您可以將查詢字串參數加入至連線物件。 下列範例顯示如何在用戶端程式代碼中設定查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

下列範例示範如何在伺服器程式碼中讀取查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

在連接的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端所支援的最佳傳輸。 如果您已經知道要使用哪一個傳輸，則可以略過此協商流程。 若要指定傳輸方法，請將傳輸物件傳遞給 Start 方法。 下列範例顯示如何在用戶端程式代碼中指定傳輸方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包含下列類別，您可以使用這些類別來指定傳輸。

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (只有在伺服器和用戶端都使用 .net 4.5 時才可使用。 ) 
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (會自動選擇用戶端和伺服器所支援的最佳傳輸。 這是預設傳輸。 將此傳遞給 `Start` 方法與未傳遞任何的效果相同。 ) 

ForeverFrame 傳輸不包含在此清單中，因為它只能由瀏覽器使用。

如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。 如需傳輸和回退的詳細資訊，請參閱 [SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>如何指定 HTTP 標頭

若要設定 HTTP 標頭，請使用 `Headers` 連線物件上的屬性。 下列範例顯示如何新增 HTTP 標頭。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>如何指定用戶端憑證

若要加入用戶端憑證，請 `AddClientCertificate` 在連線物件上使用方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>如何建立中樞 proxy

若要在用戶端上定義中樞可以從伺服器呼叫的方法，並在伺服器的中樞上叫用方法，請在連線物件上呼叫，以建立中樞的 proxy `CreateHubProxy` 。 您傳入的字串 `CreateHubProxy` 是中樞類別的名稱，或 `HubName` 屬性（如果在伺服器上使用的話）所指定的名稱。 名稱比對不區分大小寫。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**建立中樞類別的用戶端 proxy**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

如果您使用屬性裝飾您的中樞類別 `HubName` ，請使用該名稱。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**建立中樞類別的用戶端 proxy**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

如果您 `HubConnection.CreateHubProxy` 以相同的方式呼叫多次 `hubName` ，則會取得相同的快取 `IHubProxy` 物件。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在用戶端上定義伺服器可以呼叫的方法

若要定義伺服器可以呼叫的方法，請使用 proxy 的 `On` 方法來註冊事件處理常式。

方法名稱比對不區分大小寫。 例如， `Clients.All.UpdateStockPrice` 在伺服器上，伺服器將會在 `updateStockPrice` 用戶端上執行、 `updatestockprice` 或 `UpdateStockPrice` 。

不同的用戶端平臺會有不同的需求，讓您撰寫方法程式碼來更新 UI。 所顯示的範例適用于 WinRT (Windows Store .NET) 用戶端。 WPF、Silverlight 和主控台應用程式範例會在 [本主題稍後的不同章節](#wpfsl)中提供。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>沒有參數的方法

如果您要處理的方法沒有參數，請使用方法的非泛型多載 `On` ：

**呼叫不含參數之用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**從沒有參數的伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) **

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法，指定參數類型

如果您要處理的方法有參數，請將參數類型指定為方法的泛型型別 `On` 。 方法的泛型 `On` 多載可讓您指定最多8個參數， (4 的 Windows Phone 7) 上。 在下列範例中，會將一個參數傳送給 `UpdateStockPrice` 方法。

**使用參數呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**用於參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**使用參數從伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) **

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法，指定參數的動態物件

除了將參數指定為方法的泛型型別之外 `On` ，您還可以指定參數做為動態物件：

**使用參數呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**用於參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**使用參數從伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) **

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>如何移除處理常式

若要移除處理常式，請呼叫其 `Dispose` 方法。

**從伺服器呼叫之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**移除處理常式的用戶端程式代碼**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

若要在伺服器上呼叫方法，請 `Invoke` 在中樞 proxy 上使用方法。

如果伺服器方法沒有傳回值，請使用方法的非泛型多載 `Invoke` 。

**沒有傳回值之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**呼叫沒有傳回值之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

如果伺服器方法有傳回值，請將傳回型別指定為方法的泛型型別 `Invoke` 。

**具有傳回值且採用複雜型別參數之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**用於參數和傳回值的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**在 ASP.NET 4.5 非同步方法中呼叫具有傳回值並採用複雜型別參數之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**用戶端程式代碼，呼叫具有傳回值的方法，並在同步方法中採用複雜型別參數**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke`方法會以非同步方式執行，並傳回 `Task` 物件。 如果您未指定 `await` 或 `.Wait()` ，則會在您叫用的方法執行完成之前，先執行下一行程式碼。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連接存留期事件

SignalR 提供下列可供您處理的連接存留期事件：

- `Received`：在連接上收到任何資料時引發。 提供接收的資料。
- `ConnectionSlow`：當用戶端偵測到緩慢或經常中斷連接時引發。
- `Reconnecting`：當基礎傳輸開始重新連接時引發。
- `Reconnected`：當基礎傳輸重新連接時引發。
- `StateChanged`：當連接狀態變更時引發。 提供舊狀態和新的狀態。 如需連接狀態值的詳細資訊，請參閱 [ConnectionState 列舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。
- `Closed`：連接中斷連接時引發。

例如，如果您想要針對不是嚴重的錯誤顯示警告訊息，但造成間歇性的連接問題（例如緩慢或經常中斷連接），請處理 `ConnectionSlow` 事件。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

如需詳細資訊，請參閱 [瞭解及處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 在錯誤之後傳回的例外狀況物件會包含錯誤的最基本資訊。 例如，如果的呼叫 `newContosoChatMessage` 失敗，則錯誤物件中的錯誤訊息會包含「」 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 基於安全性理由，不建議在生產環境中傳送詳細的錯誤訊息給用戶端，但如果您想要啟用詳細的錯誤訊息以進行疑難排解，請在伺服器上使用下列程式碼。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

若要處理 SignalR 引發的錯誤，您可以 `Error` 在連線物件上加入事件的處理常式。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

若要處理方法調用的錯誤，請將程式碼包裝在 try-catch 區塊中。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何啟用用戶端記錄

若要啟用用戶端記錄，請 `TraceLevel` `TraceWriter` 在連線物件上設定和屬性。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>伺服器可呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例

稍早所示的程式碼範例，可用於定義伺服器可呼叫的用戶端方法，適用于 WinRT 用戶端。 下列範例顯示 WPF、Silverlight 和主控台應用程式用戶端的對等程式碼。

### <a name="methods-without-parameters"></a>沒有參數的方法

**從沒有參數的伺服器呼叫之方法的 WPF 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**從沒有參數的伺服器呼叫之方法的 Silverlight 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**從伺服器呼叫的方法的主控台應用程式用戶端程式代碼（不含參數）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法，指定參數類型

**使用參數從伺服器呼叫之方法的 WPF 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**使用參數從伺服器呼叫之方法的 Silverlight 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**使用參數從伺服器呼叫的方法的主控台應用程式用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法，指定參數的動態物件

**使用參數從伺服器呼叫的方法的 WPF 用戶端程式代碼，使用參數的動態物件**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**使用參數從伺服器呼叫的方法的 Silverlight 用戶端程式代碼，使用動態物件作為參數**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**使用參數將動態物件用於從伺服器呼叫的方法的主控台應用程式用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
