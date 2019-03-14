---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 案例：設定 Web 部署的預備環境 |Microsoft Docs
author: jrjlee
description: 本主題說明典型的 web 部署案例中的預備環境，並說明您需要完成，才能設定類似的環境的工作...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bee856c2ece6fda90ec35a87d111715def990603
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058365"
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="ecdc1-103">案例：設定 Web 部署的預備環境</span><span class="sxs-lookup"><span data-stu-id="ecdc1-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>
====================
<span data-ttu-id="ecdc1-104">藉由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ecdc1-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="ecdc1-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ecdc1-106">本主題描述預備環境的典型的 web 部署案例，並說明您需要完成，才能設定類似的環境的工作。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>


<span data-ttu-id="ecdc1-107">許多組織會使用預備環境來預覽 web 應用程式或網站的更新。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="ecdc1-108">這可讓組織內的人員有機會探索和站台 」 會上線，"，或也就部署至生產環境之前，檢閱新功能或內容。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="ecdc1-109">預備環境被設計來儘可能接近複寫生產環境，以便提供實際的預覽。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="ecdc1-110">這種預備環境通常具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="ecdc1-111">環境是由多個負載平衡的 web 伺服器和一或多個資料庫伺服器，通常與容錯移轉叢集和資料庫鏡像所組成。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="ecdc1-112">開發小組或自動 Team Build 的伺服器，可能會以手動方式部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="ecdc1-113">部署應用程式的處理序帳戶的使用者不太可能在臨時伺服器上具有系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="ecdc1-114">對應用程式部署頻繁地，因此必須支援單一步驟的環境，或自動部署。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="ecdc1-115">擴充資料庫部署到多部伺服器，已超出本教學課程的範圍。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="ecdc1-116">如需有關此區域的詳細資訊，請參閱[SQL Server 線上叢書 》](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>


<span data-ttu-id="ecdc1-117">例如，在我們[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)，Team Foundation Server (TFS) 中管理連絡管理員解決方案。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="ecdc1-118">TFS 系統管理員，Rob Walters 已建立組建定義，讓觸發部署至預備環境所需的開發人員。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="ecdc1-119">請注意，在大部分情況下，不一定要將最新的組建部署到預備環境。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="ecdc1-120">相反地，您更容易想要部署特定的組建尚未經過驗證和測試環境中的驗證。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="ecdc1-121">解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="ecdc1-121">Solution Overview</span></span>

<span data-ttu-id="ecdc1-122">在此案例中，您可以推算的部署需求分析這些事實：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="ecdc1-123">執行部署的使用者或處理序帳戶不會對系統管理員權限的預備伺服器，因此預備的 web 伺服器必須支援非系統管理員部署。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="ecdc1-124">因此，您必須設定臨時 web 伺服器來使用 Web 部署處理常式，而不是遠端代理程式。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="ecdc1-125">預備環境包含多個 web 伺服器，但它必須支援一種單鍵或自動化的部署，因此您必須使用建立伺服器陣列的 Web 伺服陣列架構 (WFF)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="ecdc1-126">使用這個方法，您可以部署一個網頁伺服器 （主要伺服器），應用程式，而且 WFF 會複寫所有其他 web 伺服器上的預備環境中部署。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="ecdc1-127">執行部署處理序帳戶的使用者必須具有建立資料庫的權限。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="ecdc1-128">因此，您必須將帳戶加入**dbcreator**在資料庫伺服器上，除了設定為支援遠端存取及部署資料庫伺服器的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="ecdc1-129">這些主題會提供您需要才能完成這些工作的所有資訊：</span><span class="sxs-lookup"><span data-stu-id="ecdc1-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="ecdc1-130">[使用 Web 伺服陣列架構建立伺服器陣列](creating-a-server-farm-with-the-web-farm-framework.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="ecdc1-131">本主題描述如何建立及設定使用 WFF，伺服器陣列，讓 web 平台產品和元件、 組態設定，以及網站和應用程式會複寫到多個負載平衡的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="ecdc1-132">[Web deploy 發行設定網頁伺服器 (Web Deploy 處理常式)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="ecdc1-133">本主題描述如何建置支援 Web Deploy 發行、 使用遠端代理程式的方法，從全新的 Windows Server 2008 R2 建置的 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="ecdc1-134">[設定資料庫伺服器，Web deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="ecdc1-135">本主題描述如何設定資料庫伺服器以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ecdc1-136">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="ecdc1-136">Further Reading</span></span>

<span data-ttu-id="ecdc1-137">如需設定的一般開發人員測試環境的指引，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="ecdc1-138">如需設定一般的生產環境的指引，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdc1-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ecdc1-139">[上一頁](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一頁](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="ecdc1-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
