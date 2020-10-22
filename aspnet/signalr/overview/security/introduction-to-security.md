---
uid: signalr/overview/security/introduction-to-security
title: SignalR 安全性簡介 |Microsoft Docs
author: bradygaster
description: 描述開發 SignalR 應用程式時，您必須考慮的安全性問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345446"
---
# <a name="introduction-to-signalr-security"></a>SignalR 安全性簡介

由 [派翠克 Fletcher](https://github.com/pfletcher)， [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文描述開發 SignalR 應用程式時，您必須考慮的安全性問題。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
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

- [SignalR 安全性概念](#concepts)

    - [驗證與授權](#authentication)
    - [連接權杖](#connectiontoken)
    - [重新連接時重新加入群組](#rejoingroup)
- [SignalR 如何防止跨網站要求偽造](#csrf)
- [SignalR 安全性建議](#recommendations)

    - [ (SSL) 通訊協定的安全通訊端層](#ssl)
    - [請勿使用群組做為安全性機制](#groupsecurity)
    - [安全地處理來自用戶端的輸入](#input)
    - [使用作用中連接協調使用者狀態的變更](#reconcile)
    - [自動產生的 JavaScript proxy 檔案](#autogen)
    - [例外狀況](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a>SignalR 安全性概念

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a>驗證與授權

SignalR 不會提供任何驗證使用者的功能。 相反地，您會將 SignalR 功能整合到應用程式的現有驗證結構中。 您可以像平常在應用程式中驗證使用者，並在您的 SignalR 程式碼中使用驗證的結果。 例如，您可以使用 ASP.NET 表單驗證來驗證使用者，然後在您的中樞內，強制執行哪些使用者或角色有權呼叫方法。 在您的中樞內，您也可以將驗證資訊（例如使用者名稱或使用者所屬角色）傳遞給用戶端。

SignalR 提供 [授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) 屬性，以指定哪些使用者可以存取中樞或方法。 您可以將授權屬性套用至中樞或中樞內的特定方法。 如果沒有授權屬性，中樞上的所有公用方法都可供連線至中樞的用戶端使用。 如需有關中樞的詳細資訊，請參閱 [SignalR 中樞的驗證和授權](hub-authorization.md)。

您將 `Authorize` 屬性套用至中樞，但不是持續連線。 若要在使用時強制執行授權規則 `PersistentConnection` ，您必須覆寫 `AuthorizeRequest` 方法。 如需持續連接的詳細資訊，請參閱 [SignalR 持續連線的驗證和授權](persistent-connection-authorization.md)。

<a id="connectiontoken"></a>

### <a name="connection-token"></a>連接權杖

SignalR 藉由驗證寄件者的身分識別，來降低執行惡意命令的風險。 針對每個要求，用戶端和伺服器都會傳遞一個連線權杖，其中包含已驗證使用者的連接識別碼和使用者名稱。 連接識別碼可唯一識別每個已連線的用戶端。 當建立新的連線時，伺服器會隨機產生連接識別碼，並在連接期間保存該識別碼。 Web 應用程式的驗證機制會提供使用者名稱。 SignalR 使用加密和數位簽章來保護連接權杖。

![](introduction-to-security/_static/image2.png)

針對每個要求，伺服器會驗證權杖的內容，以確保要求是來自指定的使用者。 使用者名稱必須對應到連接識別碼。藉由驗證連線識別碼和使用者名稱，SignalR 可防止惡意使用者輕鬆地模擬另一位使用者。 如果伺服器無法驗證連接 token，則要求會失敗。

![](introduction-to-security/_static/image4.png)

因為連接識別碼是驗證程式的一部分，所以您不應該將一個使用者的連接識別碼顯示給其他使用者，或將值儲存在用戶端上，例如 cookie 中。

#### <a name="connection-tokens-vs-other-token-types"></a>連接權杖與其他權杖類型

連線權杖偶爾會被安全性工具標示，因為它們看起來就像是會話權杖或驗證權杖，如果公開，這會帶來風險。

SignalR 的連線權杖不是驗證權杖。 它是用來確認提出此要求的使用者，與建立該連接的使用者相同。 連接 token 是必要的，因為 ASP.NET SignalR 允許連接在伺服器之間移動。 權杖會將連接與特定使用者建立關聯，但不會判斷提示提出要求之使用者的身分識別。 若要正確驗證 SignalR 要求，它必須有一些其他權杖，以判斷提示使用者的身分識別，例如 cookie 或持有人權杖。 不過，連線權杖本身不會宣告該使用者提出要求，只有權杖中包含的連接識別碼會與該使用者相關聯。

因為連線權杖不提供自己的驗證宣告，所以不會被視為「會話」或「驗證」 token。 取得指定使用者的連線權杖，並在以不同使用者身分驗證的要求中重新執行它 (或未驗證的要求) 將會失敗，因為要求的使用者識別和儲存在權杖中的身分識別不相符。

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a>重新連接時重新加入群組

根據預設，SignalR 應用程式會在從暫時中斷重新連線時，自動將使用者重新指派給適當的群組，例如，當連線中斷並重新建立連接逾時之前。重新連線時，用戶端會傳遞包含連接識別碼和指派群組的群組權杖。 群組權杖會經過數位簽署和加密。 用戶端會在重新連接之後保留相同的連接識別碼;因此，從重新連線的用戶端傳遞的連接識別碼必須符合用戶端所使用的先前連接識別碼。 這種驗證可防止惡意使用者在重新連線時，傳遞要求以加入未經授權的群組。

不過，請務必注意，群組權杖不會過期。 如果使用者屬於過去的群組，但已從該群組中予以禁用，則該使用者可能會模擬包含禁止群組的群組權杖。 如果您需要安全地管理哪些使用者屬於哪些群組，您需要將該資料儲存在伺服器上，例如資料庫中。 然後，將邏輯新增至您的應用程式，以在伺服器上驗證使用者是否屬於群組。 如需驗證群組成員資格的範例，請參閱 [使用群組](../guide-to-the-api/working-with-groups.md)。

自動重新加入群組只適用于在暫時性中斷後重新連線時。 如果使用者離開應用程式或應用程式重新開機而中斷連線，您的應用程式必須處理如何將該使用者新增至正確的群組。 如需詳細資訊，請參閱使用 [群組](../guide-to-the-api/working-with-groups.md)。

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a>SignalR 如何防止跨網站要求偽造

跨網站偽造要求 (CSRF) 是一種攻擊，惡意網站會將要求傳送至使用者目前登入的易受攻擊網站。 SignalR 可讓惡意網站極不太可能為您的 SignalR 應用程式建立有效的要求，以防止 CSRF。

### <a name="description-of-csrf-attack"></a>CSRF 攻擊的描述

以下是 CSRF 攻擊的範例：

1. 使用者使用表單驗證登入 www.example.com。
2. 伺服器會驗證使用者。 伺服器的回應包含驗證 cookie。
3. 如果沒有登出，使用者會造訪惡意網站。 此惡意網站包含下列 HTML 格式：

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   請注意，表單動作會張貼到易受攻擊的網站，而不是惡意網站。 這是 CSRF 的「跨網站」部分。
4. 使用者按一下 [提交] 按鈕。 瀏覽器包含驗證 cookie 與要求。
5. 要求會以使用者的驗證內容在 example.com 伺服器上執行，而且可以執行已驗證的使用者可以執行的任何動作。

雖然此範例需要使用者按一下 [表單] 按鈕，但是惡意網頁可以輕鬆地執行腳本，將 AJAX 要求傳送到您的 SignalR 應用程式。 此外，使用 SSL 並無法防止 CSRF 攻擊，因為惡意網站可以傳送「HTTPs://」要求。

一般來說，使用 cookie 進行驗證的網站可能會 CSRF 攻擊，因為瀏覽器會將所有相關的 cookie 傳送至目的地網站。 不過，CSRF 攻擊並不限於利用 cookie。 例如，基本和摘要式驗證也很容易受到攻擊。 在使用者使用基本或摘要式驗證登入之後，瀏覽器會自動傳送認證，直到會話結束為止。

### <a name="csrf-mitigations-taken-by-signalr"></a>CSRF SignalR 所採取的緩和措施

SignalR 會採取下列步驟，以防止惡意網站對您的應用程式建立有效的要求。 SignalR 預設會採取這些步驟，您不需要在程式碼中採取任何動作。

- **停用跨網域要求** SignalR 會停用跨網域要求，以防止使用者從外部網域呼叫 SignalR 端點。 SignalR 會將外部網域的任何要求視為無效，並封鎖要求。 建議您保留這個預設行為;否則，惡意網站可以誘騙使用者將命令傳送至您的網站。 如果您需要使用跨網域要求，請參閱     [如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) 。
- **在查詢字串中傳遞連接 token，而不是 cookie** SignalR 會將連接 token 傳遞為查詢字串值，而不是 cookie。 將連接權杖儲存在 cookie 中是不安全的，因為當遇到惡意程式碼時，瀏覽器可能會不慎轉寄連接權杖。 此外，在查詢字串中傳遞連接 token 可防止連接權杖在目前的連接之外保存。 因此，惡意使用者無法在其他使用者的驗證認證下提出要求。
- **驗證連接權杖** 如「連線     [權杖](#connectiontoken) 」一節所述，伺服器會知道哪個連接識別碼與每個已驗證的使用者相關聯。 伺服器不會處理任何來自不符合使用者名稱之連接識別碼的要求。 惡意使用者可能會猜到有效的要求，因為惡意使用者必須知道使用者名稱和目前隨機產生的連接識別碼。連接結束時，該連線識別碼就會變成無效。 匿名使用者應該無法存取任何敏感性資訊。

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a>SignalR 安全性建議

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a> (SSL) 通訊協定的安全通訊端層

SSL 通訊協定會使用加密來保護用戶端與伺服器之間的資料傳輸。 如果您的 SignalR 應用程式會在用戶端與伺服器之間傳輸機密資訊，請使用 SSL 進行傳輸。 如需設定 SSL 的詳細資訊，請參閱 [如何在 IIS 7 上設定 ssl](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)。

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a>請勿使用群組做為安全性機制

群組是一個便利的方式，可收集相關的使用者，但它們不是限制存取機密資訊的安全機制。 當使用者可以在重新連線期間自動重新加入群組時，更是如此。 相反地，請考慮將具特殊許可權的使用者新增至角色，並將中樞方法的存取限制為只有該角色的成員。 如需根據角色限制存取的範例，請參閱 [SignalR 中樞的驗證和授權](hub-authorization.md)。 如需在重新連接時檢查使用者對群組的存取權的範例，請參閱 [使用群組](../guide-to-the-api/working-with-groups.md)。

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a>安全地處理來自用戶端的輸入

若要確保惡意使用者不會將腳本傳送給其他使用者，您必須針對要廣播給其他用戶端的用戶端，將所有輸入編碼。 因為您的 SignalR 應用程式可能會有許多不同類型的用戶端，所以您應該在接收用戶端而不是伺服器上編碼訊息。 因此，HTML 編碼適用于 web 用戶端，但不適用於其他類型的用戶端。 例如，用來顯示聊天訊息的 web 用戶端方法，會藉由呼叫函數安全地處理使用者名稱和訊息 `html()` 。

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a>使用作用中連接協調使用者狀態的變更

如果使用者的驗證狀態在使用中連線存在時變更，使用者將會收到錯誤，指出「使用者身分識別無法在作用中的 SignalR 連線期間變更」。 在這種情況下，您的應用程式應該重新連接到伺服器，以確定連接識別碼和使用者名稱是協調的。 例如，如果您的應用程式允許使用者登出，而使用中的連線存在，則連接的使用者名稱將不再符合下一個要求所傳入的名稱。 您會想要在使用者登出之前停止連接，然後重新開機。

不過，請務必注意，大部分的應用程式都不需要手動停止和啟動連接。 如果您的應用程式在登出之後將使用者重新導向至另一個頁面（例如 Web Form 應用程式或 MVC 應用程式中的預設行為），或在登出後重新整理目前的頁面，則使用中的連接會自動中斷連線，而且不需要任何額外的動作。

下列範例顯示如何在使用者狀態變更時停止和啟動連接。

[!code-html[Main](introduction-to-security/samples/sample3.html)]

或者，如果您的網站使用表單驗證的滑動過期，則使用者的驗證狀態可能會變更，而且沒有可讓驗證 cookie 保持有效的活動。 在此情況下，使用者將會被登出，且使用者名稱將不再符合連接權杖中的使用者名稱。 您可以新增一些腳本，定期要求 web 伺服器上的資源，讓驗證 cookie 保持有效，以修正此問題。 下列範例說明如何每隔30分鐘要求一次資源。

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a>自動產生的 JavaScript proxy 檔案

如果您不想要將所有的中樞和方法包含在每位使用者的 JavaScript proxy 檔案中，您可以停用自動產生檔案。 如果您有多個中樞和方法，但不希望每個使用者都知道所有方法，您可以選擇此選項。 您可以將 **EnableJavaScriptProxies** 設定為 **false**，以停用自動產生。

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

如需有關 JavaScript proxy 檔案的詳細資訊，請參閱 [產生的 proxy 以及它對您的](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)功用。 <a id="exceptions"></a>

### <a name="exceptions"></a>例外狀況

您應該避免將例外狀況物件傳遞給用戶端，因為這些物件可能會將機密資訊公開給用戶端。 相反地，請在用戶端上呼叫會顯示相關錯誤訊息的方法。

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
