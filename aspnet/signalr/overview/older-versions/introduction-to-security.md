---
uid: signalr/overview/older-versions/introduction-to-security
title: SignalR 安全性簡介 (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: 描述開發 SignalR 應用程式時，您必須考慮的安全性問題。
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 715a4059-d307-4631-abbb-c789c95d6eb4
msc.legacyurl: /signalr/overview/older-versions/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 08106dd6df491da817e0d449e85a09a8bc0fc77c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422053"
---
# <a name="introduction-to-signalr-security-signalr-1x"></a>SignalR 安全性簡介 (SignalR 1.x)

藉由[Patrick Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明開發 SignalR 應用程式時，您必須考慮的安全性問題。


## <a name="overview"></a>總覽

本文件包含下列章節：

- [SignalR 安全性概念](#concepts)

    - [驗證與授權](#authentication)
    - [連線語彙基元](#connectiontoken)
    - [重新連線時，重新加入群組](#rejoingroup)
- [SignalR 如何防止跨網站偽造要求](#csrf)
- [SignalR 安全性建議](#recommendations)

    - [安全通訊端層 (SSL) 通訊協定](#ssl)
    - [做為安全性機制，不使用群組](#groupsecurity)
    - [安全地處理來自用戶端的輸入](#input)
    - [使用中連線的使用者狀態的變更，重新調整](#reconcile)
    - [自動產生的 JavaScript proxy 檔案](#autogen)
    - [例外狀況](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 安全性概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>驗證與授權

SignalR 被設計來整合到現有的應用程式的驗證結構。 它不提供任何功能來驗證使用者。 相反地，您驗證使用者，因為您通常會在您的應用程式，然後會使用 SignalR 的程式碼中的驗證結果。 例如，您可以驗證您的使用者，使用 ASP.NET 表單驗證，並接著在您的中樞，強制執行哪些使用者或角色有權呼叫的方法。 在您的中樞，您也可以傳遞驗證資訊，例如使用者名稱或使用者是否屬於的角色，用戶端。

提供 SignalR[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性來指定哪些使用者可以存取的集線器或方法。 您將 Authorize 屬性套用至中樞或中樞內的特定方法時。 沒有授權屬性，該中樞上的所有公用方法可連線至中樞的用戶端。 如需中樞的詳細資訊，請參閱[SignalR 中樞的驗證和授權](../security/hub-authorization.md)。

`Authorize`屬性僅適用於中樞。 若要強制執行時使用授權規則`PersistentConnection`您必須覆寫`AuthorizeRequest`方法。 如需持續連線的詳細資訊，請參閱[SignalR 持續連線的驗證和授權](../security/persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>連線語彙基元

SignalR 降低執行惡意的命令來驗證寄件者的身分識別的風險。 包含連線識別碼和已驗證的使用者的使用者名稱的連線語彙基元會傳遞用戶端與伺服器之間，針對每個要求。 連線識別碼是會在建立時，新的連接，而連線期間會一直保存隨機伺服器所產生的唯一識別碼。 Web 應用程式的驗證機制會提供使用者名稱。 受保護的連線語彙基元加密和數位簽章。

![](introduction-to-security/_static/image2.png)

針對每個要求，伺服器會驗證權杖，以確保要求來自指定之使用者的內容。 使用者名稱必須對應到的連線識別碼。藉由驗證的連線識別碼，而使用者名稱，SignalR 可以防止惡意使用者在輕鬆模擬另一位使用者。 如果伺服器無法驗證的連線語彙基元，要求將會失敗。

![](introduction-to-security/_static/image4.png)

因為連線識別碼是在驗證程序的一部分，不應該顯示給其他使用者的一位使用者的連線識別碼，或這類的用戶端上的值儲存在 cookie 中。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新連線時，重新加入群組

根據預設，SignalR 應用程式會自動重新將使用者指派給適當的群組從暫時中斷，例如當卸除並重新建立連線逾時之前連線重新連線時。當重新連接後，用戶端會傳遞包含連線識別碼和指派的群組的群組語彙基元。 以數位方式簽署及加密的群組語彙基元。 用戶端重新連線; 之後，保留相同的連線識別碼因此，從重新連線的用戶端傳遞的連線識別碼必須符合用戶端使用先前的連線識別碼。 此驗證可防止惡意使用者傳遞要求加入未經授權的群組，當重新連線。

不過，它是特別注意，群組語彙基元不會過期。 如果使用者屬於群組，在過去，但是已被禁用，從該群組，則該使用者，將可以模擬包含禁止的群組的群組語彙基元。 如果您需要安全地管理哪些使用者屬於哪些群組，您需要在資料庫中，例如儲存在伺服器上，該資料。 然後，將邏輯加入至您在伺服器驗證使用者是否屬於群組的應用程式中。 如需的驗證群組成員資格的範例，請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。

自動重新加入群組時，才適用連接會暫時中斷之後重新連線。 如果使用者中斷連線的巡覽離開應用程式或應用程式重新啟動，您的應用程式必須處理如何將該使用者新增至正確的群組。 如需詳細資訊，請參閱 <<c0> [ 使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR 如何防止跨網站偽造要求

跨站台要求偽造 (CSRF) 攻擊會將惡意網站傳送要求給使用者目前登入的有弱點網站的位置。 SignalR 以防止 CSRF 進行惡意的網站，才能建立有效的要求，您的 SignalR 應用程式非常不可能。

### <a name="description-of-csrf-attack"></a>CSRF 攻擊的描述

CSRF 攻擊的範例如下：

1. 使用者登入`www.example.com`，使用表單驗證。
2. 伺服器會驗證使用者。 來自伺服器的回應包含驗證 cookie。
3. 而不需要登出，使用者會造訪惡意的網站。 此惡意的網站包含 HTML 格式如下： 

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   請注意，張貼至易受攻擊的站台，不必惡意網站的表單動作。 這是 CSRF 的 「 跨站台 」 部分。
4. 使用者按一下 [提交] 按鈕。 瀏覽器會包含與要求的驗證 cookie。
5. 要求使用者的驗證內容，example.com 伺服器上執行，而且可以執行的任何已驗證的使用者能夠執行的動作項目。

雖然此範例中所需的使用者可以按一下 [表單] 按鈕，惡意的頁面無法的身分執行的指令碼，將 AJAX 要求傳送至您的 SignalR 應用程式。 此外，使用 SSL 不會防止 CSRF 攻擊中，因為惡意的網站可傳送"https://"要求。

一般而言，CSRF 攻擊是可能對網站使用 cookie 進行驗證，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。 不過，不一定要利用 cookie CSRF 攻擊。 例如，基本和摘要式驗證也是易受攻擊。 使用者登入時基本或摘要式驗證之後，瀏覽器將會自動傳送認證到工作階段結束為止。

### <a name="csrf-mitigations-taken-by-signalr"></a>SignalR 所採取的 CSRF 防護功能

SignalR 採取下列步驟以建立您的 SignalR 應用程式的有效要求時，防止惡意網站。 這些步驟會依預設，不需要在程式碼中的任何動作。

- **停用跨網域要求**  
 根據預設，跨網域要求中已停用的 SignalR 應用程式，以防止使用者呼叫 SignalR 端點來自外部網域。 任何來自外部網域的要求會自動被視為無效，而被封鎖。 建議您保留這個預設行為。否則，惡意網站可能誘騙使用者將命令傳送給您的網站。 如果您需要使用跨網域要求，請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。
- **傳入查詢字串，不 cookie 中的連線語彙基元**  
 SignalR 會當做 cookie，而不是傳遞查詢字串值的連線語彙基元。 不為 cookie 中儲存的連線語彙基元的連線語彙基元不小心透過轉送瀏覽器發生惡意程式碼時。 此外，連線語彙基元不會保存超過目前的連接。 因此，惡意使用者不能以其他使用者的驗證認證的要求。
- **確認連線語彙基元**  
 中所述[連線語彙基元](#connectiontoken) 區段中，伺服器可讓您知道哪一個連接識別碼是與每個已驗證的使用者相關聯。 伺服器不會處理來自使用者名稱不相符之連線識別碼的任何要求。 不可能的惡意使用者猜到正確的要求因為惡意使用者必須知道的使用者名稱和目前的隨機產生的連線識別碼。只要結束連接時，該連線識別碼就會變成無效。 匿名使用者不應該將任何機密資訊的存取。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 安全性建議

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a>安全通訊端層 (SSL) 通訊協定

SSL 通訊協定會使用加密來保護用戶端與伺服器之間的資料傳輸。 如果您的 SignalR 應用程式傳輸用戶端與伺服器之間的機密資訊，請使用 SSL 傳輸。 如需有關設定 SSL 的詳細資訊，請參閱 <<c0> [ 如何設定 IIS 7 上的 SSL](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>做為安全性機制，不使用群組

群組是便利的方式收集相關的使用者，但它們不安全的機制，以便限制存取機密資訊。 當使用者可以自動重新加入群組的重新連線期間，這是特別有用。 相反地，請考慮新增至角色的權限的使用者，並限制只有該角色的成員到中樞方法的存取。 如需根據角色限制存取的範例，請參閱 < [SignalR 中樞的驗證和授權](../security/hub-authorization.md)。 檢查使用者存取群組，重新連接時的範例，請參閱 <<c0> [ 使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全地處理來自用戶端的輸入

必須編碼所有來自用戶端的輸入，以供其他用戶端的廣播，以確保惡意使用者不會對其他使用者傳送指令碼。 最好是來編碼訊息接收的用戶端，而不是在伺服器上，因為您的 SignalR 應用程式可能有許多不同類型的用戶端。 因此，HTML 編碼適用於 web 用戶端，但不適用於其他類型的用戶端。 例如，web 用戶端方法，以顯示在聊天訊息會安全地處理的使用者名稱和訊息藉由呼叫`html()`函式。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>使用中連線的使用者狀態的變更，重新調整

如果使用者的驗證狀態會變更作用中連線存在時，使用者會收到錯誤訊息、 「 作用中的 SignalR 連線期間無法變更使用者的身分識別 」。 在此情況下，您的應用程式應重新連接到伺服器，以確定使用者名稱與連接識別碼進行協調。 例如，如果您的應用程式可讓使用者登出的作用中連接存在時，連接的使用者名稱將不再符合下一個要求傳入的名稱。 您想要停止連線，才能在使用者登出時，以及再重新啟動它。

不過，務必請注意，大部分的應用程式不需要手動停止和啟動的連線。 如果您的應用程式會將使用者重新導向至另一個頁面記錄處理程序，例如 Web Form 應用程式或 MVC 應用程式的預設行為，或登出之後會重新整理目前的頁面，作用中連線會自動中斷連線，而不需要採取任何其他動作。

下列範例示範如何停止和啟動的連線，使用者狀態變更時。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者，如果您的網站使用表單驗證，使用滑動期限，而且沒有任何活動，將有效的驗證 cookie，可能會變更使用者的驗證狀態。 在此情況下，會將使用者登出，使用者名稱將不再符合的連線語彙基元中的使用者名稱。 您可以藉由新增一些指令碼定期要求要保持有效的驗證 cookie 的 web 伺服器上的資源來修正這個問題。 下列範例示範如何要求資源每隔 30 分鐘。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動產生的 JavaScript proxy 檔案

如果您不想在每個使用者的 JavaScript proxy 檔案中包含所有中樞和方法，您可以停用自動產生的檔案。 如果您有多個中樞和方法，但不是想要注意的所有方法的每位使用者，您可能會選擇此選項。 您設定停用自動產生**EnableJavaScriptProxies**要**false**。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

如需 JavaScript proxy 檔案的詳細資訊，請參閱[產生的 proxy，它會為您](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外狀況

您應該避免將例外狀況物件傳遞至用戶端，因為物件可能會公開機密資訊的用戶端。 相反地，會顯示相關的錯誤訊息的用戶端上呼叫方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
