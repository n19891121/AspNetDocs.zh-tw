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
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET信號器中心 API 指南 - JAVAScript 用戶端

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文件介紹了在 JavaScript 用戶端(如瀏覽器和 Windows 應用商店 (WinJS) 應用程式中,將集線器 API 用於 SignalR 版本 2。
>
> SignalR 集線器 API 使您能夠從伺服器對連接的用戶端以及從用戶端到伺服器進行遠端過程呼叫 (RPC)。 在伺服器代碼中,定義用戶端可以調用的方法,並調用在用戶端上運行的方法。 在用戶端代碼中,定義可以從伺服器調用的方法,並調用在伺服器上運行的方法。 SignalR 為您處理所有用戶端到伺服器管道。
>
> SignalR 還提供稱為持久連接的較低級別的 API。 有關信號R、集線器和持久連接的介紹,請參閱[訊號R 簡介](../getting-started/introduction-to-signalr.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
> - .NET 4.5
> - 信號R版本 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的早期版本
>
> 有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題和評論
>
> 請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。 如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

本文件包含下列章節：

- [產生的代理及其為您做什麼](#genproxy)

    - [何時使用產生的代理程式](#cantusegenproxy)
- [用戶端設定](#clientsetup)

    - [如何參考動態產生的代理程式](#dynamicproxy)
    - [如何為 SignalR 產生的代理建立物理檔案](#manualproxy)
- [如何建立連線](#establishconnection)

    - [$.connect.hub 是 $.hubConnection() 創建的物件](#connequivalence)
    - [啟動方法的非同步執行](#asyncstart)
- [如何建立跨網域連線](#crossdomain)
- [如何設定連線](#configureconnection)

    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
- [如何取得中心類的代理](#getproxy)
- [如何在客戶端上定義伺服器可以呼叫的方法](#callclient)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連線存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何開啟客戶端記錄記錄](#logging)

有關如何對伺服器或 .NET 客戶端進行程式設計的文件,請參閱以下資源:

- [訊號器集線器 API 指南 - 伺服器](hubs-api-guide-server.md)
- [信號器集線器 API 指南 - .NET 用戶端](hubs-api-guide-net-client.md)

SignalR 2 伺服器元件僅在 .NET 4.5 上可用(儘管在 .NET 4.0 上有一個用於 SignalR 2 的 .NET 用戶端)。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>產生的代理及其為您做什麼

您可以對 JavaScript 用戶端進行程式設計,以便與 SignalR 服務進行通訊,無論是否沒有 SignalR 為您生成的代理。 代理的作用是簡化用於連接的代碼的語法、編寫伺服器調用的方法以及調用伺服器上的方法。

編寫程式以呼叫伺服器方法時,產生的代理程式讓您能夠使用看起來好像在執行本地函數的語法:可以編`serverMethod(arg1, arg2)`寫`invoke('serverMethod', arg1, arg2)`而不是 。 如果鍵入伺服器方法名稱錯誤,生成的代理語法還允許立即且可理解的用戶端錯誤。 如果手動創建定義代理的檔,還可以獲得 IntelliSense 支援編寫調用伺服器方法的代碼。

例如,假設您在伺服器上具有以下中心類:

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

以下代碼示例顯示了 JavaScript 代碼在伺服器`NewContosoChatMessage`上調用 該方法和`addContosoChatMessageToPage`從伺服器接收 方法調用的外觀。

**使用產生的代理程式**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**沒有產生的代理**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>何時使用產生的代理程式

如果要為伺服器調用的用戶端方法註冊多個事件處理程式,則不能使用生成的代理。 否則,您可以選擇使用生成的代理,或者不使用基於編碼首選項。 如果選擇不使用它,則不必在客戶端`script`代碼 中的元素中引用"信號器/集線器"URL。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

JavaScript 用戶端需要引用 jQuery 和 SignalR 核心 JavaScript 檔案。 jQuery 版本必須為 1.6.4 或主要更高版本,例如 1.7.2、1.8.2 或 1.9.1。 如果您決定使用生成的代理,還需要引用 SignalR 生成的代理 JavaScript 檔案。 下面的範例顯示了使用生成的代理的 HTML 頁中引用的外觀。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

這些引用必須包含在此順序中:jQuery 優先,之後為 SignalR 內核,最後顯示 SignalR 代理。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>如何參考動態產生的代理程式

在前面的範例中,對 SignalR 生成的代理的引用是動態生成的 JavaScript 代碼,而不是物理檔。 SignalR 動態為代理創建 JavaScript 代碼,並將其用於用戶端以回應"/信號器/集線器"URL。 如果在方法`MapSignalR`中為伺服器上的 SignalR 連接指定了不同的基本 URL,則動態生成的代理檔的 URL 是自定義 URL,並附加了"/集線器"

> [!NOTE]
> 對於 Windows 8(Windows 應用商店)JavaScript 用戶端,請使用物理代理檔而不是動態生成的檔。 有關詳細資訊,請參閱本主題後面的[「如何為 SignalR 生成的代理創建實體檔](#manualproxy)」。。

在ASP.NET MVC 4 或 5 Razor 檢視中,使用波浪線引用代理檔引用中的應用程式根:

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

有關在 MVC 5 中使用訊號 R 的詳細資訊,請參閱[使用訊號 R 和 MVC 5 入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

在ASP.NET MVC 3`Url.Content`Razor 檢視中,用於代理檔引用:

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

在ASP.NET Web 表單應用程式`ResolveClientUrl`中, 使用代理檔案參考或使用應用根相對路徑(以波浪線開頭)透過文稿管理員註冊它:

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

通常,使用相同的方法來指定用於 CSS 或 JavaScript 檔的"/信號器/集線器" 如果在不使用波浪線的情況下指定 URL,則在某些情況下,當您使用 IIS Express 在 Visual Studio 中測試時,應用程式將正常工作,但在部署到完整 IIS 時,應用程式將失敗,出現 404 錯誤。 有關詳細資訊,請參閱在 Visual Studio 中解析對 Web 伺服器中的**根級資源的引用**[,以便 ASP.NET](https://msdn.microsoft.com/library/58wxa9w5.aspx) MSDN 網站上的 Web 專案。

當您在 Visual Studio 2017 中除錯模式下執行 Web 專案時,如果您使用 Internet Explorer 作為瀏覽器,則可以在**文稿**下**的解決方案資源管理器**中看到代理檔。

要檢視檔案的內容,請按兩下**集線器**。 如果您沒有使用 Visual Studio 2012 或 2013 和 Internet Explorer,或者如果您未處於調試模式,還可以透過流覽"/signalR/集線器"URL來獲取文件內容。 例如,如果您的網站在`http://localhost:56699`中運行,請轉到`http://localhost:56699/SignalR/hubs`瀏覽器中。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>如何為 SignalR 產生的代理建立物理檔案

作為動態生成的代理的替代方法,您可以創建具有代理程式碼並引用該檔的實體檔。 您可能希望執行此操作以控制緩存或捆綁行為,或者在對伺服器方法的調用進行編碼時獲取 IntelliSense。

要建立代理檔,請執行以下步驟:

1. 安裝[Microsoft.AspNet.SignalR.Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 套件。
2. 開啟命令提示符並瀏覽到包含 SignalR.exe 檔案*的工具*資料夾。 工具資料夾位於以下位置:

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 輸入下列命令：

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.dll*的路徑通常是項目資料夾中的*bin*資料夾。

    此命令創建名為*server.js*的檔案,該檔與*signalr.exe*在同一資料夾中。
4. 將*server.js*檔案放在專案中的相應資料夾中,將其重新命名為適合您的應用程式,並添加對該檔的引用,以代替「信號器/集線器」引用。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連線

在建立連接之前,必須建立連接物件、創建代理和註冊事件處理程式,以便從伺服器調用的方法。 設置代理和事件處理程式時,通過調用`start`方法建立連接。

如果使用生成的代理,則不必在自己的代碼中創建連接物件,因為生成的代理代碼會為您創建連接物件。

<a id="nogenconnection"></a>

**建立連線(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**建立連線(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。 有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

默認情況下,中心位置是當前伺服器;如果要連接到其他伺服器,請在呼叫`start`該方法之前指定 URL,如以下範例所示:

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常,在調用 方法以建立連接`start`之前 註冊事件處理程式。 如果要在建立連接后註冊一些事件處理程式,可以執行此操作,但在調用`start`該方法之前,必須至少註冊一個事件處理程式。 原因之一是應用程式中可能有許多中心,但如果您只要使用其中一個集線器,則不希望在每個集`OnConnected`線器上觸發事件。 建立連接後,在 Hub 的代理上存在用戶端方法是指示 SignalR 觸發`OnConnected`事件的原因。 如果在調用`start`方法之前未註冊任何事件處理程式,則可以在 Hub 上調用方法,但不會調`OnConnected`用 Hub 的方法,也不會從伺服器調用任何用戶端方法。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$.connect.hub 是 $.hubConnection() 創建的物件

正如您從範例中所看到的,當您使用生成的代理時,`$.connection.hub`引用連接物件。 這與不使用生成的代理時通過調用`$.hubConnection()`獲得的物件相同。 產生的代理程式碼執行以下文句為您建立連線:

![建立建立的代理檔案建立連線](hubs-api-guide-javascript-client/_static/image3.png)

使用生成的代理時,可以使用任何不使用生成的代理時對連接物件`$.connection.hub`執行的任何操作。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>啟動方法的非同步執行

該方法`start`以異步方式執行。 它返回[jQuery 延遲物件](http://api.jquery.com/category/deferred-object/),這意味著您可以通過調`pipe`用`done`方法`fail`(如、 和) 添加回調函數。 如果已建立連接后需要執行的代碼(如調用伺服器方法),請將該代碼放入回調函數中,或從回調函數調用它。 回調`.done`方法在建立連接後執行,並在伺服器`OnConnected`上的事件處理程式方法中的任何代碼完成執行之後。

如果將上述範例中的「現在連線」語句作為`start`方法調用後的`.done`下一行代碼(不在回調中),則`console.log`該行將在建立連接之前執行,如以下範例所示:

![編寫建立連接後執行的程式碼的錯誤方法](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>如何建立跨網域連線

通常,如果瀏覽器從`http://contoso.com`載入頁面,則 SignalR 連接位於同一`http://contoso.com/signalr`域中 ,在 。 如果中的`http://contoso.com`頁面與`http://fabrikam.com/signalr`斷開連接,則為跨域連接。 出於安全原因,默認情況下禁用跨域連接。

在 SignalR 1.x 中,跨域請求由單個啟用 CrossDomain 標誌控制。 此標誌同時控制 JSONP 和 CORS 請求。 為了更靈活,所有 CORS 支援都從 SignalR 的伺服器元件中刪除(如果檢測到瀏覽器支援它,JAVAScript 用戶端仍通常使用 CORS),並且新的 OWIN 中間件已可用於支援這些方案。

如果用戶端上需要 JSONP(以支援舊瀏覽器中的跨域請求),則需要通過`EnableJSONP``HubConfiguration`在`true`物件 上設置為 (如下所示)顯式啟用它。 默認情況下禁用 JSONP,因為它的安全性低於 CORS。

**將 Microsoft.Owin.Cors 新增到您的專案中:** 要安裝此庫,請在包管理員控制台中執行以下命令:

`Install-Package Microsoft.Owin.Cors`

此命令會將包的 2.1.0 版本添加到專案中。

### <a name="calling-usecors"></a>呼叫使用參數

 以下代碼段演示如何在 SignalR 2 中實現跨域連接。

**在 SignalR 2 上實現跨網域要求**

以下代碼展示如何在 SignalR 2 專案中啟用 CORS 或 JSONP。 此代碼示例使用`Map``RunSignalR``MapSignalR`而不是 ,以便 CORS 中間件僅運行需要 CORS 支援的 SignalR 請求(而不是針對中`MapSignalR`指定的路徑上的所有流量)。映射還可用於需要為特定 URL 首碼運行的任何其他中間件,而不是整個應用程式。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 不要在代碼中設置為`jQuery.support.cors`true。
>
>     ![不要將 jQuery.support.cors 設定為 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     信號R處理CORS的使用。 設置為`jQuery.support.cors`true 禁用 JSONP,因為它會導致 SignalR 假定瀏覽器支援 CORS。
> - 當您連接到本地主機 URL 時,Internet Explorer 10 不會將其視為跨域連接,因此應用程式將在本地使用 IE 10,即使您未在伺服器上啟用跨域連接也是如此。
> - 有關將跨網域連接與 Internet Explorer 9 一起使用的資訊,請參閱[此堆疊溢出線程](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。
> - 有關使用 Chrome 跨域連接的資訊,請參閱[此堆疊溢出線程](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。
> - 範例代碼使用預設的/信號器"URL 連接到您的 SignalR 服務。 有關如何指定其他基本 URL 的資訊,請參閱[ASP.NET 訊號 R 中心 API 指南 - 伺服器 - /signalr URL](hubs-api-guide-server.md#signalrurl)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連線

在建立連接之前,可以指定查詢字串參數或指定傳輸方法。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果要在用戶端連接時將數據發送到伺服器,則可以向連接物件添加查詢字串參數。 以下範例展示如何在用戶端代碼中設置查詢字串參數。

**在呼叫 start 方法之前設定查詢字串值(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**在呼叫 start 方法之前設定查詢字串值(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

下面的範例展示如何讀取伺服器代碼中的查詢字串參數。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

作為連接過程的一部分,SignalR 用戶端通常與伺服器協商以確定伺服器和用戶端支援的最佳傳輸。 如果您已經知道要使用的傳輸,則可以在調用 方法時指定傳輸方法`start`來 繞過此協商過程。

**指定傳輸方法的客戶端碼 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**指定傳輸方法的客戶端代碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

作為替代方法,您可以按希望 SignalR 嘗試它們的順序指定多個傳輸方法:

**指定自訂傳輸回退方案(使用產生的代理)的客戶端碼**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**指定自訂傳輸回退方案的客戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

可以使用以下值指定傳輸方法:

- "網络套接字"
- "永久框架"
- "伺服器發送事件"
- "長輪詢"

以下範例展示如何找出連接正在使用哪種傳輸方法。

**顯示連線使用的傳輸方法的客戶端碼(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**顯示連線使用的傳輸方法的客戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

有關如何在伺服器代碼中檢查傳輸方法的資訊,請參閱[ASP.NET SignalR 集線器 API 指南 - 伺服器 - 如何從 Context 屬性取得有關用戶端的資訊](hubs-api-guide-server.md#contextproperty)。 有關傳輸和回退的詳細資訊,請參閱[訊號R - 傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>如何取得中心類的代理

您建立的每個連接物件都封裝了有關連接到包含一個或多個集線器類的 SignalR 服務的資訊。 要與 Hub 類通訊,請使用自己創建的代理物件(如果您不使用生成的代理)或為您生成的代理。

在用戶端上,代理名稱是集線器類名稱的駱駝大小寫版本。 SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。

**伺服器上的集線器類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**取得對中心產生的用戶端代理的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**為中心類別建立客戶端代理(沒有產生的代理)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

如果使用`HubName`屬性裝飾 Hub 類,請使用確切名稱而不更改大小寫。

**伺服器上具有 HubName 屬性的集線器類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**取得對中心產生的用戶端代理的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**為中心類別建立客戶端代理(沒有產生的代理)**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在客戶端上定義伺服器可以呼叫的方法

要定義伺服器可以從集線器呼叫的方法,請使用生成的代理`client`的屬性向中心代理添加事件處理程式,或者如果您不使用生成的代理,`on`則調用方法。 參數可以是複雜物件。

在調用 方法以建立連接之前`start`添加 事件處理程式。 (如果要在調用`start`方法後添加事件處理程式,請參閱本文檔前面[如何建立連接](#establishconnection)的說明,並使用顯示的語法來定義方法而不使用生成的代理。

方法名稱匹配不區分大小寫。 例如,`Clients.All.addContosoChatMessageToPage`在伺服器上將`AddContosoChatMessageToPage`執行`addContosoChatMessageToPage`、`addcontosochatmessagetopage`或在用戶端上。

**在用戶端上定義方法 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**在用戶端上定義方法的替代方法(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**在用戶端上定義方法(沒有產生的代理,或在呼叫 start 方法後新增時)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**呼叫用戶端方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

以下範例包括作為方法參數的複雜物件。

**在用戶端上定義採用複雜物件的方法(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**在用戶端上定義採用複雜物件的方法(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**定義複雜物件的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**使用複雜物件呼叫用戶端方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

要從用戶端呼叫伺服器方法,請使用生成的代理`server`的屬性或 Hub`invoke`代理上的方法(如果您不使用生成的代理)。 返回值或參數可以是複雜物件。

在集線器上傳遞方法名稱的駱駝大小寫版本。 SignalR 會自動進行此更改,以便 JavaScript 代碼可以符合 JavaScript 約定。

以下範例展示如何呼叫沒有返回值的伺服器方法以及如何調用具有返回值的伺服器方法。

**沒有 HubMethodName 屬性的伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**定義參數中傳遞的複雜物件的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**呼叫伺服器方法的客戶端碼 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**呼叫伺服器方法的客戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

如果使用`HubMethodName`屬性修飾 Hub 方法,請使用該名稱而不更改大小寫。

具有 HubMethodName 屬性的**伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**呼叫伺服器方法的客戶端碼 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**呼叫伺服器方法的客戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

前面的範例展示如何調用沒有返回值的伺服器方法。 以下範例簡報如何調用具有返回值的伺服器方法。

**具有傳回值的方法的伺服器代碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

**回報**值的 Stock 類別

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**呼叫伺服器方法的客戶端碼 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**呼叫伺服器方法的客戶端碼(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連線存留期事件

SignalR 提供您可以處理的以下連線存留期事件:

- `starting`:在通過連接發送任何數據之前引發。
- `received`:在連接上收到任何數據時引發。 提供接收的數據。
- `connectionSlow`:當客戶端檢測到連接緩慢或頻繁斷開時引發。
- `reconnecting`:當基礎傳輸開始重新連接時引發。
- `reconnected`:在基礎傳輸重新連接時引發。
- `stateChanged`:當連接狀態更改時引發。 提供舊狀態和新狀態(連接、連接、重新連接或斷開連接)。
- `disconnected`:連接斷開連接時引發。

例如,如果要在連接問題可能導致明顯延遲時顯示警告消息,則處理該`connectionSlow`事件。

**處理連線速度事件(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**處理連線速度慢事件(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

有關詳細資訊,請參閱在[SignalR 中瞭解與處理連線存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

SignalR JavaScript`error`用戶端提供一個事件,您可以為其添加處理程式。 您還可以使用 fail 方法為伺服器方法呼叫導致的錯誤添加處理程式。

如果未在伺服器上顯式啟用詳細的錯誤消息,則 SignalR 在錯誤後返回的異常物件包含有關該錯誤的最少資訊。 例如,如果調用`newContosoChatMessage`失敗,錯誤物件中的錯誤消息包含`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`「 出於安全原因不建議向生產中的客戶端發送詳細的錯誤訊息,但如果要啟用詳細的錯誤訊息以進行故障排除,請使用伺服器上的以下代碼。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

下面的範例展示如何為錯誤事件添加處理程式。

**新增錯誤處理程式 (使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**新增錯誤處理程式 (沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

下面的範例演示如何處理方法調用中的錯誤。

**處理方法呼叫中的錯誤(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**處理方法呼叫中的錯誤(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

如果方法調用失敗,也會引發`error`該事件,`error`因此方法處理程式中的`.fail`代碼和方法回調中的代碼將執行。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何開啟客戶端記錄記錄

要在連接上啟用客戶端日誌記錄,在調`logging``start`用 方法建立連接之前,在連接對象上設置屬性。

**開啟紀錄紀錄(使用產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**開啟紀錄紀錄(沒有產生的代理)**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

要查看日誌,請打開瀏覽器的開發人員工具,然後轉到"控制台"選項卡。有關顯示分步說明並顯示如何執行此動作的螢幕擷取的教學,請參考[ASP.NET 訊號器的伺服器廣播 - 啟用紀錄紀錄](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。
