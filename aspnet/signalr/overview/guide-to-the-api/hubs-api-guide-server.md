---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: 'ASP.NET SignalR 中樞 API 指南-Server (c # ) |Microsoft Docs'
author: bradygaster
description: 本檔介紹如何針對 SignalR 第2版的 ASP.NET SignalR 中樞 API 程式設計程式，並提供示範的程式碼範例 .。。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345375"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET SignalR 中樞 API 指南-Server (c # ) 

由 [派翠克 Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔提供使用示範一般選項的程式碼範例，設計 ASP.NET SignalR Hub API for SignalR 第2版的伺服器端程式設計簡介。
> 
> SignalR 中樞 API 可讓您進行遠端程序呼叫， (從伺服器到連線用戶端，以及從用戶端到伺服器的 Rpc) 。 在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。 在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。 SignalR 會為您處理所有用戶端對伺服器的配管。
> 
> SignalR 也提供較低層級的 API，稱為「持續連線」。 如需 SignalR、中樞和持續連線的簡介，請參閱 [SignalR 2 簡介](../getting-started/introduction-to-signalr.md)。
> 
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 第2版
>   
> 
> 
> ## <a name="topic-versions"></a>主題版本
> 
> 如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>問題與意見
> 
> 請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。 如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [如何註冊 SignalR 中介軟體](#route)

    - [/Signalr URL](#signalrurl)
    - [設定 SignalR 選項](#options)
- [如何建立和使用中樞類別](#hubclass)

    - [中樞物件存留期](#transience)
    - [在 JavaScript 用戶端中的中樞名稱的 camel 大小寫](#hubnames)
    - [多個中樞](#multiplehubs)
    - [強型別中樞](#stronglytypedhubs)
- [如何定義用戶端可以呼叫的中樞類別中的方法](#hubmethods)

    - [JavaScript 用戶端中方法名稱的 camel 大小寫](#methodnames)
    - [非同步執行的時機](#asyncmethods)
    - [定義多載](#overloads)
    - [從中樞方法調用報告進度](#progress)
- [如何從中樞類別呼叫用戶端方法](#callfromhub)

    - [選取哪些用戶端將接收 RPC](#selectingclients)
    - [沒有方法名稱的編譯時間驗證](#dynamicmethodnames)
    - [不區分大小寫的方法名稱比對](#caseinsensitive)
    - [非同步執行](#asyncclient)
- [如何從中樞類別管理群組成員資格](#groupsfromhub)

    - [非同步執行加入和移除方法](#asyncgroupmethods)
    - [群組成員資格持續性](#grouppersistence)
    - [單一使用者群組](#singleusergroups)
- [如何處理中樞類別中的連接存留期事件](#connectionlifetime)

    - [當呼叫 OnConnected、OnDisconnected 和 OnReconnected 時](#onreconnected)
    - [未填入呼叫端狀態](#nocallerstate)
- [如何從內容屬性取得用戶端的相關資訊](#contextproperty)
- [如何在用戶端與中樞類別之間傳遞狀態](#passstate)
- [如何處理中樞類別中的錯誤](#handleErrors)
- [如何從中樞類別外部呼叫用戶端方法和管理群組](#callfromoutsidehub)

    - [呼叫用戶端方法](#callingclientsoutsidehub)
    - [管理群組成員資格](#managinggroupsoutsidehub)
- [如何啟用追蹤](#tracing)
- [如何自訂中樞管線](#hubpipeline)

如需如何編寫用戶端程式的相關檔，請參閱下列資源：

- [SignalR 中樞 API 指南-JavaScript 用戶端](hubs-api-guide-javascript-client.md)
- [SignalR 中樞 API 指南-.NET 用戶端](hubs-api-guide-net-client.md)

SignalR 2 的伺服器元件僅適用于 .NET 4.5。 執行 .NET 4.0 的伺服器必須使用 SignalR v1. x。

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>如何註冊 SignalR 中介軟體

若要定義用戶端將用來連線到您中樞的路由，請 `MapSignalR` 在應用程式啟動時呼叫方法。 `MapSignalR` 是類別的 [擴充方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) `OwinExtensions` 。 下列範例示範如何使用 OWIN 啟動類別來定義 SignalR 中樞路由。

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

如果您要將 SignalR 功能新增至 ASP.NET MVC 應用程式，請確定已在其他路由之前新增 SignalR 路由。 如需詳細資訊，請參閱 [教學課程：使用 SignalR 2 和 MVC 5 消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/Signalr URL

根據預設，用戶端將用來連線到您中樞的路由 URL 是 "/signalr"。  (不要將此 URL 與 "/signalr/hubs" URL 混淆，這是自動產生的 JavaScript 檔案。 如需有關產生之 proxy 的詳細資訊，請參閱 [SignalR 中樞 API 指南-JavaScript 用戶端-產生的 proxy 和其用途](hubs-api-guide-javascript-client.md#genproxy)。 ) 

在某些情況下，可能會讓此基底 URL 無法供 SignalR 使用;例如，您的專案中有一個名為 *signalr* 的資料夾，而且您不想要變更名稱。 在此情況下，您可以變更基底 URL，如下列範例所示 (將範例程式碼中的 "/signalr" 取代為您想要的 URL) 。

**指定 URL 的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**JavaScript 用戶端程式代碼，指定與產生的 proxy (的 URL) **

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**指定 URL (的 JavaScript 用戶端程式代碼，不含產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**指定 URL 的 .NET 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>設定 SignalR 選項

方法的多載可 `MapSignalR` 讓您指定自訂 URL、自訂相依性解析程式，以及下列選項：

- 使用 CORS 或 JSONP 從瀏覽器用戶端啟用跨網域呼叫。

    一般而言，如果瀏覽器從載入頁面 `http://contoso.com` ，SignalR 連接會位於相同的網域中 `http://contoso.com/signalr` 。 如果頁面無法 `http://contoso.com` 連接到 `http://fabrikam.com/signalr` ，則為跨網域連接。 基於安全性考慮，預設會停用跨網域連接。 如需詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端-如何建立跨網域連接](hubs-api-guide-javascript-client.md#crossdomain)。
- 啟用詳細的錯誤訊息。

    發生錯誤時，SignalR 的預設行為是將通知訊息傳送給用戶端，而不會有發生什麼事的詳細資料。 不建議在生產環境中傳送詳細的錯誤資訊給用戶端，因為惡意使用者可能會對您的應用程式使用這些資訊。 若要進行疑難排解，您可以使用此選項暫時啟用更具資訊性的錯誤報表。
- 停用自動產生的 JavaScript proxy 檔案。

    根據預設，會產生一個 JavaScript 檔案，其中包含中樞類別的 proxy，以回應 URL "/signalr/hubs"。 如果您不想要使用 JavaScript proxy，或是想要以手動方式產生此檔案並參考用戶端中的實體檔案，您可以使用此選項來停用 proxy 產生。 如需詳細資訊，請參閱 [SignalR 中樞 API 指南-JavaScript 用戶端-如何為 SignalR 產生的 proxy 建立實體](hubs-api-guide-javascript-client.md#manualproxy)檔案。

下列範例顯示如何在呼叫方法時指定 SignalR 連接 URL 和這些選項 `MapSignalR` 。 若要指定自訂 URL，請使用您想要使用的 URL 來取代範例中的 "/signalr"。

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>如何建立和使用中樞類別

若要建立中樞，請建立衍生自 [Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)的類別。 下列範例顯示聊天應用程式的簡單中樞類別。

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

在此範例中，已連線的用戶端可以呼叫 `NewContosoChatMessage` 方法，而在此情況下，收到的資料會廣播至所有連線的用戶端。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>中樞物件存留期

您不會在伺服器上具現化中樞類別，或從您自己的程式碼呼叫其方法;SignalR Hub 管線會為您完成這一切。 SignalR 會在每次需要處理中樞作業（例如用戶端連接、中斷連接或對伺服器進行方法呼叫）時，建立中樞類別的新實例。

由於中樞類別的實例是暫時性的，因此您無法使用它們來維護從某個方法呼叫到下一個方法的狀態。 每次伺服器收到來自用戶端的方法呼叫時，您中樞類別的新實例就會處理訊息。 若要透過多個連接和方法呼叫來維護狀態，請使用其他方法（例如資料庫）或中樞類別上的靜態變數，或不是衍生自的不同類別 `Hub` 。 如果您將資料保存在記憶體中，則在中樞類別使用靜態變數之類的方法時，將會在應用程式域回收時遺失資料。

如果您想要從中樞類別以外的程式碼將訊息傳送至用戶端，您無法將中樞類別實例具現化，但您可以藉由取得中樞類別的 SignalR 內容物件參考來執行此作業。 如需詳細資訊，請參閱本主題稍後的 [如何從中樞類別外部呼叫用戶端方法和管理群組](#callfromoutsidehub) 。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>在 JavaScript 用戶端中的中樞名稱的 camel 大小寫

根據預設，JavaScript 用戶端會使用類別名稱的 camel 大小寫版本來參考中樞。 SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。 先前的範例會 `contosoChatHub` 在 JavaScript 程式碼中稱為。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

如果您想要指定不同的名稱供用戶端使用，請加入 `HubName` 屬性。 當您使用 `HubName` 屬性時，JavaScript 用戶端上的 camel 大小寫不會有名稱變更。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>多個中樞

您可以在應用程式中定義多個中樞類別。 當您這樣做時，連接會共用，但群組會分開：

- 所有用戶端都會使用相同的 URL 來建立與您的服務 ( "/signalr" 的 SignalR 連線，或您的自訂 URL （如果您指定了一個) ，而且該連線會用於服務所定義的所有中樞）。

    相較于在單一類別中定義所有中樞功能，多個中樞沒有任何效能差異。
- 所有中樞都取得相同的 HTTP 要求資訊。

    由於所有中樞共用相同的連線，因此伺服器所取得的唯一 HTTP 要求資訊就是原始 HTTP 要求中建立 SignalR 連接的內容。 如果您藉由指定查詢字串來使用連線要求，將資訊從用戶端傳遞至伺服器，則無法將不同的查詢字串提供給不同的中樞。 所有中樞都會收到相同的資訊。
- 產生的 JavaScript proxy 檔案將包含一個檔案中所有中樞的 proxy。

    如需有關 JavaScript proxy 的資訊，請參閱 [SignalR 中樞 API 指南-JAVAscript 用戶端-產生的 proxy 以及它為您執行的](hubs-api-guide-javascript-client.md#genproxy)工作。
- 群組會定義于中樞內。

    在 SignalR 中，您可以定義已命名的群組，以廣播到連線用戶端的子集。 群組會針對每個中樞分開維護。 例如，名為 "Administrators" 的群組會包含您類別的一組用戶端 `ContosoChatHub` ，而相同的組名則會參考您類別的一組不同的用戶端 `StockTickerHub` 。

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>Strongly-Typed 中樞

若要為您的中樞方法定義介面，讓用戶端可以參考 (並在您的中樞方法上啟用 Intellisense) ，請從 SignalR 2.1) 引進的 (衍生您的中樞， `Hub<T>` 而不是 `Hub` ：

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>如何定義用戶端可以呼叫的中樞類別中的方法

若要在中樞上公開您想要從用戶端呼叫的方法，請宣告公用方法，如下列範例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

您可以指定傳回型別和參數，包括複雜類型和陣列，就像在任何 c # 方法中一樣。 您在參數中接收或傳回給呼叫端的任何資料都會使用 JSON 在用戶端和伺服器之間進行通訊，而 SignalR 會自動處理複雜物件和物件陣列的系結。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 用戶端中方法名稱的 camel 大小寫

根據預設，JavaScript 用戶端會使用方法名稱的 camel 大小寫版本來參考中樞方法。 SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

如果您想要指定不同的名稱供用戶端使用，請加入 `HubMethodName` 屬性。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>非同步執行的時機

如果方法將會長時間執行或必須執行需要等候的工作（例如資料庫查閱或 web 服務呼叫），請傳回[工作 (取代](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)傳回 `void`) 或工作[ &lt; T &gt; ](https://msdn.microsoft.com/library/dd321424.aspx)物件 (來取代傳回類型) ，使中樞方法變成非同步 `T` 。 當您 `Task` 從方法傳回物件時，SignalR 會等待 `Task` 完成，然後將未包裝的結果傳送回用戶端，因此在用戶端中撰寫方法呼叫程式碼的方式並沒有任何差異。

使中樞方法變成非同步，可避免在使用 WebSocket 傳輸時封鎖連接。 當中樞方法以同步方式執行，而且傳輸為 WebSocket 時，在中樞方法完成之前，會封鎖從相同用戶端對中樞上的方法的後續調用。

下列範例顯示程式碼中，以同步或非同步方式執行的相同方法，後面接著用來呼叫任一版本的 JavaScript 用戶端程式代碼。

**同步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**非同步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

如需如何在 ASP.NET 4.5 中使用非同步方法的詳細資訊，請參閱 [使用 ASP.NET MVC 4 中的非同步方法](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="overloads"></a>

### <a name="defining-overloads"></a>定義多載

如果您想要定義方法的多載，則每個多載中的參數數目必須不同。 如果您只是藉由指定不同的參數類型來區分多載，則您的中樞類別將會編譯，但 SignalR 服務會在用戶端嘗試呼叫其中一個多載時，于執行時間擲回例外狀況。

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>從中樞方法調用報告進度

SignalR 2.1 新增了 .NET 4.5 中所引進 [進度報告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) 的支援。 若要執行進度報告，請 `IProgress<T>` 為您的用戶端可以存取的中樞方法定義一個參數：

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

撰寫長時間執行的伺服器方法時，請務必使用非同步程式設計模式（例如 Async/Await），而不是封鎖中樞執行緒。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>如何從中樞類別呼叫用戶端方法

若要從伺服器呼叫用戶端方法，請在 `Clients` 中樞類別的方法中使用屬性。 下列範例顯示在所有連線的用戶端上呼叫的伺服器程式碼 `addNewMessageToPage` ，以及在 JavaScript 用戶端中定義方法的用戶端程式代碼。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

叫用用戶端方法是非同步作業，並且會傳回 `Task` 。 使用 `await` ：

* 以確保訊息傳送時不會發生錯誤。 
* 啟用 try-catch 區塊中的攔截和處理錯誤。

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

您無法從用戶端方法取得傳回值。之類的語法 `int x = Clients.All.add(1,1)` 無法運作。

您可以指定參數的複雜類型和陣列。 下列範例會在方法參數中將複雜型別傳遞至用戶端。

**使用複雜物件呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**定義複雜物件的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>選取哪些用戶端將接收 RPC

用戶端屬性會傳回 [HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) 物件，這個物件會提供數個選項來指定要接收 RPC 的用戶端：

- 所有已連線的用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 只有呼叫的用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 所有用戶端（呼叫用戶端除外）。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 以連接識別碼識別的特定用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    此範例會 `addContosoChatMessageToPage` 在呼叫用戶端上呼叫，且具有與使用相同的效果 `Clients.Caller` 。
- 所有已連線的用戶端（指定的用戶端除外），以連接識別碼識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 指定群組中的所有已連線用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 指定群組中的所有已連線用戶端（指定的用戶端除外），以連接識別碼識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 指定群組中的所有已連線用戶端（呼叫用戶端除外）。

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- 依 userId 識別的特定使用者。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    根據預設，這是 `IPrincipal.Identity.Name` ，但可以藉由 [向全域主機註冊 IUserIdProvider 的執行](mapping-users-to-connections.md#IUserIdProvider)來變更。
- 連接識別碼清單中的所有用戶端和群組。

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 群組的清單。

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 依名稱的使用者。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
-  (在 SignalR 2.1) 引進的使用者名稱清單。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>沒有方法名稱的編譯時間驗證

您指定的方法名稱會被解釋為動態物件，這表示它沒有任何 IntelliSense 或編譯時期的驗證。 運算式會在執行時間進行評估。 當方法呼叫執行時，SignalR 會將方法名稱和參數值傳送至用戶端，而且如果用戶端具有符合名稱的方法，就會呼叫該方法，並將參數值傳遞給它。 如果在用戶端上找不到相符的方法，則不會引發錯誤。 如需在呼叫用戶端方法時，SignalR 在幕後傳送給用戶端之資料格式的詳細資訊，請參閱 [SignalR 簡介](../getting-started/introduction-to-signalr.md)。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>不區分大小寫的方法名稱比對

方法名稱比對不區分大小寫。 例如， `Clients.All.addContosoChatMessageToPage` 在伺服器上，伺服器將會在 `AddContosoChatMessageToPage` 用戶端上執行、 `addcontosochatmessagetopage` 或 `addContosoChatMessageToPage` 。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>非同步執行

您呼叫的方法會以非同步方式執行。 除非您指定後續的程式程式碼應等候方法完成，否則在方法呼叫至用戶端之後的任何程式碼都會立即執行，而不會等待 SignalR 完成將資料傳送到用戶端。 下列程式碼範例顯示如何依序執行兩個用戶端方法。

**使用 Await ( .NET 4.5) **

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

如果您使用 `await` 來等候用戶端方法在下一行程式碼執行之前完成，這並不表示用戶端會在下一行程式碼執行之前實際接收訊息。 用戶端方法呼叫的「完成」只表示 SignalR 已完成傳送訊息所需的所有專案。 如果您需要驗證用戶端是否已收到訊息，您必須自行設計該機制的程式。 例如，您可以在中樞上撰寫方法的程式碼 `MessageReceived` ，並在 `addContosoChatMessageToPage` 用戶端上的方法中， `MessageReceived` 執行您在用戶端上所需的任何工作。 在 `MessageReceived` 中樞內，您可以執行任何工作，取決於實際的用戶端接收和原始方法呼叫的處理。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>如何使用字串變數作為方法名稱

如果您想要使用字串變數做為方法名稱來叫用用戶端方法，請將 `Clients.All` (或 `Clients.Others` 、等 ) 轉換 `Clients.Caller` 為 `IClientProxy` ，然後再呼叫 [invoke (方法名稱、args ... ) ](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>如何從中樞類別管理群組成員資格

SignalR 中的群組提供一種方法，可將訊息廣播至指定的已連線用戶端子集。 群組可以有任意數目的用戶端，而用戶端可以是任意數量群組的成員。

若要管理群組成員資格，請使用中樞類別的屬性所提供的 [新增](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 和 [移除](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 方法 `Groups` 。 下列範例 `Groups.Add` `Groups.Remove` 會顯示在用戶端程式代碼所呼叫的中樞方法中所使用的和方法，後面接著會呼叫它們的 JavaScript 用戶端程式代碼。

**伺服器**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**使用產生的 proxy 的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

您不需要明確建立群組。 實際上，當您第一次在的呼叫中指定群組的名稱時，系統會自動建立群組 `Groups.Add` ，而且當您從成員的成員資格中移除最後一個連接時，就會將它刪除。

沒有 API 可取得群組成員資格清單或群組清單。 SignalR 會根據 [pub/sub 模型](http://en.wikipedia.org/wiki/Publish/subscribe)，將訊息傳送至用戶端和群組，而且伺服器不會維護群組或群組成員資格的清單。 這有助於將擴充性最大化，因為每當您將節點新增至 web 伺服陣列時，SignalR 維護的任何狀態都必須傳播到新的節點。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>非同步執行加入和移除方法

`Groups.Add`和 `Groups.Remove` 方法會以非同步方式執行。 如果您想要將用戶端新增至群組，並使用群組立即將訊息傳送至用戶端，您必須確定該 `Groups.Add` 方法會先完成。 下列程式碼範例示範如何執行這項作業。

**將用戶端新增至群組，然後將用戶端訊息傳送至**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>群組成員資格持續性

SignalR 會追蹤連接（而不是使用者），因此，如果您希望使用者在每次建立連線時都在相同的群組中，您必須在 `Groups.Add` 每次使用者建立新的連線時呼叫。

暫時中斷連線之後，有時 SignalR 可以自動還原連接。 在此情況下，SignalR 會還原相同的連線，而不是建立新的連線，因此會自動還原用戶端的群組成員資格。 這種情況可能是因為伺服器重新開機或失敗的原因是因為每個用戶端的線上狀態（包括群組成員資格）都是對用戶端的往返。 如果伺服器在連接逾時之前停止並由新的伺服器所取代，用戶端可以自動重新連接到新的伺服器，然後重新註冊其所屬的群組。

當連線無法在連接中斷之後、連線超時或用戶端 (中斷連線時，如果無法自動還原，例如，當瀏覽器流覽至新頁面) 時，群組成員資格會遺失。 下一次使用者連線時，將會是新的連接。 若要在相同的使用者建立新連接時維護群組成員資格，您的應用程式必須追蹤使用者和群組之間的關聯，並在每次使用者建立新連線時還原群組成員資格。

如需有關連接和重新連接的詳細資訊，請參閱本主題稍後 [的如何處理中樞類別中的連接存留期事件](#connectionlifetime) 。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>單一使用者群組

使用 SignalR 的應用程式通常必須追蹤使用者與連線之間的關聯，才能知道哪些使用者已傳送訊息，以及哪個使用者 (s) 應該接收訊息。 群組是用來執行這項操作的兩個常用模式之一。

- 單一使用者群組。

    您可以指定使用者名稱做為組名，並在每次使用者連接或重新連接時，將目前的連接識別碼加入至群組。 傳送訊息給您傳送到群組的使用者。 此方法的缺點是，群組不會提供您找出使用者是否在線上或離線狀態的方法。
- 追蹤使用者名稱與連接識別碼之間的關聯。

    您可以將每個使用者名稱和一或多個連接識別碼之間的關聯儲存在字典或資料庫中，並在每次使用者連接或中斷連線時，更新儲存的資料。 若要將訊息傳送給使用者，您必須指定連接識別碼。 這種方法的缺點是它需要更多的記憶體。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>如何處理中樞類別中的連接存留期事件

處理連接存留期事件的一般原因是追蹤使用者是否已連接，以及追蹤使用者名稱與連接識別碼之間的關聯。 若要在用戶端連線或中斷連線時執行自己的程式碼，請覆寫 `OnConnected` `OnDisconnected` 中樞類別的、和 `OnReconnected` 虛擬方法，如下列範例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>當呼叫 OnConnected、OnDisconnected 和 OnReconnected 時

每次瀏覽器導覽至新的頁面時，都必須建立新的連接，這表示 SignalR 會執行 `OnDisconnected` 方法，然後再執行 `OnConnected` 方法。 建立新連接時，SignalR 一律會建立新的連接識別碼。

`OnReconnected`當 SignalR 可以自動復原的連線中斷時，就會呼叫方法，例如在連接逾時之前，纜線暫時中斷連線並重新連線。`OnDisconnected`當用戶端已中斷連線，而 SignalR 無法自動重新連線時（例如當瀏覽器流覽至新頁面時），就會呼叫方法。 因此，指定用戶端的可能事件順序為 `OnConnected` 、 `OnReconnected` 、 `OnDisconnected` 或 `OnConnected` `OnDisconnected` 。 您將不會看到 `OnConnected` `OnDisconnected` `OnReconnected` 指定連接的順序。

`OnDisconnected`在某些情況下，不會呼叫此方法，例如當伺服器停止運作或回收應用程式網域時。 當另一部伺服器上線或應用程式域完成回收時，某些用戶端可能會重新連線並引發 `OnReconnected` 事件。

如需詳細資訊，請參閱 [瞭解及處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>未填入呼叫端狀態

連接存留期事件處理常式方法是從伺服器呼叫，這表示您放在用戶端物件中的任何狀態 `state` 都不會填入 `Caller` 伺服器上的屬性。 如需 `state` 物件和屬性的相關資訊 `Caller` ，請參閱本主題稍後的 [如何在用戶端與中樞類別之間傳遞狀態](#passstate) 。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>如何從內容屬性取得用戶端的相關資訊

若要取得用戶端的相關資訊，請使用 `Context` 中樞類別的屬性。 屬性會傳回 `Context` [HubCallerCoNtext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) 物件，此物件可讓您存取下列資訊：

- 呼叫用戶端的連線識別碼。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    連接識別碼是 SignalR 所指派的 GUID (您無法在自己的程式碼) 中指定值。 每個連線都有一個連線識別碼，如果您的應用程式中有多個中樞，則所有中樞都使用相同的連接識別碼。
- HTTP 標頭資料。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    您也可以從取得 HTTP 標頭 `Context.Headers` 。 多個參考相同內容的原因是 `Context.Headers` 先建立， `Context.Request` 稍後再加入屬性，並 `Context.Headers` 保留以提供回溯相容性。
- 查詢字串資料。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    您也可以從取得查詢字串資料 `Context.QueryString` 。

    您在這個屬性中取得的查詢字串，就是與建立 SignalR 連接的 HTTP 要求搭配使用的查詢字串。 您可以藉由設定連接將查詢字串參數新增至用戶端，這是將用戶端的相關資料從用戶端傳遞至伺服器的便利方式。 下列範例示範當您使用產生的 proxy 時，在 JavaScript 用戶端中加入查詢字串的其中一種方式。

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    如需有關設定查詢字串參數的詳細資訊，請參閱 [JavaScript](hubs-api-guide-javascript-client.md) 和 [.net](hubs-api-guide-net-client.md) 用戶端的 API 指南。

    您可以在查詢字串資料中找到用於連接的傳輸方法，以及 SignalR 內部使用的一些其他值：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    的值 `transportMethod` 將會是 "websocket"、"serverSentEvents"、"foreverFrame" 或 "longPolling"。 請注意，如果您在 `OnConnected` 事件處理常式方法中檢查此值，在某些情況下，您可能一開始會取得不是連接最後一個協商的傳輸方法的傳輸值。 在這種情況下，方法會擲回例外狀況，並在建立最後一個傳輸方法時，稍後再呼叫。
- Cookie。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    您也可以從取得 cookie `Context.RequestCookies` 。
- 使用者資訊。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 要求的 HttpCoNtext 物件：

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    使用這個方法，而不是 `HttpContext.Current` 取得 `HttpContext` SignalR 連接的物件。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>如何在用戶端與中樞類別之間傳遞狀態

用戶端 proxy 會提供一個 `state` 物件，您可以在其中儲存您想要透過每個方法呼叫傳送到伺服器的資料。 在伺服器上，您可以在 `Clients.Caller` 用戶端呼叫的中樞方法的屬性中存取此資料。 `Clients.Caller`連接存留期事件處理常式方法、和不會填入 `OnConnected` 屬性 `OnDisconnected` `OnReconnected` 。

建立或更新物件中的資料 `state` ，而 `Clients.Caller` 屬性則以雙向方式運作。 您可以補救伺服器中的值，並將它們傳回給用戶端。

下列範例示範 JavaScript 用戶端程式代碼，該程式碼會使用每個方法呼叫來儲存傳輸至伺服器的狀態。

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

下列範例顯示 .NET 用戶端中的對等程式碼。

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

在您的中樞類別中，您可以存取屬性中的這項資料 `Clients.Caller` 。 下列範例顯示的程式碼可抓取上一個範例中所參考的狀態。

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 保存狀態的這個機制不適合大量的資料，因為您放入或屬性中的所有 `state` 專案 `Clients.Caller` 都會隨著每個方法調用而往返。 它適用于較小的專案，例如使用者名稱或計數器。

在 VB.NET 或強型別中樞中，無法透過存取呼叫端狀態物件， `Clients.Caller` 而是使用 `Clients.CallerState` SignalR 2.1) 中引進的 (：

**在 C 中使用 CallerState#**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**在 Visual Basic 中使用 CallerState**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>如何處理中樞類別中的錯誤

若要處理中樞類別方法中發生的錯誤，請先確定您「觀察」非同步作業的任何例外狀況 (例如使用) 的用戶端方法 `await` 。 然後使用下列一或多個方法：

- 將您的方法程式碼包裝在 try-catch 區塊中，並記錄例外狀況物件。 基於偵錯工具的目的，您可以將例外狀況傳送給用戶端，但基於安全性考慮，不建議將詳細資訊傳送至生產環境中的用戶端。
- 建立可處理 [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) 方法的中樞管線模組。 下列範例顯示記錄錯誤的管線模組，後面接著 Startup.cs 中的程式碼，可將模組插入中樞管線。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- 使用 `HubException` (在 SignalR 2) 引進的類別。 您可以從任何中樞調用擲回此錯誤。 此函 `HubError` 式會接受字串訊息，以及用來儲存額外錯誤資料的物件。 SignalR 會自動將例外狀況序列化，並將它傳送至用戶端，以用來拒絕或使中樞方法調用失敗。

    下列程式碼範例示範如何在中樞叫用期間擲回 `HubException` ，以及如何在 JavaScript 和 .net 用戶端上處理例外狀況。

    **示範 HubException 類別的伺服器程式碼**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **示範在中樞中擲回 HubException 回應的 JavaScript 用戶端程式代碼**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **示範在中樞中擲回 HubException 回應的 .NET 用戶端程式代碼**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

如需有關中樞管線模組的詳細資訊，請參閱本主題稍後的 [如何自訂中樞管線](#hubpipeline) 。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>如何啟用追蹤

若要啟用伺服器端追蹤，請將 system.string 元素新增至您的 Web.config 檔案，如下列範例所示：

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

當您在 Visual Studio 中執行應用程式時，您可以在 [ **輸出** ] 視窗中查看記錄。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>如何從中樞類別外部呼叫用戶端方法和管理群組

若要從不同于中樞類別的類別呼叫用戶端方法，請取得中樞之 SignalR 內容物件的參考，並使用該物件呼叫用戶端上的方法或管理群組。

下列範例 `StockTicker` 類別會取得內容物件、將它儲存在類別的實例、將類別實例儲存在靜態屬性中，然後使用 singleton 類別實例的內容， `updateStockPrice` 在連線到名為的中樞的用戶端上呼叫方法 `StockTickerHub` 。

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

如果您需要在長時間存留的物件中多次使用內容，請只取得參考一次，並加以儲存，而不是每次都重新取得。 一旦取得內容，可確保 SignalR 會依照您的中樞方法進行用戶端方法調用的相同順序，將訊息傳送至用戶端。 如需示範如何使用中樞的 SignalR 內容的教學課程，請參閱 [使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>呼叫用戶端方法

您可以指定要接收 RPC 的用戶端，但您的選項會比從中樞類別呼叫的選項少。 這是因為內容不會與用戶端的特定呼叫相關聯，因此任何需要知道目前連接識別碼的方法（例如 `Clients.Others` 、或 `Clients.Caller` ） `Clients.OthersInGroup` 都無法使用。 有下列選項可供使用：

- 所有已連線的用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 以連接識別碼識別的特定用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 所有已連線的用戶端（指定的用戶端除外），以連接識別碼識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 指定群組中的所有已連線用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 指定群組中的所有已連線用戶端（指定的用戶端除外），以連接識別碼識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

如果您要從中樞類別中的方法呼叫非中樞類別，您可以傳入目前的連接識別碼，並使用它搭配 `Clients.Client` 、 `Clients.AllExcept` 或 `Clients.Group` 來模擬 `Clients.Caller` 、 `Clients.Others` 或 `Clients.OthersInGroup` 。 在下列範例中， `MoveShapeHub` 類別會將連接識別碼傳遞給 `Broadcaster` 類別，讓 `Broadcaster` 類別可以模擬 `Clients.Others` 。

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>管理群組成員資格

針對管理群組，您有與中樞類別相同的選項。

- 將用戶端新增至群組

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 從群組移除用戶端

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>如何自訂中樞管線

SignalR 可讓您將自己的程式碼插入中樞管線。 下列範例顯示的自訂中樞管線模組會記錄從用戶端接收的每個傳入方法呼叫，以及在用戶端上叫用的傳出方法呼叫：

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs*檔案中的下列程式碼會註冊要在中樞管線中執行的模組：

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

您可以覆寫許多不同的方法。 如需完整清單，請參閱 [HubPipelineModule 方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。
