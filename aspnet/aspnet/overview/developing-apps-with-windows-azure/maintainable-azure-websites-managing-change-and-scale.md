---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 實習實驗室：可維護的 Azure 網站：管理變更和調整規模 |Microsoft Docs
author: rick-anderson
description: 在此實驗室中，您將瞭解 Microsoft Azure 如何讓您輕鬆地建立網站並將其部署到生產環境。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624268"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a><span data-ttu-id="916cd-103">實習實驗室：可維護的 Azure 網站：管理變更和調整規模</span><span class="sxs-lookup"><span data-stu-id="916cd-103">Hands on Lab: Maintainable Azure Websites: Managing Change and Scale</span></span>

<span data-ttu-id="916cd-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="916cd-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="916cd-105">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="916cd-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

> <span data-ttu-id="916cd-106">Microsoft Azure 可讓您輕鬆地建立網站並將其部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-106">Microsoft Azure makes it easy to build and deploy websites to production.</span></span> <span data-ttu-id="916cd-107">但是當您的應用程式上線時，您就剛開始著手！</span><span class="sxs-lookup"><span data-stu-id="916cd-107">But you're not done when your application is live, you're just getting started!</span></span> <span data-ttu-id="916cd-108">您需要處理變更的需求、資料庫更新、規模調整等等。</span><span class="sxs-lookup"><span data-stu-id="916cd-108">You'll need to handle changing requirements, database updates, scale, and more.</span></span> <span data-ttu-id="916cd-109">幸運的是，Azure App Service 已涵蓋在內，有許多功能可協助您讓網站順暢執行。</span><span class="sxs-lookup"><span data-stu-id="916cd-109">Fortunately, Azure App Service has you covered, with plenty of features to help you keep your sites running smoothly.</span></span>
>
> <span data-ttu-id="916cd-110">Azure 為任何大小的 web 應用程式提供安全且彈性的開發、部署和調整選項。</span><span class="sxs-lookup"><span data-stu-id="916cd-110">Azure offers secure and flexible development, deployment and scaling options for any size web application.</span></span> <span data-ttu-id="916cd-111">運用您的現有工具以建立與部署應用程式，省去管理基礎結構的麻煩。</span><span class="sxs-lookup"><span data-stu-id="916cd-111">Leverage your existing tools to create and deploy applications without the hassle of managing infrastructure.</span></span>
>
> <span data-ttu-id="916cd-112">輕鬆部署使用您慣用的開發工具所建立的內容，即可在幾分鐘內自行布建生產 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-112">Provision a production web application yourself in minutes by easily deploying content created using your favorite development tool.</span></span> <span data-ttu-id="916cd-113">您可以直接從原始檔控制部署現有的網站，並支援**Git**、 **GitHub**、 **Bitbucket**、 **TFS**，甚至是**DropBox**。</span><span class="sxs-lookup"><span data-stu-id="916cd-113">You can deploy an existing site directly from source control with support for **Git**, **GitHub**, **Bitbucket**, **TFS**, and even **DropBox**.</span></span> <span data-ttu-id="916cd-114">直接從您最愛的 IDE 或在 Windows 中使用**PowerShell**或在任何 OS 上執行的**CLI**工具部署腳本。</span><span class="sxs-lookup"><span data-stu-id="916cd-114">Deploy directly from your favorite IDE or from scripts using **PowerShell** in Windows or **CLI** tools running on any OS.</span></span> <span data-ttu-id="916cd-115">一旦部署後，您的網站就可以透過持續部署的支援，保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="916cd-115">Once deployed, keep your sites constantly up-to-date with support for continuous deployment.</span></span>
>
> <span data-ttu-id="916cd-116">Azure 為任何資料提供可調式、持久的雲端儲存體、備份和復原解決方案，無論是大型或小型。</span><span class="sxs-lookup"><span data-stu-id="916cd-116">Azure provides scalable, durable cloud storage, backup, and recovery solutions for any data, big or small.</span></span> <span data-ttu-id="916cd-117">將應用程式部署至生產環境時，儲存體服務（例如資料表、Blob 和 SQL 資料庫）可協助您在雲端中調整應用程式的規模。</span><span class="sxs-lookup"><span data-stu-id="916cd-117">When deploying applications to a production environment, storage services such as Tables, Blobs and SQL Databases, help you scale your application in the cloud.</span></span>
>
> <span data-ttu-id="916cd-118">有了 SQL database，在部署新版本的應用程式時，將您的生產力資料庫保持在最新狀態是很重要的。</span><span class="sxs-lookup"><span data-stu-id="916cd-118">With SQL Databases, it is important to keep your productive database up-to-date when deploying new versions of your application.</span></span> <span data-ttu-id="916cd-119">感謝**Entity Framework Code First 移轉**，您的資料模型開發和部署已經過簡化，可以在幾分鐘內更新您的環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-119">Thanks to **Entity Framework Code First Migrations**, the development and deployment of your data model has been simplified to update your environments in minutes.</span></span> <span data-ttu-id="916cd-120">這個實際操作實驗室將會顯示您在 Microsoft Azure 中將 web 應用程式部署至生產環境時，可能會遇到的不同主題。</span><span class="sxs-lookup"><span data-stu-id="916cd-120">This hands-on lab will show you the different topics you could encounter when deploying your web app to production environments in Microsoft Azure.</span></span>
>
> <span data-ttu-id="916cd-121">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="916cd-121">All sample code and snippets are included in the Web Camps Training Kit, available at [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).</span></span>
>
> <span data-ttu-id="916cd-122">如需本主題的深入涵蓋範圍，請參閱[使用 Azure 電子書建立真實世界的雲端應用程式](building-real-world-cloud-apps-with-windows-azure/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="916cd-122">For more in-depth coverage of this topic, see the [Building Real-World Cloud Apps with Azure e-book](building-real-world-cloud-apps-with-windows-azure/introduction.md).</span></span>

<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="916cd-123">概觀</span><span class="sxs-lookup"><span data-stu-id="916cd-123">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="916cd-124">目標</span><span class="sxs-lookup"><span data-stu-id="916cd-124">Objectives</span></span>

<span data-ttu-id="916cd-125">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="916cd-125">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="916cd-126">使用現有的模型啟用 Entity Framework 遷移</span><span class="sxs-lookup"><span data-stu-id="916cd-126">Enable Entity Framework Migrations with an existing model</span></span>
- <span data-ttu-id="916cd-127">使用 Entity Framework 遷移，據以更新物件模型和資料庫</span><span class="sxs-lookup"><span data-stu-id="916cd-127">Update the object model and database accordingly using Entity Framework Migrations</span></span>
- <span data-ttu-id="916cd-128">使用 Git 部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="916cd-128">Deploy to Azure App Service using Git</span></span>
- <span data-ttu-id="916cd-129">使用 Azure 管理入口網站復原到先前的部署</span><span class="sxs-lookup"><span data-stu-id="916cd-129">Rollback to a previous deployment using the Azure Management portal</span></span>
- <span data-ttu-id="916cd-130">使用 Azure 儲存體來調整 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="916cd-130">Use Azure Storage to scale a web app</span></span>
- <span data-ttu-id="916cd-131">使用 Azure 管理入口網站為 web 應用程式設定自動調整</span><span class="sxs-lookup"><span data-stu-id="916cd-131">Configure auto-scaling for a web app using the Azure Management Portal</span></span>
- <span data-ttu-id="916cd-132">在 Visual Studio 中建立和設定負載測試專案</span><span class="sxs-lookup"><span data-stu-id="916cd-132">Create and configure a load test project in Visual Studio</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="916cd-133">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="916cd-133">Prerequisites</span></span>

<span data-ttu-id="916cd-134">若要完成此實際操作實驗室，需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="916cd-134">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="916cd-135">[適用于 Web 或更新版本的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)</span><span class="sxs-lookup"><span data-stu-id="916cd-135">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="916cd-136">Azure SDK for .NET 2。2</span><span class="sxs-lookup"><span data-stu-id="916cd-136">Azure SDK for .NET 2.2</span></span>](https://www.microsoft.com/windowsazure/sdk/)
- [<span data-ttu-id="916cd-137">GIT 版本控制系統</span><span class="sxs-lookup"><span data-stu-id="916cd-137">GIT Version Control System</span></span>](http://git-scm.com/download)
- <span data-ttu-id="916cd-138">Microsoft Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="916cd-138">A Microsoft Azure subscription</span></span>

    - <span data-ttu-id="916cd-139">註冊[免費試用版](https://aka.ms/watk-freetrial)</span><span class="sxs-lookup"><span data-stu-id="916cd-139">Sign up for a [Free Trial](https://aka.ms/watk-freetrial)</span></span>
    - <span data-ttu-id="916cd-140">如果您是 Visual Studio Professional、Test Professional、Premium 或旗艦版的 MSDN 或 MSDN 平臺訂閱者，請立即啟用您的[msdn 權益](https://aka.ms/watk-msdn)，以開始在 Azure 上進行開發和測試</span><span class="sxs-lookup"><span data-stu-id="916cd-140">If you are a Visual Studio Professional, Test Professional, Premium or Ultimate with MSDN or MSDN Platforms subscriber, activate your [MSDN benefit](https://aka.ms/watk-msdn) now to start developing and testing on Azure</span></span>
    - <span data-ttu-id="916cd-141">[BizSpark](https://aka.ms/watk-bizspark)成員會透過其 Visual Studio Ultimate 含 MSDN 訂用帳戶自動獲得 Azure 權益</span><span class="sxs-lookup"><span data-stu-id="916cd-141">[BizSpark](https://aka.ms/watk-bizspark) members automatically receive the Azure benefit through their Visual Studio Ultimate with MSDN subscriptions</span></span>
    - <span data-ttu-id="916cd-142">[Microsoft 合作夥伴網路](https://aka.ms/watk-mpn)Cloud Essentials 方案的成員免費收到每月 Azure 信用額度</span><span class="sxs-lookup"><span data-stu-id="916cd-142">Members of the [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials program receive monthly Azure credits at no charge</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="916cd-143">安裝程式</span><span class="sxs-lookup"><span data-stu-id="916cd-143">Setup</span></span>

<span data-ttu-id="916cd-144">為了在此實際操作實驗室中執行練習，您必須先設定您的環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-144">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="916cd-145">開啟 Windows Explorer 並流覽至實驗室的 [**源**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="916cd-145">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="916cd-146">以滑鼠右鍵按一下**setup.exe** ，然後選取 [以**系統管理員身分執行**] 以啟動安裝程式，以設定您的環境並安裝此實驗室的 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="916cd-146">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="916cd-147">如果顯示 [使用者帳戶控制] 對話方塊，請確認動作以繼續。</span><span class="sxs-lookup"><span data-stu-id="916cd-147">If the User Account Control dialog is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="916cd-148">執行安裝程式之前，請確定您已檢查過此實驗室的所有相依性。</span><span class="sxs-lookup"><span data-stu-id="916cd-148">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="916cd-149">使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="916cd-149">Using the Code Snippets</span></span>

<span data-ttu-id="916cd-150">在整個實驗室檔中，系統會指示您插入程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="916cd-150">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="916cd-151">為了方便起見，大部分的程式碼都是以 Visual Studio Code 程式碼片段的形式提供，您可以從 Visual Studio 2013 內進行存取，以避免必須以手動方式新增。</span><span class="sxs-lookup"><span data-stu-id="916cd-151">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="916cd-152">每個練習都附有一個起始解決方案，此方案位於練習的 [**開始**] 資料夾中，可讓您獨立于其他練習之外進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="916cd-152">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="916cd-153">請注意，在練習期間新增的程式碼片段缺少這些起始的解決方案，而且在您完成練習之前可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="916cd-153">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="916cd-154">在練習的原始程式碼中，您也會找到一個包含 Visual Studio 解決方案的**結束**資料夾，其中含有完成對應練習中步驟所產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-154">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="916cd-155">如果您在進行此實際操作實驗室時需要其他協助，您可以使用這些解決方案做為指導方針。</span><span class="sxs-lookup"><span data-stu-id="916cd-155">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>

---

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="916cd-156">練習</span><span class="sxs-lookup"><span data-stu-id="916cd-156">Exercises</span></span>

<span data-ttu-id="916cd-157">這個實際操作實驗室包含下列練習：</span><span class="sxs-lookup"><span data-stu-id="916cd-157">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="916cd-158">使用 Entity Framework 遷移</span><span class="sxs-lookup"><span data-stu-id="916cd-158">Using Entity Framework Migrations</span></span>](#Exercise1)
2. [<span data-ttu-id="916cd-159">將 Web 應用程式部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="916cd-159">Deploying a Web App to Staging</span></span>](#Exercise2)
3. [<span data-ttu-id="916cd-160">在生產環境中執行部署復原</span><span class="sxs-lookup"><span data-stu-id="916cd-160">Performing Deployment Rollback in Production</span></span>](#Exercise3)
4. [<span data-ttu-id="916cd-161">使用 Azure 儲存體進行調整</span><span class="sxs-lookup"><span data-stu-id="916cd-161">Scaling Using Azure Storage</span></span>](#Exercise4)
5. <span data-ttu-id="916cd-162">[使用 Web Apps 的自動](#Exercise5)調整（適用于 Visual Studio 2013 旗艦版的選擇性）</span><span class="sxs-lookup"><span data-stu-id="916cd-162">[Using Autoscale for Web Apps](#Exercise5) (Optional for Visual Studio 2013 Ultimate edition)</span></span>

<span data-ttu-id="916cd-163">完成此實驗室的預估時間： **75 分鐘**</span><span class="sxs-lookup"><span data-stu-id="916cd-163">Estimated time to complete this lab: **75 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="916cd-164">當您第一次啟動 Visual Studio 時，您必須選取其中一個預先定義的設定集合。</span><span class="sxs-lookup"><span data-stu-id="916cd-164">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="916cd-165">每個預先定義的集合都是設計來符合特定的開發風格，並決定視窗配置、編輯器行為、IntelliSense 程式碼片段和對話方塊選項。</span><span class="sxs-lookup"><span data-stu-id="916cd-165">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="916cd-166">本實驗室中的程式說明在使用 [**一般開發設定**] 集合時，在 Visual Studio 中完成指定工作所需的動作。</span><span class="sxs-lookup"><span data-stu-id="916cd-166">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="916cd-167">如果您針對開發環境選擇不同的 [設定] 集合，您應該考慮的步驟可能會有所差異。</span><span class="sxs-lookup"><span data-stu-id="916cd-167">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a><span data-ttu-id="916cd-168">練習1：使用 Entity Framework 遷移</span><span class="sxs-lookup"><span data-stu-id="916cd-168">Exercise 1: Using Entity Framework Migrations</span></span>

<span data-ttu-id="916cd-169">當您開發應用程式時，您的資料模型可能會隨著時間而改變。</span><span class="sxs-lookup"><span data-stu-id="916cd-169">When you are developing an application, your data model might change over time.</span></span> <span data-ttu-id="916cd-170">這些變更可能會影響資料庫中的現有模型（如果您要建立新版本），而且您必須讓資料庫保持在最新狀態，以避免發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="916cd-170">These changes could affect the existing model in your database (if you are creating a new version) and it is important to keep your database up-to-date to prevent errors.</span></span>

<span data-ttu-id="916cd-171">為了簡化模型中這些變更的追蹤， **Entity Framework Code First 移轉**會自動偵測與資料庫架構比較模型的變更，並產生特定程式碼來更新您的資料庫，並建立新*版本*的資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-171">To simplify the tracking of these changes in your model, **Entity Framework Code First Migrations** automatically detect changes comparing your model with the database schema and generates specific code to update your database, creating new *versions* of your database.</span></span>

<span data-ttu-id="916cd-172">此練習會示範如何為您的應用程式啟用**遷移**，以及如何輕鬆地偵測並產生變更以更新您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-172">This exercise shows you how to enable **Migrations** for your application and how you can easily detect and generate changes to update your databases.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a><span data-ttu-id="916cd-173">工作1–啟用遷移</span><span class="sxs-lookup"><span data-stu-id="916cd-173">Task 1 – Enabling Migrations</span></span>

<span data-ttu-id="916cd-174">在這項工作中，您將逐步完成啟用**萬能技客測驗**資料庫**Entity Framework Code First 移轉**、變更模型及瞭解這些變更反映在資料庫中的步驟。</span><span class="sxs-lookup"><span data-stu-id="916cd-174">In this task, you will go through the steps of enabling **Entity Framework Code First Migrations** to the **Geek Quiz** database, changing the model and understanding how those changes are reflected in the database.</span></span>

1. <span data-ttu-id="916cd-175">開啟 Visual Studio，然後從**Source\Ex1-UsingEntityFrameworkMigrations\Begin**開啟**GeekQuiz**方案檔。</span><span class="sxs-lookup"><span data-stu-id="916cd-175">Open Visual Studio and open the **GeekQuiz.sln** solution file from **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.</span></span>
2. <span data-ttu-id="916cd-176">建立解決方案，以便下載並安裝**NuGet**套件相依性。</span><span class="sxs-lookup"><span data-stu-id="916cd-176">Build the solution in order to download and install the **NuGet** package dependencies.</span></span> <span data-ttu-id="916cd-177">若要這樣做，請以滑鼠右鍵按一下方案，然後按一下 [**建立方案**] 或按**Ctrl + Shift + B**。</span><span class="sxs-lookup"><span data-stu-id="916cd-177">To do this, right-click the solution and click **Build Solution** or press **Ctrl + Shift + B**.</span></span>
3. <span data-ttu-id="916cd-178">從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-178">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="916cd-179">在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-179">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="916cd-180">將會建立以現有模型為基礎的初始遷移。</span><span class="sxs-lookup"><span data-stu-id="916cd-180">An initial migration based on the existing model will be created.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    <span data-ttu-id="916cd-181">![啟用遷移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "啟用移轉")</span><span class="sxs-lookup"><span data-stu-id="916cd-181">![Enabling Migrations](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Enabling Migrations")</span></span>

    <span data-ttu-id="916cd-182">*啟用遷移*</span><span class="sxs-lookup"><span data-stu-id="916cd-182">*Enabling Migrations*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-183">此命令會將 [**遷移**] 資料夾新增至萬能技客測驗專案，其中包含名為**Configuration.cs**的檔案。</span><span class="sxs-lookup"><span data-stu-id="916cd-183">This command adds a **Migrations** folder to Geek Quiz project that contains a file called **Configuration.cs**.</span></span> <span data-ttu-id="916cd-184">**Configuration**類別可讓您設定遷移如何針對您的內容運作。</span><span class="sxs-lookup"><span data-stu-id="916cd-184">The **Configuration** class allows you to configure how Migrations behaves for your context.</span></span>
5. <span data-ttu-id="916cd-185">啟用遷移之後，您必須更新**設定類別，** 以在資料庫中填入**萬能技客測驗**所需的初始資料。</span><span class="sxs-lookup"><span data-stu-id="916cd-185">With Migrations enabled, you need to update the **Configuration** class to populate the database with the initial data that **Geek Quiz** requires.</span></span> <span data-ttu-id="916cd-186">在 [**遷移**] 底下，以位於此實驗室的 [ **Source\Assets** ] 資料夾中的檔案取代**Configuration.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="916cd-186">Under **Migrations**, replace the **Configuration.cs** file with the one located in the **Source\Assets** folder of this lab.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-187">由於**遷移**將會在每次資料庫更新時呼叫**種子**方法，因此您必須確定資料庫中的記錄不會重複。</span><span class="sxs-lookup"><span data-stu-id="916cd-187">Since **Migrations** will call the **Seed** method with every database update, you need to be sure that records are not duplicated in the database.</span></span> <span data-ttu-id="916cd-188">**AddOrUpdate**方法將有助於防止重複的資料。</span><span class="sxs-lookup"><span data-stu-id="916cd-188">The **AddOrUpdate** method will help to prevent duplicate data.</span></span>
6. <span data-ttu-id="916cd-189">若要新增初始遷移，請輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-189">To add an initial migration, enter the following command and then press **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-190">請確定您的 LocalDB 實例中沒有名為 &quot;GeekQuizProd&quot; 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-190">Make sure that there is no database named &quot;GeekQuizProd&quot; in your LocalDB instance.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    <span data-ttu-id="916cd-191">![新增基底架構遷移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "新增基底架構遷移")</span><span class="sxs-lookup"><span data-stu-id="916cd-191">![Adding base schema migration](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Adding base schema migration")</span></span>

    <span data-ttu-id="916cd-192">*新增基底架構遷移*</span><span class="sxs-lookup"><span data-stu-id="916cd-192">*Adding base schema migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-193">「**新增-遷移**」會根據您在上次建立遷移之後對模型所做的變更，scaffold 下一次遷移。</span><span class="sxs-lookup"><span data-stu-id="916cd-193">**Add-Migration** will scaffold the next migration based on changes you have made to your model since the last migration was created.</span></span> <span data-ttu-id="916cd-194">在此情況下，因為它是第一次的專案遷移，所以它會加入腳本來建立**TriviaCoNtext**類別中定義的所有資料表。</span><span class="sxs-lookup"><span data-stu-id="916cd-194">In this case, as it is the first migration of the project, it will add the scripts to create all the tables defined in the **TriviaContext** class.</span></span>
7. <span data-ttu-id="916cd-195">執行下列命令來執行遷移以更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-195">Execute the migration to update the database by running the following command.</span></span> <span data-ttu-id="916cd-196">針對此命令，您將指定**Verbose**旗標，以查看要套用至目標資料庫的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="916cd-196">For this command you will specify the **Verbose** flag to view the SQL statements being applied to the target database.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    <span data-ttu-id="916cd-197">![正在建立初始資料庫](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "正在建立初始資料庫")</span><span class="sxs-lookup"><span data-stu-id="916cd-197">![Creating initial database](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Creating initial database")</span></span>

    <span data-ttu-id="916cd-198">*正在建立初始資料庫*</span><span class="sxs-lookup"><span data-stu-id="916cd-198">*Creating initial database*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-199">**更新-資料庫**會將任何暫止的遷移套用至資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-199">**Update-Database** will apply any pending migrations to the database.</span></span> <span data-ttu-id="916cd-200">在此情況下，它會使用您的 web.config 檔案中定義的連接字串來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-200">In this case, it will create the database using the connection string defined in your web.config file.</span></span>
8. <span data-ttu-id="916cd-201">移至 [**流覽**] 功能表，然後開啟 [ **SQL Server 物件總管**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-201">Go to **View** menu and open **SQL Server Object Explorer**.</span></span>

    <span data-ttu-id="916cd-202">![在 SQL Server 物件總管中開啟](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 物件總管中開啟")</span><span class="sxs-lookup"><span data-stu-id="916cd-202">![Open in SQL Server Object Explorer](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Open in SQL Server Object Explorer")</span></span>

    <span data-ttu-id="916cd-203">*在 SQL Server 物件總管中開啟*</span><span class="sxs-lookup"><span data-stu-id="916cd-203">*Open in SQL Server Object Explorer*</span></span>
9. <span data-ttu-id="916cd-204">在 [ **SQL Server 物件總管**] 視窗中，以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後選取 [**新增 SQL Server ...** ] 選項，以連接到您的 LocalDB 實例。</span><span class="sxs-lookup"><span data-stu-id="916cd-204">In the **SQL Server Object Explorer** window, connect to your LocalDB instance by right-clicking the **SQL Server** node and selecting **Add SQL Server...** option.</span></span>

    <span data-ttu-id="916cd-205">![加入 SQL Server 實例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "加入 SQL Server 實例")</span><span class="sxs-lookup"><span data-stu-id="916cd-205">![Adding a SQL Server Instance](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Adding a SQL Server Instance")</span></span>

    <span data-ttu-id="916cd-206">*將 SQL Server 實例新增至 SQL Server 物件總管*</span><span class="sxs-lookup"><span data-stu-id="916cd-206">*Adding a SQL Server instance to SQL Server Object Explorer*</span></span>
10. <span data-ttu-id="916cd-207">將 [**伺服器名稱**] 設定為 *（localdb） \v11.0* ，並將 [ **Windows 驗證**] 保留為您的驗證模式。</span><span class="sxs-lookup"><span data-stu-id="916cd-207">Set the **server name** to *(localdb)\v11.0* and leave **Windows Authentication** as your authentication mode.</span></span> <span data-ttu-id="916cd-208">按一下 [連接] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="916cd-208">Click **Connect** to continue.</span></span>

    <span data-ttu-id="916cd-209">![連接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "連接到 LocalDB")</span><span class="sxs-lookup"><span data-stu-id="916cd-209">![Connecting to LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Connecting to LocalDB")</span></span>

    <span data-ttu-id="916cd-210">*連接到 LocalDB*</span><span class="sxs-lookup"><span data-stu-id="916cd-210">*Connecting to LocalDB*</span></span>
11. <span data-ttu-id="916cd-211">開啟 [ **GeekQuizProd** ] 資料庫，然後展開 [**資料表]** 節點。</span><span class="sxs-lookup"><span data-stu-id="916cd-211">Open the **GeekQuizProd** database and expand the **Tables** node.</span></span> <span data-ttu-id="916cd-212">如您所見，**更新資料庫**命令會產生**TriviaCoNtext**類別中定義的所有資料表。</span><span class="sxs-lookup"><span data-stu-id="916cd-212">As you can see, the **Update-Database** command generated all the tables defined in the **TriviaContext** class.</span></span> <span data-ttu-id="916cd-213">找出**dbo。TriviaQuestions**資料表並開啟 [資料行] 節點。</span><span class="sxs-lookup"><span data-stu-id="916cd-213">Locate the **dbo.TriviaQuestions** table and open the columns node.</span></span> <span data-ttu-id="916cd-214">在下一個工作中，您會在此資料表中加入新的資料行，並使用**遷移**來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-214">In the next task, you will add a new column to this table and update the database using **Migrations**.</span></span>

    <span data-ttu-id="916cd-215">![邏輯問題資料行](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "邏輯問題資料行")</span><span class="sxs-lookup"><span data-stu-id="916cd-215">![Trivia Questions Columns](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Trivia Questions Columns")</span></span>

    <span data-ttu-id="916cd-216">*邏輯問題資料行*</span><span class="sxs-lookup"><span data-stu-id="916cd-216">*Trivia Questions Columns*</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a><span data-ttu-id="916cd-217">工作2–使用遷移更新資料庫架構</span><span class="sxs-lookup"><span data-stu-id="916cd-217">Task 2 – Updating Database Schema Using Migrations</span></span>

<span data-ttu-id="916cd-218">在這項工作中，您將使用**Entity Framework Code First 移轉**來偵測模型中的變更，並產生必要的程式碼來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-218">In this task, you will use **Entity Framework Code First Migrations** to detect a change in your model and generate the necessary code to update the database.</span></span> <span data-ttu-id="916cd-219">您將會藉由在其中加入新的屬性來更新**TriviaQuestions**實體。</span><span class="sxs-lookup"><span data-stu-id="916cd-219">You will update the **TriviaQuestions** entity by adding a new property to it.</span></span> <span data-ttu-id="916cd-220">接著，您將執行命令來建立新的遷移，以在資料表中包含新的資料行。</span><span class="sxs-lookup"><span data-stu-id="916cd-220">Then you will run commands to create a new Migration to include the new column in the table.</span></span>

1. <span data-ttu-id="916cd-221">在**方案總管**中，按兩下位於 [**模型**] 資料夾內的**TriviaQuestion.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="916cd-221">In **Solution Explorer**, double-click the **TriviaQuestion.cs** file located inside the **Models** folder.</span></span>
2. <span data-ttu-id="916cd-222">新增名為 [**提示**] 的新屬性，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="916cd-222">Add a new property named **Hint**, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. <span data-ttu-id="916cd-223">在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-223">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span> <span data-ttu-id="916cd-224">將會建立新的遷移，反映模型中的變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-224">A new migration will be created reflecting the change in our model.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    <span data-ttu-id="916cd-225">![新增-遷移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "新增-遷移")</span><span class="sxs-lookup"><span data-stu-id="916cd-225">![Add-Migration](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Add-Migration")</span></span>

    <span data-ttu-id="916cd-226">*新增-遷移*</span><span class="sxs-lookup"><span data-stu-id="916cd-226">*Add-Migration*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-227">遷移檔案是由兩個**向上**和**向下**的方法所組成。</span><span class="sxs-lookup"><span data-stu-id="916cd-227">A Migration file is composed of two methods, **Up** and **Down**.</span></span>
    >
    > - <span data-ttu-id="916cd-228">**Up**方法將用來指定要將應用程式的目前版本套用至資料庫所需的變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-228">The **Up** method will be used to specify what changes the current version of our application need to apply to the database.</span></span>
    > - <span data-ttu-id="916cd-229">**向下鍵**會用來反轉我們已新增至**Up**方法的變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-229">The **Down** is used to reverse the changes we have added to the **Up** method.</span></span>
    >
    > <span data-ttu-id="916cd-230">當資料庫移轉更新資料庫時，它會以時間戳記循序執行所有的遷移，而且只有自上次更新後尚未使用的所有遷移（\_MigrationHistory 表會持續追蹤已套用的遷移）。</span><span class="sxs-lookup"><span data-stu-id="916cd-230">When the Database Migration updates the database, it will run all migrations in the timestamp order, and only those that have not been used since the last update (The \_MigrationHistory table keeps track of which migrations have been applied).</span></span> <span data-ttu-id="916cd-231">所有遷移的**Up**方法都會被呼叫，並會進行已指定到資料庫的變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-231">The **Up** method of all migrations will be called and will make the changes we have specified to the database.</span></span> <span data-ttu-id="916cd-232">如果我們決定回到先前的遷移，將會呼叫**向下**方法來以相反順序重做變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-232">If we decide to go back to a previous migration, the **Down** method will be called to redo the changes in a reverse order.</span></span>
4. <span data-ttu-id="916cd-233">在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-233">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. <span data-ttu-id="916cd-234">**更新資料庫**命令的輸出會產生**Alter Table** SQL 語句，以將新的資料行加入至**TriviaQuestions**資料表，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="916cd-234">The output of the **Update-Database** command generated an **Alter Table** SQL statement to add a new column to the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="916cd-235">![已產生新增資料行 SQL 語句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "已產生新增資料行 SQL 語句")</span><span class="sxs-lookup"><span data-stu-id="916cd-235">![Add column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Add column SQL statement generated")</span></span>

    <span data-ttu-id="916cd-236">*已產生新增資料行 SQL 語句*</span><span class="sxs-lookup"><span data-stu-id="916cd-236">*Add column SQL statement generated*</span></span>
6. <span data-ttu-id="916cd-237">在**SQL Server 物件總管**中，重新整理**dbo。TriviaQuestions**資料表，並檢查是否顯示新的 [**提示**] 資料行。</span><span class="sxs-lookup"><span data-stu-id="916cd-237">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the new **Hint** column is displayed.</span></span>

    <span data-ttu-id="916cd-238">![顯示新的提示資料行](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "顯示新的提示資料行")</span><span class="sxs-lookup"><span data-stu-id="916cd-238">![Showing the new Hint Column](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Showing the new Hint Column")</span></span>

    <span data-ttu-id="916cd-239">*顯示新的提示資料行*</span><span class="sxs-lookup"><span data-stu-id="916cd-239">*Showing the new Hint Column*</span></span>
7. <span data-ttu-id="916cd-240">回到 [ **TriviaQuestion.cs**編輯器] 中，將**StringLength**條件約束加入至 [*提示*] 屬性，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="916cd-240">Back in the **TriviaQuestion.cs** editor, add a **StringLength** constraint to the *Hint* property, as shown in the following code snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. <span data-ttu-id="916cd-241">在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-241">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. <span data-ttu-id="916cd-242">在 [**套件管理員主控台**] 中，輸入下列命令，然後按**enter**。</span><span class="sxs-lookup"><span data-stu-id="916cd-242">In the **Package Manager Console**, enter the following command and then press **Enter**.</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. <span data-ttu-id="916cd-243">**更新資料庫**命令的輸出產生了**Alter Table** SQL 語句來更新**TriviaQuestions**資料表的*提示*資料行類型，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="916cd-243">The output of the **Update-Database** command generated an **Alter Table** SQL statement to update the *hint* column type of the **TriviaQuestions** table, as shown in the image below.</span></span>

    <span data-ttu-id="916cd-244">![已產生 Alter column SQL 語句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "已產生 Alter column SQL 語句")</span><span class="sxs-lookup"><span data-stu-id="916cd-244">![Alter column SQL statement generated](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL statement generated")</span></span>

    <span data-ttu-id="916cd-245">*已產生 Alter column SQL 語句*</span><span class="sxs-lookup"><span data-stu-id="916cd-245">*Alter column SQL statement generated*</span></span>
11. <span data-ttu-id="916cd-246">在**SQL Server 物件總管**中，重新整理**dbo。TriviaQuestions**資料表，並檢查 [**提示**] 資料行類型是否為 **[Nvarchar （150）** ]。</span><span class="sxs-lookup"><span data-stu-id="916cd-246">In **SQL Server Object Explorer**, refresh the **dbo.TriviaQuestions** table and check that the **Hint** column type is **nvarchar(150)**.</span></span>

    <span data-ttu-id="916cd-247">![顯示新的條件約束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "顯示新的條件約束")</span><span class="sxs-lookup"><span data-stu-id="916cd-247">![Showing the new constraint](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Showing the new constraint")</span></span>

    <span data-ttu-id="916cd-248">*顯示新的條件約束*</span><span class="sxs-lookup"><span data-stu-id="916cd-248">*Showing the new constraint*</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a><span data-ttu-id="916cd-249">練習2：將 Web 應用程式部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="916cd-249">Exercise 2: Deploying a Web App to Staging</span></span>

<span data-ttu-id="916cd-250">**Azure App Service 中的 Web Apps**可讓您執行分段發行。</span><span class="sxs-lookup"><span data-stu-id="916cd-250">**Web Apps in Azure App Service** enables you to perform staged publishing.</span></span> <span data-ttu-id="916cd-251">預備發行會為每個預設生產網站建立一個預備網站位置，並讓您在不停機時間的情況下交換這些插槽。</span><span class="sxs-lookup"><span data-stu-id="916cd-251">Staged publishing creates a staging site slot for each default production site and enables you to swap these slots with no down time.</span></span> <span data-ttu-id="916cd-252">這在發行至公用、以累加方式整合網站內容之前驗證變更，以及如果變更未如預期般運作時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="916cd-252">This is really useful to validate changes before releasing to the public, incrementally integrate site content, and roll back if changes are not working as expected.</span></span>

<span data-ttu-id="916cd-253">在此練習中，您會使用 Git 原始檔控制，將**萬能技客測驗**應用程式部署至 web 應用程式的預備環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-253">In this exercise, you will deploy the **Geek Quiz** application to the staging environment of your web app using Git source control.</span></span> <span data-ttu-id="916cd-254">若要這麼做，您將建立 web 應用程式並在管理入口網站布建必要的元件、設定**Git**存放庫，並將應用程式原始程式碼從本機電腦推送至預備位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-254">To do this, you will create the web app and provision the required components at the management portal, configure a **Git** repository and push the application source code from your local computer to the staging slot.</span></span> <span data-ttu-id="916cd-255">您也會使用您在上一個練習中建立的**Code First 移轉**來更新生產資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-255">You will also update your production database with the **Code First Migrations** you created in the previous exercise.</span></span> <span data-ttu-id="916cd-256">接著，您會在此測試環境中執行應用程式，以確認其作業是否正常。</span><span class="sxs-lookup"><span data-stu-id="916cd-256">You will then execute the application in this test environment to verify its operation.</span></span> <span data-ttu-id="916cd-257">一旦您滿意它是根據您的預期運作，就會將應用程式升階到生產環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-257">Once you are satisfied that it is working according to your expectations, you will promote the application to production.</span></span>

> [!NOTE]
> <span data-ttu-id="916cd-258">若要啟用分段發行，web 應用程式必須處於**標準模式**。</span><span class="sxs-lookup"><span data-stu-id="916cd-258">To enable staged publishing, the web app must be in **Standard mode**.</span></span> <span data-ttu-id="916cd-259">請注意，如果您將 web 應用程式變更為標準模式，將會產生額外的費用。</span><span class="sxs-lookup"><span data-stu-id="916cd-259">Note that additional charges will be incurred if you change your web app to Standard mode.</span></span> <span data-ttu-id="916cd-260">如需價格的詳細資訊，請參閱[App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="916cd-260">For more information about pricing, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a><span data-ttu-id="916cd-261">工作1–在 Azure App Service 中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="916cd-261">Task 1 – Creating a Web App in Azure App Service</span></span>

<span data-ttu-id="916cd-262">在這項工作中，您將會從管理入口網站的**Azure App Service**建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-262">In this task, you will create a web app in **Azure App Service** from the management portal.</span></span> <span data-ttu-id="916cd-263">您也會設定**SQL Database**來保存應用程式資料，以及設定原始檔控制的本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-263">You will also configure a **SQL Database** to persist the application data, and configure a local Git repository for source control.</span></span>

1. <span data-ttu-id="916cd-264">前往[Azure 管理入口網站](https://manage.windowsazure.com)，並使用與您的訂用帳戶相關聯的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-264">Go to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>

    ![登入 Azure 管理入口網站](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    <span data-ttu-id="916cd-266">*登入 Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="916cd-266">*Sign in to the Azure management portal*</span></span>
2. <span data-ttu-id="916cd-267">在頁面底部的命令列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-267">Click **New** in the command bar at the bottom of the page.</span></span>

    <span data-ttu-id="916cd-268">![建立新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "建立新的 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="916cd-268">![Creating a new web app](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Creating a new web app")</span></span>

    <span data-ttu-id="916cd-269">*建立新的 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-269">*Creating a new web app*</span></span>
3. <span data-ttu-id="916cd-270">依序按一下 [**計算**]、[**網站**] 和 [**自訂建立**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-270">Click **Compute**, **Website** and then **Custom Create**.</span></span>

    <span data-ttu-id="916cd-271">![使用自訂建立建立新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "使用自訂建立建立新的 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="916cd-271">![Creating a new web app using Custom Create](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Creating a new web app using Custom Create")</span></span>

    <span data-ttu-id="916cd-272">*使用自訂建立建立新的 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-272">*Creating a new web app using Custom Create*</span></span>
4. <span data-ttu-id="916cd-273">在 [**新增網站-自訂建立**] 對話方塊中，提供可用的**URL** （例如*萬能技客-測驗*），在 [**區域**] 下拉式清單中選取一個位置，然後在 [**資料庫**] 下拉式清單中選取 [**建立新的 SQL database** ]。</span><span class="sxs-lookup"><span data-stu-id="916cd-273">In the **New Website - Custom Create** dialog box, provide an available **URL** (e.g. *geek-quiz*), select a location in the **Region** drop-down list, and select **Create a new SQL database** in the **Database** drop-down list.</span></span> <span data-ttu-id="916cd-274">最後，選取 [**從原始檔控制發行**] 核取方塊，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-274">Finally, select the **Publish from source control** check box and click **Next**.</span></span>

    ![自訂新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    <span data-ttu-id="916cd-276">*自訂新的 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-276">*Customizing the new web app*</span></span>
5. <span data-ttu-id="916cd-277">指定資料庫設定的下列資訊：</span><span class="sxs-lookup"><span data-stu-id="916cd-277">Specify the following information for the database settings:</span></span>

   - <span data-ttu-id="916cd-278">在 [**名稱**] 文字方塊中，輸入資料庫名稱（例如， *geekquiz\_db*）</span><span class="sxs-lookup"><span data-stu-id="916cd-278">In the **Name** text box, enter a database name (e.g. *geekquiz\_db*)</span></span>
   - <span data-ttu-id="916cd-279">在 [伺服器]**下拉式**清單中，選取 [**新增 SQL database 伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-279">In the Server **drop-down** list, select **New SQL database server**.</span></span> <span data-ttu-id="916cd-280">或者，您也可以選取現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="916cd-280">Alternatively, you can select an existing server.</span></span>
   - <span data-ttu-id="916cd-281">在 [**資料庫使用者名稱**] 和 [**資料庫密碼**] 方塊中，輸入 SQL Database 伺服器的系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-281">In the **Database username** and **Database password** boxes, enter the administrator username and password for the SQL database server.</span></span> <span data-ttu-id="916cd-282">如果您選取已建立的伺服器，系統會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-282">If you select a server you have already created, you will be prompted for the password.</span></span>

     ![指定資料庫設定](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     <span data-ttu-id="916cd-284">*指定資料庫設定*</span><span class="sxs-lookup"><span data-stu-id="916cd-284">*Specifying the database settings*</span></span>
6. <span data-ttu-id="916cd-285">按 [下一步] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="916cd-285">Click **Next** to continue.</span></span>
7. <span data-ttu-id="916cd-286">選取要使用之原始檔控制的**本機 Git 存放庫**，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-286">Select **Local Git repository** for the source control to use and click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-287">系統可能會提示您輸入部署認證（使用者名稱和密碼）。</span><span class="sxs-lookup"><span data-stu-id="916cd-287">You may be prompted for the deployment credentials (a username and password).</span></span>

    ![建立 Git 存放庫](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    <span data-ttu-id="916cd-289">*建立 Git 存放庫*</span><span class="sxs-lookup"><span data-stu-id="916cd-289">*Creating the Git repository*</span></span>
8. <span data-ttu-id="916cd-290">等候新的 web 應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="916cd-290">Wait until the new web app is created.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-291">根據預設，Azure 會在*azurewebsites.net*提供網域，但也可讓您使用 Azure 管理入口網站來設定自訂網域。</span><span class="sxs-lookup"><span data-stu-id="916cd-291">By default, Azure provides domains at *azurewebsites.net* but also gives you the possibility to set custom domains using the Azure management portal.</span></span> <span data-ttu-id="916cd-292">不過，如果您使用特定的 Azure App Service 模式，則只能管理自訂網域。</span><span class="sxs-lookup"><span data-stu-id="916cd-292">However, you can only manage custom domains if you are using certain Azure App Service modes.</span></span>
    >
    > <span data-ttu-id="916cd-293">Azure App Service 在免費、共用、基本、標準和 Premium 版本中都有提供。</span><span class="sxs-lookup"><span data-stu-id="916cd-293">Azure App Service is available in Free, Shared, Basic, Standard, and Premium editions.</span></span> <span data-ttu-id="916cd-294">在 [免費] 和 [共用] 模式中，所有 web 應用程式會在多租使用者環境中執行，並具有 CPU、記憶體和網路使用量的配額。</span><span class="sxs-lookup"><span data-stu-id="916cd-294">In Free and Shared mode, all web apps run in a multi-tenant environment and have quotas for CPU, Memory, and Network usage.</span></span> <span data-ttu-id="916cd-295">免費應用程式的最大數目可能會隨著您的方案而有所不同。</span><span class="sxs-lookup"><span data-stu-id="916cd-295">The maximum number of free apps may vary with your plan.</span></span> <span data-ttu-id="916cd-296">在標準模式中，您可以選擇哪些應用程式會在對應至標準 Azure 計算資源的專用虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="916cd-296">In Standard mode, you choose which apps run on dedicated virtual machines that correspond to the standard Azure compute resources.</span></span> <span data-ttu-id="916cd-297">您可以在 web 應用程式的 [**調整**] 功能表中找到 web 應用程式模式設定。</span><span class="sxs-lookup"><span data-stu-id="916cd-297">You can find the web app mode configuration in the **Scale** menu of your web app.</span></span>
    >
    > <span data-ttu-id="916cd-298">![Azure App Service 模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 模式")</span><span class="sxs-lookup"><span data-stu-id="916cd-298">![Azure App Service Modes](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service Modes")</span></span>
    >
    > <span data-ttu-id="916cd-299">如果您使用 [**共用**] 或 [**標準**] 模式，您將可以前往應用程式的 [**設定**] 功能表，然後按一下 [*功能變數名稱*] 底下的 [**管理網域**]，來管理 web 應用程式的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="916cd-299">If you are using **Shared** or **Standard** mode, you will be able to manage custom domains for your web app by going to your app's **Configure** menu and clicking **Manage Domains** under *domain names*.</span></span>
    >
    > <span data-ttu-id="916cd-300">![管理網域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理網域")</span><span class="sxs-lookup"><span data-stu-id="916cd-300">![Manage Domains](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Manage Domains")</span></span>
    >
    > <span data-ttu-id="916cd-301">![管理自訂網域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自訂網域")</span><span class="sxs-lookup"><span data-stu-id="916cd-301">![Manage Custom Domains](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Manage Custom Domains")</span></span>
9. <span data-ttu-id="916cd-302">建立 web 應用程式之後，請按一下 [ **URL** ] 資料行下方的連結，以檢查新的 web 應用程式是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="916cd-302">Once the web app is created, click the link under the **URL** column to check that the new web app is running.</span></span>

    ![流覽至新的 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    <span data-ttu-id="916cd-304">*流覽至新的 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-304">*Browsing to the new web app*</span></span>

    ![web 應用程式正在執行](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    <span data-ttu-id="916cd-306">*web 應用程式正在執行*</span><span class="sxs-lookup"><span data-stu-id="916cd-306">*web app running*</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a><span data-ttu-id="916cd-307">工作2–建立生產 SQL Database</span><span class="sxs-lookup"><span data-stu-id="916cd-307">Task 2 – Creating the Production SQL Database</span></span>

<span data-ttu-id="916cd-308">在這項工作中，您將使用**Entity Framework Code First 移轉**建立以您在上一個工作中建立的**Azure SQL Database**實例為目標的資料庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-308">In this task, you will use the **Entity Framework Code First Migrations** to create the database targeting the **Azure SQL Database** instance you created in the previous task.</span></span>

1. <span data-ttu-id="916cd-309">在 管理入口網站中，流覽至您在上一個工作中建立的 web 應用程式，並移至其**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="916cd-309">In the Management Portal, navigate to the web app you created in the previous task and go to its **Dashboard**.</span></span>
2. <span data-ttu-id="916cd-310">在 [**儀表板**] 頁面中，按一下 [**快速概覽**] 區段底下的 [**查看連接字串**] 連結。</span><span class="sxs-lookup"><span data-stu-id="916cd-310">In the **Dashboard** page, click **View connection strings** link under the **quick glance** section.</span></span>

    <span data-ttu-id="916cd-311">![查看連接字串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看連接字串")</span><span class="sxs-lookup"><span data-stu-id="916cd-311">![View connection strings](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "View connection strings")</span></span>

    <span data-ttu-id="916cd-312">*查看連接字串*</span><span class="sxs-lookup"><span data-stu-id="916cd-312">*View connection strings*</span></span>
3. <span data-ttu-id="916cd-313">複製 [**連接字串**] 值，然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="916cd-313">Copy the **connection string** value and close the dialog box.</span></span>

    <span data-ttu-id="916cd-314">![Azure 管理入口網站中的連接字串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理入口網站中的連接字串")</span><span class="sxs-lookup"><span data-stu-id="916cd-314">![Connection String in Azure Management Portal](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Connection String in Azure Management Portal")</span></span>

    <span data-ttu-id="916cd-315">*Azure 管理入口網站中的連接字串*</span><span class="sxs-lookup"><span data-stu-id="916cd-315">*Connection String in Azure Management Portal*</span></span>
4. <span data-ttu-id="916cd-316">按一下 **[Sql 資料庫**] 以查看 Azure 中的 sql 資料庫清單</span><span class="sxs-lookup"><span data-stu-id="916cd-316">Click **SQL Databases** to see the list of SQL databases in Azure</span></span>

    <span data-ttu-id="916cd-317">![SQL Database 功能表](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 功能表")</span><span class="sxs-lookup"><span data-stu-id="916cd-317">![SQL Database menu](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database menu")</span></span>

    <span data-ttu-id="916cd-318">*SQL Database 功能表*</span><span class="sxs-lookup"><span data-stu-id="916cd-318">*SQL Database menu*</span></span>
5. <span data-ttu-id="916cd-319">找出您在上一項工作中建立的資料庫，然後按一下伺服器。</span><span class="sxs-lookup"><span data-stu-id="916cd-319">Locate the database you created in the previous task and click on the Server.</span></span>

    <span data-ttu-id="916cd-320">![SQL Database 伺服器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 伺服器")</span><span class="sxs-lookup"><span data-stu-id="916cd-320">![SQL Database server](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database server")</span></span>

    <span data-ttu-id="916cd-321">*SQL Database 伺服器*</span><span class="sxs-lookup"><span data-stu-id="916cd-321">*SQL Database server*</span></span>
6. <span data-ttu-id="916cd-322">在伺服器的 [**快速入門**] 頁面中，按一下 [**設定**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-322">In the **Quick Start** page of the server, click on **Configure**.</span></span>

    <span data-ttu-id="916cd-323">![[設定] 功能表](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "[設定] 功能表")</span><span class="sxs-lookup"><span data-stu-id="916cd-323">![Configure menu](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Configure menu")</span></span>

    <span data-ttu-id="916cd-324">*[設定] 功能表*</span><span class="sxs-lookup"><span data-stu-id="916cd-324">*Configure menu*</span></span>
7. <span data-ttu-id="916cd-325">在 [**允許的 ip 位址**] 區段中，按一下 **[新增至允許的 ip 位址**] 連結，讓您的 ip 連線至 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="916cd-325">In the **Allowed IP addresses** section, click on **Add to the allowed IP addresses** link to enable your IP to connect to the SQL Database server.</span></span>

    <span data-ttu-id="916cd-326">![允許的 IP 位址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允許的 IP 位址")</span><span class="sxs-lookup"><span data-stu-id="916cd-326">![Allowed IP addresses](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Allowed IP addresses")</span></span>

    <span data-ttu-id="916cd-327">*允許的 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="916cd-327">*Allowed IP addresses*</span></span>
8. <span data-ttu-id="916cd-328">按一下頁面底部的 [儲存] 以完成此步驟。</span><span class="sxs-lookup"><span data-stu-id="916cd-328">Click **Save** at the bottom of the page to complete the step.</span></span>
9. <span data-ttu-id="916cd-329">切換回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="916cd-329">Switch back to Visual Studio.</span></span>
10. <span data-ttu-id="916cd-330">在 [**套件管理員主控台**] 中，執行下列命令，以您從 Azure 複製的連接字串取代 *[您的連接字串]* 預留位置</span><span class="sxs-lookup"><span data-stu-id="916cd-330">In the **Package Manager Console**, execute the following command replacing *[YOUR-CONNECTION-STRING]* placeholder with the connection string you copied from Azure</span></span>

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    <span data-ttu-id="916cd-331">![更新以 Windows 為目標的資料庫 Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "更新以 Windows 為目標的資料庫 Azure SQL Database")</span><span class="sxs-lookup"><span data-stu-id="916cd-331">![Update database targeting Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Update database targeting Windows Azure SQL Database")</span></span>

    <span data-ttu-id="916cd-332">*更新資料庫目標 Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="916cd-332">*Update database targeting Azure SQL Database*</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a><span data-ttu-id="916cd-333">工作 3-使用 Git 將萬能技客測驗部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="916cd-333">Task 3 – Deploying Geek Quiz to Staging Using Git</span></span>

<span data-ttu-id="916cd-334">在這項工作中，您會在 web 應用程式中啟用分段發行。</span><span class="sxs-lookup"><span data-stu-id="916cd-334">In this task, you will enable staged publishing in your web app.</span></span> <span data-ttu-id="916cd-335">然後，您將使用 Git，直接從您的本機電腦將萬能技客測驗應用程式發佈到 web 應用程式的預備環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-335">Then, you will use Git to publish the Geek Quiz application directly from your local computer to the staging environment of your web app.</span></span>

1. <span data-ttu-id="916cd-336">返回入口網站，然後按一下 [**名稱**] 欄底下的 web 應用程式名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-336">Go back to the portal and click the name of the web app under the **Name** column to display the management pages.</span></span>

    ![開啟 web 應用程式管理頁面](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    <span data-ttu-id="916cd-338">*開啟 web 應用程式管理頁面*</span><span class="sxs-lookup"><span data-stu-id="916cd-338">*Opening the web app management pages*</span></span>
2. <span data-ttu-id="916cd-339">流覽至 [**調整**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-339">Navigate to the **Scale** page.</span></span> <span data-ttu-id="916cd-340">在 [**一般**] 區段下，針對設定選取 [**標準**]，然後按一下命令列中的 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-340">Under the **general** section, select **Standard** for the configuration and click **Save** in the command bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-341">若要以**標準**模式執行目前區域和訂用帳戶中的所有 web 應用程式，請保留 [**選擇網站**設定] 中的 [**全**選] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="916cd-341">To run all web apps in the current region and subscription in **Standard** mode, leave the **Select All** check box selected in the **Choose Sites** configuration.</span></span> <span data-ttu-id="916cd-342">否則，請清除 [**全選**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="916cd-342">Otherwise, clear the **Select All** check box.</span></span>

    <span data-ttu-id="916cd-343">![將 web 應用程式升級至標準模式](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "將 web 應用程式升級至標準模式")</span><span class="sxs-lookup"><span data-stu-id="916cd-343">![Upgrading the web app to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrading the web app to Standard mode")</span></span>

    <span data-ttu-id="916cd-344">*將 Web 應用程式升級至標準模式*</span><span class="sxs-lookup"><span data-stu-id="916cd-344">*Upgrading the Web App to Standard mode*</span></span>
3. <span data-ttu-id="916cd-345">按一下 **[是]** 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-345">Click **Yes** to confirm the changes.</span></span>

    <span data-ttu-id="916cd-346">![確認變更為標準模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "繼續變更 web 應用程式模式")</span><span class="sxs-lookup"><span data-stu-id="916cd-346">![Confirming the change to Standard mode](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Continuing with the changing of the web app mode")</span></span>

    <span data-ttu-id="916cd-347">*確認變更為標準模式*</span><span class="sxs-lookup"><span data-stu-id="916cd-347">*Confirming the change to Standard mode*</span></span>
4. <span data-ttu-id="916cd-348">移至 [**儀表板**] 頁面，然後按一下 [**快速概覽**] 區段下的 [**啟用分段發行**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-348">Go to the **Dashboard** page and click **Enable staged publishing** under the **quick glance** section.</span></span>

    <span data-ttu-id="916cd-349">![啟用分段發行](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "啟用分段發行")</span><span class="sxs-lookup"><span data-stu-id="916cd-349">![Enabling staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Enabling staged publishing")</span></span>

    <span data-ttu-id="916cd-350">*啟用分段發行*</span><span class="sxs-lookup"><span data-stu-id="916cd-350">*Enabling staged publishing*</span></span>
5. <span data-ttu-id="916cd-351">按一下 **[是]** 啟用分段發行。</span><span class="sxs-lookup"><span data-stu-id="916cd-351">Click **Yes** to enable staged publishing.</span></span>

    <span data-ttu-id="916cd-352">![確認分段發行](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "按一下 [是] 啟用分段發行")</span><span class="sxs-lookup"><span data-stu-id="916cd-352">![Confirming staged publishing](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Clicking Yes to enable staged publishing")</span></span>

    <span data-ttu-id="916cd-353">*確認分段發行*</span><span class="sxs-lookup"><span data-stu-id="916cd-353">*Confirming staged publishing*</span></span>
6. <span data-ttu-id="916cd-354">在 web 應用程式清單中，展開 web 應用程式名稱左側的標記，以顯示預備網站位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-354">In the list of web apps, expand the mark to the left of your web app name to display the staging site slot.</span></span> <span data-ttu-id="916cd-355">它具有您的 web 應用程式名稱，後面接著 ***（暫存）***。</span><span class="sxs-lookup"><span data-stu-id="916cd-355">It has the name of your web app followed by ***(staging)***.</span></span> <span data-ttu-id="916cd-356">按一下預備網站以移至 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-356">Click the staging site to go to the management page.</span></span>

    <span data-ttu-id="916cd-357">![流覽至預備 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "流覽至預備 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="916cd-357">![Navigating to the staging web app](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigating to the staging web app")</span></span>

    <span data-ttu-id="916cd-358">*流覽至預備應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-358">*Navigating to the staging app*</span></span>
7. <span data-ttu-id="916cd-359">請注意，他的管理頁面看起來就像任何其他 web 應用程式的管理頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-359">Notice that he management page looks like any other web app's management page.</span></span> <span data-ttu-id="916cd-360">流覽至 [**部署**] 頁面，並複製 [ **Git URL** ] 值。</span><span class="sxs-lookup"><span data-stu-id="916cd-360">Navigate to the **Deployments** page and copy the **Git URL** value.</span></span> <span data-ttu-id="916cd-361">稍後在本練習中將會用到它。</span><span class="sxs-lookup"><span data-stu-id="916cd-361">You will use it later in this exercise.</span></span>

    ![複製 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    <span data-ttu-id="916cd-363">*複製 Git URL 值*</span><span class="sxs-lookup"><span data-stu-id="916cd-363">*Copying the Git URL value*</span></span>
8. <span data-ttu-id="916cd-364">開啟新的**Git Bash**主控台，並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="916cd-364">Open a new **Git Bash** console and execute the following commands.</span></span> <span data-ttu-id="916cd-365">以此實驗室的**Source\Ex1-DeployingWebSiteToStaging\Begin**資料夾中**GeekQuiz**解決方案的路徑，更新 *[您的應用程式-路徑]* 預留位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-365">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution, located in the **Source\Ex1-DeployingWebSiteToStaging\Begin** folder of this lab.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和第一次認可](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    <span data-ttu-id="916cd-367">*Git 初始化和第一次認可*</span><span class="sxs-lookup"><span data-stu-id="916cd-367">*Git initialization and first commit*</span></span>
9. <span data-ttu-id="916cd-368">執行下列命令，將您的 web 應用程式推送至遠端**Git**存放庫。</span><span class="sxs-lookup"><span data-stu-id="916cd-368">Run the following command to push your web app to the remote **Git** repository.</span></span> <span data-ttu-id="916cd-369">將預留位置取代為您從管理入口網站取得的 URL。</span><span class="sxs-lookup"><span data-stu-id="916cd-369">Replace the placeholder with the URL you obtained from the management portal.</span></span> <span data-ttu-id="916cd-370">系統會提示您輸入您的部署密碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-370">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![推送至 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    <span data-ttu-id="916cd-372">*推送至 Azure*</span><span class="sxs-lookup"><span data-stu-id="916cd-372">*Pushing to Azure*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-373">當您將內容部署至 web 應用程式的 FTP 主機或 GIT 存放庫時，必須使用您從 web 應用程式的 [**快速入門**] 或 [**儀表板**] 管理頁面建立的**部署**認證來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="916cd-373">When you deploy content to the FTP host or GIT repository of a web app, you must authenticate using the **deployment credentials** that you created from the web app's **Quick Start** or **Dashboard** management pages.</span></span> <span data-ttu-id="916cd-374">如果您不知道您的部署認證，可以使用入口網站輕鬆地將其重設。</span><span class="sxs-lookup"><span data-stu-id="916cd-374">If you do not know your deployment credentials you can easily reset them using the management portal.</span></span> <span data-ttu-id="916cd-375">開啟 web 應用程式的 [**儀表板**] 頁面，然後按一下 [**重設您的部署認證**] 連結。</span><span class="sxs-lookup"><span data-stu-id="916cd-375">Open the web app **Dashboard** page and click the **Reset your deployment credentials** link.</span></span> <span data-ttu-id="916cd-376">提供新密碼，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-376">Provide a new password and click **OK**.</span></span> <span data-ttu-id="916cd-377">部署認證適用于與您的訂用帳戶相關聯的所有 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-377">Deployment credentials are valid for use with all web apps associated with your subscription.</span></span>
10. <span data-ttu-id="916cd-378">若要確認 web 應用程式已成功推送至 Azure，請回到入口網站，然後按一下 [**網站**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-378">In order to verify the web app was successfully pushed to Azure, go back to the management portal and click **Websites**.</span></span>
11. <span data-ttu-id="916cd-379">找出您的 web 應用程式，並展開該專案以顯示預備網站位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-379">Locate your web app and expand the entry to display the staging site slot.</span></span> <span data-ttu-id="916cd-380">按一下其**名稱**，以移至 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-380">Click its **Name** to go to the management page.</span></span>
12. <span data-ttu-id="916cd-381">按一下 [**部署**] 以查看**部署歷程記錄**。</span><span class="sxs-lookup"><span data-stu-id="916cd-381">Click **Deployments** to see the **deployment history**.</span></span> <span data-ttu-id="916cd-382">確認有使用中的**部署**與您的 *&quot;初始認可&quot;* 。</span><span class="sxs-lookup"><span data-stu-id="916cd-382">Verify that there is an **Active Deployment** with your *&quot;Initial Commit&quot;*.</span></span>

    ![作用中的部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    <span data-ttu-id="916cd-384">*作用中的部署*</span><span class="sxs-lookup"><span data-stu-id="916cd-384">*Active deployment*</span></span>
13. <span data-ttu-id="916cd-385">最後，按一下命令列中的 **[流覽]** 以移至 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-385">Finally, click **Browse** in the command bar to go to the web app.</span></span>

    ![流覽 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    <span data-ttu-id="916cd-387">*流覽 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-387">*Browse web app*</span></span>
14. <span data-ttu-id="916cd-388">如果已成功部署應用程式，您會看到萬能技客測驗登入頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-388">If the application is successfully deployed, you will see the Geek Quiz login page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-389">已部署應用程式的位址 URL 包含您的 web 應用程式名稱，後面接著 *-預備*。</span><span class="sxs-lookup"><span data-stu-id="916cd-389">The address URL of the deployed application contains the name of your web app followed by *-staging*.</span></span>

    ![在預備環境中執行的應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    <span data-ttu-id="916cd-391">*在預備環境中執行的應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-391">*Application running in the staging environment*</span></span>
15. <span data-ttu-id="916cd-392">如果您想要探索應用程式，請按一下 [**註冊**] 來註冊新的使用者。</span><span class="sxs-lookup"><span data-stu-id="916cd-392">If you wish to explore the application, click **Register** to register a new user.</span></span> <span data-ttu-id="916cd-393">輸入使用者名稱、電子郵件地址和密碼，以完成帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="916cd-393">Complete the account details by entering a user name, email address and password.</span></span> <span data-ttu-id="916cd-394">接下來，應用程式會顯示測驗的第一個問題。</span><span class="sxs-lookup"><span data-stu-id="916cd-394">Next, the application shows the first question of the quiz.</span></span> <span data-ttu-id="916cd-395">請回答幾個問題，確定它如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="916cd-395">Answer a few questions to make sure it is working as expected.</span></span>

    ![已備妥可供使用的應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    <span data-ttu-id="916cd-397">*已備妥可供使用的應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-397">*Application ready to be used*</span></span>

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a><span data-ttu-id="916cd-398">工作 4-將 Web 應用程式升級至生產環境</span><span class="sxs-lookup"><span data-stu-id="916cd-398">Task 4 – Promoting the Web App to Production</span></span>

<span data-ttu-id="916cd-399">現在您已確認 web 應用程式在預備環境中正常運作，您已準備好將它升級至生產環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-399">Now that you have verified that the web app is working correctly in the staging environment, you are ready to promote it to production.</span></span> <span data-ttu-id="916cd-400">在這項工作中，您會將預備網站位置與生產網站位置交換。</span><span class="sxs-lookup"><span data-stu-id="916cd-400">In this task, you will swap the staging site slot with the production site slot.</span></span>

1. <span data-ttu-id="916cd-401">返回入口網站，然後選取 [預備網站] 位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-401">Go back to the management portal and select the staging site slot.</span></span> <span data-ttu-id="916cd-402">按一下命令列中的 [**交換**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-402">Click **Swap** in the command bar.</span></span>

    ![交換至生產環境](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    <span data-ttu-id="916cd-404">*交換至生產環境*</span><span class="sxs-lookup"><span data-stu-id="916cd-404">*Swap to production*</span></span>
2. <span data-ttu-id="916cd-405">在確認對話方塊中按一下 **[是]** ，繼續進行交換操作。</span><span class="sxs-lookup"><span data-stu-id="916cd-405">Click **Yes** in the confirmation dialog box to proceed with the swap operation.</span></span> <span data-ttu-id="916cd-406">Azure 會立即將生產網站的內容與預備網站的內容交換。</span><span class="sxs-lookup"><span data-stu-id="916cd-406">Azure will immediately swap the content of the production site with the content of the staging site.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-407">預備版本的某些設定會自動複製到實際執行版本（例如連接字串覆寫、處理常式對應等），但其他設定不會變更（例如 DNS 端點、SSL 系結等）。</span><span class="sxs-lookup"><span data-stu-id="916cd-407">Some settings from the staged version will automatically be copied to the production version (e.g. connection string overrides, handler mappings, etc.) but other settings will not change (e.g. DNS endpoints, SSL bindings, etc.).</span></span>

    ![正在確認交換操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    <span data-ttu-id="916cd-409">*正在確認交換操作*</span><span class="sxs-lookup"><span data-stu-id="916cd-409">*Confirming swap operation*</span></span>
3. <span data-ttu-id="916cd-410">一旦交換完成，請選取生產位置，然後按一下命令列中的 **[流覽]** 以開啟生產網站。</span><span class="sxs-lookup"><span data-stu-id="916cd-410">Once the swap is complete, select the production slot and click **Browse** in the command bar to open the production site.</span></span> <span data-ttu-id="916cd-411">請注意網址列中的 URL。</span><span class="sxs-lookup"><span data-stu-id="916cd-411">Notice the URL in the address bar.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-412">您可能需要重新整理瀏覽器以清除快取。</span><span class="sxs-lookup"><span data-stu-id="916cd-412">You might need to refresh your browser to clear cache.</span></span> <span data-ttu-id="916cd-413">在 Internet Explorer 中，您可以按下**CTRL + R**來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="916cd-413">In Internet Explorer, you can do this by pressing **CTRL+R**.</span></span>

    ![在生產環境中執行的 Web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. <span data-ttu-id="916cd-415">在**GitBash**主控台中，將本機 Git 存放庫的遠端 URL 更新為目標為生產位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-415">In the **GitBash** console, update the remote URL for the local Git repository to target the production slot.</span></span> <span data-ttu-id="916cd-416">若要執行這項操作，請執行下列命令，將預留位置取代為您的部署使用者名稱和 web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="916cd-416">To do this, run the following command replacing the placeholders with your deployment username and the name of your web app.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-417">在下列練習中，您會將變更推送至生產網站，而不是暫存，只是為了實驗室的簡單性。</span><span class="sxs-lookup"><span data-stu-id="916cd-417">In the following exercises, you will push changes to the production site instead of staging just for the simplicity of the lab.</span></span> <span data-ttu-id="916cd-418">在真實世界的案例中，建議您先確認預備環境中的變更，再升級至生產環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-418">In a real-world scenario, it is recommended to verify the changes in the staging environment before promoting to production.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a><span data-ttu-id="916cd-419">練習3：在生產環境中執行部署復原</span><span class="sxs-lookup"><span data-stu-id="916cd-419">Exercise 3: Performing Deployment Rollback in Production</span></span>

<span data-ttu-id="916cd-420">在某些情況下，您沒有預備位置可在預備與生產環境之間執行熱交換，例如，如果您使用的是**免費**或**共用**模式。</span><span class="sxs-lookup"><span data-stu-id="916cd-420">There are scenarios where you do not have a staging slot to perform hot swap between staging and production, for example, if you are working with **Free** or **Shared** mode.</span></span> <span data-ttu-id="916cd-421">在這些情況下，您應該在測試環境（本機或遠端網站）中測試您的應用程式，然後再部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="916cd-421">In those scenarios, you should test your application in a testing environment –either locally or in a remote site– before deploying to production.</span></span> <span data-ttu-id="916cd-422">不過，在測試階段期間未偵測到的問題可能會在生產網站中發生。</span><span class="sxs-lookup"><span data-stu-id="916cd-422">However, it is possible that an issue not detected during the testing phase may arise in the production site.</span></span> <span data-ttu-id="916cd-423">在此情況下，請務必讓機制輕鬆地儘快切換至先前和更穩定的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="916cd-423">In this case, it is important to have a mechanism to easily switch to a previous and more stable version of the application as quickly as possible.</span></span>

<span data-ttu-id="916cd-424">在**Azure App Service**中，從原始檔控制進行連續部署，可能會因為管理入口網站中提供的重新**部署**動作而產生這種情況。</span><span class="sxs-lookup"><span data-stu-id="916cd-424">In **Azure App Service**, continuous deployment from source control makes this possible thanks to the **redeploy** action available in the management portal.</span></span> <span data-ttu-id="916cd-425">Azure 會持續追蹤與推送至存放庫的認可相關聯的部署，並提供選項讓您隨時使用任何先前的部署重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-425">Azure keeps track of the deployments associated with the commits pushed to the repository and provides an option to redeploy your application using any of your previous deployments, at any time.</span></span>

<span data-ttu-id="916cd-426">在此練習中，您將對**萬能技客測驗**應用程式中刻意插入*bug*的程式碼進行變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-426">In this exercise you will perform a change to the code in the **Geek Quiz** application that intentionally injects a *bug*.</span></span> <span data-ttu-id="916cd-427">您會將應用程式部署至生產環境以查看錯誤，然後您將會利用重新部署功能來回到先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="916cd-427">You will deploy the application to production to see the error, and then you will take advantage of the redeploy feature to go back to the previous state.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a><span data-ttu-id="916cd-428">工作1–更新萬能技客測驗應用程式</span><span class="sxs-lookup"><span data-stu-id="916cd-428">Task 1 – Updating the Geek Quiz Application</span></span>

<span data-ttu-id="916cd-429">在這項工作中，您將重構**TriviaController**類別的一小段程式碼，將從資料庫中取出所選測驗選項的部分，解壓縮到新的方法中。</span><span class="sxs-lookup"><span data-stu-id="916cd-429">In this task, you will refactor a small piece of code of the **TriviaController** class to extract part of the logic that retrieves the selected quiz option from the database into a new method.</span></span>

1. <span data-ttu-id="916cd-430">使用上一個練習中的**GeekQuiz**解決方案，切換到 Visual Studio 實例。</span><span class="sxs-lookup"><span data-stu-id="916cd-430">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="916cd-431">在**方案總管**中，開啟 [**控制器**] 資料夾內的**TriviaController.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="916cd-431">In **Solution Explorer**, open the **TriviaController.cs** file inside the **Controllers** folder.</span></span>
3. <span data-ttu-id="916cd-432">找出**StoreAsync**方法，並選取下圖中反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-432">Locate the **StoreAsync** method and select the code highlighted in the following figure.</span></span>

    ![選取程式碼](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    <span data-ttu-id="916cd-434">*選取程式碼*</span><span class="sxs-lookup"><span data-stu-id="916cd-434">*Selecting the code*</span></span>
4. <span data-ttu-id="916cd-435">以滑鼠右鍵按一下選取的程式碼，展開 [**重構**] 功能表，然後選取 [**解壓縮方法**...]。</span><span class="sxs-lookup"><span data-stu-id="916cd-435">Right-click the selected code, expand the **Refactor** menu and select **Extract Method...**.</span></span>

    ![將程式碼解壓縮為新方法](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    <span data-ttu-id="916cd-437">*選取 [解壓縮方法]*</span><span class="sxs-lookup"><span data-stu-id="916cd-437">*Selecting Extract Method*</span></span>
5. <span data-ttu-id="916cd-438">在 [**解壓縮方法**] 對話方塊中，將新的方法命名為*MatchesOption* ，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-438">In the **Extract Method** dialog box, name the new method *MatchesOption* and click **OK**.</span></span>

    ![指定方法名稱](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    <span data-ttu-id="916cd-440">*指定已解壓縮方法的名稱*</span><span class="sxs-lookup"><span data-stu-id="916cd-440">*Specifying the name for the extracted method*</span></span>
6. <span data-ttu-id="916cd-441">然後會將選取的程式碼解壓縮至**MatchesOption**方法。</span><span class="sxs-lookup"><span data-stu-id="916cd-441">The selected code is then extracted into the **MatchesOption** method.</span></span> <span data-ttu-id="916cd-442">產生的程式碼會顯示在下列程式碼片段中。</span><span class="sxs-lookup"><span data-stu-id="916cd-442">The resulting code is shown in the following snippet.</span></span>

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. <span data-ttu-id="916cd-443">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-443">Press **CTRL + S** to save the changes.</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a><span data-ttu-id="916cd-444">工作 2-重新部署萬能技客測驗應用程式</span><span class="sxs-lookup"><span data-stu-id="916cd-444">Task 2 – Redeploying the Geek Quiz Application</span></span>

<span data-ttu-id="916cd-445">您現在會將您在上一個工作中所做的變更推送至存放庫，這會觸發生產環境的新部署。</span><span class="sxs-lookup"><span data-stu-id="916cd-445">You will now push the changes you made in the previous task to the repository, which will trigger a new deployment to the production environment.</span></span> <span data-ttu-id="916cd-446">接著，您將使用 Internet Explorer 提供的**F12 開發工具**來疑難排解問題，然後從 Azure 管理入口網站執行復原至先前的部署。</span><span class="sxs-lookup"><span data-stu-id="916cd-446">Then, you will troubleshot an issue using the **F12 development tools** provided by Internet Explorer, and then perform a rollback to the previous deployment from the Azure management portal.</span></span>

1. <span data-ttu-id="916cd-447">開啟新的**Git Bash**主控台，將更新過的應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="916cd-447">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
2. <span data-ttu-id="916cd-448">執行下列命令，將變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="916cd-448">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="916cd-449">以**GeekQuiz**方案的路徑更新 *[您的應用程式-路徑]* 預留位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-449">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="916cd-450">系統會提示您輸入您的部署密碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-450">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![將重構的程式碼推送至 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    <span data-ttu-id="916cd-452">*將重構的程式碼推送至 Azure*</span><span class="sxs-lookup"><span data-stu-id="916cd-452">*Pushing refactored code to Azure*</span></span>
3. <span data-ttu-id="916cd-453">開啟 Internet Explorer 並流覽至您的 web 應用程式（例如 `http://<your-web-site>.azurewebsites.net`）。</span><span class="sxs-lookup"><span data-stu-id="916cd-453">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="916cd-454">使用先前建立的認證登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-454">Log in using the previously created credentials.</span></span>
4. <span data-ttu-id="916cd-455">按**F12**啟動開發工具，選取 [**網路**] 索引標籤，然後按一下 [**播放**] 按鈕以開始錄製。</span><span class="sxs-lookup"><span data-stu-id="916cd-455">Press **F12** to launch the development tools, select the **Network** tab and click the **Play** button to start recording.</span></span>

    <span data-ttu-id="916cd-456">![正在啟動網路錄製](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "正在啟動網路錄製")</span><span class="sxs-lookup"><span data-stu-id="916cd-456">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Starting network recording")</span></span>

    <span data-ttu-id="916cd-457">*正在啟動網路錄製*</span><span class="sxs-lookup"><span data-stu-id="916cd-457">*Starting network recording*</span></span>
5. <span data-ttu-id="916cd-458">選取測驗的任何選項。</span><span class="sxs-lookup"><span data-stu-id="916cd-458">Select any option of the quiz.</span></span> <span data-ttu-id="916cd-459">您會看到不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="916cd-459">You will see that nothing happens.</span></span>
6. <span data-ttu-id="916cd-460">在**F12**視窗中，與 POST HTTP 要求對應的專案會顯示 HTTP **500**結果。</span><span class="sxs-lookup"><span data-stu-id="916cd-460">In the **F12** window, the entry corresponding to the POST HTTP request shows an HTTP **500** result.</span></span>

    ![HTTP 500 錯誤](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    <span data-ttu-id="916cd-462">*HTTP 500 錯誤*</span><span class="sxs-lookup"><span data-stu-id="916cd-462">*HTTP 500 error*</span></span>
7. <span data-ttu-id="916cd-463">選取 [**主控台**] 索引標籤。會記錄錯誤的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="916cd-463">Select the **Console** tab. An error is logged with the details of the cause.</span></span>

    ![記錄的錯誤](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    <span data-ttu-id="916cd-465">*記錄的錯誤*</span><span class="sxs-lookup"><span data-stu-id="916cd-465">*Logged error*</span></span>
8. <span data-ttu-id="916cd-466">找出錯誤的詳細資料部分。</span><span class="sxs-lookup"><span data-stu-id="916cd-466">Locate the details part of the error.</span></span> <span data-ttu-id="916cd-467">很明顯地，此錯誤是由您在先前步驟中認可的程式碼重構所造成。</span><span class="sxs-lookup"><span data-stu-id="916cd-467">Clearly, this error is caused by the code refactoring you committed in the previous steps.</span></span>

    <span data-ttu-id="916cd-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`</span><span class="sxs-lookup"><span data-stu-id="916cd-468">`Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.</span></span>
9. <span data-ttu-id="916cd-469">請勿關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="916cd-469">Do not close the browser.</span></span>
10. <span data-ttu-id="916cd-470">在新的瀏覽器實例中，流覽至[Azure 管理入口網站](https://manage.windowsazure.com)，然後使用與您的訂用帳戶相關聯的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-470">In a new browser instance, navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
11. <span data-ttu-id="916cd-471">選取 [**網站**]，然後按一下您在練習2中建立的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-471">Select **Websites** and click the web app you created in Exercise 2.</span></span>
12. <span data-ttu-id="916cd-472">流覽至 [**部署**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-472">Navigate to the **Deployments** page.</span></span> <span data-ttu-id="916cd-473">請注意，所有執行的認可都會列在部署歷程記錄中。</span><span class="sxs-lookup"><span data-stu-id="916cd-473">Notice that all the commits performed are listed in the deployment history.</span></span>

    ![現有部署的清單](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    <span data-ttu-id="916cd-475">*現有部署的清單*</span><span class="sxs-lookup"><span data-stu-id="916cd-475">*List of existing deployments*</span></span>
13. <span data-ttu-id="916cd-476">選取先前的認可，然後按一下命令列上的 [重新**部署**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-476">Select the previous commit and click **Redeploy** on the command bar.</span></span>

    ![重新部署先前的認可](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    <span data-ttu-id="916cd-478">*重新部署先前的認可*</span><span class="sxs-lookup"><span data-stu-id="916cd-478">*Redeploying the previous commit*</span></span>
14. <span data-ttu-id="916cd-479">在系統提示您確認時，按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-479">When prompted to confirm, click **Yes**.</span></span>

    ![確認重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. <span data-ttu-id="916cd-481">當部署完成時，使用您的 web 應用程式切換回瀏覽器實例，然後按下**CTRL + F5**。</span><span class="sxs-lookup"><span data-stu-id="916cd-481">When the deployment completes, switch back to the browser instance with your web app and press **CTRL + F5**.</span></span>
16. <span data-ttu-id="916cd-482">按一下任何一個選項。</span><span class="sxs-lookup"><span data-stu-id="916cd-482">Click any of the options.</span></span> <span data-ttu-id="916cd-483">現在會進行翻轉動畫，並顯示結果（*正確/不正確*）。</span><span class="sxs-lookup"><span data-stu-id="916cd-483">The flip animation will now take place and the result (*correct/incorrect*) will be displayed.</span></span>
17. <span data-ttu-id="916cd-484">選擇性切換至**Git Bash**主控台並執行下列命令，以還原為先前的認可。</span><span class="sxs-lookup"><span data-stu-id="916cd-484">(Optional) Switch to the **Git Bash** console and execute the following commands to revert to the previous commit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-485">這些命令會建立新的認可，以復原在錯誤認可中所做的 Git 儲存機制中的所有變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-485">These commands create a new commit that undoes all changes in the Git repository that were made in the bad commit.</span></span> <span data-ttu-id="916cd-486">然後，Azure 會使用新的認可來重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-486">Azure will then redeploy the application using the new commit.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a><span data-ttu-id="916cd-487">練習4：使用 Azure 儲存體進行調整</span><span class="sxs-lookup"><span data-stu-id="916cd-487">Exercise 4: Scaling Using Azure Storage</span></span>

<span data-ttu-id="916cd-488">**Blob**是儲存大量非結構化文字或二進位資料（例如影片、音訊和影像）的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="916cd-488">**Blobs** are the simplest way to store large amounts of unstructured text or binary data such as video, audio and images.</span></span> <span data-ttu-id="916cd-489">將應用程式的靜態內容移至儲存體，可透過將影像或檔直接提供給瀏覽器，協助調整您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-489">Moving the static content of your application to Storage, helps to scale your application by serving images or documents directly to the browser.</span></span>

<span data-ttu-id="916cd-490">在此練習中，您會將應用程式的靜態內容移至 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="916cd-490">In this exercise, you will move the static content of your application to a Blob container.</span></span> <span data-ttu-id="916cd-491">然後，您會將應用程式設定為**在 web.config 中**新增**ASP.NET URL 重寫規則**，以將您的內容重新導向至 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="916cd-491">Then you will configure your application to add an **ASP.NET URL rewrite rule** in the **Web.config** to redirect your content to the Blob container.</span></span>

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a><span data-ttu-id="916cd-492">工作1–建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="916cd-492">Task 1 – Creating an Azure Storage Account</span></span>

<span data-ttu-id="916cd-493">在這項工作中，您將瞭解如何使用入口網站來建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="916cd-493">In this task you will learn how to create a new storage account using the management portal.</span></span>

1. <span data-ttu-id="916cd-494">流覽至[Azure 管理入口網站](https://manage.windowsazure.com)，並使用與您的訂用帳戶相關聯的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-494">Navigate to the [Azure management portal](https://manage.windowsazure.com) and sign in using the Microsoft account associated with your subscription.</span></span>
2. <span data-ttu-id="916cd-495">選取 [**新增] |資料服務 |儲存體 |[快速建立**] 以開始建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="916cd-495">Select **New | Data Services | Storage | Quick Create** to start creating a new storage account.</span></span> <span data-ttu-id="916cd-496">輸入帳戶的唯一名稱，並從清單中選取一個**區域**。</span><span class="sxs-lookup"><span data-stu-id="916cd-496">Enter a unique name for the account and select a **Region** from the list.</span></span> <span data-ttu-id="916cd-497">按一下 [**建立儲存體帳戶**] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="916cd-497">Click **Create Storage Account** to continue.</span></span>

    <span data-ttu-id="916cd-498">![建立新的儲存體帳戶](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "建立新的儲存體帳戶")</span><span class="sxs-lookup"><span data-stu-id="916cd-498">![Creating a new Storage Account](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Creating a new Storage Account")</span></span>

    <span data-ttu-id="916cd-499">*建立新的儲存體帳戶*</span><span class="sxs-lookup"><span data-stu-id="916cd-499">*Creating a new storage account*</span></span>
3. <span data-ttu-id="916cd-500">在 [**儲存體**] 區段中，等候新儲存體帳戶的狀態變更為 [*線上*]，才能繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="916cd-500">In the **Storage** section, wait until the status of the new storage account changes to *Online* in order to continue with the following step.</span></span>

    <span data-ttu-id="916cd-501">![已建立儲存體帳戶](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "已建立儲存體帳戶")</span><span class="sxs-lookup"><span data-stu-id="916cd-501">![Storage Account created](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Storage Account created")</span></span>

    <span data-ttu-id="916cd-502">*已建立儲存體帳戶*</span><span class="sxs-lookup"><span data-stu-id="916cd-502">*Storage Account created*</span></span>
4. <span data-ttu-id="916cd-503">按一下儲存體帳戶名稱，然後按一下頁面頂端的 [**儀表板**] 連結。</span><span class="sxs-lookup"><span data-stu-id="916cd-503">Click on the storage account name and then click the **Dashboard** link at the top of the page.</span></span> <span data-ttu-id="916cd-504">[**儀表板**] 頁面會提供帳戶狀態的相關資訊，以及可在應用程式中使用的服務端點。</span><span class="sxs-lookup"><span data-stu-id="916cd-504">The **Dashboard** page provides you with information about the status of the account and the service endpoints that can be used within your applications.</span></span>

    <span data-ttu-id="916cd-505">![顯示儲存體帳戶儀表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "顯示儲存體帳戶儀表板")</span><span class="sxs-lookup"><span data-stu-id="916cd-505">![Displaying the Storage Account Dashboard](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Displaying the Storage Account Dashboard")</span></span>

    <span data-ttu-id="916cd-506">*顯示儲存體帳戶儀表板*</span><span class="sxs-lookup"><span data-stu-id="916cd-506">*Displaying the Storage Account Dashboard*</span></span>
5. <span data-ttu-id="916cd-507">按一下巡覽列中的 [**管理存取金鑰**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="916cd-507">Click the **Manage Access Keys** button in the navigation bar.</span></span>

    <span data-ttu-id="916cd-508">![[管理存取金鑰] 按鈕](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "[管理存取金鑰] 按鈕")</span><span class="sxs-lookup"><span data-stu-id="916cd-508">![Manage Access Keys button](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Manage Access Keys button")</span></span>

    <span data-ttu-id="916cd-509">*[管理存取金鑰] 按鈕*</span><span class="sxs-lookup"><span data-stu-id="916cd-509">*Manage Access Keys button*</span></span>
6. <span data-ttu-id="916cd-510">在 [**管理存取金鑰**] 對話方塊中，複製 [**儲存體帳戶名稱**] 和 [**主要存取金鑰**]，因為您在下列練習中將會用到它們。</span><span class="sxs-lookup"><span data-stu-id="916cd-510">In the **Manage Access Keys** dialog box, copy the **Storage Account Name** and **Primary Access Key** as you will need them in the following exercise.</span></span> <span data-ttu-id="916cd-511">然後關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="916cd-511">Then, close the dialog box.</span></span>

    <span data-ttu-id="916cd-512">![[管理存取金鑰] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "[管理存取金鑰] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="916cd-512">![Manage Access Key dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Manage Access Key dialog box")</span></span>

    <span data-ttu-id="916cd-513">*[管理存取金鑰] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="916cd-513">*Manage Access Key dialog box*</span></span>

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a><span data-ttu-id="916cd-514">工作 2-將資產上傳至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="916cd-514">Task 2 – Uploading an Asset to Azure Blob Storage</span></span>

<span data-ttu-id="916cd-515">在這項工作中，您將使用 Visual Studio 的 [伺服器總管] 視窗連接到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="916cd-515">In this task, you will use the Server Explorer window from Visual Studio to connect to your storage account.</span></span> <span data-ttu-id="916cd-516">接著，您將建立 blob 容器，並將具有萬能技客測驗標誌的檔案上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="916cd-516">You will then create a blob container and upload a file with the Geek Quiz logo to the container.</span></span>

1. <span data-ttu-id="916cd-517">使用上一個練習中的**GeekQuiz**解決方案，切換到 Visual Studio 實例。</span><span class="sxs-lookup"><span data-stu-id="916cd-517">Switch to the Visual Studio instance with the **GeekQuiz** solution from the previous exercise.</span></span>
2. <span data-ttu-id="916cd-518">從功能表列中選取 [ **View** ]，然後按一下 [**伺服器總管**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-518">From the menu bar, select **View** and then click **Server Explorer**.</span></span>
3. <span data-ttu-id="916cd-519">在**伺服器總管**中，以滑鼠右鍵按一下 [ **Azure** ] 節點，然後選取 **[連線到 azure ...]** 。使用與您的訂用帳戶相關聯的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-519">In **Server Explorer**, right-click the **Azure** node and select **Connect to Azure...**. Sign in using the Microsoft account associated with your subscription.</span></span>

    ![連接至 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    <span data-ttu-id="916cd-521">*連接到 Azure*</span><span class="sxs-lookup"><span data-stu-id="916cd-521">*Connect to Azure*</span></span>
4. <span data-ttu-id="916cd-522">展開 [ **Azure** ] 節點，以滑鼠右鍵按一下 [**儲存體**]，然後選取 [**附加外部儲存體**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-522">Expand the **Azure** node, right-click **Storage** and select **Attach External Storage...**.</span></span>
5. <span data-ttu-id="916cd-523">在 [**加入新的儲存體帳戶**] 對話方塊中，輸入您在上一個工作中取得的**帳戶名稱**和**帳戶金鑰**，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-523">In the **Add New Storage Account** dialog box, enter the **Account name** and **Account key** you obtained in the previous task and click **OK**.</span></span>

    ![[新增儲存體帳戶] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    <span data-ttu-id="916cd-525">*[新增儲存體帳戶] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="916cd-525">*Add New Storage Account dialog box*</span></span>
6. <span data-ttu-id="916cd-526">您的儲存體帳戶應該會出現在 [**儲存體**] 節點底下。</span><span class="sxs-lookup"><span data-stu-id="916cd-526">Your storage account should appear under the **Storage** node.</span></span> <span data-ttu-id="916cd-527">展開您的儲存體帳戶，以滑鼠右鍵按一下 [ **blob** ]，然後選取 [**建立 Blob 容器**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-527">Expand your storage account, right-click **Blobs** and select **Create Blob Container...**.</span></span>

    <span data-ttu-id="916cd-528">![建立 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "建立 Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="916cd-528">![Create Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Create Blob Container")</span></span>

    <span data-ttu-id="916cd-529">*建立 Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="916cd-529">*Create Blob Container*</span></span>
7. <span data-ttu-id="916cd-530">在 [**建立 Blob 容器**] 對話方塊中，輸入 Blob 容器的名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-530">In the **Create Blob Container** dialog box, enter a name for the blob container and click **OK**.</span></span>

    <span data-ttu-id="916cd-531">![[建立 Blob 容器] 對話方塊](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "[建立 Blob 容器] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="916cd-531">![Create Blob Container dialog box](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Create Blob Container dialog box")</span></span>

    <span data-ttu-id="916cd-532">*[建立 Blob 容器] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="916cd-532">*Create Blob Container dialog box*</span></span>
8. <span data-ttu-id="916cd-533">新的 blob 容器應新增至 [ **blob** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="916cd-533">The new blob container should be added to the **Blobs** node.</span></span> <span data-ttu-id="916cd-534">變更容器中的存取權限，使容器成為公用。</span><span class="sxs-lookup"><span data-stu-id="916cd-534">Change the access permissions in the container to make the container public.</span></span> <span data-ttu-id="916cd-535">若要這麼做，請以滑鼠右鍵按一下 [ **images** ] 容器，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-535">To do this, right-click the **images** container and select **Properties**.</span></span>

    <span data-ttu-id="916cd-536">![images 容器屬性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images 容器屬性")</span><span class="sxs-lookup"><span data-stu-id="916cd-536">![images container properties](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images container properties")</span></span>

    <span data-ttu-id="916cd-537">*Images 容器屬性*</span><span class="sxs-lookup"><span data-stu-id="916cd-537">*Images container properties*</span></span>
9. <span data-ttu-id="916cd-538">在 [**屬性**] 視窗中，將 [**公用讀取權限**] 設定為 [**容器**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-538">In the **Properties** window, set the **Public Read Access** to **Container**.</span></span>

    <span data-ttu-id="916cd-539">![變更公用讀取權限屬性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "變更公用讀取權限屬性")</span><span class="sxs-lookup"><span data-stu-id="916cd-539">![Changing public read access property](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Changing public read access property")</span></span>

    <span data-ttu-id="916cd-540">*變更公用讀取權限屬性*</span><span class="sxs-lookup"><span data-stu-id="916cd-540">*Changing public read access property*</span></span>
10. <span data-ttu-id="916cd-541">當系統提示您是否確定要變更 [公用存取] 屬性時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-541">When prompted if you are sure you want to change the public access property, click **Yes**.</span></span>

    <span data-ttu-id="916cd-542">![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")</span><span class="sxs-lookup"><span data-stu-id="916cd-542">![Microsoft Visual Studio warning](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="916cd-543">*Microsoft Visual Studio 警告*</span><span class="sxs-lookup"><span data-stu-id="916cd-543">*Microsoft Visual Studio warning*</span></span>
11. <span data-ttu-id="916cd-544">在**伺服器總管**中，以滑鼠右鍵按一下**images** blob 容器，然後選取 [ **View blob container**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-544">In **Server Explorer**, right-click in the **images** blob container and select **View Blob Container**.</span></span>

    <span data-ttu-id="916cd-545">![View Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob 容器")</span><span class="sxs-lookup"><span data-stu-id="916cd-545">![View Blob Container](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "View Blob Container")</span></span>

    <span data-ttu-id="916cd-546">*View Blob 容器*</span><span class="sxs-lookup"><span data-stu-id="916cd-546">*View Blob Container*</span></span>
12. <span data-ttu-id="916cd-547">[Images] 容器應該會在新視窗中開啟，而且應該不會顯示任何專案的圖例。</span><span class="sxs-lookup"><span data-stu-id="916cd-547">The images container should open in a new window and a legend with no entries should be shown.</span></span> <span data-ttu-id="916cd-548">按一下 [**上傳**] 圖示，將檔案上傳至 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="916cd-548">Click the **upload** icon to upload a file to the blob container.</span></span>

    <span data-ttu-id="916cd-549">![沒有專案的 Images 容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "沒有專案的 Images 容器")</span><span class="sxs-lookup"><span data-stu-id="916cd-549">![Images container with no entries](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Images container with no entries")</span></span>

    <span data-ttu-id="916cd-550">*沒有專案的 Images 容器*</span><span class="sxs-lookup"><span data-stu-id="916cd-550">*Images container with no entries*</span></span>
13. <span data-ttu-id="916cd-551">在 [**上傳 Blob** ] 對話方塊中，流覽至實驗室的 [**資產**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="916cd-551">In the **Upload Blob** dialog box, navigate to the **Assets** folder of the lab.</span></span> <span data-ttu-id="916cd-552">選取 [ **logo-big** ] 檔案，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-552">Select the **logo-big.png** file and click **Open**.</span></span>
14. <span data-ttu-id="916cd-553">等候檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="916cd-553">Wait until the file is uploaded.</span></span> <span data-ttu-id="916cd-554">當上傳完成時，檔案應該會列在 images 容器中。</span><span class="sxs-lookup"><span data-stu-id="916cd-554">When the upload completes, the file should be listed in the images container.</span></span> <span data-ttu-id="916cd-555">以滑鼠右鍵按一下檔案專案，然後選取 [**複製 URL**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-555">Right-click the file entry and select **Copy URL**.</span></span>

    <span data-ttu-id="916cd-556">![複製 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "複製 blob 檔案 URL")</span><span class="sxs-lookup"><span data-stu-id="916cd-556">![Copy blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Copy blob file URL")</span></span>

    <span data-ttu-id="916cd-557">*複製 blob URL*</span><span class="sxs-lookup"><span data-stu-id="916cd-557">*Copy blob URL*</span></span>
15. <span data-ttu-id="916cd-558">開啟 Internet Explorer 並貼上 URL。</span><span class="sxs-lookup"><span data-stu-id="916cd-558">Open Internet Explorer and paste the URL.</span></span> <span data-ttu-id="916cd-559">下列影像應該會顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="916cd-559">The following image should be shown in the browser.</span></span>

    <span data-ttu-id="916cd-560">![從 Windows Blob 儲存體 logo-big .png 影像](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "從儲存體 logo-big .png 影像")</span><span class="sxs-lookup"><span data-stu-id="916cd-560">![logo-big.png image from Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "logo-big.png image from storage")</span></span>

    <span data-ttu-id="916cd-561">*從 Azure Blob 儲存體 logo-big .png 影像*</span><span class="sxs-lookup"><span data-stu-id="916cd-561">*logo-big.png image from Azure Blob Storage*</span></span>

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a><span data-ttu-id="916cd-562">工作 3-更新解決方案以取用 Azure Blob 儲存體的靜態內容</span><span class="sxs-lookup"><span data-stu-id="916cd-562">Task 3 – Updating the Solution to Consume Static Content from Azure Blob Storage</span></span>

<span data-ttu-id="916cd-563">在這項工作中，您會在**web.config**檔案中新增 ASP.NET URL 重寫規則，以將**GeekQuiz**解決方案設定為使用上傳至 Azure Blob 儲存體（而不是位於 web 應用程式中的影像）。</span><span class="sxs-lookup"><span data-stu-id="916cd-563">In this task, you will configure the **GeekQuiz** solution to consume the image uploaded to Azure Blob Storage (instead of the image located in the web app) by adding an ASP.NET URL rewrite rule in the **web.config** file.</span></span>

1. <span data-ttu-id="916cd-564">在 Visual Studio 中，開啟**GeekQuiz**專案**內的 web.config**檔案，並找出 **&lt;system.webserver&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="916cd-564">In Visual Studio, open the **Web.config** file inside the **GeekQuiz** project and locate the **&lt;system.webServer&gt;** element.</span></span>
2. <span data-ttu-id="916cd-565">新增下列程式碼，以新增 URL 重寫規則，並使用您的儲存體帳戶名稱來更新預留位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-565">Add the following code to add an URL rewrite rule, updating the placeholder with your storage account name.</span></span>

    <span data-ttu-id="916cd-566">（程式碼片段- *WebSitesInProduction-Ex4-UrlRewriteRule*）</span><span class="sxs-lookup"><span data-stu-id="916cd-566">(Code Snippet - *WebSitesInProduction - Ex4 - UrlRewriteRule*)</span></span>

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > <span data-ttu-id="916cd-567">URL 重寫程式會攔截傳入的 Web 要求，並將要求重新導向至不同的資源。</span><span class="sxs-lookup"><span data-stu-id="916cd-567">URL rewriting is the process of intercepting an incoming Web request and redirecting the request to a different resource.</span></span> <span data-ttu-id="916cd-568">URL 重寫規則會在要求需要重新導向時，告訴重寫引擎，以及應重新導向的位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-568">The URL rewriting rules tells the rewriting engine when a request needs to be redirected, and where should they be redirected.</span></span> <span data-ttu-id="916cd-569">重寫規則是由兩個字串所組成：在要求的 URL 中尋找的模式（通常是使用正則運算式），以及用來取代模式的字串（如果找到的話）。</span><span class="sxs-lookup"><span data-stu-id="916cd-569">A rewriting rule is composed of two strings: the pattern to look for in the requested URL (usually, using regular expressions), and the string to replace the pattern with, if found.</span></span> <span data-ttu-id="916cd-570">如需詳細資訊，請參閱[ASP.NET 中的 URL 重寫](https://msdn.microsoft.com/library/ms972974.aspx)。</span><span class="sxs-lookup"><span data-stu-id="916cd-570">For more information, see [URL Rewriting in ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).</span></span>
3. <span data-ttu-id="916cd-571">按**CTRL + S**儲存變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-571">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="916cd-572">開啟新的**Git Bash**主控台，將更新過的應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="916cd-572">Open a new **Git Bash** console to deploy the updated application to Azure App Service.</span></span>
5. <span data-ttu-id="916cd-573">執行下列命令，將變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="916cd-573">Execute the following commands to push the changes to Azure.</span></span> <span data-ttu-id="916cd-574">以**GeekQuiz**方案的路徑更新 *[您的應用程式-路徑]* 預留位置。</span><span class="sxs-lookup"><span data-stu-id="916cd-574">Update the *[YOUR-APPLICATION-PATH]* placeholder with the path to the **GeekQuiz** solution.</span></span> <span data-ttu-id="916cd-575">系統會提示您輸入您的部署密碼。</span><span class="sxs-lookup"><span data-stu-id="916cd-575">You will be prompted for your deployment password.</span></span>

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![將更新部署至 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    <span data-ttu-id="916cd-577">*將更新部署至 Azure*</span><span class="sxs-lookup"><span data-stu-id="916cd-577">*Deploying update to Azure*</span></span>

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a><span data-ttu-id="916cd-578">工作4–驗證</span><span class="sxs-lookup"><span data-stu-id="916cd-578">Task 4 – Verification</span></span>

<span data-ttu-id="916cd-579">在這項工作中，您將使用**Internet Explorer**流覽**萬能技客測驗**應用程式，並檢查影像的 URL 重寫規則是否正常運作，並將您重新導向至**Azure Blob 儲存體**上主控的映射。</span><span class="sxs-lookup"><span data-stu-id="916cd-579">In this task you will use **Internet Explorer** to browse the **Geek Quiz** application and check that the URL rewrite rule for images works and you are redirected to the image hosted on **Azure Blob Storage**.</span></span>

1. <span data-ttu-id="916cd-580">開啟 Internet Explorer 並流覽至您的 web 應用程式（例如 `http://<your-web-site>.azurewebsites.net`）。</span><span class="sxs-lookup"><span data-stu-id="916cd-580">Open Internet Explorer and navigate to your web app (e.g. `http://<your-web-site>.azurewebsites.net`).</span></span> <span data-ttu-id="916cd-581">使用先前建立的認證登入。</span><span class="sxs-lookup"><span data-stu-id="916cd-581">Log in using the previously created credentials.</span></span>

    <span data-ttu-id="916cd-582">![以影像顯示萬能技客測驗 web 應用程式](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "以影像顯示萬能技客測驗 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="916cd-582">![Showing the Geek Quiz web app with the image](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Showing the Geek Quiz web app with the image")</span></span>

    <span data-ttu-id="916cd-583">*以影像顯示萬能技客測驗 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="916cd-583">*Showing the Geek Quiz web app with the image*</span></span>
2. <span data-ttu-id="916cd-584">按**F12**啟動開發工具，選取 [**網路**] 索引標籤，然後開始錄製。</span><span class="sxs-lookup"><span data-stu-id="916cd-584">Press **F12** to launch the development tools, select the **Network** tab and start recording.</span></span>

    <span data-ttu-id="916cd-585">![正在啟動網路錄製](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "正在啟動網路錄製")</span><span class="sxs-lookup"><span data-stu-id="916cd-585">![Starting network recording](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Starting network recording")</span></span>

    <span data-ttu-id="916cd-586">*正在啟動網路錄製*</span><span class="sxs-lookup"><span data-stu-id="916cd-586">*Starting network recording*</span></span>
3. <span data-ttu-id="916cd-587">按**CTRL + F5**以重新整理網頁。</span><span class="sxs-lookup"><span data-stu-id="916cd-587">Press **CTRL + F5** to refresh the web page.</span></span>
4. <span data-ttu-id="916cd-588">網頁完成載入之後，您應該會看到 **/Img/logo-big.png** URL 的 HTTP 要求，其中包含 HTTP **301**結果（重新導向），以及另一個 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL 的要求與 HTTP **200**結果。</span><span class="sxs-lookup"><span data-stu-id="916cd-588">Once the page has finished loading, you should see an HTTP request for the **/img/logo-big.png** URL with an HTTP **301** result (redirect) and another request for `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL with a HTTP **200** result.</span></span>

    <span data-ttu-id="916cd-589">![驗證 URL 重新導向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "在開發人員工具中顯示重新導向")</span><span class="sxs-lookup"><span data-stu-id="916cd-589">![Verifying the URL redirect](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Showing the redirect in Dev Tools")</span></span>

    <span data-ttu-id="916cd-590">*驗證 URL 重新導向*</span><span class="sxs-lookup"><span data-stu-id="916cd-590">*Verifying the URL redirect*</span></span>

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a><span data-ttu-id="916cd-591">練習5：針對 Web Apps 使用自動調整</span><span class="sxs-lookup"><span data-stu-id="916cd-591">Exercise 5: Using Autoscale for Web Apps</span></span>

> [!NOTE]
> <span data-ttu-id="916cd-592">此練習是選擇性的，因為它需要支援 Web 負載 &amp; 效能測試，這僅適用于**Visual Studio 2013 旗艦版**。</span><span class="sxs-lookup"><span data-stu-id="916cd-592">This exercise is optional, since it requires support for Web Load &amp; Performance Testing which is only available for **Visual Studio 2013 Ultimate Edition**.</span></span> <span data-ttu-id="916cd-593">如需特定 Visual Studio 2013 功能的詳細資訊，請比較[這裡](https://www.microsoft.com/visualstudio/eng/products/compare)的版本。</span><span class="sxs-lookup"><span data-stu-id="916cd-593">For more information on specific Visual Studio 2013 features, compare versions [here](https://www.microsoft.com/visualstudio/eng/products/compare).</span></span>

<span data-ttu-id="916cd-594">**Azure App Service Web Apps**會針對以**標準模式**執行的 Web 應用程式提供自動調整功能。</span><span class="sxs-lookup"><span data-stu-id="916cd-594">**Azure App Service Web Apps** provides the Autoscale feature for web apps running in **Standard Mode**.</span></span> <span data-ttu-id="916cd-595">自動調整可讓 Azure 根據負載，自動調整 web 應用程式的實例計數。</span><span class="sxs-lookup"><span data-stu-id="916cd-595">Autoscale lets Azure automatically scale the instance count of your web app depending on the load.</span></span> <span data-ttu-id="916cd-596">啟用自動調整時，Azure 每隔五分鐘會檢查一次 web 應用程式的 CPU，並視需要在該時間點新增實例。</span><span class="sxs-lookup"><span data-stu-id="916cd-596">When Autoscale is enabled, Azure checks the CPU of your web app once every five minutes and adds instances as needed at that point in time.</span></span> <span data-ttu-id="916cd-597">如果 CPU 使用率很低，Azure 會每隔兩個小時移除實例一次，以確保 web 應用程式的效能不會降低。</span><span class="sxs-lookup"><span data-stu-id="916cd-597">If the CPU usage is low, Azure will remove instances once every two hours to ensure that the performance of your web app is not degraded.</span></span>

<span data-ttu-id="916cd-598">在此練習中，您將逐步完成為**萬能技客測驗**web 應用程式設定**自動**調整功能所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="916cd-598">In this exercise you will go through the steps required to configure the **Autoscale** feature for the **Geek Quiz** web app.</span></span> <span data-ttu-id="916cd-599">您將執行 Visual Studio 負載測試，以在應用程式上產生足夠的 CPU 負載來觸發實例升級，以驗證這項功能。</span><span class="sxs-lookup"><span data-stu-id="916cd-599">You will verify this feature by running a Visual Studio load test to generate enough CPU load on the application to trigger an instance upgrade.</span></span>

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a><span data-ttu-id="916cd-600">工作1–根據 CPU 度量設定自動調整</span><span class="sxs-lookup"><span data-stu-id="916cd-600">Task 1 – Configuring Autoscale Based on the CPU Metric</span></span>

<span data-ttu-id="916cd-601">在這項工作中，您將使用 Azure 管理入口網站，為您在練習2中建立的 web 應用程式啟用自動調整功能。</span><span class="sxs-lookup"><span data-stu-id="916cd-601">In this task you will use the Azure management portal to enable the Autoscale feature for the web app you created in Exercise 2.</span></span>

1. <span data-ttu-id="916cd-602">在[Azure 管理入口網站](https://manage.windowsazure.com/)中，選取 [**網站**]，然後按一下您在練習2中建立的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-602">In the [Azure management portal](https://manage.windowsazure.com/), select **Websites** and click the web app you created in Exercise 2.</span></span>
2. <span data-ttu-id="916cd-603">流覽至 [**調整**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-603">Navigate to the **Scale** page.</span></span> <span data-ttu-id="916cd-604">在 [**容量**] 區段下，選取 [**依度量調整規模**] 設定的 [ **CPU** ]。</span><span class="sxs-lookup"><span data-stu-id="916cd-604">Under the **capacity** section, select **CPU** for the **Scale by Metric** configuration.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-605">依 CPU 進行調整時，Azure 會在 CPU 使用量變更時，動態調整應用程式所使用的實例數目。</span><span class="sxs-lookup"><span data-stu-id="916cd-605">When scaling by CPU, Azure dynamically adjusts the number of instances that the app uses if the CPU usage changes.</span></span>

    <span data-ttu-id="916cd-606">![選取以根據 CPU 調整規模](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "選取自動調整的 CPU 度量")</span><span class="sxs-lookup"><span data-stu-id="916cd-606">![Selecting to scale by CPU](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Selecting the CPU metric for auto scaling")</span></span>

    <span data-ttu-id="916cd-607">*選取以根據 CPU 調整規模*</span><span class="sxs-lookup"><span data-stu-id="916cd-607">*Selecting to scale by CPU*</span></span>
3. <span data-ttu-id="916cd-608">將**目標 CPU 設定**變更為**20**-**40** %。</span><span class="sxs-lookup"><span data-stu-id="916cd-608">Change the **Target CPU** configuration to **20**-**40** percent.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-609">此範圍代表 web 應用程式的平均 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="916cd-609">This range represents the average CPU usage for your web app.</span></span> <span data-ttu-id="916cd-610">Azure 將會新增或移除實例，以將您的 web 應用程式保留在此範圍內。</span><span class="sxs-lookup"><span data-stu-id="916cd-610">Azure will add or remove instances to keep your web app in this range.</span></span> <span data-ttu-id="916cd-611">用於調整的實例數目下限和上限是在 [**實例計數**] 設定中指定。</span><span class="sxs-lookup"><span data-stu-id="916cd-611">The minimum and maximum number of instances used for scaling is specified in the **Instance Count** configuration.</span></span> <span data-ttu-id="916cd-612">Azure 永遠不會超出該限制。</span><span class="sxs-lookup"><span data-stu-id="916cd-612">Azure will never go above or beyond that limit.</span></span>
    >
    > <span data-ttu-id="916cd-613">預設的**目標 CPU**值只會針對此實驗室的目的而修改。</span><span class="sxs-lookup"><span data-stu-id="916cd-613">The default **Target CPU** values are modified just for the purposes of this lab.</span></span> <span data-ttu-id="916cd-614">藉由將 CPU 範圍設定為較小的值，您會增加在應用程式上放置中等負載時觸發自動調整的機會。</span><span class="sxs-lookup"><span data-stu-id="916cd-614">By configuring the CPU range with small values, you are increasing the chances to trigger Autoscale when a moderate load is placed on the application.</span></span>

    <span data-ttu-id="916cd-615">![將目標 CPU 變更為介於20到40% 之間](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "將目標 CPU 變更為介於20到40% 之間")</span><span class="sxs-lookup"><span data-stu-id="916cd-615">![Changing the target CPU to be between 20 and 40 percent](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Changing the target CPU to be between 20 and 40 percent")</span></span>

    <span data-ttu-id="916cd-616">*將目標 CPU 變更為介於20到40% 之間*</span><span class="sxs-lookup"><span data-stu-id="916cd-616">*Changing the Target CPU to be between 20 and 40 percent*</span></span>
4. <span data-ttu-id="916cd-617">按一下命令列中的 [**儲存**] 以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="916cd-617">Click **Save** in the command bar to save the changes.</span></span>

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a><span data-ttu-id="916cd-618">工作2–使用 Visual Studio 進行負載測試</span><span class="sxs-lookup"><span data-stu-id="916cd-618">Task 2 – Load Testing with Visual Studio</span></span>

<span data-ttu-id="916cd-619">現在已設定**自動**調整，您將在 Visual Studio 中建立**Web 效能和負載測試專案**，以在您的 Web 應用程式上產生一些 CPU 負載。</span><span class="sxs-lookup"><span data-stu-id="916cd-619">Now that **Autoscale** has been configured, you will create a **Web Performance and Load Test Project** in Visual Studio to generate some CPU load on your web app.</span></span>

1. <span data-ttu-id="916cd-620">開啟**Visual Studio Ultimate 2013**並選取 [檔案] **|新增 |專案 ...** 以啟動新的解決方案。</span><span class="sxs-lookup"><span data-stu-id="916cd-620">Open **Visual Studio Ultimate 2013** and select **File | New | Project...** to start a new solution.</span></span>

    <span data-ttu-id="916cd-621">![建立新專案](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "建立新專案")</span><span class="sxs-lookup"><span data-stu-id="916cd-621">![Creating a new project](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Creating a new project")</span></span>

    <span data-ttu-id="916cd-622">*建立新專案*</span><span class="sxs-lookup"><span data-stu-id="916cd-622">*Creating a new project*</span></span>
2. <span data-ttu-id="916cd-623">在 [**新增專案**] 對話方塊中，選取視覺效果  **C#底下的 [Web 效能和負載測試專案] |[測試**] 索引標籤。請確定已選取 **.NET Framework 4.5** ，將專案命名為*WebAndLoadTestProject*，選擇**位置**，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-623">In the **New Project** dialog box, select **Web Performance and Load Test Project** under the **Visual C# | Test** tab. Make sure **.NET Framework 4.5** is selected, name the project *WebAndLoadTestProject*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="916cd-624">![建立新的 Web 和負載測試專案](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "建立新的 Web 和負載測試專案")</span><span class="sxs-lookup"><span data-stu-id="916cd-624">![Creating a new Web and Load Test project](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Creating a new Web and Load Test project")</span></span>

    <span data-ttu-id="916cd-625">*建立新的 Web 和負載測試專案*</span><span class="sxs-lookup"><span data-stu-id="916cd-625">*Creating a new Web and Load Test project*</span></span>
3. <span data-ttu-id="916cd-626">在 [ **webtest1.webtest] webtest**中，以滑鼠右鍵按一下**webtest1.webtest**節點，然後按一下 [**新增要求**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-626">In the **WebTest1.webtest** Right-click the **WebTest1** node and click **Add Request**.</span></span>

    <span data-ttu-id="916cd-627">![將要求新增至 Webtest1.webtest](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "將要求新增至 Webtest1.webtest")</span><span class="sxs-lookup"><span data-stu-id="916cd-627">![Adding a request to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Adding a request to WebTest1")</span></span>

    <span data-ttu-id="916cd-628">*將要求新增至 Webtest1.webtest*</span><span class="sxs-lookup"><span data-stu-id="916cd-628">*Adding a request to WebTest1*</span></span>
4. <span data-ttu-id="916cd-629">在 [新增要求] 節點的 [**屬性**] 視窗中，更新 [ **url** ] 屬性以指向 WEB 應用程式的 url （例如 *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ）。</span><span class="sxs-lookup"><span data-stu-id="916cd-629">In the **Properties** window of the new request node, update the **Url** property to point to the URL of your web app (e.g. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)*).</span></span>

    <span data-ttu-id="916cd-630">![變更 Url 屬性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "變更 Url 屬性")</span><span class="sxs-lookup"><span data-stu-id="916cd-630">![Changing the Url property](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Changing the Url property")</span></span>

    <span data-ttu-id="916cd-631">*變更 Url 屬性*</span><span class="sxs-lookup"><span data-stu-id="916cd-631">*Changing the Url property*</span></span>
5. <span data-ttu-id="916cd-632">在 [ **webtest1.webtest webtest** ] 視窗中，以滑鼠右鍵按一下**webtest1.webtest** ，然後按一下 [**新增迴圈**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-632">In the **WebTest1.webtest** window, right-click **WebTest1** and click **Add Loop...**.</span></span>

    <span data-ttu-id="916cd-633">![將迴圈新增至 Webtest1.webtest](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "將迴圈新增至 Webtest1.webtest")</span><span class="sxs-lookup"><span data-stu-id="916cd-633">![Adding a loop to WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Adding a loop to WebTest1")</span></span>

    <span data-ttu-id="916cd-634">*將迴圈新增至 Webtest1.webtest*</span><span class="sxs-lookup"><span data-stu-id="916cd-634">*Adding a loop to WebTest1*</span></span>
6. <span data-ttu-id="916cd-635">在 [**加入條件式規則和要迴圈的專案**] 對話方塊中，選取 [ **For 迴圈**] 規則，並修改下列屬性。</span><span class="sxs-lookup"><span data-stu-id="916cd-635">In the **Add Conditional Rule and Items to Loop** dialog box, select the **For Loop** rule and modify the following properties.</span></span>

   1. <span data-ttu-id="916cd-636">**終止值：** 1000</span><span class="sxs-lookup"><span data-stu-id="916cd-636">**Terminating value:** 1000</span></span>
   2. <span data-ttu-id="916cd-637">**內容參數名稱：** 定位</span><span class="sxs-lookup"><span data-stu-id="916cd-637">**Context Parameter Name:** Iterator</span></span>
   3. <span data-ttu-id="916cd-638">**遞增值：** 1</span><span class="sxs-lookup"><span data-stu-id="916cd-638">**Increment Value:** 1</span></span>

      <span data-ttu-id="916cd-639">![選取「For 迴圈」規則並更新屬性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "選取「For 迴圈」規則並更新屬性")</span><span class="sxs-lookup"><span data-stu-id="916cd-639">![Selecting the For Loop rule and updating the properties](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Selecting the For Loop rule and updating the properties")</span></span>

      <span data-ttu-id="916cd-640">*選取「For 迴圈」規則並更新屬性*</span><span class="sxs-lookup"><span data-stu-id="916cd-640">*Selecting the For Loop rule and updating the properties*</span></span>
7. <span data-ttu-id="916cd-641">在 [**迴圈中的專案**] 區段下，選取您先前建立的要求做為迴圈的第一個和最後一個專案。</span><span class="sxs-lookup"><span data-stu-id="916cd-641">Under the **Items in loop** section, select the request you created previously to be the first and last item for the loop.</span></span> <span data-ttu-id="916cd-642">按一下 [確定] 繼續操作。</span><span class="sxs-lookup"><span data-stu-id="916cd-642">Click **OK** to continue.</span></span>

    <span data-ttu-id="916cd-643">![選取迴圈的第一個和最後一個專案](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "選取迴圈的第一個和最後一個專案")</span><span class="sxs-lookup"><span data-stu-id="916cd-643">![Selecting the first and last items for the loop](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Selecting the first and last items for the loop")</span></span>

    <span data-ttu-id="916cd-644">*選取迴圈的第一個和最後一個專案*</span><span class="sxs-lookup"><span data-stu-id="916cd-644">*Selecting the first and last items for the loop*</span></span>
8. <span data-ttu-id="916cd-645">在**方案總管**中，以滑鼠右鍵按一下**WebAndLoadTestProject**專案，展開 [**新增**] 功能表，然後選取 [**負載測試 ...** ]。</span><span class="sxs-lookup"><span data-stu-id="916cd-645">In **Solution Explorer**, right-click the **WebAndLoadTestProject** project, expand the **Add** menu and select **Load Test...**.</span></span>

    <span data-ttu-id="916cd-646">![將負載測試加入至 WebAndLoadTestProject 專案](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "將負載測試加入至 WebAndLoadTestProject 專案")</span><span class="sxs-lookup"><span data-stu-id="916cd-646">![Adding a Load Test to the WebAndLoadTestProject project](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Adding a Load Test to the WebAndLoadTestProject project")</span></span>

    <span data-ttu-id="916cd-647">*將負載測試加入至 WebAndLoadTestProject 專案*</span><span class="sxs-lookup"><span data-stu-id="916cd-647">*Adding a Load Test to the WebAndLoadTestProject project*</span></span>
9. <span data-ttu-id="916cd-648">在 [**新增負載測試精靈**] 對話方塊中，按 **[下一步**]。</span><span class="sxs-lookup"><span data-stu-id="916cd-648">In the **New Load Test Wizard** dialog box, click **Next**.</span></span>

    <span data-ttu-id="916cd-649">![新增負載測試精靈](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新增負載測試精靈")</span><span class="sxs-lookup"><span data-stu-id="916cd-649">![New Load Test Wizard](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "New Load Test Wizard")</span></span>

    <span data-ttu-id="916cd-650">*新增負載測試精靈*</span><span class="sxs-lookup"><span data-stu-id="916cd-650">*New Load Test Wizard*</span></span>
10. <span data-ttu-id="916cd-651">在 [**案例**] 頁面中，選取 [不**使用考慮時間**]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-651">In the **Scenario** page, select **Do not use think times** and click **Next**.</span></span>

    <span data-ttu-id="916cd-652">![選取不使用考慮時間](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "選取不使用考慮時間")</span><span class="sxs-lookup"><span data-stu-id="916cd-652">![Selecting not to use think times](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Selecting not to use think times")</span></span>

    <span data-ttu-id="916cd-653">*選取不使用考慮時間*</span><span class="sxs-lookup"><span data-stu-id="916cd-653">*Selecting not to use think times*</span></span>
11. <span data-ttu-id="916cd-654">在 [**負載模式**] 頁面中，確認已選取 [**常數載入**] 選項。</span><span class="sxs-lookup"><span data-stu-id="916cd-654">In the **Load Pattern** page, make sure that the **Constant Load** option is selected.</span></span> <span data-ttu-id="916cd-655">將 [**使用者計數**] 設定變更為**250**個使用者，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-655">Change the **User Count** setting to **250** users and click **Next**.</span></span>

    <span data-ttu-id="916cd-656">![將使用者計數變更為250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "將使用者計數變更為250")</span><span class="sxs-lookup"><span data-stu-id="916cd-656">![Changing the user count to 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Changing the user count to 250")</span></span>

    <span data-ttu-id="916cd-657">*將使用者計數變更為250*</span><span class="sxs-lookup"><span data-stu-id="916cd-657">*Changing the user count to 250*</span></span>
12. <span data-ttu-id="916cd-658">在 [**測試混合模型**] 頁面中，選取 [**根據順序測試順序**]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-658">In the **Test Mix Model** page, select **Based on sequential test order** and click **Next**.</span></span>

    <span data-ttu-id="916cd-659">![選取測試混合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "選取測試混合模型")</span><span class="sxs-lookup"><span data-stu-id="916cd-659">![Selecting the test mix model](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Selecting the test mix model")</span></span>

    <span data-ttu-id="916cd-660">*選取測試混合模型*</span><span class="sxs-lookup"><span data-stu-id="916cd-660">*Selecting the test mix model*</span></span>
13. <span data-ttu-id="916cd-661">在 [**測試混合模型**] 頁面中，按一下 [**加入**]，將測試加入至混合。</span><span class="sxs-lookup"><span data-stu-id="916cd-661">In the **Test Mix Model** page, click **Add...** to add a test to the mix.</span></span>

    <span data-ttu-id="916cd-662">![將測試加入至測試混合](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "將測試加入至測試混合")</span><span class="sxs-lookup"><span data-stu-id="916cd-662">![Adding a test to the test mix](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Adding a test to the test mix")</span></span>

    <span data-ttu-id="916cd-663">*將測試加入至測試混合*</span><span class="sxs-lookup"><span data-stu-id="916cd-663">*Adding a test to the test mix*</span></span>
14. <span data-ttu-id="916cd-664">在 [**加入測試**] 對話方塊中，按兩下 [ **webtest1.webtest** ]，將測試加入至 [**選取的測試**] 清單。</span><span class="sxs-lookup"><span data-stu-id="916cd-664">In the **Add Tests** dialog box, double-click **WebTest1** to add the test to the **Selected tests** list.</span></span> <span data-ttu-id="916cd-665">按一下 [確定] 繼續操作。</span><span class="sxs-lookup"><span data-stu-id="916cd-665">Click **OK** to continue.</span></span>

    <span data-ttu-id="916cd-666">![新增 Webtest1.webtest 測試](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "新增 Webtest1.webtest 測試")</span><span class="sxs-lookup"><span data-stu-id="916cd-666">![Adding the WebTest1 test](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Adding the WebTest1 test")</span></span>

    <span data-ttu-id="916cd-667">*新增 Webtest1.webtest 測試*</span><span class="sxs-lookup"><span data-stu-id="916cd-667">*Adding the WebTest1 test*</span></span>
15. <span data-ttu-id="916cd-668">回到 [**測試混合**] 頁面，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-668">Back in the **Test Mix** page, click **Next**.</span></span>

    <span data-ttu-id="916cd-669">![正在完成測試混合頁面](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "正在完成測試混合頁面")</span><span class="sxs-lookup"><span data-stu-id="916cd-669">![Completing the Test Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Completing the Test Mix page")</span></span>

    <span data-ttu-id="916cd-670">*正在完成測試混合頁面*</span><span class="sxs-lookup"><span data-stu-id="916cd-670">*Completing the Test Mix page*</span></span>
16. <span data-ttu-id="916cd-671">在 [**網路混合**] 頁面上，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-671">In the **Network Mix** page, click **Next**.</span></span>

    <span data-ttu-id="916cd-672">![在 [網路混合] 頁面中按一下 [下一步]](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "在 [網路混合] 頁面中按一下 [下一步]")</span><span class="sxs-lookup"><span data-stu-id="916cd-672">![Clicking next in the Network Mix page](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Clicking next in the Network Mix page")</span></span>

    <span data-ttu-id="916cd-673">*在 [網路混合] 頁面中按一下 [下一步]*</span><span class="sxs-lookup"><span data-stu-id="916cd-673">*Clicking next in the Network Mix page*</span></span>
17. <span data-ttu-id="916cd-674">在 [**瀏覽器混合**] 頁面中，選取**Internet Explorer 10.0**作為瀏覽器類型，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-674">In the **Browser Mix** page, select **Internet Explorer 10.0** as the browser type and click **Next**.</span></span>

    <span data-ttu-id="916cd-675">![選取瀏覽器類型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "選取瀏覽器類型")</span><span class="sxs-lookup"><span data-stu-id="916cd-675">![Selecting the browser type](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Selecting the browser type")</span></span>

    <span data-ttu-id="916cd-676">*選取瀏覽器類型*</span><span class="sxs-lookup"><span data-stu-id="916cd-676">*Selecting the browser type*</span></span>
18. <span data-ttu-id="916cd-677">在 [**計數器集合**] 頁面上，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-677">In the **Counter Sets** page, click **Next**.</span></span>

    <span data-ttu-id="916cd-678">![按一下 [計數器集合] 頁面中的 [下一步]](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "按一下 [計數器集合] 頁面中的 [下一步]")</span><span class="sxs-lookup"><span data-stu-id="916cd-678">![Clicking Next in the Counter Sets page](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Clicking Next in the Counter Sets page")</span></span>

    <span data-ttu-id="916cd-679">*按一下 [計數器集合] 頁面中的 [下一步]*</span><span class="sxs-lookup"><span data-stu-id="916cd-679">*Clicking Next in the Counter Sets page*</span></span>
19. <span data-ttu-id="916cd-680">在 [回合**設定**] 頁面上，將**負載測試持續時間**設定為**5 分鐘**，然後按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="916cd-680">In the **Run Settings** page, set the **Load test duration** to **5 minutes** and click **Finish**.</span></span>

    <span data-ttu-id="916cd-681">![將負載測試持續時間設定為5分鐘](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "將負載測試持續時間設定為5分鐘")</span><span class="sxs-lookup"><span data-stu-id="916cd-681">![Setting the load test duration to 5 minutes](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Setting the load test duration to 5 minutes")</span></span>

    <span data-ttu-id="916cd-682">*將負載測試持續時間設定為5分鐘*</span><span class="sxs-lookup"><span data-stu-id="916cd-682">*Setting the load test duration to 5 minutes*</span></span>
20. <span data-ttu-id="916cd-683">在**方案總管**中，按兩下本機的**配置**檔案，以流覽測試設定。</span><span class="sxs-lookup"><span data-stu-id="916cd-683">In **Solution Explorer**, double-click the **Local.settings** file to explore the test settings.</span></span> <span data-ttu-id="916cd-684">根據預設，Visual Studio 會使用您的本機電腦來執行測試。</span><span class="sxs-lookup"><span data-stu-id="916cd-684">By default, Visual Studio uses your local computer to run the tests.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-685">或者，您可以使用**Azure Test Plans**，將您的測試專案設定為在雲端中執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="916cd-685">Alternatively, you can configure your test project to run the load tests in the cloud using **Azure Test Plans**.</span></span> <span data-ttu-id="916cd-686">Azure Test Plans 提供以雲端為基礎的負載測試服務，可模擬更實際的負載，避免像是 CPU 容量、可用記憶體和網路頻寬等本機環境的條件約束。</span><span class="sxs-lookup"><span data-stu-id="916cd-686">Azure Test Plans provides a cloud-based load testing service that simulates a more realistic load, avoiding local environment constraints like CPU capacity, available memory, and network bandwidth.</span></span> <span data-ttu-id="916cd-687">如需使用 Azure Test Plans 執行負載測試的詳細資訊，請參閱[負載測試案例](/azure/devops/test/load-test/overview?view=vsts)。</span><span class="sxs-lookup"><span data-stu-id="916cd-687">For more information about using Azure Test Plans to run load tests, see [Load testing scenarios](/azure/devops/test/load-test/overview?view=vsts).</span></span>

    ![測試設定](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a><span data-ttu-id="916cd-689">工作 3-自動調整驗證</span><span class="sxs-lookup"><span data-stu-id="916cd-689">Task 3 – Autoscale Verification</span></span>

<span data-ttu-id="916cd-690">您現在會執行您在上一項工作中建立的負載測試，並查看您的 web 應用程式在負載下的行為。</span><span class="sxs-lookup"><span data-stu-id="916cd-690">You will now execute the load test you created in the previous task and see how your web app behaves under load.</span></span>

1. <span data-ttu-id="916cd-691">在**方案總管**中，按兩下**loadtest1.loadtest loadtest**以開啟負載測試。</span><span class="sxs-lookup"><span data-stu-id="916cd-691">In **Solution Explorer**, double-click **LoadTest1.loadtest** to open the load test.</span></span>

    <span data-ttu-id="916cd-692">![開啟 Loadtest1.loadtest。 loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "開啟 Loadtest1.loadtest。 loadtest")</span><span class="sxs-lookup"><span data-stu-id="916cd-692">![Opening LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Opening LoadTest1.loadtest")</span></span>

    <span data-ttu-id="916cd-693">*開啟 Loadtest1.loadtest。 loadtest*</span><span class="sxs-lookup"><span data-stu-id="916cd-693">*Opening LoadTest1.loadtest*</span></span>
2. <span data-ttu-id="916cd-694">在 [ **loadtest1.loadtest loadtest** ] 視窗中，按一下 [工具箱] 中的第一個按鈕以執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="916cd-694">In the **LoadTest1.loadtest** window, click the first button in the toolbox to run the load test.</span></span>

    <span data-ttu-id="916cd-695">![執行負載測試](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "執行負載測試")</span><span class="sxs-lookup"><span data-stu-id="916cd-695">![Running the load test](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Running the load test")</span></span>

    <span data-ttu-id="916cd-696">*執行負載測試*</span><span class="sxs-lookup"><span data-stu-id="916cd-696">*Running the load test*</span></span>
3. <span data-ttu-id="916cd-697">等待負載測試完成。</span><span class="sxs-lookup"><span data-stu-id="916cd-697">Wait until the load test completes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-698">負載測試會模擬多個將要求同時傳送至 web 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="916cd-698">The load test simulates multiple users that send requests to the web app simultaneously.</span></span> <span data-ttu-id="916cd-699">當測試正在執行時，您可以監視可用的計數器，以偵測任何與負載測試回合相關的錯誤、警告或其他資訊。</span><span class="sxs-lookup"><span data-stu-id="916cd-699">When the test is running, you can monitor the available counters to detect any errors, warnings or other information related to your load test run.</span></span>

    <span data-ttu-id="916cd-700">![負載測試正在執行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "等待負載測試完成")</span><span class="sxs-lookup"><span data-stu-id="916cd-700">![Load test running](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Waiting until the load test completes")</span></span>

    <span data-ttu-id="916cd-701">*負載測試正在執行*</span><span class="sxs-lookup"><span data-stu-id="916cd-701">*Load test running*</span></span>
4. <span data-ttu-id="916cd-702">測試完成之後，請回到入口網站，並流覽至 web 應用程式的 [**調整規模**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="916cd-702">Once the test completes, go back to the management portal and navigate to the **Scale** page of your web app.</span></span> <span data-ttu-id="916cd-703">在 [**容量**] 區段下，您應該會在圖表中看到新實例已自動部署。</span><span class="sxs-lookup"><span data-stu-id="916cd-703">Under the **capacity** section, you should see in the graph that a new instance was automatically deployed.</span></span>

    ![已自動部署新的實例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    <span data-ttu-id="916cd-705">*已自動部署新的實例*</span><span class="sxs-lookup"><span data-stu-id="916cd-705">*New instance automatically deployed*</span></span>

    > [!NOTE]
    > <span data-ttu-id="916cd-706">可能需要幾分鐘的時間，變更才會出現在圖形中（請定期按**CTRL + F5**以重新整理頁面）。</span><span class="sxs-lookup"><span data-stu-id="916cd-706">It may take several minutes for the changes to appear in the graph (press **CTRL + F5** periodically to refresh the page).</span></span> <span data-ttu-id="916cd-707">如果您看不到任何變更，可以嘗試下列動作：</span><span class="sxs-lookup"><span data-stu-id="916cd-707">If you do not see any changes, you can try the following:</span></span>
    >
    > - <span data-ttu-id="916cd-708">增加負載測試的持續時間（例如**10 分鐘**）</span><span class="sxs-lookup"><span data-stu-id="916cd-708">Increase the duration of the load test (e.g. to **10 minutes**)</span></span>
    > - <span data-ttu-id="916cd-709">在 web 應用程式的自動調整規模設定中，減少**目標 CPU**範圍的最大值和最小值</span><span class="sxs-lookup"><span data-stu-id="916cd-709">Reduce the maximum and minimum values of the **Target CPU** range in the Autoscale configuration of your web app</span></span>
    > - <span data-ttu-id="916cd-710">使用**Azure Test Plans**在雲端中執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="916cd-710">Run the load test in the cloud with **Azure Test Plans**.</span></span> <span data-ttu-id="916cd-711">如需詳細資訊，請參閱[這裡](/azure/devops/test/load-test/index?view=vsts)。</span><span class="sxs-lookup"><span data-stu-id="916cd-711">More information [here](/azure/devops/test/load-test/index?view=vsts)</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="916cd-712">總結</span><span class="sxs-lookup"><span data-stu-id="916cd-712">Summary</span></span>

<span data-ttu-id="916cd-713">在此實際操作實驗室中，您已瞭解如何在 Azure 中設定應用程式，並將其部署至生產 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="916cd-713">In this hands-on lab, you learned how to set up and deploy your application to production web apps in Azure.</span></span> <span data-ttu-id="916cd-714">您一開始會使用**Entity Framework Code First 移轉**來偵測及更新您的資料庫，然後繼續使用**Git**部署新版本的網站，並執行復原至網站的最新穩定版本。</span><span class="sxs-lookup"><span data-stu-id="916cd-714">You started by detecting and updating your databases using **Entity Framework Code First Migrations**, then continued by deploying new versions of your site using **Git** and performing rollbacks to the latest stable version of your site.</span></span> <span data-ttu-id="916cd-715">此外，您已瞭解如何使用儲存體來調整您的應用程式，以將您的靜態內容移至 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="916cd-715">Additionally, you learned how to scale your app using Storage to move your static content to a Blob container.</span></span>
