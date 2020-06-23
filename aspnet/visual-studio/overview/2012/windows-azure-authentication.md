---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 驗證 |Microsoft Docs
author: Rick-Anderson
description: 適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具可讓您輕鬆地針對 Windows Azure 網站上託管的 web 應用程式啟用驗證 .。。
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ab75218cbe3817c14a064e9816388aebc7e431f7
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240562"
---
# <a name="windows-azure-authentication"></a><span data-ttu-id="2e911-103">Windows Azure 驗證</span><span class="sxs-lookup"><span data-stu-id="2e911-103">Windows Azure Authentication</span></span>

<span data-ttu-id="2e911-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2e911-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="2e911-105">適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具可讓您輕鬆地針對[Windows Azure 網站](https://www.windowsazure.com/home/features/web-sites/)上託管的 web 應用程式啟用驗證。</span><span class="sxs-lookup"><span data-stu-id="2e911-105">Microsoft ASP.NET tools for Windows Azure Active Directory makes it simple to enable authentication for web applications hosted on [Windows Azure Web Sites](https://www.windowsazure.com/home/features/web-sites/).</span></span> <span data-ttu-id="2e911-106">您可以使用 Windows Azure 驗證，向您的組織驗證 Office 365 使用者、從內部部署 Active Directory 同步處理的公司帳戶，或在您自己的自訂 Windows Azure Active Directory 網域中建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="2e911-106">You can use Windows Azure Authentication to authenticate Office 365 users from your organization, corporate accounts synced from your on-premise Active Directory or users created in your own custom Windows Azure Active Directory domain.</span></span> <span data-ttu-id="2e911-107">啟用 Windows Azure 驗證會將您的應用程式設定為使用單一[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租使用者來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="2e911-107">Enabling Windows Azure Authentication configures your application to authenticate users using a single [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) tenant.</span></span>
>
> <span data-ttu-id="2e911-108">雲端服務中的 web 角色不支援 ASP.NET Windows Azure 驗證工具，但我們計畫在未來的版本中執行此操作。</span><span class="sxs-lookup"><span data-stu-id="2e911-108">The ASP.NET Windows Azure Authentication tool is not supported for web roles in a cloud service but we plan to do so in a future release.</span></span> <span data-ttu-id="2e911-109">Windows Azure web 角色支援[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) （WIF）。</span><span class="sxs-lookup"><span data-stu-id="2e911-109">[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) is supported in Windows Azure web roles.</span></span>
>
> <span data-ttu-id="2e911-110">如需如何設定內部部署 Active Directory 與 Windows Azure Active Directory 租使用者之間同步處理的詳細資訊，請參閱[使用 AD FS 2.0 來執行和管理單一登入](https://technet.microsoft.com/library/jj205462.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e911-110">For details on how to setup synchronization between your on-premise Active Directory and your Windows Azure Active Directory tenant please see [Use AD FS 2.0 to implement and manage single sign-on](https://technet.microsoft.com/library/jj205462.aspx).</span></span>
>
> <span data-ttu-id="2e911-111">Windows Azure Active Directory 目前以[免費預覽服務](https://azure.microsoft.com/free/dotnet/)的形式提供。</span><span class="sxs-lookup"><span data-stu-id="2e911-111">Windows Azure Active Directory is currently available as a [free preview service](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="requirements"></a><span data-ttu-id="2e911-112">需求：</span><span class="sxs-lookup"><span data-stu-id="2e911-112">Requirements:</span></span>

- <span data-ttu-id="2e911-113">Visual Studio 2012 或[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span><span class="sxs-lookup"><span data-stu-id="2e911-113">Visual Studio 2012 or [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)</span></span>
- <span data-ttu-id="2e911-114">適用于 Visual Studio Express 2012 的 Visual Studio 2012 或[Web 工具擴充](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)功能的[web 工具擴充](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)功能</span><span class="sxs-lookup"><span data-stu-id="2e911-114">[Web Tools Extensions for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) or [Web Tools Extensions for Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)</span></span>
- <span data-ttu-id="2e911-115">[適用于 windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或適用[于 Windows 的 Microsoft ASP.NET 工具 Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span><span class="sxs-lookup"><span data-stu-id="2e911-115">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) or [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)</span></span>

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a><span data-ttu-id="2e911-116">建立具有 Visual Studio 2012 的 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2e911-116">Create an ASP.NET Web Application with Visual Studio 2012</span></span>

<span data-ttu-id="2e911-117">您可以使用 Visual Studio 2012 建立任何 Web 應用程式，本教學課程會使用 ASP.NET MVC 內部網路範本。</span><span class="sxs-lookup"><span data-stu-id="2e911-117">You can create any Web Application with Visual Studio 2012, this tutorial uses the ASP.NET MVC intranet template.</span></span>

1. <span data-ttu-id="2e911-118">建立新的 ASP.NET MVC 4 內部網路應用程式，並接受所有預設值。</span><span class="sxs-lookup"><span data-stu-id="2e911-118">Create a new ASP.NET MVC 4 Intranet Application and accept all the defaults.</span></span> <span data-ttu-id="2e911-119">（它必須是**tra** net 中的，而不是 **&** net 專案中的）。</span><span class="sxs-lookup"><span data-stu-id="2e911-119">(It must be an In **tra** net and not In **ter** net project).</span></span>
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a><span data-ttu-id="2e911-120">啟用 Windows Azure 驗證（當您是原則的全域管理員時）</span><span class="sxs-lookup"><span data-stu-id="2e911-120">Enable Window Azure Authentication (When you are a Global Administrator of the Tenet)</span></span>

<span data-ttu-id="2e911-121">如果您沒有現有的 Windows Azure Active Directory 租使用者（例如，透過現有的 Office 365 帳戶），您可以註冊[新的 windows Azure Active Directory 帳戶](https://g.microsoftonline.com/0AX00en/5)來建立新的租使用者。</span><span class="sxs-lookup"><span data-stu-id="2e911-121">If you do not have an existing Windows Azure Active Directory tenant (For example, through an existing Office 365 account) you can create a new tenant by signing up for a [new Windows Azure Active Directory account](https://g.microsoftonline.com/0AX00en/5).</span></span>

1. <span data-ttu-id="2e911-122">從 [專案] 功能表中，選取 [**啟用 Windows Azure 驗證**]：</span><span class="sxs-lookup"><span data-stu-id="2e911-122">From the Project menu select **Enable Windows Azure Authentication**:</span></span>

   ![](windows-azure-authentication/_static/image2.png)

2. <span data-ttu-id="2e911-123">輸入 Windows Azure Active Directory 租使用者的網域（例如 contoso.onmicrosoft.com），然後按一下 [**啟用**]：</span><span class="sxs-lookup"><span data-stu-id="2e911-123">Enter the domain for your Windows Azure Active Directory tenant (for example, contoso.onmicrosoft.com) and click **Enable**:</span></span>

![](windows-azure-authentication/_static/image3.png)

3. <span data-ttu-id="2e911-124">在 [Web 驗證] 對話方塊中，以您的 Windows Azure Active Directory 租使用者的系統管理員身分登入：</span><span class="sxs-lookup"><span data-stu-id="2e911-124">In the Web Authentication dialog sign in as an administrator for your Windows Azure Active Directory tenant:</span></span>

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a><span data-ttu-id="2e911-125">以非系統管理員的原則啟用 Window Azure</span><span class="sxs-lookup"><span data-stu-id="2e911-125">Enable Window Azure by a non-administrator of the Tenet</span></span>

<span data-ttu-id="2e911-126">如果您沒有 Windows Azure Active Directory 租使用者的全域管理員許可權，您可以取消核取布建應用程式的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2e911-126">If you do not have Global Administrator privilege for your Windows Azure Active Directory tenant, you can uncheck the checkbox for provisioning the application.</span></span>

![](windows-azure-authentication/_static/image6.png)

<span data-ttu-id="2e911-127">對話方塊會顯示使用 Azure Active Directory 的原則布建應用程式時所需的 [**網域**]、[**應用程式主體識別碼**] 和 [**回復 URL** ]。</span><span class="sxs-lookup"><span data-stu-id="2e911-127">The dialog will display the **Domain**, **Application Principal Id** and **Reply URL** which are required for provisioning the application with an Azure Active Directory tenet.</span></span> <span data-ttu-id="2e911-128">您必須將此資訊提供給具有足夠許可權的使用者來布建應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e911-128">You need to give this information to someone who has sufficient privilege to provision the application.</span></span> <span data-ttu-id="2e911-129">如需如何使用 Cmdlet 來手動建立服務主體的詳細資訊，請參閱[如何搭配 Windows Azure Active Directory ASP.NET 應用程式執行單一登入](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)。</span><span class="sxs-lookup"><span data-stu-id="2e911-129">See[How to implement single sign-on with Windows Azure Active Directory - ASP.NET Application](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) for details on how to use cmdlet to create the service principal manually.</span></span>
<span data-ttu-id="2e911-130">成功布建應用程式之後，您可以按一下 **[繼續]，以選取的設定來更新 web.config**。</span><span class="sxs-lookup"><span data-stu-id="2e911-130">Once the application has been successfully provisioned, you can click on **Continue to update web.config with the selected settings**.</span></span> <span data-ttu-id="2e911-131">如果您想要在等候布建發生時繼續開發應用程式，您可以按一下 **[關閉]，以記住 [專案檔] 中的設定**。</span><span class="sxs-lookup"><span data-stu-id="2e911-131">If you want to continue developing the application while waiting for provisioning to happen, you can click **Close to remember the settings in project file**.</span></span> <span data-ttu-id="2e911-132">下次您叫用 [啟用 Windows Azure 驗證] 並取消核取 [布建] 核取方塊時，您會看到相同的設定，而且您可以按一下 [**繼續**]，然後按一下 [**在 web.config中套用這些設定**。</span><span class="sxs-lookup"><span data-stu-id="2e911-132">The next time you invoke Enable Windows Azure Authentication and uncheck the provisioning checkbox, you will see the same settings and you can click **Continue**, then click, **Apply these settings in web.config**.</span></span>

1. <span data-ttu-id="2e911-133">請等候您的應用程式設定為使用 windows Azure 驗證，並以 Windows Azure Active Directory 進行布建。</span><span class="sxs-lookup"><span data-stu-id="2e911-133">Wait while your application is configured for Windows Azure Authentication and provisioned with Windows Azure Active Directory.</span></span>
2. <span data-ttu-id="2e911-134">啟用應用程式的 Windows Azure 驗證之後，請按一下 [**關閉]：**</span><span class="sxs-lookup"><span data-stu-id="2e911-134">Once Windows Azure Authentication has been enabled for your application, click **Close:**</span></span>

    ![](windows-azure-authentication/_static/image7.png)
3. <span data-ttu-id="2e911-135">按 F5 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e911-135">Hit F5 to run your application.</span></span> <span data-ttu-id="2e911-136">您應該會自動重新導向至登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e911-136">You should automatically get redirected to login page.</span></span> <span data-ttu-id="2e911-137">使用目錄的 [原則] [使用者認證] 來登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e911-137">Use the directory tenet user credentials to login to the application..</span></span>

    ![](windows-azure-authentication/_static/image1.jpg)
4. <span data-ttu-id="2e911-138">因為您的應用程式目前使用自我簽署的測試憑證，所以您會收到來自瀏覽器的警告，指出憑證不是由受信任的憑證授權單位單位所發行。</span><span class="sxs-lookup"><span data-stu-id="2e911-138">Because your application is currently using a self-signed test certificate you will receive a warning from the browser that the certificate was not issued by a trusted certificate authority.</span></span>

    <span data-ttu-id="2e911-139">您可以按一下 [**繼續流覽此網站**]，安全地在本機開發期間忽略此警告：</span><span class="sxs-lookup"><span data-stu-id="2e911-139">This warning can be safely ignored during local development by clicking **Continue to this website:**</span></span>

    ![](windows-azure-authentication/_static/image8.png)
5. <span data-ttu-id="2e911-140">您現在已使用 Windows Azure 驗證成功登入您的應用程式！</span><span class="sxs-lookup"><span data-stu-id="2e911-140">You have now successfully logged in to your application using Windows Azure Authentication!</span></span>

    ![](windows-azure-authentication/_static/image2.jpg)

<span data-ttu-id="2e911-141">啟用 Windows Azure 驗證會對您的應用程式進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="2e911-141">Enabling Windows Azure authentication makes the following changes to your application:</span></span>

- <span data-ttu-id="2e911-142">已將反跨網站偽造要求（[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))）類別（*應用程式 \_ Start\AntiXsrfConfig.cs* ）新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="2e911-142">An Anti-Cross-Site Request Forgery ([CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))) class ( *App\_Start\AntiXsrfConfig.cs* ) is added to your project.</span></span>
- <span data-ttu-id="2e911-143">NuGet 套件 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 會新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="2e911-143">The NuGet packages `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` is added to your project.</span></span>
- <span data-ttu-id="2e911-144">您應用程式中的 windows Identity Foundation 設定會設定為接受來自您 Windows Azure Active Directory 租使用者的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="2e911-144">Windows Identity Foundation settings in your application will be configured to accept security tokens from your Windows Azure Active Directory tenant.</span></span> <span data-ttu-id="2e911-145">按一下下方影像，以查看對*Web.config*檔案所做變更的展開。</span><span class="sxs-lookup"><span data-stu-id="2e911-145">Click on the image below to see an expanded view of the changes made to the *Web.config* file.</span></span>

     ![](windows-azure-authentication/_static/image9.png)
- <span data-ttu-id="2e911-146">將會布建您的 Windows Azure Active Directory 租使用者中應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="2e911-146">A service principal for your application in your Windows Azure Active Directory tenant will be provisioned.</span></span>
- <span data-ttu-id="2e911-147">已啟用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="2e911-147">HTTPS is enabled.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="2e911-148">將應用程式部署至 Windows Azure</span><span class="sxs-lookup"><span data-stu-id="2e911-148">Deploy the application to Windows Azure</span></span>

<span data-ttu-id="2e911-149">如需完整指示，請參閱將[ASP.NET Web 應用程式部署至 Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)網站。</span><span class="sxs-lookup"><span data-stu-id="2e911-149">For complete instructions, see [Deploying an ASP.NET Web Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

<span data-ttu-id="2e911-150">若要將使用 Windows Azure 驗證的應用程式發行至 Azure 網站：</span><span class="sxs-lookup"><span data-stu-id="2e911-150">To publish an application using Windows Azure Authentication to an Azure Web Site:</span></span>

1. <span data-ttu-id="2e911-151">以滑鼠右鍵按一下您的應用程式，然後選取 [**發佈]：**</span><span class="sxs-lookup"><span data-stu-id="2e911-151">Right click on your application and select **Publish:**</span></span>

    ![](windows-azure-authentication/_static/image3.jpg)
2. <span data-ttu-id="2e911-152">從 [發行 Web] 對話方塊下載並匯入 Azure 網站的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="2e911-152">From the Publish Web dialog download and import a publishing profile for your Azure Web Site.</span></span>

    ![](windows-azure-authentication/_static/image4.jpg)
3. <span data-ttu-id="2e911-153">[**連接**] 索引標籤會顯示**目的地 URL** （應用程式的公開 url）。</span><span class="sxs-lookup"><span data-stu-id="2e911-153">The **Connection** tab shows the **Destination URL** (the public facing URL for your application).</span></span> <span data-ttu-id="2e911-154">按一下 [**驗證**連線] 以測試您的連接：</span><span class="sxs-lookup"><span data-stu-id="2e911-154">Click **Validate Connection** to test your connection:</span></span>

    ![](windows-azure-authentication/_static/image5.jpg)
4. <span data-ttu-id="2e911-155">如果您先前已發佈到這個 Azure 網站，請考慮勾選 [**移除目的地的其他**檔案] 設定，以確保您的應用程式能完全發行。</span><span class="sxs-lookup"><span data-stu-id="2e911-155">If you have published to this Azure Web Site previously consider checking the **Remove additional files at destination** setting to ensure your application publishes cleanly.</span></span> <span data-ttu-id="2e911-156">請注意，已選取 [**啟用 Windows Azure 驗證**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2e911-156">Notice the **Enable Windows Azure Authentication** check box is selected.</span></span>

    ![](windows-azure-authentication/_static/image10.png)
5. <span data-ttu-id="2e911-157">選擇性：在 [**預覽**] 索引標籤上，按一下 [**開始預覽**] 以查看已部署的檔案。</span><span class="sxs-lookup"><span data-stu-id="2e911-157">Optional: On the **Preview** tab click **Start Preview** to see the files deployed.</span></span>

    ![](windows-azure-authentication/_static/image6.jpg)
6. <span data-ttu-id="2e911-158">按一下 [**發佈]。**</span><span class="sxs-lookup"><span data-stu-id="2e911-158">Click **Publish.**</span></span>

    <span data-ttu-id="2e911-159">系統會提示您啟用目標主機的 Windows Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="2e911-159">You will be prompted to enable Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="2e911-160">按一下 [**啟用**] 以繼續：</span><span class="sxs-lookup"><span data-stu-id="2e911-160">Click **Enable** to continue:</span></span>

    ![](windows-azure-authentication/_static/image11.png)
7. <span data-ttu-id="2e911-161">輸入您的 Windows Azure Active Directory 租使用者的系統管理員認證：</span><span class="sxs-lookup"><span data-stu-id="2e911-161">Enter your administrator credentials for your Windows Azure Active Directory tenant:</span></span>

    ![](windows-azure-authentication/_static/image7.jpg)
8. <span data-ttu-id="2e911-162">成功發行應用程式之後，瀏覽器就會開啟發行的網站。</span><span class="sxs-lookup"><span data-stu-id="2e911-162">Once your application has been successfully published, a browser will open to the published web site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e911-163">在啟用目標主機的 Windows Azure 驗證之後，您的應用程式最多可能需要五分鐘（通常不會減少），才能完全布建 Windows Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="2e911-163">It may take up to five minutes (typically must less) for your application to be fully provisioned with Windows Azure Active Directory after enabling Windows Azure Authentication for the target host.</span></span> <span data-ttu-id="2e911-164">當您第一次執行應用程式時，如果收到錯誤 ACS50001：找不到名稱為 ' [領域] ' 的信賴憑證者，請稍候幾分鐘，然後再次嘗試執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e911-164">When you first run your application if you receive error ACS50001: Relying party with name ‘[realm]' was not found, then wait a few minutes and try running the application again.</span></span>
9. <span data-ttu-id="2e911-165">出現提示時，以使用者身分登入您的目錄：</span><span class="sxs-lookup"><span data-stu-id="2e911-165">When prompted, log in as a user in your directory:</span></span>

    ![](windows-azure-authentication/_static/image8.jpg)
10. <span data-ttu-id="2e911-166">您現在已使用 Windows Azure 驗證成功登入您的 Azure 託管應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e911-166">You have now successfully logged into your Azure hosted application using Windows Azure Authentication.</span></span>

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a><span data-ttu-id="2e911-167">已知問題</span><span class="sxs-lookup"><span data-stu-id="2e911-167">Known Issues</span></span>

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a><span data-ttu-id="2e911-168">使用 Windows Azure 驗證時以角色為基礎的授權失敗</span><span class="sxs-lookup"><span data-stu-id="2e911-168">Role-based authorization fails when using Windows Azure Authentication</span></span>

<span data-ttu-id="2e911-169">Windows Azure 驗證目前未提供必要的角色宣告，因此可以執行以角色為基礎的授權。</span><span class="sxs-lookup"><span data-stu-id="2e911-169">Windows Azure Authentication does not currently provide the necessary role claim so that role-based authorization can be performed.</span></span> <span data-ttu-id="2e911-170">已驗證使用者的角色必須以手動方式從 Windows Azure Active Directory 中取出。</span><span class="sxs-lookup"><span data-stu-id="2e911-170">The role of the authenticated user must be manually retrieved from Windows Azure Active Directory.</span></span>

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="2e911-171">流覽至具有 Windows Azure 驗證的應用程式會導致錯誤「ACS20016 登入使用者的網域（live.com）不符合此 STS 的任何允許網域」</span><span class="sxs-lookup"><span data-stu-id="2e911-171">Browsing to an application with Windows Azure Authentication results in the error "ACS20016 The domain of the logged in user (live.com) does not match any allowed domain of this STS"</span></span>

<span data-ttu-id="2e911-172">如果您已經登入 Microsoft 帳戶（例如 hotmail.com、live.com、outlook.com），而您嘗試存取已啟用 Windows Azure 驗證的應用程式，您可能會收到400錯誤回應，因為 Windows Azure Active Directory 無法辨識 Microsoft 帳戶的網域。</span><span class="sxs-lookup"><span data-stu-id="2e911-172">If you are already logged in to a Microsoft Account (for example hotmail.com, live.com, outlook.com) and you attempt to access an application that has enabled Windows Azure Authentication you may get a 400 error response because the domain of your Microsoft Account is not recognized by Windows Azure Active Directory.</span></span> <span data-ttu-id="2e911-173">若要登入應用程式，請先從您的 Microsoft 帳戶登出。</span><span class="sxs-lookup"><span data-stu-id="2e911-173">To log into the application, log out from your Microsoft Account first.</span></span>

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a><span data-ttu-id="2e911-174">登入已啟用 Windows Azure 驗證的應用程式，而非 [無] 的 X509certificatevalidationmode.custom 會導致 accounts.accesscontrol.windows.net 憑證的憑證驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="2e911-174">Logging into an application with Windows Azure Authentication enabled and a X509CertificateValidationMode other than None results in certificate validation errors for the accounts.accesscontrol.windows.net certificate</span></span>

<span data-ttu-id="2e911-175">憑證驗證不是必要的，應保持停用。</span><span class="sxs-lookup"><span data-stu-id="2e911-175">Certificate validation is not required and should be left disabled.</span></span> <span data-ttu-id="2e911-176">此簽發者憑證的指紋會由 WSFederationAuthenticationModule 驗證。</span><span class="sxs-lookup"><span data-stu-id="2e911-176">The thumbprint of the issuer certificate is validated by the WSFederationAuthenticationModule.</span></span>

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a><span data-ttu-id="2e911-177">嘗試啟用 Windows Azure 驗證時，[Web 驗證] 對話方塊會顯示錯誤「ACS20016：登入使用者（contoso.onmicrosoft.com）的網域不符合此 STS 的任何允許網域」。</span><span class="sxs-lookup"><span data-stu-id="2e911-177">When attempting to enable Windows Azure Authentication the Web Authentication dialog shows the error "ACS20016: The domain of the logged in user (contoso.onmicrosoft.com) does not match any allowed domain of this STS."</span></span>

<span data-ttu-id="2e911-178">當您先前使用不同的 Windows Azure Active Directory 帳戶從相同的 Visual Studio 程式內成功登入時，可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="2e911-178">You may see this error when you have previously successfully logged in using a different Windows Azure Active Directory account from within the same Visual Studio process.</span></span> <span data-ttu-id="2e911-179">從指定的帳號登出，或 Visual Studio 重新開機。</span><span class="sxs-lookup"><span data-stu-id="2e911-179">Log out from the specified account or restart Visual Studio.</span></span> <span data-ttu-id="2e911-180">如果您先前已登入並選取 [讓我保持登入] 選項，您可能需要清除瀏覽器 cookie。</span><span class="sxs-lookup"><span data-stu-id="2e911-180">If you previously logged in and selected the option to "Keep me signed in" then you may need to clear your browser cookies.</span></span>

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a><span data-ttu-id="2e911-181">ACS20012：要求不是有效的 WS-同盟通訊協定訊息</span><span class="sxs-lookup"><span data-stu-id="2e911-181">ACS20012: The request is not a valid WS-Federation protocol message</span></span>

<span data-ttu-id="2e911-182">如果您已經使用一些其他 Microsoft 識別碼登入其中一個 Azure 服務，就可能發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="2e911-182">This can happen if you are already logged in with some other Microsoft ID to one of the Azure services.</span></span> <span data-ttu-id="2e911-183">使用私用瀏覽器視窗（例如在 IE 中的 InPrivate 或 Chrome 中的 Incognito），或清除所有 cookie。</span><span class="sxs-lookup"><span data-stu-id="2e911-183">Use Private browser window like InPrivate in IE or Incognito in Chrome or clear all the cookies.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e911-184">其他資源</span><span class="sxs-lookup"><span data-stu-id="2e911-184">Additional Resources</span></span>

- <span data-ttu-id="2e911-185">[適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="2e911-185">[Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="2e911-186">Windows Azure 功能：身分識別</span><span class="sxs-lookup"><span data-stu-id="2e911-186">Windows Azure Features: Identity</span></span>](https://docs.microsoft.com/azure/active-directory/)
- [<span data-ttu-id="2e911-187">TechNet： Windows Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e911-187">TechNet: Windows Azure Active Directory</span></span>](https://technet.microsoft.com/library/hh967619.aspx)
- [<span data-ttu-id="2e911-188">Windows Azure Active Directory：為您的組織開發應用程式</span><span class="sxs-lookup"><span data-stu-id="2e911-188">Windows Azure Active Directory: Develop Apps for your organization</span></span>](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [<span data-ttu-id="2e911-189">Windows Azure Active Directory：為多個組織開發應用程式</span><span class="sxs-lookup"><span data-stu-id="2e911-189">Windows Azure Active Directory: Develop Apps for multiple organizations</span></span>](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [<span data-ttu-id="2e911-190">如何使用 Windows Azure Active Directory 執行單一登入</span><span class="sxs-lookup"><span data-stu-id="2e911-190">How to implement single sign-on with Windows Azure Active Directory</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- <span data-ttu-id="2e911-191">[使用 Windows Azure Active Directory 的單一登入：深入探討](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci</span><span class="sxs-lookup"><span data-stu-id="2e911-191">[Single Sign-On with Windows Azure Active Directory: a Deep Dive](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci</span></span>
- [<span data-ttu-id="2e911-192">使用 AD FS 2.0 來執行和管理單一登入</span><span class="sxs-lookup"><span data-stu-id="2e911-192">Use AD FS 2.0 to implement and manage single sign-on</span></span>](https://technet.microsoft.com/library/jj205462.aspx)
