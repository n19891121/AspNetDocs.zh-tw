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
# <a name="signalr-performance"></a><span data-ttu-id="7856b-103">SignalR 效能</span><span class="sxs-lookup"><span data-stu-id="7856b-103">SignalR Performance</span></span>

<span data-ttu-id="7856b-104">由[派翠克·弗萊徹](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="7856b-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="7856b-105">本主題介紹如何為 SignalR 應用程式中的設計、測量和改進性能。</span><span class="sxs-lookup"><span data-stu-id="7856b-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="7856b-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="7856b-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="7856b-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7856b-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="7856b-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="7856b-108">.NET 4.5</span></span>
> - <span data-ttu-id="7856b-109">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="7856b-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="7856b-110">本主題的早期版本</span><span class="sxs-lookup"><span data-stu-id="7856b-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="7856b-111">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="7856b-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="7856b-112">問題和評論</span><span class="sxs-lookup"><span data-stu-id="7856b-112">Questions and comments</span></span>
>
> <span data-ttu-id="7856b-113">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="7856b-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="7856b-114">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="7856b-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="7856b-115">有關 SignalR 性能和縮放的最新演示文稿,請參閱[使用ASP.NET訊號R 縮放即時 Web。](https://channel9.msdn.com/Events/Build/2013/3-502)</span><span class="sxs-lookup"><span data-stu-id="7856b-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="7856b-116">本主題包含下列幾節：</span><span class="sxs-lookup"><span data-stu-id="7856b-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="7856b-117">設計考量</span><span class="sxs-lookup"><span data-stu-id="7856b-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="7856b-118">調整 SignalR 伺服器的效能</span><span class="sxs-lookup"><span data-stu-id="7856b-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="7856b-119">針對效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7856b-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="7856b-120">使用訊號R效能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="7856b-121">使用其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="7856b-122">其他資源</span><span class="sxs-lookup"><span data-stu-id="7856b-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="7856b-123">設計考量</span><span class="sxs-lookup"><span data-stu-id="7856b-123">Design considerations</span></span>

<span data-ttu-id="7856b-124">本節介紹在設計 SignalR 應用程序期間可以實現的模式,以確保不會因生成不必要的網路流量而妨礙性能。</span><span class="sxs-lookup"><span data-stu-id="7856b-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="7856b-125">限制訊息頻率</span><span class="sxs-lookup"><span data-stu-id="7856b-125">Throttling message frequency</span></span>

<span data-ttu-id="7856b-126">即使在以高頻率發送消息的應用程式(如即時遊戲應用程式)中,大多數應用程式也不需要每秒發送多條消息。</span><span class="sxs-lookup"><span data-stu-id="7856b-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="7856b-127">為了減少每個用戶端生成的流量,可以實現一個消息迴圈,該佇列和發送消息的頻率不會超過固定速率(也就是說,如果該時間間隔內有要發送的消息,每秒最多發送一定數量的消息)。</span><span class="sxs-lookup"><span data-stu-id="7856b-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="7856b-128">有關將訊息限制到特定速率(來自用戶端和伺服器)的範例應用程式,請參閱[使用 SignalR 的高頻即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="7856b-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="7856b-129">遞減小訊息大小</span><span class="sxs-lookup"><span data-stu-id="7856b-129">Reducing message size</span></span>

<span data-ttu-id="7856b-130">您可以通過減小序列化物件的大小來減小 SignalR 消息的大小。</span><span class="sxs-lookup"><span data-stu-id="7856b-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="7856b-131">在伺服器代碼中,如果發送的物件包含不需要傳輸的屬性,則防止使用`JsonIgnore`屬性 序列化這些屬性。</span><span class="sxs-lookup"><span data-stu-id="7856b-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="7856b-132">屬性的名稱也存儲在消息中;可以使用 屬性`JsonProperty`縮短 屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="7856b-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="7856b-133">以下代碼範例展示如何排除屬性傳送到用戶端,以及如何縮短屬性名稱:</span><span class="sxs-lookup"><span data-stu-id="7856b-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="7856b-134">**.NET 伺服器代碼,用於展示 JsonIgnore 屬性,以排除傳送到客戶端的資料,以及用於減小消息大小的 JsonProperty 屬性**</span><span class="sxs-lookup"><span data-stu-id="7856b-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="7856b-135">為了在客戶端代碼中保持可讀性/可維護性,在收到消息后,可以將縮寫屬性名稱重新映射到人友好名稱。</span><span class="sxs-lookup"><span data-stu-id="7856b-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="7856b-136">以下代碼範例展示了一種透過將縮短的名稱重新映射到較長的名稱的方法,方法是定義消息協定(映射),並使用函數`reMap`將協定應用於優化的消息類:</span><span class="sxs-lookup"><span data-stu-id="7856b-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="7856b-137">**用戶端 JavaScript 程式碼會縮短的屬性名稱重新映射到人可讀名稱**</span><span class="sxs-lookup"><span data-stu-id="7856b-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="7856b-138">名稱也可以使用相同的方法在從用戶端到伺服器的電子郵件中縮短。</span><span class="sxs-lookup"><span data-stu-id="7856b-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="7856b-139">減少消息物件的記憶體佔用空間(即用於消息的記憶體量)也可以提高性能。</span><span class="sxs-lookup"><span data-stu-id="7856b-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="7856b-140">例如,如果不需要全部範圍的,`int`則可以改用`short``byte`或 。</span><span class="sxs-lookup"><span data-stu-id="7856b-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="7856b-141">由於郵件存儲在伺服器記憶體中的消息總線中,因此減小消息大小還可以解決伺服器記憶體問題。</span><span class="sxs-lookup"><span data-stu-id="7856b-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="7856b-142">調整 SignalR 伺服器的效能</span><span class="sxs-lookup"><span data-stu-id="7856b-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="7856b-143">以下配置設定可用於調整伺服器,以便在 SignalR 應用程式中獲得更好的性能。</span><span class="sxs-lookup"><span data-stu-id="7856b-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="7856b-144">有關如何提高ASP.NET應用程式中性能的一般資訊,請參閱[改進ASP.NET性能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7856b-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="7856b-145">**訊號R設定設定**</span><span class="sxs-lookup"><span data-stu-id="7856b-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="7856b-146">**默認消息緩衝區大小**:預設情況下,SignalR 每個連接的記憶體中保留 1000 條消息。</span><span class="sxs-lookup"><span data-stu-id="7856b-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="7856b-147">如果使用大型消息,則可能會產生記憶體問題,通過減小此值來緩解這些問題。</span><span class="sxs-lookup"><span data-stu-id="7856b-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="7856b-148">此設置可以在ASP.NET應用程式中`Application_Start`的事件處理程式中設置,也可以在自託管應用程式中的OWIN啟動類`Configuration`方法中設置。</span><span class="sxs-lookup"><span data-stu-id="7856b-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="7856b-149">以下範例展示如何減小此值以減少應用程式的記憶體佔用量,以減少使用的伺服器記憶體量:</span><span class="sxs-lookup"><span data-stu-id="7856b-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="7856b-150">**Startup.cs中,此伺服器代碼,用於減少預設的郵件緩衝區大小**</span><span class="sxs-lookup"><span data-stu-id="7856b-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="7856b-151">**IIS 設定設定**</span><span class="sxs-lookup"><span data-stu-id="7856b-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="7856b-152">**每個應用程式的最多併發請求**:增加併發 IIS 請求的數量將增加可用於服務請求的伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="7856b-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="7856b-153">默認值為 5000;要增加此設定,請在提升的指令提示符中執行以下命令:</span><span class="sxs-lookup"><span data-stu-id="7856b-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="7856b-154">**應用程式池佇列長度**:這是 Http.sys 為應用程式池排隊的最大請求數。</span><span class="sxs-lookup"><span data-stu-id="7856b-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="7856b-155">佇列已滿時,新請求將收到 503"服務不可用"回應。</span><span class="sxs-lookup"><span data-stu-id="7856b-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="7856b-156">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="7856b-156">The default value is 1000.</span></span>

    <span data-ttu-id="7856b-157">縮短應用程式託管的應用程式池中工作進程的佇列長度將節省記憶體資源。</span><span class="sxs-lookup"><span data-stu-id="7856b-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="7856b-158">有關詳細資訊,請參閱[管理、調整和設定應用程式池](https://technet.microsoft.com/library/cc745955.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7856b-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="7856b-159">**ASP.NET 設定設定**</span><span class="sxs-lookup"><span data-stu-id="7856b-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="7856b-160">本節包括可在檔中設置的`aspnet.config`配置設置。</span><span class="sxs-lookup"><span data-stu-id="7856b-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="7856b-161">此檔案位於兩個位置之一,具體取決於平臺:</span><span class="sxs-lookup"><span data-stu-id="7856b-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="7856b-162">可能提高 SignalR 效能ASP.NET設定包括:</span><span class="sxs-lookup"><span data-stu-id="7856b-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="7856b-163">**每個 CPU 的最大併發請求**:增加此設置可能會緩解性能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="7856b-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="7856b-164">要增加此設定,向`aspnet.config`檔案新增以下設定設定:</span><span class="sxs-lookup"><span data-stu-id="7856b-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="7856b-165">**請求佇列限制**:當連接總數`maxConcurrentRequestsPerCPU`超過 設置時,ASP.NET將使用佇列開始限制請求。</span><span class="sxs-lookup"><span data-stu-id="7856b-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="7856b-166">要增加佇列的大小,可以增加`requestQueueLimit`設置。</span><span class="sxs-lookup"><span data-stu-id="7856b-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="7856b-167">為此,向中的`processModel``config/machine.config`節點添加以下配置設定(而不是`aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="7856b-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="7856b-168">針對效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="7856b-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="7856b-169">本節介紹查找應用程式中的性能瓶頸的方法。</span><span class="sxs-lookup"><span data-stu-id="7856b-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="7856b-170">認證是否正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="7856b-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="7856b-171">雖然 SignalR 可以使用各種傳輸在用戶端和伺服器之間通訊,但 WebSocket 具有顯著的性能優勢,如果用戶端和伺服器支援它,則應使用它。</span><span class="sxs-lookup"><span data-stu-id="7856b-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="7856b-172">要確定客戶端和伺服器是否滿足 WebSocket 的要求,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="7856b-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="7856b-173">要確定應用程式中正在使用哪些傳輸,可以使用瀏覽器開發人員工具,並檢查日誌以查看用於連接的傳輸。</span><span class="sxs-lookup"><span data-stu-id="7856b-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="7856b-174">有關在 Internet 資源管理員和 Chrome 中使用瀏覽器開發工具的資訊,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="7856b-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="7856b-175">使用訊號R效能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-175">Using SignalR performance counters</span></span>

<span data-ttu-id="7856b-176">本節介紹如何在`Microsoft.AspNet.SignalR.Utils`封裝中找到的啟用和使用 SignalR 性能計數器。</span><span class="sxs-lookup"><span data-stu-id="7856b-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="7856b-177">安裝訊號器.exe</span><span class="sxs-lookup"><span data-stu-id="7856b-177">Installing signalr.exe</span></span>

<span data-ttu-id="7856b-178">可以使用稱為 SignalR.exe 的實用程式將性能計數器添加到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7856b-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="7856b-179">要安裝此實用程式,請按照以下步驟操作:</span><span class="sxs-lookup"><span data-stu-id="7856b-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="7856b-180">在視覺化工作室中,選擇**工具** > **NuGet 套件管理員** > **管理 NuGet 套件以進行解決方案**</span><span class="sxs-lookup"><span data-stu-id="7856b-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="7856b-181">搜尋**信號器.utils,** 然後選擇"安裝"</span><span class="sxs-lookup"><span data-stu-id="7856b-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="7856b-182">接受安裝包的許可協定。</span><span class="sxs-lookup"><span data-stu-id="7856b-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="7856b-183">SignalR.exe 將安裝`<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`到 。</span><span class="sxs-lookup"><span data-stu-id="7856b-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="7856b-184">使用 SignalR.exe 安裝效能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="7856b-185">要安裝 SignalR 效能計數器,請使用以下參數在提升的指令提示符中執行 SignalR.exe:</span><span class="sxs-lookup"><span data-stu-id="7856b-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="7856b-186">要刪除 SignalR 效能計數器,請使用以下參數在提升的指令提示符中執行 SignalR.exe:</span><span class="sxs-lookup"><span data-stu-id="7856b-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="7856b-187">訊號R性能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-187">SignalR Performance counters</span></span>

<span data-ttu-id="7856b-188">實用程式包安裝以下性能計數器。</span><span class="sxs-lookup"><span data-stu-id="7856b-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="7856b-189">「總計」計數器測量自上次應用程式池或伺服器重新啟動以來的事件數。</span><span class="sxs-lookup"><span data-stu-id="7856b-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="7856b-190">**連接計量**</span><span class="sxs-lookup"><span data-stu-id="7856b-190">**Connection metrics**</span></span>

<span data-ttu-id="7856b-191">以下指標衡量發生的連接存留期事件。</span><span class="sxs-lookup"><span data-stu-id="7856b-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="7856b-192">有關詳細資訊,請參閱[瞭解和處理連線存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="7856b-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="7856b-193">**連線已連線**</span><span class="sxs-lookup"><span data-stu-id="7856b-193">**Connections Connected**</span></span>
- <span data-ttu-id="7856b-194">**連線重新連線**</span><span class="sxs-lookup"><span data-stu-id="7856b-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="7856b-195">**連線已斷線連線**</span><span class="sxs-lookup"><span data-stu-id="7856b-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="7856b-196">**連接電流**</span><span class="sxs-lookup"><span data-stu-id="7856b-196">**Connections Current**</span></span>

<span data-ttu-id="7856b-197">**訊息計量**</span><span class="sxs-lookup"><span data-stu-id="7856b-197">**Message metrics**</span></span>

<span data-ttu-id="7856b-198">以下指標測量 SignalR 生成的消息流量。</span><span class="sxs-lookup"><span data-stu-id="7856b-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="7856b-199">**接收的連線訊息總數**</span><span class="sxs-lookup"><span data-stu-id="7856b-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="7856b-200">**連線訊息傳送總數**</span><span class="sxs-lookup"><span data-stu-id="7856b-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="7856b-201">**已接收/秒的連線訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="7856b-202">**已傳送/秒的連線訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="7856b-203">**訊息匯流排**</span><span class="sxs-lookup"><span data-stu-id="7856b-203">**Message bus metrics**</span></span>

<span data-ttu-id="7856b-204">以下指標測量通過內部 SignalR 消息總線(放置所有傳入和傳出 SignalR 消息的佇列)的流量。</span><span class="sxs-lookup"><span data-stu-id="7856b-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="7856b-205">訊息在傳送或廣播時**已發布**。</span><span class="sxs-lookup"><span data-stu-id="7856b-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="7856b-206">此上下文中的**訂閱伺服器**是消息總線上的訂閱;這應該等於用戶端數加上伺服器本身。</span><span class="sxs-lookup"><span data-stu-id="7856b-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="7856b-207">**已分配的工作線程**是將數據發送到活動連接的元件;**忙工作人員**是主動發送消息的工作人員。</span><span class="sxs-lookup"><span data-stu-id="7856b-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="7856b-208">**接收到的訊息總線訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="7856b-209">**收到/秒的消息總線訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="7856b-210">**訊息總線訊息已發佈總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="7856b-211">**已發佈/秒的消息總線訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="7856b-212">**訊息總線訂閱伺服器目前**</span><span class="sxs-lookup"><span data-stu-id="7856b-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="7856b-213">**訊息總線訂閱者總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="7856b-214">**訊息總線訂閱者/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="7856b-215">**訊息總線配置工作**</span><span class="sxs-lookup"><span data-stu-id="7856b-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="7856b-216">**消息總線忙工作人員**</span><span class="sxs-lookup"><span data-stu-id="7856b-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="7856b-217">**郵件匯流主題目前**</span><span class="sxs-lookup"><span data-stu-id="7856b-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="7856b-218">**錯誤指標**</span><span class="sxs-lookup"><span data-stu-id="7856b-218">**Error metrics**</span></span>

<span data-ttu-id="7856b-219">以下指標測量由 SignalR 消息流量生成的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7856b-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="7856b-220">當無法解析中心或中心方法時,就會發生**中心解析**錯誤。</span><span class="sxs-lookup"><span data-stu-id="7856b-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="7856b-221">**中心調用**錯誤是在調用集線器方法時引發的異常。</span><span class="sxs-lookup"><span data-stu-id="7856b-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="7856b-222">**傳輸**錯誤是在 HTTP 請求或回應期間引發的連接錯誤。</span><span class="sxs-lookup"><span data-stu-id="7856b-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="7856b-223">**錯誤:全部總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-223">**Errors: All Total**</span></span>
- <span data-ttu-id="7856b-224">**錯誤:所有/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="7856b-225">**錯誤:中心解析度總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="7856b-226">**錯誤:集線器解析度/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="7856b-227">**錯誤:集線器呼叫總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="7856b-228">**錯誤:集線器呼叫/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="7856b-229">**錯誤:傳輸總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="7856b-230">**錯誤:傳輸/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="7856b-231">**橫向延伸指標**</span><span class="sxs-lookup"><span data-stu-id="7856b-231">**Scaleout metrics**</span></span>

<span data-ttu-id="7856b-232">以下指標衡量橫向擴展提供程式生成的流量和錯誤。</span><span class="sxs-lookup"><span data-stu-id="7856b-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="7856b-233">此上下文中的**流**是橫向擴展提供程式使用的縮放單位;如果使用 SQL Server,則這是表;使用服務總線時的主題;如果使用 Redis,則為訂閱。</span><span class="sxs-lookup"><span data-stu-id="7856b-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="7856b-234">每個流確保有序的讀取和寫入操作;單個流是潛在的規模瓶頸,因此可以增加流的數量,以幫助減少該瓶頸。</span><span class="sxs-lookup"><span data-stu-id="7856b-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="7856b-235">如果使用多個流,SignalR 將自動在這些流中分發(分片)消息,以確保從任何給定連接發送的消息按順序排列。</span><span class="sxs-lookup"><span data-stu-id="7856b-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="7856b-236">["最大佇列長度](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)"設置控制 SignalR 維護的橫向擴展發送佇列的長度。</span><span class="sxs-lookup"><span data-stu-id="7856b-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="7856b-237">將其設置為大於 0 的值將使發送佇列中的所有消息一次發送到配置的消息背板。</span><span class="sxs-lookup"><span data-stu-id="7856b-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="7856b-238">如果佇列的大小高於配置的長度,則後續發送的呼叫將立即失敗,使用[InvalidTheAa,](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx)直到佇列中的消息數再次小於設置。</span><span class="sxs-lookup"><span data-stu-id="7856b-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="7856b-239">默認情況下禁用排隊,因為實現的背板通常有自己的佇列或流控制。</span><span class="sxs-lookup"><span data-stu-id="7856b-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="7856b-240">對於 SQL Server,連接池有效地限制了任何一次進行發送的次數。</span><span class="sxs-lookup"><span data-stu-id="7856b-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="7856b-241">預設情況下,只有一個流用於 SQL Server 和 Redis,五個流用於服務總線,並且禁用排隊,但這些設置可以通過 SQL Server 和服務總線上的配置更改:</span><span class="sxs-lookup"><span data-stu-id="7856b-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="7856b-242">**.NET 伺服器代碼,用於設定 SQL Server 背板的表計數和佇列長度**</span><span class="sxs-lookup"><span data-stu-id="7856b-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="7856b-243">**.NET 伺服器代碼,用於設定服務總線背板的主題計數和佇列長度**</span><span class="sxs-lookup"><span data-stu-id="7856b-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="7856b-244">**緩衝**流是已進入錯誤狀態的流流;當流處於故障狀態時,發送到背板的所有消息將立即失敗,直到流不再出現故障。</span><span class="sxs-lookup"><span data-stu-id="7856b-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="7856b-245">**發送佇列長度**是已過帳但尚未發送的郵件數。</span><span class="sxs-lookup"><span data-stu-id="7856b-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="7856b-246">**已接收/秒的橫向延伸訊息匯流排訊息**</span><span class="sxs-lookup"><span data-stu-id="7856b-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="7856b-247">**橫向延伸流總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="7856b-248">**展開延伸流**</span><span class="sxs-lookup"><span data-stu-id="7856b-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="7856b-249">**橫向延伸流緩衝**</span><span class="sxs-lookup"><span data-stu-id="7856b-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="7856b-250">**橫向延伸錯誤總計**</span><span class="sxs-lookup"><span data-stu-id="7856b-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="7856b-251">**橫向延伸錯誤/秒**</span><span class="sxs-lookup"><span data-stu-id="7856b-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="7856b-252">**橫向延伸傳送佇列長度**</span><span class="sxs-lookup"><span data-stu-id="7856b-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="7856b-253">有關這些計數器正在測量的內容的詳細資訊,請參閱[使用 Azure 服務匯流排進行訊號 R 橫向擴展](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="7856b-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="7856b-254">使用其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="7856b-254">Using other performance counters</span></span>

<span data-ttu-id="7856b-255">以下性能計數器在監視應用程式的性能時可能也很有用。</span><span class="sxs-lookup"><span data-stu-id="7856b-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="7856b-256">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="7856b-256">**Memory**</span></span>

- <span data-ttu-id="7856b-257">.NET CLR\\記憶體 = 所有堆中的位元組(對於 w3wp)</span><span class="sxs-lookup"><span data-stu-id="7856b-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="7856b-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="7856b-258">**ASP.NET**</span></span>

- <span data-ttu-id="7856b-259">ASP.NET_請求目前</span><span class="sxs-lookup"><span data-stu-id="7856b-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="7856b-260">ASP.NET_已排隊</span><span class="sxs-lookup"><span data-stu-id="7856b-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="7856b-261">ASP.NET_已拒絕</span><span class="sxs-lookup"><span data-stu-id="7856b-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="7856b-262">**Cpu**</span><span class="sxs-lookup"><span data-stu-id="7856b-262">**CPU**</span></span>

- <span data-ttu-id="7856b-263">處理器資訊+處理器時間</span><span class="sxs-lookup"><span data-stu-id="7856b-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="7856b-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="7856b-264">**TCP/IP**</span></span>

- <span data-ttu-id="7856b-265">TCPv6/已建立連線</span><span class="sxs-lookup"><span data-stu-id="7856b-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="7856b-266">TCPv4/已建立連線</span><span class="sxs-lookup"><span data-stu-id="7856b-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="7856b-267">**網路服務**</span><span class="sxs-lookup"><span data-stu-id="7856b-267">**Web Service**</span></span>

- <span data-ttu-id="7856b-268">Web 服務\目前連線</span><span class="sxs-lookup"><span data-stu-id="7856b-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="7856b-269">Web 服務= 最大連線</span><span class="sxs-lookup"><span data-stu-id="7856b-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="7856b-270">**執行緒**</span><span class="sxs-lookup"><span data-stu-id="7856b-270">**Threading**</span></span>

- <span data-ttu-id="7856b-271">.NET CLR\\鎖 與緒執行線執行程式 。</span><span class="sxs-lookup"><span data-stu-id="7856b-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="7856b-272">.NET CLR\\鎖 與緒執行線... # 目前的實體線程</span><span class="sxs-lookup"><span data-stu-id="7856b-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="7856b-273">其他資源</span><span class="sxs-lookup"><span data-stu-id="7856b-273">Other Resources</span></span>

<span data-ttu-id="7856b-274">有關ASP.NET性能監視和調優的詳細資訊,請參閱以下主題:</span><span class="sxs-lookup"><span data-stu-id="7856b-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="7856b-275">[ASP.NET 效能概觀](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="7856b-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="7856b-276">iIS 7.5、IIS 7.0 和IIS6.0上的ASP.NET線程使用方式</span><span class="sxs-lookup"><span data-stu-id="7856b-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="7856b-277">&lt;應用程式池&gt;元素(Web 設定)</span><span class="sxs-lookup"><span data-stu-id="7856b-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
