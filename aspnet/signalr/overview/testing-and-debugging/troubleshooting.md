---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR 疑難排解 |Microsoft Docs
author: bradygaster
description: 本文說明開發 SignalR 應用程式的常見問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3e3ba353184f94621ffc0fb1c50647caf1a89514
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59402761"
---
# <a name="signalr-troubleshooting"></a><span data-ttu-id="e241d-103">SignalR 疑難排解</span><span class="sxs-lookup"><span data-stu-id="e241d-103">SignalR Troubleshooting</span></span>

<span data-ttu-id="e241d-104">藉由[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e241d-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="e241d-105">本文件說明使用 SignalR 的常見疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="e241d-105">This document describes common troubleshooting issues with SignalR.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="e241d-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="e241d-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="e241d-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e241d-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="e241d-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="e241d-108">.NET 4.5</span></span>
> - <span data-ttu-id="e241d-109">SignalR 第 2 版</span><span class="sxs-lookup"><span data-stu-id="e241d-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="e241d-110">本主題的上一個版本</span><span class="sxs-lookup"><span data-stu-id="e241d-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="e241d-111">如需舊版 SignalR 的資訊，請參閱[SignalR 舊版](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="e241d-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="e241d-112">提出問題或意見</span><span class="sxs-lookup"><span data-stu-id="e241d-112">Questions and comments</span></span>
>
> <span data-ttu-id="e241d-113">您喜歡本教學課程中的方式，和我們可以改善在頁面底部的註解中，歡迎留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="e241d-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="e241d-114">如果您有不直接相關的教學課程中的問題，您可以張貼他們[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或是[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="e241d-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="e241d-115">本文件包含下列各節。</span><span class="sxs-lookup"><span data-stu-id="e241d-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="e241d-116">以無訊息方式失敗呼叫用戶端與伺服器之間的方法</span><span class="sxs-lookup"><span data-stu-id="e241d-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="e241d-117">設定 IIS websockets，ping/pong 來偵測無作用的用戶端</span><span class="sxs-lookup"><span data-stu-id="e241d-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="e241d-118">其他連線問題</span><span class="sxs-lookup"><span data-stu-id="e241d-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="e241d-119">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="e241d-120">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="e241d-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="e241d-121">Internet Information Services 的問題</span><span class="sxs-lookup"><span data-stu-id="e241d-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="e241d-122">Microsoft Azure 問題</span><span class="sxs-lookup"><span data-stu-id="e241d-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="e241d-123">以無訊息方式失敗呼叫用戶端與伺服器之間的方法</span><span class="sxs-lookup"><span data-stu-id="e241d-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="e241d-124">本章節描述針對方法呼叫失敗不會有意義的錯誤訊息的用戶端與伺服器之間的可能原因。</span><span class="sxs-lookup"><span data-stu-id="e241d-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="e241d-125">SignalR 應用程式中，伺服器會有任何用戶端會實作; 方法的相關資訊當伺服器叫用的用戶端方法，方法名稱和參數資料傳送到用戶端，和方法，就會執行只存在於伺服器指定的格式。</span><span class="sxs-lookup"><span data-stu-id="e241d-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="e241d-126">如果沒有符合的方法會找到在用戶端，會發生任何事，而且不會引發錯誤訊息的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="e241d-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="e241d-127">若要進一步調查用戶端未呼叫的方法，您可以開啟之前呼叫 start 方法上的中樞，以查看哪些呼叫來自伺服器的記錄。</span><span class="sxs-lookup"><span data-stu-id="e241d-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="e241d-128">若要啟用記錄中的 JavaScript 應用程式，請參閱[如何啟用用戶端記錄 （JavaScript 用戶端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="e241d-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="e241d-129">若要啟用記錄功能在.NET 用戶端應用程式，請參閱[如何啟用用戶端記錄 （.NET 用戶端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。</span><span class="sxs-lookup"><span data-stu-id="e241d-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="e241d-130">拼錯的方法、 不正確的方法簽章或不正確的中樞名稱</span><span class="sxs-lookup"><span data-stu-id="e241d-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="e241d-131">如果名稱或被呼叫的方法簽章不完全符合適當的方法，用戶端上，呼叫會失敗。</span><span class="sxs-lookup"><span data-stu-id="e241d-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="e241d-132">請確認伺服器所呼叫的方法名稱符合用戶端上方法的名稱。</span><span class="sxs-lookup"><span data-stu-id="e241d-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="e241d-133">此外，SignalR 建立中樞 proxy 使用依照 camel 命名法大小寫的方法，為適用於 JavaScript，因此呼叫的方法`SendMessage`會呼叫伺服器上`sendMessage`中用戶端 proxy。</span><span class="sxs-lookup"><span data-stu-id="e241d-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="e241d-134">如果您使用`HubName`您伺服器端程式碼中的屬性，請確認所使用的名稱，符合用來在用戶端建立中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="e241d-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="e241d-135">如果您不要使用`HubName`屬性，則驗證中的 JavaScript 用戶端中樞的名稱是依照 camel 命名法大小寫慣例，而不是 ChatHub chatHub 等。</span><span class="sxs-lookup"><span data-stu-id="e241d-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="e241d-136">重複的用戶端上的方法名稱</span><span class="sxs-lookup"><span data-stu-id="e241d-136">Duplicate method name on client</span></span>

<span data-ttu-id="e241d-137">請確認，您不需要重複的方法只有大小寫不同的用戶端上。</span><span class="sxs-lookup"><span data-stu-id="e241d-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="e241d-138">如果用戶端應用程式有一個方法，叫做`sendMessage`，確認沒有也呼叫的方法`SendMessage`以及。</span><span class="sxs-lookup"><span data-stu-id="e241d-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="e241d-139">在用戶端上遺漏的 JSON 剖析器</span><span class="sxs-lookup"><span data-stu-id="e241d-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="e241d-140">SignalR 需要 JSON 剖析器要出現序列化伺服器與用戶端之間的呼叫。</span><span class="sxs-lookup"><span data-stu-id="e241d-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="e241d-141">如果您的用戶端沒有內建的 JSON 剖析器 （例如 Internet Explorer 7)，您必須包含在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e241d-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="e241d-142">您可以下載 JSON 剖析器[此處](http://nuget.org/packages/json2)。</span><span class="sxs-lookup"><span data-stu-id="e241d-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="e241d-143">混用中樞 PersistentConnection 語法</span><span class="sxs-lookup"><span data-stu-id="e241d-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="e241d-144">SignalR 使用兩種通訊模式：中樞和 PersistentConnections。</span><span class="sxs-lookup"><span data-stu-id="e241d-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="e241d-145">呼叫這兩個通訊模型的語法是不同的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="e241d-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="e241d-146">如果您已新增中樞伺服器程式碼中，確認所有用戶端程式碼會使用適當的中樞語法。</span><span class="sxs-lookup"><span data-stu-id="e241d-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

**<span data-ttu-id="e241d-147">建立 PersistentConnection JavaScript 用戶端中的 JavaScript 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-147">JavaScript client code that creates a PersistentConnection in a JavaScript client</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**<span data-ttu-id="e241d-148">建立 Javascript 用戶端中的中樞 Proxy 的 JavaScript 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-148">JavaScript client code that creates a Hub Proxy in a Javascript client</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**<span data-ttu-id="e241d-149">C# 伺服端程式碼會將路由對應到 PersistentConnection</span><span class="sxs-lookup"><span data-stu-id="e241d-149">C# server code that maps a route to a PersistentConnection</span></span>**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**<span data-ttu-id="e241d-150">C#路由至中樞，或對應至多個中樞有多個應用程式的伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-150">C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications</span></span>**

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="e241d-151">開始之前會加入訂用帳戶的連線</span><span class="sxs-lookup"><span data-stu-id="e241d-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="e241d-152">如果可以從伺服器呼叫的方法加入至 proxy 之前啟動中樞的連接，就不會收到訊息。</span><span class="sxs-lookup"><span data-stu-id="e241d-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="e241d-153">下列 JavaScript 程式碼將不會啟動中樞正確：</span><span class="sxs-lookup"><span data-stu-id="e241d-153">The following JavaScript code will not start the hub properly:</span></span>

**<span data-ttu-id="e241d-154">不正確 JavaScript 用戶端程式碼，不允許中樞接收訊息</span><span class="sxs-lookup"><span data-stu-id="e241d-154">Incorrect JavaScript client code that will not allow Hubs messages to be received</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="e241d-155">相反地，加入方法的訂用帳戶呼叫開始之前：</span><span class="sxs-lookup"><span data-stu-id="e241d-155">Instead, add the method subscriptions before calling Start:</span></span>

**<span data-ttu-id="e241d-156">正確加入至中樞的 訂用帳戶的 JavaScript 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-156">JavaScript client code that correctly adds subscriptions to a hub</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="e241d-157">中樞 proxy 上遺漏的方法名稱</span><span class="sxs-lookup"><span data-stu-id="e241d-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="e241d-158">請確認訂閱用戶端上，在伺服器上定義的方法。</span><span class="sxs-lookup"><span data-stu-id="e241d-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="e241d-159">即使伺服器定義的方法，它必須仍會加入至用戶端 proxy。</span><span class="sxs-lookup"><span data-stu-id="e241d-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="e241d-160">方法可以透過下列方式新增至用戶端 proxy (請注意，此方法會加入至`client`中樞，而不是中樞直接的成員):</span><span class="sxs-lookup"><span data-stu-id="e241d-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

**<span data-ttu-id="e241d-161">將方法新增至中樞 proxy 的 JavaScript 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-161">JavaScript client code that adds methods to a hub proxy</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="e241d-162">中樞或中樞方法未宣告為公用</span><span class="sxs-lookup"><span data-stu-id="e241d-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="e241d-163">若要顯示在用戶端上，在中樞實作和方法必須宣告為`public`。</span><span class="sxs-lookup"><span data-stu-id="e241d-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="e241d-164">從不同的應用程式存取中樞</span><span class="sxs-lookup"><span data-stu-id="e241d-164">Accessing hub from a different application</span></span>

<span data-ttu-id="e241d-165">SignalR 中樞只能透過實作 SignalR 用戶端的應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="e241d-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="e241d-166">SignalR 無法交互操作，與其他的通訊程式庫 （例如 SOAP 或 WCF web 服務。）如果沒有可供您的目標平台的 SignalR 用戶端，您無法直接存取伺服器的端點。</span><span class="sxs-lookup"><span data-stu-id="e241d-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="e241d-167">以手動方式將資料序列化</span><span class="sxs-lookup"><span data-stu-id="e241d-167">Manually serializing data</span></span>

<span data-ttu-id="e241d-168">SignalR 會自動使用 JSON 序列化程式的方法參數那里的不需要自行進行此作業。</span><span class="sxs-lookup"><span data-stu-id="e241d-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="e241d-169">遠端未在 OnDisconnected 函式中的用戶端上執行的中樞方法</span><span class="sxs-lookup"><span data-stu-id="e241d-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="e241d-170">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-170">This behavior is by design.</span></span> <span data-ttu-id="e241d-171">當`OnDisconnected`是呼叫，中樞已進入`Disconnected`不允許進一步的中樞方法呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="e241d-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

**<span data-ttu-id="e241d-172">C# 伺服端程式碼正確執行 OnDisconnected 事件中的 程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-172">C# server code that correctly executes code in the OnDisconnected event</span></span>**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="e241d-173">OnDisconnect 未引發一致的時間</span><span class="sxs-lookup"><span data-stu-id="e241d-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="e241d-174">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-174">This behavior is by design.</span></span> <span data-ttu-id="e241d-175">當使用者嘗試離開頁面有使用中的 SignalR 連線時，則 SignalR 用戶端接著便可通知伺服器將會停止用戶端連線的最佳嘗試。</span><span class="sxs-lookup"><span data-stu-id="e241d-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="e241d-176">如果 SignalR 用戶端的最佳嘗試無法連線到伺服器，伺服器將會處置之後可設定的連接`DisconnectTimeout`更新版本中，在這段`OnDisconnected`事件就會引發。</span><span class="sxs-lookup"><span data-stu-id="e241d-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="e241d-177">如果 SignalR 用戶端的最佳嘗試會成功，`OnDisconnected`事件就會立即引發。</span><span class="sxs-lookup"><span data-stu-id="e241d-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="e241d-178">如需設定資訊`DisconnectTimeout`設定，請參閱[處理連線存留期事件：DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)。</span><span class="sxs-lookup"><span data-stu-id="e241d-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="e241d-179">已達到連線限制</span><span class="sxs-lookup"><span data-stu-id="e241d-179">Connection limit reached</span></span>

<span data-ttu-id="e241d-180">當用戶端作業系統，例如 Windows 7 上使用完整版的 IIS，10 連接是加諸的限制。</span><span class="sxs-lookup"><span data-stu-id="e241d-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="e241d-181">當使用用戶端作業系統，請改用 IIS Express 若要避免這項限制。</span><span class="sxs-lookup"><span data-stu-id="e241d-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="e241d-182">跨網域連線設定不正確</span><span class="sxs-lookup"><span data-stu-id="e241d-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="e241d-183">如果跨網域連接未正確設定 （的 SignalR URL 不在與裝載網頁位於相同網域的連線），沒有錯誤訊息，則連線可能失敗。</span><span class="sxs-lookup"><span data-stu-id="e241d-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="e241d-184">如需如何啟用跨網域通訊的詳細資訊，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="e241d-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="e241d-185">使用 NTLM (Active Directory) 不在.NET 用戶端的連線</span><span class="sxs-lookup"><span data-stu-id="e241d-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="e241d-186">如果連接未正確設定，使用網域安全性的.NET 用戶端應用程式中的連接可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e241d-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="e241d-187">若要使用 SignalR 網域環境中，將必要的連接屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e241d-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

**<span data-ttu-id="e241d-188">C# 用戶端程式碼實作連線認證</span><span class="sxs-lookup"><span data-stu-id="e241d-188">C# client code that implements connection credentials</span></span>**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="e241d-189">設定 IIS websockets，ping/pong 來偵測無作用的用戶端</span><span class="sxs-lookup"><span data-stu-id="e241d-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="e241d-190">SignalR 伺服器不知道，是否用戶端是廢與否，而且它們都依賴來自基礎 websocket 連線失敗的通知，也就是，`OnClose`回呼。</span><span class="sxs-lookup"><span data-stu-id="e241d-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the `OnClose` callback.</span></span> <span data-ttu-id="e241d-191">此問題的解決方案之一是設定為您執行 ping/pong IIS websockets。</span><span class="sxs-lookup"><span data-stu-id="e241d-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="e241d-192">這可確保如果意外中斷，將會關閉您的連線。</span><span class="sxs-lookup"><span data-stu-id="e241d-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="e241d-193">如需詳細資訊，請參閱[這篇 stackoverflow 文章](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)。</span><span class="sxs-lookup"><span data-stu-id="e241d-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="e241d-194">其他連線問題</span><span class="sxs-lookup"><span data-stu-id="e241d-194">Other connection issues</span></span>

<span data-ttu-id="e241d-195">本章節描述的原因和解決方案的特定徵狀或在連接期間發生的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e241d-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="e241d-196">「 在傳送資料前，必須呼叫啟動 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="e241d-197">如果程式碼會在開始連接之前，先將 SignalR 物件參考，通常可以看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="e241d-198">處理常式和類似裝設，會呼叫方法，在伺服器上定義必須新增連線完成後。</span><span class="sxs-lookup"><span data-stu-id="e241d-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="e241d-199">請注意，呼叫`Start`是非同步的因此程式碼之後呼叫可能會執行它之前完成。</span><span class="sxs-lookup"><span data-stu-id="e241d-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="e241d-200">若要連接完全啟動之後，加入處理常式，最好是將它們放到做為參數傳遞至 start 方法的回呼函式：</span><span class="sxs-lookup"><span data-stu-id="e241d-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

**<span data-ttu-id="e241d-201">正確地將參考 SignalR 物件的事件處理常式的 JavaScript 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-201">JavaScript client code that correctly adds event handlers that reference SignalR objects</span></span>**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="e241d-202">如果仍然正在參考 SignalR 物件時，就會停止連線，也會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="e241d-203">「 永久 301 已移動 」 或者 「 暫時 302 已移動 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="e241d-204">如果專案包含名為 SignalR 會干擾自動建立 proxy 的資料夾，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="e241d-205">若要避免這個錯誤，不使用名為的資料夾`SignalR`在您的應用程式或關閉自動 proxy 產生關閉。</span><span class="sxs-lookup"><span data-stu-id="e241d-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="e241d-206">請參閱[產生的 Proxy，它會為您](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="e241d-207">在.NET 或 Silverlight 用戶端的 「 403 禁止 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="e241d-208">在其中跨網域通訊未正確啟用的跨網域環境中可能會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="e241d-209">如需如何啟用跨網域通訊的詳細資訊，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="e241d-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="e241d-210">若要建立跨網域連接 Silverlight 用戶端中的，請參閱[來自 Silverlight 用戶端的跨網域連線](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="e241d-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="e241d-211">「 找不到 404 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-211">"404 Not Found" error</span></span>

<span data-ttu-id="e241d-212">有多種原因會導致此問題。</span><span class="sxs-lookup"><span data-stu-id="e241d-212">There are several causes for this issue.</span></span> <span data-ttu-id="e241d-213">請確認下列各項：</span><span class="sxs-lookup"><span data-stu-id="e241d-213">Verify all of the following:</span></span>

- <span data-ttu-id="e241d-214">**中樞 proxy 的位址參考的格式不正確：** 如果產生的中樞 proxy 位址的參考的格式不正確，通常會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="e241d-215">確認會正確地設定中樞位址的參考。</span><span class="sxs-lookup"><span data-stu-id="e241d-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="e241d-216">請參閱[如何參考動態產生的 proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="e241d-217">**加入應用程式，然後再加入中樞路由的路由：** 如果您的應用程式使用其他路由，請確認新增的第一個路由會呼叫`MapSignalR`。</span><span class="sxs-lookup"><span data-stu-id="e241d-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="e241d-218">**使用 IIS 7 或沒有更新 7.5 無副檔名的 url:** 使用 IIS 7 或 7.5 無副檔名的 url 需要更新，以便在伺服器可以提供存取中樞定義`/signalr/hubs`。</span><span class="sxs-lookup"><span data-stu-id="e241d-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="e241d-219">您可以找到更新[此處](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="e241d-219">The update can be found [here](https://support.microsoft.com/kb/980368).</span></span>
- <span data-ttu-id="e241d-220">**IIS 快取過期或已損毀：** 若要確認快取內容不會過期，請清除快取的 PowerShell 視窗中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="e241d-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="e241d-221">「 500 內部伺服器錯誤 」</span><span class="sxs-lookup"><span data-stu-id="e241d-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="e241d-222">這是種泛泛的錯誤，可能有各種不同的原因。</span><span class="sxs-lookup"><span data-stu-id="e241d-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="e241d-223">錯誤的詳細資料應該會出現在伺服器的事件記錄檔，或可透過偵錯伺服器。</span><span class="sxs-lookup"><span data-stu-id="e241d-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="e241d-224">藉由開啟詳細的錯誤，伺服器上可取得更詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="e241d-225">如需詳細資訊，請參閱 <<c0> [ 如何處理中樞類別中的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="e241d-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="e241d-226">如果防火牆或 proxy 設定不正確，導致重寫要求標頭，通常也會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="e241d-227">解決方法是請確定連接埠 80 已啟用防火牆或 proxy 上。</span><span class="sxs-lookup"><span data-stu-id="e241d-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="e241d-228">「 非預期的回應碼：500"</span><span class="sxs-lookup"><span data-stu-id="e241d-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="e241d-229">如果應用程式中使用的.NET framework 版本不符合在 Web.Config 中指定的版本，可能會發生此錯誤。解決方法是確認.NET 4.5 用於應用程式設定和 Web.Config 檔案。</span><span class="sxs-lookup"><span data-stu-id="e241d-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="e241d-230">「 TypeError: &lt;hubType&gt;是未定義 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="e241d-231">如果將產生此錯誤的呼叫`MapSignalR`，不會正確。</span><span class="sxs-lookup"><span data-stu-id="e241d-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="e241d-232">請參閱[如何註冊 SignalR 中介軟體，並設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="e241d-233">JsonSerializationException 未處理使用者程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="e241d-234">請確認您傳送給您的方法的參數不包含非可序列化的型別 （例如檔案控制代碼或資料庫連接）。</span><span class="sxs-lookup"><span data-stu-id="e241d-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="e241d-235">如果您需要在您不想要傳送至用戶端 （無論是安全性或序列化的原因），使用伺服器端物件上使用成員`JSONIgnore`屬性。</span><span class="sxs-lookup"><span data-stu-id="e241d-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="e241d-236">「 通訊協定錯誤：未知的傳輸中 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="e241d-237">如果用戶端不支援 SignalR 使用的傳輸，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="e241d-238">請參閱[傳輸和後援](../getting-started/introduction-to-signalr.md#transports)所在的瀏覽器可以使用與 SignalR 的資訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="e241d-239">「 JavaScript 中樞 proxy 的產生具有已停用。 」</span><span class="sxs-lookup"><span data-stu-id="e241d-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="e241d-240">如果會發生此錯誤`DisableJavaScriptProxies`時也包括在動態產生之 proxy 的參考設定`signalr/hubs`。</span><span class="sxs-lookup"><span data-stu-id="e241d-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="e241d-241">如需有關如何手動建立 proxy 的詳細資訊，請參閱 <<c0> [ 產生的 proxy，它會為您](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="e241d-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="e241d-242">"的格式不正確的連接識別碼 」 或 「 使用者身分識別不能變更期間作用中的 SignalR 連線 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="e241d-243">如果使用驗證時，並停止連線之前，登出用戶端，可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="e241d-244">解決方法是停止前用戶端登出 SignalR 連線。</span><span class="sxs-lookup"><span data-stu-id="e241d-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="e241d-245">「 無法攔截錯誤：找不到 SignalR: jQuery。</span><span class="sxs-lookup"><span data-stu-id="e241d-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="e241d-246">請確定 jQuery 參考 SignalR.js 檔案前 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="e241d-247">SignalR JavaScript 用戶端需要執行的 jQuery。</span><span class="sxs-lookup"><span data-stu-id="e241d-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="e241d-248">請確認您參考 jQuery 是正確的所使用的路徑有效，且參考至 jQuery 是 signalr 參考之前。</span><span class="sxs-lookup"><span data-stu-id="e241d-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="e241d-249">「 無法攔截 TypeError:無法讀取屬性 '&lt;屬性&gt;' 未定義 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="e241d-250">從沒有 jQuery 或參考正確的中樞 proxy 會產生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="e241d-251">請確認您到 jQuery 和中樞 proxy 的參考正確，所使用的路徑有效，且參考 jQuery 是之前的中樞 proxy 的參考。</span><span class="sxs-lookup"><span data-stu-id="e241d-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="e241d-252">中樞 proxy 的預設參考看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="e241d-252">The default reference to the hubs proxy should look like the following:</span></span>

**<span data-ttu-id="e241d-253">正確地參考中樞 proxy 的 HTML 用戶端程式碼</span><span class="sxs-lookup"><span data-stu-id="e241d-253">HTML client-side code that correctly references the Hubs proxy</span></span>**

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="e241d-254">「 使用者程式碼未處理 RuntimeBinderException 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="e241d-255">可能會發生此錯誤時的不正確的多載`Hub.On`用。</span><span class="sxs-lookup"><span data-stu-id="e241d-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="e241d-256">如果方法具有傳回值，傳回的型別必須指定為泛型類型參數：</span><span class="sxs-lookup"><span data-stu-id="e241d-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

**<span data-ttu-id="e241d-257">（沒有產生的 proxy) 的用戶端上定義的方法</span><span class="sxs-lookup"><span data-stu-id="e241d-257">Method defined on the client (without generated proxy)</span></span>**

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="e241d-258">連線識別碼不一致或頁面載入之間的連線中斷</span><span class="sxs-lookup"><span data-stu-id="e241d-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="e241d-259">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-259">This behavior is by design.</span></span> <span data-ttu-id="e241d-260">因為中樞物件裝載在的頁面物件中，當頁面重新整理時，就會終結中樞。</span><span class="sxs-lookup"><span data-stu-id="e241d-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="e241d-261">多頁應用程式需要維護使用者與連線識別碼的關聯，以便將其載入頁面之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="e241d-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="e241d-262">可以在伺服器上儲存的連線識別碼`ConcurrentDictionary`物件或資料庫。</span><span class="sxs-lookup"><span data-stu-id="e241d-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="e241d-263">"Value cannot be null 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-263">"Value cannot be null" error</span></span>

<span data-ttu-id="e241d-264">目前不支援伺服器端方法，以選擇性的參數;如果省略選擇性參數，則此方法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e241d-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="e241d-265">如需詳細資訊，請參閱 <<c0> [ 選擇性參數](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="e241d-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="e241d-266">「 Firefox 無法連接到伺服器&lt;地址&gt;」 在 Firebug 中的錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="e241d-267">如果 WebSocket 傳輸的交涉失敗，而另一種傳輸會改為使用相同，就可以在 Firebug 中看到此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e241d-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="e241d-268">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="e241d-269">在.NET 用戶端應用程式中的 「 遠端憑證無效根據驗證程序 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="e241d-270">如果您的伺服器需要自訂用戶端憑證，然後您可以加入 x509certificate 連接之前提出要求。</span><span class="sxs-lookup"><span data-stu-id="e241d-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="e241d-271">將憑證新增至連線使用`Connection.AddClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="e241d-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="e241d-272">驗證逾時之後，會卸除連接</span><span class="sxs-lookup"><span data-stu-id="e241d-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="e241d-273">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-273">This behavior is by design.</span></span> <span data-ttu-id="e241d-274">連線處於作用中; 時，就無法修改驗證認證若要重新整理認證，連接必須停止並重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e241d-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="e241d-275">使用 jQuery Mobile 時，兩次呼叫 OnConnected</span><span class="sxs-lookup"><span data-stu-id="e241d-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="e241d-276">jQuery Mobile 的`initializePage`函式會強制重新執行，每個頁面中的指令碼以建立第二個連接。</span><span class="sxs-lookup"><span data-stu-id="e241d-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="e241d-277">此問題的解決方案包括：</span><span class="sxs-lookup"><span data-stu-id="e241d-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="e241d-278">包含您的 JavaScript 檔案之前的 jQuery Mobile 的參考。</span><span class="sxs-lookup"><span data-stu-id="e241d-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="e241d-279">停用`initializePage`函式，藉由設定`$.mobile.autoInitializePage = false`。</span><span class="sxs-lookup"><span data-stu-id="e241d-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="e241d-280">等候完成之前啟動連線初始化頁面。</span><span class="sxs-lookup"><span data-stu-id="e241d-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="e241d-281">訊息會顯示在 Silverlight 應用程式使用伺服器傳送事件</span><span class="sxs-lookup"><span data-stu-id="e241d-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="e241d-282">使用伺服器在 Silverlight 上傳送事件時，會延遲訊息。</span><span class="sxs-lookup"><span data-stu-id="e241d-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="e241d-283">啟動連線時，若要強制長時間輪詢要改為使用中，使用下列：</span><span class="sxs-lookup"><span data-stu-id="e241d-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="e241d-284">不限次數 」 權限遭拒 」 使用框架通訊協定</span><span class="sxs-lookup"><span data-stu-id="e241d-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="e241d-285">這是已知的問題，並說明[此處](https://github.com/SignalR/SignalR/issues/1963)。</span><span class="sxs-lookup"><span data-stu-id="e241d-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="e241d-286">這個徵兆可能會看到使用最新的 JQuery 程式庫;因應措施是降級至 JQuery 1.8.2 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e241d-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="e241d-287">「 InvalidOperationException:不是有效的 web 通訊端要求。</span><span class="sxs-lookup"><span data-stu-id="e241d-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="e241d-288">如果使用 WebSocket 通訊協定，但網路 proxy 正在修改的要求標頭，則可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="e241d-289">解決方法是設定 proxy 以允許連接埠 80 上的使用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="e241d-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="e241d-290">「 例外狀況：&lt;方法名稱&gt;方法無法解決 「 當用戶端呼叫伺服器上的方法</span><span class="sxs-lookup"><span data-stu-id="e241d-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="e241d-291">此錯誤可能起因於使用找不到 JSON 承載，例如陣列中的資料類型。</span><span class="sxs-lookup"><span data-stu-id="e241d-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="e241d-292">因應措施是使用 JSON，例如 IList 可探索的資料類型。</span><span class="sxs-lookup"><span data-stu-id="e241d-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="e241d-293">如需詳細資訊，請參閱 <<c0> [ 無法呼叫具有陣列參數的中樞方法的.NET 用戶端](https://github.com/SignalR/SignalR/issues/2672)。</span><span class="sxs-lookup"><span data-stu-id="e241d-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="e241d-294">編譯和伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="e241d-295">下節包含可能的解決方案，編譯器和伺服器端執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span>

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="e241d-296">中樞執行個體的參考為 null</span><span class="sxs-lookup"><span data-stu-id="e241d-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="e241d-297">針對每個連接所建立的中樞執行個體，因為您無法中樞執行的個體在程式碼中自行建立。</span><span class="sxs-lookup"><span data-stu-id="e241d-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="e241d-298">若要呼叫方法，從中樞本身之外，請參閱[如何呼叫方法的用戶端和管理中樞類別外的群組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)為濆爧髍孮中樞內容的參考。</span><span class="sxs-lookup"><span data-stu-id="e241d-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="e241d-299">HTTPContext.Current.Session 為 null</span><span class="sxs-lookup"><span data-stu-id="e241d-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="e241d-300">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-300">This behavior is by design.</span></span> <span data-ttu-id="e241d-301">SignalR 不支援 ASP.NET 工作階段狀態，因為啟用的工作階段狀態，就會破壞雙工通訊。</span><span class="sxs-lookup"><span data-stu-id="e241d-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="e241d-302">若要覆寫任何合適的方法</span><span class="sxs-lookup"><span data-stu-id="e241d-302">No suitable method to override</span></span>

<span data-ttu-id="e241d-303">如果您使用程式碼，從較舊的文件或部落格，您會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="e241d-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="e241d-304">請確認您所未參考的已變更或已被取代的方法名稱 (例如`OnConnectedAsync`)。</span><span class="sxs-lookup"><span data-stu-id="e241d-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="e241d-305">HostContextExtensions.WebSocketServerUrl 為 null</span><span class="sxs-lookup"><span data-stu-id="e241d-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="e241d-306">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-306">This behavior is by design.</span></span> <span data-ttu-id="e241d-307">這個成員已被取代，而且不應該使用。</span><span class="sxs-lookup"><span data-stu-id="e241d-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="e241d-308">「 已將名為 'signalr.hubs' 已在路由集合中 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="e241d-309">將會看到此錯誤，如果`MapSignalR`兩次呼叫您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e241d-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="e241d-310">某些範例應用程式會呼叫`MapSignalR`直接在啟動類別中其他人進行的呼叫包裝函式類別中。</span><span class="sxs-lookup"><span data-stu-id="e241d-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="e241d-311">請確定您的應用程式不會兩者。</span><span class="sxs-lookup"><span data-stu-id="e241d-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="e241d-312">不會使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="e241d-312">WebSocket is not used</span></span>

<span data-ttu-id="e241d-313">如果您已確認您的伺服器和用戶端符合 WebSocket 的需求 (列入[支援的平台](../getting-started/supported-platforms.md)文件)，您必須在您的伺服器上啟用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="e241d-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="e241d-314">執行此動作的指示，請參閱[此處](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。</span><span class="sxs-lookup"><span data-stu-id="e241d-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="e241d-315">$.connection 是未定義</span><span class="sxs-lookup"><span data-stu-id="e241d-315">$.connection is undefined</span></span>

<span data-ttu-id="e241d-316">此錯誤表示，在頁面上的指令碼不正確，載入或無法連線到中樞 proxy，或不正確地存取。</span><span class="sxs-lookup"><span data-stu-id="e241d-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="e241d-317">確認頁面上的指令碼參考對應到在您專案中，載入的指令碼，且在瀏覽器可存取，/signalr/hubs，當伺服器執行。</span><span class="sxs-lookup"><span data-stu-id="e241d-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="e241d-318">找不到編譯動態運算式所需的一或多個型別</span><span class="sxs-lookup"><span data-stu-id="e241d-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="e241d-319">這個錯誤表示`Microsoft.CSharp`遺漏的文件庫。</span><span class="sxs-lookup"><span data-stu-id="e241d-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="e241d-320">將它加入**組件-&gt;Framework**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e241d-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="e241d-321">無法從 Clients.Caller 強型別的中樞; 或 Visual Basic 中存取呼叫端狀態"從類型 'Task (Of Object)' 為類型 'String' 的轉換無效 」 錯誤</span><span class="sxs-lookup"><span data-stu-id="e241d-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="e241d-322">若要存取強型別中樞或 Visual Basic 中的呼叫端狀態，請使用`Clients.CallerState`屬性 （於 SignalR 2.1 引進），而不是`Clients.Caller`。</span><span class="sxs-lookup"><span data-stu-id="e241d-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="e241d-323">Visual Studio 問題</span><span class="sxs-lookup"><span data-stu-id="e241d-323">Visual Studio issues</span></span>

<span data-ttu-id="e241d-324">本節說明在 Visual Studio 中遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="e241d-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="e241d-325">指令碼文件] 節點不會出現在 [方案總管</span><span class="sxs-lookup"><span data-stu-id="e241d-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="e241d-326">某些我們的教學課程將您導向至 [指令碼文件] 節點，在 [方案總管] 中偵錯時。</span><span class="sxs-lookup"><span data-stu-id="e241d-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="e241d-327">這個節點由 JavaScript 偵錯工具所產生，並只會出現在偵錯在 Internet Explorer; 中的瀏覽器用戶端時如果使用 Chrome 或 Firefox，不會出現的節點。</span><span class="sxs-lookup"><span data-stu-id="e241d-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="e241d-328">如果正在執行的另一個用戶端偵錯工具，例如 Silverlight 偵錯工具，也將無法執行 JavaScript 偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="e241d-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="e241d-329">SignalR 不適 Visual Studio 2008 或更早版本</span><span class="sxs-lookup"><span data-stu-id="e241d-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="e241d-330">這種行為是設計上的預期行為。</span><span class="sxs-lookup"><span data-stu-id="e241d-330">This behavior is by design.</span></span> <span data-ttu-id="e241d-331">SignalR 需要.NET Framework 4 或更新版本;這需要在 Visual Studio 2010 或更新版本開發 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e241d-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="e241d-332">SignalR 的伺服器元件需要.NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="e241d-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="e241d-333">IIS 問題</span><span class="sxs-lookup"><span data-stu-id="e241d-333">IIS issues</span></span>

<span data-ttu-id="e241d-334">本章節包含使用 Internet Information Services 的問題。</span><span class="sxs-lookup"><span data-stu-id="e241d-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="e241d-335">在 Visual Studio 程式開發伺服器，但未在 IIS 中的 SignalR 運作方式</span><span class="sxs-lookup"><span data-stu-id="e241d-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="e241d-336">SignalR 支援 IIS 7.0 和 7.5，但必須新增無副檔名 Url 的支援。</span><span class="sxs-lookup"><span data-stu-id="e241d-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="e241d-337">若要加入支援無副檔名的 Url，請參閱 [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="e241d-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="e241d-338">SignalR 要求 （未安裝 ASP.NET 在 IIS 預設情況下） 的伺服器上安裝 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="e241d-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="e241d-339">若要安裝 ASP.NET，請參閱[ASP.NET 下載](https://www.asp.net/downloads)。</span><span class="sxs-lookup"><span data-stu-id="e241d-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="e241d-340">Microsoft Azure 問題</span><span class="sxs-lookup"><span data-stu-id="e241d-340">Microsoft Azure issues</span></span>

<span data-ttu-id="e241d-341">本章節包含使用 Microsoft Azure 的問題。</span><span class="sxs-lookup"><span data-stu-id="e241d-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="e241d-342">FileLoadException 時裝載 Azure 背景工作角色中的 SignalR</span><span class="sxs-lookup"><span data-stu-id="e241d-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="e241d-343">裝載 Azure 背景工作角色中的 SignalR 可能會導致例外狀況 「 無法載入檔案或組件 ' Microsoft.Owin，版本 = 2.0.0.0"。</span><span class="sxs-lookup"><span data-stu-id="e241d-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="e241d-344">這是 NuGet; 的已知的問題在 Azure 背景工作角色專案中，則不會自動新增繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="e241d-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="e241d-345">若要修正此問題，您可以手動新增繫結重新導向。</span><span class="sxs-lookup"><span data-stu-id="e241d-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="e241d-346">新增下列行以`app.config`背景工作角色專案的檔案。</span><span class="sxs-lookup"><span data-stu-id="e241d-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="e241d-347">未接收訊息透過 Azure 後擋板之後變更的主題名稱</span><span class="sxs-lookup"><span data-stu-id="e241d-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="e241d-348">使用 Azure 的後擋板的主題會在內部，維護它們不被要作為使用者可設定。</span><span class="sxs-lookup"><span data-stu-id="e241d-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
