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
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="58d20-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="58d20-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="58d20-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="58d20-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="58d20-105">SameSite 是一項 [IETF](https://ietf.org/about/) 草稿標準，其設計目的是為了提供某些保護，以防止跨網站偽造要求 (CSRF) 攻擊。</span><span class="sxs-lookup"><span data-stu-id="58d20-105">SameSite is an [IETF](https://ietf.org/about/) draft standard designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="58d20-106">最初是在 [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07)中繪製草稿標準，已于 [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)更新。</span><span class="sxs-lookup"><span data-stu-id="58d20-106">Originally drafted in [2016](https://tools.ietf.org/html/draft-west-first-party-cookies-07), the draft standard was updated in [2019](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00).</span></span> <span data-ttu-id="58d20-107">更新的標準與先前的標準沒有回溯相容性，但以下是最顯著的差異：</span><span class="sxs-lookup"><span data-stu-id="58d20-107">The updated standard is not backward compatible with the previous standard, with the following being the most noticeable differences:</span></span>

* <span data-ttu-id="58d20-108">預設會將不含 SameSite 標頭的 cookie 視為 `SameSite=Lax` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-108">Cookies without SameSite header are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="58d20-109">`SameSite=None` 必須用來允許跨網站 cookie 使用。</span><span class="sxs-lookup"><span data-stu-id="58d20-109">`SameSite=None` must be used to allow cross-site cookie use.</span></span>
* <span data-ttu-id="58d20-110">判斷提示的 cookie `SameSite=None` 也必須標示為 `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-110">Cookies that assert `SameSite=None` must also be marked as `Secure`.</span></span>
* <span data-ttu-id="58d20-111">使用的應用程式 [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) 可能會遇到 `sameSite=Lax` 或 cookie 的問題， `sameSite=Strict` 因為 `<iframe>` 會被視為跨網站案例。</span><span class="sxs-lookup"><span data-stu-id="58d20-111">Applications that use [`<iframe>`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe) may experience issues with `sameSite=Lax` or `sameSite=Strict` cookies because `<iframe>` is treated as cross-site scenarios.</span></span>
* <span data-ttu-id="58d20-112">`SameSite=None` [2016 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)不允許此值，並且會導致某些執行將這類 cookie 視為 `SameSite=Strict` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-112">The value `SameSite=None` is not allowed by the [2016 standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) and causes some implementations to treat such cookies as `SameSite=Strict`.</span></span> <span data-ttu-id="58d20-113">請參閱本檔中的 [支援舊版瀏覽器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-113">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="58d20-114">此 `SameSite=Lax` 設定適用于大部分的應用程式 cookie。</span><span class="sxs-lookup"><span data-stu-id="58d20-114">The `SameSite=Lax` setting works for most application cookies.</span></span> <span data-ttu-id="58d20-115">某些形式的驗證，例如 [OpenID Connect](https://openid.net/connect/) (OIDC) 和 [WS-同盟](https://auth0.com/docs/protocols/ws-fed) 預設為以 POST 為基礎的重新導向。</span><span class="sxs-lookup"><span data-stu-id="58d20-115">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="58d20-116">以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件會停用 SameSite。</span><span class="sxs-lookup"><span data-stu-id="58d20-116">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="58d20-117">由於要求流程的差異，大部分的 [OAuth](https://oauth.net/) 登入不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="58d20-117">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="58d20-118">發出 cookie 的每個 ASP.NET 元件都必須判斷 SameSite 是否適當。</span><span class="sxs-lookup"><span data-stu-id="58d20-118">Each ASP.NET component that emits cookies needs to decide if SameSite is appropriate.</span></span>

<span data-ttu-id="58d20-119">在安裝 2019 .Net SameSite 更新之後，請參閱應用程式問題的 [已知問題](#known) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-119">See [Known Issues](#known) for problems with applications after installing the 2019 .Net SameSite updates.</span></span>

## <a name="using-samesite-in-aspnet-472-and-48"></a><span data-ttu-id="58d20-120">在 ASP.NET 4.7.2 和4.8 中使用 SameSite</span><span class="sxs-lookup"><span data-stu-id="58d20-120">Using SameSite in ASP.NET 4.7.2 and 4.8</span></span>

<span data-ttu-id="58d20-121">.Net 4.7.2 和4.8 支援自12月2019版更新以來的 [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite。</span><span class="sxs-lookup"><span data-stu-id="58d20-121">.Net 4.7.2 and 4.8 supports the [2019 draft standard](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00) for SameSite since the release of updates in December 2019.</span></span> <span data-ttu-id="58d20-122">開發人員可以使用 [HttpCookie SameSite 屬性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)，以程式設計方式控制 SameSite 標頭的值。</span><span class="sxs-lookup"><span data-stu-id="58d20-122">Developers are able to programmatically control the value of the SameSite header using the [HttpCookie.SameSite property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite).</span></span> <span data-ttu-id="58d20-123">將 `SameSite` 屬性設為 `Strict` 、 `Lax` 或會 `None` 導致這些值以 cookie 寫入至網路。</span><span class="sxs-lookup"><span data-stu-id="58d20-123">Setting the `SameSite` property to `Strict`, `Lax`, or `None` results in those values being written on the network with the cookie.</span></span> <span data-ttu-id="58d20-124">將其設為等於 `(SameSiteMode)(-1)` 表示網路上沒有任何 SameSite 標頭應該包含在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="58d20-124">Setting it equal to `(SameSiteMode)(-1)` indicates that no SameSite header should be included on the network with the cookie.</span></span> <span data-ttu-id="58d20-125">設定檔中的 [HttpCookie 屬性](/dotnet/api/system.web.httpcookie.secure)（或 ' requireSSL '）可以用來將 cookie 標示為 `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-125">The [HttpCookie.Secure Property](/dotnet/api/system.web.httpcookie.secure), or 'requireSSL' in config files, can be used to mark the cookie as `Secure` or not.</span></span>

<span data-ttu-id="58d20-126">新的 `HttpCookie` 實例會預設為 `SameSite=(SameSiteMode)(-1)` 和 `Secure=false` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-126">New `HttpCookie` instances will default to `SameSite=(SameSiteMode)(-1)` and `Secure=false`.</span></span> <span data-ttu-id="58d20-127">您可以在 [設定] 區段中覆寫這些預設值 `system.web/httpCookies` ，其中字串 `"Unspecified"` 是的易記僅限設定語法 `(SameSiteMode)(-1)` ：</span><span class="sxs-lookup"><span data-stu-id="58d20-127">These defaults can be overridden in the `system.web/httpCookies` configuration section, where the string `"Unspecified"` is a friendly configuration-only syntax for `(SameSiteMode)(-1)`:</span></span>

```xml
<configuration>
 <system.web>
  <httpCookies sameSite="[Strict|Lax|None|Unspecified]" requireSSL="[true|false]" />
 <system.web>
<configuration>
```

<span data-ttu-id="58d20-128">ASP.Net 也會針對這些功能發出自己的四個特定 cookie：匿名驗證、表單驗證、會話狀態和角色管理。</span><span class="sxs-lookup"><span data-stu-id="58d20-128">ASP.Net also issues four specific cookies of its own for these features: Anonymous Authentication, Forms Authentication, Session State, and Role Management.</span></span> <span data-ttu-id="58d20-129">這些在執行時間中取得之 cookie 的實例可以使用 `SameSite` 和屬性來操作， `Secure` 就像任何其他 HttpCookie 實例一樣。</span><span class="sxs-lookup"><span data-stu-id="58d20-129">Instances of these cookies obtained in runtime can be manipulated using the `SameSite` and `Secure` properties just like any other HttpCookie instance.</span></span> <span data-ttu-id="58d20-130">不過，由於 SameSite 標準的摒棄修補作業引發，這四項功能的設定選項不一致。</span><span class="sxs-lookup"><span data-stu-id="58d20-130">However, due to the patchwork emergence of the SameSite standard, configuration options for these four features cookies is inconsistent.</span></span> <span data-ttu-id="58d20-131">相關的設定區段和屬性（含預設值）如下所示。</span><span class="sxs-lookup"><span data-stu-id="58d20-131">The relevant configuration sections and attributes, with defaults, are shown below.</span></span> <span data-ttu-id="58d20-132">如果 `SameSite` 功能沒有或 `Secure` 相關的屬性，則此功能會切換回上述章節中所設定的預設值 `system.web/httpCookies` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-132">If there is no `SameSite` or `Secure` related attribute for a feature, then the feature will fall back on the defaults configured in the `system.web/httpCookies` section discussed above.</span></span>

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

<span data-ttu-id="58d20-133">**注意**：目前只能使用「未指定」 `system.web/httpCookies@sameSite` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-133">**Note**: 'Unspecified' is only available to `system.web/httpCookies@sameSite` at the moment.</span></span> <span data-ttu-id="58d20-134">我們希望在未來的更新中，將類似的語法新增至先前所顯示的 cookieSameSite 屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-134">We hope to add similar syntax to the previously shown cookieSameSite attributes in future updates.</span></span> <span data-ttu-id="58d20-135">程式 `(SameSiteMode)(-1)` 代碼中的設定仍可在這些 cookie 的實例上運作。 \*</span><span class="sxs-lookup"><span data-stu-id="58d20-135">Setting `(SameSiteMode)(-1)` in code still works on instances of these cookies.\*</span></span>

[!INCLUDE[](~/includes/MTcomments.md)]

<a name="retargeting"></a>

### <a name="retarget-net-apps"></a><span data-ttu-id="58d20-136">將 .NET 應用程式重定目標</span><span class="sxs-lookup"><span data-stu-id="58d20-136">Retarget .NET apps</span></span>

<span data-ttu-id="58d20-137">以 .NET 4.7.2 或更新版本為目標：</span><span class="sxs-lookup"><span data-stu-id="58d20-137">To target .NET 4.7.2 or later:</span></span>

* <span data-ttu-id="58d20-138">確定 *web.config* 包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="58d20-138">Ensure *web.config* contains the following:</span></span>  <!-- review, I removed `debug="true"` -->

  ```xml
  <system.web>
    <compilation targetFramework="4.7.2"/>
    <httpRuntime targetFramework="4.7.2"/>
  </system.web>

* Verify the project file contains the correct [TargetFrameworkVersion](/visualstudio/msbuild/msbuild-target-framework-and-target-platform?view=vs-2019):

  ```xml
  <TargetFrameworkVersion>v4.7.2</TargetFrameworkVersion>
  ```

  <span data-ttu-id="58d20-139">[.Net 遷移指南](/dotnet/framework/migration-guide/)有更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58d20-139">The [.NET Migration Guide](/dotnet/framework/migration-guide/) has more details.</span></span>

* <span data-ttu-id="58d20-140">確認專案中的 NuGet 套件是以正確的 framework 版本為目標。</span><span class="sxs-lookup"><span data-stu-id="58d20-140">Verify NuGet packages in the project are targeted at the correct framework version.</span></span> <span data-ttu-id="58d20-141">您可以藉由檢查 *packages.config* 檔案來驗證正確的 framework 版本，例如：</span><span class="sxs-lookup"><span data-stu-id="58d20-141">You can verify the correct framework version by examining the *packages.config* file, for example:</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <packages>
    <package id="Microsoft.AspNet.Mvc" version="5.2.7" targetFramework="net472" />
    <package id="Microsoft.ApplicationInsights" version="2.4.0" targetFramework="net451" />
  </packages>
  ```

  <span data-ttu-id="58d20-142">在上述的 *packages.config* 檔案中， `Microsoft.ApplicationInsights` 封裝：</span><span class="sxs-lookup"><span data-stu-id="58d20-142">In the preceding *packages.config* file, the `Microsoft.ApplicationInsights` package:</span></span>
    * <span data-ttu-id="58d20-143">以 .NET 4.5.1 為目標。</span><span class="sxs-lookup"><span data-stu-id="58d20-143">Is  targeted against .NET 4.5.1.</span></span>
    * <span data-ttu-id="58d20-144">`targetFramework`如果有更新的套件以您的 framework 目標為目標，則應該將其屬性更新為 `net472` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-144">Should have its `targetFramework` attribute updated to `net472` if an updated package targeting your framework target exists.</span></span>

<a name="nope"></a>

### <a name="net-versions-earlier-than-472"></a><span data-ttu-id="58d20-145">早于4.7.2 的 .NET 版本</span><span class="sxs-lookup"><span data-stu-id="58d20-145">.NET versions earlier than 4.7.2</span></span>

<span data-ttu-id="58d20-146">Microsoft 不支援較低的 .NET 版本來撰寫相同的網站 cookie 屬性4.7.2。</span><span class="sxs-lookup"><span data-stu-id="58d20-146">Microsoft does not support .NET versions lower that 4.7.2 for writing the same-site cookie attribute.</span></span> <span data-ttu-id="58d20-147">我們找不到可靠的方法來進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="58d20-147">We have not found a reliable way to:</span></span>

* <span data-ttu-id="58d20-148">確定已根據瀏覽器版本正確寫入屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-148">Ensure the attribute is written correctly based on browser version.</span></span>
* <span data-ttu-id="58d20-149">在較舊的 framework 版本上攔截及調整驗證和會話 cookie。</span><span class="sxs-lookup"><span data-stu-id="58d20-149">Intercept and adjust authentication and session cookies on older framework versions.</span></span>

### <a name="december-patch-behavior-changes"></a><span data-ttu-id="58d20-150">12月的修補程式列為變更</span><span class="sxs-lookup"><span data-stu-id="58d20-150">December patch behavior changes</span></span>

<span data-ttu-id="58d20-151">.NET Framework 的特定行為變更是 `SameSite` 屬性如何解讀 `None` 值：</span><span class="sxs-lookup"><span data-stu-id="58d20-151">The specific behavior change for .NET Framework is how the `SameSite` property interprets the `None` value:</span></span>

* <span data-ttu-id="58d20-152">在修補程式的值之前 `None` ：</span><span class="sxs-lookup"><span data-stu-id="58d20-152">Before the patch a value of `None` meant:</span></span>
  * <span data-ttu-id="58d20-153">完全不要發出屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-153">Do not emit the attribute at all.</span></span>
* <span data-ttu-id="58d20-154">修補之後：</span><span class="sxs-lookup"><span data-stu-id="58d20-154">After the patch:</span></span>
  * <span data-ttu-id="58d20-155">`None`其值表示「發出具有值的屬性」 `None` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-155">A value of `None`it means "Emit the attribute with a value of `None`".</span></span>
  * <span data-ttu-id="58d20-156">的 `SameSite` 值 `(SameSiteMode)(-1)` 會導致不發出屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-156">A `SameSite` value of `(SameSiteMode)(-1)` causes the attribute not to be emitted.</span></span>

<span data-ttu-id="58d20-157">表單驗證和會話狀態 cookie 的預設 SameSite 值已從變更 `None` 為 `Lax` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-157">The default SameSite value for forms authentication and session state cookies was changed from `None` to `Lax`.</span></span>

### <a name="summary-of-change-impact-on-browsers"></a><span data-ttu-id="58d20-158">變更瀏覽器的變更影響摘要</span><span class="sxs-lookup"><span data-stu-id="58d20-158">Summary of change impact on browsers</span></span>

<span data-ttu-id="58d20-159">如果您安裝了修補程式併發出 cookie `SameSite.None` ，就會發生下列其中一種情況：</span><span class="sxs-lookup"><span data-stu-id="58d20-159">If you install the patch and issue a cookie with `SameSite.None`, one of two things will happen:</span></span>
* <span data-ttu-id="58d20-160">Chrome v80 會根據新的執行來處理此 cookie，而不會在 cookie 上強制執行相同的網站限制。</span><span class="sxs-lookup"><span data-stu-id="58d20-160">Chrome v80 will treat this cookie according to the new implementation, and not enforce same site restrictions on the cookie.</span></span>
* <span data-ttu-id="58d20-161">任何未更新為支援新執行的瀏覽器都會遵循舊的執行。</span><span class="sxs-lookup"><span data-stu-id="58d20-161">Any browser that has not been updated to support the new implementation will follow the old implementation.</span></span> <span data-ttu-id="58d20-162">舊的實作為：</span><span class="sxs-lookup"><span data-stu-id="58d20-162">The old implementation says:</span></span>
  * <span data-ttu-id="58d20-163">如果您看到不了解的值，請忽略它並切換至嚴格相同的網站限制。</span><span class="sxs-lookup"><span data-stu-id="58d20-163">If you see a value you don't understand, ignore it and switch to strict same site restrictions.</span></span>

<span data-ttu-id="58d20-164">如此一來，應用程式就會在 Chrome 中中斷，或在其他許多地方中斷。</span><span class="sxs-lookup"><span data-stu-id="58d20-164">So either the app breaks in Chrome, or you break in numerous other places.</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="58d20-165">歷程記錄和變更</span><span class="sxs-lookup"><span data-stu-id="58d20-165">History and changes</span></span>

<span data-ttu-id="58d20-166">SameSite 支援已在 .NET 4.7.2 中使用 [2016 草稿標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)來執行。</span><span class="sxs-lookup"><span data-stu-id="58d20-166">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="58d20-167">Windows 的2019年11月19日更新，從2016標準版更新為2019標準的 .NET 4.7.2 +。</span><span class="sxs-lookup"><span data-stu-id="58d20-167">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="58d20-168">其他版本的 Windows 即將推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="58d20-168">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="58d20-169">如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="58d20-169">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="58d20-170">SameSite 規格的2019草稿：</span><span class="sxs-lookup"><span data-stu-id="58d20-170">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="58d20-171">與 2016 draft **不** 相容。</span><span class="sxs-lookup"><span data-stu-id="58d20-171">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="58d20-172">如需詳細資訊，請參閱本檔中的 [支援舊版瀏覽器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-172">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="58d20-173">指定依預設會將 cookie 視為 `SameSite=Lax` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-173">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="58d20-174">指定明確判斷提示 `SameSite=None` 以便啟用跨網站傳遞的 cookie，也應標示為 `Secure` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-174">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should also be marked as `Secure`.</span></span>
* <span data-ttu-id="58d20-175">如上面所列的 KB 所述，已發出的修補程式會支援。</span><span class="sxs-lookup"><span data-stu-id="58d20-175">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="58d20-176">預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由[Chrome](https://chromestatus.com/feature/5088147346030592)啟用。</span><span class="sxs-lookup"><span data-stu-id="58d20-176">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="58d20-177">瀏覽器已在2019中開始移至此標準。</span><span class="sxs-lookup"><span data-stu-id="58d20-177">Browsers started moving to this standard in 2019.</span></span>

<a name="known"></a>

## <a name="known-issues"></a><span data-ttu-id="58d20-178">已知問題</span><span class="sxs-lookup"><span data-stu-id="58d20-178">Known Issues</span></span>

<span data-ttu-id="58d20-179">由於2016和2019草稿規格不相容，因此 11 2019 月版 .Net Framework 更新引進一些可能中斷的變更。</span><span class="sxs-lookup"><span data-stu-id="58d20-179">Because the 2016 and 2019 draft specifications are not compatible, the November 2019 .Net Framework update introduces some changes that may be breaking.</span></span>

* <span data-ttu-id="58d20-180">會話狀態與表單驗證 cookie 現在會以 `Lax` 非指定的形式寫入網路。</span><span class="sxs-lookup"><span data-stu-id="58d20-180">Session State and Forms Authentication cookies are now written to the network as `Lax` instead of unspecified.</span></span>
  * <span data-ttu-id="58d20-181">雖然大部分的應用程式 `SameSite=Lax` 都能使用 cookie，但是在使用的網站或應用程式上張貼的應用程式 `iframe` 可能會發現其會話狀態或表單驗證 cookie 未如預期般使用。</span><span class="sxs-lookup"><span data-stu-id="58d20-181">While most apps work with `SameSite=Lax` cookies, apps that POST across sites or applications that make use of `iframe` may find that their session state or forms authorization cookies aren't being used as expected.</span></span> <span data-ttu-id="58d20-182">若要解決此情況，請變更 `cookieSameSite` 先前所討論之適當設定區段中的值。</span><span class="sxs-lookup"><span data-stu-id="58d20-182">To remedy this, change the `cookieSameSite` value in the appropriate configuration section as discussed previously.</span></span>
* <span data-ttu-id="58d20-183">在程式碼或設定中明確設定的 HttpCookies `SameSite=None` 現在會有以 cookie 撰寫的值，但先前已省略。</span><span class="sxs-lookup"><span data-stu-id="58d20-183">HttpCookies that explicitly set `SameSite=None` in code or configuration now have that value written with the cookie, whereas it was previously omitted.</span></span> <span data-ttu-id="58d20-184">這可能會造成舊版瀏覽器的問題，而這些瀏覽器僅支援2016草稿標準。</span><span class="sxs-lookup"><span data-stu-id="58d20-184">This may cause issues with older browsers that only support the 2016 draft standard.</span></span>
  * <span data-ttu-id="58d20-185">以具有 cookie 的2019草稿標準的瀏覽器為目標時 `SameSite=None` ，請記得也將其標示， `Secure` 否則可能無法辨識。</span><span class="sxs-lookup"><span data-stu-id="58d20-185">When targeting browsers supporting the 2019 draft standard with `SameSite=None` cookies, remember to also mark them `Secure` or they may not be recognized.</span></span>
  * <span data-ttu-id="58d20-186">若要還原為未寫入的2016行為 `SameSite=None` ，請使用應用程式設定 `aspnet:SupressSameSiteNone=true` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-186">To revert to the 2016 behavior of not writing `SameSite=None`, use the app setting `aspnet:SupressSameSiteNone=true`.</span></span> <span data-ttu-id="58d20-187">請注意，這會套用至應用程式中的所有 HttpCookies。</span><span class="sxs-lookup"><span data-stu-id="58d20-187">Note that this will apply to all HttpCookies in the app.</span></span>

### <a name="azure-app-servicesamesite-cookie-handling"></a><span data-ttu-id="58d20-188">Azure App Service-SameSite cookie 處理</span><span class="sxs-lookup"><span data-stu-id="58d20-188">Azure App Service—SameSite cookie handling</span></span>

<span data-ttu-id="58d20-189">如需有關 Azure App Service 如何在 .Net 4.7.2 應用程式中設定 SameSite 行為的詳細資訊，請參閱 [Azure App Service （SameSite cookie 處理和 .NET Framework 4.7.2 修補程式](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-189">See [Azure App Service—SameSite cookie handling and .NET Framework 4.7.2 patch](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/) for information about how Azure App Service is configuring SameSite behaviors in .Net 4.7.2 apps.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="58d20-190">支援較舊的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="58d20-190">Supporting older browsers</span></span>

<span data-ttu-id="58d20-191">2016 SameSite 標準規定必須將未知值視為 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="58d20-191">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="58d20-192">從較舊的瀏覽器存取的應用程式（支援 2016 SameSite 標準）在取得具有值的 SameSite 屬性時可能會中斷 `None` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-192">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="58d20-193">如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。</span><span class="sxs-lookup"><span data-stu-id="58d20-193">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="58d20-194">ASP.NET 不會執行瀏覽器偵測，因為使用者代理程式值會高度變動且經常變更。</span><span class="sxs-lookup"><span data-stu-id="58d20-194">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span>

<span data-ttu-id="58d20-195">Microsoft 解決問題的方法是協助您執行瀏覽器偵測元件，以 `sameSite=None` 從 cookie 中去除屬性（如果已知瀏覽器不支援的話）。</span><span class="sxs-lookup"><span data-stu-id="58d20-195">Microsoft's approach to fixing the problem is to help you implement browser detection components to strip the `sameSite=None` attribute from cookies if a browser is known to not support it.</span></span> <span data-ttu-id="58d20-196">Google 的建議是發出雙重 cookie （一個具有新的屬性），另一個則沒有屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-196">Google's advice was to issue double cookies, one with the new attribute, and one without the attribute at all.</span></span> <span data-ttu-id="58d20-197">不過，我們認為 Google 的建議有限。</span><span class="sxs-lookup"><span data-stu-id="58d20-197">However we consider Google's advice limited.</span></span> <span data-ttu-id="58d20-198">有些瀏覽器，特別是行動瀏覽器對於網站的 cookie 數目或功能變數名稱可以傳送的限制極小。</span><span class="sxs-lookup"><span data-stu-id="58d20-198">Some browsers, especially mobile browsers have very small limits on the number of cookies a site, or a domain name can send.</span></span> <span data-ttu-id="58d20-199">傳送多個 cookie （尤其是像驗證 cookie 這樣的大型 cookie）很快就能達到行動瀏覽器的限制，而導致難以診斷和修正的應用程式失敗。</span><span class="sxs-lookup"><span data-stu-id="58d20-199">Sending multiple cookies, especially large cookies like authentication cookies can reach the mobile browser limit very quickly, causing app failures that are hard to diagnose and fix.</span></span> <span data-ttu-id="58d20-200">此外，架構中有很大的協力廠商程式碼和元件的生態系統，可能不會更新為使用雙重 cookie 方法。</span><span class="sxs-lookup"><span data-stu-id="58d20-200">Furthermore as a framework there is a large ecosystem of third party code and components that may not be updated to use a double cookie approach.</span></span>

<span data-ttu-id="58d20-201">[此 GitHub 存放庫]()中範例專案所使用的瀏覽器偵測程式碼包含在兩個檔案中</span><span class="sxs-lookup"><span data-stu-id="58d20-201">The browser detection code used in the sample projects in [this GitHub repository]() is contained in two files</span></span>

* [<span data-ttu-id="58d20-202">C # SameSiteSupport.cs</span><span class="sxs-lookup"><span data-stu-id="58d20-202">C# SameSiteSupport.cs</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.cs)
* [<span data-ttu-id="58d20-203">VB SameSiteSupport .vb</span><span class="sxs-lookup"><span data-stu-id="58d20-203">VB SameSiteSupport.vb</span></span>](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/SameSiteSupport.vb)

<span data-ttu-id="58d20-204">這些偵測是我們所見到的最常見瀏覽器代理程式，可支援2016標準，而且必須完全移除屬性。</span><span class="sxs-lookup"><span data-stu-id="58d20-204">These detections are the most common browser agents we have seen that support the 2016 standard and for which the attribute needs to be completely removed.</span></span> <span data-ttu-id="58d20-205">這並不是完整的實作為：</span><span class="sxs-lookup"><span data-stu-id="58d20-205">It isn't meant as a complete implementation:</span></span>

* <span data-ttu-id="58d20-206">您的應用程式可能會看到我們的測試網站沒有的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="58d20-206">Your app may see browsers that our test sites do not.</span></span>
* <span data-ttu-id="58d20-207">您應該準備好新增環境所需的偵測。</span><span class="sxs-lookup"><span data-stu-id="58d20-207">You should be prepared to add detections as necessary for your environment.</span></span>

<span data-ttu-id="58d20-208">連接偵測的方式會根據您所使用的 .NET 版本和 web 架構而有所不同。</span><span class="sxs-lookup"><span data-stu-id="58d20-208">How you wire up the detection varies according the version of .NET and the web framework that you are using.</span></span> <span data-ttu-id="58d20-209">您可以在 [HttpCookie](/dotnet/api/system.web.httpcookie) 呼叫位置呼叫下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="58d20-209">The following code can be called at the [HttpCookie](/dotnet/api/system.web.httpcookie) call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="58d20-210">請參閱下列 ASP.NET 4.7.2 SameSite cookie 主題：</span><span class="sxs-lookup"><span data-stu-id="58d20-210">See the following ASP.NET 4.7.2 SameSite cookie topics:</span></span>

* [<span data-ttu-id="58d20-211">C# MVC</span><span class="sxs-lookup"><span data-stu-id="58d20-211">C# MVC</span></span>](xref:samesite/csMVC)
* [<span data-ttu-id="58d20-212">C# WebForms</span><span class="sxs-lookup"><span data-stu-id="58d20-212">C# WebForms</span></span>](xref:samesite/CSharpWebForms)
* [<span data-ttu-id="58d20-213">VB WebForms</span><span class="sxs-lookup"><span data-stu-id="58d20-213">VB WebForms</span></span>](xref:samesite/vbWF)
* [<span data-ttu-id="58d20-214">VB MVC</span><span class="sxs-lookup"><span data-stu-id="58d20-214">VB MVC</span></span>](xref:samesite/vbMVC)
<!--
* <xref:samesite/csMVC>
* <xref:samesite/CSharpWebForms>
* <xref:samesite/vbWF>
* <xref:samesite/vbMVC>
-->

### <a name="ensuring-your-site-redirects-to-https"></a><span data-ttu-id="58d20-215">確保您的網站會重新導向至 HTTPS</span><span class="sxs-lookup"><span data-stu-id="58d20-215">Ensuring your site redirects to HTTPS</span></span>

<span data-ttu-id="58d20-216">針對 ASP.NET 4.x、WebForms 和 MVC， [IIS 的 URL 重寫](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) 功能可以用來將所有要求重新導向至 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="58d20-216">For ASP.NET 4.x, WebForms and MVC, [IIS's URL Rewrite](/iis/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module) feature can be used to redirect all requests to HTTPS.</span></span> <span data-ttu-id="58d20-217">下列 XML 會顯示範例規則：</span><span class="sxs-lookup"><span data-stu-id="58d20-217">The following XML shows a sample rule:</span></span>

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

<span data-ttu-id="58d20-218">在內部部署中， [IIS URL 重寫](https://www.iis.net/downloads/microsoft/url-rewrite) 是可能需要安裝的選擇性功能。</span><span class="sxs-lookup"><span data-stu-id="58d20-218">In on-premises installations of [IIS URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) is an optional feature that may need installing.</span></span>

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="58d20-219">測試應用程式的 SameSite 問題</span><span class="sxs-lookup"><span data-stu-id="58d20-219">Test apps for SameSite problems</span></span>

<span data-ttu-id="58d20-220">您必須使用所支援的瀏覽器來測試您的應用程式，並完成牽涉到 cookie 的案例。</span><span class="sxs-lookup"><span data-stu-id="58d20-220">You must test your app with the browsers you support and go through your scenarios that involve cookies.</span></span> <span data-ttu-id="58d20-221">Cookie 案例通常涉及</span><span class="sxs-lookup"><span data-stu-id="58d20-221">Cookie scenarios typically involve</span></span>

* <span data-ttu-id="58d20-222">登入表單</span><span class="sxs-lookup"><span data-stu-id="58d20-222">Login forms</span></span>
* <span data-ttu-id="58d20-223">外部登入機制，例如 Facebook、Azure AD、OAuth 和 OIDC</span><span class="sxs-lookup"><span data-stu-id="58d20-223">External login mechanisms such as Facebook, Azure AD, OAuth and OIDC</span></span>
* <span data-ttu-id="58d20-224">接受來自其他網站之要求的頁面</span><span class="sxs-lookup"><span data-stu-id="58d20-224">Pages that accept requests from other sites</span></span>
* <span data-ttu-id="58d20-225">您應用程式中的頁面，其設計目的是要內嵌在 iframe 中</span><span class="sxs-lookup"><span data-stu-id="58d20-225">Pages in your app designed to be embedded in iframes</span></span>

<span data-ttu-id="58d20-226">您應該檢查 cookie 是否已在您的應用程式中正確建立、保存及刪除。</span><span class="sxs-lookup"><span data-stu-id="58d20-226">You should check that cookies are created, persisted and deleted correctly in your app.</span></span>

<span data-ttu-id="58d20-227">與遠端網站互動的應用程式（例如透過協力廠商登入）必須：</span><span class="sxs-lookup"><span data-stu-id="58d20-227">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="58d20-228">在多個瀏覽器上測試互動。</span><span class="sxs-lookup"><span data-stu-id="58d20-228">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="58d20-229">套用這份檔中討論的 [瀏覽器偵測和緩和措施](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-229">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="58d20-230">使用可加入新 SameSite 行為的用戶端版本，測試 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58d20-230">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="58d20-231">Chrome、Firefox 和 Chromium Edge 都有新的加入宣告功能旗標，可用於測試。</span><span class="sxs-lookup"><span data-stu-id="58d20-231">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="58d20-232">當您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（特別是 Safari）進行測試。</span><span class="sxs-lookup"><span data-stu-id="58d20-232">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="58d20-233">如需詳細資訊，請參閱本檔中的 [支援舊版瀏覽器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-233">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="58d20-234">使用 Chrome 測試</span><span class="sxs-lookup"><span data-stu-id="58d20-234">Test with Chrome</span></span>

<span data-ttu-id="58d20-235">Chrome 78 + 提供誤導的結果，因為它有暫時的緩和措施。</span><span class="sxs-lookup"><span data-stu-id="58d20-235">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="58d20-236">Chrome 78 + 暫時性緩和可讓 cookie 的時間不超過兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="58d20-236">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="58d20-237">使用已啟用適當測試旗標的 Chrome 76 或77可提供更精確的結果。</span><span class="sxs-lookup"><span data-stu-id="58d20-237">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="58d20-238">測試新的 SameSite 行為切換 `chrome://flags/#same-site-by-default-cookies` 為 **啟用狀態**。</span><span class="sxs-lookup"><span data-stu-id="58d20-238">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="58d20-239">較舊版本的 Chrome (75 和以下的) 會回報為失敗，並出現新的 `None` 設定。</span><span class="sxs-lookup"><span data-stu-id="58d20-239">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="58d20-240">請參閱本檔中的 [支援舊版瀏覽器](#sob) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-240">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="58d20-241">Google 未提供較舊的 chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="58d20-241">Google does not make older chrome versions available.</span></span> <span data-ttu-id="58d20-242">遵循 [下載 Chromium](https://www.chromium.org/getting-involved/download-chromium) 中的指示，測試舊版的 Chrome。</span><span class="sxs-lookup"><span data-stu-id="58d20-242">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="58d20-243">請勿從搜尋較舊版本 chrome 所提供的 **連結下載 Chrome** 。</span><span class="sxs-lookup"><span data-stu-id="58d20-243">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="58d20-244">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="58d20-244">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="58d20-245">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="58d20-245">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)
* <span data-ttu-id="58d20-246">如果您不是使用64位版本的 Windows，可以使用 [ [OmahaProxy 檢視器]](https://omahaproxy.appspot.com/) 查閱 [Chromium 所提供的指示](https://www.chromium.org/getting-involved/download-chromium)，將哪個 Chromium 分支對應至 Chrome 74 (v 74.0.3729.108) 。</span><span class="sxs-lookup"><span data-stu-id="58d20-246">If you're not using a 64bit version of Windows you can use the [OmahaProxy viewer](https://omahaproxy.appspot.com/) to look up which Chromium branch corresponds to Chrome 74 (v74.0.3729.108) using the [instructions provided by Chromium](https://www.chromium.org/getting-involved/download-chromium).</span></span>

<span data-ttu-id="58d20-247">從未放大的版本開始 `80.0.3975.0` ，您可以使用新的旗標來停用寬鬆的 + POST 暫時緩和措施， `--enable-features=SameSiteDefaultChecksMethodRigorously` 以在移除緩和措施的功能的最終狀態下測試網站和服務。</span><span class="sxs-lookup"><span data-stu-id="58d20-247">Starting in Canary version `80.0.3975.0`, the Lax+POST temporary mitigation can be disabled for testing purposes using the new flag `--enable-features=SameSiteDefaultChecksMethodRigorously` to allow testing of sites and services in the eventual end state of the feature where the mitigation has been removed.</span></span> <span data-ttu-id="58d20-248">如需詳細資訊，請參閱 Chromium Projects [SameSite 更新](https://www.chromium.org/updates/same-site)</span><span class="sxs-lookup"><span data-stu-id="58d20-248">For more information, see The Chromium Projects [SameSite Updates](https://www.chromium.org/updates/same-site)</span></span>

#### <a name="test-with-chrome-80"></a><span data-ttu-id="58d20-249">使用 Chrome 80 + 進行測試</span><span class="sxs-lookup"><span data-stu-id="58d20-249">Test with Chrome 80+</span></span>

<span data-ttu-id="58d20-250">[下載](https://www.google.com/chrome/) 支援其新屬性的 Chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="58d20-250">[Download](https://www.google.com/chrome/) a version of Chrome that supports their new attribute.</span></span> <span data-ttu-id="58d20-251">在撰寫本文時，目前的版本為 Chrome 80。</span><span class="sxs-lookup"><span data-stu-id="58d20-251">At the time of writing, the current version is Chrome 80.</span></span> <span data-ttu-id="58d20-252">Chrome 80 需要啟用旗標 `chrome://flags/#same-site-by-default-cookies` ，才能使用新的行為。</span><span class="sxs-lookup"><span data-stu-id="58d20-252">Chrome 80 needs the flag `chrome://flags/#same-site-by-default-cookies` enabled to use the new behavior.</span></span> <span data-ttu-id="58d20-253">您也應該啟用 (`chrome://flags/#cookies-without-same-site-must-be-secure`) ，以針對未啟用 sameSite 屬性的 cookie 測試即將推出的行為。</span><span class="sxs-lookup"><span data-stu-id="58d20-253">You should also enable (`chrome://flags/#cookies-without-same-site-must-be-secure`) to test the upcoming behavior for cookies which have no sameSite attribute enabled.</span></span> <span data-ttu-id="58d20-254">Chrome 80 的目標是要讓切換器將 cookie 視為沒有屬性的 cookie `SameSite=Lax` ，雖然某些要求的時間寬限期也是如此。</span><span class="sxs-lookup"><span data-stu-id="58d20-254">Chrome 80 is on target to make the switch to treat cookies without the attribute as `SameSite=Lax`, albeit with a timed grace period for certain requests.</span></span> <span data-ttu-id="58d20-255">若要停用計時寬限期，可使用下列命令列引數來啟動 Chrome 80：</span><span class="sxs-lookup"><span data-stu-id="58d20-255">To disable the timed grace period Chrome 80 can be launched with the following command line argument:</span></span>

`--enable-features=SameSiteDefaultChecksMethodRigorously`

<span data-ttu-id="58d20-256">Chrome 80 在瀏覽器主控台中有關于遺漏 sameSite 屬性的警告訊息。</span><span class="sxs-lookup"><span data-stu-id="58d20-256">Chrome 80 has warning messages in the browser console about missing sameSite attributes.</span></span> <span data-ttu-id="58d20-257">使用 F12 開啟瀏覽器主控台。</span><span class="sxs-lookup"><span data-stu-id="58d20-257">Use F12 to open the browser console.</span></span>

### <a name="test-with-safari"></a><span data-ttu-id="58d20-258">使用 Safari 測試</span><span class="sxs-lookup"><span data-stu-id="58d20-258">Test with Safari</span></span>

<span data-ttu-id="58d20-259">Safari 12 會嚴格地實作為先前的草稿，並在新 `None` 值為 cookie 時失敗。</span><span class="sxs-lookup"><span data-stu-id="58d20-259">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="58d20-260">`None` 可透過支援本檔中 [舊版流覽](#sob) 器的瀏覽器偵測程式碼來避免。</span><span class="sxs-lookup"><span data-stu-id="58d20-260">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="58d20-261">使用 MSAL、ADAL 或您所使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。</span><span class="sxs-lookup"><span data-stu-id="58d20-261">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="58d20-262">問題取決於基礎作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="58d20-262">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="58d20-263">已知 OSX Mojave (10.14) 和 iOS 12 具有新 SameSite 行為的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="58d20-263">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="58d20-264">將作業系統升級至 OSX Catalina (10.15) 或 iOS 13 可修正問題。</span><span class="sxs-lookup"><span data-stu-id="58d20-264">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="58d20-265">Safari 目前沒有可用於測試新規格行為的加入宣告旗標。</span><span class="sxs-lookup"><span data-stu-id="58d20-265">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="58d20-266">使用 Firefox 進行測試</span><span class="sxs-lookup"><span data-stu-id="58d20-266">Test with Firefox</span></span>

<span data-ttu-id="58d20-267">您可以在頁面上選擇具有功能旗標的，以在版本 68 + 上測試新標準的 Firefox 支援 `about:config` `network.cookie.sameSite.laxByDefault` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-267">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="58d20-268">舊版 Firefox 沒有相容性問題的報告。</span><span class="sxs-lookup"><span data-stu-id="58d20-268">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-legacy-browser"></a><span data-ttu-id="58d20-269">使用 Edge (舊版) 瀏覽器進行測試</span><span class="sxs-lookup"><span data-stu-id="58d20-269">Test with Edge (Legacy) browser</span></span>

<span data-ttu-id="58d20-270">Edge 支援舊的 SameSite 標準。</span><span class="sxs-lookup"><span data-stu-id="58d20-270">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="58d20-271">Edge 版本 44 + 沒有任何已知的新標準相容性問題。</span><span class="sxs-lookup"><span data-stu-id="58d20-271">Edge version 44+ doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="58d20-272">使用 Edge (Chromium) 進行測試</span><span class="sxs-lookup"><span data-stu-id="58d20-272">Test with Edge (Chromium)</span></span>

<span data-ttu-id="58d20-273">SameSite 旗標是在頁面上設定的 `edge://flags/#same-site-by-default-cookies` 。</span><span class="sxs-lookup"><span data-stu-id="58d20-273">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="58d20-274">Edge Chromium 未發現任何相容性問題。</span><span class="sxs-lookup"><span data-stu-id="58d20-274">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="58d20-275">使用 Electron 進行測試</span><span class="sxs-lookup"><span data-stu-id="58d20-275">Test with Electron</span></span>

<span data-ttu-id="58d20-276">Electron 的版本包括舊版的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="58d20-276">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="58d20-277">例如，小組所使用的 Electron 版本是 Chromium 66，這會展示較舊的行為。</span><span class="sxs-lookup"><span data-stu-id="58d20-277">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="58d20-278">您必須使用您的產品所使用的 Electron 版本來執行您自己的相容性測試。</span><span class="sxs-lookup"><span data-stu-id="58d20-278">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="58d20-279">請參閱 [支援較舊的瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="58d20-279">See [Supporting older browsers](#sob).</span></span>

## <a name="reverting-samesite-patches"></a><span data-ttu-id="58d20-280">還原 SameSite 修補程式</span><span class="sxs-lookup"><span data-stu-id="58d20-280">Reverting SameSite patches</span></span>

<span data-ttu-id="58d20-281">您可以將 .NET Framework apps 中更新的 sameSite 行為還原為先前的行為，其中不會針對的值發出 sameSite 屬性 `None` ，並將驗證和會話 cookie 還原為不發出值。</span><span class="sxs-lookup"><span data-stu-id="58d20-281">You can revert the updated sameSite behavior in .NET Framework apps to its previous behavior where the sameSite attribute is not emitted for a value of `None`, and revert the authentication and session cookies to not emit the value.</span></span> <span data-ttu-id="58d20-282">這應該視為 *極暫時性的修正*，因為 Chrome 變更會中斷任何外部 POST 要求或使用瀏覽器的使用者驗證，以支援標準的變更。</span><span class="sxs-lookup"><span data-stu-id="58d20-282">This should be viewed as an *extremely temporary fix*, as the Chrome changes will break any external POST requests or authentication for users using browsers which support the changes to the standard.</span></span>

### <a name="reverting-net-472-behavior"></a><span data-ttu-id="58d20-283">還原 .NET 4.7.2 行為</span><span class="sxs-lookup"><span data-stu-id="58d20-283">Reverting .NET 4.7.2 behavior</span></span>

<span data-ttu-id="58d20-284">更新 *web.config* 以包含下列設定：</span><span class="sxs-lookup"><span data-stu-id="58d20-284">Update *web.config* to include the following configuration settings:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="58d20-285">其他資源</span><span class="sxs-lookup"><span data-stu-id="58d20-285">Additional resources</span></span>

* [<span data-ttu-id="58d20-286">ASP.NET 和 ASP.NET Core 中即將推出的 SameSite Cookie 變更</span><span class="sxs-lookup"><span data-stu-id="58d20-286">Upcoming SameSite Cookie Changes in ASP.NET and ASP.NET Core</span></span>](https://devblogs.microsoft.com/aspnet/upcoming-samesite-cookie-changes-in-asp-net-and-asp-net-core/)
* [<span data-ttu-id="58d20-287">依預設 SameSite 測試和偵錯工具的秘訣，以及 "SameSite = None;安全的「cookie</span><span class="sxs-lookup"><span data-stu-id="58d20-287">Tips for testing and debugging SameSite-by-default and “SameSite=None; Secure” cookies</span></span>](https://www.chromium.org/updates/same-site/test-debug)
* [<span data-ttu-id="58d20-288">Chromium Blog：開發人員：準備開始新的 SameSite = None;安全的 Cookie 設定</span><span class="sxs-lookup"><span data-stu-id="58d20-288">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="58d20-289">SameSite cookie 說明</span><span class="sxs-lookup"><span data-stu-id="58d20-289">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)
* [<span data-ttu-id="58d20-290">Chrome 更新</span><span class="sxs-lookup"><span data-stu-id="58d20-290">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)
* [<span data-ttu-id="58d20-291">.NET SameSite 修補程式</span><span class="sxs-lookup"><span data-stu-id="58d20-291">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
* [<span data-ttu-id="58d20-292">Azure Web 應用程式相同的網站資訊</span><span class="sxs-lookup"><span data-stu-id="58d20-292">Azure Web Applications Same Site Information</span></span>](https://azure.microsoft.com/updates/app-service-samesite-cookie-update/)
* [<span data-ttu-id="58d20-293">Azure ActiveDirectory 相同網站資訊</span><span class="sxs-lookup"><span data-stu-id="58d20-293">Azure ActiveDirectory Same Site Information</span></span>](/azure/active-directory/develop/howto-handle-samesite-cookie-changes-chrome-browser)
