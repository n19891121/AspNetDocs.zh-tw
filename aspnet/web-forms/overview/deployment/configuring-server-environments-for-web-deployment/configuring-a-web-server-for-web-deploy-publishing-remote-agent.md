---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 設定 Web Deploy 發佈 (遠端代理程式) 的 Web 服務器 |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 Internet Information Services (IIS) web 伺服器，以支援使用 IIS Web 部署的 web 發行和部署 .。。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: 39064045bccfe01d00ded60df17f1e152e5c1190
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609678"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a><span data-ttu-id="6931c-103">設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)</span><span class="sxs-lookup"><span data-stu-id="6931c-103">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>

<span data-ttu-id="6931c-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="6931c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="6931c-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="6931c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="6931c-106">本主題說明如何使用 IIS Web 部署工具 (Web Deploy) 遠端代理程式服務，設定 Internet Information Services (IIS) web 伺服器來支援 web 發行和部署。</span><span class="sxs-lookup"><span data-stu-id="6931c-106">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deployment Tool (Web Deploy) Remote Agent Service.</span></span>
> 
> <span data-ttu-id="6931c-107">當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放到 Web 服務器上。</span><span class="sxs-lookup"><span data-stu-id="6931c-107">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="6931c-108">您可以：</span><span class="sxs-lookup"><span data-stu-id="6931c-108">You can:</span></span>
> 
> - <span data-ttu-id="6931c-109">使用 *Web Deploy 遠端代理程式服務*。</span><span class="sxs-lookup"><span data-stu-id="6931c-109">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="6931c-110">這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何程式部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="6931c-110">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="6931c-111">使用 *Web Deploy 處理常式*。</span><span class="sxs-lookup"><span data-stu-id="6931c-111">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="6931c-112">這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6931c-112">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="6931c-113">不過，當您使用此方法時，您可以設定 IIS 以允許非系統管理員的使用者執行部署。</span><span class="sxs-lookup"><span data-stu-id="6931c-113">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="6931c-114">Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6931c-114">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="6931c-115">使用 *離線部署*。</span><span class="sxs-lookup"><span data-stu-id="6931c-115">Use *offline deployment*.</span></span> <span data-ttu-id="6931c-116">這種方法需要最少的 web 伺服器設定，但是伺服器管理員必須手動將 web 套件複製到伺服器上，然後透過 IIS 管理員將它匯入。</span><span class="sxs-lookup"><span data-stu-id="6931c-116">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="6931c-117">如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱 [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="6931c-117">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a><span data-ttu-id="6931c-118">Web Deploy 遠端代理程式是正確的方法嗎？</span><span class="sxs-lookup"><span data-stu-id="6931c-118">Is the Web Deploy Remote Agent the Right Approach for You?</span></span>

<span data-ttu-id="6931c-119">是的，如果要部署內容的使用者可以提供目的地伺服器上的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6931c-119">Yes, if the user who will deploy the content can supply the credentials of an administrator on the destination server.</span></span> <span data-ttu-id="6931c-120">在這些類型的案例中，通常會需要這種方法：</span><span class="sxs-lookup"><span data-stu-id="6931c-120">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="6931c-121">開發或測試環境，讓開發人員可以完全掌控目的地網頁伺服器和資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="6931c-121">Development or test environments, where the developer has full control over the destination web server and database server.</span></span>
- <span data-ttu-id="6931c-122">小型組織，其中單一使用者或一群使用者可以控制整個應用程式生命週期。</span><span class="sxs-lookup"><span data-stu-id="6931c-122">Smaller organizations in which a single user or a small group of users has control over the entire application lifecycle.</span></span>

<span data-ttu-id="6931c-123">在許多較大型的組織中，特別是針對暫存或生產環境，在 web 伺服器上提供使用者系統管理員許可權通常並不切合實際。</span><span class="sxs-lookup"><span data-stu-id="6931c-123">In lots of larger organizations, and particularly for staging or production environments, it's often not realistic to give users administrator rights on web servers.</span></span> <span data-ttu-id="6931c-124">如果是裝載的 web 伺服器，這種情況特別不可能發生。</span><span class="sxs-lookup"><span data-stu-id="6931c-124">In the case of hosted web servers, this is especially unlikely to be the case.</span></span> <span data-ttu-id="6931c-125">此外，如果您打算從組建伺服器自動化部署，您可能不想要使用系統管理員認證進行部署程式。</span><span class="sxs-lookup"><span data-stu-id="6931c-125">In addition, if you're planning to automate deployment from a build server, you may not want to use administrator credentials for the deployment process.</span></span> <span data-ttu-id="6931c-126">在這些情況下，將您的 web 伺服器設定為支援使用 [Web Deploy 處理常式](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 進行部署，可能會提供更滿意的選擇。</span><span class="sxs-lookup"><span data-stu-id="6931c-126">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Handler](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) may provide a more satisfactory choice.</span></span>

## <a name="task-overview"></a><span data-ttu-id="6931c-127">工作總覽</span><span class="sxs-lookup"><span data-stu-id="6931c-127">Task Overview</span></span>

<span data-ttu-id="6931c-128">本主題說明如何設定 Internet Information Services (IIS) 7.5 web 伺服器，以使用 Web Deploy 遠端代理程式方法，從遠端電腦接受及部署 web 套件。</span><span class="sxs-lookup"><span data-stu-id="6931c-128">This topic describes how to configure an Internet Information Services (IIS) 7.5 web server to accept and deploy web packages from a remote computer using the Web Deploy Remote Agent approach.</span></span> <span data-ttu-id="6931c-129">您必須：</span><span class="sxs-lookup"><span data-stu-id="6931c-129">You'll need to:</span></span>

- <span data-ttu-id="6931c-130">安裝 IIS 7.5 和 IIS 7 建議的設定。</span><span class="sxs-lookup"><span data-stu-id="6931c-130">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="6931c-131">安裝 Web Deploy 2.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6931c-131">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="6931c-132">建立 IIS 網站來裝載已部署的內容。</span><span class="sxs-lookup"><span data-stu-id="6931c-132">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="6931c-133">確定 Web Deployment Agent 服務正在執行。</span><span class="sxs-lookup"><span data-stu-id="6931c-133">Ensure that the Web Deployment Agent Service is running.</span></span>

<span data-ttu-id="6931c-134">若要特別裝載範例解決方案，您也需要：</span><span class="sxs-lookup"><span data-stu-id="6931c-134">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="6931c-135">安裝 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="6931c-135">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="6931c-136">安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="6931c-136">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="6931c-137">本主題將示範如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="6931c-137">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="6931c-138">本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="6931c-138">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="6931c-139">繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="6931c-139">Before you continue, ensure that:</span></span>

- <span data-ttu-id="6931c-140">已安裝 Windows Server 2008 R2 Service Pack 1 及所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="6931c-140">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="6931c-141">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="6931c-141">The server is domain-joined.</span></span>
- <span data-ttu-id="6931c-142">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6931c-142">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="6931c-143">如需將電腦加入網域的詳細資訊，請參閱將 [電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="6931c-143">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="6931c-144">如需設定靜態 IP 位址的詳細資訊，請參閱 [設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6931c-144">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="6931c-145">IIS 6 還支援遠端代理程式服務，而且您不需要加入網域。</span><span class="sxs-lookup"><span data-stu-id="6931c-145">The Remote Agent service is supported by IIS 6 onwards and does not require you to be joined to a domain.</span></span> <span data-ttu-id="6931c-146">不過，本教學課程中的步驟是在 IIS 7.5 上開發和測試，而其他版本的程式可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="6931c-146">However, the steps in this tutorial were developed and tested on IIS 7.5 and procedures for other versions may vary.</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="6931c-147">安裝產品和元件</span><span class="sxs-lookup"><span data-stu-id="6931c-147">Install Products and Components</span></span>

<span data-ttu-id="6931c-148">本節將引導您在 web 伺服器上安裝必要的產品和元件。</span><span class="sxs-lookup"><span data-stu-id="6931c-148">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="6931c-149">開始之前，最好先執行 Windows Update，以確保您的伺服器完全處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="6931c-149">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="6931c-150">在此情況下，您必須安裝下列專案：</span><span class="sxs-lookup"><span data-stu-id="6931c-150">In this case, you need to install these things:</span></span>

- <span data-ttu-id="6931c-151">**IIS 7 建議**的設定。</span><span class="sxs-lookup"><span data-stu-id="6931c-151">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="6931c-152">這可讓 web 伺服器 \*\* (iis) \*\* 角色在您的 web 伺服器上，並安裝您所需的一組 iis 模組和元件，以便裝載 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6931c-152">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="6931c-153">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="6931c-153">**.NET Framework 4.0**.</span></span> <span data-ttu-id="6931c-154">若要執行以此版本的 .NET Framework 建立的應用程式，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="6931c-154">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="6931c-155">**Web 部署工具2.1 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="6931c-155">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="6931c-156">這會在您的伺服器上安裝 Web Deploy (及其基礎可執行檔 MSDeploy.exe) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-156">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="6931c-157">在這個過程中，它會安裝並啟動 Web Deployment Agent 服務。</span><span class="sxs-lookup"><span data-stu-id="6931c-157">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="6931c-158">這種服務可讓您從遠端電腦部署 web 套件。</span><span class="sxs-lookup"><span data-stu-id="6931c-158">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="6931c-159">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="6931c-159">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="6931c-160">這會安裝執行 MVC 3 應用程式所需的元件。</span><span class="sxs-lookup"><span data-stu-id="6931c-160">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="6931c-161">本逐步解說將說明如何使用 Web Platform Installer 來安裝和設定必要的元件。</span><span class="sxs-lookup"><span data-stu-id="6931c-161">This walkthrough describes the use of the Web Platform Installer to install and configure the required components.</span></span> <span data-ttu-id="6931c-162">雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6931c-162">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="6931c-163">如需詳細資訊，請參閱 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="6931c-163">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="6931c-164">**若要安裝必要的產品和元件**</span><span class="sxs-lookup"><span data-stu-id="6931c-164">**To install the required products and components**</span></span>

1. <span data-ttu-id="6931c-165">下載並安裝 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="6931c-165">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="6931c-166">安裝完成時，Web Platform Installer 將會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="6931c-166">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6931c-167">您現在可以從 [ **開始** ] 功能表啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="6931c-167">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="6931c-168">若要這樣做，請在 [ **開始** ] 功能表上，按一下 [ **所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-168">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="6931c-169">在 **Web Platform Installer 3.0** ] 視窗的頂端，按一下 [ **產品**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-169">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="6931c-170">在視窗的左側 **，按一下 [** 流覽] 窗格中的 [架構]。</span><span class="sxs-lookup"><span data-stu-id="6931c-170">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="6931c-171">在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-171">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6931c-172">您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="6931c-172">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="6931c-173">如果已安裝產品或元件，Web Platform Installer 將會以**安裝**的文字取代 [**新增**] 按鈕來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="6931c-173">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. <span data-ttu-id="6931c-174">在 \*\*ASP.NET MVC 3 (Visual Studio 2010) \*\* 資料列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-174">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="6931c-175">在流覽窗格中，按一下 [ **伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-175">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="6931c-176">在 [ **IIS 7 建議** 的設定] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-176">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="6931c-177">在 [ **Web 部署工具 2.1** ] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-177">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="6931c-178">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="6931c-178">Click **Install**.</span></span> <span data-ttu-id="6931c-179">Web Platform Installer 將會顯示一份產品清單，其中包含要安裝之任何相關聯的相依性&#x2014;&#x2014;，並會提示您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="6931c-179">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. <span data-ttu-id="6931c-180">請參閱授權條款，如果您同意條款，請按一下 [ **我接受**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-180">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="6931c-181">當安裝完成時，請按一下 **[完成]**，然後關閉 **Web Platform Installer 3.0** 視窗。</span><span class="sxs-lookup"><span data-stu-id="6931c-181">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="6931c-182">如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，則必須執行 [ASP.NET Iis 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 註冊最新版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="6931c-182">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="6931c-183">如果您沒有這麼做，您會發現 IIS 將提供靜態內容 (像是 HTML 檔案) 沒有任何問題，但它會傳回 **HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時，找不到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="6931c-183">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="6931c-184">您可以使用這個程式來確定 ASP.NET 4.0 已註冊。</span><span class="sxs-lookup"><span data-stu-id="6931c-184">You can use this procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="6931c-185">**若要向 IIS 註冊 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="6931c-185">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="6931c-186">按一下 [ **開始**]，然後輸入 **命令提示**字元。</span><span class="sxs-lookup"><span data-stu-id="6931c-186">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="6931c-187">在搜尋結果中，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-187">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="6931c-188">在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="6931c-188">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="6931c-189">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="6931c-189">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. <span data-ttu-id="6931c-190">如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="6931c-190">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="6931c-191">若要這樣做，請在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="6931c-191">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="6931c-192">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="6931c-192">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

<span data-ttu-id="6931c-193">好的做法是，此時再次使用 Windows Update，以下載並安裝您已安裝之新產品和元件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="6931c-193">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="6931c-194">設定 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="6931c-194">Configure the IIS Website</span></span>

<span data-ttu-id="6931c-195">在您可以將 web 內容部署到伺服器之前，您必須先建立並設定 IIS 網站來裝載內容。</span><span class="sxs-lookup"><span data-stu-id="6931c-195">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="6931c-196">Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。</span><span class="sxs-lookup"><span data-stu-id="6931c-196">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="6931c-197">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="6931c-197">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="6931c-198">在檔案系統上建立資料夾來裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="6931c-198">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="6931c-199">建立 IIS 網站以提供內容，並將它與本機資料夾產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6931c-199">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="6931c-200">將讀取權限授與本機資料夾上的應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="6931c-200">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="6931c-201">雖然不會阻止您將內容部署至 IIS 中的預設網站，但不建議針對測試或示範情節以外的任何專案使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="6931c-201">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="6931c-202">若要模擬生產環境，您應該建立新的 IIS 網站，其中包含您的應用程式需求特有的設定。</span><span class="sxs-lookup"><span data-stu-id="6931c-202">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="6931c-203">**若要建立及設定 IIS 網站**</span><span class="sxs-lookup"><span data-stu-id="6931c-203">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="6931c-204">在本機檔案系統上建立資料夾，以儲存您的內容 (例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-204">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="6931c-205">在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。</span><span class="sxs-lookup"><span data-stu-id="6931c-205">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="6931c-206">在 [IIS 管理員] 的 [ **連接** ] 窗格中，展開伺服器節點 (例如 **TESTWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-206">In IIS Manager, in the **Connections** pane, expand the server node (for example, **TESTWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. <span data-ttu-id="6931c-207">以滑鼠右鍵按一下 [ **網站** ] 節點，然後按一下 [ **新增網站**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-207">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="6931c-208">在 [ **網站名稱** ] 方塊中，輸入 IIS 網站的名稱 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-208">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="6931c-209">在 [ **實體路徑** ] 方塊中，輸入 (或流覽以) 本機資料夾的路徑 (例如， **C:\DemoSite**) ]。</span><span class="sxs-lookup"><span data-stu-id="6931c-209">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="6931c-210">在 [ **埠** ] 方塊中，輸入您要用來裝載網站 (的埠號碼，例如 **85**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-210">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="6931c-211">適用于 HTTP 的標準埠號碼是80，而 HTTPS 則是443。</span><span class="sxs-lookup"><span data-stu-id="6931c-211">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="6931c-212">但是，如果您在埠80上裝載此網站，您必須先停止預設網站，才能存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="6931c-212">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="6931c-213">將 [ **主機名稱** ] 方塊保留空白，除非您要為網站設定網域名稱系統 (DNS) 記錄，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-213">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="6931c-214">在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="6931c-214">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="6931c-215">如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱 [設定網站的主機標頭 (iis 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6931c-215">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="6931c-216">如需有關 Windows Server 2008 R2 中的 DNS 伺服器角色的詳細資訊，請參閱 [Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="6931c-216">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="6931c-217">在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-217">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="6931c-218">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [新增]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6931c-218">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. <span data-ttu-id="6931c-219">在 [ **新增網站** 系結] 對話方塊中，將 [ **IP 位址** ] 和 [ **埠** ] 設定為符合您現有的網站設定。</span><span class="sxs-lookup"><span data-stu-id="6931c-219">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="6931c-220">在 [ **主機名稱** ] 方塊中，輸入您的 web 伺服器名稱 (例如， **TESTWEB1**) ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-220">In the **Host name** box, type the name of your web server (for example, **TESTWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="6931c-221">第一個網站系結可讓您使用 IP 位址和埠或，在本機存取網站 `http://localhost:85` 。</span><span class="sxs-lookup"><span data-stu-id="6931c-221">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="6931c-222">第二個網站系結可讓您使用電腦名稱稱從網域上的其他電腦存取網站 (例如， http://testweb1:85) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-222">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://testweb1:85).</span></span>
13. <span data-ttu-id="6931c-223">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [關閉]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6931c-223">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="6931c-224">在 [連線]\*\*\*\* 窗格中，按一下 [應用程式集區]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6931c-224">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="6931c-225">在 [ **應用程式** 集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [ **基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-225">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="6931c-226">根據預設，您的應用程式集區名稱會與您的網站名稱相符 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-226">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="6931c-227">在 [ **.NET Framework 版本** ] 清單中，選取 **.NET Framework v 4.0.30319**，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-227">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="6931c-228">範例解決方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="6931c-228">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="6931c-229">這不是一般 Web Deploy 的需求。</span><span class="sxs-lookup"><span data-stu-id="6931c-229">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="6931c-230">為了讓您的網站提供內容，應用程式集區身分識別必須具有儲存內容的本機資料夾的 [讀取] 許可權。</span><span class="sxs-lookup"><span data-stu-id="6931c-230">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="6931c-231">在 IIS 7.5 中，應用程式集區預設會使用唯一的應用程式集區身分識別來執行 (與舊版的 IIS 相反，因為應用程式集區通常會使用網路服務帳戶) 來執行。</span><span class="sxs-lookup"><span data-stu-id="6931c-231">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="6931c-232">應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組的清單上&#x2014;而是在應用程式集區啟動時動態建立。</span><span class="sxs-lookup"><span data-stu-id="6931c-232">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="6931c-233">每個應用程式集區身分識別都會新增至本機 **IIS \_ IUSRS** 安全性群組作為隱藏專案。</span><span class="sxs-lookup"><span data-stu-id="6931c-233">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="6931c-234">若要授與許可權給檔案或資料夾上的應用程式集區身分識別，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="6931c-234">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="6931c-235">使用 **Iis AppPool \[ 應用程式集區名稱** 的格式，直接將許可權指派給應用程式集區身分識別] (例如 **iis AppPool\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="6931c-235">Assign permissions to the application pool identity directly, using the format **IIS AppPool\[application pool name]** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="6931c-236">將許可權指派給 **IIS \_ IUSRS** 群組。</span><span class="sxs-lookup"><span data-stu-id="6931c-236">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="6931c-237">最常見的方法是將許可權指派給本機 **IIS \_ IUSRS** 群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。</span><span class="sxs-lookup"><span data-stu-id="6931c-237">The most common approach is to assign permissions to the local **IIS\_IUSRS** group because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="6931c-238">下一個程式會使用這個以群組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="6931c-238">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="6931c-239">如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱 [應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="6931c-239">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="6931c-240">**設定 IIS 網站的資料夾許可權**</span><span class="sxs-lookup"><span data-stu-id="6931c-240">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="6931c-241">在 Windows 檔案總管中，流覽至本機資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="6931c-241">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="6931c-242">在資料夾上按一下滑鼠右鍵，然後按一下 [內容]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="6931c-242">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="6931c-243">在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-243">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="6931c-244">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="6931c-244">Click **Locations**.</span></span> <span data-ttu-id="6931c-245">在 [ **位置** ] 對話方塊中，選取本機伺服器，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-245">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. <span data-ttu-id="6931c-246">在 [ **選取使用者或群組** ] 對話方塊中，輸入 **IIS \_ IUSRS**，按一下 [ **檢查名稱**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-246">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="6931c-247">在 [ \*\* (資料夾名稱的許可權) ] 對話方塊\*\*中，請注意，根據預設，已將 [ **讀取] & [執行**]、[ **列出資料夾內容**] 和 [ **讀取** ] 許可權指派給新群組。</span><span class="sxs-lookup"><span data-stu-id="6931c-247">In the **Permissions for (folder name) dialog box**, notice that the new group has been assigned the **Read & execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="6931c-248">保持不變，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="6931c-248">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="6931c-249">按一下 **[確定** ]，關閉 \*\* (資料夾名稱) \*\* 內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6931c-249">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

<span data-ttu-id="6931c-250">在您嘗試將任何 web 封裝部署到您的伺服器之前，請先確定 Web Deployment Agent 服務正在執行，這是最後一項工作。</span><span class="sxs-lookup"><span data-stu-id="6931c-250">As a final task before you attempt to deploy any web packages to your server, you should ensure that the Web Deployment Agent Service is running.</span></span> <span data-ttu-id="6931c-251">當您從遠端電腦部署封裝時，Web Deployment Agent 服務會負責解壓縮和安裝封裝的內容。</span><span class="sxs-lookup"><span data-stu-id="6931c-251">When you deploy a package from a remote computer, the Web Deployment Agent Service is responsible for extracting and installing the contents of the package.</span></span> <span data-ttu-id="6931c-252">當您安裝 Web 部署工具並以 Network Service 身分識別執行時，預設會啟動服務。</span><span class="sxs-lookup"><span data-stu-id="6931c-252">The service is started by default when you install the Web Deployment Tool and runs under the Network Service identity.</span></span>

<span data-ttu-id="6931c-253">您可以使用各種命令列公用程式或 Windows PowerShell Cmdlet，以多種不同的方式檢查服務是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="6931c-253">You can check whether a service is running in multiple different ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="6931c-254">此程式描述以 UI 為基礎的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="6931c-254">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="6931c-255">**檢查 Web Deployment Agent 服務是否正在執行**</span><span class="sxs-lookup"><span data-stu-id="6931c-255">**To check that the Web Deployment Agent Service is running**</span></span>

1. <span data-ttu-id="6931c-256">在 [開始]  功能表上，指向 [系統管理工具]  ，然後按一下 [服務]  。</span><span class="sxs-lookup"><span data-stu-id="6931c-256">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="6931c-257">找出 **Web Deployment Agent 服務** 資料列，並確認 **狀態** 設定為 [ **已啟動**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-257">Locate the **Web Deployment Agent Service** row, and verify that the **Status** is set to **Started**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. <span data-ttu-id="6931c-258">如果此服務尚未啟動，請按一下 [ **啟動**]。</span><span class="sxs-lookup"><span data-stu-id="6931c-258">If the service is not already started, click **Start**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="6931c-259">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="6931c-259">Configure Firewall Exceptions</span></span>

<span data-ttu-id="6931c-260">根據預設，遠端代理程式服務會接聽 TCP 通訊埠80，網址為：</span><span class="sxs-lookup"><span data-stu-id="6931c-260">By default, the Remote Agent Service listens on TCP port 80, at this URL:</span></span>

<http://servername.com/MSDEPLOYAGENTSERVICE>

<span data-ttu-id="6931c-261">在大多數情況下，您不需要為遠端代理程式服務設定任何額外的防火牆規則，因為網頁伺服器通常會接聽埠80上的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="6931c-261">In most cases, you won't need to configure any additional firewall rules for the Remote Agent Service because web servers typically listen for HTTP requests on port 80.</span></span> <span data-ttu-id="6931c-262">如果您將安裝自訂為在非標準埠上接聽，您將需要視需要設定防火牆例外。</span><span class="sxs-lookup"><span data-stu-id="6931c-262">If you customized your installation to listen on a nonstandard port, you'll need to configure firewall exceptions as required.</span></span>

## <a name="conclusion"></a><span data-ttu-id="6931c-263">結論</span><span class="sxs-lookup"><span data-stu-id="6931c-263">Conclusion</span></span>

<span data-ttu-id="6931c-264">至此，您的網頁伺服器已準備好接受並安裝來自遠端電腦的 web 套件。</span><span class="sxs-lookup"><span data-stu-id="6931c-264">At this point, your web server is ready to accept and install web packages from a remote computer.</span></span> <span data-ttu-id="6931c-265">在您嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查這些重點：</span><span class="sxs-lookup"><span data-stu-id="6931c-265">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="6931c-266">您是否已向 IIS 註冊 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="6931c-266">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="6931c-267">應用程式集區身分識別是否擁有您網站源資料夾的讀取存取權？</span><span class="sxs-lookup"><span data-stu-id="6931c-267">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="6931c-268">Web Deployment Agent 服務是否正在執行？</span><span class="sxs-lookup"><span data-stu-id="6931c-268">Is the Web Deployment Agent Service running?</span></span>

## <a name="further-reading"></a><span data-ttu-id="6931c-269">深入閱讀</span><span class="sxs-lookup"><span data-stu-id="6931c-269">Further Reading</span></span>

<span data-ttu-id="6931c-270">如需有關如何設定自訂 Microsoft Build Engine (MSBuild) 專案檔，以將 web 套件部署到遠端代理程式服務的指引，請參閱 [設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="6931c-270">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Remote Agent Service, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6931c-271">[上一個](scenario-configuring-a-production-environment-for-web-deployment.md) 
> [下一步](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span><span class="sxs-lookup"><span data-stu-id="6931c-271">[Previous](scenario-configuring-a-production-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)</span></span>
