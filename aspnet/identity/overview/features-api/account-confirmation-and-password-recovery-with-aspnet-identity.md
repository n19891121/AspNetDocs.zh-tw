---
uid: identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
title: '帳戶確認 & 密碼復原-ASP.NET Identity (c # ) -ASP.NET 4。x'
author: HaoK
description: 在進行本教學課程之前，您應該先完成以登入、電子郵件確認和密碼重設建立安全 ASP.NET MVC 5 web 應用程式。 本教學課程 .。。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 8d54180d-f826-4df7-b503-7debf5ed9fb3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: e27d9180bf8da3572b48cb342be4e703f093d45a
ms.sourcegitcommit: 6727454a30f11ac2365e1cc8a37ef0005f5d15b3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/09/2020
ms.locfileid: "96934106"
---
# <a name="account-confirmation-and-password-recovery-with-aspnet-identity-c"></a>使用 ASP.NET Identity (c # ) 的帳戶確認和密碼復原

> 在進行本教學課程之前，您應該先完成 [以登入、電子郵件確認和密碼重設建立安全 ASP.NET MVC 5 web 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。 本教學課程包含更多詳細資料，並會示範如何設定電子郵件以進行本機帳戶確認，並允許使用者在 ASP.NET Identity 中重設其忘記的密碼。

本機使用者帳戶會要求使用者建立帳戶的密碼，而該密碼會在 web 應用程式中安全地) 儲存 (。 ASP.NET Identity 也支援社交帳戶，而不需要使用者建立應用程式的密碼。 [社交帳戶](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 使用協力廠商 (，例如 Google、Twitter、Facebook 或 Microsoft) 來驗證使用者。 本主題包含下列項目：

- [建立 ASP.NET MVC 應用程式](#createMvc) ，並探索 ASP.NET Identity 功能。
- [建立身分識別範例](#build)
- [設定電子郵件確認](#email)

新使用者會註冊其電子郵件別名，以建立本機帳戶。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image1.png)

選取 [註冊] 按鈕會將包含驗證權杖的確認電子郵件傳送到其電子郵件地址。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image2.png)

系統會傳送電子郵件給使用者，其中包含其帳戶的確認權杖。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image3.png)

選取連結會確認帳戶。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image4.png)

<a id="passwordReset"></a>

## <a name="password-recoveryreset"></a>密碼復原/重設

忘記密碼的本機使用者可以將安全性權杖傳送到其電子郵件帳戶，讓他們重設密碼。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image5.png)  
  
使用者很快就會收到一封包含連結的電子郵件，讓他們可以重設其密碼。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image6.png)  
選取此連結將會帶至 [重設] 頁面。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image7.png)  
  
選取 [ **重設** ] 按鈕將會確認密碼已重設。  
  
![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image8.png)

<a id="createMvc"></a>

## <a name="create-an-aspnet-web-app"></a>建立 ASP.NET Web 應用程式

從安裝和執行 [Visual Studio 2017](https://visualstudio.microsoft.com/)開始。

1. 建立新的 ASP.NET Web 專案，然後選取 MVC 範本。 Web Form 也支援 ASP.NET Identity，因此您可以在 web Forms 應用程式中遵循類似的步驟。
2. 將驗證變更為 **個別的使用者帳戶**。
3. 執行應用程式，選取 [ **註冊** ] 連結並註冊使用者。 此時，電子郵件上的唯一驗證是使用 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 屬性。
4. 在伺服器總管中，流覽至 [ **資料 Connections\DefaultConnection\Tables\AspNetUsers**]，按一下滑鼠右鍵，然後選取 [ **開啟資料表定義**]。

    下圖顯示 `AspNetUsers` 架構：

    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image9.png)
5. 以滑鼠右鍵按一下 [ **AspNetUsers** ] 資料表，然後選取 [ **顯示資料表資料**]。  
  
    ![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image10.png)  
  
   此時尚未確認電子郵件。

ASP.NET Identity 的預設資料存放區是 Entity Framework 的，但您可以將它設定為使用其他資料存放區，並新增其他欄位。 請參閱本教學課程結尾的 [其他資源](#addRes) 一節。

當應用程式啟動並叫用應用程式 Start\Startup.Auth.cs 中的方法時，會呼叫 [OWIN startup 類別](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) ( Startup.cs ) `ConfigureAuth` ，其會設定 OWIN 管線並初始化 ASP.NET Identity。 *\_* 檢查 `ConfigureAuth` 方法。 每個 `CreatePerOwinContext` 呼叫都會註冊一個回呼 (儲存在 `OwinContext`) 中，每個要求會呼叫一次，以建立所指定類型的實例。 您可以在每個型別 () 的函式和方法中設定中斷點， `Create` `ApplicationDbContext, ApplicationUserManager` 並確認每個要求都會呼叫它們。 和的實例 `ApplicationDbContext` `ApplicationUserManager` 儲存在 OWIN 內容中，可以在整個應用程式中存取。 ASP.NET Identity 透過 cookie 中介軟體連結至 OWIN 管線。 如需詳細資訊，請參閱 [ASP.NET Identity 中的針對 UserManager 類別的每個要求存留期管理](https://blogs.msdn.com/b/webdev/archive/2014/02/12/per-request-lifetime-management-for-usermanager-class-in-asp-net-identity.aspx)。

當您變更安全性設定檔時，會產生新的安全性戳記，並儲存在 `SecurityStamp` *AspNetUsers* 資料表的欄位中。 請注意，此 `SecurityStamp` 欄位與安全性 cookie 不同。 安全性 cookie 不會儲存在 `AspNetUsers` 資料表 (或身分識別 DB) 的其他位置。 安全性 cookie 權杖會使用 [DPAPI](https://msdn.microsoft.com/library/system.security.cryptography.protecteddata.aspx) 自我簽署，並且會使用 `UserId, SecurityStamp` 和到期時間資訊建立。

Cookie 中介軟體會檢查每個要求上的 cookie。 `SecurityStampValidator`類別中的方法會 `Startup` 叫用 DB，並定期檢查安全性戳記，如所指定 `validateInterval` 。 除非您變更安全性設定檔，否則每隔30分鐘就會在我們的範例) 中 (。 選擇30分鐘的間隔，以將資料庫的行程降至最低。 如需詳細資訊，請參閱我的 [雙因素驗證教學](index.md) 課程。

根據程式碼中的批註， `UseCookieAuthentication` 方法支援 cookie 驗證。 `SecurityStamp`欄位和相關聯的程式碼為您的應用程式提供額外的安全性層級。當您變更密碼時，將會登出您用來登入的瀏覽器。 `SecurityStampValidator.OnValidateIdentity`方法可讓應用程式在使用者登入時驗證安全性權杖，而當您變更密碼或使用外部登入時，就會使用此權杖。 這是為了確保使用舊密碼所產生)  (cookie 的任何權杖都會失效。 在範例專案中，如果您變更使用者的密碼，則會為使用者產生新的權杖，任何先前的權杖都會失效，並 `SecurityStamp` 更新欄位。

身分識別系統可讓您設定應用程式，以在使用者的安全性設定檔變更時 (例如，當使用者變更其密碼或變更相關登入 (（例如從 Facebook、Google、) Microsoft 帳戶等）時，使用者會登出所有瀏覽器實例。 例如，下圖顯示 [單一 signout 範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample) 應用程式，此應用程式可讓使用者登出 (在此案例中的所有瀏覽器實例，例如 IE、Firefox 和 Chrome) ，方法是選取一個按鈕。 此外，此範例可讓您只登出特定的瀏覽器實例。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image11.png)

[單一 signout 範例](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SingleSignOutSample)應用程式會顯示 ASP.NET Identity 如何讓您重新產生安全性權杖。 這是為了確保使用舊密碼所產生)  (cookie 的任何權杖都會失效。 這項功能可為您的應用程式提供額外的安全性層級;當您變更密碼時，將會登出您登入此應用程式的位置。

*應用程式 \_ Start\IdentityConfig.cs* 檔包含 `ApplicationUserManager` 、 `EmailService` 和 `SmsService` 類別。 `EmailService`和 `SmsService` 類別都會執行 `IIdentityMessageService` 介面，因此您在每個類別中都有共同的方法可設定電子郵件和 SMS。 雖然本教學課程僅說明如何透過 [SendGrid](http://sendgrid.com/)新增電子郵件通知，但您可以使用 SMTP 和其他機制傳送電子郵件。

此 `Startup` 類別也包含將社交登入新增 (Facebook、twitter 等 ) 的定案面板。如需詳細資訊，請參閱 [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的教學課程 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 。

檢查 `ApplicationUserManager` 包含使用者身分識別資訊的類別，並設定下列功能：

- 密碼強度需求。
- 使用者鎖定 (的嘗試和時間) 。
- 雙因素驗證 (2FA) 。 在另一個教學課程中，我將討論2FA 和 SMS。
- 連結電子郵件和 SMS 服務。  (我會在另一個教學課程中討論 SMS) 。

`ApplicationUserManager`類別衍生自泛型 `UserManager<ApplicationUser>` 類別。 `ApplicationUser` 衍生自 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser.aspx)。 `IdentityUser` 衍生自泛型 `IdentityUser` 類別：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample1.cs)]

上述屬性與資料表中的屬性一致 `AspNetUsers` ，如上所示。

上的泛型引數可 `IUser` 讓您使用不同的主要索引鍵類型來衍生類別。 請參閱 [ChangePK](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) 範例，其中顯示如何將主鍵從字串變更為 INT 或 GUID。

### <a name="applicationuser"></a>>applicationuser

`ApplicationUser` (`public class ApplicationUserManager : UserManager<ApplicationUser>`) 在 *Models\IdentityModels.cs* 中定義為：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample2.cs?highlight=8-9)]

上述反白顯示的程式碼會產生 [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)。 ASP.NET Identity 和 OWIN Cookie 驗證是以宣告為基礎，因此架構會要求應用程式為 `ClaimsIdentity` 使用者產生。 `ClaimsIdentity` 具有使用者所有宣告的相關資訊，例如使用者的名稱、年齡以及使用者所屬的角色。 您也可以在這個階段為使用者新增更多宣告。

OWIN `AuthenticationManager.SignIn` 方法會傳入 `ClaimsIdentity` 並登入使用者：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample3.cs?highlight=4-6)]

[使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 會顯示如何將其他屬性新增至 `ApplicationUser` 類別。

## <a name="email-confirmation"></a>電子郵件確認

最好是確認新使用者註冊的電子郵件，以確認他們不會模擬他人 (也就是尚未向他人的電子郵件) 註冊。 假設您有一個討論論壇，您想要防止 `"bob@example.com"` 註冊為 `"joe@contoso.com"` 。 若未確認電子郵件， `"joe@contoso.com"` 可能會從您的應用程式取得不需要的電子郵件。 假設 Bob 不慎註冊為 `"bib@example.com"` 但未注意到，因為應用程式沒有正確的電子郵件，所以無法使用密碼復原。 電子郵件確認只會提供 bot 的有限保護，並且不會提供保護，讓他們有許多可以用來註冊的工作電子郵件別名。在下列範例中，使用者將無法變更其帳戶，直到他們在其註冊的電子郵件帳戶上所收到的確認連結被確認 (為止。 ) 您可以將此工作流程套用至其他案例，例如傳送連結以確認及重設系統管理員所建立之新帳戶的密碼，並在使用者變更其設定檔時傳送電子郵件給使用者。 您通常會想要防止新使用者在電子郵件、SMS 文字訊息或其他機制確認之前，將任何資料張貼到您的網站。 <a id="build"></a>

## <a name="build-a-more-complete-sample"></a>建立更完整的範例

在本節中，您將使用 NuGet 來下載我們將使用的更完整範例。

1. 建立新的 ***empty** _ ASP.NET Web 專案。
2. 在封裝管理員主控台中，輸入下列命令： 

    [!code-console[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample4.cmd)]

   在本教學課程中，我們將使用 [SendGrid](http://sendgrid.com/) 來傳送電子郵件。 `Identity.Samples`封裝會安裝我們將使用的程式碼。
3. 將 [專案設定為使用 SSL](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。
4. 藉由執行應用程式、選取 _ *註冊** 連結，以及張貼註冊表單，來測試本機帳戶的建立。
5. 選取 [示範電子郵件] 連結，以模擬電子郵件確認。
6. 從範例 (帳戶控制器中的程式碼移除示範電子郵件連結確認碼 `ViewBag.Link` 。 ) ，請參閱 `DisplayEmail` 和 `ForgotPasswordConfirmation` 動作方法和 razor views。

> [!WARNING]
> 如果您變更此範例中的任何安全性設定，生產應用程式將需要進行安全性審核，以明確地呼叫所做的變更。

## <a name="examine-the-code-in-app_startidentityconfigcs"></a>檢查應用程式 Start\IdentityConfig.cs 中的程式碼 \_

此範例會示範如何建立帳戶，並將它新增至系統 *管理員* 角色。 您應該將範例中的電子郵件取代為系統管理員帳戶所使用的電子郵件。 立即建立系統管理員帳戶的最簡單方式是在方法中以程式設計方式進行 `Seed` 。 我們希望未來有一項工具可讓您建立和管理使用者和角色。 範例程式碼可讓您建立和管理使用者和角色，但您必須先擁有系統管理員帳戶，才能執行 [角色] 和 [使用者管理] 頁面。 在此範例中，系統會在植入資料庫時建立系統管理員帳戶。

變更密碼，並將名稱變更為您可以接收電子郵件通知的帳戶。

> [!WARNING]
> 安全性-永不將機密資料儲存在您的原始程式碼中。

如先前所述， `app.CreatePerOwinContext` startup 類別中的呼叫會將回呼新增至 `Create` 應用程式 DB 內容、使用者管理員和角色管理員類別的方法。 OWIN 管線會 `Create` 針對每個要求在這些類別上呼叫方法，並儲存每個類別的內容。 帳戶控制器會從包含 OWIN 內容) 的 HTTP 內容中公開使用者管理員 (：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample5.cs)]

當使用者註冊本機帳戶時， `HTTP Post Register` 會呼叫方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample6.cs)]

上述程式碼使用模型資料，透過輸入的電子郵件和密碼來建立新的使用者帳戶。 如果電子郵件別名位於資料存放區中，帳戶建立會失敗，並再次顯示表單。 `GenerateEmailConfirmationTokenAsync`方法會建立安全的確認權杖，並將它儲存在 ASP.NET Identity 資料存放區中。 [Url。動作](https://msdn.microsoft.com/library/dd505232(v=vs.118).aspx)方法會建立包含 `UserId` 和確認權杖的連結。 然後，此連結會透過電子郵件傳送給使用者，使用者可以在其電子郵件應用程式中選取該連結，以確認其帳戶。

<a id="email"></a>

## <a name="set-up-email-confirmation"></a>設定電子郵件確認

移至 SendGrid 註冊頁面，並註冊免費帳戶。 加入類似下列的程式碼來設定 SendGrid：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample7.cs?highlight=5)]

> [!NOTE]
> 電子郵件客戶通常只接受文字訊息 (沒有 HTML) 。 您應提供文字和 HTML 格式的訊息。 在上述的 SendGrid 範例中，這是利用上述的和程式碼來完成 `myMessage.Text` `myMessage.Html` 。

下列程式碼顯示如何使用 [send-mailmessage](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) 類別傳送電子郵件，其中 `message.Body` 只會傳回連結。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample8.cs)]

> [!WARNING]
> 安全性-永不將機密資料儲存在您的原始程式碼中。 帳戶和認證會儲存在 appSetting 中。 在 Azure 上，您可以將這些值安全地儲存在 Azure 入口網站的 [ **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** ] 索引標籤上。 請參閱 [將密碼和其他機密資料部署至 ASP.NET 和 Azure 的最佳做法](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。

輸入您的 SendGrid 認證、執行應用程式、使用電子郵件別名註冊可以選取電子郵件中的 [確認] 連結。 若要瞭解如何使用您的 [Outlook.com](http://outlook.com) 電子郵件帳戶執行此作業，請參閱 John Atten 的 [c # smtp CONFIGURATION For Outlook.Com SMTP 主機](http://typecastexception.com/post/2013/12/20/C-SMTP-Configuration-for-OutlookCom-SMTP-Host.aspx) 和他的[ASP.NET Identity 2.0：設定帳戶驗證和 Two-Factor 授權](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) 文章。

當使用者選取 [ **註冊** ] 按鈕時，會將包含驗證權杖的確認電子郵件傳送到其電子郵件地址。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image12.png)

系統會傳送電子郵件給使用者，其中包含其帳戶的確認權杖。

![](account-confirmation-and-password-recovery-with-aspnet-identity/_static/image13.png)

## <a name="examine-the-code"></a>檢查程式碼

下列程式碼顯示 `POST ForgotPassword` 方法。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample9.cs)]

如果未確認使用者電子郵件，此方法會以無訊息模式失敗。 如果電子郵件地址的電子郵件地址已張貼錯誤，惡意使用者就可以使用該資訊來尋找有效的 userId (電子郵件別名) 以進行攻擊。

下列程式碼顯示 `ConfirmEmail` 帳戶控制器中的方法，當使用者在傳送給他們的電子郵件中選取確認連結時，會呼叫此方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample10.cs)]

一旦使用了遺忘的密碼權杖，就會失效。 `Create`*應用程式 \_ Start\IdentityConfig.cs* 檔中方法 (的下列程式碼變更) 將權杖設定為在3小時內到期。

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample11.cs?highlight=6-8)]

使用上述程式碼，忘記的密碼和電子郵件確認權杖將會在3小時內到期。 預設值 `TokenLifespan` 為一天。

下列程式碼顯示電子郵件確認方法：

[!code-csharp[Main](account-confirmation-and-password-recovery-with-aspnet-identity/samples/sample12.cs)]

 為了讓您的應用程式更安全，ASP.NET Identity 支援 Two-Factor 驗證 (2FA) 。 請參閱 [ASP.NET Identity 2.0：設定帳戶驗證以及](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx) John Atten 的 Two-Factor 授權。 雖然您可以在登入密碼嘗試失敗時設定帳戶鎖定，但這種方法會讓您的登入容易受到 [DOS](http://en.wikipedia.org/wiki/Denial-of-service_attack) 鎖定。 建議您只使用2FA 的帳戶鎖定。  
<a id="addRes"></a>

## <a name="additional-resources"></a>其他資源

- [ASP.NET Identity 的自訂儲存體提供者概觀](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入的 MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 也會顯示如何將設定檔資訊新增至 [使用者] 資料表。
- [ASP.NET MVC 和 Identity 2.0：瞭解 John Atten 的基本概念](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx) 。
- [ASP.NET Identity 簡介](../getting-started/introduction-to-aspnet-identity.md)
- [宣佈 RTM 的 ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) By Pranav 請參閱 rastogi。
