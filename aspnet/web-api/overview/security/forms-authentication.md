---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API 中表單驗證 |Microsoft Docs
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用表單驗證。
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59410069"
---
# <a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="277d6-103">ASP.NET Web API 中的表單驗證</span><span class="sxs-lookup"><span data-stu-id="277d6-103">Forms Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="277d6-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="277d6-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="277d6-105">表單驗證會使用 HTML 表單，使用者的認證傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="277d6-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="277d6-106">它不是網際網路標準。</span><span class="sxs-lookup"><span data-stu-id="277d6-106">It is not an Internet standard.</span></span> <span data-ttu-id="277d6-107">讓使用者可以互動的 HTML 表單，表單驗證僅適用於 web 的 web 應用程式中，從呼叫的 Api。</span><span class="sxs-lookup"><span data-stu-id="277d6-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="277d6-108">優點</span><span class="sxs-lookup"><span data-stu-id="277d6-108">Advantages</span></span> | <span data-ttu-id="277d6-109">缺點</span><span class="sxs-lookup"><span data-stu-id="277d6-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="277d6-110">輕鬆實作：內建於 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="277d6-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="277d6-111">-使用 ASP.NET 成員資格提供者，方便您管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="277d6-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="277d6-112">-不標準 HTTP 驗證機制;會使用 HTTP cookie，而不是標準的授權標頭。</span><span class="sxs-lookup"><span data-stu-id="277d6-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="277d6-113">-需要瀏覽器用戶端。</span><span class="sxs-lookup"><span data-stu-id="277d6-113">- Requires a browser client.</span></span> <span data-ttu-id="277d6-114">認證會以純文字傳送。</span><span class="sxs-lookup"><span data-stu-id="277d6-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="277d6-115">-容易遭受跨網站要求偽造 (CSRF);需要防 CSRF 的量值。</span><span class="sxs-lookup"><span data-stu-id="277d6-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="277d6-116">-很難從 nonbrowser 用戶端使用。</span><span class="sxs-lookup"><span data-stu-id="277d6-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="277d6-117">登入需要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="277d6-117">Login requires a browser.</span></span> <span data-ttu-id="277d6-118">在要求中傳送使用者認證。</span><span class="sxs-lookup"><span data-stu-id="277d6-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="277d6-119">-部分的使用者停用 cookie。</span><span class="sxs-lookup"><span data-stu-id="277d6-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="277d6-120">簡單地說，在 ASP.NET 中的表單驗證的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="277d6-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="277d6-121">用戶端要求需要驗證的資源。</span><span class="sxs-lookup"><span data-stu-id="277d6-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="277d6-122">如果使用者未經過驗證，伺服器就會傳回 HTTP 302 （已找到），並將重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="277d6-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="277d6-123">使用者輸入認證，並送出表單。</span><span class="sxs-lookup"><span data-stu-id="277d6-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="277d6-124">伺服器會傳回另一個 HTTP 302 重新導向回到原始的 URI。</span><span class="sxs-lookup"><span data-stu-id="277d6-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="277d6-125">此回應包含驗證 cookie。</span><span class="sxs-lookup"><span data-stu-id="277d6-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="277d6-126">用戶端一次要求的資源。</span><span class="sxs-lookup"><span data-stu-id="277d6-126">The client requests the resource again.</span></span> <span data-ttu-id="277d6-127">要求會包含驗證 cookie，因此伺服器會授與的要求。</span><span class="sxs-lookup"><span data-stu-id="277d6-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="277d6-128">如需詳細資訊，請參閱[的表單驗證概觀。](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="277d6-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="277d6-129">使用表單驗證來使用 Web API</span><span class="sxs-lookup"><span data-stu-id="277d6-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="277d6-130">若要建立使用表單驗證的應用程式，選取 [MVC 4 專案精靈] 中的 「 網際網路應用程式 」 範本。</span><span class="sxs-lookup"><span data-stu-id="277d6-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="277d6-131">此範本會建立適用於帳戶管理的 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="277d6-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="277d6-132">您也可以使用 「 單一頁面應用程式 」 範本，在 ASP.NET Fall 2012 更新中提供。</span><span class="sxs-lookup"><span data-stu-id="277d6-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="277d6-133">在您的 web API 控制器，您可以使用限制存取`[Authorize]`屬性中所述[使用 [Authorize] 屬性](authentication-and-authorization-in-aspnet-web-api.md#auth3)。</span><span class="sxs-lookup"><span data-stu-id="277d6-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="277d6-134">表單驗證會使用工作階段 cookie 來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="277d6-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="277d6-135">瀏覽器會自動將所有相關的 cookie 傳送至目的地網站。</span><span class="sxs-lookup"><span data-stu-id="277d6-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="277d6-136">這項功能，可讓表單驗證可能容易遭受跨網站要求偽造 (CSRF) 攻擊，請參閱[防止跨網站要求偽造 (CSRF) 攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。</span><span class="sxs-lookup"><span data-stu-id="277d6-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="277d6-137">表單驗證不會加密使用者認證。</span><span class="sxs-lookup"><span data-stu-id="277d6-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="277d6-138">因此，不安全，除非搭配 SSL 使用表單驗證。</span><span class="sxs-lookup"><span data-stu-id="277d6-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="277d6-139">請參閱[使用 Web API 中的 SSL](working-with-ssl-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="277d6-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
