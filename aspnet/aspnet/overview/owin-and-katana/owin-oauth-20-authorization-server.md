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
<a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 授權伺服器
====================
由[孫洪業](https://github.com/hongyes)和[普拉布拉傑·蒂加拉詹](https://github.com/Praburaj)

> 本教學將指導您如何使用 OWIN OAuth 中間件實現 OAuth 2.0 授權伺服器。 這是一個高級教程,僅概述創建 OWIN OAuth 2.0 授權伺服器的步驟。 這不是一步一步的教程。 [下載範例代碼](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)。
>
> > [!NOTE]
> > 此大綱不應用於創建安全生產應用。 本教學旨在僅提供如何使用 OWIN OAuth 中間件實現 OAuth 2.0 授權伺服器的大綱。
>
>
> ## <a name="software-versions"></a>軟體版本
>
> | **在教學中顯示** | **也適用於** |
> | --- | --- |
> | Windows 8.1 | 視窗 8, 視窗 7 |
> | [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) | [視覺工作室 2013 快遞為桌面](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express). 帶有最新更新的 Visual Studio 2012 應該可以正常工作,但本教程尚未使用它進行測試,並且某些功能表選擇和對話方塊是不同的。 |
> | .NET 4.5 |  |
>
> ## <a name="questions-and-comments"></a>問題和評論
>
> 如果您有與本教程沒有直接關係的問題,您可以在[GitHub 上的 Katana 專案](https://github.com/aspnet/AspNetKatana/)上發佈這些問題。 有關教程本身的問題和註釋,請參閱頁面底部的註釋部分。


[OAuth 2.0 框架](http://tools.ietf.org/html/rfc6749)使第三方應用能夠獲得對 HTTP 服務的有限存取許可權。 用戶端不需要使用資源擁有者的憑據來訪問受保護的資源,而是獲取訪問權杖(這是表示特定作用域、存留期和其他訪問屬性的字串)。 訪問權杖由授權伺服器在資源擁有者批准下頒發給第三方用戶端。

本教學將介紹:

- 如何建立授權伺服器以支援四種授權的類別和刷新權杖:
    - 授權代碼授予
    - 隱含式
    - 資源擁有者密碼認證
    - 用戶端認證
- 建立受訪問權杖保護的資源伺服器。
- 創建 OAuth 2.0 用戶端。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>必要條件

- [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions)或免費[的 Visual Studio Express 2013,](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)如頁面頂部**的軟體版本**所示。
- 熟悉 OWIN。 請參閱[開始與卡塔納項目和](https://msdn.microsoft.com/magazine/dn451439.aspx)[什麼在OWIN和卡塔納的新增功能](index.md)。
- 熟悉[OAuth](http://tools.ietf.org/html/rfc6749)的術語,包括[角色](http://tools.ietf.org/html/rfc6749#section-1.1)、[協定流程](http://tools.ietf.org/html/rfc6749#section-1.2)與[授權的授予](http://tools.ietf.org/html/rfc6749#section-1.3)。 [OAuth 2.0 介紹](http://tools.ietf.org/html/rfc6749#section-1)提供了很好的介紹。

## <a name="create-an-authorization-server"></a>建立授權伺服器

在本教學中,我們將大致勾勒出如何使用[OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx)和 ASP.NET MVC 創建授權伺服器。 我們希望很快為已完成的示例提供下載,因為本教程不包括每個步驟。 首先,建立名為 *「授權伺服器」* 的空 Web 應用程式並安裝以下程式套件:

- 微軟.阿斯普內.Mvc
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth
- Microsoft.Owin.Security.Cookies
- 微軟.Owin.Security.Google(或任何其他社交登錄包,如微軟.Owin.Security.Facebook)

在名為 *「啟動」* 的項目根資料夾下新增[OWIN 啟動類別](owin-startup-class-detection.md)。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

建立 *"\_應用 開始'* 資料夾。 選擇 *「\_應用程式啟動」* 資料夾並使用 Shift_Alt_A 添加 *「\_授權伺服器」[應用啟動]啟動.Auth.cs*檔的下載版本。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

上述代碼支援應用程式/外部登錄 Cookie 和 Google 身份驗證,授權伺服器本身使用它們來管理帳戶。

擴展`UseOAuthAuthorizationServer`方法是設置授權伺服器。 設定選項包括:

- `AuthorizeEndpointPath`:客戶端應用程式將重定向使用者代理以獲得使用者同意發出權杖或代碼的請求路徑。 它必須以前導斜杠開頭,例如,""。`/Authorize`
- `TokenEndpointPath`:請求路徑用戶端應用程式直接通信以獲取訪問權杖。 它必須以前導斜杠開頭,如"/令牌"。 如果用戶端被頒發[\_客戶端密鑰](http://tools.ietf.org/html/rfc6749#appendix-A.2),則必須將其提供給此終結點。
- `ApplicationCanDisplayErrors`:設定為`true`如果 Web 應用程式想要為`/Authorize`終結點上的 客戶端驗證錯誤生成自訂錯誤頁。 只當瀏覽器未重定向回用戶端應用程式(例如,`client_id`當`redirect_uri`或不正確時),才需要這樣做。 終結點`/Authorize`應期望看到"auth"。錯誤","哦。錯誤描述"和"錯誤描述"ErrorUri"屬性將添加到 OWIN 環境中。

    > [!NOTE]
    > 如果為 true,授權伺服器將返回包含錯誤詳細資訊的預設錯誤頁。
- `AllowInsecureHttp`:如果為 True,允許授權和權杖請求到達 HTTP URI`redirect_uri`位址,並允許 傳入授權請求參數具有 HTTP URI 位址。

    > [!WARNING]
    > 安全性 - 這僅用於開發。
- `Provider`:應用程式為處理授權伺服器中間件引發的事件而提供的物件。 應用程式可以完全實現介面,也可以創建此伺服器支援的 OAuth`OAuthAuthorizationServerProvider`流所需的實例和分配委託。
- `AuthorizationCodeProvider`:生成一次性授權代碼以返回到用戶端應用程式。 為了保護 OAuth 伺服器的安全,應用程式**必須**提供一個`AuthorizationCodeProvider`實體`OnCreate/OnCreateAsync`,其中事件產生的權杖僅對一次呼`OnReceive/OnReceiveAsync`叫有效 。
- `RefreshTokenProvider`:生成刷新權杖,可在需要時用於生成新的訪問權杖。 如果未提供授權伺服器將不會從`/Token`終結點返回刷新權杖。

## <a name="account-management"></a>帳戶管理

OAuth 不關心您管理使用者帳戶資訊的位置或方式。 負責它的[ASP.NET 身份](../../../identity/index.md)。 在本教學中,我們將簡化帳戶管理代碼,並確保使用者可以使用 OWIN Cookie 中間件登錄。 下面是 :`AccountController`的 簡化範例碼:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

`ValidateClientRedirectUri`用於驗證用戶端及其註冊的重定向 URL。 `ValidateClientAuthentication`檢查基本方案標頭和窗體正文以獲取客戶端的認證。

登入頁面如下所示:

![](owin-oauth-20-authorization-server/_static/image1.png)

立即查看 IETF 的 OAuth 2[授權代碼授予](http://tools.ietf.org/html/rfc6749#section-4.1)部分。

**提供者**(下表中)是[OAuth 授權伺服器選項](https://msdn.microsoft.com/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)。提供程式,其類型`OAuthAuthorizationServerProvider`為 ,它包含所有 OAuth 伺服器事件。

| 授權代碼授予部分的流步驟 | 範例下載以下步驟: |
| --- | --- |
|  |  |
| (A) 客戶端通過將資源擁有者的使用者代理定向到授權終結點來啟動流。 用戶端包括其客戶端識別碼、請求的範圍、本地狀態和重定向 URI,授權伺服器將在授予(或拒絕)訪問許可權後將使用者代理發送回該 URI。 | 提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點 |
|  |  |
| (B) 授權伺服器對資源擁有者進行身份驗證(通過使用者代理),並確定資源擁有者是授予還是拒絕用戶端的訪問請求。 | **如果使用者授予存取&gt;&lt;權限**提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點授權碼提供者.建立Async |
|  |  |
| (C) 假設資源擁有者授予存取許可權,授權伺服器使用前面提供的重定向 URI(在請求中或用戶端註冊期間)將使用者代理重定向回用戶端。 ... |  |
|  |  |
| (D) 客戶端通過包含上一步驟中收到的授權代碼,從授權伺服器的權杖終結點請求訪問權杖。 發出請求時,用戶端會使用授權伺服器進行身份驗證。 用戶端包括用於獲取驗證授權碼的重定向URI。 | 提供者.符合終結點提供者.驗證客戶端認證授權代碼提供者.接收 Async 提供者.驗證權杖請求提供者.授權代碼提供者.權限點存取權杖提供者.建立 async 刷新權杖提供者.建立async |

下面顯示了`AuthorizationCodeProvider.CreateAsync``ReceiveAsync`用於和控制授權代碼的創建和驗證的範例實現。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

上述代碼使用記憶體中併發字典來存儲代碼和標識票證,並在收到代碼後還原標識。 在實際應用程式中,它將被持久性數據存儲替換。 授權終結點供資源擁有者授予對用戶端的訪問許可權。 通常,它需要一個使用者介面來允許用戶按下按鈕並確認授予。 OWIN OAuth 中間件允許應用程式代碼處理授權終結點。 在我們的示例應用中,我們使用調用`OAuthController`的MVC控制器來處理它。 下面是實現的範例:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

此操作`Authorize`將首先檢查使用者是否登錄到授權伺服器。 如果沒有,身份驗證中間件會向調用方提出使用"應用程式"Cookie 進行身份驗證的挑戰,並重定向到登錄頁。 (請參閱上面突出顯示的代碼。如果使用者已登錄,它將呈現「授權」視圖,如下所示:

![](owin-oauth-20-authorization-server/_static/image2.png)

如果選擇了 **「授予**」`Authorize`按鈕, 該操作將創建新的「持有者」 識別並登入。 它將觸發授權伺服器以生成無記名令牌,並將其發送回具有 JSON 負載的用戶端。

### <a name="implicit-grant"></a>隱含式

立即請參閱 IETF 的 OAuth 2[隱式授予](http://tools.ietf.org/html/rfc6749#section-4.2)部分。

 圖 4 所示[的隱式授予](http://tools.ietf.org/html/rfc6749#section-4.2)流是 OWIN OAuth 中間件後面的流和映射。

| 來自隱式授予部分的流步驟 | 範例下載以下步驟: |
| --- | --- |
|  |  |
| (A) 客戶端通過將資源擁有者的使用者代理定向到授權終結點來啟動流。 用戶端包括其客戶端識別碼、請求的範圍、本地狀態和重定向 URI,授權伺服器將在授予(或拒絕)訪問許可權後將使用者代理發送回該 URI。 | 提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點 |
|  |  |
| (B) 授權伺服器對資源擁有者進行身份驗證(通過使用者代理),並確定資源擁有者是授予還是拒絕用戶端的訪問請求。 | **如果使用者授予存取&gt;&lt;權限**提供者.符合終結點提供者.驗證客戶端重定提供者.驗證授權請求提供者.授權終結點授權碼提供者.建立Async |
|  |  |
| (C) 假設資源擁有者授予存取許可權,授權伺服器使用前面提供的重定向 URI(在請求中或用戶端註冊期間)將使用者代理重定向回用戶端。 ... |  |
|  |  |
| (D) 客戶端通過包含上一步驟中收到的授權代碼,從授權伺服器的權杖終結點請求訪問權杖。 發出請求時,用戶端會使用授權伺服器進行身份驗證。 用戶端包括用於獲取驗證授權碼的重定向URI。 |  |

由於我們已經實現了授權代碼授予的授權終結點`OAuthController.Authorize`(操作),因此它會自動啟用隱式流。 注意:`Provider.ValidateClientRedirectUri`用於驗證客戶端 ID 及其重定向 URL,它保護隱式授予流從發送存取權杖到惡意用戶端([中間人攻擊](https://www.owasp.org/index.php/Man-in-the-middle_attack))。

### <a name="resource-owner-password-credentials-grant"></a>資源擁有者密碼認證

立即請參閱 IETF 的 OAuth 2[資源擁有者密碼認證認證的授予](http://tools.ietf.org/html/rfc6749#section-4.3)部分。

 圖 5 所示[的資源擁有者密碼認證授予](http://tools.ietf.org/html/rfc6749#section-4.3)串流是 OWIN OAuth 中間件後面的流和映射。

| 來自資源擁有者密碼認證的串流步驟 | 範例下載以下步驟: |
| --- | --- |
|  |  |
| (A) 資源擁有者向用戶端提供其使用者名和密碼。 |  |
|  |  |
| (B) 客戶端通過包含從資源擁有者收到的憑據來請求來自授權伺服器令牌終結點的訪問權杖。 發出請求時,用戶端會使用授權伺服器進行身份驗證。 | 提供者.符合終結點提供者.驗證客戶端身份認證提供者.驗證權杖請求提供者.授權資源擁有者認證提供者.權限點存取權碼提供者.建立同步刷新權碼提供者.建立async |
|  |  |
| (C) 授權伺服器對用戶端進行身份驗證並驗證資源擁有者憑據,如果有效,則頒發訪問權杖。 |  |

下面是`Provider.GrantResourceOwnerCredentials`以下範例實現:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> 上面的代碼旨在解釋本教程的這一部分,不應在安全或生產應用中使用。 它不檢查資源擁有者憑據。 它假定每個憑據都有效,併為其創建新標識。 新標識將用於生成訪問權杖和刷新權杖。 請將代碼取代為您自己的安全帳戶管理代碼。


### <a name="client-credentials-grant"></a>用戶端認證

立即請參閱 IETF 的 OAuth 2[客戶端認證授予](http://tools.ietf.org/html/rfc6749#section-4.4)部分。

 圖 6 所示[的用戶端認證授予](http://tools.ietf.org/html/rfc6749#section-4.4)串流是 OWIN OAuth 中間件後面的流和映射。

| 來自用戶端憑據授予部分的流步驟 | 範例下載以下步驟: |
| --- | --- |
|  |  |
| (A) 用戶端使用授權伺服器進行身份驗證,並從權杖終結點請求訪問權杖。 | 提供者.符合終結點提供者.驗證客戶端認證提供者.驗證權杖請求提供者.授權用戶端認證者提供者.權杖終結點存取權碼提供者.建立同步刷新權杖提供者.建立async |
|  |  |
| (B) 授權伺服器對用戶端進行身份驗證,如果有效,則頒發訪問令牌。 |  |

下面是`Provider.GrantClientCredentials`以下範例實現:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> 上面的代碼旨在解釋本教程的這一部分,不應在安全或生產應用中使用。 請將代碼取代為您自己的安全用戶端管理代碼。


### <a name="refresh-token"></a>重新整理權杖

立即請參閱 IETF 的 OAuth 2[刷新權杖](http://tools.ietf.org/html/rfc6749#section-1.5)部分。

 圖 2 所示的[刷新令牌](http://tools.ietf.org/html/rfc6749#section-1.5)流是 OWIN OAuth 中間件後面的流和映射。

| 來自用戶端憑據授予部分的流步驟 | 範例下載以下步驟: |
| --- | --- |
|  |  |
| (G) 客戶端透過使用授權伺服器進行身份驗證並呈現刷新權杖來請求新的存取權杖。 用戶端身份驗證要求基於用戶端類型和授權伺服器策略。 | 提供者.符合終結點提供者.驗證客戶端身份驗證刷新權杖提供者.接收async提供者.驗證權杖請求提供者.授予refreshtoken提供者.權杖終結點存取權杖提供者.建立async刷新權杖提供者.創建Async |
|  |  |
| (H) 授權伺服器對用戶端進行身份驗證並驗證刷新權杖,如果有效,則頒發新的訪問權杖(以及可選為新刷新權杖)。 |  |

下面是`Provider.GrantRefreshToken`以下範例實現:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a>建立權限存取權杖保護的資源伺服器

建立空 Web 應用程式專案並在專案中安裝以下套件:

- 微軟.AspNet.WebApi.Owin
- Microsoft.Owin.Host.SystemWeb
- Microsoft.Owin.Security.OAuth

創建啟動類並配置身份驗證和 Web API。 請參閱*示例下載中的授權伺服器\資源伺服器\啟動.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

請參閱*示例下載中的授權伺服器\\_資源 伺服器\應用啟動\啟動.Auth.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

請參閱*示例下載中的授權伺服器\\_資源 伺服器\應用啟動\啟動.WebApi.cs。*

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- `UseCors`方法允許所有域的 CORS。
- `UseOAuthBearerAuthentication`方法啟用 OAuth 承載權杖身份驗證中間件,它將從請求中的授權標頭接收和驗證無記名令牌。
- `Config.SuppressDefaultHostAuthenticaiton`禁止從應用中預設主機經過身份驗證的主體,因此在此調用後所有請求都將是匿名的。
- `HostAuthenticationFilter`僅針對指定的身份驗證類型啟用身份驗證。 在這種情況下,它是承載身份驗證類型。

為了示範經過身份驗證的身份,我們創建了一個 ApiController 來輸出當前使用者的聲明。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

如果授權伺服器和資源伺服器不在同一台電腦上,OAuth 中間件將使用不同的電腦密鑰來加密和解密承載訪問權杖。 為了在兩個項目之間共用相同的私鑰,我們在兩個`machinekey`*Web.config*檔中添加相同的設置。

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a>建立 OAuth 2.0 用戶端

 我們使用[DotNetOpenAuth.OAuth2.用戶端](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client)NuGet 包來簡化用戶端代碼。

### <a name="authorization-code-grant-client"></a>授權代碼授權

 此用戶端是MVC應用程式。 它將觸發授權代碼授予流,以便從後端獲取訪問權杖。 它有一個頁面,如下所示:

![](owin-oauth-20-authorization-server/_static/image3.png)

- "**授權"** 按鈕將瀏覽器重定向到授權伺服器,以通知資源擁有者授予對此用戶端的訪問許可權。
- 「**刷新**」按鈕將使用當前刷新權杖取得新的存取權杖和刷新權杖。
- **"存取受保護資源 API"** 按鈕將呼叫資源伺服器獲取當前使用者的聲明數據並在頁面上顯示這些資料。

下面是用戶端`HomeController`的範例代碼。

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

`DotNetOpenAuth`默認情況下需要 SSL。 由於我們的展示使用 HTTP,您需要在設定檔中新增以下設定:

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> 安全性 - 切勿在生產應用中禁用 SSL。 您的登錄憑據現在以明文形式通過網路發送。 上面的代碼僅用於本地示例調試和探索。


### <a name="implicit-grant-client"></a>隱含控制程式

此用戶端使用 JavaScript 來:

1. 打開新視窗並重定向到授權伺服器的授權終結點。
2. 當 URL 片段重定向回時,從它獲取訪問權杖。

下圖顯示了此過程:

![](owin-oauth-20-authorization-server/_static/image4.png)

客戶端應該有兩個頁面:一個用於主頁,另一個用於回調。下面是*在 Index.cshtml*檔中找不到的範例 JavaScript 程式碼:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

下面是*SignIn.cshtml*檔中的回檔處理程式碼:

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> 最佳做法是將 JAVAScript 移至外部檔,而不是將其嵌入 Razor 標記中。 為了保持此示例的簡單性,它們已被合併。


### <a name="resource-owner-password-credentials-grant-client"></a>資源擁有者密碼認證認證的分享客戶端

我們使用主控台應用程式來展示此用戶端。 程式碼如下：

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a>用戶端認證的客戶端

與資源擁有者密碼認證給類似,下面是主控台應用程式碼:

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]
