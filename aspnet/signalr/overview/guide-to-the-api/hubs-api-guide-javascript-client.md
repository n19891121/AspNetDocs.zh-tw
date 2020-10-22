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
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔提供在 JavaScript 用戶端（例如瀏覽器和 Windows Store (WinJS) 應用程式）中使用適用于 SignalR 第2版的中樞 API 的簡介。
>
> SignalR 中樞 API 可讓您進行遠端程序呼叫， (從伺服器到連線用戶端，以及從用戶端到伺服器的 Rpc) 。 在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。 在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。 SignalR 會為您處理所有用戶端對伺服器的配管。
>
> SignalR 也提供較低層級的 API，稱為「持續連線」。 如需 SignalR、中樞和持續連線的簡介，請參閱 [SignalR 簡介](../getting-started/introduction-to-signalr.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。 如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [產生的 proxy 以及它為您執行的工作](#genproxy)

    - [使用產生的 proxy 的時機](#cantusegenproxy)
- [用戶端設定](#clientsetup)

    - [如何參考動態產生的 proxy](#dynamicproxy)
    - [如何建立 SignalR 產生之 proxy 的實體檔案](#manualproxy)
- [如何建立連接](#establishconnection)

    - [hubConnection ( # A1 所建立的相同物件](#connequivalence)
    - [啟動方法的非同步執行](#asyncstart)
- [如何建立跨網域連接](#crossdomain)
- [如何設定連接](#configureconnection)

    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
- [如何取得中樞類別的 proxy](#getproxy)
- [如何在用戶端上定義伺服器可以呼叫的方法](#callclient)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連接存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何啟用用戶端記錄](#logging)

如需有關如何對伺服器或 .NET 用戶端進行程式設計的檔，請參閱下列資源：

- [SignalR 中樞 API 指南-伺服器](hubs-api-guide-server.md)
- [SignalR 中樞 API 指南-.NET 用戶端](hubs-api-guide-net-client.md)

SignalR 2 server 元件僅適用于 .NET 4.5 (但 .net 4.0) 上有適用于 SignalR 2 的 .NET 用戶端。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>產生的 proxy 以及它為您執行的工作

您可以使用或不使用 SignalR 為您產生的 proxy，程式設計 JavaScript 用戶端與 SignalR 服務通訊。 Proxy 為您提供的功能是簡化您用來連接的程式碼語法、撰寫伺服器呼叫的方法，以及呼叫伺服器上的方法。

當您撰寫程式碼來呼叫伺服器方法時，產生的 proxy 可讓您使用看起來像是執列區域函數的語法：您可以撰寫 `serverMethod(arg1, arg2)` 而不是 `invoke('serverMethod', arg1, arg2)` 。 如果您錯誤地出現伺服器方法名稱，產生的 proxy 語法也會啟用立即和智慧型的用戶端錯誤。 如果您手動建立定義 proxy 的檔案，也可以取得 IntelliSense 支援，以撰寫呼叫伺服器方法的程式碼。

例如，假設您在伺服器上有下列 Hub 類別：

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

下列程式碼範例顯示在 `NewContosoChatMessage` 伺服器上叫用方法，以及從伺服器接收方法調用時，JavaScript 程式碼的樣子 `addContosoChatMessageToPage` 。

**使用產生的 proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**沒有產生的 proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>使用產生的 proxy 的時機

如果您想要為伺服器所呼叫的用戶端方法註冊多個事件處理常式，則無法使用產生的 proxy。 否則，您可以選擇使用產生的 proxy，或不要根據您的程式碼撰寫喜好設定。 如果您選擇不使用它，就不需要在 `script` 用戶端程式代碼的元素中參考 "signalr/hub" URL。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

JavaScript 用戶端需要 jQuery 和 SignalR core JavaScript 檔案的參考。 JQuery 版本必須是1.6.4 版或主要版本，例如1.7.2 版、1.8.2 或1.9.1。 如果您決定使用產生的 proxy，也需要 SignalR 產生之 proxy JavaScript 檔案的參考。 下列範例顯示在使用產生的 proxy 的 HTML 網頁中，參考可能會顯示的樣子。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

這些參考必須包含在此順序中： jQuery first、SignalR core 之後，以及 SignalR proxy last。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>如何參考動態產生的 proxy

在上述範例中，SignalR 產生之 proxy 的參考是動態產生的 JavaScript 程式碼，而不是實體檔案。 SignalR 會即時建立 proxy 的 JavaScript 程式碼，並將它提供給用戶端，以回應 "/signalr/hubs" URL。 如果您在方法中為伺服器上的 SignalR 連接指定不同的基底 URL `MapSignalR` ，動態產生的 proxy 檔案的 URL 就是附加 "/hubs" 的自訂 url。

> [!NOTE]
> 針對 Windows 8 (Windows Store) JavaScript 用戶端，請使用實體 proxy 檔案，而不是動態產生的檔案。 如需詳細資訊，請參閱本主題稍後的 [如何為 SignalR 產生的 proxy 建立實體](#manualproxy) 檔案。

在 ASP.NET MVC 4 或 5 Razor view 中，使用波狀符號來參考 proxy 檔案參考中的應用程式根目錄：

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

如需在 MVC 5 中使用 SignalR 的詳細資訊，請參閱 [使用 SignalR 和 MVC 5 的消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

在 ASP.NET MVC 3 Razor view 中，使用 `Url.Content` 作為 proxy 檔案參考：

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

在 ASP.NET Web Forms 應用程式中， `ResolveClientUrl` 針對您的 proxy 檔案參考使用，或使用應用程式根目錄相對路徑 (（以波狀符號) 開始）透過 ScriptManager 進行註冊：

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

一般來說，使用相同的方法來指定用於 CSS 或 JavaScript 檔案的 "/signalr/hubs" URL。 如果您在不使用波狀符號的情況下指定 URL，在某些情況下，當您使用 IIS Express 在 Visual Studio 中進行測試時，您的應用程式將會正常運作，但當您部署至完整404的 IIS 時，將會失敗 如需詳細資訊，請參閱 MSDN 網站上的[針對 ASP.NET Web 專案在 Visual Studio 中解析 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)中**Root-Level 資源的參考**。

當您在 [偵測模式] 的 Visual Studio 2017 中執行 Web 專案時，如果使用 Internet Explorer 作為瀏覽器，您可以在 [**腳本**] 底下的**方案總管**中看到 proxy 檔案。

若要查看檔案的內容，請按兩下 [ **集線器**]。 如果您不是使用 Visual Studio 2012 或 Internet Explorer 2013，或不是處於「偵測」模式，也可以流覽至 "/signalR/hubs" URL 來取得檔案的內容。 例如，如果您的網站正在執行 `http://localhost:56699` ，請移至 `http://localhost:56699/SignalR/hubs` 瀏覽器中的。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>如何建立 SignalR 產生之 proxy 的實體檔案

作為動態產生之 proxy 的替代方案，您可以建立具有 proxy 程式碼的實體檔案並參考該檔案。 您可能會想要這樣做，以控制快取或組合行為，或在撰寫伺服器方法的呼叫程式碼時取得 IntelliSense。

若要建立 proxy 檔案，請執行下列步驟：

1. 安裝 [SignalR. 公用程式](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 套件。
2. 開啟命令提示字元，然後流覽至包含 SignalR.exe 檔案的 [ *tools* ] 資料夾。 [工具] 資料夾位於下列位置：

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 輸入下列命令：

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.Dll*的路徑通常是您專案資料夾中的*bin*資料夾。

    此命令會在與*signalr.exe*相同的資料夾中，建立名為*server.js*的檔案。
4. 將 *server.js* 檔案放在專案的適當資料夾中，將它重新命名為適用于您的應用程式，並在其中新增參考以取代 "signalr/hub" 參考。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連接

建立連接之前，您必須建立連線物件、建立 proxy，以及註冊可從伺服器呼叫之方法的事件處理常式。 設定 proxy 和事件處理常式時，請呼叫方法來建立連接 `start` 。

如果您使用產生的 proxy，則不需要在自己的程式碼中建立連線物件，因為產生的 proxy 程式碼會為您執行此工作。

<a id="nogenconnection"></a>

**建立與產生的 proxy (的連接) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**建立沒有產生之 proxy 的連接 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

根據預設，中樞位置是目前的伺服器;如果您要連接到不同的伺服器，請在呼叫方法之前指定 URL `start` ，如下列範例所示：

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 一般來說，您會先註冊事件處理常式，然後再呼叫 `start` 方法來建立連接。 如果您想要在建立連接之後註冊某些事件處理常式，您可以這樣做，但您必須在呼叫方法之前，先在) 中至少註冊一個事件處理常式 (`start` 。 其中一個原因是應用程式中可能會有許多中樞，但 `OnConnected` 如果您只是要使用其中一個中樞，就不會想要在每個中樞上觸發該事件。 建立連線時，中樞 proxy 上的用戶端方法是否存在會告知 SignalR 觸發 `OnConnected` 事件。 如果您未在呼叫方法之前註冊任何事件處理常式 `start` ，您將能夠在中樞上叫用方法，但不會呼叫中樞的方法，也不會 `OnConnected` 從伺服器叫用任何用戶端方法。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>hubConnection ( # A1 所建立的相同物件

如您在範例中所見，當您使用產生的 proxy 時，會 `$.connection.hub` 參考連線物件。 `$.hubConnection()`當您未使用產生的 proxy 時，就會呼叫這個相同的物件。 產生的 proxy 程式碼會藉由執行下列語句，為您建立連接：

![在產生的 proxy 檔案中建立連接](hubs-api-guide-javascript-client/_static/image3.png)

當您使用產生的 proxy 時，您可以使用連線物件來進行任何動作， `$.connection.hub` 而不是使用產生的 proxy。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>啟動方法的非同步執行

`start`方法會以非同步方式執行。 它會傳回 [JQuery 延遲的物件](http://api.jquery.com/category/deferred-object/)，這表示您可以藉由呼叫、和等方法來加入回呼函數 `pipe` `done` `fail` 。 如果您有想要在建立連接之後執行的程式碼，例如對伺服器方法的呼叫，請將該程式碼放在回呼函式中，或從回呼函數呼叫它。 `.done`回呼方法是在建立連接之後，以及 `OnConnected` 伺服器上的事件處理常式方法中的任何程式碼完成執行之後執行。

如果您將上述範例中的「立即連線」語句做為方法呼叫之後的下一行程式碼 `start` (不在 `.done` 回呼) 中，則 `console.log` 會在建立連接之前執行這一行，如下列範例所示：

![撰寫在建立連線後執行之程式碼的錯誤方式](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>如何建立跨網域連接

一般而言，如果瀏覽器從載入頁面 `http://contoso.com` ，SignalR 連接會位於相同的網域中 `http://contoso.com/signalr` 。 如果頁面無法 `http://contoso.com` 連接到 `http://fabrikam.com/signalr` ，則為跨網域連接。 基於安全性考慮，預設會停用跨網域連接。

在 SignalR 1.x 中，跨網域要求是由單一 EnableCrossDomain 旗標所控制。 此旗標會控制 JSONP 和 CORS 要求。 為了獲得更大的彈性，已從 SignalR 的伺服器元件中移除所有 CORS 支援 (如果偵測到瀏覽器支援) ，且已提供新的 OWIN 中介軟體以支援這些案例，則這些用戶端仍會正常使用 CORS。

如果用戶端 (需要 JSONP，以支援舊版瀏覽器中的跨網域要求) ，則必須將 `EnableJSONP` 物件上的設定設為，以明確地啟用它 `HubConfiguration` `true` ，如下所示。 JSONP 預設為停用，因為它比 CORS 更不安全。

**將 Owin 新增至您的專案：** 若要安裝此程式庫，請在封裝管理員主控台中執行下列命令：

`Install-Package Microsoft.Owin.Cors`

此命令會將2.1.0 版本的套件新增至您的專案。

### <a name="calling-usecors"></a>呼叫 UseCors

 下列程式碼片段示範如何在 SignalR 2 中執行跨網域連接。

**在 SignalR 2 中執行跨網域要求**

下列程式碼示範如何在 SignalR 2 專案中啟用 CORS 或 JSONP。 這個程式碼範例 `Map` 會使用和 `RunSignalR` 而不是 `MapSignalR` ，因此 cors 中介軟體只會針對需要 CORS 支援的 SignalR 要求執行，而不是針對中指定之路徑上的所有流量執行 (`MapSignalR` 。 ) 對應也可以用於任何其他需要針對特定 URL 前置詞執行的中介軟體，而不是整個應用程式。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 請勿 `jQuery.support.cors` 在程式碼中將設定為 true。
>
>     ![請勿將 jQuery 設定為 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR 會處理 CORS 的使用。 將設定 `jQuery.support.cors` 為 true 會停用 JSONP，因為它會導致 SignalR 假設瀏覽器支援 CORS。
> - 當您連線到 localhost URL 時，Internet Explorer 10 不會將它視為跨網域連線，因此即使您未在伺服器上啟用跨網域連線，應用程式還是會在本機使用 IE 10。
> - 如需有關搭配 Internet Explorer 9 使用跨網域連接的詳細資訊，請參閱 [這個 StackOverflow 執行緒](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。
> - 如需有關搭配使用跨網域連接與 Chrome 的詳細資訊，請參閱 [這個 StackOverflow 執行緒](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。
> - 範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連接

建立連接之前，您可以指定查詢字串參數，或指定傳輸方法。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果您想要在用戶端連接時將資料傳送至伺服器，您可以將查詢字串參數加入至連線物件。 下列範例示範如何在用戶端程式代碼中設定查詢字串參數。

**先設定查詢字串值，再使用產生的 proxy 呼叫 start 方法 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**在不使用產生的 proxy 呼叫開始方法 (之前，請先設定查詢字串值) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

下列範例示範如何在伺服器程式碼中讀取查詢字串參數。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

在連接的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端所支援的最佳傳輸。 如果您已經知道要使用哪一個傳輸，可以在呼叫方法時指定傳輸方法，以略過此協商程式 `start` 。

**用戶端程式代碼，指定與產生的 proxy (的傳輸方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**指定傳輸方法 (的用戶端程式代碼，不含產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

或者，您可以依照想要 SignalR 嘗試的順序來指定多個傳輸方法：

**指定與產生的 proxy (的自訂傳輸回溯配置的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**指定自訂傳輸回溯配置的用戶端程式代碼 (沒有產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

您可以使用下列值來指定傳輸方法：

- Websocket
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

下列範例會示範如何找出連接所使用的傳輸方法。

**用戶端程式代碼，顯示連接 (與產生的 proxy 所使用的傳輸方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**用戶端程式代碼，顯示連接 (所使用的傳輸方法，不含產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱 [ASP.NET SignalR 中樞 API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。 如需傳輸和回退的詳細資訊，請參閱 [SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>如何取得中樞類別的 proxy

您建立的每個連線物件都會封裝與包含一或多個中樞類別的 SignalR 服務連線相關的資訊。 若要與中樞類別通訊，請使用您自己建立的 proxy 物件 (如果您不是使用產生的 proxy) 或為您產生的 proxy。

在用戶端上，proxy 名稱是中樞類別名稱的 camel 大小寫版本。 SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**取得針對中樞所產生之用戶端 proxy 的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**建立中樞類別 (的用戶端 proxy，而不產生 proxy) **

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

如果您使用屬性裝飾您的中樞類別 `HubName` ，請使用完整名稱，而不變更大小寫。

**伺服器上具有 HubName 屬性的中樞類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**取得針對中樞所產生之用戶端 proxy 的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**建立中樞類別 (的用戶端 proxy，而不產生 proxy) **

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在用戶端上定義伺服器可以呼叫的方法

若要定義伺服器可以從中樞呼叫的方法，請使用所產生之 proxy 的屬性將事件處理常式新增至中樞 proxy `client` ，或者， `on` 如果您未使用產生的 proxy，請呼叫方法。 這些參數可以是複雜的物件。

先加入事件處理常式，然後再呼叫 `start` 方法來建立連接。  (如果您要在呼叫方法之後新增事件處理常式 `start` ，請參閱本檔前面 [如何建立連接](#establishconnection) 的附注，並使用所示的語法來定義方法，而不使用產生的 proxy。 ) 

方法名稱比對不區分大小寫。 例如， `Clients.All.addContosoChatMessageToPage` 在伺服器上，伺服器將會在 `AddContosoChatMessageToPage` 用戶端上執行、 `addContosoChatMessageToPage` 或 `addcontosochatmessagetopage` 。

**使用產生的 proxy 定義用戶端 (上的方法) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**使用產生的 proxy 在用戶端 (上定義方法的替代方式) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**在用戶端 (上定義不含產生之 proxy 的方法，或在呼叫 start 方法之後新增時) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

下列範例包含複雜物件做為方法參數。

**在用戶端上定義方法，該方法會採用複雜物件 (與產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**在用戶端上定義方法，此方法會採用複雜物件 (沒有產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**定義複雜物件的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**使用複雜物件呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

若要從用戶端呼叫伺服器方法，請使用所 `server` 產生之 proxy 的屬性或 `invoke` 中樞 proxy 上的方法（如果您未使用產生的 proxy）。 傳回值或參數可以是複雜的物件。

傳入中樞上方法名稱的 camel 大小寫版本。 SignalR 會自動進行這種變更，讓 JavaScript 程式碼符合 JavaScript 慣例。

下列範例示範如何呼叫沒有傳回值的伺服器方法，以及如何呼叫有傳回值的伺服器方法。

**沒有 HubMethodName 屬性的伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**定義在參數中傳遞之複雜物件的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

如果您使用屬性裝飾中樞方法 `HubMethodName` ，請使用該名稱，而不變更大小寫。

具有 HubMethodName 屬性的**伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

上述範例示範如何呼叫沒有傳回值的伺服器方法。 下列範例示範如何呼叫具有傳回值的伺服器方法。

**具有傳回值之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

用於傳回值的**Stock 類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**使用產生的 proxy 叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**在沒有產生的 proxy 的情況下，叫用伺服器方法 (的用戶端程式代碼) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連接存留期事件

SignalR 提供下列可供您處理的連接存留期事件：

- `starting`：在透過連接傳送任何資料之前引發。
- `received`：在連接上收到任何資料時引發。 提供接收的資料。
- `connectionSlow`：當用戶端偵測到緩慢或經常中斷連接時引發。
- `reconnecting`：當基礎傳輸開始重新連接時引發。
- `reconnected`：當基礎傳輸重新連接時引發。
- `stateChanged`：當連接狀態變更時引發。 提供舊狀態和新狀態 (連接、連線、重新連線或中斷連線) 。
- `disconnected`：連接中斷連接時引發。

例如，如果您想要在有可能造成明顯延遲的連接問題時顯示警告訊息，請處理 `connectionSlow` 事件。

**使用產生的 proxy 來處理 connectionSlow 事件 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**處理 connectionSlow 事件 (而不需要產生的 proxy) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

如需詳細資訊，請參閱 [瞭解及處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

SignalR JavaScript 用戶端會提供 `error` 您可以為其新增處理常式的事件。 您也可以使用 fail 方法來加入伺服器方法調用所產生之錯誤的處理常式。

如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 在錯誤之後傳回的例外狀況物件會包含錯誤的最基本資訊。 例如，如果的呼叫 `newContosoChatMessage` 失敗，則錯誤物件中的錯誤訊息會包含「」 `There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.` 基於安全性理由，不建議在生產環境中傳送詳細的錯誤訊息給用戶端，但如果您想要啟用詳細的錯誤訊息以進行疑難排解，請在伺服器上使用下列程式碼。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

下列範例顯示如何加入錯誤事件的處理常式。

**使用產生的 proxy 加入錯誤處理常式 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**在沒有產生的 proxy 的情況下新增錯誤處理常式 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

下列範例顯示如何處理方法調用的錯誤。

**使用產生的 proxy 處理方法調用 (的錯誤) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**在沒有產生的 proxy 的情況下，處理方法調用 (的錯誤) **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

如果方法調用失敗， `error` 也會引發事件，因此您在 `error` 方法處理常式和方法回呼中的程式碼 `.fail` 都會執行。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何啟用用戶端記錄

若要啟用連接的用戶端記錄，請先在 `logging` 連線物件上設定屬性，然後再呼叫 `start` 方法來建立連接。

**使用產生的 proxy 啟用記錄 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**不使用產生的 proxy 來啟用記錄 () **

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

若要查看記錄，請開啟瀏覽器的開發人員工具，並移至 [主控台] 索引標籤。如需示範如何執行這項操作的逐步指示和螢幕擷取畫面的教學課程，請參閱 [使用 ASP.NET Signalr 進行伺服器廣播-啟用記錄](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。
