---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 使用模型系結和 web forms 來抓取和顯示資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。 模型系結讓資料互動更為直接-.。。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: d5f1982196c5985b001ca42c2711174e036bb1ec
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240747"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="120a9-104">使用模型系結和 web forms 來抓取和顯示資料</span><span class="sxs-lookup"><span data-stu-id="120a9-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="120a9-105">本教學課程系列示範使用模型系結搭配 ASP.NET Web Forms 專案的基本層面。</span><span class="sxs-lookup"><span data-stu-id="120a9-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="120a9-106">模型系結可讓資料互動比處理資料來源物件（例如 ObjectDataSource 或 SqlDataSource）更直接。</span><span class="sxs-lookup"><span data-stu-id="120a9-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="120a9-107">此系列從簡介材料開始，並在稍後的教學課程中移至更先進的概念。</span><span class="sxs-lookup"><span data-stu-id="120a9-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="120a9-108">模型系結模式適用于任何資料存取技術。</span><span class="sxs-lookup"><span data-stu-id="120a9-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="120a9-109">在本教學課程中，您將使用 Entity Framework，但您可以使用最熟悉的資料存取技術。</span><span class="sxs-lookup"><span data-stu-id="120a9-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="120a9-110">從資料系結伺服器控制項（例如 GridView、ListView、DetailsView 或 FormView 控制項），您可以指定用來選取、更新、刪除及建立資料的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="120a9-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="120a9-111">在本教學課程中，您將指定 SelectMethod 的值。</span><span class="sxs-lookup"><span data-stu-id="120a9-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="120a9-112">在該方法中，您會提供用來抓取資料的邏輯。</span><span class="sxs-lookup"><span data-stu-id="120a9-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="120a9-113">在下一個教學課程中，您將設定 UpdateMethod、DeleteMethod 和 InsertMethod 的值。</span><span class="sxs-lookup"><span data-stu-id="120a9-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="120a9-114">您可以[下載](https://go.microsoft.com/fwlink/?LinkId=286116)c # 或 Visual Basic 中的完整專案。</span><span class="sxs-lookup"><span data-stu-id="120a9-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="120a9-115">可下載的程式碼適用于 Visual Studio 2012 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="120a9-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="120a9-116">它會使用 Visual Studio 2012 範本，這與本教學課程中所顯示的 Visual Studio 2017 範本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="120a9-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="120a9-117">在教學課程中，您會在 Visual Studio 中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="120a9-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="120a9-118">您也可以將應用程式部署至主機服務提供者，使其可透過網際網路使用。</span><span class="sxs-lookup"><span data-stu-id="120a9-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="120a9-119">Microsoft 提供免費的 web 主機服務，最多可達10個網站</span><span class="sxs-lookup"><span data-stu-id="120a9-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="120a9-120">[免費的 Azure 試用帳戶](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="120a9-120">[free Azure trial account](https://azure.microsoft.com/free/dotnet/).</span></span> <span data-ttu-id="120a9-121">如需如何將 Visual Studio Web 專案部署至 Azure App Service Web Apps 的詳細資訊，請參閱[使用 Visual Studio 系列的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="120a9-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="120a9-122">該教學課程也會示範如何使用 Entity Framework Code First 移轉將您的 SQL Server 資料庫部署至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="120a9-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="120a9-123">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="120a9-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="120a9-124">Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="120a9-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="120a9-125">本教學課程也適用于 Visual Studio 2012 和 Visual Studio 2013，但使用者介面和專案範本中有一些差異。</span><span class="sxs-lookup"><span data-stu-id="120a9-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="120a9-126">您將建立的內容</span><span class="sxs-lookup"><span data-stu-id="120a9-126">What you'll build</span></span>

<span data-ttu-id="120a9-127">在本教學課程中，您將會：</span><span class="sxs-lookup"><span data-stu-id="120a9-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="120a9-128">建立資料物件，以反映學生在課程中註冊的大學</span><span class="sxs-lookup"><span data-stu-id="120a9-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="120a9-129">從物件建立資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="120a9-129">Build database tables from the objects</span></span>
* <span data-ttu-id="120a9-130">以測試資料填入資料庫</span><span class="sxs-lookup"><span data-stu-id="120a9-130">Populate the database with test data</span></span>
* <span data-ttu-id="120a9-131">在 web 表單中顯示資料</span><span class="sxs-lookup"><span data-stu-id="120a9-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="120a9-132">建立專案</span><span class="sxs-lookup"><span data-stu-id="120a9-132">Create the project</span></span>

1. <span data-ttu-id="120a9-133">在 Visual Studio 2017 中，建立名為**ContosoUniversityModelBinding**的**ASP.NET Web 應用程式（.NET Framework）** 專案。</span><span class="sxs-lookup"><span data-stu-id="120a9-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![建立專案](retrieving-data/_static/image19.png)

2. <span data-ttu-id="120a9-135">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="120a9-135">Select **OK**.</span></span> <span data-ttu-id="120a9-136">選取範本的對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="120a9-136">The dialog box to select a template appears.</span></span>

   ![選取 web 表單](retrieving-data/_static/image3.png)

3. <span data-ttu-id="120a9-138">選取 [ **Web** form] 範本。</span><span class="sxs-lookup"><span data-stu-id="120a9-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="120a9-139">如有必要，請將驗證變更為**個別使用者帳戶**。</span><span class="sxs-lookup"><span data-stu-id="120a9-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="120a9-140">選取 [確定] 可建立專案。</span><span class="sxs-lookup"><span data-stu-id="120a9-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="120a9-141">修改網站外觀</span><span class="sxs-lookup"><span data-stu-id="120a9-141">Modify site appearance</span></span>

   <span data-ttu-id="120a9-142">進行一些變更，以自訂網站外觀。</span><span class="sxs-lookup"><span data-stu-id="120a9-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="120a9-143">開啟網站. Master 檔案。</span><span class="sxs-lookup"><span data-stu-id="120a9-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="120a9-144">變更標題以顯示**Contoso 大學**，而不是**我的 ASP.NET 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="120a9-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="120a9-145">將標題文字從 [**應用程式名稱**] 變更為 [ **Contoso 大學**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="120a9-146">將導覽標頭連結變更為適當的網站。</span><span class="sxs-lookup"><span data-stu-id="120a9-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="120a9-147">移除 [**關於**] 和 [**連絡人**] 的連結，改為連結至您將建立的 [**學生**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="120a9-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="120a9-148">儲存網站。</span><span class="sxs-lookup"><span data-stu-id="120a9-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="120a9-149">新增 web 表單以顯示學生資料</span><span class="sxs-lookup"><span data-stu-id="120a9-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="120a9-150">在**方案總管**中，以滑鼠右鍵按一下您的專案，然後依序選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="120a9-151">在 [**加入新專案**] 對話方塊中，選取 [**含有主版頁面的 Web 表單**] 範本，並將其命名為 [student **. .aspx**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![建立頁面](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="120a9-153">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="120a9-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="120a9-154">在 web 表單的主版頁面上，選取 [**網站. 主機**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="120a9-155">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="120a9-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="120a9-156">加入資料模型</span><span class="sxs-lookup"><span data-stu-id="120a9-156">Add the data model</span></span>

<span data-ttu-id="120a9-157">在 [**模型**] 資料夾中，新增名為**UniversityModels.cs**的類別。</span><span class="sxs-lookup"><span data-stu-id="120a9-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="120a9-158">以滑鼠右鍵按一下 [**模型**]，然後依序選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="120a9-159">[加入新項目] \*\*\*\* 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="120a9-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="120a9-160">從左側導覽功能表中，依序選取 [程式**代碼**] 和 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![建立模型類別](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="120a9-162">將類別命名為**UniversityModels.cs** ，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="120a9-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="120a9-163">在此檔案中，定義 `SchoolContext` 、 `Student` 、 `Enrollment` 和 `Course` 類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="120a9-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="120a9-164">`SchoolContext`類別衍生自 `DbContext` ，其會管理資料庫連接和資料中的變更。</span><span class="sxs-lookup"><span data-stu-id="120a9-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="120a9-165">在 `Student` 類別中，請注意套用至 `FirstName` 、 `LastName` 和屬性的屬性 `Year` 。</span><span class="sxs-lookup"><span data-stu-id="120a9-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="120a9-166">本教學課程會使用這些屬性來進行資料驗證。</span><span class="sxs-lookup"><span data-stu-id="120a9-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="120a9-167">為了簡化程式碼，只有這些屬性會以資料驗證屬性來標示。</span><span class="sxs-lookup"><span data-stu-id="120a9-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="120a9-168">在實際專案中，您會將驗證屬性套用至需要驗證的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="120a9-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="120a9-169">儲存 UniversityModels.cs。</span><span class="sxs-lookup"><span data-stu-id="120a9-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="120a9-170">根據類別設定資料庫</span><span class="sxs-lookup"><span data-stu-id="120a9-170">Set up the database based on classes</span></span>

<span data-ttu-id="120a9-171">本教學課程使用[Code First 移轉](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)來建立物件和資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="120a9-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="120a9-172">這些表格會儲存學生及其課程的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="120a9-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="120a9-173">選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="120a9-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="120a9-174">在 [**套件管理員主控台**] 中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="120a9-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="120a9-175">如果命令順利完成，就會出現訊息，指出已啟用 [遷移]。</span><span class="sxs-lookup"><span data-stu-id="120a9-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![啟用遷移](retrieving-data/_static/image8.png)

      <span data-ttu-id="120a9-177">請注意，已建立名為*Configuration.cs*的檔案。</span><span class="sxs-lookup"><span data-stu-id="120a9-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="120a9-178">`Configuration`類別具有 `Seed` 方法，可以預先填入含有測試資料的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="120a9-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="120a9-179">預先填入資料庫</span><span class="sxs-lookup"><span data-stu-id="120a9-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="120a9-180">開啟 Configuration.cs。</span><span class="sxs-lookup"><span data-stu-id="120a9-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="120a9-181">將下列程式碼新增至 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="120a9-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="120a9-182">此外，加入 `using` 命名空間的語句 `ContosoUniversityModelBinding. Models` 。</span><span class="sxs-lookup"><span data-stu-id="120a9-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="120a9-183">儲存 Configuration.cs。</span><span class="sxs-lookup"><span data-stu-id="120a9-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="120a9-184">在 [套件管理員主控台] 中，執行 [**新增-遷移初始**] 命令。</span><span class="sxs-lookup"><span data-stu-id="120a9-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="120a9-185">執行命令**update-database**。</span><span class="sxs-lookup"><span data-stu-id="120a9-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="120a9-186">如果您在執行此命令時收到例外狀況， `StudentID` 和 `CourseID` 值可能與 `Seed` 方法值不同。</span><span class="sxs-lookup"><span data-stu-id="120a9-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="120a9-187">開啟這些資料庫資料表，並尋找和的現有值 `StudentID` `CourseID` 。</span><span class="sxs-lookup"><span data-stu-id="120a9-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="120a9-188">將這些值新增至程式碼以植入 `Enrollments` 資料表。</span><span class="sxs-lookup"><span data-stu-id="120a9-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="120a9-189">新增 GridView 控制項</span><span class="sxs-lookup"><span data-stu-id="120a9-189">Add a GridView control</span></span>

<span data-ttu-id="120a9-190">填入資料庫資料之後，您就可以開始取出該資料並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="120a9-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="120a9-191">開啟 [student]。</span><span class="sxs-lookup"><span data-stu-id="120a9-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="120a9-192">找出 `MainContent` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="120a9-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="120a9-193">在該預留位置內，新增包含此程式碼的**GridView**控制項。</span><span class="sxs-lookup"><span data-stu-id="120a9-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="120a9-194">注意事項：</span><span class="sxs-lookup"><span data-stu-id="120a9-194">Things to note:</span></span>
   * <span data-ttu-id="120a9-195">請注意 `SelectMethod` GridView 元素中屬性的設定值。</span><span class="sxs-lookup"><span data-stu-id="120a9-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="120a9-196">這個值會指定用來抓取 GridView 資料的方法，您可以在下一個步驟中建立此資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="120a9-197">`ItemType`屬性會設定為稍 `Student` 早建立的類別。</span><span class="sxs-lookup"><span data-stu-id="120a9-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="120a9-198">此設定可讓您參考標記中的類別屬性。</span><span class="sxs-lookup"><span data-stu-id="120a9-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="120a9-199">例如， `Student` 類別具有名為的集合 `Enrollments` 。</span><span class="sxs-lookup"><span data-stu-id="120a9-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="120a9-200">您可以使用 `Item.Enrollments` 來抓取該集合，然後使用[LINQ 語法](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)來抓取每個學生的已註冊點數總和。</span><span class="sxs-lookup"><span data-stu-id="120a9-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="120a9-201">儲存 student .aspx。</span><span class="sxs-lookup"><span data-stu-id="120a9-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="120a9-202">加入程式碼以取出資料</span><span class="sxs-lookup"><span data-stu-id="120a9-202">Add code to retrieve data</span></span>

   <span data-ttu-id="120a9-203">在 student 程式碼後置檔案中，新增針對值所指定的方法 `SelectMethod` 。</span><span class="sxs-lookup"><span data-stu-id="120a9-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="120a9-204">開啟 Students.aspx.cs。</span><span class="sxs-lookup"><span data-stu-id="120a9-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="120a9-205">`using`為 `ContosoUniversityModelBinding. Models` 和 `System.Data.Entity` 命名空間新增語句。</span><span class="sxs-lookup"><span data-stu-id="120a9-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="120a9-206">新增您為指定的方法 `SelectMethod` ：</span><span class="sxs-lookup"><span data-stu-id="120a9-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="120a9-207">`Include`子句可改善查詢效能，但不是必要的。</span><span class="sxs-lookup"><span data-stu-id="120a9-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="120a9-208">如果沒有 `Include` 子句，就會使用消極式[*載入*](https://en.wikipedia.org/wiki/Lazy_loading)來抓取資料，這牽涉到每次取得相關資料時，將個別查詢傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="120a9-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="120a9-209">使用 `Include` 子句時，會使用積極式*載入*來抓取資料，這表示單一資料庫查詢會抓取所有相關資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="120a9-210">如果未使用相關資料，積極式載入會較不有效率，因為會抓取更多資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="120a9-211">不過，在此情況下，積極式載入會提供最佳效能，因為會顯示每筆記錄的相關資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="120a9-212">如需載入相關資料時的效能考慮的詳細資訊，請參閱[ASP.NET MVC 應用程式一文中的使用 Entity Framework 讀取相關資料](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)一節中的「**延遲」、「積極」和「明確載入相關資料**」一節。</span><span class="sxs-lookup"><span data-stu-id="120a9-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="120a9-213">根據預設，資料會依標示為索引鍵的屬性值進行排序。</span><span class="sxs-lookup"><span data-stu-id="120a9-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="120a9-214">您可以加入 `OrderBy` 子句來指定不同的排序值。</span><span class="sxs-lookup"><span data-stu-id="120a9-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="120a9-215">在此範例中，預設 `StudentID` 屬性用於排序。</span><span class="sxs-lookup"><span data-stu-id="120a9-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="120a9-216">在[排序、分頁及篩選資料](sorting-paging-and-filtering-data.md)一文中，使用者可以選取資料行進行排序。</span><span class="sxs-lookup"><span data-stu-id="120a9-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="120a9-217">儲存 Students.aspx.cs。</span><span class="sxs-lookup"><span data-stu-id="120a9-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="120a9-218">執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="120a9-218">Run your application</span></span> 

<span data-ttu-id="120a9-219">執行您的 web 應用程式（**F5**），然後流覽至 [**學生**] 頁面，其中會顯示下列內容：</span><span class="sxs-lookup"><span data-stu-id="120a9-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![顯示資料](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="120a9-221">自動產生模型系結方法</span><span class="sxs-lookup"><span data-stu-id="120a9-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="120a9-222">當您完成本教學課程系列時，您可以直接將教學課程中的程式碼複製到您的專案。</span><span class="sxs-lookup"><span data-stu-id="120a9-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="120a9-223">不過，這種方法的其中一個缺點是，您可能不會注意到 Visual Studio 所提供的功能會自動產生模型系結方法的程式碼。</span><span class="sxs-lookup"><span data-stu-id="120a9-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="120a9-224">當您處理自己的專案時，自動產生程式碼可以節省您的時間，並協助您瞭解如何執行作業。</span><span class="sxs-lookup"><span data-stu-id="120a9-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="120a9-225">本節說明自動程式碼產生功能。</span><span class="sxs-lookup"><span data-stu-id="120a9-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="120a9-226">此區段僅供參考，而且不包含您在專案中所需執行的任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="120a9-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="120a9-227">在 `SelectMethod` 標記程式碼中設定、、或屬性的值時 `UpdateMethod` `InsertMethod` `DeleteMethod` ，您可以選取 [**建立新方法**] 選項。</span><span class="sxs-lookup"><span data-stu-id="120a9-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![建立方法](retrieving-data/_static/image18.png)

<span data-ttu-id="120a9-229">Visual Studio 不僅會在程式碼後置中建立具有適當簽章的方法，也會產生可執行作業的實做程式碼。</span><span class="sxs-lookup"><span data-stu-id="120a9-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="120a9-230">如果您在 `ItemType` 使用自動程式碼產生功能之前先設定屬性，則產生的程式碼會使用該類型進行作業。</span><span class="sxs-lookup"><span data-stu-id="120a9-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="120a9-231">例如，設定 `UpdateMethod` 屬性時，會自動產生下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="120a9-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="120a9-232">同樣地，此程式碼不需要新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="120a9-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="120a9-233">在下一個教學課程中，您將會執行更新、刪除和加入新資料的方法。</span><span class="sxs-lookup"><span data-stu-id="120a9-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="120a9-234">摘要</span><span class="sxs-lookup"><span data-stu-id="120a9-234">Summary</span></span>

<span data-ttu-id="120a9-235">在本教學課程中，您已建立資料模型類別，並從這些類別產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="120a9-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="120a9-236">您已使用測試資料填入資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="120a9-236">You filled the database tables with test data.</span></span> <span data-ttu-id="120a9-237">您已使用模型系結來抓取資料庫中的資料，然後在 GridView 中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="120a9-238">在此系列的下一個[教學](updating-deleting-and-creating-data.md)課程中，您將會啟用更新、刪除和建立資料。</span><span class="sxs-lookup"><span data-stu-id="120a9-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="120a9-239">下一步</span><span class="sxs-lookup"><span data-stu-id="120a9-239">Next</span></span>](updating-deleting-and-creating-data.md)
