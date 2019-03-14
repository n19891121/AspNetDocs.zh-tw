---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 範例 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: b8ce2b40a19e0429f1ccedb03b8f829582652d24
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056395"
---
<a name="katana-samples"></a>Katana 範例
====================
by [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 範例

**ASP.NET 路由範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
在某些應用程式，您會想要連結與非 OWIN 元件並存的 Asp.Net 路由表中的 OWIN 元件。 此範例示範如何使用 MapOwinPath 和 MapOwinRoute Microsoft.Owin.Host.SystemWeb 所提供的 RouteCollection 擴充方法。

**分支管線範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 要求處理管線就不需要是線性，它們可以分支到不同的方式處理要求。 此範例示範如何建構要求路徑或其他要求資料，例如標頭為基礎的分支管線。 這些元件是 Microsoft.Owin.Mapping nuget 套件中可用的。

**自訂伺服器範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
示範如何使用自訂的 OWIN 伺服器自我裝載時 OWIN。

**內嵌範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
某些 OWIN 伺服器可以在自己的程序內執行 (&quot;自我裝載&quot;)。 此範例示範如何開始使用 Microsoft.Owin.Hosting nuget 套件所提供的工具的 OWIN 應用程式。

**HelloWorld 範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN 會是 HTTP 伺服器 API 抽象概念，可讓應用程式可攜性，設定跨越各種伺服器。 這個範例會示範如何撰寫 Hello World 應用程式使用某些**簡單的包裝函式**未經處理的 OWIN 抽象概念和執行它的 web 伺服器上像是 ASP.NET。

**Hello World 未經處理的 OWIN 範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
這個範例會示範如何撰寫 Hello World 應用程式，使用**原始**OWIN 抽象概念，例如 Asp.Net web 伺服器上加以執行。

**SignalR 範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
示範如何在自我裝載使用 OWIN SignalR / Katana。 如需自我裝載的 SignalR 相關的詳細資訊，請參閱[教學課程：SignalR 自我裝載](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

**靜態檔案範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
示範如何使用 OWIN 的靜態檔案的支援 HTTP 要求 / Katana。

**Web API** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
此範例示範如何裝載在 IIS 中的 OWIN，以及將 Web API 新增至 OWIN 管線。

**Web 通訊端範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
示範如何使用 OWIN 支援 Web 通訊端[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)類別。
