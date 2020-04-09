---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET信號器中心 API 指南 - JAVAScript 用戶端 |微軟文件
author: bradygaster
description: 本文件介紹了在 JavaScript 用戶端(如瀏覽器和 Windows 應用商店 (WinJS) 應用中,將集線器 API 用於 SignalR 版本 2。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676080"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a><span data-ttu-id="13bbd-103">ASP.NET信號器中心 API 指南 - JAVAScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="13bbd-103">ASP.NET SignalR Hubs API Guide - JavaScript Client</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="13bbd-104">本文件介紹了在 JavaScript 用戶端(如瀏覽器和 Windows 應用商店 (WinJS) 應用程式中,將集線器 API 用於 SignalR 版本 2。</span><span class="sxs-lookup"><span data-stu-id="13bbd-104">This document provides an introduction to using the Hubs API for SignalR version 2 in JavaScript clients, such as browsers and Windows Store (WinJS) applications.</span></span>
>
> <span data-ttu-id="13bbd-105">SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="13bbd-106">在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="13bbd-107">在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="13bbd-108">SignalR 為您處理所有用戶端到伺服器管道。</span><span class="sxs-lookup"><span data-stu-id="13bbd-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="13bbd-109">SignalR 還提供稱為持久連接的較低級別的 API。</span><span class="sxs-lookup"><span data-stu-id="13bbd-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="13bbd-110">有關信號R、集線器和持久連接的介紹,請參閱[訊號R 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-110">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="13bbd-111">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="13bbd-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="13bbd-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="13bbd-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="13bbd-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="13bbd-113">.NET 4.5</span></span>
> - <span data-ttu-id="13bbd-114">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="13bbd-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="13bbd-115">本主題的早期版本</span><span class="sxs-lookup"><span data-stu-id="13bbd-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="13bbd-116">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="13bbd-117">問題和評論</span><span class="sxs-lookup"><span data-stu-id="13bbd-117">Questions and comments</span></span>
>
> <span data-ttu-id="13bbd-118">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="13bbd-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="13bbd-119">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="13bbd-120">概觀</span><span class="sxs-lookup"><span data-stu-id="13bbd-120">Overview</span></span>

<span data-ttu-id="13bbd-121">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="13bbd-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="13bbd-122">產生的代理及其為您做什麼</span><span class="sxs-lookup"><span data-stu-id="13bbd-122">The generated proxy and what it does for you</span></span>](#genproxy)

    - [<span data-ttu-id="13bbd-123">何時使用產生的代理程式</span><span class="sxs-lookup"><span data-stu-id="13bbd-123">When to use the generated proxy</span></span>](#cantusegenproxy)
- [<span data-ttu-id="13bbd-124">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="13bbd-124">Client Setup</span></span>](#clientsetup)

    - [<span data-ttu-id="13bbd-125">如何參考動態產生的代理程式</span><span class="sxs-lookup"><span data-stu-id="13bbd-125">How to reference the dynamically generated proxy</span></span>](#dynamicproxy)
    - [<span data-ttu-id="13bbd-126">如何為 SignalR 產生的代理建立物理檔案</span><span class="sxs-lookup"><span data-stu-id="13bbd-126">How to create a physical file for the SignalR generated proxy</span></span>](#manualproxy)
- [<span data-ttu-id="13bbd-127">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-127">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="13bbd-128">$.connect.hub 是 $.hubConnection() 創建的物件</span><span class="sxs-lookup"><span data-stu-id="13bbd-128">$.connection.hub is the same object that $.hubConnection() creates</span></span>](#connequivalence)
    - [<span data-ttu-id="13bbd-129">啟動方法的非同步執行</span><span class="sxs-lookup"><span data-stu-id="13bbd-129">Asynchronous execution of the start method</span></span>](#asyncstart)
- [<span data-ttu-id="13bbd-130">如何建立跨網域連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-130">How to establish a cross-domain connection</span></span>](#crossdomain)
- [<span data-ttu-id="13bbd-131">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-131">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="13bbd-132">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="13bbd-132">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="13bbd-133">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-133">How to specify the transport method</span></span>](#transport)
- [<span data-ttu-id="13bbd-134">如何取得中心類的代理</span><span class="sxs-lookup"><span data-stu-id="13bbd-134">How to get a proxy for a Hub class</span></span>](#getproxy)
- [<span data-ttu-id="13bbd-135">如何在客戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-135">How to define methods on the client that the server can call</span></span>](#callclient)
- [<span data-ttu-id="13bbd-136">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-136">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="13bbd-137">如何處理連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="13bbd-137">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="13bbd-138">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="13bbd-138">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="13bbd-139">如何開啟客戶端記錄記錄</span><span class="sxs-lookup"><span data-stu-id="13bbd-139">How to enable client-side logging</span></span>](#logging)

<span data-ttu-id="13bbd-140">有關如何對伺服器或 .NET 客戶端進行程式設計的文件,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="13bbd-140">For documentation on how to program the server or .NET clients, see the following resources:</span></span>

- [<span data-ttu-id="13bbd-141">訊號器集線器 API 指南 - 伺服器</span><span class="sxs-lookup"><span data-stu-id="13bbd-141">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="13bbd-142">信號器集線器 API 指南 - .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="13bbd-142">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="13bbd-143">SignalR 2 伺服器元件僅在 .NET 4.5 上可用(儘管在 .NET 4.0 上有一個用於 SignalR 2 的 .NET 用戶端)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-143">The SignalR 2 server component is only available on .NET 4.5 (though there is a .NET client for SignalR 2 on .NET 4.0).</span></span>

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a><span data-ttu-id="13bbd-144">產生的代理及其為您做什麼</span><span class="sxs-lookup"><span data-stu-id="13bbd-144">The generated proxy and what it does for you</span></span>

<span data-ttu-id="13bbd-145">您可以對 JavaScript 用戶端進行程式設計,以便與 SignalR 服務進行通訊,無論是否沒有 SignalR 為您生成的代理。</span><span class="sxs-lookup"><span data-stu-id="13bbd-145">You can program a JavaScript client to communicate with a SignalR service with or without a proxy that SignalR generates for you.</span></span> <span data-ttu-id="13bbd-146">代理的作用是簡化用於連接的代碼的語法、編寫伺服器調用的方法以及調用伺服器上的方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-146">What the proxy does for you is simplify the syntax of the code you use to connect, write methods that the server calls, and call methods on the server.</span></span>

<span data-ttu-id="13bbd-147">編寫程式以呼叫伺服器方法時,產生的代理程式讓您能夠使用看起來好像在執行本地函數的語法:可以編`serverMethod(arg1, arg2)`寫`invoke('serverMethod', arg1, arg2)`而不是 。</span><span class="sxs-lookup"><span data-stu-id="13bbd-147">When you write code to call server methods, the generated proxy enables you to use syntax that looks as though you were executing a local function: you can write `serverMethod(arg1, arg2)` instead of `invoke('serverMethod', arg1, arg2)`.</span></span> <span data-ttu-id="13bbd-148">如果鍵入伺服器方法名稱錯誤,生成的代理語法還允許立即且可理解的用戶端錯誤。</span><span class="sxs-lookup"><span data-stu-id="13bbd-148">The generated proxy syntax also enables an immediate and intelligible client-side error if you mistype a server method name.</span></span> <span data-ttu-id="13bbd-149">如果手動創建定義代理的檔,還可以獲得 IntelliSense 支援編寫調用伺服器方法的代碼。</span><span class="sxs-lookup"><span data-stu-id="13bbd-149">And if you manually create the file that defines the proxies, you can also get IntelliSense support for writing code that calls server methods.</span></span>

<span data-ttu-id="13bbd-150">例如,假設您在伺服器上具有以下中心類:</span><span class="sxs-lookup"><span data-stu-id="13bbd-150">For example, suppose you have the following Hub class on the server:</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

<span data-ttu-id="13bbd-151">以下代碼示例顯示了 JavaScript 代碼在伺服器`NewContosoChatMessage`上調用 該方法和`addContosoChatMessageToPage`從伺服器接收 方法調用的外觀。</span><span class="sxs-lookup"><span data-stu-id="13bbd-151">The following code examples show what JavaScript code looks like for invoking the `NewContosoChatMessage` method on the server and receiving invocations of the `addContosoChatMessageToPage` method from the server.</span></span>

<span data-ttu-id="13bbd-152">**使用產生的代理程式**</span><span class="sxs-lookup"><span data-stu-id="13bbd-152">**With the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

<span data-ttu-id="13bbd-153">**沒有產生的代理**</span><span class="sxs-lookup"><span data-stu-id="13bbd-153">**Without the generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a><span data-ttu-id="13bbd-154">何時使用產生的代理程式</span><span class="sxs-lookup"><span data-stu-id="13bbd-154">When to use the generated proxy</span></span>

<span data-ttu-id="13bbd-155">如果要為伺服器調用的用戶端方法註冊多個事件處理程式,則不能使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="13bbd-155">If you want to register multiple event handlers for a client method that the server calls, you can't use the generated proxy.</span></span> <span data-ttu-id="13bbd-156">否則,您可以選擇使用生成的代理,或者不使用基於編碼首選項。</span><span class="sxs-lookup"><span data-stu-id="13bbd-156">Otherwise, you can choose to use the generated proxy or not based on your coding preference.</span></span> <span data-ttu-id="13bbd-157">如果選擇不使用它,則不必在客戶端`script`代碼 中的元素中引用"信號器/集線器"URL。</span><span class="sxs-lookup"><span data-stu-id="13bbd-157">If you choose not to use it, you don't have to reference the "signalr/hubs" URL in a `script` element in your client code.</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="13bbd-158">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="13bbd-158">Client setup</span></span>

<span data-ttu-id="13bbd-159">JavaScript 用戶端需要引用 jQuery 和 SignalR 核心 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="13bbd-159">A JavaScript client requires references to jQuery and the SignalR core JavaScript file.</span></span> <span data-ttu-id="13bbd-160">jQuery 版本必須為 1.6.4 或主要更高版本,例如 1.7.2、1.8.2 或 1.9.1。</span><span class="sxs-lookup"><span data-stu-id="13bbd-160">The jQuery version must be 1.6.4 or major later versions, such as 1.7.2, 1.8.2, or 1.9.1.</span></span> <span data-ttu-id="13bbd-161">如果您決定使用生成的代理,還需要引用 SignalR 生成的代理 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="13bbd-161">If you decide to use the generated proxy, you also need a reference to the SignalR generated proxy JavaScript file.</span></span> <span data-ttu-id="13bbd-162">下面的範例顯示了使用生成的代理的 HTML 頁中引用的外觀。</span><span class="sxs-lookup"><span data-stu-id="13bbd-162">The following example shows what the references might look like in an HTML page that uses the generated proxy.</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

<span data-ttu-id="13bbd-163">這些引用必須包含在此順序中:jQuery 優先,之後為 SignalR 內核,最後顯示 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="13bbd-163">These references must be included in this order: jQuery first, SignalR core after that, and SignalR proxies last.</span></span>

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a><span data-ttu-id="13bbd-164">如何參考動態產生的代理程式</span><span class="sxs-lookup"><span data-stu-id="13bbd-164">How to reference the dynamically generated proxy</span></span>

<span data-ttu-id="13bbd-165">在前面的範例中,對 SignalR 生成的代理的引用是動態生成的 JavaScript 代碼,而不是物理檔。</span><span class="sxs-lookup"><span data-stu-id="13bbd-165">In the preceding example, the reference to the SignalR generated proxy is to dynamically generated JavaScript code, not to a physical file.</span></span> <span data-ttu-id="13bbd-166">SignalR 動態為代理創建 JavaScript 代碼,並將其用於用戶端以回應"/信號器/集線器"URL。</span><span class="sxs-lookup"><span data-stu-id="13bbd-166">SignalR creates the JavaScript code for the proxy on the fly and serves it to the client in response to the "/signalr/hubs" URL.</span></span> <span data-ttu-id="13bbd-167">如果在方法`MapSignalR`中為伺服器上的 SignalR 連接指定了不同的基本 URL,則動態生成的代理檔的 URL 是自定義 URL,並附加了"/集線器"</span><span class="sxs-lookup"><span data-stu-id="13bbd-167">If you specified a different base URL for SignalR connections on the server in your `MapSignalR` method, the URL for the dynamically generated proxy file is your custom URL with "/hubs" appended to it.</span></span>

> [!NOTE]
> <span data-ttu-id="13bbd-168">對於 Windows 8(Windows 應用商店)JavaScript 用戶端,請使用物理代理檔而不是動態生成的檔。</span><span class="sxs-lookup"><span data-stu-id="13bbd-168">For Windows 8 (Windows Store) JavaScript clients, use the physical proxy file instead of the dynamically generated one.</span></span> <span data-ttu-id="13bbd-169">有關詳細資訊,請參閱本主題後面的[「如何為 SignalR 生成的代理創建實體檔](#manualproxy)」。。</span><span class="sxs-lookup"><span data-stu-id="13bbd-169">For more information, see [How to create a physical file for the SignalR generated proxy](#manualproxy) later in this topic.</span></span>

<span data-ttu-id="13bbd-170">在ASP.NET MVC 4 或 5 Razor 檢視中,使用波浪線引用代理檔引用中的應用程式根:</span><span class="sxs-lookup"><span data-stu-id="13bbd-170">In an ASP.NET MVC 4 or 5 Razor view, use the tilde to refer to the application root in your proxy file reference:</span></span>

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

<span data-ttu-id="13bbd-171">有關在 MVC 5 中使用訊號 R 的詳細資訊,請參閱[使用訊號 R 和 MVC 5 入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-171">For more information about using SignalR in MVC 5, see [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="13bbd-172">在ASP.NET MVC 3`Url.Content`Razor 檢視中,用於代理檔引用:</span><span class="sxs-lookup"><span data-stu-id="13bbd-172">In an ASP.NET MVC 3 Razor view, use `Url.Content` for your proxy file reference:</span></span>

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

<span data-ttu-id="13bbd-173">在ASP.NET Web 表單應用程式`ResolveClientUrl`中, 使用代理檔案參考或使用應用根相對路徑(以波浪線開頭)透過文稿管理員註冊它:</span><span class="sxs-lookup"><span data-stu-id="13bbd-173">In an ASP.NET Web Forms application, use `ResolveClientUrl` for your proxies file reference or register it via the ScriptManager using an app root relative path (starting with a tilde):</span></span>

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

<span data-ttu-id="13bbd-174">通常,使用相同的方法來指定用於 CSS 或 JavaScript 檔的"/信號器/集線器"</span><span class="sxs-lookup"><span data-stu-id="13bbd-174">As a general rule, use the same method for specifying the "/signalr/hubs" URL that you use for CSS or JavaScript files.</span></span> <span data-ttu-id="13bbd-175">如果在不使用波浪線的情況下指定 URL,則在某些情況下,當您使用 IIS Express 在 Visual Studio 中測試時,應用程式將正常工作,但在部署到完整 IIS 時,應用程式將失敗,出現 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="13bbd-175">If you specify a URL without using a tilde, in some scenarios your application will work correctly when you test in Visual Studio using IIS Express but will fail with a 404 error when you deploy to full IIS.</span></span> <span data-ttu-id="13bbd-176">有關詳細資訊,請參閱在 Visual Studio 中解析對 Web 伺服器中的**根級資源的引用**[,以便 ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) MSDN 網站上的 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="13bbd-176">For more information, see **Resolving References to Root-Level Resources** in [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx) on the MSDN site.</span></span>

<span data-ttu-id="13bbd-177">當您在 Visual Studio 2017 中除錯模式下執行 Web 專案時,如果您使用 Internet Explorer 作為瀏覽器,則可以在**文稿**下**的解決方案資源管理器**中看到代理檔。</span><span class="sxs-lookup"><span data-stu-id="13bbd-177">When you run a web project in Visual Studio 2017 in debug mode, and if you use Internet Explorer as your browser, you can see the proxy file in **Solution Explorer** under **Scripts**.</span></span>

<span data-ttu-id="13bbd-178">要檢視檔案的內容,請按兩下**集線器**。</span><span class="sxs-lookup"><span data-stu-id="13bbd-178">To see the contents of the file, double-click **hubs**.</span></span> <span data-ttu-id="13bbd-179">如果您沒有使用 Visual Studio 2012 或 2013 和 Internet Explorer,或者如果您未處於調試模式,還可以透過流覽"/signalR/集線器"URL來獲取文件內容。</span><span class="sxs-lookup"><span data-stu-id="13bbd-179">If you are not using Visual Studio 2012 or 2013 and Internet Explorer, or if you are not in debug mode, you can also get the contents of the file by browsing to the "/signalR/hubs" URL.</span></span> <span data-ttu-id="13bbd-180">例如,如果您的網站在`http://localhost:56699`中運行,請轉到`http://localhost:56699/SignalR/hubs`瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="13bbd-180">For example, if your site is running at `http://localhost:56699`, go to `http://localhost:56699/SignalR/hubs` in your browser.</span></span>

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a><span data-ttu-id="13bbd-181">如何為 SignalR 產生的代理建立物理檔案</span><span class="sxs-lookup"><span data-stu-id="13bbd-181">How to create a physical file for the SignalR generated proxy</span></span>

<span data-ttu-id="13bbd-182">作為動態生成的代理的替代方法,您可以創建具有代理程式碼並引用該檔的實體檔。</span><span class="sxs-lookup"><span data-stu-id="13bbd-182">As an alternative to the dynamically generated proxy, you can create a physical file that has the proxy code and reference that file.</span></span> <span data-ttu-id="13bbd-183">您可能希望執行此操作以控制緩存或捆綁行為,或者在對伺服器方法的調用進行編碼時獲取 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="13bbd-183">You might want to do that for control over caching or bundling behavior, or to get IntelliSense when you are coding calls to server methods.</span></span>

<span data-ttu-id="13bbd-184">要建立代理檔,請執行以下步驟:</span><span class="sxs-lookup"><span data-stu-id="13bbd-184">To create a proxy file, perform the following steps:</span></span>

1. <span data-ttu-id="13bbd-185">安裝[Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-185">Install the [Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet package.</span></span>
2. <span data-ttu-id="13bbd-186">開啟命令提示符並瀏覽到包含 SignalR.exe 檔案*的工具*資料夾。</span><span class="sxs-lookup"><span data-stu-id="13bbd-186">Open a command prompt and browse to the *tools* folder that contains the SignalR.exe file.</span></span> <span data-ttu-id="13bbd-187">工具資料夾位於以下位置:</span><span class="sxs-lookup"><span data-stu-id="13bbd-187">The tools folder is at the following location:</span></span>

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. <span data-ttu-id="13bbd-188">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="13bbd-188">Enter the following command:</span></span>

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    <span data-ttu-id="13bbd-189">*.dll*的路徑通常是項目資料夾中的*bin*資料夾。</span><span class="sxs-lookup"><span data-stu-id="13bbd-189">The path to your *.dll* is typically the *bin* folder in your project folder.</span></span>

    <span data-ttu-id="13bbd-190">此命令創建名為*server.js*的檔案,該檔與*signalr.exe*在同一資料夾中。</span><span class="sxs-lookup"><span data-stu-id="13bbd-190">This command creates a file named *server.js* in the same folder as *signalr.exe*.</span></span>
4. <span data-ttu-id="13bbd-191">將*server.js*檔案放在專案中的相應資料夾中,將其重新命名為適合您的應用程式,並添加對該檔的引用,以代替「信號器/集線器」引用。</span><span class="sxs-lookup"><span data-stu-id="13bbd-191">Put the *server.js* file in an appropriate folder in your project, rename it as appropriate for your application, and add a reference to it in place of the "signalr/hubs" reference.</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="13bbd-192">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-192">How to establish a connection</span></span>

<span data-ttu-id="13bbd-193">在建立連接之前,必須建立連接物件、創建代理和註冊事件處理程式,以便從伺服器調用的方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-193">Before you can establish a connection, you have to create a connection object, create a proxy, and register event handlers for methods that can be called from the server.</span></span> <span data-ttu-id="13bbd-194">設置代理和事件處理程式時,通過調用`start`方法建立連接。</span><span class="sxs-lookup"><span data-stu-id="13bbd-194">When the proxy and event handlers are set up, establish the connection by calling the `start` method.</span></span>

<span data-ttu-id="13bbd-195">如果使用生成的代理,則不必在自己的代碼中創建連接物件,因為生成的代理代碼會為您創建連接物件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-195">If you are using the generated proxy, you don't have to create the connection object in your own code because the generated proxy code does it for you.</span></span>

<a id="nogenconnection"></a>

<span data-ttu-id="13bbd-196">**建立連線(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-196">**Establish a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

<span data-ttu-id="13bbd-197">**建立連線(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-197">**Establish a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

<span data-ttu-id="13bbd-198">範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="13bbd-198">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="13bbd-199">有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-199">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="13bbd-200">默認情況下,中心位置是當前伺服器;如果要連接到其他伺服器,請在呼叫`start`該方法之前指定 URL,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="13bbd-200">By default, the hub location is the current server; if you are connecting to a different server, specify the URL before calling the `start` method, as shown in the following example:</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> <span data-ttu-id="13bbd-201">通常,在調用 方法以建立連接`start`之前 註冊事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-201">Normally you register event handlers before calling the `start` method to establish the connection.</span></span> <span data-ttu-id="13bbd-202">如果要在建立連接后註冊一些事件處理程式,可以執行此操作,但在調用`start`該方法之前,必須至少註冊一個事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-202">If you want to register some event handlers after establishing the connection, you can do that, but you must register at least one of your event handler(s) before calling the `start` method.</span></span> <span data-ttu-id="13bbd-203">原因之一是應用程式中可能有許多中心,但如果您只要使用其中一個集線器,則不希望在每個集`OnConnected`線器上觸發事件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-203">One reason for this is that there can be many Hubs in an application, but you wouldn't want to trigger the `OnConnected` event on every Hub if you are only going to use to one of them.</span></span> <span data-ttu-id="13bbd-204">建立連接後,在 Hub 的代理上存在用戶端方法是指示 SignalR 觸發`OnConnected`事件的原因。</span><span class="sxs-lookup"><span data-stu-id="13bbd-204">When the connection is established, the presence of a client method on a Hub's proxy is what tells SignalR to trigger the `OnConnected` event.</span></span> <span data-ttu-id="13bbd-205">如果在調用`start`方法之前未註冊任何事件處理程式,則可以在 Hub 上調用方法,但不會調`OnConnected`用 Hub 的方法,也不會從伺服器調用任何用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-205">If you don't register any event handlers before calling the `start` method, you will be able to invoke methods on the Hub, but the Hub's `OnConnected` method won't be called and no client methods will be invoked from the server.</span></span>

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a><span data-ttu-id="13bbd-206">$.connect.hub 是 $.hubConnection() 創建的物件</span><span class="sxs-lookup"><span data-stu-id="13bbd-206">$.connection.hub is the same object that $.hubConnection() creates</span></span>

<span data-ttu-id="13bbd-207">正如您從範例中所看到的,當您使用生成的代理時,`$.connection.hub`引用連接物件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-207">As you can see from the examples, when you use the generated proxy, `$.connection.hub` refers to the connection object.</span></span> <span data-ttu-id="13bbd-208">這與不使用生成的代理時通過調用`$.hubConnection()`獲得的物件相同。</span><span class="sxs-lookup"><span data-stu-id="13bbd-208">This is the same object that you get by calling `$.hubConnection()` when you aren't using the generated proxy.</span></span> <span data-ttu-id="13bbd-209">產生的代理程式碼執行以下文句為您建立連線:</span><span class="sxs-lookup"><span data-stu-id="13bbd-209">The generated proxy code creates the connection for you by executing the following statement:</span></span>

![建立建立的代理檔案建立連線](hubs-api-guide-javascript-client/_static/image3.png)

<span data-ttu-id="13bbd-211">使用生成的代理時,可以使用任何不使用生成的代理時對連接物件`$.connection.hub`執行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="13bbd-211">When you're using the generated proxy, you can do anything with `$.connection.hub` that you can do with a connection object when you're not using the generated proxy.</span></span>

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a><span data-ttu-id="13bbd-212">啟動方法的非同步執行</span><span class="sxs-lookup"><span data-stu-id="13bbd-212">Asynchronous execution of the start method</span></span>

<span data-ttu-id="13bbd-213">該方法`start`以異步方式執行。</span><span class="sxs-lookup"><span data-stu-id="13bbd-213">The `start` method executes asynchronously.</span></span> <span data-ttu-id="13bbd-214">它返回[jQuery 延遲物件](http://api.jquery.com/category/deferred-object/),這意味著您可以通過調`pipe`用`done`方法`fail`(如、 和) 添加回調函數。</span><span class="sxs-lookup"><span data-stu-id="13bbd-214">It returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means that you can add callback functions by calling methods such as `pipe`, `done`, and `fail`.</span></span> <span data-ttu-id="13bbd-215">如果已建立連接后需要執行的代碼(如調用伺服器方法),請將該代碼放入回調函數中,或從回調函數調用它。</span><span class="sxs-lookup"><span data-stu-id="13bbd-215">If you have code that you want to execute after the connection is established, such as a call to a server method, put that code in a callback function or call it from a callback function.</span></span> <span data-ttu-id="13bbd-216">回調`.done`方法在建立連接後執行,並在伺服器`OnConnected`上的事件處理程式方法中的任何代碼完成執行之後。</span><span class="sxs-lookup"><span data-stu-id="13bbd-216">The `.done` callback method is executed after the connection has been established, and after any code that you have in your `OnConnected` event handler method on the server finishes executing.</span></span>

<span data-ttu-id="13bbd-217">如果將上述範例中的「現在連線」語句作為`start`方法調用後的`.done`下一行代碼(不在回調中),則`console.log`該行將在建立連接之前執行,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="13bbd-217">If you put the "Now connected" statement from the preceding example as the next line of code after the `start` method call (not in a `.done` callback), the `console.log` line will execute before the connection is established, as shown in the following example:</span></span>

![編寫建立連接後執行的程式碼的錯誤方法](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a><span data-ttu-id="13bbd-219">如何建立跨網域連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-219">How to establish a cross-domain connection</span></span>

<span data-ttu-id="13bbd-220">通常,如果瀏覽器從`http://contoso.com`載入頁面,則 SignalR 連接位於同一`http://contoso.com/signalr`域中 ,在 。</span><span class="sxs-lookup"><span data-stu-id="13bbd-220">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="13bbd-221">如果中的`http://contoso.com`頁面與`http://fabrikam.com/signalr`斷開連接,則為跨域連接。</span><span class="sxs-lookup"><span data-stu-id="13bbd-221">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="13bbd-222">出於安全原因,默認情況下禁用跨域連接。</span><span class="sxs-lookup"><span data-stu-id="13bbd-222">For security reasons, cross-domain connections are disabled by default.</span></span>

<span data-ttu-id="13bbd-223">在 SignalR 1.x 中,跨域請求由單個啟用 CrossDomain 標誌控制。</span><span class="sxs-lookup"><span data-stu-id="13bbd-223">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="13bbd-224">此標誌同時控制 JSONP 和 CORS 請求。</span><span class="sxs-lookup"><span data-stu-id="13bbd-224">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="13bbd-225">為了更靈活,所有 CORS 支援都從 SignalR 的伺服器元件中刪除(如果檢測到瀏覽器支援它,JAVAScript 用戶端仍通常使用 CORS),並且新的 OWIN 中間件已可用於支援這些方案。</span><span class="sxs-lookup"><span data-stu-id="13bbd-225">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="13bbd-226">如果用戶端上需要 JSONP(以支援舊瀏覽器中的跨域請求),則需要通過`EnableJSONP``HubConfiguration`在`true`物件 上設置為 (如下所示)顯式啟用它。</span><span class="sxs-lookup"><span data-stu-id="13bbd-226">If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="13bbd-227">默認情況下禁用 JSONP,因為它的安全性低於 CORS。</span><span class="sxs-lookup"><span data-stu-id="13bbd-227">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="13bbd-228">**將 Microsoft.Owin.Cors 新增到您的專案中:** 要安裝此庫,請在包管理員控制台中執行以下命令:</span><span class="sxs-lookup"><span data-stu-id="13bbd-228">**Adding Microsoft.Owin.Cors to your project:** To install this library, run the following command in the Package Manager Console:</span></span>

`Install-Package Microsoft.Owin.Cors`

<span data-ttu-id="13bbd-229">此命令會將包的 2.1.0 版本添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="13bbd-229">This command will add the 2.1.0 version of the package to your project.</span></span>

### <a name="calling-usecors"></a><span data-ttu-id="13bbd-230">呼叫使用參數</span><span class="sxs-lookup"><span data-stu-id="13bbd-230">Calling UseCors</span></span>

 <span data-ttu-id="13bbd-231">以下代碼段演示如何在 SignalR 2 中實現跨域連接。</span><span class="sxs-lookup"><span data-stu-id="13bbd-231">The following code snippet demonstrates how to implement cross-domain connections in SignalR 2.</span></span>

<span data-ttu-id="13bbd-232">**在 SignalR 2 上實現跨網域要求**</span><span class="sxs-lookup"><span data-stu-id="13bbd-232">**Implementing cross-domain requests in SignalR 2**</span></span>

<span data-ttu-id="13bbd-233">以下代碼展示如何在 SignalR 2 專案中啟用 CORS 或 JSONP。</span><span class="sxs-lookup"><span data-stu-id="13bbd-233">The following code demonstrates how to enable CORS or JSONP in a SignalR 2 project.</span></span> <span data-ttu-id="13bbd-234">此代碼示例使用`Map``RunSignalR``MapSignalR`而不是 ,以便 CORS 中間件僅運行需要 CORS 支援的 SignalR 請求(而不是針對中`MapSignalR`指定的路徑上的所有流量)。映射還可用於需要為特定 URL 首碼運行的任何其他中間件,而不是整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-234">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) Map can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - <span data-ttu-id="13bbd-235">不要在代碼中設置為`jQuery.support.cors`true。</span><span class="sxs-lookup"><span data-stu-id="13bbd-235">Don't set `jQuery.support.cors` to true in your code.</span></span>
>
>     ![不要將 jQuery.support.cors 設定為 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     <span data-ttu-id="13bbd-237">信號R處理CORS的使用。</span><span class="sxs-lookup"><span data-stu-id="13bbd-237">SignalR handles the use of CORS.</span></span> <span data-ttu-id="13bbd-238">設置為`jQuery.support.cors`true 禁用 JSONP,因為它會導致 SignalR 假定瀏覽器支援 CORS。</span><span class="sxs-lookup"><span data-stu-id="13bbd-238">Setting `jQuery.support.cors` to true disables JSONP because it causes SignalR to assume the browser supports CORS.</span></span>
> - <span data-ttu-id="13bbd-239">當您連接到本地主機 URL 時,Internet Explorer 10 不會將其視為跨域連接,因此應用程式將在本地使用 IE 10,即使您未在伺服器上啟用跨域連接也是如此。</span><span class="sxs-lookup"><span data-stu-id="13bbd-239">When you're connecting to a localhost URL, Internet Explorer 10 won't consider it a cross-domain connection, so the application will work locally with IE 10 even if you haven't enabled cross-domain connections on the server.</span></span>
> - <span data-ttu-id="13bbd-240">有關將跨網域連接與 Internet Explorer 9 一起使用的資訊,請參閱[此堆疊溢出線程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-240">For information about using cross-domain connections with Internet Explorer 9, see [this StackOverflow thread](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work).</span></span>
> - <span data-ttu-id="13bbd-241">有關使用 Chrome 跨域連接的資訊,請參閱[此堆疊溢出線程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-241">For information about using cross-domain connections with Chrome, see [this StackOverflow thread](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome).</span></span>
> - <span data-ttu-id="13bbd-242">範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="13bbd-242">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="13bbd-243">有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-243">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="13bbd-244">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="13bbd-244">How to configure the connection</span></span>

<span data-ttu-id="13bbd-245">在建立連接之前,可以指定查詢字串參數或指定傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-245">Before you establish a connection, you can specify query string parameters or specify the transport method.</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="13bbd-246">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="13bbd-246">How to specify query string parameters</span></span>

<span data-ttu-id="13bbd-247">如果要在用戶端連接時將數據發送到伺服器,則可以向連接物件添加查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="13bbd-247">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="13bbd-248">以下範例展示如何在用戶端代碼中設置查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="13bbd-248">The following examples show how to set a query string parameter in client code.</span></span>

<span data-ttu-id="13bbd-249">**在呼叫 start 方法之前設定查詢字串值(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-249">**Set a query string value before calling the start method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

<span data-ttu-id="13bbd-250">**在呼叫 start 方法之前設定查詢字串值(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-250">**Set a query string value before calling the start method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

<span data-ttu-id="13bbd-251">下面的範例展示如何讀取伺服器代碼中的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="13bbd-251">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="13bbd-252">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-252">How to specify the transport method</span></span>

<span data-ttu-id="13bbd-253">作為連接過程的一部分,SignalR 用戶端通常與伺服器協商以確定伺服器和用戶端支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="13bbd-253">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="13bbd-254">如果您已經知道要使用的傳輸,則可以在調用 方法時指定傳輸方法`start`來 繞過此協商過程。</span><span class="sxs-lookup"><span data-stu-id="13bbd-254">If you already know which transport you want to use, you can bypass this negotiation process by specifying the transport method when you call the `start` method.</span></span>

<span data-ttu-id="13bbd-255">**指定傳輸方法的客戶端碼 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-255">**Client code that specifies the transport method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

<span data-ttu-id="13bbd-256">**指定傳輸方法的客戶端代碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-256">**Client code that specifies the transport method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

<span data-ttu-id="13bbd-257">作為替代方法,您可以按希望 SignalR 嘗試它們的順序指定多個傳輸方法:</span><span class="sxs-lookup"><span data-stu-id="13bbd-257">As an alternative, you can specify multiple transport methods in the order in which you want SignalR to try them:</span></span>

<span data-ttu-id="13bbd-258">**指定自訂傳輸回退方案(使用產生的代理)的客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-258">**Client code that specifies a custom transport fallback scheme (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

<span data-ttu-id="13bbd-259">**指定自訂傳輸回退方案的客戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-259">**Client code that specifies a custom transport fallback scheme (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

<span data-ttu-id="13bbd-260">可以使用以下值指定傳輸方法:</span><span class="sxs-lookup"><span data-stu-id="13bbd-260">You can use the following values for specifying the transport method:</span></span>

- <span data-ttu-id="13bbd-261">"網络套接字"</span><span class="sxs-lookup"><span data-stu-id="13bbd-261">"webSockets"</span></span>
- <span data-ttu-id="13bbd-262">"永久框架"</span><span class="sxs-lookup"><span data-stu-id="13bbd-262">"foreverFrame"</span></span>
- <span data-ttu-id="13bbd-263">"伺服器發送事件"</span><span class="sxs-lookup"><span data-stu-id="13bbd-263">"serverSentEvents"</span></span>
- <span data-ttu-id="13bbd-264">"長輪詢"</span><span class="sxs-lookup"><span data-stu-id="13bbd-264">"longPolling"</span></span>

<span data-ttu-id="13bbd-265">以下範例展示如何找出連接正在使用哪種傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-265">The following examples show how to find out which transport method is being used by a connection.</span></span>

<span data-ttu-id="13bbd-266">**顯示連線使用的傳輸方法的客戶端碼(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-266">**Client code that displays the transport method used by a connection (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

<span data-ttu-id="13bbd-267">**顯示連線使用的傳輸方法的客戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-267">**Client code that displays the transport method used by a connection (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

<span data-ttu-id="13bbd-268">有關如何在伺服器代碼中檢查傳輸方法的資訊,請參閱[ASP.NET SignalR 集線器 API 指南 - 伺服器 - 如何從 Context 屬性取得有關用戶端的資訊](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-268">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="13bbd-269">有關傳輸和回退的詳細資訊,請參閱[訊號R - 傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-269">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a><span data-ttu-id="13bbd-270">如何取得中心類的代理</span><span class="sxs-lookup"><span data-stu-id="13bbd-270">How to get a proxy for a Hub class</span></span>

<span data-ttu-id="13bbd-271">您建立的每個連接物件都封裝了有關連接到包含一個或多個集線器類的 SignalR 服務的資訊。</span><span class="sxs-lookup"><span data-stu-id="13bbd-271">Each connection object that you create encapsulates information about a connection to a SignalR service that contains one or more Hub classes.</span></span> <span data-ttu-id="13bbd-272">要與 Hub 類通訊,請使用自己創建的代理物件(如果您不使用生成的代理)或為您生成的代理。</span><span class="sxs-lookup"><span data-stu-id="13bbd-272">To communicate with a Hub class, you use a proxy object which you create yourself (if you're not using the generated proxy) or which is generated for you.</span></span>

<span data-ttu-id="13bbd-273">在用戶端上,代理名稱是集線器類名稱的駱駝大小寫版本。</span><span class="sxs-lookup"><span data-stu-id="13bbd-273">On the client the proxy name is a camel-cased version of the Hub class name.</span></span> <span data-ttu-id="13bbd-274">SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。</span><span class="sxs-lookup"><span data-stu-id="13bbd-274">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="13bbd-275">**伺服器上的集線器類別**</span><span class="sxs-lookup"><span data-stu-id="13bbd-275">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

<span data-ttu-id="13bbd-276">**取得對中心產生的用戶端代理的參考**</span><span class="sxs-lookup"><span data-stu-id="13bbd-276">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

<span data-ttu-id="13bbd-277">**為中心類別建立客戶端代理(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-277">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

<span data-ttu-id="13bbd-278">如果使用`HubName`屬性裝飾 Hub 類,請使用確切名稱而不更改大小寫。</span><span class="sxs-lookup"><span data-stu-id="13bbd-278">If you decorate your Hub class with a `HubName` attribute, use the exact name without changing case.</span></span>

<span data-ttu-id="13bbd-279">**伺服器上具有 HubName 屬性的集線器類別**</span><span class="sxs-lookup"><span data-stu-id="13bbd-279">**Hub class on server with HubName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

<span data-ttu-id="13bbd-280">**取得對中心產生的用戶端代理的參考**</span><span class="sxs-lookup"><span data-stu-id="13bbd-280">**Get a reference to the generated client proxy for the Hub**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

<span data-ttu-id="13bbd-281">**為中心類別建立客戶端代理(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-281">**Create client proxy for the Hub class (without generated proxy)**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="13bbd-282">如何在客戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-282">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="13bbd-283">要定義伺服器可以從集線器呼叫的方法,請使用生成的代理`client`的屬性向中心代理添加事件處理程式,或者如果您不使用生成的代理,`on`則調用方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-283">To define a method that the server can call from a Hub, add an event handler to the Hub proxy by using the `client` property of the generated proxy, or call the `on` method if you aren't using the generated proxy.</span></span> <span data-ttu-id="13bbd-284">參數可以是複雜物件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-284">The parameters can be complex objects.</span></span>

<span data-ttu-id="13bbd-285">在調用 方法以建立連接之前`start`添加 事件處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-285">Add the event handler before you call the `start` method to establish the connection.</span></span> <span data-ttu-id="13bbd-286">(如果要在調用`start`方法後添加事件處理程式,請參閱本文檔前面[如何建立連接](#establishconnection)的說明,並使用顯示的語法來定義方法而不使用生成的代理。</span><span class="sxs-lookup"><span data-stu-id="13bbd-286">(If you want to add event handlers after calling the `start` method, see the note in [How to establish a connection](#establishconnection) earlier in this document, and use the syntax shown for defining a method without using the generated proxy.)</span></span>

<span data-ttu-id="13bbd-287">方法名稱匹配不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="13bbd-287">Method name matching is case-insensitive.</span></span> <span data-ttu-id="13bbd-288">例如,`Clients.All.addContosoChatMessageToPage`在伺服器上將`AddContosoChatMessageToPage`執行`addContosoChatMessageToPage`、`addcontosochatmessagetopage`或在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="13bbd-288">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addContosoChatMessageToPage`, or `addcontosochatmessagetopage` on the client.</span></span>

<span data-ttu-id="13bbd-289">**在用戶端上定義方法 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-289">**Define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

<span data-ttu-id="13bbd-290">**在用戶端上定義方法的替代方法(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-290">**Alternate way to define method on client (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

<span data-ttu-id="13bbd-291">**在用戶端上定義方法(沒有產生的代理,或在呼叫 start 方法後新增時)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-291">**Define method on client (without the generated proxy, or when adding after calling the start method)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

<span data-ttu-id="13bbd-292">**呼叫用戶端方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-292">**Server code that calls the client method**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

<span data-ttu-id="13bbd-293">以下範例包括作為方法參數的複雜物件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-293">The following examples include a complex object as a method parameter.</span></span>

<span data-ttu-id="13bbd-294">**在用戶端上定義採用複雜物件的方法(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-294">**Define method on client that takes a complex object (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

<span data-ttu-id="13bbd-295">**在用戶端上定義採用複雜物件的方法(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-295">**Define method on client that takes a complex object (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

<span data-ttu-id="13bbd-296">**定義複雜物件的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-296">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

<span data-ttu-id="13bbd-297">**使用複雜物件呼叫用戶端方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-297">**Server code that calls the client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="13bbd-298">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="13bbd-298">How to call server methods from the client</span></span>

<span data-ttu-id="13bbd-299">要從用戶端呼叫伺服器方法,請使用生成的代理`server`的屬性或 Hub`invoke`代理上的方法(如果您不使用生成的代理)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-299">To call a server method from the client, use the `server` property of the generated proxy or the `invoke` method on the Hub proxy if you aren't using the generated proxy.</span></span> <span data-ttu-id="13bbd-300">返回值或參數可以是複雜物件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-300">The return value or parameters can be complex objects.</span></span>

<span data-ttu-id="13bbd-301">在集線器上傳遞方法名稱的駱駝大小寫版本。</span><span class="sxs-lookup"><span data-stu-id="13bbd-301">Pass in a camel-case version of the method name on the Hub.</span></span> <span data-ttu-id="13bbd-302">SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。</span><span class="sxs-lookup"><span data-stu-id="13bbd-302">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="13bbd-303">以下範例展示如何呼叫沒有返回值的伺服器方法以及如何調用具有返回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-303">The following examples show how to call a server method that doesn't have a return value and how to call a server method that does have a return value.</span></span>

<span data-ttu-id="13bbd-304">**沒有 HubMethodName 屬性的伺服器方法**</span><span class="sxs-lookup"><span data-stu-id="13bbd-304">**Server method with no HubMethodName attribute**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

<span data-ttu-id="13bbd-305">**定義參數中傳遞的複雜物件的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-305">**Server code that defines the complex object passed in a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

<span data-ttu-id="13bbd-306">**呼叫伺服器方法的客戶端碼 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-306">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

<span data-ttu-id="13bbd-307">**呼叫伺服器方法的客戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-307">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

<span data-ttu-id="13bbd-308">如果使用`HubMethodName`屬性修飾 Hub 方法,請使用該名稱而不更改大小寫。</span><span class="sxs-lookup"><span data-stu-id="13bbd-308">If you decorated the Hub method with a `HubMethodName` attribute, use that name without changing case.</span></span>

<span data-ttu-id="13bbd-309">具有 HubMethodName 屬性的**伺服器方法**</span><span class="sxs-lookup"><span data-stu-id="13bbd-309">**Server method** with a HubMethodName attribute</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

<span data-ttu-id="13bbd-310">**呼叫伺服器方法的客戶端碼 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-310">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

<span data-ttu-id="13bbd-311">**呼叫伺服器方法的客戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-311">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

<span data-ttu-id="13bbd-312">前面的範例展示如何調用沒有返回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-312">The preceding examples show how to call a server method that has no return value.</span></span> <span data-ttu-id="13bbd-313">以下範例簡報如何調用具有返回值的伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="13bbd-313">The following examples show how to call a server method that has a return value.</span></span>

<span data-ttu-id="13bbd-314">**具有傳回值的方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="13bbd-314">**Server code for a method that has a return value**</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

<span data-ttu-id="13bbd-315">**回報**值的 Stock 類別</span><span class="sxs-lookup"><span data-stu-id="13bbd-315">**The Stock class used for the** return value</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

<span data-ttu-id="13bbd-316">**呼叫伺服器方法的客戶端碼 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-316">**Client code that invokes the server method (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

<span data-ttu-id="13bbd-317">**呼叫伺服器方法的客戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-317">**Client code that invokes the server method (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="13bbd-318">如何處理連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="13bbd-318">How to handle connection lifetime events</span></span>

<span data-ttu-id="13bbd-319">SignalR 提供您可以處理的以下連線存留期事件:</span><span class="sxs-lookup"><span data-stu-id="13bbd-319">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="13bbd-320">`starting`:在通過連接發送任何數據之前引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-320">`starting`: Raised before any data is sent over the connection.</span></span>
- <span data-ttu-id="13bbd-321">`received`:在連接上收到任何數據時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-321">`received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="13bbd-322">提供接收的數據。</span><span class="sxs-lookup"><span data-stu-id="13bbd-322">Provides the received data.</span></span>
- <span data-ttu-id="13bbd-323">`connectionSlow`:當客戶端檢測到連接緩慢或頻繁斷開時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-323">`connectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="13bbd-324">`reconnecting`:當基礎傳輸開始重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-324">`reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="13bbd-325">`reconnected`:在基礎傳輸重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-325">`reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="13bbd-326">`stateChanged`:當連接狀態更改時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-326">`stateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="13bbd-327">提供舊狀態和新狀態(連接、連接、重新連接或斷開連接)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-327">Provides the old state and the new state (Connecting, Connected, Reconnecting, or Disconnected).</span></span>
- <span data-ttu-id="13bbd-328">`disconnected`:連接斷開連接時引發。</span><span class="sxs-lookup"><span data-stu-id="13bbd-328">`disconnected`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="13bbd-329">例如,如果要在連接問題可能導致明顯延遲時顯示警告消息,則處理該`connectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="13bbd-329">For example, if you want to display warning messages when there are connection problems that might cause noticeable delays, handle the `connectionSlow` event.</span></span>

<span data-ttu-id="13bbd-330">**處理連線速度事件(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-330">**Handle the connectionSlow event (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

<span data-ttu-id="13bbd-331">**處理連線速度慢事件(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-331">**Handle the connectionSlow event (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

<span data-ttu-id="13bbd-332">有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-332">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="13bbd-333">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="13bbd-333">How to handle errors</span></span>

<span data-ttu-id="13bbd-334">SignalR JavaScript`error`用戶端提供一個事件,您可以為其添加處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-334">The SignalR JavaScript client provides an `error` event that you can add a handler for.</span></span> <span data-ttu-id="13bbd-335">您還可以使用 fail 方法為伺服器方法呼叫導致的錯誤添加處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-335">You can also use the fail method to add a handler for errors that result from a server method invocation.</span></span>

<span data-ttu-id="13bbd-336">如果未在伺服器上顯式啟用詳細的錯誤消息,則 SignalR 在錯誤後返回的異常物件包含有關該錯誤的最少資訊。</span><span class="sxs-lookup"><span data-stu-id="13bbd-336">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="13bbd-337">例如,如果調用`newContosoChatMessage`失敗,錯誤物件中的錯誤消息包含`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`「 出於安全原因不建議向生產中的客戶端發送詳細的錯誤訊息,但如果要啟用詳細的錯誤訊息以進行故障排除,請使用伺服器上的以下代碼。</span><span class="sxs-lookup"><span data-stu-id="13bbd-337">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

<span data-ttu-id="13bbd-338">下面的範例展示如何為錯誤事件添加處理程式。</span><span class="sxs-lookup"><span data-stu-id="13bbd-338">The following example shows how to add a handler for the error event.</span></span>

<span data-ttu-id="13bbd-339">**新增錯誤處理程式 (使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-339">**Add an error handler (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

<span data-ttu-id="13bbd-340">**新增錯誤處理程式 (沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-340">**Add an error handler (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

<span data-ttu-id="13bbd-341">下面的範例演示如何處理方法調用中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="13bbd-341">The following example shows how to handle an error from a method invocation.</span></span>

<span data-ttu-id="13bbd-342">**處理方法呼叫中的錯誤(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-342">**Handle an error from a method invocation (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

<span data-ttu-id="13bbd-343">**處理方法呼叫中的錯誤(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-343">**Handle an error from a method invocation (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

<span data-ttu-id="13bbd-344">如果方法調用失敗,也會引發`error`該事件,`error`因此方法處理程式中的`.fail`代碼和方法回調中的代碼將執行。</span><span class="sxs-lookup"><span data-stu-id="13bbd-344">If a method invocation fails, the `error` event is also raised, so your code in the `error` method handler and in the `.fail` method callback would execute.</span></span>

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="13bbd-345">如何開啟客戶端記錄記錄</span><span class="sxs-lookup"><span data-stu-id="13bbd-345">How to enable client-side logging</span></span>

<span data-ttu-id="13bbd-346">要在連接上啟用客戶端日誌記錄,在調`logging``start`用 方法建立連接之前,在連接對象上設置屬性。</span><span class="sxs-lookup"><span data-stu-id="13bbd-346">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="13bbd-347">**開啟紀錄紀錄(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-347">**Enable logging (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

<span data-ttu-id="13bbd-348">**開啟紀錄紀錄(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="13bbd-348">**Enable logging (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

<span data-ttu-id="13bbd-349">要查看日誌,請打開瀏覽器的開發人員工具,然後轉到"控制台"選項卡。有關顯示分步說明並顯示如何執行此動作的螢幕擷取的教學,請參考[ASP.NET 訊號器的伺服器廣播 - 啟用紀錄紀錄](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。</span><span class="sxs-lookup"><span data-stu-id="13bbd-349">To see the logs, open your browser's developer tools and go to the Console tab. For a tutorial that shows step-by-step instructions and screen shots that show how to do this, see [Server Broadcast with ASP.NET Signalr - Enable Logging](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging).</span></span>
