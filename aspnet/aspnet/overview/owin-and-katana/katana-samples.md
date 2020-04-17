---
uid: aspnet/overview/owin-and-katana/katana-samples
title: 卡塔納樣品 |微軟文件
author: rick-anderson
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 15cc1084b16db2619f2295ee21dec4f49eb2e354
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540437"
---
# <a name="katana-samples"></a><span data-ttu-id="740e2-102">Katana 範例</span><span class="sxs-lookup"><span data-stu-id="740e2-102">Katana Samples</span></span>

<span data-ttu-id="740e2-103">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="740e2-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="740e2-104">Katana 範例</span><span class="sxs-lookup"><span data-stu-id="740e2-104">Katana Samples</span></span>

<span data-ttu-id="740e2-105">**ASP.NET路由範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="740e2-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="740e2-106">在某些應用程式中,您需要將Asp.Net路由表中的OWIN元件與非OWIN元件並排連接。</span><span class="sxs-lookup"><span data-stu-id="740e2-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="740e2-107">此示例演示如何使用 Microsoft.Owin.Host.SystemWeb 提供的路由收集擴展方法 MapOwinPath 和 MapOwinRoute。</span><span class="sxs-lookup"><span data-stu-id="740e2-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="740e2-108">**分支導管示例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="740e2-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="740e2-109">OWIN 請求處理管道不需要線性處理,它們可以通過不同的方式分支處理請求。</span><span class="sxs-lookup"><span data-stu-id="740e2-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="740e2-110">此示例演示如何基於請求路徑或其他請求數據(如標頭)構造分支管道。</span><span class="sxs-lookup"><span data-stu-id="740e2-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="740e2-111">這些元件在Microsoft.Owin.映射nuget包中可用。</span><span class="sxs-lookup"><span data-stu-id="740e2-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="740e2-112">**自訂伺服器範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="740e2-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="740e2-113">演示如何在自託管 OWIN 時使用自定義 OWIN 伺服器。</span><span class="sxs-lookup"><span data-stu-id="740e2-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="740e2-114">**內嵌式範例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="740e2-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="740e2-115">某些 OWIN 伺服器可以在您自己的&quot;進程(&quot;自託管 )內運行。</span><span class="sxs-lookup"><span data-stu-id="740e2-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="740e2-116">此示例演示如何使用 Microsoft.Owin.Hosting nuget 套件提供的工具啟動 OWIN 應用程式。</span><span class="sxs-lookup"><span data-stu-id="740e2-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="740e2-117">**HelloWorld 範例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="740e2-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="740e2-118">OWIN 是一個 HTTP 伺服器 API 抽象,可在各種伺服器上實現應用程式可移植性。</span><span class="sxs-lookup"><span data-stu-id="740e2-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="740e2-119">此示例演示如何使用原始 OWIN 抽象周圍的一些**簡單包裝器**編寫 Hello World 應用程式,並在 web 伺服器上運行它,如 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="740e2-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="740e2-120">**你好世界原始OWIN樣品** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="740e2-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="740e2-121">此示例演示如何使用**原始**OWIN 抽象編寫 Hello World 應用程式,並在 web 伺服器上運行它,如 Asp.Net。</span><span class="sxs-lookup"><span data-stu-id="740e2-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="740e2-122">**訊號樣本** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="740e2-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="740e2-123">展示如何使用 OWIN / Katana 自承載 SignalR。</span><span class="sxs-lookup"><span data-stu-id="740e2-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="740e2-124">有關自託管信號R的詳細資訊,請參閱[教程:SignalR 自主機](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="740e2-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="740e2-125">**靜態檔案範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="740e2-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="740e2-126">展示如何使用 OWIN / Katana 支援靜態檔的 HTTP 請求。</span><span class="sxs-lookup"><span data-stu-id="740e2-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="740e2-127">**Web API** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="740e2-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="740e2-128">此示例展示如何在IIS中託管OWIN並將Web API添加到OWIN管道。</span><span class="sxs-lookup"><span data-stu-id="740e2-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="740e2-129">**Web 通訊形字示程式** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span><span class="sxs-lookup"><span data-stu-id="740e2-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="740e2-130">展示如何使用[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)類支援 OWIN 中的 Web 套接字。</span><span class="sxs-lookup"><span data-stu-id="740e2-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
