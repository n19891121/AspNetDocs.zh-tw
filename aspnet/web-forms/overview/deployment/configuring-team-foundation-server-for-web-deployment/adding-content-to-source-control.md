---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: 將內容新增至原始檔控制 |Microsoft Docs
author: jrjlee
description: 本主題說明如何將內容新增至原始檔控制 Team Foundation Server (TFS) 2010年中。 它說明如何將方案和專案加入至 team 專案...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 2119705a75d0717d05d4a7db69b3f5d38b1cdd45
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050855"
---
<a name="adding-content-to-source-control"></a><span data-ttu-id="7ab07-104">將內容新增至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="7ab07-104">Adding Content to Source Control</span></span>
====================
<span data-ttu-id="7ab07-105">藉由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="7ab07-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="7ab07-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="7ab07-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="7ab07-107">本主題說明如何將內容新增至原始檔控制 Team Foundation Server (TFS) 2010年中。</span><span class="sxs-lookup"><span data-stu-id="7ab07-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="7ab07-108">它會描述如何將方案和專案加入至 TFS 中 team 專案，並說明如何將類似的架構或組件的外部相依性新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>


<span data-ttu-id="7ab07-109">本主題是構成一系列以名為 Fabrikam，Inc.的虛構公司的企業部署需求為基礎的教學課程的一部分本教學課程系列會使用範例解決方案&#x2014;[連絡管理員解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;來代表實際的層級的複雜性，包括 ASP.NET MVC 3 應用程式時，Windows Communication 的 web 應用程式Foundation (WCF) 服務與資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="7ab07-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="7ab07-110">工作概觀</span><span class="sxs-lookup"><span data-stu-id="7ab07-110">Task Overview</span></span>

<span data-ttu-id="7ab07-111">在大部分情況下，每個開發小組成員應該可以將內容加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="7ab07-112">若要將方案加入至 TFS 中的原始檔控制中，您將需要完成下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="7ab07-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="7ab07-113">連接到 team 專案。</span><span class="sxs-lookup"><span data-stu-id="7ab07-113">Connect to a team project.</span></span>
- <span data-ttu-id="7ab07-114">將 team 專案的資料夾結構，在伺服器上對應至本機電腦上的資料夾結構中。</span><span class="sxs-lookup"><span data-stu-id="7ab07-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="7ab07-115">加入原始檔控制的方案和其內容。</span><span class="sxs-lookup"><span data-stu-id="7ab07-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="7ab07-116">加入原始檔控制中的任何外部相依性。</span><span class="sxs-lookup"><span data-stu-id="7ab07-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="7ab07-117">本主題將示範如何執行這些程序。</span><span class="sxs-lookup"><span data-stu-id="7ab07-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="7ab07-118">工作與本主題中的逐步解說假設，您已經建立新的 TFS team 專案來管理您的內容。</span><span class="sxs-lookup"><span data-stu-id="7ab07-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="7ab07-119">如需有關如何建立新的 team 專案的詳細資訊，請參閱 <<c0> [ 在 TFS 中建立 Team 專案](creating-a-team-project-in-tfs.md)。</span><span class="sxs-lookup"><span data-stu-id="7ab07-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="7ab07-120">對於執行這些程序？</span><span class="sxs-lookup"><span data-stu-id="7ab07-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="7ab07-121">在大部分情況下，每個開發小組成員應該能夠加入和修改特定的 team 專案內的內容。</span><span class="sxs-lookup"><span data-stu-id="7ab07-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="7ab07-122">連接到 Team 專案，並建立的資料夾對應</span><span class="sxs-lookup"><span data-stu-id="7ab07-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="7ab07-123">您將任何內容新增至原始檔控制之前，您需要連接到 team 專案，並在本機電腦上建立伺服器上的資料夾結構和檔案系統之間的對應。</span><span class="sxs-lookup"><span data-stu-id="7ab07-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="7ab07-124">**連接到 team 專案，並將對應的本機路徑**</span><span class="sxs-lookup"><span data-stu-id="7ab07-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="7ab07-125">在您開發人員工作站上，開啟 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="7ab07-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="7ab07-126">在 Visual Studio 中，在**Team**功能表上，按一下**連接到 Team Foundation Server**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ab07-127">如果您已經設定 TFS 伺服器的連接，您可以省略步驟 3-6。</span><span class="sxs-lookup"><span data-stu-id="7ab07-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="7ab07-128">在 [**連接至 Team 專案**] 對話方塊中，按一下**伺服器**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="7ab07-129">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="7ab07-130">在 [**加入 Team Foundation Server** ] 對話方塊中，提供您的 TFS 執行個體的詳細資料，然後按**確定**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="7ab07-131">在 [**新增/移除 Team Foundation Server** ] 對話方塊中，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="7ab07-132">在 **連接到 Team 專案** 對話方塊中，選取 TFS 執行個體，您想要連線，請選取 team 專案集合，選取您想要新增、 team 專案，然後按一下  **Connect**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="7ab07-133">在 [ **Team Explorer** ] 視窗中，展開您的 team 專案，然後按兩下**原始檔控制**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="7ab07-134">在 **原始檔控制總管**索引標籤上，按一下**未對應**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="7ab07-135">在**地圖**對話方塊中，於**本機資料夾**方塊中，瀏覽至 （或建立） 本機資料夾，以做為 team 專案的根資料夾，然後按一下**對應**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="7ab07-136">當系統提示您下載原始程式檔時，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="7ab07-137">到目前為止，您已對應的 team 專案的伺服器端資料夾至您的開發人員工作站上的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="7ab07-138">您也已經從 team 專案下載任何現有的內容，以您的本機資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="7ab07-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="7ab07-139">您現在可以開始將您自己的內容加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="7ab07-140">加入原始檔控制專案和方案</span><span class="sxs-lookup"><span data-stu-id="7ab07-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="7ab07-141">若要加入原始檔控制的專案和方案，您需要將本機電腦上將它們移至 team 專案的對應資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="7ab07-142">您接著可以簽入與伺服器同步處理新增的內容。</span><span class="sxs-lookup"><span data-stu-id="7ab07-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="7ab07-143">**若要將專案加入原始檔控制**</span><span class="sxs-lookup"><span data-stu-id="7ab07-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="7ab07-144">在您開發人員工作站上，將移至 team 專案對應的資料夾結構中的適當位置的專案和解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ab07-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7ab07-145">許多組織都會有慣用的方法，專案和方案應該組織的方式在原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="7ab07-146">如需有關資料夾結構的指引，請參閱[How To:結構，您在 Team Foundation Server 的原始檔控制資料夾](https://msdn.microsoft.com/library/bb668992.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ab07-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="7ab07-147">Visual Studio 2010 中開啟的方案。</span><span class="sxs-lookup"><span data-stu-id="7ab07-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="7ab07-148">在 [**方案總管**] 視窗中，以滑鼠右鍵按一下方案，然後**將方案加入至原始檔控制**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="7ab07-149">在某些情況下，視您的組織結構的內容，在 TFS 中，按讚的方式而定，您可能需要將專案加入原始檔控制，分別可提供更細微的控制，透過您的程式碼的組織方式。</span><span class="sxs-lookup"><span data-stu-id="7ab07-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="7ab07-150">確認**原始檔控制總管**索引標籤會顯示您已新增 team 專案的伺服器資料夾結構內的內容。</span><span class="sxs-lookup"><span data-stu-id="7ab07-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="7ab07-151">**原始檔控制總管**索引標籤會顯示您的內容不再提示，因為您將您的解決方案新增至本機檔案系統上的對應資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="7ab07-152">如果您的方案位於未對應的位置，系統會提示您指定 TFS 和您的本機檔案系統中的資料夾位置。</span><span class="sxs-lookup"><span data-stu-id="7ab07-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="7ab07-153">上**原始檔控制總管**索引標籤**資料夾**窗格中，以滑鼠右鍵按一下 team 專案 (比方說， **ContactManager**)，然後按一下 **簽入暫止的變更**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="7ab07-154">在 [**簽入 – 原始程式檔**] 對話方塊中，輸入註解，，然後按一下**簽入**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="7ab07-155">此時您已將您的方案加入原始檔控制在 TFS 中。</span><span class="sxs-lookup"><span data-stu-id="7ab07-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="7ab07-156">加入原始檔控制中的外部相依性</span><span class="sxs-lookup"><span data-stu-id="7ab07-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="7ab07-157">當您將專案或方案加入原始檔控制時，也會新增任何檔案和您的專案或方案中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="7ab07-158">不過，在許多情況下，專案和方案也依賴外部的相依性，例如本機的組件，才能正確運作。</span><span class="sxs-lookup"><span data-stu-id="7ab07-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="7ab07-159">您要加入至原始檔控制，讓 Team Build 和開發人員小組的其他成員的任何這類資源已成功建置程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ab07-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="7ab07-160">比方說，「 連絡人管理員 」 範例方案的資料夾結構包含名為套件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="7ab07-161">這用於 ADO.NET Entity Framework 4.1 包含組件和各種支援的資源。</span><span class="sxs-lookup"><span data-stu-id="7ab07-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="7ab07-162">[封裝] 資料夾不是屬於連絡管理員解決方案，但沒有它的方案將會成功建置。</span><span class="sxs-lookup"><span data-stu-id="7ab07-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="7ab07-163">若要啟用 Team Build 建置方案，您要加入原始檔控制中的 [packages] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7ab07-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="7ab07-164">包含的封裝資料夾是典型的 Entity Framework 或類似的資源，加入您使用 Visual Studio 2010 的 NuGet 擴充功能的解決方案時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="7ab07-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>


<span data-ttu-id="7ab07-165">**將非專案內容加入至原始檔控制**</span><span class="sxs-lookup"><span data-stu-id="7ab07-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="7ab07-166">請確定您想要新增 （例如，[封裝] 資料夾） 的項目位於您本機檔案系統上的對應資料夾內的適當位置。</span><span class="sxs-lookup"><span data-stu-id="7ab07-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="7ab07-167">在 Visual Studio 2010 中，在**Team Explorer**  視窗中，展開您的 team 專案，然後按兩下**原始檔控制**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="7ab07-168">在 **原始檔控制總管**索引標籤中，於**資料夾**窗格中，選取想要新增的資料夾包含的項目或項目。</span><span class="sxs-lookup"><span data-stu-id="7ab07-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="7ab07-169">按一下 [**新增至資料夾的項目**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ab07-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="7ab07-170">在 [**加入原始檔控制**對話方塊方塊中，選取資料夾或您想要新增，然後再按的項目**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="7ab07-171">在 **排除項目**索引標籤上，選取任何必要的項目，已自動排除 （例如，組件），然後按一下**包含的項目**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="7ab07-172">在 **要加入項目**索引標籤上，確認您想要包含的所有檔案會列出，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="7ab07-173">在 **原始檔控制總管** 視窗中，按一下**簽入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ab07-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="7ab07-174">在 [**簽入 – 原始程式檔**] 對話方塊中，輸入註解，，然後按一下**簽入**。</span><span class="sxs-lookup"><span data-stu-id="7ab07-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="7ab07-175">此時，您已新增外部的相依性為您的方案加入原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7ab07-176">結論</span><span class="sxs-lookup"><span data-stu-id="7ab07-176">Conclusion</span></span>

<span data-ttu-id="7ab07-177">本主題說明如何連接到 team 專案，將對應資料夾結構，並將內容加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="7ab07-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="7ab07-178">如需有關如何使用原始檔控制下的項目的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ab07-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="7ab07-179">下一個主題中，[設定 Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)，說明如何準備的 TFS Team Build server 建置和部署您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ab07-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="7ab07-180">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="7ab07-180">Further Reading</span></span>

<span data-ttu-id="7ab07-181">更廣泛使用在 TFS 中的原始檔控制的詳細資訊，請參閱[使用版本控制](https://msdn.microsoft.com/library/ms181368.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ab07-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ab07-182">[上一頁](creating-a-team-project-in-tfs.md)
> [下一頁](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="7ab07-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
