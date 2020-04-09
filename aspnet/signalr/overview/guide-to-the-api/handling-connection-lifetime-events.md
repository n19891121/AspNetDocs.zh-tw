---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 理解和處理信號R中的連接壽命事件 |微軟文件
author: bradygaster
description: 本文介紹如何使用中心 API 公開的事件。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676213"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>了解及處理 SignalR 的連線存留期事件

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文概述了可以處理的 SignalR 連接、重新連接和斷開連接事件,以及可以配置的超時和保持活動設置。
>
> 本文假定您已經對 SignalR 和連接存留期事件有所瞭解。 有關信號R 的介紹,請參閱[信號R 簡介](../getting-started/introduction-to-signalr.md)。 有關連接存留期事件的清單,請參閱以下資源:
>
> - [如何處理集線器類別的連線存留期事件](hubs-api-guide-server.md#connectionlifetime)
> - [如何處理 JavaScript 用戶端的連線存留期事件](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [如何處理 .NET 用戶端的連線存留期事件](hubs-api-guide-net-client.md#connectionlifetime)
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

本文包含下列各節：

- [連線存留期的術語和機制](#terminology)

    - [訊號R連線、傳輸連線和物理連線](#signalrvstransport)
    - [傳輸斷線連接](#transportdisconnect)
    - [用戶端斷線連接機制](#clientdisconnect)
    - [伺服器斷線連接機制](#serverdisconnect)
- [逾時與保持活動設定](#timeoutkeepalive)

    - [連線逾時](#connectiontimeout)
    - [離線逾時](#disconnecttimeout)
    - [保持活力](#keepalive)
    - [如何變更逾時並保持活動設定](#changetimeout)
- [如何通知使用者斷線連線](#notifydisconnect)
- [如何持續重新連線](#continuousreconnect)
- [如何在伺服器代碼中斷開客戶端](#disconnectclientfromserver)
- [偵測斷連線的原因](#detectingreasonfordisconnection)

指向 API 參考主題的連結指向 API 的 .NET 4.5 版本。 如果使用 .NET 4,請參閱[API 主題的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>連線存留期的術語和機制

SignalR Hub`OnReconnected`中的事件處理程式可以直接在給`OnConnected`定用戶端`OnDisconnected`之後執行, 但不能在之後執行。 在沒有斷開連接的情況下進行重新連接的原因是,在 SignalR 中使用"連接"一詞有多種方式。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>訊號R連線、傳輸連線和物理連線

本文將區分*SignalR 連線*,*傳輸連線*與*物理連線*:

- **SignalR 連接**是指用戶端和伺服器 URL 之間的邏輯關係,由 SignalR API 維護,並由連接 ID 唯一標識。 有關此關係的數據由 SignalR 維護,用於建立傳輸連接。 當用戶端調用`Stop`方法或達到超時限制時,當 SignalR 嘗試重新建立丟失的傳輸連接時,關係結束,SignalR 會釋放數據。
- **傳輸連接**是指用戶端和伺服器之間的邏輯關係,由四個傳輸 API 之一維護:WebSockets、伺服器發送的事件、永久幀或長輪詢。 SignalR 使用傳輸 API 創建傳輸連接,傳輸 API 取決於物理網路連接的存在來創建傳輸連接。 當 SignalR 終止傳輸連接或傳輸 API 檢測到物理連接斷開時,傳輸連接將結束。
- **物理連接**是指促進用戶端計算機與伺服器計算機之間通信的實體網路鏈路(電線、無線信號、路由器等)。 物理連接必須存在才能建立傳輸連接,並且必須建立傳輸連接才能建立 SignalR 連接。 但是,中斷物理連接並不總是會立即結束傳輸連接或 SignalR 連接,本主題稍後將對此進行說明。

在下圖中,SignalR 連接由集線器 API 和持久連接 API SignalR 層表示,傳輸連接由傳輸層表示,物理連接由伺服器和用戶端之間的線表示。

![訊號R架構圖](handling-connection-lifetime-events/_static/image1.png)

在 SignalR`Start`用戶端中呼叫 該方法時,您提供 SignalR 用戶端代碼,並提供它所需的所有資訊,以便建立與伺服器的物理連接。 SignalR 用戶端代碼使用此資訊發出 HTTP 請求,並建立使用四種傳輸方法之一的物理連接。 如果傳輸連接失敗或伺服器發生故障,SignalR 連接不會立即消失,因為用戶端仍然擁有自動重新建立到同一 SignalR URL 的新傳輸連接所需的資訊。 在這種情況下,不涉及來自使用者應用程式的干預,當 SignalR 用戶端代碼建立新的傳輸連接時,它不會啟動新的 SignalR 連接。 SignalR 連接的連續性反映在這樣一個事實中:在調`Start`用 方法時創建的連接 ID 不會更改。

當`OnReconnected`傳輸連接在丟失後自動重新建立時,中心上的事件處理程式將執行。 事件`OnDisconnected`處理程式在 SignalR 連接的末尾執行。 SignalR 連線可以以以下任何方式結束:

- 如果用戶端呼叫方法`Stop`,將停止訊息將發送到伺服器,並且客戶端和伺服器都會立即終止 SignalR 連接。
- 用戶端和伺服器之間的連接丟失後,用戶端將嘗試重新連接,並且伺服器等待用戶端重新連接。 如果重新連接的嘗試不成功,並且斷開連接超時期結束,則用戶端和伺服器都終止 SignalR 連接。 用戶端停止嘗試重新連接,伺服器將釋放其 SignalR 連接的表示形式。
- 如果用戶端停止運行而沒有機會調用`Stop`該方法,伺服器將等待用戶端重新連接,然後在斷開連接超時期后結束 SignalR 連接。
- 如果伺服器停止運行,用戶端將嘗試重新連接(重新建立傳輸連接),然後在斷開連接超時期間後結束 SignalR 連接。

當沒有連接問題時,並且使用者應用程式通過調用`Stop`該方法結束 SignalR 連接時,SignalR 連接和傳輸連接大約在同一時間開始和結束。 以下各節將更詳細地介紹其他方案。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>傳輸斷線連接

物理連接可能很慢,或者連接可能有中斷。 根據中斷長度等因素,可能會斷開傳輸連接。 然後,SignalR 嘗試重新建立傳輸連接。 有時傳輸連接 API 檢測到中斷並丟棄傳輸連接,SignalR 會立即發現連接丟失。 在其他情況下,傳輸連接 API 和 SignalR 都不會立即意識到連接已丟失。 對於除長輪詢之外的所有傳輸,SignalR 用戶端使用名為 *"保持活動"* 的函數來檢查傳輸 API 無法檢測到的連接損失。 有關長輪詢連接的資訊,請參閱本主題後面的[超時和保持活動設定](#timeoutkeepalive)。

當連接處於非活動狀態時,伺服器會定期向客戶端發送保持活動數據包。 截至撰寫本文之日,默認頻率為每 10 秒一次。 通過偵聽這些數據包,用戶端可以判斷是否有連接問題。 如果預期時未收到保持活動數據包,則在短時間內用戶端假定存在連接問題,如速度緩慢或中斷。 如果長時間后仍未收到保持活動,則用戶端假定連接已斷開,並開始嘗試重新連接。

下圖說明了在典型方案中在傳輸 API 無法立即識別的物理連接出現問題時引發的用戶端和伺服器事件。 該圖適用於以下情況:

- 傳輸是 WebSocket、永久幀或伺服器發送的事件。
- 物理網路連接中斷的時間各不相同。
- 傳輸 API 不會意識到中斷,因此 SignalR 依賴於保持狀態功能來檢測中斷。

![傳輸斷線](handling-connection-lifetime-events/_static/image2.png)

如果用戶端進入重新連接模式,但無法在斷開連接超時限制內建立傳輸連接,伺服器將終止 SignalR 連接。 發生這種情況時,伺服器將執行 Hub`OnDisconnected`的方法,並排隊將斷開連接消息發送到用戶端,以防用戶端以後設法連接。 如果客戶端隨後重新連接,它將接收斷開連接命令並調`Stop`用 方法。 在這種情況下,`OnReconnected`在用戶端重新連接時不執行,`OnDisconnected`並且在用戶端調`Stop`用 時不執行。 下圖說明了此方案。

![傳輸中斷 - 伺服器逾時](handling-connection-lifetime-events/_static/image3.png)

可能在用戶端上引發的 SignalR 連接存留期事件如下:

- `ConnectionSlow`用戶端事件。

    自收到最後一條消息或保持活 ping 以來,保持活動超時的預設比例已過時引發。 默認保持活動超時警告週期為保持活動超時的 2/3。 保持活動超時為 20 秒,因此警告在大約 13 秒時發生。

    默認情況下,伺服器每 10 秒發送一次保持活動 ping,客戶端大約每 2 秒檢查一次保持活動 ping(保持活動超時值和保持活動超時警告值之間的三分之一差異)。

    如果傳輸 API 意識到斷開連接,則在保持活動超時警告期之前,可能會通知 SignalR 斷開連接。 在這種情況下,`ConnectionSlow`將不會引發該事件,SignalR 將直接轉`Reconnecting`到該 事件。
- `Reconnecting`用戶端事件。

    當 (a) 傳輸 API 檢測到連接丟失,或 (b) 自上次收到消息或保持活動 ping 以來,保持活動超時期已過。 SignalR 用戶端代碼開始嘗試重新連接。 如果您希望應用程式在傳輸連接丟失時執行某些操作,則可以處理此事件。 預設保持活動超時期限當前為 20 秒。

    如果用戶端代碼嘗試在 SignalR 處於重新連接模式時調用 Hub 方法,SignalR 將嘗試發送命令。 大多數時候,這種嘗試會失敗,但在某些情況下,它們可能會成功。 對於伺服器發送的事件、永久幀和長輪詢傳輸,SignalR 使用兩個通信通道,一個通信通道是用戶端用於發送消息的,另一個用於接收消息。 用於接收的通道是永久打開的通道,在物理連接中斷時,該通道將關閉。 用於發送的通道仍然可用,因此,如果恢復物理連接,則在重新建立接收通道之前,用戶端到伺服器的方法調用可能成功。 在 SignalR 重新打開用於接收的通道之前,不會接收返回值。
- `Reconnected`用戶端事件。

    重新建立傳輸連接時引發。 中心`OnReconnected`中的事件處理程序執行。
- `Closed`用戶端事件(JAVAScript`disconnected`中的事件)。

    當斷開連接超時期到期時,當 SignalR 用戶端代碼在丟失傳輸連接後嘗試重新連接時引發。 默認斷開連接超時為 30 秒。 (當連接結束時,也會引發此事件,`Stop`因為呼叫該方法。

傳輸 API 未偵測到的傳輸連接中斷,並且不會延遲伺服器中保持活動 ping 的接收時間超過保持活動超時警告期的時間,則可能導致引發任何連接存留期事件。

某些網路環境有意關閉空閒連接,保持狀態數據包的另一個功能是通過讓這些網路知道 SignalR 連接正在使用來説明防止這種情況。 在極端情況下,保持活值的默認頻率可能不足以阻止關閉連接。 在這種情況下,您可以將保持活動 ping 配置為更頻繁地發送。 有關詳細資訊,請參閱本主題後面的[超時和保持活動設定](#timeoutkeepalive)。

> [!NOTE]
>
> **重要提示**:此處描述的事件序列不保證。 根據此方案,SignalR 會嘗試以可預測的方式引發連接存留期事件,但網路事件有許多變化,以及傳輸 API 等基礎通訊框架處理這些事件的許多方式。 例如,用戶端重新`Reconnected`連接時可能不會引發該事件,或者當嘗試建立連接失敗`OnConnected`時,伺服器上的處理程式可能會運行。 本主題僅描述通常由某些典型情況產生的影響。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>用戶端斷線連接機制

在瀏覽器用戶端中,維護 SignalR 連接的 SignalR 用戶端代碼在網頁的 JavaScript 上下文中運行。 這就是為什麼當您從一個頁面導航到另一個頁面時,SignalR 連接必須結束,這就是為什麼如果您從多個瀏覽器視窗或選項卡連接時,您有多個連接與多個連接指示。 當使用者關閉瀏覽器視窗或選項卡,或導航到新頁面或刷新頁面時,SignalR 連接將立即結束,因為 SignalR 用戶端代碼會為您處理該瀏覽器事件`Stop`並調用 該方法。 在這些情況下,或者在應用程式`Stop`呼叫方法時的任何用戶端平臺中`OnDisconnected`, 事件處理程式會立即在伺服器上執行,並且`Closed`客戶端引發事件(事件在 JAvaScript`disconnected`中命名)。

如果用戶端應用程式或運行在崩潰時運行的電腦崩潰或進入睡眠狀態(例如,當使用者關閉便攜式計算機時),伺服器不會被告知發生了什麼。 據伺服器所知,用戶端丟失可能是由於連接中斷,用戶端可能嘗試重新連接。 因此,在這些情況下,伺服器等待給用戶端重新連接的機會,並且`OnDisconnected`在斷開連接超時期到期之前不會執行(預設情況下約為 30 秒)。 下圖說明了此方案。

![用戶端電腦故障](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>伺服器斷線連接機制

當伺服器離線時 (它重新啟動、 失敗、 應用域回收等 ) 結果可能類似於遺失的連接,或者傳輸 API 和 SignalR 可能立即知道伺服器已消失,SignalR 可能開始嘗試重新連線而不引發`ConnectionSlow`事件。 如果用戶端進入重新連接模式,並且伺服器恢復或重新啟動,或者新伺服器在斷開連接超時期到期之前連線,則客戶端將重新連接到已還原或新伺服器。 在這種情況下,SignalR 連接將繼續在用戶端上`Reconnected`, 並引發事件。 在第一台伺服器上,`OnDisconnected`從不執行,在新伺服器上執行`OnReconnected`,`OnConnected`儘管 以前從未為該伺服器上的用戶端執行過。 (如果用戶端在重新啟動或應用域回收后重新連接到同一伺服器,則效果相同,因為當伺服器重新啟動時,它沒有以前連接活動的記憶體。下圖假定傳輸 API 會立即意識到丟失的連接,`ConnectionSlow`因此不會引發 事件。

![伺服器容錯並重新連線](handling-connection-lifetime-events/_static/image5.png)

如果伺服器在斷開連接超時期間不可用,SignalR 連接將結束。 在這種情況下,事件`Closed`(`disconnected`在 JAvaScript 用戶端中)在用戶端上引發,`OnDisconnected`但從未在伺服器上調用。 下圖假定傳輸 API 不會意識到丟失的連接,因此 SignalR 保持`ConnectionSlow`活動功能檢測到該 事件並引發事件。

![伺服器故障和逾時](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>逾時與保持活動設定

預設`ConnectionTimeout`的`DisconnectTimeout`和`KeepAlive`值適用於大多數方案,但如果環境有特殊需要,則可以更改。 例如,如果網路環境關閉空閒 5 秒的連接,則可能必須減小保持活動值。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

此設定表示在關閉傳輸連接和打開新連接之前保持傳輸連接打開並等待回應的時間量。 默認值為 110 秒。

此設置僅在禁用保持活動功能時適用,這通常僅適用於長輪詢傳輸。 下圖說明了此設置對長輪詢傳輸連接的影響。

![長輪詢傳輸連線](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>離線逾時

此設置表示引發`Disconnected`事件之前傳輸連接丟失後等待的時間量。 預設值為 30 秒。 設定時`DisconnectTimeout`,`KeepAlive`將自動設定為值`DisconnectTimeout`的 1/3。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

此設置表示在通過空閒連接發送保持活動數據包之前等待的時間量。 預設值為 10 秒。 此值不能超過該值的`DisconnectTimeout`1/3。

`DisconnectTimeout`如果要設定與`KeepAlive`,則`KeepAlive`設定為`DisconnectTimeout`。 否則,`KeepAlive`當自動設置`KeepAlive`為 超時`DisconnectTimeout`值的 1/3 時,您的設置將被覆蓋。

如果要關閉保持活動功能,請設定為`KeepAlive`null。 對於長輪詢傳輸,將自動禁用保持活動功能。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>如何變更逾時並保持活動設定

要更改這些設定的預設值,請將其設置在`Application_Start` *Global.asax*檔中,如以下範例所示。 範例代碼中顯示的值與預設值相同。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>如何通知使用者斷線連線

在某些應用程式中,您可能希望在存在連接問題時向用戶顯示消息。 對於如何以及何時執行此操作,您有多種選擇。 以下代碼示例適用於使用生成的代理的 JavaScript 用戶端。

- 在`connectionSlow`SignalR 意識到連接問題後,在事件進入重新連接模式時,立即處理該事件以顯示消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 當`reconnecting`SignalR 意識到斷開並進入重新連接模式時,處理事件以顯示消息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 當嘗試`disconnected`重新連接超時時,處理事件以顯示消息。在這種情況下,再次與伺服器重新建立連接的唯一方法是透過調用`Start`方法重新啟動 SignalR 連接,這將創建新的連接 ID。 以下代碼示例使用標誌來確保僅在重新連接超時後發出通知,而不是在調用`Stop`方法導致的 SignalR 連接的正常結束之後發出通知。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>如何持續重新連線

在某些應用程式中,您可能希望在連接丟失且重新連接嘗試超時後自動重新建立連接。為此,可以從`Start``Closed`事件處理程式(JAvaScript`disconnected`用戶端上的事件處理程式)調用方法。 您可能需要在調用`Start`之前等待一段時間,以避免在伺服器或物理連接不可用時過於頻繁地執行此操作。 以下代碼示例適用於使用生成的代理的 JavaScript 用戶端。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

在移動用戶端中需要注意的一個潛在問題是,當伺服器或物理連接不可用時,連續重新連接嘗試可能會導致不必要的電池耗盡。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>如何在伺服器代碼中斷開客戶端

SignalR 版本 2 沒有用於斷開用戶端的內建伺服器 API。 有[計劃在未來新增此功能](https://github.com/SignalR/SignalR/issues/2101)。 在當前 SignalR 版本中,將用戶端與伺服器斷開連接的最簡單方法是在用戶端上實現斷開連接方法,並從伺服器調用該方法。 以下代碼示例顯示了使用生成的代理的 JavaScript 客戶端的斷開連接方法。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 安全性 - 此連接用戶端的方法和建議的內置 API 都不會解決運行惡意代碼的受駭客攻擊的用戶端的情況,因為用戶端可以重新連接,或者被駭客攻擊`stopClient`的代碼可能會刪除 該方法或更改它的作用。 實現有狀態拒絕服務 (DOS) 保護的適當位置不在框架或伺服器層中,而是在前端基礎結構中。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>偵測斷連線的原因

SignalR 2.1`OnDisconnect`向伺服器 事件添加重載,指示用戶端是否有意斷開連接,而不是超時。如果`StopCalled`客戶端顯示式關閉連接,則參數為 true。 在 JavaScript 中,如果伺服器錯誤導致客戶端斷線連接,則錯誤資訊將作為`$.connection.hub.lastError`傳遞給用戶端 。

**C# 伺服器`stopCalled`代碼 :參數**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 客戶端代碼`lastError``disconnect`:在 事件中訪問。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
