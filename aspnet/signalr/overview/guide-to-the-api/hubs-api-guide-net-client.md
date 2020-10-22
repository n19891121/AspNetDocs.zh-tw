---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: 'ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (c # ) |Microsoft Docs'
author: bradygaster
description: 本檔提供在 .NET 用戶端中使用適用于 SignalR 第2版的中樞 API 的簡介，例如 Windows Store (WinRT) 、WPF、Silverlight 和缺點 .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345542"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="6fa76-103">ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (c # ) </span><span class="sxs-lookup"><span data-stu-id="6fa76-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="6fa76-104">本檔提供在 .NET 用戶端中使用適用于 SignalR 第2版的中樞 API 的簡介，例如 Windows Store (WinRT) 、WPF、Silverlight 和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6fa76-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="6fa76-105">SignalR 中樞 API 可讓您進行遠端程序呼叫， (從伺服器到連線用戶端，以及從用戶端到伺服器的 Rpc) 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="6fa76-106">在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="6fa76-107">在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="6fa76-108">SignalR 會為您處理所有用戶端對伺服器的配管。</span><span class="sxs-lookup"><span data-stu-id="6fa76-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="6fa76-109">SignalR 也提供較低層級的 API，稱為「持續連線」。</span><span class="sxs-lookup"><span data-stu-id="6fa76-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="6fa76-110">如需 SignalR、中樞和持續連線的簡介，或說明如何建立完整 SignalR 應用程式的教學課程，請參閱 [SignalR-消費者入門](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="6fa76-111">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="6fa76-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="6fa76-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6fa76-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="6fa76-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6fa76-113">.NET 4.5</span></span>
> - <span data-ttu-id="6fa76-114">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="6fa76-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="6fa76-115">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="6fa76-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="6fa76-116">如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="6fa76-117">問題與意見</span><span class="sxs-lookup"><span data-stu-id="6fa76-117">Questions and comments</span></span>
>
> <span data-ttu-id="6fa76-118">請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="6fa76-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6fa76-119">如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="6fa76-120">概觀</span><span class="sxs-lookup"><span data-stu-id="6fa76-120">Overview</span></span>

<span data-ttu-id="6fa76-121">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="6fa76-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="6fa76-122">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="6fa76-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="6fa76-123">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="6fa76-124">Silverlight 用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="6fa76-125">如何設定連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="6fa76-126">如何在 WPF 用戶端中設定並行連接的最大數目</span><span class="sxs-lookup"><span data-stu-id="6fa76-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="6fa76-127">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="6fa76-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="6fa76-128">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="6fa76-129">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="6fa76-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="6fa76-130">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="6fa76-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="6fa76-131">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="6fa76-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="6fa76-132">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="6fa76-133">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="6fa76-134">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="6fa76-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="6fa76-135">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="6fa76-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="6fa76-136">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="6fa76-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="6fa76-137">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="6fa76-138">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="6fa76-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="6fa76-139">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="6fa76-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="6fa76-140">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="6fa76-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="6fa76-141">伺服器可呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6fa76-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="6fa76-142">如需範例 .NET 用戶端專案，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="6fa76-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="6fa76-143">[>gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com (WinRT、Silverlight、主控台應用程式範例) 的範例。</span><span class="sxs-lookup"><span data-stu-id="6fa76-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="6fa76-144">GitHub.com 上的[DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) (WPF 範例) 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="6fa76-145">[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) GitHub.com (主控台應用程式範例) 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="6fa76-146">如需有關如何對伺服器或 JavaScript 用戶端進行程式設計的檔，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="6fa76-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="6fa76-147">SignalR 中樞 API 指南-伺服器</span><span class="sxs-lookup"><span data-stu-id="6fa76-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="6fa76-148">SignalR 中樞 API 指南-JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="6fa76-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="6fa76-149">API 參考主題的連結是 .NET 4.5 版的 API。</span><span class="sxs-lookup"><span data-stu-id="6fa76-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="6fa76-150">如果您使用的是 .NET 4，請參閱 [.net 4 版的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="6fa76-151">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="6fa76-151">Client setup</span></span>

<span data-ttu-id="6fa76-152">將 SignalR 安裝 (不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)封裝) 的[用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6fa76-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="6fa76-153">針對 .NET 4 和 .NET 4.5，此套件支援 WinRT、Silverlight、WPF、主控台應用程式和 Windows Phone 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6fa76-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="6fa76-154">如果您在用戶端上的 SignalR 版本與伺服器上的版本不同，則 SignalR 通常可以調整成差異。</span><span class="sxs-lookup"><span data-stu-id="6fa76-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="6fa76-155">例如，執行 SignalR 第2版的伺服器將支援已安裝 1.1. x 的用戶端，以及安裝了版本2的用戶端。</span><span class="sxs-lookup"><span data-stu-id="6fa76-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="6fa76-156">如果伺服器上的版本與用戶端上的版本之間的差異太大，或用戶端比伺服器更新時，SignalR 會在 `InvalidOperationException` 用戶端嘗試建立連接時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6fa76-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="6fa76-157">錯誤訊息為 " `You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X` "。</span><span class="sxs-lookup"><span data-stu-id="6fa76-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="6fa76-158">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-158">How to establish a connection</span></span>

<span data-ttu-id="6fa76-159">您必須先建立物件並建立 proxy，才能建立連線 `HubConnection` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="6fa76-160">若要建立連接，請 `Start` 在物件上呼叫 `HubConnection` 方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> <span data-ttu-id="6fa76-161">針對 JavaScript 用戶端，您必須先註冊至少一個事件處理常式，才能呼叫 `Start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="6fa76-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="6fa76-162">.NET 用戶端不需要這項功能。</span><span class="sxs-lookup"><span data-stu-id="6fa76-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="6fa76-163">針對 JavaScript 用戶端，產生的 proxy 程式碼會自動為存在於伺服器上的所有中樞建立 proxy，並註冊處理常式，就是您指出用戶端想要使用的中樞。</span><span class="sxs-lookup"><span data-stu-id="6fa76-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="6fa76-164">但是針對 .NET 用戶端，您會以手動方式建立中樞 proxy，所以 SignalR 會假設您將使用任何建立 proxy 的中樞。</span><span class="sxs-lookup"><span data-stu-id="6fa76-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="6fa76-165">範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="6fa76-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="6fa76-166">如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="6fa76-167">`Start`方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="6fa76-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="6fa76-168">為了確保後續的程式程式碼在建立連接之後不會執行，請 `await` 在 ASP.NET 4.5 非同步方法或 `.Wait()` 同步方法中使用。</span><span class="sxs-lookup"><span data-stu-id="6fa76-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="6fa76-169">請勿 `.Wait()` 在 WinRT 用戶端中使用。</span><span class="sxs-lookup"><span data-stu-id="6fa76-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="6fa76-170">Silverlight 用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="6fa76-171">如需有關如何啟用 Silverlight 用戶端的跨網域連線的詳細資訊，請參閱 [讓服務可跨網域界限使用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="6fa76-172">如何設定連接</span><span class="sxs-lookup"><span data-stu-id="6fa76-172">How to configure the connection</span></span>

<span data-ttu-id="6fa76-173">建立連接之前，您可以指定下列任何選項：</span><span class="sxs-lookup"><span data-stu-id="6fa76-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="6fa76-174">並行連接限制。</span><span class="sxs-lookup"><span data-stu-id="6fa76-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="6fa76-175">查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="6fa76-175">Query string parameters.</span></span>
- <span data-ttu-id="6fa76-176">傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-176">The transport method.</span></span>
- <span data-ttu-id="6fa76-177">HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="6fa76-177">HTTP headers.</span></span>
- <span data-ttu-id="6fa76-178">用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="6fa76-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="6fa76-179">如何在 WPF 用戶端中設定並行連接的最大數目</span><span class="sxs-lookup"><span data-stu-id="6fa76-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="6fa76-180">在 WPF 用戶端中，您可能必須從預設值2增加並行連接的最大數目。</span><span class="sxs-lookup"><span data-stu-id="6fa76-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="6fa76-181">建議值為10。</span><span class="sxs-lookup"><span data-stu-id="6fa76-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

<span data-ttu-id="6fa76-182">如需詳細資訊，請參閱 [ServicePointManager. >servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="6fa76-183">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="6fa76-183">How to specify query string parameters</span></span>

<span data-ttu-id="6fa76-184">如果您想要在用戶端連接時將資料傳送至伺服器，您可以將查詢字串參數加入至連線物件。</span><span class="sxs-lookup"><span data-stu-id="6fa76-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="6fa76-185">下列範例顯示如何在用戶端程式代碼中設定查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="6fa76-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="6fa76-186">下列範例示範如何在伺服器程式碼中讀取查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="6fa76-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="6fa76-187">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-187">How to specify the transport method</span></span>

<span data-ttu-id="6fa76-188">在連接的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端所支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fa76-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="6fa76-189">如果您已經知道要使用哪一個傳輸，則可以略過此協商流程。</span><span class="sxs-lookup"><span data-stu-id="6fa76-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="6fa76-190">若要指定傳輸方法，請將傳輸物件傳遞給 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="6fa76-191">下列範例顯示如何在用戶端程式代碼中指定傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

<span data-ttu-id="6fa76-192">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包含下列類別，您可以使用這些類別來指定傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fa76-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="6fa76-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="6fa76-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="6fa76-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="6fa76-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="6fa76-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (只有在伺服器和用戶端都使用 .net 4.5 時才可使用。 ) </span><span class="sxs-lookup"><span data-stu-id="6fa76-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="6fa76-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (會自動選擇用戶端和伺服器所支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fa76-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="6fa76-197">這是預設傳輸。</span><span class="sxs-lookup"><span data-stu-id="6fa76-197">This is the default transport.</span></span> <span data-ttu-id="6fa76-198">將此傳遞給 `Start` 方法與未傳遞任何的效果相同。 ) </span><span class="sxs-lookup"><span data-stu-id="6fa76-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="6fa76-199">ForeverFrame 傳輸不包含在此清單中，因為它只能由瀏覽器使用。</span><span class="sxs-lookup"><span data-stu-id="6fa76-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="6fa76-200">如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="6fa76-201">如需傳輸和回退的詳細資訊，請參閱 [SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="6fa76-202">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="6fa76-202">How to specify HTTP headers</span></span>

<span data-ttu-id="6fa76-203">若要設定 HTTP 標頭，請使用 `Headers` 連線物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="6fa76-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="6fa76-204">下列範例顯示如何新增 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="6fa76-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="6fa76-205">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="6fa76-205">How to specify client certificates</span></span>

<span data-ttu-id="6fa76-206">若要加入用戶端憑證，請 `AddClientCertificate` 在連線物件上使用方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="6fa76-207">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="6fa76-207">How to create the Hub proxy</span></span>

<span data-ttu-id="6fa76-208">若要在用戶端上定義中樞可以從伺服器呼叫的方法，並在伺服器的中樞上叫用方法，請在連線物件上呼叫，以建立中樞的 proxy `CreateHubProxy` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="6fa76-209">您傳入的字串 `CreateHubProxy` 是中樞類別的名稱，或 `HubName` 屬性（如果在伺服器上使用的話）所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa76-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="6fa76-210">名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6fa76-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="6fa76-211">**伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="6fa76-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="6fa76-212">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="6fa76-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

<span data-ttu-id="6fa76-213">如果您使用屬性裝飾您的中樞類別 `HubName` ，請使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa76-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="6fa76-214">**伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="6fa76-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="6fa76-215">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="6fa76-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

<span data-ttu-id="6fa76-216">如果您 `HubConnection.CreateHubProxy` 以相同的方式呼叫多次 `hubName` ，則會取得相同的快取 `IHubProxy` 物件。</span><span class="sxs-lookup"><span data-stu-id="6fa76-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="6fa76-217">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="6fa76-218">若要定義伺服器可以呼叫的方法，請使用 proxy 的 `On` 方法來註冊事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="6fa76-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="6fa76-219">方法名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="6fa76-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="6fa76-220">例如， `Clients.All.UpdateStockPrice` 在伺服器上，伺服器將會在 `updateStockPrice` 用戶端上執行、 `updatestockprice` 或 `UpdateStockPrice` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="6fa76-221">不同的用戶端平臺會有不同的需求，讓您撰寫方法程式碼來更新 UI。</span><span class="sxs-lookup"><span data-stu-id="6fa76-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="6fa76-222">所顯示的範例適用于 WinRT (Windows Store .NET) 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6fa76-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="6fa76-223">WPF、Silverlight 和主控台應用程式範例會在 [本主題稍後的不同章節](#wpfsl)中提供。</span><span class="sxs-lookup"><span data-stu-id="6fa76-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="6fa76-224">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-224">Methods without parameters</span></span>

<span data-ttu-id="6fa76-225">如果您要處理的方法沒有參數，請使用方法的非泛型多載 `On` ：</span><span class="sxs-lookup"><span data-stu-id="6fa76-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="6fa76-226">**呼叫不含參數之用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="6fa76-227">\*\*從沒有參數的伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="6fa76-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="6fa76-228">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="6fa76-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="6fa76-229">如果您要處理的方法有參數，請將參數類型指定為方法的泛型型別 `On` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="6fa76-230">方法的泛型 `On` 多載可讓您指定最多8個參數， (4 的 Windows Phone 7) 上。</span><span class="sxs-lookup"><span data-stu-id="6fa76-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="6fa76-231">在下列範例中，會將一個參數傳送給 `UpdateStockPrice` 方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="6fa76-232">**使用參數呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="6fa76-233">**用於參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="6fa76-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="6fa76-234">\*\*使用參數從伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="6fa76-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="6fa76-235">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="6fa76-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="6fa76-236">除了將參數指定為方法的泛型型別之外 `On` ，您還可以指定參數做為動態物件：</span><span class="sxs-lookup"><span data-stu-id="6fa76-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="6fa76-237">**使用參數呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="6fa76-238">**用於參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="6fa76-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="6fa76-239">\*\*使用參數從伺服器呼叫的方法的 WinRT 用戶端程式代碼 ([參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)) \*\*</span><span class="sxs-lookup"><span data-stu-id="6fa76-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="6fa76-240">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="6fa76-240">How to remove a handler</span></span>

<span data-ttu-id="6fa76-241">若要移除處理常式，請呼叫其 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="6fa76-242">**從伺服器呼叫之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="6fa76-243">**移除處理常式的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="6fa76-244">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-244">How to call server methods from the client</span></span>

<span data-ttu-id="6fa76-245">若要在伺服器上呼叫方法，請 `Invoke` 在中樞 proxy 上使用方法。</span><span class="sxs-lookup"><span data-stu-id="6fa76-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="6fa76-246">如果伺服器方法沒有傳回值，請使用方法的非泛型多載 `Invoke` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="6fa76-247">**沒有傳回值之方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="6fa76-248">**呼叫沒有傳回值之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="6fa76-249">如果伺服器方法有傳回值，請將傳回型別指定為方法的泛型型別 `Invoke` 。</span><span class="sxs-lookup"><span data-stu-id="6fa76-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="6fa76-250">**具有傳回值且採用複雜型別參數之方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="6fa76-251">**用於參數和傳回值的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="6fa76-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="6fa76-252">**在 ASP.NET 4.5 非同步方法中呼叫具有傳回值並採用複雜型別參數之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="6fa76-253">**用戶端程式代碼，呼叫具有傳回值的方法，並在同步方法中採用複雜型別參數**</span><span class="sxs-lookup"><span data-stu-id="6fa76-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="6fa76-254">`Invoke`方法會以非同步方式執行，並傳回 `Task` 物件。</span><span class="sxs-lookup"><span data-stu-id="6fa76-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="6fa76-255">如果您未指定 `await` 或 `.Wait()` ，則會在您叫用的方法執行完成之前，先執行下一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="6fa76-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="6fa76-256">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="6fa76-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="6fa76-257">SignalR 提供下列可供您處理的連接存留期事件：</span><span class="sxs-lookup"><span data-stu-id="6fa76-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="6fa76-258">`Received`：在連接上收到任何資料時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="6fa76-259">提供接收的資料。</span><span class="sxs-lookup"><span data-stu-id="6fa76-259">Provides the received data.</span></span>
- <span data-ttu-id="6fa76-260">`ConnectionSlow`：當用戶端偵測到緩慢或經常中斷連接時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="6fa76-261">`Reconnecting`：當基礎傳輸開始重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="6fa76-262">`Reconnected`：當基礎傳輸重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="6fa76-263">`StateChanged`：當連接狀態變更時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="6fa76-264">提供舊狀態和新的狀態。</span><span class="sxs-lookup"><span data-stu-id="6fa76-264">Provides the old state and the new state.</span></span> <span data-ttu-id="6fa76-265">如需連接狀態值的詳細資訊，請參閱 [ConnectionState 列舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="6fa76-266">`Closed`：連接中斷連接時引發。</span><span class="sxs-lookup"><span data-stu-id="6fa76-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="6fa76-267">例如，如果您想要針對不是嚴重的錯誤顯示警告訊息，但造成間歇性的連接問題（例如緩慢或經常中斷連接），請處理 `ConnectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="6fa76-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="6fa76-268">如需詳細資訊，請參閱 [瞭解及處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa76-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="6fa76-269">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="6fa76-269">How to handle errors</span></span>

<span data-ttu-id="6fa76-270">如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 在錯誤之後傳回的例外狀況物件會包含錯誤的最基本資訊。</span><span class="sxs-lookup"><span data-stu-id="6fa76-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="6fa76-271">例如，如果的呼叫 `newContosoChatMessage` 失敗，則錯誤物件中的錯誤訊息會包含「」 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 基於安全性理由，不建議在生產環境中傳送詳細的錯誤訊息給用戶端，但如果您想要啟用詳細的錯誤訊息以進行疑難排解，請在伺服器上使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="6fa76-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="6fa76-272">若要處理 SignalR 引發的錯誤，您可以 `Error` 在連線物件上加入事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="6fa76-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="6fa76-273">若要處理方法調用的錯誤，請將程式碼包裝在 try-catch 區塊中。</span><span class="sxs-lookup"><span data-stu-id="6fa76-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="6fa76-274">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="6fa76-274">How to enable client-side logging</span></span>

<span data-ttu-id="6fa76-275">若要啟用用戶端記錄，請 `TraceLevel` `TraceWriter` 在連線物件上設定和屬性。</span><span class="sxs-lookup"><span data-stu-id="6fa76-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="6fa76-276">伺服器可呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6fa76-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="6fa76-277">稍早所示的程式碼範例，可用於定義伺服器可呼叫的用戶端方法，適用于 WinRT 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6fa76-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="6fa76-278">下列範例顯示 WPF、Silverlight 和主控台應用程式用戶端的對等程式碼。</span><span class="sxs-lookup"><span data-stu-id="6fa76-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="6fa76-279">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="6fa76-279">Methods without parameters</span></span>

<span data-ttu-id="6fa76-280">**從沒有參數的伺服器呼叫之方法的 WPF 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="6fa76-281">**從沒有參數的伺服器呼叫之方法的 Silverlight 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="6fa76-282">**從伺服器呼叫的方法的主控台應用程式用戶端程式代碼（不含參數）**</span><span class="sxs-lookup"><span data-stu-id="6fa76-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="6fa76-283">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="6fa76-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="6fa76-284">**使用參數從伺服器呼叫之方法的 WPF 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="6fa76-285">**使用參數從伺服器呼叫之方法的 Silverlight 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="6fa76-286">**使用參數從伺服器呼叫的方法的主控台應用程式用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="6fa76-287">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="6fa76-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="6fa76-288">**使用參數從伺服器呼叫的方法的 WPF 用戶端程式代碼，使用參數的動態物件**</span><span class="sxs-lookup"><span data-stu-id="6fa76-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="6fa76-289">**使用參數從伺服器呼叫的方法的 Silverlight 用戶端程式代碼，使用動態物件作為參數**</span><span class="sxs-lookup"><span data-stu-id="6fa76-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="6fa76-290">**使用參數將動態物件用於從伺服器呼叫的方法的主控台應用程式用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="6fa76-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
