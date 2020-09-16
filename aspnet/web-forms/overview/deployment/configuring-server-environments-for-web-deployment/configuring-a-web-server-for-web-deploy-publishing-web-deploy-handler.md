---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)
author: jrjlee
description: 本主題說明如何設定 Internet Information Services (IIS) web 伺服器，以支援使用 IIS Web Deploy 漢字的 web 發佈和部署 .。。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: af46b5a74309fbae4b5db072363e71d965445f9a
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609688"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="a8417-103">設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)</span><span class="sxs-lookup"><span data-stu-id="a8417-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>

[<span data-ttu-id="a8417-104">PDF 下載</span><span class="sxs-lookup"><span data-stu-id="a8417-104">PDF Download</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a8417-105">本主題說明如何使用 IIS Web Deploy 處理常式，設定 Internet Information Services (IIS) web 伺服器來支援 web 發行和部署。</span><span class="sxs-lookup"><span data-stu-id="a8417-105">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="a8417-106">當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放到 Web 服務器上。</span><span class="sxs-lookup"><span data-stu-id="a8417-106">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="a8417-107">您可以：</span><span class="sxs-lookup"><span data-stu-id="a8417-107">You can:</span></span>
> 
> - <span data-ttu-id="a8417-108">使用 *Web Deploy 遠端代理程式服務*。</span><span class="sxs-lookup"><span data-stu-id="a8417-108">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="a8417-109">這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何程式部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="a8417-109">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="a8417-110">使用 *Web Deploy 處理常式*。</span><span class="sxs-lookup"><span data-stu-id="a8417-110">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="a8417-111">這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a8417-111">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="a8417-112">不過，當您使用此方法時，您可以設定 IIS 以允許非系統管理員的使用者執行部署。</span><span class="sxs-lookup"><span data-stu-id="a8417-112">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="a8417-113">Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a8417-113">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="a8417-114">使用 *離線部署*。</span><span class="sxs-lookup"><span data-stu-id="a8417-114">Use *offline deployment*.</span></span> <span data-ttu-id="a8417-115">這種方法需要最少的 web 伺服器設定，但是伺服器管理員必須手動將 web 套件複製到伺服器上，然後透過 IIS 管理員將它匯入。</span><span class="sxs-lookup"><span data-stu-id="a8417-115">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="a8417-116">如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱 [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="a8417-116">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="a8417-117">是，如果您想要允許非系統管理員的使用者將內容部署到特定的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="a8417-117">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="a8417-118">在這些類型的案例中，通常會需要這種方法：</span><span class="sxs-lookup"><span data-stu-id="a8417-118">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="a8417-119">暫存或生產環境，在此環境中，觸發遠端部署的人員或服務帳戶不太可能存取伺服器管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="a8417-119">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="a8417-120">裝載的環境，您想要讓遠端使用者能夠更新其網站，而不需讓他們完全掌控您的 web 伺服器 (或存取任何其他網站) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-120">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="a8417-121">在開發或測試案例中，或在小型組織中，使用伺服器管理員認證來部署內容通常較不之間爭論。</span><span class="sxs-lookup"><span data-stu-id="a8417-121">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="a8417-122">在這些情況下，將您的網頁伺服器設定為支援使用 [Web Deploy 遠端代理程式服務](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 進行部署，可提供更簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="a8417-122">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="a8417-123">工作總覽</span><span class="sxs-lookup"><span data-stu-id="a8417-123">Task Overview</span></span>

<span data-ttu-id="a8417-124">若要使用 Web Deploy 處理常式方法，將網頁伺服器設定為從遠端電腦接受及部署 web 封裝，您必須：</span><span class="sxs-lookup"><span data-stu-id="a8417-124">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="a8417-125">建立或選擇網域使用者帳戶 (「非系統管理員使用者」 ) 您將用來執行部署的認證。</span><span class="sxs-lookup"><span data-stu-id="a8417-125">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="a8417-126">安裝 IIS 7.5，包括 Web 管理服務和基本驗證模組。</span><span class="sxs-lookup"><span data-stu-id="a8417-126">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="a8417-127">安裝 Web Deploy 2.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a8417-127">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="a8417-128">將 Web 管理服務設定為允許遠端連線，並啟動服務。</span><span class="sxs-lookup"><span data-stu-id="a8417-128">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="a8417-129">建立 IIS 網站來裝載已部署的內容。</span><span class="sxs-lookup"><span data-stu-id="a8417-129">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="a8417-130">在 IIS 管理員中，為您的網站授與非系統管理員的使用者許可權。</span><span class="sxs-lookup"><span data-stu-id="a8417-130">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="a8417-131">確定 Web 管理服務委派規則允許服務使用您的非系統管理員使用者帳戶來新增和變更網站內容。</span><span class="sxs-lookup"><span data-stu-id="a8417-131">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="a8417-132">設定任何防火牆，以允許埠8172上的連入連線。</span><span class="sxs-lookup"><span data-stu-id="a8417-132">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="a8417-133">若要特別裝載 ContactManager 範例解決方案，您也需要：</span><span class="sxs-lookup"><span data-stu-id="a8417-133">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="a8417-134">安裝 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="a8417-134">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="a8417-135">安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="a8417-135">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="a8417-136">本主題將示範如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="a8417-136">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="a8417-137">本主題中的工作和逐步解說假設您是從執行 Windows Server 2016 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="a8417-137">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2016.</span></span> <span data-ttu-id="a8417-138">繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="a8417-138">Before you continue, ensure that:</span></span>

- <span data-ttu-id="a8417-139">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a8417-139">Windows Server 2016</span></span>
- <span data-ttu-id="a8417-140">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="a8417-140">The server is domain-joined.</span></span>
- <span data-ttu-id="a8417-141">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a8417-141">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="a8417-142">如需將電腦加入網域的詳細資訊，請參閱將 [電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="a8417-142">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="a8417-143">如需設定靜態 IP 位址的詳細資訊，請參閱 [設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a8417-143">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="a8417-144">安裝產品和元件</span><span class="sxs-lookup"><span data-stu-id="a8417-144">Install Products and Components</span></span>

<span data-ttu-id="a8417-145">本節將引導您在 web 伺服器上安裝必要的產品和元件。</span><span class="sxs-lookup"><span data-stu-id="a8417-145">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="a8417-146">開始之前，最好先執行 Windows Update，以確保您的伺服器完全處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="a8417-146">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="a8417-147">在此情況下，您必須安裝下列專案：</span><span class="sxs-lookup"><span data-stu-id="a8417-147">In this case, you need to install these things:</span></span>

- <span data-ttu-id="a8417-148">**IIS 7 建議**的設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-148">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="a8417-149">這可讓 web 伺服器 \*\* (iis) \*\* 角色在您的 web 伺服器上，並安裝您所需的一組 iis 模組和元件，以便裝載 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8417-149">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="a8417-150">**IIS：管理服務**。</span><span class="sxs-lookup"><span data-stu-id="a8417-150">**IIS: Management Service**.</span></span> <span data-ttu-id="a8417-151">這會在 IIS 中安裝 Web 管理服務 (WMSvc) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-151">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="a8417-152">這項服務可讓您從遠端系統管理 IIS 網站，並向用戶端公開 Web Deploy 處理常式端點。</span><span class="sxs-lookup"><span data-stu-id="a8417-152">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="a8417-153">**IIS：基本驗證**。</span><span class="sxs-lookup"><span data-stu-id="a8417-153">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="a8417-154">這會安裝 IIS 基本驗證模組。</span><span class="sxs-lookup"><span data-stu-id="a8417-154">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="a8417-155">這可讓 Web 管理服務 (WMSvc) 驗證您所提供的認證。</span><span class="sxs-lookup"><span data-stu-id="a8417-155">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="a8417-156">**Web 部署工具2.1 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="a8417-156">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="a8417-157">這會在您的伺服器上安裝 Web Deploy (及其基礎可執行檔 MSDeploy.exe) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-157">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="a8417-158">在這個程式中，它會安裝 Web Deploy 處理常式，並將它與 Web 管理服務整合。</span><span class="sxs-lookup"><span data-stu-id="a8417-158">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="a8417-159">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="a8417-159">**.NET Framework 4.0**.</span></span> <span data-ttu-id="a8417-160">若要執行以此版本的 .NET Framework 建立的應用程式，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="a8417-160">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="a8417-161">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="a8417-161">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="a8417-162">這會安裝執行 MVC 3 應用程式所需的元件。</span><span class="sxs-lookup"><span data-stu-id="a8417-162">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="a8417-163">本逐步解說將說明如何使用 Web Platform Installer 來安裝和設定各種元件。</span><span class="sxs-lookup"><span data-stu-id="a8417-163">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="a8417-164">雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a8417-164">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="a8417-165">如需詳細資訊，請參閱 [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="a8417-165">For more information, see [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="a8417-166">**若要安裝必要的產品和元件**</span><span class="sxs-lookup"><span data-stu-id="a8417-166">**To install the required products and components**</span></span>

1. <span data-ttu-id="a8417-167">下載並安裝 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="a8417-167">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="a8417-168">安裝完成時，Web Platform Installer 將會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="a8417-168">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8417-169">您現在可以從 [ **開始** ] 功能表啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="a8417-169">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="a8417-170">若要這樣做，請在 [ **開始** ] 功能表上，按一下 [ **所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-170">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="a8417-171">在 [Web Platform Installer]\*\*\*\* 視窗的頂端，按一下 [產品]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a8417-171">At the top of the **Web Platform Installer** window, click **Products**.</span></span>
4. <span data-ttu-id="a8417-172">在視窗的左側 **，按一下 [** 流覽] 窗格中的 [架構]。</span><span class="sxs-lookup"><span data-stu-id="a8417-172">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="a8417-173">在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-173">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8417-174">您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="a8417-174">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="a8417-175">如果已安裝產品或元件，Web Platform Installer 將會以**安裝**的文字取代 [**新增**] 按鈕來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="a8417-175">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="a8417-176">在 \*\*ASP.NET MVC 3 (Visual Studio 2010) \*\* 資料列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-176">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="a8417-177">在流覽窗格中，按一下 [ **伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-177">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="a8417-178">在 [ **IIS 7 建議** 的設定] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-178">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="a8417-179">在 [ **Web 部署工具 2.1** ] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-179">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="a8417-180">在 [ **IIS：基本驗證** ] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-180">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="a8417-181">在 [ **IIS：管理服務** ] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-181">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="a8417-182">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="a8417-182">Click **Install**.</span></span> <span data-ttu-id="a8417-183">Web Platform Installer 將會顯示一份產品清單，其中包含要安裝之任何相關聯的相依性&#x2014;&#x2014;，並會提示您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="a8417-183">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="a8417-184">請參閱授權條款，如果您同意條款，請按一下 [ **我接受**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-184">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="a8417-185">當安裝完成時，請按一下 **[完成**]，然後關閉 **Web Platform Installer** 視窗。</span><span class="sxs-lookup"><span data-stu-id="a8417-185">When the installation is complete, click **Finish**, and then close the **Web Platform Installer** window.</span></span>

<span data-ttu-id="a8417-186">如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，則必須執行 [ASP.NET Iis 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 註冊最新版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a8417-186">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="a8417-187">如果您沒有這麼做，您會發現 IIS 將提供靜態內容 (像是 HTML 檔案) 沒有任何問題，但它會傳回 **HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時，找不到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="a8417-187">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="a8417-188">您可以使用下一個程式來確定 ASP.NET 4.0 已註冊。</span><span class="sxs-lookup"><span data-stu-id="a8417-188">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="a8417-189">**若要向 IIS 註冊 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="a8417-189">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="a8417-190">按一下 [ **開始**]，然後輸入 **命令提示**字元。</span><span class="sxs-lookup"><span data-stu-id="a8417-190">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="a8417-191">在搜尋結果中，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-191">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="a8417-192">在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="a8417-192">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="a8417-193">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="a8417-193">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="a8417-194">如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="a8417-194">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="a8417-195">若要這樣做，請在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="a8417-195">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="a8417-196">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="a8417-196">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="a8417-197">好的做法是，此時再次使用 Windows Update，以下載並安裝您已安裝之新產品和元件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="a8417-197">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="a8417-198">設定 Web 管理服務</span><span class="sxs-lookup"><span data-stu-id="a8417-198">Configure the Web Management Service</span></span>

<span data-ttu-id="a8417-199">現在您已安裝所需的所有專案，下一步是在 IIS 中設定 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="a8417-199">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="a8417-200">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="a8417-200">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="a8417-201">在伺服器層級啟用基本驗證。</span><span class="sxs-lookup"><span data-stu-id="a8417-201">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="a8417-202">將 Web 管理服務設定為接受遠端連線。</span><span class="sxs-lookup"><span data-stu-id="a8417-202">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="a8417-203">啟動 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="a8417-203">Start the Web Management Service.</span></span>
- <span data-ttu-id="a8417-204">檢查必要的 Web 管理服務委派規則是否已就緒。</span><span class="sxs-lookup"><span data-stu-id="a8417-204">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="a8417-205">**設定 Web 管理服務**</span><span class="sxs-lookup"><span data-stu-id="a8417-205">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="a8417-206">在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。</span><span class="sxs-lookup"><span data-stu-id="a8417-206">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="a8417-207">在 [IIS 管理員] 的 [ **連接** ] 窗格中，按一下 [伺服器] 節點 (例如 **STAGEWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-207">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="a8417-208">在中央窗格的 [ **IIS**] 底下，按兩下 [ **驗證**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-208">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. <span data-ttu-id="a8417-209">以滑鼠右鍵按一下 [ **基本驗證**]，然後按一下 [ **啟用**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-209">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="a8417-210">**在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-210">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="a8417-211">在中央窗格的 [ **管理**] 下，按兩下 [ **管理服務**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-211">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="a8417-212">在中央窗格中，選取 [ **啟用遠端連線**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-212">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8417-213">如果 Web 管理服務已在執行，您必須先將它停止。</span><span class="sxs-lookup"><span data-stu-id="a8417-213">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="a8417-214">在 [ **動作** ] 窗格中，按一下 [ **啟動** ] 以啟動 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="a8417-214">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="a8417-215">如果系統提示您儲存設定，請按一下 **[是]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-215">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8417-216">您也可能想要將服務設定為自動啟動。</span><span class="sxs-lookup"><span data-stu-id="a8417-216">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="a8417-217">若要這樣做，請開啟 [服務] 主控台，在 [ **Web 管理服務**] 上 **按一下滑鼠**右鍵，然後按一下 [內容]。</span><span class="sxs-lookup"><span data-stu-id="a8417-217">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="a8417-218">在 [ **啟動類型** ] 下拉式清單中，選取 [ **自動**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-218">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="a8417-219">**在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-219">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="a8417-220">在中央窗格的 [ **管理**] 下，按兩下 [ **管理服務委派**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-220">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="a8417-221">確認中央窗格包含一組規則。</span><span class="sxs-lookup"><span data-stu-id="a8417-221">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="a8417-222">這些規則可讓已授權的 Web 管理服務使用者使用各種 Web Deploy 提供者。</span><span class="sxs-lookup"><span data-stu-id="a8417-222">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="a8417-223">例如，若要透過 Web Deploy 處理常式，將 web 應用程式和內容部署至 IIS，則必須有委派規則，讓所有已驗證的 Web 管理服務使用者使用 **contentPath** 和 **iisApp** 提供者， (您可以在螢幕擷取畫面) 中看到的最後一個規則。</span><span class="sxs-lookup"><span data-stu-id="a8417-223">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="a8417-224">如果您依照本主題所述的順序安裝產品和元件，最新版本的 Web Deploy 應該會自動將所有必要的委派規則新增至 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="a8417-224">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="a8417-225">如果 [管理服務委派] 頁面未顯示任何規則，您必須自行建立。</span><span class="sxs-lookup"><span data-stu-id="a8417-225">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="a8417-226">如需有關如何進行此動作的指示，請參閱 [設定 Web 部署處理常式](https://go.microsoft.com/?linkid=9805124)。</span><span class="sxs-lookup"><span data-stu-id="a8417-226">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="a8417-227">**在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-227">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="a8417-228">建立和設定 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="a8417-228">Create and Configure an IIS Website</span></span>

<span data-ttu-id="a8417-229">在您可以將 web 內容部署到伺服器之前，您必須先建立並設定 IIS 網站來裝載內容。</span><span class="sxs-lookup"><span data-stu-id="a8417-229">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="a8417-230">Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。</span><span class="sxs-lookup"><span data-stu-id="a8417-230">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="a8417-231">您也需要進行一些額外的設定，以允許您的非系統管理員帳戶從遠端部署內容。</span><span class="sxs-lookup"><span data-stu-id="a8417-231">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="a8417-232">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="a8417-232">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="a8417-233">在檔案系統上建立資料夾來裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="a8417-233">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="a8417-234">建立 IIS 網站以提供內容，並將它與本機資料夾產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a8417-234">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="a8417-235">將讀取權限授與本機資料夾上的應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="a8417-235">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="a8417-236">將部署 web 應用程式所需的 IIS 許可權授與網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="a8417-236">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="a8417-237">雖然不會阻止您將內容部署至 IIS 中的預設網站，但不建議針對測試或示範情節以外的任何專案使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="a8417-237">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="a8417-238">若要模擬生產環境，您應該建立新的 IIS 網站，其中包含您的應用程式需求特有的設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-238">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="a8417-239">**若要建立 IIS 網站**</span><span class="sxs-lookup"><span data-stu-id="a8417-239">**To create an IIS website**</span></span>

1. <span data-ttu-id="a8417-240">在本機檔案系統上建立資料夾，以儲存您的內容 (例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-240">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="a8417-241">在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。</span><span class="sxs-lookup"><span data-stu-id="a8417-241">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="a8417-242">在 [IIS 管理員] 的 [ **連接** ] 窗格中，展開伺服器節點 (例如 **STAGEWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-242">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="a8417-243">以滑鼠右鍵按一下 [ **網站** ] 節點，然後按一下 [ **新增網站**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-243">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="a8417-244">在 [ **網站名稱** ] 方塊中，輸入 IIS 網站的名稱 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-244">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="a8417-245">在 [ **實體路徑** ] 方塊中，輸入 (或流覽以) 本機資料夾的路徑 (例如， **C:\DemoSite**) ]。</span><span class="sxs-lookup"><span data-stu-id="a8417-245">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="a8417-246">在 [ **埠** ] 方塊中，輸入您要用來裝載網站 (的埠號碼，例如 **85**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-246">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8417-247">適用于 HTTP 的標準埠號碼是80，而 HTTPS 則是443。</span><span class="sxs-lookup"><span data-stu-id="a8417-247">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="a8417-248">但是，如果您在埠80上裝載此網站，您必須先停止預設網站，才能存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="a8417-248">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="a8417-249">將 [ **主機名稱** ] 方塊保留空白，除非您要為網站設定網域名稱系統 (DNS) 記錄，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-249">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="a8417-250">在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="a8417-250">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="a8417-251">如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱 [設定網站的主機標頭 (iis 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a8417-251">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="a8417-252">如需 Windows Server 中的 DNS 伺服器角色的詳細資訊，請參閱 [Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="a8417-252">For more information on the DNS Server role in Windows Server, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="a8417-253">在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-253">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="a8417-254">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [新增]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a8417-254">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="a8417-255">在 [ **新增網站** 系結] 對話方塊中，將 [ **IP 位址** ] 和 [ **埠** ] 設定為符合您現有的網站設定。</span><span class="sxs-lookup"><span data-stu-id="a8417-255">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="a8417-256">在 [ **主機名稱** ] 方塊中，輸入您的 web 伺服器名稱 (例如， **STAGEWEB1**) ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-256">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="a8417-257">第一個網站系結可讓您使用 IP 位址和埠或，在本機存取網站 `http://localhost:85` 。</span><span class="sxs-lookup"><span data-stu-id="a8417-257">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="a8417-258">第二個網站系結可讓您使用電腦名稱稱從網域上的其他電腦存取網站 (例如， http://stageweb1:85) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-258">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="a8417-259">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [關閉]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a8417-259">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="a8417-260">在 [連線]\*\*\*\* 窗格中，按一下 [應用程式集區]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a8417-260">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="a8417-261">在 [ **應用程式** 集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [ **基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-261">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="a8417-262">根據預設，您的應用程式集區名稱會與您的網站名稱相符 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-262">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="a8417-263">在 [ **.NET clr 版本** ] 清單中，選取 [ **.net Clr v 4.0.30319**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-263">In the **.NET CLR version** list, select **.NET CLR v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > <span data-ttu-id="a8417-264">範例解決方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="a8417-264">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="a8417-265">這不是一般 Web Deploy 的需求。</span><span class="sxs-lookup"><span data-stu-id="a8417-265">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="a8417-266">為了讓您的網站提供內容，應用程式集區身分識別必須具有儲存內容的本機資料夾的 [讀取] 許可權。</span><span class="sxs-lookup"><span data-stu-id="a8417-266">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="a8417-267">在 IIS 7.5 中，應用程式集區預設會使用唯一的應用程式集區身分識別來執行 (與舊版的 IIS 相反，因為應用程式集區通常會使用網路服務帳戶) 來執行。</span><span class="sxs-lookup"><span data-stu-id="a8417-267">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="a8417-268">應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組的清單上&#x2014;而是在應用程式集區啟動時動態建立。</span><span class="sxs-lookup"><span data-stu-id="a8417-268">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="a8417-269">每個應用程式集區身分識別都會新增至本機 **IIS \_ IUSRS** 安全性群組作為隱藏專案。</span><span class="sxs-lookup"><span data-stu-id="a8417-269">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="a8417-270">若要授與許可權給檔案或資料夾上的應用程式集區身分識別，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="a8417-270">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="a8417-271">直接將許可權指派給應用程式集區身分識別，使用 \*\*Iis AppPool \( 應用程式集區名稱 \*\* 的格式)  (例如 **iis AppPool\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="a8417-271">Assign permissions to the application pool identity directly, using the format **IIS AppPool\(application pool name)** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="a8417-272">將許可權指派給 **IIS \_ IUSRS** 群組。</span><span class="sxs-lookup"><span data-stu-id="a8417-272">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="a8417-273">最常見的方法是將許可權指派給本機 **IIS \_ IUSRS** 群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。</span><span class="sxs-lookup"><span data-stu-id="a8417-273">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="a8417-274">下一個程式會使用這個以群組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="a8417-274">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="a8417-275">如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱 [應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="a8417-275">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="a8417-276">**設定 IIS 網站的資料夾許可權**</span><span class="sxs-lookup"><span data-stu-id="a8417-276">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="a8417-277">在 Windows 檔案總管中，流覽至本機資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="a8417-277">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="a8417-278">在資料夾上按一下滑鼠右鍵，然後按一下 [內容]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="a8417-278">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="a8417-279">在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-279">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="a8417-280">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="a8417-280">Click **Locations**.</span></span> <span data-ttu-id="a8417-281">在 [ **位置** ] 對話方塊中，選取本機伺服器，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-281">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="a8417-282">在 [ **選取使用者或群組** ] 對話方塊中，輸入 **IIS \_ IUSRS**，按一下 [ **檢查名稱**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-282">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="a8417-283">在 [ \*\* (資料夾名稱的許可權) \*\* ] 對話方塊中，請注意，根據預設，已將 [ **讀取 &amp; 執行**]、[ **列出資料夾內容**] 和 [ **讀取** ] 許可權指派給新群組。</span><span class="sxs-lookup"><span data-stu-id="a8417-283">In the **Permissions for (folder name)** dialog box, notice that the new group has been assigned the **Read &amp; execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="a8417-284">保持不變，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-284">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="a8417-285">按一下 **[確定** ]，關閉 \*\* (資料夾名稱) \*\* 內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a8417-285">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

<span data-ttu-id="a8417-286">在最後一個工作中，您必須將適當的許可權授與您將用來部署內容的非系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="a8417-286">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="a8417-287">此使用者需要許可權，才能從遠端將內容部署至您的網站。</span><span class="sxs-lookup"><span data-stu-id="a8417-287">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="a8417-288">**設定非系統管理員網域使用者的 IIS 網站許可權**</span><span class="sxs-lookup"><span data-stu-id="a8417-288">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="a8417-289">在 [IIS 管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下 **您的網站** 節點 (例如， **DemoSite**) ，指向 [ **部署**]，然後按一下 [ **設定 Web Deploy 發佈**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-289">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="a8417-290">在 [ **設定 Web Deploy 發佈** ] 對話方塊中，于 [ **選取使用者以提供發佈許可權** ] 清單的右邊，按一下省略號按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8417-290">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="a8417-291">在 [ **允許使用者** ] 對話方塊中，輸入您要用來部署內容之帳戶的網域和使用者名稱，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="a8417-291">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="a8417-292">在 [ **設定 Web Deploy 發佈** ] 對話方塊中，按一下 [ **安裝**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-292">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="a8417-293">這項作業會在一個步驟中執行兩個主要功能。</span><span class="sxs-lookup"><span data-stu-id="a8417-293">This operation performs two key functions in one step.</span></span> <span data-ttu-id="a8417-294">首先，它會根據您在上一節中檢查的委派規則，授與使用者透過 Web 管理服務遠端修改網站的許可權。</span><span class="sxs-lookup"><span data-stu-id="a8417-294">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="a8417-295">其次，它會授與使用者對網站源資料夾的完全控制權，讓使用者能夠新增、修改及設定網站內容的許可權。</span><span class="sxs-lookup"><span data-stu-id="a8417-295">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="a8417-296">在 [ **設定 Web Deploy 發佈** ] 對話方塊中，按一下 [ **關閉**]。</span><span class="sxs-lookup"><span data-stu-id="a8417-296">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="a8417-297">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="a8417-297">Configure Firewall Exceptions</span></span>

<span data-ttu-id="a8417-298">根據預設，IIS Web 管理服務會接聽 TCP 通訊埠8172。</span><span class="sxs-lookup"><span data-stu-id="a8417-298">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="a8417-299">如果您的 web 伺服器啟用了 Windows 防火牆，您將需要建立新的輸入規則，以允許埠8172上的 TCP 流量 (Windows 防火牆) 預設允許所有輸出流量。</span><span class="sxs-lookup"><span data-stu-id="a8417-299">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="a8417-300">如果您使用協力廠商防火牆，您必須建立規則以允許流量。</span><span class="sxs-lookup"><span data-stu-id="a8417-300">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="a8417-301">方向</span><span class="sxs-lookup"><span data-stu-id="a8417-301">Direction</span></span> | <span data-ttu-id="a8417-302">從埠</span><span class="sxs-lookup"><span data-stu-id="a8417-302">From Port</span></span> | <span data-ttu-id="a8417-303">到埠</span><span class="sxs-lookup"><span data-stu-id="a8417-303">To Port</span></span> | <span data-ttu-id="a8417-304">連接埠類型</span><span class="sxs-lookup"><span data-stu-id="a8417-304">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a8417-305">輸入</span><span class="sxs-lookup"><span data-stu-id="a8417-305">Inbound</span></span> | <span data-ttu-id="a8417-306">任意</span><span class="sxs-lookup"><span data-stu-id="a8417-306">Any</span></span> | <span data-ttu-id="a8417-307">8172</span><span class="sxs-lookup"><span data-stu-id="a8417-307">8172</span></span> | <span data-ttu-id="a8417-308">TCP</span><span class="sxs-lookup"><span data-stu-id="a8417-308">TCP</span></span> |
| <span data-ttu-id="a8417-309">輸出</span><span class="sxs-lookup"><span data-stu-id="a8417-309">Outbound</span></span> | <span data-ttu-id="a8417-310">8172</span><span class="sxs-lookup"><span data-stu-id="a8417-310">8172</span></span> | <span data-ttu-id="a8417-311">任意</span><span class="sxs-lookup"><span data-stu-id="a8417-311">Any</span></span> | <span data-ttu-id="a8417-312">TCP</span><span class="sxs-lookup"><span data-stu-id="a8417-312">TCP</span></span> |

<span data-ttu-id="a8417-313">如需在 Windows 防火牆中設定規則的詳細資訊，請參閱設定 [防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="a8417-313">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="a8417-314">如需協力廠商防火牆，請參閱您的產品檔。</span><span class="sxs-lookup"><span data-stu-id="a8417-314">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a8417-315">結論</span><span class="sxs-lookup"><span data-stu-id="a8417-315">Conclusion</span></span>

<span data-ttu-id="a8417-316">您的網頁伺服器現在應該已經準備好接受透過 Web 管理服務對 Web Deploy 處理常式進行遠端部署。</span><span class="sxs-lookup"><span data-stu-id="a8417-316">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="a8417-317">在您嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查這些重點：</span><span class="sxs-lookup"><span data-stu-id="a8417-317">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="a8417-318">您是否已在 IIS 的伺服器層級上啟用基本驗證？</span><span class="sxs-lookup"><span data-stu-id="a8417-318">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="a8417-319">您是否已啟用 Web 管理服務的遠端連線？</span><span class="sxs-lookup"><span data-stu-id="a8417-319">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="a8417-320">您是否已啟動 Web 管理服務？</span><span class="sxs-lookup"><span data-stu-id="a8417-320">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="a8417-321">是否已有管理服務委派規則？</span><span class="sxs-lookup"><span data-stu-id="a8417-321">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="a8417-322">應用程式集區身分識別是否擁有您網站源資料夾的讀取存取權？</span><span class="sxs-lookup"><span data-stu-id="a8417-322">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="a8417-323">非系統管理員的使用者帳戶是否有 IIS 中的網站層級許可權？</span><span class="sxs-lookup"><span data-stu-id="a8417-323">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="a8417-324">您的防火牆是否允許 TCP 埠8172上的伺服器進行連入連線？</span><span class="sxs-lookup"><span data-stu-id="a8417-324">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="a8417-325">深入閱讀</span><span class="sxs-lookup"><span data-stu-id="a8417-325">Further Reading</span></span>

<span data-ttu-id="a8417-326">如需有關如何設定自訂 Microsoft Build Engine (MSBuild) 專案檔，以將 web 封裝部署至 Web Deploy 處理常式的指引，請參閱 [設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="a8417-326">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8417-327">[上一個](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 
> [下一步](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="a8417-327">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
