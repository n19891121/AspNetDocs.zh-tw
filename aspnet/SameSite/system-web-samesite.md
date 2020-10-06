---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 瞭解如何在 ASP.NET 中使用 SameSite cookie
ms.author: riande
ms.date: 2/15/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 2a39663dcbfa97ae441edd9a9768172cafbaab03
ms.sourcegitcommit: 09a34635ed0e74d6c2625f6a485c78f201c689ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91763457"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a>在 ASP.NET 中使用 SameSite cookie

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

SameSite 是一項 [IETF](https://ietf.org/about/) 草稿標準，其設計目的是為了提供某些保護，以防止跨網站偽造要求 (CSRF) 攻擊。 最初是在 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中繪製草稿標準，已于 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)更新。 更新的標準與先前的標準沒有回溯相容性，但以下是最顯著的差異：

* 預設會將不含 SameSite 標頭的 cookie 視為 `SameSite=Lax` 。
* `SameSite=None` 必須用來允許跨網站 cookie 使用。
* 判斷提示的 cookie `SameSite=None` 也必須標示為 `Secure` 。
* 使用的應用程式 [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 可能會遇到 `sameSite=Lax` 或 cookie 的問題， `sameSite=Strict` 因為 `<iframe>` 會被視為跨網站案例。
* `SameSite=None` [2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允許此值，並且會導致某些執行將這類 cookie 視為 `SameSite=Strict` 。 請參閱本檔中的 [支援舊版瀏覽器](#sob) 。

此 `SameSite=Lax` 設定適用于大部分的應用程式 cookie。 某些形式的驗證，例如 [OpenID Connect](https://openid.net/connect/) (OIDC) 和 [WS-同盟](https://auth0.com/docs/protocols/ws-fed) 預設為以 POST 為基礎的重新導向。 以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件會停用 SameSite。 由於要求流程的差異，大部分的 [OAuth](https://oauth.net/) 登入不會受到影響。

發出 cookie 的每個 ASP.NET 元件都必須判斷 SameSite 是否適當。

在安裝 2019 .Net SameSite 更新之後，請參閱應用程式問題的 [已知問題](#known) 。

## <a name="using-samesite-in-aspnet-472-and-48"></a>在 ASP.NET 4.7.2 和4.8 中使用 SameSite

.Net 4.7.2 和4.8 支援自12月2019版更新以來的 [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite。 開發人員可以使用 [HttpCookie SameSite 屬性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)，以程式設計方式控制 SameSite 標頭的值。 將 `SameSite` 屬性設為 `Strict` 、 `Lax` 或會 `None` 導致這些值以 cookie 寫入至網路。 將其設為等於 `(SameSiteMode)(-1)` 表示網路上沒有任何 SameSite 標頭應該包含在 cookie 中。 設定檔中的 [HttpCookie 屬性](/dotnet/api/system.web.httpcookie.secure)（或 ' requireSSL '）可以用來將 cookie 標示為 `Secure` 。

新的 `HttpCookie` 實例會預設為 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false` 。 您可以在 [設定] 區段中覆寫這些預設值 `system.web/httpCookies` ，其中字串 `"Unspecified"` 是的易記僅限設定語法 `(SameSiteMode)(-1)` ：

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

ASP.Net 也會針對這些功能發出自己的四個特定 cookie：匿名驗證、表單驗證、會話狀態和角色管理。 這些在執行時間中取得之 cookie 的實例可以使用 `SameSite` 和屬性來操作， `Secure` 就像任何其他 HttpCookie 實例一樣。 不過，由於 SameSite 標準的摒棄修補作業引發，這四項功能的設定選項不一致。 相關的設定區段和屬性（含預設值）如下所示。 如果 `SameSite` 功能沒有或 `Secure` 相關的屬性，則此功能會切換回上述章節中所設定的預設值 `system.web/httpCookies` 。

```xml
<configuration>
 <system.web>
  <anonymousIdentification cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
  <authentication>
   <forms cookieSameSite="Lax" requireSSL="false" />
  </authentication>
  <sessionState cookieSameSite="Lax" /> <!-- No config attribute for Secure -->
  <roleManager cookieRequireSSL="false" /> <!-- No config attribute for SameSite -->
 <system.web>
<configuration>
```  

**注意**：目前只能使用「未指定」 `system.web/httpCookies@sameSite` 。 我們希望在未來的更新中，將類似的語法新增至先前所顯示的 cookieSameSite 屬性。 程式 `(SameSiteMode)(-1)` 代碼中的設定仍可在這些 cookie 的實例上運作。 *

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a>將 .NET 應用程式重定目標

以 .NET 4.7.2 或更新版本為目標：

* 確定 *web.config* 包含下列各項：  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  [.Net 遷移指南](/dotnet/framework/migration-guide/)有更多詳細資料。

* 確認專案中的 NuGet 套件是以正確的 framework 版本為目標。 您可以藉由檢查 *packages.config* 檔案來驗證正確的 framework 版本，例如：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  在上述的 *packages.config* 檔案中， `Microsoft.ApplicationInsights` 封裝：
    * 以 .NET 4.5.1 為目標。
    * `targetFramework`如果有更新的套件以您的 framework 目標為目標，則應該將其屬性更新為 `net472` 。

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a>早于4.7.2 的 .NET 版本

Microsoft 不支援較低的 .NET 版本來撰寫相同的網站 cookie 屬性4.7.2。 我們找不到可靠的方法來進行下列動作：

* 確定已根據瀏覽器版本正確寫入屬性。
* 在較舊的 framework 版本上攔截及調整驗證和會話 cookie。

### <a name="december-patch-behavior-changes"></a>12月的修補程式列為變更

.NET Framework 的特定行為變更是 `SameSite` 屬性如何解讀 `None` 值：

* 在修補程式的值之前 `None` ：
  * 完全不要發出屬性。
* 修補之後：
  * `None`其值表示「發出具有值的屬性」 `None` 。
  * 的 `SameSite` 值 `(SameSiteMode)(-1)` 會導致不發出屬性。

表單驗證和會話狀態 cookie 的預設 SameSite 值已從變更 `None` 為 `Lax` 。

### <a name="summary-of-change-impact-on-browsers"></a>變更瀏覽器的變更影響摘要

如果您安裝了修補程式併發出 cookie `SameSite.None` ，就會發生下列其中一種情況：
* Chrome v80 會根據新的執行來處理此 cookie，而不會在 cookie 上強制執行相同的網站限制。
* 任何未更新為支援新執行的瀏覽器都會遵循舊的執行。 舊的實作為：
  * 如果您看到不了解的值，請忽略它並切換至嚴格相同的網站限制。

如此一來，應用程式就會在 Chrome 中中斷，或在其他許多地方中斷。

## <a name="history-and-changes"></a>歷程記錄和變更

SameSite 支援已在 .NET 4.7.2 中使用 [2016 草稿標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)來執行。

Windows 的2019年11月19日更新，從2016標準版更新為2019標準的 .NET 4.7.2 +。 其他版本的 Windows 即將推出其他更新。 如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。

 SameSite 規格的2019草稿：

* 與 2016 draft **不** 相容。 如需詳細資訊，請參閱本檔中的 [支援舊版瀏覽器](#sob) 。
* 指定依預設會將 cookie 視為 `SameSite=Lax` 。
* 指定明確判斷提示 `SameSite=None` 以便啟用跨網站傳遞的 cookie，也應標示為 `Secure` 。
* 如上面所列的 KB 所述，已發出的修補程式會支援。
* 預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由[Chrome](https://chromestatus.com/feature/5088147346030592)啟用。 瀏覽器已在2019中開始移至此標準。

<a name="known"></a>

## <a name="known-issues"></a>已知問題

由於2016和2019草稿規格不相容，因此 11 2019 月版 .Net Framework 更新引進一些可能中斷的變更。

* 會話狀態與表單驗證 cookie 現在會以 `Lax` 非指定的形式寫入網路。
  * 雖然大部分的應用程式 `SameSite=Lax` 都能使用 cookie，但是在使用的網站或應用程式上張貼的應用程式 `iframe` 可能會發現其會話狀態或表單驗證 cookie 未如預期般使用。 若要解決此情況，請變更 `cookieSameSite` 先前所討論之適當設定區段中的值。
* 在程式碼或設定中明確設定的 HttpCookies `SameSite=None` 現在會有以 cookie 撰寫的值，但先前已省略。 這可能會造成舊版瀏覽器的問題，而這些瀏覽器僅支援2016草稿標準。
  * 以具有 cookie 的2019草稿標準的瀏覽器為目標時 `SameSite=None` ，請記得也將其標示， `Secure` 否則可能無法辨識。
  * 若要還原為未寫入的2016行為 `SameSite=None` ，請使用應用程式設定 `aspnet:SupressSameSiteNone=true` 。 請注意，這會套用至應用程式中的所有 HttpCookies。

### <a name="azure-app-servicesamesite-cookie-handling"></a>Azure App Service-SameSite cookie 處理

如需有關 Azure App Service 如何在 .Net 4.7.2 應用程式中設定 SameSite 行為的詳細資訊，請參閱 [Azure App Service （SameSite cookie 處理和 .NET Framework 4.7.2 修補程式](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 。

<a name="sob"></a>

## <a name="supporting-older-browsers"></a>支援較舊的瀏覽器

2016 SameSite 標準規定必須將未知值視為 `SameSite=Strict` 值。 從較舊的瀏覽器存取的應用程式（支援 2016 SameSite 標準）在取得具有值的 SameSite 屬性時可能會中斷 `None` 。 如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。 ASP.NET 不會執行瀏覽器偵測，因為使用者代理程式值會高度變動且經常變更。

Microsoft 解決問題的方法是協助您執行瀏覽器偵測元件，以 `sameSite=None` 從 cookie 中去除屬性（如果已知瀏覽器不支援的話）。 Google 的建議是發出雙重 cookie （一個具有新的屬性），另一個則沒有屬性。 不過，我們認為 Google 的建議有限。 有些瀏覽器，特別是行動瀏覽器對於網站的 cookie 數目或功能變數名稱可以傳送的限制極小。 傳送多個 cookie （尤其是像驗證 cookie 這樣的大型 cookie）很快就能達到行動瀏覽器的限制，而導致難以診斷和修正的應用程式失敗。 此外，架構中有很大的協力廠商程式碼和元件的生態系統，可能不會更新為使用雙重 cookie 方法。

[此 GitHub 存放庫]()中範例專案所使用的瀏覽器偵測程式碼包含在兩個檔案中

* [C # SameSiteSupport.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [VB SameSiteSupport .vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

這些偵測是我們所見到的最常見瀏覽器代理程式，可支援2016標準，而且必須完全移除屬性。 這並不是完整的實作為：

* 您的應用程式可能會看到我們的測試網站沒有的瀏覽器。
* 您應該準備好新增環境所需的偵測。

連接偵測的方式會根據您所使用的 .NET 版本和 web 架構而有所不同。 您可以在 [HttpCookie](/dotnet/api/system.web.httpcookie) 呼叫位置呼叫下列程式碼：

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

請參閱下列 ASP.NET 4.7.2 SameSite cookie 主題：

* [C# MVC](xref:samesite/csMVC)
* [C# WebForms](xref:samesite/CSharpWebForms)
* [VB WebForms](xref:samesite/vbWF)
* [VB MVC](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a>確保您的網站會重新導向至 HTTPS

針對 ASP.NET 4.x、WebForms 和 MVC， [IIS 的 URL 重寫](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 功能可以用來將所有要求重新導向至 HTTPS。 下列 XML 會顯示範例規則：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Redirect to https" stopProcessing="true">
          <match url="(.*)"/>
          <conditions>
            <add input="{HTTPS}" pattern="Off"/>
            <add input="{REQUEST_METHOD}" pattern="^get$|^head$" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" redirectType="Permanent"/>
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

在內部部署中， [IIS URL 重寫](https://www.iis.net/downloads/microsoft/url-rewrite) 是可能需要安裝的選擇性功能。

## <a name="test-apps-for-samesite-problems"></a>測試應用程式的 SameSite 問題

您必須使用所支援的瀏覽器來測試您的應用程式，並完成牽涉到 cookie 的案例。 Cookie 案例通常涉及

* 登入表單
* 外部登入機制，例如 Facebook、Azure AD、OAuth 和 OIDC
* 接受來自其他網站之要求的頁面
* 您應用程式中的頁面，其設計目的是要內嵌在 iframe 中

您應該檢查 cookie 是否已在您的應用程式中正確建立、保存及刪除。

與遠端網站互動的應用程式（例如透過協力廠商登入）必須：

* 在多個瀏覽器上測試互動。
* 套用這份檔中討論的 [瀏覽器偵測和緩和措施](#sob) 。

使用可加入新 SameSite 行為的用戶端版本，測試 web 應用程式。 Chrome、Firefox 和 Chromium Edge 都有新的加入宣告功能旗標，可用於測試。 當您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（特別是 Safari）進行測試。 如需詳細資訊，請參閱本檔中的 [支援舊版瀏覽器](#sob) 。

### <a name="test-with-chrome"></a>使用 Chrome 測試

Chrome 78 + 提供誤導的結果，因為它有暫時的緩和措施。 Chrome 78 + 暫時性緩和可讓 cookie 的時間不超過兩分鐘。 使用已啟用適當測試旗標的 Chrome 76 或77可提供更精確的結果。 測試新的 SameSite 行為切換 `chrome://flags/#same-site-by-default-cookies` 為 **啟用狀態**。 較舊版本的 Chrome (75 和以下的) 會回報為失敗，並出現新的 `None` 設定。 請參閱本檔中的 [支援舊版瀏覽器](#sob) 。

Google 未提供較舊的 chrome 版本。 遵循 [下載 Chromium](https://www.chromium.org/getting-involved/download-chromium) 中的指示，測試舊版的 Chrome。 請勿從搜尋較舊版本 chrome 所提供的 **連結下載 Chrome** 。

* [Chromium 76 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [Chromium 74 Win64](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* 如果您不是使用64位版本的 Windows，可以使用 [ [OmahaProxy 檢視器]](https://omahaproxy.appspot.com/) 查閱 [Chromium 所提供的指示](https://www.chromium.org/getting-involved/download-chromium)，將哪個 Chromium 分支對應至 Chrome 74 (v 74.0.3729.108) 。

從未放大的版本開始 `80.0.3975.0` ，您可以使用新的旗標來停用寬鬆的 + POST 暫時緩和措施， `--enable-features=SameSiteDefaultChecksMethodRigorously` 以在移除緩和措施的功能的最終狀態下測試網站和服務。 如需詳細資訊，請參閱 Chromium Projects [SameSite 更新](https://www.chromium.org/updates/same-site)

#### <a name="test-with-chrome-80"></a>使用 Chrome 80 + 進行測試

[下載](https://www.google.com/chrome/) 支援其新屬性的 Chrome 版本。 在撰寫本文時，目前的版本為 Chrome 80。 Chrome 80 需要啟用旗標 `chrome://flags/#same-site-by-default-cookies` ，才能使用新的行為。 您也應該啟用 (`chrome://flags/#cookies-without-same-site-must-be-secure`) ，以針對未啟用 sameSite 屬性的 cookie 測試即將推出的行為。 Chrome 80 的目標是要讓切換器將 cookie 視為沒有屬性的 cookie `SameSite=Lax` ，雖然某些要求的時間寬限期也是如此。 若要停用計時寬限期，可使用下列命令列引數來啟動 Chrome 80：

`--enable-features=SameSiteDefaultChecksMethodRigorously`

Chrome 80 在瀏覽器主控台中有關于遺漏 sameSite 屬性的警告訊息。 使用 F12 開啟瀏覽器主控台。

### <a name="test-with-safari"></a>使用 Safari 測試

Safari 12 會嚴格地實作為先前的草稿，並在新 `None` 值為 cookie 時失敗。 `None` 可透過支援本檔中 [舊版流覽](#sob) 器的瀏覽器偵測程式碼來避免。 使用 MSAL、ADAL 或您所使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。 問題取決於基礎作業系統版本。 已知 OSX Mojave (10.14) 和 iOS 12 具有新 SameSite 行為的相容性問題。 將作業系統升級至 OSX Catalina (10.15) 或 iOS 13 可修正問題。 Safari 目前沒有可用於測試新規格行為的加入宣告旗標。

### <a name="test-with-firefox"></a>使用 Firefox 進行測試

您可以在頁面上選擇具有功能旗標的，以在版本 68 + 上測試新標準的 Firefox 支援 `about:config` `network.cookie.sameSite.laxByDefault` 。 舊版 Firefox 沒有相容性問題的報告。

### <a name="test-with-edge-legacy-browser"></a>使用 Edge (舊版) 瀏覽器進行測試

Edge 支援舊的 SameSite 標準。 Edge 版本 44 + 沒有任何已知的新標準相容性問題。

### <a name="test-with-edge-chromium"></a>使用 Edge (Chromium) 進行測試

SameSite 旗標是在頁面上設定的 `edge://flags/#same-site-by-default-cookies` 。 Edge Chromium 未發現任何相容性問題。

### <a name="test-with-electron"></a>使用 Electron 進行測試

Electron 的版本包括舊版的 Chromium。 例如，小組所使用的 Electron 版本是 Chromium 66，這會展示較舊的行為。 您必須使用您的產品所使用的 Electron 版本來執行您自己的相容性測試。 請參閱 [支援較舊的瀏覽器](#sob)。

## <a name="reverting-samesite-patches"></a>還原 SameSite 修補程式

您可以將 .NET Framework apps 中更新的 sameSite 行為還原為先前的行為，其中不會針對的值發出 sameSite 屬性 `None` ，並將驗證和會話 cookie 還原為不發出值。 這應該視為 *極暫時性的修正*，因為 Chrome 變更會中斷任何外部 POST 要求或使用瀏覽器的使用者驗證，以支援標準的變更。

### <a name="reverting-net-472-behavior"></a>還原 .NET 4.7.2 行為

更新 *web.config* 以包含下列設定：

```xml
<configuration> 
  <appSettings>
    <add key="aspnet:SuppressSameSiteNone" value="true" />
  </appSettings>
 
  <system.web> 
    <authentication> 
      <forms cookieSameSite="None" /> 
    </authentication> 
    <sessionState cookieSameSite="None" /> 
  </system.web> 
</configuration>
```

## <a name="additional-resources"></a>其他資源

* [ASP.NET 和 ASP.NET Core 中即將推出的 SameSite Cookie 變更](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [依預設 SameSite 測試和偵錯工具的秘訣，以及 "SameSite = None;安全的「cookie](https://www.chromium.org/updates/same-site/test-debug)
* [Chromium Blog：開發人員：準備開始新的 SameSite = None;安全的 Cookie 設定](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [SameSite cookie 說明](https://web.dev/samesite-cookies-explained/)
* [Chrome 更新](https://www.chromium.org/updates/same-site)
* [.NET SameSite 修補程式](/aspnet/samesite/kbs-samesite)
* [Azure Web 應用程式相同的網站資訊](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [Azure ActiveDirectory 相同網站資訊](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
