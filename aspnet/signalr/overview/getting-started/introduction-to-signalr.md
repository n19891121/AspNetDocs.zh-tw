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
# <a name="introduction-to-signalr"></a><span data-ttu-id="ad00d-103">SignalR 簡介</span><span class="sxs-lookup"><span data-stu-id="ad00d-103">Introduction to SignalR</span></span>

<span data-ttu-id="ad00d-104">依 [派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ad00d-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ad00d-105">本文說明 SignalR 是什麼，以及它設計來建立的一些解決方案。</span><span class="sxs-lookup"><span data-stu-id="ad00d-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="ad00d-106">問題與意見</span><span class="sxs-lookup"><span data-stu-id="ad00d-106">Questions and comments</span></span>
> 
> <span data-ttu-id="ad00d-107">請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="ad00d-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ad00d-108">如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。</span><span class="sxs-lookup"><span data-stu-id="ad00d-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="ad00d-109">什麼是 SignalR？</span><span class="sxs-lookup"><span data-stu-id="ad00d-109">What is SignalR?</span></span>

<span data-ttu-id="ad00d-110">ASP.NET SignalR 是 ASP.NET 開發人員的程式庫，可簡化將即時 web 功能新增至應用程式的流程。</span><span class="sxs-lookup"><span data-stu-id="ad00d-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="ad00d-111">即時 web 功能是能夠讓伺服器程式碼在連線的用戶端變成可用時立即將內容推送至連線的用戶端，而不是讓伺服器等待用戶端要求新的資料。</span><span class="sxs-lookup"><span data-stu-id="ad00d-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="ad00d-112">SignalR 可以用來將任何種類的「即時」 web 功能新增至您的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad00d-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="ad00d-113">雖然聊天通常是用來做為範例，但您可以多做一些。</span><span class="sxs-lookup"><span data-stu-id="ad00d-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="ad00d-114">當使用者重新整理網頁以查看新的資料時，或此頁面會執行 [長時間輪詢](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 來取得新的資料時，就是使用 SignalR 的候選項。</span><span class="sxs-lookup"><span data-stu-id="ad00d-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="ad00d-115">範例包括儀表板和監視應用程式、共同作業應用程式 (例如同時編輯檔) 、作業進度更新和即時表單。</span><span class="sxs-lookup"><span data-stu-id="ad00d-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="ad00d-116">SignalR 也可提供完全新的 web 應用程式類型，這些 web 應用程式需要伺服器的高頻率更新，例如即時遊戲。</span><span class="sxs-lookup"><span data-stu-id="ad00d-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="ad00d-117">SignalR 提供簡單的 API，可用於建立伺服器對用戶端的遠端程序呼叫， (RPC) 在用戶端瀏覽器中呼叫 JavaScript 函式 (以及從伺服器端 .NET 程式碼) 的其他用戶端平臺。</span><span class="sxs-lookup"><span data-stu-id="ad00d-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="ad00d-118">SignalR 也包含連接管理的 API (例如，連線和中斷連接事件) ，以及群組連接。</span><span class="sxs-lookup"><span data-stu-id="ad00d-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![使用 SignalR 叫用方法](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="ad00d-120">SignalR 會自動處理連線管理，讓您能夠將訊息同時廣播到所有連線的用戶端，例如聊天室。</span><span class="sxs-lookup"><span data-stu-id="ad00d-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="ad00d-121">您也可以將訊息傳送給特定的用戶端。</span><span class="sxs-lookup"><span data-stu-id="ad00d-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="ad00d-122">不同於傳統的 HTTP 連線，用戶端與伺服器之間的連線是持續性的，此連線會基於每次通訊重新建立。</span><span class="sxs-lookup"><span data-stu-id="ad00d-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="ad00d-123">SignalR 支援「伺服器推送」功能，在此功能中，伺服器程式碼可以在瀏覽器中使用遠端程序呼叫 (RPC) 來呼叫用戶端程式代碼，而不是現今 web 上常見的要求-回應模型。</span><span class="sxs-lookup"><span data-stu-id="ad00d-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="ad00d-124">SignalR 應用程式可以使用內建和協力廠商向外延展提供者，向外延展至數千個用戶端。</span><span class="sxs-lookup"><span data-stu-id="ad00d-124">SignalR applications can scale out to thousands of clients using built-in, and third-party scale-out providers.</span></span>

<span data-ttu-id="ad00d-125">內建提供者包括：</span><span class="sxs-lookup"><span data-stu-id="ad00d-125">Built-in providers include:</span></span>
* [<span data-ttu-id="ad00d-126">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="ad00d-126">Service Bus</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [<span data-ttu-id="ad00d-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ad00d-127">SQL Server</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [<span data-ttu-id="ad00d-128">Redis</span><span class="sxs-lookup"><span data-stu-id="ad00d-128">Redis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

<span data-ttu-id="ad00d-129">協力廠商提供者包括：</span><span class="sxs-lookup"><span data-stu-id="ad00d-129">Third-party providers include:</span></span>
* <span data-ttu-id="ad00d-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。</span><span class="sxs-lookup"><span data-stu-id="ad00d-130">[NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html).</span></span>

<span data-ttu-id="ad00d-131">SignalR 是開放原始碼，可透過 [GitHub](https://github.com/signalr)進行存取。</span><span class="sxs-lookup"><span data-stu-id="ad00d-131">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="ad00d-132">SignalR 和 WebSocket</span><span class="sxs-lookup"><span data-stu-id="ad00d-132">SignalR and WebSocket</span></span>

<span data-ttu-id="ad00d-133">SignalR 會使用新的 WebSocket 傳輸（如果有的話），並視需要切換回較舊的傳輸。</span><span class="sxs-lookup"><span data-stu-id="ad00d-133">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="ad00d-134">雖然您當然可以直接使用 WebSocket 來撰寫應用程式，但使用 SignalR 表示已為您完成許多需要執行的額外功能。</span><span class="sxs-lookup"><span data-stu-id="ad00d-134">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="ad00d-135">最重要的是，這表示您可以撰寫應用程式的程式碼以利用 WebSocket，而不必擔心為舊版用戶端建立個別的程式碼路徑。</span><span class="sxs-lookup"><span data-stu-id="ad00d-135">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="ad00d-136">SignalR 也會讓您不必擔心 WebSocket 的更新，因為 SignalR 會更新為支援基礎傳輸的變更，讓您的應用程式在不同的 WebSocket 版本之間提供一致的介面。</span><span class="sxs-lookup"><span data-stu-id="ad00d-136">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="ad00d-137">傳輸和回退</span><span class="sxs-lookup"><span data-stu-id="ad00d-137">Transports and fallbacks</span></span>

<span data-ttu-id="ad00d-138">SignalR 是在用戶端與伺服器之間執行即時工作所需的部分傳輸的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="ad00d-138">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="ad00d-139">SignalR 會先嘗試建立 WebSocket 連接（如果可能的話）。</span><span class="sxs-lookup"><span data-stu-id="ad00d-139">SignalR first attempts to establish a WebSocket connection if possible.</span></span> <span data-ttu-id="ad00d-140">WebSocket 是 SignalR 的最佳傳輸，因為它具有：</span><span class="sxs-lookup"><span data-stu-id="ad00d-140">WebSocket is the optimal transport for SignalR because it has:</span></span>

* <span data-ttu-id="ad00d-141">伺服器記憶體最有效率的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ad00d-141">The most efficient use of server memory.</span></span>
* <span data-ttu-id="ad00d-142">最低延遲。</span><span class="sxs-lookup"><span data-stu-id="ad00d-142">The lowest latency.</span></span>
* <span data-ttu-id="ad00d-143">最基礎的功能，例如用戶端與伺服器之間的全雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="ad00d-143">The most underlying features, such as full duplex communication between client and server.</span></span>
* <span data-ttu-id="ad00d-144">最嚴格的需求是，WebSocket 需要伺服器：</span><span class="sxs-lookup"><span data-stu-id="ad00d-144">The most stringent requirements, WebSocket requires the server:</span></span>
  * <span data-ttu-id="ad00d-145">在 Windows Server 2012 或 Windows 8 上執行。</span><span class="sxs-lookup"><span data-stu-id="ad00d-145">Run on Windows Server 2012 or Windows 8.</span></span>
  * <span data-ttu-id="ad00d-146">.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="ad00d-146">.NET Framework 4.5.</span></span>

<span data-ttu-id="ad00d-147">如果不符合這些需求，SignalR 會嘗試使用其他傳輸來進行連接。</span><span class="sxs-lookup"><span data-stu-id="ad00d-147">If these requirements are not met, SignalR attempts to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="ad00d-148">HTML 5 傳輸</span><span class="sxs-lookup"><span data-stu-id="ad00d-148">HTML 5 transports</span></span>

<span data-ttu-id="ad00d-149">這些傳輸取決於 [HTML 5](http://en.wikipedia.org/wiki/HTML5)的支援。</span><span class="sxs-lookup"><span data-stu-id="ad00d-149">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="ad00d-150">如果用戶端瀏覽器不支援 HTML 5 標準，則會使用較舊的傳輸。</span><span class="sxs-lookup"><span data-stu-id="ad00d-150">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="ad00d-151">如果伺服器和瀏覽器兩者都指出可支援 Websocket) ，則 (**websocket** 。</span><span class="sxs-lookup"><span data-stu-id="ad00d-151">**WebSocket** (if both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="ad00d-152">WebSocket 是唯一在用戶端與伺服器之間建立真正持續性雙向連線的傳輸方式。</span><span class="sxs-lookup"><span data-stu-id="ad00d-152">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="ad00d-153">不過，WebSocket 也有最嚴格的需求;只有最新版本的 Microsoft Internet Explorer、Google Chrome 和 Mozilla Firefox 才會受到完整支援，而且在其他瀏覽器（例如 Opera 和 Safari）中只會有部分執行。</span><span class="sxs-lookup"><span data-stu-id="ad00d-153">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="ad00d-154">如果瀏覽器支援伺服器傳送的事件，也就是**伺服器傳送的事件**（也稱為 EventSource (，這基本上是除了 Internet Explorer 以外的所有瀏覽器。 ) </span><span class="sxs-lookup"><span data-stu-id="ad00d-154">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="ad00d-155">Comet 傳輸</span><span class="sxs-lookup"><span data-stu-id="ad00d-155">Comet transports</span></span>

<span data-ttu-id="ad00d-156">下列傳輸是以 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 應用程式模型為基礎，在此模型中，瀏覽器或其他用戶端會維護長時間的 HTTP 要求，而伺服器可以使用它來將資料推送至用戶端，而不需要用戶端特別要求它。</span><span class="sxs-lookup"><span data-stu-id="ad00d-156">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="ad00d-157">**永遠** 只有 Internet Explorer) 的框架 (。</span><span class="sxs-lookup"><span data-stu-id="ad00d-157">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="ad00d-158">永久框架會建立隱藏的 IFrame，以對伺服器上未完成的端點提出要求。</span><span class="sxs-lookup"><span data-stu-id="ad00d-158">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="ad00d-159">伺服器接著會持續將腳本傳送給立即執行的用戶端，提供從伺服器到用戶端的單向即時連線。</span><span class="sxs-lookup"><span data-stu-id="ad00d-159">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="ad00d-160">從用戶端到伺服器的連接會使用不同于伺服器與用戶端連線的連接，而且就像標準的 HTTP 要求一樣，會針對每個需要傳送的資料片段建立新的連接。</span><span class="sxs-lookup"><span data-stu-id="ad00d-160">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="ad00d-161">**Ajax 長時間輪詢**。</span><span class="sxs-lookup"><span data-stu-id="ad00d-161">**Ajax long polling**.</span></span> <span data-ttu-id="ad00d-162">長時間輪詢不會建立持續性連接，但是會在伺服器回應之前，以保持開啟狀態的要求來輪詢伺服器，此時會關閉連線，並立即要求新的連接。</span><span class="sxs-lookup"><span data-stu-id="ad00d-162">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="ad00d-163">這可能會在連接重設時造成一些延遲。</span><span class="sxs-lookup"><span data-stu-id="ad00d-163">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="ad00d-164">如需在哪些設定下支援哪些傳輸的詳細資訊，請參閱 [支援的平臺](supported-platforms.md)。</span><span class="sxs-lookup"><span data-stu-id="ad00d-164">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="ad00d-165">傳輸選取進程</span><span class="sxs-lookup"><span data-stu-id="ad00d-165">Transport selection process</span></span>

<span data-ttu-id="ad00d-166">下列清單顯示 SignalR 用來決定要使用哪個傳輸的步驟。</span><span class="sxs-lookup"><span data-stu-id="ad00d-166">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="ad00d-167">如果瀏覽器是 Internet Explorer 8 或更早的版本，則會使用長輪詢。</span><span class="sxs-lookup"><span data-stu-id="ad00d-167">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="ad00d-168">如果設定了 JSONP (也就是， `jsonp` 參數會設定為 `true` 啟動連接) 時，會使用長時間輪詢。</span><span class="sxs-lookup"><span data-stu-id="ad00d-168">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="ad00d-169">如果正在進行跨網域連線 (也就是說，如果 SignalR 端點與裝載頁面) 不在相同的網域中，則會在符合下列條件時使用 WebSocket：</span><span class="sxs-lookup"><span data-stu-id="ad00d-169">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="ad00d-170">用戶端支援 CORS (跨原始資源分享) 。</span><span class="sxs-lookup"><span data-stu-id="ad00d-170">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="ad00d-171">如需哪些用戶端支援 CORS 的詳細資訊，請參閱 [caniuse.com 的 cors](http://www.caniuse.com/CORS)。</span><span class="sxs-lookup"><span data-stu-id="ad00d-171">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="ad00d-172">用戶端支援 WebSocket</span><span class="sxs-lookup"><span data-stu-id="ad00d-172">The client supports WebSocket</span></span>
   - <span data-ttu-id="ad00d-173">伺服器支援 WebSocket</span><span class="sxs-lookup"><span data-stu-id="ad00d-173">The server supports WebSocket</span></span>

     <span data-ttu-id="ad00d-174">如果不符合上述任何準則，將會使用長時間輪詢。</span><span class="sxs-lookup"><span data-stu-id="ad00d-174">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="ad00d-175">如需跨網域連接的詳細資訊，請參閱 [如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="ad00d-175">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="ad00d-176">如果未設定 JSONP，且連接不是跨網域，則會在用戶端和伺服器都支援時使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="ad00d-176">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="ad00d-177">如果用戶端或伺服器不支援 WebSocket，則會使用伺服器傳送的事件（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="ad00d-177">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="ad00d-178">如果無法使用伺服器傳送的事件，則會嘗試永久框架。</span><span class="sxs-lookup"><span data-stu-id="ad00d-178">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="ad00d-179">如果永久框架失敗，則會使用長時間輪詢。</span><span class="sxs-lookup"><span data-stu-id="ad00d-179">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="ad00d-180">監視傳輸</span><span class="sxs-lookup"><span data-stu-id="ad00d-180">Monitoring transports</span></span>

<span data-ttu-id="ad00d-181">您可以藉由在中樞上啟用記錄功能，並在瀏覽器中開啟主控台視窗，來判斷應用程式所使用的傳輸。</span><span class="sxs-lookup"><span data-stu-id="ad00d-181">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="ad00d-182">若要在瀏覽器中啟用中樞事件的記錄，請將下列命令新增至您的用戶端應用程式：</span><span class="sxs-lookup"><span data-stu-id="ad00d-182">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="ad00d-183">在 Internet Explorer 中，按 F12 開啟開發人員工具，然後按一下 [主控台] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ad00d-183">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer 中的主控台](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="ad00d-185">在 Chrome 中，按 Ctrl + Shift + J 開啟主控台。</span><span class="sxs-lookup"><span data-stu-id="ad00d-185">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome 中的主控台](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="ad00d-187">開啟主控台並啟用記錄之後，您就可以查看 SignalR 正在使用的傳輸。</span><span class="sxs-lookup"><span data-stu-id="ad00d-187">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![顯示 WebSocket 傳輸 Internet Explorer 中的主控台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="ad00d-189">指定傳輸</span><span class="sxs-lookup"><span data-stu-id="ad00d-189">Specifying a transport</span></span>

<span data-ttu-id="ad00d-190">協調傳輸需要經過一段時間和用戶端/伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="ad00d-190">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="ad00d-191">如果已知用戶端功能，則可以在用戶端連接啟動時指定傳輸。</span><span class="sxs-lookup"><span data-stu-id="ad00d-191">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="ad00d-192">下列程式碼片段示範如何使用 Ajax Long 輪詢傳輸來啟動連接，如果已知用戶端不支援任何其他通訊協定，就會使用：</span><span class="sxs-lookup"><span data-stu-id="ad00d-192">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="ad00d-193">如果您想要讓用戶端依序嘗試特定的傳輸，則可以指定回溯順序。</span><span class="sxs-lookup"><span data-stu-id="ad00d-193">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="ad00d-194">下列程式碼片段示範如何嘗試 WebSocket，以及失敗的情況，並直接進入長時間輪詢。</span><span class="sxs-lookup"><span data-stu-id="ad00d-194">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="ad00d-195">指定傳輸的字串常數定義如下：</span><span class="sxs-lookup"><span data-stu-id="ad00d-195">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="ad00d-196">連接和中樞</span><span class="sxs-lookup"><span data-stu-id="ad00d-196">Connections and Hubs</span></span>

<span data-ttu-id="ad00d-197">SignalR API 包含兩個模型，可在用戶端與伺服器之間進行通訊：持續連線和中樞。</span><span class="sxs-lookup"><span data-stu-id="ad00d-197">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="ad00d-198">連接代表傳送單一收件者、群組或廣播訊息的簡單端點。</span><span class="sxs-lookup"><span data-stu-id="ad00d-198">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="ad00d-199">持續連線 API (在 .NET 程式碼中以 PersistentConnection 類別表示，) 可讓開發人員直接存取 SignalR 公開的低層級通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ad00d-199">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="ad00d-200">使用以連線為基礎的 Api （例如 Windows Communication Foundation）的開發人員很熟悉如何使用連接通訊模型。</span><span class="sxs-lookup"><span data-stu-id="ad00d-200">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="ad00d-201">中樞是以連接 API 為基礎所建立的高階管線，可讓您的用戶端和伺服器直接呼叫彼此的方法。</span><span class="sxs-lookup"><span data-stu-id="ad00d-201">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="ad00d-202">SignalR 可處理跨電腦界限的分派，就像魔術一樣，讓用戶端可以像本機方法一樣輕鬆地在伺服器上呼叫方法，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="ad00d-202">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="ad00d-203">使用「遠端叫用 Api」（例如 .NET 遠端處理）的開發人員會熟悉中樞通訊模型。</span><span class="sxs-lookup"><span data-stu-id="ad00d-203">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="ad00d-204">使用中樞也可讓您將強型別參數傳遞給方法，以啟用模型系結。</span><span class="sxs-lookup"><span data-stu-id="ad00d-204">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="ad00d-205">架構圖</span><span class="sxs-lookup"><span data-stu-id="ad00d-205">Architecture diagram</span></span>

<span data-ttu-id="ad00d-206">下圖顯示中樞、持續連線和用於傳輸的基礎技術之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="ad00d-206">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![顯示 Api、傳輸和用戶端的 SignalR 架構圖](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="ad00d-208">中樞的運作方式</span><span class="sxs-lookup"><span data-stu-id="ad00d-208">How Hubs work</span></span>

<span data-ttu-id="ad00d-209">當伺服器端程式碼在用戶端上呼叫方法時，會在作用中的傳輸上傳送封包，其中包含要呼叫之方法的名稱和參數 (當物件傳送為方法參數時，就會使用 JSON) 進行序列化。</span><span class="sxs-lookup"><span data-stu-id="ad00d-209">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="ad00d-210">然後，用戶端會比對方法名稱與用戶端程式代碼中定義的方法。</span><span class="sxs-lookup"><span data-stu-id="ad00d-210">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="ad00d-211">如果有相符的，則會使用已還原序列化的參數資料來執行用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="ad00d-211">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="ad00d-212">您可以使用 Fiddler 之類的工具來監視方法呼叫 [。](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="ad00d-212">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="ad00d-213">下圖顯示在 Fiddler 的 [記錄] 窗格中，從 SignalR 伺服器傳送至網頁瀏覽器用戶端的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="ad00d-213">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="ad00d-214">從名為的中樞傳送方法呼叫 `MoveShapeHub` ，並呼叫所叫用的方法 `updateShape` 。</span><span class="sxs-lookup"><span data-stu-id="ad00d-214">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![顯示 SignalR 流量的 Fiddler 記錄視圖](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="ad00d-216">在此範例中，中樞名稱會以參數識別 `H` ，方法名稱會以 `M` 參數識別，而傳送至方法的資料會以 `A` 參數識別。</span><span class="sxs-lookup"><span data-stu-id="ad00d-216">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="ad00d-217">產生此訊息的應用程式是在 [高頻率即時](tutorial-high-frequency-realtime-with-signalr.md) 教學課程中建立的。</span><span class="sxs-lookup"><span data-stu-id="ad00d-217">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="ad00d-218">選擇通訊模型</span><span class="sxs-lookup"><span data-stu-id="ad00d-218">Choosing a communication model</span></span>

<span data-ttu-id="ad00d-219">大部分的應用程式都應該使用中樞 API。</span><span class="sxs-lookup"><span data-stu-id="ad00d-219">Most applications should use the Hubs API.</span></span> <span data-ttu-id="ad00d-220">連接 API 可用於下列情況：</span><span class="sxs-lookup"><span data-stu-id="ad00d-220">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="ad00d-221">需要指定所傳送的實際訊息格式。</span><span class="sxs-lookup"><span data-stu-id="ad00d-221">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="ad00d-222">開發人員偏好使用訊息和分派模型，而不是遠端調用模型。</span><span class="sxs-lookup"><span data-stu-id="ad00d-222">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="ad00d-223">使用訊息模型的現有應用程式正在移植以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="ad00d-223">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
