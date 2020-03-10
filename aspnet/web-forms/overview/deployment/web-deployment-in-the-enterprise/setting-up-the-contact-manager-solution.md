---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 設定 Contact Manager 解決方案 |Microsoft Docs
author: jrjlee
description: 本主題說明如何下載並設定 Contact Manager 解決方案，以在開發人員工作站上本機執行。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629854"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="c3c3f-103">設定連絡管理員解決方案</span><span class="sxs-lookup"><span data-stu-id="c3c3f-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="c3c3f-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c3c3f-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c3c3f-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="c3c3f-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c3c3f-106">本主題說明如何下載並設定 Contact Manager 解決方案，以在開發人員工作站上本機執行。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="c3c3f-107">系統需求</span><span class="sxs-lookup"><span data-stu-id="c3c3f-107">System Requirements</span></span>

<span data-ttu-id="c3c3f-108">若要在本機執行 Contact Manager 解決方案，以及執行本教學課程中所述的其他工作，您必須在開發人員工作站上安裝此軟體：</span><span class="sxs-lookup"><span data-stu-id="c3c3f-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="c3c3f-109">Visual Studio 2010 Service Pack 1、Premium 或旗艦版</span><span class="sxs-lookup"><span data-stu-id="c3c3f-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="c3c3f-110">Internet Information Services (IIS) 7.5 Express</span><span class="sxs-lookup"><span data-stu-id="c3c3f-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="c3c3f-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c3c3f-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="c3c3f-112">IIS Web Deployment Tool （Web Deploy）2.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="c3c3f-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="c3c3f-113">ASP.NET 4。0</span><span class="sxs-lookup"><span data-stu-id="c3c3f-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="c3c3f-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="c3c3f-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="c3c3f-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="c3c3f-115">.NET Framework 4</span></span>
- <span data-ttu-id="c3c3f-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="c3c3f-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="c3c3f-117">除了 Visual Studio 2010 以外，您還可以透過[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)下載並安裝所有這些產品和元件的最新版本。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="c3c3f-118">下載並解壓縮解決方案</span><span class="sxs-lookup"><span data-stu-id="c3c3f-118">Download and Extract the Solution</span></span>

<span data-ttu-id="c3c3f-119">您可以從[這裡](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)的 MSDN 程式碼庫下載 Contact Manager 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="c3c3f-120">設定及執行解決方案</span><span class="sxs-lookup"><span data-stu-id="c3c3f-120">Configure and Run the Solution</span></span>

<span data-ttu-id="c3c3f-121">若要在本機電腦上設定並執行 Contact Manager 解決方案，您必須執行下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="c3c3f-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="c3c3f-122">如果您還沒有帳戶，請建立已啟用成員資格和角色管理功能的本機 ASP.NET 應用程式服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="c3c3f-123">編輯*web.config*檔案中的連接字串，以指向您的本機 SQL Server Express 實例。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="c3c3f-124">從 Visual Studio 2010 執行解決方案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="c3c3f-125">本節的其餘部分提供如何完成這些工作的更多指引。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="c3c3f-126">**若要建立應用程式服務資料庫**</span><span class="sxs-lookup"><span data-stu-id="c3c3f-126">**To create the application services database**</span></span>

1. <span data-ttu-id="c3c3f-127">開啟 Visual Studio 2010 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="c3c3f-128">若要這樣做，請在 [**開始**] 功能表上，指向 [**所有程式**]，按一下 [ **Microsoft Visual Studio 2010**]，按一下 [ **Visual Studio Tools**]，然後按一下 **[Visual Studio 命令提示字元（2010）** ]。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="c3c3f-129">在命令提示字元中，輸入下列命令，然後按 Enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="c3c3f-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="c3c3f-130">使用 **– C**參數來指定資料庫伺服器的連接字串。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="c3c3f-131">使用 **– A**參數來指定您想要新增至資料庫的應用程式服務功能。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="c3c3f-132">在此情況下， **m**表示您想要新增成員資格提供者的支援，而**r**則表示您想要加入角色管理員的支援。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="c3c3f-133">使用 **– d**參數來指定應用程式服務資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="c3c3f-134">如果您省略此參數，公用程式會建立預設名稱為**aspnetdb.mdf**的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="c3c3f-135">成功建立資料庫之後，命令提示字元就會顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="c3c3f-136">如需 aspnet\_regsql 公用程式的詳細資訊，請參閱[ASP.NET SQL Server 註冊工具（aspnet\_regsql .exe）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="c3c3f-137">下一個步驟是確定 Contact Manager 解決方案中的連接字串指向 SQL Server Express 的本機實例。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="c3c3f-138">**若要更新連接字串**</span><span class="sxs-lookup"><span data-stu-id="c3c3f-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="c3c3f-139">在 Visual Studio 2010 中開啟 Contact Manager 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="c3c3f-140">在 [**方案總管**] 視窗中，展開 [ **ContactManager** ] 專案，然後按兩下 **[web.config] 節點。**</span><span class="sxs-lookup"><span data-stu-id="c3c3f-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3c3f-141">ContactManager 專案包含兩個*web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="c3c3f-142">您需要編輯專案層級檔案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="c3c3f-143">在**connectionStrings**元素中，確認名為**microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception**的連接字串指向您的本機 ASP.NET 應用程式服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="c3c3f-144">在 [**方案總管**] 視窗中，展開 [ **ContactManager** ] 專案，然後按兩下 **[web.config] 節點。**</span><span class="sxs-lookup"><span data-stu-id="c3c3f-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="c3c3f-145">在**connectionStrings**元素中，于名為**contactmanager.models.contactmanagercoNtext**的連接字串中，確認 [**資料來源**] 屬性已設定為 SQL Server Express 的本機實例。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="c3c3f-146">您不需要變更連接字串中的任何其他專案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="c3c3f-147">儲存所有開啟的檔案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-147">Save all open files.</span></span>

<span data-ttu-id="c3c3f-148">您現在應該已準備好在本機電腦上執行 Contact Manager 解決方案。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="c3c3f-149">如果您在沒有先建立應用程式服務資料庫的情況下執行這些步驟，ASP.NET 會在您第一次嘗試建立使用者時建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="c3c3f-150">不過，手動建立資料庫可讓您更充分掌控您想要支援的應用程式服務功能集。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="c3c3f-151">**執行 Contact Manager 解決方案**</span><span class="sxs-lookup"><span data-stu-id="c3c3f-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="c3c3f-152">在 Visual Studio 2010 中，按 F5。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="c3c3f-153">Internet Explorer 會啟動並要求 Contact Manager ASP.NET MVC 3 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="c3c3f-154">根據預設，應用程式會顯示 [**所有連絡人**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="c3c3f-155">新增一些連絡人，然後確認應用程式如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="c3c3f-156">流覽至 `http://localhost:50114/Account/Register` （如果您要將應用程式裝載在不同的埠上，請調整 URL）。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="c3c3f-157">新增 [使用者名稱]、[電子郵件地址] 和 [密碼]，並確認您能夠成功註冊帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="c3c3f-158">流覽至 `http://localhost:50114/Account/LogOn` （如果您要將應用程式裝載在不同的埠上，請調整 URL）。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="c3c3f-159">確認您能夠使用剛建立的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="c3c3f-160">關閉 Internet Explorer 以停止調試。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c3c3f-161">結論</span><span class="sxs-lookup"><span data-stu-id="c3c3f-161">Conclusion</span></span>

<span data-ttu-id="c3c3f-162">此時，必須將 Contact Manager 解決方案完整設定為在您的本機電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="c3c3f-163">當您逐步執行本教學課程中的其他主題時，您可以使用此解決方案做為參考。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="c3c3f-164">下一個主題：[瞭解專案](understanding-the-project-file.md)檔，說明如何使用 Contact Manager 方案內的自訂 Microsoft Build Engine （MSBuild）專案檔來控制部署程式。</span><span class="sxs-lookup"><span data-stu-id="c3c3f-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3c3f-165">[上一頁](the-contact-manager-solution.md)
> [下一頁](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="c3c3f-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
