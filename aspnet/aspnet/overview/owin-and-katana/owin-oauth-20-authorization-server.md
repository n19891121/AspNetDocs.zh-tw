---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授權伺服器 |微軟文件
author: hongyes
description: 本教學將指導您如何使用 OWIN OAuth 中間件實現 OAuth 2.0 授權伺服器。 這是一個高級教程,只有出...
ms.author: riande
ms.date: 03/20/2014
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: d758fa2639d10e1b7be8d87c5d1f7adb7e292ac7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540384"
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="c4f94-104">OWIN OAuth 2.0 授權伺服器</span><span class="sxs-lookup"><span data-stu-id="c4f94-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="c4f94-105">由[孫洪業](https://github.com/hongyes)和[普拉布拉傑·蒂加拉詹](https://github.com/Praburaj)</span><span class="sxs-lookup"><span data-stu-id="c4f94-105">by [Hongye Sun](https://github.com/hongyes) and [Praburaj Thiagarajan](https://github.com/Praburaj)</span></span>

> <span data-ttu-id="c4f94-106">本教學將指導您如何使用 OWIN OAuth 中間件實現 OAuth 2.0 授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4f94-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="c4f94-107">這是一個高級教程,僅概述創建 OWIN OAuth 2.0 授權伺服器的步驟。</span><span class="sxs-lookup"><span data-stu-id="c4f94-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="c4f94-108">這不是一步一步的教程。</span><span class="sxs-lookup"><span data-stu-id="c4f94-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="c4f94-109">[下載範例代碼](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
>
> > [!NOTE]
> > <span data-ttu-id="c4f94-110">此大綱不應用於創建安全生產應用。</span><span class="sxs-lookup"><span data-stu-id="c4f94-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="c4f94-111">本教學旨在僅提供如何使用 OWIN OAuth 中間件實現 OAuth 2.0 授權伺服器的大綱。</span><span class="sxs-lookup"><span data-stu-id="c4f94-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="c4f94-112">軟體版本</span><span class="sxs-lookup"><span data-stu-id="c4f94-112">Software versions</span></span>
>
> | <span data-ttu-id="c4f94-113">**在教學中顯示**</span><span class="sxs-lookup"><span data-stu-id="c4f94-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="c4f94-114">**也適用於**</span><span class="sxs-lookup"><span data-stu-id="c4f94-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="c4f94-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c4f94-115">Windows 8.1</span></span> | <span data-ttu-id="c4f94-116">視窗 8, 視窗 7</span><span class="sxs-lookup"><span data-stu-id="c4f94-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="c4f94-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c4f94-117">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | <span data-ttu-id="c4f94-118">[視覺工作室 2013 快遞為桌面](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span><span class="sxs-lookup"><span data-stu-id="c4f94-118">[Visual Studio 2013 Express for Desktop](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express).</span></span> <span data-ttu-id="c4f94-119">帶有最新更新的 Visual Studio 2012 應該可以正常工作,但本教程尚未使用它進行測試,並且某些功能表選擇和對話方塊是不同的。</span><span class="sxs-lookup"><span data-stu-id="c4f94-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="c4f94-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c4f94-120">.NET 4.5</span></span> |  |
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c4f94-121">問題和評論</span><span class="sxs-lookup"><span data-stu-id="c4f94-121">Questions and Comments</span></span>
>
> <span data-ttu-id="c4f94-122">如果您有與本教程沒有直接關係的問題,您可以在[GitHub 上的 Katana 專案](https://github.com/aspnet/AspNetKatana/)上發佈這些問題。</span><span class="sxs-lookup"><span data-stu-id="c4f94-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="c4f94-123">有關教程本身的問題和註釋,請參閱頁面底部的註釋部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="c4f94-124">[OAuth 2.0 框架](http://tools.ietf.org/html/rfc6749)使第三方應用能夠獲得對 HTTP 服務的有限存取許可權。</span><span class="sxs-lookup"><span data-stu-id="c4f94-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="c4f94-125">用戶端不需要使用資源擁有者的憑據來訪問受保護的資源,而是獲取訪問權杖(這是表示特定作用域、存留期和其他訪問屬性的字串)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="c4f94-126">訪問權杖由授權伺服器在資源擁有者批准下頒發給第三方用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="c4f94-127">本教學將介紹:</span><span class="sxs-lookup"><span data-stu-id="c4f94-127">This tutorial will cover:</span></span>

- <span data-ttu-id="c4f94-128">如何建立授權伺服器以支援四種授權的類別和刷新權杖:</span><span class="sxs-lookup"><span data-stu-id="c4f94-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="c4f94-129">授權代碼授予</span><span class="sxs-lookup"><span data-stu-id="c4f94-129">Authorization code grant</span></span>
    - <span data-ttu-id="c4f94-130">隱含式</span><span class="sxs-lookup"><span data-stu-id="c4f94-130">Implicit Grant</span></span>
    - <span data-ttu-id="c4f94-131">資源擁有者密碼認證</span><span class="sxs-lookup"><span data-stu-id="c4f94-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="c4f94-132">用戶端認證</span><span class="sxs-lookup"><span data-stu-id="c4f94-132">Client Credentials Grant</span></span>
- <span data-ttu-id="c4f94-133">建立受訪問權杖保護的資源伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4f94-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="c4f94-134">創建 OAuth 2.0 用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="c4f94-135">必要條件</span><span class="sxs-lookup"><span data-stu-id="c4f94-135">Prerequisites</span></span>

- <span data-ttu-id="c4f94-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免費[的 Visual Studio Express 2013,](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)如頁面頂部**的軟體版本**所示。</span><span class="sxs-lookup"><span data-stu-id="c4f94-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="c4f94-137">熟悉 OWIN。</span><span class="sxs-lookup"><span data-stu-id="c4f94-137">Familiarity with OWIN.</span></span> <span data-ttu-id="c4f94-138">請參閱[開始與卡塔納項目和](https://msdn.microsoft.com/magazine/dn451439.aspx)[什麼在OWIN和卡塔納的新增功能](index.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="c4f94-139">熟悉[OAuth](http://tools.ietf.org/html/rfc6749)的術語,包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)、[協定流程](http://tools.ietf.org/html/rfc6749#section-1.2)與[授權的授予](http://tools.ietf.org/html/rfc6749#section-1.3)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="c4f94-140">[OAuth 2.0 介紹](http://tools.ietf.org/html/rfc6749#section-1)提供了很好的介紹。</span><span class="sxs-lookup"><span data-stu-id="c4f94-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="c4f94-141">建立授權伺服器</span><span class="sxs-lookup"><span data-stu-id="c4f94-141">Create an Authorization Server</span></span>

<span data-ttu-id="c4f94-142">在本教學中,我們將大致勾勒出如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 創建授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4f94-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="c4f94-143">我們希望很快為已完成的示例提供下載,因為本教程不包括每個步驟。</span><span class="sxs-lookup"><span data-stu-id="c4f94-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="c4f94-144">首先,建立名為 *「授權伺服器」* 的空 Web 應用程式並安裝以下程式套件:</span><span class="sxs-lookup"><span data-stu-id="c4f94-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="c4f94-145">微軟.阿斯普內.Mvc</span><span class="sxs-lookup"><span data-stu-id="c4f94-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="c4f94-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="c4f94-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="c4f94-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="c4f94-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="c4f94-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="c4f94-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="c4f94-149">微軟.Owin.Security.Google(或任何其他社交登錄包,如微軟.Owin.Security.Facebook)</span><span class="sxs-lookup"><span data-stu-id="c4f94-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="c4f94-150">在名為 *「啟動」* 的項目根資料夾下新增[OWIN 啟動類別](owin-startup-class-detection.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="c4f94-151">建立 *"\_應用 開始'* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c4f94-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="c4f94-152">選擇 *「\_應用程式啟動」* 資料夾並使用 Shift_Alt_A 添加 *「\_授權伺服器」[應用啟動]啟動.Auth.cs*檔的下載版本。</span><span class="sxs-lookup"><span data-stu-id="c4f94-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="c4f94-153">上述代碼支援應用程式/外部登錄 Cookie 和 Google 身份驗證,授權伺服器本身使用它們來管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4f94-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="c4f94-154">擴展`UseOAuthAuthorizationServer`方法是設置授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4f94-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="c4f94-155">設定選項包括:</span><span class="sxs-lookup"><span data-stu-id="c4f94-155">The setup options are:</span></span>

- <span data-ttu-id="c4f94-156">`AuthorizeEndpointPath`:客戶端應用程式將重定向使用者代理以獲得使用者同意發出權杖或代碼的請求路徑。</span><span class="sxs-lookup"><span data-stu-id="c4f94-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="c4f94-157">它必須以前導斜杠開頭,例如,""。`/Authorize`</span><span class="sxs-lookup"><span data-stu-id="c4f94-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="c4f94-158">`TokenEndpointPath`:請求路徑用戶端應用程式直接通信以獲取訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="c4f94-159">它必須以前導斜杠開頭,如"/令牌"。</span><span class="sxs-lookup"><span data-stu-id="c4f94-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="c4f94-160">如果用戶端被頒發[\_客戶端密鑰](http://tools.ietf.org/html/rfc6749#appendix-A.2),則必須將其提供給此終結點。</span><span class="sxs-lookup"><span data-stu-id="c4f94-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="c4f94-161">`ApplicationCanDisplayErrors`:設定為`true`如果 Web 應用程式想要為`/Authorize`終結點上的 客戶端驗證錯誤生成自訂錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="c4f94-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="c4f94-162">只當瀏覽器未重定向回用戶端應用程式(例如,`client_id`當`redirect_uri`或不正確時),才需要這樣做。</span><span class="sxs-lookup"><span data-stu-id="c4f94-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="c4f94-163">終結點`/Authorize`應期望看到"auth"。錯誤","哦。錯誤描述"和"錯誤描述"ErrorUri"屬性將添加到 OWIN 環境中。</span><span class="sxs-lookup"><span data-stu-id="c4f94-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4f94-164">如果為 true,授權伺服器將返回包含錯誤詳細資訊的預設錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="c4f94-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="c4f94-165">`AllowInsecureHttp`:如果為 True,允許授權和權杖請求到達 HTTP URI`redirect_uri`位址,並允許 傳入授權請求參數具有 HTTP URI 位址。</span><span class="sxs-lookup"><span data-stu-id="c4f94-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c4f94-166">安全性 - 這僅用於開發。</span><span class="sxs-lookup"><span data-stu-id="c4f94-166">Security - This is for development only.</span></span>
- <span data-ttu-id="c4f94-167">`Provider`:應用程式為處理授權伺服器中間件引發的事件而提供的物件。</span><span class="sxs-lookup"><span data-stu-id="c4f94-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="c4f94-168">應用程式可以完全實現介面,也可以創建此伺服器支援的 OAuth`OAuthAuthorizationServerProvider`流所需的實例和分配委託。</span><span class="sxs-lookup"><span data-stu-id="c4f94-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="c4f94-169">`AuthorizationCodeProvider`:生成一次性授權代碼以返回到用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4f94-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="c4f94-170">為了保護 OAuth 伺服器的安全,應用程式**必須**提供一個`AuthorizationCodeProvider`實體`OnCreate/OnCreateAsync`,其中事件產生的權杖僅對一次呼`OnReceive/OnReceiveAsync`叫有效 。</span><span class="sxs-lookup"><span data-stu-id="c4f94-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="c4f94-171">`RefreshTokenProvider`:生成刷新權杖,可在需要時用於生成新的訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="c4f94-172">如果未提供授權伺服器將不會從`/Token`終結點返回刷新權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="c4f94-173">帳戶管理</span><span class="sxs-lookup"><span data-stu-id="c4f94-173">Account Management</span></span>

<span data-ttu-id="c4f94-174">OAuth 不關心您管理使用者帳戶資訊的位置或方式。</span><span class="sxs-lookup"><span data-stu-id="c4f94-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="c4f94-175">負責它的[ASP.NET 身份](../../../identity/index.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="c4f94-176">在本教學中,我們將簡化帳戶管理代碼,並確保使用者可以使用 OWIN Cookie 中間件登錄。</span><span class="sxs-lookup"><span data-stu-id="c4f94-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="c4f94-177">下面是 :`AccountController`的 簡化範例碼:</span><span class="sxs-lookup"><span data-stu-id="c4f94-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="c4f94-178">`ValidateClientRedirectUri`用於驗證用戶端及其註冊的重定向 URL。</span><span class="sxs-lookup"><span data-stu-id="c4f94-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="c4f94-179">`ValidateClientAuthentication`檢查基本方案標頭和窗體正文以獲取客戶端的認證。</span><span class="sxs-lookup"><span data-stu-id="c4f94-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="c4f94-180">登入頁面如下所示:</span><span class="sxs-lookup"><span data-stu-id="c4f94-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="c4f94-181">立即查看 IETF 的 OAuth 2[授權代碼授予](http://tools.ietf.org/html/rfc6749#section-4.1)部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span>

<span data-ttu-id="c4f94-182">**提供者**(下表中)是[OAuth 授權伺服器選項](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程式,其類型`OAuthAuthorizationServerProvider`為 ,它包含所有 OAuth 伺服器事件。</span><span class="sxs-lookup"><span data-stu-id="c4f94-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span>

| <span data-ttu-id="c4f94-183">授權代碼授予部分的流步驟</span><span class="sxs-lookup"><span data-stu-id="c4f94-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="c4f94-184">範例下載以下步驟:</span><span class="sxs-lookup"><span data-stu-id="c4f94-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c4f94-185">(A) 客戶端通過將資源擁有者的使用者代理定向到授權終結點來啟動流。</span><span class="sxs-lookup"><span data-stu-id="c4f94-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="c4f94-186">用戶端包括其客戶端識別碼、請求的範圍、本地狀態和重定向 URI,授權伺服器將在授予(或拒絕)訪問許可權後將使用者代理發送回該 URI。</span><span class="sxs-lookup"><span data-stu-id="c4f94-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="c4f94-187">提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點</span><span class="sxs-lookup"><span data-stu-id="c4f94-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="c4f94-188">(B) 授權伺服器對資源擁有者進行身份驗證(通過使用者代理),並確定資源擁有者是授予還是拒絕用戶端的訪問請求。</span><span class="sxs-lookup"><span data-stu-id="c4f94-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="c4f94-189">**如果使用者授予存取&gt;&lt;權限**提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點授權碼提供者.建立Async</span><span class="sxs-lookup"><span data-stu-id="c4f94-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c4f94-190">(C) 假設資源擁有者授予存取許可權,授權伺服器使用前面提供的重定向 URI(在請求中或用戶端註冊期間)將使用者代理重定向回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="c4f94-191">...</span><span class="sxs-lookup"><span data-stu-id="c4f94-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="c4f94-192">(D) 客戶端通過包含上一步驟中收到的授權代碼,從授權伺服器的權杖終結點請求訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="c4f94-193">發出請求時,用戶端會使用授權伺服器進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c4f94-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="c4f94-194">用戶端包括用於獲取驗證授權碼的重定向URI。</span><span class="sxs-lookup"><span data-stu-id="c4f94-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="c4f94-195">提供者.符合終結點提供者.驗證客戶端認證授權代碼提供者.接收 Async 提供者.驗證權杖請求提供者.授權代碼提供者.權限點存取權杖提供者.建立 async 刷新權杖提供者.建立async</span><span class="sxs-lookup"><span data-stu-id="c4f94-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="c4f94-196">下面顯示了`AuthorizationCodeProvider.CreateAsync``ReceiveAsync`用於和控制授權代碼的創建和驗證的範例實現。</span><span class="sxs-lookup"><span data-stu-id="c4f94-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="c4f94-197">上述代碼使用記憶體中併發字典來存儲代碼和標識票證,並在收到代碼後還原標識。</span><span class="sxs-lookup"><span data-stu-id="c4f94-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="c4f94-198">在實際應用程式中,它將被持久性數據存儲替換。</span><span class="sxs-lookup"><span data-stu-id="c4f94-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="c4f94-199">授權終結點供資源擁有者授予對用戶端的訪問許可權。</span><span class="sxs-lookup"><span data-stu-id="c4f94-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="c4f94-200">通常,它需要一個使用者介面來允許用戶按下按鈕並確認授予。</span><span class="sxs-lookup"><span data-stu-id="c4f94-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="c4f94-201">OWIN OAuth 中間件允許應用程式代碼處理授權終結點。</span><span class="sxs-lookup"><span data-stu-id="c4f94-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="c4f94-202">在我們的示例應用中,我們使用調用`OAuthController`的MVC控制器來處理它。</span><span class="sxs-lookup"><span data-stu-id="c4f94-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="c4f94-203">下面是實現的範例:</span><span class="sxs-lookup"><span data-stu-id="c4f94-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="c4f94-204">此操作`Authorize`將首先檢查使用者是否登錄到授權伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4f94-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="c4f94-205">如果沒有,身份驗證中間件會向調用方提出使用"應用程式"Cookie 進行身份驗證的挑戰,並重定向到登錄頁。</span><span class="sxs-lookup"><span data-stu-id="c4f94-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="c4f94-206">(請參閱上面突出顯示的代碼。如果使用者已登錄,它將呈現「授權」視圖,如下所示:</span><span class="sxs-lookup"><span data-stu-id="c4f94-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="c4f94-207">如果選擇了 **「授予**」`Authorize`按鈕, 該操作將創建新的「持有者」 識別並登入。</span><span class="sxs-lookup"><span data-stu-id="c4f94-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="c4f94-208">它將觸發授權伺服器以生成無記名令牌,並將其發送回具有 JSON 負載的用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span>

### <a name="implicit-grant"></a><span data-ttu-id="c4f94-209">隱含式</span><span class="sxs-lookup"><span data-stu-id="c4f94-209">Implicit Grant</span></span>

<span data-ttu-id="c4f94-210">立即請參閱 IETF 的 OAuth 2[隱式授予](http://tools.ietf.org/html/rfc6749#section-4.2)部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="c4f94-211">圖 4 所示[的隱式授予](http://tools.ietf.org/html/rfc6749#section-4.2)流是 OWIN OAuth 中間件後面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="c4f94-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="c4f94-212">來自隱式授予部分的流步驟</span><span class="sxs-lookup"><span data-stu-id="c4f94-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="c4f94-213">範例下載以下步驟:</span><span class="sxs-lookup"><span data-stu-id="c4f94-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c4f94-214">(A) 客戶端通過將資源擁有者的使用者代理定向到授權終結點來啟動流。</span><span class="sxs-lookup"><span data-stu-id="c4f94-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="c4f94-215">用戶端包括其客戶端識別碼、請求的範圍、本地狀態和重定向 URI,授權伺服器將在授予(或拒絕)訪問許可權後將使用者代理發送回該 URI。</span><span class="sxs-lookup"><span data-stu-id="c4f94-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="c4f94-216">提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點</span><span class="sxs-lookup"><span data-stu-id="c4f94-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="c4f94-217">(B) 授權伺服器對資源擁有者進行身份驗證(通過使用者代理),並確定資源擁有者是授予還是拒絕用戶端的訪問請求。</span><span class="sxs-lookup"><span data-stu-id="c4f94-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="c4f94-218">**如果使用者授予存取&gt;&lt;權限**提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點授權碼提供者.建立Async</span><span class="sxs-lookup"><span data-stu-id="c4f94-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c4f94-219">(C) 假設資源擁有者授予存取許可權,授權伺服器使用前面提供的重定向 URI(在請求中或用戶端註冊期間)將使用者代理重定向回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="c4f94-220">...</span><span class="sxs-lookup"><span data-stu-id="c4f94-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="c4f94-221">(D) 客戶端通過包含上一步驟中收到的授權代碼,從授權伺服器的權杖終結點請求訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="c4f94-222">發出請求時,用戶端會使用授權伺服器進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c4f94-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="c4f94-223">用戶端包括用於獲取驗證授權碼的重定向URI。</span><span class="sxs-lookup"><span data-stu-id="c4f94-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="c4f94-224">由於我們已經實現了授權代碼授予的授權終結點`OAuthController.Authorize`(操作),因此它會自動啟用隱式流。</span><span class="sxs-lookup"><span data-stu-id="c4f94-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="c4f94-225">注意:`Provider.ValidateClientRedirectUri`用於驗證客戶端 ID 及其重定向 URL,它保護隱式授予流從發送存取權杖到惡意用戶端([中間人攻擊](https://www.owasp.org/index.php/Man-in-the-middle_attack))。</span><span class="sxs-lookup"><span data-stu-id="c4f94-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="c4f94-226">資源擁有者密碼認證</span><span class="sxs-lookup"><span data-stu-id="c4f94-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="c4f94-227">立即請參閱 IETF 的 OAuth 2[資源擁有者密碼認證認證的授予](http://tools.ietf.org/html/rfc6749#section-4.3)部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="c4f94-228">圖 5 所示[的資源擁有者密碼認證授予](http://tools.ietf.org/html/rfc6749#section-4.3)串流是 OWIN OAuth 中間件後面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="c4f94-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="c4f94-229">來自資源擁有者密碼認證的串流步驟</span><span class="sxs-lookup"><span data-stu-id="c4f94-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="c4f94-230">範例下載以下步驟:</span><span class="sxs-lookup"><span data-stu-id="c4f94-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c4f94-231">(A) 資源擁有者向用戶端提供其使用者名和密碼。</span><span class="sxs-lookup"><span data-stu-id="c4f94-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="c4f94-232">(B) 客戶端通過包含從資源擁有者收到的憑據來請求來自授權伺服器令牌終結點的訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="c4f94-233">發出請求時,用戶端會使用授權伺服器進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c4f94-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="c4f94-234">提供者.符合終結點提供者.驗證客戶端身份認證提供者.驗證權杖請求提供者.授權資源擁有者認證提供者.權限點存取權碼提供者.建立同步刷新權碼提供者.建立async</span><span class="sxs-lookup"><span data-stu-id="c4f94-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c4f94-235">(C) 授權伺服器對用戶端進行身份驗證並驗證資源擁有者憑據,如果有效,則頒發訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="c4f94-236">下面是`Provider.GrantResourceOwnerCredentials`以下範例實現:</span><span class="sxs-lookup"><span data-stu-id="c4f94-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="c4f94-237">上面的代碼旨在解釋本教程的這一部分,不應在安全或生產應用中使用。</span><span class="sxs-lookup"><span data-stu-id="c4f94-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="c4f94-238">它不檢查資源擁有者憑據。</span><span class="sxs-lookup"><span data-stu-id="c4f94-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="c4f94-239">它假定每個憑據都有效,併為其創建新標識。</span><span class="sxs-lookup"><span data-stu-id="c4f94-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="c4f94-240">新標識將用於生成訪問權杖和刷新權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="c4f94-241">請將代碼取代為您自己的安全帳戶管理代碼。</span><span class="sxs-lookup"><span data-stu-id="c4f94-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="c4f94-242">用戶端認證</span><span class="sxs-lookup"><span data-stu-id="c4f94-242">Client Credentials Grant</span></span>

<span data-ttu-id="c4f94-243">立即請參閱 IETF 的 OAuth 2[客戶端認證授予](http://tools.ietf.org/html/rfc6749#section-4.4)部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="c4f94-244">圖 6 所示[的用戶端認證授予](http://tools.ietf.org/html/rfc6749#section-4.4)串流是 OWIN OAuth 中間件後面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="c4f94-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="c4f94-245">來自用戶端憑據授予部分的流步驟</span><span class="sxs-lookup"><span data-stu-id="c4f94-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="c4f94-246">範例下載以下步驟:</span><span class="sxs-lookup"><span data-stu-id="c4f94-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c4f94-247">(A) 用戶端使用授權伺服器進行身份驗證,並從權杖終結點請求訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="c4f94-248">提供者.符合終結點提供者.驗證客戶端認證提供者.驗證權杖請求提供者.授權用戶端認證者提供者.權杖終結點存取權碼提供者.建立同步刷新權杖提供者.建立async</span><span class="sxs-lookup"><span data-stu-id="c4f94-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c4f94-249">(B) 授權伺服器對用戶端進行身份驗證,如果有效,則頒發訪問令牌。</span><span class="sxs-lookup"><span data-stu-id="c4f94-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="c4f94-250">下面是`Provider.GrantClientCredentials`以下範例實現:</span><span class="sxs-lookup"><span data-stu-id="c4f94-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="c4f94-251">上面的代碼旨在解釋本教程的這一部分,不應在安全或生產應用中使用。</span><span class="sxs-lookup"><span data-stu-id="c4f94-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="c4f94-252">請將代碼取代為您自己的安全用戶端管理代碼。</span><span class="sxs-lookup"><span data-stu-id="c4f94-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="c4f94-253">重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="c4f94-253">Refresh Token</span></span>

<span data-ttu-id="c4f94-254">立即請參閱 IETF 的 OAuth 2[刷新權杖](http://tools.ietf.org/html/rfc6749#section-1.5)部分。</span><span class="sxs-lookup"><span data-stu-id="c4f94-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="c4f94-255">圖 2 所示的[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)流是 OWIN OAuth 中間件後面的流和映射。</span><span class="sxs-lookup"><span data-stu-id="c4f94-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>

| <span data-ttu-id="c4f94-256">來自用戶端憑據授予部分的流步驟</span><span class="sxs-lookup"><span data-stu-id="c4f94-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="c4f94-257">範例下載以下步驟:</span><span class="sxs-lookup"><span data-stu-id="c4f94-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="c4f94-258">(G) 客戶端透過使用授權伺服器進行身份驗證並呈現刷新權杖來請求新的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="c4f94-259">用戶端身份驗證要求基於用戶端類型和授權伺服器策略。</span><span class="sxs-lookup"><span data-stu-id="c4f94-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="c4f94-260">提供者.符合終結點提供者.驗證客戶端身份驗證刷新權杖提供者.接收async提供者.驗證權杖請求提供者.授予refreshtoken提供者.權杖終結點存取權杖提供者.建立async刷新權杖提供者.創建Async</span><span class="sxs-lookup"><span data-stu-id="c4f94-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="c4f94-261">(H) 授權伺服器對用戶端進行身份驗證並驗證刷新權杖,如果有效,則頒發新的訪問權杖(以及可選為新刷新權杖)。</span><span class="sxs-lookup"><span data-stu-id="c4f94-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="c4f94-262">下面是`Provider.GrantRefreshToken`以下範例實現:</span><span class="sxs-lookup"><span data-stu-id="c4f94-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="c4f94-263">建立權限存取權杖保護的資源伺服器</span><span class="sxs-lookup"><span data-stu-id="c4f94-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="c4f94-264">建立空 Web 應用程式專案並在專案中安裝以下套件:</span><span class="sxs-lookup"><span data-stu-id="c4f94-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="c4f94-265">微軟.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="c4f94-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="c4f94-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="c4f94-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="c4f94-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="c4f94-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="c4f94-268">創建啟動類並配置身份驗證和 Web API。</span><span class="sxs-lookup"><span data-stu-id="c4f94-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="c4f94-269">請參閱*示例下載中的授權伺服器\資源伺服器\啟動.cs。*</span><span class="sxs-lookup"><span data-stu-id="c4f94-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="c4f94-270">請參閱*示例下載中的授權伺服器\\_資源 伺服器\應用啟動\啟動.Auth.cs。*</span><span class="sxs-lookup"><span data-stu-id="c4f94-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="c4f94-271">請參閱*示例下載中的授權伺服器\\_資源 伺服器\應用啟動\啟動.WebApi.cs。*</span><span class="sxs-lookup"><span data-stu-id="c4f94-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="c4f94-272">`UseCors`方法允許所有域的 CORS。</span><span class="sxs-lookup"><span data-stu-id="c4f94-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="c4f94-273">`UseOAuthBearerAuthentication`方法啟用 OAuth 承載權杖身份驗證中間件,它將從請求中的授權標頭接收和驗證無記名令牌。</span><span class="sxs-lookup"><span data-stu-id="c4f94-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="c4f94-274">`Config.SuppressDefaultHostAuthenticaiton`禁止從應用中預設主機經過身份驗證的主體,因此在此調用後所有請求都將是匿名的。</span><span class="sxs-lookup"><span data-stu-id="c4f94-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="c4f94-275">`HostAuthenticationFilter`僅針對指定的身份驗證類型啟用身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c4f94-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="c4f94-276">在這種情況下,它是承載身份驗證類型。</span><span class="sxs-lookup"><span data-stu-id="c4f94-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="c4f94-277">為了示範經過身份驗證的身份,我們創建了一個 ApiController 來輸出當前使用者的聲明。</span><span class="sxs-lookup"><span data-stu-id="c4f94-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="c4f94-278">如果授權伺服器和資源伺服器不在同一台電腦上,OAuth 中間件將使用不同的電腦密鑰來加密和解密承載訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="c4f94-279">為了在兩個項目之間共用相同的私鑰,我們在兩個`machinekey`*Web.config*檔中添加相同的設置。</span><span class="sxs-lookup"><span data-stu-id="c4f94-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="c4f94-280">建立 OAuth 2.0 用戶端</span><span class="sxs-lookup"><span data-stu-id="c4f94-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="c4f94-281">我們使用[DotNetOpenAuth.OAuth2.用戶端](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client)NuGet 包來簡化用戶端代碼。</span><span class="sxs-lookup"><span data-stu-id="c4f94-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="c4f94-282">授權代碼授權</span><span class="sxs-lookup"><span data-stu-id="c4f94-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="c4f94-283">此用戶端是MVC應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4f94-283">This client is an MVC application.</span></span> <span data-ttu-id="c4f94-284">它將觸發授權代碼授予流,以便從後端獲取訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="c4f94-285">它有一個頁面,如下所示:</span><span class="sxs-lookup"><span data-stu-id="c4f94-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="c4f94-286">"**授權"** 按鈕將瀏覽器重定向到授權伺服器,以通知資源擁有者授予對此用戶端的訪問許可權。</span><span class="sxs-lookup"><span data-stu-id="c4f94-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="c4f94-287">「**刷新**」按鈕將使用當前刷新權杖取得新的存取權杖和刷新權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="c4f94-288">**"存取受保護資源 API"** 按鈕將呼叫資源伺服器獲取當前使用者的聲明數據並在頁面上顯示這些資料。</span><span class="sxs-lookup"><span data-stu-id="c4f94-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="c4f94-289">下面是用戶端`HomeController`的範例代碼。</span><span class="sxs-lookup"><span data-stu-id="c4f94-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="c4f94-290">`DotNetOpenAuth`默認情況下需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="c4f94-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="c4f94-291">由於我們的展示使用 HTTP,您需要在設定檔中新增以下設定:</span><span class="sxs-lookup"><span data-stu-id="c4f94-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="c4f94-292">安全性 - 切勿在生產應用中禁用 SSL。</span><span class="sxs-lookup"><span data-stu-id="c4f94-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="c4f94-293">您的登錄憑據現在以明文形式通過網路發送。</span><span class="sxs-lookup"><span data-stu-id="c4f94-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="c4f94-294">上面的代碼僅用於本地示例調試和探索。</span><span class="sxs-lookup"><span data-stu-id="c4f94-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="c4f94-295">隱含控制程式</span><span class="sxs-lookup"><span data-stu-id="c4f94-295">Implicit Grant Client</span></span>

<span data-ttu-id="c4f94-296">此用戶端使用 JavaScript 來:</span><span class="sxs-lookup"><span data-stu-id="c4f94-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="c4f94-297">打開新視窗並重定向到授權伺服器的授權終結點。</span><span class="sxs-lookup"><span data-stu-id="c4f94-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="c4f94-298">當 URL 片段重定向回時,從它獲取訪問權杖。</span><span class="sxs-lookup"><span data-stu-id="c4f94-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="c4f94-299">下圖顯示了此過程:</span><span class="sxs-lookup"><span data-stu-id="c4f94-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="c4f94-300">客戶端應該有兩個頁面:一個用於主頁,另一個用於回調。下面是*在 Index.cshtml*檔中找不到的範例 JavaScript 程式碼:</span><span class="sxs-lookup"><span data-stu-id="c4f94-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="c4f94-301">下面是*SignIn.cshtml*檔中的回檔處理程式碼:</span><span class="sxs-lookup"><span data-stu-id="c4f94-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="c4f94-302">最佳做法是將 JAVAScript 移至外部檔,而不是將其嵌入 Razor 標記中。</span><span class="sxs-lookup"><span data-stu-id="c4f94-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="c4f94-303">為了保持此示例的簡單性,它們已被合併。</span><span class="sxs-lookup"><span data-stu-id="c4f94-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="c4f94-304">資源擁有者密碼認證認證的分享客戶端</span><span class="sxs-lookup"><span data-stu-id="c4f94-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="c4f94-305">我們使用主控台應用程式來展示此用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4f94-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="c4f94-306">程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="c4f94-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="c4f94-307">用戶端認證的客戶端</span><span class="sxs-lookup"><span data-stu-id="c4f94-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="c4f94-308">與資源擁有者密碼認證給類似,下面是主控台應用程式碼:</span><span class="sxs-lookup"><span data-stu-id="c4f94-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
