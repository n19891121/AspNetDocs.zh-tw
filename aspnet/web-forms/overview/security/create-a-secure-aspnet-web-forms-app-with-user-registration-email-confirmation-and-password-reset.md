---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 建立安全的 ASP.NET Web Forms 應用程式與使用者註冊、 電子郵件確認和密碼重設 (C#) |Microsoft Docs
author: Erikre
description: 本教學課程會示範如何建置 ASP.NET Web Forms 應用程式與使用者註冊、 電子郵件確認和密碼重設使用 ASP.NET Identity 成員...
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: 3df728891103de9c8e461ab9507237c9b14e8251
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59390684"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a><span data-ttu-id="95d34-103">以使用者註冊、電子郵件確認和密碼重設建立安全的 ASP.NET Web Forms 應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="95d34-103">Create a secure ASP.NET Web Forms app with user registration, email confirmation and password reset (C#)</span></span>

<span data-ttu-id="95d34-104">藉由[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="95d34-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="95d34-105">本教學課程會示範如何建置 ASP.NET Web Forms 應用程式與使用者註冊、 電子郵件確認和密碼重設使用 ASP.NET 身分識別的成員資格系統。</span><span class="sxs-lookup"><span data-stu-id="95d34-105">This tutorial shows you how to build an ASP.NET Web Forms app with user registration, email confirmation and password reset using the ASP.NET Identity membership system.</span></span> <span data-ttu-id="95d34-106">本教學課程已根據 Rick Anderson [MVC 教學課程](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)。</span><span class="sxs-lookup"><span data-stu-id="95d34-106">This tutorial was based on Rick Anderson's [MVC tutorial](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md).</span></span>


## <a name="introduction"></a><span data-ttu-id="95d34-107">簡介</span><span class="sxs-lookup"><span data-stu-id="95d34-107">Introduction</span></span>

<span data-ttu-id="95d34-108">本教學課程會引導您完成建立 ASP.NET Web Forms 應用程式使用 Visual Studio 和 ASP.NET 4.5 來建立安全的 Web Form 應用程式以使用者註冊、 電子郵件確認和密碼重設所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="95d34-108">This tutorial guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio and ASP.NET 4.5 to create a secure Web Forms app with user registration, email confirmation and password reset.</span></span>

### <a name="tutorial-tasks-and-information"></a><span data-ttu-id="95d34-109">教學課程的工作和資訊：</span><span class="sxs-lookup"><span data-stu-id="95d34-109">Tutorial Tasks and Information:</span></span>

- [<span data-ttu-id="95d34-110">建立 ASP.NET Web Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="95d34-110">Create an ASP.NET Web Forms app</span></span>](#createWebForms)
- [<span data-ttu-id="95d34-111">將 SendGrid 連結</span><span class="sxs-lookup"><span data-stu-id="95d34-111">Hook Up SendGrid</span></span>](#SG)
- [<span data-ttu-id="95d34-112">需要先登入的電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="95d34-112">Require Email Confirmation Before Log In</span></span>](#require)
- [<span data-ttu-id="95d34-113">密碼復原和重設</span><span class="sxs-lookup"><span data-stu-id="95d34-113">Password Recovery and Reset</span></span>](#reset)
- [<span data-ttu-id="95d34-114">重新傳送電子郵件確認連結</span><span class="sxs-lookup"><span data-stu-id="95d34-114">Resend Email Confirmation Link</span></span>](#rsend)
- [<span data-ttu-id="95d34-115">疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="95d34-115">Troubleshooting the App</span></span>](#dbg)
- [<span data-ttu-id="95d34-116">其他資源</span><span class="sxs-lookup"><span data-stu-id="95d34-116">Additional Resources</span></span>](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a><span data-ttu-id="95d34-117">建立 ASP.NET Web Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="95d34-117">Create an ASP.NET Web Forms App</span></span>

<span data-ttu-id="95d34-118">開始安裝並執行[Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058)或是[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="95d34-118">Start by installing and running [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="95d34-119">安裝[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更高版本以及。</span><span class="sxs-lookup"><span data-stu-id="95d34-119">Install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher as well.</span></span>

> [!NOTE]
> <span data-ttu-id="95d34-120">警告：您必須安裝[Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465)或更新版本，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="95d34-120">Warning: You must install [Visual Studio 2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390465) or higher to complete this tutorial.</span></span>


1. <span data-ttu-id="95d34-121">建立新的專案 (**檔案** - &gt; **新專案**)，然後選取**ASP.NET Web 應用程式**範本和最新的.NET Framework從版本**新的專案** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="95d34-121">Create a new project (**File** -&gt; **New Project**) and select the **ASP.NET Web Application** template and the latest .NET Framework version from the **New Project** dialog box.</span></span>
2. <span data-ttu-id="95d34-122">從**新的 ASP.NET 專案**對話方塊中，選取**Web Form**範本。</span><span class="sxs-lookup"><span data-stu-id="95d34-122">From the **New ASP.NET Project** dialog box, select the **Web Forms** template.</span></span> <span data-ttu-id="95d34-123">保留為預設的驗證**個別使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="95d34-123">Leave the default authentication as **Individual User Accounts**.</span></span> <span data-ttu-id="95d34-124">如果您想要裝載在 Azure 中的應用程式，將保留**雲端中的主機**勾選核取方塊。</span><span class="sxs-lookup"><span data-stu-id="95d34-124">If you'd like to host the app in Azure, leave the **Host in the cloud** check box checked.</span></span>   
 <span data-ttu-id="95d34-125">然後，按一下**確定**建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="95d34-125">Then, click **OK** to create the new project.</span></span>  
    <span data-ttu-id="95d34-126">![[新增 ASP.NET 專案] 對話方塊](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="95d34-126">![New ASP.NET Project dialog box](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)</span></span>
3. <span data-ttu-id="95d34-127">啟用 Secure Sockets Layer (SSL) 專案。</span><span class="sxs-lookup"><span data-stu-id="95d34-127">Enable Secure Sockets Layer (SSL) for the project.</span></span> <span data-ttu-id="95d34-128">請遵循中提供的步驟**啟用專案的 SSL**一節[開始使用 Web Form 教學課程系列](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)。</span><span class="sxs-lookup"><span data-stu-id="95d34-128">Follow the steps available in the **Enable SSL for the Project** section of the [Getting Started with Web Forms tutorial series](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms).</span></span>
4. <span data-ttu-id="95d34-129">執行應用程式，請按一下**註冊**連結，並註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="95d34-129">Run the app, click the **Register** link and register a new user.</span></span> <span data-ttu-id="95d34-130">唯一的驗證電子郵件根據到目前為止， [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)以確保電子郵件地址的格式正確的屬性。</span><span class="sxs-lookup"><span data-stu-id="95d34-130">At this point, the only validation on the email is based on the [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) attribute to ensure the email address is well-formed.</span></span> <span data-ttu-id="95d34-131">您將修改程式碼來新增電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="95d34-131">You will modify the code to add email confirmation.</span></span> <span data-ttu-id="95d34-132">關閉瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="95d34-132">Close the browser window.</span></span>
5. <span data-ttu-id="95d34-133">在 [**伺服器總管**的 Visual Studio (**檢視** - &gt; **伺服器總管]**)，瀏覽至**資料 Connections\DefaultConnection\Tables\AspNetUsers**，以滑鼠右鍵按一下並選取**開啟資料表定義**。</span><span class="sxs-lookup"><span data-stu-id="95d34-133">In **Server Explorer** of Visual Studio (**View** -&gt; **Server Explorer**), navigate to **Data Connections\DefaultConnection\Tables\AspNetUsers**, right click and select **Open table definition**.</span></span> 

    <span data-ttu-id="95d34-134">下圖顯示`AspNetUsers`資料表結構描述：</span><span class="sxs-lookup"><span data-stu-id="95d34-134">The following image shows the `AspNetUsers` table schema:</span></span>

    ![AspNetUsers 資料表結構描述](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. <span data-ttu-id="95d34-136">在 **伺服器總管**，以滑鼠右鍵按一下**AspNetUsers**資料表，然後選取**顯示資料表資料**。</span><span class="sxs-lookup"><span data-stu-id="95d34-136">In **Server Explorer**, right-click on the **AspNetUsers** table and select **Show Table Data**.</span></span>  
  
    ![AspNetUsers 資料表資料](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 <span data-ttu-id="95d34-138">此時已不確認的註冊使用者的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95d34-138">At this point the email for the registered user has not been confirmed.</span></span>
7. <span data-ttu-id="95d34-139">按一下資料列，然後選取刪除要刪除的使用者。</span><span class="sxs-lookup"><span data-stu-id="95d34-139">Click on the row and select delete to delete the user.</span></span> <span data-ttu-id="95d34-140">您將在下一個步驟中再次新增這封電子郵件，並將確認訊息傳送至電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="95d34-140">You'll add this email again in the next step and send a confirmation message to the email address.</span></span>

## <a name="email-confirmation"></a><span data-ttu-id="95d34-141">電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="95d34-141">Email Confirmation</span></span>

<span data-ttu-id="95d34-142">最好確認電子郵件以確認它們不會模擬其他人的新使用者的註冊期間 （也就是尚未註冊使用其他人的電子郵件）。</span><span class="sxs-lookup"><span data-stu-id="95d34-142">It's a best practice to confirm the email during the registration of a new user to verify they are not impersonating someone else (that is, they haven't registered with someone else's email).</span></span> <span data-ttu-id="95d34-143">假設您有討論論壇，您會想要防止`"bob@cpandl.com"`註冊為`"joe@contoso.com"`。</span><span class="sxs-lookup"><span data-stu-id="95d34-143">Suppose you had a discussion forum, you would want to prevent `"bob@cpandl.com"` from registering as `"joe@contoso.com"`.</span></span> <span data-ttu-id="95d34-144">而不需要電子郵件確認`"joe@contoso.com"`無法從您的應用程式收到不想要的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95d34-144">Without email confirmation, `"joe@contoso.com"` could get unwanted email from your app.</span></span> <span data-ttu-id="95d34-145">假設 Bob 不小心註冊為`"bib@cpandl.com"`並沒注意到，他便無法使用密碼復原，因為應用程式不需要其正確的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95d34-145">Suppose Bob accidentally registered as `"bib@cpandl.com"` and hadn't noticed it, he wouldn't be able to use password recovery because the app doesn't have his correct email.</span></span> <span data-ttu-id="95d34-146">電子郵件確認從 bot 提供有限的保護，並不提供從決定濫發垃圾郵件者的保護。</span><span class="sxs-lookup"><span data-stu-id="95d34-146">Email confirmation provides only limited protection from bots and doesn't provide protection from determined spammers.</span></span>

<span data-ttu-id="95d34-147">您通常想要防止新使用者張貼至您的網站的任何資料之前確認透過其中一個電子郵件、 SMS 文字訊息或其他機制。</span><span class="sxs-lookup"><span data-stu-id="95d34-147">You generally want to prevent new users from posting any data to your website before they have been confirmed by either email, an SMS text message or another mechanism.</span></span> <span data-ttu-id="95d34-148">在下列章節中，我們將啟用電子郵件確認和修改程式碼以防止新註冊的使用者登入，直到已確認其電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95d34-148">In the sections below, we will enable email confirmation and modify the code to prevent newly registered users from logging in until their email has been confirmed.</span></span> <span data-ttu-id="95d34-149">您將在本教學課程中使用 SendGrid 電子郵件服務。</span><span class="sxs-lookup"><span data-stu-id="95d34-149">You'll use the email service SendGrid in this tutorial.</span></span>

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a><span data-ttu-id="95d34-150">將 SendGrid 連結</span><span class="sxs-lookup"><span data-stu-id="95d34-150">Hook up SendGrid</span></span>

<span data-ttu-id="95d34-151">SendGrid 已變更的 API，因為撰寫本教學課程。</span><span class="sxs-lookup"><span data-stu-id="95d34-151">SendGrid has changed it's API since this tutorial was written.</span></span> <span data-ttu-id="95d34-152">目前的 SendGrid 指示，請參閱[SendGrid](http://sendgrid.com/)或是[啟用的帳戶確認和密碼復原](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)。</span><span class="sxs-lookup"><span data-stu-id="95d34-152">For current SendGrid instructions, see [SendGrid](http://sendgrid.com/) or [Enable account confirmation and password recovery](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery).</span></span>

<span data-ttu-id="95d34-153">雖然本教學課程中只會顯示如何將透過電子郵件通知[SendGrid](http://sendgrid.com/)，您可以傳送電子郵件使用 SMTP 和其他機制 (請參閱[其他資源](#addRes))。</span><span class="sxs-lookup"><span data-stu-id="95d34-153">Although this tutorial only shows how to add email notification through [SendGrid](http://sendgrid.com/), you can send email using SMTP and other mechanisms (see [additional resources](#addRes)).</span></span>

1. <span data-ttu-id="95d34-154">在 Visual Studio 中開啟**Package Manager Console** (**工具** - &gt; **NuGet 封裝管理員** - &gt;**Package Manager Console**)，並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="95d34-154">In Visual Studio, open the **Package Manager Console** (**Tools** -&gt; **NuGet Package Manger** -&gt; **Package Manager Console**), and enter the following command:</span></span>  
    `Install-Package SendGrid`
2. <span data-ttu-id="95d34-155">移至[Azure SendGrid 註冊頁面](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/)並註冊免費的 SendGrid 帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d34-155">Go to the [Azure SendGrid sign-up page](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) and register for free SendGrid account.</span></span> <span data-ttu-id="95d34-156">您可以也註冊免費的 SendGrid 帳戶直接依據[SendGrid 的站台](http://www.sendgrid.com)。</span><span class="sxs-lookup"><span data-stu-id="95d34-156">You can also sign-up for a free SendGrid account directly on [SendGrid's site](http://www.sendgrid.com).</span></span>
3. <span data-ttu-id="95d34-157">從**方案總管**開啟*IdentityConfig.cs*中的檔案*應用程式\_啟動*資料夾，並新增下列程式碼的黃色反白顯示`EmailService`類別，以設定**SendGrid**:</span><span class="sxs-lookup"><span data-stu-id="95d34-157">From **Solution Explorer** open the *IdentityConfig.cs* file in the *App\_Start* folder and add the following code highlighted in yellow to the `EmailService` class to configure **SendGrid**:</span></span>

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. <span data-ttu-id="95d34-158">此外，新增下列`using`開頭的陳述式*IdentityConfig.cs*檔案：</span><span class="sxs-lookup"><span data-stu-id="95d34-158">Also, add the following `using` statements to the beginning of the *IdentityConfig.cs* file:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. <span data-ttu-id="95d34-159">為了簡化此範例中，您將儲存中的電子郵件服務帳戶值`appSettings`一節*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="95d34-159">To keep this sample simple, you'll store the email service account values in the `appSettings` section of the *web.config* file.</span></span> <span data-ttu-id="95d34-160">新增下列 XML 以黃色反白顯示*web.config*您的專案根目錄的檔案：</span><span class="sxs-lookup"><span data-stu-id="95d34-160">Add the following XML highlighted in yellow to the *web.config* file at the root of your project:</span></span>

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > <span data-ttu-id="95d34-161">安全性-機密資料絕不儲存在原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="95d34-161">Security - Never store sensitive data in your source code.</span></span> <span data-ttu-id="95d34-162">在此範例中，帳戶和認證會儲存在**appSetting**一節*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="95d34-162">In this example, the account and credentials are stored in the **appSetting** section of the *Web.config* file.</span></span> <span data-ttu-id="95d34-163">在 Azure 上，您可以安全地儲存這些值在 **[設定](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 在 Azure 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="95d34-163">On Azure, you can securely store these values on the **[Configure](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** tab in the Azure portal.</span></span> <span data-ttu-id="95d34-164">如需相關資訊，請參閱 Rick Anderson 主題[最佳做法將密碼和其他機密資料部署到 ASP.NET 和 Azure](https://go.microsoft.com/fwlink/?LinkId=513141)。</span><span class="sxs-lookup"><span data-stu-id="95d34-164">For related information see Rick Anderson's topic titled [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure](https://go.microsoft.com/fwlink/?LinkId=513141).</span></span>
6. <span data-ttu-id="95d34-165">新增電子郵件服務值，以反映您的 SendGrid 驗證值 （使用者名稱和密碼），讓您可以成功傳送電子郵件從您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="95d34-165">Add the email service values to reflect your SendGrid authentication values (User Name and Password) so that you can successful send email from your app.</span></span> <span data-ttu-id="95d34-166">請務必使用您的 SendGrid 帳戶名稱，而不是您提供 SendGrid 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="95d34-166">Be sure to use your SendGrid account name rather than the email address you provided SendGrid.</span></span>

### <a name="enable-email-confirmation"></a><span data-ttu-id="95d34-167">啟用電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="95d34-167">Enable Email Confirmation</span></span>

 <span data-ttu-id="95d34-168">若要啟用電子郵件確認，您將修改的登錄程式碼使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="95d34-168">To enable email confirmation, you'll modify the registration code using the following steps.</span></span>  
 

1. <span data-ttu-id="95d34-169">在 *帳戶*資料夾中，開啟*Register.aspx.cs*程式碼後置，並更新`CreateUser_Click`方法，以啟用下列醒目提示的變更：</span><span class="sxs-lookup"><span data-stu-id="95d34-169">In the *Account* folder, open the *Register.aspx.cs* code-behind and update the `CreateUser_Click` method to enable the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. <span data-ttu-id="95d34-170">在 [**方案總管] 中**，以滑鼠右鍵按一下*Default.aspx* ，然後選取**設定為起始頁**。</span><span class="sxs-lookup"><span data-stu-id="95d34-170">In **Solution Explorer**, right-click *Default.aspx* and select **Set As Start Page**.</span></span>
3. <span data-ttu-id="95d34-171">執行應用程式藉由按下**F5。**</span><span class="sxs-lookup"><span data-stu-id="95d34-171">Run the app by pressing **F5.**</span></span> <span data-ttu-id="95d34-172">頁面會顯示之後，請按一下**註冊**連結可以顯示 [註冊] 頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-172">After the page is displayed, click the **Register** link to display the Register page.</span></span>
4. <span data-ttu-id="95d34-173">輸入您的電子郵件和密碼，然後按一下 [**註冊**] 按鈕，透過 SendGrid 電子郵件訊息傳送。</span><span class="sxs-lookup"><span data-stu-id="95d34-173">Enter your email and password, then click the **Register** button to send an email message via SendGrid.</span></span>  
   <span data-ttu-id="95d34-174">您的專案和程式碼的目前狀態可讓使用者登入後他們完成註冊表單中，即使它們尚未確認他們的帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d34-174">The current state of your project and code will allow the user to log in once they complete the registration form, even though they haven't confirmed their account.</span></span>
5. <span data-ttu-id="95d34-175">檢查您的電子郵件帳戶，然後按一下連結，以確認您的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95d34-175">Check your email account and click on the link to confirm your email.</span></span>  
   <span data-ttu-id="95d34-176">一旦您提交註冊表單，您將登入。</span><span class="sxs-lookup"><span data-stu-id="95d34-176">Once you submit the registration form, you will be logged in.</span></span>  
    ![範例網站-登入](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a><span data-ttu-id="95d34-178">需要先登入的電子郵件確認</span><span class="sxs-lookup"><span data-stu-id="95d34-178">Require Email Confirmation Before Log In</span></span>

<span data-ttu-id="95d34-179">雖然您已確認的電子郵件帳戶，此時您就不需要完整登入的驗證電子郵件中所包含的連結上按一下。</span><span class="sxs-lookup"><span data-stu-id="95d34-179">Although you have confirmed the email account, at this point you would not need to click on the link contained in the verification email to be fully signed-in.</span></span> <span data-ttu-id="95d34-180">在下一節中，您將修改要求新的使用者將確認電子郵件之前在登入時 （驗證） 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="95d34-180">In the following section, you will modify the code requiring new users to have a confirmed email before they are logged in (authenticated).</span></span>

1. <span data-ttu-id="95d34-181">在 [**方案總管] 中**的 Visual Studio 中，更新`CreateUser_Click`中的事件*Register.aspx.cs*程式碼後置中包含*帳戶*資料夾中的，使用下列醒目提示的變更：</span><span class="sxs-lookup"><span data-stu-id="95d34-181">In **Solution Explorer** of Visual Studio, update the `CreateUser_Click` event in the *Register.aspx.cs* code-behind contained in the *Accounts* folder with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. <span data-ttu-id="95d34-182">更新`LogIn`方法中的*Login.aspx.cs*程式碼後置與下列醒目提示的變更：</span><span class="sxs-lookup"><span data-stu-id="95d34-182">Update the `LogIn` method in the *Login.aspx.cs* code-behind with the following highlighted changes:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a><span data-ttu-id="95d34-183">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="95d34-183">Run the Application</span></span>

 <span data-ttu-id="95d34-184">既然您已實作的程式碼，以檢查是否已確認使用者的電子郵件地址，您可以檢查的功能，兩者**註冊**並**登入**頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-184">Now that you have implemented the code to check whether a user's email address has been confirmed, you can check the functionality on both the **Register** and **Login** pages.</span></span> 

1. <span data-ttu-id="95d34-185">刪除中的任何帳戶**AspNetUsers**包含您想要測試的電子郵件別名的資料表。</span><span class="sxs-lookup"><span data-stu-id="95d34-185">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
2. <span data-ttu-id="95d34-186">執行應用程式 (**F5**)，並確認您已確認您的電子郵件地址之前，無法註冊為使用者。</span><span class="sxs-lookup"><span data-stu-id="95d34-186">Run the app (**F5**) and verify you cannot register as a user until you have confirmed your email address.</span></span>
3. <span data-ttu-id="95d34-187">確認新的帳戶透過剛被傳送的電子郵件之前, 嘗試新的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="95d34-187">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
 <span data-ttu-id="95d34-188">您會看到您已無法登入進行，您必須確認電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d34-188">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span>
4. <span data-ttu-id="95d34-189">一旦您確認您的電子郵件地址，請登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="95d34-189">Once you confirm your email address, log in to the app.</span></span>

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a><span data-ttu-id="95d34-190">密碼復原和重設</span><span class="sxs-lookup"><span data-stu-id="95d34-190">Password Recovery and Reset</span></span>

1. <span data-ttu-id="95d34-191">在 Visual Studio 中，移除註解字元`Forgot`方法中的*Forgot.aspx.cs*程式碼後置內*帳戶*資料夾中，因此，此方法會顯示為如下所示：</span><span class="sxs-lookup"><span data-stu-id="95d34-191">In Visual Studio, remove the comment characters from the `Forgot` method in the *Forgot.aspx.cs* code-behind contained in the *Account* folder, so that the method appears as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. <span data-ttu-id="95d34-192">開啟*Login.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-192">Open the *Login.aspx* page.</span></span> <span data-ttu-id="95d34-193">將標記結尾附近**loginForm**區段以反白顯示如下：</span><span class="sxs-lookup"><span data-stu-id="95d34-193">Replace the markup near the end of the **loginForm** section as highlighted below:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. <span data-ttu-id="95d34-194">開啟*Login.aspx.cs*程式碼後置和下列從黃色反白顯示的程式碼行取消註解`Page_Load`事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="95d34-194">Open the *Login.aspx.cs* code-behind and uncomment the following line of code highlighted in yellow from the `Page_Load` event handler:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. <span data-ttu-id="95d34-195">執行應用程式藉由按下**F5。**</span><span class="sxs-lookup"><span data-stu-id="95d34-195">Run the app by pressing **F5.**</span></span> <span data-ttu-id="95d34-196">頁面會顯示之後，請按一下**登入**連結。</span><span class="sxs-lookup"><span data-stu-id="95d34-196">After the page is displayed, click the **Log in** link.</span></span>
5. <span data-ttu-id="95d34-197">按一下 **忘記密碼？** 連結，以顯示**忘記密碼**頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-197">Click the **Forgot your password?** link to display the **Forgot Password** page.</span></span>
6. <span data-ttu-id="95d34-198">輸入您的電子郵件地址，然後按一下**送出**傳送電子郵件給您的地址才可重設密碼 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95d34-198">Enter your email address and click the **Submit** button to send an email to your address which will allow you to reset your password.</span></span>   
   <span data-ttu-id="95d34-199">檢查您的電子郵件帳戶，然後按一下連結以顯示**重設密碼**頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-199">Check your email account and click on the link to display the **Reset Password** page.</span></span>
7. <span data-ttu-id="95d34-200">在 **重設密碼**頁面上，輸入您的電子郵件、 密碼和確認的密碼。</span><span class="sxs-lookup"><span data-stu-id="95d34-200">On the **Reset Password** page, enter your email, password, and confirmed password.</span></span> <span data-ttu-id="95d34-201">然後按**重設** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95d34-201">Then, press the **Reset** button.</span></span>  
   <span data-ttu-id="95d34-202">當您已成功重設密碼，請**變更密碼**將會顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="95d34-202">When you successfully reset your password, the **Password Changed** page will be displayed.</span></span> <span data-ttu-id="95d34-203">現在您可以登入您的新密碼。</span><span class="sxs-lookup"><span data-stu-id="95d34-203">Now you can log in with your new password.</span></span>

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a><span data-ttu-id="95d34-204">重新傳送電子郵件確認連結</span><span class="sxs-lookup"><span data-stu-id="95d34-204">Resend Email Confirmation Link</span></span>

<span data-ttu-id="95d34-205">一旦使用者建立新的本機帳戶時，它們是電子郵件確認連結，他們才能使用之前，他們可以登入。</span><span class="sxs-lookup"><span data-stu-id="95d34-205">Once a user creates a new local account, they are emailed a confirmation link they are required to use before they can log on.</span></span> <span data-ttu-id="95d34-206">如果使用者不小心刪除的確認電子郵件，或永遠不會收到電子郵件，他們必須重新傳送確認連結。</span><span class="sxs-lookup"><span data-stu-id="95d34-206">If the user accidentally deletes the confirmation email, or the email never arrives, they will need the confirmation link sent again.</span></span> <span data-ttu-id="95d34-207">下列程式碼變更會示範如何啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="95d34-207">The following code changes show how to enable this.</span></span>

1. <span data-ttu-id="95d34-208">在 Visual Studio 中開啟**Login.aspx.cs**程式碼後置，並新增下列事件處理常式之後`LogIn`事件處理常式：</span><span class="sxs-lookup"><span data-stu-id="95d34-208">In Visual Studio, open the **Login.aspx.cs** code-behind and add the following event handler after the `LogIn` event handler:</span></span>   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. <span data-ttu-id="95d34-209">修改`LogIn`中的事件處理常式*Login.aspx.cs*程式碼後置藉由變更黃色反白顯示，如下所示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="95d34-209">Modify the `LogIn` event handler in the *Login.aspx.cs* code-behind by changing the code highlighted in yellow as follows:</span></span> 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. <span data-ttu-id="95d34-210">更新*Login.aspx*頁面加上黃色反白顯示，如下所示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="95d34-210">Update the *Login.aspx* page by adding the code highlighted in yellow as follows:</span></span> 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. <span data-ttu-id="95d34-211">刪除中的任何帳戶**AspNetUsers**包含您想要測試的電子郵件別名的資料表。</span><span class="sxs-lookup"><span data-stu-id="95d34-211">Delete any accounts in the **AspNetUsers** table that contain the email alias you wish to test.</span></span>
5. <span data-ttu-id="95d34-212">執行應用程式 (**F5**)，並註冊您的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="95d34-212">Run the app (**F5**) and register your email address.</span></span>
6. <span data-ttu-id="95d34-213">確認新的帳戶透過剛被傳送的電子郵件之前, 嘗試新的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="95d34-213">Before confirming your new account via the email that was just sent, attempt to log in with the new account.</span></span>  
   <span data-ttu-id="95d34-214">您會看到您已無法登入進行，您必須確認電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d34-214">You'll see that you are unable to log in and that you must have a confirmed email account.</span></span> <span data-ttu-id="95d34-215">此外，您現在可以重新確認訊息傳送至您的電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="95d34-215">In addition, you can now resend a confirmation message to your email account.</span></span>
7. <span data-ttu-id="95d34-216">輸入您的電子郵件地址和密碼，然後按**重新傳送確認** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="95d34-216">Enter your email address and password, then press the **Resend confirmation** button.</span></span>
8. <span data-ttu-id="95d34-217">一旦您確認您根據新傳送的電子郵件訊息的電子郵件地址，請登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="95d34-217">Once you confirm your email address based on the newly sent email message, log in to the app.</span></span>

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a><span data-ttu-id="95d34-218">疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="95d34-218">Troubleshooting the App</span></span>

<span data-ttu-id="95d34-219">如果您未收到電子郵件包含此連結來確認您的認證：</span><span class="sxs-lookup"><span data-stu-id="95d34-219">If you don't receive an email containing the link to verify your credentials:</span></span>

- <span data-ttu-id="95d34-220">請檢查垃圾郵件或垃圾郵件資料夾。</span><span class="sxs-lookup"><span data-stu-id="95d34-220">Check your junk or spam folder.</span></span>
- <span data-ttu-id="95d34-221">登入您的 SendGrid 帳戶，然後按一下[電子郵件 」 活動連結](https://sendgrid.com/logs/index)。</span><span class="sxs-lookup"><span data-stu-id="95d34-221">Log into your SendGrid account and click on the [Email Activity link](https://sendgrid.com/logs/index).</span></span>
- <span data-ttu-id="95d34-222">確定您使用您的 SendGrid 使用者帳戶名稱，作為*Web.config*值而不是您的 SendGrid 帳戶電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="95d34-222">Be certain you used your SendGrid user account name as a *Web.config* value rather than your SendGrid account email address.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="95d34-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="95d34-223">Additional Resources</span></span>

- [<span data-ttu-id="95d34-224">連結至 ASP.NET Identity 建議資源</span><span class="sxs-lookup"><span data-stu-id="95d34-224">Links to ASP.NET Identity Recommended Resources</span></span>](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [<span data-ttu-id="95d34-225">帳戶確認和密碼復原，使用 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="95d34-225">Account Confirmation and Password Recovery with ASP.NET Identity</span></span>](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [<span data-ttu-id="95d34-226">ASP.NET Web Form 教學課程系列-新增 OAuth 2.0 提供者</span><span class="sxs-lookup"><span data-stu-id="95d34-226">ASP.NET Web Forms tutorial series - Add an OAuth 2.0 Provider</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [<span data-ttu-id="95d34-227">使用成員資格、 OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="95d34-227">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [<span data-ttu-id="95d34-228">ASP.NET Web Form 教學課程系列-啟用專案的 SSL</span><span class="sxs-lookup"><span data-stu-id="95d34-228">ASP.NET Web Forms tutorial series - Enable SSL for the Project</span></span>](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
