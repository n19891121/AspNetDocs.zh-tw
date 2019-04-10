---
uid: web-api/overview/security/basic-authentication
title: ASP.NET Web API 中的基本驗證 |Microsoft Docs
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用基本驗證。
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412550"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="2ede7-103">ASP.NET Web API 中的基本驗證</span><span class="sxs-lookup"><span data-stu-id="2ede7-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="2ede7-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2ede7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2ede7-105">基本驗證定義於[RFC 2617、 HTTP 驗證：基本和摘要式驗證存取](http://www.ietf.org/rfc/rfc2617.txt)。</span><span class="sxs-lookup"><span data-stu-id="2ede7-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="2ede7-106">缺點</span><span class="sxs-lookup"><span data-stu-id="2ede7-106">Disadvantages</span></span>

- <span data-ttu-id="2ede7-107">在要求中傳送使用者認證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="2ede7-108">認證會以純文字傳送。</span><span class="sxs-lookup"><span data-stu-id="2ede7-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="2ede7-109">認證會隨著每個要求傳送。</span><span class="sxs-lookup"><span data-stu-id="2ede7-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="2ede7-110">無法登出，除非結束瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="2ede7-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="2ede7-111">容易遭受跨網站要求偽造 (CSRF);需要防 CSRF 的量值。</span><span class="sxs-lookup"><span data-stu-id="2ede7-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="2ede7-112">優點</span><span class="sxs-lookup"><span data-stu-id="2ede7-112">Advantages</span></span>

- <span data-ttu-id="2ede7-113">網際網路標準。</span><span class="sxs-lookup"><span data-stu-id="2ede7-113">Internet standard.</span></span>
- <span data-ttu-id="2ede7-114">支援所有主要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="2ede7-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="2ede7-115">相當簡單的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2ede7-115">Relatively simple protocol.</span></span>

<span data-ttu-id="2ede7-116">基本驗證的運作方式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ede7-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="2ede7-117">如果要求必須經過驗證，伺服器就會傳回 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="2ede7-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="2ede7-118">此回應包含 Www-authenticate 標頭，指出伺服器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="2ede7-119">用戶端會傳送另一個要求，使用授權標頭中的用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="2ede7-120">認證會格式化為 「 名稱： 密碼 」，以 base64 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="2ede7-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="2ede7-121">不會加密認證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="2ede7-122">基本驗證會執行內容中的"realm"。</span><span class="sxs-lookup"><span data-stu-id="2ede7-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="2ede7-123">伺服器的 WWW 驗證標頭中包含的領域名稱。</span><span class="sxs-lookup"><span data-stu-id="2ede7-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="2ede7-124">使用者的認證的有效期內該領域。</span><span class="sxs-lookup"><span data-stu-id="2ede7-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="2ede7-125">領域的確切的範圍是伺服器所定義。</span><span class="sxs-lookup"><span data-stu-id="2ede7-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="2ede7-126">比方說，您可以定義數個領域中資料分割資源的順序。</span><span class="sxs-lookup"><span data-stu-id="2ede7-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="2ede7-127">認證會傳送未加密的因為基本驗證是只保護透過 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="2ede7-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="2ede7-128">請參閱[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="2ede7-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="2ede7-129">基本驗證也是很容易遭受 CSRF 攻擊。</span><span class="sxs-lookup"><span data-stu-id="2ede7-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="2ede7-130">使用者輸入認證之後，瀏覽器會自動傳送它們在後續要求相同的網域中，工作階段的持續時間。</span><span class="sxs-lookup"><span data-stu-id="2ede7-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="2ede7-131">這包括 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="2ede7-131">This includes AJAX requests.</span></span> <span data-ttu-id="2ede7-132">請參閱[防止跨網站要求偽造 (CSRF) 攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="2ede7-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="2ede7-133">Iis 基本驗證</span><span class="sxs-lookup"><span data-stu-id="2ede7-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="2ede7-134">IIS 支援基本驗證，但還有一點要注意：他們的 Windows 認證驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="2ede7-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="2ede7-135">這表示使用者必須擁有伺服器的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ede7-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="2ede7-136">公開網站，您通常會想要對 ASP.NET 成員資格提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="2ede7-137">若要啟用使用 IIS 的基本驗證，將驗證模式設定為您的 ASP.NET 專案的 Web.config 中的"Windows":</span><span class="sxs-lookup"><span data-stu-id="2ede7-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="2ede7-138">在此模式中，IIS 會使用 Windows 認證來驗證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="2ede7-139">此外，您必須啟用 IIS 中的基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="2ede7-140">在 [IIS 管理員] 中，移至 [功能檢視] 中選取 [驗證]，啟用基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="2ede7-141">在您的 Web API 專案中加入`[Authorize]`適用於任何需要驗證的控制器動作的屬性。</span><span class="sxs-lookup"><span data-stu-id="2ede7-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="2ede7-142">用戶端會進行自我驗證要求中設定授權標頭。</span><span class="sxs-lookup"><span data-stu-id="2ede7-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="2ede7-143">瀏覽器用戶端會自動執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="2ede7-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="2ede7-144">Nonbrowser 用戶端必須設定的標頭。</span><span class="sxs-lookup"><span data-stu-id="2ede7-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="2ede7-145">具有自訂成員資格的基本驗證</span><span class="sxs-lookup"><span data-stu-id="2ede7-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="2ede7-146">如所述，內建在 IIS 基本驗證會使用 Windows 認證。</span><span class="sxs-lookup"><span data-stu-id="2ede7-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="2ede7-147">這表示您需要建立使用者帳戶對您的主控伺服器上。</span><span class="sxs-lookup"><span data-stu-id="2ede7-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="2ede7-148">但是，網際網路應用程式，使用者帳戶通常會儲存在外部資料庫。</span><span class="sxs-lookup"><span data-stu-id="2ede7-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="2ede7-149">下列程式碼如何執行基本驗證的 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="2ede7-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="2ede7-150">您可以輕鬆地外掛的 ASP.NET 成員資格提供者，藉由取代`CheckPassword`方法，這是在此範例中的虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="2ede7-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="2ede7-151">在 Web API 2 中，您應該考慮撰寫[驗證篩選條件](authentication-filters.md)或是[OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/index.md)，而不是 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="2ede7-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="2ede7-152">若要啟用 HTTP 模組，將下列內容新增到您的 web.config 檔案中**system.webServer**區段：</span><span class="sxs-lookup"><span data-stu-id="2ede7-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="2ede7-153">（不包括 「 dll 」 擴充功能） 的組件的名稱取代"YourAssemblyName 」。</span><span class="sxs-lookup"><span data-stu-id="2ede7-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="2ede7-154">您應該停用其他的驗證配置，例如 Forms 或 Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="2ede7-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>
