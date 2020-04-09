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
# <a name="introduction-to-signalr"></a><span data-ttu-id="256e2-103">SignalR 簡介</span><span class="sxs-lookup"><span data-stu-id="256e2-103">Introduction to SignalR</span></span>

<span data-ttu-id="256e2-104">由[派翠克·弗萊徹](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="256e2-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="256e2-105">本文介紹了 SignalR 是什麼,以及它旨在創建的一些解決方案。</span><span class="sxs-lookup"><span data-stu-id="256e2-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="256e2-106">問題和評論</span><span class="sxs-lookup"><span data-stu-id="256e2-106">Questions and comments</span></span>
> 
> <span data-ttu-id="256e2-107">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="256e2-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="256e2-108">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="256e2-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="256e2-109">什麼是信號R?</span><span class="sxs-lookup"><span data-stu-id="256e2-109">What is SignalR?</span></span>

<span data-ttu-id="256e2-110">ASP.NET SignalR 是一個面向ASP.NET開發人員的庫,它簡化了向應用程式添加即時 Web 功能的過程。</span><span class="sxs-lookup"><span data-stu-id="256e2-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="256e2-111">即時 Web 功能是讓伺服器代碼在可用時立即將內容推送到連接的用戶端,而不是讓伺服器等待用戶端請求新數據的能力。</span><span class="sxs-lookup"><span data-stu-id="256e2-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="256e2-112">SignalR 可用於向ASP.NET應用程式添加任何類型的「即時」Web 功能。</span><span class="sxs-lookup"><span data-stu-id="256e2-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="256e2-113">雖然聊天通常用作示例,但您可以執行更多操作。</span><span class="sxs-lookup"><span data-stu-id="256e2-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="256e2-114">每當使用者刷新網頁以查看新數據,或者該頁實現[長輪詢](http://en.wikipedia.org/wiki/Push_technology#Long_polling)以檢索新數據時,它都是使用 SignalR 的候選資料庫。</span><span class="sxs-lookup"><span data-stu-id="256e2-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="256e2-115">範例包括儀表板和監視應用程式、協作應用程式(如同時編輯文檔)、作業進度更新和即時表單。</span><span class="sxs-lookup"><span data-stu-id="256e2-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="256e2-116">SignalR 還支援需要伺服器進行高頻更新(例如即時遊戲)的全新 Web 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="256e2-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="256e2-117">SignalR 提供了一個簡單的 API,用於建立伺服器到用戶端的遠端過程呼叫 (RPC),該呼叫從伺服器端 .NET 代碼呼叫用戶端瀏覽器(和其他用戶端平臺)中的 JavaScript 函數。</span><span class="sxs-lookup"><span data-stu-id="256e2-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="256e2-118">SignalR 還包括用於連接管理的 API(例如,連接和斷開連接事件)和分組連接。</span><span class="sxs-lookup"><span data-stu-id="256e2-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![使用訊號R呼叫方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="256e2-120">SignalR 會自動處理連線管理，讓您能夠將訊息同時廣播到所有連線的用戶端，例如聊天室。</span><span class="sxs-lookup"><span data-stu-id="256e2-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="256e2-121">您也可以將訊息傳送給特定的用戶端。</span><span class="sxs-lookup"><span data-stu-id="256e2-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="256e2-122">不同於傳統的 HTTP 連線，用戶端與伺服器之間的連線是持續性的，此連線會基於每次通訊重新建立。</span><span class="sxs-lookup"><span data-stu-id="256e2-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="256e2-123">SignalR 支援「伺服器推送」功能,即伺服器代碼可以使用遠端過程呼叫 (RPC) 向瀏覽器中的用戶端代碼調用,而不是網站上常見的請求-回應模型。</span><span class="sxs-lookup"><span data-stu-id="256e2-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="256e2-124">SignalR 應用程式可以使用內建和第三方橫向擴展提供程式擴展到數千個用戶端。</span><span class="sxs-lookup"><span data-stu-id="256e2-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="256e2-125">內建提供者包括:</span><span class="sxs-lookup"><span data-stu-id="256e2-125">Built-in providers include:</span></span>
* [<span data-ttu-id="256e2-126">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="256e2-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="256e2-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="256e2-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="256e2-128">Redis</span><span class="sxs-lookup"><span data-stu-id="256e2-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="256e2-129">第三方提供者包括:</span><span class="sxs-lookup"><span data-stu-id="256e2-129">Third-party providers include:</span></span>
* <span data-ttu-id="256e2-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span><span class="sxs-lookup"><span data-stu-id="256e2-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="256e2-131">信號R是開源的,可通過[GitHub](https://github.com/signalr)訪問。</span><span class="sxs-lookup"><span data-stu-id="256e2-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="256e2-132">訊號R和網路插座</span><span class="sxs-lookup"><span data-stu-id="256e2-132">SignalR and WebSocket</span></span>

<span data-ttu-id="256e2-133">SignalR在可用時使用新的 WebSocket 傳輸,並在必要時回退到較舊的傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="256e2-134">雖然您肯定可以使用 WebSocket 直接編寫應用,但使用 SignalR 意味著您需要實現的大部分額外功能已經為您完成。</span><span class="sxs-lookup"><span data-stu-id="256e2-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="256e2-135">最重要的是,這意味著您可以編寫應用代碼以利用 WebSocket,而無需擔心為較舊的用戶端創建單獨的代碼路徑。</span><span class="sxs-lookup"><span data-stu-id="256e2-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="256e2-136">SignalR 還保護您不必擔心 WebSocket 的更新,因為 SignalR 已更新以支援基礎傳輸中的更改,從而為您的應用程式提供跨 WebSocket 版本的一致的介面。</span><span class="sxs-lookup"><span data-stu-id="256e2-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="256e2-137">傳輸和回退</span><span class="sxs-lookup"><span data-stu-id="256e2-137">Transports and fallbacks</span></span>

<span data-ttu-id="256e2-138">SignalR 是一種對在用戶端和伺服器之間執行即時工作所需的一些傳輸的抽象。</span><span class="sxs-lookup"><span data-stu-id="256e2-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="256e2-139">SignalR 連接以 HTTP 開頭,然後將其提升為 WebSocket 連接(如果可用)。</span><span class="sxs-lookup"><span data-stu-id="256e2-139">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="256e2-140">WebSocket 是 SignalR 的理想傳輸方式,因為它最有效地使用伺服器記憶體,具有最低的延遲,並具有最基本的功能(如用戶端和伺服器之間的全雙工通信),但它也具有最嚴格的要求:WebSocket 要求伺服器使用 Windows Server 2012 或 Windows 8 以及 .NET 框架 4.5。</span><span class="sxs-lookup"><span data-stu-id="256e2-140">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="256e2-141">如果不符合這些要求,SignalR 將嘗試使用其他傳輸來建立連接。</span><span class="sxs-lookup"><span data-stu-id="256e2-141">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="256e2-142">HTML 5 傳輸</span><span class="sxs-lookup"><span data-stu-id="256e2-142">HTML 5 transports</span></span>

<span data-ttu-id="256e2-143">這些傳輸依賴於對 HTML [5](http://en.wikipedia.org/wiki/HTML5)的支援。</span><span class="sxs-lookup"><span data-stu-id="256e2-143">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="256e2-144">如果用戶端瀏覽器不支援 HTML 5 標準,將使用較舊的傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-144">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="256e2-145">**WebSocket(** 如果伺服器和瀏覽器都表示它們可以支援 Websocket)。</span><span class="sxs-lookup"><span data-stu-id="256e2-145">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="256e2-146">WebSocket 是建立用戶端和伺服器之間真正持久雙向連接的唯一傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-146">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="256e2-147">但是,WebSocket 也有最嚴格的要求;它僅在最新版本的微軟瀏覽器、谷歌 Chrome 和 Mozilla Firefox 中得到充分支援,並且僅在其他瀏覽器(如 Opera 和 Safari)中具有部分實現。</span><span class="sxs-lookup"><span data-stu-id="256e2-147">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="256e2-148">**伺服器發送事件**,也稱為事件源(如果瀏覽器支援伺服器發送事件,這基本上是除 Internet 資源管理器之外的所有瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="256e2-148">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="256e2-149">彗星運輸</span><span class="sxs-lookup"><span data-stu-id="256e2-149">Comet transports</span></span>

<span data-ttu-id="256e2-150">以下傳輸基於[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) Web 應用程式模型,其中瀏覽器或其他用戶端維護長期持有的 HTTP 請求,伺服器可以使用該請求將數據推送到用戶端,而無需用戶端專門請求該請求。</span><span class="sxs-lookup"><span data-stu-id="256e2-150">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="256e2-151">**永久幀**(僅適用於 Internet 資源管理員)。</span><span class="sxs-lookup"><span data-stu-id="256e2-151">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="256e2-152">永久幀創建一個隱藏的 IFrame,該 IFrame 向伺服器上未完成終結點的請求。</span><span class="sxs-lookup"><span data-stu-id="256e2-152">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="256e2-153">然後,伺服器不斷向用戶端發送腳本,並立即執行該腳本,提供從伺服器到用戶端的單向即時連接。</span><span class="sxs-lookup"><span data-stu-id="256e2-153">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="256e2-154">從用戶端到伺服器的連接使用從伺服器到用戶端連接的單獨連接,並且與標準 HTTP 請求一樣,為需要發送的每個數據段創建新連接。</span><span class="sxs-lookup"><span data-stu-id="256e2-154">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="256e2-155">**阿賈克斯長輪詢**。</span><span class="sxs-lookup"><span data-stu-id="256e2-155">**Ajax long polling**.</span></span> <span data-ttu-id="256e2-156">長輪詢不會創建持久連接,而是輪詢伺服器的請求,該請求保持打開狀態,直到伺服器回應,此時連接將關閉,並立即請求新連接。</span><span class="sxs-lookup"><span data-stu-id="256e2-156">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="256e2-157">這可能會在連接重置時引入一些延遲。</span><span class="sxs-lookup"><span data-stu-id="256e2-157">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="256e2-158">有關支援哪些傳輸的設定的詳細資訊,請參閱[支援的平臺](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="256e2-158">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="256e2-159">傳輸選擇程序</span><span class="sxs-lookup"><span data-stu-id="256e2-159">Transport selection process</span></span>

<span data-ttu-id="256e2-160">下面的清單顯示了 SignalR 用來決定要使用的傳輸的步驟。</span><span class="sxs-lookup"><span data-stu-id="256e2-160">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="256e2-161">如果瀏覽器是 Internet 資源管理器 8 或更早版本,則使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="256e2-161">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="256e2-162">如果配置了 JSONP(即`jsonp`參數`true`設置為 啟動連接時),則使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="256e2-162">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="256e2-163">如果進行跨域連接(即,如果 SignalR 終結點與託管頁不在同一域中),則如果滿足以下條件,將使用 WebSocket:</span><span class="sxs-lookup"><span data-stu-id="256e2-163">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="256e2-164">用戶端支援 CORS(跨源資源分享)。</span><span class="sxs-lookup"><span data-stu-id="256e2-164">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="256e2-165">有關哪些用戶端支援 CORS 的詳細資訊,請參閱[caniuse.com上的 CORS。](http://www.caniuse.com/CORS)</span><span class="sxs-lookup"><span data-stu-id="256e2-165">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="256e2-166">用戶端支援 WebSocket</span><span class="sxs-lookup"><span data-stu-id="256e2-166">The client supports WebSocket</span></span>
   - <span data-ttu-id="256e2-167">伺服器支援 Web 插座</span><span class="sxs-lookup"><span data-stu-id="256e2-167">The server supports WebSocket</span></span>

     <span data-ttu-id="256e2-168">如果未滿足上述任何條件,將使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="256e2-168">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="256e2-169">有關跨域連接的詳細資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="256e2-169">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="256e2-170">如果未配置 JSONP 並且連接不是跨域,則如果用戶端和伺服器都支援它,將使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="256e2-170">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="256e2-171">如果用戶端或伺服器不支援 WebSocket,則使用伺服器發送事件(如果可用)。</span><span class="sxs-lookup"><span data-stu-id="256e2-171">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="256e2-172">如果伺服器發送事件不可用,則嘗試"永久幀"。</span><span class="sxs-lookup"><span data-stu-id="256e2-172">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="256e2-173">如果"永久幀"失敗,則使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="256e2-173">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="256e2-174">監控運輸</span><span class="sxs-lookup"><span data-stu-id="256e2-174">Monitoring transports</span></span>

<span data-ttu-id="256e2-175">通過在集線器上啟用日誌記錄,並在瀏覽器中打開控制台視窗,可以確定應用程式正在使用什麼傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-175">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="256e2-176">要在瀏覽器中啟用中心事件紀錄記錄,請向用戶端應用程式新增以下命令:</span><span class="sxs-lookup"><span data-stu-id="256e2-176">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="256e2-177">在 Internet 資源管理器中,透過按 F12 打開開發人員工具,然後單擊「控制台」選項卡。</span><span class="sxs-lookup"><span data-stu-id="256e2-177">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![微軟網際網路瀏覽器中的主控台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="256e2-179">在 Chrome 中,通過按 Ctrl_Shift_J 打開主控台。</span><span class="sxs-lookup"><span data-stu-id="256e2-179">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![谷歌瀏覽器中的主控台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="256e2-181">啟用主控台並啟用日誌記錄後,您將能夠看到 SignalR 正在使用哪種傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-181">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![顯示 WebSocket 傳輸的 Internet 資源管理員中的主控台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="256e2-183">指定傳輸</span><span class="sxs-lookup"><span data-stu-id="256e2-183">Specifying a transport</span></span>

<span data-ttu-id="256e2-184">協商傳輸需要一定的時間和用戶端/伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="256e2-184">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="256e2-185">如果用戶端功能已知,則可以在啟動用戶端連接時指定傳輸。</span><span class="sxs-lookup"><span data-stu-id="256e2-185">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="256e2-186">以下代碼段演示使用 Ajax Long 輪詢傳輸啟動連接,如果已知用戶端不支援任何其他協定,則使用該傳輸:</span><span class="sxs-lookup"><span data-stu-id="256e2-186">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="256e2-187">如果希望客戶端按順序嘗試特定傳輸,則可以指定回退順序。</span><span class="sxs-lookup"><span data-stu-id="256e2-187">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="256e2-188">以下代碼段演示了嘗試 WebSocket,如果失敗,請直接訪問長輪詢。</span><span class="sxs-lookup"><span data-stu-id="256e2-188">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="256e2-189">指定指定的字串常量定義的字串常量定義的字串常量定義的字串:</span><span class="sxs-lookup"><span data-stu-id="256e2-189">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="256e2-190">連接和集線器</span><span class="sxs-lookup"><span data-stu-id="256e2-190">Connections and Hubs</span></span>

<span data-ttu-id="256e2-191">SignalR API 包含兩種用於用戶端和伺服器之間通信的模型:持久連接和集線器。</span><span class="sxs-lookup"><span data-stu-id="256e2-191">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="256e2-192">連接表示用於發送單收件者、分組消息或廣播消息的簡單終結點。</span><span class="sxs-lookup"><span data-stu-id="256e2-192">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="256e2-193">持久連接 API(由持久連接類在 .NET 代碼中表示)使開發人員能夠直接訪問 SignalR 公開的低級通訊協定。</span><span class="sxs-lookup"><span data-stu-id="256e2-193">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="256e2-194">使用連接通訊模型對於使用基於連接的 API(如 Windows 通信基礎)的開發人員來說,是熟悉的。</span><span class="sxs-lookup"><span data-stu-id="256e2-194">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="256e2-195">集線器是一個基於連接 API 構建的更高級管道,允許用戶端和伺服器直接呼叫彼此的方法。</span><span class="sxs-lookup"><span data-stu-id="256e2-195">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="256e2-196">SignalR 處理跨計算機邊界的調度,就像通過魔術一樣,允許用戶端像本地方法一樣輕鬆地調用伺服器上的方法,反之亦然。</span><span class="sxs-lookup"><span data-stu-id="256e2-196">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="256e2-197">使用中心通信模型對於使用遠端調用 API(如 .NET 遠端處理)的開發人員來說,是熟悉的。</span><span class="sxs-lookup"><span data-stu-id="256e2-197">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="256e2-198">使用集線器還允許您將強類型參數傳遞給方法,從而啟用模型綁定。</span><span class="sxs-lookup"><span data-stu-id="256e2-198">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="256e2-199">架構圖</span><span class="sxs-lookup"><span data-stu-id="256e2-199">Architecture diagram</span></span>

<span data-ttu-id="256e2-200">下圖顯示了集線器、持久連接和用於傳輸的基礎技術之間的關係。</span><span class="sxs-lookup"><span data-stu-id="256e2-200">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![顯示 API、傳輸和客戶端的訊號 R 架構圖](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="256e2-202">中心的工作原理</span><span class="sxs-lookup"><span data-stu-id="256e2-202">How Hubs work</span></span>

<span data-ttu-id="256e2-203">當伺服器端代碼在用戶端上調用方法時,數據包將跨活動傳輸發送,該傳輸包含要調用的方法的名稱和參數(當物件作為方法參數發送時,使用 JSON 對其進行序列化)。</span><span class="sxs-lookup"><span data-stu-id="256e2-203">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="256e2-204">然後,用戶端將方法名稱與用戶端代碼中定義的方法匹配。</span><span class="sxs-lookup"><span data-stu-id="256e2-204">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="256e2-205">如果存在匹配項,將使用反序列化參數數據執行用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="256e2-205">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="256e2-206">可以使用[Fiddler](http://fiddler2.com/)等工具監視方法調用。</span><span class="sxs-lookup"><span data-stu-id="256e2-206">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="256e2-207">下圖顯示了 Fiddler 的 Logs 窗格中從 SignalR 伺服器發送到 Web 瀏覽器用戶端的方法調用。</span><span class="sxs-lookup"><span data-stu-id="256e2-207">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="256e2-208">方法呼叫是從稱為`MoveShapeHub`的中心傳送的,並且呼叫的方法`updateShape`稱為 。</span><span class="sxs-lookup"><span data-stu-id="256e2-208">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![顯示訊號 R 流量的 Fiddler 紀錄檢視](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="256e2-210">在此示例中,中心名稱與 參數`H`一起標識;因此,使用 參數標識中心名稱。方法名稱與`M`參數一起標識,發送到方法的數據用`A`參數 標識。</span><span class="sxs-lookup"><span data-stu-id="256e2-210">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="256e2-211">生成此消息的應用程式在[高頻即時](tutorial-high-frequency-realtime-with-signalr.md)教程中創建。</span><span class="sxs-lookup"><span data-stu-id="256e2-211">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="256e2-212">選擇通訊模型</span><span class="sxs-lookup"><span data-stu-id="256e2-212">Choosing a communication model</span></span>

<span data-ttu-id="256e2-213">大多數應用程式應使用集線器 API。</span><span class="sxs-lookup"><span data-stu-id="256e2-213">Most applications should use the Hubs API.</span></span> <span data-ttu-id="256e2-214">連線 API 可用於以下情況:</span><span class="sxs-lookup"><span data-stu-id="256e2-214">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="256e2-215">需要指定發送的實際訊息的格式。</span><span class="sxs-lookup"><span data-stu-id="256e2-215">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="256e2-216">開發人員更喜歡使用消息傳遞和調度模型,而不是遠端調用模型。</span><span class="sxs-lookup"><span data-stu-id="256e2-216">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="256e2-217">正在移植使用消息傳遞模型的現有應用程式以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="256e2-217">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
