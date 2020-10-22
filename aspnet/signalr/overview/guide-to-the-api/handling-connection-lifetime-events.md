---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 瞭解和處理 SignalR 中的連接存留期事件 |Microsoft Docs
author: bradygaster
description: 本文說明如何使用中樞 API 所公開的事件。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345228"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>了解及處理 SignalR 的連線存留期事件

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文概述您可以處理的 SignalR 連線、重新連線和中斷線上活動，以及您可以設定的 timeout 和 keepalive 設定。
>
> 本文假設您已具備 SignalR 和連線存留期事件的一些知識。 如需 SignalR 的簡介，請參閱 [SignalR 簡介](../getting-started/introduction-to-signalr.md)。 如需連接存留期事件的清單，請參閱下列資源：
>
> - [如何處理中樞類別中的連接存留期事件](hubs-api-guide-server.md#connectionlifetime)
> - [如何在 JavaScript 用戶端中處理連接存留期事件](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [如何在 .NET 用戶端中處理連接存留期事件](hubs-api-guide-net-client.md#connectionlifetime)
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

本文包含下列各節：

- [連接存留期術語和案例](#terminology)

    - [SignalR 連接、傳輸連線和實體連線](#signalrvstransport)
    - [傳輸中斷連接案例](#transportdisconnect)
    - [用戶端中斷連接案例](#clientdisconnect)
    - [伺服器中斷連接案例](#serverdisconnect)
- [Timeout 和 keepalive 設定](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [如何變更 timeout 和 keepalive 設定](#changetimeout)
- [如何通知使用者中斷連線](#notifydisconnect)
- [如何持續重新連線](#continuousreconnect)
- [如何在伺服器程式碼中中斷用戶端連線](#disconnectclientfromserver)
- [偵測中斷連接的原因](#detectingreasonfordisconnection)

API 參考主題的連結是 .NET 4.5 版的 API。 如果您使用的是 .NET 4，請參閱 [.net 4 版的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>連接存留期術語和案例

`OnReconnected`SignalR 中樞內的事件處理常式可以在 `OnConnected` 指定用戶端的之後，直接執行，但不能執行 `OnDisconnected` 。 有幾種方式可讓您在沒有中斷連線的情況下重新連線，就是在 SignalR 中使用 "connection" 這個字。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 連接、傳輸連線和實體連線

本文將會區分 *SignalR 連接*、 *傳輸*連線和 *實體*連線：

- **SignalR 連接** 是指用戶端和伺服器 URL 之間的邏輯關聯性，由 SignalR API 維護，並且以連接識別碼唯一識別。 有關此關聯性的資料是由 SignalR 維護，並且用來建立傳輸連接。 當用戶端呼叫方法時，關聯性的 end 和 SignalR 會處置資料，當 `Stop` SignalR 嘗試重新建立遺失的傳輸連線時，就會達到超時限制。
- **傳輸連接** 是指用戶端與伺服器之間的邏輯關聯性，由四種傳輸 api 的其中一種來維護： websocket、伺服器傳送事件、永久框架或長輪詢。 SignalR 會使用傳輸 API 來建立傳輸連線，而傳輸 API 則取決於實體網路連接是否存在，以建立傳輸連線。 傳輸連線會在 SignalR 終止時結束，或在傳輸 API 偵測到實體連接中斷時結束。
- **實體** 連線指的是可加速用戶端電腦與伺服器電腦之間通訊的實體網路連結（電線、無線信號、路由器等）。 必須要有實體連線才能建立傳輸連線，而且必須建立傳輸連線才能建立 SignalR 連接。 不過，中斷實體連線不一定會立即結束傳輸連線或 SignalR 連接，如本主題稍後所述。

在下圖中，SignalR 連線由中樞 API 和 PersistentConnection API SignalR 層代表，傳輸層會以傳輸層表示，而實體連線則是以伺服器和用戶端之間的程式列來表示。

![SignalR 架構圖表](handling-connection-lifetime-events/_static/image1.png)

當您 `Start` 在 SignalR 用戶端中呼叫方法時，您會提供 SignalR 用戶端程式代碼，以建立與伺服器的實體連接所需的所有資訊。 SignalR 用戶端程式代碼會使用這項資訊來提出 HTTP 要求，並建立使用四種傳輸方法之一的實體連接。 如果傳輸連接失敗或伺服器失敗，SignalR 連線將不會立即消失，因為用戶端仍具有自動重新建立與相同 SignalR URL 的新傳輸連線所需的資訊。 在此案例中，不會涉及使用者應用程式的介入，而且當 SignalR 用戶端程式代碼建立新的傳輸連線時，不會啟動新的 SignalR 連接。 SignalR 連接的持續性反映在您呼叫方法時所建立的連接識別碼 `Start` 不會變更。

`OnReconnected`當傳輸連接在遺失之後自動重新建立時，中樞上的事件處理常式會執行。 `OnDisconnected`事件處理常式會在 SignalR 連接結束時執行。 SignalR 連接可以下列任何一種方式結束：

- 如果用戶端呼叫 `Stop` 方法，則會將停止訊息傳送至伺服器，而且用戶端和伺服器都會立即結束 SignalR 連接。
- 用戶端與伺服器之間的連線中斷之後，用戶端會嘗試重新連線，而且伺服器會等候用戶端重新連線。 如果嘗試重新連接失敗，而且中斷連接逾時期間結束，則用戶端和伺服器都會結束 SignalR 連接。 用戶端會停止嘗試重新連接，而伺服器會處置其 SignalR 連接的表示。
- 如果用戶端在沒有機會呼叫方法的情況下停止 `Stop` 執行，伺服器會等候用戶端重新連接，然後在中斷連接逾時時間之後結束 SignalR 連線。
- 如果伺服器停止執行，用戶端會嘗試重新連線 (重新建立傳輸連線) ，然後在中斷連線超時時間後結束 SignalR 連接。

如果沒有連線問題，而且使用者應用程式藉由呼叫方法來結束 SignalR 連接 `Stop` ，則 SignalR 連接和傳輸連接會在大約相同的時間開始和結束。 下列各節會更詳細地說明其他案例。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>傳輸中斷連接案例

實體連線可能很慢，或連線可能會中斷。 根據不同的因素，例如中斷的長度，可能會卸載傳輸連接。 SignalR 接著會嘗試重新建立傳輸連接。 有時傳輸連線 API 會偵測到中斷並卸載傳輸連線，而 SignalR 會立即發現連接中斷。 在其他案例中，傳輸連線 API 或 SignalR 都不會立即察覺連線已遺失。 對於長時間輪詢以外的所有傳輸，SignalR 用戶端會使用稱為 *keepalive* 的函式來檢查傳輸 API 無法偵測到的連線中斷。 如需長時間輪詢連接的詳細資訊，請參閱本主題稍後的「 [Timeout 和 keepalive」設定](#timeoutkeepalive) 。

當連線處於非使用中狀態時，伺服器會定期將 keepalive 封包傳送給用戶端。 在撰寫本文的日期起，預設頻率為每隔10秒。 藉由接聽這些封包，用戶端可以分辨是否有連線問題。 如果未在預期的情況下收到 keepalive 封包，則在一小段時間之後，用戶端會假設發生連線問題，例如緩慢或中斷。 如果持續時間超過一段時間後仍未收到，用戶端會假設連接已中斷，並開始嘗試重新連接。

下圖說明當傳輸 API 無法立即辨識的實體連線發生問題時，在一般案例中引發的用戶端和伺服器事件。 此圖表適用于下列狀況：

- 傳輸為 Websocket、永久框架或伺服器傳送的事件。
- 實體網路連線中有不同的停機時間。
- 傳輸 API 不會察覺到中斷，所以 SignalR 會依賴 keepalive 功能來偵測它們。

![傳輸中斷連線](handling-connection-lifetime-events/_static/image2.png)

如果用戶端進入重新連線模式，但無法在中斷連接逾時限制內建立傳輸連線，伺服器就會終止 SignalR 連接。 發生這種情況時，伺服器會執行中樞的 `OnDisconnected` 方法，並將中斷連線的訊息排入佇列，以在用戶端管理稍後連線時傳送給用戶端。 如果用戶端接著重新連接，則會接收中斷連接命令，並呼叫 `Stop` 方法。 在此情況下， `OnReconnected` 不會在用戶端重新連線時執行，而且在 `OnDisconnected` 用戶端呼叫時不會執行 `Stop` 。 下圖說明此案例。

![傳輸中斷-伺服器超時](handling-connection-lifetime-events/_static/image3.png)

可能會在用戶端上引發的 SignalR 連接存留期事件如下：

- `ConnectionSlow` 用戶端事件。

    在收到上一個訊息或 keepalive 偵測後經過的預設持續時間（keepalive）時間比例時引發。 預設的持續時間警告期間是持續時間的2/3。 Keepalive timeout 為20秒，因此警告大約會出現13秒。

    根據預設，伺服器每隔10秒就會傳送一次持續性偵測，而用戶端會每隔2秒檢查一次 keepalive ping， (keepalive timeout 值與 keepalive timeout 警告值) 之間的第三個差異。

    如果傳輸 API 會察覺到中斷連線，則在持續性超時警告期間之前，SignalR 可能會收到中斷連接的通知。 在此情況下， `ConnectionSlow` 不會引發事件，而 SignalR 會直接進入 `Reconnecting` 事件。
- `Reconnecting` 用戶端事件。

    當 () 傳輸 API 偵測到連接遺失時引發，或 (b) 在收到最後一個訊息或 keepalive 偵測之後，已超過持續時間長度。 SignalR 用戶端程式代碼會開始嘗試重新連接。 如果您希望應用程式在傳輸連線遺失時採取一些動作，您可以處理這個事件。 預設 keepalive timeout 期限目前為20秒。

    如果您的用戶端程式代碼在 SignalR 處於重新連接模式時嘗試呼叫中樞方法，SignalR 將會嘗試傳送命令。 大部分的情況下，這類嘗試將會失敗，但在某些情況下，可能會成功。 針對伺服器傳送的事件、永遠框架和長時間輪詢傳輸，SignalR 會使用兩個通道，用戶端會使用這兩個通道來傳送訊息，而另一個通道用來接收訊息。 用來接收的通道是永久開啟的通道，也就是實體連接中斷時所關閉的通道。 用於傳送的通道仍可供使用，因此，如果已還原實體連接，則從用戶端到伺服器的方法呼叫可能會成功，然後才會重新建立接收通道。 在 SignalR 重新開啟用於接收的通道之前，將不會收到傳回值。
- `Reconnected` 用戶端事件。

    重新建立傳輸連接時引發。 `OnReconnected`中樞內的事件處理常式會執行。
- `Closed``disconnected`JavaScript) 中的用戶端事件 (事件。

    當 SignalR 用戶端程式代碼在遺失傳輸連線之後嘗試重新連接時，在中斷連接逾時期間過期時引發。 預設的中斷連接逾時為30秒。  (當連接結束時，也會引發此事件，因為 `Stop` 呼叫方法。 ) 

傳輸 API 未偵測到傳輸連接中斷，且不會延遲伺服器的持續性偵測超過 keepalive 超時警告期間，可能不會引發任何連接存留期事件。

有些網路環境刻意關閉閒置的連線，而 keepalive 封包的另一項功能是，藉由讓這些網路知道 SignalR 連線正在使用中，來協助防止這種情況。 在極端情況下，keepalive 偵測的預設頻率可能不足以防止關閉連接。 在這種情況下，您可以設定讓 keepalive ping 更頻繁地傳送。 如需詳細資訊，請參閱本主題稍後的「 [Timeout 和 keepalive」設定](#timeoutkeepalive) 。

> [!NOTE]
>
> **重要**：不保證此處所述的事件順序。 SignalR 會根據此配置，以可預測的方式讓每次嘗試引發連接存留期事件，但有許多不同的網路事件變化，以及許多基礎通訊架構（例如傳輸 Api）處理這些事件的方式。 例如， `Reconnected` 當用戶端重新連接時，可能不會引發事件，或是 `OnConnected` 當嘗試建立連接失敗時，伺服器上的處理常式可能會執行。 本主題只會說明通常會由特定一般情況產生的效果。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>用戶端中斷連接案例

在瀏覽器用戶端中，維護 SignalR 連接的 SignalR 用戶端程式代碼會在網頁的 JavaScript 內容中執行。 這就是為什麼當您從某個頁面流覽至另一個頁面時，SignalR 連接必須結束的原因，因此，如果您從多個瀏覽器視窗或索引標籤連線，就會有多個連接識別碼的連接。 當使用者關閉瀏覽器視窗或索引標籤，或流覽至新頁面或重新整理頁面時，SignalR 連接會立即結束，因為 SignalR 用戶端程式代碼會為您處理該瀏覽器事件，並呼叫 `Stop` 方法。 在這些情況下，或在任何用戶端平臺中，當您的應用程式呼叫 `Stop` 方法時， `OnDisconnected` 事件處理常式會在伺服器上立即執行，而且用戶端 `Closed` 會引發事件 (事件是 `disconnected` 以 JavaScript) 命名。

如果用戶端應用程式或其執行的電腦損毀或進入睡眠 (例如，當使用者關閉膝上型電腦) 時，不會通知伺服器發生什麼事。 在伺服器知道的情況下，用戶端可能會因為連線中斷而遺失，而用戶端可能會嘗試重新連線。 因此，在這些情況下，伺服器會等候用戶端重新連線，而且 `OnDisconnected` 在中斷連接逾時期間到期之前 (大約30秒) 。 下圖說明此案例。

![用戶端電腦失敗](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>伺服器中斷連接案例

當伺服器離線時，它會重新開機、失敗、應用程式網域回收等等。--結果可能類似于遺失的連接，或者傳輸 API 和 SignalR 可能會立即知道伺服器已消失，而且 SignalR 可能會開始嘗試重新連接，而不會引發 `ConnectionSlow` 事件。 如果用戶端進入重新連接模式，而且伺服器復原或重新開機，或在中斷連接逾時期間過期之前讓新的伺服器上線，用戶端會重新連接到已還原的伺服器或新的伺服器。 在此情況下，SignalR 連接會在用戶端上繼續，並 `Reconnected` 引發事件。 在第一部伺服器上，絕對不會 `OnDisconnected` 執行，而且在新的伺服器上， `OnReconnected` 會執行，但在 `OnConnected` 之前從未針對該伺服器上的該用戶端執行。 如果用戶端在重新開機或應用程式網域回收之後重新連線至相同的伺服器， (效果相同，因為當伺服器重新開機時，沒有先前連接活動的記憶體。 ) 下圖假設傳輸 API 會立即察覺遺失的連接，因此 `ConnectionSlow` 不會引發事件。

![伺服器失敗並重新連接](handling-connection-lifetime-events/_static/image5.png)

如果伺服器在中斷連線超時時間內無法使用，SignalR 連接會結束。 在此案例中， `Closed` `disconnected` JavaScript 用戶端) 中的事件 (會在用戶端上引發，但 `OnDisconnected` 永遠不會在伺服器上呼叫。 下圖假設傳輸 API 不會察覺遺失的連接，因此 SignalR 的 keepalive 功能會偵測到它，並 `ConnectionSlow` 引發事件。

![伺服器失敗和超時](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Timeout 和 keepalive 設定

預設 `ConnectionTimeout` 值、 `DisconnectTimeout` 和 `KeepAlive` 值適用于大部分的情況，但如果您的環境具有特殊需求，則可以變更。 例如，如果您的網路環境關閉閒置5秒鐘的連線，您可能必須減少 keepalive 值。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

這項設定代表開啟傳輸連線，並在關閉並開啟新連接之前等候回應的時間長度。 預設值為110秒。

這項設定僅適用于停用 keepalive 功能時，通常僅適用于長時間輪詢傳輸。 下圖說明此設定在長輪詢傳輸連線上的效果。

![長時間輪詢傳輸連接](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

這項設定代表在引發事件之前，在傳輸連線遺失之前等候的時間量 `Disconnected` 。 預設值為 30 秒。 當您設定時 `DisconnectTimeout` ， `KeepAlive` 會自動將值設為 1/3 `DisconnectTimeout` 。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

這項設定代表透過閒置連接傳送 keepalive 封包之前所等待的時間量。 預設值為 10 秒。 此值不得超過1/3 的 `DisconnectTimeout` 值。

如果您想要同時設定 `DisconnectTimeout` 和 `KeepAlive` ，請設定 `KeepAlive` after `DisconnectTimeout` 。 否則， `KeepAlive` 當 `DisconnectTimeout` 自動將 timeout 值設定為1/3 時，將會覆寫您 `KeepAlive` 的設定。

如果您想要停用 keepalive 功能，請設定 `KeepAlive` 為 null。 長期輪詢傳輸會自動停用 Keepalive 功能。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>如何變更 timeout 和 keepalive 設定

若要變更這些設定的預設值，請在 global.asax 檔案中將它們設定 `Application_Start` 為，如下列範例所示。 *Global.asax* 範例程式碼中顯示的值與預設值相同。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>如何通知使用者中斷連線

在某些應用程式中，您可能會想要在發生連線問題時向使用者顯示訊息。 您有數個選項可供您和何時進行。 下列程式碼範例適用于使用所產生之 proxy 的 JavaScript 用戶端。

- 處理 `connectionSlow` 事件，以便在 SignalR 知道連線問題時，立即顯示訊息，然後再進入重新連接模式。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 處理 `reconnecting` 事件，以便在 SignalR 感知中斷連線並進入重新連接模式時顯示訊息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 處理 `disconnected` 事件，以便在重新連接嘗試超時時顯示訊息。在此案例中，重新建立與伺服器之連接的唯一方法，是藉由呼叫方法來重新開機 SignalR 連接 `Start` ，這將會建立新的連接識別碼。 下列程式碼範例會使用旗標，以確保您只會在重新連接逾時之後發出通知，而不是在呼叫方法所造成 SignalR 連接的一般端之後發出通知 `Stop` 。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>如何持續重新連線

在某些應用程式中，您可能會想要在連線遺失之後自動重新建立連線，並將重新連線的嘗試超時。若要這樣做，您可以 `Start` 從事件處理常式中呼叫方法， `Closed` (`disconnected` JavaScript 用戶端上的事件處理常式) 。 在呼叫之前，您可能會想要等候一段時間 `Start` ，以避免在伺服器或實體連線無法使用時，過於頻繁地執行此操作。 下列程式碼範例適用于使用所產生之 proxy 的 JavaScript 用戶端。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

在行動用戶端中可能要注意的問題是，當伺服器或實體連線無法使用時，連續重新連接嘗試可能會造成不必要的電池耗盡。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>如何在伺服器程式碼中中斷用戶端連線

SignalR 第2版沒有內建的伺服器 API 可中斷用戶端連線。 未來會有 [新增此功能的計畫](https://github.com/SignalR/SignalR/issues/2101)。 在目前的 SignalR 版本中，將用戶端與伺服器中斷連線最簡單的方式，就是在用戶端上執行中斷連接方法，並從伺服器呼叫該方法。 下列程式碼範例顯示使用產生的 proxy 之 JavaScript 用戶端的中斷連線方法。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 安全性-此方法不會中斷用戶端的連線，也不會提供建議的內建 API，因為用戶端可以重新連線，或遭到駭客攻擊的程式碼可能會移除 `stopClient` 方法或變更其用途。 執行可設定狀態的拒絕服務 (DOS) 保護的適當位置不在架構或伺服器層，而是在前端基礎結構中。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>偵測中斷連接的原因

SignalR 2.1 會將多載新增至伺服器 `OnDisconnect` 事件，指出用戶端是否刻意中斷連線，而不是超時。 `StopCalled` 如果用戶端明確關閉連接，則此參數為 true。 在 JavaScript 中，如果伺服器錯誤導致用戶端中斷連線，則會將錯誤資訊以形式傳遞給用戶端 `$.connection.hub.lastError` 。

**C # 伺服器程式碼： `stopCalled` 參數**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 用戶端程式代碼： `lastError` 在 `disconnect` 事件中存取。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
