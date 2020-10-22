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
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a><span data-ttu-id="fa934-103">使用 Facebook、Twitter、LinkedIn 與 Google OAuth2 登入建立 ASP.NET MVC 5 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="fa934-103">Create an ASP.NET MVC 5 App with Facebook, Twitter, LinkedIn and Google OAuth2 Sign-on (C#)</span></span>

<span data-ttu-id="fa934-104">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="fa934-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="fa934-105">本教學課程說明如何建立 ASP.NET MVC 5 web 應用程式，讓使用者能夠使用 [OAuth 2.0](http://oauth.net/2/) 搭配來自外部驗證提供者（例如 Facebook、Twitter、LinkedIn、Microsoft 或 Google）的認證來登入。</span><span class="sxs-lookup"><span data-stu-id="fa934-105">This tutorial shows you how to build an ASP.NET MVC 5 web application that enables users to log in using [OAuth 2.0](http://oauth.net/2/) with credentials from an external authentication provider, such as Facebook, Twitter, LinkedIn, Microsoft, or Google.</span></span> <span data-ttu-id="fa934-106">為了簡單起見，本教學課程著重于使用 Facebook 和 Google 的認證。</span><span class="sxs-lookup"><span data-stu-id="fa934-106">For simplicity, this tutorial focuses on working with credentials from Facebook and Google.</span></span>
> 
> <span data-ttu-id="fa934-107">在您的網站中啟用這些認證可提供顯著的優點，因為數百萬個使用者已經有這些外部提供者的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa934-107">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="fa934-108">如果您的網站不需要建立並記住一組新的認證，則這些使用者可能更傾向于註冊您的網站。</span><span class="sxs-lookup"><span data-stu-id="fa934-108">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span>
> 
> <span data-ttu-id="fa934-109">另請參閱 [使用 SMS 和電子郵件 Two-Factor 驗證來 ASP.NET MVC 5 應用程式](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="fa934-109">See also [ASP.NET MVC 5 app with SMS and email Two-Factor Authentication](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).</span></span>
> 
> <span data-ttu-id="fa934-110">本教學課程也會說明如何新增使用者的設定檔資料，以及如何使用成員資格 API 來新增角色。</span><span class="sxs-lookup"><span data-stu-id="fa934-110">The tutorial also shows how to add profile data for the user, and how to use the Membership API to add roles.</span></span> <span data-ttu-id="fa934-111">本教學課程由 [Rick Anderson](https://blogs.msdn.com/rickAndy) 撰寫 ( 請在 Twitter 上關注我： [@RickAndMSFT](https://twitter.com/RickAndMSFT) ) 。</span><span class="sxs-lookup"><span data-stu-id="fa934-111">This tutorial was written by [Rick Anderson](https://blogs.msdn.com/rickAndy) ( Please follow me on Twitter: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).</span></span>

<a id="start"></a>
## <a name="getting-started"></a><span data-ttu-id="fa934-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="fa934-112">Getting Started</span></span>

<span data-ttu-id="fa934-113">從安裝和[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)[執行適用于 Web 或 Visual Studio 2013 的 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058)開始。</span><span class="sxs-lookup"><span data-stu-id="fa934-113">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="fa934-114">安裝 Visual Studio [2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390521) 版本。</span><span class="sxs-lookup"><span data-stu-id="fa934-114">Install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher.</span></span> <span data-ttu-id="fa934-115">如需 Dropbox、GitHub、Linkedin、Instagram、Buffer、Salesforce、串流、Stack Exchange、Tripit、Twitch、Twitter、Yahoo！等的說明，請參閱此 [範例專案](https://github.com/matthewdunsdon/oauthforaspnet)。</span><span class="sxs-lookup"><span data-stu-id="fa934-115">For help with Dropbox, GitHub, Linkedin, Instagram, Buffer, Salesforce, STEAM, Stack Exchange, Tripit, Twitch, Twitter, Yahoo!, and more, see this [sample project](https://github.com/matthewdunsdon/oauthforaspnet).</span></span>

> [!NOTE]
> <span data-ttu-id="fa934-116">您必須安裝 Visual Studio [2013 Update 3 或更新](https://go.microsoft.com/fwlink/?LinkId=390521) 版本，才能使用 Google OAuth 2，並在本機進行無 SSL 警告的調試。</span><span class="sxs-lookup"><span data-stu-id="fa934-116">You must install Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) or higher to use Google OAuth 2 and to debug locally without SSL warnings.</span></span>

<span data-ttu-id="fa934-117">按一下 [**開始**] 頁面中的 [**新增專案**]，或者，您可以使用功能表**並選取 [** 檔案]，然後選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-117">Click **New Project** from the **Start** page, or you can use the menu and select **File**, and then **New Project**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a><span data-ttu-id="fa934-118">建立您的第一個應用程式</span><span class="sxs-lookup"><span data-stu-id="fa934-118">Creating Your First Application</span></span>

<span data-ttu-id="fa934-119">按一下 [ **新增專案**]，然後選取左側的 [ **Visual c #** ]、[ **Web** ]，然後選取 [ **ASP.NET web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-119">Click **New Project**, then select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="fa934-120">將您的專案命名為 "MvcAuth"，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="fa934-120">Name your project "MvcAuth" and then click **OK**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

<span data-ttu-id="fa934-121">在 [ **新增 ASP.NET 專案** ] 對話方塊中，按一下 [ **MVC**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-121">In the **New ASP.NET Project** dialog, click **MVC**.</span></span> <span data-ttu-id="fa934-122">如果驗證不是 **個別的使用者帳戶**，請按一下 [ **變更驗證** ] 按鈕，然後選取 [ **個別使用者帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-122">If the Authentication is not **Individual User Accounts**, click the **Change Authentication** button and select **Individual User Accounts**.</span></span> <span data-ttu-id="fa934-123">藉由檢查 **雲端中的主機**，應用程式很容易就能裝載在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="fa934-123">By checking **Host in the cloud**, the app will be very easy to host in Azure.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

<span data-ttu-id="fa934-124">如果您在 **雲端中選取 [主機**]，請完成 [設定] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fa934-124">If you selected **Host in the cloud**, complete the configure dialog.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a><span data-ttu-id="fa934-125">使用 NuGet 更新至最新的 OWIN 中介軟體</span><span class="sxs-lookup"><span data-stu-id="fa934-125">Use NuGet to update to the latest OWIN middleware</span></span>

<span data-ttu-id="fa934-126">使用 NuGet 套件管理員來更新 [OWIN 中介軟體](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="fa934-126">Use the NuGet package manager to update the [OWIN middleware](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md).</span></span> <span data-ttu-id="fa934-127">選取左側功能表中的 [ **更新** ]。</span><span class="sxs-lookup"><span data-stu-id="fa934-127">Select **Updates** in the left menu.</span></span> <span data-ttu-id="fa934-128">您可以按一下 [ **全部更新** ] 按鈕，也可以搜尋 (下一個影像) 所示的 OWIN 套件：</span><span class="sxs-lookup"><span data-stu-id="fa934-128">You can click on the **Update All** button or you can search for only OWIN packages (shown in the next image):</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

<span data-ttu-id="fa934-129">在下圖中，只會顯示 OWIN 套件：</span><span class="sxs-lookup"><span data-stu-id="fa934-129">In the image below, only OWIN packages are shown:</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

<span data-ttu-id="fa934-130">從封裝管理員主控台 (PMC) 中，您可以輸入 `Update-Package` 命令來更新所有套件。</span><span class="sxs-lookup"><span data-stu-id="fa934-130">From the Package Manager Console (PMC), you can enter the `Update-Package` command, which will update all packages.</span></span>

<span data-ttu-id="fa934-131">按 **f5** 或 **Ctrl + f5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-131">Press **F5** or **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="fa934-132">在下圖中，埠號碼為1234。</span><span class="sxs-lookup"><span data-stu-id="fa934-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="fa934-133">當您執行應用程式時，您會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="fa934-133">When you run the application, you'll see a different port number.</span></span>

<span data-ttu-id="fa934-134">視瀏覽器視窗的大小而定，您可能需要按一下流覽圖示來查看 [ **首頁**]、[ **關於**] **、**[ **註冊** ] 和 [ **登入** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="fa934-134">Depending on the size of your browser window, you might need to click the navigation icon to see the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a><span data-ttu-id="fa934-135">在專案中設定 SSL</span><span class="sxs-lookup"><span data-stu-id="fa934-135">Setting up SSL in the Project</span></span>

<span data-ttu-id="fa934-136">若要連線至驗證提供者（例如 Google 和 Facebook），您必須將 IIS-Express 設定為使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="fa934-136">To connect to authentication providers like Google and Facebook, you will need to set up IIS-Express to use SSL.</span></span> <span data-ttu-id="fa934-137">請務必在登入後繼續使用 SSL，而不要回傳至 HTTP，而您的登入 cookie 就像您的使用者名稱和密碼一樣是秘密，而不使用 SSL，則會以純文字方式透過網路傳送。</span><span class="sxs-lookup"><span data-stu-id="fa934-137">It's important to keep using SSL after login and not drop back to HTTP, your login cookie is just as secret as your username and password, and without using SSL you're sending it in clear-text across the wire.</span></span> <span data-ttu-id="fa934-138">此外，您已經花時間執行交握，並保護通道 (這是在執行 MVC 管線之前，使 HTTPS 比 HTTP) 慢很多的情況，因此在您登入之後重新導向回 HTTP，並不會讓目前的要求或未來的要求速度變得更快。</span><span class="sxs-lookup"><span data-stu-id="fa934-138">Besides, you've already taken the time to perform the handshake and secure the channel (which is the bulk of what makes HTTPS slower than HTTP) before the MVC pipeline is run, so redirecting back to HTTP after you're logged in won't make the current request or future requests much faster.</span></span>

1. <span data-ttu-id="fa934-139">在 **方案總管**中，按一下 [ **MvcAuth** ] 專案。</span><span class="sxs-lookup"><span data-stu-id="fa934-139">In **Solution Explorer**, click the **MvcAuth** project.</span></span>
2. <span data-ttu-id="fa934-140">按 F4 鍵以顯示專案屬性。</span><span class="sxs-lookup"><span data-stu-id="fa934-140">Hit the F4 key to show the project properties.</span></span> <span data-ttu-id="fa934-141">或者，您可以從 [ **View** ] 功能表選取 [ **屬性視窗]**。</span><span class="sxs-lookup"><span data-stu-id="fa934-141">Alternatively, from the **View** menu you can select **Properties Window**.</span></span>
3. <span data-ttu-id="fa934-142">將 **已啟用的 SSL** 變更為 True。</span><span class="sxs-lookup"><span data-stu-id="fa934-142">Change **SSL Enabled** to True.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. <span data-ttu-id="fa934-143">複製 SSL URL (這會是 `https://localhost:44300/` ，除非您已建立其他 ssl 專案) 。</span><span class="sxs-lookup"><span data-stu-id="fa934-143">Copy the SSL URL (which will be `https://localhost:44300/` unless you've created other SSL projects).</span></span>
5. <span data-ttu-id="fa934-144">在 **方案總管**中，以滑鼠右鍵按一下 **MvcAuth** 專案，然後選取 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-144">In **Solution Explorer**, right click the **MvcAuth** project and select **Properties**.</span></span>
6. <span data-ttu-id="fa934-145">選取 [ **Web** ] 索引標籤，然後將 SSL URL 貼到 [ **專案 URL** ] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="fa934-145">Select the **Web** tab, and then paste the SSL URL into the **Project Url** box.</span></span> <span data-ttu-id="fa934-146">將檔案儲存 (Ctl + S) 。</span><span class="sxs-lookup"><span data-stu-id="fa934-146">Save the file (Ctl+S).</span></span> <span data-ttu-id="fa934-147">您將需要此 URL 來設定 Facebook 和 Google 驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-147">You will need this URL to configure Facebook and Google authentication apps.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. <span data-ttu-id="fa934-148">將 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 屬性新增至 `Home` 控制器，要求所有要求都必須使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="fa934-148">Add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) attribute to the `Home` controller to require all requests must use HTTPS.</span></span> <span data-ttu-id="fa934-149">更安全的方法是將 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 篩選器新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-149">A more secure approach is to add the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter to the application.</span></span> <span data-ttu-id="fa934-150">請參閱教學課程中的「 &quot; 使用 SSL 保護應用程式和授權屬性」一節，以 &quot; [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="fa934-150">See the section &quot;Protect the Application with SSL and the Authorize Attribute&quot; in my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="fa934-151">首頁控制器的一部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="fa934-151">A portion of the Home controller is shown below.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. <span data-ttu-id="fa934-152">按 CTRL+F5 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-152">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="fa934-153">如果您已安裝憑證，您可以略過本節的其餘部分，並跳至 [建立 OAuth 2 的 Google 應用程式，並將應用程式連接到專案](#goog)，否則請遵循指示來信任 IIS Express 所產生的自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="fa934-153">If you've installed the certificate in the past, you can skip the rest of this section and jump to [Creating a Google app for OAuth 2 and connecting the app to the project](#goog), otherwise, follow the instructions to trust the self-signed certificate that IIS Express has generated.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. <span data-ttu-id="fa934-154">閱讀 [ **安全性警告** ] 對話方塊，如果您想要安裝代表 localhost 的憑證，請按一下 [ **是]** 。</span><span class="sxs-lookup"><span data-stu-id="fa934-154">Read the **Security Warning** dialog and then click **Yes** if you want to install the certificate representing localhost.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. <span data-ttu-id="fa934-155">IE 顯示 *首頁* ，沒有出現 SSL 警告。</span><span class="sxs-lookup"><span data-stu-id="fa934-155">IE shows the *Home* page and there are no SSL warnings.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. <span data-ttu-id="fa934-156">Google Chrome 也接受憑證，並且會顯示 HTTPS 內容而不顯示警告。</span><span class="sxs-lookup"><span data-stu-id="fa934-156">Google Chrome also accepts the certificate and will show HTTPS content without a warning.</span></span> <span data-ttu-id="fa934-157">Firefox 使用自己的憑證存放區，因此會顯示警告。</span><span class="sxs-lookup"><span data-stu-id="fa934-157">Firefox uses its own certificate store, so it will display a warning.</span></span> <span data-ttu-id="fa934-158">針對我們的應用程式，您可以放心地按一下 **我瞭解的風險**。</span><span class="sxs-lookup"><span data-stu-id="fa934-158">For our application you can safely click **I Understand the Risks**.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a><span data-ttu-id="fa934-159">建立適用于 OAuth 2 的 Google app，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="fa934-159">Creating a Google app for OAuth 2 and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="fa934-160">如需目前的 Google OAuth 指示，請參閱 [在 ASP.NET Core 中設定 Google 驗證](/aspnet/core/security/authentication/social/google-logins)。</span><span class="sxs-lookup"><span data-stu-id="fa934-160">For current Google OAuth instructions, see [Configuring Google authentication in ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).</span></span>

1. <span data-ttu-id="fa934-161">瀏覽至 [Google Developers Console](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="fa934-161">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span>
2. <span data-ttu-id="fa934-162">如果您之前尚未建立專案，請在左側索引標籤中選取 [ **認證** ]，然後選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-162">If you haven't created a project before, select **Credentials** in the left tab, and then select **Create**.</span></span>
3. <span data-ttu-id="fa934-163">在左側索引標籤中，按一下 [ **認證**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-163">In the left tab, click **Credentials**.</span></span>
4. <span data-ttu-id="fa934-164">按一下 [ **建立認證** ]，然後按一下 [ **OAUTH 用戶端識別碼**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-164">Click **Create credentials** then **OAuth client ID**.</span></span> 

    1. <span data-ttu-id="fa934-165">在 [ **建立用戶端識別碼** ] 對話方塊中，保留應用程式類型的預設 **Web 應用程式** 。</span><span class="sxs-lookup"><span data-stu-id="fa934-165">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
    2. <span data-ttu-id="fa934-166">將 **授權的 JavaScript** 來源設定為您在上面使用的 ssl URL (`https://localhost:44300/` 除非您已建立其他 ssl 專案) </span><span class="sxs-lookup"><span data-stu-id="fa934-166">Set the **Authorized JavaScript** origins to the SSL URL you used above (`https://localhost:44300/` unless you've created other SSL projects)</span></span>
    3. <span data-ttu-id="fa934-167">將授權的重新 **導向 URI** 設定為：</span><span class="sxs-lookup"><span data-stu-id="fa934-167">Set the **Authorized redirect URI** to:</span></span>  
         `https://localhost:44300/signin-google`
5. <span data-ttu-id="fa934-168">按一下 [OAuth 同意畫面] 功能表項目，然後設定您的電子郵件地址和產品名稱。</span><span class="sxs-lookup"><span data-stu-id="fa934-168">Click the OAuth Consent screen menu item, then set your email address and product name.</span></span> <span data-ttu-id="fa934-169">當您完成表單時，請按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-169">When you have completed the form click **Save**.</span></span>
6. <span data-ttu-id="fa934-170">按一下 [程式庫] 功能表項目、搜尋 **Google + API**、按一下該專案，然後按 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="fa934-170">Click the Library menu item, search **Google+ API**, click on it then press Enable.</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   <span data-ttu-id="fa934-171">下圖顯示已啟用的 Api。</span><span class="sxs-lookup"><span data-stu-id="fa934-171">The image below shows the enabled APIs.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. <span data-ttu-id="fa934-172">從 Google Api API 管理員前往 [ **認證** ] 索引標籤，以取得 **用戶端識別碼**。</span><span class="sxs-lookup"><span data-stu-id="fa934-172">From the Google APIs API Manager, visit the **Credentials** tab to obtain the **Client ID**.</span></span> <span data-ttu-id="fa934-173">下載以儲存具有應用程式秘密的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa934-173">Download to save a JSON file with application secrets.</span></span> <span data-ttu-id="fa934-174">將**ClientId**和**ClientSecret**複製並貼到 `UseGoogleAuthentication` *App_Start*資料夾的*Startup.Auth.cs*檔中找到的方法。</span><span class="sxs-lookup"><span data-stu-id="fa934-174">Copy and paste the **ClientId** and **ClientSecret** into the `UseGoogleAuthentication` method found in the *Startup.Auth.cs* file in the *App_Start* folder.</span></span> <span data-ttu-id="fa934-175">以下顯示的 **ClientId** 和 **ClientSecret** 值為範例，無法運作。</span><span class="sxs-lookup"><span data-stu-id="fa934-175">The **ClientId** and **ClientSecret** values shown below are samples and don't work.</span></span>

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > <span data-ttu-id="fa934-176">安全性-永不將機密資料儲存在您的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="fa934-176">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="fa934-177">系統會將帳戶和認證新增至上述程式碼，以保持範例的簡易。</span><span class="sxs-lookup"><span data-stu-id="fa934-177">The account and credentials are added to the code above to keep the sample simple.</span></span> <span data-ttu-id="fa934-178">請參閱 [將密碼和其他機密資料部署至 ASP.NET 和 Azure App Service 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="fa934-178">See [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).</span></span>
8. <span data-ttu-id="fa934-179">按 **CTRL + F5** 來建立並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-179">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="fa934-180">按一下 [登入] \*\*\*\* 連結。</span><span class="sxs-lookup"><span data-stu-id="fa934-180">Click the **Log in** link.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. <span data-ttu-id="fa934-181">在 [ **使用其他服務登入**] 底下，按一下 [ **Google**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-181">Under **Use another service to log in**, click **Google**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > <span data-ttu-id="fa934-182">如果您錯過上述任何步驟，則會收到 HTTP 401 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa934-182">If you miss any of the steps above you will get a HTTP 401 error.</span></span> <span data-ttu-id="fa934-183">重新檢查您上述的步驟。</span><span class="sxs-lookup"><span data-stu-id="fa934-183">Recheck your steps above.</span></span> <span data-ttu-id="fa934-184">如果遺漏必要的設定 (例如 **產品名稱**) ，請新增遺失的專案並儲存;驗證可能需要幾分鐘的時間才能運作。</span><span class="sxs-lookup"><span data-stu-id="fa934-184">If you miss a required setting (for example **product name**), add the missing item and save; it can take a few minutes for authentication to work.</span></span>
10. <span data-ttu-id="fa934-185">系統會將您重新導向至您將在其中輸入認證的 Google 網站。</span><span class="sxs-lookup"><span data-stu-id="fa934-185">You will be redirected to the Google site where you will enter your credentials.</span></span>   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. <span data-ttu-id="fa934-186">輸入認證後，系統便會提示您提供權限給剛建立的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fa934-186">After you enter your credentials, you will be prompted to give permissions to the web application you just created:</span></span>
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. <span data-ttu-id="fa934-187">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="fa934-187">Click **Accept**.</span></span> <span data-ttu-id="fa934-188">您現在會重新導向回到 MvcAuth 應用程式的 [ **註冊** ] 頁面，您可以在其中註冊 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa934-188">You will now be redirected back to the **Register** page of the MvcAuth application where you can register your Google account.</span></span> <span data-ttu-id="fa934-189">您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。</span><span class="sxs-lookup"><span data-stu-id="fa934-189">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="fa934-190">按一下 [註冊] 。</span><span class="sxs-lookup"><span data-stu-id="fa934-190">Click **Register**.</span></span>  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a><span data-ttu-id="fa934-191">在 Facebook 中建立應用程式，並將應用程式連接到專案</span><span class="sxs-lookup"><span data-stu-id="fa934-191">Creating the app in Facebook and connecting the app to the project</span></span>

> [!WARNING]
> <span data-ttu-id="fa934-192">如需目前的 Facebook OAuth2 驗證指示，請參閱設定 [facebook 驗證](/aspnet/core/security/authentication/social/facebook-logins)</span><span class="sxs-lookup"><span data-stu-id="fa934-192">For current Facebook OAuth2 authentication instructions, see [Configuring Facebook authentication](/aspnet/core/security/authentication/social/facebook-logins)</span></span>

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a><span data-ttu-id="fa934-193">檢查成員資格資料</span><span class="sxs-lookup"><span data-stu-id="fa934-193">Examine the Membership Data</span></span>

<span data-ttu-id="fa934-194">在 [ **View** ] 功能表中，按一下 [ **伺服器總管**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-194">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

<span data-ttu-id="fa934-195">展開 [ \*\*DefaultConnection] (MvcAuth) \*\*，展開 [ **資料表]**，以滑鼠右鍵按一下 **AspNetUsers** ，然後按一下 [ **顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-195">Expand **DefaultConnection (MvcAuth)**, expand **Tables**, right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![aspnetusers 資料表資料](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a><span data-ttu-id="fa934-197">將設定檔資料新增至使用者類別</span><span class="sxs-lookup"><span data-stu-id="fa934-197">Adding Profile Data to the User Class</span></span>

<span data-ttu-id="fa934-198">在本節中，您會在註冊期間將出生日期和首頁城鎮新增至使用者資料，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="fa934-198">In this section you'll add birth date and home town to the user data during registration, as shown in the following image.</span></span>

![使用房屋城鎮和 Bday 的 reg](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

<span data-ttu-id="fa934-200">開啟 *Models\IdentityModels.cs* 檔案，並新增出生日期和主城鎮屬性：</span><span class="sxs-lookup"><span data-stu-id="fa934-200">Open the *Models\IdentityModels.cs* file and add birth date and home town properties:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

<span data-ttu-id="fa934-201">開啟 *Models\AccountViewModels.cs* 檔案，並在中開啟 [設定出生日期] 和 [首頁城鎮] 屬性 `ExternalLoginConfirmationViewModel` 。</span><span class="sxs-lookup"><span data-stu-id="fa934-201">Open the *Models\AccountViewModels.cs* file and the set birth date and home town properties in `ExternalLoginConfirmationViewModel`.</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

<span data-ttu-id="fa934-202">開啟 *Controllers\AccountController.cs* 檔案，並在動作方法中新增出生日期和主城鎮的程式碼， `ExternalLoginConfirmation` 如下所示：</span><span class="sxs-lookup"><span data-stu-id="fa934-202">Open the *Controllers\AccountController.cs* file and add code for birth date and home town in the `ExternalLoginConfirmation` action method as shown:</span></span>

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

<span data-ttu-id="fa934-203">將出生日期和首頁城鎮新增至 *Views\Account\ExternalLoginConfirmation.cshtml* 檔案：</span><span class="sxs-lookup"><span data-stu-id="fa934-203">Add birth date and home town to the *Views\Account\ExternalLoginConfirmation.cshtml* file:</span></span>

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

<span data-ttu-id="fa934-204">刪除成員資格資料庫，讓您可以再次向應用程式註冊您的 Facebook 帳戶，並確認您可以加入新的出生日期和主城鎮設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="fa934-204">Delete the membership database so you can again register your Facebook account with your application and verify you can add the new birth date and home town profile information.</span></span>

<span data-ttu-id="fa934-205">在 **方案總管**中，按一下 **[顯示所有** 檔案] 圖示，然後以滑鼠右鍵按一下 [ \*新增 \_ Data\aspnet-MvcAuth- &lt; dateStamp &gt; \* ]，再按一下 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-205">From **Solution Explorer**, click the **Show All Files** icon, then right click *Add\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;.mdf* and click **Delete**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

<span data-ttu-id="fa934-206">從 [ **工具** ] 功能表按一下 [ **NuGet 套件**管理員]，然後按一下 [ **封裝管理員主控台** ] (PMC) 。</span><span class="sxs-lookup"><span data-stu-id="fa934-206">From the **Tools** menu, click **NuGet Package Manger**, then click **Package Manager Console** (PMC).</span></span> <span data-ttu-id="fa934-207">在 PMC 中輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="fa934-207">Enter the following commands in the PMC.</span></span>

1. <span data-ttu-id="fa934-208">Enable-Migrations</span><span class="sxs-lookup"><span data-stu-id="fa934-208">Enable-Migrations</span></span>
2. <span data-ttu-id="fa934-209">Add-Migration Init</span><span class="sxs-lookup"><span data-stu-id="fa934-209">Add-Migration Init</span></span>
3. <span data-ttu-id="fa934-210">Update-Database</span><span class="sxs-lookup"><span data-stu-id="fa934-210">Update-Database</span></span>

<span data-ttu-id="fa934-211">執行應用程式，並使用 FaceBook 和 Google 登入並註冊某些使用者。</span><span class="sxs-lookup"><span data-stu-id="fa934-211">Run the application and use FaceBook and Google to log in and register some users.</span></span>

## <a name="examine-the-membership-data"></a><span data-ttu-id="fa934-212">檢查成員資格資料</span><span class="sxs-lookup"><span data-stu-id="fa934-212">Examine the Membership Data</span></span>

<span data-ttu-id="fa934-213">在 [ **View** ] 功能表中，按一下 [ **伺服器總管**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-213">In the **View** menu, click **Server Explorer**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

<span data-ttu-id="fa934-214">以滑鼠右鍵按一下 **AspNetUsers** ，然後按一下 [ **顯示資料表資料**]。</span><span class="sxs-lookup"><span data-stu-id="fa934-214">Right click **AspNetUsers** and click **Show Table Data**.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

<span data-ttu-id="fa934-215">`HomeTown`和 `BirthDate` 欄位如下所示。</span><span class="sxs-lookup"><span data-stu-id="fa934-215">The `HomeTown` and `BirthDate` fields are shown below.</span></span>

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a><span data-ttu-id="fa934-216">登出您的應用程式，並使用其他帳戶登入</span><span class="sxs-lookup"><span data-stu-id="fa934-216">Logging off your App and Logging in With Another Account</span></span>

<span data-ttu-id="fa934-217">如果您使用 Facebook 登入應用程式，然後登出再嘗試使用不同的 Facebook 帳戶登入 (使用相同的瀏覽器) ，您將會立即登入先前使用的 Facebook 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa934-217">If you log on to your app with Facebook,, and then log out and try to log in again with a different Facebook account (using the same browser), you will be immediately logged in to the previous Facebook account you used.</span></span> <span data-ttu-id="fa934-218">若要使用其他帳戶，您需要流覽至 Facebook 並登出于 Facebook。</span><span class="sxs-lookup"><span data-stu-id="fa934-218">In order to use another account, you need to navigate to Facebook and log out at Facebook.</span></span> <span data-ttu-id="fa934-219">相同的規則適用于其他任何協力廠商驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="fa934-219">The same rule applies to any other 3rd party authentication provider.</span></span> <span data-ttu-id="fa934-220">或者，您可以使用不同的瀏覽器，以其他帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="fa934-220">Alternatively, you can log in with another account by using a different browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa934-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa934-221">Next Steps</span></span>

<span data-ttu-id="fa934-222">請參閱 OWIN by >jerrie Pelser 的 [yahoo 和 Linkedin OAuth 安全性提供者簡介](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) ，以瞭解 Yahoo 和 linkedin 的指示。</span><span class="sxs-lookup"><span data-stu-id="fa934-222">See [Introducing the Yahoo and LinkedIn OAuth security providers for OWIN](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) by Jerrie Pelser for Yahoo and LinkedIn instructions.</span></span> <span data-ttu-id="fa934-223">請參閱 >jerrie 的 ASP.NET MVC 5 的很好社交登入按鈕，以取得啟用社交登入按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa934-223">See Jerrie's Pretty social login buttons for ASP.NET MVC 5 to get enable social login buttons.</span></span>

<span data-ttu-id="fa934-224">遵循教學課程， [使用 auth 和 SQL DB 建立 ASP.NET MVC 應用程式，並部署到 Azure App Service，以繼續進行](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)本教學課程，並顯示下列內容：</span><span class="sxs-lookup"><span data-stu-id="fa934-224">Follow my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), which continues this tutorial and shows the following:</span></span>

1. <span data-ttu-id="fa934-225">如何將應用程式部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="fa934-225">How to deploy your app to Azure.</span></span>
2. <span data-ttu-id="fa934-226">如何使用角色保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-226">How to secure you app with roles.</span></span>
3. <span data-ttu-id="fa934-227">如何使用 [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) 和 [授權](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) 篩選來保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa934-227">How to secure your app with the [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) and [Authorize](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filters.</span></span>
4. <span data-ttu-id="fa934-228">如何使用成員資格 API 來新增使用者和角色。</span><span class="sxs-lookup"><span data-stu-id="fa934-228">How to use the membership API to add users and roles.</span></span>

<span data-ttu-id="fa934-229">請針對您喜歡本教學課程的方式以及我們可以改進的內容留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="fa934-229">Please leave feedback on how you liked this tutorial and what we could improve.</span></span> <span data-ttu-id="fa934-230">您也可以向我要求新 [的主題，告訴我如何使用程式碼](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。</span><span class="sxs-lookup"><span data-stu-id="fa934-230">You can also request new topics at [Show Me How With Code](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code).</span></span> <span data-ttu-id="fa934-231">您甚至可以要求及投票要新增至 ASP.NET 的新功能。</span><span class="sxs-lookup"><span data-stu-id="fa934-231">You can even ask for and vote on new features to be added to ASP.NET.</span></span> <span data-ttu-id="fa934-232">例如，您可以投票工具來 [建立及管理使用者和角色。](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span><span class="sxs-lookup"><span data-stu-id="fa934-232">For example, you can vote for a tool to [create and manage users and roles.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)</span></span>

<span data-ttu-id="fa934-233">如需 ASP.NET 外部驗證服務運作方式的良好說明，請參閱 Robert McMurray 的 [外部驗證服務](https://asp.net/web-api/overview/security/external-authentication-services)。</span><span class="sxs-lookup"><span data-stu-id="fa934-233">For an good explanation of how ASP.NET External Authentication Services work, see Robert McMurray's [External Authentication Services](https://asp.net/web-api/overview/security/external-authentication-services).</span></span> <span data-ttu-id="fa934-234">Robert 的文章也會詳細說明如何啟用 Microsoft 和 Twitter 驗證。</span><span class="sxs-lookup"><span data-stu-id="fa934-234">Robert's article also goes into detail in enabling Microsoft and Twitter authentication.</span></span> <span data-ttu-id="fa934-235">Tom Dykstra 的絕佳 [EF/MVC 教學](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 課程說明如何使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="fa934-235">Tom Dykstra's excellent [EF/MVC tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) shows how to work with the Entity Framework.</span></span>
