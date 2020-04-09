---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET信號器集線器 API 指南 - 伺服器 (C#) |微軟文件
author: bradygaster
description: 此文件介紹了為 SignalR 版本 2 編寫ASP.NET訊號R 集線器 API 的伺服器端,並演示了代碼範例...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676185"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="0c99d-103">ASP.NET訊號器集線器 API 指南 - 伺服器 (C#)</span><span class="sxs-lookup"><span data-stu-id="0c99d-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="0c99d-104">由[派翠克·弗萊徹](https://github.com/pfletcher),[湯姆·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0c99d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="0c99d-105">本文件介紹了為 SignalR 版本 2 編寫ASP.NET訊號R 集線器 API 的伺服器端,並演示了常見選項的代碼示例。</span><span class="sxs-lookup"><span data-stu-id="0c99d-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="0c99d-106">SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="0c99d-107">在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="0c99d-108">在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="0c99d-109">SignalR 為您處理所有用戶端到伺服器管道。</span><span class="sxs-lookup"><span data-stu-id="0c99d-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="0c99d-110">SignalR 還提供稱為持久連接的較低級別的 API。</span><span class="sxs-lookup"><span data-stu-id="0c99d-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="0c99d-111">有關信號R、集線器和持久連接的介紹,請參閱[訊號R 2 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="0c99d-112">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="0c99d-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="0c99d-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="0c99d-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="0c99d-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="0c99d-114">.NET 4.5</span></span>
> - <span data-ttu-id="0c99d-115">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="0c99d-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="0c99d-116">主題版本</span><span class="sxs-lookup"><span data-stu-id="0c99d-116">Topic versions</span></span>
> 
> <span data-ttu-id="0c99d-117">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="0c99d-118">問題和評論</span><span class="sxs-lookup"><span data-stu-id="0c99d-118">Questions and comments</span></span>
> 
> <span data-ttu-id="0c99d-119">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="0c99d-120">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="0c99d-121">概觀</span><span class="sxs-lookup"><span data-stu-id="0c99d-121">Overview</span></span>

<span data-ttu-id="0c99d-122">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="0c99d-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="0c99d-123">如何註冊SignalR中間件</span><span class="sxs-lookup"><span data-stu-id="0c99d-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="0c99d-124">/信號器網址</span><span class="sxs-lookup"><span data-stu-id="0c99d-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="0c99d-125">設定訊號</span><span class="sxs-lookup"><span data-stu-id="0c99d-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="0c99d-126">如何建立與使用中心類別</span><span class="sxs-lookup"><span data-stu-id="0c99d-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="0c99d-127">中心物件存留期</span><span class="sxs-lookup"><span data-stu-id="0c99d-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="0c99d-128">JavaScript 用戶端中中心名稱的駱駝大小寫</span><span class="sxs-lookup"><span data-stu-id="0c99d-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="0c99d-129">多個中心</span><span class="sxs-lookup"><span data-stu-id="0c99d-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="0c99d-130">強類型集線器</span><span class="sxs-lookup"><span data-stu-id="0c99d-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="0c99d-131">如何在中心類別定義客戶端可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="0c99d-132">JavaScript 用戶端中方法名稱的駱駝大小寫</span><span class="sxs-lookup"><span data-stu-id="0c99d-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="0c99d-133">何時同步執行</span><span class="sxs-lookup"><span data-stu-id="0c99d-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="0c99d-134">定義重載</span><span class="sxs-lookup"><span data-stu-id="0c99d-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="0c99d-135">報告中心方法呼叫進度</span><span class="sxs-lookup"><span data-stu-id="0c99d-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="0c99d-136">如何從中心類調用用戶端方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="0c99d-137">選擇哪些用戶端將收到 RPC</span><span class="sxs-lookup"><span data-stu-id="0c99d-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="0c99d-138">方法名稱沒有編譯時間驗證</span><span class="sxs-lookup"><span data-stu-id="0c99d-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="0c99d-139">區分大小寫的方法名稱符合</span><span class="sxs-lookup"><span data-stu-id="0c99d-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="0c99d-140">非同步執行</span><span class="sxs-lookup"><span data-stu-id="0c99d-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="0c99d-141">如何從中心類管理組成員身份</span><span class="sxs-lookup"><span data-stu-id="0c99d-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="0c99d-142">新增與移除方法的非同步</span><span class="sxs-lookup"><span data-stu-id="0c99d-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="0c99d-143">群組成員身份持久性</span><span class="sxs-lookup"><span data-stu-id="0c99d-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="0c99d-144">單使用者群組</span><span class="sxs-lookup"><span data-stu-id="0c99d-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="0c99d-145">如何處理集線器類別的連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="0c99d-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="0c99d-146">當"連接"時,打開斷開狀態,並調用"重新連接"</span><span class="sxs-lookup"><span data-stu-id="0c99d-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="0c99d-147">未填滿的呼叫者狀態</span><span class="sxs-lookup"><span data-stu-id="0c99d-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="0c99d-148">如何從內容取得有關用戶端的資訊</span><span class="sxs-lookup"><span data-stu-id="0c99d-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="0c99d-149">如何在用戶端和中心類之間傳遞狀態</span><span class="sxs-lookup"><span data-stu-id="0c99d-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="0c99d-150">如何處理中心類別的錯誤</span><span class="sxs-lookup"><span data-stu-id="0c99d-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="0c99d-151">如何呼叫用戶端方法並管理來自中心類外部的群組</span><span class="sxs-lookup"><span data-stu-id="0c99d-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="0c99d-152">呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="0c99d-153">管理群組成員身份</span><span class="sxs-lookup"><span data-stu-id="0c99d-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="0c99d-154">如何開啟追蹤</span><span class="sxs-lookup"><span data-stu-id="0c99d-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="0c99d-155">如何自訂中心管道</span><span class="sxs-lookup"><span data-stu-id="0c99d-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="0c99d-156">有關如何對客戶端進行程式設計的文件,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="0c99d-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="0c99d-157">信號器中心 API 指南 - JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="0c99d-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="0c99d-158">信號器集線器 API 指南 - .NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="0c99d-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="0c99d-159">SignalR 2 的伺服器元件僅在 .NET 4.5 中可用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="0c99d-160">運行 .NET 4.0 的伺服器必須使用 SignalR v1.x。</span><span class="sxs-lookup"><span data-stu-id="0c99d-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="0c99d-161">如何註冊SignalR中間件</span><span class="sxs-lookup"><span data-stu-id="0c99d-161">How to register SignalR middleware</span></span>

<span data-ttu-id="0c99d-162">要定義用戶端將用於連接到集線器的路由,請在`MapSignalR`應用程式啟動時調用方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="0c99d-163">`MapSignalR`是類別的`OwinExtensions`[擴充方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="0c99d-164">下面的範例展示如何使用OWIN啟動類定義SignalR中心路由。</span><span class="sxs-lookup"><span data-stu-id="0c99d-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="0c99d-165">如果要將 SignalR 功能添加到 ASP.NET MVC 應用程式,請確保在其他路由之前添加 SignalR 路由。</span><span class="sxs-lookup"><span data-stu-id="0c99d-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="0c99d-166">有關詳細資訊,請參閱[教程:開始使用 SignalR 2 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="0c99d-167">/信號器網址</span><span class="sxs-lookup"><span data-stu-id="0c99d-167">The /signalr URL</span></span>

<span data-ttu-id="0c99d-168">默認情況下,用戶端將用於連接到集線器的路由網址為"/信號器"。</span><span class="sxs-lookup"><span data-stu-id="0c99d-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="0c99d-169">(不要將此網址與"/信號器/集線器"URL 混淆,該 URL 適用於自動生成的 JAVAScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c99d-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="0c99d-170">有關產生的代理的詳細資訊,請參閱[SignalR 中心 API 指南 - JAvaScript 用戶端 - 產生的代理及其為您做什麼](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="0c99d-171">可能存在異常情況,使此基 URL 不適用於 SignalR;例如,專案中有一個名為*信號器*的資料夾,並且不想更改名稱。</span><span class="sxs-lookup"><span data-stu-id="0c99d-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="0c99d-172">在這種情況下,您可以更改基本 URL,如以下範例所示(將範例代碼中的"/信號器"替換為所需的 URL)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="0c99d-173">**指定網址的伺服器碼**</span><span class="sxs-lookup"><span data-stu-id="0c99d-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="0c99d-174">**指定網址的 JavaScript 用戶端碼(使用產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="0c99d-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="0c99d-175">**指定網址的 JavaScript 用戶端碼(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="0c99d-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="0c99d-176">**指定 URL 的 .NET 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="0c99d-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="0c99d-177">設定訊號設定選項</span><span class="sxs-lookup"><span data-stu-id="0c99d-177">Configuring SignalR Options</span></span>

<span data-ttu-id="0c99d-178">`MapSignalR`方法的重載讓您能夠指定自訂網址、自訂依賴項解析器以及以下選項:</span><span class="sxs-lookup"><span data-stu-id="0c99d-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="0c99d-179">使用瀏覽器用戶端的 CORS 或 JSONP 啟用跨域調用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="0c99d-180">通常,如果瀏覽器從`http://contoso.com`載入頁面,則 SignalR 連接位於同一`http://contoso.com/signalr`域中 ,在 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="0c99d-181">如果中的`http://contoso.com`頁面與`http://fabrikam.com/signalr`斷開連接,則為跨域連接。</span><span class="sxs-lookup"><span data-stu-id="0c99d-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="0c99d-182">出於安全原因,默認情況下禁用跨域連接。</span><span class="sxs-lookup"><span data-stu-id="0c99d-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="0c99d-183">有關詳細資訊,請參閱[ASP.NET 訊號R中心 API 指南 - JAvaScript 用戶端 - 如何建立跨網域連接](hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="0c99d-184">啟用詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="0c99d-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="0c99d-185">發生錯誤時,SignalR 的默認行為是向用戶端發送通知消息,而不詳細說明發生的情況。</span><span class="sxs-lookup"><span data-stu-id="0c99d-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="0c99d-186">在生產中不建議向用戶端發送詳細的錯誤資訊,因為惡意使用者可能能夠在針對應用程式的攻擊中使用該資訊。</span><span class="sxs-lookup"><span data-stu-id="0c99d-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="0c99d-187">對於故障排除,可以使用此選項暫時啟用資訊量更大的錯誤報告。</span><span class="sxs-lookup"><span data-stu-id="0c99d-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="0c99d-188">關閉自動產生的 JavaScript 代理檔。</span><span class="sxs-lookup"><span data-stu-id="0c99d-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="0c99d-189">默認情況下,將生成具有中心類代理的 JavaScript 檔,以回應 URL"/信號器/集線器"。</span><span class="sxs-lookup"><span data-stu-id="0c99d-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="0c99d-190">如果不想使用 JavaScript 代理,或者要手動生成此檔並引用用戶端中的物理檔案,則可以使用此選項禁用代理生成。</span><span class="sxs-lookup"><span data-stu-id="0c99d-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="0c99d-191">有關詳細資訊,請參閱[SignalR 中心 API 指南 - JavaScript 用戶端 - 如何為 SignalR 產生的代理產生實體檔](hubs-api-guide-javascript-client.md#manualproxy)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="0c99d-192">下面的範例展示如何在調用`MapSignalR`方法中指定 SignalR 連接 URL 和這些選項。</span><span class="sxs-lookup"><span data-stu-id="0c99d-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="0c99d-193">要指定自定義 URL,請將範例中的"/信號器" 取代為要使用的網址。</span><span class="sxs-lookup"><span data-stu-id="0c99d-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="0c99d-194">如何建立與使用中心類別</span><span class="sxs-lookup"><span data-stu-id="0c99d-194">How to create and use Hub classes</span></span>

<span data-ttu-id="0c99d-195">要建立集線器,請創建一個派生自[Microsoft 的類。](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="0c99d-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="0c99d-196">下面的示例顯示了聊天應用程式的簡單中心類。</span><span class="sxs-lookup"><span data-stu-id="0c99d-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="0c99d-197">在此示例中,連接的用戶端可以調用`NewContosoChatMessage`方法,當它調用時,接收的數據將廣播到所有連接的用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="0c99d-198">中心物件存留期</span><span class="sxs-lookup"><span data-stu-id="0c99d-198">Hub object lifetime</span></span>

<span data-ttu-id="0c99d-199">您不會實例化 Hub 類,也不會從伺服器上自己的代碼調用其方法;否則,您就不會實例化 Hub 類,所有由 SignalR 中心管道為您完成。</span><span class="sxs-lookup"><span data-stu-id="0c99d-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="0c99d-200">SignalR 在每次需要處理集線器操作(例如用戶端連接、斷開連接或對伺服器進行方法調用時)時,都會創建 Hub 類的新實例。</span><span class="sxs-lookup"><span data-stu-id="0c99d-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="0c99d-201">由於 Hub 類的實例是暫時性的,因此不能使用它們來維護從一個方法調用到下一個方法的狀態。</span><span class="sxs-lookup"><span data-stu-id="0c99d-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="0c99d-202">每次伺服器收到來自用戶端的方法調用時,Hub 類的新實例都會處理該消息。</span><span class="sxs-lookup"><span data-stu-id="0c99d-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="0c99d-203">要通過多個連接和方法調用維護狀態,請使用其他方法,如資料庫或 Hub 類上的靜態變數,或者不派生`Hub`自的不同類。</span><span class="sxs-lookup"><span data-stu-id="0c99d-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="0c99d-204">如果在記憶體中保留數據,使用 Hub 類上靜態變數等方法,則當應用域回收時,數據將丟失。</span><span class="sxs-lookup"><span data-stu-id="0c99d-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="0c99d-205">如果要從在 Hub 類之外運行的您自己的代碼向用戶端發送消息,不能通過實例化 Hub 類實例來執行此操作,但可以通過獲取對 Hub 類的 SignalR 上下文物件的引用來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="0c99d-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="0c99d-206">有關詳細資訊,請參閱本主題稍後在[中心類外部呼叫用戶端方法和管理組](#callfromoutsidehub)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="0c99d-207">JavaScript 用戶端中中心名稱的駱駝大小寫</span><span class="sxs-lookup"><span data-stu-id="0c99d-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="0c99d-208">默認情況下,JavaScript 用戶端使用類名稱的駱駝大小寫版本引用集線器。</span><span class="sxs-lookup"><span data-stu-id="0c99d-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="0c99d-209">SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。</span><span class="sxs-lookup"><span data-stu-id="0c99d-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="0c99d-210">前面的範例將稱為`contosoChatHub`JavaScript 代碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="0c99d-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="0c99d-212">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="0c99d-213">如果要為用戶端指定要使用的其他名稱,請添加該`HubName`屬性。</span><span class="sxs-lookup"><span data-stu-id="0c99d-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="0c99d-214">使用`HubName`屬性時,JAVAScript 用戶端上不會更改駱駝大小寫的名稱。</span><span class="sxs-lookup"><span data-stu-id="0c99d-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="0c99d-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="0c99d-216">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="0c99d-217">多個中心</span><span class="sxs-lookup"><span data-stu-id="0c99d-217">Multiple Hubs</span></span>

<span data-ttu-id="0c99d-218">您可以在應用程式中定義多個中心類。</span><span class="sxs-lookup"><span data-stu-id="0c99d-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="0c99d-219">執行此操作時,連線是共用的,但組是獨立的:</span><span class="sxs-lookup"><span data-stu-id="0c99d-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="0c99d-220">所有用戶端都將使用相同的 URL 與服務建立 SignalR 連接("/信號器" 或自訂網址(如果您指定了一個),並且該連接用於服務定義的所有中心。</span><span class="sxs-lookup"><span data-stu-id="0c99d-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="0c99d-221">與在單個類中定義所有中心功能相比,多個中心的性能差異沒有差異。</span><span class="sxs-lookup"><span data-stu-id="0c99d-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="0c99d-222">所有中心都獲取相同的 HTTP 請求資訊。</span><span class="sxs-lookup"><span data-stu-id="0c99d-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="0c99d-223">由於所有集線器共用相同的連接,因此伺服器獲得的唯一 HTTP 請求資訊是建立 SignalR 連接的原始 HTTP 請求中的內容。</span><span class="sxs-lookup"><span data-stu-id="0c99d-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="0c99d-224">如果使用連線請求透過指定查詢字串將資訊從客戶端傳遞到伺服器,則不能向不同的中心提供不同的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="0c99d-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="0c99d-225">所有中心都將收到相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="0c99d-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="0c99d-226">生成的 JavaScript 代理檔將包含一個檔中所有中心代理。</span><span class="sxs-lookup"><span data-stu-id="0c99d-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="0c99d-227">有關 JavaScript 代理的資訊,請參閱[SignalR 中心 API 指南 - JavaScript 客戶端 - 產生的代理及其為您做什麼](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="0c99d-228">組在中心內定義。</span><span class="sxs-lookup"><span data-stu-id="0c99d-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="0c99d-229">在 SignalR 中,您可以定義要廣播到連接用戶端子集的命名組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="0c99d-230">每個中心分別維護組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="0c99d-231">例如,名為「管理員」的組將包含類`ContosoChatHub`的一組用戶端,而相同的組名稱將引用`StockTickerHub`類的不同用戶端集。</span><span class="sxs-lookup"><span data-stu-id="0c99d-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="0c99d-232">強類型集線器</span><span class="sxs-lookup"><span data-stu-id="0c99d-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="0c99d-233">要為用戶端可以引用的集線器方法定義介面(並在集線器方法上啟用 Intellisense),請`Hub<T>`從 (在 SignalR`Hub`2.1 中 引入) 而不是 派生中心。</span><span class="sxs-lookup"><span data-stu-id="0c99d-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="0c99d-234">如何在中心類別定義客戶端可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="0c99d-235">要在 Hub 上公開要從用戶端調用的方法,請聲明公共方法,如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="0c99d-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="0c99d-236">您可以指定返回類型和參數,包括複雜類型和陣列,就像在任何 C# 方法中一樣。</span><span class="sxs-lookup"><span data-stu-id="0c99d-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="0c99d-237">使用 JSON 在用戶端和伺服器之間通訊以參數接收或返回到調用方的任何數據,SignalR 會自動處理複雜物件和物件數組的綁定。</span><span class="sxs-lookup"><span data-stu-id="0c99d-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="0c99d-238">JavaScript 用戶端中方法名稱的駱駝大小寫</span><span class="sxs-lookup"><span data-stu-id="0c99d-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="0c99d-239">默認情況下,JavaScript 用戶端使用方法名稱的駱駝大小寫版本引用 Hub 方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="0c99d-240">SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。</span><span class="sxs-lookup"><span data-stu-id="0c99d-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="0c99d-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="0c99d-242">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="0c99d-243">如果要為用戶端指定要使用的其他名稱,請添加該`HubMethodName`屬性。</span><span class="sxs-lookup"><span data-stu-id="0c99d-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="0c99d-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="0c99d-245">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="0c99d-246">何時同步執行</span><span class="sxs-lookup"><span data-stu-id="0c99d-246">When to execute asynchronously</span></span>

<span data-ttu-id="0c99d-247">如果該方法將長時間運行或必須執行需要等待的工作(如資料庫查找或 Web 服務呼叫),則[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)透過傳回`void`任務 (代替返回)或[Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx)物件(代替`T`返回類型)使 Hub 方法非同步。</span><span class="sxs-lookup"><span data-stu-id="0c99d-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="0c99d-248">當您從方法`Task`返回物件時,SignalR 會`Task`等待 完成,然後它將未包裝的結果發送回用戶端,因此在用戶端中編寫方法調用的代碼沒有區別。</span><span class="sxs-lookup"><span data-stu-id="0c99d-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="0c99d-249">使集線器方法非同步可避免使用 WebSocket 傳輸時阻塞連接。</span><span class="sxs-lookup"><span data-stu-id="0c99d-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="0c99d-250">當集線器方法同步執行且傳輸為 WebSocket 時,從同一用戶端在集線器上調用方法將被阻止,直到中心方法完成。</span><span class="sxs-lookup"><span data-stu-id="0c99d-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="0c99d-251">下面的範例顯示編碼為同步或非同步執行的相同方法,然後是適用於調用任一版本的 JavaScript 客戶端碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="0c99d-252">**同步**</span><span class="sxs-lookup"><span data-stu-id="0c99d-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="0c99d-253">**非同步**</span><span class="sxs-lookup"><span data-stu-id="0c99d-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="0c99d-254">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="0c99d-255">有關如何在 ASP.NET 4.5 中使用非同步方法的詳細資訊,請參閱[在 mVC 4 中使用非同步方法 ASP.NET](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="0c99d-256">定義重載</span><span class="sxs-lookup"><span data-stu-id="0c99d-256">Defining Overloads</span></span>

<span data-ttu-id="0c99d-257">如果要為方法定義重載,則每個重載中的參數數必須不同。</span><span class="sxs-lookup"><span data-stu-id="0c99d-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="0c99d-258">如果僅通過指定不同的參數類型來區分重載,則 Hub 類將編譯,但當客戶端嘗試調用其中一個重載時,SignalR 服務將在運行時引發異常。</span><span class="sxs-lookup"><span data-stu-id="0c99d-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="0c99d-259">報告中心方法呼叫進度</span><span class="sxs-lookup"><span data-stu-id="0c99d-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="0c99d-260">SignalR 2.1 添加了對 .NET 4.5 中引入[的進度報告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)的支援。</span><span class="sxs-lookup"><span data-stu-id="0c99d-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="0c99d-261">要實現進度報告,請為`IProgress<T>`用戶端可以存取的集線器方法定義參數:</span><span class="sxs-lookup"><span data-stu-id="0c99d-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="0c99d-262">編寫長時間運行的伺服器方法時,使用非同步程式設計模式(如 Async/Await)而不是阻止中心線程非常重要。</span><span class="sxs-lookup"><span data-stu-id="0c99d-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="0c99d-263">如何從中心類調用用戶端方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="0c99d-264">要從伺服器呼叫用戶端方法,`Clients`請使用 Hub 類中方法中的 屬性。</span><span class="sxs-lookup"><span data-stu-id="0c99d-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="0c99d-265">下面的範例顯示呼叫`addNewMessageToPage`所有連接的用戶端的伺服器代碼,以及定義 JavaScript 用戶端中方法的用戶端代碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="0c99d-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="0c99d-267">呼叫客戶端方法是非同步操作,並傳`Task`回 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="0c99d-268">使用`await`:</span><span class="sxs-lookup"><span data-stu-id="0c99d-268">Use `await`:</span></span>

* <span data-ttu-id="0c99d-269">確保消息發送時沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c99d-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="0c99d-270">啟用在嘗試捕獲塊中捕獲和處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c99d-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="0c99d-271">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="0c99d-272">無法從用戶端方法獲取返回值;因此,無法從用戶端方法獲取返回值。語法,如`int x = Clients.All.add(1,1)`不工作。</span><span class="sxs-lookup"><span data-stu-id="0c99d-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="0c99d-273">您可以為參數指定複雜的類型和陣列。</span><span class="sxs-lookup"><span data-stu-id="0c99d-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="0c99d-274">下面的示例將複雜類型傳遞給方法參數中的用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="0c99d-275">**使用複雜物件呼叫用戶端方法的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="0c99d-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="0c99d-276">**定義複雜物件的伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="0c99d-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="0c99d-277">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="0c99d-278">選擇哪些用戶端將收到 RPC</span><span class="sxs-lookup"><span data-stu-id="0c99d-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="0c99d-279">用戶端屬性傳回[HubConnectionConnection 物件](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx),該物件提供了多個選項來指定哪些用戶端將接收 RPC:</span><span class="sxs-lookup"><span data-stu-id="0c99d-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="0c99d-280">所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="0c99d-281">僅調用用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="0c99d-282">除調用用戶端之外的所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="0c99d-283">由連接 ID 標識的特定用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="0c99d-284">此示例調用`addContosoChatMessageToPage`調用客戶端,並且`Clients.Caller`與使用具有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="0c99d-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="0c99d-285">除指定客戶端外的所有連接用戶端,由連接 ID 標識。</span><span class="sxs-lookup"><span data-stu-id="0c99d-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="0c99d-286">指定組中的所有連接用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="0c99d-287">指定群組中的所有連接客戶端(指定用戶端除外),由連接 ID 識別。</span><span class="sxs-lookup"><span data-stu-id="0c99d-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="0c99d-288">指定群組中的所有已連接客戶端(呼叫用戶端除外)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="0c99d-289">使用者 Id 識別的特定使用者。</span><span class="sxs-lookup"><span data-stu-id="0c99d-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="0c99d-290">默認情況下,這是`IPrincipal.Identity.Name`,但可以通過[向全域主機註冊 IUserIdProvider 的實現](mapping-users-to-connections.md#IUserIdProvider)來更改。</span><span class="sxs-lookup"><span data-stu-id="0c99d-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="0c99d-291">連接指示清單中的所有用戶端和組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="0c99d-292">組的清單。</span><span class="sxs-lookup"><span data-stu-id="0c99d-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="0c99d-293">按名稱命名的使用者。</span><span class="sxs-lookup"><span data-stu-id="0c99d-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="0c99d-294">使用者名清單(在 SignalR 2.1 中介紹)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="0c99d-295">方法名稱沒有編譯時間驗證</span><span class="sxs-lookup"><span data-stu-id="0c99d-295">No compile-time validation for method names</span></span>

<span data-ttu-id="0c99d-296">您指定的方法名稱被解釋為動態物件,這意味著沒有 IntelliSense 或編譯時間驗證。</span><span class="sxs-lookup"><span data-stu-id="0c99d-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="0c99d-297">表達式在運行時計算。</span><span class="sxs-lookup"><span data-stu-id="0c99d-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="0c99d-298">當方法調用執行時,SignalR 會將方法名稱和參數值發送到用戶端,如果用戶端具有與該名稱匹配的方法,則調用該方法並將參數值傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="0c99d-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="0c99d-299">如果在用戶端上找不到匹配方法,則不引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c99d-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="0c99d-300">有關 SignalR 呼叫客戶端方法時在後台傳輸到客戶端的資料格式的資訊,請參閱[SignalR 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="0c99d-301">區分大小寫的方法名稱符合</span><span class="sxs-lookup"><span data-stu-id="0c99d-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="0c99d-302">方法名稱匹配不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="0c99d-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="0c99d-303">例如,`Clients.All.addContosoChatMessageToPage`在伺服器上將`AddContosoChatMessageToPage`執行`addcontosochatmessagetopage`、`addContosoChatMessageToPage`或在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="0c99d-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="0c99d-304">非同步執行</span><span class="sxs-lookup"><span data-stu-id="0c99d-304">Asynchronous execution</span></span>

<span data-ttu-id="0c99d-305">調用的方法以異步方式執行。</span><span class="sxs-lookup"><span data-stu-id="0c99d-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="0c99d-306">對用戶端進行方法調用後出現的任何代碼將立即執行,而無需等待 SignalR 完成向用戶端傳輸數據,除非您指定後續代碼行應等待方法完成。</span><span class="sxs-lookup"><span data-stu-id="0c99d-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="0c99d-307">下面的代碼示例演示如何按順序執行兩個用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="0c99d-308">**使用 Await (.NET 4.5)**</span><span class="sxs-lookup"><span data-stu-id="0c99d-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="0c99d-309">如果使用等待`await`用戶端方法在下一行代碼執行之前完成,這並不意味著用戶端將在執行下一行代碼之前實際收到消息。</span><span class="sxs-lookup"><span data-stu-id="0c99d-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="0c99d-310">用戶端方法呼叫的「完成」僅意味著 SignalR 已執行發送消息所需的一切。</span><span class="sxs-lookup"><span data-stu-id="0c99d-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="0c99d-311">如果您需要驗證用戶端是否收到該消息,您必須自己對該機制進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="0c99d-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="0c99d-312">例如,您可以在 Hub`MessageReceived`上 編寫方法代碼,`addContosoChatMessageToPage`在用戶端上 編寫方法後,您可以在`MessageReceived`執行需要在用戶端 上執行的任何工作後調用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="0c99d-313">在`MessageReceived`Hub 中,您可以執行依賴於原始方法調用的實際用戶端接收和處理的任何工作。</span><span class="sxs-lookup"><span data-stu-id="0c99d-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="0c99d-314">如何使用字串變數作為方法名稱</span><span class="sxs-lookup"><span data-stu-id="0c99d-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="0c99d-315">如果要使用字串變數作為方法名稱呼叫用戶端方法,則強制`Clients.All`(或`Clients.Others`、等`Clients.Caller`)呼叫`IClientProxy` [Invoke(方法名稱、args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="0c99d-316">如何從中心類管理組成員身份</span><span class="sxs-lookup"><span data-stu-id="0c99d-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="0c99d-317">SignalR 中的組提供了一種將消息廣播到連接客戶端的指定子集的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="0c99d-318">組可以具有任意數量的用戶端,並且用戶端可以是任意數量的組的成員。</span><span class="sxs-lookup"><span data-stu-id="0c99d-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="0c99d-319">要管理群組成員身份,請使用中心類`Groups`的屬性提供的[「添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)[和刪除」](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="0c99d-320">下面的範例顯示了由客戶`Groups.Add`端`Groups.Remove`碼 呼叫的 Hub 方法中使用的和方法,然後是呼叫它們的 JavaScript 客戶端碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="0c99d-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="0c99d-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="0c99d-322">**使用產生的代理的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="0c99d-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="0c99d-323">您不必顯式創建組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="0c99d-324">實際上,在調用`Groups.Add`中首次指定其名稱時會自動創建組,並且當您從其成員身份中刪除最後一個連接時,該組將被刪除。</span><span class="sxs-lookup"><span data-stu-id="0c99d-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="0c99d-325">沒有用於獲取組成員身份清單或組清單的 API。</span><span class="sxs-lookup"><span data-stu-id="0c99d-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="0c99d-326">SignalR 根據[pub/子模型](http://en.wikipedia.org/wiki/Publish/subscribe)向用戶端和組發送消息,並且伺服器不維護組或組成員身份的清單。</span><span class="sxs-lookup"><span data-stu-id="0c99d-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="0c99d-327">這有助於最大化可伸縮性,因為每當將節點添加到 Web 場時,SignalR 維護的任何狀態都必須傳播到新節點。</span><span class="sxs-lookup"><span data-stu-id="0c99d-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="0c99d-328">新增與移除方法的非同步</span><span class="sxs-lookup"><span data-stu-id="0c99d-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="0c99d-329">`Groups.Add`和`Groups.Remove`方法以異步方式執行。</span><span class="sxs-lookup"><span data-stu-id="0c99d-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="0c99d-330">如果要將用戶端添加到組,然後使用組立即向用戶端發送消息,則必須確保`Groups.Add`該方法首先完成。</span><span class="sxs-lookup"><span data-stu-id="0c99d-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="0c99d-331">下面的代碼示例演示如何執行此操作。</span><span class="sxs-lookup"><span data-stu-id="0c99d-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="0c99d-332">**將用戶端新增到群組,然後向該客戶端傳送訊息**</span><span class="sxs-lookup"><span data-stu-id="0c99d-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="0c99d-333">群組成員身份持久性</span><span class="sxs-lookup"><span data-stu-id="0c99d-333">Group membership persistence</span></span>

<span data-ttu-id="0c99d-334">SignalR 追蹤連線,而不是使用者,因此,如果您希望使用者每次建立連接時都位於同一組中,則每次使用者建立新連線時都必須呼`Groups.Add`叫 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="0c99d-335">在暫時失去連接後,有時 SignalR 可以自動復原連接。</span><span class="sxs-lookup"><span data-stu-id="0c99d-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="0c99d-336">在這種情況下,SignalR 正在還原相同的連接,而不是建立新連接,因此用戶端的組成員身份將自動還原。</span><span class="sxs-lookup"><span data-stu-id="0c99d-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="0c99d-337">即使臨時中斷是伺服器重新啟動或失敗的結果,也是可能的,因為每個用戶端(包括組成員身份)的連接狀態都向用戶端四捨五入。</span><span class="sxs-lookup"><span data-stu-id="0c99d-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="0c99d-338">如果伺服器在連接超時之前出現故障並由新伺服器替換,則用戶端可以自動重新連接到新伺服器,並重新註冊其成員的組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="0c99d-339">當連接在失去連接後或連接超時或客戶端斷開連接(例如,當瀏覽器導航到新頁面時)無法自動恢復時,組成員身份將丟失。</span><span class="sxs-lookup"><span data-stu-id="0c99d-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="0c99d-340">使用者下次連接時將是一個新連接。</span><span class="sxs-lookup"><span data-stu-id="0c99d-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="0c99d-341">要在同一使用者建立新連接時維護組成員身份,應用程式必須跟蹤使用者和組之間的關聯,並在每次使用者建立新連接時還原組成員身份。</span><span class="sxs-lookup"><span data-stu-id="0c99d-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="0c99d-342">有關連線和重新連線的詳細資訊,請參閱本主題後面的[「集線器」 類別如何處理連線存留期事件](#connectionlifetime)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="0c99d-343">單使用者群組</span><span class="sxs-lookup"><span data-stu-id="0c99d-343">Single-user groups</span></span>

<span data-ttu-id="0c99d-344">使用 SignalR 的應用程式通常必須追蹤使用者和連接之間的關聯,以便知道哪個使用者發送消息以及應該接收哪些使用者。</span><span class="sxs-lookup"><span data-stu-id="0c99d-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="0c99d-345">組用於執行此操作的兩個常用模式之一。</span><span class="sxs-lookup"><span data-stu-id="0c99d-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="0c99d-346">單使用者組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-346">Single-user groups.</span></span>

    <span data-ttu-id="0c99d-347">您可以將使用者名稱指定為組名稱,並在每次使用者連接或重新連接時將當前連接 ID 添加到群組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="0c99d-348">向發送給組的用戶發送消息。</span><span class="sxs-lookup"><span data-stu-id="0c99d-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="0c99d-349">此方法的缺點是,組不為您提供一種方法來了解使用者是連線還是脫機。</span><span class="sxs-lookup"><span data-stu-id="0c99d-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="0c99d-350">跟蹤使用者名和連接指示之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="0c99d-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="0c99d-351">您可以將每個使用者名稱與字典或資料庫中的一個或多個連接 I 之間的關聯存儲,並在每次使用者連接或斷開連接時更新儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="0c99d-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="0c99d-352">要向使用者發送消息,請指定連接指示。</span><span class="sxs-lookup"><span data-stu-id="0c99d-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="0c99d-353">此方法的缺點是它需要更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="0c99d-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="0c99d-354">如何處理集線器類別的連線存留期事件</span><span class="sxs-lookup"><span data-stu-id="0c99d-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="0c99d-355">處理連接存留期事件的典型原因是跟蹤使用者是否已連接,並跟蹤使用者名和連接權杖之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="0c99d-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="0c99d-356">要在用戶端連接或斷開連接時運行自己的代碼,請重寫`OnConnected``OnDisconnected`Hub`OnReconnected`類的和和虛擬方法,如以下示例所示。</span><span class="sxs-lookup"><span data-stu-id="0c99d-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="0c99d-357">當"連接"時,打開斷開狀態,並調用"重新連接"</span><span class="sxs-lookup"><span data-stu-id="0c99d-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="0c99d-358">每次瀏覽器導航到新頁面時,都必須建立一個新連接,這意味著 SignalR 將執行方法`OnDisconnected``OnConnected`後跟 的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="0c99d-359">建立新連接時,SignalR 始終建立新的連接 ID。</span><span class="sxs-lookup"><span data-stu-id="0c99d-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="0c99d-360">當`OnReconnected`SignalR 可以自動復原的連接出現暫時中斷時調用該方法,例如電纜在連接超時之前暫時斷開並重新連接時。當`OnDisconnected`客戶端斷開連接且 SignalR 無法自動重新連接時,如瀏覽器導航到新頁面時,將調用該方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="0c99d-361">因此,給定用戶端的可能事件序列為`OnConnected`,`OnReconnected``OnDisconnected`和或`OnConnected``OnDisconnected`。</span><span class="sxs-lookup"><span data-stu-id="0c99d-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="0c99d-362">對於給定的連線,`OnConnected``OnDisconnected`您將看不到序列,。 `OnReconnected`</span><span class="sxs-lookup"><span data-stu-id="0c99d-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="0c99d-363">在某些情況下`OnDisconnected`,例如伺服器出現故障或 App Domain 被回收時,不會調用該方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="0c99d-364">當另一台伺服器上線或 App Domain 完成其回收時,某些用戶端可能能夠重新連接`OnReconnected`並觸發 事件。</span><span class="sxs-lookup"><span data-stu-id="0c99d-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="0c99d-365">有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="0c99d-366">未填滿的呼叫者狀態</span><span class="sxs-lookup"><span data-stu-id="0c99d-366">Caller state not populated</span></span>

<span data-ttu-id="0c99d-367">連接存留期事件處理程式方法從伺服器呼叫,這意味著您`state`在 用戶端上的物件中放置的任何狀態將不會填充在`Caller`伺服器上 的屬性中。</span><span class="sxs-lookup"><span data-stu-id="0c99d-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="0c99d-368">有關`state`物件`Caller`和 屬性的資訊,請參閱本主題後面的[「如何在用戶端和中心類之間傳遞狀態](#passstate)」。</span><span class="sxs-lookup"><span data-stu-id="0c99d-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="0c99d-369">如何從內容取得有關用戶端的資訊</span><span class="sxs-lookup"><span data-stu-id="0c99d-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="0c99d-370">要取得有關用戶端的資訊`Context`, 請使用 Hub 類的屬性。</span><span class="sxs-lookup"><span data-stu-id="0c99d-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="0c99d-371">該`Context`屬性傳回[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)物件,該物件提供對以下資訊的存取:</span><span class="sxs-lookup"><span data-stu-id="0c99d-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="0c99d-372">呼叫用戶端的連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="0c99d-373">連接 ID 是由 SignalR 分配的 GUID(您無法在自己的代碼中指定值)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="0c99d-374">每個連接都有一個連接 ID,如果應用程式中有多個集線器,則所有集線器都使用相同的連接 ID。</span><span class="sxs-lookup"><span data-stu-id="0c99d-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="0c99d-375">HTTP 標頭數據。</span><span class="sxs-lookup"><span data-stu-id="0c99d-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="0c99d-376">還可以從`Context.Headers`獲取 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="0c99d-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="0c99d-377">對同一事物`Context.Headers`的多次引用的原因是首先創建`Context.Request`, 該屬性在以後添加`Context.Headers`,並保留為向後相容性。</span><span class="sxs-lookup"><span data-stu-id="0c99d-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="0c99d-378">查詢字串數據。</span><span class="sxs-lookup"><span data-stu-id="0c99d-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="0c99d-379">還可以從`Context.QueryString`獲取查詢字串數據。</span><span class="sxs-lookup"><span data-stu-id="0c99d-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="0c99d-380">在此屬性中獲取的查詢字串是與建立 SignalR 連接的 HTTP 請求一起使用的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="0c99d-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="0c99d-381">您可以通過設定連接在用戶端中添加查詢字串參數,這是將有關用戶端的數據從用戶端傳遞到伺服器的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="0c99d-382">下面的範例顯示了在使用生成的代理時在 JavaScript 用戶端中添加查詢字串的一種方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="0c99d-383">有關設置查詢字串參數的詳細資訊,請參閱[JavaScript](hubs-api-guide-javascript-client.md)和[.NET](hubs-api-guide-net-client.md)用戶端的 API 指南。</span><span class="sxs-lookup"><span data-stu-id="0c99d-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="0c99d-384">您可以在查詢字串資料中找到用於連接的傳輸方法,以及 SignalR 內部使用的一些其他值:</span><span class="sxs-lookup"><span data-stu-id="0c99d-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="0c99d-385">的值`transportMethod`將是"webSocket"、"伺服器發送事件"、"永久幀"或"長輪詢"。</span><span class="sxs-lookup"><span data-stu-id="0c99d-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="0c99d-386">請注意,如果在`OnConnected`事件處理程式方法中檢查此值,在某些情況下,最初可能會獲取傳輸值,該值不是連接的最終協商傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="0c99d-387">在這種情況下,該方法將引發異常,並在建立最終傳輸方法時稍後再次調用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="0c99d-388">Cookie。</span><span class="sxs-lookup"><span data-stu-id="0c99d-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="0c99d-389">您也可以從`Context.RequestCookies`獲取 Cookie。</span><span class="sxs-lookup"><span data-stu-id="0c99d-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="0c99d-390">使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="0c99d-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="0c99d-391">要求的 HttpContext 物件 :</span><span class="sxs-lookup"><span data-stu-id="0c99d-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="0c99d-392">使用此方法,而不是獲取`HttpContext.Current`SignalR`HttpContext`連接的物件。</span><span class="sxs-lookup"><span data-stu-id="0c99d-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="0c99d-393">如何在用戶端和中心類之間傳遞狀態</span><span class="sxs-lookup"><span data-stu-id="0c99d-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="0c99d-394">用戶端代理提供一個`state`物件,您可以在其中存儲要通過每個方法調用傳輸到伺服器的數據。</span><span class="sxs-lookup"><span data-stu-id="0c99d-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="0c99d-395">在伺服器上,您可以在用戶端呼叫的`Clients.Caller`Hub 方法中的屬性中存取此資料。</span><span class="sxs-lookup"><span data-stu-id="0c99d-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="0c99d-396">無法`Clients.Caller`為連線存留期事件處理程式填`OnConnected`滿`OnDisconnected`屬性`OnReconnected`, 並與 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="0c99d-397">在`state`物件中建立或更新數據`Clients.Caller`, 屬性在兩個方向上工作。</span><span class="sxs-lookup"><span data-stu-id="0c99d-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="0c99d-398">您可以更新伺服器中的值,並將它們傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="0c99d-399">下面的範例顯示 JavaScript 客戶端代碼,該代碼儲存狀態,以便透過每個方法呼叫傳輸到伺服器。</span><span class="sxs-lookup"><span data-stu-id="0c99d-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="0c99d-400">下面的範例顯示了 .NET 用戶端中的等效代碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="0c99d-401">在 Hub 類中,`Clients.Caller`您可以在 屬性中存取此資料。</span><span class="sxs-lookup"><span data-stu-id="0c99d-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="0c99d-402">下面的範例顯示檢索上一個範例中引用的狀態的代碼。</span><span class="sxs-lookup"><span data-stu-id="0c99d-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="0c99d-403">此持久狀態機制不適用於大量數據,因為在`state`或`Clients.Caller`屬性中放置的所有內容都隨每個方法調用一起迴圈。</span><span class="sxs-lookup"><span data-stu-id="0c99d-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="0c99d-404">它對於較小的專案(如使用者名或計數器)很有用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="0c99d-405">在VB.NET或強類型中心中,無法通過`Clients.Caller`而是使用`Clients.CallerState`(在信號R 2.1 中介紹):</span><span class="sxs-lookup"><span data-stu-id="0c99d-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="0c99d-406">**在 C 中使用呼叫方狀態#**</span><span class="sxs-lookup"><span data-stu-id="0c99d-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="0c99d-407">**以視覺化基礎使用呼叫方狀態**</span><span class="sxs-lookup"><span data-stu-id="0c99d-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="0c99d-408">如何處理中心類別的錯誤</span><span class="sxs-lookup"><span data-stu-id="0c99d-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="0c99d-409">要處理在 Hub 類方法中發生的錯誤,首先請`await`確保使用 「觀察」非同步操作(如調用用戶端方法)中的任何異常。</span><span class="sxs-lookup"><span data-stu-id="0c99d-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="0c99d-410">然後使用以下一種或多種方法:</span><span class="sxs-lookup"><span data-stu-id="0c99d-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="0c99d-411">將方法代碼包裝在 try-catch 塊中並記錄異常物件。</span><span class="sxs-lookup"><span data-stu-id="0c99d-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="0c99d-412">出於除錯目的,您可以將異常發送給用戶端,但出於安全原因,不建議向生產中的客戶端發送詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c99d-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="0c99d-413">建立處理[On 傳入錯誤](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法的集線器管道模組。</span><span class="sxs-lookup"><span data-stu-id="0c99d-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="0c99d-414">下面的示例顯示了一個管道模組,該模組記錄錯誤,然後是Startup.cs中的代碼,該代碼將模組注入到集線器管道中。</span><span class="sxs-lookup"><span data-stu-id="0c99d-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="0c99d-415">使用類`HubException`(在 SignalR 2 中介紹)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="0c99d-416">可以從任何集線器調用引發此錯誤。</span><span class="sxs-lookup"><span data-stu-id="0c99d-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="0c99d-417">建構`HubError`函數獲取字串訊息和用於存儲額外錯誤數據的物件。</span><span class="sxs-lookup"><span data-stu-id="0c99d-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="0c99d-418">SignalR 將自動序列化異常並將其發送到用戶端,用戶端將用於拒絕或失敗集線器方法調用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="0c99d-419">以下代碼示例演示如何在中心調用期間引發`HubException`,以及如何處理 JavaScript 和 .NET 用戶端上的異常。</span><span class="sxs-lookup"><span data-stu-id="0c99d-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="0c99d-420">**展示 HubException 類別的伺服器碼**</span><span class="sxs-lookup"><span data-stu-id="0c99d-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="0c99d-421">**JavaScript 客戶端碼展示對在中心中引發 HubException 的回應**</span><span class="sxs-lookup"><span data-stu-id="0c99d-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="0c99d-422">**.NET 用戶端代碼,用於回應在中心中引發 HubException**</span><span class="sxs-lookup"><span data-stu-id="0c99d-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="0c99d-423">有關集線器管線模組的詳細資訊,請參閱本主題後面的[如何自訂中心管道](#hubpipeline)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="0c99d-424">如何開啟追蹤</span><span class="sxs-lookup"><span data-stu-id="0c99d-424">How to enable tracing</span></span>

<span data-ttu-id="0c99d-425">要啟用伺服器端追蹤,請向 Web.config 檔案加入 system.診斷元素,如以下範例所示:</span><span class="sxs-lookup"><span data-stu-id="0c99d-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="0c99d-426">在 Visual Studio 中執行應用程式時,可以在 **「輸出」** 視窗中查看日誌。</span><span class="sxs-lookup"><span data-stu-id="0c99d-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="0c99d-427">如何呼叫用戶端方法並管理來自中心類外部的群組</span><span class="sxs-lookup"><span data-stu-id="0c99d-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="0c99d-428">要從與 Hub 類不同的類調用用戶端方法,請獲取對集線器的 SignalR 上下文物件的引用,並用它來呼叫用戶端或管理組上的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="0c99d-429">以下範例`StockTicker`類獲取上下文物件,將其儲存在類的實例中,將類實例存儲在靜態屬性中,並使用 singleton 類實例中的上下文調用`updateStockPrice``StockTickerHub`連接到名為 的 Hub 的用戶端上的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="0c99d-430">如果需要在長壽命物件中多次使用上下文,獲取引用一次並保存它,而不是每次都再次獲取它。</span><span class="sxs-lookup"><span data-stu-id="0c99d-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="0c99d-431">獲取上下文一次可確保 SignalR 以與集線器方法進行用戶端方法調用的順序相同的順序向用戶端發送消息。</span><span class="sxs-lookup"><span data-stu-id="0c99d-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="0c99d-432">有關展示如何對集線器使用 SignalR 上下文的教學,請參閱[使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="0c99d-433">呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="0c99d-433">Calling client methods</span></span>

<span data-ttu-id="0c99d-434">您可以指定哪些用戶端將收到 RPC,但與從中心類調用時相比,選項更少。</span><span class="sxs-lookup"><span data-stu-id="0c99d-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="0c99d-435">原因是上下文與來自用戶端的特定調用不相關聯,因此任何需要瞭解當前連接 ID 的方法`Clients.Others`(`Clients.Caller`如`Clients.OthersInGroup`或或 ) 都不可用。</span><span class="sxs-lookup"><span data-stu-id="0c99d-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="0c99d-436">有下列選項可供使用：</span><span class="sxs-lookup"><span data-stu-id="0c99d-436">The following options are available:</span></span>

- <span data-ttu-id="0c99d-437">所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="0c99d-438">由連接 ID 標識的特定用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="0c99d-439">除指定客戶端外的所有連接用戶端,由連接 ID 標識。</span><span class="sxs-lookup"><span data-stu-id="0c99d-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="0c99d-440">指定組中的所有連接用戶端。</span><span class="sxs-lookup"><span data-stu-id="0c99d-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="0c99d-441">指定群組中的所有連接客戶端(指定用戶端除外),由連接 ID 識別。</span><span class="sxs-lookup"><span data-stu-id="0c99d-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="0c99d-442">如果要從 Hub 類別的方法呼叫非 Hub 類別,則可以將`Clients.Client`目前連線 ID 傳遞`Clients.AllExcept`,`Clients.Group`並將`Clients.Caller`其`Clients.Others`用於`Clients.OthersInGroup`, 或模擬或 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="0c99d-443">在下面的範例中`MoveShapeHub`,類別將連接 ID`Broadcaster`來傳`Broadcaster`給類別,`Clients.Others`以便類可以類比 。</span><span class="sxs-lookup"><span data-stu-id="0c99d-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="0c99d-444">管理群組成員身份</span><span class="sxs-lookup"><span data-stu-id="0c99d-444">Managing group membership</span></span>

<span data-ttu-id="0c99d-445">對於管理組,您具有與在中心類中相同的選項。</span><span class="sxs-lookup"><span data-stu-id="0c99d-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="0c99d-446">新增客戶端到群組</span><span class="sxs-lookup"><span data-stu-id="0c99d-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="0c99d-447">從群組中移除客戶端</span><span class="sxs-lookup"><span data-stu-id="0c99d-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="0c99d-448">如何自訂中心管道</span><span class="sxs-lookup"><span data-stu-id="0c99d-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="0c99d-449">SignalR 使您能夠將您自己的代碼注入集線器管道。</span><span class="sxs-lookup"><span data-stu-id="0c99d-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="0c99d-450">下面的範例顯示了一個自定義 Hub 管道模組,該模組記錄從用戶端和在用戶端上調用的傳出方法調用收到的每個傳入方法呼叫:</span><span class="sxs-lookup"><span data-stu-id="0c99d-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="0c99d-451">*Startup.cs*檔案中的以下代碼註冊在集線器導管中執行的模組:</span><span class="sxs-lookup"><span data-stu-id="0c99d-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="0c99d-452">您可以重寫許多不同的方法。</span><span class="sxs-lookup"><span data-stu-id="0c99d-452">There are many different methods that you can override.</span></span> <span data-ttu-id="0c99d-453">有關完整清單,請參閱[HubPipeline 模組方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="0c99d-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
