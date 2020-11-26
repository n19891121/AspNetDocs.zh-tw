---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure 背景工作角色中的主機 OWIN |Microsoft Docs
author: MikeWasson
description: 本教學課程說明如何在 Microsoft Azure 背景工作角色中自行裝載 OWIN。 Open Web Interface for .NET (OWIN) 定義 .NET web 伺服器之間的抽象 .。。
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: f4faeda4cc8428c54b761f30833f9a31edfd2ddb
ms.sourcegitcommit: 4b78855427f1397df0a7be3559e04ec94a78c308
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96151889"
---
# <a name="host-owin-in-an-azure-worker-role"></a><span data-ttu-id="fc107-104">將 OWIN 裝載在 Azure 背景工作角色中</span><span class="sxs-lookup"><span data-stu-id="fc107-104">Host OWIN in an Azure Worker Role</span></span>

<span data-ttu-id="fc107-105">由 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fc107-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="fc107-106">本教學課程說明如何在 Microsoft Azure 背景工作角色中自行裝載 OWIN。</span><span class="sxs-lookup"><span data-stu-id="fc107-106">This tutorial shows how to self-host OWIN in a Microsoft Azure worker role.</span></span>
>
> <span data-ttu-id="fc107-107">[Open Web Interface for .net](http://owin.org/) (OWIN) 定義 .net web 伺服器和 Web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="fc107-107">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="fc107-108">OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 很適合在您自己的進程中（例如，在 Azure 背景工作角色內）自我裝載 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc107-108">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="fc107-109">在本教學課程中，您將瞭解如何在 Microsoft Azure 背景工作角色內自我裝載 OWIN 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc107-109">In this tutorial, you'll learn how to self-host an OWIN applications inside a Microsoft Azure worker role.</span></span> <span data-ttu-id="fc107-110">若要深入瞭解背景工作角色，請參閱 [Azure 執行模型](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices)。</span><span class="sxs-lookup"><span data-stu-id="fc107-110">To learn more about worker roles, see [Azure Execution Models](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fc107-111">本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="fc107-111">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="fc107-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fc107-112">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [<span data-ttu-id="fc107-113">Azure SDK for .NET 2.3</span><span class="sxs-lookup"><span data-stu-id="fc107-113">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)
> - [<span data-ttu-id="fc107-114">Owin. Selfhost 2.1。0</span><span class="sxs-lookup"><span data-stu-id="fc107-114">Microsoft.Owin.Selfhost 2.1.0</span></span>](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="fc107-115">建立 Microsoft Azure 專案</span><span class="sxs-lookup"><span data-stu-id="fc107-115">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="fc107-116">以系統管理員許可權啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="fc107-116">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="fc107-117">需要有系統管理員許可權，才能使用 Azure 計算模擬器在本機上進行應用程式的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="fc107-117">Administrator privileges are needed to debug the application locally, using the Azure Compute Emulator.</span></span>

<span data-ttu-id="fc107-118">**在 [檔案**] 功能表上，按一下 [**新增**]，然後按一下 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-118">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="fc107-119">從 **已安裝的範本**，在 Visual c # 底下，按一下 [ **雲端** ]，然後按一下 [ **Windows Azure 雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-119">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="fc107-120">將專案命名為 ">azureapp.java"，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="fc107-120">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="fc107-121">在 [ **新的 Windows Azure 雲端服務** ] 對話方塊中，按兩下 [背景 **工作角色**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-121">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="fc107-122">將預設名稱保留 ( "WorkerRole1" ) 。</span><span class="sxs-lookup"><span data-stu-id="fc107-122">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="fc107-123">此步驟會將背景工作角色新增至方案。</span><span class="sxs-lookup"><span data-stu-id="fc107-123">This step adds a worker role to the solution.</span></span> <span data-ttu-id="fc107-124">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="fc107-124">Click **OK**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="fc107-125">所建立的 Visual Studio 方案包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="fc107-125">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="fc107-126">&quot;>azureapp.java 會 &quot; 定義 Azure 應用程式的角色和設定。</span><span class="sxs-lookup"><span data-stu-id="fc107-126">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="fc107-127">&quot;WorkerRole1 &quot; 包含背景工作角色的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fc107-127">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="fc107-128">一般而言，Azure 應用程式可以包含多個角色，雖然本教學課程使用單一角色。</span><span class="sxs-lookup"><span data-stu-id="fc107-128">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a><span data-ttu-id="fc107-129">新增 OWIN Self-Host 套件</span><span class="sxs-lookup"><span data-stu-id="fc107-129">Add the OWIN Self-Host Packages</span></span>

<span data-ttu-id="fc107-130">從 [ **工具** ] 功能表按一下 [ **NuGet 封裝管理員**]，然後按一下 [ **封裝管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-130">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="fc107-131">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fc107-131">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="fc107-132">新增 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="fc107-132">Add an HTTP Endpoint</span></span>

<span data-ttu-id="fc107-133">在方案總管中，展開 [>azureapp.java] 專案。</span><span class="sxs-lookup"><span data-stu-id="fc107-133">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="fc107-134">展開 [角色] 節點，以滑鼠右鍵按一下 [WorkerRole1]，然後選取 [ **屬性**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-134">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="fc107-135">按一下 **[端點]**，然後按一下 **[新增端點]**。</span><span class="sxs-lookup"><span data-stu-id="fc107-135">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="fc107-136">在 [ **通訊協定** ] 下拉式清單中，選取 [HTTP]。</span><span class="sxs-lookup"><span data-stu-id="fc107-136">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="fc107-137">在 [ **公用埠** ] 和 [ **私人埠**] 中，輸入80。</span><span class="sxs-lookup"><span data-stu-id="fc107-137">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="fc107-138">這些連接埠號碼可以不同。</span><span class="sxs-lookup"><span data-stu-id="fc107-138">These port numbers can be different.</span></span> <span data-ttu-id="fc107-139">公用埠是用戶端將要求傳送至角色時所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="fc107-139">The public port is what clients use when they send a request to the role.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a><span data-ttu-id="fc107-140">建立 OWIN Startup 類別</span><span class="sxs-lookup"><span data-stu-id="fc107-140">Create the OWIN Startup Class</span></span>

<span data-ttu-id="fc107-141">在方案總管中，以滑鼠右鍵按一下 WorkerRole1 專案，然後選取 [**加入**  /  **類別**] 來加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="fc107-141">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="fc107-142">將類別命名為 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="fc107-142">Name the class `Startup`.</span></span>

<span data-ttu-id="fc107-143">以下列程式碼取代所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="fc107-143">Replace all of the boilerplate code with the following:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

<span data-ttu-id="fc107-144">`UseWelcomePage`擴充方法會將簡單的 HTML 網頁新增至您的應用程式，以確認網站可正常運作。</span><span class="sxs-lookup"><span data-stu-id="fc107-144">The `UseWelcomePage` extension method adds a simple HTML page to your application, to verify the site is working.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="fc107-145">啟動 OWIN 主機</span><span class="sxs-lookup"><span data-stu-id="fc107-145">Start the OWIN Host</span></span>

<span data-ttu-id="fc107-146">開啟 WorkerRole.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="fc107-146">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="fc107-147">這個類別會定義在背景工作角色啟動和停止時所執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fc107-147">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="fc107-148">加入下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="fc107-148">Add the following using statement:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="fc107-149">將 **IDisposable** 成員新增至 `WorkerRole` 類別：</span><span class="sxs-lookup"><span data-stu-id="fc107-149">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="fc107-150">在 `OnStart` 方法中，新增下列程式碼以啟動主機：</span><span class="sxs-lookup"><span data-stu-id="fc107-150">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

<span data-ttu-id="fc107-151">**WebApp 啟動** 方法會啟動 OWIN 主控制項。</span><span class="sxs-lookup"><span data-stu-id="fc107-151">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="fc107-152">類別的名稱 `Startup` 是方法的型別參數。</span><span class="sxs-lookup"><span data-stu-id="fc107-152">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="fc107-153">依照慣例，主機會呼叫 `Configure` 這個類別的方法。</span><span class="sxs-lookup"><span data-stu-id="fc107-153">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="fc107-154">覆寫 `OnStop` 以處置 *\_ 應用程式* 實例：</span><span class="sxs-lookup"><span data-stu-id="fc107-154">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

<span data-ttu-id="fc107-155">以下是 WorkerRole.cs 的完整程式碼：</span><span class="sxs-lookup"><span data-stu-id="fc107-155">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="fc107-156">建立方案，然後按 F5，在 Azure 計算模擬器中本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc107-156">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="fc107-157">根據您的防火牆設定，您可能需要允許模擬器通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="fc107-157">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

<span data-ttu-id="fc107-158">計算模擬器會將本機 IP 位址指派給端點。</span><span class="sxs-lookup"><span data-stu-id="fc107-158">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="fc107-159">您可以藉由查看計算模擬器 UI 來尋找 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fc107-159">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="fc107-160">在工作列通知區域中的模擬器圖示上按一下滑鼠右鍵，然後選取 [ **顯示計算模擬器 UI**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-160">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="fc107-161">在 [服務部署]、[部署 [識別碼]]、[服務詳細資料] 底下尋找 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fc107-161">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="fc107-162">開啟網頁瀏覽器並流覽至 HTTP： \/ \/ *address*，其中 *address* 是計算模擬器所指派的 IP 位址; 例如 `http://127.0.0.1:80` 。</span><span class="sxs-lookup"><span data-stu-id="fc107-162">Open a web browser and navigate to http:\/\/*address*, where *address* is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80`.</span></span> <span data-ttu-id="fc107-163">您應該會看到 OWIN 歡迎使用頁面：</span><span class="sxs-lookup"><span data-stu-id="fc107-163">You should see the OWIN welcome page:</span></span>

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="fc107-164">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="fc107-164">Deploy to Azure</span></span>

<span data-ttu-id="fc107-165">在此步驟中，您必須擁有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc107-165">For this step, you must have an Azure account.</span></span> <span data-ttu-id="fc107-166">如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc107-166">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fc107-167">如需詳細資訊，請參閱 [Microsoft Azure 免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="fc107-167">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="fc107-168">在方案總管中，以滑鼠右鍵按一下 [>azureapp.java] 專案。</span><span class="sxs-lookup"><span data-stu-id="fc107-168">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="fc107-169">選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="fc107-169">Select **Publish**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image12.png)

<span data-ttu-id="fc107-170">如果您未登入 Azure 帳戶，請按一下 [登 **入**]。</span><span class="sxs-lookup"><span data-stu-id="fc107-170">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="fc107-171">登入之後，請選擇訂用帳戶，然後按 **[下一步]**。</span><span class="sxs-lookup"><span data-stu-id="fc107-171">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

<span data-ttu-id="fc107-172">輸入雲端服務的名稱，然後選擇區域。</span><span class="sxs-lookup"><span data-stu-id="fc107-172">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="fc107-173">按一下 [建立]  。</span><span class="sxs-lookup"><span data-stu-id="fc107-173">Click **Create**.</span></span>

![](host-owin-in-an-azure-worker-role/_static/image17.png)

<span data-ttu-id="fc107-174">按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="fc107-174">Click **Publish**.</span></span>

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="fc107-175">[Azure 活動記錄] 視窗會顯示部署的進度。</span><span class="sxs-lookup"><span data-stu-id="fc107-175">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="fc107-176">部署應用程式時，請流覽至 `http://appname.cloudapp.net/` ，其中 *appname* 是您雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc107-176">When the app is deployed, browse to `http://appname.cloudapp.net/`, where *appname* is the name of your cloud service.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc107-177">其他資源</span><span class="sxs-lookup"><span data-stu-id="fc107-177">Additional Resources</span></span>

- [<span data-ttu-id="fc107-178">Katana 專案概觀</span><span class="sxs-lookup"><span data-stu-id="fc107-178">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)
- [<span data-ttu-id="fc107-179">GitHub 上的 Katana 專案</span><span class="sxs-lookup"><span data-stu-id="fc107-179">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana/)
