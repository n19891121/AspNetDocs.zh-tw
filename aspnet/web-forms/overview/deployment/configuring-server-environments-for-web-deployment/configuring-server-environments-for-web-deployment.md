---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 設定 Web 部署的伺服器環境 |Microsoft Docs
author: jrjlee
description: 本教學課程將示範如何設定伺服器環境，只要按一下，或自動化的支援網站部署，各種不同的畫面中的發行...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 4f6433f0b8a9ad3b3634c9bcd8d95015eebaa865
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043525"
---
<a name="configuring-server-environments-for-web-deployment"></a><span data-ttu-id="06baa-103">設定 Web 部署的伺服器環境</span><span class="sxs-lookup"><span data-stu-id="06baa-103">Configuring Server Environments for Web Deployment</span></span>
====================
<span data-ttu-id="06baa-104">藉由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="06baa-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="06baa-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="06baa-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="06baa-106">本教學課程會示範如何設定伺服器環境，以支援一種單鍵或自動化、 網站部署和發佈各種不同的案例中。</span><span class="sxs-lookup"><span data-stu-id="06baa-106">This tutorial will show you how to set up server environments to support one-click, or automated, website deployment and publishing in various different scenarios.</span></span> <span data-ttu-id="06baa-107">本教學課程包含的主題，以引導您完成各種工作，例如設定 web 伺服器，以支援特定的方法，來部署及設定 Web 伺服陣列架構 (WFF) 伺服器陣列，以及提供以案例為基礎的概觀較高層級的端對端指引。</span><span class="sxs-lookup"><span data-stu-id="06baa-107">The tutorial includes topics to walk you through completing various tasks, like configuring a web server to support specific approaches to deployment and setting up a Web Farm Framework (WFF) server farm, together with scenario-based overviews that provide higher-level end-to-end guidance.</span></span>
> 
> <span data-ttu-id="06baa-108">本教學課程會使用 Fabrikam，Inc.部署案例中所述[企業 Web 部署：案例概觀](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)作為參考點，如需範例和網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="06baa-108">The tutorial uses the Fabrikam, Inc. deployment scenario described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) as a reference point for examples and network infrastructure.</span></span>
> 
> <span data-ttu-id="06baa-109">這些教學課程義大利文翻譯，請瀏覽[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="06baa-109">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="06baa-110">本教學課程包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="06baa-110">This tutorial includes these topics:</span></span>

- [<span data-ttu-id="06baa-111">選擇 Web 部署的正確方法</span><span class="sxs-lookup"><span data-stu-id="06baa-111">Choosing the Right Approach to Web Deployment</span></span>](choosing-the-right-approach-to-web-deployment.md)
- [<span data-ttu-id="06baa-112">案例：設定 Web 部署的測試環境</span><span class="sxs-lookup"><span data-stu-id="06baa-112">Scenario: Configuring a Test Environment for Web Deployment</span></span>](scenario-configuring-a-test-environment-for-web-deployment.md)
- [<span data-ttu-id="06baa-113">案例：設定 Web 部署的預備環境</span><span class="sxs-lookup"><span data-stu-id="06baa-113">Scenario: Configuring a Staging Environment for Web Deployment</span></span>](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [<span data-ttu-id="06baa-114">案例：設定 Web 部署的生產環境</span><span class="sxs-lookup"><span data-stu-id="06baa-114">Scenario: Configuring a Production Environment for Web Deployment</span></span>](scenario-configuring-a-production-environment-for-web-deployment.md)
- [<span data-ttu-id="06baa-115">設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)</span><span class="sxs-lookup"><span data-stu-id="06baa-115">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [<span data-ttu-id="06baa-116">設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)</span><span class="sxs-lookup"><span data-stu-id="06baa-116">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [<span data-ttu-id="06baa-117">設定 Web Deploy 發行的網頁伺服器 (離線部署)</span><span class="sxs-lookup"><span data-stu-id="06baa-117">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [<span data-ttu-id="06baa-118">設定 Web Deploy 發行的資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="06baa-118">Configuring a Database Server for Web Deploy Publishing</span></span>](configuring-a-database-server-for-web-deploy-publishing.md)
- [<span data-ttu-id="06baa-119">使用 Web 伺服陣列架構建立伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="06baa-119">Creating a Server Farm with the Web Farm Framework</span></span>](creating-a-server-farm-with-the-web-farm-framework.md)
- [<span data-ttu-id="06baa-120">設定目標環境的部署屬性</span><span class="sxs-lookup"><span data-stu-id="06baa-120">Configuring Deployment Properties for a Target Environment</span></span>](configuring-deployment-properties-for-a-target-environment.md)

<span data-ttu-id="06baa-121">第一個主題中，[選擇 Web 部署的權限方法](choosing-the-right-approach-to-web-deployment.md)，描述主要的方法可用來發佈 web 應用程式，使用 Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0。</span><span class="sxs-lookup"><span data-stu-id="06baa-121">The first topic, [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md), describes the main approaches you can use to publish web applications by using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0.</span></span> <span data-ttu-id="06baa-122">它也會識別對應至每一種方法的案例。</span><span class="sxs-lookup"><span data-stu-id="06baa-122">It also identifies the scenarios that map to each approach.</span></span> <span data-ttu-id="06baa-123">從這裡開始，每個案例的主題會提供您需要完成的工作的高階概觀，並識別您要透過運作，可協助您完成這些工作的主題。</span><span class="sxs-lookup"><span data-stu-id="06baa-123">From here, each scenario topic provides a high-level overview of the tasks you need to complete and identifies the topics you'll need to work through to help you complete these tasks.</span></span>

<span data-ttu-id="06baa-124">如果您使用分割的專案檔案方法中所述[了解建置程序](../web-deployment-in-the-enterprise/understanding-the-build-process.md)來建置及部署您的方案，最後一個主題中，[設定部署屬性的目標環境](configuring-deployment-properties-for-a-target-environment.md)，說明如何設定以部署至不同目的地環境的特定環境的專案檔。</span><span class="sxs-lookup"><span data-stu-id="06baa-124">If you're using the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md) to build and deploy your solution, the final topic, [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md), describes how to configure environment-specific project files for deployment to different destination environments.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="06baa-125">主要技術</span><span class="sxs-lookup"><span data-stu-id="06baa-125">Key Technologies</span></span>

<span data-ttu-id="06baa-126">本教學課程著重於如何使用這些產品和技術來支援 web 部署：</span><span class="sxs-lookup"><span data-stu-id="06baa-126">This tutorial focuses on how to use these products and technologies to support web deployment:</span></span>

- <span data-ttu-id="06baa-127">IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="06baa-127">IIS 7.5</span></span>
- <span data-ttu-id="06baa-128">Web Deploy 2.x</span><span class="sxs-lookup"><span data-stu-id="06baa-128">Web Deploy 2.x</span></span>
- <span data-ttu-id="06baa-129">WFF 2.x</span><span class="sxs-lookup"><span data-stu-id="06baa-129">WFF 2.x</span></span>
- <span data-ttu-id="06baa-130">IIS Web 管理服務 (WMSvc)</span><span class="sxs-lookup"><span data-stu-id="06baa-130">IIS Web Management Service (WMSvc)</span></span>

<span data-ttu-id="06baa-131">本教學課程也會牽涉到 Windows Server 2008 R2 及 SQL Server 2008 R2、 ASP.NET 4.0 ASP.NET MVC 3 的使用。</span><span class="sxs-lookup"><span data-stu-id="06baa-131">The tutorial also touches on the use of Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="06baa-132">在這一系列的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="06baa-132">Other Tutorials in This Series</span></span>

<span data-ttu-id="06baa-133">這會形成企業級 web 部署的一系列五個教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="06baa-133">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="06baa-134">這些是系列中的其他教學課程：</span><span class="sxs-lookup"><span data-stu-id="06baa-134">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="06baa-135">[部署 Web 應用程式，在企業案例](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="06baa-135">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="06baa-136">此介紹的內容會提供教學課程系列中的內容相關的背景。</span><span class="sxs-lookup"><span data-stu-id="06baa-136">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="06baa-137">其中說明教學課程的案例中，並說明了如何工作和逐步解說所述，在整個系列納入更廣泛的應用程式生命週期管理 (ALM) 程序。</span><span class="sxs-lookup"><span data-stu-id="06baa-137">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="06baa-138">[Web 部署在企業中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="06baa-138">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="06baa-139">本教學課程提供 Microsoft Build Engine (MSBuild) 專案檔的概念性簡介、 Web 發行管線、 Web Deploy 和其他相關的技術。</span><span class="sxs-lookup"><span data-stu-id="06baa-139">This tutorial provides a conceptual introduction to Microsoft Build Engine (MSBuild) project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="06baa-140">它說明如何使用這些工具搭配來管理複雜的部署程序。</span><span class="sxs-lookup"><span data-stu-id="06baa-140">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="06baa-141">[設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="06baa-141">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="06baa-142">本教學課程說明如何設定 Team Foundation Server (TFS) 支援各種部署案例，包括持續整合 (CI) 程序的一部分自動的部署，並手動觸發的特定組建的部署。</span><span class="sxs-lookup"><span data-stu-id="06baa-142">This tutorial describes how to configure Team Foundation Server (TFS) to support various deployment scenarios, including automated deployment as part of a continuous integration (CI) process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="06baa-143">[進階企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="06baa-143">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="06baa-144">本教學課程說明如何完成各種進階的部署工作，例如自訂多個環境的資料庫部署、 從部署中排除檔案和資料夾以及部署程序期間取得 web 應用程式離線.</span><span class="sxs-lookup"><span data-stu-id="06baa-144">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="06baa-145">下一步</span><span class="sxs-lookup"><span data-stu-id="06baa-145">Next</span></span>](choosing-the-right-approach-to-web-deployment.md)
