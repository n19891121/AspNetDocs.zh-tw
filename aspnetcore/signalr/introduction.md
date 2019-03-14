---
title: ASP.NET Core SignalR 簡介
author: bradygaster
description: 了解 ASP.NET Core SignalR 程式庫如何簡化將即時功能新增至應用程式。
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 04/25/2018
uid: signalr/introduction
ms.openlocfilehash: 673efafce60dfa46cb99f9537fda2bca42bf9822
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063005"
---
# <a name="introduction-to-aspnet-core-signalr"></a><span data-ttu-id="9d1f8-103">ASP.NET Core SignalR 簡介</span><span class="sxs-lookup"><span data-stu-id="9d1f8-103">Introduction to ASP.NET Core SignalR</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="9d1f8-104">SignalR 是什麼？</span><span class="sxs-lookup"><span data-stu-id="9d1f8-104">What is SignalR?</span></span>

<span data-ttu-id="9d1f8-105">ASP.NET Core SignalR 是能簡化新增即時 web 功能的應用程式的開放原始碼程式庫。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-105">ASP.NET Core SignalR is an open-source library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="9d1f8-106">即時 web 功能立即可讓用戶端推入內容的伺服器端程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-106">Real-time web functionality enables server-side code to push content to clients instantly.</span></span>

<span data-ttu-id="9d1f8-107">Signalr 的良好候選項目：</span><span class="sxs-lookup"><span data-stu-id="9d1f8-107">Good candidates for SignalR:</span></span>

* <span data-ttu-id="9d1f8-108">需要來自伺服器的高頻率更新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-108">Apps that require high frequency updates from the server.</span></span> <span data-ttu-id="9d1f8-109">範例包括遊戲、 社交網路、 投票、 拍賣、 對應和 GPS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-109">Examples are gaming, social networks, voting, auction, maps, and GPS apps.</span></span>
* <span data-ttu-id="9d1f8-110">儀表板和監視的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-110">Dashboards and monitoring apps.</span></span> <span data-ttu-id="9d1f8-111">範例包括公司儀表板，立即銷售的更新，或的旅遊警示。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-111">Examples include company dashboards, instant sales updates, or travel alerts.</span></span>
* <span data-ttu-id="9d1f8-112">共同作業應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-112">Collaborative apps.</span></span> <span data-ttu-id="9d1f8-113">白板應用程式和小組會議軟體是共同作業應用程式的範例。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-113">Whiteboard apps and team meeting software are examples of collaborative apps.</span></span>
* <span data-ttu-id="9d1f8-114">需要通知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-114">Apps that require notifications.</span></span> <span data-ttu-id="9d1f8-115">社交網路、 電子郵件、 聊天室、 遊戲、 的移動警示和許多其他應用程式使用通知。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-115">Social networks, email, chat, games, travel alerts, and many other apps use notifications.</span></span>

<span data-ttu-id="9d1f8-116">SignalR 提供的 API 來建立伺服器到用戶端[遠端程序呼叫 (RPC)](https://wikipedia.org/wiki/Remote_procedure_call)。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-116">SignalR provides an API for creating server-to-client [remote procedure calls (RPC)](https://wikipedia.org/wiki/Remote_procedure_call).</span></span> <span data-ttu-id="9d1f8-117">從伺服器端.NET Core 程式碼，Rpc 會呼叫 JavaScript 函式在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-117">The RPCs call JavaScript functions on clients from server-side .NET Core code.</span></span>

<span data-ttu-id="9d1f8-118">以下是適用於 ASP.NET Core SignalR 的一些功能：</span><span class="sxs-lookup"><span data-stu-id="9d1f8-118">Here are some features of SignalR for ASP.NET Core:</span></span>

* <span data-ttu-id="9d1f8-119">會自動處理連接管理。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-119">Handles connection management automatically.</span></span>
* <span data-ttu-id="9d1f8-120">同時將訊息傳送至所有連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-120">Sends messages to all connected clients simultaneously.</span></span> <span data-ttu-id="9d1f8-121">比方說，聊天室。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-121">For example, a chat room.</span></span>
* <span data-ttu-id="9d1f8-122">將訊息傳送至特定的用戶端或群組的用戶端。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-122">Sends messages to specific clients or groups of clients.</span></span>
* <span data-ttu-id="9d1f8-123">可調整來處理增加的流量。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-123">Scales to handle increasing traffic.</span></span>

<span data-ttu-id="9d1f8-124">來源裝載於[SignalR GitHub 上的存放庫](https://github.com/aspnet/AspNetCore/tree/master/src/SignalR)。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-124">The source is hosted in a [SignalR repository on GitHub](https://github.com/aspnet/AspNetCore/tree/master/src/SignalR).</span></span>

## <a name="transports"></a><span data-ttu-id="9d1f8-125">傳輸</span><span class="sxs-lookup"><span data-stu-id="9d1f8-125">Transports</span></span>

<span data-ttu-id="9d1f8-126">SignalR 支援數種技術來處理即時通訊：</span><span class="sxs-lookup"><span data-stu-id="9d1f8-126">SignalR supports several techniques for handling real-time communications:</span></span>

* [<span data-ttu-id="9d1f8-127">WebSockets</span><span class="sxs-lookup"><span data-stu-id="9d1f8-127">WebSockets</span></span>](https://tools.ietf.org/html/rfc7118)
* <span data-ttu-id="9d1f8-128">伺服器傳送事件</span><span class="sxs-lookup"><span data-stu-id="9d1f8-128">Server-Sent Events</span></span>
* <span data-ttu-id="9d1f8-129">長輪詢</span><span class="sxs-lookup"><span data-stu-id="9d1f8-129">Long Polling</span></span>

<span data-ttu-id="9d1f8-130">SignalR 會自動選擇最佳的傳輸方法內的伺服器和用戶端功能。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-130">SignalR automatically chooses the best transport method that is within the capabilities of the server and client.</span></span>

## <a name="hubs"></a><span data-ttu-id="9d1f8-131">中樞</span><span class="sxs-lookup"><span data-stu-id="9d1f8-131">Hubs</span></span>

<span data-ttu-id="9d1f8-132">使用 SignalR*中樞*用戶端和伺服器之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-132">SignalR uses *hubs* to communicate between clients and servers.</span></span>

<span data-ttu-id="9d1f8-133">中樞是可讓用戶端與伺服器彼此呼叫方法的高階管線。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-133">A hub is a high-level pipeline that allows a client and server to call methods on each other.</span></span> <span data-ttu-id="9d1f8-134">SignalR 處理分派跨電腦界限會自動允許用戶端呼叫方法，在伺服器上，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-134">SignalR handles the dispatching across machine boundaries automatically, allowing clients to call methods on the server and vice versa.</span></span> <span data-ttu-id="9d1f8-135">您可以傳遞強型別參數至方法，可使用模型繫結。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-135">You can pass strongly-typed parameters to methods, which enables model binding.</span></span> <span data-ttu-id="9d1f8-136">SignalR 提供兩個內建中樞通訊協定： 文字通訊協定會根據 JSON 和二進位通訊協定為基礎[MessagePack](https://msgpack.org/)。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-136">SignalR provides two built-in hub protocols: a text protocol based on JSON and a binary protocol based on [MessagePack](https://msgpack.org/).</span></span>  <span data-ttu-id="9d1f8-137">MessagePack 通常會建立較小的訊息，相較於 JSON。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-137">MessagePack generally creates smaller messages compared to JSON.</span></span> <span data-ttu-id="9d1f8-138">必須支援舊版瀏覽器[XHR 層級 2](https://caniuse.com/#feat=xhr2)提供 MessagePack 通訊協定支援。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-138">Older browsers must support [XHR level 2](https://caniuse.com/#feat=xhr2) to provide MessagePack protocol support.</span></span>

<span data-ttu-id="9d1f8-139">中樞會呼叫用戶端程式碼，藉由傳送訊息，它包含名稱和用戶端方法的參數。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-139">Hubs call client-side code by sending messages that contain the name and parameters of the client-side method.</span></span> <span data-ttu-id="9d1f8-140">做為方法參數傳送的物件會使用設定的通訊協定來還原序列化。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-140">Objects sent as method parameters are deserialized using the configured protocol.</span></span> <span data-ttu-id="9d1f8-141">用戶端會嘗試比對用戶端程式碼中的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-141">The client tries to match the name to a method in the client-side code.</span></span> <span data-ttu-id="9d1f8-142">當用戶端找到相符項目時，它會呼叫方法，並已還原序列化的參數資料傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="9d1f8-142">When the client finds a match, it calls the method and passes to it the deserialized parameter data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d1f8-143">其他資源</span><span class="sxs-lookup"><span data-stu-id="9d1f8-143">Additional resources</span></span>

* [<span data-ttu-id="9d1f8-144">開始使用 SignalR 的 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9d1f8-144">Get started with SignalR for ASP.NET Core</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="9d1f8-145">支援的平台</span><span class="sxs-lookup"><span data-stu-id="9d1f8-145">Supported Platforms</span></span>](xref:signalr/supported-platforms)
* [<span data-ttu-id="9d1f8-146">中樞</span><span class="sxs-lookup"><span data-stu-id="9d1f8-146">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="9d1f8-147">JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="9d1f8-147">JavaScript client</span></span>](xref:signalr/javascript-client)
