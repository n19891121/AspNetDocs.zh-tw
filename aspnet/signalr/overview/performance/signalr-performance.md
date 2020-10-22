---
uid: signalr/overview/performance/signalr-performance
title: SignalR 效能 |Microsoft Docs
author: bradygaster
description: SignalR 效能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345277"
---
# <a name="signalr-performance"></a>SignalR 效能

依 [派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題說明如何在 SignalR 應用程式中設計、測量及改善效能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

如需有關 SignalR 效能和調整的最新簡報，請參閱 [使用 ASP.NET SignalR 調整即時 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。

本主題包含下列幾節：

- [設計考量](#design)
- [調整 SignalR 伺服器的效能](#tuning)
- [針對效能問題進行疑難排解](#troubleshooting)
- [使用 SignalR 效能計數器](#perfcounters)
- [使用其他效能計數器](#othercounters)
- [其他資源](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>設計考量

本節說明可在設計 SignalR 應用程式期間執行的模式，以確保不會產生不必要的網路流量來妨礙運作效能。

### <a name="throttling-message-frequency"></a>節流訊息頻率

即使是在以高頻率傳送訊息的應用程式中 (例如即時遊戲應用程式) ，大部分的應用程式都不需要一次傳送多則訊息。 若要減少每個用戶端產生的流量數量，可以將訊息迴圈實作為佇列，並將訊息傳送出去，而不是固定的速率 (也就是，如果時間間隔中有訊息要傳送) ，則會每秒傳送一次訊息。 如需將訊息從用戶端和伺服器)  (的特定速率的範例應用程式，請參閱 [使用 SignalR 的高頻率即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。

### <a name="reducing-message-size"></a>減少訊息大小

您可以藉由減少序列化物件的大小來縮減 SignalR 訊息的大小。 在 [伺服器程式碼] 中，如果您要傳送的物件包含不需要傳送的屬性，請使用屬性防止這些屬性進行序列化 `JsonIgnore` 。 屬性的名稱也會儲存在訊息中;您可以使用屬性來縮短屬性的名稱 `JsonProperty` 。 下列程式碼範例將示範如何將屬性排除傳送給用戶端，以及如何縮短屬性名稱：

**示範 JsonIgnore 屬性以排除將資料傳送給用戶端的 .NET server 程式碼，以及用來縮減訊息大小的 >jsonproperty 屬性。**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

為了在用戶端程式代碼中保留可讀性/可維護性，您可以在接收到訊息之後，將縮寫的屬性名稱重新對應到人類易記的名稱。 下列程式碼範例將示範如何藉由定義訊息合約 (對應) ，以及使用函式將合約套用至優化訊息類別，來將縮短的名稱重新對應到較長的名稱 `reMap` ：

**用戶端 JavaScript 程式碼，可將縮短的屬性名稱重新對應為人們可讀取的名稱**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

您也可以使用相同的方法，從用戶端到伺服器的訊息中將名稱縮短。

減少記憶體使用量 (也就是說，訊息物件的訊息) 所使用的記憶體數量也可以改善效能。 例如，如果不需要的完整範圍 `int` ，則 `short` `byte` 可以改用或。

由於訊息會儲存在訊息匯流排的伺服器記憶體中，因此減少訊息的大小也可解決伺服器記憶體的問題。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>調整 SignalR 伺服器的效能

您可以使用下列設定來調整伺服器，以在 SignalR 應用程式中獲得更佳的效能。 如需如何在 ASP.NET 應用程式中改善效能的一般資訊，請參閱 [改善 ASP.NET 效能](https://msdn.microsoft.com/library/ff647787.aspx)。

**SignalR 設定**

- **DefaultMessageBufferSize**：根據預設，SignalR 會在每個連接的每個中樞，保留1000的訊息。 如果使用大型的訊息，這可能會建立記憶體問題，藉由減少此值來減輕問題。 這項設定可以在 `Application_Start` ASP.NET 應用程式的事件處理常式中設定，也可以在自我裝載的應用程式中，于 `Configuration` OWIN startup 類別的方法中設定。 下列範例示範如何減少此值，以減少應用程式的記憶體使用量，以減少使用的伺服器記憶體數量：

    **Startup.cs 中用來減少預設訊息緩衝區大小的 .NET server 程式碼**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 設定**

- **每個應用程式的最大並行要求**數：增加並行 IIS 要求的數目，將會增加可用來提供要求的伺服器資源。 預設值為 5000;若要增加此設定，請在提升許可權的命令提示字元中執行下列命令：

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**：這是 Http.sys 應用程式集區佇列的要求數目上限。 當佇列已滿時，新的要求會收到503「服務無法使用」的回應。 預設值為 1000。

    縮短裝載您應用程式之應用程式集區中工作者進程的佇列長度，將會節省記憶體資源。 如需詳細資訊，請參閱 [管理、調整和設定應用程式](https://technet.microsoft.com/library/cc745955.aspx)集區。

**ASP.NET 設定**

本節包含可在檔案中設定的設定 `aspnet.config` 。 您可以在下列兩個位置的其中一個位置找到這個檔案（視平臺而定）：

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

可能改善 SignalR 效能的 ASP.NET 設定包括下列各項：

- **每個 CPU 的並行要求數目上限**：增加此設定可能會減輕效能瓶頸。 若要增加此設定，請將下列設定設定新增至檔案 `aspnet.config` ：

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **要求佇列限制**：當連線總數超過 `maxConcurrentRequestsPerCPU` 設定時，ASP.NET 會使用佇列開始節流要求。 若要增加佇列的大小，您可以增加 `requestQueueLimit` 設定。 若要這樣做，請將下列設定設定新增至 `processModel` (中的節點， `config/machine.config` 而不是 `aspnet.config`) ：

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>針對效能問題進行疑難排解

本節說明在應用程式中尋找效能瓶頸的方法。

### <a name="verifying-that-websocket-is-being-used"></a>確認正在使用 WebSocket

雖然 SignalR 可以使用各種不同的傳輸來進行用戶端和伺服器之間的通訊，但 WebSocket 提供明顯的效能優勢，而且如果用戶端和伺服器支援，則應該使用。 若要判斷您的用戶端和伺服器是否符合 WebSocket 的需求，請參閱 [傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。 若要判斷應用程式中所使用的傳輸，您可以使用瀏覽器開發人員工具，並檢查記錄以查看連接所使用的傳輸。 如需在 Internet Explorer 和 Chrome 中使用瀏覽器開發工具的相關資訊，請參閱 [傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>使用 SignalR 效能計數器

本節說明如何啟用和使用在套件中找到的 SignalR 效能計數器 `Microsoft.AspNet.SignalR.Utils` 。

### <a name="installing-signalrexe"></a>安裝 signalr.exe

您可以使用稱為 SignalR.exe 的公用程式，將效能計數器新增至伺服器。 若要安裝此公用程式，請遵循下列步驟：

1. 在 Visual Studio 中，選取 [**工具**  >  **nuget 封裝管理員**  >  **管理解決方案的 nuget 套件**]
2. 搜尋 **signalr. 公用程式**，然後選取 [安裝]。

    ![](signalr-performance/_static/image1.png)
3. 接受授權合約以安裝套件。
4. SignalR.exe 將會安裝至 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools` 。

### <a name="installing-performance-counters-with-signalrexe"></a>使用 SignalR.exe 安裝效能計數器

若要安裝 SignalR 效能計數器，請使用下列參數在提高許可權的命令提示字元中執行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

若要移除 SignalR 效能計數器，請使用下列參數在提高許可權的命令提示字元中執行 SignalR.exe：

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 效能計數器

公用程式套件會安裝下列效能計數器。 「總計」計數器會測量自上次應用程式集區或伺服器重新開機之後的事件數目。

**連接計量**

下列計量會測量發生的連接存留期事件。 如需詳細資訊，請參閱 [瞭解及處理連接存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

- **連接連接**
- **連線重新連接**
- **連接中斷連線**
- **目前的連接**

**訊息計量**

下列計量會測量 SignalR 所產生的訊息流量。

- **接收的連接訊息總數**
- **傳送的連接訊息總計**
- **接收的連接訊息數/秒**
- **傳送的連接訊息/秒**

**訊息匯流排度量**

下列計量會測量流經內部 SignalR 訊息匯流排的流量，以及用來放置所有傳入和傳出 SignalR 訊息的佇列。 傳送或廣播訊息時，就會 **發佈** 訊息。 此內容中的「 **訂閱者** 」是訊息匯流排上的訂用帳戶;這應該等於用戶端的數目加上伺服器本身。 配置的背景 **工作角色** 是將資料傳送至作用中連線的元件; **忙碌的工作者** 是主動傳送訊息的工作者。

- **訊息匯流排接收的訊息總數**
- **訊息匯流排接收訊息數/秒**
- **已發佈的訊息匯流排訊息總數**
- **發佈的訊息匯流排訊息/秒**
- **訊息匯流排訂閱者目前**
- **訊息匯流排訂閱者總計**
- **訊息匯流排訂閱者/秒**
- **訊息匯流排配置的背景工作**
- **訊息匯流排忙碌背景工作**
- **目前的訊息匯流排主題**

**錯誤計量**

下列計量會測量 SignalR 訊息流量產生的錯誤。 無法解析中樞或中樞方法時，就會發生**中樞解析**錯誤。 **中樞調用** 錯誤是叫用中樞方法時擲回的例外狀況。 **傳輸** 錯誤是在 HTTP 要求或回應期間擲回的連接錯誤。

- **錯誤：所有總計**
- **錯誤：全部/秒**
- **錯誤：中樞解析總數**
- **錯誤：中樞解析/秒**
- **錯誤：中樞調用總數**
- **錯誤：中樞調用/秒**
- **錯誤：傳輸總計**
- **錯誤：傳輸/秒**

<a id="scaleout_metrics"></a>

**向外延展計量**

下列計量會測量向外延展提供者所產生的流量和錯誤。 此內容中的 **資料流程** 是向外延展提供者所使用的縮放單位;這是使用 SQL Server 的資料表、使用服務匯流排的主題，以及使用 Redis 時的訂用帳戶。 每個資料流程都可確保排序的讀取和寫入作業;單一資料流程是潛在的調整瓶頸，因此可以增加資料流程數目來協助降低瓶頸。 如果使用多個資料流程，SignalR 會自動散發這些資料流程的 (分區) 訊息，以確保從任何指定連線傳送的訊息順序都是如此。

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定會控制 SignalR 所維護的向外延展傳送佇列長度。 將它設定為大於0的值，就會將傳送佇列中的所有訊息一次一次傳送至設定的訊息後擋板。 如果佇列的大小超過設定的長度，則後續呼叫傳送將會立即失敗，並傳回 [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ，直到佇列中的訊息數目小於設定為止。 預設會停用佇列，因為實作為的背板通常會有自己的佇列或流程式控制制。 在 SQL Server 的情況下，連接共用會有效地限制在一次傳送時的傳送數目。

依預設，只有一個資料流程用於 SQL Server 和 Redis、五個串流用於服務匯流排，而佇列已停用，但您可以透過 SQL Server 和服務匯流排上的設定來變更這些設定：

**針對 SQL Server 後擋板設定資料表計數和佇列長度的 .NET Server 程式碼**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**用來設定服務匯流排背板主題計數和佇列長度的 .NET Server 程式碼**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**緩衝**資料流程是指進入錯誤狀態的資料流程;當資料流程處於「錯誤」狀態時，傳送至後擋板的所有訊息都會立即失敗，直到資料流程不再發生錯誤為止。 **傳送佇列長度**是已公佈但尚未傳送的訊息數目。

- **向外延展接收的訊息匯流排訊息/秒**
- **向外延展串流總數**
- **開啟的向外延展資料流程**
- **向外延展資料流程緩衝**
- **向外延展錯誤總計**
- **向外延展錯誤數/秒**
- **向外延展傳送佇列長度**

如需這些計數器的測量方式的詳細資訊，請參閱 [SignalR 向外延展與 Azure 服務匯流排](scaleout-with-windows-azure-service-bus.md)。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>使用其他效能計數器

下列效能計數器也有助於監視應用程式的效能。

**記憶體**

- \\W3wp.exe) 的所有堆積 (中的 .NET CLR 記憶體 # 位元組

**ASP.NET**

- ASP. NET\Requests Current
- ASP. NET\Queued
- ASP. NET\Rejected

**CPU**

- 處理器 Information\Processor 時間

**TCP/IP**

- 已建立 TCPv6/連接
- 已建立 TCPv4/連接

**Web 服務**

- Web Service\current connections 連接
- Web Service\Maximum 連接

**執行緒**

- .NET CLR 鎖定和執行緒 \\ # 個目前的邏輯執行緒
- .NET CLR 鎖定和執行緒 \\ # 個目前的實體執行緒

<a id="otherresources"></a>

## <a name="other-resources"></a>其他資源

如需有關 ASP.NET 效能監視和微調的詳細資訊，請參閱下列主題：

- [ASP.NET 效能概觀](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [IIS 7.5、IIS 7.0 和 IIS 6.0 上的 ASP.NET 執行緒使用量](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;&gt; (Web 設定) 的 applicationPool 元素](https://msdn.microsoft.com/library/dd560842.aspx)
