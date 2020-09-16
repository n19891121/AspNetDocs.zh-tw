---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 設定 Web 服務器以 Web Deploy 發行 (離線部署) |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。 當您使用 Internet Information Services (.。。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: ed11720e6ea00df22f58d9afd32ccce95a5d1a60
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609665"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="181f7-104">設定 Web Deploy 發行的網頁伺服器 (離線部署)</span><span class="sxs-lookup"><span data-stu-id="181f7-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>

<span data-ttu-id="181f7-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="181f7-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="181f7-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="181f7-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="181f7-107">本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。</span><span class="sxs-lookup"><span data-stu-id="181f7-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="181f7-108">當您使用 Internet Information Services (IIS) Web 部署工具 (Web Deploy) 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放到 Web 服務器上。</span><span class="sxs-lookup"><span data-stu-id="181f7-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="181f7-109">您可以：</span><span class="sxs-lookup"><span data-stu-id="181f7-109">You can:</span></span>
> 
> - <span data-ttu-id="181f7-110">使用 *Web Deploy 遠端代理程式服務*。</span><span class="sxs-lookup"><span data-stu-id="181f7-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="181f7-111">這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何程式部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="181f7-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="181f7-112">使用 *Web Deploy 處理常式*。</span><span class="sxs-lookup"><span data-stu-id="181f7-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="181f7-113">這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="181f7-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="181f7-114">不過，當您使用此方法時，您可以設定 IIS 以允許非系統管理員的使用者執行部署。</span><span class="sxs-lookup"><span data-stu-id="181f7-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="181f7-115">Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="181f7-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="181f7-116">使用 *離線部署*。</span><span class="sxs-lookup"><span data-stu-id="181f7-116">Use *offline deployment*.</span></span> <span data-ttu-id="181f7-117">這種方法需要最少的 web 伺服器設定，但是伺服器管理員必須手動將 web 套件複製到伺服器上，然後透過 IIS 管理員將它匯入。</span><span class="sxs-lookup"><span data-stu-id="181f7-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="181f7-118">如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱 [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="181f7-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="181f7-119">是，如果您的網路基礎結構或安全性限制會防止遠端部署。</span><span class="sxs-lookup"><span data-stu-id="181f7-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="181f7-120">這很可能是在網際網路對向生產環境中的情況，也就是從您的伺服器基礎結構的其餘部分&#x2014;的&#x2014;，將網頁伺服器隔離。</span><span class="sxs-lookup"><span data-stu-id="181f7-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="181f7-121">很明顯地，如果您的 web 應用程式會定期更新，這種方法就變得較不理想。</span><span class="sxs-lookup"><span data-stu-id="181f7-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="181f7-122">如果您的基礎結構允許，您可能會想要考慮使用 Web Deploy 處理常式或 Web Deploy 遠端代理程式服務來啟用遠端部署。</span><span class="sxs-lookup"><span data-stu-id="181f7-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="181f7-123">工作總覽</span><span class="sxs-lookup"><span data-stu-id="181f7-123">Task Overview</span></span>

<span data-ttu-id="181f7-124">若要將網頁伺服器設定為支援離線匯入和部署 web 封裝，您必須：</span><span class="sxs-lookup"><span data-stu-id="181f7-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="181f7-125">安裝 IIS 7.5 和 IIS 7 建議的設定。</span><span class="sxs-lookup"><span data-stu-id="181f7-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="181f7-126">安裝 Web Deploy 2.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="181f7-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="181f7-127">建立 IIS 網站來裝載已部署的內容。</span><span class="sxs-lookup"><span data-stu-id="181f7-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="181f7-128">停用 Web Deployment Agent 服務。</span><span class="sxs-lookup"><span data-stu-id="181f7-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="181f7-129">若要特別裝載範例解決方案，您也需要：</span><span class="sxs-lookup"><span data-stu-id="181f7-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="181f7-130">安裝 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="181f7-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="181f7-131">安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="181f7-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="181f7-132">本主題將示範如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="181f7-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="181f7-133">本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="181f7-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="181f7-134">繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="181f7-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="181f7-135">已安裝 Windows Server 2008 R2 Service Pack 1 及所有可用的更新。</span><span class="sxs-lookup"><span data-stu-id="181f7-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="181f7-136">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="181f7-136">The server is domain-joined.</span></span>
- <span data-ttu-id="181f7-137">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="181f7-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="181f7-138">如需將電腦加入網域的詳細資訊，請參閱將 [電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="181f7-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="181f7-139">如需設定靜態 IP 位址的詳細資訊，請參閱 [設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="181f7-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="181f7-140">安裝產品和元件</span><span class="sxs-lookup"><span data-stu-id="181f7-140">Install Products and Components</span></span>

<span data-ttu-id="181f7-141">本節將引導您在 web 伺服器上安裝必要的產品和元件。</span><span class="sxs-lookup"><span data-stu-id="181f7-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="181f7-142">開始之前，最好先執行 Windows Update，以確保您的伺服器完全處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="181f7-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="181f7-143">在此情況下，您必須安裝下列專案：</span><span class="sxs-lookup"><span data-stu-id="181f7-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="181f7-144">**IIS 7 建議**的設定。</span><span class="sxs-lookup"><span data-stu-id="181f7-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="181f7-145">這可讓 web 伺服器 \*\* (iis) \*\* 角色在您的 web 伺服器上，並安裝您所需的一組 iis 模組和元件，以便裝載 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="181f7-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="181f7-146">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="181f7-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="181f7-147">若要執行以此版本的 .NET Framework 建立的應用程式，這是必要的。</span><span class="sxs-lookup"><span data-stu-id="181f7-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="181f7-148">**Web 部署工具2.1 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="181f7-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="181f7-149">這會在您的伺服器上安裝 Web Deploy (及其基礎可執行檔 MSDeploy.exe) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="181f7-150">Web Deploy 與 IIS 整合，並可讓您匯入和匯出 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="181f7-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="181f7-151">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="181f7-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="181f7-152">這會安裝執行 MVC 3 應用程式所需的元件。</span><span class="sxs-lookup"><span data-stu-id="181f7-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="181f7-153">本逐步解說將說明如何使用 Web Platform Installer 來安裝和設定各種元件。</span><span class="sxs-lookup"><span data-stu-id="181f7-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="181f7-154">雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。</span><span class="sxs-lookup"><span data-stu-id="181f7-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="181f7-155">如需詳細資訊，請參閱 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="181f7-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="181f7-156">**若要安裝必要的產品和元件**</span><span class="sxs-lookup"><span data-stu-id="181f7-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="181f7-157">下載並安裝 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="181f7-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="181f7-158">安裝完成時，Web Platform Installer 將會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="181f7-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="181f7-159">您現在可以從 [ **開始** ] 功能表啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="181f7-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="181f7-160">若要這樣做，請在 [ **開始** ] 功能表上，按一下 [ **所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="181f7-161">在 **Web Platform Installer 3.0** ] 視窗的頂端，按一下 [ **產品**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="181f7-162">在視窗的左側 **，按一下 [** 流覽] 窗格中的 [架構]。</span><span class="sxs-lookup"><span data-stu-id="181f7-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="181f7-163">在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="181f7-164">您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="181f7-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="181f7-165">如果已安裝產品或元件，Web Platform Installer 將會以**安裝**的文字取代 [**新增**] 按鈕來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="181f7-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="181f7-166">在 \*\*ASP.NET MVC 3 (Visual Studio 2010) \*\* 資料列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="181f7-167">在流覽窗格中，按一下 [ **伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="181f7-168">在 [ **IIS 7 建議** 的設定] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="181f7-169">在 [ **Web 部署工具 2.1** ] 列中，按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="181f7-170">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="181f7-170">Click **Install**.</span></span> <span data-ttu-id="181f7-171">Web Platform Installer 將會顯示一份產品清單，其中包含要安裝之任何相關聯的相依性&#x2014;&#x2014;，並會提示您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="181f7-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="181f7-172">請參閱授權條款，如果您同意條款，請按一下 [ **我接受**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="181f7-173">當安裝完成時，請按一下 **[完成]**，然後關閉 **Web Platform Installer 3.0** 視窗。</span><span class="sxs-lookup"><span data-stu-id="181f7-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="181f7-174">如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，則必須執行 [ASP.NET Iis 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 註冊最新版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="181f7-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="181f7-175">如果您沒有這麼做，您會發現 IIS 將提供靜態內容 (像是 HTML 檔案) 沒有任何問題，但它會傳回 **HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時，找不到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="181f7-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="181f7-176">您可以使用下一個程式來確定 ASP.NET 4.0 已註冊。</span><span class="sxs-lookup"><span data-stu-id="181f7-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="181f7-177">**若要向 IIS 註冊 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="181f7-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="181f7-178">按一下 [ **開始**]，然後輸入 **命令提示**字元。</span><span class="sxs-lookup"><span data-stu-id="181f7-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="181f7-179">在搜尋結果中，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="181f7-180">在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="181f7-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="181f7-181">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="181f7-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="181f7-182">如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="181f7-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="181f7-183">若要這樣做，請在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目錄。</span><span class="sxs-lookup"><span data-stu-id="181f7-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="181f7-184">輸入此命令，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="181f7-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="181f7-185">好的做法是，此時再次使用 Windows Update，以下載並安裝您已安裝之新產品和元件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="181f7-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="181f7-186">設定 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="181f7-186">Configure the IIS Website</span></span>

<span data-ttu-id="181f7-187">在您可以將 web 內容部署到伺服器之前，您必須先建立並設定 IIS 網站來裝載內容。</span><span class="sxs-lookup"><span data-stu-id="181f7-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="181f7-188">Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。</span><span class="sxs-lookup"><span data-stu-id="181f7-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="181f7-189">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="181f7-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="181f7-190">在檔案系統上建立資料夾來裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="181f7-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="181f7-191">建立 IIS 網站以提供內容，並將它與本機資料夾產生關聯。</span><span class="sxs-lookup"><span data-stu-id="181f7-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="181f7-192">將讀取權限授與本機資料夾上的應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="181f7-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="181f7-193">雖然不會阻止您將內容部署至 IIS 中的預設網站，但不建議針對測試或示範情節以外的任何專案使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="181f7-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="181f7-194">若要模擬生產環境，您應該建立新的 IIS 網站，其中包含您的應用程式需求特有的設定。</span><span class="sxs-lookup"><span data-stu-id="181f7-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="181f7-195">**若要建立及設定 IIS 網站**</span><span class="sxs-lookup"><span data-stu-id="181f7-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="181f7-196">在本機檔案系統上建立資料夾，以儲存您的內容 (例如 **C:\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="181f7-197">在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。</span><span class="sxs-lookup"><span data-stu-id="181f7-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="181f7-198">在 [IIS 管理員] 的 [ **連接** ] 窗格中，展開伺服器節點 (例如 **PROWEB1**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="181f7-199">以滑鼠右鍵按一下 [ **網站** ] 節點，然後按一下 [ **新增網站**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="181f7-200">在 [ **網站名稱** ] 方塊中，輸入 IIS 網站的名稱 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="181f7-201">在 [ **實體路徑** ] 方塊中，輸入 (或流覽以) 本機資料夾的路徑 (例如， **C:\DemoSite**) ]。</span><span class="sxs-lookup"><span data-stu-id="181f7-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="181f7-202">在 [ **埠** ] 方塊中，輸入您要用來裝載網站 (的埠號碼，例如 **85**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="181f7-203">適用于 HTTP 的標準埠號碼是80，而 HTTPS 則是443。</span><span class="sxs-lookup"><span data-stu-id="181f7-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="181f7-204">但是，如果您在埠80上裝載此網站，您必須先停止預設網站，才能存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="181f7-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="181f7-205">將 [ **主機名稱** ] 方塊保留空白，除非您要為網站設定網域名稱系統 (DNS) 記錄，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="181f7-206">在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="181f7-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="181f7-207">如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱 [設定網站的主機標頭 (iis 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="181f7-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="181f7-208">如需有關 Windows Server 2008 R2 中的 DNS 伺服器角色的詳細資訊，請參閱 [Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="181f7-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="181f7-209">在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="181f7-210">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [新增]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="181f7-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="181f7-211">在 [ **新增網站** 系結] 對話方塊中，將 [ **IP 位址** ] 和 [ **埠** ] 設定為符合您現有的網站設定。</span><span class="sxs-lookup"><span data-stu-id="181f7-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="181f7-212">在 [ **主機名稱** ] 方塊中，輸入您的 web 伺服器名稱 (例如， **PROWEB1**) ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="181f7-213">第一個網站系結可讓您使用 IP 位址和埠或，在本機存取網站 `http://localhost:85` 。</span><span class="sxs-lookup"><span data-stu-id="181f7-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="181f7-214">第二個網站系結可讓您使用電腦名稱稱從網域上的其他電腦存取網站 (例如， http://proweb1:85) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="181f7-215">在 [站台繫結]\*\*\*\* 對話方塊中，按一下 [關閉]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="181f7-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="181f7-216">在 [連線]\*\*\*\* 窗格中，按一下 [應用程式集區]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="181f7-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="181f7-217">在 [ **應用程式** 集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [ **基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="181f7-218">根據預設，您的應用程式集區名稱會與您的網站名稱相符 (例如， **DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="181f7-219">在 [ **.NET Framework 版本** ] 清單中，選取 **.NET Framework v 4.0.30319**，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="181f7-220">範例解決方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="181f7-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="181f7-221">這不是一般 Web Deploy 的需求。</span><span class="sxs-lookup"><span data-stu-id="181f7-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="181f7-222">為了讓您的網站提供內容，應用程式集區身分識別必須具有儲存內容的本機資料夾的 [讀取] 許可權。</span><span class="sxs-lookup"><span data-stu-id="181f7-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="181f7-223">在 IIS 7.5 中，應用程式集區預設會使用唯一的應用程式集區身分識別來執行 (與舊版的 IIS 相反，因為應用程式集區通常會使用網路服務帳戶) 來執行。</span><span class="sxs-lookup"><span data-stu-id="181f7-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="181f7-224">應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組的清單上&#x2014;而是在應用程式集區啟動時動態建立。</span><span class="sxs-lookup"><span data-stu-id="181f7-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="181f7-225">每個應用程式集區身分識別都會新增至本機 **IIS \_ IUSRS** 安全性群組作為隱藏專案。</span><span class="sxs-lookup"><span data-stu-id="181f7-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="181f7-226">若要授與許可權給檔案或資料夾上的應用程式集區身分識別，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="181f7-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="181f7-227">直接將許可權指派給應用程式集區身分識別，使用 \*\*Iis AppPool \( 應用程式集區名稱 \*\* 的格式)  (例如 **iis AppPool\DemoSite**) 。</span><span class="sxs-lookup"><span data-stu-id="181f7-227">Assign permissions to the application pool identity directly, using the format **IIS AppPool\(application pool name)** (for example, **IIS AppPool\DemoSite**).</span></span>
- <span data-ttu-id="181f7-228">將許可權指派給 **IIS \_ IUSRS** 群組。</span><span class="sxs-lookup"><span data-stu-id="181f7-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="181f7-229">最常見的方法是將許可權指派給本機 **IIS \_ IUSRS** 群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。</span><span class="sxs-lookup"><span data-stu-id="181f7-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="181f7-230">下一個程式會使用這個以群組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="181f7-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="181f7-231">如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱 [應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="181f7-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="181f7-232">**設定 IIS 網站的資料夾許可權**</span><span class="sxs-lookup"><span data-stu-id="181f7-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="181f7-233">在 Windows 檔案總管中，流覽至本機資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="181f7-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="181f7-234">在資料夾上按一下滑鼠右鍵，然後按一下 [內容]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="181f7-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="181f7-235">在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="181f7-236">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="181f7-236">Click **Locations**.</span></span> <span data-ttu-id="181f7-237">在 [ **位置** ] 對話方塊中，選取本機伺服器，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="181f7-238">在 [ **選取使用者或群組** ] 對話方塊中，輸入 **IIS \_ IUSRS**，按一下 [ **檢查名稱**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="181f7-239">在 [ \*\* (資料夾名稱的許可權) \*\* ] 對話方塊中，請注意，根據預設，已將 [ **讀取] & [執行**]、[ **列出資料夾內容**] 和 [ **讀取** ] 許可權指派給新群組。</span><span class="sxs-lookup"><span data-stu-id="181f7-239">In the **Permissions for (folder name)** dialog box, notice that the new group has been assigned the **Read & execute**, **List folder contents**, and **Read** permissions by default.</span></span> <span data-ttu-id="181f7-240">保持不變，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-240">Leave this unchanged and click **OK**.</span></span>
7. <span data-ttu-id="181f7-241">按一下 **[確定** ]，關閉 \*\* (資料夾名稱) \*\* 內容] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="181f7-241">Click **OK** to close the **(folder name) Properties** dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="181f7-242">停用遠端代理程式服務</span><span class="sxs-lookup"><span data-stu-id="181f7-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="181f7-243">當您安裝 Web Deploy 時，Web Deployment Agent 服務會自動安裝並啟動。</span><span class="sxs-lookup"><span data-stu-id="181f7-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="181f7-244">這種服務可讓您從遠端位置部署和發佈 web 套件。</span><span class="sxs-lookup"><span data-stu-id="181f7-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="181f7-245">在此案例中，您將不會使用遠端部署功能，因此您應該停止並停用服務。</span><span class="sxs-lookup"><span data-stu-id="181f7-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="181f7-246">您不需要停止遠端代理程式服務，就能手動匯入和部署 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="181f7-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="181f7-247">不過，如果您不打算使用服務，最好是停止並停用服務。</span><span class="sxs-lookup"><span data-stu-id="181f7-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>

<span data-ttu-id="181f7-248">您可以使用各種命令列公用程式或 Windows PowerShell Cmdlet，以多種方式來停止和停用服務。</span><span class="sxs-lookup"><span data-stu-id="181f7-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="181f7-249">此程式描述以 UI 為基礎的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="181f7-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="181f7-250">**停止和停用遠端代理程式服務**</span><span class="sxs-lookup"><span data-stu-id="181f7-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="181f7-251">在 [開始]  功能表上，指向 [系統管理工具]  ，然後按一下 [服務]  。</span><span class="sxs-lookup"><span data-stu-id="181f7-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="181f7-252">在 [服務] 主控台中，找出 **Web Deployment Agent 服務** 資料列。</span><span class="sxs-lookup"><span data-stu-id="181f7-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="181f7-253">以滑鼠右鍵按一下 [ **Web Deployment Agent Service**]， **然後按一下 [** 內容]。</span><span class="sxs-lookup"><span data-stu-id="181f7-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="181f7-254">在 **Web Deployment Agent 服務屬性** ] 對話方塊中，按一下 [ **停止**]。</span><span class="sxs-lookup"><span data-stu-id="181f7-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="181f7-255">在 [ **啟動類型** ] 清單中，選取 [ **已停用**]，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="181f7-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="181f7-256">結論</span><span class="sxs-lookup"><span data-stu-id="181f7-256">Conclusion</span></span>

<span data-ttu-id="181f7-257">至此，您的網頁伺服器已準備好進行離線 web 封裝部署。</span><span class="sxs-lookup"><span data-stu-id="181f7-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="181f7-258">在您嘗試將 web 套件匯入至 IIS 網站之前，您可能會想要檢查這些重點：</span><span class="sxs-lookup"><span data-stu-id="181f7-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="181f7-259">您是否已向 IIS 註冊 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="181f7-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="181f7-260">應用程式集區身分識別是否擁有您網站源資料夾的讀取存取權？</span><span class="sxs-lookup"><span data-stu-id="181f7-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="181f7-261">您是否已停止 Web Deployment Agent 服務？</span><span class="sxs-lookup"><span data-stu-id="181f7-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="181f7-262">[上一個](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 
> [下一步](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="181f7-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
