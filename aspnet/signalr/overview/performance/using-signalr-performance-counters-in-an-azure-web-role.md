---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: 在 Azure Web 角色中使用 SignalR 效能計數器 |Microsoft Docs
author: guardrex
description: 如何在 Azure Web 角色中安裝和使用 SignalR 效能計數器。
keywords: ASP.NET，signalr，效能計數器，azure web 角色
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240643"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a><span data-ttu-id="660fe-104">使用 Azure Web 角色中的 SignalR 效能計數器</span><span class="sxs-lookup"><span data-stu-id="660fe-104">Using SignalR performance counters in an Azure Web Role</span></span>

<span data-ttu-id="660fe-105">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="660fe-105">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="660fe-106">SignalR 效能計數器是用來監視您的應用程式在 Azure Web 角色中的效能。</span><span class="sxs-lookup"><span data-stu-id="660fe-106">SignalR performance counters are used to monitor your app's performance in an Azure Web Role.</span></span> <span data-ttu-id="660fe-107">這些計數器是由 Microsoft Azure 診斷所捕捉。</span><span class="sxs-lookup"><span data-stu-id="660fe-107">The counters are captured by Microsoft Azure Diagnostics.</span></span> <span data-ttu-id="660fe-108">您可以使用*signalr.exe*（用於獨立或內部部署應用程式的相同工具），在 Azure 上安裝 SignalR 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="660fe-108">You install SignalR performance counters on Azure with *signalr.exe*, the same tool used for standalone or on-premises apps.</span></span> <span data-ttu-id="660fe-109">由於 Azure 角色是暫時性的，因此您可以設定應用程式在啟動時安裝並註冊 SignalR 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="660fe-109">Since Azure roles are transient, you configure an app to install and register SignalR performance counters upon startup.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="660fe-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="660fe-110">Prerequisites</span></span>

* <span data-ttu-id="660fe-111">Visual Studio 2015 或[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span><span class="sxs-lookup"><span data-stu-id="660fe-111">Visual Studio 2015 or [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)</span></span>
* <span data-ttu-id="660fe-112">[Visual Studio 的 MICROSOFT AZURE SDK](https://azure.microsoft.com/downloads/) **附注：安裝 sdk 之後，請重新開機您的電腦。**</span><span class="sxs-lookup"><span data-stu-id="660fe-112">[Microsoft Azure SDK for Visual Studio](https://azure.microsoft.com/downloads/) **Note: Restart your machine after installing the SDK.**</span></span>
* <span data-ttu-id="660fe-113">Microsoft Azure 訂用帳戶：若要註冊免費的 Azure 試用帳戶，請參閱[Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="660fe-113">Microsoft Azure subscription: To sign up for a free Azure trial account, see [Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a><span data-ttu-id="660fe-114">建立可公開 SignalR 效能計數器的 Azure Web 角色應用程式</span><span class="sxs-lookup"><span data-stu-id="660fe-114">Creating an Azure Web Role application that exposes SignalR performance counters</span></span>

1. <span data-ttu-id="660fe-115">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="660fe-115">Open Visual Studio.</span></span>

2. <span data-ttu-id="660fe-116">在 Visual Studio 中，選取 [檔案] >  [新增] >  [專案]。</span><span class="sxs-lookup"><span data-stu-id="660fe-116">In Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="660fe-117">在 [**新增專案**] 對話方塊中，選取左側的 [ **Visual c #**  >  **雲端**] 類別，然後選取 [ **Azure 雲端服務**] 範本。</span><span class="sxs-lookup"><span data-stu-id="660fe-117">In the **New Project** dialog box, select the **Visual C#** > **Cloud** category on the left, and then select the **Azure Cloud Service** template.</span></span> <span data-ttu-id="660fe-118">將應用程式命名為**SignalRPerfCounters** ，然後選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="660fe-118">Name the app **SignalRPerfCounters** and select **OK**.</span></span>

   ![新的雲端應用程式](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > <span data-ttu-id="660fe-120">如果您沒有看到 [**雲端**範本] 類別或 [ **azure 雲端服務**] 範本，則需要安裝適用于 Visual Studio 2017 的**Azure 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="660fe-120">If you don't see the **Cloud** template category or the **Azure Cloud Service** template, you need to install the **Azure development** workload for Visual Studio 2017.</span></span> <span data-ttu-id="660fe-121">選擇 [**新增專案**] 對話方塊左下角的 [**開啟 Visual Studio 安裝程式**] 連結，以開啟 Visual Studio 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="660fe-121">Choose the **Open Visual Studio Installer** link on the bottom-left side of the **New Project** dialog to open Visual Studio Installer.</span></span> <span data-ttu-id="660fe-122">選取 [ **Azure 開發**] 工作負載，然後選擇 [**修改**] 以開始安裝工作負載。</span><span class="sxs-lookup"><span data-stu-id="660fe-122">Select the **Azure development** workload, and then choose **Modify** to start installing the workload.</span></span>
   >
   > ![Visual Studio 安裝程式中的 Azure 開發工作負載](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. <span data-ttu-id="660fe-124">在 [**新增 Microsoft Azure 雲端服務**] 對話方塊中，選取 [ **ASP.NET Web 角色**]，然後選取 [>] 按鈕，將角色新增至專案。</span><span class="sxs-lookup"><span data-stu-id="660fe-124">In the **New Microsoft Azure Cloud Service** dialog, select **ASP.NET Web Role** and select the > button to add the role to the project.</span></span> <span data-ttu-id="660fe-125">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="660fe-125">Select **OK**.</span></span>

   ![新增 ASP.NET Web 角色](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. <span data-ttu-id="660fe-127">在 [**新增 ASP.NET Web 應用程式-WebRole1** ] 對話方塊中，選取 [ **MVC** ] 範本，然後選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="660fe-127">In the **New ASP.NET Web Application - WebRole1** dialog, select the **MVC** template, and then select **OK**.</span></span>

   ![新增 MVC 和 Web API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. <span data-ttu-id="660fe-129">在**方案總管**中，開啟**WebRole1**下的*diagnostics.wadcfgx*檔案。</span><span class="sxs-lookup"><span data-stu-id="660fe-129">In **Solution Explorer**, open the *diagnostics.wadcfgx* file under **WebRole1**.</span></span>

   ![方案總管診斷 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. <span data-ttu-id="660fe-131">以下列設定取代檔案的內容，並儲存檔案：</span><span class="sxs-lookup"><span data-stu-id="660fe-131">Replace the contents of the file with the following configuration and save the file:</span></span>

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. <span data-ttu-id="660fe-132">從 [**工具**] [NuGet 套件管理員] 開啟 [**套件管理員主控台**]  >  \*\* \*\*。</span><span class="sxs-lookup"><span data-stu-id="660fe-132">Open the **Package Manager Console** from **Tools** > **NuGet Package Manager**.</span></span> <span data-ttu-id="660fe-133">輸入下列命令以安裝最新版本的 SignalR 和 SignalR 公用程式套件：</span><span class="sxs-lookup"><span data-stu-id="660fe-133">Enter the following commands to install the latest version of SignalR and the SignalR utilities package:</span></span>

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. <span data-ttu-id="660fe-134">設定應用程式，以便在啟動或回收時，將 SignalR 效能計數器安裝到角色實例。</span><span class="sxs-lookup"><span data-stu-id="660fe-134">Configure the app to install the SignalR performance counters into the role instance when it starts up or recycles.</span></span> <span data-ttu-id="660fe-135">在**方案總管**中，以滑鼠右鍵按一下**WebRole1**專案，然後選取 [**加入**  >  **新資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-135">In **Solution Explorer**, right-click on the **WebRole1** project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="660fe-136">將新資料夾命名為*Startup*。</span><span class="sxs-lookup"><span data-stu-id="660fe-136">Name the new folder *Startup*.</span></span>

   ![加入開機檔案夾](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. <span data-ttu-id="660fe-138">從**Microsoft.AspNet.SignalR.Utils** /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. *signalr.exe* \<project folder> 複製 \<version>signalr.exe檔案（以 Utils 套件新增）/tools 至您在上一個步驟中建立的 [*啟動*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="660fe-138">Copy the *signalr.exe* file (added with the **Microsoft.AspNet.SignalR.Utils** package) from \<project folder>/SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\<version>/tools to the *Startup* folder you created in the previous step.</span></span>

11. <span data-ttu-id="660fe-139">在**方案總管**中，以滑鼠右鍵按一下 [*啟動*] 資料夾，然後選取 [**新增**] [  >  **現有專案**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-139">In **Solution Explorer**, right-click the *Startup* folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="660fe-140">在出現的對話方塊中，選取 [ *signalr.exe* ]，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-140">In the dialog that appears, select *signalr.exe* and select **Add**.</span></span>

    ![將 signalr.exe 新增至專案](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. <span data-ttu-id="660fe-142">以滑鼠右鍵按一下您所建立的 [*啟動*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="660fe-142">Right-click on the *Startup* folder you created.</span></span> <span data-ttu-id="660fe-143">選取 [**加入**  >  **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-143">Select **Add** > **New Item**.</span></span> <span data-ttu-id="660fe-144">選取 [**一般**] 節點，選取 [**文字檔**]，並將新專案命名為*SignalRPerfCounterInstall。*</span><span class="sxs-lookup"><span data-stu-id="660fe-144">Select the **General** node, select **Text File**, and name the new item *SignalRPerfCounterInstall.cmd*.</span></span> <span data-ttu-id="660fe-145">此命令檔會將 SignalR 效能計數器安裝到 web 角色。</span><span class="sxs-lookup"><span data-stu-id="660fe-145">This command file will install the SignalR performance counters into the web role.</span></span>

    ![建立 SignalR 效能計數器安裝批次檔](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. <span data-ttu-id="660fe-147">當 Visual Studio 建立*SignalRPerfCounterInstall .cmd*檔案時，它會自動在主視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="660fe-147">When Visual Studio creates the *SignalRPerfCounterInstall.cmd* file, it will automatically open in the main window.</span></span> <span data-ttu-id="660fe-148">使用下列腳本來取代檔案的內容，然後儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="660fe-148">Replace the contents of the file with the following script, then save and close the file.</span></span> <span data-ttu-id="660fe-149">此腳本會執行*signalr.exe*，這會將 SignalR 效能計數器新增至角色實例。</span><span class="sxs-lookup"><span data-stu-id="660fe-149">This script executes *signalr.exe*, which adds the SignalR performance counters to the role instance.</span></span>

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. <span data-ttu-id="660fe-150">選取**方案總管**中的*signalr.exe*檔案。</span><span class="sxs-lookup"><span data-stu-id="660fe-150">Select the *signalr.exe* file in **Solution Explorer**.</span></span> <span data-ttu-id="660fe-151">在檔案的**屬性**中，將 [**複製到輸出目錄**] 設定為 [**永遠複製**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-151">In the file's **Properties**, set **Copy to Output Directory** to **Copy Always**.</span></span>

    ![將 [複製到輸出目錄] 設定為 [永遠複製]](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. <span data-ttu-id="660fe-153">針對*SignalRPerfCounterInstall* ，重複上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="660fe-153">Repeat the previous step for the *SignalRPerfCounterInstall.cmd* file.</span></span>

16. <span data-ttu-id="660fe-154">以滑鼠右鍵按一下 [ *SignalRPerfCounterInstall* ] 檔案，然後選取 [**開啟方式**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-154">Right-click on the *SignalRPerfCounterInstall.cmd* file and select **Open With**.</span></span> <span data-ttu-id="660fe-155">在出現的對話方塊中，選取 [**二進位編輯器**]，然後選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="660fe-155">In the dialog that appears, select **Binary Editor** and select **OK**.</span></span>

    ![以二進位編輯器開啟](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. <span data-ttu-id="660fe-157">在二進位編輯器中，選取檔案中的任何前置位元組並加以刪除。</span><span class="sxs-lookup"><span data-stu-id="660fe-157">In the binary editor, select any leading bytes in the file and delete them.</span></span> <span data-ttu-id="660fe-158">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="660fe-158">Save and close the file.</span></span>

    ![刪除前置位元組](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. <span data-ttu-id="660fe-160">開啟*ServiceDefinition* ，並新增啟動工作，以在服務啟動時執行*SignalrPerfCounterInstall .cmd*檔案：</span><span class="sxs-lookup"><span data-stu-id="660fe-160">Open *ServiceDefinition.csdef* and add a startup task that executes the *SignalrPerfCounterInstall.cmd* file when the service starts up:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. <span data-ttu-id="660fe-161">開啟 `Views/Shared/_Layout.cshtml` 並移除檔案結尾的 jQuery 配套腳本。</span><span class="sxs-lookup"><span data-stu-id="660fe-161">Open `Views/Shared/_Layout.cshtml` and remove the jQuery bundle script from the end of the file.</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. <span data-ttu-id="660fe-162">新增會持續在伺服器上呼叫方法的 JavaScript 用戶端 `increment` 。</span><span class="sxs-lookup"><span data-stu-id="660fe-162">Add a JavaScript client that continuously calls the `increment` method on the server.</span></span> <span data-ttu-id="660fe-163">開啟 `Views/Home/Index.cshtml` ，並將內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="660fe-163">Open `Views/Home/Index.cshtml` and replace the contents with the following code:</span></span>

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. <span data-ttu-id="660fe-164">在名為*hub*的**WebRole1**專案中建立新的資料夾。</span><span class="sxs-lookup"><span data-stu-id="660fe-164">Create a new folder in the **WebRole1** project named *Hubs*.</span></span> <span data-ttu-id="660fe-165">以滑鼠右鍵按一下**方案總管**中的 [*中樞*] 資料夾，**然後選取 [**  >  **新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-165">Right-click the *Hubs* folder in **Solution Explorer** and select **Add** > **New Item**.</span></span> <span data-ttu-id="660fe-166">在 [**加入新專案**] 對話方塊中，選取 [ **Web**  >  **SignalR** ] 類別，然後選取 [ **SignalR Hub Class （v2）** ] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="660fe-166">In the **Add New Item** dialog box, select the **Web** > **SignalR** category, and then select the **SignalR Hub Class (v2)** item template.</span></span> <span data-ttu-id="660fe-167">將新的中樞命名為*MyHub.cs* ，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-167">Name the new hub *MyHub.cs* and select **Add**.</span></span>

    ![將 SignalR 中樞類別新增至 [新增專案] 對話方塊中的 [中樞] 資料夾](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. <span data-ttu-id="660fe-169">*MyHub.cs*會自動在主視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="660fe-169">*MyHub.cs* will automatically open in the main window.</span></span> <span data-ttu-id="660fe-170">將內容取代為下列程式碼，然後儲存並關閉檔案：</span><span class="sxs-lookup"><span data-stu-id="660fe-170">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. <span data-ttu-id="660fe-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* 是 SignalR 程式碼基底所提供的連接密度測試控管。</span><span class="sxs-lookup"><span data-stu-id="660fe-171">*[Crank.exe](signalr-connection-density-testing-with-crank.md)* is a connection density testing tool provided with the SignalR codebase.</span></span> <span data-ttu-id="660fe-172">由於迅速地建立需要持續連線，因此您可以將其新增至您的網站，以便在測試時使用。</span><span class="sxs-lookup"><span data-stu-id="660fe-172">Since Crank requires a persistent connection, you add one to your site for use when testing.</span></span> <span data-ttu-id="660fe-173">將新資料夾新增至名為*PersistentConnections*的**WebRole1**專案。</span><span class="sxs-lookup"><span data-stu-id="660fe-173">Add a new folder to the **WebRole1** project called *PersistentConnections*.</span></span> <span data-ttu-id="660fe-174">以滑鼠右鍵按一下此資料夾，然後選取 [**新增**  >  **類別**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-174">Right-click this folder and select **Add** > **Class**.</span></span> <span data-ttu-id="660fe-175">將新的類別檔案命名為*MyPersistentConnections.cs* ，**然後選取 [新增]**。</span><span class="sxs-lookup"><span data-stu-id="660fe-175">Name the new class file *MyPersistentConnections.cs* and select **Add**.</span></span>

24. <span data-ttu-id="660fe-176">Visual Studio 會在主視窗中開啟*MyPersistentConnections.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="660fe-176">Visual Studio will open the *MyPersistentConnections.cs* file in the main window.</span></span> <span data-ttu-id="660fe-177">將內容取代為下列程式碼，然後儲存並關閉檔案：</span><span class="sxs-lookup"><span data-stu-id="660fe-177">Replace the contents with the following code, then save and close the file:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. <span data-ttu-id="660fe-178">使用 `Startup` 類別時，SignalR 物件會在 OWIN 啟動時啟動。</span><span class="sxs-lookup"><span data-stu-id="660fe-178">Using the `Startup` class, the SignalR objects start when OWIN starts up.</span></span> <span data-ttu-id="660fe-179">開啟或建立*Startup.cs* ，並將內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="660fe-179">Open or create *Startup.cs* and replace the contents with the following code:</span></span>

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    <span data-ttu-id="660fe-180">在上述程式碼中， `OwinStartup` 屬性會標示此類別以開始 OWIN。</span><span class="sxs-lookup"><span data-stu-id="660fe-180">In the code above, the `OwinStartup` attribute marks this class to start OWIN.</span></span> <span data-ttu-id="660fe-181">`Configuration`方法會啟動 SignalR。</span><span class="sxs-lookup"><span data-stu-id="660fe-181">The `Configuration` method starts SignalR.</span></span>

26. <span data-ttu-id="660fe-182">按**F5**在 Microsoft Azure 模擬器中測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="660fe-182">Test your application in the Microsoft Azure Emulator by pressing **F5**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="660fe-183">如果您在**MapSignalR**遇到**FileLoadException** ，請將*web.config*中的系結重新導向變更為下列內容：</span><span class="sxs-lookup"><span data-stu-id="660fe-183">If you encounter a **FileLoadException** at **MapSignalR**, change the binding redirects in *web.config* to the following:</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. <span data-ttu-id="660fe-184">等待約一分鐘。</span><span class="sxs-lookup"><span data-stu-id="660fe-184">Wait about one minute.</span></span> <span data-ttu-id="660fe-185">在 Visual Studio 中開啟 [Cloud Explorer 工具] 視窗（**View**  >  **Cloud Explorer**），然後展開路徑 `(Local)/Storage Accounts/(Development)/Tables` 。</span><span class="sxs-lookup"><span data-stu-id="660fe-185">Open the Cloud Explorer tool window in Visual Studio (**View** > **Cloud Explorer**) and expand the path `(Local)/Storage Accounts/(Development)/Tables`.</span></span> <span data-ttu-id="660fe-186">按兩下 [ **WADPerformanceCountersTable**]。</span><span class="sxs-lookup"><span data-stu-id="660fe-186">Double-click **WADPerformanceCountersTable**.</span></span> <span data-ttu-id="660fe-187">您應該會在資料表資料中看到 SignalR 計數器。</span><span class="sxs-lookup"><span data-stu-id="660fe-187">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="660fe-188">如果您看不到資料表，可能需要重新輸入您的 Azure 儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="660fe-188">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="660fe-189">您可能需要選取 [重新整理] 按鈕來查看**Cloud Explorer**中的資料表，或選取 [開啟資料表] 視窗中的 [重新整理 **] 按鈕，** 以查看資料表**中的資料**。</span><span class="sxs-lookup"><span data-stu-id="660fe-189">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

    ![選取 Visual Studio Cloud Explorer 中的 WAD 效能計數器資料表](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![顯示 WAD 效能計數器資料表中收集的計數器](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. <span data-ttu-id="660fe-192">若要在雲端中測試您的應用程式，請更新**serviceconfiguration.cscfg** ，並將設定 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 為有效的 Azure 儲存體帳戶連接字串。</span><span class="sxs-lookup"><span data-stu-id="660fe-192">To test your application in the cloud, update the **ServiceConfiguration.Cloud.cscfg** file and set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` to a valid Azure Storage account connection string.</span></span>

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. <span data-ttu-id="660fe-193">將應用程式部署至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="660fe-193">Deploy the application to your Azure subscription.</span></span> <span data-ttu-id="660fe-194">如需如何將應用程式部署至 Azure 的詳細資訊，請參閱[如何建立和部署雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)。</span><span class="sxs-lookup"><span data-stu-id="660fe-194">For details on how to deploy an application to Azure, see [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span>

30. <span data-ttu-id="660fe-195">請等待數分鐘。</span><span class="sxs-lookup"><span data-stu-id="660fe-195">Wait a few minutes.</span></span> <span data-ttu-id="660fe-196">在**Cloud Explorer**中，找出您在上面設定的儲存體帳戶，並 `WADPerformanceCountersTable` 在其中尋找資料表。</span><span class="sxs-lookup"><span data-stu-id="660fe-196">In **Cloud Explorer**, locate the storage account you configured above and find the `WADPerformanceCountersTable` table in it.</span></span> <span data-ttu-id="660fe-197">您應該會在資料表資料中看到 SignalR 計數器。</span><span class="sxs-lookup"><span data-stu-id="660fe-197">You should see SignalR counters in the table data.</span></span> <span data-ttu-id="660fe-198">如果您看不到資料表，可能需要重新輸入您的 Azure 儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="660fe-198">If you don't see the table, you may need to re-enter your Azure Storage credentials.</span></span> <span data-ttu-id="660fe-199">您可能需要選取 [重新整理] 按鈕來查看**Cloud Explorer**中的資料表，或選取 [開啟資料表] 視窗中的 [重新整理 **] 按鈕，** 以查看資料表**中的資料**。</span><span class="sxs-lookup"><span data-stu-id="660fe-199">You may need to select the **Refresh** button to see the table in **Cloud Explorer** or select the **Refresh** button in the open table window to see data in the table.</span></span>

<span data-ttu-id="660fe-200">特別感謝這個教學課程中使用的原始內容的[聖馬丁 Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 。</span><span class="sxs-lookup"><span data-stu-id="660fe-200">Special thanks to [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) for the original content used in this tutorial.</span></span>
