---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: 使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登錄 (C#) 創建 MVC 5 應用程式 |微軟文件
author: Rick-Anderson
description: 本教程介紹如何構建ASP.NET MVC 5 Web 應用程式,使用戶能夠使用 OAuth 2.0 使用外部 authenti 的認證登錄...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676318"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>使用 Facebook、Twitter、LinkedIn 與 Google OAuth2 登入建立 ASP.NET MVC 5 應用程式 (C#)

由[里克·安德森](https://twitter.com/RickAndMSFT)

> 本教程介紹如何構建ASP.NET MVC 5 Web 應用程式,使用戶能夠使用[OAuth 2.0](http://oauth.net/2/)使用外部身份驗證供應商(如Facebook、Twitter、LinkedIn、微軟或Google)的認證登入。 為簡單起見,本教程重點介紹使用來自 Facebook 和 Google 的認證。
> 
> 在您的網站中啟用這些憑據提供了顯著優勢,因為數百萬使用者已經擁有了這些外部供應商的帳戶。 如果使用者不必創建並記住一組新的憑據,他們可能更傾向於註冊您的網站。
> 
> 另請參閱[ASP.NET MVC 5 應用程式與簡訊和電子郵件雙重身份驗證](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。
> 
> 本教學還展示如何為使用者添加配置檔數據,以及如何使用成員資格 API 添加角色。 本教程是由[里克安德森](https://blogs.msdn.com/rickAndy)(請關注我[@RickAndMSFT](https://twitter.com/RickAndMSFT)在推特上: ).

<a id="start"></a>
## <a name="getting-started"></a>開始使用

首先安裝與執行[Visual Studio Express 2013 用於 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[視覺化工作室 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安裝可視化工作室[2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。 有關 Dropbox、GitHub、LinkedIn、Instagram、緩衝、銷售力量、STEAM、堆疊交換、三聯、Twitch、Twitter、Yahoo!等的説明,請參閱此示例[專案](https://github.com/matthewdunsdon/oauthforaspnet)。

> [!NOTE]
> 您必須安裝 Visual Studio [2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本才能使用 Google OAuth 2 並在本地調試,而無需出現 SSL 警告。

按下 **「開始」** 頁中的 **「新專案**」,也可以使用選單並選擇 **「檔案**」,然後選擇 **「新專案**」 。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>建立第一個應用程式

點選 **「新項目**」,然後選擇左側的**視覺化 C#,** 然後選擇**Web,** 然後選擇**ASP.NET Web 應用程式**。 將專案命名為"MvcAuth",然後單擊"**確定**"。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

在 **「新ASP.NET專案」** 對話框中,按下**MVC**。 如果認證不是**單個使用者帳戶**,請按下 **「更改身份認證**」按鈕並選擇**單個使用者帳戶**。 通過檢查**雲中的主機**,應用程式將很容易在 Azure 中託管。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

如果在**雲中選擇"主機**",請完成配置對話方塊。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>使用 NuGet 更新到最新的 OWIN 中間元件

使用 NuGet 套件管理員更新[OWIN 中間件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。 選擇左側功能表中的 **「更新**」 。 您可以按下 **「 全部更新」** 按鈕,也可以僅搜尋 OWIN 套件(下一張圖片所示):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

在下圖中,僅顯示 OWIN 套件:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

從包管理員主控台 (PMC) 中`Update-Package`,您可以輸入該命令,該命令將更新所有包。

按**F5**或**Ctrl+F5**以運行應用程式。 在下圖中,埠號為 1234。 運行應用程式時,您將看到不同的埠號。

根據瀏覽器視窗的大小,您可能需要按一下導航圖示才能查看 **「主頁**、**關於**」、**聯繫**、**註冊**和**登入**連結。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>在項目中設定 SSL

要連接到 Google 和 Facebook 等身份驗證供應商,您需要設置 IIS-Express 才能使用 SSL。 登錄後繼續使用 SSL 而不回退到 HTTP 非常重要,您的登錄 Cookie 與使用者名和密碼一樣具有機密性,無需使用 SSL,則透過線發送清晰文本。 此外,在運行 MVC 管道之前,您已經花時間執行握手並保護通道(這是使 HTTPS 比 HTTP 慢的大部分),因此在登錄後重定向回 HTTP 不會使當前請求或將來的請求更快。

1. 在**解決方案資源管理器中**,按**一下 MvcAuth**專案。
2. 點擊 F4 鍵以顯示項目屬性。 或者,從 **「檢視」** 選單中選擇 **「屬性視窗**」。。
3. 將**啟用的 SSL**更改為 true。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. 複製 SSL URL(除非您`https://localhost:44300/`建立了 其他 SSL 項目,否則這將是 SSL URL)。
5. 在**解決方案資源管理員**中,右鍵按**一下 MvcAuth**專案並選擇**屬性**。
6. 選擇 **"Web"** 選項卡,然後將 SSL URL 貼上到 **'專案網址'** 框中。 保存檔 (Ctl_S)。 您需要此網址來配置 Facebook 和 Google 身份驗證應用。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. 將[「要求HTT」](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)屬性`Home`添加到控制器,以要求所有請求都必須使用 HTTPS。 更安全的方法是向應用程式添加[「需要H.S'](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)篩選器。 請參考我的教學&quot;中的「使用 SSL 與授權&quot;屬性 保護應用程式」 ,[建立一個帶有身份驗證與 SQL DB 的 ASP.NET MVC 應用程式並部署到 Azure 應用服務](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 主控制器的一部分如下所示。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. 按 CTRL+F5 執行應用程式。 如果您過去安裝了證書,則可以跳過本節的其餘部分,跳轉到[為 OAuth 2 創建 Google 應用並將應用連接到專案](#goog),否則,請按照說明信任 IIS Express 生成的自簽名證書。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. 閱讀**安全警告**對話框,然後按下「**是**」,如果要安裝表示本地主機的證書。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. IE 顯示 *首頁* ，沒有出現 SSL 警告。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome 也接受該證書,並在不發出警告的情況下顯示 HTTPS 內容。 Firefox 使用自己的證書存儲,因此將顯示警告。 對於我們的應用程式,您可以安全地點擊 **「我了解風險**」。。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>為 OAuth 2 建立 Google 應用並將應用連線到專案

> [!WARNING]
> 有關目前 Google OAuth 說明,請參閱[在 ASP.NET 核心 中設定 Google 身份驗證](/aspnet/core/security/authentication/social/google-logins)。

1. 瀏覽至 [Google Developers Console](https://console.developers.google.com/)。
2. 如果以前未建立專案,請在左側選項卡中選擇 **「憑據」,** 然後選擇「**創建**」。
3. 在左側選項卡中,按兩下 **「憑據**」。。
4. 按下 **「建立認證**」,然後按下**OAuth 客戶端代碼**。 

    1. 在 **"建立用戶端 ID'** 對話框中,保留應用程式類型的預設**Web 應用程式**。
    2. 將**授權 JavaScript**源設定為此使用的 SSL 網址(`https://localhost:44300/`除非您建立其他 SSL 專案 )
    3. 將**授權重定向 URI**設定為:  
         `https://localhost:44300/signin-google`
5. 按下"OAuth 同意"螢幕功能表項,然後設置您的電子郵件地址和產品名稱。 填寫完表格後,按一下「**保存**」。
6. 點擊庫菜單專案,搜索**谷歌+API,** 點擊它,然後按啟用。
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   下圖顯示了啟用的 API。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. 從 Google API API API 管理員,存**取認證**的選項卡以取得**客戶端 ID**。 下載以保存包含應用程式機密的 JSON 檔。 將**客戶端 Id**和**用戶端機密**複製並貼上`UseGoogleAuthentication`*App_Start*資料夾中*Startup.Auth.cs*檔中找到的方法。 下面顯示的**用戶端 Id**和**用戶端機密**值是示例,不起作用。

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > 安全性 - 切勿將敏感數據存儲在原始碼中。 帳戶和憑據將添加到上面的代碼中,以保持示例簡單。 請參考[將密碼和其他敏感資料部署到 ASP.NET 和 Azure 應用服務的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
8. 按**CTRL+F5**生成並運行應用程式。 按一下 [登入] **** 連結。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. 在 **「使用其他服務登入**」下,按**一下 Google**。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > 如果您錯過了上述任何步驟,您將獲得 HTTP 401 錯誤。 重新檢查上面的步驟。 如果錯過了所需的設置(例如**產品名稱**),則添加缺少的專案並保存;身份驗證可能需要幾分鐘才能工作。
10. 您將被重定向到 Google 網站,您將在其中輸入您的認證。   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. 輸入認證後，系統便會提示您提供權限給剛建立的 Web 應用程式：
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. 按下"**接受**"。 現在,您將被重定向回 MvcAuth 應用程式的**註冊**頁面,您可以在其中註冊您的 Google 帳戶。 您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。 按一下 [註冊]  。  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>在 Facebook 中建立應用並將應用連線到專案

> [!WARNING]
> 有關當前 Facebook OAuth2 身份驗證說明,請參閱[配置 Facebook 身份驗證](/aspnet/core/security/authentication/social/facebook-logins)

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>檢查成員資格資料

在 **「查看」** 選單中,按下 **「伺服器資源管理員**」。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

展開**預設連線 (MvcAuth),** 展開**表**, 右鍵按**下 AspNetUsers**並按下**顯示表格資料**。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetuser 表資料](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>將設定檔資料加入使用者類別

在本節中,您將在註冊期間將出生日期和家鄉添加到用戶數據中,如下圖所示。

![與家鄉和布萊德](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

開啟*模型_身份模型.cs*檔並添加出生日期和家鄉屬性:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

打開*模型_AccountViewModels.cs*檔以及`ExternalLoginConfirmationViewModel`中的設定出生日期和家鄉屬性。

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

開啟*控制器\AccountController.cs*檔案`ExternalLoginConfirmation`,並在 操作方法中添加出生日期和家鄉的代碼,如圖所示:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

將出生日期和家鄉添加到*檢視\帳戶\外部登錄確認.cshtml*檔:

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

刪除會員資料庫,以便您可以再次將您的 Facebook 帳戶註冊到您的應用程式,並驗證您可以添加新的出生日期和家鄉個人資料資訊。

從**解決方案資源管理員**中,按下 **「顯示所有檔案**」圖示,然後單擊 *「\_新增&lt;資料\aspnet-MvcAuth-dateStamp.mdf」,&gt;* 然後按一下「**刪除**」 。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

在**工具選**單中,按下**NuGet 套件管理器,** 然後單擊**套件管理器主控台**(PMC)。 在 PMC 中輸入以下命令。

1. 開啟移轉
2. 新增移轉 Init
3. 更新資料庫

運行該應用程式並使用FaceBook和Google登錄並註冊一些使用者。

## <a name="examine-the-membership-data"></a>檢查成員資格資料

在 **「查看」** 選單中,按下 **「伺服器資源管理員**」。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

右鍵按**一下 AspNetUsers**並按下「**顯示表數據**」。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

和`HomeTown``BirthDate`字段如下所示。

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>登出應用程式並與其他帳戶登入

如果您使用 Facebook 登錄你的應用,然後登出並嘗試使用其他 Facebook 帳戶(使用相同的瀏覽器)再次登錄,您將立即登錄到您使用的以前的 Facebook 帳戶。 要使用其他帳戶,您需要導航到 Facebook 並在 Facebook 登出。 相同的規則適用於任何其他第三方身份驗證提供程式。 或者,您可以使用其他瀏覽器使用其他帳戶登錄。

## <a name="next-steps"></a>後續步驟

請參閱介紹[雅虎和LinkedInOAuth安全供應商為OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)由傑里佩爾瑟雅虎和LinkedIn說明。 請參閱 Jerrie 的「漂亮的社交登錄按鈕」ASP.NET MVC 5,以獲得啟用社交登錄按鈕。

按照我的教程[創建一個帶有 auth 和 SQL DB 的 ASP.NET MVC 應用並部署到 Azure 應用服務](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),該教程將繼續本教程並顯示以下內容:

1. 如何將應用部署到 Azure。
2. 如何使用角色保護應用。
3. 如何使用[「需要 HTTP"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)和[「授權](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)」篩選器保護應用。
4. 如何使用成員資格 API 添加使用者和角色。

請留下反饋,關於你喜歡本教程的方式,以及我們可以改進什麼。 您也可以在[「向我展示代碼如何](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)」上請求新主題。 您甚至可以要求並投票表決要添加到ASP.NET的新功能。 例如,您可以投票選擇[創建和管理使用者和角色的工具。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

有關外部身份驗證服務ASP.NET工作方式的良好說明,請參閱羅伯特·麥克默裡的外部[身份驗證服務](https://asp.net/web-api/overview/security/external-authentication-services)。 羅伯特的文章還詳細介紹了微軟和Twitter的認證。 Tom Dykstra 出色的[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)展示了如何使用實體框架。
