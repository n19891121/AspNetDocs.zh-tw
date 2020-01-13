---
title: 在 ASP.NET 中使用 SameSite cookie
author: rick-anderson
description: 瞭解如何在 ASP.NET 中使用 SameSite cookie
ms.author: riande
ms.date: 12/03/2019
uid: samesite/system-web-samesite
ms.openlocfilehash: 47a3d7576edb0e818c39b32fbbcb98475248e18e
ms.sourcegitcommit: 7b1e1784213dd4c301635f9e181764f3e2f94162
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74993060"
---
# <a name="work-with-samesite-cookies-in-aspnet"></a><span data-ttu-id="fda50-103">在 ASP.NET 中使用 SameSite cookie</span><span class="sxs-lookup"><span data-stu-id="fda50-103">Work with SameSite cookies in ASP.NET</span></span>

<span data-ttu-id="fda50-104">由 [Rick Anderson](https://twitter.com/RickAndMSFT) 提供</span><span class="sxs-lookup"><span data-stu-id="fda50-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="fda50-105">SameSite 是一種[IETF](https://ietf.org/about/)草稿，其設計目的是要針對跨網站偽造要求（CSRF）攻擊提供一些保護。</span><span class="sxs-lookup"><span data-stu-id="fda50-105">SameSite is an [IETF](https://ietf.org/about/) draft designed to provide some protection against cross-site request forgery (CSRF) attacks.</span></span> <span data-ttu-id="fda50-106">[SameSite 2019 草稿](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00)：</span><span class="sxs-lookup"><span data-stu-id="fda50-106">The [SameSite 2019 draft](https://tools.ietf.org/html/draft-west-cookie-incrementalism-00):</span></span>

* <span data-ttu-id="fda50-107">預設會將 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="fda50-107">Treats cookies as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="fda50-108">說明明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie 應標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="fda50-108">States cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span>

<span data-ttu-id="fda50-109">`Lax` 適用于大部分的應用程式 cookie。</span><span class="sxs-lookup"><span data-stu-id="fda50-109">`Lax` works for most app cookies.</span></span> <span data-ttu-id="fda50-110">某些形式的驗證，例如[OpenID connect](https://openid.net/connect/) （OIDC）和[WS-同盟](https://auth0.com/docs/protocols/ws-fed)，預設為以 POST 為基礎的重新導向。</span><span class="sxs-lookup"><span data-stu-id="fda50-110">Some forms of authentication like [OpenID Connect](https://openid.net/connect/) (OIDC) and [WS-Federation](https://auth0.com/docs/protocols/ws-fed) default to POST based redirects.</span></span> <span data-ttu-id="fda50-111">以 POST 為基礎的重新導向會觸發 SameSite 瀏覽器保護，因此這些元件已停用 SameSite。</span><span class="sxs-lookup"><span data-stu-id="fda50-111">The POST based redirects trigger the SameSite browser protections, so SameSite is disabled for these components.</span></span> <span data-ttu-id="fda50-112">大部分的[OAuth](https://oauth.net/)登入都不會受到影響，因為要求的流動方式不同。</span><span class="sxs-lookup"><span data-stu-id="fda50-112">Most [OAuth](https://oauth.net/) logins are not affected due to differences in how the request flows.</span></span>

<span data-ttu-id="fda50-113">`None` 參數會導致用戶端的相容性問題，而此標準會實作為先前的[2016 草稿標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07)（例如 iOS 12）。</span><span class="sxs-lookup"><span data-stu-id="fda50-113">The `None` parameter causes compatibility problems with clients that implemented the prior [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07) (for example, iOS 12).</span></span> <span data-ttu-id="fda50-114">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-114">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="fda50-115">每個發出 cookie 的 ASP.NET Core 元件都必須決定是否適合 SameSite。</span><span class="sxs-lookup"><span data-stu-id="fda50-115">Each ASP.NET Core component that emits cookies needs to decide if SameSite is appropriate.</span></span>

## <a name="api-usage-with-samesite"></a><span data-ttu-id="fda50-116">使用 SameSite 的 API 使用方式</span><span class="sxs-lookup"><span data-stu-id="fda50-116">API usage with SameSite</span></span>

<span data-ttu-id="fda50-117">請參閱[HttpCookie. SameSite 屬性](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)</span><span class="sxs-lookup"><span data-stu-id="fda50-117">See [HttpCookie.SameSite Property](/dotnet/api/system.web.httpcookie.samesite#System_Web_HttpCookie_SameSite)</span></span>

## <a name="history-and-changes"></a><span data-ttu-id="fda50-118">歷程記錄和變更</span><span class="sxs-lookup"><span data-stu-id="fda50-118">History and changes</span></span>

<span data-ttu-id="fda50-119">SameSite 支援首次使用[2016 draft 標準](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1)在 .net 4.7.2 中執行。</span><span class="sxs-lookup"><span data-stu-id="fda50-119">SameSite support was first implemented in .NET 4.7.2 using the [2016 draft standard](https://tools.ietf.org/html/draft-west-first-party-cookies-07#section-4.1).</span></span>

<span data-ttu-id="fda50-120">2019年11月19日的 Windows 更新，已將 .NET 4.7.2 + 從2016標準更新為2019標準。</span><span class="sxs-lookup"><span data-stu-id="fda50-120">The November 19, 2019 updates for Windows updated .NET 4.7.2+ from the 2016 standard to the 2019 standard.</span></span> <span data-ttu-id="fda50-121">其他版本的 Windows 即將推出其他更新。</span><span class="sxs-lookup"><span data-stu-id="fda50-121">Additional updates are forthcoming for other versions of Windows.</span></span> <span data-ttu-id="fda50-122">如需詳細資訊，請參閱<xref:samesite/kbs-samesite>。</span><span class="sxs-lookup"><span data-stu-id="fda50-122">For more information, see <xref:samesite/kbs-samesite>.</span></span>

 <span data-ttu-id="fda50-123">SameSite 規格的2019草稿：</span><span class="sxs-lookup"><span data-stu-id="fda50-123">The 2019 draft of the SameSite specification:</span></span>

* <span data-ttu-id="fda50-124">與2016草稿**不**相容。</span><span class="sxs-lookup"><span data-stu-id="fda50-124">Is **not** backwards compatible with the 2016 draft.</span></span> <span data-ttu-id="fda50-125">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-125">For more information, see [Supporting older browsers](#sob) in this document.</span></span>
* <span data-ttu-id="fda50-126">指定預設會將 cookie 視為 `SameSite=Lax`。</span><span class="sxs-lookup"><span data-stu-id="fda50-126">Specifies cookies are treated as `SameSite=Lax` by default.</span></span>
* <span data-ttu-id="fda50-127">指定明確判斷提示 `SameSite=None` 以啟用跨網站傳遞的 cookie，應該標示為 `Secure`。</span><span class="sxs-lookup"><span data-stu-id="fda50-127">Specifies cookies that explicitly assert `SameSite=None` in order to enable cross-site delivery should be marked as `Secure`.</span></span> <span data-ttu-id="fda50-128">`None` 是退出宣告的新專案。</span><span class="sxs-lookup"><span data-stu-id="fda50-128">`None` is a new entry to opt out.</span></span>
* <span data-ttu-id="fda50-129">發行的修補程式支援，如上述 KB 所述。</span><span class="sxs-lookup"><span data-stu-id="fda50-129">Is supported by patches issued as described in the KB's listed above.</span></span>
* <span data-ttu-id="fda50-130">排定預設會在[2020 年2月](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)由 [Chrome](https://chromestatus.com/feature/5088147346030592) 啟用。</span><span class="sxs-lookup"><span data-stu-id="fda50-130">Is scheduled to be enabled by [Chrome](https://chromestatus.com/feature/5088147346030592) by default in [Feb 2020](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html).</span></span> <span data-ttu-id="fda50-131">瀏覽器已開始移至2019中的此標準。</span><span class="sxs-lookup"><span data-stu-id="fda50-131">Browsers started moving to this standard in 2019.</span></span>

<a name="sob"></a>

## <a name="supporting-older-browsers"></a><span data-ttu-id="fda50-132">支援舊版瀏覽器</span><span class="sxs-lookup"><span data-stu-id="fda50-132">Supporting older browsers</span></span>

<span data-ttu-id="fda50-133">2016 SameSite 標準規定必須將未知的值視為 `SameSite=Strict` 值。</span><span class="sxs-lookup"><span data-stu-id="fda50-133">The 2016 SameSite standard mandated that unknown values must be treated as `SameSite=Strict` values.</span></span> <span data-ttu-id="fda50-134">從支援 2016 SameSite standard 的舊版瀏覽器存取的應用程式，可能會在取得值為 `None`的 SameSite 屬性時中斷。</span><span class="sxs-lookup"><span data-stu-id="fda50-134">Apps accessed from older browsers which support the 2016 SameSite standard may break when they get a SameSite property with a value of `None`.</span></span> <span data-ttu-id="fda50-135">如果 Web 應用程式想要支援較舊的瀏覽器，則必須執行瀏覽器偵測。</span><span class="sxs-lookup"><span data-stu-id="fda50-135">Web apps must implement browser detection if they intend to support older browsers.</span></span> <span data-ttu-id="fda50-136">ASP.NET 不會實作為瀏覽器偵測，因為使用者代理程式的值會高度變動並經常變更。</span><span class="sxs-lookup"><span data-stu-id="fda50-136">ASP.NET doesn't implement browser detection because User-Agents values are highly volatile and change frequently.</span></span> <span data-ttu-id="fda50-137">可以在 <xref:HTTP.HttpCookie> 呼叫位置呼叫下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="fda50-137">The following code can be called at the <xref:HTTP.HttpCookie> call site:</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet)]

<span data-ttu-id="fda50-138">在上述範例中，`MyUserAgentDetectionLib.DisallowsSameSiteNone` 是使用者提供的程式庫，可偵測使用者代理程式是否不支援 SameSite `None`。</span><span class="sxs-lookup"><span data-stu-id="fda50-138">In the preceding sample, `MyUserAgentDetectionLib.DisallowsSameSiteNone` is a user supplied library that detects if the user agent doesn't support SameSite `None`.</span></span> <span data-ttu-id="fda50-139">下列程式碼顯示範例 `DisallowsSameSiteNone` 方法：</span><span class="sxs-lookup"><span data-stu-id="fda50-139">The following code shows a sample `DisallowsSameSiteNone` method:</span></span>

> [!WARNING]
> <span data-ttu-id="fda50-140">下列程式碼僅供示範之用：</span><span class="sxs-lookup"><span data-stu-id="fda50-140">The following code is for demonstration only:</span></span>
> * <span data-ttu-id="fda50-141">不應該將它視為已完成。</span><span class="sxs-lookup"><span data-stu-id="fda50-141">It should not be considered complete.</span></span>
> * <span data-ttu-id="fda50-142">不會維護或支援。</span><span class="sxs-lookup"><span data-stu-id="fda50-142">It is not maintained or supported.</span></span>

[!code-csharp[](sample/SameSiteCheck.cs?name=snippet2)]

## <a name="test-apps-for-samesite-problems"></a><span data-ttu-id="fda50-143">測試應用程式的 SameSite 問題</span><span class="sxs-lookup"><span data-stu-id="fda50-143">Test apps for SameSite problems</span></span>

<span data-ttu-id="fda50-144">與遠端網站（例如透過協力廠商登入）互動的應用程式需要：</span><span class="sxs-lookup"><span data-stu-id="fda50-144">Apps that interact with remote sites such as through third-party login need to:</span></span>

* <span data-ttu-id="fda50-145">測試多個瀏覽器的互動。</span><span class="sxs-lookup"><span data-stu-id="fda50-145">Test the interaction on multiple browsers.</span></span>
* <span data-ttu-id="fda50-146">套用本檔中討論的[瀏覽器偵測和緩和措施](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-146">Apply the [browser detection and mitigation](#sob) discussed in this document.</span></span>

<span data-ttu-id="fda50-147">使用可選擇新 SameSite 行為的用戶端版本來測試 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fda50-147">Test web apps using a client version that can opt-in to the new SameSite behavior.</span></span> <span data-ttu-id="fda50-148">Chrome、Firefox 和 Chromium Edge 全都具有可用於測試的新加入宣告功能旗標。</span><span class="sxs-lookup"><span data-stu-id="fda50-148">Chrome, Firefox, and Chromium Edge all have new opt-in feature flags that can be used for testing.</span></span> <span data-ttu-id="fda50-149">在您的應用程式套用 SameSite 修補程式之後，請使用較舊的用戶端版本（尤其是 Safari）進行測試。</span><span class="sxs-lookup"><span data-stu-id="fda50-149">After your app applies the SameSite patches, test it with older client versions, especially Safari.</span></span> <span data-ttu-id="fda50-150">如需詳細資訊，請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-150">For more information, see [Supporting older browsers](#sob) in this document.</span></span>

### <a name="test-with-chrome"></a><span data-ttu-id="fda50-151">使用 Chrome 進行測試</span><span class="sxs-lookup"><span data-stu-id="fda50-151">Test with Chrome</span></span>

<span data-ttu-id="fda50-152">Chrome 78 + 會提供誤導的結果，因為它有暫時的緩和措施。</span><span class="sxs-lookup"><span data-stu-id="fda50-152">Chrome 78+ gives misleading results because it has a temporary mitigation in place.</span></span> <span data-ttu-id="fda50-153">Chrome 78 + 暫時緩和可讓 cookie 少於兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="fda50-153">The Chrome 78+ temporary mitigation allows cookies less than two minutes old.</span></span> <span data-ttu-id="fda50-154">已啟用適當測試旗標的 Chrome 76 或77提供更精確的結果。</span><span class="sxs-lookup"><span data-stu-id="fda50-154">Chrome 76 or 77 with the appropriate test flags enabled provides more accurate results.</span></span> <span data-ttu-id="fda50-155">若要測試新的 SameSite 行為，請切換 `chrome://flags/#same-site-by-default-cookies` 為 [**已啟用**]。</span><span class="sxs-lookup"><span data-stu-id="fda50-155">To test the new SameSite behavior toggle `chrome://flags/#same-site-by-default-cookies` to **Enabled**.</span></span> <span data-ttu-id="fda50-156">舊版 Chrome （75和更低版本）會回報為失敗，並出現新的 `None` 設定。</span><span class="sxs-lookup"><span data-stu-id="fda50-156">Older versions of Chrome (75 and below) are reported to fail with the new `None` setting.</span></span> <span data-ttu-id="fda50-157">請參閱本檔中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-157">See [Supporting older browsers](#sob) in this document.</span></span>

<span data-ttu-id="fda50-158">Google 不會提供舊版的 chrome 版本。</span><span class="sxs-lookup"><span data-stu-id="fda50-158">Google does not make older chrome versions available.</span></span> <span data-ttu-id="fda50-159">請遵循[下載 Chromium](https://www.chromium.org/getting-involved/download-chromium)的指示來測試舊版 Chrome。</span><span class="sxs-lookup"><span data-stu-id="fda50-159">Follow the instructions at [Download Chromium](https://www.chromium.org/getting-involved/download-chromium) to test older versions of Chrome.</span></span> <span data-ttu-id="fda50-160">請勿從搜尋舊版 chrome 所提供的**連結下載 Chrome** 。</span><span class="sxs-lookup"><span data-stu-id="fda50-160">Do **not** download Chrome from links provided by searching for older versions of chrome.</span></span>

* [<span data-ttu-id="fda50-161">Chromium 76 Win64</span><span class="sxs-lookup"><span data-stu-id="fda50-161">Chromium 76 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/664998/)
* [<span data-ttu-id="fda50-162">Chromium 74 Win64</span><span class="sxs-lookup"><span data-stu-id="fda50-162">Chromium 74 Win64</span></span>](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Win_x64/638880/)

### <a name="test-with-safari"></a><span data-ttu-id="fda50-163">使用 Safari 進行測試</span><span class="sxs-lookup"><span data-stu-id="fda50-163">Test with Safari</span></span>

<span data-ttu-id="fda50-164">Safari 12 會嚴格實作為先前的草稿，並在新的 `None` 值在 cookie 中失敗。</span><span class="sxs-lookup"><span data-stu-id="fda50-164">Safari 12 strictly implemented the prior draft and fails when the new `None` value is in a cookie.</span></span> <span data-ttu-id="fda50-165">透過此檔中[支援較舊流覽](#sob)器的瀏覽器偵測程式碼，可避免 `None`。</span><span class="sxs-lookup"><span data-stu-id="fda50-165">`None` is avoided via the browser detection code [Supporting older browsers](#sob) in this document.</span></span> <span data-ttu-id="fda50-166">使用 MSAL、ADAL 或您使用的任何程式庫，測試 Safari 12、Safari 13 和以 WebKit 為基礎的 OS 樣式登入。</span><span class="sxs-lookup"><span data-stu-id="fda50-166">Test Safari 12, Safari 13, and WebKit based OS style logins using MSAL, ADAL or whatever library you are using.</span></span> <span data-ttu-id="fda50-167">問題取決於基礎作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="fda50-167">The problem is dependent on the underlying OS version.</span></span> <span data-ttu-id="fda50-168">OSX Mojave （10.14）和 iOS 12 已知具有新 SameSite 行為的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fda50-168">OSX Mojave (10.14) and iOS 12 are known to have compatibility problems with the new SameSite behavior.</span></span> <span data-ttu-id="fda50-169">將 OS 升級至 OSX Catalina （10.15）或 iOS 13 會修正問題。</span><span class="sxs-lookup"><span data-stu-id="fda50-169">Upgrading the OS to OSX Catalina (10.15) or iOS 13 fixes the problem.</span></span> <span data-ttu-id="fda50-170">Safari 目前沒有加入宣告旗標來測試新的規格行為。</span><span class="sxs-lookup"><span data-stu-id="fda50-170">Safari does not currently have an opt-in flag for testing the new spec behavior.</span></span>

### <a name="test-with-firefox"></a><span data-ttu-id="fda50-171">使用 Firefox 進行測試</span><span class="sxs-lookup"><span data-stu-id="fda50-171">Test with Firefox</span></span>

<span data-ttu-id="fda50-172">在 [`about:config`] 頁面上選擇 [`network.cookie.sameSite.laxByDefault`] 功能旗標，即可在版本 68 + 上測試新標準的 Firefox 支援。</span><span class="sxs-lookup"><span data-stu-id="fda50-172">Firefox support for the new standard can be tested on version 68+ by opting in on the `about:config` page with the feature flag `network.cookie.sameSite.laxByDefault`.</span></span> <span data-ttu-id="fda50-173">尚未報告舊版 Firefox 的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fda50-173">There haven't been reports of compatibility issues with older versions of Firefox.</span></span>

### <a name="test-with-edge-browser"></a><span data-ttu-id="fda50-174">使用 Edge 瀏覽器進行測試</span><span class="sxs-lookup"><span data-stu-id="fda50-174">Test with Edge browser</span></span>

<span data-ttu-id="fda50-175">Edge 支援舊的 SameSite 標準。</span><span class="sxs-lookup"><span data-stu-id="fda50-175">Edge supports the old SameSite standard.</span></span> <span data-ttu-id="fda50-176">Edge 版本44沒有任何已知的新標準相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fda50-176">Edge version 44 doesn't have any known compatibility problems with the new standard.</span></span>

### <a name="test-with-edge-chromium"></a><span data-ttu-id="fda50-177">使用 Edge 進行測試（Chromium）</span><span class="sxs-lookup"><span data-stu-id="fda50-177">Test with Edge (Chromium)</span></span>

<span data-ttu-id="fda50-178">在 [`edge://flags/#same-site-by-default-cookies`] 頁面上設定 SameSite 旗標。</span><span class="sxs-lookup"><span data-stu-id="fda50-178">SameSite flags are set on the `edge://flags/#same-site-by-default-cookies` page.</span></span> <span data-ttu-id="fda50-179">Edge Chromium 未發現相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fda50-179">No compatibility issues were discovered with Edge Chromium.</span></span>

### <a name="test-with-electron"></a><span data-ttu-id="fda50-180">使用 Electron 進行測試</span><span class="sxs-lookup"><span data-stu-id="fda50-180">Test with Electron</span></span>

<span data-ttu-id="fda50-181">Electron 的版本包含舊版的 Chromium。</span><span class="sxs-lookup"><span data-stu-id="fda50-181">Versions of Electron include older versions of Chromium.</span></span> <span data-ttu-id="fda50-182">例如，小組所使用的 Electron 版本是 Chromium 66，這會展現較舊的行為。</span><span class="sxs-lookup"><span data-stu-id="fda50-182">For example, the version of Electron used by Teams is Chromium 66, which exhibits the older behavior.</span></span> <span data-ttu-id="fda50-183">您必須使用您的產品所使用的 Electron 版本來執行自己的相容性測試。</span><span class="sxs-lookup"><span data-stu-id="fda50-183">You must perform your own compatibility testing with the version of Electron your product uses.</span></span> <span data-ttu-id="fda50-184">請參閱下一節中的[支援舊版瀏覽器](#sob)。</span><span class="sxs-lookup"><span data-stu-id="fda50-184">See [Supporting older browsers](#sob) in the following section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fda50-185">其他資源</span><span class="sxs-lookup"><span data-stu-id="fda50-185">Additional resources</span></span>

* [<span data-ttu-id="fda50-186">Chromium Blog：開發人員：準備開始新的 SameSite = None;安全 Cookie 設定</span><span class="sxs-lookup"><span data-stu-id="fda50-186">Chromium Blog:Developers: Get Ready for New SameSite=None; Secure Cookie Settings</span></span>](https://blog.chromium.org/2019/10/developers-get-ready-for-new.html)
* [<span data-ttu-id="fda50-187">SameSite cookie 說明</span><span class="sxs-lookup"><span data-stu-id="fda50-187">SameSite cookies explained</span></span>](https://web.dev/samesite-cookies-explained/)