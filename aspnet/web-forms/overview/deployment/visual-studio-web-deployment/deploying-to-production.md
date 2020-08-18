---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio：部署到生產環境的 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何部署 (發佈) ASP.NET web 應用程式，以 Azure App Service Web Apps 或協力廠商主機服務提供者，互動 .。。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ec025e757d00cbfbfbcda9408739d2593908bc07
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240625"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a><span data-ttu-id="57ce9-103">使用 Visual Studio：部署到生產環境的 ASP.NET Web 部署</span><span class="sxs-lookup"><span data-stu-id="57ce9-103">ASP.NET Web Deployment using Visual Studio: Deploying to Production</span></span>

<span data-ttu-id="57ce9-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="57ce9-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="57ce9-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="57ce9-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="57ce9-106">本教學課程系列會說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 (發佈) ASP.NET web 應用程式部署至 Azure App Service Web Apps 或協力廠商主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="57ce9-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="57ce9-107">如需此系列的詳細資訊，請參閱 [本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="57ce9-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="57ce9-108">總覽</span><span class="sxs-lookup"><span data-stu-id="57ce9-108">Overview</span></span>

<span data-ttu-id="57ce9-109">在本教學課程中，您會設定 Microsoft Azure 帳戶、建立預備環境和生產環境，並使用 Visual Studio 單鍵發佈功能將 ASP.NET web 應用程式部署到預備環境和生產環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-109">In this tutorial, you set up a Microsoft Azure account, create staging and production environments, and deploy your ASP.NET web application to the staging and production environments by using the Visual Studio one-click publish feature.</span></span>

<span data-ttu-id="57ce9-110">如果您想要的話，也可以部署到協力廠商主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="57ce9-110">If you prefer, you can deploy to a third-party hosting provider.</span></span> <span data-ttu-id="57ce9-111">本教學課程中所述的大部分程式都與主機服務提供者或 Azure 相同，不同之處在于每個提供者都有自己的使用者介面來進行帳戶和網站管理。</span><span class="sxs-lookup"><span data-stu-id="57ce9-111">Most of the procedures described in this tutorial are the same for a hosting provider or for Azure, except that each provider has its own user interface for account and web site management.</span></span> <span data-ttu-id="57ce9-112">您可以在 Microsoft.com 網站上的提供者資源 [庫](https://www.microsoft.com/web/hosting) 中找到主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="57ce9-112">You can find a hosting provider in the [gallery of providers](https://www.microsoft.com/web/hosting) on the Microsoft.com web site.</span></span>

<span data-ttu-id="57ce9-113">提醒：如果您在進行本教學課程時收到錯誤訊息或某個內容無法運作，請務必查看此教學課程系列中的 [疑難排解] 頁面。</span><span class="sxs-lookup"><span data-stu-id="57ce9-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the Troubleshooting page in this tutorial series.</span></span>

## <a name="get-a-microsoft-azure-account"></a><span data-ttu-id="57ce9-114">取得 Microsoft Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="57ce9-114">Get a Microsoft Azure account</span></span>

<span data-ttu-id="57ce9-115">如果您還沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="57ce9-115">If you don't already have an Azure account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="57ce9-116">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="create-a-staging-environment"></a><span data-ttu-id="57ce9-117">建立預備環境</span><span class="sxs-lookup"><span data-stu-id="57ce9-117">Create a staging environment</span></span>

> [!NOTE]
> <span data-ttu-id="57ce9-118">自從撰寫本教學課程之後，Azure App Service 加入了一項新功能，可將許多建立預備環境和生產環境的程式自動化。</span><span class="sxs-lookup"><span data-stu-id="57ce9-118">Since this tutorial was written, Azure App Service added a new feature to automate many of the processes for creating staging and production environments.</span></span> <span data-ttu-id="57ce9-119">請參閱 [在 Azure App Service 中設定 web apps 的預備環境](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-119">See [Set up staging environments for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).</span></span>

<span data-ttu-id="57ce9-120">如同「 [部署至測試環境」教學](deploying-to-iis.md)課程中所述，最可靠的測試環境是主機服務提供者的網站，就像生產網站一樣。</span><span class="sxs-lookup"><span data-stu-id="57ce9-120">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), the most reliable test environment is a web site at the hosting provider that's just like the production web site.</span></span> <span data-ttu-id="57ce9-121">在許多主機服務提供者中，您必須將此項的優點降低為額外成本，但在 Azure 中，您可以建立額外的免費 web 應用程式作為預備應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-121">At many hosting providers you would have to weigh the benefits of this against significant additional cost, but in Azure you can create an additional free web app as your staging app.</span></span> <span data-ttu-id="57ce9-122">您也需要資料庫，而且在實際執行資料庫中的費用可能會是無或最小量的額外費用。</span><span class="sxs-lookup"><span data-stu-id="57ce9-122">You also need a database, and the additional expense for that over the expense of your production database will be either none or minimal.</span></span> <span data-ttu-id="57ce9-123">在 Azure 中，您需支付所使用的資料庫儲存體數量，而不是每個資料庫的費用，而您將在預備環境中使用的額外儲存體量將會降至最低。</span><span class="sxs-lookup"><span data-stu-id="57ce9-123">In Azure you pay for the amount of database storage you use rather than for each database, and the amount of additional storage you'll use in staging will be minimal.</span></span>

<span data-ttu-id="57ce9-124">如同「 [部署至測試環境」教學](deploying-to-iis.md)課程中所述，在預備和生產環境中，您會將兩個資料庫部署到一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="57ce9-124">As explained in the [Deploy to the Test Environment tutorial](deploying-to-iis.md), in staging and production you're going to deploy your two databases into one database.</span></span> <span data-ttu-id="57ce9-125">如果您想要將它們分開，程式會相同，不同之處在于您會為每個環境建立額外的資料庫，而且當您建立發行設定檔時，會為每個資料庫選取正確的目的地字串。</span><span class="sxs-lookup"><span data-stu-id="57ce9-125">If you wanted to keep them separate, the process would be the same except that you'd create an additional database for each environment and you would select the correct destination string for each database when you create the publish profile.</span></span>

<span data-ttu-id="57ce9-126">在本教學課程的這一節中，您將建立要用於預備環境的 web 應用程式和資料庫，而且您將在建立和部署到生產環境之前，部署至預備環境並在該處進行測試。</span><span class="sxs-lookup"><span data-stu-id="57ce9-126">In this section of the tutorial you'll create a web app and database to use for the staging environment, and you'll deploy to staging and test there before creating and deploying to the production environment.</span></span>

> [!NOTE]
> <span data-ttu-id="57ce9-127">下列步驟說明如何使用 Azure 入口網站，在 Azure App Service 中建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-127">The following steps show how to create a web app in Azure App Service by using the Azure management portal.</span></span> <span data-ttu-id="57ce9-128">在最新版的 Azure SDK 中，您也可以使用伺服器總管在不離開 Visual Studio 的情況下進行。</span><span class="sxs-lookup"><span data-stu-id="57ce9-128">In the latest version of the Azure SDK, you can also do this without leaving Visual Studio, by using Server Explorer.</span></span> <span data-ttu-id="57ce9-129">在 Visual Studio 2013 中，您也可以直接從 [發行] 對話方塊中建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-129">In Visual Studio 2013, you can also create a web app directly from the Publish dialog.</span></span> <span data-ttu-id="57ce9-130">如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET web 應用程式。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span><span class="sxs-lookup"><span data-stu-id="57ce9-130">For more information, see [Create an ASP.NET web app in Azure App Service.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)</span></span>

1. <span data-ttu-id="57ce9-131">在 [Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下 [ **網站**]，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-131">In the [Azure Management Portal](https://manage.windowsazure.com/), click **Websites**, and then click **New**.</span></span>
2. <span data-ttu-id="57ce9-132">按一下 [ **網站**]，然後按一下 [ **自訂建立**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-132">Click **Website**, and then click **Custom Create**.</span></span>

    <span data-ttu-id="57ce9-133">**新的網站-自訂建立**嚮導隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="57ce9-133">The **New Website - Custom Create** wizard opens.</span></span> <span data-ttu-id="57ce9-134">**自訂建立**嚮導可讓您同時建立網站和資料庫。</span><span class="sxs-lookup"><span data-stu-id="57ce9-134">The **Custom Create** wizard enables you to create a web site and a database at the same time.</span></span>
3. <span data-ttu-id="57ce9-135">在嚮導的 [ **建立網站** ] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式預備環境的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="57ce9-135">In the **Create Website** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application's staging environment.</span></span> <span data-ttu-id="57ce9-136">例如，輸入 ContosoUniversity-staging123 (包含在結尾的亂數字，以使其成為唯一的，以防 ContosoUniversity 暫存) 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-136">For example, enter ContosoUniversity-staging123 (including random numbers at the end to make it unique in case ContosoUniversity-staging is taken).</span></span>

    <span data-ttu-id="57ce9-137">完整的 URL 將包含您在此處輸入的字串，加上您在文字方塊旁看到的尾碼。</span><span class="sxs-lookup"><span data-stu-id="57ce9-137">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span>
4. <span data-ttu-id="57ce9-138">在 [ **區域** ] 下拉式清單中，選擇最接近您的區域。</span><span class="sxs-lookup"><span data-stu-id="57ce9-138">In the **Region** drop-down list, choose the region that is closest to you.</span></span>

    <span data-ttu-id="57ce9-139">這項設定會指定您的 web 應用程式將在哪一個資料中心執行。</span><span class="sxs-lookup"><span data-stu-id="57ce9-139">This setting specifies which data center your web app will run in.</span></span>
5. <span data-ttu-id="57ce9-140">在 [ **資料庫** ] 下拉式清單中，選擇 [ **建立新的 SQL Database**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-140">In the **Database** drop-down list, choose **Create a new SQL database**.</span></span>
6. <span data-ttu-id="57ce9-141">在 [ **DB 連接字串名稱** ] 方塊中，保留預設值 *DefaultConnection*。</span><span class="sxs-lookup"><span data-stu-id="57ce9-141">In the **DB Connection String Name** box, leave the default value, *DefaultConnection*.</span></span>
7. <span data-ttu-id="57ce9-142">按一下指向方塊底部右邊的箭號。</span><span class="sxs-lookup"><span data-stu-id="57ce9-142">Click the arrow that points to the right at the bottom of the box.</span></span>

    <span data-ttu-id="57ce9-143">下圖顯示內含範例值的 [ **建立網站** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="57ce9-143">The following illustration shows the **Create Website** dialog with sample values in it.</span></span> <span data-ttu-id="57ce9-144">您輸入的 URL 和區域將會不同。</span><span class="sxs-lookup"><span data-stu-id="57ce9-144">The URL and Region that you have entered will be different.</span></span>

    ![建立網站步驟](deploying-to-production/_static/image1.png)

    <span data-ttu-id="57ce9-146">精靈隨即前進至 [指定資料庫設定] \*\*\*\* 步驟。</span><span class="sxs-lookup"><span data-stu-id="57ce9-146">The wizard advances to the **Specify database settings** step.</span></span>
8. <span data-ttu-id="57ce9-147">在 [ **名稱** ] 方塊中，輸入 *ContosoUniversity* 加上一個亂數字，以使其成為唯一的，例如 *ContosoUniversity123*。</span><span class="sxs-lookup"><span data-stu-id="57ce9-147">In the **Name** box, enter *ContosoUniversity* plus a random number to make it unique, for example *ContosoUniversity123*.</span></span>
9. <span data-ttu-id="57ce9-148">在 [ **伺服器** ] 方塊中，選取 [ **新增 SQL Database 伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-148">In the **Server** box, select **New SQL Database Server**.</span></span>
10. <span data-ttu-id="57ce9-149">輸入系統管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="57ce9-149">Enter an administrator name and password.</span></span>

    <span data-ttu-id="57ce9-150">您不會在這裡輸入現有的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="57ce9-150">You aren't entering an existing name and password here.</span></span> <span data-ttu-id="57ce9-151">而是輸入新的名稱和密碼；您現在定義的名稱和密碼將供未來存取資料庫時使用。</span><span class="sxs-lookup"><span data-stu-id="57ce9-151">You're entering a new name and password that you're defining now to use later when you access the database.</span></span>
11. <span data-ttu-id="57ce9-152">在 [ **區域** ] 方塊中，選擇您為 web 應用程式選擇的相同區域。</span><span class="sxs-lookup"><span data-stu-id="57ce9-152">In the **Region** box, choose the same region that you chose for the web app.</span></span>

    <span data-ttu-id="57ce9-153">將網頁伺服器和資料庫伺服器保持在相同區域，可讓您獲得最佳效能，並將費用降至最低。</span><span class="sxs-lookup"><span data-stu-id="57ce9-153">Keeping the web server and the database server in the same region gives you the best performance and minimizes expenses.</span></span>
12. <span data-ttu-id="57ce9-154">按一下方塊底部的核取記號，表示您已完成。</span><span class="sxs-lookup"><span data-stu-id="57ce9-154">Click the check mark at the bottom of the box to indicate that you're finished.</span></span>

    <span data-ttu-id="57ce9-155">下圖顯示 [ **指定資料庫設定** ] 對話方塊，其中包含範例值。</span><span class="sxs-lookup"><span data-stu-id="57ce9-155">The following illustration shows the **Specify database settings** dialog with sample values in it.</span></span> <span data-ttu-id="57ce9-156">您輸入的值可能會不同。</span><span class="sxs-lookup"><span data-stu-id="57ce9-156">The values you have entered may be different.</span></span>

    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](deploying-to-production/_static/image2.png)

    <span data-ttu-id="57ce9-158">管理入口網站回到 [網站] 頁面，[ **狀態** ] 欄會顯示正在建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-158">The Management Portal returns to the Websites page, and the **Status** column shows that the web app is being created.</span></span> <span data-ttu-id="57ce9-159">在一段時間後 (通常不到一分鐘的) ，[ **狀態** ] 欄會顯示已成功建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-159">After a while (typically less than a minute), the **Status** column shows that the web app was successfully created.</span></span> <span data-ttu-id="57ce9-160">在左側導覽列中，您帳戶中的 web 應用程式數目會出現在 [ **網站** ] 圖示旁，而資料庫數目會出現在 [ **SQL 資料庫** ] 圖示旁。</span><span class="sxs-lookup"><span data-stu-id="57ce9-160">In the navigation bar at the left, the number of web apps you have in your account appears next to the **Websites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

    ![Web Sites 管理入口網站的網站頁面](deploying-to-production/_static/image3.png)

    <span data-ttu-id="57ce9-162">您的 web 應用程式名稱將會與圖中的範例應用程式不同。</span><span class="sxs-lookup"><span data-stu-id="57ce9-162">Your web app name will be different from the example app in the illustration.</span></span>

## <a name="deploy-the-application-to-staging"></a><span data-ttu-id="57ce9-163">將應用程式部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="57ce9-163">Deploy the application to staging</span></span>

<span data-ttu-id="57ce9-164">現在您已建立預備環境的 web 應用程式和資料庫，您可以將專案部署至該環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-164">Now that you have created a web app and database for the staging environment, you can deploy the project to it.</span></span>

> [!NOTE]
> <span data-ttu-id="57ce9-165">這些指示說明如何藉由下載 *.publishsettings* 檔案來建立發行設定檔，此檔案不僅適用于 Azure，也適用于協力廠商主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="57ce9-165">These instructions show how to create a publish profile by downloading a *.publishsettings* file, which works not only for Azure but also for third-party hosting providers.</span></span> <span data-ttu-id="57ce9-166">最新的 Azure SDK 也可讓您從 Visual Studio 直接連線到 Azure，並從您的 Azure 帳戶中的 web 應用程式清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="57ce9-166">The latest Azure SDK also enables you to connect directly to Azure from Visual Studio, and choose from a list of web apps that you have in your Azure account.</span></span> <span data-ttu-id="57ce9-167">在 Visual Studio 2013 中，您可以從 [ **Web 發佈** ] 對話方塊或從 [ **伺服器總管** ] 視窗登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="57ce9-167">In Visual Studio 2013, you can sign in to Azure from the **Web Publish** dialog or from the **Server Explorer** window.</span></span> <span data-ttu-id="57ce9-168">如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-168">For more information, see [Create an ASP.NET web app in Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span>

### <a name="download-the-publishsettings-file"></a><span data-ttu-id="57ce9-169">下載 .publishsettings 檔案</span><span class="sxs-lookup"><span data-stu-id="57ce9-169">Download the .publishsettings file</span></span>

1. <span data-ttu-id="57ce9-170">按一下您剛才建立的 web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="57ce9-170">Click the name of the web app that you just created.</span></span>

    ![按一下網站以移至儀表板](deploying-to-production/_static/image4.png)
2. <span data-ttu-id="57ce9-172">在 [**儀表板**] 索引標籤的 [**快速概覽**] 底下，按一下 [**下載發行設定檔**</span><span class="sxs-lookup"><span data-stu-id="57ce9-172">Under **Quick glance** in the **Dashboard** tab, click **Download publish profile**.</span></span>

    ![下載發行設定檔連結](deploying-to-production/_static/image5.png)

    <span data-ttu-id="57ce9-174">此步驟會下載包含您將應用程式部署至 web 應用程式所需之所有設定的檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-174">This step downloads a file that contains all of the settings that you need in order to deploy an application to your web app.</span></span> <span data-ttu-id="57ce9-175">您會將此檔案匯入 Visual Studio，因此您不需要手動輸入此資訊。</span><span class="sxs-lookup"><span data-stu-id="57ce9-175">You'll import this file into Visual Studio so you don't have to enter this information manually.</span></span>
3. <span data-ttu-id="57ce9-176">將 *.publishsettings* 檔案儲存在您可以從 Visual Studio 存取的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="57ce9-176">Save the *.publishsettings* file in a folder that you can access from Visual Studio.</span></span>

    ![儲存 .publishsettings 檔案](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > <span data-ttu-id="57ce9-178">安全性- *.publishsettings* 檔案包含您的認證 (未編碼的) ，用來管理您的 Azure 訂用帳戶和服務。</span><span class="sxs-lookup"><span data-stu-id="57ce9-178">Security - The *.publishsettings* file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="57ce9-179">這個檔案的安全性最佳作法是暫時儲存在來源目錄之外 (例如在 Libraries\Documents 資料夾)，然後在匯入完成後予以刪除。</span><span class="sxs-lookup"><span data-stu-id="57ce9-179">The security best practice for this file is to store it temporarily outside your source directories (for example in the Libraries\Documents folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="57ce9-180">取得 *.publishsettings* 檔案存取權的惡意使用者可以編輯、建立及刪除您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="57ce9-180">A malicious user who gains access to the *.publishsettings* file can edit, create, and delete your Azure services.</span></span>

### <a name="create-a-publish-profile"></a><span data-ttu-id="57ce9-181">建立發行設定檔</span><span class="sxs-lookup"><span data-stu-id="57ce9-181">Create a publish profile</span></span>

1. <span data-ttu-id="57ce9-182">在 Visual Studio 中，以滑鼠右鍵按一下 **方案總管** 中的 ContosoUniversity 專案，然後從內容功能表中選取 [ **發行** ]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-182">In Visual Studio, right-click the ContosoUniversity project in **Solution Explorer** and select **Publish** from the context menu.</span></span>

    <span data-ttu-id="57ce9-183">此時會開啟 [發行 Web] \*\*\*\* 精靈。</span><span class="sxs-lookup"><span data-stu-id="57ce9-183">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="57ce9-184">按一下 [個人資料]\*\*\*\* 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57ce9-184">Click the **Profile** tab.</span></span>
3. <span data-ttu-id="57ce9-185">按一下 [匯入]  。</span><span class="sxs-lookup"><span data-stu-id="57ce9-185">Click **Import**.</span></span>
4. <span data-ttu-id="57ce9-186">流覽至您稍早下載的 *.publishsettings* 檔案，然後按一下 [ **開啟**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-186">Navigate to the *.publishsettings* file you downloaded earlier, and then click **Open**.</span></span>

    ![匯入發行設定對話方塊](deploying-to-production/_static/image7.png)
5. <span data-ttu-id="57ce9-188">在 [ **連接** ] 索引標籤中，按一下 [ **驗證連接** ]，確認設定正確無誤。</span><span class="sxs-lookup"><span data-stu-id="57ce9-188">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>

    <span data-ttu-id="57ce9-189">驗證連接之後，[ **驗證** 連線] 按鈕旁邊會顯示綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="57ce9-189">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span>

    <span data-ttu-id="57ce9-190">針對某些主控提供者，當您按一下 [ **驗證連接**] 時，可能會看到 [ **憑證錯誤** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="57ce9-190">For some hosting providers, when you click **Validate Connection**, you might see a **Certificate Error** dialog box.</span></span> <span data-ttu-id="57ce9-191">如果您這樣做，請確認伺服器名稱是否符合您的預期。</span><span class="sxs-lookup"><span data-stu-id="57ce9-191">If you do, verify that the server name is what you expect.</span></span> <span data-ttu-id="57ce9-192">如果伺服器名稱正確，請選取 [ **儲存此憑證以供 Visual Studio 的未來會話** ]，然後按一下 [ **接受**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-192">If the server name is correct, select **Save this certificate for future sessions of Visual Studio** and click **Accept**.</span></span> <span data-ttu-id="57ce9-193"> (此錯誤表示主控提供者已選擇避免針對您要部署的 URL 購買 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="57ce9-193">(This error means that the hosting provider has chosen to avoid the expense of purchasing an SSL certificate for the URL that you are deploying to.</span></span> <span data-ttu-id="57ce9-194">如果您想要使用有效的憑證來建立安全連線，請洽詢您的主機服務提供者。 ) </span><span class="sxs-lookup"><span data-stu-id="57ce9-194">If you prefer to establish a secure connection by using a valid certificate, contact your hosting provider.)</span></span>
6. <span data-ttu-id="57ce9-195">按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="57ce9-195">Click **Next**.</span></span>

    ![連線索引標籤中的 [連接成功] 圖示和 [下一頁] 按鈕](deploying-to-production/_static/image8.png)
7. <span data-ttu-id="57ce9-197">在 [ **設定** ] 索引標籤中，展開 [檔案 **發佈選項**]，然後選取 **[從應用程式 \_ 資料檔案夾中排除**檔案]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-197">In the **Settings** tab, expand **File Publish Options**, and then select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="57ce9-198">如需 [檔案 **發行選項**] 下其他選項的詳細資訊，請參閱 [部署至 IIS](deploying-to-iis.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="57ce9-198">For information about the other options under **File Publish Options**, see the [deploying to IIS](deploying-to-iis.md) tutorial.</span></span> <span data-ttu-id="57ce9-199">顯示此步驟結果和下列資料庫設定步驟的螢幕擷取畫面，位於資料庫設定步驟的結尾。</span><span class="sxs-lookup"><span data-stu-id="57ce9-199">The screen shot that shows the result of this step and the following database configuration steps is at the end of the database configuration steps.</span></span>
8. <span data-ttu-id="57ce9-200">在 [**資料庫**] 區段的 [ **DefaultConnection** ] 下，為成員資格資料庫設定資料庫部署。</span><span class="sxs-lookup"><span data-stu-id="57ce9-200">Under **DefaultConnection** in the **Databases** section, configure database deployment for the membership database.</span></span>
9. 1. <span data-ttu-id="57ce9-201">選取 [ **更新資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-201">Select **Update database**.</span></span>

        <span data-ttu-id="57ce9-202">緊接在**DefaultConnection**下方的 [**遠端連線字串**] 方塊會填入 .publishsettings 檔案中的連接字串。連接字串包含 SQL Server 的認證，以純文字格式儲存在 *.pubxml*檔案中。</span><span class="sxs-lookup"><span data-stu-id="57ce9-202">The **Remote connection string** box directly below **DefaultConnection** is filled in with the connection string from the .publishsettings file.The connection string includes SQL Server credentials, which are stored in plain text in the *.pubxml* file.</span></span> <span data-ttu-id="57ce9-203">如果您不想將它們永久儲存在該處，您可以在部署資料庫之後，將其從發行設定檔中移除，並將其儲存在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="57ce9-203">If you prefer not to store them permanently there, you can remove them from the publish profile after the database is deployed and store them in Azure instead.</span></span> <span data-ttu-id="57ce9-204">如需詳細資訊，請參閱 Scott Hanselman 的 blog 上 [從來源部署至 Azure 時，如何確保 ASP.NET 資料庫連接字串的安全性](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-204">For more information, see [How to keep your ASP.NET database connection strings secure when deploying to Azure from Source](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) on Scott Hanselman's blog.</span></span>
      2. <span data-ttu-id="57ce9-205">按一下 [ **設定資料庫更新**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-205">Click **Configure database updates**.</span></span>
      3. <span data-ttu-id="57ce9-206">在 [ **設定資料庫更新** ] 對話方塊中，按一下 [ **加入 SQL 腳本**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-206">In the **Configure Database Updates** dialog box, click **Add SQL Script**.</span></span>
      4. <span data-ttu-id="57ce9-207">在 [ **加入 SQL 腳本** ] 方塊中，流覽至您稍早在方案資料夾中儲存的 *aspnet-data-prod .sql* 腳本，然後按一下 [ **開啟**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-207">In the **Add SQL Script** box, navigate to the *aspnet-data-prod.sql* script that you saved earlier in the solution folder, and then click **Open**.</span></span>
      5. <span data-ttu-id="57ce9-208">關閉 [ **設定資料庫更新** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="57ce9-208">Close the **Configure Database Updates** dialog box.</span></span>
10. <span data-ttu-id="57ce9-209">在 [**資料庫**] 區段的 [ **SchoolCoNtext** ] 底下，選取 [**執行 Code First 移轉 (在應用程式啟動) 上執行**。</span><span class="sxs-lookup"><span data-stu-id="57ce9-209">Under **SchoolContext** in the **Databases** section, select **Execute Code First Migrations (runs on application start)**.</span></span>

    <span data-ttu-id="57ce9-210">Visual Studio 會顯示 **執行 Code First 移轉** ，而不是類別的 **更新資料庫** `DbContext` 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-210">Visual Studio displays **Execute Code First Migrations** instead of **Update Database** for `DbContext` classes.</span></span> <span data-ttu-id="57ce9-211">如果您想要使用用於 dbdacfx 提供者（而不是遷移）來部署使用類別存取的資料庫 `DbContext` ，請參閱 MSDN 上 Visual Studio 和 ASP.NET 的 Web 部署常見問題中的 [如何? 部署不含遷移的 Code First 資料庫？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-211">If you want to use the dbDacFx provider instead of Migrations to deploy a database that you access by using a `DbContext` class, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the Web Deployment FAQ for Visual Studio and ASP.NET on MSDN.</span></span>

    <span data-ttu-id="57ce9-212">[ **設定** ] 索引標籤現在看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="57ce9-212">The **Settings** tab now looks like the following example:</span></span>

    ![預備環境的 [設定] 索引標籤](deploying-to-production/_static/image9.png)
11. <span data-ttu-id="57ce9-214">請執行下列步驟來儲存設定檔，並將其重新命名為 *預備*環境：</span><span class="sxs-lookup"><span data-stu-id="57ce9-214">Perform the following steps to save the profile and rename it to *Staging*:</span></span>

    1. <span data-ttu-id="57ce9-215">按一下 [ **設定檔** ] 索引標籤，然後按一下 [ **管理設定檔**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-215">Click the **Profile** tab, and then click **Manage Profiles**.</span></span>
    2. <span data-ttu-id="57ce9-216">匯入會建立兩個新的設定檔，一個用於 FTP，另一個用於 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="57ce9-216">The import created two new profiles, one for FTP and one for Web Deploy.</span></span> <span data-ttu-id="57ce9-217">您已設定 Web Deploy 設定檔：將此設定檔重新命名為 *預備*環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-217">You configured the Web Deploy profile: rename this profile to *Staging*.</span></span>

        ![將設定檔重新命名為預備環境](deploying-to-production/_static/image10.png)
    3. <span data-ttu-id="57ce9-219">關閉 [ **編輯 Web 發行設定檔** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="57ce9-219">Close the **Edit Web Publish Profiles** dialog box.</span></span>
    4. <span data-ttu-id="57ce9-220">關閉 [ **發行 Web** wizard]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-220">Close the **Publish Web** wizard.</span></span>

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a><span data-ttu-id="57ce9-221">設定環境指標的發行設定檔轉換</span><span class="sxs-lookup"><span data-stu-id="57ce9-221">Configure a publish profile transform for the environment indicator</span></span>

> [!NOTE]
> <span data-ttu-id="57ce9-222">本節說明如何設定環境指標的 Web.config 轉換。</span><span class="sxs-lookup"><span data-stu-id="57ce9-222">This section shows how to set up a Web.config transform for the environment indicator.</span></span> <span data-ttu-id="57ce9-223">因為指標位於專案中，所以您可以在 `<appSettings>` 部署到 Azure App Service 時，有另一個指定轉換的替代方法。</span><span class="sxs-lookup"><span data-stu-id="57ce9-223">Because the indicator is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Azure App Service.</span></span> <span data-ttu-id="57ce9-224">如需詳細資訊，請參閱 [在 Azure 中指定 Web.config 設定](web-config-transformations.md#watransforms)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-224">For more information, see [Specifying Web.config settings in Azure](web-config-transformations.md#watransforms).</span></span>

1. <span data-ttu-id="57ce9-225">在 **方案總管**中，展開 [ **屬性**]，然後展開 [ **PublishProfiles**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-225">In **Solution Explorer**, expand **Properties**, and then expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="57ce9-226">以滑鼠右鍵按一下 [ *.pubxml*]，然後按一下 [ **新增設定轉換**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-226">Right-click *Staging.pubxml*, and then click **Add Config Transform**.</span></span>

    ![新增用於暫存的設定轉換](deploying-to-production/_static/image11.png)

    <span data-ttu-id="57ce9-228">Visual Studio 建立 *Web.Staging.config* 轉換檔案並加以開啟。</span><span class="sxs-lookup"><span data-stu-id="57ce9-228">Visual Studio creates the *Web.Staging.config* transform file and opens it.</span></span>
3. <span data-ttu-id="57ce9-229">在 *Web.Staging.config* 轉換檔中，將下列程式碼插入緊接在開頭 `configuration` 標記之後。</span><span class="sxs-lookup"><span data-stu-id="57ce9-229">In the *Web.Staging.config* transform file, insert the following code immediately after the opening `configuration` tag.</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    <span data-ttu-id="57ce9-230">當您使用預備發行設定檔時，這種轉換會將環境指標設定為「生產」。</span><span class="sxs-lookup"><span data-stu-id="57ce9-230">When you use the Staging publish profile, this transform sets the environment indicator to "Prod".</span></span> <span data-ttu-id="57ce9-231">在已部署的 web 應用程式中，您將不會在 "Contoso 大學" H1 標題之後看到任何尾碼，例如 " (Dev) " 或 " (Test) "。</span><span class="sxs-lookup"><span data-stu-id="57ce9-231">In the deployed web app, you won't see any suffix such as "(Dev)" or "(Test)" after the "Contoso University" H1 heading.</span></span>
4. <span data-ttu-id="57ce9-232">以滑鼠右鍵按一下 *Web.Staging.config* 檔案，然後按一下 [ **預覽轉換** ] 以確定您編碼的轉換會產生預期的變更。</span><span class="sxs-lookup"><span data-stu-id="57ce9-232">Right-click the *Web.Staging.config* file and click **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="57ce9-233">Web.config 的 [ \*\* 預覽\*\* ] 視窗會顯示套用 *Web.Release.config* 轉換和 *Web.Staging.config* 轉換的結果。</span><span class="sxs-lookup"><span data-stu-id="57ce9-233">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Staging.config* transforms.</span></span>

### <a name="prevent-public-use-of-the-test-app"></a><span data-ttu-id="57ce9-234">防止公開使用測試應用程式</span><span class="sxs-lookup"><span data-stu-id="57ce9-234">Prevent public use of the test app</span></span>

<span data-ttu-id="57ce9-235">預備應用程式的重要考慮是它會存留在網際網路上，但您不想讓公用使用它。</span><span class="sxs-lookup"><span data-stu-id="57ce9-235">An important consideration for the staging app is that it will be live on the Internet, but you don't want the public to use it.</span></span> <span data-ttu-id="57ce9-236">您可以使用下列一種或多種方法，以將人員發現和使用的可能性降至最低：</span><span class="sxs-lookup"><span data-stu-id="57ce9-236">To minimize the likelihood that people will find and use it, you can use one or more of the following methods:</span></span>

- <span data-ttu-id="57ce9-237">設定防火牆規則，僅允許從您用來測試預備環境的 IP 位址存取暫存應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-237">Set firewall rules that allow access to the staging app only from IP addresses that you use to test staging.</span></span>
- <span data-ttu-id="57ce9-238">請使用不可能猜測的模糊 URL。</span><span class="sxs-lookup"><span data-stu-id="57ce9-238">Use an obfuscated URL that would be impossible to guess.</span></span>
- <span data-ttu-id="57ce9-239">建立 *robots.txt* 檔案，以確保搜尋引擎不會在搜尋結果中將測試應用程式與報表連結進行編目。</span><span class="sxs-lookup"><span data-stu-id="57ce9-239">Create a *robots.txt* file to ensure that search engines will not crawl the test app and report links to it in search results.</span></span>

<span data-ttu-id="57ce9-240">這些方法的第一種是最有效的，但不在本教學課程中討論，因為它會要求您部署至 Azure 雲端服務，而不是 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="57ce9-240">The first of these methods is the most effective but is not covered in this tutorial because it would require that you deploy to an Azure Cloud Service instead of Azure App Service.</span></span> <span data-ttu-id="57ce9-241">如需 Azure 中的雲端服務和 IP 限制的詳細資訊，請參閱 [Azure 提供的計算裝載選項](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) ，以及 [封鎖特定 IP 位址，使其無法存取 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-241">For more information about Cloud Services and IP restrictions in Azure, see [Compute Hosting Options Provided by Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) and [Block Specific IP Addresses from Accessing a Web Role](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx).</span></span> <span data-ttu-id="57ce9-242">如果您要部署到協力廠商主機服務提供者，請洽詢提供者，以瞭解如何實行 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="57ce9-242">If you are deploying to a third-party hosting provider, contact the provider to find out how to implement IP restrictions.</span></span>

<span data-ttu-id="57ce9-243">在本教學課程中，您將建立 *robots.txt* 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-243">For this tutorial, you'll create a *robots.txt* file.</span></span>

1. <span data-ttu-id="57ce9-244">在 **方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [ **加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-244">In **Solution Explorer**, right-click the ContosoUniversity project and click **Add New Item**.</span></span>
2. <span data-ttu-id="57ce9-245">建立名為*robots.txt*的新**文字檔**，然後在其中放入下列文字：</span><span class="sxs-lookup"><span data-stu-id="57ce9-245">Create a new **Text File** named *robots.txt*, and put the following text in it:</span></span>

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    <span data-ttu-id="57ce9-246">`User-agent`該行會告知搜尋引擎，檔案中的規則會套用到所有搜尋引擎的 web 編目程式 (機器人) ，而 `Disallow` 這一行會指定網站上的任何頁面都不應進行編目。</span><span class="sxs-lookup"><span data-stu-id="57ce9-246">The `User-agent` line tells search engines that the rules in the file apply to all search engine web crawlers (robots), and the `Disallow` line specifies that no pages on the site should be crawled.</span></span>

    <span data-ttu-id="57ce9-247">您需要搜尋引擎來為您的生產應用程式進行編目，因此您需要將此檔案從生產環境部署中排除。</span><span class="sxs-lookup"><span data-stu-id="57ce9-247">You do want search engines to catalog your production app, so you need to exclude this file from production deployment.</span></span> <span data-ttu-id="57ce9-248">若要這樣做，您將在建立生產發行設定檔時，設定其設定。</span><span class="sxs-lookup"><span data-stu-id="57ce9-248">To do that, you'll configure a setting in the Production publish profile when you create it.</span></span>

### <a name="deploy-to-staging"></a><span data-ttu-id="57ce9-249">部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="57ce9-249">Deploy to staging</span></span>

1. <span data-ttu-id="57ce9-250">以滑鼠右鍵按一下 Contoso 大學專案，然後按一下 [**發佈**]，開啟 [**發佈 Web** ]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-250">Open the **Publish Web** wizard by right-clicking the Contoso University project and clicking **Publish**.</span></span>
2. <span data-ttu-id="57ce9-251">請確定已選取 [ **暫存** 設定檔]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-251">Make sure that the **Staging** profile is selected.</span></span>
3. <span data-ttu-id="57ce9-252">按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-252">Click **Publish**.</span></span>

    <span data-ttu-id="57ce9-253">[輸出] \*\*\*\* 視窗會顯示已採取的部署動作，並報告部署作業已順利完成。</span><span class="sxs-lookup"><span data-stu-id="57ce9-253">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span> <span data-ttu-id="57ce9-254">預設瀏覽器會自動開啟至已部署 web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="57ce9-254">The default browser automatically opens to the URL of the deployed web app.</span></span>

## <a name="test-in-the-staging-environment"></a><span data-ttu-id="57ce9-255">在預備環境中測試</span><span class="sxs-lookup"><span data-stu-id="57ce9-255">Test in the staging environment</span></span>

<span data-ttu-id="57ce9-256">請注意，環境指示器不存在 (在 H1 標題之後沒有 " (Test) " 或 " (Dev) "，這會顯示環境指標的 *Web.config* 轉換成功。</span><span class="sxs-lookup"><span data-stu-id="57ce9-256">Notice that the environment indicator is absent (there is no "(Test)" or "(Dev)" after the H1 heading, which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

![首頁預備環境](deploying-to-production/_static/image12.png)

<span data-ttu-id="57ce9-258">執行 [ **學生** ] 頁面，確認已部署的資料庫沒有任何學生。</span><span class="sxs-lookup"><span data-stu-id="57ce9-258">Run the **Students** page to verify that the deployed database has no students.</span></span>

<span data-ttu-id="57ce9-259">執行 **講師** 頁面，確認 Code First 使用講師資料植入資料庫：</span><span class="sxs-lookup"><span data-stu-id="57ce9-259">Run the **Instructors** page to verify that Code First seeded the database with instructor data:</span></span>

<span data-ttu-id="57ce9-260">選取 [**學生**] 功能表中的 [**加入學生**]、新增學生，然後在 [**學生**] 頁面中查看新的學生，確認您可以成功寫入資料庫。</span><span class="sxs-lookup"><span data-stu-id="57ce9-260">Select **Add Students** from the **Students** menu, add a student, and then view the new student in the **Students** page to verify that you can successfully write to the database.</span></span>

<span data-ttu-id="57ce9-261">在 [ **課程** ] 頁面中，按一下 [ **更新點數**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-261">From the **Courses** page, click **Update Credits**.</span></span> <span data-ttu-id="57ce9-262">[ **更新點數** ] 頁面需要系統管理員許可權，因此會顯示 [ **登入** ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="57ce9-262">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="57ce9-263">輸入您稍早建立的系統管理員帳號憑證 ( "admin" 和 "prodpwd" ) 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-263">Enter the administrator account credentials that you created earlier ("admin" and "prodpwd").</span></span> <span data-ttu-id="57ce9-264">[ **更新點數** ] 頁面隨即顯示，確認您在上一個教學課程中建立的系統管理員帳戶已正確部署至測試環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-264">The **Update Credits** page is displayed, which verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="57ce9-265">要求不正確 URL，以產生 ELMAH 將追蹤的錯誤，然後要求 ELMAH 錯誤報表。</span><span class="sxs-lookup"><span data-stu-id="57ce9-265">Request an invalid URL to cause an error that ELMAH will track, and then request the ELMAH error report.</span></span> <span data-ttu-id="57ce9-266">如果您要部署到協力廠商主機服務提供者，您可能會發現報表是空的，因為它在上一個教學課程中是空的。</span><span class="sxs-lookup"><span data-stu-id="57ce9-266">If you are deploying to a third-party hosting provider, you will probably find that the report is empty for the same reason that it was empty in the previous tutorial.</span></span> <span data-ttu-id="57ce9-267">您必須使用主控提供者的帳戶管理工具來設定資料夾許可權，以讓 ELMAH 寫入至記錄資料夾。</span><span class="sxs-lookup"><span data-stu-id="57ce9-267">You will have to use the hosting provider's account management tools to configure folder permissions to enable ELMAH to write to the log folder.</span></span>

<span data-ttu-id="57ce9-268">您所建立的應用程式現在會在 web 應用程式中于雲端中執行，就像您將用於生產環境的應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="57ce9-268">The application that you created is now running in the cloud in a web app that is just like what you will use for production.</span></span> <span data-ttu-id="57ce9-269">因為一切都能正常運作，下一步是部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-269">Since everything is working correctly, the next step is to deploy to production.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="57ce9-270">部署到生產</span><span class="sxs-lookup"><span data-stu-id="57ce9-270">Deploy to production</span></span>

<span data-ttu-id="57ce9-271">建立生產 web 應用程式並部署至生產環境的程式與預備環境的程式相同，不同之處在于您需要從部署中排除 *robots.txt* 。</span><span class="sxs-lookup"><span data-stu-id="57ce9-271">The process for creating a production web app and deploying to production is the same as for staging, except that you need to exclude the *robots.txt* from deployment.</span></span> <span data-ttu-id="57ce9-272">若要這樣做，您要編輯發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="57ce9-272">To do that you'll edit the publish profile file.</span></span>

### <a name="create-the-production-environment-and-the-production-publish-profile"></a><span data-ttu-id="57ce9-273">建立生產環境和生產發行設定檔</span><span class="sxs-lookup"><span data-stu-id="57ce9-273">Create the production environment and the production publish profile</span></span>

1. <span data-ttu-id="57ce9-274">遵循您用於預備環境的相同程式，在 Azure 中建立生產環境 web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="57ce9-274">Create the production web app and database in Azure, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="57ce9-275">當您建立資料庫時，您可以選擇將它放在您稍早建立的相同伺服器上，或建立新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="57ce9-275">When you create the database, you can choose to put it on the same server you created earlier, or create a new server.</span></span>
2. <span data-ttu-id="57ce9-276">下載 *.publishsettings* 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-276">Download the *.publishsettings* file.</span></span>
3. <span data-ttu-id="57ce9-277">匯入 *.publishsettings* 檔案以建立發行設定檔，並遵循您用於預備環境的相同程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-277">Create the publish profile by importing the production *.publishsettings* file, following the same procedure that you used for staging.</span></span>

    <span data-ttu-id="57ce9-278">別忘了在 [**設定**] 索引標籤的 [**資料庫**] 區段中，于 [ **DefaultConnection** ] 下設定資料部署腳本。</span><span class="sxs-lookup"><span data-stu-id="57ce9-278">Don't forget to configure the data deployment script under **DefaultConnection** in the **Databases** section of the **Settings** tab.</span></span>
4. <span data-ttu-id="57ce9-279">將發行設定檔重新命名為 *生產環境*。</span><span class="sxs-lookup"><span data-stu-id="57ce9-279">Rename the publish profile to *Production*.</span></span>
5. <span data-ttu-id="57ce9-280">設定環境指標的發行設定檔轉換，遵循您用於預備的相同程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-280">Configure a publish profile transform for the environment indicator, following the same procedure that you used for staging..</span></span>

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a><span data-ttu-id="57ce9-281">編輯 .pubxml 檔案以排除 robots.txt</span><span class="sxs-lookup"><span data-stu-id="57ce9-281">Edit the .pubxml file to exclude robots.txt</span></span>

<span data-ttu-id="57ce9-282">發行設定檔的名稱為 &lt; profilename &gt; *.pubxml* ，而且位於*PublishProfiles*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="57ce9-282">Publish profile files are named &lt;profilename&gt;*.pubxml* and are located in the *PublishProfiles* folder.</span></span> <span data-ttu-id="57ce9-283">[ *PublishProfiles* ] 資料夾位於 c # web 應用程式專案的 [ *Properties* ] 資料夾底下、VB web 應用程式專案中的 [ *我的專案* ] 資料夾底下，或是在 Web 應用程式專案的 [ *應用程式 \_ 資料* ] 資料夾底下。</span><span class="sxs-lookup"><span data-stu-id="57ce9-283">The *PublishProfiles* folder is under the *Properties* folder in a C# web application project, under the *My Project* folder in a VB web application project, or under the *App\_Data* folder in a web app project.</span></span> <span data-ttu-id="57ce9-284">每個 *.pubxml* 檔案都包含適用于一個發行設定檔的設定。</span><span class="sxs-lookup"><span data-stu-id="57ce9-284">Each *.pubxml* file contains settings that apply to one publish profile.</span></span> <span data-ttu-id="57ce9-285">您在 [發佈 Web] 中輸入的值會儲存在這些檔案中，您可以編輯這些值，以建立或變更 Visual Studio UI 中未提供的設定。</span><span class="sxs-lookup"><span data-stu-id="57ce9-285">The values you enter in the Publish Web wizard are stored in these files, and you can edit them to create or change settings that aren't made available in the Visual Studio UI.</span></span>

<span data-ttu-id="57ce9-286">依預設，當您建立發行設定檔時，專案中會包含 *.pubxml* 檔案，但您可以將它們從專案中排除，Visual Studio 仍會使用這些檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-286">By default, *.pubxml* files are included in the project when you create a publish profile, but you can exclude them from the project and Visual Studio will still use them.</span></span> <span data-ttu-id="57ce9-287">Visual Studio 會在 *.pubxml*檔案的*PublishProfiles*資料夾中尋找，不論專案中是否包含這些檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-287">Visual Studio looks in the *PublishProfiles* folder for *.pubxml* files, regardless of whether they are included in the project.</span></span>

<span data-ttu-id="57ce9-288">每個 *.pubxml* 檔案都有 *.pubxml. 使用者* 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-288">For each *.pubxml* file there is a *.pubxml.user* file.</span></span> <span data-ttu-id="57ce9-289">如果您選取了 [**儲存密碼**] 選項， *.pubxml*就會包含加密的密碼，而且根據預設，它會從專案中排除。</span><span class="sxs-lookup"><span data-stu-id="57ce9-289">The *.pubxml.user* file contains the encrypted password if you selected the **Save password** option, and by default it is excluded from the project.</span></span>

<span data-ttu-id="57ce9-290">*.Pubxml*檔案包含與特定發行設定檔相關的設定。</span><span class="sxs-lookup"><span data-stu-id="57ce9-290">A *.pubxml* file contains the settings that pertain to a specific publish profile.</span></span> <span data-ttu-id="57ce9-291">如果您想要設定適用于所有設定檔的設定，您可以建立一個 *wpp .targets* 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-291">If you want to configure settings that apply to all profiles, you can create a *.wpp.targets* file.</span></span> <span data-ttu-id="57ce9-292">組建程式會將這些檔案匯入 *.csproj* 或 *vbproj* 專案檔中，因此您可以在專案檔中設定的大部分設定都可以在這些檔案中進行設定。</span><span class="sxs-lookup"><span data-stu-id="57ce9-292">The build process imports these files into the *.csproj* or *.vbproj* project file, so most settings that you can configure in the project file can be configured in these files.</span></span> <span data-ttu-id="57ce9-293">如需有關 *.Pubxml* 檔案和 *wpp .targets* 檔案的詳細資訊，請參閱 [如何：編輯發行設定檔中的部署設定 (. .Pubxml) 檔和 Visual Studio Web 專案中的 wpp .targets](https://msdn.microsoft.com/library/ff398069.aspx)檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-293">For more information about *.pubxml* files and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

1. <span data-ttu-id="57ce9-294">在 **方案總管**中，展開 [ **屬性** ]，然後展開 [ **PublishProfiles**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-294">In **Solution Explorer**, expand **Properties** and expand **PublishProfiles**.</span></span>
2. <span data-ttu-id="57ce9-295">以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [ **開啟**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-295">Right-click *Production.pubxml* and click **Open**.</span></span>

    ![開啟 .pubxml 檔案](deploying-to-production/_static/image13.png)
3. <span data-ttu-id="57ce9-297">以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [ **開啟**]。</span><span class="sxs-lookup"><span data-stu-id="57ce9-297">Right-click *Production.pubxml* and click **Open**.</span></span>
4. <span data-ttu-id="57ce9-298">緊接在結尾元素之前加入下列幾行 `PropertyGroup` ：</span><span class="sxs-lookup"><span data-stu-id="57ce9-298">Add the following lines immediately before the closing `PropertyGroup` element:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    <span data-ttu-id="57ce9-299">.Pubxml 檔案現在看起來類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="57ce9-299">The .pubxml file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    <span data-ttu-id="57ce9-300">如需有關如何排除檔案和資料夾的詳細資訊，請參閱 MSDN 上的**Visual Studio 和 ASP.NET 的 Web 部署常見問題**中的「[我可以從部署中排除特定檔案或資料夾嗎？](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 」。</span><span class="sxs-lookup"><span data-stu-id="57ce9-300">For more information about how to exclude files and folders, see [Can I exclude specific files or folders from deployment?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) in the **Web Deployment FAQ for Visual Studio and ASP.NET** on MSDN.</span></span>

### <a name="deploy-to-production"></a><span data-ttu-id="57ce9-301">部署到生產</span><span class="sxs-lookup"><span data-stu-id="57ce9-301">Deploy to production</span></span>

1. <span data-ttu-id="57ce9-302">開啟 [**發佈 Web** ] 嚮導，確認已選取 [**生產**發行設定檔]，然後按一下 [**預覽**] 索引標籤上的 [**開始預覽**]，以確認*robots.txt*檔案不會複製到生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-302">Open the **Publish Web** wizard make sure that the **Production** publish profile is selected, and then click **Start Preview** on the **Preview** tab to verify that the *robots.txt* file will not be copied to the production app.</span></span>

    ![要發行至生產環境的檔預覽](deploying-to-production/_static/image14.png)

    <span data-ttu-id="57ce9-304">檢查將複製的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="57ce9-304">Review the list of files that will be copied.</span></span> <span data-ttu-id="57ce9-305">您會看到所有的 *.cs* 檔案，包括 *aspx.cs*、 *. aspx.designer.cs*、 *Master.cs*和 *Master.designer.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-305">You'll see that all of the *.cs* files, including *.aspx.cs*, *.aspx.designer.cs*, *Master.cs*, and *Master.designer.cs* files are omitted.</span></span> <span data-ttu-id="57ce9-306">此程式碼的所有程式碼都已編譯成*ContosoUniversity.dll* ，並 ContosoUniversity 您將在*bin*資料夾中找到的 *.pdb*檔。</span><span class="sxs-lookup"><span data-stu-id="57ce9-306">All of this code has been compiled into the *ContosoUniversity.dll* and *ContosoUniversity.pdb* files that you'll find in the *bin* folder.</span></span> <span data-ttu-id="57ce9-307">因為只需要 *.dll* 來執行應用程式，而且您先前指定只有執行應用程式所需的檔案才會進行部署，所以不會將 *.cs* 檔案複製到目的地環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-307">Because only the *.dll* is needed to run the application, and you specified earlier that only files needed to run the application should be deployed, no *.cs* files were copied to the destination environment.</span></span> <span data-ttu-id="57ce9-308">*Obj*資料夾和*ContosoUniversity .csproj*和 *.csproj. 使用者*檔案會因相同原因而省略。</span><span class="sxs-lookup"><span data-stu-id="57ce9-308">The *obj* folder and the *ContosoUniversity.csproj* and *.csproj.user* files are omitted for the same reason.</span></span>

    <span data-ttu-id="57ce9-309">按一下 [ **發佈** ] 以部署至生產環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-309">Click **Publish** to deploy to the production environment.</span></span>
2. <span data-ttu-id="57ce9-310">在生產環境中測試，遵循您用於預備的相同程式。</span><span class="sxs-lookup"><span data-stu-id="57ce9-310">Test in production, following the same procedure you used for staging.</span></span>

    <span data-ttu-id="57ce9-311">除了 URL 和缺少 *robots.txt* 檔案之外，所有專案都與預備環境相同。</span><span class="sxs-lookup"><span data-stu-id="57ce9-311">Everything is identical to staging except for the URL and the absence of the *robots.txt* file.</span></span>

## <a name="summary"></a><span data-ttu-id="57ce9-312">摘要</span><span class="sxs-lookup"><span data-stu-id="57ce9-312">Summary</span></span>

<span data-ttu-id="57ce9-313">您現在已成功部署並測試您的 web 應用程式，並可透過網際網路公開使用。</span><span class="sxs-lookup"><span data-stu-id="57ce9-313">You have now successfully deployed and tested your web app and it is available publicly over the Internet.</span></span>

![首頁生產](deploying-to-production/_static/image15.png)

<span data-ttu-id="57ce9-315">在下一個教學課程中，您將更新應用程式程式碼，並將變更部署到測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="57ce9-315">In the next tutorial, you'll update application code and deploy the change to the test, staging, and production environments.</span></span>

> [!NOTE]
> <span data-ttu-id="57ce9-316">當您的應用程式在生產環境中使用時，您應該執行復原方案。</span><span class="sxs-lookup"><span data-stu-id="57ce9-316">While your application is in use in the production environment you should be implementing a recovery plan.</span></span> <span data-ttu-id="57ce9-317">也就是說，您應該定期將資料庫從生產環境應用程式備份到安全的儲存位置，而且您應該保留數個這類備份的層代。</span><span class="sxs-lookup"><span data-stu-id="57ce9-317">That is, you should be periodically backing up your databases from the production app to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="57ce9-318">當您更新資料庫時，您應該在變更前立即建立備份複本。</span><span class="sxs-lookup"><span data-stu-id="57ce9-318">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="57ce9-319">然後，如果您在將它部署到生產環境之後不會發現錯誤，您仍然可以將資料庫復原到它損毀之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="57ce9-319">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span> <span data-ttu-id="57ce9-320">如需詳細資訊，請參閱 [Azure SQL Database 備份和還原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-320">For more information, see [Azure SQL Database Backup and Restore](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).</span></span>
> 
> 
> [!NOTE]
> <span data-ttu-id="57ce9-321">在本教學課程中，您要部署的 SQL Server 版本 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="57ce9-321">In this tutorial the SQL Server edition that you are deploying to is Azure SQL Database.</span></span> <span data-ttu-id="57ce9-322">雖然部署程式與其他版本的 SQL Server 很類似，但實際的生產環境應用程式在某些情況下可能需要特殊的程式碼才能 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="57ce9-322">While the deployment process is similar to other editions of SQL Server, a real production application might require special code for Azure SQL Database in some scenarios.</span></span> <span data-ttu-id="57ce9-323">如需詳細資訊，請參閱 [使用 Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) 以及 [在 SQL Server 和 Azure SQL Database 之間進行選擇](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。</span><span class="sxs-lookup"><span data-stu-id="57ce9-323">For more information, see [Working with Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) and [Choosing between SQL Server and Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="57ce9-324">[上一個](setting-folder-permissions.md) 
> [下一步](deploying-a-code-update.md)</span><span class="sxs-lookup"><span data-stu-id="57ce9-324">[Previous](setting-folder-permissions.md)
[Next](deploying-a-code-update.md)</span></span>
