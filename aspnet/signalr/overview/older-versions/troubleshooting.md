---
uid: signalr/overview/older-versions/troubleshooting
title: 信號R故障排除(信號R 1.x) |微軟文件
author: bradygaster
description: 本文介紹了開發SignalR應用的常見問題。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543089"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 疑難排解 (SignalR 1.x)

由[派翠克·弗萊徹](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文檔介紹 SignalR 的常見故障排除問題。

本文檔包含以下部分。

- [用戶端與伺服器之間的呼叫方法以靜默方式失敗](#connection)
- [其他連線問題](#other)
- [編譯與伺服器端錯誤](#server)
- [視覺工作室問題](#vs)
- [網際網路資訊服務問題](#iis)
- [Azure 問題](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>用戶端與伺服器之間的呼叫方法以靜默方式失敗

本節介紹客戶端和伺服器之間的方法調用失敗而不出現有意義的錯誤消息的可能原因。 在 SignalR 應用程式中,伺服器沒有關於客戶端實現的方法的資訊;因此,伺服器沒有實現的方法。當伺服器調用用戶端方法時,方法名稱和參數數據將發送到用戶端,並且僅當該方法以伺服器指定的格式存在時才執行該方法。 如果在用戶端上找不到匹配方法,則不發生任何操作,並且伺服器上不引發錯誤消息。

要進一步調查未被調用的用戶端方法,可以在調用集線器上的 start 方法之前打開日誌記錄,以查看來自伺服器的調用。 要在 JavaScript 應用程式中啟用日誌記錄,請參閱[如何啟用用戶端日誌記錄(JAvaScript 用戶端版本)。](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging) 要在 .NET 用戶端應用程式中啟用日誌記錄,請參閱[如何啟用用戶端日誌記錄 (.NET 用戶端版本)。](../guide-to-the-api/hubs-api-guide-net-client.md#logging)

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>拼字錯誤的方法、不正確的方法簽名或不正確的中心名稱

如果被調用方法的名稱或簽名與用戶端上的適當方法不完全匹配,則調用將失敗。 驗證伺服器調用的方法名稱是否與用戶端上的方法的名稱匹配。 此外,SignalR 使用駱駝大小寫方法創建集線器代理,這在 JavaScript 中`SendMessage`是合適的 ,因此`sendMessage`在用戶端代理中 調用伺服器上調用的方法。 如果在伺服器端代碼`HubName`中使用該屬性,請驗證所使用的名稱是否與在用戶端上創建中心的名稱匹配。 如果不使用`HubName`該 屬性,請驗證 JavaScript 用戶端中中心的名稱是否為駱駝大小寫,例如聊天Hub而不是 ChatHub。

### <a name="duplicate-method-name-on-client"></a>用戶端上的重複方法名稱

驗證用戶端上沒有僅因大小寫而異的重複方法。 如果用戶端應用程式具有稱為`sendMessage`的方法,請驗證是否也沒有調`SendMessage`用 的方法。

### <a name="missing-json-parser-on-the-client"></a>用戶端上缺少 JSON 解析器

SignalR 需要 JSON 解析器存在以序列化伺服器和用戶端之間的呼叫。 如果客戶端沒有內置的 JSON 解析器(如 Internet Explorer 7),則需要在應用程式中包含一個。 你可以[在這裡](http://nuget.org/packages/json2)下載JSON解析器。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>混合集線器與持久連接語法

SignalR 使用兩種通信模型:集線器和持久連接。 調用這兩種通信模型的語法在客戶端代碼中是不同的。 如果在伺服器代碼中添加了中心,請驗證所有用戶端代碼是否使用正確的中心語法。

**在 JavaScript 客戶端建立的 JavaScript 客戶端碼**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**在 Javascript 客戶端建立中心代理的 JavaScript 客戶端碼**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**將路由映射到持久連線的 C# 伺服器代碼**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C# 伺服器代碼,用於將路由映射到集線器,或者如果您有多個應用程式,則映射到多個集線器**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>新增訂閱之前啟動的連線

如果在將可以從伺服器調用的方法添加到代理之前啟動中心連接,將不會接收消息。 以下 JavaScript 代碼會無法正確啟動中心:

**不正確的 JavaScript 客戶端碼,不允許接收中心訊息**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

而是在調用「開始」之前添加方法訂閱:

**正確將訂閱加入中心的 JavaScript 客戶端碼**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>中心代理上缺少方法名稱

驗證在伺服器上定義的方法是否訂閱在用戶端上。 即使伺服器定義了該方法,仍必須將其添加到用戶端代理中。 方法可以通過以下方式添加到用戶端代理(請注意,該方法已添加到`client`中心 成員,而不是直接添加到中心):

**將方法加入到中心代理的 JavaScript 客戶端碼**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>未聲明為公共的集線器或中心方法

要在用戶端上可見,必須將中心實現和方法聲明為`public`。

### <a name="accessing-hub-from-a-different-application"></a>從其他應用程式存取集線器

信號R中心只能通過實現SignalR用戶端的應用程序進行訪問。 SignalR 不能與其他通訊庫(如 SOAP 或 WCF Web 服務)互通。如果目標平台沒有可用的 SignalR 用戶端,則無法直接訪問伺服器的終結點。

### <a name="manually-serializing-data"></a>手動序列化資料

SignalR 將自動使用 JSON 來序列化方法參數 - 無需自行執行。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>在 OnDisconnected 函數中的用戶端上未執行遠端中心方法

這是設計的行為。 調用`OnDisconnected`時,中心已進入`Disconnected`狀態 ,不允許調用其他集線器方法。

**C# 伺服器代碼,在「不斷開」事件中正確執行代碼**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>達到連線限制

在 Windows 7 等用戶端作業系統上使用完整版本的 IIS 時,將強制實施 10 個連接限制。 使用用戶端作業系統時,請使用IIS Express來避免此限制。

### <a name="cross-domain-connection-not-set-up-properly"></a>跨域連接設定不正確

如果跨域連接(SignalR URL 與託管頁不在同一域中的連接)設置不正確,則連接可能會失敗,而不會出現錯誤消息。 有關如何啟用跨域通訊的資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>使用 NTLM(活動目錄)在 .NET 用戶端中不起作用的連線

如果連接配置不正確,則使用域安全的 .NET 用戶端應用程式中的連接可能會失敗。 要在網域環境中使用 SignalR,請使用以下方式設定所需的連線屬性:

**連線認證認證的 C# 客戶端碼**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>其他連線問題

本節介紹連接過程中發生的特定癥狀或錯誤消息的原因和解決方案。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>「必須先呼叫開始才能送出資料」錯誤

如果代碼在連接啟動之前引用 SignalR 物件,則通常可以看到此錯誤。 必須在連接完成後添加處理程式的佈線等調用伺服器上定義的調用方法。 請注意,調用`Start`是非同步的,因此在調用完成之前可以執行調用後的代碼。 在連線完全啟動後添加處理程式的最佳方法是將它們放入回檔函數中,該函數作為參數傳遞給 start 方法:

**正確新增參考 SignalR 物件的事件處理程式的 JavaScript 客戶端碼**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

如果連接在仍在引用 SignalR 物件時停止,也會看到此錯誤。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>"301 永久移動'或"302臨時移動"錯誤

如果專案包含名為 SignalR 的資料夾,則可能會看到此錯誤,這將干擾自動創建的代理。 為了避免此錯誤,請勿使用應用程式中調用`SignalR`的資料夾,或關閉自動代理生成。 有關詳細資訊[,請參閱產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 或銀光用戶端中的"403 禁止"錯誤

此錯誤可能發生在跨域環境中,其中跨域通信未正確啟用。 有關如何啟用跨域通訊的資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。 要在 Silverlight 用戶端中建立跨網域連接,請參閱[來自 Silverlight 用戶端的跨域連接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。

### <a name="404-not-found-error"></a>"404 找不到錯誤

此問題有多種原因。 驗證以下所有情況:

- **中心代理地址引用格式不正確:** 如果對生成的中心代理位址的引用格式不正確,則通常可以看到此錯誤。 驗證對中心位址的引用是否正確。 關於詳細資訊[,請參閱如何參考動態產生的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。
- **在新增中心路由之前向應用程式添加路由:** 如果應用程式使用其他路由,請驗證新增的第一個路由是否呼叫`MapHubs`。

### <a name="500-internal-server-error"></a>"500 內部伺服器錯誤"

這是一個非常通用的錯誤,可能有各種各樣的原因。 錯誤的詳細資訊應出現在伺服器的事件日誌中,或者可以通過調試伺服器找到。 通過在伺服器上打開詳細的錯誤,可以獲得更詳細的錯誤資訊。 有關詳細資訊,請參閱如何處理[Hub 類別的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>型態錯誤:&lt;中心&gt;類型 未定義錯誤

如果調用`MapHubs`不正確,將導致此錯誤。 關於詳細資訊[,請參考如何註冊 SignalR 路由與設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>使用者代碼未處理 Json 序列化異常

驗證發送到方法的參數是否不包括不可序列化的類型(如檔句柄或資料庫連接)。 如果需要在不希望發送到用戶端的伺服器端物件上使用成員(出於安全性或序列化原因),請使用該`JSONIgnore`屬性。

### <a name="protocol-error-unknown-transport-error"></a>'協定錯誤:未知傳輸"錯誤

如果用戶端不支援 SignalR 使用的傳輸,則可能發生此錯誤。 有關哪些瀏覽器可與 SignalR 一起使用的資訊,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>"JavaScript 中心代理生成已被禁用。

如果`DisableJavaScriptProxies`設置時將發生此錯誤,同時還包括對 動態生成的代理`signalr/hubs`的引用。 有關手動建立代理的詳細資訊,請參閱[產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>連線 ID 格式不正確或使用者身份在作用 SignalR 連線期間無法變更錯誤

如果正在使用身份驗證,並且用戶端在停止連接之前註銷,則可能會看到此錯誤。 解決方案是在註銷用戶端之前停止 SignalR 連接。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>"未捕獲錯誤:信號R:找不到 jQuery。 請確定在 SignalR.js 檔錯誤之前引用 jQuery

SignalR JavaScript 用戶端需要 jQuery 才能運行。 驗證對 jQuery 的引用是否正確,使用的路徑是否有效,以及對 jQuery 的引用是否位於對 SignalR 的引用之前。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>「未捕捉的類型錯誤:無法讀取屬性」&lt;屬性&gt;'未定義"錯誤

此錯誤導致沒有正確引用 jQuery 或中心代理。 驗證對 jQuery 和集線器代理的引用是否正確,使用的路徑是否有效,以及對 jQuery 的引用是否位於對集線器代理的引用之前。 對集線器代理的預設引用應如下所示:

**正確參考中心代理的 HTML 客戶端碼**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>執行時Binder異常未由使用者代碼處理錯誤

當使用不正確的重載`Hub.On`時,可能會出現此錯誤。 如果方法具有傳回值,則必須將傳回類型指定為泛型型態參數:

**在用戶端上定義的方法(沒有產生的代理)**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>連線 ID 不一致或頁面載入之間的連線中斷

這是設計的行為。 由於中心物件託管在頁面物件中,因此在頁面刷新時將銷毀中心。 多頁應用程式需要維護使用者和連接指示之間的關聯,以便它們在頁面載入之間保持一致。 連接指示可以存儲在`ConcurrentDictionary`物件或資料庫中的伺服器上。

### <a name="value-cannot-be-null-error"></a>"值不能為空"錯誤

當前不支援具有可選參數的伺服器端方法;如果省略可選參數,該方法將失敗。 有關詳細資訊,請參閱[可選參數](https://github.com/SignalR/SignalR/issues/324)。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>Firefox 無法在&lt;位址&gt;建立與伺服器的連接「Firebug」 中的錯誤

如果 WebSocket 傳輸協商失敗,並且使用另一個傳輸,可以在 Firebug 中看到此錯誤消息。 這是設計的行為。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 用戶端應用程式中的"遠端憑證根據驗證過程無效"錯誤

如果伺服器需要自定義用戶端證書,則可以在發出請求之前向連接添加 x509 證書。 使用此憑證加入到連線中`Connection.AddClientCertificate`。

### <a name="connection-drops-after-authentication-times-out"></a>驗證逾時後連接斷線

這是設計的行為。 當連接處於活動狀態時,無法修改身份驗證憑據;要刷新憑據,必須停止並重新啟動連接。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>使用 jQuery 移動時,OnConnected 被呼叫兩次

jQuery`initializePage`Mobile 的功能強制重新執行每個頁面中的文稿,從而創建第二個連接。 此問題的解決方案包括:

- 在 JavaScript 檔之前包括對 jQuery 移動的引用。
- 通過設置`initializePage``$.mobile.autoInitializePage = false`禁用 函數。
- 在開始連接之前,等待頁面完成初始化。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>使用伺服器傳送事件在 Silverlight 應用程式中延遲訊息

在 Silverlight 上使用伺服器發送的事件時,消息會延遲。 要強制使用長輪詢,在啟動連接時使用以下內容:

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>使用永久幀協定"拒絕許可權"

這是一個已知的問題,[此處](https://github.com/SignalR/SignalR/issues/1963)描述。 可以使用最新的 JQuery 庫看到此癥狀;解決方法是將應用程式降級為 JQuery 1.8.2。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>編譯與伺服器端錯誤

 以下部分包含編譯器和伺服器端運行時錯誤的可能解決方案。 

### <a name="reference-to-hub-instance-is-null"></a>對中心實體的引用為空

由於為每個連接創建了一個中心實例,因此無法自己在代碼中創建集線器的實例。 要從中心外部調用方法,請參閱[如何調用用戶端方法並從中心類外部管理組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub),瞭解如何獲取對中心上下文的引用。

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.當前.工作階段為空

這是設計的行為。 SignalR 不支援ASP.NET會話狀態,因為啟用會話狀態將中斷雙工消息。

### <a name="no-suitable-method-to-override"></a>沒有合適的方法可以重寫

如果您使用的是來自舊文檔或博客的代碼,則可能會看到此錯誤。 驗證您沒有引用已更改或棄用的方法的名稱(如`OnConnectedAsync`)。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>主機上下文擴展.WebSocket伺服器網址為空

這是設計的行為。 此成員已棄用,不應使用。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>"名為"Signalr.hubs"的路由已在路由集合中"錯誤

如果`MapHubs`應用程式調用了兩次,則將看到此錯誤。 一些示例應用程式`MapHubs`直接調用全域應用程式檔中;其他人在包裝類中進行調用。 確保應用程式不同時執行這兩種操作。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>視覺工作室問題

本節介紹視覺工作室中遇到的問題。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>文稿文件節點未顯示在解決方案資源管理員中

我們的一些教程將引導您到解決方案資源管理器中的"腳本文檔"節點進行調試。 此節點由 JavaScript 除錯器生成,僅在 Internet 資源管理器中除錯瀏覽器客戶端時出現;如果使用 Chrome 或 Firefox,將不會顯示該節點。 如果運行了另一個用戶端調試器(如 Silverlight 調試器),JAVAScript 調試器也不會運行。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>信號R在視覺工作室 2008 或更早版本上不起作用

這是設計的行為。 信號R需要 .NET 框架 4 或更高版本;這要求在 Visual Studio 2010 或更高版本中開發 SignalR 應用程式。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 問題

本節包含互聯網資訊服務的問題。

### <a name="web-site-crashes-after-maphubs-call"></a>地圖中心呼叫後網站崩潰

此問題已在最新版本的 SignalR 中修復。 使用 NuGet 更新安裝,驗證您使用的是最新版本的 SignalR。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 問題

本節包含 Microsoft Azure 的問題。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>變更主題名稱後,不會透過 Azure 背板接收訊息

Azure 背板使用的主題不用於使用者配置。
