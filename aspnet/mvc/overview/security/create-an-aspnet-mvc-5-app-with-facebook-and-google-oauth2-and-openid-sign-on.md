---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: '使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入建立 MVC 5 應用程式 (c # ) |Microsoft Docs'
author: Rick-Anderson
description: 本教學課程說明如何建立 ASP.NET MVC 5 web 應用程式，讓使用者能夠使用 OAuth 2.0 搭配來自外部驗證的認證來登入 .。。
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345642"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>使用 Facebook、Twitter、LinkedIn 與 Google OAuth2 登入建立 ASP.NET MVC 5 應用程式 (C#)

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程說明如何建立 ASP.NET MVC 5 web 應用程式，讓使用者能夠使用 [OAuth 2.0](http://oauth.net/2/) 搭配來自外部驗證提供者（例如 Facebook、Twitter、LinkedIn、Microsoft 或 Google）的認證來登入。 為了簡單起見，本教學課程著重于使用 Facebook 和 Google 的認證。
> 
> 在您的網站中啟用這些認證可提供顯著的優點，因為數百萬個使用者已經有這些外部提供者的帳戶。 如果您的網站不需要建立並記住一組新的認證，則這些使用者可能更傾向于註冊您的網站。
> 
> 另請參閱 [使用 SMS 和電子郵件 Two-Factor 驗證來 ASP.NET MVC 5 應用程式](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。
> 
> 本教學課程也會說明如何新增使用者的設定檔資料，以及如何使用成員資格 API 來新增角色。 本教學課程由 [Rick Anderson](https://blogs.msdn.com/rickAndy) 撰寫 ( 請在 Twitter 上關注我： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ) 。

<a id="start"></a>
## <a name="getting-started"></a>開始使用

從安裝和[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[執行適用于 Web 或 Visual Studio 2013 的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058)開始。 安裝 Visual Studio [2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390521) 版本。 如需 Dropbox、GitHub、Linkedin、Instagram、Buffer、Salesforce、串流、Stack Exchange、Tripit、Twitch、Twitter、Yahoo！等的說明，請參閱此 [範例專案](https://github.com/matthewdunsdon/oauthforaspnet)。

> [!NOTE]
> 您必須安裝 Visual Studio [2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390521) 版本，才能使用 Google OAuth 2，並在本機進行無 SSL 警告的調試。

按一下 [**開始**] 頁面中的 [**新增專案**]，或者，您可以使用功能表**並選取 [** 檔案]，然後選取 [**新增專案**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>建立您的第一個應用程式

按一下 [ **新增專案**]，然後選取左側的 [ **Visual c #** ]、[ **Web** ]，然後選取 [ **ASP.NET web 應用程式**]。 將您的專案命名為 "MvcAuth"，然後按一下 **[確定]**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

在 [ **新增 ASP.NET 專案** ] 對話方塊中，按一下 [ **MVC**]。 如果驗證不是 **個別的使用者帳戶**，請按一下 [ **變更驗證** ] 按鈕，然後選取 [ **個別使用者帳戶**]。 藉由檢查 **雲端中的主機**，應用程式很容易就能裝載在 Azure 中。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

如果您在 **雲端中選取 [主機**]，請完成 [設定] 對話方塊。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>使用 NuGet 更新至最新的 OWIN 中介軟體

使用 NuGet 套件管理員來更新 [OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。 選取左側功能表中的 [ **更新** ]。 您可以按一下 [ **全部更新** ] 按鈕，也可以搜尋 (下一個影像) 所示的 OWIN 套件：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

在下圖中，只會顯示 OWIN 套件：

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

從封裝管理員主控台 (PMC) 中，您可以輸入 `Update-Package` 命令來更新所有套件。

按 **f5** 或 **Ctrl + f5** 執行應用程式。 在下圖中，埠號碼為1234。 當您執行應用程式時，您會看到不同的埠號碼。

視瀏覽器視窗的大小而定，您可能需要按一下流覽圖示來查看 [ **首頁**]、[ **關於**] **、**[ **註冊** ] 和 [ **登入** ] 連結。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>在專案中設定 SSL

若要連線至驗證提供者（例如 Google 和 Facebook），您必須將 IIS-Express 設定為使用 SSL。 請務必在登入後繼續使用 SSL，而不要回傳至 HTTP，而您的登入 cookie 就像您的使用者名稱和密碼一樣是秘密，而不使用 SSL，則會以純文字方式透過網路傳送。 此外，您已經花時間執行交握，並保護通道 (這是在執行 MVC 管線之前，使 HTTPS 比 HTTP) 慢很多的情況，因此在您登入之後重新導向回 HTTP，並不會讓目前的要求或未來的要求速度變得更快。

1. 在 **方案總管**中，按一下 [ **MvcAuth** ] 專案。
2. 按 F4 鍵以顯示專案屬性。 或者，您可以從 [ **View** ] 功能表選取 [ **屬性視窗]**。
3. 將 **已啟用的 SSL** 變更為 True。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. 複製 SSL URL (這會是 `https://localhost:44300/` ，除非您已建立其他 ssl 專案) 。
5. 在 **方案總管**中，以滑鼠右鍵按一下 **MvcAuth** 專案，然後選取 [ **屬性**]。
6. 選取 [ **Web** ] 索引標籤，然後將 SSL URL 貼到 [ **專案 URL** ] 方塊中。 將檔案儲存 (Ctl + S) 。 您將需要此 URL 來設定 Facebook 和 Google 驗證應用程式。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 將 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 屬性新增至 `Home` 控制器，要求所有要求都必須使用 HTTPS。 更安全的方法是將 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 篩選器新增至應用程式。 請參閱教學課程中的「 &quot; 使用 SSL 保護應用程式和授權屬性」一節，以 &quot; [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 首頁控制器的一部分如下所示。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. 按 CTRL+F5 執行應用程式。 如果您已安裝憑證，您可以略過本節的其餘部分，並跳至 [建立 OAuth 2 的 Google 應用程式，並將應用程式連接到專案](#goog)，否則請遵循指示來信任 IIS Express 所產生的自我簽署憑證。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 閱讀 [ **安全性警告** ] 對話方塊，如果您想要安裝代表 localhost 的憑證，請按一下 [ **是]** 。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 顯示 *首頁* ，沒有出現 SSL 警告。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 也接受憑證，並且會顯示 HTTPS 內容而不顯示警告。 Firefox 使用自己的憑證存放區，因此會顯示警告。 針對我們的應用程式，您可以放心地按一下 **我瞭解的風險**。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>建立適用于 OAuth 2 的 Google app，並將應用程式連接到專案

> [!WARNING]
> 如需目前的 Google OAuth 指示，請參閱 [在 ASP.NET Core 中設定 Google 驗證](/aspnet/core/security/authentication/social/google-logins)。

1. 瀏覽至 [Google Developers Console](https://console.developers.google.com/)。
2. 如果您之前尚未建立專案，請在左側索引標籤中選取 [ **認證** ]，然後選取 [ **建立**]。
3. 在左側索引標籤中，按一下 [ **認證**]。
4. 按一下 [ **建立認證** ]，然後按一下 [ **OAUTH 用戶端識別碼**]。 

    1. 在 [ **建立用戶端識別碼** ] 對話方塊中，保留應用程式類型的預設 **Web 應用程式** 。
    2. 將 **授權的 JavaScript** 來源設定為您在上面使用的 ssl URL (`https://localhost:44300/` 除非您已建立其他 ssl 專案) 
    3. 將授權的重新 **導向 URI** 設定為：  
         `https://localhost:44300/signin-google`
5. 按一下 [OAuth 同意畫面] 功能表項目，然後設定您的電子郵件地址和產品名稱。 當您完成表單時，請按一下 [ **儲存**]。
6. 按一下 [程式庫] 功能表項目、搜尋 **Google + API**、按一下該專案，然後按 [啟用]。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   下圖顯示已啟用的 Api。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. 從 Google Api API 管理員前往 [ **認證** ] 索引標籤，以取得 **用戶端識別碼**。 下載以儲存具有應用程式秘密的 JSON 檔案。 將**ClientId**和**ClientSecret**複製並貼到 `UseGoogleAuthentication` *App_Start*資料夾的*Startup.Auth.cs*檔中找到的方法。 以下顯示的 **ClientId** 和 **ClientSecret** 值為範例，無法運作。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 安全性-永不將機密資料儲存在您的原始程式碼中。 系統會將帳戶和認證新增至上述程式碼，以保持範例的簡易。 請參閱 [將密碼和其他機密資料部署至 ASP.NET 和 Azure App Service 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
8. 按 **CTRL + F5** 來建立並執行應用程式。 按一下 [登入] **** 連結。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 在 [ **使用其他服務登入**] 底下，按一下 [ **Google**]。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 如果您錯過上述任何步驟，則會收到 HTTP 401 錯誤。 重新檢查您上述的步驟。 如果遺漏必要的設定 (例如 **產品名稱**) ，請新增遺失的專案並儲存;驗證可能需要幾分鐘的時間才能運作。
10. 系統會將您重新導向至您將在其中輸入認證的 Google 網站。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 輸入認證後，系統便會提示您提供權限給剛建立的 Web 應用程式：
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 按一下 [接受]。 您現在會重新導向回到 MvcAuth 應用程式的 [ **註冊** ] 頁面，您可以在其中註冊 Google 帳戶。 您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。 按一下 [註冊] 。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>在 Facebook 中建立應用程式，並將應用程式連接到專案

> [!WARNING]
> 如需目前的 Facebook OAuth2 驗證指示，請參閱設定 [facebook 驗證](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>檢查成員資格資料

在 [ **View** ] 功能表中，按一下 [ **伺服器總管**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

展開 [ **DefaultConnection] (MvcAuth) **，展開 [ **資料表]**，以滑鼠右鍵按一下 **AspNetUsers** ，然後按一下 [ **顯示資料表資料**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 資料表資料](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>將設定檔資料新增至使用者類別

在本節中，您會在註冊期間將出生日期和首頁城鎮新增至使用者資料，如下圖所示。

![使用房屋城鎮和 Bday 的 reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

開啟 *Models\IdentityModels.cs* 檔案，並新增出生日期和主城鎮屬性：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

開啟 *Models\AccountViewModels.cs* 檔案，並在中開啟 [設定出生日期] 和 [首頁城鎮] 屬性 `ExternalLoginConfirmationViewModel` 。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

開啟 *Controllers\AccountController.cs* 檔案，並在動作方法中新增出生日期和主城鎮的程式碼， `ExternalLoginConfirmation` 如下所示：

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

將出生日期和首頁城鎮新增至 *Views\Account\ExternalLoginConfirmation.cshtml* 檔案：

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

刪除成員資格資料庫，讓您可以再次向應用程式註冊您的 Facebook 帳戶，並確認您可以加入新的出生日期和主城鎮設定檔資訊。

在 **方案總管**中，按一下 **[顯示所有** 檔案] 圖示，然後以滑鼠右鍵按一下 [ *新增 \_ Data\aspnet-MvcAuth- &lt; dateStamp &gt; * ]，再按一下 [ **刪除**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

從 [ **工具** ] 功能表按一下 [ **NuGet 套件**管理員]，然後按一下 [ **封裝管理員主控台** ] (PMC) 。 在 PMC 中輸入下列命令。

1. Enable-Migrations
2. Add-Migration Init
3. Update-Database

執行應用程式，並使用 FaceBook 和 Google 登入並註冊某些使用者。

## <a name="examine-the-membership-data"></a>檢查成員資格資料

在 [ **View** ] 功能表中，按一下 [ **伺服器總管**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

以滑鼠右鍵按一下 **AspNetUsers** ，然後按一下 [ **顯示資料表資料**]。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

`HomeTown`和 `BirthDate` 欄位如下所示。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>登出您的應用程式，並使用其他帳戶登入

如果您使用 Facebook 登入應用程式，然後登出再嘗試使用不同的 Facebook 帳戶登入 (使用相同的瀏覽器) ，您將會立即登入先前使用的 Facebook 帳戶。 若要使用其他帳戶，您需要流覽至 Facebook 並登出于 Facebook。 相同的規則適用于其他任何協力廠商驗證提供者。 或者，您可以使用不同的瀏覽器，以其他帳戶登入。

## <a name="next-steps"></a>後續步驟

請參閱 OWIN by >jerrie Pelser 的 [yahoo 和 Linkedin OAuth 安全性提供者簡介](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) ，以瞭解 Yahoo 和 linkedin 的指示。 請參閱 >jerrie 的 ASP.NET MVC 5 的很好社交登入按鈕，以取得啟用社交登入按鈕。

遵循教學課程， [使用 auth 和 SQL DB 建立 ASP.NET MVC 應用程式，並部署到 Azure App Service，以繼續進行](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)本教學課程，並顯示下列內容：

1. 如何將應用程式部署到 Azure。
2. 如何使用角色保護您的應用程式。
3. 如何使用 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 和 [授權](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 篩選來保護您的應用程式。
4. 如何使用成員資格 API 來新增使用者和角色。

請針對您喜歡本教學課程的方式以及我們可以改進的內容留下意見反應。 您也可以向我要求新 [的主題，告訴我如何使用程式碼](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。 您甚至可以要求及投票要新增至 ASP.NET 的新功能。 例如，您可以投票工具來 [建立及管理使用者和角色。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

如需 ASP.NET 外部驗證服務運作方式的良好說明，請參閱 Robert McMurray 的 [外部驗證服務](https://asp.net/web-api/overview/security/external-authentication-services)。 Robert 的文章也會詳細說明如何啟用 Microsoft 和 Twitter 驗證。 Tom Dykstra 的絕佳 [EF/MVC 教學](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 課程說明如何使用 Entity Framework。
