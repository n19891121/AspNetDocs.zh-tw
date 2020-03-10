---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: 使用 Web 伺服陣列架構建立伺服器陣列 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 Web 伺服陣列架構（WFF）2.0，從伺服器集合建立和設定 web 伺服器陣列。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637246"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a><span data-ttu-id="49d63-103">使用 Web 伺服陣列架構建立伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="49d63-103">Creating a Server Farm with the Web Farm Framework</span></span>

<span data-ttu-id="49d63-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="49d63-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="49d63-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="49d63-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="49d63-106">本主題描述如何使用 Web 伺服陣列架構（WFF）2.0，從伺服器集合建立和設定 web 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-106">This topic describes how to use the Web Farm Framework (WFF) 2.0 to create and configure a web server farm from a collection of servers.</span></span>

<span data-ttu-id="49d63-107">WFF 可讓您跨多個負載平衡的 web 伺服器同步處理 web 平台產品和元件、web 應用程式、網站和設定。</span><span class="sxs-lookup"><span data-stu-id="49d63-107">WFF lets you synchronize web platform products and components, web applications, websites, and configuration settings across multiple load-balanced web servers.</span></span> <span data-ttu-id="49d63-108">在您需要一部以上的 web 伺服器（例如預備和生產環境）的案例中，這可能會大幅簡化您的部署和設定程式。</span><span class="sxs-lookup"><span data-stu-id="49d63-108">In scenarios where you need more than one web server, like staging and production environments, this can vastly simplify your deployment and configuration process.</span></span> <span data-ttu-id="49d63-109">您可以將 web 應用程式部署到單一伺服器&#x2014;*主伺服器*&#x2014;，而 WFF 會在伺服器陣列中的所有其他 web 伺服器上自動複寫該 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="49d63-109">You can deploy a web application to a single server&#x2014;the *primary server*&#x2014;and WFF will automatically replicate that web application on all the other web servers in the server farm.</span></span>

## <a name="understanding-the-web-farm-framework"></a><span data-ttu-id="49d63-110">瞭解 Web 伺服陣列架構</span><span class="sxs-lookup"><span data-stu-id="49d63-110">Understanding the Web Farm Framework</span></span>

<span data-ttu-id="49d63-111">您可以使用 WFF 2.0 來布建、管理及部署內容到一組網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-111">You can use WFF 2.0 to provision, manage, and deploy content to a group of web servers.</span></span> <span data-ttu-id="49d63-112">WFF 部署包含三個主要伺服器角色：</span><span class="sxs-lookup"><span data-stu-id="49d63-112">A WFF deployment consists of three key server roles:</span></span>

- <span data-ttu-id="49d63-113">*控制器伺服器*。</span><span class="sxs-lookup"><span data-stu-id="49d63-113">The *controller server*.</span></span> <span data-ttu-id="49d63-114">您可以使用此伺服器來建立及設定 WFF 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-114">You use this server to create and configure WFF server farms.</span></span> <span data-ttu-id="49d63-115">控制器伺服器會管理伺服器陣列中網頁伺服器之間的 web 平臺元件、設定和應用程式的同步處理。</span><span class="sxs-lookup"><span data-stu-id="49d63-115">The controller server manages the synchronization of web platform components, configuration settings, and applications between the web servers in a server farm.</span></span> <span data-ttu-id="49d63-116">您會在控制器伺服器上安裝 WFF 2.0，而控制器伺服器會接著在伺服器陣列中的每部伺服器上安裝 WFF 代理程式。</span><span class="sxs-lookup"><span data-stu-id="49d63-116">You install WFF 2.0 on the controller server, and the controller server will in turn install the WFF agent on each of the servers in a server farm.</span></span> <span data-ttu-id="49d63-117">控制器伺服器在概念上不屬於任何 WFF 伺服器陣列，而單一控制器伺服器可以管理多個伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-117">The controller server does not conceptually belong to any WFF server farm, and a single controller server can manage multiple server farms.</span></span> <span data-ttu-id="49d63-118">在此案例中，您會使用單一的 WFF 控制器伺服器來建立和管理預備伺服器陣列與實際執行伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-118">In this scenario, you use a single WFF controller server to create and manage the staging server farm and the production server farm.</span></span>
- <span data-ttu-id="49d63-119">*主伺服器*。</span><span class="sxs-lookup"><span data-stu-id="49d63-119">The *primary server*.</span></span> <span data-ttu-id="49d63-120">每個 WFF 伺服器陣列都包含單一的主伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-120">Each WFF server farm includes a single primary server.</span></span> <span data-ttu-id="49d63-121">當您安裝 web platform 元件或將應用程式部署到主伺服器時，WFF 會同步處理您對伺服器陣列中所有其他伺服器的變更。</span><span class="sxs-lookup"><span data-stu-id="49d63-121">When you install web platform components or deploy applications to the primary server, the WFF synchronizes your changes to all the other servers in the server farm.</span></span>
- <span data-ttu-id="49d63-122">*次要伺服器*。</span><span class="sxs-lookup"><span data-stu-id="49d63-122">The *secondary server*.</span></span> <span data-ttu-id="49d63-123">每個 WFF 伺服器陣列都包含一或多部次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-123">Each WFF server farm includes one or more secondary servers.</span></span> <span data-ttu-id="49d63-124">您對主伺服器所做的任何變更都會複寫到伺服器陣列內的每一部次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-124">Any changes you make to the primary server are replicated to every secondary server within the server farm.</span></span>

<span data-ttu-id="49d63-125">這會顯示這些伺服器角色與 Fabrikam、Inc 和生產環境之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="49d63-125">This shows how these server roles relate to the Fabrikam, Inc. staging and production environments:</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

<span data-ttu-id="49d63-126">在此案例中，預備環境和生產環境都設定為 WFF 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-126">In this scenario, the staging environment and the production environment are both configured as WFF server farms.</span></span> <span data-ttu-id="49d63-127">單一 WFF 控制器伺服器會管理這兩個伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-127">A single WFF controller server manages both farms.</span></span> <span data-ttu-id="49d63-128">在每個伺服器陣列中，對主伺服器所做的任何變更都會複寫到每個次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-128">Within each server farm, any changes to the primary server are replicated to every secondary server.</span></span>

<span data-ttu-id="49d63-129">在您開始設定預備和生產環境之前，建議您先閱讀下列文章，以熟悉 WFF 2.0 的重要概念：</span><span class="sxs-lookup"><span data-stu-id="49d63-129">Before you start to configure your staging and production environments, we recommend that you read these articles to familiarize yourself with the key concepts of WFF 2.0:</span></span>

- [<span data-ttu-id="49d63-130">IIS 7 的 Web Farm Framework 2.0 總覽</span><span class="sxs-lookup"><span data-stu-id="49d63-130">Overview of the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805126)
- [<span data-ttu-id="49d63-131">使用 Web Farm Framework 2.0 為 IIS 7 設定伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="49d63-131">Setting up a Server Farm with the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805127)
- [<span data-ttu-id="49d63-132">適用于 IIS 7 之 Web Farm Framework 2.0 的系統和平臺需求</span><span class="sxs-lookup"><span data-stu-id="49d63-132">System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7</span></span>](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a><span data-ttu-id="49d63-133">工作總覽</span><span class="sxs-lookup"><span data-stu-id="49d63-133">Task Overview</span></span>

<span data-ttu-id="49d63-134">若要完成本主題中的工作和逐步解說，您至少需要三部&#x2014;伺服器：一個 WFF 控制器、一個用於伺服器陣列的主要 web 伺服器，以及一個或多個伺服器陣列的次要 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-134">To complete the tasks and walkthroughs in this topic, you'll need at least three servers&#x2014;one WFF controller, one primary web server for the server farm, and one or more secondary web servers for the server farm.</span></span> <span data-ttu-id="49d63-135">您可以隨時在 WFF 伺服器陣列中新增更多次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-135">You can add more secondary servers to a WFF server farm at any time.</span></span> <span data-ttu-id="49d63-136">概括而言，若要為您的預備或生產環境建立和設定 WFF 伺服器陣列，您必須：</span><span class="sxs-lookup"><span data-stu-id="49d63-136">At a high level, to create and configure a WFF server farm for your staging or production environment you'll need to:</span></span>

- <span data-ttu-id="49d63-137">藉由安裝 Internet Information Services （IIS）7.5 和 WFF 2.0 來建立控制器伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-137">Create a controller server by installing Internet Information Services (IIS) 7.5 and WFF 2.0.</span></span>
- <span data-ttu-id="49d63-138">藉由建立一般的系統管理員帳戶並設定防火牆例外狀況，來準備主要和次要伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-138">Prepare primary and secondary servers by creating a common administrator account and configuring firewall exceptions.</span></span>
- <span data-ttu-id="49d63-139">使用控制器伺服器上的 IIS 管理員來設定伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-139">Configure the server farm by using IIS Manager on the controller server.</span></span>
- <span data-ttu-id="49d63-140">使用 IIS 應用程式要求路由（ARR）或替代的負載平衡技術來設定負載平衡。</span><span class="sxs-lookup"><span data-stu-id="49d63-140">Configure load balancing using IIS Application Request Routing (ARR) or an alternative load-balancing technology.</span></span>

<span data-ttu-id="49d63-141">本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="49d63-141">The tasks and walkthroughs in this topic assume that you're starting with clean server builds running Windows Server 2008 R2.</span></span> <span data-ttu-id="49d63-142">開始之前，針對每部伺服器，請確定：</span><span class="sxs-lookup"><span data-stu-id="49d63-142">Before you begin, for each server, ensure that:</span></span>

- <span data-ttu-id="49d63-143">Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。</span><span class="sxs-lookup"><span data-stu-id="49d63-143">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="49d63-144">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="49d63-144">The server is domain-joined.</span></span>
- <span data-ttu-id="49d63-145">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="49d63-145">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="49d63-146">如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="49d63-146">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="49d63-147">如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="49d63-147">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="create-the-wff-controller-server"></a><span data-ttu-id="49d63-148">建立 WFF 控制器伺服器</span><span class="sxs-lookup"><span data-stu-id="49d63-148">Create the WFF Controller Server</span></span>

<span data-ttu-id="49d63-149">若要建立 WFF 控制器伺服器，您必須同時安裝 IIS 7 或更新版本，以及 WFF 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="49d63-149">To create a WFF controller server, you'll need to install both IIS 7 or later and WFF 2.0 or later.</span></span> <span data-ttu-id="49d63-150">實際上，WFF 會使用 IIS Web Deployment Tool （Web Deploy）2.x 來同步處理您伺服器陣列中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-150">Under the covers, WFF uses the IIS Web Deployment Tool (Web Deploy) 2.x to synchronize the servers in your farm.</span></span> <span data-ttu-id="49d63-151">如果您使用 Web Platform Installer 安裝 WFF，安裝程式會自動為您下載並安裝 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="49d63-151">If you use the Web Platform Installer to install WFF, the installer will automatically download and install Web Deploy for you.</span></span>

<span data-ttu-id="49d63-152">**建立 WFF 控制器伺服器**</span><span class="sxs-lookup"><span data-stu-id="49d63-152">**To create the WFF controller server**</span></span>

1. <span data-ttu-id="49d63-153">下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9739157)。</span><span class="sxs-lookup"><span data-stu-id="49d63-153">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9739157).</span></span>
2. <span data-ttu-id="49d63-154">在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-154">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="49d63-155">在視窗左側的流覽窗格中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-155">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="49d63-156">在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-156">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
5. <span data-ttu-id="49d63-157">在<strong>Web Farm Framework 2 中。</strong><em>x</em>列，按一下 [<strong>新增</strong>]。</span><span class="sxs-lookup"><span data-stu-id="49d63-157">In the <strong>Web Farm Framework 2.</strong><em>x</em> row, click <strong>Add</strong>.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. <span data-ttu-id="49d63-158">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="49d63-158">Click **Install**.</span></span> <span data-ttu-id="49d63-159">請注意，Web Platform Installer 已在安裝清單中新增 Web 部署工具以及其他各種相依性。</span><span class="sxs-lookup"><span data-stu-id="49d63-159">Notice that the Web Platform Installer has added the Web Deployment Tool, along with various other dependencies, to the installation list.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. <span data-ttu-id="49d63-160">請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-160">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
8. <span data-ttu-id="49d63-161">當安裝完成時，按一下 **[完成]** ，然後關閉 [ **Web Platform Installer 3.0** ] 視窗。</span><span class="sxs-lookup"><span data-stu-id="49d63-161">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

## <a name="configure-the-primary-and-secondary-servers"></a><span data-ttu-id="49d63-162">設定主要和次要伺服器</span><span class="sxs-lookup"><span data-stu-id="49d63-162">Configure the Primary and Secondary Servers</span></span>

<span data-ttu-id="49d63-163">建立 WFF 伺服器陣列之前，您應該先在將組成伺服器陣列的 web 伺服器上完成一些準備工作：</span><span class="sxs-lookup"><span data-stu-id="49d63-163">Before you create a WFF server farm, you should complete some preparation tasks on the web servers that will make up the farm:</span></span>

- <span data-ttu-id="49d63-164">新增防火牆例外，以允許**核心網路**功能、**遠端系統管理**以及檔案**和印表機共用**功能與 WFF 控制器伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="49d63-164">Add firewall exceptions to allow the **Core Networking**, **Remote Administration**, and **File and Printer Sharing** features to communicate with the WFF controller server.</span></span>
- <span data-ttu-id="49d63-165">在 Active Directory 中建立網域帳戶（例如， **FABRIKAM\stagingfarm**），並將它新增至每部伺服器上的本機系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="49d63-165">Create a domain account (for example, **FABRIKAM\stagingfarm**) in Active Directory and add it to the local administrators group on each server.</span></span> <span data-ttu-id="49d63-166">當您建立伺服器陣列時，會使用此帳戶做為伺服器陣列系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="49d63-166">You'll use this account as the server farm administrator account when you create the server farm.</span></span>

<span data-ttu-id="49d63-167">如需有關如何在 Windows 防火牆中設定這些防火牆例外的詳細資訊，請參閱[IIS 7 的 Web 伺服陣列架構2.0 的系統和平臺需求](https://go.microsoft.com/?linkid=9805128)。</span><span class="sxs-lookup"><span data-stu-id="49d63-167">For more information on how to configure these firewall exceptions in Windows Firewall, see [System and Platform Requirements for the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805128).</span></span> <span data-ttu-id="49d63-168">如需其他防火牆系統，請參閱您的產品檔。</span><span class="sxs-lookup"><span data-stu-id="49d63-168">For other firewall systems, consult your product documentation.</span></span>

<span data-ttu-id="49d63-169">您可以使用下一個程式，將網域帳戶新增至 Windows Server 2008 R2 中的本機 administrators 群組。</span><span class="sxs-lookup"><span data-stu-id="49d63-169">You can use the next procedure to add a domain account to the local administrators group in Windows Server 2008 R2.</span></span> <span data-ttu-id="49d63-170">您應該在每個想要新增至伺服器&#x2014;陣列的伺服器上執行此程式，換句話說，請將相同的網域帳戶新增至主伺服器和每部次要伺服器上的本機系統管理員群組。</span><span class="sxs-lookup"><span data-stu-id="49d63-170">You should perform this procedure on every server that you want to add to the server farm&#x2014;in other words, add the same domain account to the local administrators group on the primary server and on each secondary server.</span></span>

<span data-ttu-id="49d63-171">**將網域帳戶新增至本機系統管理員群組**</span><span class="sxs-lookup"><span data-stu-id="49d63-171">**To add a domain account to the local administrators group**</span></span>

1. <span data-ttu-id="49d63-172">在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [**伺服器管理員**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-172">On the **Start** menu, point to **Administrative Tools**, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="49d63-173">在 [**伺服器管理員**] 視窗的 [樹狀檢視] 窗格中，依序展開 [設定]、[**本機使用者和群組** **]，然後**按一下 [**群組**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-173">In the **Server Manager** window, in the tree view pane, expand **Configuration**, expand **Local Users and Groups**, and then click **Groups**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. <span data-ttu-id="49d63-174">在 [**群組**] 窗格中，按兩下 [系統**管理員**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-174">In the **Groups** pane, double-click **Administrators**.</span></span>
4. <span data-ttu-id="49d63-175">在 [系統**管理員屬性**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-175">In the **Administrators Properties** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="49d63-176">在 [**選取使用者、電腦、服務帳戶或群組**] 對話方塊中，輸入（或流覽）您的網域帳戶（例如， **FABRIKAM\stagingfarm**），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="49d63-176">In the **Select Users, Computers, Service Accounts, or Groups** dialog box, type (or browse) to your domain account (for example, **FABRIKAM\stagingfarm**), and then click **OK**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. <span data-ttu-id="49d63-177">在 [系統**管理員屬性**] 對話方塊中，按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="49d63-177">In the **Administrators Properties** dialog box, click **OK**.</span></span>

<span data-ttu-id="49d63-178">您的伺服器現在可以加入至伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-178">Your servers are now ready to be added to a server farm.</span></span> <span data-ttu-id="49d63-179">在主伺服器的情況下，您可以在這兩種情況下，在建立伺服器&#x2014;陣列之前或之後設定伺服器以符合您的應用程式需求，WFF 將會藉由將相同的產品、元件或設定部署到次要伺服器來同步處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-179">In the case of the primary server, you can configure the server to meet your application requirements before or after you create the server farm&#x2014;in both cases, the WFF will synchronize the servers by deploying the same products, components, or configuration to your secondary servers.</span></span> <span data-ttu-id="49d63-180">為了簡單起見，本教學課程假設您將在完成建立伺服器陣列時設定主伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-180">For the sake of simplicity, this tutorial assumes that you'll configure the primary server when you've finished creating the server farm.</span></span>

## <a name="create-the-wff-server-farm"></a><span data-ttu-id="49d63-181">建立 WFF 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="49d63-181">Create the WFF Server Farm</span></span>

<span data-ttu-id="49d63-182">此時，您的所有伺服器都已準備好新增至 WFF 伺服器陣列：</span><span class="sxs-lookup"><span data-stu-id="49d63-182">At this point, all your servers are ready to be added to a WFF server farm:</span></span>

- <span data-ttu-id="49d63-183">您已在控制器伺服器上安裝 WFF。</span><span class="sxs-lookup"><span data-stu-id="49d63-183">You've installed WFF on the controller server.</span></span>
- <span data-ttu-id="49d63-184">您已在主要和次要 web 伺服器上設定防火牆例外。</span><span class="sxs-lookup"><span data-stu-id="49d63-184">You've configured firewall exceptions on your primary and secondary web servers.</span></span>
- <span data-ttu-id="49d63-185">您已將網域帳戶新增至主要和次要 web 伺服器上的本機 [系統管理員] 群組。</span><span class="sxs-lookup"><span data-stu-id="49d63-185">You've added a domain account to the local administrators group on your primary and secondary web servers.</span></span>

<span data-ttu-id="49d63-186">下一步是在 WFF 中建立伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-186">The next step is to create the server farm in WFF.</span></span> <span data-ttu-id="49d63-187">您可以從 WFF 控制器伺服器上的 IIS 管理員執行此動作。</span><span class="sxs-lookup"><span data-stu-id="49d63-187">You can do this from IIS Manager on the WFF controller server.</span></span>

<span data-ttu-id="49d63-188">**建立 WFF 伺服器陣列**</span><span class="sxs-lookup"><span data-stu-id="49d63-188">**To create a WFF server farm**</span></span>

1. <span data-ttu-id="49d63-189">在 WFF 控制器伺服器的 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-189">On the WFF controller server, on the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="49d63-190">在 [**連接**] 窗格中，展開本機伺服器節點，以滑鼠右鍵按一下 [**伺服器**陣列]，然後按一下 [**建立伺服器**陣列]。</span><span class="sxs-lookup"><span data-stu-id="49d63-190">In the **Connections** pane, expand the local server node, right-click **Server Farms**, and then click **Create Server Farm**.</span></span>
3. <span data-ttu-id="49d63-191">在 [**建立伺服器**陣列] 對話方塊中，為伺服器陣列輸入有意義的名稱（例如，[**臨時**伺服器陣列]），然後選取 [**提供伺服器**陣列]。</span><span class="sxs-lookup"><span data-stu-id="49d63-191">In the **Create Server Farm** dialog box, type a meaningful name for the server farm (for example, **Staging Farm**), and then select **Provision server farm**.</span></span>
4. <span data-ttu-id="49d63-192">輸入您在每部伺服器上新增至本機 administrators 群組的網域帳戶之使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="49d63-192">Type the user name and password of the domain account that you added to the local administrators group on each server.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. <span data-ttu-id="49d63-193">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="49d63-193">Click **Next**.</span></span>
6. <span data-ttu-id="49d63-194">在 [**新增伺服器**] 頁面上，輸入主伺服器的完整功能變數名稱（FQDN），選取 [**主伺服器**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-194">On the **Add Servers** page, type the fully qualified domain name (FQDN) of the primary server, select **Primary Server**, and then click **Add**.</span></span>
7. <span data-ttu-id="49d63-195">此時，WFF 會嘗試使用您所提供的認證來聯繫主伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-195">At this point, WFF will attempt to contact the primary server using the credentials you provided.</span></span> <span data-ttu-id="49d63-196">如果連線成功，主伺服器將會新增至 [**新增伺服器**] 頁面上的資料表。</span><span class="sxs-lookup"><span data-stu-id="49d63-196">If the connection succeeds, the primary server will be added to the table on the **Add Servers** page.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="49d63-197">您可能已經注意到，預設已選取 [**伺服器已可供負載平衡**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-197">You might have noticed that **Server is available for Load Balancing** is selected by default.</span></span> <span data-ttu-id="49d63-198">WFF 會使用 IIS ARR 模組來執行負載平衡，並藉此將要求分散到伺服器陣列中的 web 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="49d63-198">WFF uses the IIS ARR module to implement load balancing and thereby distribute requests across the web servers in your server farm.</span></span> <span data-ttu-id="49d63-199">在大部分的情況下，如果您想要改用協力廠商負載平衡解決方案，您只會清除 [**伺服器適用于負載平衡**] 選項。</span><span class="sxs-lookup"><span data-stu-id="49d63-199">In most scenarios, you'd only clear the **Server is available for Load Balancing** option if you wanted to use a third-party load balancing solution instead.</span></span>
8. <span data-ttu-id="49d63-200">在 [**新增伺服器**] 頁面上，輸入第一部次要伺服器的 FQDN，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-200">On the **Add Servers** page, type the FQDN of your first secondary server, and then click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. <span data-ttu-id="49d63-201">針對伺服器陣列中的任何其他次要伺服器重複步驟7，然後按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="49d63-201">Repeat step 7 for any additional secondary servers in your farm, and then click **Finish**.</span></span>

<span data-ttu-id="49d63-202">您的 WFF 伺服器陣列現在已啟動且正在執行。</span><span class="sxs-lookup"><span data-stu-id="49d63-202">Your WFF server farm is now up and running.</span></span> <span data-ttu-id="49d63-203">任何您安裝在主伺服器上的 web 平台產品或元件，以及您部署到主伺服器的任何 web 應用程式或內容，都會自動布建到所有次要伺服器上。</span><span class="sxs-lookup"><span data-stu-id="49d63-203">Any web platform products or components that you install on the primary server, and any web applications or content that you deploy to the primary server, will be automatically provisioned on all your secondary servers.</span></span>

<span data-ttu-id="49d63-204">WFF 是廣泛且複雜的主題，您可以在[Microsoft Web Farm Framework 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129)網站深入瞭解。</span><span class="sxs-lookup"><span data-stu-id="49d63-204">WFF is a broad and complex topic, and you can learn more about it on the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span> <span data-ttu-id="49d63-205">不過，在這段時間內，您必須注意兩個功能區：</span><span class="sxs-lookup"><span data-stu-id="49d63-205">For the time being, however, there are two features areas that you need to be aware of:</span></span>

- <span data-ttu-id="49d63-206">*應用程式*布建是在伺服器陣列中的所有次要伺服器上複寫主伺服器內容（例如 web 應用程式和設定）的過程。</span><span class="sxs-lookup"><span data-stu-id="49d63-206">*Application provisioning* is the process that replicates content from the primary server, like web applications and configuration settings, across all the secondary servers in the server farm.</span></span> <span data-ttu-id="49d63-207">例如，如果您將 Contact Manager 範例解決方案部署到主要的預備伺服器，WFF 應用程式布建程式會將此解決方案部署到您所有的次要預備伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-207">For example, if you deploy the Contact Manager sample solution to your primary staging server, the WFF application provisioning process will deploy this solution to all your secondary staging servers.</span></span> <span data-ttu-id="49d63-208">根據預設，每隔30秒會執行一次應用程式布建進程。</span><span class="sxs-lookup"><span data-stu-id="49d63-208">By default, the application provisioning process runs every 30 seconds.</span></span>
- <span data-ttu-id="49d63-209">*平臺*布建是將 web 平台產品和元件從主伺服器同步處理到伺服器陣列中所有次要伺服器的程式。</span><span class="sxs-lookup"><span data-stu-id="49d63-209">*Platform provisioning* is the process that synchronizes web platform products and components from the primary server to all the secondary servers in the server farm.</span></span> <span data-ttu-id="49d63-210">例如，如果您在主要暫存伺服器上安裝 ASP.NET MVC 3，平臺布建程式將會使用 Web Platform Installer 在所有次要暫存伺服器上安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="49d63-210">For example, if you install ASP.NET MVC 3 on your primary staging server, the platform provisioning process will use the Web Platform Installer to install ASP.NET MVC 3 on all your secondary staging servers.</span></span> <span data-ttu-id="49d63-211">根據預設，平臺布建程式會每隔五分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="49d63-211">By default, the platform provisioning process runs every five minutes.</span></span>

<span data-ttu-id="49d63-212">您可以從 WFF 控制器伺服器上的 IIS 管理員管理基本應用程式和平臺布建設定。</span><span class="sxs-lookup"><span data-stu-id="49d63-212">You can manage basic application and platform provisioning settings from IIS Manager on your WFF controller server.</span></span>

<span data-ttu-id="49d63-213">**探索應用程式和平臺布建設定**</span><span class="sxs-lookup"><span data-stu-id="49d63-213">**Explore application and platform provisioning settings**</span></span>

1. <span data-ttu-id="49d63-214">在 **[IIS**管理員] 的 [連線] 窗格中，選取您的伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="49d63-214">In IIS Manager, in the **Connections** pane, select your server farm.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. <span data-ttu-id="49d63-215">在 [**伺服器**陣列] 窗格中，按兩下 [**應用程式**布建]。</span><span class="sxs-lookup"><span data-stu-id="49d63-215">In the **Server Farm** pane, double-click **Application Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. <span data-ttu-id="49d63-216">如您所見，伺服器陣列目前設定為每隔30秒同步處理主伺服器和次要伺服器之間的 web 內容和設定。</span><span class="sxs-lookup"><span data-stu-id="49d63-216">As you can see, the server farm is currently configured to synchronize web content and configuration settings between the primary server and the secondary servers every 30 seconds.</span></span>
4. <span data-ttu-id="49d63-217">按一下 [**上一步**]，然後按兩下 [**平臺**布建]。</span><span class="sxs-lookup"><span data-stu-id="49d63-217">Click **Back**, and then double-click **Platform Provisioning**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. <span data-ttu-id="49d63-218">如您所見，伺服器陣列目前設定為每隔五分鐘同步處理主伺服器和次要伺服器之間的 web 平台產品和元件。</span><span class="sxs-lookup"><span data-stu-id="49d63-218">As you can see, the server farm is currently configured to synchronize web platform products and components between the primary server and the secondary servers every five minutes.</span></span>
6. <span data-ttu-id="49d63-219">按一下 [上一步]。</span><span class="sxs-lookup"><span data-stu-id="49d63-219">Click **Back**.</span></span>
7. <span data-ttu-id="49d63-220">若要強制服務器陣列立即同步處理 web 平台產品，請在 [**動作**] 窗格中，按一下 [布建**平臺**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-220">To force the server farm to synchronize web platform products immediately, in the **Actions** pane, click **Provision Platform**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > <span data-ttu-id="49d63-221">平臺布建可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="49d63-221">Platform provisioning may take some time.</span></span> <span data-ttu-id="49d63-222">安裝程式進程會在伺服器陣列中的次要伺服器上以背景執行。</span><span class="sxs-lookup"><span data-stu-id="49d63-222">The installer process runs in the background on the secondary servers in your server farm.</span></span>
8. <span data-ttu-id="49d63-223">當您有足夠的時間讓布建程式完成時，您可以確認您新增到主伺服器的產品和元件現在已複寫到次要伺服器上。</span><span class="sxs-lookup"><span data-stu-id="49d63-223">Once you've allowed sufficient time for the provisioning process to complete, you can verify that the products and components that you added to the primary server have now been replicated on the secondary servers.</span></span> <span data-ttu-id="49d63-224">例如，您可以登入次要伺服器，並使用 [**伺服器管理員**] 視窗，確認已安裝 web 伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="49d63-224">For example, you can log on to a secondary server and use the **Server Manager** window to verify that the web server role has been installed.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. <span data-ttu-id="49d63-225">您也可以檢查 [已安裝的程式] 清單，以確認已新增各種 web 平臺元件。</span><span class="sxs-lookup"><span data-stu-id="49d63-225">You can also check the installed programs list to verify that various web platform components have been added.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a><span data-ttu-id="49d63-226">設定負載平衡</span><span class="sxs-lookup"><span data-stu-id="49d63-226">Configure Load Balancing</span></span>

<span data-ttu-id="49d63-227">當您建立 web 伺服陣列時，您必須設定某種形式的負載平衡，以便在您的 web 伺服器之間散發 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="49d63-227">When you create a web farm, you need to set up some form of load balancing to distribute HTTP requests between your web servers.</span></span> <span data-ttu-id="49d63-228">這可能是 Windows Server 2008 網路負載平衡、IIS ARR，或協力廠商軟體型或硬體型負載平衡解決方案。</span><span class="sxs-lookup"><span data-stu-id="49d63-228">This could be Windows Server 2008 network load balancing, IIS ARR, or a third-party software-based or hardware-based load balancing solution.</span></span>

<span data-ttu-id="49d63-229">WFF 的設計目的是要與 IIS ARR 緊密整合。</span><span class="sxs-lookup"><span data-stu-id="49d63-229">WFF is designed to integrate closely with IIS ARR.</span></span> <span data-ttu-id="49d63-230">若要利用這項整合，您必須在 WFF 控制器伺服器上安裝 ARR 模組。</span><span class="sxs-lookup"><span data-stu-id="49d63-230">To take advantage of this integration, you need to install the ARR module on the WFF controller server.</span></span> <span data-ttu-id="49d63-231">接著，您可以將所有網路流量導向控制器伺服器，通常是藉由設定網域名稱系統（DNS）記錄。</span><span class="sxs-lookup"><span data-stu-id="49d63-231">You then direct all your web traffic to the controller server, typically by configuring Domain Name System (DNS) records.</span></span> <span data-ttu-id="49d63-232">然後，控制器伺服器會根據伺服器可用性和其他各種準則，將傳入要求分散到您伺服器陣列中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-232">The controller server will then distribute incoming requests among the servers in your farm, based on server availability and various other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="49d63-233">您不需要使用 ARR 搭配 WFF;您可以將 WFF 設定為與協力廠商負載平衡解決方案搭配使用。</span><span class="sxs-lookup"><span data-stu-id="49d63-233">You don't have to use ARR with WFF; you can configure WFF to work with third-party load balancing solutions.</span></span> <span data-ttu-id="49d63-234">如需詳細資訊，請參閱[IIS 7 的 Web Farm Framework 2.0 總覽](https://go.microsoft.com/?linkid=9805126)。</span><span class="sxs-lookup"><span data-stu-id="49d63-234">For more information, see [Overview of the Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805126).</span></span>

<span data-ttu-id="49d63-235">使用 ARR 進行負載平衡是一個複雜的主題，其中大部分都超出本教學課程的範圍。</span><span class="sxs-lookup"><span data-stu-id="49d63-235">Load balancing using ARR is a complex topic, most of which is beyond the scope of this tutorial.</span></span> <span data-ttu-id="49d63-236">不過，您可以使用下一個程式來安裝 ARR 模組，並開始使用負載平衡。</span><span class="sxs-lookup"><span data-stu-id="49d63-236">However, you can use the next procedure to install the ARR module and get started with load balancing.</span></span>

<span data-ttu-id="49d63-237">**在 WFF 控制器伺服器上設定負載平衡**</span><span class="sxs-lookup"><span data-stu-id="49d63-237">**To set up load balancing on the WFF controller server**</span></span>

1. <span data-ttu-id="49d63-238">在 WFF 控制器伺服器上，啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="49d63-238">On the WFF controller server, launch the Web Platform Installer.</span></span>
2. <span data-ttu-id="49d63-239">在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-239">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
3. <span data-ttu-id="49d63-240">在視窗左側的流覽窗格中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-240">On the left side of the window, in the navigation pane, click **Server**.</span></span>
4. <span data-ttu-id="49d63-241">在 [**應用程式要求路由 2.5** ] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-241">In the **Application Request Routing 2.5** row, click **Add**.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. <span data-ttu-id="49d63-242">按一下 [**安裝**]，然後依照 [ **Web Platform 安裝**] 視窗中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="49d63-242">Click **Install**, and then follow the instructions in the **Web Platform Installation** window.</span></span>
6. <span data-ttu-id="49d63-243">當安裝完成時，啟動 [IIS 管理員]，**然後在 [連線] 窗格**中，按一下您的伺服器陣列節點。</span><span class="sxs-lookup"><span data-stu-id="49d63-243">When the installation is complete, launch IIS Manager, and in the **Connections** pane, click your server farm node.</span></span> <span data-ttu-id="49d63-244">請注意，[**伺服器**陣列] 窗格中已加入數個新的圖示。</span><span class="sxs-lookup"><span data-stu-id="49d63-244">Notice that several new icons have been added to the **Server Farm** pane.</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. <span data-ttu-id="49d63-245">在 [伺服器陣列] 窗格中，按兩下 [負載平衡]。</span><span class="sxs-lookup"><span data-stu-id="49d63-245">In the **Server Farm** pane, double-click **Load Balance**.</span></span>
8. <span data-ttu-id="49d63-246">在 [**負載平衡**] 窗格中，選取負載平衡演算法（例如，**最少目前的要求**）。</span><span class="sxs-lookup"><span data-stu-id="49d63-246">In the **Load Balance** pane, select a load balance algorithm (for example, **Least current request**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="49d63-247">如需負載平衡演算法和其他設定的詳細資訊，請參閱[應用程式要求路由模組](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="49d63-247">For more information on load balancing algorithms and other configuration settings, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. <span data-ttu-id="49d63-248">在 [**動作**] 窗格中 **，按一下 [** 套用]。</span><span class="sxs-lookup"><span data-stu-id="49d63-248">In the **Actions** pane, click **Apply**.</span></span>

<span data-ttu-id="49d63-249">您現在已為伺服器陣列中的伺服器設定基本負載平衡。</span><span class="sxs-lookup"><span data-stu-id="49d63-249">You have now configured basic load balancing for the servers in your server farm.</span></span> <span data-ttu-id="49d63-250">如果您將所有的 web 伺服陣列流量導向至控制器伺服器，則會根據您選取的可用性和負載平衡演算法，將要求分散到您伺服器陣列中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="49d63-250">If you direct all your web farm traffic to the controller server, the requests will be distributed between the servers in your farm according to availability and the load balancing algorithm you selected.</span></span>

<span data-ttu-id="49d63-251">如需有關如何使用 ARR 來設定負載平衡的詳細資訊，請參閱[應用程式要求路由模組](https://go.microsoft.com/?linkid=9805130)。</span><span class="sxs-lookup"><span data-stu-id="49d63-251">For more information on how to configure load balancing with ARR, see [Application Request Routing Module](https://go.microsoft.com/?linkid=9805130).</span></span>

## <a name="monitor-the-server-farm"></a><span data-ttu-id="49d63-252">監視伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="49d63-252">Monitor the Server Farm</span></span>

<span data-ttu-id="49d63-253">您可以隨時透過控制器伺服器上的 IIS 管理員監視伺服器陣列的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="49d63-253">You can monitor the health of your server farm at any time through IIS Manager on the controller server.</span></span> <span data-ttu-id="49d63-254">在 [**連接**] 窗格中，展開您的伺服器陣列，然後按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="49d63-254">In the **Connections** pane, expand your server farm, and then click **Servers**.</span></span> <span data-ttu-id="49d63-255">中間窗格會顯示伺服器陣列中每一部伺服器的摘要，以及最近活動的追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="49d63-255">The center pane will show a summary of each server in the farm together with a trace log of recent activity.</span></span>

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a><span data-ttu-id="49d63-256">結論</span><span class="sxs-lookup"><span data-stu-id="49d63-256">Conclusion</span></span>

<span data-ttu-id="49d63-257">您的 WFF 伺服器陣列現在應該已啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="49d63-257">Your WFF server farm should now be up and running.</span></span> <span data-ttu-id="49d63-258">您可以設定主伺服器，以支援您偏好&#x2014;的任何部署方法，請參閱進一步閱讀章節&#x2014;以取得詳細資料，而且您的設定將會在伺服器陣列中的每部次要伺服器上複寫。</span><span class="sxs-lookup"><span data-stu-id="49d63-258">You can configure the primary server to support whichever deployment approach you prefer&#x2014;see the Further Reading section for details&#x2014;and your configuration will be replicated on each secondary server in the server farm.</span></span>

## <a name="further-reading"></a><span data-ttu-id="49d63-259">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="49d63-259">Further Reading</span></span>

<span data-ttu-id="49d63-260">如需有關設定和使用 WFF 的所有層面的詳細指引，請參閱[Microsoft Web Farm Framework 2.0 FOR IIS 7](https://go.microsoft.com/?linkid=9805129)網站。</span><span class="sxs-lookup"><span data-stu-id="49d63-260">For more guidance on all aspects of configuring and using the WFF, see the [Microsoft Web Farm Framework 2.0 for IIS 7](https://go.microsoft.com/?linkid=9805129) website.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="49d63-261">[上一頁](configuring-a-database-server-for-web-deploy-publishing.md)
> [下一頁](configuring-deployment-properties-for-a-target-environment.md)</span><span class="sxs-lookup"><span data-stu-id="49d63-261">[Previous](configuring-a-database-server-for-web-deploy-publishing.md)
[Next](configuring-deployment-properties-for-a-target-environment.md)</span></span>
