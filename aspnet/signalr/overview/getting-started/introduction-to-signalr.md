---
uid: signalr/overview/getting-started/introduction-to-signalr
title: 信號R簡介 |微軟文件
author: bradygaster
description: 本文介紹了 SignalR 是什麼,以及它旨在創建的一些解決方案。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676346"
---
# <a name="introduction-to-signalr"></a>SignalR 簡介

由[派翠克·弗萊徹](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介紹了 SignalR 是什麼,以及它旨在創建的一些解決方案。 
> 
> ## <a name="questions-and-comments"></a>問題和評論
> 
> 請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。 如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。

## <a name="what-is-signalr"></a>什麼是信號R?

ASP.NET SignalR 是一個面向ASP.NET開發人員的庫,它簡化了向應用程式添加即時 Web 功能的過程。 即時 Web 功能是讓伺服器代碼在可用時立即將內容推送到連接的用戶端,而不是讓伺服器等待用戶端請求新數據的能力。

SignalR 可用於向ASP.NET應用程式添加任何類型的「即時」Web 功能。 雖然聊天通常用作示例,但您可以執行更多操作。 每當使用者刷新網頁以查看新數據,或者該頁實現[長輪詢](http://en.wikipedia.org/wiki/Push_technology#Long_polling)以檢索新數據時,它都是使用 SignalR 的候選資料庫。 範例包括儀表板和監視應用程式、協作應用程式(如同時編輯文檔)、作業進度更新和即時表單。

SignalR 還支援需要伺服器進行高頻更新(例如即時遊戲)的全新 Web 應用程式類型。

SignalR 提供了一個簡單的 API,用於建立伺服器到用戶端的遠端過程呼叫 (RPC),該呼叫從伺服器端 .NET 代碼呼叫用戶端瀏覽器(和其他用戶端平臺)中的 JavaScript 函數。 SignalR 還包括用於連接管理的 API(例如,連接和斷開連接事件)和分組連接。

![使用訊號R呼叫方法](introduction-to-signalr/_static/image1.png)

SignalR 會自動處理連線管理，讓您能夠將訊息同時廣播到所有連線的用戶端，例如聊天室。 您也可以將訊息傳送給特定的用戶端。 不同於傳統的 HTTP 連線，用戶端與伺服器之間的連線是持續性的，此連線會基於每次通訊重新建立。

SignalR 支援「伺服器推送」功能,即伺服器代碼可以使用遠端過程呼叫 (RPC) 向瀏覽器中的用戶端代碼調用,而不是網站上常見的請求-回應模型。

SignalR 應用程式可以使用內建和第三方橫向擴展提供程式擴展到數千個用戶端。

內建提供者包括:
* [服務匯流排](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

第三方提供者包括:
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).

信號R是開源的,可通過[GitHub](https://github.com/signalr)訪問。

## <a name="signalr-and-websocket"></a>訊號R和網路插座

SignalR在可用時使用新的 WebSocket 傳輸,並在必要時回退到較舊的傳輸。 雖然您肯定可以使用 WebSocket 直接編寫應用,但使用 SignalR 意味著您需要實現的大部分額外功能已經為您完成。 最重要的是,這意味著您可以編寫應用代碼以利用 WebSocket,而無需擔心為較舊的用戶端創建單獨的代碼路徑。 SignalR 還保護您不必擔心 WebSocket 的更新,因為 SignalR 已更新以支援基礎傳輸中的更改,從而為您的應用程式提供跨 WebSocket 版本的一致的介面。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>傳輸和回退

SignalR 是一種對在用戶端和伺服器之間執行即時工作所需的一些傳輸的抽象。 SignalR 連接以 HTTP 開頭,然後將其提升為 WebSocket 連接(如果可用)。 WebSocket 是 SignalR 的理想傳輸方式,因為它最有效地使用伺服器記憶體,具有最低的延遲,並具有最基本的功能(如用戶端和伺服器之間的全雙工通信),但它也具有最嚴格的要求:WebSocket 要求伺服器使用 Windows Server 2012 或 Windows 8 以及 .NET 框架 4.5。 如果不符合這些要求,SignalR 將嘗試使用其他傳輸來建立連接。

### <a name="html-5-transports"></a>HTML 5 傳輸

這些傳輸依賴於對 HTML [5](http://en.wikipedia.org/wiki/HTML5)的支援。 如果用戶端瀏覽器不支援 HTML 5 標準,將使用較舊的傳輸。

- **WebSocket(** 如果伺服器和瀏覽器都表示它們可以支援 Websocket)。 WebSocket 是建立用戶端和伺服器之間真正持久雙向連接的唯一傳輸。 但是,WebSocket 也有最嚴格的要求;它僅在最新版本的微軟瀏覽器、谷歌 Chrome 和 Mozilla Firefox 中得到充分支援,並且僅在其他瀏覽器(如 Opera 和 Safari)中具有部分實現。
- **伺服器發送事件**,也稱為事件源(如果瀏覽器支援伺服器發送事件,這基本上是除 Internet 資源管理器之外的所有瀏覽器。

### <a name="comet-transports"></a>彗星運輸

以下傳輸基於[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web 應用程式模型,其中瀏覽器或其他用戶端維護長期持有的 HTTP 請求,伺服器可以使用該請求將數據推送到用戶端,而無需用戶端專門請求該請求。

- **永久幀**(僅適用於 Internet 資源管理員)。 永久幀創建一個隱藏的 IFrame,該 IFrame 向伺服器上未完成終結點的請求。 然後,伺服器不斷向用戶端發送腳本,並立即執行該腳本,提供從伺服器到用戶端的單向即時連接。 從用戶端到伺服器的連接使用從伺服器到用戶端連接的單獨連接,並且與標準 HTTP 請求一樣,為需要發送的每個數據段創建新連接。
- **阿賈克斯長輪詢**。 長輪詢不會創建持久連接,而是輪詢伺服器的請求,該請求保持打開狀態,直到伺服器回應,此時連接將關閉,並立即請求新連接。 這可能會在連接重置時引入一些延遲。

有關支援哪些傳輸的設定的詳細資訊,請參閱[支援的平臺](supported-platforms.md)。

### <a name="transport-selection-process"></a>傳輸選擇程序

下面的清單顯示了 SignalR 用來決定要使用的傳輸的步驟。

1. 如果瀏覽器是 Internet 資源管理器 8 或更早版本,則使用長輪詢。
2. 如果配置了 JSONP(即`jsonp`參數`true`設置為 啟動連接時),則使用長輪詢。
3. 如果進行跨域連接(即,如果 SignalR 終結點與託管頁不在同一域中),則如果滿足以下條件,將使用 WebSocket:

   - 用戶端支援 CORS(跨源資源分享)。 有關哪些用戶端支援 CORS 的詳細資訊,請參閱[caniuse.com上的 CORS。](http://www.caniuse.com/CORS)
   - 用戶端支援 WebSocket
   - 伺服器支援 Web 插座

     如果未滿足上述任何條件,將使用長輪詢。 有關跨域連接的詳細資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
4. 如果未配置 JSONP 並且連接不是跨域,則如果用戶端和伺服器都支援它,將使用 WebSocket。
5. 如果用戶端或伺服器不支援 WebSocket,則使用伺服器發送事件(如果可用)。
6. 如果伺服器發送事件不可用,則嘗試"永久幀"。
7. 如果"永久幀"失敗,則使用長輪詢。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>監控運輸

通過在集線器上啟用日誌記錄,並在瀏覽器中打開控制台視窗,可以確定應用程式正在使用什麼傳輸。

要在瀏覽器中啟用中心事件紀錄記錄,請向用戶端應用程式新增以下命令:

`$.connection.hub.logging = true;`

- 在 Internet 資源管理器中,透過按 F12 打開開發人員工具,然後單擊「控制台」選項卡。

    ![微軟網際網路瀏覽器中的主控台](introduction-to-signalr/_static/image2.png)
- 在 Chrome 中,通過按 Ctrl_Shift_J 打開主控台。

    ![谷歌瀏覽器中的主控台](introduction-to-signalr/_static/image3.png)

啟用主控台並啟用日誌記錄後,您將能夠看到 SignalR 正在使用哪種傳輸。

![顯示 WebSocket 傳輸的 Internet 資源管理員中的主控台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>指定傳輸

協商傳輸需要一定的時間和用戶端/伺服器資源。 如果用戶端功能已知,則可以在啟動用戶端連接時指定傳輸。 以下代碼段演示使用 Ajax Long 輪詢傳輸啟動連接,如果已知用戶端不支援任何其他協定,則使用該傳輸:

`connection.start({ transport: 'longPolling' });`

如果希望客戶端按順序嘗試特定傳輸,則可以指定回退順序。 以下代碼段演示了嘗試 WebSocket,如果失敗,請直接訪問長輪詢。

`connection.start({ transport: ['webSockets','longPolling'] });`

指定指定的字串常量定義的字串常量定義的字串常量定義的字串:

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>連接和集線器

SignalR API 包含兩種用於用戶端和伺服器之間通信的模型:持久連接和集線器。

連接表示用於發送單收件者、分組消息或廣播消息的簡單終結點。 持久連接 API(由持久連接類在 .NET 代碼中表示)使開發人員能夠直接訪問 SignalR 公開的低級通訊協定。 使用連接通訊模型對於使用基於連接的 API(如 Windows 通信基礎)的開發人員來說,是熟悉的。

集線器是一個基於連接 API 構建的更高級管道,允許用戶端和伺服器直接呼叫彼此的方法。 SignalR 處理跨計算機邊界的調度,就像通過魔術一樣,允許用戶端像本地方法一樣輕鬆地調用伺服器上的方法,反之亦然。 使用中心通信模型對於使用遠端調用 API(如 .NET 遠端處理)的開發人員來說,是熟悉的。 使用集線器還允許您將強類型參數傳遞給方法,從而啟用模型綁定。

### <a name="architecture-diagram"></a>架構圖

下圖顯示了集線器、持久連接和用於傳輸的基礎技術之間的關係。

![顯示 API、傳輸和客戶端的訊號 R 架構圖](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>中心的工作原理

當伺服器端代碼在用戶端上調用方法時,數據包將跨活動傳輸發送,該傳輸包含要調用的方法的名稱和參數(當物件作為方法參數發送時,使用 JSON 對其進行序列化)。 然後,用戶端將方法名稱與用戶端代碼中定義的方法匹配。 如果存在匹配項,將使用反序列化參數數據執行用戶端方法。

可以使用[Fiddler](http://fiddler2.com/)等工具監視方法調用。 下圖顯示了 Fiddler 的 Logs 窗格中從 SignalR 伺服器發送到 Web 瀏覽器用戶端的方法調用。 方法呼叫是從稱為`MoveShapeHub`的中心傳送的,並且呼叫的方法`updateShape`稱為 。

![顯示訊號 R 流量的 Fiddler 紀錄檢視](introduction-to-signalr/_static/image6.png)

在此示例中,中心名稱與 參數`H`一起標識;因此,使用 參數標識中心名稱。方法名稱與`M`參數一起標識,發送到方法的數據用`A`參數 標識。 生成此消息的應用程式在[高頻即時](tutorial-high-frequency-realtime-with-signalr.md)教程中創建。

### <a name="choosing-a-communication-model"></a>選擇通訊模型

大多數應用程式應使用集線器 API。 連線 API 可用於以下情況:

- 需要指定發送的實際訊息的格式。
- 開發人員更喜歡使用消息傳遞和調度模型,而不是遠端調用模型。
- 正在移植使用消息傳遞模型的現有應用程式以使用 SignalR。
