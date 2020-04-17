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
# <a name="katana-samples"></a>Katana 範例

由[微軟](https://github.com/microsoft)

## <a name="katana-samples"></a>Katana 範例

**ASP.NET路由範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
在某些應用程式中,您需要將Asp.Net路由表中的OWIN元件與非OWIN元件並排連接。 此示例演示如何使用 Microsoft.Owin.Host.SystemWeb 提供的路由收集擴展方法 MapOwinPath 和 MapOwinRoute。

**分支導管示例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
OWIN 請求處理管道不需要線性處理,它們可以通過不同的方式分支處理請求。 此示例演示如何基於請求路徑或其他請求數據(如標頭)構造分支管道。 這些元件在Microsoft.Owin.映射nuget包中可用。

**自訂伺服器範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
演示如何在自託管 OWIN 時使用自定義 OWIN 伺服器。

**內嵌式範例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
某些 OWIN 伺服器可以在您自己的&quot;進程(&quot;自託管 )內運行。 此示例演示如何使用 Microsoft.Owin.Hosting nuget 套件提供的工具啟動 OWIN 應用程式。

**HelloWorld 範例** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN 是一個 HTTP 伺服器 API 抽象,可在各種伺服器上實現應用程式可移植性。 此示例演示如何使用原始 OWIN 抽象周圍的一些**簡單包裝器**編寫 Hello World 應用程式,並在 web 伺服器上運行它,如 ASP.NET。

**你好世界原始OWIN樣品** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
此示例演示如何使用**原始**OWIN 抽象編寫 Hello World 應用程式,並在 web 伺服器上運行它,如 Asp.Net。

**訊號樣本** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
展示如何使用 OWIN / Katana 自承載 SignalR。 有關自託管信號R的詳細資訊,請參閱[教程:SignalR 自主機](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

**靜態檔案範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
展示如何使用 OWIN / Katana 支援靜態檔的 HTTP 請求。

**Web API** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
此示例展示如何在IIS中託管OWIN並將Web API添加到OWIN管道。

**Web 通訊形字示程式** | [源碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
展示如何使用[System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx)類支援 OWIN 中的 Web 套接字。
