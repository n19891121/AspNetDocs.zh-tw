---
uid: mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
title: ASP.NET MVC 和 Web Pages 中的 XSRF/CSRF 防護 |Microsoft Docs
author: Rick-Anderson
description: 跨網站偽造要求 (也稱為 XSRF 或 CSRF) 是針對 web 裝載的應用程式進行攻擊，而惡意的網站可能會影響 interacti .。。
ms.author: riande
ms.date: 03/14/2013
ms.assetid: aadc5fa4-8215-4fc7-afd5-bcd2ef879728
msc.legacyurl: /mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages
msc.type: authoredcontent
ms.openlocfilehash: 7c45e342bc55ece3a6b41dcc42a0f33cd3eceffd
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151861"
---
# <a name="xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages"></a>ASP.NET MVC 和 ASP.NET Web Pages 中的 XSRF/CSRF 防護

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

> 跨網站要求偽造 (也稱為 XSRF 或 CSRF) 是針對 web 裝載的應用程式進行攻擊，而惡意網站可能會影響用戶端瀏覽器和該瀏覽器所信任之網站之間的互動。 這些攻擊的原因可能是因為網頁瀏覽器會在每個網站要求時自動傳送驗證權杖。 ASP.NET 的 Forms Authentication 票證即是驗證 Cookie 的標準範例。 不過，使用任何持續性驗證機制 (例如 Windows 驗證、基本等等) 的網站，可能會以這些攻擊為目標。
> 
> XSRF 攻擊與網路釣魚攻擊不同。 網路釣魚攻擊需要與受害者互動。 在網路釣魚攻擊中，惡意網站將模仿目標網站，而犧牲者愚弄將敏感性資訊提供給攻擊者。 XSRF 攻擊則通常不需要與受害者互動。 相反地，攻擊者會依賴瀏覽器自動將所有相關的 cookie 傳送至目的地網站。
> 
> 如需詳細資訊，請參閱 [開放式 Web 應用程式安全性專案](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))。

## <a name="anatomy-of-an-attack"></a>攻擊的剖析

若要逐步進行 XSRF 攻擊，請考慮想要執行一些線上銀行交易的使用者。 此使用者會先造訪 WoodgroveBank.com 並登入，此時回應標頭會包含她的驗證 cookie：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample1.cmd)]

因為驗證 cookie 是會話 cookie，所以瀏覽器會在瀏覽器進程結束時自動清除。 不過，在這段時間之前，瀏覽器會自動在每個要求中包含 WoodgroveBank.com 的 cookie。 使用者現在想要將 $1000 傳送到另一個帳戶，因此她填滿銀行網站上的表單，而瀏覽器會向伺服器提出此要求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample2.cmd)]

因為這項作業有副作用 (它會起始) 的貨幣交易，所以銀行網站已選擇要求 HTTP POST 以起始此作業。 伺服器會從要求中讀取驗證權杖、查閱目前使用者的帳戶號碼、確認有足夠的資金，然後將交易起始到目的地帳戶。

她的線上銀行完成，使用者離開銀行網站，並造訪網路上的其他位置。 其中一個網站– fabrikam.com –在 iframe 中內嵌的頁面上包含下列標記 &lt; &gt; ：

[!code-html[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample3.html)]

然後，瀏覽器會提出此要求：

[!code-console[Main](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/samples/sample4.cmd)]

攻擊者使用的事實是，使用者可能仍有目標網站的有效驗證權杖，而且她使用一小段 JAVAscript 來讓瀏覽器自動對目標網站發出 HTTP POST。 如果驗證權杖仍然有效，則銀行網站將會起始將 $250 傳送到攻擊者所選擇的帳戶。

### <a name="ineffective-mitigations"></a>不正確緩和措施

值得注意的是，在上述案例中，WoodgroveBank.com 是透過 SSL 存取，並具有僅限 SSL 的驗證 cookie，不足以防止攻擊。 攻擊者可以在其 form 元素中指定 (HTTPs) 的 [URI 配置](http://en.wikipedia.org/wiki/URI_scheme) &lt; &gt; ，且只要這些 cookie 與預定目標的 URI 配置一致，瀏覽器就會繼續將未到期的 cookie 傳送到目標網站。

其中一個人可能會認為使用者不應該直接造訪不受信任的網站，因為僅造訪信任的網站可協助保持線上安全。 這項功能有一些事實，但不幸的是，這項建議並非永遠可行。 也許使用者「信任」當地新聞網站 ConsolidatedMessenger.com，並改為造訪該網站，但是該網站有 XSS 弱點，可讓攻擊者插入在 fabrikam.com 上執行的相同程式碼片段。

您可以驗證連入要求的 [推薦者標頭](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 是否參考您的網域。 這會停止從協力廠商網域中不知情提交的要求。 不過，有些人會基於隱私權原因停用其瀏覽器的推薦者標頭，而攻擊者有時可能會詐騙該標頭（如果受害者已安裝某些不安全的軟體）。 確認 [推薦者標頭](http://www.w3.org/Protocols/HTTP/HTRQ_Headers.html#z14) 不會被視為防止 XSRF 攻擊的安全方法。

## <a name="web-stack-runtime-xsrf-mitigations"></a>Web Stack 執行時間 XSRF 緩和措施

ASP.NET Web Stack 執行時間會使用 [同步器權杖模式](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html#synchronizer-token-pattern) 的變體來防禦 XSRF 攻擊。 同步器權杖模式的一般形式是，除了驗證權杖) 之外，還會將兩個反 XSRF token 提交到伺服器 (：一個權杖作為 cookie，另一個則為表單值。 ASP.NET 執行時間所產生的權杖值不具決定性，也不能由攻擊者預測。 提交權杖時，伺服器只會在兩個權杖都通過比較檢查時，才允許要求繼續進行。

XSRF 要求驗證 *會話權杖* 會儲存為 HTTP cookie，而且目前在其承載中包含下列資訊：

- 由隨機128位識別碼組成的安全性權杖。   
 下圖顯示 Internet Explorer F12 開發人員工具所顯示的 XSRF 要求驗證會話權杖： (注意這是目前的執行，甚至可能變更。 ) 

![](xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages/_static/image1.png)

*欄位標記* 會儲存為 `<input type="hidden" />` ，並在其承載中包含下列資訊：

- 登入使用者的使用者名稱 (（如果已驗證) ）。
- [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)所提供的任何其他資料。

XSRF token 的承載會經過加密及簽署，因此當您使用工具來檢查權杖時，就無法查看使用者名稱。 當 web 應用程式以 ASP.NET 4.0 為目標時，密碼編譯服務會由 [MachineKey 提供。編碼](https://msdn.microsoft.com/library/system.web.security.machinekey.encode.aspx) 常式。 當 web 應用程式以 ASP.NET 4.5 或更高版本為目標時，MachineKey 會提供密碼編譯服務 [。保護](https://msdn.microsoft.com/library/system.web.security.machinekey.protect(v=vs.110)) 常式可提供更佳的效能、擴充性和安全性。 如需詳細資訊，請參閱下列 blog 文章：

- [ASP.NET 4.5，pt 中的密碼編譯增強功能](https://blogs.msdn.com/b/webdev/archive/2012/10/22/cryptographic-improvements-in-asp-net-4-5-pt-1.aspx)
- [ASP.NET 4.5，pt 中的密碼編譯增強功能](https://blogs.msdn.com/b/webdev/archive/2012/10/23/cryptographic-improvements-in-asp-net-4-5-pt-2.aspx)
- [ASP.NET 4.5 的密碼編譯增強功能，pt. 3](https://blogs.msdn.com/b/webdev/archive/2012/10/24/cryptographic-improvements-in-asp-net-4-5-pt-3.aspx)

## <a name="generating-the-tokens"></a>產生權杖

若要產生反 XSRF 權杖，請 [@Html.AntiForgeryToken](https://msdn.microsoft.com/library/dd470175.aspx) 從 MVC 視圖呼叫方法，或 @AntiForgery.GetHtml 從 Razor 頁面 ( # A1。 執行時間會接著執行下列步驟：

1. 如果目前的 HTTP 要求已包含反 XSRF 會話權杖 (XSRF cookie \_ \_ RequestVerificationToken) ，則會從它解壓縮安全性權杖。 如果 HTTP 要求不包含反 XSRF 會話權杖，或安全性權杖的解壓縮失敗，則會產生新的隨機反 XSRF token。
2. XSRF 欄位標記是使用步驟 (1) 的安全性權杖，以及目前登入使用者的身分識別產生的。  (如需判斷使用者身分識別的詳細資訊，請參閱下面的 **[特殊支援的案例](#_Scenarios_with_special)** 。 ) 此外，如果已設定 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/jj158328(v=vs.111).aspx) ，執行時間會呼叫其 [GetAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.getadditionaldata(v=vs.111).aspx) 方法，並將傳回的字串包含在欄位標記中。  (如需詳細資訊，請參閱設定 **[和](#_Configuration_and_extensibility)** 擴充性一節。 ) 
3. 如果在步驟 (1) 中產生新的防 XSRF token，則會建立新的會話權杖以包含該權杖，並將其新增至輸出 HTTP cookie 集合。 步驟 (2) 的欄位 token 將包裝在 `<input type="hidden" />` 元素中，而這個 HTML 標籤將是或的傳回值 `Html.AntiForgeryToken()` `AntiForgery.GetHtml()` 。

## <a name="validating-the-tokens"></a>驗證權杖

若要驗證傳入的反 XSRF token，開發人員會在其 MVC 動作或控制器上包含 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(VS.108).aspx) 屬性，或 `@AntiForgery.Validate()` 從她的 Razor 頁面進行呼叫。 執行時間將執行下列步驟：

1. 系統會讀取傳入會話權杖和欄位權杖，並從每個權杖中解壓縮反 XSRF token。 XSRF 權杖在產生常式中的每個步驟 (2) 都必須相同。
2. 如果目前的使用者已通過驗證，她的使用者名稱會與儲存在欄位 token 中的使用者名稱進行比較。 使用者名稱必須相符。
3. 如果已設定 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) ，執行時間會呼叫其 *ValidateAdditionalData* 方法。 方法必須傳回布林值 *true*。

如果驗證成功，則允許要求繼續進行。 如果驗證失敗，架構將會擲回 *HttpAntiForgeryException*。

## <a name="failure-conditions"></a>失敗狀況

從 ASP.NET Web Stack Runtime v2 開始，驗證期間擲回的任何 *HttpAntiForgeryException* 將會包含發生錯誤的詳細資訊。 目前定義的失敗狀況如下：

- 要求中不存在會話權杖或表單權杖。
- 無法讀取會話權杖或表單權杖。 最可能的原因是伺服器陣列執行的 ASP.NET Web Stack 執行時間不相符，或伺服器陣列 &lt; 中 Web.config 的 machineKey &gt; 元素不同。 您可以使用 Fiddler 之類的工具來強制執行此例外狀況，方法是使用反 XSRF token 來進行篡改。
- 會話權杖和欄位標記已交換。
- 會話權杖和欄位標記包含不相符的安全性權杖。
- 內嵌在欄位標記中的使用者名稱與目前登入使用者的使用者名稱不相符。
- *[IAntiForgeryAdditionalDataProvider. ValidateAdditionalData](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider.validateadditionaldata(v=vs.111).aspx)* 方法傳回 *false*。

防 XSRF 設施也可能在權杖產生或驗證期間執行額外檢查，而這些檢查期間的失敗可能會導致擲回例外狀況。 如需詳細資訊，請參閱 [WIF/ACS/宣告式驗證](#_WIF_ACS) 和設定 **[和](#_Configuration_and_extensibility)** 擴充性章節。

<a id="_Scenarios_with_special"></a>

## <a name="scenarios-with-special-support"></a>具有特殊支援的案例

### <a name="anonymous-authentication"></a>匿名驗證

反 XSRF 系統包含匿名使用者的特殊支援，其中「匿名」定義為使用者，其中 *IIdentity. IsAuthenticated* 屬性會傳回 *false*。 案例包括將 XSRF 保護提供給登入頁面 (在使用者經過驗證之後) 和自訂驗證配置，其中應用程式會使用 *IIdentity* 以外的機制來識別使用者。

若要支援這些案例，請記得會話和欄位標記是由安全性權杖所聯結，這是一個128位隨機產生的不透明識別碼。 此安全性權杖可用來在流覽網站時追蹤個別使用者的會話，因此它會有效地提供匿名識別碼的用途。 空字串用來取代上述產生和驗證常式的使用者名稱。

<a id="_WIF_ACS"></a>

### <a name="wif--acs--claims-based-authentication"></a>WIF/ACS/宣告式驗證

一般來說，內建于 .NET Framework 的 *IIdentity* 類別具有 *IIdentity.Name* 足夠的屬性，可唯一識別特定應用程式內的特定使用者。 例如， *FormsIdentity.Name* 會傳回儲存在成員資格資料庫中的使用者名稱 (這對所有應用程式而言都是唯一的，因為該資料庫) 、 *WindowsIdentity.Name* 會傳回使用者的網域限定身分識別等等。 這些系統不僅提供驗證，它們也會 *識別* 應用程式的使用者。

另一方面，以宣告為基礎的驗證不一定需要識別特定的使用者。 相反地， *ClaimsPrincipal* 和 *ClaimsIdentity* 類型會與一組宣告實例相關聯，其中個別宣告可能是 "是 18 + 年的年齡" 或 "是系統管理員 *" 的任何* 其他宣告。 因為不一定會識別使用者，所以執行時間不能使用 *ClaimsIdentity.Name* 屬性做為此特定使用者的唯一識別碼。 小組已經看過真實世界的範例，其中的 *ClaimsIdentity.Name* 會傳回 *null*、傳回易記的 (顯示) 名稱，或傳回不適合做為使用者唯一識別碼的字串。

許多使用宣告式驗證的部署都是使用 [Azure 存取控制服務](https://msdn.microsoft.com/library/windowsazure/gg429786.aspx) (ACS) 。 ACS 可讓開發人員設定個別的身分 *識別提供 (者* ，例如 ADFS、Microsoft 帳戶提供者、OpenID 提供者（例如 yahoo！等） ) ，以及身分識別提供者傳回 *名稱識別碼*。 這些名稱識別碼可能包含個人識別資訊 (PII) 例如電子郵件地址，也可以像私人個人識別碼 (PPID) 一樣匿名。 無論是哪一種，元組 (身分識別提供者、名稱識別碼) 足以作為特定使用者在流覽網站時的適當追蹤權杖，所以 ASP.NET Web Stack 執行時間可以在產生並驗證反 XSRF 欄位 token 時，使用元組取代使用者名稱。 身分識別提供者和名稱識別碼的特定 Uri 如下：

- `https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider`
- `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`

 (如需詳細資訊，請參閱此 [ACS doc 頁面](https://msdn.microsoft.com/library/windowsazure/gg185971.aspx) 。 ) 

產生或驗證權杖時，ASP.NET Web Stack 執行時間會在執行時間嘗試系結至類型：

- `Microsoft.IdentityModel.Claims.IClaimsIdentity, Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35` WIF SDK 的 (。 ) 
- `System.Security.Claims.ClaimsIdentity` 適用于 .NET 4.5) 的 (。

如果這些類型存在，而且目前使用者的 *IIIIdentity* 會執行其中一種類型，則反 XSRF 設備會使用 (識別提供者、名稱識別碼) 元組來取代在產生和驗證權杖時的使用者名稱。 如果沒有這樣的元組，要求將會失敗，並出現錯誤，說明開發人員如何設定防 XSRF 系統，以瞭解使用中的特定宣告式驗證機制。 如需詳細資訊，請參閱設定 **[和](#_Configuration_and_extensibility)** 擴充性一節。

### <a name="oauth--openid-authentication"></a>OAuth/OpenID 驗證

最後，反 XSRF 設備對使用 OAuth 或 OpenID 驗證的應用程式具有特殊支援。 這項支援是以啟發學習法為基礎：如果目前 *IIdentity.Name* 的開頭是 HTTP://或 HTTPs://，則會使用序數比較子來進行使用者名稱比較，而不是使用預設 OrdinalIgnoreCase 比較子。

<a id="_Configuration_and_extensibility"></a>

## <a name="configuration-and-extensibility"></a>設定和擴充性

有時候，開發人員可能想要對反 XSRF 產生和驗證行為進行更嚴密的控制。 例如，MVC 和網頁協助程式的預設行為（自動將 HTTP cookie 新增至回應）是不必要的，而開發人員可能會想要在其他地方保存權杖。 有兩個 Api 可協助您：

`AntiForgery.GetTokens(string oldCookieToken, out string newCookieToken, out string formToken);`  
`AntiForgery.Validate(string cookieToken, string formToken);`

*GetTokens* 方法會以現有的 XSRF 要求驗證會話權杖作為輸入 (這可能是 null) ，並產生新的 XSRF 要求驗證會話權杖和欄位 token 作為輸出。 權杖是不透明的字串，不含裝飾;實例的 *formToken* 值不會包裝在 &lt; 輸入標記中 &gt; 。 *NewCookieToken* 值可能是 null;如果發生這種情況， *oldCookieToken* 值仍然有效，且不需要設定任何新的回應 cookie。 *GetTokens* 的呼叫端負責保存任何必要的回應 cookie，或產生任何必要的標記;*GetTokens* 方法本身不會將回應變更為副作用。 *Validate* 方法會接受傳入的會話和欄位權杖，並對其執行上述驗證邏輯。

### <a name="antiforgeryconfig"></a>AntiForgeryConfig

開發人員可能會從應用程式啟動設定防 XSRF 系統 \_ 。 設定是以程式設計方式進行。 靜態 *AntiForgeryConfig* 類型的屬性如下所述。 大部分使用宣告的使用者都想要設定 UniqueClaimTypeIdentifier 屬性。

| **屬性** | **說明** |
| --- | --- |
| **AdditionalDataProvider** | 在權杖產生期間提供額外資料的 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) ，並在權杖驗證期間取用其他資料。 預設值為 *null*。 如需詳細資訊，請參閱 [IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx) 一節。 |
| **CookieName** | 字串，提供用來儲存反 XSRF 會話權杖之 HTTP cookie 的名稱。 如果未設定此值，將會根據應用程式部署的虛擬路徑自動產生名稱。 預設值為 *null*。 |
| **RequireSsl** | 布林值，指定是否需要透過 SSL 安全通道來提交反 XSRF token。 如果此值為 *true*，任何自動產生的 cookie 都會設定「安全」旗標，而且如果是從不是透過 SSL 提交的要求內呼叫，則會擲回反 XSRF api。 預設值為 *false*。 |
| **SuppressIdentityHeuristicChecks** | 布林值，指定反 XSRF 系統是否應該停用其對宣告型身分識別的支援。 如果這個值為 *true*，系統會假設 *IIdentity.Name* 適用于做為唯一的每個使用者識別碼，而且不會嘗試如 [WIF/ACS/宣告式驗證](#_WIF_ACS)一節中所述的特殊案例 *IClaimsIdentity* 或 *ClClaimsIdentity* 。 預設值為 `false`。 |
| **UniqueClaimTypeIdentifier** | 字串，指出適合用來做為唯一每個使用者識別碼的宣告類型。 如果已設定此值，且目前的 *IIdentity* 是以宣告為基礎，系統將會嘗試解壓縮 *UniqueClaimTypeIdentifier* 所指定之類型的宣告，而且在產生欄位標記時，會使用對應的值來取代使用者的使用者名稱。 如果找不到宣告類型，系統將會導致要求失敗。 預設值為 *null*，表示系統應使用 (識別提供者、名稱識別碼) 元組，如先前所述，取代使用者的使用者名稱。 |

<a id="_IAntiForgeryAdditionalDataProvider"></a>

### <a name="iantiforgeryadditionaldataprovider"></a>IAntiForgeryAdditionalDataProvider

*[IAntiForgeryAdditionalDataProvider](https://msdn.microsoft.com/library/system.web.helpers.iantiforgeryadditionaldataprovider(v=vs.111).aspx)* 型別可讓開發人員藉由在每個權杖中來回往返額外資料，來擴充反 XSRF 系統的行為。 每次產生欄位 token 時都會呼叫 *GetAdditionalData* 方法，並將傳回值內嵌在產生的權杖內。 實施者可能會從這個方法傳回時間戳記、nonce 或任何其他值。

同樣地， *ValidateAdditionalData* 方法會在每次驗證欄位 token 時呼叫，並將內嵌在權杖內的「其他資料」字串傳遞給方法。 驗證常式可以藉由檢查目前的時間與建立權杖時所儲存的時間) 、nonce 檢查常式或任何其他所需的邏輯，來執行超時 (。

## <a name="design-decisions-and-security-considerations"></a>設計決策和安全性考慮

只有在嘗試防止匿名/未經驗證的使用者遭受 XSRF 攻擊時，才需要在技術上連結會話和欄位權杖的安全性權杖。 當使用者經過驗證時，驗證權杖本身 (應以 cookie 形式提交) 可作為同步器權杖配對的一半。 不過，有一個有效的案例可保護未經過驗證的使用者所叫用的登入頁面，而反 XSRF 邏輯則是透過永遠產生和驗證安全性權杖（即使是已驗證的使用者）來簡化。 如果攻擊者入侵了欄位權杖，也可以提供一些額外的保護，因為設定或猜測會話權杖會是攻擊者克服的另一個障礙。

在單一網域中裝載多個應用程式時，開發人員應謹慎使用。 例如，雖然 *example1.cloudapp.net* 和 *example2.cloudapp.net* 是不同的主機，但 *\* cloudapp.net* 網域下的所有主機之間都有隱含的信任關係。 此隱含信任關聯性 [可讓可能不受信任的主機影響彼此的 cookie](http://stackoverflow.com/questions/9636857/how-can-asp-net-or-asp-net-mvc-be-protected-from-related-domain-cookie-attacks) (管理 AJAX 要求的相同原始原則不一定適用于) 的 HTTP cookie。 ASP.NET Web Stack 執行時間提供了一些風險降低，因為使用者名稱已內嵌到欄位 token 中，所以即使惡意子域可以覆寫會話權杖，也無法為使用者產生有效的欄位 token。 不過，在這種環境中裝載時，內建的防 XSRF 常式仍無法防禦會話劫持或登入 XSRF。

反 XSRF 常式目前不會防禦 [點擊劫持](https://www.owasp.org/index.php/Clickjacking)。 想要針對點擊劫持防護的應用程式，可以藉由傳送 X 框架選項： SAMEORIGIN 標頭與每個回應來輕鬆執行此動作。 所有最新的瀏覽器都支援此標頭。 如需詳細資訊，請參閱 [IE blog](https://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx)、 [SDL blog](https://blogs.msdn.com/b/sdl/archive/2009/02/05/clickjacking-defense-in-ie8.aspx)和 [OWASP](https://www.owasp.org/index.php/Clickjacking)。 在未來的版本中，ASP.NET Web Stack 執行時間可能會使 MVC 和網頁反 XSRF 協助程式自動設定此標頭，讓應用程式能夠自動受到這項攻擊的保護。

Web 開發人員應繼續確保其網站不容易遭受 XSS 攻擊。 XSS 攻擊的功能非常強大，而成功的惡意探索也會中斷 ASP.NET Web Stack 執行時間防禦以防範 XSRF 攻擊。

## <a name="acknowledgment"></a>通知

[@LeviBroderick](https://twitter.com/LeviBroderick)，他寫了許多 ASP.NET 的安全性程式碼，這是大部分的資訊。
