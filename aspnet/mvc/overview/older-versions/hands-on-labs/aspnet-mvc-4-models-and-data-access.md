---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和資料存取 |Microsoft Docs
author: rick-anderson
description: 注意:這個實際操作實驗室會假設您有 ASP.NET mvc 的基本知識。 如果您未曾使用之前的 ASP.NET MVC，我們建議您將會透過 ASP.NET MVC 4...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 10c2f6379f6d3139dd3bcf1027ff456e074298c3
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425089"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="eced9-104">ASP.NET MVC 4 模型和資料存取</span><span class="sxs-lookup"><span data-stu-id="eced9-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="eced9-105">藉由[Web Camp 小組](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="eced9-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="eced9-106">下載 Web 研討會訓練套件</span><span class="sxs-lookup"><span data-stu-id="eced9-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="eced9-107">這個實際操作實驗室會假設您有的基本知識**ASP.NET MVC**。</span><span class="sxs-lookup"><span data-stu-id="eced9-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="eced9-108">如果您未曾使用**ASP.NET MVC**之前，我們建議您將逐一**ASP.NET MVC 4 基本概念**實際操作實驗室。</span><span class="sxs-lookup"><span data-stu-id="eced9-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="eced9-109">這個實驗室會引導您完成先前所述將微幅的變更套用到來源資料夾中提供的範例 Web 應用程式的新功能與增強功能。</span><span class="sxs-lookup"><span data-stu-id="eced9-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-110">所有的範例程式碼和程式碼片段會包含在 Web 研討會訓練套件，可在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="eced9-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="eced9-111">這個實驗室中的特定專案將會位於[ASP.NET MVC 4 模型和資料存取](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)。</span><span class="sxs-lookup"><span data-stu-id="eced9-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="eced9-112">在  **ASP.NET MVC 基礎**實際操作實驗室中，您有已硬式編碼的資料將從傳遞控制站至檢視範本。</span><span class="sxs-lookup"><span data-stu-id="eced9-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="eced9-113">但是，若要建置實際的 Web 應用程式，您可能想要使用實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="eced9-114">這個實際操作實驗室會示範如何使用資料庫引擎來儲存和擷取音樂市集應用程式所需的資料。</span><span class="sxs-lookup"><span data-stu-id="eced9-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="eced9-115">若要達到此目的，您會啟動與現有的資料庫，並從它建立實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="eced9-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="eced9-116">在這個實驗室中，您將會符合**Database First**方法，以及**Code First**方法。</span><span class="sxs-lookup"><span data-stu-id="eced9-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="eced9-117">不過，您也可以使用**Model First**方法，建立相同的模型使用的工具，然後從它產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="eced9-118">![第一個與資料庫。Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs。第一次建立模型")</span><span class="sxs-lookup"><span data-stu-id="eced9-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="eced9-119">*第一個與資料庫。第一次建立模型*</span><span class="sxs-lookup"><span data-stu-id="eced9-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="eced9-120">之後產生模型，以提供從資料庫中，而不是使用硬式編碼資料的資料存放區檢視 StoreController 中進行適當調整。</span><span class="sxs-lookup"><span data-stu-id="eced9-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="eced9-121">此外，您將不需要進行任何變更的檢視範本 StoreController 將相同的 Viewmodel 傳回檢視範本，因為雖然此時資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="eced9-122">**Code First 方法**</span><span class="sxs-lookup"><span data-stu-id="eced9-122">**The Code First Approach**</span></span>

<span data-ttu-id="eced9-123">Code First 方法可讓我們不會產生類別，通常會結合 framework 定義的程式碼中的模型。</span><span class="sxs-lookup"><span data-stu-id="eced9-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="eced9-124">在程式碼第一，模型物件會定義 Poco，&quot;純舊 CLR 物件&quot;。</span><span class="sxs-lookup"><span data-stu-id="eced9-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="eced9-125">Poco 是簡單的一般類別，具有沒有繼承，而且不會實作介面。</span><span class="sxs-lookup"><span data-stu-id="eced9-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="eced9-126">我們可以自動產生的資料庫，或者我們可以使用現有的資料庫，並從程式碼產生的類別對應。</span><span class="sxs-lookup"><span data-stu-id="eced9-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="eced9-127">使用這種方法的優點是，模型會維持不變 （在此情況下，Entity Framework），持續性架構無關的 Poco 類別不會搭配對應的架構。</span><span class="sxs-lookup"><span data-stu-id="eced9-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-128">這個實驗室根據 ASP.NET MVC 4 和自訂的音樂市集 」 範例應用程式的版本，和最小化成只顯示這個實際操作實驗室的功能。</span><span class="sxs-lookup"><span data-stu-id="eced9-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="eced9-129">如果您想要瀏覽整個**音樂市集**您可以找到它的應用程式教學課程[MVC Music 市集](https://github.com/evilDave/MVC-Music-Store)。</span><span class="sxs-lookup"><span data-stu-id="eced9-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="eced9-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="eced9-130">Prerequisites</span></span>

<span data-ttu-id="eced9-131">您必須具備下列項目，即可完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="eced9-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="eced9-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更好 (讀取[附錄 A](#AppendixA)如需有關如何安裝它)。</span><span class="sxs-lookup"><span data-stu-id="eced9-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="eced9-133">安裝程式</span><span class="sxs-lookup"><span data-stu-id="eced9-133">Setup</span></span>

<span data-ttu-id="eced9-134">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="eced9-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="eced9-135">為了方便起見，大部分的程式碼，您將沿著這個實驗室管理可從 Visual Studio 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="eced9-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="eced9-136">若要安裝執行的程式碼片段 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="eced9-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="eced9-137">如果您不熟悉 Visual Studio 程式碼片段，而且想要了解如何使用它們，您可以從這份文件參考附錄&quot;[附錄 c:使用程式碼片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="eced9-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="eced9-138">練習</span><span class="sxs-lookup"><span data-stu-id="eced9-138">Exercises</span></span>

<span data-ttu-id="eced9-139">這個實際操作實驗室是由下列練習所組成的：</span><span class="sxs-lookup"><span data-stu-id="eced9-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="eced9-140">練習 1:加入資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="eced9-141">練習 2:使用 Code First 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="eced9-142">練習 3:查詢參數的資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="eced9-143">每個練習會伴隨**結束**包含完成練習之後，您應該取得所產生的方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="eced9-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="eced9-144">如果您需要的所有練習所使用的其他說明，您可以使用此解決方案作為指南。</span><span class="sxs-lookup"><span data-stu-id="eced9-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="eced9-145">估計的時間才能完成這個實驗室：**35 分鐘內**。</span><span class="sxs-lookup"><span data-stu-id="eced9-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="eced9-146">練習 1:加入資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="eced9-147">在此練習中，您將學習如何新增含有 MusicStore 應用程式方案，以便取用其資料的資料表的資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="eced9-148">一旦資料庫產生模型，然後加入至方案，您將修改 StoreController 類別，以提供從資料庫中，而不是使用硬式編碼值的資料檢視範本。</span><span class="sxs-lookup"><span data-stu-id="eced9-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="eced9-149">工作 1-新增資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="eced9-150">在這個工作中，您將加入已建立的資料庫解決方案 MusicStore 應用程式的主資料表。</span><span class="sxs-lookup"><span data-stu-id="eced9-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="eced9-151">開啟**開始**解決方案位於**來源/Ex1-AddingADatabaseDBFirst/開始/** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eced9-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="eced9-152">您必須下載某些缺少的 NuGet 封裝才能繼續。</span><span class="sxs-lookup"><span data-stu-id="eced9-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="eced9-153">若要這樣做，請按一下**專案**功能表，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="eced9-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="eced9-154">在 [**管理 NuGet 套件**] 對話方塊中，按一下**還原**才能下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="eced9-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="eced9-155">最後，按一下 建置方案**建置** | **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="eced9-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="eced9-156">使用 NuGet 的優點之一是，您不需要寄送您的專案中的所有程式庫專案縮小。</span><span class="sxs-lookup"><span data-stu-id="eced9-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="eced9-157">NuGet Power tools，藉由指定封裝版本在 Packages.config 檔案中，您將能夠下載所有必要的程式庫第一次執行專案。</span><span class="sxs-lookup"><span data-stu-id="eced9-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="eced9-158">這就是為什麼您必須在您開啟現有的方案從這個實驗室之後，執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="eced9-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="eced9-159">新增**MvcMusicStore**資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="eced9-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="eced9-160">在這個實際操作實驗室中，您將使用已建立的資料庫呼叫**MvcMusicStore.mdf**。</span><span class="sxs-lookup"><span data-stu-id="eced9-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="eced9-161">若要這樣做，請以滑鼠右鍵按一下**應用程式\_資料**資料夾，指向**新增**，然後按一下**現有項目**。</span><span class="sxs-lookup"><span data-stu-id="eced9-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="eced9-162">瀏覽至 **\Source\Assets** ，然後選取 **MvcMusicStore.mdf** 檔案。</span><span class="sxs-lookup"><span data-stu-id="eced9-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="eced9-163">![加入現有項目](aspnet-mvc-4-models-and-data-access/_static/image2.png "加入現有項目")</span><span class="sxs-lookup"><span data-stu-id="eced9-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="eced9-164">*加入現有項目*</span><span class="sxs-lookup"><span data-stu-id="eced9-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="eced9-165">![MvcMusicStore.mdf 資料庫檔案](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 資料庫檔案")</span><span class="sxs-lookup"><span data-stu-id="eced9-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="eced9-166">*MvcMusicStore.mdf 資料庫檔案*</span><span class="sxs-lookup"><span data-stu-id="eced9-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="eced9-167">資料庫已新增至專案。</span><span class="sxs-lookup"><span data-stu-id="eced9-167">The database has been added to the project.</span></span> <span data-ttu-id="eced9-168">即使資料庫位於置於方案中，您可以查詢並更新它，因為它裝載在不同的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="eced9-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="eced9-169">![在 方案總管 MvcMusicStore 資料庫](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore 方案總管 中的資料庫")</span><span class="sxs-lookup"><span data-stu-id="eced9-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="eced9-170">*在 [方案總管] 中的 MvcMusicStore 資料庫*</span><span class="sxs-lookup"><span data-stu-id="eced9-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="eced9-171">請確認資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="eced9-171">Verify the connection to the database.</span></span> <span data-ttu-id="eced9-172">若要這樣做，請按兩下**MvcMusicStore.mdf**建立連線。</span><span class="sxs-lookup"><span data-stu-id="eced9-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="eced9-173">![連接到 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "連接到 MvcMusicStore.mdf")</span><span class="sxs-lookup"><span data-stu-id="eced9-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="eced9-174">*連接到 MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="eced9-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="eced9-175">工作 2-建立資料模型</span><span class="sxs-lookup"><span data-stu-id="eced9-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="eced9-176">在這個工作中，您將建立資料模型與先前的工作中新增的資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="eced9-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="eced9-177">建立資料模型，以代表資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="eced9-178">若要這樣做，請在 方案總管 中以滑鼠右鍵按一下**模型**資料夾，指向**新增**，然後按一下 **新項目**。</span><span class="sxs-lookup"><span data-stu-id="eced9-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="eced9-179">在 **加入新項目**對話方塊中，選取**Data**範本，然後**ADO.NET 實體資料模型**項目。</span><span class="sxs-lookup"><span data-stu-id="eced9-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="eced9-180">資料模型將名稱變更為**StoreDB.edmx**然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="eced9-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="eced9-181">![新增 StoreDB ADO.NET 實體資料模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "新增 StoreDB ADO.NET 實體資料模型")</span><span class="sxs-lookup"><span data-stu-id="eced9-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="eced9-182">*新增 StoreDB ADO.NET 實體資料模型*</span><span class="sxs-lookup"><span data-stu-id="eced9-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="eced9-183">**Entity Data Model 精靈**會出現。</span><span class="sxs-lookup"><span data-stu-id="eced9-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="eced9-184">此精靈會引導您完成建立模型層。</span><span class="sxs-lookup"><span data-stu-id="eced9-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="eced9-185">由於此模型應該根據最近新增的現有資料庫建立，選取**從資料庫產生**然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eced9-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="eced9-186">![選擇模型內容](aspnet-mvc-4-models-and-data-access/_static/image7.png "選擇模型內容")</span><span class="sxs-lookup"><span data-stu-id="eced9-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="eced9-187">*選擇模型內容*</span><span class="sxs-lookup"><span data-stu-id="eced9-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="eced9-188">因為您從資料庫產生模型，您必須指定要使用的連接。</span><span class="sxs-lookup"><span data-stu-id="eced9-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="eced9-189">按一下 **新的連接**。</span><span class="sxs-lookup"><span data-stu-id="eced9-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="eced9-190">選取  **Microsoft SQL Server 資料庫檔案**然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="eced9-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="eced9-191">![選擇資料來源](aspnet-mvc-4-models-and-data-access/_static/image8.png "選擇資料來源")</span><span class="sxs-lookup"><span data-stu-id="eced9-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="eced9-192">*[選擇資料來源] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="eced9-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="eced9-193">按一下 **瀏覽**，然後選取資料庫**MvcMusicStore.mdf**您位於**應用程式\_資料**資料夾，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="eced9-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="eced9-194">![連接屬性](aspnet-mvc-4-models-and-data-access/_static/image9.png "連接屬性")</span><span class="sxs-lookup"><span data-stu-id="eced9-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="eced9-195">*連接屬性*</span><span class="sxs-lookup"><span data-stu-id="eced9-195">*Connection properties*</span></span>
6. <span data-ttu-id="eced9-196">產生的類別應該具有相同名稱的實體連接字串，因此它將名稱變更為**MusicStoreEntities**然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eced9-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="eced9-197">![選擇資料連接](aspnet-mvc-4-models-and-data-access/_static/image10.png "選擇資料連接")</span><span class="sxs-lookup"><span data-stu-id="eced9-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="eced9-198">*選擇資料連接*</span><span class="sxs-lookup"><span data-stu-id="eced9-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="eced9-199">選擇要使用的資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="eced9-199">Choose the database objects to use.</span></span> <span data-ttu-id="eced9-200">因為實體模型將使用剛才資料庫的資料表，選取**資料表**選項，並確定**模型中包含外部索引鍵資料行**和**化或單數化產生物件名稱**選項也會一併選取。</span><span class="sxs-lookup"><span data-stu-id="eced9-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="eced9-201">若要將模型命名空間變更**MvcMusicStore.Model**然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="eced9-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="eced9-202">![選擇的資料庫物件](aspnet-mvc-4-models-and-data-access/_static/image11.png "選擇的資料庫物件")</span><span class="sxs-lookup"><span data-stu-id="eced9-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="eced9-203">*選擇的資料庫物件*</span><span class="sxs-lookup"><span data-stu-id="eced9-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-204">如果會顯示安全性警告對話方塊，按一下**確定**執行範本，並產生該模型實體的類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="eced9-205">將會建立個別的類別對應至資料庫的每個資料表實體的圖表資料庫將會出現。</span><span class="sxs-lookup"><span data-stu-id="eced9-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="eced9-206">例如，**專輯**資料表會由**專輯**類別，其中每個資料行的資料表中會對應至類別內容。</span><span class="sxs-lookup"><span data-stu-id="eced9-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="eced9-207">這可讓您查詢及處理物件，代表在資料庫中的資料列。</span><span class="sxs-lookup"><span data-stu-id="eced9-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="eced9-208">![實體圖表](aspnet-mvc-4-models-and-data-access/_static/image12.png "實體圖表")</span><span class="sxs-lookup"><span data-stu-id="eced9-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="eced9-209">*實體圖表*</span><span class="sxs-lookup"><span data-stu-id="eced9-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-210">T4 範本 (.tt) 執行程式碼來產生實體類別，並具有相同名稱將會覆寫現有的類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="eced9-211">在此範例中，類別&quot;專輯&quot;， &quot;Genre&quot;並&quot;演出者&quot;已覆寫產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="eced9-212">工作 3-建置應用程式</span><span class="sxs-lookup"><span data-stu-id="eced9-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="eced9-213">在這個工作中，您將會檢查，雖然模型產生已移除**專輯**， **Genre**並**演出者**模型類別專案成功建置使用新的資料模型類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="eced9-214">建置專案，方法是選取**建置**功能表項目，然後**建置 MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="eced9-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="eced9-215">![建置專案](aspnet-mvc-4-models-and-data-access/_static/image13.png "建置專案")</span><span class="sxs-lookup"><span data-stu-id="eced9-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="eced9-216">*建置專案*</span><span class="sxs-lookup"><span data-stu-id="eced9-216">*Building the project*</span></span>
2. <span data-ttu-id="eced9-217">專案建置成功。</span><span class="sxs-lookup"><span data-stu-id="eced9-217">The project builds successfully.</span></span> <span data-ttu-id="eced9-218">為什麼它仍在使用？</span><span class="sxs-lookup"><span data-stu-id="eced9-218">Why does it still work?</span></span> <span data-ttu-id="eced9-219">這是因為資料庫資料表有包含您所使用的屬性已移除的類別中的欄位**專輯**並**內容類型**。</span><span class="sxs-lookup"><span data-stu-id="eced9-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="eced9-220">![成功的組建](aspnet-mvc-4-models-and-data-access/_static/image14.png "成功的組建")</span><span class="sxs-lookup"><span data-stu-id="eced9-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="eced9-221">*組建成功*</span><span class="sxs-lookup"><span data-stu-id="eced9-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="eced9-222">雖然設計工具會以圖表格式顯示實體，但它們其實是 C# 類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="eced9-223">依序展開**StoreDB.edmx**方案總管 中的節點，然後**StoreDB.tt**，您會看到新產生的實體。</span><span class="sxs-lookup"><span data-stu-id="eced9-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="eced9-224">![產生的檔案](aspnet-mvc-4-models-and-data-access/_static/image15.png "產生的檔案")</span><span class="sxs-lookup"><span data-stu-id="eced9-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="eced9-225">*產生的檔案*</span><span class="sxs-lookup"><span data-stu-id="eced9-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="eced9-226">工作 4-查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="eced9-227">在這個工作中，您將會更新 StoreController 類別，以便不使用硬式編碼資料，它會查詢資料庫以擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="eced9-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="eced9-228">開啟**Controllers\StoreController.cs**並將下列欄位新增至類別，以保存的執行個體**MusicStoreEntities**類別，名為**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="eced9-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="eced9-229">(程式碼片段-*模型和資料存取-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="eced9-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="eced9-230">**MusicStoreEntities**類別會公開資料庫中的每個資料表的集合屬性。</span><span class="sxs-lookup"><span data-stu-id="eced9-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="eced9-231">更新**瀏覽**動作方法，來擷取所有的內容類型**專輯**。</span><span class="sxs-lookup"><span data-stu-id="eced9-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="eced9-232">(程式碼片段-*模型和資料存取-Ex1 存放區瀏覽*)</span><span class="sxs-lookup"><span data-stu-id="eced9-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="eced9-233">您使用的功能，稱為.NET **LINQ** (language integrated query) 撰寫強型別的查詢運算式，針對這些集合-將會執行對資料庫的程式碼，並傳回物件，您可以設計程式針對。</span><span class="sxs-lookup"><span data-stu-id="eced9-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="eced9-234">如需有關 LINQ 的詳細資訊，請瀏覽[msdn 網站](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eced9-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="eced9-235">更新**Index**動作方法，來擷取所有的內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="eced9-236">(程式碼片段-*模型和資料存取-Ex1 存放區索引*)</span><span class="sxs-lookup"><span data-stu-id="eced9-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="eced9-237">更新**Index**動作方法，來擷取所有的內容類型，並轉換為清單集合。</span><span class="sxs-lookup"><span data-stu-id="eced9-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="eced9-238">(程式碼片段-*模型和資料存取-Ex1 市集 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="eced9-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="eced9-239">工作 5-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="eced9-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="eced9-240">在這個工作中，您將會檢查存放區索引頁面現在會顯示儲存在資料庫中，而不是硬式編碼的內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="eced9-241">若要變更檢視範本，因為不需要**StoreController**傳回相同的實體和以前一樣，雖然這次的資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="eced9-242">重建方案，然後按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="eced9-243">專案一開始在首頁上。</span><span class="sxs-lookup"><span data-stu-id="eced9-243">The project starts in the Home page.</span></span> <span data-ttu-id="eced9-244">確認的功能表**內容類型**不再是硬式編碼清單，並直接從資料庫擷取資料。</span><span class="sxs-lookup"><span data-stu-id="eced9-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="eced9-246">*瀏覽的內容類型，從資料庫*</span><span class="sxs-lookup"><span data-stu-id="eced9-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="eced9-247">現在瀏覽至任何內容類型，並確認從資料庫填入相簿。</span><span class="sxs-lookup"><span data-stu-id="eced9-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="eced9-248">![從資料庫中瀏覽專輯](aspnet-mvc-4-models-and-data-access/_static/image17.png "瀏覽的專輯，從資料庫")</span><span class="sxs-lookup"><span data-stu-id="eced9-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="eced9-249">*從資料庫中瀏覽相簿*</span><span class="sxs-lookup"><span data-stu-id="eced9-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="eced9-250">練習 2:第一次使用的程式碼建立資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="eced9-251">在此練習中，您將了解如何使用 Code First 方法來建立資料庫資料表 MusicStore 應用程式，以及如何存取其資料。</span><span class="sxs-lookup"><span data-stu-id="eced9-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="eced9-252">一旦產生模型時，您將修改 StoreController 取自資料庫，而不是使用硬式編碼值的資料提供檢視範本。</span><span class="sxs-lookup"><span data-stu-id="eced9-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-253">如果您已完成練習 1，而且已經使用資料庫第一種方法，您現在將會了解如何取得相同的結果，以不同方式處理。</span><span class="sxs-lookup"><span data-stu-id="eced9-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="eced9-254">為了方便您讀取已標示和練習 1 相同的工作。</span><span class="sxs-lookup"><span data-stu-id="eced9-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="eced9-255">如果您有未完成練習 1，但想要了解 Code First 方法，您可以從這個練習中啟動，並取得主題的完整的涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="eced9-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="eced9-256">工作 1-填入範例資料</span><span class="sxs-lookup"><span data-stu-id="eced9-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="eced9-257">在這個工作中，您將資料庫中填入範例資料一開始建立使用 Code First 時。</span><span class="sxs-lookup"><span data-stu-id="eced9-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="eced9-258">開啟**開始**解決方案位於**來源/Ex2-CreatingADatabaseCodeFirst/開始/** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="eced9-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="eced9-259">否則，您可能會繼續使用**結束**方案取得完成前一個練習。</span><span class="sxs-lookup"><span data-stu-id="eced9-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="eced9-260">如果您開啟提供**開始**解決方案中，您必須下載某些缺少的 NuGet 封裝才能繼續。</span><span class="sxs-lookup"><span data-stu-id="eced9-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="eced9-261">若要這樣做，請按一下**專案**功能表，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="eced9-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="eced9-262">在 [**管理 NuGet 套件**] 對話方塊中，按一下**還原**才能下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="eced9-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="eced9-263">最後，按一下 建置方案**建置** | **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="eced9-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="eced9-264">使用 NuGet 的優點之一是，您不需要寄送您的專案中的所有程式庫專案縮小。</span><span class="sxs-lookup"><span data-stu-id="eced9-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="eced9-265">NuGet Power tools，藉由指定封裝版本在 Packages.config 檔案中，您將能夠下載所有必要的程式庫第一次執行專案。</span><span class="sxs-lookup"><span data-stu-id="eced9-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="eced9-266">這就是為什麼您必須在您開啟現有的方案從這個實驗室之後，執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="eced9-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="eced9-267">新增**SampleData.cs**的檔案**模型**資料夾。</span><span class="sxs-lookup"><span data-stu-id="eced9-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="eced9-268">若要這樣做，請以滑鼠右鍵按一下**模型**資料夾，指向**新增**，然後按一下 **現有項目**。</span><span class="sxs-lookup"><span data-stu-id="eced9-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="eced9-269">瀏覽至 **\Source\Assets** ，然後選取 **SampleData.cs** 檔案。</span><span class="sxs-lookup"><span data-stu-id="eced9-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="eced9-270">![範例資料填入程式碼](aspnet-mvc-4-models-and-data-access/_static/image18.png "範例資料填入程式碼")</span><span class="sxs-lookup"><span data-stu-id="eced9-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="eced9-271">*範例資料填入程式碼*</span><span class="sxs-lookup"><span data-stu-id="eced9-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="eced9-272">開啟**Global.asax.cs**檔案，並新增下列*使用*陳述式。</span><span class="sxs-lookup"><span data-stu-id="eced9-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="eced9-273">(程式碼片段-*模型和資料存取-Ex2 全域 Asax Using*)</span><span class="sxs-lookup"><span data-stu-id="eced9-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="eced9-274">在 **應用程式\_start （)** 方法中加入下列這一行加入設定的資料庫初始設定式。</span><span class="sxs-lookup"><span data-stu-id="eced9-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="eced9-275">(程式碼片段-*模型和資料存取-Ex2 全域 Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="eced9-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="eced9-276">工作 2-設定資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="eced9-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="eced9-277">既然您已新增資料庫至我們的專案，您將撰寫**Web.config**檔案的連接字串。</span><span class="sxs-lookup"><span data-stu-id="eced9-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="eced9-278">新增在連接字串**Web.config**。若要這樣做，請開啟**Web.config**專案根目錄，取代連接字串中的這一行以命名 DefaultConnection **&lt;connectionStrings&gt;** 區段：</span><span class="sxs-lookup"><span data-stu-id="eced9-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="eced9-279">![Web.config 檔案位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 檔案位置")</span><span class="sxs-lookup"><span data-stu-id="eced9-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="eced9-280">*Web.config 檔案位置*</span><span class="sxs-lookup"><span data-stu-id="eced9-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="eced9-281">工作 3-使用模型</span><span class="sxs-lookup"><span data-stu-id="eced9-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="eced9-282">既然您已經設定資料庫的連接，您將連結的模型與資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="eced9-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="eced9-283">在這個工作中，您將建立的類別，將會連結到使用 Code First 資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="eced9-284">請記住，有現存的 POCO 模型類別，應該加以修改。</span><span class="sxs-lookup"><span data-stu-id="eced9-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-285">如果您已完成練習 1 時，您會發現此步驟已執行精靈。</span><span class="sxs-lookup"><span data-stu-id="eced9-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="eced9-286">透過這種程式碼第一次，您將手動建立將會連結至資料實體的類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="eced9-287">開啟 POCO 模型類別**Genre**從**模型**專案資料夾，並包含執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="eced9-288">使用 int 屬性同名**GenreId**。</span><span class="sxs-lookup"><span data-stu-id="eced9-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="eced9-289">(程式碼片段-*模型和資料存取-Ex2 程式碼的第一個內容類型*)</span><span class="sxs-lookup"><span data-stu-id="eced9-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="eced9-290">若要使用 Code First 慣例，內容類型的類別必須將會自動偵測到主索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="eced9-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="eced9-291">您可以深入了解程式碼中的第一個慣例[msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eced9-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="eced9-292">現在，開啟 POCO 模型類別**專輯**從**模型**專案資料夾和包含外部索引鍵中，建立具有名稱的屬性**GenreId**並**ArtistId**。</span><span class="sxs-lookup"><span data-stu-id="eced9-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="eced9-293">這個類別已經**GenreId**主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="eced9-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="eced9-294">(程式碼片段-*模型和資料存取-Ex2 程式碼的第一張專輯*)</span><span class="sxs-lookup"><span data-stu-id="eced9-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="eced9-295">開啟 POCO 模型類別**演出者**，並包含**ArtistId**屬性。</span><span class="sxs-lookup"><span data-stu-id="eced9-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="eced9-296">(程式碼片段-*模型和資料存取-Ex2 程式碼的第一位演出者*)</span><span class="sxs-lookup"><span data-stu-id="eced9-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="eced9-297">以滑鼠右鍵按一下**模型**專案資料夾，然後選取**新增 |類別**。</span><span class="sxs-lookup"><span data-stu-id="eced9-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="eced9-298">將檔案命名**MusicStoreEntities.cs**。</span><span class="sxs-lookup"><span data-stu-id="eced9-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="eced9-299">然後，按一下 **新增。**</span><span class="sxs-lookup"><span data-stu-id="eced9-299">Then, click **Add.**</span></span>

    <span data-ttu-id="eced9-300">![加入類別](aspnet-mvc-4-models-and-data-access/_static/image20.png "加入類別")</span><span class="sxs-lookup"><span data-stu-id="eced9-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="eced9-301">*加入新項目*</span><span class="sxs-lookup"><span data-stu-id="eced9-301">*Adding a new item*</span></span>

    <span data-ttu-id="eced9-302">![新增 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "新增 class2")</span><span class="sxs-lookup"><span data-stu-id="eced9-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="eced9-303">*加入類別*</span><span class="sxs-lookup"><span data-stu-id="eced9-303">*Adding a class*</span></span>
5. <span data-ttu-id="eced9-304">開啟您剛才建立的類別**MusicStoreEntities.cs**，並包含命名空間**System.Data.Entity**並**System.Data.Entity.Infrastructure**。</span><span class="sxs-lookup"><span data-stu-id="eced9-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="eced9-305">取代類別宣告，來擴充**DbContext**類別： 宣告公用**DBSet**並覆寫**OnModelCreating**方法。</span><span class="sxs-lookup"><span data-stu-id="eced9-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="eced9-306">在此步驟之後，您會將連結您的模型使用 Entity Framework 的網域類別。</span><span class="sxs-lookup"><span data-stu-id="eced9-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="eced9-307">若要這樣做，請將類別的程式碼取代為下列：</span><span class="sxs-lookup"><span data-stu-id="eced9-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="eced9-308">(程式碼片段-*模型和資料存取-Ex2 程式碼的第一個 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="eced9-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="eced9-309">使用 Entity Framework **DbContext**並**DBSet**您將能夠查詢 POCO 類別內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="eced9-310">藉由擴充**OnModelCreating**方法，就中指定**程式碼**內容類型對應至資料庫資料表的方式。</span><span class="sxs-lookup"><span data-stu-id="eced9-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="eced9-311">您可以在這篇 msdn 文章中找到 DBContext 和 DBSet 的詳細資訊：[連結](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="eced9-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="eced9-312">工作 4-查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="eced9-313">在這個工作中，您將會更新 StoreController 類別，以便不使用硬式編碼資料，它將它從資料庫擷取。</span><span class="sxs-lookup"><span data-stu-id="eced9-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-314">這項工作是與啟動器相同之練習 1。</span><span class="sxs-lookup"><span data-stu-id="eced9-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="eced9-315">如果您已完成練習 1 您會發現這些步驟也在這兩種方法 (第一次資料庫或 Code first)。</span><span class="sxs-lookup"><span data-stu-id="eced9-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="eced9-316">它們是不同的模型中，會連結的資料，但存取資料的實體是透明的控制站。</span><span class="sxs-lookup"><span data-stu-id="eced9-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="eced9-317">開啟**Controllers\StoreController.cs**並將下列欄位新增至類別，以保存的執行個體**MusicStoreEntities**類別，名為**storeDB**:</span><span class="sxs-lookup"><span data-stu-id="eced9-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="eced9-318">(程式碼片段-*模型和資料存取-Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="eced9-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="eced9-319">**MusicStoreEntities**類別會公開資料庫中的每個資料表的集合屬性。</span><span class="sxs-lookup"><span data-stu-id="eced9-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="eced9-320">更新**瀏覽**動作方法，來擷取所有的內容類型**專輯**。</span><span class="sxs-lookup"><span data-stu-id="eced9-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="eced9-321">(程式碼片段-*模型和資料存取-Ex2 存放區瀏覽*)</span><span class="sxs-lookup"><span data-stu-id="eced9-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="eced9-322">您使用的功能，稱為.NET **LINQ** (language integrated query) 撰寫強型別的查詢運算式，針對這些集合-將會執行對資料庫的程式碼，並傳回物件，您可以設計程式針對。</span><span class="sxs-lookup"><span data-stu-id="eced9-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="eced9-323">如需有關 LINQ 的詳細資訊，請瀏覽[msdn 網站](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="eced9-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="eced9-324">更新**Index**動作方法，來擷取所有的內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="eced9-325">(程式碼片段-*模型和資料存取-Ex2 存放區索引*)</span><span class="sxs-lookup"><span data-stu-id="eced9-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="eced9-326">更新**Index**動作方法，來擷取所有的內容類型，並轉換為清單集合。</span><span class="sxs-lookup"><span data-stu-id="eced9-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="eced9-327">(程式碼片段-*模型和資料存取-Ex2 市集 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="eced9-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="eced9-328">工作 5-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="eced9-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="eced9-329">在這個工作中，您將會檢查存放區索引頁面現在會顯示儲存在資料庫中，而不是硬式編碼的內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="eced9-330">若要變更檢視範本，因為不需要**StoreController**會傳回相同**StoreIndexViewModel**如往常一般，但這次的資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="eced9-331">重建方案，然後按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="eced9-332">專案一開始在首頁上。</span><span class="sxs-lookup"><span data-stu-id="eced9-332">The project starts in the Home page.</span></span> <span data-ttu-id="eced9-333">確認的功能表**內容類型**不再是硬式編碼清單，並直接從資料庫擷取資料。</span><span class="sxs-lookup"><span data-stu-id="eced9-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="eced9-335">*瀏覽的內容類型，從資料庫*</span><span class="sxs-lookup"><span data-stu-id="eced9-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="eced9-336">現在瀏覽至任何內容類型，並確認從資料庫填入相簿。</span><span class="sxs-lookup"><span data-stu-id="eced9-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="eced9-337">![從資料庫中瀏覽專輯](aspnet-mvc-4-models-and-data-access/_static/image23.png "瀏覽的專輯，從資料庫")</span><span class="sxs-lookup"><span data-stu-id="eced9-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="eced9-338">*從資料庫中瀏覽相簿*</span><span class="sxs-lookup"><span data-stu-id="eced9-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="eced9-339">練習 3:查詢參數的資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="eced9-340">在這個練習中，您將學習如何查詢資料庫中使用參數，以及如何使用查詢結果成形，功能會減少數字的資料庫存取擷取資料以更有效率的方式。</span><span class="sxs-lookup"><span data-stu-id="eced9-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-341">如需查詢結果成形的詳細資訊，請造訪下列[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eced9-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="eced9-342">工作 1-修改 StoreController 從資料庫擷取相簿</span><span class="sxs-lookup"><span data-stu-id="eced9-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="eced9-343">在這個工作中，您會變更**StoreController**類別來存取資料庫，以擷取特定的內容類型中的專輯。</span><span class="sxs-lookup"><span data-stu-id="eced9-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="eced9-344">開啟**開始**解決方案位於**Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin**資料夾，如果您想要使用程式碼優先方法或**Source\Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin**資料夾，如果您想要使用資料庫優先方法。</span><span class="sxs-lookup"><span data-stu-id="eced9-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="eced9-345">否則，您可能會繼續使用**結束**方案取得完成前一個練習。</span><span class="sxs-lookup"><span data-stu-id="eced9-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="eced9-346">如果您開啟提供**開始**解決方案中，您必須下載某些缺少的 NuGet 封裝才能繼續。</span><span class="sxs-lookup"><span data-stu-id="eced9-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="eced9-347">若要這樣做，請按一下**專案**功能表，然後選取**管理 NuGet 套件**。</span><span class="sxs-lookup"><span data-stu-id="eced9-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="eced9-348">在 [**管理 NuGet 套件**] 對話方塊中，按一下**還原**才能下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="eced9-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="eced9-349">最後，按一下 建置方案**建置** | **建置方案**。</span><span class="sxs-lookup"><span data-stu-id="eced9-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="eced9-350">使用 NuGet 的優點之一是，您不需要寄送您的專案中的所有程式庫專案縮小。</span><span class="sxs-lookup"><span data-stu-id="eced9-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="eced9-351">NuGet Power tools，藉由指定封裝版本在 Packages.config 檔案中，您將能夠下載所有必要的程式庫第一次執行專案。</span><span class="sxs-lookup"><span data-stu-id="eced9-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="eced9-352">這就是為什麼您必須在您開啟現有的方案從這個實驗室之後，執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="eced9-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="eced9-353">開啟**StoreController**類別，以變更**瀏覽**動作方法。</span><span class="sxs-lookup"><span data-stu-id="eced9-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="eced9-354">若要這樣做，請在**方案總管**，展開**控制站**資料夾，然後按兩下**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="eced9-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="eced9-355">變更**瀏覽**動作方法，來擷取特定的內容類型的相簿。</span><span class="sxs-lookup"><span data-stu-id="eced9-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="eced9-356">若要這樣做，請取代下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="eced9-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="eced9-357">(程式碼片段-*模型和資料存取-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="eced9-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="eced9-358">若要填入實體的集合，您必須使用**Include**方法，以指定您想要太擷取的專輯。</span><span class="sxs-lookup"><span data-stu-id="eced9-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="eced9-359">您可以使用。**Single （)** LINQ 中的延伸模組因為在此情況下為 album 預期只有一個內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="eced9-360">**Single （)** 方法會採用 Lambda 運算式當做參數，而在此情況下，其名稱符合定義的值，指定單一的內容類型物件。</span><span class="sxs-lookup"><span data-stu-id="eced9-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="eced9-361">您會利用可讓您指出您想要在擷取的內容類型的物件時所一併載入其他相關的實體的功能。</span><span class="sxs-lookup"><span data-stu-id="eced9-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="eced9-362">這項功能稱為**查詢結果成形**，並可讓您減少存取資料庫，以擷取資訊所需的次數。</span><span class="sxs-lookup"><span data-stu-id="eced9-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="eced9-363">在此案例中，您會想要預先擷取的專輯，如您所擷取的內容類型。</span><span class="sxs-lookup"><span data-stu-id="eced9-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="eced9-364">此查詢包含**Genres.Include (&quot;專輯&quot;)** 以表示您想要相關的相簿。</span><span class="sxs-lookup"><span data-stu-id="eced9-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="eced9-365">這會導致更有效率的應用程式中，因為它會擷取在單一資料庫的要求中的內容類型和專輯資料。</span><span class="sxs-lookup"><span data-stu-id="eced9-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="eced9-366">工作 2-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="eced9-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="eced9-367">在這個工作中，您將執行應用程式，並從資料庫擷取的特定內容類型的相簿。</span><span class="sxs-lookup"><span data-stu-id="eced9-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="eced9-368">按下**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="eced9-369">專案一開始在首頁上。</span><span class="sxs-lookup"><span data-stu-id="eced9-369">The project starts in the Home page.</span></span> <span data-ttu-id="eced9-370">將 URL 變更為 **/Store/瀏覽？ 內容類型 = Pop**驗證，正在從資料庫擷取的結果。</span><span class="sxs-lookup"><span data-stu-id="eced9-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="eced9-371">![依內容類型瀏覽](aspnet-mvc-4-models-and-data-access/_static/image24.png "依內容類型瀏覽")</span><span class="sxs-lookup"><span data-stu-id="eced9-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="eced9-372">*瀏覽/Store/瀏覽？ 內容類型 = Pop*</span><span class="sxs-lookup"><span data-stu-id="eced9-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="eced9-373">工作 3-Id 所存取的相簿</span><span class="sxs-lookup"><span data-stu-id="eced9-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="eced9-374">在這個工作中，您將會重複先前的程序，以取得由其 id 的相簿</span><span class="sxs-lookup"><span data-stu-id="eced9-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="eced9-375">關閉瀏覽器，如有需要若要返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="eced9-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="eced9-376">開啟**StoreController**類別，以變更**詳細資料**動作方法。</span><span class="sxs-lookup"><span data-stu-id="eced9-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="eced9-377">若要這樣做，請在**方案總管**，展開**控制站**資料夾，然後按兩下**StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="eced9-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="eced9-378">變更**詳細資料**擷取專輯詳細資料的動作方法，根據其**識別碼**。若要這樣做，請取代下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="eced9-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="eced9-379">(程式碼片段-*模型和資料存取-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="eced9-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="eced9-380">工作 4-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="eced9-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="eced9-381">在這個工作中，您會在網頁瀏覽器中執行應用程式，並取得專輯詳細資料，其識別碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="eced9-382">按下**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="eced9-383">專案一開始在首頁上。</span><span class="sxs-lookup"><span data-stu-id="eced9-383">The project starts in the Home page.</span></span> <span data-ttu-id="eced9-384">將 URL 變更為 **/Store/Details/51**或瀏覽的內容類型，並選取驗證，正在從資料庫擷取的結果 album。</span><span class="sxs-lookup"><span data-stu-id="eced9-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="eced9-385">![瀏覽詳細資料](aspnet-mvc-4-models-and-data-access/_static/image25.png "瀏覽詳細資料")</span><span class="sxs-lookup"><span data-stu-id="eced9-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="eced9-386">*瀏覽 /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="eced9-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="eced9-387">此外，您可以在其中部署此應用程式以 Windows Azure 網站的下列[附錄 b:發行 ASP.NET MVC 4 應用程式使用 Web Deploy](#AppendixB)。</span><span class="sxs-lookup"><span data-stu-id="eced9-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="eced9-388">總結</span><span class="sxs-lookup"><span data-stu-id="eced9-388">Summary</span></span>

<span data-ttu-id="eced9-389">藉由完成這個實際操作實驗室，您已了解 ASP.NET MVC 模型和資料存取的基本概念、 使用**Database First**方法，以及**Code First**方法：</span><span class="sxs-lookup"><span data-stu-id="eced9-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="eced9-390">如何將資料庫加入至方案中，若要取用其資料</span><span class="sxs-lookup"><span data-stu-id="eced9-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="eced9-391">如何更新控制站，以提供取自資料庫而不是硬式編碼的資料檢視範本</span><span class="sxs-lookup"><span data-stu-id="eced9-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="eced9-392">如何查詢使用參數的資料庫</span><span class="sxs-lookup"><span data-stu-id="eced9-392">How to query the database using parameters</span></span>
- <span data-ttu-id="eced9-393">如何使用查詢結果形成的功能會減少資料庫存取數目，以更有效率的方式擷取資料</span><span class="sxs-lookup"><span data-stu-id="eced9-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="eced9-394">如何使用 Database First 和程式碼優先方法中，Microsoft Entity Framework 的模型資料庫連結</span><span class="sxs-lookup"><span data-stu-id="eced9-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="eced9-395">附錄 a:安裝 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="eced9-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="eced9-396">您可以安裝**Microsoft Visual Studio Express 2012 for Web**或另一個&quot;Express&quot;使用版本 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="eced9-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="eced9-397">下列指示會引導您完成安裝所需的步驟*Visual studio Express 2012 for Web*使用*Microsoft Web Platform Installer*。</span><span class="sxs-lookup"><span data-stu-id="eced9-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="eced9-398">移至[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="eced9-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="eced9-399">或者，如果您已安裝 Web Platform Installer，您可以開啟它，並搜尋產品&quot; <em>Visual Studio Express 2012 for Web 含 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="eced9-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="eced9-400">按一下 **立即安裝**。</span><span class="sxs-lookup"><span data-stu-id="eced9-400">Click on **Install Now**.</span></span> <span data-ttu-id="eced9-401">如果您不需要**Web Platform Installer**您將會重新導向至下載並安裝第一次。</span><span class="sxs-lookup"><span data-stu-id="eced9-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="eced9-402">一次**Web Platform Installer**已開啟，按一下**安裝**，啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="eced9-403">![安裝 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="eced9-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="eced9-404">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="eced9-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="eced9-405">閱讀所有產品的授權和詞彙，然後按一下**我接受**以繼續。</span><span class="sxs-lookup"><span data-stu-id="eced9-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="eced9-407">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="eced9-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="eced9-408">等候完成的下載與安裝程序。</span><span class="sxs-lookup"><span data-stu-id="eced9-408">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="eced9-410">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="eced9-410">*Installation progress*</span></span>
6. <span data-ttu-id="eced9-411">安裝完成時，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="eced9-411">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="eced9-413">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="eced9-413">*Installation completed*</span></span>
7. <span data-ttu-id="eced9-414">按一下 **結束**關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="eced9-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="eced9-415">若要開啟 Visual Studio Express for Web，請前往**開始**畫面，即可開始撰寫&quot; **VS Express**&quot;，然後按一下**VS Express for Web**圖格。</span><span class="sxs-lookup"><span data-stu-id="eced9-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 圖格](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="eced9-417">*VS Express for Web 圖格*</span><span class="sxs-lookup"><span data-stu-id="eced9-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="eced9-418">附錄 b:發行 ASP.NET MVC 4 應用程式使用 Web Deploy</span><span class="sxs-lookup"><span data-stu-id="eced9-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="eced9-419">本附錄將說明如何從 Windows Azure 管理入口網站中建立新的網站和發行您取得所遵循的實驗室中，利用 Web Deploy 發行功能的 Windows Azure 所提供的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="eced9-420">工作 1-建立新的網站，從 Windows Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eced9-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="eced9-421">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="eced9-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-422">使用 Windows Azure，您可以免費託管 10 個 ASP.NET 網站，並再隨著流量成長而調整。</span><span class="sxs-lookup"><span data-stu-id="eced9-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="eced9-423">您可以註冊申請[此處](https://aka.ms/aspnet-hol-azure)。</span><span class="sxs-lookup"><span data-stu-id="eced9-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="eced9-424">![登入 Windows Azure 入口網站](aspnet-mvc-4-models-and-data-access/_static/image31.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="eced9-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="eced9-425">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="eced9-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="eced9-426">按一下 **新增**命令列上。</span><span class="sxs-lookup"><span data-stu-id="eced9-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="eced9-427">![建立新的 Web 站台](aspnet-mvc-4-models-and-data-access/_static/image32.png "建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="eced9-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="eced9-428">*建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="eced9-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="eced9-429">按一下 **計算** | **網站**。</span><span class="sxs-lookup"><span data-stu-id="eced9-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="eced9-430">然後選取**快速建立**選項。</span><span class="sxs-lookup"><span data-stu-id="eced9-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="eced9-431">新的網站提供可用的 URL，然後按**建立網站**。</span><span class="sxs-lookup"><span data-stu-id="eced9-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-432">Windows Azure 網站時，您可以控制和管理雲端中執行的 web 應用程式的主應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="eced9-433">[快速建立] 選項可讓您部署已完成的 web 應用程式至 Windows Azure 網站從入口網站外部。</span><span class="sxs-lookup"><span data-stu-id="eced9-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="eced9-434">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="eced9-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="eced9-435">![建立新的網站上，使用 快速建立](aspnet-mvc-4-models-and-data-access/_static/image33.png "建立新的網站上，使用 快速建立")</span><span class="sxs-lookup"><span data-stu-id="eced9-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="eced9-436">*建立新的網站上，使用 快速建立*</span><span class="sxs-lookup"><span data-stu-id="eced9-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="eced9-437">等到新**網站**建立。</span><span class="sxs-lookup"><span data-stu-id="eced9-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="eced9-438">建立網站後按一下底下的連結**URL**資料行。</span><span class="sxs-lookup"><span data-stu-id="eced9-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="eced9-439">檢查新的網站運作。</span><span class="sxs-lookup"><span data-stu-id="eced9-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="eced9-440">![瀏覽至新的 web 站台](aspnet-mvc-4-models-and-data-access/_static/image34.png "瀏覽至新的網站")</span><span class="sxs-lookup"><span data-stu-id="eced9-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="eced9-441">*瀏覽至新的網站*</span><span class="sxs-lookup"><span data-stu-id="eced9-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="eced9-442">![執行的 web 站台](aspnet-mvc-4-models-and-data-access/_static/image35.png "執行的網站")</span><span class="sxs-lookup"><span data-stu-id="eced9-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="eced9-443">*執行的網站*</span><span class="sxs-lookup"><span data-stu-id="eced9-443">*Web site running*</span></span>
6. <span data-ttu-id="eced9-444">返回入口網站並按一下底下的網站名稱**名稱**資料行來顯示 [管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="eced9-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="eced9-445">![開啟 網站管理頁面](aspnet-mvc-4-models-and-data-access/_static/image36.png "開啟的網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="eced9-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="eced9-446">*開啟 網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="eced9-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="eced9-447">在 **儀表板**頁面的 **快速概覽**區段中，按一下**下載發行設定檔**連結。</span><span class="sxs-lookup"><span data-stu-id="eced9-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-448">*發行設定檔*包含所有發行至 Windows Azure 網站的每個已啟用的發行方法的 web 應用程式所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="eced9-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="eced9-449">發行設定檔包含 Url、 使用者認證和連接到並對每個發行集的方法已啟用的端點進行驗證所需的資料庫字串。</span><span class="sxs-lookup"><span data-stu-id="eced9-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="eced9-450">**Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**並**Microsoft Visual Studio 2012**支援讀取發行設定檔，以自動化的這些程式的組態正在發行至 Windows Azure 網站的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eced9-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="eced9-451">![正在下載網站發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image37.png "下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="eced9-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="eced9-452">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="eced9-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="eced9-453">下載發行設定檔至已知位置。</span><span class="sxs-lookup"><span data-stu-id="eced9-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="eced9-454">進一步在這個練習中，您會看到如何從 Visual Studio 的 web 應用程式至 Windows Azure 網站發行使用此檔案。</span><span class="sxs-lookup"><span data-stu-id="eced9-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="eced9-455">![儲存發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image38.png "儲存發佈設定檔")</span><span class="sxs-lookup"><span data-stu-id="eced9-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="eced9-456">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="eced9-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="eced9-457">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="eced9-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="eced9-458">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="eced9-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="eced9-459">如果您想要部署簡單的應用程式不會使用 SQL Server，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="eced9-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="eced9-460">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="eced9-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="eced9-461">您可以從您的訂用帳戶，在 Windows Azure Management 入口網站中檢視 SQL Database 伺服器**Sql Database** | **伺服器** | **伺服器儀表板**。</span><span class="sxs-lookup"><span data-stu-id="eced9-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="eced9-462">如果您沒有建立伺服器，您可以建立一個使用**新增**命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="eced9-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="eced9-463">請記下的**伺服器名稱和 URL、 系統管理員身分登入名稱和密碼**，如同您會在下一個工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="eced9-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="eced9-464">並未建立資料庫，因為它會建立在稍後的階段。</span><span class="sxs-lookup"><span data-stu-id="eced9-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="eced9-465">![SQL Database 伺服器儀表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 伺服器儀表板")</span><span class="sxs-lookup"><span data-stu-id="eced9-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="eced9-466">*SQL Database 伺服器儀表板*</span><span class="sxs-lookup"><span data-stu-id="eced9-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="eced9-467">下一個工作在您將測試資料庫連接，從 Visual Studio 中，因此您需要在伺服器的清單包含您的本機 IP 位址**允許的 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="eced9-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="eced9-468">若要這樣做，請按一下**設定**，選取的 IP 位址**目前的用戶端 IP 位址**並將它貼上**起始 IP 位址**並**結束 IP 位址**文字方塊中，然後按一下 [ ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eced9-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![新增用戶端 IP 位址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="eced9-470">*新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="eced9-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="eced9-471">一次**用戶端 IP 位址**新增至允許的 IP 位址清單中，按一下**儲存**來確認變更。</span><span class="sxs-lookup"><span data-stu-id="eced9-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="eced9-473">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="eced9-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="eced9-474">工作 3-發行 ASP.NET MVC 4 應用程式使用 Web Deploy</span><span class="sxs-lookup"><span data-stu-id="eced9-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="eced9-475">返回至 ASP.NET MVC 4 的方案。</span><span class="sxs-lookup"><span data-stu-id="eced9-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="eced9-476">在 **方案總管**，以滑鼠右鍵按一下網站專案，然後選取**發佈**。</span><span class="sxs-lookup"><span data-stu-id="eced9-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="eced9-477">![發行應用程式](aspnet-mvc-4-models-and-data-access/_static/image43.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="eced9-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="eced9-478">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="eced9-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="eced9-479">匯入發行設定檔儲存在第一項工作。</span><span class="sxs-lookup"><span data-stu-id="eced9-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="eced9-480">![匯入發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image44.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="eced9-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="eced9-481">*匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="eced9-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="eced9-482">按一下 **驗證連線**。</span><span class="sxs-lookup"><span data-stu-id="eced9-482">Click **Validate Connection**.</span></span> <span data-ttu-id="eced9-483">驗證完成後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="eced9-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eced9-484">一旦您看到 [驗證連線] 按鈕旁邊會出現綠色核取記號完成驗證。</span><span class="sxs-lookup"><span data-stu-id="eced9-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="eced9-485">![驗證連接](aspnet-mvc-4-models-and-data-access/_static/image45.png "驗證連線")</span><span class="sxs-lookup"><span data-stu-id="eced9-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="eced9-486">*驗證連接*</span><span class="sxs-lookup"><span data-stu-id="eced9-486">*Validating connection*</span></span>
4. <span data-ttu-id="eced9-487">在 **設定**頁面的 **資料庫**區段中，按一下您的資料庫連接文字方塊旁邊的按鈕 (也就是**DefaultConnection**)。</span><span class="sxs-lookup"><span data-stu-id="eced9-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="eced9-488">![Web 部署組態](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web 部署設定")</span><span class="sxs-lookup"><span data-stu-id="eced9-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="eced9-489">*Web 部署設定*</span><span class="sxs-lookup"><span data-stu-id="eced9-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="eced9-490">設定資料庫連線，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eced9-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="eced9-491">在 **伺服器名稱**輸入您使用 SQL Database 伺服器的 URL *tcp:* 前置詞。</span><span class="sxs-lookup"><span data-stu-id="eced9-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="eced9-492">在 **使用者名**輸入您的伺服器系統管理員身分登入名稱。</span><span class="sxs-lookup"><span data-stu-id="eced9-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="eced9-493">在 **密碼**輸入您的伺服器系統管理員身分登入密碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="eced9-494">輸入新的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="eced9-494">Type a new database name.</span></span>

     <span data-ttu-id="eced9-495">![設定目的地連接字串](aspnet-mvc-4-models-and-data-access/_static/image47.png "設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="eced9-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="eced9-496">*設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="eced9-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="eced9-497">然後按一下 [確定]。 </span><span class="sxs-lookup"><span data-stu-id="eced9-497">Then click **OK**.</span></span> <span data-ttu-id="eced9-498">當系統提示您建立資料庫時，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="eced9-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="eced9-499">![建立資料庫](aspnet-mvc-4-models-and-data-access/_static/image48.png "建立的資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="eced9-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="eced9-500">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="eced9-500">*Creating the database*</span></span>
7. <span data-ttu-id="eced9-501">您將用來連接至 Windows Azure 中的 SQL 資料庫的連接字串會顯示在文字方塊中的預設連線。</span><span class="sxs-lookup"><span data-stu-id="eced9-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="eced9-502">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="eced9-502">Then click **Next**.</span></span>

    <span data-ttu-id="eced9-503">![連接字串指向 SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "連接字串指向 SQL Database")</span><span class="sxs-lookup"><span data-stu-id="eced9-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="eced9-504">*連接字串指向 SQL Database*</span><span class="sxs-lookup"><span data-stu-id="eced9-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="eced9-505">在  **Preview**頁面上，按一下**發佈**。</span><span class="sxs-lookup"><span data-stu-id="eced9-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="eced9-506">![Web 應用程式發行](aspnet-mvc-4-models-and-data-access/_static/image50.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="eced9-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="eced9-507">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="eced9-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="eced9-508">當發行程序完成時，預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="eced9-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="eced9-509">附錄 c:使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="eced9-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="eced9-510">使用程式碼片段，您會有您需要在隨手可得的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="eced9-511">實驗室課程文件會告訴您完全時您可以使用它們，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="eced9-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="eced9-512">![若要將程式碼插入您的專案使用 Visual Studio 程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image51.png "程式碼插入您的專案使用 Visual Studio 程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="eced9-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="eced9-513">*若要將程式碼插入您的專案使用 Visual Studio 程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="eced9-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="eced9-514">***若要新增的程式碼片段，使用鍵盤 （僅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="eced9-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="eced9-515">將游標放在您想要插入的程式碼。</span><span class="sxs-lookup"><span data-stu-id="eced9-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="eced9-516">開始輸入程式碼片段名稱 （不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="eced9-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="eced9-517">觀看為 IntelliSense 會顯示相符的程式碼片段的名稱。</span><span class="sxs-lookup"><span data-stu-id="eced9-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="eced9-518">選取正確的程式碼片段 （或直到選取整個程式碼片段名稱時，保留 輸入）。</span><span class="sxs-lookup"><span data-stu-id="eced9-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="eced9-519">按下 Tab 鍵兩次的游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="eced9-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="eced9-520">![開始鍵入程式碼片段名稱](aspnet-mvc-4-models-and-data-access/_static/image52.png "開始輸入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="eced9-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="eced9-521">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="eced9-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="eced9-522">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="eced9-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="eced9-523">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="eced9-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="eced9-524">![再次按 Tab 鍵和程式碼片段會依序展開](aspnet-mvc-4-models-and-data-access/_static/image54.png "再次按 Tab 鍵和程式碼片段會展開")</span><span class="sxs-lookup"><span data-stu-id="eced9-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="eced9-525">*再次按 Tab 鍵和程式碼片段會展開*</span><span class="sxs-lookup"><span data-stu-id="eced9-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="eced9-526">***若要新增的程式碼片段，使用滑鼠 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="eced9-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="eced9-527">以滑鼠右鍵按一下您要插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="eced9-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="eced9-528">選取 **插入程式碼片段**後面**My Code Snippets**。</span><span class="sxs-lookup"><span data-stu-id="eced9-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="eced9-529">選擇相關的程式片段，從清單中，對它按一下。</span><span class="sxs-lookup"><span data-stu-id="eced9-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="eced9-530">![以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image55.png "以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="eced9-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="eced9-531">*以滑鼠右鍵按一下您要插入程式碼片段，然後選取 插入程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="eced9-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="eced9-532">![對它按一下挑選清單中，相關程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image56.png "對它按一下挑選清單中，相關程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="eced9-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="eced9-533">*對它按一下挑選清單中，相關程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="eced9-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
