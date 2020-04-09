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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="94fb6-103">使用 Facebook、Twitter、LinkedIn 與 Google OAuth2 登入建立 ASP.NET MVC 5 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="94fb6-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="94fb6-104">由[里克·安德森](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="94fb6-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="94fb6-105">本教程介紹如何構建ASP.NET MVC 5 Web 應用程式,使用戶能夠使用[OAuth 2.0](http://oauth.net/2/)使用外部身份驗證供應商(如Facebook、Twitter、LinkedIn、微軟或Google)的認證登入。</span><span class="sxs-lookup"><span data-stu-id="94fb6-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="94fb6-106">為簡單起見,本教程重點介紹使用來自 Facebook 和 Google 的認證。</span><span class="sxs-lookup"><span data-stu-id="94fb6-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="94fb6-107">在您的網站中啟用這些憑據提供了顯著優勢,因為數百萬使用者已經擁有了這些外部供應商的帳戶。</span><span class="sxs-lookup"><span data-stu-id="94fb6-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="94fb6-108">如果使用者不必創建並記住一組新的憑據,他們可能更傾向於註冊您的網站。</span><span class="sxs-lookup"><span data-stu-id="94fb6-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="94fb6-109">另請參閱[ASP.NET MVC 5 應用程式與簡訊和電子郵件雙重身份驗證](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="94fb6-110">本教學還展示如何為使用者添加配置檔數據,以及如何使用成員資格 API 添加角色。</span><span class="sxs-lookup"><span data-stu-id="94fb6-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="94fb6-111">本教程是由[里克安德森](https://blogs.msdn.com/rickAndy)(請關注我[@RickAndMSFT](https://twitter.com/RickAndMSFT)在推特上: ).</span><span class="sxs-lookup"><span data-stu-id="94fb6-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="94fb6-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="94fb6-112">Getting Started</span></span>

<span data-ttu-id="94fb6-113">首先安裝與執行[Visual Studio Express 2013 用於 Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[視覺化工作室 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="94fb6-114">安裝可視化工作室[2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="94fb6-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="94fb6-115">有關 Dropbox、GitHub、LinkedIn、Instagram、緩衝、銷售力量、STEAM、堆疊交換、三聯、Twitch、Twitter、Yahoo!等的説明,請參閱此示例[專案](https://github.com/matthewdunsdon/oauthforaspnet)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="94fb6-116">您必須安裝 Visual Studio [2013 更新 3](https://go.microsoft.com/fwlink/?LinkId=390521)或更高版本才能使用 Google OAuth 2 並在本地調試,而無需出現 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="94fb6-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="94fb6-117">按下 **「開始」** 頁中的 **「新專案**」,也可以使用選單並選擇 **「檔案**」,然後選擇 **「新專案**」 。</span><span class="sxs-lookup"><span data-stu-id="94fb6-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="94fb6-118">建立第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="94fb6-118">Creating Your First Application</span></span>

<span data-ttu-id="94fb6-119">點選 **「新項目**」,然後選擇左側的**視覺化 C#,** 然後選擇**Web,** 然後選擇**ASP.NET Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="94fb6-120">將專案命名為"MvcAuth",然後單擊"**確定**"。</span><span class="sxs-lookup"><span data-stu-id="94fb6-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="94fb6-121">在 **「新ASP.NET專案」** 對話框中,按下**MVC**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="94fb6-122">如果認證不是**單個使用者帳戶**,請按下 **「更改身份認證**」按鈕並選擇**單個使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="94fb6-123">通過檢查**雲中的主機**,應用程式將很容易在 Azure 中託管。</span><span class="sxs-lookup"><span data-stu-id="94fb6-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="94fb6-124">如果在**雲中選擇"主機**",請完成配置對話方塊。</span><span class="sxs-lookup"><span data-stu-id="94fb6-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="94fb6-125">使用 NuGet 更新到最新的 OWIN 中間元件</span><span class="sxs-lookup"><span data-stu-id="94fb6-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="94fb6-126">使用 NuGet 套件管理員更新[OWIN 中間件](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="94fb6-127">選擇左側功能表中的 **「更新**」 。</span><span class="sxs-lookup"><span data-stu-id="94fb6-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="94fb6-128">您可以按下 **「 全部更新」** 按鈕,也可以僅搜尋 OWIN 套件(下一張圖片所示):</span><span class="sxs-lookup"><span data-stu-id="94fb6-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="94fb6-129">在下圖中,僅顯示 OWIN 套件:</span><span class="sxs-lookup"><span data-stu-id="94fb6-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="94fb6-130">從包管理員主控台 (PMC) 中`Update-Package`,您可以輸入該命令,該命令將更新所有包。</span><span class="sxs-lookup"><span data-stu-id="94fb6-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="94fb6-131">按**F5**或**Ctrl+F5**以運行應用程式。</span><span class="sxs-lookup"><span data-stu-id="94fb6-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="94fb6-132">在下圖中,埠號為 1234。</span><span class="sxs-lookup"><span data-stu-id="94fb6-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="94fb6-133">運行應用程式時,您將看到不同的埠號。</span><span class="sxs-lookup"><span data-stu-id="94fb6-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="94fb6-134">根據瀏覽器視窗的大小,您可能需要按一下導航圖示才能查看 **「主頁**、**關於**」、**聯繫**、**註冊**和**登入**連結。</span><span class="sxs-lookup"><span data-stu-id="94fb6-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="94fb6-135">在項目中設定 SSL</span><span class="sxs-lookup"><span data-stu-id="94fb6-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="94fb6-136">要連接到 Google 和 Facebook 等身份驗證供應商,您需要設置 IIS-Express 才能使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="94fb6-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="94fb6-137">登錄後繼續使用 SSL 而不回退到 HTTP 非常重要,您的登錄 Cookie 與使用者名和密碼一樣具有機密性,無需使用 SSL,則透過線發送清晰文本。</span><span class="sxs-lookup"><span data-stu-id="94fb6-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="94fb6-138">此外,在運行 MVC 管道之前,您已經花時間執行握手並保護通道(這是使 HTTPS 比 HTTP 慢的大部分),因此在登錄後重定向回 HTTP 不會使當前請求或將來的請求更快。</span><span class="sxs-lookup"><span data-stu-id="94fb6-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="94fb6-139">在**解決方案資源管理器中**,按**一下 MvcAuth**專案。</span><span class="sxs-lookup"><span data-stu-id="94fb6-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="94fb6-140">點擊 F4 鍵以顯示項目屬性。</span><span class="sxs-lookup"><span data-stu-id="94fb6-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="94fb6-141">或者,從 **「檢視」** 選單中選擇 **「屬性視窗**」。。</span><span class="sxs-lookup"><span data-stu-id="94fb6-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="94fb6-142">將**啟用的 SSL**更改為 true。</span><span class="sxs-lookup"><span data-stu-id="94fb6-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="94fb6-143">複製 SSL URL(除非您`https://localhost:44300/`建立了 其他 SSL 項目,否則這將是 SSL URL)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="94fb6-144">在**解決方案資源管理員**中,右鍵按**一下 MvcAuth**專案並選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="94fb6-145">選擇 **"Web"** 選項卡,然後將 SSL URL 貼上到 **'專案網址'** 框中。</span><span class="sxs-lookup"><span data-stu-id="94fb6-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="94fb6-146">保存檔 (Ctl_S)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="94fb6-147">您需要此網址來配置 Facebook 和 Google 身份驗證應用。</span><span class="sxs-lookup"><span data-stu-id="94fb6-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="94fb6-148">將[「要求HTT」](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)屬性`Home`添加到控制器,以要求所有請求都必須使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="94fb6-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="94fb6-149">更安全的方法是向應用程式添加[「需要H.S'](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)篩選器。</span><span class="sxs-lookup"><span data-stu-id="94fb6-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="94fb6-150">請參考我的教學&quot;中的「使用 SSL 與授權&quot;屬性 保護應用程式」 ,[建立一個帶有身份驗證與 SQL DB 的 ASP.NET MVC 應用程式並部署到 Azure 應用服務](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="94fb6-151">主控制器的一部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="94fb6-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="94fb6-152">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="94fb6-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="94fb6-153">如果您過去安裝了證書,則可以跳過本節的其餘部分,跳轉到[為 OAuth 2 創建 Google 應用並將應用連接到專案](#goog),否則,請按照說明信任 IIS Express 生成的自簽名證書。</span><span class="sxs-lookup"><span data-stu-id="94fb6-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="94fb6-154">閱讀**安全警告**對話框,然後按下「**是**」,如果要安裝表示本地主機的證書。</span><span class="sxs-lookup"><span data-stu-id="94fb6-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="94fb6-155">IE 顯示 *首頁* ，沒有出現 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="94fb6-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="94fb6-156">Google Chrome 也接受該證書,並在不發出警告的情況下顯示 HTTPS 內容。</span><span class="sxs-lookup"><span data-stu-id="94fb6-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="94fb6-157">Firefox 使用自己的證書存儲,因此將顯示警告。</span><span class="sxs-lookup"><span data-stu-id="94fb6-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="94fb6-158">對於我們的應用程式,您可以安全地點擊 **「我了解風險**」。。</span><span class="sxs-lookup"><span data-stu-id="94fb6-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="94fb6-159">為 OAuth 2 建立 Google 應用並將應用連線到專案</span><span class="sxs-lookup"><span data-stu-id="94fb6-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="94fb6-160">有關目前 Google OAuth 說明,請參閱[在 ASP.NET 核心 中設定 Google 身份驗證](/aspnet/core/security/authentication/social/google-logins)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="94fb6-161">瀏覽至 [Google Developers Console](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="94fb6-162">如果以前未建立專案,請在左側選項卡中選擇 **「憑據」,** 然後選擇「**創建**」。</span><span class="sxs-lookup"><span data-stu-id="94fb6-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="94fb6-163">在左側選項卡中,按兩下 **「憑據**」。。</span><span class="sxs-lookup"><span data-stu-id="94fb6-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="94fb6-164">按下 **「建立認證**」,然後按下**OAuth 客戶端代碼**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="94fb6-165">在 **"建立用戶端 ID'** 對話框中,保留應用程式類型的預設**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="94fb6-166">將**授權 JavaScript**源設定為此使用的 SSL 網址(`https://localhost:44300/`除非您建立其他 SSL 專案 )</span><span class="sxs-lookup"><span data-stu-id="94fb6-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="94fb6-167">將**授權重定向 URI**設定為:</span><span class="sxs-lookup"><span data-stu-id="94fb6-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="94fb6-168">按下"OAuth 同意"螢幕功能表項,然後設置您的電子郵件地址和產品名稱。</span><span class="sxs-lookup"><span data-stu-id="94fb6-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="94fb6-169">填寫完表格後,按一下「**保存**」。</span><span class="sxs-lookup"><span data-stu-id="94fb6-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="94fb6-170">點擊庫菜單專案,搜索**谷歌+API,** 點擊它,然後按啟用。</span><span class="sxs-lookup"><span data-stu-id="94fb6-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="94fb6-171">下圖顯示了啟用的 API。</span><span class="sxs-lookup"><span data-stu-id="94fb6-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="94fb6-172">從 Google API API API 管理員,存**取認證**的選項卡以取得**客戶端 ID**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="94fb6-173">下載以保存包含應用程式機密的 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="94fb6-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="94fb6-174">將**客戶端 Id**和**用戶端機密**複製並貼上`UseGoogleAuthentication`*App_Start*資料夾中*Startup.Auth.cs*檔中找到的方法。</span><span class="sxs-lookup"><span data-stu-id="94fb6-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="94fb6-175">下面顯示的**用戶端 Id**和**用戶端機密**值是示例,不起作用。</span><span class="sxs-lookup"><span data-stu-id="94fb6-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="94fb6-176">安全性 - 切勿將敏感數據存儲在原始碼中。</span><span class="sxs-lookup"><span data-stu-id="94fb6-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="94fb6-177">帳戶和憑據將添加到上面的代碼中,以保持示例簡單。</span><span class="sxs-lookup"><span data-stu-id="94fb6-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="94fb6-178">請參考[將密碼和其他敏感資料部署到 ASP.NET 和 Azure 應用服務的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="94fb6-179">按**CTRL+F5**生成並運行應用程式。</span><span class="sxs-lookup"><span data-stu-id="94fb6-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="94fb6-180">按一下 [登入] \*\*\*\* 連結。</span><span class="sxs-lookup"><span data-stu-id="94fb6-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="94fb6-181">在 **「使用其他服務登入**」下,按**一下 Google**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="94fb6-182">如果您錯過了上述任何步驟,您將獲得 HTTP 401 錯誤。</span><span class="sxs-lookup"><span data-stu-id="94fb6-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="94fb6-183">重新檢查上面的步驟。</span><span class="sxs-lookup"><span data-stu-id="94fb6-183">Recheck your steps above.</span></span> <span data-ttu-id="94fb6-184">如果錯過了所需的設置(例如**產品名稱**),則添加缺少的專案並保存;身份驗證可能需要幾分鐘才能工作。</span><span class="sxs-lookup"><span data-stu-id="94fb6-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="94fb6-185">您將被重定向到 Google 網站,您將在其中輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="94fb6-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="94fb6-186">輸入認證後，系統便會提示您提供權限給剛建立的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="94fb6-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="94fb6-187">按下"**接受**"。</span><span class="sxs-lookup"><span data-stu-id="94fb6-187">Click **Accept**.</span></span> <span data-ttu-id="94fb6-188">現在,您將被重定向回 MvcAuth 應用程式的**註冊**頁面,您可以在其中註冊您的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94fb6-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="94fb6-189">您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="94fb6-190">按一下 [註冊]  。</span><span class="sxs-lookup"><span data-stu-id="94fb6-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="94fb6-191">在 Facebook 中建立應用並將應用連線到專案</span><span class="sxs-lookup"><span data-stu-id="94fb6-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="94fb6-192">有關當前 Facebook OAuth2 身份驗證說明,請參閱[配置 Facebook 身份驗證](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="94fb6-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="94fb6-193">檢查成員資格資料</span><span class="sxs-lookup"><span data-stu-id="94fb6-193">Examine the Membership Data</span></span>

<span data-ttu-id="94fb6-194">在 **「查看」** 選單中,按下 **「伺服器資源管理員**」。</span><span class="sxs-lookup"><span data-stu-id="94fb6-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="94fb6-195">展開**預設連線 (MvcAuth),** 展開**表**, 右鍵按**下 AspNetUsers**並按下**顯示表格資料**。</span><span class="sxs-lookup"><span data-stu-id="94fb6-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetuser 表資料](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="94fb6-197">將設定檔資料加入使用者類別</span><span class="sxs-lookup"><span data-stu-id="94fb6-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="94fb6-198">在本節中,您將在註冊期間將出生日期和家鄉添加到用戶數據中,如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="94fb6-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![與家鄉和布萊德](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="94fb6-200">開啟*模型_身份模型.cs*檔並添加出生日期和家鄉屬性:</span><span class="sxs-lookup"><span data-stu-id="94fb6-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="94fb6-201">打開*模型_AccountViewModels.cs*檔以及`ExternalLoginConfirmationViewModel`中的設定出生日期和家鄉屬性。</span><span class="sxs-lookup"><span data-stu-id="94fb6-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="94fb6-202">開啟*控制器\AccountController.cs*檔案`ExternalLoginConfirmation`,並在 操作方法中添加出生日期和家鄉的代碼,如圖所示:</span><span class="sxs-lookup"><span data-stu-id="94fb6-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="94fb6-203">將出生日期和家鄉添加到*檢視\帳戶\外部登錄確認.cshtml*檔:</span><span class="sxs-lookup"><span data-stu-id="94fb6-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="94fb6-204">刪除會員資料庫,以便您可以再次將您的 Facebook 帳戶註冊到您的應用程式,並驗證您可以添加新的出生日期和家鄉個人資料資訊。</span><span class="sxs-lookup"><span data-stu-id="94fb6-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="94fb6-205">從**解決方案資源管理員**中,按下 **「顯示所有檔案**」圖示,然後單擊 *「\_新增&lt;資料\aspnet-MvcAuth-dateStamp.mdf」,&gt;* 然後按一下「**刪除**」 。</span><span class="sxs-lookup"><span data-stu-id="94fb6-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="94fb6-206">在**工具選**單中,按下**NuGet 套件管理器,** 然後單擊**套件管理器主控台**(PMC)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="94fb6-207">在 PMC 中輸入以下命令。</span><span class="sxs-lookup"><span data-stu-id="94fb6-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="94fb6-208">開啟移轉</span><span class="sxs-lookup"><span data-stu-id="94fb6-208">Enable-Migrations</span></span>
2. <span data-ttu-id="94fb6-209">新增移轉 Init</span><span class="sxs-lookup"><span data-stu-id="94fb6-209">Add-Migration Init</span></span>
3. <span data-ttu-id="94fb6-210">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="94fb6-210">Update-Database</span></span>

<span data-ttu-id="94fb6-211">運行該應用程式並使用FaceBook和Google登錄並註冊一些使用者。</span><span class="sxs-lookup"><span data-stu-id="94fb6-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="94fb6-212">檢查成員資格資料</span><span class="sxs-lookup"><span data-stu-id="94fb6-212">Examine the Membership Data</span></span>

<span data-ttu-id="94fb6-213">在 **「查看」** 選單中,按下 **「伺服器資源管理員**」。</span><span class="sxs-lookup"><span data-stu-id="94fb6-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="94fb6-214">右鍵按**一下 AspNetUsers**並按下「**顯示表數據**」。</span><span class="sxs-lookup"><span data-stu-id="94fb6-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="94fb6-215">和`HomeTown``BirthDate`字段如下所示。</span><span class="sxs-lookup"><span data-stu-id="94fb6-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="94fb6-216">登出應用程式並與其他帳戶登入</span><span class="sxs-lookup"><span data-stu-id="94fb6-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="94fb6-217">如果您使用 Facebook 登錄你的應用,然後登出並嘗試使用其他 Facebook 帳戶(使用相同的瀏覽器)再次登錄,您將立即登錄到您使用的以前的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="94fb6-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="94fb6-218">要使用其他帳戶,您需要導航到 Facebook 並在 Facebook 登出。</span><span class="sxs-lookup"><span data-stu-id="94fb6-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="94fb6-219">相同的規則適用於任何其他第三方身份驗證提供程式。</span><span class="sxs-lookup"><span data-stu-id="94fb6-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="94fb6-220">或者,您可以使用其他瀏覽器使用其他帳戶登錄。</span><span class="sxs-lookup"><span data-stu-id="94fb6-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94fb6-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94fb6-221">Next Steps</span></span>

<span data-ttu-id="94fb6-222">請參閱介紹[雅虎和LinkedInOAuth安全供應商為OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/)由傑里佩爾瑟雅虎和LinkedIn說明。</span><span class="sxs-lookup"><span data-stu-id="94fb6-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="94fb6-223">請參閱 Jerrie 的「漂亮的社交登錄按鈕」ASP.NET MVC 5,以獲得啟用社交登錄按鈕。</span><span class="sxs-lookup"><span data-stu-id="94fb6-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="94fb6-224">按照我的教程[創建一個帶有 auth 和 SQL DB 的 ASP.NET MVC 應用並部署到 Azure 應用服務](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data),該教程將繼續本教程並顯示以下內容:</span><span class="sxs-lookup"><span data-stu-id="94fb6-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="94fb6-225">如何將應用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="94fb6-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="94fb6-226">如何使用角色保護應用。</span><span class="sxs-lookup"><span data-stu-id="94fb6-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="94fb6-227">如何使用[「需要 HTTP"](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx)和[「授權](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx)」篩選器保護應用。</span><span class="sxs-lookup"><span data-stu-id="94fb6-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="94fb6-228">如何使用成員資格 API 添加使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="94fb6-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="94fb6-229">請留下反饋,關於你喜歡本教程的方式,以及我們可以改進什麼。</span><span class="sxs-lookup"><span data-stu-id="94fb6-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="94fb6-230">您也可以在[「向我展示代碼如何](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)」上請求新主題。</span><span class="sxs-lookup"><span data-stu-id="94fb6-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="94fb6-231">您甚至可以要求並投票表決要添加到ASP.NET的新功能。</span><span class="sxs-lookup"><span data-stu-id="94fb6-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="94fb6-232">例如,您可以投票選擇[創建和管理使用者和角色的工具。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="94fb6-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="94fb6-233">有關外部身份驗證服務ASP.NET工作方式的良好說明,請參閱羅伯特·麥克默裡的外部[身份驗證服務](https://asp.net/web-api/overview/security/external-authentication-services)。</span><span class="sxs-lookup"><span data-stu-id="94fb6-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="94fb6-234">羅伯特的文章還詳細介紹了微軟和Twitter的認證。</span><span class="sxs-lookup"><span data-stu-id="94fb6-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="94fb6-235">Tom Dykstra 出色的[EF/MVC 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)展示了如何使用實體框架。</span><span class="sxs-lookup"><span data-stu-id="94fb6-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
