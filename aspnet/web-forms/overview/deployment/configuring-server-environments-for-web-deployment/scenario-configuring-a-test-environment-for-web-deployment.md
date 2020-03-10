---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 案例：設定 Web 部署的測試環境 |Microsoft Docs
author: jrjlee
description: 本主題描述開發人員或測試環境的一般 web 部署案例，並說明您需要完成才能設定 si 的工作 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637813"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a><span data-ttu-id="d8921-103">案例：設定 Web 部署的測試環境</span><span class="sxs-lookup"><span data-stu-id="d8921-103">Scenario: Configuring a Test Environment for Web Deployment</span></span>

<span data-ttu-id="d8921-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d8921-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d8921-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="d8921-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d8921-106">本主題描述開發人員或測試環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。</span><span class="sxs-lookup"><span data-stu-id="d8921-106">This topic describes a typical web deployment scenario for developer or test environments and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="d8921-107">當開發人員在 web 應用程式上工作時，他們通常會被授與伺服器環境的存取權，讓他們可以在實際的設定下用來測試應用程式的變更。</span><span class="sxs-lookup"><span data-stu-id="d8921-107">When developers work on web applications, they're often given access to a server environment that they can use to test changes to their applications in a realistic setting.</span></span> <span data-ttu-id="d8921-108">這種開發或測試環境通常具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="d8921-108">This kind of development or test environment typically has these characteristics:</span></span>

- <span data-ttu-id="d8921-109">環境是由單一 web 伺服器和單一資料庫伺服器所組成。</span><span class="sxs-lookup"><span data-stu-id="d8921-109">The environment consists of a single web server and a single database server.</span></span>
- <span data-ttu-id="d8921-110">開發人員通常會在伺服器上擁有系統管理員許可權，讓他們將環境設定為其應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="d8921-110">The developers usually have administrator privileges on the servers, to let them configure the environment to the requirements of their applications.</span></span>
- <span data-ttu-id="d8921-111">應用程式的變更會經常部署，因此環境必須支援單一步驟或自動化部署。</span><span class="sxs-lookup"><span data-stu-id="d8921-111">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

<span data-ttu-id="d8921-112">例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Matt Hink 是 Fabrikam，inc. Matt 正致力於 Contact Manager 解決方案，並且定期需要將變更部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="d8921-112">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink is a developer at Fabrikam, Inc. Matt is working on the Contact Manager solution and regularly needs to deploy changes to a test environment.</span></span> <span data-ttu-id="d8921-113">Matt 是測試 web 伺服器和測試資料庫伺服器上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d8921-113">Matt is an administrator on the test web server and the test database server.</span></span> <span data-ttu-id="d8921-114">一開始，Matt 必須能夠直接將解決方案部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="d8921-114">Initially, Matt needs to be able to deploy the solution to the test environment directly.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="d8921-115">隨著工作進展和更多開發人員加入小組，Contact Manager 解決方案會針對 Team Foundation Server （TFS）中的持續整合（CI）進行設定。</span><span class="sxs-lookup"><span data-stu-id="d8921-115">As work progresses and more developers join the team, the Contact Manager solution is configured for continuous integration (CI) in Team Foundation Server (TFS).</span></span> <span data-ttu-id="d8921-116">每當開發人員簽入內容時，Team Build 應該會建立方案、執行任何單元測試，並將方案自動部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="d8921-116">Whenever a developer checks in content, Team Build should build the solution, run any unit tests, and automatically deploy the solution to the test environment.</span></span>

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a><span data-ttu-id="d8921-117">方案概觀</span><span class="sxs-lookup"><span data-stu-id="d8921-117">Solution Overview</span></span>

<span data-ttu-id="d8921-118">測試環境必須支援遠端電腦的單一步驟或自動化部署，因此您可以選擇兩個主要方法。</span><span class="sxs-lookup"><span data-stu-id="d8921-118">The test environment needs to support single-step or automated deployment from a remote computer, so you have a choice of two main approaches.</span></span> <span data-ttu-id="d8921-119">您可以：</span><span class="sxs-lookup"><span data-stu-id="d8921-119">You can:</span></span>

- <span data-ttu-id="d8921-120">設定測試 web 伺服器，以支援使用 Web Deployment Agent 服務（「遠端代理程式」）進行部署。</span><span class="sxs-lookup"><span data-stu-id="d8921-120">Configure the test web server to support deployment using the Web Deployment Agent Service (the "remote agent").</span></span>
- <span data-ttu-id="d8921-121">設定測試 web 伺服器，以支援使用 Web Deploy 處理常式進行部署。</span><span class="sxs-lookup"><span data-stu-id="d8921-121">Configure the test web server to support deployment using the Web Deploy handler.</span></span>

> [!NOTE]
> <span data-ttu-id="d8921-122">您也可以[視需要使用 Web Deploy](https://technet.microsoft.com/library/ee517345(WS.10).aspx) （「temp 代理程式」）。</span><span class="sxs-lookup"><span data-stu-id="d8921-122">You could also use [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx) (the "temp agent").</span></span> <span data-ttu-id="d8921-123">這類似于在需求和條件約束方面的遠端代理程式方法。</span><span class="sxs-lookup"><span data-stu-id="d8921-123">This is similar to the remote agent approach in terms of requirements and constraints.</span></span>

<span data-ttu-id="d8921-124">在此情況下，開發人員在目的地伺服器上具有系統管理員許可權，而且測試環境不受嚴格的安全性限制，因此邏輯選擇是將測試 web 伺服器設定為支援使用遠端代理程式進行部署。</span><span class="sxs-lookup"><span data-stu-id="d8921-124">In this case, the developers have administrator privileges on the destination servers, and the test environment is not subject to strict security constraints, so the logical choice is to configure the test web server to support deployment using the remote agent.</span></span> <span data-ttu-id="d8921-125">這比較不復雜，而且需要的初始設定比 Web Deploy 處理常式方法少。</span><span class="sxs-lookup"><span data-stu-id="d8921-125">This is less complex and requires less initial configuration than the Web Deploy Handler approach.</span></span> <span data-ttu-id="d8921-126">您也需要設定您的資料庫伺服器，以支援遠端存取和部署。</span><span class="sxs-lookup"><span data-stu-id="d8921-126">You'll also need to configure your database server to support remote access and deployment.</span></span>

<span data-ttu-id="d8921-127">這些主題提供完成這些工作所需的所有資訊：</span><span class="sxs-lookup"><span data-stu-id="d8921-127">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="d8921-128">[設定用於 Web Deploy 發佈的網頁伺服器（遠端代理程式）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="d8921-128">[Configure a Web Server for Web Deploy Publishing (Remote Agent)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span> <span data-ttu-id="d8921-129">本主題說明如何使用遠端代理程式方法（從全新的 Windows Server 2008 R2 組建開始），建立支援 Web Deploy 發行的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="d8921-129">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="d8921-130">[設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="d8921-130">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="d8921-131">本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。</span><span class="sxs-lookup"><span data-stu-id="d8921-131">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d8921-132">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="d8921-132">Further Reading</span></span>

<span data-ttu-id="d8921-133">如需設定一般預備環境的指引，請參閱[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="d8921-133">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span> <span data-ttu-id="d8921-134">如需設定一般生產環境的指引，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="d8921-134">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d8921-135">[上一頁](choosing-the-right-approach-to-web-deployment.md)
> [下一頁](scenario-configuring-a-staging-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="d8921-135">[Previous](choosing-the-right-approach-to-web-deployment.md)
[Next](scenario-configuring-a-staging-environment-for-web-deployment.md)</span></span>
