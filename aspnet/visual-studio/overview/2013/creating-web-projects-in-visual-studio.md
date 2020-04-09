---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 在可視化工作室創建ASP.NET Web 專案 2013 |微軟文件
author: tdykstra
description: 本主題介紹在 Visual Studio 2013 中創建ASP.NET Web 專案的選項,其中介紹了 Web 開發中的一些新功能。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676045"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a><span data-ttu-id="546cb-103">在 Visual Studio 2013 中建立 ASP.NET Web 專案</span><span class="sxs-lookup"><span data-stu-id="546cb-103">Creating ASP.NET Web Projects in Visual Studio 2013</span></span>

<span data-ttu-id="546cb-104">湯姆[·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="546cb-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="546cb-105">本主題介紹使用 Update 3 在 Visual Studio 2013 中建立ASP.NET Web 專案的選項</span><span class="sxs-lookup"><span data-stu-id="546cb-105">This topic explains the options for creating ASP.NET web projects in Visual Studio 2013 with Update 3</span></span>
> 
> <span data-ttu-id="546cb-106">與早期版本的 Visual Studio 相比,以下是 Web 開發中的一些新功能:</span><span class="sxs-lookup"><span data-stu-id="546cb-106">Here are some of the new features for web development compared to earlier versions of Visual Studio:</span></span>
> 
> - <span data-ttu-id="546cb-107">用於建立支援[多個ASP.NET架構](#add)(Web 窗體、MVC 和 Web API)的專案的簡單 UI。</span><span class="sxs-lookup"><span data-stu-id="546cb-107">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](#add) (Web Forms, MVC, and Web API).</span></span>
> - <span data-ttu-id="546cb-108">[ASP.NET標識](#indauth),一個新的ASP.NET成員系統,在所有ASP.NET框架中都工作相同,並且與IIS以外的Web託管軟體配合使用。</span><span class="sxs-lookup"><span data-stu-id="546cb-108">[ASP.NET Identity](#indauth), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
> - <span data-ttu-id="546cb-109">使用[Bootstrap](#bootstrap)提供回應式設計和準備功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-109">The use of [Bootstrap](#bootstrap) to provide responsive design and theming capabilities.</span></span>
> - <span data-ttu-id="546cb-110">以前只為 MVC 提供的 Web 窗體的新功能,例如[自動測試項目建立](#testproj)與 Intranet[網站樣本](#winauth)。</span><span class="sxs-lookup"><span data-stu-id="546cb-110">New features for Web Forms that used to be offered only for MVC, such as [automatic test project creation](#testproj) and an [Intranet site template](#winauth).</span></span>
> 
> <span data-ttu-id="546cb-111">有關如何為 Azure 雲端服務或 Azure 行動服務建立 Web 專案的資訊,請參閱[使用 Azure 雲端服務開始使用「ASP.NET」](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)以及[使用 Azure 行動服務 .NET 後端建立排行榜應用](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。</span><span class="sxs-lookup"><span data-stu-id="546cb-111">For information about how to create web projects for Azure Cloud Services or Azure Mobile Services, see [Get Started with Azure Cloud Services and ASP.NET](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) and [Creating a Leaderboard App with Azure Mobile Services .NET Backend](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/).</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="546cb-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="546cb-112">Prerequisites</span></span>

<span data-ttu-id="546cb-113">本文適用於安裝了[更新 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的 Visual [Studio 2013。](https://go.microsoft.com/fwlink/?LinkId=306566)</span><span class="sxs-lookup"><span data-stu-id="546cb-113">This article applies to [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with [Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) installed.</span></span>

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a><span data-ttu-id="546cb-114">Web 應用程式專案與網站專案</span><span class="sxs-lookup"><span data-stu-id="546cb-114">Web application projects versus web site projects</span></span>

<span data-ttu-id="546cb-115">ASP.NET在兩種Web專案之間做出選擇 *:Web應用程式*專案和*網站專案*。</span><span class="sxs-lookup"><span data-stu-id="546cb-115">ASP.NET gives you a choice between two kinds of web projects: *web application projects* and *web site projects*.</span></span> <span data-ttu-id="546cb-116">我們建議 Web 應用程式專案用於新開發,本文僅適用於 Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="546cb-116">We recommend web application projects for new development, and this article applies only to web application projects.</span></span> <span data-ttu-id="546cb-117">有關詳細資訊,請參閱 MSDN 網站上的[Visual Studio 中的 Web 應用程式專案與網站專案](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-117">For more information, see [Web Application Projects versus Web Site Projects in Visual Studio](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) on the MSDN site.</span></span>

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a><span data-ttu-id="546cb-118">Web 應用程式項目建立概述</span><span class="sxs-lookup"><span data-stu-id="546cb-118">Overview of web application project creation</span></span>

<span data-ttu-id="546cb-119">以下步驟展示如何建立 Web 專案:</span><span class="sxs-lookup"><span data-stu-id="546cb-119">The following steps show how to create a web project:</span></span>

1. <span data-ttu-id="546cb-120">按下 **「開始」** 頁或 **「檔案**」 選單中的 **「新專案**」 。</span><span class="sxs-lookup"><span data-stu-id="546cb-120">Click **New Project** in the **Start** page or in the **File** menu.</span></span>
2. <span data-ttu-id="546cb-121">在**新項目對話**框中,按下左方窗格中的**Web,** 並在中間窗格**中按下 ASP.NET Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="546cb-121">In the **New Project** dialog, click **Web** in the left pane and **ASP.NET Web Application** in the middle pane.</span></span>

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image1.png)

    <span data-ttu-id="546cb-123">可以選擇左邊窗格中的 **「雲**」來建立[Azure 雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)[、Azure 行動服務](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或[Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。</span><span class="sxs-lookup"><span data-stu-id="546cb-123">You can choose **Cloud** in the left pane to create an [Azure Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure Mobile Service](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx), or [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs).</span></span> <span data-ttu-id="546cb-124">本主題不包括這些範本。</span><span class="sxs-lookup"><span data-stu-id="546cb-124">This topic doesn't cover those templates.</span></span>
3. <span data-ttu-id="546cb-125">在右邊窗格中,如果希望對應用程式進行運行狀況和使用方式監視,請按下 **「 將應用程式見解添加到專案**」複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-125">In the right pane, click the **Add Application Insights to Project** check box if you want health and usage monitoring for your application.</span></span> <span data-ttu-id="546cb-126">如需詳細資訊，請參閱[監視 Web 應用程式中的效能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。</span><span class="sxs-lookup"><span data-stu-id="546cb-126">For more information, see [Monitor performance in web applications](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/).</span></span>
4. <span data-ttu-id="546cb-127">指定項目**名稱**、**位置**和其他選項,然後按下 **「確定**」。</span><span class="sxs-lookup"><span data-stu-id="546cb-127">Specify project **Name**, **Location**, and other options, and then click **OK**.</span></span>

    <span data-ttu-id="546cb-128">[**新增 ASP.NET 專案**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="546cb-128">The **New ASP.NET Project** dialog appears.</span></span>

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image2.png)
5. <span data-ttu-id="546cb-130">單擊範本。</span><span class="sxs-lookup"><span data-stu-id="546cb-130">Click a template.</span></span>

    ![選取範本](creating-web-projects-in-visual-studio/_static/image3.png)
6. <span data-ttu-id="546cb-132">如果要添加對範本中未包括的其他框架的支援,請單擊相應的複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-132">If you want to add support for additional frameworks not included in the template, click the appropriate check box.</span></span> <span data-ttu-id="546cb-133">(在所示示例中,您可以將 MVC 和/或 Web API 添加到 Web 窗體專案中。</span><span class="sxs-lookup"><span data-stu-id="546cb-133">(In the example shown, you could add MVC and/or Web API to a Web Forms project.)</span></span>

    ![新增框架](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a><span data-ttu-id="546cb-135">如果要添加單元測試專案,請按一下「**添加單元測試**」。</span><span class="sxs-lookup"><span data-stu-id="546cb-135">If you want to add a unit test project, click **Add unit tests**.</span></span>

    ![新增單元測試](creating-web-projects-in-visual-studio/_static/image5.png)
8. <span data-ttu-id="546cb-137">如果想要與範本預設提供的身份驗證方法不同的身份驗證方法,請單擊「**更改身份驗證**」。</span><span class="sxs-lookup"><span data-stu-id="546cb-137">If you want a different authentication method than what the template provides by default, click **Change Authentication**.</span></span>

    ![設定驗證按鈕](creating-web-projects-in-visual-studio/_static/image6.png)

    ![設定驗證對話框](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a><span data-ttu-id="546cb-140">在 Azure 建立 Web 應用或虛擬機器</span><span class="sxs-lookup"><span data-stu-id="546cb-140">Create a web app or virtual machine in Azure</span></span>

<span data-ttu-id="546cb-141">Visual Studio 包含的功能,使使用 Azure 服務輕鬆託管 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-141">Visual Studio includes features that make it easy to work with Azure services for hosting web applications.</span></span> <span data-ttu-id="546cb-142">例如,您可以在 Visual Studio IDE 執行以下所有操作:</span><span class="sxs-lookup"><span data-stu-id="546cb-142">For example, you can do all of the following right from the Visual Studio IDE:</span></span>

- <span data-ttu-id="546cb-143">創建和管理 Web 應用或虛擬機器,使應用程式在 Internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="546cb-143">Create and manage web apps or virtual machines that make your application available over the Internet.</span></span>
- <span data-ttu-id="546cb-144">查看應用程式在雲端中執行時創建的紀錄。</span><span class="sxs-lookup"><span data-stu-id="546cb-144">View logs created by the application as it runs in the cloud.</span></span>
- <span data-ttu-id="546cb-145">應用程式在雲中運行時,在調試模式下遠端運行。</span><span class="sxs-lookup"><span data-stu-id="546cb-145">Run in debug mode remotely while the application runs in the cloud.</span></span>
- <span data-ttu-id="546cb-146">查看和管理其他 Azure 服務,如 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="546cb-146">View and manage other Azure services such as SQL databases.</span></span>

<span data-ttu-id="546cb-147">您可以創建包含基本服務(如免費 Web 應用)的[Azure 帳戶](https://www.windowsazure.com/pricing/free-trial/),如果您是 MSDN 訂閱者,則可以[啟動每月](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)為其他 Azure 服務提供積分的好處。</span><span class="sxs-lookup"><span data-stu-id="546cb-147">You can [create an Azure account](https://www.windowsazure.com/pricing/free-trial/) that includes basic services such as web apps for free, and if you are an MSDN subscriber you can [activate benefits](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) that give you monthly credits toward additional Azure services.</span></span> 

<span data-ttu-id="546cb-148">預設情況下,「**新建ASP.NET專案」** 對話框使您能夠為新 Web 專案建立 Web 應用或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="546cb-148">By default the **New ASP.NET Project** dialog box enables you to create a web app or virtual machine for a new web project.</span></span> <span data-ttu-id="546cb-149">如果不想創建新的 Web 應用或虛擬機,請清除**雲端中的「主機**」複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-149">If you don't want to create a new web app or virtual machine, clear the **Host in the cloud** check box.</span></span>

![建立遠端資源](creating-web-projects-in-visual-studio/_static/image8.png)

<span data-ttu-id="546cb-151">複選框標題可能是**雲中的主機**或**創建遠端資源**,在這兩種情況下效果都相同。</span><span class="sxs-lookup"><span data-stu-id="546cb-151">The check box caption might be **Host in the cloud** or **Create remote resources**, and in either case the effect is the same.</span></span> <span data-ttu-id="546cb-152">如果選中選取中該複選框,Visual Studio 預設情況下會在 Azure 應用服務中創建 Web 應用。</span><span class="sxs-lookup"><span data-stu-id="546cb-152">If you leave the check box selected, Visual Studio creates a web app in Azure App Service by default.</span></span> <span data-ttu-id="546cb-153">如果您願意,可以使用下拉框將此方塊更改為**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="546cb-153">You can use the drop-down box to change that to a **Virtual Machine** if you prefer.</span></span> <span data-ttu-id="546cb-154">如果您尚未登錄到 Azure,系統將提示您輸入 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="546cb-154">If you're not already signed in to Azure, you're prompted for Azure credentials.</span></span> <span data-ttu-id="546cb-155">登錄後,一個對話框允許您配置 Visual Studio 將為專案創建的資源。</span><span class="sxs-lookup"><span data-stu-id="546cb-155">After you sign in, a dialog box enables you to configure the resources that Visual Studio will create for your project.</span></span> <span data-ttu-id="546cb-156">下圖顯示了 Web 應用的對話方塊;如果選擇創建虛擬機,則會出現不同的選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-156">The following illustration shows the dialog for a web app; different options appear if you choose to create a virtual machine.</span></span>

![設定 Azure 應用設定](creating-web-projects-in-visual-studio/_static/image9.png)

<span data-ttu-id="546cb-158">有關如何使用此過程建立 Azure 資源的詳細資訊,請參閱使用 Azure[啟動和 ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)以及[使用 Visual Studio 為網站建立虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="546cb-158">For more information about how to use this process for creating Azure resources, see [Get Started with Azure and ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) and [Creating a virtual machine for a web site with Visual Studio](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/).</span></span>

<span data-ttu-id="546cb-159">本文的其餘部分提供了有關可用範本及其選項的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="546cb-159">The remainder of this article provides more information about the available templates and their options.</span></span> <span data-ttu-id="546cb-160">本文還介紹了範本中使用的 Bootstrap、佈局和準備框架。</span><span class="sxs-lookup"><span data-stu-id="546cb-160">The article also introduces Bootstrap, the layout and theming framework used in the templates.</span></span>

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a><span data-ttu-id="546cb-161">視覺化工作室 2013 Web 專案範本</span><span class="sxs-lookup"><span data-stu-id="546cb-161">Visual Studio 2013 Web Project Templates</span></span>

<span data-ttu-id="546cb-162">Visual Studio 使用範本創建 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="546cb-162">Visual Studio uses templates to create web projects.</span></span> <span data-ttu-id="546cb-163">專案範本可以在新項目中創建檔和資料夾,安裝 NuGet 包,並為基本工作應用程式提供範例代碼。</span><span class="sxs-lookup"><span data-stu-id="546cb-163">A project template can create files and folders in the new project, install NuGet packages, and provide sample code for a rudimentary working application.</span></span> <span data-ttu-id="546cb-164">樣本實現最新的 Web 標準,旨在展示如何使用 ASP.NET 技術的最佳做法,並讓您開始創建自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-164">Templates implement the latest web standards and are intended to demonstrate best practices for how to use ASP.NET technologies as well as give you a jump start on creating your own application.</span></span>

<span data-ttu-id="546cb-165">Visual Studio 2013 為針對 .NET 4.5 或更高版本的 .NET 框架的專案提供以下 Web 專案樣本選項:</span><span class="sxs-lookup"><span data-stu-id="546cb-165">Visual Studio 2013 provides the following choices for web project templates for projects that target .NET 4.5 or later versions of the .NET framework:</span></span>

- [<span data-ttu-id="546cb-166">空範本</span><span class="sxs-lookup"><span data-stu-id="546cb-166">Empty template</span></span>](#empty)
- [<span data-ttu-id="546cb-167">Web 表單範本</span><span class="sxs-lookup"><span data-stu-id="546cb-167">Web Forms template</span></span>](#wf)
- [<span data-ttu-id="546cb-168">MVC 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-168">MVC template</span></span>](#mvc)
- [<span data-ttu-id="546cb-169">Web API 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-169">Web API template</span></span>](#webapi)
- [<span data-ttu-id="546cb-170">單頁應用程式範本</span><span class="sxs-lookup"><span data-stu-id="546cb-170">Single Page Application template</span></span>](#spa)
- [<span data-ttu-id="546cb-171">Azure 行動服務範本</span><span class="sxs-lookup"><span data-stu-id="546cb-171">Azure Mobile Service template</span></span>](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [<span data-ttu-id="546cb-172">視覺工作室 2012 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-172">Visual Studio 2012 Templates</span></span>](#vs2012)

<span data-ttu-id="546cb-173">您還可以安裝提供[Facebook 範本](#facebook)的視覺工作室擴展。</span><span class="sxs-lookup"><span data-stu-id="546cb-173">You can also install a Visual Studio extension that provides a [Facebook template](#facebook).</span></span>

<span data-ttu-id="546cb-174">有關如何建立面向 .NET 4 的項目的資訊,請參閱本主題後面的[Visual Studio 2012 範本](#vs2012)。</span><span class="sxs-lookup"><span data-stu-id="546cb-174">For information about how to create projects that target .NET 4, see [Visual Studio 2012 Templates](#vs2012) later in this topic.</span></span>

<span data-ttu-id="546cb-175">有關如何為行動客戶端建立ASP.NET應用程式的資訊,請參閱 ASP.NET[中的行動支援](../../../mobile/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="546cb-175">For information about how to create ASP.NET applications for mobile clients, see [Mobile Support in ASP.NET](../../../mobile/overview.md).</span></span>

<a id="empty"></a>
### <a name="empty-template"></a><span data-ttu-id="546cb-176">空範本</span><span class="sxs-lookup"><span data-stu-id="546cb-176">Empty Template</span></span>

<span data-ttu-id="546cb-177">"空"樣本為ASP.NET Web 應用(如專案檔 *(.csproj*或 )提供最少的資料夾和檔。*vbproj*) 和*Web.config*檔。</span><span class="sxs-lookup"><span data-stu-id="546cb-177">The Empty template provides the bare minimum folders and files for an ASP.NET web app, such as a project file (*.csproj* or .*vbproj*) and a *Web.config* file.</span></span> <span data-ttu-id="546cb-178">您可以使用「**新增資料夾」 下的複選框和核心引用**:標籤,添加對 Web 窗體、MVC 和/或 Web API 的支援。</span><span class="sxs-lookup"><span data-stu-id="546cb-178">You can add support for Web Forms, MVC, and/or Web API by using the check boxes under the **Add folders and core references for:** label.</span></span>

<span data-ttu-id="546cb-179">對於空範本,沒有可用的身份驗證選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-179">For the Empty template no authentication options are available.</span></span> <span data-ttu-id="546cb-180">身份驗證功能在示例應用程式中實現,空範本不建立範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-180">Authentication functionality is implemented in sample applications, and the Empty template does not create a sample application.</span></span>

<a id="wf"></a>
### <a name="web-forms-template"></a><span data-ttu-id="546cb-181">Web 表單範本</span><span class="sxs-lookup"><span data-stu-id="546cb-181">Web Forms Template</span></span>

<span data-ttu-id="546cb-182">Web 表單結構框架提供以下功能,讓您能夠快速產生具有豐富 UI 和資料存取功能的網站:</span><span class="sxs-lookup"><span data-stu-id="546cb-182">The Web Forms framework provides the following features that let you rapidly build web sites that are rich in UI and data access features:</span></span>

- <span data-ttu-id="546cb-183">視覺工作室的 WYSIWYG 設計師。</span><span class="sxs-lookup"><span data-stu-id="546cb-183">A WYSIWYG designer in Visual Studio.</span></span>
- <span data-ttu-id="546cb-184">呈現 HTML 的伺服器控制項,以及可以透過設定屬性和樣式進行自訂的伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="546cb-184">Server controls that render HTML and that you can customize by setting properties and styles.</span></span>
- <span data-ttu-id="546cb-185">用於數據訪問和數據顯示的豐富類型控制項。</span><span class="sxs-lookup"><span data-stu-id="546cb-185">A rich assortment of controls for data access and data display.</span></span>
- <span data-ttu-id="546cb-186">公開事件的事件模型,您可以像對用戶端應用程式(如 WPF)進行程式設計一樣進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="546cb-186">An event model that exposes events which you can program like you would program a client application such as WPF.</span></span>
- <span data-ttu-id="546cb-187">自動在 HTTP 請求之間保留狀態(數據)。</span><span class="sxs-lookup"><span data-stu-id="546cb-187">Automatic preservation of state (data) between HTTP requests.</span></span>

<span data-ttu-id="546cb-188">通常,與使用ASP.NET MVC 框架創建同一應用程式相比,創建Web窗體應用程式所需的程式設計工作量更少。</span><span class="sxs-lookup"><span data-stu-id="546cb-188">In general, creating a Web Forms application requires less programming effort than creating the same application by using the ASP.NET MVC framework.</span></span> <span data-ttu-id="546cb-189">但是,Web 窗體並不僅僅用於快速應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="546cb-189">However, Web Forms is not just for rapid application development.</span></span> <span data-ttu-id="546cb-190">有許多複雜的商業應用程式和框架建立在 Web 窗體之上。</span><span class="sxs-lookup"><span data-stu-id="546cb-190">There are many complex commercial applications and frameworks built on top of Web Forms.</span></span>

<span data-ttu-id="546cb-191">由於 Web 窗體頁和頁面上的控制器會自動生成發送到瀏覽器的大部分標記,因此您沒有 ASP.NET MVC 提供的 HTML 的細粒度控制。</span><span class="sxs-lookup"><span data-stu-id="546cb-191">Because a Web Forms page and the controls on the page automatically generate much of the markup that's sent to the browser, you don't have the kind of fine-grained control over the HTML that ASP.NET MVC offers.</span></span> <span data-ttu-id="546cb-192">用於配置頁面和控制的聲明性模型最大限度地減少了必須編寫的代碼量,但隱藏了 HTML 和 HTTP 的某些行為。</span><span class="sxs-lookup"><span data-stu-id="546cb-192">The declarative model for configuring pages and controls minimizes the amount of code you have to write but hides some of the behavior of HTML and HTTP.</span></span> <span data-ttu-id="546cb-193">例如,並不總是能夠準確指定控制項可能生成哪些標記。</span><span class="sxs-lookup"><span data-stu-id="546cb-193">For example, it's not always possible to specify exactly what markup might be generated by a control.</span></span>

<span data-ttu-id="546cb-194">Web 表單框架不像 MVC ASP.NET 一樣容易適應基於模式的開發實作,例如[測試驅動開發](http://en.wikipedia.org/wiki/Test-driven_development)、[關注分離](http://en.wikipedia.org/wiki/Separation_of_concerns),[控制反向](http://en.wikipedia.org/wiki/Inversion_of_control)與[相依的 。](http://en.wikipedia.org/wiki/Dependency_injection)</span><span class="sxs-lookup"><span data-stu-id="546cb-194">The Web Forms framework doesn't lend itself as readily as ASP.NET MVC to patterns-based development practices such as [test-driven development](http://en.wikipedia.org/wiki/Test-driven_development), [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control), and [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection).</span></span> <span data-ttu-id="546cb-195">如果要用這種方式編寫分解的代碼,可以;它只是不像ASP.NETMVC框架那樣自動。</span><span class="sxs-lookup"><span data-stu-id="546cb-195">If you want to write code factored that way, you can; it's just not as automatic as it is in the ASP.NET MVC framework.</span></span> <span data-ttu-id="546cb-196">[ASP.NET Web 窗體 MVP](http://webformsmvp.com/)專案展示了一種有助於區分關注點和可測試性的方法,同時保持 Web 窗體為交付而構建的快速開發。</span><span class="sxs-lookup"><span data-stu-id="546cb-196">The [ASP.NET Web Forms MVP](http://webformsmvp.com/) project shows an approach that facilitates separation of concerns and testability while maintaining the rapid development that Web Forms was built to deliver.</span></span> <span data-ttu-id="546cb-197">微軟 SharePoint 建立在 Web 表單 MVP 之上。</span><span class="sxs-lookup"><span data-stu-id="546cb-197">Microsoft SharePoint is built on Web Forms MVP.</span></span>

<span data-ttu-id="546cb-198">Web 表單表板建立範例 Web 窗體應用程式,該應用程式使用[Bootstrap](#bootstrap)提供回應式設計和主發功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-198">The Web Forms template creates a sample Web Forms application that uses [Bootstrap](#bootstrap) to provide responsive design and theming features.</span></span> <span data-ttu-id="546cb-199">下圖顯示了主頁。</span><span class="sxs-lookup"><span data-stu-id="546cb-199">The following illustration shows the home page.</span></span>

![Web 表單範本應用程式主頁](creating-web-projects-in-visual-studio/_static/image10.png)

<span data-ttu-id="546cb-201">有關 Web 表單的詳細資訊,請參閱[ASP.NET Web 窗體](https://asp.net/web-forms)。</span><span class="sxs-lookup"><span data-stu-id="546cb-201">For more information about Web Forms, see [ASP.NET Web Forms](https://asp.net/web-forms).</span></span> <span data-ttu-id="546cb-202">有關 Web 表單樣本為您做什麼的資訊,請參閱使用[Visual Studio 2013 建構基本 Web 表單應用程式](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-202">For information about what the Web Forms template does for you, see [Building a basic Web Forms application using Visual Studio 2013](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx).</span></span>

<a id="mvc"></a>
### <a name="mvc-template"></a><span data-ttu-id="546cb-203">MVC 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-203">MVC Template</span></span>

<span data-ttu-id="546cb-204">ASP.NET MVC 旨在促進基於模式的開發實作,例如[測試驅動開發](http://en.wikipedia.org/wiki/Test-driven_development)、[關注分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反轉](http://en.wikipedia.org/wiki/Inversion_of_control)與[相依法 。](http://en.wikipedia.org/wiki/Dependency_injection)</span><span class="sxs-lookup"><span data-stu-id="546cb-204">ASP.NET MVC was designed to facilitate patterns-based development practices such as [test-driven development](http://en.wikipedia.org/wiki/Test-driven_development), [separation of concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control), and [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection).</span></span> <span data-ttu-id="546cb-205">該框架鼓勵將 Web 應用程式的業務邏輯層與其表示層分開。</span><span class="sxs-lookup"><span data-stu-id="546cb-205">The framework encourages separating the business logic layer of a web application from its presentation layer.</span></span> <span data-ttu-id="546cb-206">通過將應用程式劃分為模型 (M)、視圖 (V) 和控制器 (C),ASP.NET MVC 可以更輕鬆地管理較大應用程式中的複雜性。</span><span class="sxs-lookup"><span data-stu-id="546cb-206">By dividing the application into models (M), views (V), and controllers (C), ASP.NET MVC can make it easier to manage complexity in larger applications.</span></span>

<span data-ttu-id="546cb-207">使用ASP.NET MVC,您更直接地使用 HTML 和 HTTP 而不是 Web 窗體。</span><span class="sxs-lookup"><span data-stu-id="546cb-207">With ASP.NET MVC, you work more directly with HTML and HTTP than in Web Forms.</span></span> <span data-ttu-id="546cb-208">例如,Web 窗體可以在 HTTP 請求之間自動保留狀態,但您必須在 MVC 中顯式編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="546cb-208">For example, Web Forms can automatically preserve state between HTTP requests, but you have to code that explicitly in MVC.</span></span> <span data-ttu-id="546cb-209">MVC 模型的優點是,它使您能夠完全控制應用程式正在執行的操作以及它在 Web 環境中的表現。</span><span class="sxs-lookup"><span data-stu-id="546cb-209">The advantage of the MVC model is that it enables you to take complete control over exactly what your application is doing and how it behaves in the web environment.</span></span> <span data-ttu-id="546cb-210">缺點是您必須編寫更多的代碼。</span><span class="sxs-lookup"><span data-stu-id="546cb-210">The disadvantage is that you have to write more code.</span></span>

<span data-ttu-id="546cb-211">MVC 設計為可擴展,使電力開發人員能夠根據他們的應用程式需求自定義框架。</span><span class="sxs-lookup"><span data-stu-id="546cb-211">MVC was designed to be extensible, providing power developers the ability to customize the framework for their application needs.</span></span> <span data-ttu-id="546cb-212">此外,ASP.NET MVC 原始程式碼在 OSI 許可證下可用。</span><span class="sxs-lookup"><span data-stu-id="546cb-212">In addition, the ASP.NET MVC source code is available under an OSI license.</span></span>

<span data-ttu-id="546cb-213">MVC 模板創建一個範例 MVC 5 應用程式,該應用程式使用[Bootstrap](#bootstrap)提供回應式設計和主旋律功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-213">The MVC template creates a sample MVC 5 application that uses [Bootstrap](#bootstrap) to provide responsive design and theming features.</span></span> <span data-ttu-id="546cb-214">下圖顯示了主頁。</span><span class="sxs-lookup"><span data-stu-id="546cb-214">The following illustration shows the home page.</span></span>

![MVC 範例應用程式](creating-web-projects-in-visual-studio/_static/image11.png)

<span data-ttu-id="546cb-216">有關 MVC 的詳細資訊,請參閱[ASP.NET MVC](https://asp.net/mvc)。</span><span class="sxs-lookup"><span data-stu-id="546cb-216">For more information about MVC, see [ASP.NET MVC](https://asp.net/mvc).</span></span> <span data-ttu-id="546cb-217">有關如何選擇 MVC 4 樣本的資訊,請參閱本文後面的[Visual Studio 2012 樣本](#vs2012)。</span><span class="sxs-lookup"><span data-stu-id="546cb-217">For information about how to select the MVC 4 template, see [Visual Studio 2012 templates](#vs2012) later in this article.</span></span>

<a id="webapi"></a>
### <a name="web-api-template"></a><span data-ttu-id="546cb-218">Web API 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-218">Web API Template</span></span>

<span data-ttu-id="546cb-219">Web API 樣本基於 Web API 建立範例 Web 服務,包括基於 MVC 的 API 幫助頁。</span><span class="sxs-lookup"><span data-stu-id="546cb-219">The Web API template creates a sample web service based on Web API, including API help pages based on MVC.</span></span>

<span data-ttu-id="546cb-220">ASP.NET Web API 是一個架構，可輕易建置 HTTP 服務並擴及廣大的用戶端範圍，包括瀏覽器和行動裝置。</span><span class="sxs-lookup"><span data-stu-id="546cb-220">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="546cb-221">ASP.NET Web API 是在 .NET 框架上構建 RESTful 服務的理想平臺。</span><span class="sxs-lookup"><span data-stu-id="546cb-221">ASP.NET Web API is an ideal platform for building RESTful services on the .NET Framework.</span></span>

<span data-ttu-id="546cb-222">Web API 範本建立範例 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="546cb-222">The Web API template creates a sample web service.</span></span> <span data-ttu-id="546cb-223">下圖顯示了示例幫助頁。</span><span class="sxs-lookup"><span data-stu-id="546cb-223">The following illustrations show sample help pages.</span></span>

![Web API 說明頁](creating-web-projects-in-visual-studio/_static/image12.png)

![用於 GET API 的 Web API 說明頁](creating-web-projects-in-visual-studio/_static/image13.png)

<span data-ttu-id="546cb-226">有關 Web API 的詳細資訊,請參閱[ASP.NET Web API](https://asp.net/web-api)。</span><span class="sxs-lookup"><span data-stu-id="546cb-226">For more information about Web API, see [ASP.NET Web API](https://asp.net/web-api).</span></span>

<a id="spa"></a>
### <a name="single-page-application-template"></a><span data-ttu-id="546cb-227">單一網頁應用程式範本</span><span class="sxs-lookup"><span data-stu-id="546cb-227">Single Page Application Template</span></span>

<span data-ttu-id="546cb-228">單頁應用程式 (SPA) 樣本建立一個範例應用程式,該應用程式在用戶端上使用 JavaScript、HTML 5 和[挖空JS,](http://knockoutjs.com/)並在伺服器上 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="546cb-228">The Single Page Application (SPA) template creates a sample application that uses JavaScript, HTML 5, and [KnockoutJS](http://knockoutjs.com/) on the client, and ASP.NET Web API on the server.</span></span>

<span data-ttu-id="546cb-229">SPA 樣本的唯一身份驗證選項是[個人使用者帳戶](#indauth)。</span><span class="sxs-lookup"><span data-stu-id="546cb-229">The only authentication option for the SPA template is [Individual User Accounts](#indauth).</span></span>

<span data-ttu-id="546cb-230">下圖顯示了 SPA 範本生成的範例應用程式的初始狀態。</span><span class="sxs-lookup"><span data-stu-id="546cb-230">The following illustration shows the initial state of the sample application that the SPA template builds.</span></span>

![SPA 範例應用程式](creating-web-projects-in-visual-studio/_static/image14.png)

<span data-ttu-id="546cb-232">有關如何使用 SPA 樣本建立應用程式的資訊,請參閱[Web API - 外部身份驗證服務](../../../web-api/overview/security/external-authentication-services.md)。</span><span class="sxs-lookup"><span data-stu-id="546cb-232">For information about how to create an application by using the SPA template, see [Web API - External Authentication Services](../../../web-api/overview/security/external-authentication-services.md).</span></span>

<span data-ttu-id="546cb-233">有關ASP.NET單頁應用程式以及使用 JAVAScript 框架(而不是挖空JS)的其他 SPA 樣本的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="546cb-233">For more information about ASP.NET Single Page Applications, and about additional SPA templates that use JavaScript frameworks other than KnockoutJS, see the following resources:</span></span>

- <span data-ttu-id="546cb-234">[ASP.NET單頁應用程式](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="546cb-234">[ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- [<span data-ttu-id="546cb-235">瞭解 VS2013 RC SPA 樣本中的安全功能</span><span class="sxs-lookup"><span data-stu-id="546cb-235">Understanding Security Features in the SPA Template for VS2013 RC</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [<span data-ttu-id="546cb-236">單頁應用程式:使用ASP.NET建構現代、回應迅速的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-236">Single-Page Applications: Build Modern, Responsive Web Apps with ASP.NET</span></span>](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a><span data-ttu-id="546cb-237">Facebook 樣本</span><span class="sxs-lookup"><span data-stu-id="546cb-237">Facebook Template</span></span>

<span data-ttu-id="546cb-238">您可以安裝一個[視覺工作室擴展,提供一個Facebook範本](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="546cb-238">You can install a [Visual Studio extension that provides a Facebook template](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409).</span></span> <span data-ttu-id="546cb-239">此範本創建一個範例應用程式,該應用程式旨在在 Facebook 網站內運行。</span><span class="sxs-lookup"><span data-stu-id="546cb-239">This template creates a sample application that is designed to run inside the Facebook web site.</span></span> <span data-ttu-id="546cb-240">它基於ASP.NET MVC,並使用Web API進行即時更新功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-240">It is based on ASP.NET MVC and uses Web API for real-time update functionality.</span></span>

<span data-ttu-id="546cb-241">Facebook 範本沒有可用的身份驗證選項,因為 Facebook 應用程式在 Facebook 網站內運行,並且依賴於 Facebook 的身份驗證。</span><span class="sxs-lookup"><span data-stu-id="546cb-241">No authentication options are available for the Facebook template because Facebook applications run within the Facebook site and rely on Facebook's authentication.</span></span>

<span data-ttu-id="546cb-242">有關ASP.NET Facebook 應用程式的詳細資訊,請參閱[更新 MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-242">For more information about ASP.NET Facebook applications, see [Updating the MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx).</span></span>

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a><span data-ttu-id="546cb-243">視覺工作室 2012 範本</span><span class="sxs-lookup"><span data-stu-id="546cb-243">Visual Studio 2012 Templates</span></span>

<span data-ttu-id="546cb-244">Visual Studio 2013 Web 專案建立對話方塊不提供對 Visual Studio 2012 中提供的某些範本的訪問。</span><span class="sxs-lookup"><span data-stu-id="546cb-244">The Visual Studio 2013 web project creation dialog does not provide access to some templates that were available in Visual Studio 2012.</span></span> <span data-ttu-id="546cb-245">如果要使用這些範本之一,可以單擊"可視化工作室新項目"對話框左側窗格中的 Visual Studio 2012 節點。</span><span class="sxs-lookup"><span data-stu-id="546cb-245">If you want to use one of these templates, you can click the Visual Studio 2012 node in the left pane of the Visual Studio New Project dialog box.</span></span>

![視覺化工作室 2012 範本](creating-web-projects-in-visual-studio/_static/image15.png)

<span data-ttu-id="546cb-247">**Visual Studio 2012**節點允許您在 Visual Studio 2013 的預設樣本清單中選擇您無法存取的以下 Web 樣本:</span><span class="sxs-lookup"><span data-stu-id="546cb-247">The **Visual Studio 2012** node lets you choose the following web templates that you don't have access to in the default list of templates for Visual Studio 2013:</span></span>

- <span data-ttu-id="546cb-248">ASP.NET MVC 4 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-248">ASP.NET MVC 4 Web Application</span></span>
- <span data-ttu-id="546cb-249">ASP.NET 動態資料實體 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-249">ASP.NET Dynamic Data Entities Web Application</span></span>
- <span data-ttu-id="546cb-250">ASP.NET AJAX 伺服器控制</span><span class="sxs-lookup"><span data-stu-id="546cb-250">ASP.NET AJAX Server Control</span></span>
- <span data-ttu-id="546cb-251">ASP.NET AJAX 伺服器控制擴充器</span><span class="sxs-lookup"><span data-stu-id="546cb-251">ASP.NET AJAX Server Control Extender</span></span>
- <span data-ttu-id="546cb-252">ASP.NET 伺服器控制</span><span class="sxs-lookup"><span data-stu-id="546cb-252">ASP.NET Server Control</span></span>

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a><span data-ttu-id="546cb-253">視覺化工作室 2013 Web 專案範本中的引導</span><span class="sxs-lookup"><span data-stu-id="546cb-253">Bootstrap in the Visual Studio 2013 web project templates</span></span>

<span data-ttu-id="546cb-254">Visual Studio 2013 專案樣本使用[Bootstrap,](http://getbootstrap.com/)這是由 Twitter 創建的佈局和主框。</span><span class="sxs-lookup"><span data-stu-id="546cb-254">The Visual Studio 2013 project templates use [Bootstrap](http://getbootstrap.com/), a layout and theming framework created by Twitter.</span></span> <span data-ttu-id="546cb-255">Bootstrap 使用 CSS3 提供回應式設計,這意味著佈局可以動態適應不同的瀏覽器視窗大小。</span><span class="sxs-lookup"><span data-stu-id="546cb-255">Bootstrap uses CSS3 to provide responsive design, which means layouts can dynamically adapt to different browser window sizes.</span></span> <span data-ttu-id="546cb-256">例如,在寬瀏覽器視窗中,Web 窗體範本建立的主頁如下所示:</span><span class="sxs-lookup"><span data-stu-id="546cb-256">For example, in a wide browser window the home page created by the Web Forms template looks like the following illustration:</span></span>

![Web 表單範本應用程式主頁](creating-web-projects-in-visual-studio/_static/image16.png)

<span data-ttu-id="546cb-258">將視窗變窄,水平排列的欄移到垂直排列中:</span><span class="sxs-lookup"><span data-stu-id="546cb-258">Make the window narrower, and the horizontally arranged columns move into vertical arrangement:</span></span>

![開機垂直柱排列](creating-web-projects-in-visual-studio/_static/image17.png)

<span data-ttu-id="546cb-260">稍微縮小視窗範圍,水平頂部選單將變為一個圖示,您可以按下該圖示以展開垂直方向的選單:</span><span class="sxs-lookup"><span data-stu-id="546cb-260">Narrow the window a little more, and the horizontal top menu turns into an icon that you can click to expand into a vertically oriented menu:</span></span>

![開機選單圖示](creating-web-projects-in-visual-studio/_static/image18.png)

![開機垂直選單](creating-web-projects-in-visual-studio/_static/image19.png)

<span data-ttu-id="546cb-263">您還可以使用 Bootstrap 的「主」功能輕鬆影響應用程式的外觀和感覺的變化。</span><span class="sxs-lookup"><span data-stu-id="546cb-263">You can also use Bootstrap's theming feature to easily effect a change in the application's look and feel.</span></span> <span data-ttu-id="546cb-264">例如,您可以執行以下步驟來更改主題。</span><span class="sxs-lookup"><span data-stu-id="546cb-264">For example, you can do the following steps to change the theme.</span></span>

1. <span data-ttu-id="546cb-265">在瀏覽器中,轉到[http://Bootswatch.com](http://Bootswatch.com),選擇主題,然後單擊"**下載**"。</span><span class="sxs-lookup"><span data-stu-id="546cb-265">In your browser, go to [http://Bootswatch.com](http://Bootswatch.com), choose a theme, and then click **Download**.</span></span> <span data-ttu-id="546cb-266">(默認情況下,此下載*引導.min.css;* 如果要檢查 CSS 代碼,請獲取*引導.css*而不是小版本。</span><span class="sxs-lookup"><span data-stu-id="546cb-266">(This downloads *bootstrap.min.css* by default; if you want to examine the CSS code, get *bootstrap.css* instead of the minified version.)</span></span>
2. <span data-ttu-id="546cb-267">複製下載的 CSS 檔的內容。</span><span class="sxs-lookup"><span data-stu-id="546cb-267">Copy the contents of the downloaded CSS file.</span></span>
3. <span data-ttu-id="546cb-268">在 Visual Studio 中,在*內容*資料夾中創建名為*bootstrap-thethe.css*的新**樣式表**檔,並將下載的 CSS 代碼貼上到其中。</span><span class="sxs-lookup"><span data-stu-id="546cb-268">In Visual Studio, create a new **Style Sheet** file named *bootstrap-theme.css* in the *Content* folder and paste the downloaded CSS code into it.</span></span>
4. <span data-ttu-id="546cb-269">開啟*\_應用程式 開始/捆綁.設定*與變更*開機主機主題.css*.*bootstrap-theme.css*</span><span class="sxs-lookup"><span data-stu-id="546cb-269">Open *App\_Start/Bundle.config* and change *bootstrap.css* to *bootstrap-theme.css*.</span></span>

<span data-ttu-id="546cb-270">再次運行專案,應用程式具有新外觀。</span><span class="sxs-lookup"><span data-stu-id="546cb-270">Run the project again, and the application has a new look.</span></span> <span data-ttu-id="546cb-271">下圖顯示了阿米莉亞主題的效果:</span><span class="sxs-lookup"><span data-stu-id="546cb-271">The following illustration shows the effect of the Amelia theme:</span></span>

![靴子阿米莉亞主題](creating-web-projects-in-visual-studio/_static/image20.png)

<span data-ttu-id="546cb-273">許多引導主題是可用的,無論是免費和高級版本。</span><span class="sxs-lookup"><span data-stu-id="546cb-273">Many Bootstrap themes are available, both free and premium versions.</span></span> <span data-ttu-id="546cb-274">Bootstrap 提供多種 UI 元件,如[下拉](http://twitter.github.io/bootstrap/components.html#dropdowns),[按鈕群組](http://twitter.github.io/bootstrap/components.html#buttonGroups)與[圖示](http://twitter.github.io/bootstrap/base-css.html#images)。</span><span class="sxs-lookup"><span data-stu-id="546cb-274">Bootstrap also offers a wide variety of UI components, such as [drop-downs](http://twitter.github.io/bootstrap/components.html#dropdowns), [button groups](http://twitter.github.io/bootstrap/components.html#buttonGroups), and [icons](http://twitter.github.io/bootstrap/base-css.html#images).</span></span> <span data-ttu-id="546cb-275">有關引導器的詳細資訊,請參閱[引導網站](http://twitter.github.io/bootstrap/)。</span><span class="sxs-lookup"><span data-stu-id="546cb-275">For more information about Bootstrap, see [the Bootstrap site](http://twitter.github.io/bootstrap/).</span></span>

<span data-ttu-id="546cb-276">如果在 Visual Studio 中使用 Web 窗體設計器,請注意,設計器不支援 CSS3,因此無法準確顯示 Bootstrap 主題或回應式佈局更改的所有效果。</span><span class="sxs-lookup"><span data-stu-id="546cb-276">If you use the Web Forms designer in Visual Studio, note that the designer doesn't support CSS3, so it doesn't accurately show all the effects of Bootstrap themes or responsive layout changes.</span></span> <span data-ttu-id="546cb-277">但是,使用瀏覽器查看時,Web 窗體頁面將正確顯示。</span><span class="sxs-lookup"><span data-stu-id="546cb-277">However, the Web Forms pages will display correctly when viewed with a browser.</span></span>

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a><span data-ttu-id="546cb-278">新增對附加框架</span><span class="sxs-lookup"><span data-stu-id="546cb-278">Adding Support for Additional Frameworks</span></span>

<span data-ttu-id="546cb-279">選擇範本時,將自動選擇範本所使用的框架的複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-279">When you select a template, the check box for the framework(s) used by the template is automatically selected.</span></span> <span data-ttu-id="546cb-280">例如,如果選擇 **「Web 窗體」** 樣本,則選中 **「Web 窗體」** 複選框,但無法清除該範本。</span><span class="sxs-lookup"><span data-stu-id="546cb-280">For example, if you select the **Web Forms** template, the **Web Forms** check box is selected and you can't clear it.</span></span>

![選取範本](creating-web-projects-in-visual-studio/_static/image21.png)

![新增框架](creating-web-projects-in-visual-studio/_static/image22.png)

<span data-ttu-id="546cb-283">可以為範本中未包含的框架選擇複選框,以便在創建專案時添加對該框架的支援。</span><span class="sxs-lookup"><span data-stu-id="546cb-283">You can select the check box for a framework that isn't included in the template in order to add support for that framework when the project is created.</span></span> <span data-ttu-id="546cb-284">例如,要在選擇 MVC 範本時啟用 Web 窗體 *.aspx*頁面的使用,請選擇 **「Web 窗體」** 複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-284">For example, to enable the use of Web Forms *.aspx* pages when you've selected the MVC template, select the **Web Forms** check box.</span></span> <span data-ttu-id="546cb-285">或者,要在使用 Web 窗體範本時啟用 MVC,請單擊**MVC**複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-285">Or to enable MVC when you're using the Web Forms template, click the **MVC** check box.</span></span> <span data-ttu-id="546cb-286">添加框架可實現設計時和運行時支援。</span><span class="sxs-lookup"><span data-stu-id="546cb-286">Adding a framework enables design-time as well as run-time support.</span></span> <span data-ttu-id="546cb-287">例如,如果將 MVC 支援添加到 Web 窗體專案,則可以對控制器和視圖進行基架。</span><span class="sxs-lookup"><span data-stu-id="546cb-287">For example, if you add MVC support to a Web Forms project, you will be able to scaffold controllers and views.</span></span>

<span data-ttu-id="546cb-288">如果在專案中組合 Web 窗體和 MVC 並在 Web 窗體中啟用[友好 URL,](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)則可能存在意外的路由問題,其中一個 URL 具有多個可能的目標。</span><span class="sxs-lookup"><span data-stu-id="546cb-288">If you combine Web Forms and MVC in a project and enable [Friendly URLs](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) in Web Forms, there might be unexpected routing problems where one URL has multiple possible targets.</span></span> <span data-ttu-id="546cb-289">首先定義的路由將優先。</span><span class="sxs-lookup"><span data-stu-id="546cb-289">The routes that are defined first will take precedence.</span></span> <span data-ttu-id="546cb-290">例如`Home`,如果您有控制器和*Home.aspx*頁,`http://contoso.com/home`則如果在`Home``MapRoute``EnableFriendlyUrls``EnableFriendlyUrls``MapRoute` *RouteConfig.cs*調用 該方法之前調用 該方法,則 URL 將轉到*Home.aspx,* 或者,如果之前調用,則相同的 URL 將轉到控制器的預設檢視。</span><span class="sxs-lookup"><span data-stu-id="546cb-290">For example, if you have a `Home` controller and a *Home.aspx* page, the `http://contoso.com/home` URL will go to *Home.aspx* if you call the `EnableFriendlyUrls` method before you call the `MapRoute` method in *RouteConfig.cs*, or the same URL will go to the default view for your `Home` controller if you call `MapRoute` before `EnableFriendlyUrls`.</span></span>

<span data-ttu-id="546cb-291">添加框架不會添加任何範例應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-291">Adding a framework does not add any sample application functionality.</span></span> <span data-ttu-id="546cb-292">例如,如果在選擇 MVC 樣本時添加 Web 窗體支援,則不會創建*Default.aspx*主頁檔。</span><span class="sxs-lookup"><span data-stu-id="546cb-292">For example, if you add Web Forms support when you've selected the MVC template, no *Default.aspx* home page file is created.</span></span> <span data-ttu-id="546cb-293">僅添加支援框架所需的資料夾、檔案和引用。</span><span class="sxs-lookup"><span data-stu-id="546cb-293">Only the folders, files, and references required to support the framework are added.</span></span> <span data-ttu-id="546cb-294">因此,添加框架不會更改身份驗證選項,這些選項由範本創建的範例應用程式中的代碼實現。</span><span class="sxs-lookup"><span data-stu-id="546cb-294">For that reason, adding frameworks doesn't change authentication options, which are implemented by code in sample applications created by the templates.</span></span> <span data-ttu-id="546cb-295">例如,如果選擇「空範本」並添加 Web 窗體或 MVC 支援,則仍將禁用 **「設定身份驗證」** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="546cb-295">For example, if you select the Empty template and add Web Forms or MVC support, the **Configure Authentication** button will still be disabled.</span></span>

<span data-ttu-id="546cb-296">以下各節簡要描述每個複選框的效果。</span><span class="sxs-lookup"><span data-stu-id="546cb-296">The following sections describe briefly the effect of each check box.</span></span>

### <a name="add-web-forms-support"></a><span data-ttu-id="546cb-297">新增 Web 表單支援</span><span class="sxs-lookup"><span data-stu-id="546cb-297">Add Web Forms Support</span></span>

<span data-ttu-id="546cb-298">建立空*的應用\_資料和\*\*模型*資料夾和*全域.asax*檔案。</span><span class="sxs-lookup"><span data-stu-id="546cb-298">Creates empty *App\_Data* and *Models* folders and a *Global.asax* file.</span></span> <span data-ttu-id="546cb-299">這些範本已由空範本以外的所有範本創建,因此選擇"Web 窗體"複選框對其他範本沒有影響。</span><span class="sxs-lookup"><span data-stu-id="546cb-299">These are already created by all templates other than the Empty template, so selecting the Web Forms check box makes no difference for other templates.</span></span>

<span data-ttu-id="546cb-300">預設情況下,Web 窗體範本啟用友好 URL,但當您透過選擇「Web 窗體」複選框將 Web 窗體支援添加到其他樣本時,不會自動啟用"友好 URL"。</span><span class="sxs-lookup"><span data-stu-id="546cb-300">The Web Forms template enables Friendly URLs by default, but when you add Web Forms support to other templates by selecting the Web Forms check box Friendly URLs are not automatically enabled.</span></span>

### <a name="add-mvc-support"></a><span data-ttu-id="546cb-301">新增 MVC 支援</span><span class="sxs-lookup"><span data-stu-id="546cb-301">Add MVC Support</span></span>

<span data-ttu-id="546cb-302">安裝 MVC、Razor 和 WebPages NuGet 套件,建立空*的應用\_資料*,*控制器*,*模型*與*檢視*資料夾,使用*RouteConfig.cs*檔案建立*\_應用程式啟動*資料夾,並創建*Global.asax*檔。</span><span class="sxs-lookup"><span data-stu-id="546cb-302">Installs MVC, Razor, and WebPages NuGet packages, creates empty *App\_Data*, *Controllers*, *Models*, and *Views* folders, creates *App\_Start* folder with *RouteConfig.cs* file, and creates *Global.asax* file.</span></span>

### <a name="add-web-api-support"></a><span data-ttu-id="546cb-303">新增 Web API 支援</span><span class="sxs-lookup"><span data-stu-id="546cb-303">Add Web API Support</span></span>

<span data-ttu-id="546cb-304">安裝 WebApi 和 Newtonsoft.Json NuGet 套件,建立空*的應用程式\_資料*,*控制器*和*模型*資料夾,建立包含*WebApiConfig.cs*檔案*\_的應用程式啟動*資料夾,並創建*Global.asax*檔案。</span><span class="sxs-lookup"><span data-stu-id="546cb-304">Installs WebApi and Newtonsoft.Json NuGet packages, creates empty *App\_Data*, *Controllers*, and *Models* folders, creates *App\_Start* folder with *WebApiConfig.cs* file, and creates *Global.asax* file.</span></span>

<a id="auth"></a>
## <a name="authentication-methods"></a><span data-ttu-id="546cb-305">驗證方法</span><span class="sxs-lookup"><span data-stu-id="546cb-305">Authentication Methods</span></span>

<span data-ttu-id="546cb-306">Visual Studio 2013 為 Web 窗體、MVC 和 Web API 樣本提供多個身份驗證選項:</span><span class="sxs-lookup"><span data-stu-id="546cb-306">Visual Studio 2013 offers several authentication options for the Web Forms, MVC, and Web API templates:</span></span>

- [<span data-ttu-id="546cb-307">沒有認證</span><span class="sxs-lookup"><span data-stu-id="546cb-307">No Authentication</span></span>](#noauth)
- <span data-ttu-id="546cb-308">[個人使用者帳戶](#indauth)(ASP.NET標識,以前稱為ASP.NET成員資格)</span><span class="sxs-lookup"><span data-stu-id="546cb-308">[Individual User Accounts](#indauth) (ASP.NET Identity, formerly known as ASP.NET membership)</span></span>
- <span data-ttu-id="546cb-309">[組織帳號](#orgauth)(Windows 伺服器活動目錄或 Azure 活動目錄)</span><span class="sxs-lookup"><span data-stu-id="546cb-309">[Organizational Accounts](#orgauth) (Windows Server Active Directory or Azure Active Directory)</span></span>
- <span data-ttu-id="546cb-310">[視窗認證](#winauth)(內聯網)</span><span class="sxs-lookup"><span data-stu-id="546cb-310">[Windows Authentication](#winauth) (Intranet)</span></span>

![設定驗證對話框](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a><span data-ttu-id="546cb-312">不需要驗證</span><span class="sxs-lookup"><span data-stu-id="546cb-312">No Authentication</span></span>

<span data-ttu-id="546cb-313">如果選擇 **「無身份認證」 ,** 則範例將不包含用於登入的網頁、指示登入者使用的 UI、成員資格資料庫的實體類以及成員資格資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="546cb-313">If you select **No Authentication**, the sample application will contain no web pages for logging in, no UI indicating who is logged in, no entity classes for a membership database, and no connection string for a membership database.</span></span>

<a id="indauth"></a>
### <a name="individual-user-accounts"></a><span data-ttu-id="546cb-314">個別使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="546cb-314">Individual User Accounts</span></span>

<span data-ttu-id="546cb-315">如果選擇 **「個人使用者帳戶**」,則示例應用程式將配置為使用ASP.NET標識(以前稱為ASP.NET成員資格)進行使用者身份驗證。</span><span class="sxs-lookup"><span data-stu-id="546cb-315">If you select **Individual User Accounts**, the sample application will be configured to use ASP.NET Identity (formerly known as ASP.NET membership) for user authentication.</span></span> <span data-ttu-id="546cb-316">ASP.NET身份允許使用者透過在網站上創建使用者名稱和密碼或與 Facebook、Google、微軟帳戶或 Twitter 等社交供應商登錄來註冊帳戶。</span><span class="sxs-lookup"><span data-stu-id="546cb-316">ASP.NET Identity enables a user to register an account, by creating a username and password on the site or by signing in with social providers such as Facebook, Google, Microsoft Account, or Twitter.</span></span> <span data-ttu-id="546cb-317">ASP.NET識別中使用者配置檔的預設資料儲存是 SQL Server LocalDB 資料庫,您可以將該資料庫部署到生產網站的 SQL Server 或 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="546cb-317">The default data store for user profiles in ASP.NET Identity is a SQL Server LocalDB database, which you can deploy to SQL Server or Azure SQL Database for the production site.</span></span>

<span data-ttu-id="546cb-318">在 Visual Studio 2013 中,這些功能與 Visual Studio 2012 中的功能相同,但 ASP.NET 成員資格系統的基礎代碼已被重寫。</span><span class="sxs-lookup"><span data-stu-id="546cb-318">In Visual Studio 2013 these features are the same as in Visual Studio 2012, but the underlying code for the ASP.NET membership system has been rewritten.</span></span> <span data-ttu-id="546cb-319">新代碼庫的優點包括:</span><span class="sxs-lookup"><span data-stu-id="546cb-319">Advantages of the new code base include the following:</span></span>

- <span data-ttu-id="546cb-320">新的成員資格系統基於[OWIN](http://owin.org/)而不是ASP.NET窗體身份驗證模組。</span><span class="sxs-lookup"><span data-stu-id="546cb-320">The new membership system is based on [OWIN](http://owin.org/) rather than the ASP.NET Forms Authentication module.</span></span> <span data-ttu-id="546cb-321">這意味著無論您是在 IIS 中使用 Web 窗體還是 MVC,還是自託管 Web API 或 SignalR,您都可以使用相同的身份驗證機制。</span><span class="sxs-lookup"><span data-stu-id="546cb-321">This means that you can use the same authentication mechanism whether you're using Web Forms or MVC in IIS, or you're self-hosting Web API or SignalR.</span></span>
- <span data-ttu-id="546cb-322">新的成員資格資料庫由實體框架代碼優先管理,所有表都由可以修改的實體類表示。</span><span class="sxs-lookup"><span data-stu-id="546cb-322">The new membership database is managed by Entity Framework Code First, and all of the tables are represented by entity classes that you can modify.</span></span> <span data-ttu-id="546cb-323">這意味著您可以輕鬆地自定義資料庫架構和設定檔相關的 Web UI 以滿足您自己的需求,並且可以使用程式碼優先遷移輕鬆部署更新。</span><span class="sxs-lookup"><span data-stu-id="546cb-323">This means that you can easily customize the database schema and profile-related web UI to fit your own needs, and you can easily deploy your updates using Code First Migrations.</span></span>

<span data-ttu-id="546cb-324">新的成員資格系統在新範本中自動實現,可以在以 .NET 4.5 或更高版本為目標的任何專案中手動實現。</span><span class="sxs-lookup"><span data-stu-id="546cb-324">The new membership system is implemented automatically in the new templates, and it can be implemented manually in any project that targets .NET 4.5 or later.</span></span>

<span data-ttu-id="546cb-325">ASP.NET身份是一個不錯的選擇,如果你正在創建一個互聯網網站,主要是為外部客戶。</span><span class="sxs-lookup"><span data-stu-id="546cb-325">ASP.NET Identity is a good choice if you are creating an Internet web site which is mainly for external customers.</span></span> <span data-ttu-id="546cb-326">如果您的組織使用 Active Directory 或 Office 365,並且希望創建一個為員工和業務合作夥伴啟用單一登錄的專案,則 **「組織帳戶」** 選項可能是一個更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="546cb-326">If your organization uses Active Directory or Office 365 and you want to create a project that enables single-sign-on for employees and business partners, the **Organizational Accounts** option might be a better choice.</span></span>

<span data-ttu-id="546cb-327">有關「個人使用者帳戶」選項的詳細資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="546cb-327">For more information about the Individual User Accounts option, see the following resources:</span></span>

- <span data-ttu-id="546cb-328">[www.asp.net/identity](../../../identity/index.md).</span><span class="sxs-lookup"><span data-stu-id="546cb-328">[www.asp.net/identity](../../../identity/index.md).</span></span> <span data-ttu-id="546cb-329">有關ASP.NET網站上ASP.NET標識的文檔。</span><span class="sxs-lookup"><span data-stu-id="546cb-329">Documentation about ASP.NET Identity on the ASP.NET web site.</span></span>
- <span data-ttu-id="546cb-330">[建立 ASP.NETMVC 5 應用程式與 Facebook 和 GoogleAuth2 和開放 ID 登錄](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="546cb-330">[Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span> <span data-ttu-id="546cb-331">還演示如何自定義使用者配置文件數據。</span><span class="sxs-lookup"><span data-stu-id="546cb-331">Also shows how to customize user profile data.</span></span>
- [<span data-ttu-id="546cb-332">Web API - 外部認證服務</span><span class="sxs-lookup"><span data-stu-id="546cb-332">Web API - External Authentication Services</span></span>](../../../web-api/overview/security/external-authentication-services.md)
- [<span data-ttu-id="546cb-333">在 Visual Studio 2013 中向 ASP.NET 應用程式新增外部登入</span><span class="sxs-lookup"><span data-stu-id="546cb-333">Adding External Logins to your ASP.NET application in Visual Studio 2013</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a><span data-ttu-id="546cb-334">組織帳戶</span><span class="sxs-lookup"><span data-stu-id="546cb-334">Organizational Accounts</span></span>

<span data-ttu-id="546cb-335">如果選擇 **「組織帳戶**」,則示例應用程式將配置為使用 Windows 識別基礎 (WIF) 根據 Azure 活動目錄(Azure AD,包括 Office 365)或 Windows 伺服器活動目錄中的使用者帳戶進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="546cb-335">If you select **Organizational Accounts**, the sample application will be configured to use Windows Identity Foundation (WIF) for authentication based on user accounts in Azure Active Directory (Azure AD, which includes Office 365) or Windows Server Active Directory.</span></span> <span data-ttu-id="546cb-336">有關詳細資訊,請參閱本主題後面的[組織帳戶身份驗證選項](#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="546cb-336">For more information, see [Organizational account authentication options](#orgauthoptions) later in this topic.</span></span>

<a id="winauth"></a>
### <a name="windows-authentication"></a><span data-ttu-id="546cb-337">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="546cb-337">Windows Authentication</span></span>

<span data-ttu-id="546cb-338">如果選擇**Windows 身份驗證**,則示例應用程式將配置為使用 Windows 身份驗證 IIS 模組進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="546cb-338">If you select **Windows Authentication**, the sample application will be configured to use the Windows Authentication IIS module for authentication.</span></span> <span data-ttu-id="546cb-339">應用程式將顯示登入 Windows 但不包括使用者註冊或登入 UI 的 Active 目錄或本地電腦帳戶的網域和使用者 ID。</span><span class="sxs-lookup"><span data-stu-id="546cb-339">The application will display the domain and user ID of the Active directory or local machine account that is logged into Windows but won't include user registration or log-in UI.</span></span> <span data-ttu-id="546cb-340">此選項適用於 Intranet 網站。</span><span class="sxs-lookup"><span data-stu-id="546cb-340">This option is intended for Intranet web sites.</span></span>

<span data-ttu-id="546cb-341">或者,您可以通過在[組織帳戶下選擇"本地"選項](#orgauthonprem)來創建使用 AD 身份驗證的 Intranet 網站。</span><span class="sxs-lookup"><span data-stu-id="546cb-341">Alternatively, you can create an Intranet site that uses AD authentication by choosing the [On-Premises option under Organizational Accounts](#orgauthonprem).</span></span> <span data-ttu-id="546cb-342">「本地」選項使用 Windows 識別基礎 (WIF) 而不是 Windows 身份驗證模組。</span><span class="sxs-lookup"><span data-stu-id="546cb-342">The On-Premises option uses Windows Identity Foundation (WIF) instead of the Windows Authentication module.</span></span> <span data-ttu-id="546cb-343">需要執行一些其他步驟才能設置"本地"選項,但 WIF 啟用 Windows 身份驗證模組中不可用的功能。</span><span class="sxs-lookup"><span data-stu-id="546cb-343">Some additional steps are required in order to set up the On-Premises option, but WIF enables features that aren't available with the Windows Authentication module.</span></span> <span data-ttu-id="546cb-344">例如,使用 WIF 可以在 Active Directory 和查詢目錄數據中設定應用程式訪問。</span><span class="sxs-lookup"><span data-stu-id="546cb-344">For example, with WIF you can configure application access in Active Directory and query directory data.</span></span>

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a><span data-ttu-id="546cb-345">組織帳號身份驗證選項</span><span class="sxs-lookup"><span data-stu-id="546cb-345">Organizational account authentication options</span></span>

<span data-ttu-id="546cb-346">**設定身份驗證對話**框為 Azure 活動目錄(Azure AD,包括 Office 365)或 Windows 伺服器活動目錄 (AD) 帳戶身份驗證提供了多個選項:</span><span class="sxs-lookup"><span data-stu-id="546cb-346">The **Configure Authentication** dialog gives you several options for Azure Active Directory (Azure AD, which includes Office 365) or Windows Server Active Directory (AD) account authentication:</span></span>

- <span data-ttu-id="546cb-347">[雲 - 單個組織](#orgauthsingle)(使用與 Azure AD 的目錄整合的 Azure AD 或 AD)</span><span class="sxs-lookup"><span data-stu-id="546cb-347">[Cloud - Single Organization](#orgauthsingle) (Azure AD, or AD using directory integration with Azure AD)</span></span>
- <span data-ttu-id="546cb-348">[雲 - 多組織](#orgauthmulti)(使用目錄與 Azure AD 整合的 Azure AD 或 AD)</span><span class="sxs-lookup"><span data-stu-id="546cb-348">[Cloud - Multi Organization](#orgauthmulti) (Azure AD, or AD using directory integration with Azure AD)</span></span>
- <span data-ttu-id="546cb-349">[內部(AD)](#orgauthonprem)</span><span class="sxs-lookup"><span data-stu-id="546cb-349">[On-Premises](#orgauthonprem) (AD)</span></span>

<span data-ttu-id="546cb-350">如果要嘗試 Azure AD 選項之一,但尚未擁有帳戶,[請按下此處註冊 Azure AD 帳號](https://go.microsoft.com/fwlink/?LinkId=309942)。</span><span class="sxs-lookup"><span data-stu-id="546cb-350">If you want to try one of the Azure AD options but don't have an account yet, [click here to sign up for a Azure AD account](https://go.microsoft.com/fwlink/?LinkId=309942).</span></span>

> [!NOTE]
> <span data-ttu-id="546cb-351">如果選擇 Azure AD 選項之一,則專案需要資料庫,並且必須登錄到 Azure AD 租戶的全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="546cb-351">If you choose one of the Azure AD options, your project requires a database and you have to sign in to a global administrator account for your Azure AD tenant.</span></span> <span data-ttu-id="546cb-352">輸入具有 Azure AD 租戶管理許可權的組織帳戶admin@contoso.onmicrosoft.com的名稱 和密碼。</span><span class="sxs-lookup"><span data-stu-id="546cb-352">Enter the name and password for an organizational account (for example, admin@contoso.onmicrosoft.com) that has administrative permissions for your Azure AD tenant.</span></span>
> 
> <span data-ttu-id="546cb-353">**不要在登錄對話框中輸入 Microsoft 帳戶的認證(例如contoso@hotmail.com)。**</span><span class="sxs-lookup"><span data-stu-id="546cb-353">**Don't enter credentials for a Microsoft account (for example, contoso@hotmail.com) in the sign-in dialog box.**</span></span>

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a><span data-ttu-id="546cb-354">雲 - 單一組織認證</span><span class="sxs-lookup"><span data-stu-id="546cb-354">Cloud - Single Organization Authentication</span></span>

![單一組織識別](creating-web-projects-in-visual-studio/_static/image24.png)

<span data-ttu-id="546cb-356">如果要為一個 Azure AD[租戶](https://technet.microsoft.com/library/jj573650.aspx)中定義的使用者帳戶啟用身份驗證,請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-356">Choose this option if you want to enable authentication for user accounts that are defined in one Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx).</span></span> <span data-ttu-id="546cb-357">例如,該網站contoso.com,它將提供給 Contoso 公司位於租戶contoso.onmicrosoft.com的員工。</span><span class="sxs-lookup"><span data-stu-id="546cb-357">For example, the site is contoso.com and it will be made available to employees of the Contoso Company who are in the contoso.onmicrosoft.com tenant.</span></span> <span data-ttu-id="546cb-358">您將無法將 Azure AD 設定為允許其他租戶的使用者存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-358">You won't be able to configure Azure AD to allow users from other tenants to access the application.</span></span>

#### <a name="domain"></a><span data-ttu-id="546cb-359">網域</span><span class="sxs-lookup"><span data-stu-id="546cb-359">Domain</span></span>

<span data-ttu-id="546cb-360">輸入要在 中設定應用程式的 Azure AD`contoso.onmicrosoft.com`網域,例如:</span><span class="sxs-lookup"><span data-stu-id="546cb-360">Enter the Azure AD domain that you want to set up the application in, for example: `contoso.onmicrosoft.com`.</span></span> <span data-ttu-id="546cb-361">如果您有[自定義域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)`contoso.com`,`contoso.onmicrosoft.com`例如 , 可以在此處輸入該域。</span><span class="sxs-lookup"><span data-stu-id="546cb-361">If you have a [custom domain](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/), such as `contoso.com` instead of `contoso.onmicrosoft.com`, you can enter that here.</span></span>

#### <a name="access-level"></a><span data-ttu-id="546cb-362">存取層級</span><span class="sxs-lookup"><span data-stu-id="546cb-362">Access Level</span></span>

<span data-ttu-id="546cb-363">如果應用程式需要使用圖形 API 查詢或更新目錄資訊,請選擇**單一登入、讀取目錄資料**或**單一登入、讀取及寫入目錄資料**。</span><span class="sxs-lookup"><span data-stu-id="546cb-363">If the application needs to query or update directory information by using the Graph API, choose **Single Sign-On, Read Directory Data** or **Single Sign-On, Read and Write Directory Data**.</span></span> <span data-ttu-id="546cb-364">否則,請選擇**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="546cb-364">Otherwise, choose **Single Sign-On**.</span></span> <span data-ttu-id="546cb-365">有關詳細資訊,請參閱[應用程式存取等級](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)和使用圖形[API 查詢 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-365">For more information, see [Application Access Levels](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) and [Using the Graph API to Query Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx).</span></span>

#### <a name="application-id-uri"></a><span data-ttu-id="546cb-366">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="546cb-366">Application ID URI</span></span>

<span data-ttu-id="546cb-367">預設情況下,範本通過將專案名稱追加到 Azure AD 功能,為您創建應用程式 ID URI。</span><span class="sxs-lookup"><span data-stu-id="546cb-367">By default, the template creates an application ID URI for you by appending the project name to the Azure AD domain.</span></span> <span data-ttu-id="546cb-368">例如,如果專案名稱稱為`Example`,並且網`contoso.onmicrosoft.com`域為 ,則`https://contoso.onmicrosoft.com/Example`應用程式 ID URI 變為 。</span><span class="sxs-lookup"><span data-stu-id="546cb-368">For example, if the project name is `Example` and the domain is `contoso.onmicrosoft.com`, the application ID URI becomes `https://contoso.onmicrosoft.com/Example`.</span></span> <span data-ttu-id="546cb-369">如果要手動指定應用程式 ID URI,請展開 **「更多選項」** 部分,並在文字框中輸入應用程式 ID URI。</span><span class="sxs-lookup"><span data-stu-id="546cb-369">If you want to manually specify the application ID URI, expand the **More Options** section and enter the application ID URI in the text box.</span></span> <span data-ttu-id="546cb-370">應用程式識別碼必須`https://`以開頭。</span><span class="sxs-lookup"><span data-stu-id="546cb-370">The application ID URI must begin with `https://`.</span></span>

<span data-ttu-id="546cb-371">預設情況下,如果已在 Azure AD 中預配的應用程式具有與 Visual Studio 用於專案的應用程式 ID URI 相同的應用程式 ID URI,則專案將連接到現有應用程式,而不是預配新應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-371">By default, if an application that is already provisioned in Azure AD has the same application ID URI as the one that Visual Studio is using for the project, the project will be connected to the existing application instead of provisioning a new one.</span></span> <span data-ttu-id="546cb-372">如果希望在這種情況下預配新應用程式,**請清除「覆蓋應用程式項目」(如果具有相同 ID 的應用程式條目已存在**)複選框。</span><span class="sxs-lookup"><span data-stu-id="546cb-372">If you want a new application to be provisioned in that case, clear the **Overwrite the application entry if one with the same ID already exists** check box.</span></span>

<span data-ttu-id="546cb-373">如果清除 **「覆蓋**」複選框,並且 Visual Studio 尋找具有相同應用程式 ID URI 的現有應用程式,則透過將數位追加到要使用的 URI 來創建新 URI。</span><span class="sxs-lookup"><span data-stu-id="546cb-373">If the **Overwrite** check box is cleared, and Visual Studio finds an existing application with the same application ID URI, it creates a new URI by appending a number to the URI it was going to use.</span></span> <span data-ttu-id="546cb-374">例如,假設專案名稱為`Example`,您將文本框留空,清除**覆蓋**複選框,Azure AD 租戶`https://contoso.onmicrosoft.com/Example`已具有帶有 URI 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-374">For example, suppose the project name is `Example`, you leave the text box blank, you clear the **Overwrite** check box, and the Azure AD tenant already has an application with the URI `https://contoso.onmicrosoft.com/Example`.</span></span> <span data-ttu-id="546cb-375">在這種情況下,將預配一個新應用程式,並設定應用程式 ID URI,如`https://contoso.onmicrosoft.com/Example_20130619330903`。</span><span class="sxs-lookup"><span data-stu-id="546cb-375">In that case, a new application will be provisioned with an application ID URI like `https://contoso.onmicrosoft.com/Example_20130619330903`.</span></span>

#### <a name="provisioning-the-application-in-azure-ad"></a><span data-ttu-id="546cb-376">在 Azure AD 中預先應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-376">Provisioning the application in Azure AD</span></span>

<span data-ttu-id="546cb-377">為了在 Azure AD 中預配應用程式或將專案連接到現有應用程式,Visual Studio 需要域的全域管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="546cb-377">In order to provision the application in Azure AD or connect the project to an existing application, Visual Studio needs the credentials of a global administrator for the domain.</span></span> <span data-ttu-id="546cb-378">在「**設定身份驗證**」對話框中按下 **「確定」** 時,系統會提示您輸入您指定的網域的全域管理員的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="546cb-378">When you click **OK** in the **Configure Authentication** dialog box, you are prompted for the user name and password of a global administrator for the domain you specified.</span></span> <span data-ttu-id="546cb-379">稍後,當您按下 **「新建ASP.NET專案**」對話框中**創建專案**時,Visual Studio 在 Azure AD 中提供應用程式。</span><span class="sxs-lookup"><span data-stu-id="546cb-379">Later, when you click **Create Project** in the **New ASP.NET Project** dialog, Visual Studio provisions the application in Azure AD.</span></span> <span data-ttu-id="546cb-380">請注意,作為此過程的一部分,Visual Studio 會在 Web.config 檔中嵌入用戶端機密值,該檔在創建一年後過期。</span><span class="sxs-lookup"><span data-stu-id="546cb-380">Note that as part of this process Visual Studio embeds client secret values in the Web.config file that expire one year after creation.</span></span>

<span data-ttu-id="546cb-381">有關如何建立使用**雲 - 單一組織**認證的應用程式的資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="546cb-381">For information about how to create applications that use **Cloud - Single Organization** authentication, see the following resources:</span></span>

- [<span data-ttu-id="546cb-382">Azure 認證</span><span class="sxs-lookup"><span data-stu-id="546cb-382">Azure Authentication</span></span>](../2012/windows-azure-authentication.md)
- [<span data-ttu-id="546cb-383">使用 Azure AD 將登入新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-383">Adding Sign-On to Your Web Application Using Azure AD</span></span>](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [<span data-ttu-id="546cb-384">使用 Azure Active Dirctory 開發 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="546cb-384">Developing ASP.NET Apps with Azure Active Directory</span></span>](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [<span data-ttu-id="546cb-385">使用 Azure AD 和 Microsoft OWIN 元件ASP.NET Web API 安全</span><span class="sxs-lookup"><span data-stu-id="546cb-385">Secure ASP.NET Web API with Azure AD and Microsoft OWIN Components</span></span>](https://msdn.microsoft.com/magazine/dn463788.aspx)

<span data-ttu-id="546cb-386">Visual Studio 2013 的教程尚未更新;教程指導您手動執行的一些操作在 Visual Studio 2013 中是自動化的。</span><span class="sxs-lookup"><span data-stu-id="546cb-386">The tutorials have not yet been updated for Visual Studio 2013; some of what the tutorials direct you to do manually is automated in Visual Studio 2013.</span></span>

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a><span data-ttu-id="546cb-387">雲 - 多組織認證</span><span class="sxs-lookup"><span data-stu-id="546cb-387">Cloud - Multi Organization Authentication</span></span>

![多個組織身份驗證](creating-web-projects-in-visual-studio/_static/image25.png)

<span data-ttu-id="546cb-389">如果要為多個 Azure AD[租戶](https://technet.microsoft.com/library/jj573650.aspx)中定義的使用者帳戶啟用身份驗證,請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-389">Choose this option if you want to enable authentication for user accounts that are defined in multiple Azure AD [tenants](https://technet.microsoft.com/library/jj573650.aspx).</span></span> <span data-ttu-id="546cb-390">例如,該網站contoso.com,它將提供給 contoso 公司位於contoso.onmicrosoft.com租戶的員工以及法布裡卡姆公司fabrikam.onmicrosoft.com租戶的員工。</span><span class="sxs-lookup"><span data-stu-id="546cb-390">For example, the site is contoso.com and it will be made available to employees of the Contoso Company who are in the contoso.onmicrosoft.com tenant, and employees of the Fabrikam Company who are in the fabrikam.onmicrosoft.com tenant.</span></span>

<span data-ttu-id="546cb-391">輸入的設定與應用程式預先定義的步驟來顯示[單一個組織認證](#orgauthsingle)。</span><span class="sxs-lookup"><span data-stu-id="546cb-391">The settings that you enter and the application provisioning step are similar to [single organization authentication](#orgauthsingle).</span></span>

<span data-ttu-id="546cb-392">有關如何創建使用**雲 - 多組織**認證的應用程式的資訊,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="546cb-392">For information about how to create applications that use **Cloud - Multi Organization** authentication, see the following resources:</span></span>

- <span data-ttu-id="546cb-393">[輕鬆 Web 應用程式與&amp;Azure 活動 目錄整合,ASP.NET活動目錄團隊部落格上的視覺化工作室](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-393">[Easy Web App Integration with Azure Active Directory, ASP.NET &amp; Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) on the Active Directory Team blog.</span></span>
- <span data-ttu-id="546cb-394">[使用 Azure AD 教學開發多租戶 Web 應用程式](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)。</span><span class="sxs-lookup"><span data-stu-id="546cb-394">[Developing Multi-Tenant Web Applications with Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) tutorial.</span></span> <span data-ttu-id="546cb-395">本教程尚未更新為 Visual Studio 2013;本教學指導您手動執行的一些操作在 Visual Studio 2013 中是自動化的。</span><span class="sxs-lookup"><span data-stu-id="546cb-395">The tutorial hasn't yet been updated for Visual Studio 2013; some of what the tutorial directs you to do manually is automated in Visual Studio 2013.</span></span>
- <span data-ttu-id="546cb-396">[您必須在應用程式ASP.NET使用自己的多個組織註冊,然後才能登錄](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。</span><span class="sxs-lookup"><span data-stu-id="546cb-396">[You Have to Sign Up With Your Own Multiple Organizations ASP.NET App Before You Can Sign In](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/).</span></span> <span data-ttu-id="546cb-397">Vittorio Bertocci 的部落格,解釋如何解決人們在創建使用多組織身份驗證的專案時遇到的常見問題。</span><span class="sxs-lookup"><span data-stu-id="546cb-397">Blog by Vittorio Bertocci that explains how to resolve a common problem people encounter when creating a project that uses multi-organization authentication.</span></span>

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a><span data-ttu-id="546cb-398">本地組織身份驗證</span><span class="sxs-lookup"><span data-stu-id="546cb-398">On-Premises Organizational Authentication</span></span>

![本地組織身份驗證](creating-web-projects-in-visual-studio/_static/image26.png)

<span data-ttu-id="546cb-400">如果要為 Windows 伺服器活動目錄 (AD) 中定義的使用者帳戶啟用身份驗證,並且不想使用 Azure AD,請選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-400">Choose this option if you want to enable authentication for user accounts that are defined in Windows Server Active Directory (AD), and you don't want to use Azure AD.</span></span> <span data-ttu-id="546cb-401">您可以使用此選項創建 Intranet 網站或 Internet 網站。</span><span class="sxs-lookup"><span data-stu-id="546cb-401">You can use this option to create an Intranet site or an Internet site.</span></span> <span data-ttu-id="546cb-402">對於 Internet 網站,請使用活動目錄聯合服務 (ADFS) 提供對 AD 的訪問。</span><span class="sxs-lookup"><span data-stu-id="546cb-402">For an Internet site, use Active Directory Federation Services (ADFS) to provide access to AD.</span></span> <span data-ttu-id="546cb-403">有關詳細資訊,請參閱在[Visual Studio 2013 中使用具有ASP.NET的本地組織身份驗證選項 (ADFS)。](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)</span><span class="sxs-lookup"><span data-stu-id="546cb-403">For more information, see [Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/).</span></span>

<span data-ttu-id="546cb-404">對於 Intranet 網站,作為替代方法,您可以選擇[Windows 身份驗證](#winauth)而不是此選項。</span><span class="sxs-lookup"><span data-stu-id="546cb-404">For an Intranet site, as an alternative you can choose [Windows Authentication](#winauth) instead of this option.</span></span> <span data-ttu-id="546cb-405">對於 Windows 身份驗證選項,您不必提供中繼資料文件 URL。</span><span class="sxs-lookup"><span data-stu-id="546cb-405">For the Windows Authentication option you don't have to provide a metadata document URL.</span></span> <span data-ttu-id="546cb-406">但是,Windows 身份驗證無法控制活動目錄中的應用程序訪問或查詢目錄數據。</span><span class="sxs-lookup"><span data-stu-id="546cb-406">However, Windows Authentication does not give you the ability to control application access in Active Directory or to query directory data.</span></span>

#### <a name="on-premises-authority"></a><span data-ttu-id="546cb-407">內部管理局</span><span class="sxs-lookup"><span data-stu-id="546cb-407">On-Premises Authority</span></span>

<span data-ttu-id="546cb-408">輸入指向元資料文件的 URL。</span><span class="sxs-lookup"><span data-stu-id="546cb-408">Enter a URL that points to the metadata document.</span></span> <span data-ttu-id="546cb-409">元數據文件包含許可權的座標。</span><span class="sxs-lookup"><span data-stu-id="546cb-409">The metadata document contains the coordinates of the authority.</span></span> <span data-ttu-id="546cb-410">應用程式將使用這些座標來驅動 Web 登錄流。</span><span class="sxs-lookup"><span data-stu-id="546cb-410">The application will use those coordinates to drive the web sign-on flow.</span></span>

#### <a name="application-id-uri"></a><span data-ttu-id="546cb-411">應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="546cb-411">Application ID URI</span></span>

<span data-ttu-id="546cb-412">提供 AD 可用於識別此應用程式的唯一 URI,或留空以讓 Visual Studio 創建一個。</span><span class="sxs-lookup"><span data-stu-id="546cb-412">Provide a unique URI that AD can use to identify this application, or leave blank to let Visual Studio create one.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="546cb-413">後續步驟</span><span class="sxs-lookup"><span data-stu-id="546cb-413">Next steps</span></span>

<span data-ttu-id="546cb-414">本文件為在 Visual Studio 2013 中創建新 ASP.NET Web 專案提供了一些基本説明。</span><span class="sxs-lookup"><span data-stu-id="546cb-414">This document has provided some basic help for creating a new ASP.NET web project in Visual Studio 2013.</span></span> <span data-ttu-id="546cb-415">有關將 Visual Studio 用於 Web[https://www.asp.net/visual-studio/](../../index.md)開發的詳細資訊 ,請參閱。</span><span class="sxs-lookup"><span data-stu-id="546cb-415">For more information about using for Visual Studio for web development, see [https://www.asp.net/visual-studio/](../../index.md).</span></span>
