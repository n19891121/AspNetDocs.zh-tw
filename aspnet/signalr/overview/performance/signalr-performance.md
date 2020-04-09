---
uid: signalr/overview/performance/signalr-performance
title: 信號器性能 |微軟文件
author: bradygaster
description: SignalR 效能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676087"
---
# <a name="signalr-performance"></a>SignalR 效能

由[派翠克·弗萊徹](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題介紹如何為 SignalR 應用程式中的設計、測量和改進性能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

有關 SignalR 性能和縮放的最新演示文稿,請參閱[使用ASP.NET訊號R 縮放即時 Web。](https://channel9.msdn.com/Events/Build/2013/3-502)

本主題包含下列幾節：

- [設計考量](#design)
- [調整 SignalR 伺服器的效能](#tuning)
- [針對效能問題進行疑難排解](#troubleshooting)
- [使用訊號R效能計數器](#perfcounters)
- [使用其他效能計數器](#othercounters)
- [其他資源](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>設計考量

本節介紹在設計 SignalR 應用程序期間可以實現的模式,以確保不會因生成不必要的網路流量而妨礙性能。

### <a name="throttling-message-frequency"></a>限制訊息頻率

即使在以高頻率發送消息的應用程式(如即時遊戲應用程式)中,大多數應用程式也不需要每秒發送多條消息。 為了減少每個用戶端生成的流量,可以實現一個消息迴圈,該佇列和發送消息的頻率不會超過固定速率(也就是說,如果該時間間隔內有要發送的消息,每秒最多發送一定數量的消息)。 有關將訊息限制到特定速率(來自用戶端和伺服器)的範例應用程式,請參閱[使用 SignalR 的高頻即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。

### <a name="reducing-message-size"></a>遞減小訊息大小

您可以通過減小序列化物件的大小來減小 SignalR 消息的大小。 在伺服器代碼中,如果發送的物件包含不需要傳輸的屬性,則防止使用`JsonIgnore`屬性 序列化這些屬性。 屬性的名稱也存儲在消息中;可以使用 屬性`JsonProperty`縮短 屬性的名稱。 以下代碼範例展示如何排除屬性傳送到用戶端,以及如何縮短屬性名稱:

**.NET 伺服器代碼,用於展示 JsonIgnore 屬性,以排除傳送到客戶端的資料,以及用於減小消息大小的 JsonProperty 屬性**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

為了在客戶端代碼中保持可讀性/可維護性,在收到消息后,可以將縮寫屬性名稱重新映射到人友好名稱。 以下代碼範例展示了一種透過將縮短的名稱重新映射到較長的名稱的方法,方法是定義消息協定(映射),並使用函數`reMap`將協定應用於優化的消息類:

**用戶端 JavaScript 程式碼會縮短的屬性名稱重新映射到人可讀名稱**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

名稱也可以使用相同的方法在從用戶端到伺服器的電子郵件中縮短。

減少消息物件的記憶體佔用空間(即用於消息的記憶體量)也可以提高性能。 例如,如果不需要全部範圍的,`int`則可以改用`short``byte`或 。

由於郵件存儲在伺服器記憶體中的消息總線中,因此減小消息大小還可以解決伺服器記憶體問題。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>調整 SignalR 伺服器的效能

以下配置設定可用於調整伺服器,以便在 SignalR 應用程式中獲得更好的性能。 有關如何提高ASP.NET應用程式中性能的一般資訊,請參閱[改進ASP.NET性能](https://msdn.microsoft.com/library/ff647787.aspx)。

**訊號R設定設定**

- **默認消息緩衝區大小**:預設情況下,SignalR 每個連接的記憶體中保留 1000 條消息。 如果使用大型消息,則可能會產生記憶體問題,通過減小此值來緩解這些問題。 此設置可以在ASP.NET應用程式中`Application_Start`的事件處理程式中設置,也可以在自託管應用程式中的OWIN啟動類`Configuration`方法中設置。 以下範例展示如何減小此值以減少應用程式的記憶體佔用量,以減少使用的伺服器記憶體量:

    **Startup.cs中,此伺服器代碼,用於減少預設的郵件緩衝區大小**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 設定設定**

- **每個應用程式的最多併發請求**:增加併發 IIS 請求的數量將增加可用於服務請求的伺服器資源。 默認值為 5000;要增加此設定,請在提升的指令提示符中執行以下命令:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **應用程式池佇列長度**:這是 Http.sys 為應用程式池排隊的最大請求數。 佇列已滿時,新請求將收到 503"服務不可用"回應。 預設值為 1000。

    縮短應用程式託管的應用程式池中工作進程的佇列長度將節省記憶體資源。 有關詳細資訊,請參閱[管理、調整和設定應用程式池](https://technet.microsoft.com/library/cc745955.aspx)。

**ASP.NET 設定設定**

本節包括可在檔中設置的`aspnet.config`配置設置。 此檔案位於兩個位置之一,具體取決於平臺:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

可能提高 SignalR 效能ASP.NET設定包括:

- **每個 CPU 的最大併發請求**:增加此設置可能會緩解性能瓶頸。 要增加此設定,向`aspnet.config`檔案新增以下設定設定:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **請求佇列限制**:當連接總數`maxConcurrentRequestsPerCPU`超過 設置時,ASP.NET將使用佇列開始限制請求。 要增加佇列的大小,可以增加`requestQueueLimit`設置。 為此,向中的`processModel``config/machine.config`節點添加以下配置設定(而不是`aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>針對效能問題進行疑難排解

本節介紹查找應用程式中的性能瓶頸的方法。

### <a name="verifying-that-websocket-is-being-used"></a>認證是否正在使用 WebSocket

雖然 SignalR 可以使用各種傳輸在用戶端和伺服器之間通訊,但 WebSocket 具有顯著的性能優勢,如果用戶端和伺服器支援它,則應使用它。 要確定客戶端和伺服器是否滿足 WebSocket 的要求,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。 要確定應用程式中正在使用哪些傳輸,可以使用瀏覽器開發人員工具,並檢查日誌以查看用於連接的傳輸。 有關在 Internet 資源管理員和 Chrome 中使用瀏覽器開發工具的資訊,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>使用訊號R效能計數器

本節介紹如何在`Microsoft.AspNet.SignalR.Utils`封裝中找到的啟用和使用 SignalR 性能計數器。

### <a name="installing-signalrexe"></a>安裝訊號器.exe

可以使用稱為 SignalR.exe 的實用程式將性能計數器添加到伺服器。 要安裝此實用程式,請按照以下步驟操作:

1. 在視覺化工作室中,選擇**工具** > **NuGet 套件管理員** > **管理 NuGet 套件以進行解決方案**
2. 搜尋**信號器.utils,** 然後選擇"安裝"

    ![](signalr-performance/_static/image1.png)
3. 接受安裝包的許可協定。
4. SignalR.exe 將安裝`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`到 。

### <a name="installing-performance-counters-with-signalrexe"></a>使用 SignalR.exe 安裝效能計數器

要安裝 SignalR 效能計數器,請使用以下參數在提升的指令提示符中執行 SignalR.exe:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

要刪除 SignalR 效能計數器,請使用以下參數在提升的指令提示符中執行 SignalR.exe:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>訊號R性能計數器

實用程式包安裝以下性能計數器。 「總計」計數器測量自上次應用程式池或伺服器重新啟動以來的事件數。

**連接計量**

以下指標衡量發生的連接存留期事件。 有關詳細資訊,請參閱[瞭解和處理連線存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

- **連線已連線**
- **連線重新連線**
- **連線已斷線連線**
- **連接電流**

**訊息計量**

以下指標測量 SignalR 生成的消息流量。

- **接收的連線訊息總數**
- **連線訊息傳送總數**
- **已接收/秒的連線訊息**
- **已傳送/秒的連線訊息**

**訊息匯流排**

以下指標測量通過內部 SignalR 消息總線(放置所有傳入和傳出 SignalR 消息的佇列)的流量。 訊息在傳送或廣播時**已發布**。 此上下文中的**訂閱伺服器**是消息總線上的訂閱;這應該等於用戶端數加上伺服器本身。 **已分配的工作線程**是將數據發送到活動連接的元件;**忙工作人員**是主動發送消息的工作人員。

- **接收到的訊息總線訊息**
- **收到/秒的消息總線訊息**
- **訊息總線訊息已發佈總計**
- **已發佈/秒的消息總線訊息**
- **訊息總線訂閱伺服器目前**
- **訊息總線訂閱者總計**
- **訊息總線訂閱者/秒**
- **訊息總線配置工作**
- **消息總線忙工作人員**
- **郵件匯流主題目前**

**錯誤指標**

以下指標測量由 SignalR 消息流量生成的錯誤。 當無法解析中心或中心方法時,就會發生**中心解析**錯誤。 **中心調用**錯誤是在調用集線器方法時引發的異常。 **傳輸**錯誤是在 HTTP 請求或回應期間引發的連接錯誤。

- **錯誤:全部總計**
- **錯誤:所有/秒**
- **錯誤:中心解析度總計**
- **錯誤:集線器解析度/秒**
- **錯誤:集線器呼叫總計**
- **錯誤:集線器呼叫/秒**
- **錯誤:傳輸總計**
- **錯誤:傳輸/秒**

<a id="scaleout_metrics"></a>

**橫向延伸指標**

以下指標衡量橫向擴展提供程式生成的流量和錯誤。 此上下文中的**流**是橫向擴展提供程式使用的縮放單位;如果使用 SQL Server,則這是表;使用服務總線時的主題;如果使用 Redis,則為訂閱。 每個流確保有序的讀取和寫入操作;單個流是潛在的規模瓶頸,因此可以增加流的數量,以幫助減少該瓶頸。 如果使用多個流,SignalR 將自動在這些流中分發(分片)消息,以確保從任何給定連接發送的消息按順序排列。

["最大佇列長度](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)"設置控制 SignalR 維護的橫向擴展發送佇列的長度。 將其設置為大於 0 的值將使發送佇列中的所有消息一次發送到配置的消息背板。 如果佇列的大小高於配置的長度,則後續發送的呼叫將立即失敗,使用[InvalidTheAa,](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)直到佇列中的消息數再次小於設置。 默認情況下禁用排隊,因為實現的背板通常有自己的佇列或流控制。 對於 SQL Server,連接池有效地限制了任何一次進行發送的次數。

預設情況下,只有一個流用於 SQL Server 和 Redis,五個流用於服務總線,並且禁用排隊,但這些設置可以通過 SQL Server 和服務總線上的配置更改:

**.NET 伺服器代碼,用於設定 SQL Server 背板的表計數和佇列長度**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**.NET 伺服器代碼,用於設定服務總線背板的主題計數和佇列長度**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**緩衝**流是已進入錯誤狀態的流流;當流處於故障狀態時,發送到背板的所有消息將立即失敗,直到流不再出現故障。 **發送佇列長度**是已過帳但尚未發送的郵件數。

- **已接收/秒的橫向延伸訊息匯流排訊息**
- **橫向延伸流總計**
- **展開延伸流**
- **橫向延伸流緩衝**
- **橫向延伸錯誤總計**
- **橫向延伸錯誤/秒**
- **橫向延伸傳送佇列長度**

有關這些計數器正在測量的內容的詳細資訊,請參閱[使用 Azure 服務匯流排進行訊號 R 橫向擴展](scaleout-with-windows-azure-service-bus.md)。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>使用其他效能計數器

以下性能計數器在監視應用程式的性能時可能也很有用。

**記憶體**

- .NET CLR\\記憶體 = 所有堆中的位元組(對於 w3wp)

**ASP.NET**

- ASP.NET_請求目前
- ASP.NET_已排隊
- ASP.NET_已拒絕

**Cpu**

- 處理器資訊+處理器時間

**TCP/IP**

- TCPv6/已建立連線
- TCPv4/已建立連線

**網路服務**

- Web 服務\目前連線
- Web 服務= 最大連線

**執行緒**

- .NET CLR\\鎖 與緒執行線執行程式 。
- .NET CLR\\鎖 與緒執行線... # 目前的實體線程

<a id="otherresources"></a>

## <a name="other-resources"></a>其他資源

有關ASP.NET性能監視和調優的詳細資訊,請參閱以下主題:

- [ASP.NET 效能概觀](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [iIS 7.5、IIS 7.0 和IIS6.0上的ASP.NET線程使用方式](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;應用程式池&gt;元素(Web 設定)](https://msdn.microsoft.com/library/dd560842.aspx)
