---
uid: signalr/overview/security/introduction-to-security
title: 信號R安全簡介 |微軟文件
author: bradygaster
description: 描述在開發 SignalR 應用程式時必須考慮的安全問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676192"
---
# <a name="introduction-to-signalr-security"></a>SignalR 安全性簡介

由[派翠克·弗萊徹](https://github.com/pfletcher),[湯姆·菲茨麥克肯](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介紹了在開發 SignalR 應用程式時必須考慮的安全問題。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

- [訊號R安全概念](#concepts)

    - [驗證和授權](#authentication)
    - [連線權杖](#connectiontoken)
    - [重新連線時重新加入群組](#rejoingroup)
- [信號器如何防止跨網站請求偽造](#csrf)
- [訊號R安全建議](#recommendations)

    - [安全通訊端字層 (SSL) 協定](#ssl)
    - [不要將群組用作安全機制](#groupsecurity)
    - [安全地處理來自用戶端的輸入](#input)
    - [協調使用者狀態變更與活動連線](#reconcile)
    - [自動產生的 JavaScript 代理檔](#autogen)
    - [例外狀況](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>訊號R安全概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>驗證和授權

SignalR 不提供任何用於驗證使用者的功能。 相反,您將 SignalR 功能整合到應用程式的現有身份驗證結構中。 您可以像在應用程式中通常一樣對使用者進行身份驗證,並處理 SignalR 代碼中的身份驗證結果。 例如,您可以使用ASP.NET窗體身份驗證對使用者進行身份驗證,然後在中心中強制授權哪些使用者或角色調用方法。 在集線器中,還可以將身份驗證資訊(如使用者名或使用者是否屬於角色)傳遞給用戶端。

SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性來指定哪些使用者有權存取集線器或方法。 將「授權」屬性應用於中心或中心中的特定方法。 如果沒有"授權"屬性,則連接到集線器的用戶端可以使用集線器上的所有公共方法。 有關集線器的詳細資訊,請參閱[SignalR 集線器的身分驗證與授權](hub-authorization.md)。

將`Authorize`屬性應用於中心,但不應用於持久連接。 在使用 時強制實施授權`PersistentConnection`規則 ,必須`AuthorizeRequest`重寫 方法。 有關持久連線的詳細資訊,請參閱[SignalR 持久連線的身份驗證與授權](persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>連線權杖

SignalR 通過驗證發件人的身份來降低執行惡意命令的風險。 對於每個請求,用戶端和伺服器傳遞一個連接權杖,其中包含經過身份驗證的使用者的連接ID和使用者名。 連接 ID 唯一標識每個連接的用戶端。 伺服器在創建新連接時隨機生成連接 ID,並在連接期間保留該 ID。 Web 應用程式的身份驗證機制提供使用者名。 SignalR 使用加密和數位簽名來保護連接權杖。

![](introduction-to-security/_static/image2.png)

對於每個請求,伺服器驗證令牌的內容,以確保請求來自指定使用者。 使用者名必須對應於連接 ID。通過驗證連接ID和使用者名,SignalR可防止惡意用戶輕鬆類比其他使用者。 如果伺服器無法驗證連接權杖,則請求失敗。

![](introduction-to-security/_static/image4.png)

由於連接 ID 是驗證過程的一部分,因此不應向其他使用者顯示一個使用者的連接 ID 或將該值存儲在用戶端上(如 Cookie 中)。

#### <a name="connection-tokens-vs-other-token-types"></a>連線權杖與其他權杖型態

連接令牌偶爾會被安全工具標記,因為它們看起來像是會話令牌或身份驗證令牌,如果暴露,就會造成風險。

SignalR 的連接權杖不是身份驗證權杖。 它用於確認發出此請求的使用者與創建連接的使用者相同。 連接權杖是必需的,因為ASP.NET SignalR允許連接在伺服器之間移動。 令牌將連接與特定使用者關聯,但不斷言發出請求的使用者的身份。 要對 SignalR 請求進行正確身份驗證,它必須具有一些其他維護使用者身份的權杖,例如 Cookie 或承載權杖。 但是,連接權杖本身不聲明請求是由該使用者發出,只是聲明令牌中包含的連接ID與該使用者相關聯。

由於連接權杖不提供自己的身份驗證聲明,因此它不被視為"工作階段"或"身份驗證"權杖。 獲取給定使用者的連接權杖並在作為其他使用者(或未身份驗證的請求)身份驗證的請求中重播該權杖將失敗,因為請求的使用者標識和存儲在權杖中的標識不匹配。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新連線時重新加入群組

默認情況下,SignalR 應用程式在從臨時中斷重新連接時(例如連接在連接超時之前斷開和重新建立連接時)時,將自動將使用者重新分配給相應的組。重新連接時,客戶端傳遞一個組權杖,其中包含連接ID和分配的組。 組令牌經過數位簽名和加密。 用戶端在重新連接後保留相同的連接 ID;因此,從重新連接的用戶端傳遞的連接ID必須與用戶端使用以前的連接ID匹配。 此驗證可防止惡意使用者在重新連接時傳遞加入未授權組的請求。

但是,請務必注意,組令牌不會過期。 如果用戶過去屬於一個組,但被禁止從該組,該使用者可能能夠類比包含禁止組的組令牌。 如果需要安全地管理哪些用戶屬於哪些組,則需要將數據存儲在伺服器上,例如資料庫中。 然後,向應用程式添加邏輯,以驗證伺服器上的使用者是否屬於組。 驗證組成員身份的範例,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

僅當連接在臨時中斷後重新連接時,自動重新加入組才適用。 如果用戶通過導航離開應用程式而斷開連接,或者應用程式重新啟動,則應用程式必須處理如何將該使用者添加到正確的組。 有關詳細資訊,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>信號器如何防止跨網站請求偽造

跨網站請求偽造 (CSRF) 是惡意網站向使用者當前登錄的易受攻擊網站發送請求的攻擊。 SignalR 透過使惡意站點極不可能為 SignalR 應用程式建立有效請求來防止 CSRF。

### <a name="description-of-csrf-attack"></a>CSRF 攻擊的描述

下面是 CSRF 攻擊的範例:

1. 使用者使用表單身份驗證登錄到www.example.com。
2. 伺服器對用戶進行身份驗證。 來自伺服器的回應包括身份驗證 Cookie。
3. 無需註銷,使用者將訪問惡意網站。 此惡意網站包含以下 HTML 表單:

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   請注意,表單操作發佈到易受攻擊的網站,而不是惡意網站。 這是CSRF的「跨網站」部分。
4. 用戶按一下提交按鈕。 瀏覽器包含帶有請求的身份驗證 Cookie。
5. 請求在具有使用者身份驗證上下文的example.com伺服器上運行,並可以執行允許經過身份驗證的使用者執行的任何操作。

儘管此示例要求使用者按下單鍵按鈕,但惡意頁面同樣可以輕鬆地運行向 SignalR 應用程式發送 AJAX 請求的腳稿。 此外,使用 SSL 不會阻止 CSRF 攻擊,因為惡意網站可以發送" HTTPs://請求。

通常,CSRF 攻擊可能會針對使用 Cookie 進行身份驗證的網站,因為瀏覽器會將所有相關 Cookie 發送到目標網站。 但是,CSRF 的攻擊並不僅限於利用 Cookie。 例如,基本身份驗證和摘要身份驗證也容易受到攻擊。 使用者使用「基本」或「摘要」身份驗證登錄後,瀏覽器會自動發送憑據,直到工作階段結束。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 採取的 CSRF 緩解措施

SignalR 採取以下步驟防止惡意網站向應用程式創建有效請求。 默認情況下,SignalR 執行這些步驟,無需在代碼中執行任何操作。

- **關閉跨網域要求**SignalR 禁用跨域請求,以防止使用者從外部域調用 SignalR 終結點。 SignalR 認為來自外部域的任何請求都無效,並阻止請求。 我們建議您保留此默認行為;但是,我們建議您保留此默認行為。否則,惡意網站可能會誘使用戶向您的網站發送命令。 如果需要使用跨域要求,請參閱[如何建立跨域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
- **在查詢字串中傳遞連接權杖,而不是 Cookie**SignalR 將連接權杖作為查詢字串值傳遞,而不是作為Cookie傳遞。 將連接權杖儲存在 Cookie 中不安全,因為當遇到惡意代碼時,瀏覽器可能會無意中轉發連接權杖。 此外,在查詢字串中傳遞連接權杖可防止連接權杖保留在當前連接之外。 因此,惡意使用者不能根據其他使用者的身份驗證憑據發出請求。
- **驗證連線權杖**如[連接權杖](#connectiontoken)部分所述,伺服器知道哪個連接ID與每個經過身份驗證的使用者相關聯。 伺服器不處理來自連接 ID 與使用者名不匹配的任何請求。 惡意使用者不太可能猜到有效請求,因為惡意用戶必須知道使用者名和當前隨機生成的連接 ID。連接 ID 一旦結束,該連接 ID 將變為無效。 匿名使用者不應訪問任何敏感資訊。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>訊號R安全建議

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>安全通訊端字層 (SSL) 協定

SSL 協定使用加密來保護用戶端和伺服器之間的數據傳輸。 如果您的 SignalR 應用程式在用戶端和伺服器之間傳輸敏感資訊,請使用 SSL 進行傳輸。 有關設置 SSL 的詳細資訊,請參閱[如何在 IIS 7 上設置 SSL。](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>不要將群組用作安全機制

組是收集相關使用者的便捷方式,但它們不是限制對敏感資訊訪問的安全機制。 當用戶可以在重新連接期間自動重新加入組時,尤其如此。 相反,請考慮將特權使用者添加到角色,並將對中心方法的訪問限制為該角色的成員。 有關基於角色限制存取的範例,請參閱[SignalR 中心的身份認證與授權](hub-authorization.md)。 有關在重新連線時檢查使用者存取群組的範例,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全地處理來自用戶端的輸入

為了確保惡意使用者不會向其他使用者發送腳本,您必須對用戶端用於廣播到其他用戶端的所有輸入進行編碼。 您應該對接收用戶端而不是伺服器上的消息進行編碼,因為 SignalR 應用程式可能具有許多不同類型的用戶端。 因此,HTML 編碼適用於 Web 用戶端,但對於其他類型的用戶端則不有效。 例如,顯示聊天消息的 Web 用戶端方法可以`html()`通過調用 函數安全地處理使用者名和消息。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>協調使用者狀態變更與活動連線

如果使用者的身份驗證狀態在存在活動連接時發生更改,則使用者將收到一個錯誤,指出「使用者標識在活動 SignalR 連接期間無法更改」。 在這種情況下,應用程式應重新連接到伺服器,以確保連接 ID 和使用者名得到協調。 例如,如果應用程式允許使用者在存在活動連接時註銷,則連接的用戶名將不再與為下一個請求傳入的名稱匹配。 您需要在使用者註銷之前停止連接,然後重新啟動它。

但是,請務必注意,大多數應用程式不需要手動停止並啟動連接。 如果應用程式在註銷後將使用者重定向到單獨的頁面(例如 Web 窗體應用程式或 MVC 應用程式中的默認行為,或在註銷後刷新當前頁面,則活動連接將自動斷開連接,不需要任何其他操作。

下面的範例展示如何在使用者狀態更改時停止和啟動連接。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者,如果您的網站使用表單身份驗證的滑動過期,並且沒有活動保持身份驗證 Cookie 的有效性,則使用者的身份驗證狀態可能會更改。 在這種情況下,使用者將被註銷,用戶名將不再與連接令牌中的使用者名匹配。 您可以通過添加一些腳本來解決此問題,這些腳本定期請求 Web 伺服器上的資源以保持身份驗證 Cookie 的有效性。 下面的示例演示如何每 30 分鐘請求一次資源。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動產生的 JavaScript 代理檔

如果不想在每個使用者的 JavaScript 代理檔中包含所有中心和方法,則可以禁用該檔的自動生成。 如果有多個集線器和方法,但不希望每個使用者都瞭解所有方法,則可以選擇此選項。 通過將**啟用JavaScriptProxie設置為** **false,** 可以禁用自動生成。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

有關 JavaScript 代理檔的詳細資訊,請參閱[產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外狀況

應避免將異常物件傳遞給客戶端,因為物件可能會向用戶端公開敏感資訊。 相反,在顯示相關錯誤消息的用戶端上調用方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
