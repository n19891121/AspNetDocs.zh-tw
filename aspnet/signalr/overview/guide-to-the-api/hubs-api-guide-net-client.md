---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET信號器集線器 API 指南 - .NET 用戶端 (C#) |微軟文件
author: bradygaster
description: 本文檔介紹了在 .NET 用戶端(如 Windows 應用商店 (WinRT)、WPF、Silverlight 和 cons...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676332"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="28417-103">ASP.NET訊號器集線器 API 指南 - .NET 用戶端 (C#)</span><span class="sxs-lookup"><span data-stu-id="28417-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="28417-104">本文件介紹了在 .NET 用戶端(如 Windows 應用商店 (WinRT)、WPF、Silverlight 和控制台應用程式)中為 SignalR 版本 2 使用集線器 API 的簡介。</span><span class="sxs-lookup"><span data-stu-id="28417-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="28417-105">SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。</span><span class="sxs-lookup"><span data-stu-id="28417-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="28417-106">在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="28417-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="28417-107">在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="28417-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="28417-108">SignalR 為您處理所有用戶端到伺服器管道。</span><span class="sxs-lookup"><span data-stu-id="28417-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="28417-109">SignalR 還提供稱為持久連接的較低級別的 API。</span><span class="sxs-lookup"><span data-stu-id="28417-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="28417-110">有關 SignalR、集線器和持久連線的介紹,或者有關如何建構完整的 SignalR 應用程式的教學,請參閱[SignalR - 入門](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="28417-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="28417-111">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="28417-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="28417-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="28417-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="28417-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="28417-113">.NET 4.5</span></span>
> - <span data-ttu-id="28417-114">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="28417-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="28417-115">本主題的早期版本</span><span class="sxs-lookup"><span data-stu-id="28417-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="28417-116">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="28417-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="28417-117">問題和評論</span><span class="sxs-lookup"><span data-stu-id="28417-117">Questions and comments</span></span>
>
> <span data-ttu-id="28417-118">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="28417-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="28417-119">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="28417-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="28417-120">概觀</span><span class="sxs-lookup"><span data-stu-id="28417-120">Overview</span></span>

<span data-ttu-id="28417-121">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="28417-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="28417-122">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="28417-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="28417-123">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="28417-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="28417-124">來自銀光用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="28417-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="28417-125">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="28417-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="28417-126">如何設定 WPF 用戶端中的最大併發連線數</span><span class="sxs-lookup"><span data-stu-id="28417-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="28417-127">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="28417-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="28417-128">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="28417-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="28417-129">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="28417-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="28417-130">如何指定客戶端憑證</span><span class="sxs-lookup"><span data-stu-id="28417-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="28417-131">如何建立中心代理</span><span class="sxs-lookup"><span data-stu-id="28417-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="28417-132">如何在客戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="28417-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="28417-133">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="28417-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="28417-134">具有參數的方法,指定參數類型</span><span class="sxs-lookup"><span data-stu-id="28417-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="28417-135">具有參數的方法,為參數指定動態物件</span><span class="sxs-lookup"><span data-stu-id="28417-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="28417-136">如何移除處理程式</span><span class="sxs-lookup"><span data-stu-id="28417-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="28417-137">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="28417-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="28417-138">如何處理連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="28417-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="28417-139">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="28417-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="28417-140">如何開啟客戶端記錄記錄</span><span class="sxs-lookup"><span data-stu-id="28417-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="28417-141">WPF、Silverlight 和主控台應用程式代碼範例,用於伺服器可以呼叫的用戶端方法</span><span class="sxs-lookup"><span data-stu-id="28417-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="28417-142">有關範例 .NET 客戶端專案,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="28417-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="28417-143">[古斯塔沃-阿爾門塔 / 信號R-樣本](https://github.com/gustavo-armenta/SignalR-Samples)GitHub.com(WinRT,銀光,控制台應用程式示例)。</span><span class="sxs-lookup"><span data-stu-id="28417-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="28417-144">[達米安愛德華茲 / 信號R-移動形狀演示 / 移動形狀.桌面](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop)GitHub.com (WPF 示例)。</span><span class="sxs-lookup"><span data-stu-id="28417-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="28417-145">[信號R / 微軟.AspNet.SignalR.用戶端.GitHub.com上的樣本](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples)(控制台應用範例)。</span><span class="sxs-lookup"><span data-stu-id="28417-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="28417-146">有關如何對伺服器或 JAVAScript 客戶端進行程式設計的文件,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="28417-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="28417-147">訊號器集線器 API 指南 - 伺服器</span><span class="sxs-lookup"><span data-stu-id="28417-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="28417-148">信號器中心 API 指南 - JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="28417-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="28417-149">指向 API 參考主題的連結指向 API 的 .NET 4.5 版本。</span><span class="sxs-lookup"><span data-stu-id="28417-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="28417-150">如果使用 .NET 4,請參閱[API 主題的 .NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="28417-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="28417-151">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="28417-151">Client setup</span></span>

<span data-ttu-id="28417-152">安裝[微軟.AspNet.SignalR.用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 包(不是[微軟.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)包)。</span><span class="sxs-lookup"><span data-stu-id="28417-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="28417-153">此包支援 WinRT、Silverlight、WPF、控制台應用程式和 Windows Phone 用戶端,適用於 .NET 4 和 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="28417-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="28417-154">如果用戶端上的 SignalR 版本與伺服器上的版本不同,則 SignalR 通常能夠適應差異。</span><span class="sxs-lookup"><span data-stu-id="28417-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="28417-155">例如,運行 SignalR 版本 2 的伺服器將支援安裝了 1.1.x 的用戶端以及安裝了版本 2 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="28417-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="28417-156">如果伺服器上的版本和用戶端上的版本之間的差異太大,或者如果用戶端比伺服器新,則在用戶端嘗試建立連接時,SignalR 會`InvalidOperationException`引發異常。</span><span class="sxs-lookup"><span data-stu-id="28417-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="28417-157">錯誤消息為""`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`</span><span class="sxs-lookup"><span data-stu-id="28417-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="28417-158">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="28417-158">How to establish a connection</span></span>

<span data-ttu-id="28417-159">在建立連接之前,必須創建物件`HubConnection`並創建代理。</span><span class="sxs-lookup"><span data-stu-id="28417-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="28417-160">要建立連接,請`Start`調用`HubConnection`物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="28417-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="28417-161">對於 JavaScript 用戶端,在調用方法建立連接`Start`之前, 您必須至少註冊一個事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="28417-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="28417-162">對於 .NET 用戶端,這不需要。</span><span class="sxs-lookup"><span data-stu-id="28417-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="28417-163">對於 JavaScript 用戶端,生成的代理程式碼會自動為伺服器上存在的所有中心創建代理,註冊處理程式是指示用戶端打算使用哪個集線器的方式。</span><span class="sxs-lookup"><span data-stu-id="28417-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="28417-164">但對於 .NET 用戶端,您可以手動創建集線器代理,因此 SignalR 假定您將使用為其創建代理的任何集線器。</span><span class="sxs-lookup"><span data-stu-id="28417-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="28417-165">範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="28417-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="28417-166">有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="28417-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="28417-167">該方法`Start`以異步方式執行。</span><span class="sxs-lookup"><span data-stu-id="28417-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="28417-168">為了確保後續代碼行在建立連接之前不會執行,請使用`await`ASP.NET 4.5 非同步`.Wait()`方法或同步方法。</span><span class="sxs-lookup"><span data-stu-id="28417-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="28417-169">不要在 WinRT`.Wait()`用戶端中使用。</span><span class="sxs-lookup"><span data-stu-id="28417-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="28417-170">來自銀光用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="28417-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="28417-171">有關如何啟用來自 Silverlight 用戶端的跨域連接的資訊,請參閱[使服務跨域邊界可用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="28417-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="28417-172">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="28417-172">How to configure the connection</span></span>

<span data-ttu-id="28417-173">在建立連線之前,可以指定以下任一選項:</span><span class="sxs-lookup"><span data-stu-id="28417-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="28417-174">併發連接限制。</span><span class="sxs-lookup"><span data-stu-id="28417-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="28417-175">查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="28417-175">Query string parameters.</span></span>
- <span data-ttu-id="28417-176">傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="28417-176">The transport method.</span></span>
- <span data-ttu-id="28417-177">HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="28417-177">HTTP headers.</span></span>
- <span data-ttu-id="28417-178">用戶端證書。</span><span class="sxs-lookup"><span data-stu-id="28417-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="28417-179">如何設定 WPF 用戶端中的最大併發連線數</span><span class="sxs-lookup"><span data-stu-id="28417-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="28417-180">在 WPF 用戶端中,您可能需要從預設值 2 增加併發連接的最大數量。</span><span class="sxs-lookup"><span data-stu-id="28417-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="28417-181">建議的值為 10。</span><span class="sxs-lookup"><span data-stu-id="28417-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="28417-182">有關詳細資訊,請參閱[服務點管理員.預設連線限制](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="28417-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="28417-183">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="28417-183">How to specify query string parameters</span></span>

<span data-ttu-id="28417-184">如果要在用戶端連接時將數據發送到伺服器,則可以向連接物件添加查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="28417-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="28417-185">下面的範例展示如何在用戶端代碼中設置查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="28417-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="28417-186">下面的範例展示如何讀取伺服器代碼中的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="28417-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="28417-187">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="28417-187">How to specify the transport method</span></span>

<span data-ttu-id="28417-188">作為連接過程的一部分,SignalR 用戶端通常與伺服器協商以確定伺服器和用戶端支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="28417-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="28417-189">如果您已經知道要使用的傳輸,可以繞過此協商過程。</span><span class="sxs-lookup"><span data-stu-id="28417-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="28417-190">要指定傳輸方法,請將傳輸物件傳遞給 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="28417-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="28417-191">下面的範例展示如何在用戶端代碼中指定傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="28417-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="28417-192">[Microsoft.AspNet.SignalR.Client.傳輸](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包括以下類,可用於指定傳輸。</span><span class="sxs-lookup"><span data-stu-id="28417-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="28417-193">[長輪詢傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="28417-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="28417-194">[伺服器傳送事件傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="28417-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="28417-195">[WebSocket 傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx)(僅在伺服器和用戶端使用 .NET 4.5 時可用。</span><span class="sxs-lookup"><span data-stu-id="28417-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="28417-196">[自動傳輸](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx)(自動選擇客戶端和伺服器支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="28417-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="28417-197">這是默認傳輸。</span><span class="sxs-lookup"><span data-stu-id="28417-197">This is the default transport.</span></span> <span data-ttu-id="28417-198">將此傳遞給`Start`方法的效果與不傳入任何內容的效果相同。</span><span class="sxs-lookup"><span data-stu-id="28417-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="28417-199">ForeverFrame 傳輸不包括在此清單中,因為它僅由瀏覽器使用。</span><span class="sxs-lookup"><span data-stu-id="28417-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="28417-200">有關如何在伺服器代碼中檢查傳輸方法的資訊,請參閱[ASP.NET SignalR 集線器 API 指南 - 伺服器 - 如何從 Context 屬性取得有關用戶端的資訊](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="28417-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="28417-201">有關傳輸和回退的詳細資訊,請參閱[訊號R - 傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="28417-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="28417-202">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="28417-202">How to specify HTTP headers</span></span>

<span data-ttu-id="28417-203">要設置 HTTP 標`Headers`頭, 請使用連接物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="28417-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="28417-204">下面的範例展示如何添加 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="28417-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="28417-205">如何指定客戶端憑證</span><span class="sxs-lookup"><span data-stu-id="28417-205">How to specify client certificates</span></span>

<span data-ttu-id="28417-206">要添加用戶端證書,`AddClientCertificate`請使用連接物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="28417-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="28417-207">如何建立中心代理</span><span class="sxs-lookup"><span data-stu-id="28417-207">How to create the Hub proxy</span></span>

<span data-ttu-id="28417-208">為了在用戶端上定義集線器可以從伺服器調用的方法,並在伺服器上的集線器上調用方法,請通過調用`CreateHubProxy`連接物件為集線器創建代理。</span><span class="sxs-lookup"><span data-stu-id="28417-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="28417-209">傳遞給的字串`CreateHubProxy`是 Hub 類的名稱`HubName`,或者 屬性指定的名稱(如果在伺服器上使用)。</span><span class="sxs-lookup"><span data-stu-id="28417-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="28417-210">名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="28417-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="28417-211">**伺服器上的集線器類別**</span><span class="sxs-lookup"><span data-stu-id="28417-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="28417-212">**為中心類別建立用戶端代理**</span><span class="sxs-lookup"><span data-stu-id="28417-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="28417-213">如果使用`HubName`屬性修飾 Hub 類,請使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="28417-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="28417-214">**伺服器上的集線器類別**</span><span class="sxs-lookup"><span data-stu-id="28417-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="28417-215">**為中心類別建立用戶端代理**</span><span class="sxs-lookup"><span data-stu-id="28417-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="28417-216">如果使用相同的`HubConnection.CreateHubProxy``hubName`調用多次 ,則會獲取相同的`IHubProxy`緩存 物件。</span><span class="sxs-lookup"><span data-stu-id="28417-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="28417-217">如何在客戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="28417-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="28417-218">要定義伺服器可以調用的方法,請使用代理`On`的方法註冊事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="28417-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="28417-219">方法名稱匹配不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="28417-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="28417-220">例如,`Clients.All.UpdateStockPrice`在伺服器上將`updateStockPrice`執行`updatestockprice`、`UpdateStockPrice`或在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="28417-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="28417-221">不同的用戶端平臺對如何編寫方法來更新 UI 有不同的要求。</span><span class="sxs-lookup"><span data-stu-id="28417-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="28417-222">顯示的範例適用於 WinRT (Windows 應用商店 .NET) 用戶端。</span><span class="sxs-lookup"><span data-stu-id="28417-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="28417-223">WPF、Silverlight 和主控台應用程式範例在本[主題後面的單獨部分](#wpfsl)提供。</span><span class="sxs-lookup"><span data-stu-id="28417-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="28417-224">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="28417-224">Methods without parameters</span></span>

<span data-ttu-id="28417-225">如果正在處理的方法沒有參數,請使用`On`方法的非泛型重載:</span><span class="sxs-lookup"><span data-stu-id="28417-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="28417-226">**伺服器代碼呼叫沒有參數的用戶端方法**</span><span class="sxs-lookup"><span data-stu-id="28417-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="28417-227">**WinRT 客戶端碼用於從伺服器呼叫沒有參數的方法([請參閱本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="28417-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="28417-228">具有參數的方法,指定參數類型</span><span class="sxs-lookup"><span data-stu-id="28417-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="28417-229">如果要處理的方法具有參數,請指定參數的類型作為`On`方法的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="28417-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="28417-230">`On`該方法有泛型重載,使您能夠指定最多 8 個參數(Windows Phone 7 上的 4 個參數)。</span><span class="sxs-lookup"><span data-stu-id="28417-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="28417-231">在下面的示例中,一個參數發送到`UpdateStockPrice`方法。</span><span class="sxs-lookup"><span data-stu-id="28417-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="28417-232">**使用參數呼叫用戶端方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="28417-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="28417-233">**參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="28417-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="28417-234">**WinRT 客戶端碼用於從具有參數的伺服器呼叫的方法([請參閱本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="28417-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="28417-235">具有參數的方法,為參數指定動態物件</span><span class="sxs-lookup"><span data-stu-id="28417-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="28417-236">作為將參數指定為`On`方法的泛型型別的替代方法,可以將參數指定為動態物件:</span><span class="sxs-lookup"><span data-stu-id="28417-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="28417-237">**使用參數呼叫用戶端方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="28417-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="28417-238">**參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="28417-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="28417-239">**WinRT 客戶端碼用於使用參數從伺服器呼叫的方法,使用參數的動態物件([請參考本主題後面的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="28417-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="28417-240">如何移除處理程式</span><span class="sxs-lookup"><span data-stu-id="28417-240">How to remove a handler</span></span>

<span data-ttu-id="28417-241">要刪除處理程式,請調用其`Dispose`方法。</span><span class="sxs-lookup"><span data-stu-id="28417-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="28417-242">**從伺服器呼叫的方法的客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="28417-243">**用戶端代碼以移除處理程式**</span><span class="sxs-lookup"><span data-stu-id="28417-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="28417-244">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="28417-244">How to call server methods from the client</span></span>

<span data-ttu-id="28417-245">要在伺服器上調用方法,`Invoke`請使用集線器代理上的方法。</span><span class="sxs-lookup"><span data-stu-id="28417-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="28417-246">如果伺服器方法沒有返回值,請使用`Invoke`方法的非泛型重載。</span><span class="sxs-lookup"><span data-stu-id="28417-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="28417-247">**沒有傳回值的方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="28417-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="28417-248">**呼叫沒有返回值的方法的客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="28417-249">如果伺服器方法具有返回值,請指定返回類型作為`Invoke`方法的泛型類型。</span><span class="sxs-lookup"><span data-stu-id="28417-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="28417-250">**具有傳回值並採用複雜類型參數的方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="28417-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="28417-251">**參數與傳回值的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="28417-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="28417-252">**用戶端代碼呼叫具有傳回值並採用複雜類型參數的方法,在 ASP.NET 4.5 非同步方法中呼叫**</span><span class="sxs-lookup"><span data-stu-id="28417-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="28417-253">**用戶端代碼呼叫具有傳回值並採用複雜類型參數的方法(在同步方法中)**</span><span class="sxs-lookup"><span data-stu-id="28417-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="28417-254">該方法`Invoke`非同步執行並傳`Task`回物件 。</span><span class="sxs-lookup"><span data-stu-id="28417-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="28417-255">如果不指定`await``.Wait()`或 ,則下一行代碼將在調用的方法完成執行之前執行。</span><span class="sxs-lookup"><span data-stu-id="28417-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="28417-256">如何處理連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="28417-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="28417-257">SignalR 提供您可以處理的以下連線存留期事件:</span><span class="sxs-lookup"><span data-stu-id="28417-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="28417-258">`Received`:在連接上收到任何數據時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="28417-259">提供接收的數據。</span><span class="sxs-lookup"><span data-stu-id="28417-259">Provides the received data.</span></span>
- <span data-ttu-id="28417-260">`ConnectionSlow`:當客戶端檢測到連接緩慢或頻繁斷開時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="28417-261">`Reconnecting`:當基礎傳輸開始重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="28417-262">`Reconnected`:在基礎傳輸重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="28417-263">`StateChanged`:當連接狀態更改時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="28417-264">提供舊狀態和新狀態。</span><span class="sxs-lookup"><span data-stu-id="28417-264">Provides the old state and the new state.</span></span> <span data-ttu-id="28417-265">有關連接狀態值的資訊,請參閱[連接狀態枚舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="28417-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="28417-266">`Closed`:連接斷開連接時引發。</span><span class="sxs-lookup"><span data-stu-id="28417-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="28417-267">例如,如果要顯示未致命但會導致間歇性連接問題(如連接速度慢或頻繁斷開)的錯誤的警告消息,則處理該`ConnectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="28417-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="28417-268">有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="28417-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="28417-269">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="28417-269">How to handle errors</span></span>

<span data-ttu-id="28417-270">如果未在伺服器上顯式啟用詳細的錯誤消息,則 SignalR 在錯誤後返回的異常物件包含有關該錯誤的最少資訊。</span><span class="sxs-lookup"><span data-stu-id="28417-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="28417-271">例如,如果調用`newContosoChatMessage`失敗,錯誤物件中的錯誤消息包含`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`「 出於安全原因不建議向生產中的客戶端發送詳細的錯誤訊息,但如果要啟用詳細的錯誤訊息以進行故障排除,請使用伺服器上的以下代碼。</span><span class="sxs-lookup"><span data-stu-id="28417-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="28417-272">要處理 SignalR 引發的錯誤,可以在連接物件`Error`上為 事件添加處理程式。</span><span class="sxs-lookup"><span data-stu-id="28417-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="28417-273">要處理方法調用中的錯誤,請將代碼包裝在 try-catch 塊中。</span><span class="sxs-lookup"><span data-stu-id="28417-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="28417-274">如何開啟客戶端記錄記錄</span><span class="sxs-lookup"><span data-stu-id="28417-274">How to enable client-side logging</span></span>

<span data-ttu-id="28417-275">要啟用客戶端日誌記錄,在連接物件`TraceLevel`上`TraceWriter`設置和 屬性。</span><span class="sxs-lookup"><span data-stu-id="28417-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="28417-276">WPF、Silverlight 和主控台應用程式代碼範例,用於伺服器可以呼叫的用戶端方法</span><span class="sxs-lookup"><span data-stu-id="28417-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="28417-277">前面顯示的代碼示例用於定義伺服器可以調用的用戶端方法,應用於 WinRT 用戶端。</span><span class="sxs-lookup"><span data-stu-id="28417-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="28417-278">以下範例顯示了 WPF、Silverlight 和主控台應用程式用戶端的等效代碼。</span><span class="sxs-lookup"><span data-stu-id="28417-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="28417-279">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="28417-279">Methods without parameters</span></span>

<span data-ttu-id="28417-280">**WPF 客戶端碼,用於從伺服器呼叫無參數的方法**</span><span class="sxs-lookup"><span data-stu-id="28417-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="28417-281">**銀光客戶端代碼,用於從伺服器呼叫無參數的方法**</span><span class="sxs-lookup"><span data-stu-id="28417-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="28417-282">**主控台應用程式客戶端碼,用於從伺服器呼叫無參數的方法**</span><span class="sxs-lookup"><span data-stu-id="28417-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="28417-283">具有參數的方法,指定參數類型</span><span class="sxs-lookup"><span data-stu-id="28417-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="28417-284">**WPF 客戶端碼,用於從具有參數的伺服器呼叫的方法**</span><span class="sxs-lookup"><span data-stu-id="28417-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="28417-285">**使用參數從伺服器呼叫的方法的 Silverlight 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="28417-286">**主控台應用程式客戶端代碼,用於從具有參數的伺服器呼叫的方法**</span><span class="sxs-lookup"><span data-stu-id="28417-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="28417-287">具有參數的方法,為參數指定動態物件</span><span class="sxs-lookup"><span data-stu-id="28417-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="28417-288">**使用參數的動態物件從伺服器呼叫的方法的 WPF 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="28417-289">**使用參數的動態物件從伺服器呼叫的方法的 Silverlight 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="28417-290">**使用參數的動態物件從伺服器呼叫的方法的主控台應用程式客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="28417-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
