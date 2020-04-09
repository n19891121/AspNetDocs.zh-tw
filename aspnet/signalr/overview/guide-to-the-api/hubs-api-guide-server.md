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
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a>ASP.NET訊號器集線器 API 指南 - 伺服器 (C#)

由[派翠克·弗萊徹](https://github.com/pfletcher),[湯姆·戴克斯特拉](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文件介紹了為 SignalR 版本 2 編寫ASP.NET訊號R 集線器 API 的伺服器端,並演示了常見選項的代碼示例。
> 
> SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。 在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。 在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。 SignalR 為您處理所有用戶端到伺服器管道。
> 
> SignalR 還提供稱為持久連接的較低級別的 API。 有關信號R、集線器和持久連接的介紹,請參閱[訊號R 2 簡介](../getting-started/introduction-to-signalr.md)。
> 
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - 信號R版本 2
>   
> 
> 
> ## <a name="topic-versions"></a>主題版本
> 
> 有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。
> 
> ## <a name="questions-and-comments"></a>問題和評論
> 
> 請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。 如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [如何註冊SignalR中間件](#route)

    - [/信號器網址](#signalrurl)
    - [設定訊號](#options)
- [如何建立與使用中心類別](#hubclass)

    - [中心物件存留期](#transience)
    - [JavaScript 用戶端中中心名稱的駱駝大小寫](#hubnames)
    - [多個中心](#multiplehubs)
    - [強類型集線器](#stronglytypedhubs)
- [如何在中心類別定義客戶端可以呼叫的方法](#hubmethods)

    - [JavaScript 用戶端中方法名稱的駱駝大小寫](#methodnames)
    - [何時同步執行](#asyncmethods)
    - [定義重載](#overloads)
    - [報告中心方法呼叫進度](#progress)
- [如何從中心類調用用戶端方法](#callfromhub)

    - [選擇哪些用戶端將收到 RPC](#selectingclients)
    - [方法名稱沒有編譯時間驗證](#dynamicmethodnames)
    - [區分大小寫的方法名稱符合](#caseinsensitive)
    - [非同步執行](#asyncclient)
- [如何從中心類管理組成員身份](#groupsfromhub)

    - [新增與移除方法的非同步](#asyncgroupmethods)
    - [群組成員身份持久性](#grouppersistence)
    - [單使用者群組](#singleusergroups)
- [如何處理集線器類別的連線存留期事件](#connectionlifetime)

    - [當"連接"時,打開斷開狀態,並調用"重新連接"](#onreconnected)
    - [未填滿的呼叫者狀態](#nocallerstate)
- [如何從內容取得有關用戶端的資訊](#contextproperty)
- [如何在用戶端和中心類之間傳遞狀態](#passstate)
- [如何處理中心類別的錯誤](#handleErrors)
- [如何呼叫用戶端方法並管理來自中心類外部的群組](#callfromoutsidehub)

    - [呼叫用戶端方法](#callingclientsoutsidehub)
    - [管理群組成員身份](#managinggroupsoutsidehub)
- [如何開啟追蹤](#tracing)
- [如何自訂中心管道](#hubpipeline)

有關如何對客戶端進行程式設計的文件,請參閱以下資源:

- [信號器中心 API 指南 - JavaScript 用戶端](hubs-api-guide-javascript-client.md)
- [信號器集線器 API 指南 - .NET 用戶端](hubs-api-guide-net-client.md)

SignalR 2 的伺服器元件僅在 .NET 4.5 中可用。 運行 .NET 4.0 的伺服器必須使用 SignalR v1.x。

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a>如何註冊SignalR中間件

要定義用戶端將用於連接到集線器的路由,請在`MapSignalR`應用程式啟動時調用方法。 `MapSignalR`是類別的`OwinExtensions`[擴充方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。 下面的範例展示如何使用OWIN啟動類定義SignalR中心路由。

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

如果要將 SignalR 功能添加到 ASP.NET MVC 應用程式,請確保在其他路由之前添加 SignalR 路由。 有關詳細資訊,請參閱[教程:開始使用 SignalR 2 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a>/信號器網址

默認情況下,用戶端將用於連接到集線器的路由網址為"/信號器"。 (不要將此網址與"/信號器/集線器"URL 混淆,該 URL 適用於自動生成的 JAVAScript 檔案。 有關產生的代理的詳細資訊,請參閱[SignalR 中心 API 指南 - JAvaScript 用戶端 - 產生的代理及其為您做什麼](hubs-api-guide-javascript-client.md#genproxy)。

可能存在異常情況,使此基 URL 不適用於 SignalR;例如,專案中有一個名為*信號器*的資料夾,並且不想更改名稱。 在這種情況下,您可以更改基本 URL,如以下範例所示(將範例代碼中的"/信號器"替換為所需的 URL)。

**指定網址的伺服器碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

**指定網址的 JavaScript 用戶端碼(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

**指定網址的 JavaScript 用戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

**指定 URL 的 .NET 客戶端碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a>設定訊號設定選項

`MapSignalR`方法的重載讓您能夠指定自訂網址、自訂依賴項解析器以及以下選項:

- 使用瀏覽器用戶端的 CORS 或 JSONP 啟用跨域調用。

    通常,如果瀏覽器從`http://contoso.com`載入頁面,則 SignalR 連接位於同一`http://contoso.com/signalr`域中 ,在 。 如果中的`http://contoso.com`頁面與`http://fabrikam.com/signalr`斷開連接,則為跨域連接。 出於安全原因,默認情況下禁用跨域連接。 有關詳細資訊,請參閱[ASP.NET 訊號R中心 API 指南 - JAvaScript 用戶端 - 如何建立跨網域連接](hubs-api-guide-javascript-client.md#crossdomain)。
- 啟用詳細的錯誤訊息。

    發生錯誤時,SignalR 的默認行為是向用戶端發送通知消息,而不詳細說明發生的情況。 在生產中不建議向用戶端發送詳細的錯誤資訊,因為惡意使用者可能能夠在針對應用程式的攻擊中使用該資訊。 對於故障排除,可以使用此選項暫時啟用資訊量更大的錯誤報告。
- 關閉自動產生的 JavaScript 代理檔。

    默認情況下,將生成具有中心類代理的 JavaScript 檔,以回應 URL"/信號器/集線器"。 如果不想使用 JavaScript 代理,或者要手動生成此檔並引用用戶端中的物理檔案,則可以使用此選項禁用代理生成。 有關詳細資訊,請參閱[SignalR 中心 API 指南 - JavaScript 用戶端 - 如何為 SignalR 產生的代理產生實體檔](hubs-api-guide-javascript-client.md#manualproxy)。

下面的範例展示如何在調用`MapSignalR`方法中指定 SignalR 連接 URL 和這些選項。 要指定自定義 URL,請將範例中的"/信號器" 取代為要使用的網址。

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a>如何建立與使用中心類別

要建立集線器,請創建一個派生自[Microsoft 的類。](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) 下面的示例顯示了聊天應用程式的簡單中心類。

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

在此示例中,連接的用戶端可以調用`NewContosoChatMessage`方法,當它調用時,接收的數據將廣播到所有連接的用戶端。

<a id="transience"></a>

### <a name="hub-object-lifetime"></a>中心物件存留期

您不會實例化 Hub 類,也不會從伺服器上自己的代碼調用其方法;否則,您就不會實例化 Hub 類,所有由 SignalR 中心管道為您完成。 SignalR 在每次需要處理集線器操作(例如用戶端連接、斷開連接或對伺服器進行方法調用時)時,都會創建 Hub 類的新實例。

由於 Hub 類的實例是暫時性的,因此不能使用它們來維護從一個方法調用到下一個方法的狀態。 每次伺服器收到來自用戶端的方法調用時,Hub 類的新實例都會處理該消息。 要通過多個連接和方法調用維護狀態,請使用其他方法,如資料庫或 Hub 類上的靜態變數,或者不派生`Hub`自的不同類。 如果在記憶體中保留數據,使用 Hub 類上靜態變數等方法,則當應用域回收時,數據將丟失。

如果要從在 Hub 類之外運行的您自己的代碼向用戶端發送消息,不能通過實例化 Hub 類實例來執行此操作,但可以通過獲取對 Hub 類的 SignalR 上下文物件的引用來執行此操作。 有關詳細資訊,請參閱本主題稍後在[中心類外部呼叫用戶端方法和管理組](#callfromoutsidehub)。

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a>JavaScript 用戶端中中心名稱的駱駝大小寫

默認情況下,JavaScript 用戶端使用類名稱的駱駝大小寫版本引用集線器。 SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。 前面的範例將稱為`contosoChatHub`JavaScript 代碼。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

如果要為用戶端指定要使用的其他名稱,請添加該`HubName`屬性。 使用`HubName`屬性時,JAVAScript 用戶端上不會更改駱駝大小寫的名稱。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a>多個中心

您可以在應用程式中定義多個中心類。 執行此操作時,連線是共用的,但組是獨立的:

- 所有用戶端都將使用相同的 URL 與服務建立 SignalR 連接("/信號器" 或自訂網址(如果您指定了一個),並且該連接用於服務定義的所有中心。

    與在單個類中定義所有中心功能相比,多個中心的性能差異沒有差異。
- 所有中心都獲取相同的 HTTP 請求資訊。

    由於所有集線器共用相同的連接,因此伺服器獲得的唯一 HTTP 請求資訊是建立 SignalR 連接的原始 HTTP 請求中的內容。 如果使用連線請求透過指定查詢字串將資訊從客戶端傳遞到伺服器,則不能向不同的中心提供不同的查詢字串。 所有中心都將收到相同的資訊。
- 生成的 JavaScript 代理檔將包含一個檔中所有中心代理。

    有關 JavaScript 代理的資訊,請參閱[SignalR 中心 API 指南 - JavaScript 客戶端 - 產生的代理及其為您做什麼](hubs-api-guide-javascript-client.md#genproxy)。
- 組在中心內定義。

    在 SignalR 中,您可以定義要廣播到連接用戶端子集的命名組。 每個中心分別維護組。 例如,名為「管理員」的組將包含類`ContosoChatHub`的一組用戶端,而相同的組名稱將引用`StockTickerHub`類的不同用戶端集。

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a>強類型集線器

要為用戶端可以引用的集線器方法定義介面(並在集線器方法上啟用 Intellisense),請`Hub<T>`從 (在 SignalR`Hub`2.1 中 引入) 而不是 派生中心。

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a>如何在中心類別定義客戶端可以呼叫的方法

要在 Hub 上公開要從用戶端調用的方法,請聲明公共方法,如以下示例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

您可以指定返回類型和參數,包括複雜類型和陣列,就像在任何 C# 方法中一樣。 使用 JSON 在用戶端和伺服器之間通訊以參數接收或返回到調用方的任何數據,SignalR 會自動處理複雜物件和物件數組的綁定。

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a>JavaScript 用戶端中方法名稱的駱駝大小寫

默認情況下,JavaScript 用戶端使用方法名稱的駱駝大小寫版本引用 Hub 方法。 SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

如果要為用戶端指定要使用的其他名稱,請添加該`HubMethodName`屬性。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a>何時同步執行

如果該方法將長時間運行或必須執行需要等待的工作(如資料庫查找或 Web 服務呼叫),則[Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)透過傳回`void`任務 (代替返回)或[Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx)物件(代替`T`返回類型)使 Hub 方法非同步。 當您從方法`Task`返回物件時,SignalR 會`Task`等待 完成,然後它將未包裝的結果發送回用戶端,因此在用戶端中編寫方法調用的代碼沒有區別。

使集線器方法非同步可避免使用 WebSocket 傳輸時阻塞連接。 當集線器方法同步執行且傳輸為 WebSocket 時,從同一用戶端在集線器上調用方法將被阻止,直到中心方法完成。

下面的範例顯示編碼為同步或非同步執行的相同方法,然後是適用於調用任一版本的 JavaScript 客戶端碼。

**同步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

**非同步**

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

有關如何在 ASP.NET 4.5 中使用非同步方法的詳細資訊,請參閱[在 mVC 4 中使用非同步方法 ASP.NET](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。

<a id="overloads"></a>

### <a name="defining-overloads"></a>定義重載

如果要為方法定義重載,則每個重載中的參數數必須不同。 如果僅通過指定不同的參數類型來區分重載,則 Hub 類將編譯,但當客戶端嘗試調用其中一個重載時,SignalR 服務將在運行時引發異常。

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a>報告中心方法呼叫進度

SignalR 2.1 添加了對 .NET 4.5 中引入[的進度報告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)的支援。 要實現進度報告,請為`IProgress<T>`用戶端可以存取的集線器方法定義參數:

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

編寫長時間運行的伺服器方法時,使用非同步程式設計模式(如 Async/Await)而不是阻止中心線程非常重要。

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a>如何從中心類調用用戶端方法

要從伺服器呼叫用戶端方法,`Clients`請使用 Hub 類中方法中的 屬性。 下面的範例顯示呼叫`addNewMessageToPage`所有連接的用戶端的伺服器代碼,以及定義 JavaScript 用戶端中方法的用戶端代碼。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

呼叫客戶端方法是非同步操作,並傳`Task`回 。 使用`await`:

* 確保消息發送時沒有錯誤。 
* 啟用在嘗試捕獲塊中捕獲和處理錯誤。

**使用產生的代理的 JavaScript 用戶端**

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

無法從用戶端方法獲取返回值;因此,無法從用戶端方法獲取返回值。語法,如`int x = Clients.All.add(1,1)`不工作。

您可以為參數指定複雜的類型和陣列。 下面的示例將複雜類型傳遞給方法參數中的用戶端。

**使用複雜物件呼叫用戶端方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

**定義複雜物件的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a>選擇哪些用戶端將收到 RPC

用戶端屬性傳回[HubConnectionConnection 物件](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx),該物件提供了多個選項來指定哪些用戶端將接收 RPC:

- 所有已連線的用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- 僅調用用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- 除調用用戶端之外的所有用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- 由連接 ID 標識的特定用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    此示例調用`addContosoChatMessageToPage`調用客戶端,並且`Clients.Caller`與使用具有相同的效果。
- 除指定客戶端外的所有連接用戶端,由連接 ID 標識。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- 指定組中的所有連接用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- 指定群組中的所有連接客戶端(指定用戶端除外),由連接 ID 識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- 指定群組中的所有已連接客戶端(呼叫用戶端除外)。

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- 使用者 Id 識別的特定使用者。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    默認情況下,這是`IPrincipal.Identity.Name`,但可以通過[向全域主機註冊 IUserIdProvider 的實現](mapping-users-to-connections.md#IUserIdProvider)來更改。
- 連接指示清單中的所有用戶端和組。

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- 組的清單。

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- 按名稱命名的使用者。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- 使用者名清單(在 SignalR 2.1 中介紹)。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a>方法名稱沒有編譯時間驗證

您指定的方法名稱被解釋為動態物件,這意味著沒有 IntelliSense 或編譯時間驗證。 表達式在運行時計算。 當方法調用執行時,SignalR 會將方法名稱和參數值發送到用戶端,如果用戶端具有與該名稱匹配的方法,則調用該方法並將參數值傳遞給它。 如果在用戶端上找不到匹配方法,則不引發錯誤。 有關 SignalR 呼叫客戶端方法時在後台傳輸到客戶端的資料格式的資訊,請參閱[SignalR 簡介](../getting-started/introduction-to-signalr.md)。

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a>區分大小寫的方法名稱符合

方法名稱匹配不區分大小寫。 例如,`Clients.All.addContosoChatMessageToPage`在伺服器上將`AddContosoChatMessageToPage`執行`addcontosochatmessagetopage`、`addContosoChatMessageToPage`或在用戶端上。

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a>非同步執行

調用的方法以異步方式執行。 對用戶端進行方法調用後出現的任何代碼將立即執行,而無需等待 SignalR 完成向用戶端傳輸數據,除非您指定後續代碼行應等待方法完成。 下面的代碼示例演示如何按順序執行兩個用戶端方法。

**使用 Await (.NET 4.5)**

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

如果使用等待`await`用戶端方法在下一行代碼執行之前完成,這並不意味著用戶端將在執行下一行代碼之前實際收到消息。 用戶端方法呼叫的「完成」僅意味著 SignalR 已執行發送消息所需的一切。 如果您需要驗證用戶端是否收到該消息,您必須自己對該機制進行程式設計。 例如,您可以在 Hub`MessageReceived`上 編寫方法代碼,`addContosoChatMessageToPage`在用戶端上 編寫方法後,您可以在`MessageReceived`執行需要在用戶端 上執行的任何工作後調用。 在`MessageReceived`Hub 中,您可以執行依賴於原始方法調用的實際用戶端接收和處理的任何工作。

### <a name="how-to-use-a-string-variable-as-the-method-name"></a>如何使用字串變數作為方法名稱

如果要使用字串變數作為方法名稱呼叫用戶端方法,則強制`Clients.All`(或`Clients.Others`、等`Clients.Caller`)呼叫`IClientProxy` [Invoke(方法名稱、args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a>如何從中心類管理組成員身份

SignalR 中的組提供了一種將消息廣播到連接客戶端的指定子集的方法。 組可以具有任意數量的用戶端,並且用戶端可以是任意數量的組的成員。

要管理群組成員身份,請使用中心類`Groups`的屬性提供的[「添加](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)[和刪除」](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)方法。 下面的範例顯示了由客戶`Groups.Add`端`Groups.Remove`碼 呼叫的 Hub 方法中使用的和方法,然後是呼叫它們的 JavaScript 客戶端碼。

**Server**

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

**使用產生的代理的 JavaScript 用戶端**

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

您不必顯式創建組。 實際上,在調用`Groups.Add`中首次指定其名稱時會自動創建組,並且當您從其成員身份中刪除最後一個連接時,該組將被刪除。

沒有用於獲取組成員身份清單或組清單的 API。 SignalR 根據[pub/子模型](http://en.wikipedia.org/wiki/Publish/subscribe)向用戶端和組發送消息,並且伺服器不維護組或組成員身份的清單。 這有助於最大化可伸縮性,因為每當將節點添加到 Web 場時,SignalR 維護的任何狀態都必須傳播到新節點。

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a>新增與移除方法的非同步

`Groups.Add`和`Groups.Remove`方法以異步方式執行。 如果要將用戶端添加到組,然後使用組立即向用戶端發送消息,則必須確保`Groups.Add`該方法首先完成。 下面的代碼示例演示如何執行此操作。

**將用戶端新增到群組,然後向該客戶端傳送訊息**

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a>群組成員身份持久性

SignalR 追蹤連線,而不是使用者,因此,如果您希望使用者每次建立連接時都位於同一組中,則每次使用者建立新連線時都必須呼`Groups.Add`叫 。

在暫時失去連接後,有時 SignalR 可以自動復原連接。 在這種情況下,SignalR 正在還原相同的連接,而不是建立新連接,因此用戶端的組成員身份將自動還原。 即使臨時中斷是伺服器重新啟動或失敗的結果,也是可能的,因為每個用戶端(包括組成員身份)的連接狀態都向用戶端四捨五入。 如果伺服器在連接超時之前出現故障並由新伺服器替換,則用戶端可以自動重新連接到新伺服器,並重新註冊其成員的組。

當連接在失去連接後或連接超時或客戶端斷開連接(例如,當瀏覽器導航到新頁面時)無法自動恢復時,組成員身份將丟失。 使用者下次連接時將是一個新連接。 要在同一使用者建立新連接時維護組成員身份,應用程式必須跟蹤使用者和組之間的關聯,並在每次使用者建立新連接時還原組成員身份。

有關連線和重新連線的詳細資訊,請參閱本主題後面的[「集線器」 類別如何處理連線存留期事件](#connectionlifetime)。

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a>單使用者群組

使用 SignalR 的應用程式通常必須追蹤使用者和連接之間的關聯,以便知道哪個使用者發送消息以及應該接收哪些使用者。 組用於執行此操作的兩個常用模式之一。

- 單使用者組。

    您可以將使用者名稱指定為組名稱,並在每次使用者連接或重新連接時將當前連接 ID 添加到群組。 向發送給組的用戶發送消息。 此方法的缺點是,組不為您提供一種方法來了解使用者是連線還是脫機。
- 跟蹤使用者名和連接指示之間的關聯。

    您可以將每個使用者名稱與字典或資料庫中的一個或多個連接 I 之間的關聯存儲,並在每次使用者連接或斷開連接時更新儲存的資料。 要向使用者發送消息,請指定連接指示。 此方法的缺點是它需要更多的記憶體。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a>如何處理集線器類別的連線存留期事件

處理連接存留期事件的典型原因是跟蹤使用者是否已連接,並跟蹤使用者名和連接權杖之間的關聯。 要在用戶端連接或斷開連接時運行自己的代碼,請重寫`OnConnected``OnDisconnected`Hub`OnReconnected`類的和和虛擬方法,如以下示例所示。

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a>當"連接"時,打開斷開狀態,並調用"重新連接"

每次瀏覽器導航到新頁面時,都必須建立一個新連接,這意味著 SignalR 將執行方法`OnDisconnected``OnConnected`後跟 的方法。 建立新連接時,SignalR 始終建立新的連接 ID。

當`OnReconnected`SignalR 可以自動復原的連接出現暫時中斷時調用該方法,例如電纜在連接超時之前暫時斷開並重新連接時。當`OnDisconnected`客戶端斷開連接且 SignalR 無法自動重新連接時,如瀏覽器導航到新頁面時,將調用該方法。 因此,給定用戶端的可能事件序列為`OnConnected`,`OnReconnected``OnDisconnected`和或`OnConnected``OnDisconnected`。 對於給定的連線,`OnConnected``OnDisconnected`您將看不到序列,。 `OnReconnected`

在某些情況下`OnDisconnected`,例如伺服器出現故障或 App Domain 被回收時,不會調用該方法。 當另一台伺服器上線或 App Domain 完成其回收時,某些用戶端可能能夠重新連接`OnReconnected`並觸發 事件。

有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a>未填滿的呼叫者狀態

連接存留期事件處理程式方法從伺服器呼叫,這意味著您`state`在 用戶端上的物件中放置的任何狀態將不會填充在`Caller`伺服器上 的屬性中。 有關`state`物件`Caller`和 屬性的資訊,請參閱本主題後面的[「如何在用戶端和中心類之間傳遞狀態](#passstate)」。

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a>如何從內容取得有關用戶端的資訊

要取得有關用戶端的資訊`Context`, 請使用 Hub 類的屬性。 該`Context`屬性傳回[HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)物件,該物件提供對以下資訊的存取:

- 呼叫用戶端的連線識別碼。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    連接 ID 是由 SignalR 分配的 GUID(您無法在自己的代碼中指定值)。 每個連接都有一個連接 ID,如果應用程式中有多個集線器,則所有集線器都使用相同的連接 ID。
- HTTP 標頭數據。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    還可以從`Context.Headers`獲取 HTTP 標頭。 對同一事物`Context.Headers`的多次引用的原因是首先創建`Context.Request`, 該屬性在以後添加`Context.Headers`,並保留為向後相容性。
- 查詢字串數據。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    還可以從`Context.QueryString`獲取查詢字串數據。

    在此屬性中獲取的查詢字串是與建立 SignalR 連接的 HTTP 請求一起使用的查詢字串。 您可以通過設定連接在用戶端中添加查詢字串參數,這是將有關用戶端的數據從用戶端傳遞到伺服器的便捷方法。 下面的範例顯示了在使用生成的代理時在 JavaScript 用戶端中添加查詢字串的一種方法。

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    有關設置查詢字串參數的詳細資訊,請參閱[JavaScript](hubs-api-guide-javascript-client.md)和[.NET](hubs-api-guide-net-client.md)用戶端的 API 指南。

    您可以在查詢字串資料中找到用於連接的傳輸方法,以及 SignalR 內部使用的一些其他值:

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    的值`transportMethod`將是"webSocket"、"伺服器發送事件"、"永久幀"或"長輪詢"。 請注意,如果在`OnConnected`事件處理程式方法中檢查此值,在某些情況下,最初可能會獲取傳輸值,該值不是連接的最終協商傳輸方法。 在這種情況下,該方法將引發異常,並在建立最終傳輸方法時稍後再次調用。
- Cookie。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    您也可以從`Context.RequestCookies`獲取 Cookie。
- 使用者資訊。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- 要求的 HttpContext 物件 :

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    使用此方法,而不是獲取`HttpContext.Current`SignalR`HttpContext`連接的物件。

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a>如何在用戶端和中心類之間傳遞狀態

用戶端代理提供一個`state`物件,您可以在其中存儲要通過每個方法調用傳輸到伺服器的數據。 在伺服器上,您可以在用戶端呼叫的`Clients.Caller`Hub 方法中的屬性中存取此資料。 無法`Clients.Caller`為連線存留期事件處理程式填`OnConnected`滿`OnDisconnected`屬性`OnReconnected`, 並與 。

在`state`物件中建立或更新數據`Clients.Caller`, 屬性在兩個方向上工作。 您可以更新伺服器中的值,並將它們傳回用戶端。

下面的範例顯示 JavaScript 客戶端代碼,該代碼儲存狀態,以便透過每個方法呼叫傳輸到伺服器。

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

下面的範例顯示了 .NET 用戶端中的等效代碼。

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

在 Hub 類中,`Clients.Caller`您可以在 屬性中存取此資料。 下面的範例顯示檢索上一個範例中引用的狀態的代碼。

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> 此持久狀態機制不適用於大量數據,因為在`state`或`Clients.Caller`屬性中放置的所有內容都隨每個方法調用一起迴圈。 它對於較小的專案(如使用者名或計數器)很有用。

在VB.NET或強類型中心中,無法通過`Clients.Caller`而是使用`Clients.CallerState`(在信號R 2.1 中介紹):

**在 C 中使用呼叫方狀態#**

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

**以視覺化基礎使用呼叫方狀態**

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a>如何處理中心類別的錯誤

要處理在 Hub 類方法中發生的錯誤,首先請`await`確保使用 「觀察」非同步操作(如調用用戶端方法)中的任何異常。 然後使用以下一種或多種方法:

- 將方法代碼包裝在 try-catch 塊中並記錄異常物件。 出於除錯目的,您可以將異常發送給用戶端,但出於安全原因,不建議向生產中的客戶端發送詳細資訊。
- 建立處理[On 傳入錯誤](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法的集線器管道模組。 下面的示例顯示了一個管道模組,該模組記錄錯誤,然後是Startup.cs中的代碼,該代碼將模組注入到集線器管道中。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- 使用類`HubException`(在 SignalR 2 中介紹)。 可以從任何集線器調用引發此錯誤。 建構`HubError`函數獲取字串訊息和用於存儲額外錯誤數據的物件。 SignalR 將自動序列化異常並將其發送到用戶端,用戶端將用於拒絕或失敗集線器方法調用。

    以下代碼示例演示如何在中心調用期間引發`HubException`,以及如何處理 JavaScript 和 .NET 用戶端上的異常。

    **展示 HubException 類別的伺服器碼**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    **JavaScript 客戶端碼展示對在中心中引發 HubException 的回應**

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    **.NET 用戶端代碼,用於回應在中心中引發 HubException**

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

有關集線器管線模組的詳細資訊,請參閱本主題後面的[如何自訂中心管道](#hubpipeline)。

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a>如何開啟追蹤

要啟用伺服器端追蹤,請向 Web.config 檔案加入 system.診斷元素,如以下範例所示:

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

在 Visual Studio 中執行應用程式時,可以在 **「輸出」** 視窗中查看日誌。

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a>如何呼叫用戶端方法並管理來自中心類外部的群組

要從與 Hub 類不同的類調用用戶端方法,請獲取對集線器的 SignalR 上下文物件的引用,並用它來呼叫用戶端或管理組上的方法。

以下範例`StockTicker`類獲取上下文物件,將其儲存在類的實例中,將類實例存儲在靜態屬性中,並使用 singleton 類實例中的上下文調用`updateStockPrice``StockTickerHub`連接到名為 的 Hub 的用戶端上的方法。

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

如果需要在長壽命物件中多次使用上下文,獲取引用一次並保存它,而不是每次都再次獲取它。 獲取上下文一次可確保 SignalR 以與集線器方法進行用戶端方法調用的順序相同的順序向用戶端發送消息。 有關展示如何對集線器使用 SignalR 上下文的教學,請參閱[使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a>呼叫用戶端方法

您可以指定哪些用戶端將收到 RPC,但與從中心類調用時相比,選項更少。 原因是上下文與來自用戶端的特定調用不相關聯,因此任何需要瞭解當前連接 ID 的方法`Clients.Others`(`Clients.Caller`如`Clients.OthersInGroup`或或 ) 都不可用。 有下列選項可供使用：

- 所有已連線的用戶端。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- 由連接 ID 標識的特定用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- 除指定客戶端外的所有連接用戶端,由連接 ID 標識。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- 指定組中的所有連接用戶端。

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- 指定群組中的所有連接客戶端(指定用戶端除外),由連接 ID 識別。

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

如果要從 Hub 類別的方法呼叫非 Hub 類別,則可以將`Clients.Client`目前連線 ID 傳遞`Clients.AllExcept`,`Clients.Group`並將`Clients.Caller`其`Clients.Others`用於`Clients.OthersInGroup`, 或模擬或 。 在下面的範例中`MoveShapeHub`,類別將連接 ID`Broadcaster`來傳`Broadcaster`給類別,`Clients.Others`以便類可以類比 。

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a>管理群組成員身份

對於管理組,您具有與在中心類中相同的選項。

- 新增客戶端到群組

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- 從群組中移除客戶端

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a>如何自訂中心管道

SignalR 使您能夠將您自己的代碼注入集線器管道。 下面的範例顯示了一個自定義 Hub 管道模組,該模組記錄從用戶端和在用戶端上調用的傳出方法調用收到的每個傳入方法呼叫:

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

*Startup.cs*檔案中的以下代碼註冊在集線器導管中執行的模組:

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

您可以重寫許多不同的方法。 有關完整清單,請參閱[HubPipeline 模組方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。
