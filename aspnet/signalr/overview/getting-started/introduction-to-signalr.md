---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 簡介 |Microsoft Docs
author: bradygaster
description: 本文說明 SignalR 是什麼，以及它設計來建立的一些解決方案。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 76e8fd03292eafa4b0b579ee1746fb54b57ac66b
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643682"
---
# <a name="introduction-to-signalr"></a>SignalR 簡介

依 [派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明 SignalR 是什麼，以及它設計來建立的一些解決方案。 
> 
> ## <a name="questions-and-comments"></a>問題與意見
> 
> 請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。 如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。

## <a name="what-is-signalr"></a>什麼是 SignalR？

ASP.NET SignalR 是 ASP.NET 開發人員的程式庫，可簡化將即時 web 功能新增至應用程式的流程。 即時 web 功能是能夠讓伺服器程式碼在連線的用戶端變成可用時立即將內容推送至連線的用戶端，而不是讓伺服器等待用戶端要求新的資料。

SignalR 可以用來將任何種類的「即時」 web 功能新增至您的 ASP.NET 應用程式。 雖然聊天通常是用來做為範例，但您可以多做一些。 當使用者重新整理網頁以查看新的資料時，或此頁面會執行 [長時間輪詢](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 來取得新的資料時，就是使用 SignalR 的候選項。 範例包括儀表板和監視應用程式、共同作業應用程式 (例如同時編輯檔) 、作業進度更新和即時表單。

SignalR 也可提供完全新的 web 應用程式類型，這些 web 應用程式需要伺服器的高頻率更新，例如即時遊戲。

SignalR 提供簡單的 API，可用於建立伺服器對用戶端的遠端程序呼叫， (RPC) 在用戶端瀏覽器中呼叫 JavaScript 函式 (以及從伺服器端 .NET 程式碼) 的其他用戶端平臺。 SignalR 也包含連接管理的 API (例如，連線和中斷連接事件) ，以及群組連接。

![使用 SignalR 叫用方法](introduction-to-signalr/_static/image1.png)

SignalR 會自動處理連線管理，讓您能夠將訊息同時廣播到所有連線的用戶端，例如聊天室。 您也可以將訊息傳送給特定的用戶端。 不同於傳統的 HTTP 連線，用戶端與伺服器之間的連線是持續性的，此連線會基於每次通訊重新建立。

SignalR 支援「伺服器推送」功能，在此功能中，伺服器程式碼可以在瀏覽器中使用遠端程序呼叫 (RPC) 來呼叫用戶端程式代碼，而不是現今 web 上常見的要求-回應模型。

SignalR 應用程式可以使用內建和協力廠商向外延展提供者，向外延展至數千個用戶端。

內建提供者包括：
* [服務匯流排](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

協力廠商提供者包括：
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。

SignalR 是開放原始碼，可透過 [GitHub](https://github.com/signalr)進行存取。

## <a name="signalr-and-websocket"></a>SignalR 和 WebSocket

SignalR 會使用新的 WebSocket 傳輸（如果有的話），並視需要切換回較舊的傳輸。 雖然您當然可以直接使用 WebSocket 來撰寫應用程式，但使用 SignalR 表示已為您完成許多需要執行的額外功能。 最重要的是，這表示您可以撰寫應用程式的程式碼以利用 WebSocket，而不必擔心為舊版用戶端建立個別的程式碼路徑。 SignalR 也會讓您不必擔心 WebSocket 的更新，因為 SignalR 會更新為支援基礎傳輸的變更，讓您的應用程式在不同的 WebSocket 版本之間提供一致的介面。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>傳輸和回退

SignalR 是在用戶端與伺服器之間執行即時工作所需的部分傳輸的抽象概念。 SignalR 會先嘗試建立 WebSocket 連接（如果可能的話）。 WebSocket 是 SignalR 的最佳傳輸，因為它具有：

* 伺服器記憶體最有效率的使用方式。
* 最低延遲。
* 最基礎的功能，例如用戶端與伺服器之間的全雙工通訊。
* 最嚴格的需求是，WebSocket 需要伺服器：
  * 在 Windows Server 2012 或 Windows 8 上執行。
  * .NET Framework 4.5。

如果不符合這些需求，SignalR 會嘗試使用其他傳輸來進行連接。

### <a name="html-5-transports"></a>HTML 5 傳輸

這些傳輸取決於 [HTML 5](http://en.wikipedia.org/wiki/HTML5)的支援。 如果用戶端瀏覽器不支援 HTML 5 標準，則會使用較舊的傳輸。

- 如果伺服器和瀏覽器兩者都指出可支援 Websocket) ，則 (**websocket** 。 WebSocket 是唯一在用戶端與伺服器之間建立真正持續性雙向連線的傳輸方式。 不過，WebSocket 也有最嚴格的需求;只有最新版本的 Microsoft Internet Explorer、Google Chrome 和 Mozilla Firefox 才會受到完整支援，而且在其他瀏覽器（例如 Opera 和 Safari）中只會有部分執行。
- 如果瀏覽器支援伺服器傳送的事件，也就是**伺服器傳送的事件**（也稱為 EventSource (，這基本上是除了 Internet Explorer 以外的所有瀏覽器。 ) 

### <a name="comet-transports"></a>Comet 傳輸

下列傳輸是以 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 應用程式模型為基礎，在此模型中，瀏覽器或其他用戶端會維護長時間的 HTTP 要求，而伺服器可以使用它來將資料推送至用戶端，而不需要用戶端特別要求它。

- **永遠** 只有 Internet Explorer) 的框架 (。 永久框架會建立隱藏的 IFrame，以對伺服器上未完成的端點提出要求。 伺服器接著會持續將腳本傳送給立即執行的用戶端，提供從伺服器到用戶端的單向即時連線。 從用戶端到伺服器的連接會使用不同于伺服器與用戶端連線的連接，而且就像標準的 HTTP 要求一樣，會針對每個需要傳送的資料片段建立新的連接。
- **Ajax 長時間輪詢**。 長時間輪詢不會建立持續性連接，但是會在伺服器回應之前，以保持開啟狀態的要求來輪詢伺服器，此時會關閉連線，並立即要求新的連接。 這可能會在連接重設時造成一些延遲。

如需在哪些設定下支援哪些傳輸的詳細資訊，請參閱 [支援的平臺](supported-platforms.md)。

### <a name="transport-selection-process"></a>傳輸選取進程

下列清單顯示 SignalR 用來決定要使用哪個傳輸的步驟。

1. 如果瀏覽器是 Internet Explorer 8 或更早的版本，則會使用長輪詢。
2. 如果設定了 JSONP (也就是， `jsonp` 參數會設定為 `true` 啟動連接) 時，會使用長時間輪詢。
3. 如果正在進行跨網域連線 (也就是說，如果 SignalR 端點與裝載頁面) 不在相同的網域中，則會在符合下列條件時使用 WebSocket：

   - 用戶端支援 CORS (跨原始資源分享) 。 如需哪些用戶端支援 CORS 的詳細資訊，請參閱 [caniuse.com 的 cors](http://www.caniuse.com/CORS)。
   - 用戶端支援 WebSocket
   - 伺服器支援 WebSocket

     如果不符合上述任何準則，將會使用長時間輪詢。 如需跨網域連接的詳細資訊，請參閱 [如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
4. 如果未設定 JSONP，且連接不是跨網域，則會在用戶端和伺服器都支援時使用 WebSocket。
5. 如果用戶端或伺服器不支援 WebSocket，則會使用伺服器傳送的事件（如果有的話）。
6. 如果無法使用伺服器傳送的事件，則會嘗試永久框架。
7. 如果永久框架失敗，則會使用長時間輪詢。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>監視傳輸

您可以藉由在中樞上啟用記錄功能，並在瀏覽器中開啟主控台視窗，來判斷應用程式所使用的傳輸。

若要在瀏覽器中啟用中樞事件的記錄，請將下列命令新增至您的用戶端應用程式：

`$.connection.hub.logging = true;`

- 在 Internet Explorer 中，按 F12 開啟開發人員工具，然後按一下 [主控台] 索引標籤。

    ![Microsoft Internet Explorer 中的主控台](introduction-to-signalr/_static/image2.png)
- 在 Chrome 中，按 Ctrl + Shift + J 開啟主控台。

    ![Google Chrome 中的主控台](introduction-to-signalr/_static/image3.png)

開啟主控台並啟用記錄之後，您就可以查看 SignalR 正在使用的傳輸。

![顯示 WebSocket 傳輸 Internet Explorer 中的主控台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>指定傳輸

協調傳輸需要經過一段時間和用戶端/伺服器資源。 如果已知用戶端功能，則可以在用戶端連接啟動時指定傳輸。 下列程式碼片段示範如何使用 Ajax Long 輪詢傳輸來啟動連接，如果已知用戶端不支援任何其他通訊協定，就會使用：

`connection.start({ transport: 'longPolling' });`

如果您想要讓用戶端依序嘗試特定的傳輸，則可以指定回溯順序。 下列程式碼片段示範如何嘗試 WebSocket，以及失敗的情況，並直接進入長時間輪詢。

`connection.start({ transport: ['webSockets','longPolling'] });`

指定傳輸的字串常數定義如下：

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>連接和中樞

SignalR API 包含兩個模型，可在用戶端與伺服器之間進行通訊：持續連線和中樞。

連接代表傳送單一收件者、群組或廣播訊息的簡單端點。 持續連線 API (在 .NET 程式碼中以 PersistentConnection 類別表示，) 可讓開發人員直接存取 SignalR 公開的低層級通訊協定。 使用以連線為基礎的 Api （例如 Windows Communication Foundation）的開發人員很熟悉如何使用連接通訊模型。

中樞是以連接 API 為基礎所建立的高階管線，可讓您的用戶端和伺服器直接呼叫彼此的方法。 SignalR 可處理跨電腦界限的分派，就像魔術一樣，讓用戶端可以像本機方法一樣輕鬆地在伺服器上呼叫方法，反之亦然。 使用「遠端叫用 Api」（例如 .NET 遠端處理）的開發人員會熟悉中樞通訊模型。 使用中樞也可讓您將強型別參數傳遞給方法，以啟用模型系結。

### <a name="architecture-diagram"></a>架構圖

下圖顯示中樞、持續連線和用於傳輸的基礎技術之間的關聯性。

![顯示 Api、傳輸和用戶端的 SignalR 架構圖](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>中樞的運作方式

當伺服器端程式碼在用戶端上呼叫方法時，會在作用中的傳輸上傳送封包，其中包含要呼叫之方法的名稱和參數 (當物件傳送為方法參數時，就會使用 JSON) 進行序列化。 然後，用戶端會比對方法名稱與用戶端程式代碼中定義的方法。 如果有相符的，則會使用已還原序列化的參數資料來執行用戶端方法。

您可以使用 Fiddler 之類的工具來監視方法呼叫 [。](http://fiddler2.com/) 下圖顯示在 Fiddler 的 [記錄] 窗格中，從 SignalR 伺服器傳送至網頁瀏覽器用戶端的方法呼叫。 從名為的中樞傳送方法呼叫 `MoveShapeHub` ，並呼叫所叫用的方法 `updateShape` 。

![顯示 SignalR 流量的 Fiddler 記錄視圖](introduction-to-signalr/_static/image6.png)

在此範例中，中樞名稱會以參數識別 `H` ，方法名稱會以 `M` 參數識別，而傳送至方法的資料會以 `A` 參數識別。 產生此訊息的應用程式是在 [高頻率即時](tutorial-high-frequency-realtime-with-signalr.md) 教學課程中建立的。

### <a name="choosing-a-communication-model"></a>選擇通訊模型

大部分的應用程式都應該使用中樞 API。 連接 API 可用於下列情況：

- 需要指定所傳送的實際訊息格式。
- 開發人員偏好使用訊息和分派模型，而不是遠端調用模型。
- 使用訊息模型的現有應用程式正在移植以使用 SignalR。
