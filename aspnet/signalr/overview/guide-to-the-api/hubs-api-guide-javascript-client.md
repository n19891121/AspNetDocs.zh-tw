---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端 |Microsoft Docs
author: bradygaster
description: 本檔提供在 JavaScript 用戶端中使用適用于 SignalR 第2版的中樞 API 的簡介，例如瀏覽器和 Windows Store (WinJS) applicat .。。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345433"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="cb1fc-103">ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="cb1fc-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="cb1fc-104">本檔提供在 JavaScript 用戶端（例如瀏覽器和 Windows Store (WinJS) 應用程式）中使用適用于 SignalR 第2版的中樞 API 的簡介。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="cb1fc-105">SignalR 中樞 API 可讓您進行遠端程序呼叫， (從伺服器到連線用戶端，以及從用戶端到伺服器的 Rpc) 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="cb1fc-106">在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="cb1fc-107">在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="cb1fc-108">SignalR 會為您處理所有用戶端對伺服器的配管。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="cb1fc-109">SignalR 也提供較低層級的 API，稱為「持續連線」。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="cb1fc-110">如需 SignalR、中樞和持續連線的簡介，請參閱 [SignalR 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="cb1fc-111">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="cb1fc-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="cb1fc-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="cb1fc-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="cb1fc-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="cb1fc-113">.NET 4.5</span></span>
> - <span data-ttu-id="cb1fc-114">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="cb1fc-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="cb1fc-115">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="cb1fc-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="cb1fc-116">如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="cb1fc-117">問題與意見</span><span class="sxs-lookup"><span data-stu-id="cb1fc-117">Questions and comments</span></span>
>
> <span data-ttu-id="cb1fc-118">請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="cb1fc-119">如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="cb1fc-120">概觀</span><span class="sxs-lookup"><span data-stu-id="cb1fc-120">Overview</span></span>

<span data-ttu-id="cb1fc-121">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="cb1fc-122">產生的 proxy 以及它為您執行的工作</span><span class="sxs-lookup"><span data-stu-id="cb1fc-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="cb1fc-123">使用產生的 proxy 的時機</span><span class="sxs-lookup"><span data-stu-id="cb1fc-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="cb1fc-124">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="cb1fc-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="cb1fc-125">如何參考動態產生的 proxy</span><span class="sxs-lookup"><span data-stu-id="cb1fc-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="cb1fc-126">如何建立 SignalR 產生之 proxy 的實體檔案</span><span class="sxs-lookup"><span data-stu-id="cb1fc-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="cb1fc-127">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="cb1fc-128">hubConnection ( # A1 所建立的相同物件</span><span class="sxs-lookup"><span data-stu-id="cb1fc-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="cb1fc-129">啟動方法的非同步執行</span><span class="sxs-lookup"><span data-stu-id="cb1fc-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="cb1fc-130">如何建立跨網域連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="cb1fc-131">如何設定連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="cb1fc-132">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="cb1fc-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="cb1fc-133">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="cb1fc-134">如何取得中樞類別的 proxy</span><span class="sxs-lookup"><span data-stu-id="cb1fc-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="cb1fc-135">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="cb1fc-136">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="cb1fc-137">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="cb1fc-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="cb1fc-138">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="cb1fc-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="cb1fc-139">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="cb1fc-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="cb1fc-140">如需有關如何對伺服器或 .NET 用戶端進行程式設計的檔，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="cb1fc-141">SignalR 中樞 API 指南-伺服器</span><span class="sxs-lookup"><span data-stu-id="cb1fc-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="cb1fc-142">SignalR 中樞 API 指南-.NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="cb1fc-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="cb1fc-143">SignalR 2 server 元件僅適用于 .NET 4.5 (但 .net 4.0) 上有適用于 SignalR 2 的 .NET 用戶端。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="cb1fc-144">產生的 proxy 以及它為您執行的工作</span><span class="sxs-lookup"><span data-stu-id="cb1fc-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="cb1fc-145">您可以使用或不使用 SignalR 為您產生的 proxy，程式設計 JavaScript 用戶端與 SignalR 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="cb1fc-146">Proxy 為您提供的功能是簡化您用來連接的程式碼語法、撰寫伺服器呼叫的方法，以及呼叫伺服器上的方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="cb1fc-147">當您撰寫程式碼來呼叫伺服器方法時，產生的 proxy 可讓您使用看起來像是執列區域函數的語法：您可以撰寫 `serverMethod(arg1, arg2)` 而不是 `invoke('serverMethod', arg1, arg2)` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="cb1fc-148">如果您錯誤地出現伺服器方法名稱，產生的 proxy 語法也會啟用立即和智慧型的用戶端錯誤。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="cb1fc-149">如果您手動建立定義 proxy 的檔案，也可以取得 IntelliSense 支援，以撰寫呼叫伺服器方法的程式碼。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="cb1fc-150">例如，假設您在伺服器上有下列 Hub 類別：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="cb1fc-151">下列程式碼範例顯示在 `NewContosoChatMessage` 伺服器上叫用方法，以及從伺服器接收方法調用時，JavaScript 程式碼的樣子 `addContosoChatMessageToPage` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="cb1fc-152">**使用產生的 proxy**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="cb1fc-153">**沒有產生的 proxy**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="cb1fc-154">使用產生的 proxy 的時機</span><span class="sxs-lookup"><span data-stu-id="cb1fc-154">When to use the generated proxy</span></span>

<span data-ttu-id="cb1fc-155">如果您想要為伺服器所呼叫的用戶端方法註冊多個事件處理常式，則無法使用產生的 proxy。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="cb1fc-156">否則，您可以選擇使用產生的 proxy，或不要根據您的程式碼撰寫喜好設定。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="cb1fc-157">如果您選擇不使用它，就不需要在 `script` 用戶端程式代碼的元素中參考 "signalr/hub" URL。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="cb1fc-158">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="cb1fc-158">Client setup</span></span>

<span data-ttu-id="cb1fc-159">JavaScript 用戶端需要 jQuery 和 SignalR core JavaScript 檔案的參考。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="cb1fc-160">JQuery 版本必須是1.6.4 版或主要版本，例如1.7.2 版、1.8.2 或1.9.1。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="cb1fc-161">如果您決定使用產生的 proxy，也需要 SignalR 產生之 proxy JavaScript 檔案的參考。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="cb1fc-162">下列範例顯示在使用產生的 proxy 的 HTML 網頁中，參考可能會顯示的樣子。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="cb1fc-163">這些參考必須包含在此順序中： jQuery first、SignalR core 之後，以及 SignalR proxy last。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="cb1fc-164">如何參考動態產生的 proxy</span><span class="sxs-lookup"><span data-stu-id="cb1fc-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="cb1fc-165">在上述範例中，SignalR 產生之 proxy 的參考是動態產生的 JavaScript 程式碼，而不是實體檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="cb1fc-166">SignalR 會即時建立 proxy 的 JavaScript 程式碼，並將它提供給用戶端，以回應 "/signalr/hubs" URL。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="cb1fc-167">如果您在方法中為伺服器上的 SignalR 連接指定不同的基底 URL `MapSignalR` ，動態產生的 proxy 檔案的 URL 就是附加 "/hubs" 的自訂 url。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="cb1fc-168">針對 Windows 8 (Windows Store) JavaScript 用戶端，請使用實體 proxy 檔案，而不是動態產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="cb1fc-169">如需詳細資訊，請參閱本主題稍後的 [如何為 SignalR 產生的 proxy 建立實體](#manualproxy) 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="cb1fc-170">在 ASP.NET MVC 4 或 5 Razor view 中，使用波狀符號來參考 proxy 檔案參考中的應用程式根目錄：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="cb1fc-171">如需在 MVC 5 中使用 SignalR 的詳細資訊，請參閱 [使用 SignalR 和 MVC 5 的消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="cb1fc-172">在 ASP.NET MVC 3 Razor view 中，使用 `Url.Content` 作為 proxy 檔案參考：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="cb1fc-173">在 ASP.NET Web Forms 應用程式中， `ResolveClientUrl` 針對您的 proxy 檔案參考使用，或使用應用程式根目錄相對路徑 (（以波狀符號) 開始）透過 ScriptManager 進行註冊：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="cb1fc-174">一般來說，使用相同的方法來指定用於 CSS 或 JavaScript 檔案的 "/signalr/hubs" URL。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="cb1fc-175">如果您在不使用波狀符號的情況下指定 URL，在某些情況下，當您使用 IIS Express 在 Visual Studio 中進行測試時，您的應用程式將會正常運作，但當您部署至完整404的 IIS 時，將會失敗</span><span class="sxs-lookup"><span data-stu-id="cb1fc-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="cb1fc-176">如需詳細資訊，請參閱 MSDN 網站上的[針對 ASP.NET Web 專案在 Visual Studio 中解析 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)中**Root-Level 資源的參考**。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="cb1fc-177">當您在 [偵測模式] 的 Visual Studio 2017 中執行 Web 專案時，如果使用 Internet Explorer 作為瀏覽器，您可以在 [**腳本**] 底下的**方案總管**中看到 proxy 檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="cb1fc-178">若要查看檔案的內容，請按兩下 [ **集線器**]。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="cb1fc-179">如果您不是使用 Visual Studio 2012 或 Internet Explorer 2013，或不是處於「偵測」模式，也可以流覽至 "/signalR/hubs" URL 來取得檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="cb1fc-180">例如，如果您的網站正在執行 `http://localhost:56699` ，請移至 `http://localhost:56699/SignalR/hubs` 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="cb1fc-181">如何建立 SignalR 產生之 proxy 的實體檔案</span><span class="sxs-lookup"><span data-stu-id="cb1fc-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="cb1fc-182">作為動態產生之 proxy 的替代方案，您可以建立具有 proxy 程式碼的實體檔案並參考該檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="cb1fc-183">您可能會想要這樣做，以控制快取或組合行為，或在撰寫伺服器方法的呼叫程式碼時取得 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="cb1fc-184">若要建立 proxy 檔案，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="cb1fc-185">安裝 [SignalR. 公用程式](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="cb1fc-186">開啟命令提示字元，然後流覽至包含 SignalR.exe 檔案的 [ *tools* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="cb1fc-187">[工具] 資料夾位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="cb1fc-188">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="cb1fc-189">*.Dll*的路徑通常是您專案資料夾中的*bin*資料夾。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="cb1fc-190">此命令會在與*signalr.exe*相同的資料夾中，建立名為*server.js*的檔案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="cb1fc-191">將 *server.js* 檔案放在專案的適當資料夾中，將它重新命名為適用于您的應用程式，並在其中新增參考以取代 "signalr/hub" 參考。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="cb1fc-192">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-192">How to establish a connection</span></span>

<span data-ttu-id="cb1fc-193">建立連接之前，您必須建立連線物件、建立 proxy，以及註冊可從伺服器呼叫之方法的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="cb1fc-194">設定 proxy 和事件處理常式時，請呼叫方法來建立連接 `start` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="cb1fc-195">如果您使用產生的 proxy，則不需要在自己的程式碼中建立連線物件，因為產生的 proxy 程式碼會為您執行此工作。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="cb1fc-196">\*\*建立與產生的 proxy (的連接) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="cb1fc-197">\*\*建立沒有產生之 proxy 的連接 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="cb1fc-198">範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="cb1fc-199">如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="cb1fc-200">根據預設，中樞位置是目前的伺服器;如果您要連接到不同的伺服器，請在呼叫方法之前指定 URL `start` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="cb1fc-201">一般來說，您會先註冊事件處理常式，然後再呼叫 `start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="cb1fc-202">如果您想要在建立連接之後註冊某些事件處理常式，您可以這樣做，但您必須在呼叫方法之前，先在) 中至少註冊一個事件處理常式 (`start` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="cb1fc-203">其中一個原因是應用程式中可能會有許多中樞，但 `OnConnected` 如果您只是要使用其中一個中樞，就不會想要在每個中樞上觸發該事件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="cb1fc-204">建立連線時，中樞 proxy 上的用戶端方法是否存在會告知 SignalR 觸發 `OnConnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="cb1fc-205">如果您未在呼叫方法之前註冊任何事件處理常式 `start` ，您將能夠在中樞上叫用方法，但不會呼叫中樞的方法，也不會 `OnConnected` 從伺服器叫用任何用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="cb1fc-206">hubConnection ( # A1 所建立的相同物件</span><span class="sxs-lookup"><span data-stu-id="cb1fc-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="cb1fc-207">如您在範例中所見，當您使用產生的 proxy 時，會 `$.connection.hub` 參考連線物件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="cb1fc-208">`$.hubConnection()`當您未使用產生的 proxy 時，就會呼叫這個相同的物件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="cb1fc-209">產生的 proxy 程式碼會藉由執行下列語句，為您建立連接：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![在產生的 proxy 檔案中建立連接](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="cb1fc-211">當您使用產生的 proxy 時，您可以使用連線物件來進行任何動作， `$.connection.hub` 而不是使用產生的 proxy。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="cb1fc-212">啟動方法的非同步執行</span><span class="sxs-lookup"><span data-stu-id="cb1fc-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="cb1fc-213">`start`方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="cb1fc-214">它會傳回 [JQuery 延遲的物件](http://api.jquery.com/category/deferred-object/)，這表示您可以藉由呼叫、和等方法來加入回呼函數 `pipe` `done` `fail` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="cb1fc-215">如果您有想要在建立連接之後執行的程式碼，例如對伺服器方法的呼叫，請將該程式碼放在回呼函式中，或從回呼函數呼叫它。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="cb1fc-216">`.done`回呼方法是在建立連接之後，以及 `OnConnected` 伺服器上的事件處理常式方法中的任何程式碼完成執行之後執行。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="cb1fc-217">如果您將上述範例中的「立即連線」語句做為方法呼叫之後的下一行程式碼 `start` (不在 `.done` 回呼) 中，則 `console.log` 會在建立連接之前執行這一行，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![撰寫在建立連線後執行之程式碼的錯誤方式](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="cb1fc-219">如何建立跨網域連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="cb1fc-220">一般而言，如果瀏覽器從載入頁面 `http://contoso.com` ，SignalR 連接會位於相同的網域中 `http://contoso.com/signalr` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="cb1fc-221">如果頁面無法 `http://contoso.com` 連接到 `http://fabrikam.com/signalr` ，則為跨網域連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="cb1fc-222">基於安全性考慮，預設會停用跨網域連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="cb1fc-223">在 SignalR 1.x 中，跨網域要求是由單一 EnableCrossDomain 旗標所控制。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="cb1fc-224">此旗標會控制 JSONP 和 CORS 要求。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="cb1fc-225">為了獲得更大的彈性，已從 SignalR 的伺服器元件中移除所有 CORS 支援 (如果偵測到瀏覽器支援) ，且已提供新的 OWIN 中介軟體以支援這些案例，則這些用戶端仍會正常使用 CORS。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="cb1fc-226">如果用戶端 (需要 JSONP，以支援舊版瀏覽器中的跨網域要求) ，則必須將 `EnableJSONP` 物件上的設定設為，以明確地啟用它 `HubConfiguration` `true` ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="cb1fc-227">JSONP 預設為停用，因為它比 CORS 更不安全。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="cb1fc-228">**將 Owin 新增至您的專案：** 若要安裝此程式庫，請在封裝管理員主控台中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="cb1fc-229">此命令會將2.1.0 版本的套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="cb1fc-230">呼叫 UseCors</span><span class="sxs-lookup"><span data-stu-id="cb1fc-230">Calling UseCors</span></span>

 <span data-ttu-id="cb1fc-231">下列程式碼片段示範如何在 SignalR 2 中執行跨網域連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="cb1fc-232">**在 SignalR 2 中執行跨網域要求**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="cb1fc-233">下列程式碼示範如何在 SignalR 2 專案中啟用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="cb1fc-234">這個程式碼範例 `Map` 會使用和 `RunSignalR` 而不是 `MapSignalR` ，因此 cors 中介軟體只會針對需要 CORS 支援的 SignalR 要求執行，而不是針對中指定之路徑上的所有流量執行 (`MapSignalR` 。 ) 對應也可以用於任何其他需要針對特定 URL 前置詞執行的中介軟體，而不是整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="cb1fc-235">請勿 `jQuery.support.cors` 在程式碼中將設定為 true。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![請勿將 jQuery 設定為 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="cb1fc-237">SignalR 會處理 CORS 的使用。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="cb1fc-238">將設定 `jQuery.support.cors` 為 true 會停用 JSONP，因為它會導致 SignalR 假設瀏覽器支援 CORS。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="cb1fc-239">當您連線到 localhost URL 時，Internet Explorer 10 不會將它視為跨網域連線，因此即使您未在伺服器上啟用跨網域連線，應用程式還是會在本機使用 IE 10。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="cb1fc-240">如需有關搭配 Internet Explorer 9 使用跨網域連接的詳細資訊，請參閱 [這個 StackOverflow 執行緒](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="cb1fc-241">如需有關搭配使用跨網域連接與 Chrome 的詳細資訊，請參閱 [這個 StackOverflow 執行緒](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="cb1fc-242">範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="cb1fc-243">如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="cb1fc-244">如何設定連接</span><span class="sxs-lookup"><span data-stu-id="cb1fc-244">How to configure the connection</span></span>

<span data-ttu-id="cb1fc-245">建立連接之前，您可以指定查詢字串參數，或指定傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="cb1fc-246">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="cb1fc-246">How to specify query string parameters</span></span>

<span data-ttu-id="cb1fc-247">如果您想要在用戶端連接時將資料傳送至伺服器，您可以將查詢字串參數加入至連線物件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="cb1fc-248">下列範例示範如何在用戶端程式代碼中設定查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="cb1fc-249">\*\*先設定查詢字串值，再使用產生的 proxy 呼叫 start 方法 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="cb1fc-250">\*\*在不使用產生的 proxy 呼叫開始方法 (之前，請先設定查詢字串值) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="cb1fc-251">下列範例示範如何在伺服器程式碼中讀取查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="cb1fc-252">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-252">How to specify the transport method</span></span>

<span data-ttu-id="cb1fc-253">在連接的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端所支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="cb1fc-254">如果您已經知道要使用哪一個傳輸，可以在呼叫方法時指定傳輸方法，以略過此協商程式 `start` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="cb1fc-255">\*\*用戶端程式代碼，指定與產生的 proxy (的傳輸方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="cb1fc-256">\*\*指定傳輸方法 (的用戶端程式代碼，不含產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="cb1fc-257">或者，您可以依照想要 SignalR 嘗試的順序來指定多個傳輸方法：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="cb1fc-258">\*\*指定與產生的 proxy (的自訂傳輸回溯配置的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="cb1fc-259">\*\*指定自訂傳輸回溯配置的用戶端程式代碼 (沒有產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="cb1fc-260">您可以使用下列值來指定傳輸方法：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="cb1fc-261">Websocket</span><span class="sxs-lookup"><span data-stu-id="cb1fc-261">"webSockets"</span></span>
- <span data-ttu-id="cb1fc-262">"foreverFrame"</span><span class="sxs-lookup"><span data-stu-id="cb1fc-262">"foreverFrame"</span></span>
- <span data-ttu-id="cb1fc-263">"serverSentEvents"</span><span class="sxs-lookup"><span data-stu-id="cb1fc-263">"serverSentEvents"</span></span>
- <span data-ttu-id="cb1fc-264">"longPolling"</span><span class="sxs-lookup"><span data-stu-id="cb1fc-264">"longPolling"</span></span>

<span data-ttu-id="cb1fc-265">下列範例會示範如何找出連接所使用的傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="cb1fc-266">\*\*用戶端程式代碼，顯示連接 (與產生的 proxy 所使用的傳輸方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="cb1fc-267">\*\*用戶端程式代碼，顯示連接 (所使用的傳輸方法，不含產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="cb1fc-268">如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="cb1fc-269">如需傳輸和回退的詳細資訊，請參閱 [SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="cb1fc-270">如何取得中樞類別的 proxy</span><span class="sxs-lookup"><span data-stu-id="cb1fc-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="cb1fc-271">您建立的每個連線物件都會封裝與包含一或多個中樞類別的 SignalR 服務連線相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="cb1fc-272">若要與中樞類別通訊，請使用您自己建立的 proxy 物件 (如果您不是使用產生的 proxy) 或為您產生的 proxy。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="cb1fc-273">在用戶端上，proxy 名稱是中樞類別名稱的 camel 大小寫版本。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="cb1fc-274">SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="cb1fc-275">**伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="cb1fc-276">**取得針對中樞所產生之用戶端 proxy 的參考**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="cb1fc-277">\*\*建立中樞類別 (的用戶端 proxy，而不產生 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="cb1fc-278">如果您使用屬性裝飾您的中樞類別 `HubName` ，請使用完整名稱，而不變更大小寫。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="cb1fc-279">**伺服器上具有 HubName 屬性的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="cb1fc-280">**取得針對中樞所產生之用戶端 proxy 的參考**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="cb1fc-281">\*\*建立中樞類別 (的用戶端 proxy，而不產生 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="cb1fc-282">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="cb1fc-283">若要定義伺服器可以從中樞呼叫的方法，請使用所產生之 proxy 的屬性將事件處理常式新增至中樞 proxy `client` ，或者， `on` 如果您未使用產生的 proxy，請呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="cb1fc-284">這些參數可以是複雜的物件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="cb1fc-285">先加入事件處理常式，然後再呼叫 `start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="cb1fc-286"> (如果您要在呼叫方法之後新增事件處理常式 `start` ，請參閱本檔前面 [如何建立連接](#establishconnection) 的附注，並使用所示的語法來定義方法，而不使用產生的 proxy。 ) </span><span class="sxs-lookup"><span data-stu-id="cb1fc-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="cb1fc-287">方法名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="cb1fc-288">例如， `Clients.All.addContosoChatMessageToPage` 在伺服器上，伺服器將會在 `AddContosoChatMessageToPage` 用戶端上執行、 `addContosoChatMessageToPage` 或 `addcontosochatmessagetopage` 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="cb1fc-289">\*\*使用產生的 proxy 定義用戶端 (上的方法) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="cb1fc-290">\*\*使用產生的 proxy 在用戶端 (上定義方法的替代方式) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="cb1fc-291">\*\*在用戶端 (上定義不含產生之 proxy 的方法，或在呼叫 start 方法之後新增時) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="cb1fc-292">**呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="cb1fc-293">下列範例包含複雜物件做為方法參數。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="cb1fc-294">\*\*在用戶端上定義方法，該方法會採用複雜物件 (與產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="cb1fc-295">\*\*在用戶端上定義方法，此方法會採用複雜物件 (沒有產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="cb1fc-296">**定義複雜物件的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="cb1fc-297">**使用複雜物件呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="cb1fc-298">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="cb1fc-298">How to call server methods from the client</span></span>

<span data-ttu-id="cb1fc-299">若要從用戶端呼叫伺服器方法，請使用所 `server` 產生之 proxy 的屬性或 `invoke` 中樞 proxy 上的方法（如果您未使用產生的 proxy）。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="cb1fc-300">傳回值或參數可以是複雜的物件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="cb1fc-301">傳入中樞上方法名稱的 camel 大小寫版本。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="cb1fc-302">SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="cb1fc-303">下列範例示範如何呼叫沒有傳回值的伺服器方法，以及如何呼叫有傳回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="cb1fc-304">**沒有 HubMethodName 屬性的伺服器方法**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="cb1fc-305">**定義在參數中傳遞之複雜物件的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="cb1fc-306">\*\*使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="cb1fc-307">\*\*在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="cb1fc-308">如果您使用屬性裝飾中樞方法 `HubMethodName` ，請使用該名稱，而不變更大小寫。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="cb1fc-309">具有 HubMethodName 屬性的**伺服器方法**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="cb1fc-310">\*\*使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="cb1fc-311">\*\*在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="cb1fc-312">上述範例示範如何呼叫沒有傳回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="cb1fc-313">下列範例示範如何呼叫具有傳回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="cb1fc-314">**具有傳回值之方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="cb1fc-315">用於傳回值的**Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="cb1fc-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="cb1fc-316">\*\*使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="cb1fc-317">\*\*在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="cb1fc-318">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="cb1fc-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="cb1fc-319">SignalR 提供下列可供您處理的連接存留期事件：</span><span class="sxs-lookup"><span data-stu-id="cb1fc-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="cb1fc-320">`starting`：在透過連接傳送任何資料之前引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="cb1fc-321">`received`：在連接上收到任何資料時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="cb1fc-322">提供接收的資料。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-322">Provides the received data.</span></span>
- <span data-ttu-id="cb1fc-323">`connectionSlow`：當用戶端偵測到緩慢或經常中斷連接時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="cb1fc-324">`reconnecting`：當基礎傳輸開始重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="cb1fc-325">`reconnected`：當基礎傳輸重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="cb1fc-326">`stateChanged`：當連接狀態變更時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="cb1fc-327">提供舊狀態和新狀態 (連接、連線、重新連線或中斷連線) 。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="cb1fc-328">`disconnected`：連接中斷連接時引發。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="cb1fc-329">例如，如果您想要在有可能造成明顯延遲的連接問題時顯示警告訊息，請處理 `connectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="cb1fc-330">\*\*使用產生的 proxy 來處理 connectionSlow 事件 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="cb1fc-331">\*\*處理 connectionSlow 事件 (而不需要產生的 proxy) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="cb1fc-332">如需詳細資訊，請參閱 [瞭解及處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="cb1fc-333">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="cb1fc-333">How to handle errors</span></span>

<span data-ttu-id="cb1fc-334">SignalR JavaScript 用戶端會提供 `error` 您可以為其新增處理常式的事件。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="cb1fc-335">您也可以使用 fail 方法來加入伺服器方法調用所產生之錯誤的處理常式。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="cb1fc-336">如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 在錯誤之後傳回的例外狀況物件會包含錯誤的最基本資訊。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="cb1fc-337">例如，如果的呼叫 `newContosoChatMessage` 失敗，則錯誤物件中的錯誤訊息會包含「」 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 基於安全性理由，不建議在生產環境中傳送詳細的錯誤訊息給用戶端，但如果您想要啟用詳細的錯誤訊息以進行疑難排解，請在伺服器上使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="cb1fc-338">下列範例顯示如何加入錯誤事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="cb1fc-339">\*\*使用產生的 proxy 加入錯誤處理常式 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="cb1fc-340">\*\*在沒有產生的 proxy 的情況下新增錯誤處理常式 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="cb1fc-341">下列範例顯示如何處理方法調用的錯誤。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="cb1fc-342">\*\*使用產生的 proxy 處理方法調用 (的錯誤) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="cb1fc-343">\*\*在沒有產生的 proxy 的情況下，處理方法調用 (的錯誤) \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="cb1fc-344">如果方法調用失敗， `error` 也會引發事件，因此您在 `error` 方法處理常式和方法回呼中的程式碼 `.fail` 都會執行。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="cb1fc-345">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="cb1fc-345">How to enable client-side logging</span></span>

<span data-ttu-id="cb1fc-346">若要啟用連接的用戶端記錄，請先在 `logging` 連線物件上設定屬性，然後再呼叫 `start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="cb1fc-347">\*\*使用產生的 proxy 啟用記錄 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="cb1fc-348">\*\*不使用產生的 proxy 來啟用記錄 () \*\*</span><span class="sxs-lookup"><span data-stu-id="cb1fc-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="cb1fc-349">若要查看記錄，請開啟瀏覽器的開發人員工具，並移至 [主控台] 索引標籤。如需示範如何執行這項操作的逐步指示和螢幕擷取畫面的教學課程，請參閱 [使用 ASP.NET Signalr 進行伺服器廣播-啟用記錄](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。</span><span class="sxs-lookup"><span data-stu-id="cb1fc-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
