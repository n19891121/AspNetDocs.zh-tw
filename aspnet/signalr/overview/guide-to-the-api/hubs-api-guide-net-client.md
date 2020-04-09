---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET信號器集線器 API 指南 - .NET 用戶端 (C#) |微軟文件
author: bradygaster
description: 本文檔介紹了在 .NET 用戶端(如 Windows 應用商店 (WinRT)、WPF、Silverlight 和 cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676332"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET訊號器集線器 API 指南 - .NET 用戶端 (C#)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文件介紹了在 .NET 用戶端(如 Windows 應用商店 (WinRT)、WPF、Silverlight 和控制台應用程式)中為 SignalR 版本 2 使用集線器 API 的簡介。
>
> SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。 在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。 在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。 SignalR 為您處理所有用戶端到伺服器管道。
>
> SignalR 還提供稱為持久連接的較低級別的 API。 有關 SignalR、集線器和持久連線的介紹,或者有關如何建構完整的 SignalR 應用程式的教學,請參閱[SignalR - 入門](../getting-started/index.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - 信號R版本 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的早期版本
>
> 有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題和評論
>
> 請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。 如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [用戶端設定](#clientsetup)
- [如何建立連線](#establishconnection)

    - [來自銀光用戶端的跨網域連接](#slcrossdomain)
- [如何設定連線](#configureconnection)

    - [如何設定 WPF 用戶端中的最大併發連線數](#maxconnections)
    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
    - [如何指定 HTTP 標頭](#httpheaders)
    - [如何指定客戶端憑證](#clientcertificate)
- [如何建立中心代理](#proxy)
- [如何在客戶端上定義伺服器可以呼叫的方法](#callclient)

    - [沒有參數的方法](#clientmethodswithoutparms)
    - [具有參數的方法,指定參數類型](#clientmethodswithparmtypes)
    - [具有參數的方法,為參數指定動態物件](#clientmethodswithdynamparms)
    - [如何移除處理程式](#removehandler)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連線存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何開啟客戶端記錄記錄](#logging)
- [WPF、Silverlight 和主控台應用程式代碼範例,用於伺服器可以呼叫的用戶端方法](#wpfsl)

有關範例 .NET 客戶端專案,請參閱以下資源:

- [古斯塔沃-阿爾門塔 / 信號R-樣本](https://github.com/gustavo-armenta/SignalR-Samples)GitHub.com(WinRT,銀光,控制台應用程式示例)。
- [達米安愛德華茲 / 信號R-移動形狀演示 / 移動形狀.桌面](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)GitHub.com (WPF 示例)。
- [信號R / 微軟.AspNet.SignalR.用戶端.GitHub.com上的樣本](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)(控制台應用範例)。

有關如何對伺服器或 JAVAScript 客戶端進行程式設計的文件,請參閱以下資源:

- [訊號器集線器 API 指南 - 伺服器](hubs-api-guide-server.md)
- [信號器中心 API 指南 - JavaScript 用戶端](hubs-api-guide-javascript-client.md)

指向 API 參考主題的連結指向 API 的 .NET 4.5 版本。 如果使用 .NET 4,請參閱[API 主題的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

安裝[微軟.AspNet.SignalR.用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 包(不是[微軟.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包)。 此包支援 WinRT、Silverlight、WPF、控制台應用程式和 Windows Phone 用戶端,適用於 .NET 4 和 .NET 4.5。

如果用戶端上的 SignalR 版本與伺服器上的版本不同,則 SignalR 通常能夠適應差異。 例如,運行 SignalR 版本 2 的伺服器將支援安裝了 1.1.x 的用戶端以及安裝了版本 2 的用戶端。 如果伺服器上的版本和用戶端上的版本之間的差異太大,或者如果用戶端比伺服器新,則在用戶端嘗試建立連接時,SignalR 會`InvalidOperationException`引發異常。 錯誤消息為""`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連線

在建立連接之前,必須創建物件`HubConnection`並創建代理。 要建立連接,請`Start`調用`HubConnection`物件上的方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> 對於 JavaScript 用戶端,在調用方法建立連接`Start`之前, 您必須至少註冊一個事件處理程式。 對於 .NET 用戶端,這不需要。 對於 JavaScript 用戶端,生成的代理程式碼會自動為伺服器上存在的所有中心創建代理,註冊處理程式是指示用戶端打算使用哪個集線器的方式。 但對於 .NET 用戶端,您可以手動創建集線器代理,因此 SignalR 假定您將使用為其創建代理的任何集線器。

範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。 有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

該方法`Start`以異步方式執行。 為了確保後續代碼行在建立連接之前不會執行,請使用`await`ASP.NET 4.5 非同步`.Wait()`方法或同步方法。 不要在 WinRT`.Wait()`用戶端中使用。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>來自銀光用戶端的跨網域連接

有關如何啟用來自 Silverlight 用戶端的跨域連接的資訊,請參閱[使服務跨域邊界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連線

在建立連線之前,可以指定以下任一選項:

- 併發連接限制。
- 查詢字串參數。
- 傳輸方法。
- HTTP 標頭。
- 用戶端證書。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>如何設定 WPF 用戶端中的最大併發連線數

在 WPF 用戶端中,您可能需要從預設值 2 增加併發連接的最大數量。 建議的值為 10。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

有關詳細資訊,請參閱[服務點管理員.預設連線限制](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果要在用戶端連接時將數據發送到伺服器,則可以向連接物件添加查詢字串參數。 下面的範例展示如何在用戶端代碼中設置查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

下面的範例展示如何讀取伺服器代碼中的查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

作為連接過程的一部分,SignalR 用戶端通常與伺服器協商以確定伺服器和用戶端支援的最佳傳輸。 如果您已經知道要使用的傳輸,可以繞過此協商過程。 要指定傳輸方法,請將傳輸物件傳遞給 Start 方法。 下面的範例展示如何在用戶端代碼中指定傳輸方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[Microsoft.AspNet.SignalR.Client.傳輸](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包括以下類,可用於指定傳輸。

- [長輪詢傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [伺服器傳送事件傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocket 傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)(僅在伺服器和用戶端使用 .NET 4.5 時可用。
- [自動傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)(自動選擇客戶端和伺服器支援的最佳傳輸。 這是默認傳輸。 將此傳遞給`Start`方法的效果與不傳入任何內容的效果相同。

ForeverFrame 傳輸不包括在此清單中,因為它僅由瀏覽器使用。

有關如何在伺服器代碼中檢查傳輸方法的資訊,請參閱[ASP.NET SignalR 集線器 API 指南 - 伺服器 - 如何從 Context 屬性取得有關用戶端的資訊](hubs-api-guide-server.md#contextproperty)。 有關傳輸和回退的詳細資訊,請參閱[訊號R - 傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>如何指定 HTTP 標頭

要設置 HTTP 標`Headers`頭, 請使用連接物件上的屬性。 下面的範例展示如何添加 HTTP 標頭。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>如何指定客戶端憑證

要添加用戶端證書,`AddClientCertificate`請使用連接物件上的方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>如何建立中心代理

為了在用戶端上定義集線器可以從伺服器調用的方法,並在伺服器上的集線器上調用方法,請通過調用`CreateHubProxy`連接物件為集線器創建代理。 傳遞給的字串`CreateHubProxy`是 Hub 類的名稱`HubName`,或者 屬性指定的名稱(如果在伺服器上使用)。 名稱比對不區分大小寫。

**伺服器上的集線器類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**為中心類別建立用戶端代理**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

如果使用`HubName`屬性修飾 Hub 類,請使用該名稱。

**伺服器上的集線器類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**為中心類別建立用戶端代理**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

如果使用相同的`HubConnection.CreateHubProxy``hubName`調用多次 ,則會獲取相同的`IHubProxy`緩存 物件。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客戶端上定義伺服器可以呼叫的方法

要定義伺服器可以調用的方法,請使用代理`On`的方法註冊事件處理程式。

方法名稱匹配不區分大小寫。 例如,`Clients.All.UpdateStockPrice`在伺服器上將`updateStockPrice`執行`updatestockprice`、`UpdateStockPrice`或在用戶端上。

不同的用戶端平臺對如何編寫方法來更新 UI 有不同的要求。 顯示的範例適用於 WinRT (Windows 應用商店 .NET) 用戶端。 WPF、Silverlight 和主控台應用程式範例在本[主題後面的單獨部分](#wpfsl)提供。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>沒有參數的方法

如果正在處理的方法沒有參數,請使用`On`方法的非泛型重載:

**伺服器代碼呼叫沒有參數的用戶端方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**WinRT 客戶端碼用於從伺服器呼叫沒有參數的方法([請參閱本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法,指定參數類型

如果要處理的方法具有參數,請指定參數的類型作為`On`方法的泛型類型。 `On`該方法有泛型重載,使您能夠指定最多 8 個參數(Windows Phone 7 上的 4 個參數)。 在下面的示例中,一個參數發送到`UpdateStockPrice`方法。

**使用參數呼叫用戶端方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**WinRT 客戶端碼用於從具有參數的伺服器呼叫的方法([請參閱本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法,為參數指定動態物件

作為將參數指定為`On`方法的泛型型別的替代方法,可以將參數指定為動態物件:

**使用參數呼叫用戶端方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**WinRT 客戶端碼用於使用參數從伺服器呼叫的方法,使用參數的動態物件([請參考本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>如何移除處理程式

要刪除處理程式,請調用其`Dispose`方法。

**從伺服器呼叫的方法的客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**用戶端代碼以移除處理程式**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

要在伺服器上調用方法,`Invoke`請使用集線器代理上的方法。

如果伺服器方法沒有返回值,請使用`Invoke`方法的非泛型重載。

**沒有傳回值的方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**呼叫沒有返回值的方法的客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

如果伺服器方法具有返回值,請指定返回類型作為`Invoke`方法的泛型類型。

**具有傳回值並採用複雜類型參數的方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**參數與傳回值的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**用戶端代碼呼叫具有傳回值並採用複雜類型參數的方法,在 ASP.NET 4.5 非同步方法中呼叫**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**用戶端代碼呼叫具有傳回值並採用複雜類型參數的方法(在同步方法中)**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

該方法`Invoke`非同步執行並傳`Task`回物件 。 如果不指定`await``.Wait()`或 ,則下一行代碼將在調用的方法完成執行之前執行。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連線存留期事件

SignalR 提供您可以處理的以下連線存留期事件:

- `Received`:在連接上收到任何數據時引發。 提供接收的數據。
- `ConnectionSlow`:當客戶端檢測到連接緩慢或頻繁斷開時引發。
- `Reconnecting`:當基礎傳輸開始重新連接時引發。
- `Reconnected`:在基礎傳輸重新連接時引發。
- `StateChanged`:當連接狀態更改時引發。 提供舊狀態和新狀態。 有關連接狀態值的資訊,請參閱[連接狀態枚舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。
- `Closed`:連接斷開連接時引發。

例如,如果要顯示未致命但會導致間歇性連接問題(如連接速度慢或頻繁斷開)的錯誤的警告消息,則處理該`ConnectionSlow`事件。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

如果未在伺服器上顯式啟用詳細的錯誤消息,則 SignalR 在錯誤後返回的異常物件包含有關該錯誤的最少資訊。 例如,如果調用`newContosoChatMessage`失敗,錯誤物件中的錯誤消息包含`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`「 出於安全原因不建議向生產中的客戶端發送詳細的錯誤訊息,但如果要啟用詳細的錯誤訊息以進行故障排除,請使用伺服器上的以下代碼。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

要處理 SignalR 引發的錯誤,可以在連接物件`Error`上為 事件添加處理程式。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

要處理方法調用中的錯誤,請將代碼包裝在 try-catch 塊中。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何開啟客戶端記錄記錄

要啟用客戶端日誌記錄,在連接物件`TraceLevel`上`TraceWriter`設置和 屬性。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>WPF、Silverlight 和主控台應用程式代碼範例,用於伺服器可以呼叫的用戶端方法

前面顯示的代碼示例用於定義伺服器可以調用的用戶端方法,應用於 WinRT 用戶端。 以下範例顯示了 WPF、Silverlight 和主控台應用程式用戶端的等效代碼。

### <a name="methods-without-parameters"></a>沒有參數的方法

**WPF 客戶端碼,用於從伺服器呼叫無參數的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**銀光客戶端代碼,用於從伺服器呼叫無參數的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**主控台應用程式客戶端碼,用於從伺服器呼叫無參數的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法,指定參數類型

**WPF 客戶端碼,用於從具有參數的伺服器呼叫的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**使用參數從伺服器呼叫的方法的 Silverlight 客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**主控台應用程式客戶端代碼,用於從具有參數的伺服器呼叫的方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法,為參數指定動態物件

**使用參數的動態物件從伺服器呼叫的方法的 WPF 客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**使用參數的動態物件從伺服器呼叫的方法的 Silverlight 客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**使用參數的動態物件從伺服器呼叫的方法的主控台應用程式客戶端碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
