---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 教學課程：開始使用 Entity Framework 6 Code First 使用 MVC 5 |Microsoft Docs
description: 在此系列教學課程中，您將了解如何建置使用 Entity Framework 6 存取資料的 ASP.NET MVC 5 應用程式。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057965"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a><span data-ttu-id="d5e17-103">教學課程：開始使用 Entity Framework 6 Code First 使用 MVC 5</span><span class="sxs-lookup"><span data-stu-id="d5e17-103">Tutorial: Get Started with Entity Framework 6 Code First using MVC 5</span></span>

> [!NOTE]
> <span data-ttu-id="d5e17-104">對於新的開發，我們建議[ASP.NET Core Razor Pages](/aspnet/core/razor-pages)透過 ASP.NET MVC 控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="d5e17-104">For new development, we recommend [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) over ASP.NET MVC controllers and views.</span></span> <span data-ttu-id="d5e17-105">類似如下的教學課程系列的使用 Razor 頁面，請參閱[教學課程：開始使用 ASP.NET Core 中的 Razor Pages](/aspnet/core/tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-105">For a tutorial series similar to this one using Razor Pages, see [Tutorial: Get started with Razor Pages in ASP.NET Core](/aspnet/core/tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="d5e17-106">新的教學課程：</span><span class="sxs-lookup"><span data-stu-id="d5e17-106">The new tutorial:</span></span>
> * <span data-ttu-id="d5e17-107">比較容易學習。</span><span class="sxs-lookup"><span data-stu-id="d5e17-107">Is easier to follow.</span></span>
> * <span data-ttu-id="d5e17-108">提供更多 EF Core 最佳做法。</span><span class="sxs-lookup"><span data-stu-id="d5e17-108">Provides more EF Core best practices.</span></span>
> * <span data-ttu-id="d5e17-109">使用更有效率的查詢。</span><span class="sxs-lookup"><span data-stu-id="d5e17-109">Uses more efficient queries.</span></span>
> * <span data-ttu-id="d5e17-110">具有最新的 API。</span><span class="sxs-lookup"><span data-stu-id="d5e17-110">Is more current with the latest API.</span></span>
> * <span data-ttu-id="d5e17-111">涵蓋更多功能。</span><span class="sxs-lookup"><span data-stu-id="d5e17-111">Covers more features.</span></span>
> * <span data-ttu-id="d5e17-112">是新應用程式開發的建議方法。</span><span class="sxs-lookup"><span data-stu-id="d5e17-112">Is the preferred approach for new application development.</span></span>

<span data-ttu-id="d5e17-113">在此系列教學課程中，您將了解如何建置使用 Entity Framework 6 存取資料的 ASP.NET MVC 5 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e17-113">In this series of tutorials, you learn how to build an ASP.NET MVC 5 application that uses Entity Framework 6 for data access.</span></span> <span data-ttu-id="d5e17-114">本教學課程使用 Code First 的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d5e17-114">This tutorial uses the Code First workflow.</span></span> <span data-ttu-id="d5e17-115">如需有關如何選擇 Code First、 Database First 或 Model First 的資訊，請參閱[建立模型](/ef/ef6/modeling/)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-115">For information about how to choose between Code First, Database First, and Model First, see [Create a model](/ef/ef6/modeling/).</span></span>

<span data-ttu-id="d5e17-116">本教學課程系列會說明如何建立 Contoso 大學範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e17-116">This tutorial series explains how to build the Contoso University sample application.</span></span> <span data-ttu-id="d5e17-117">範例應用程式是簡單的大學網站。</span><span class="sxs-lookup"><span data-stu-id="d5e17-117">The sample application is a simple university website.</span></span> <span data-ttu-id="d5e17-118">有了它，您可以檢視和更新學生、 課程和講師資訊。</span><span class="sxs-lookup"><span data-stu-id="d5e17-118">With it, you can view and update student, course, and instructor information.</span></span> <span data-ttu-id="d5e17-119">以下是兩個您所建立的畫面：</span><span class="sxs-lookup"><span data-stu-id="d5e17-119">Here are two of the screens you create:</span></span>

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![編輯學生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="d5e17-122">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="d5e17-122">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5e17-123">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d5e17-123">Create an MVC web app</span></span>
> * <span data-ttu-id="d5e17-124">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="d5e17-124">Set up the site style</span></span>
> * <span data-ttu-id="d5e17-125">安裝 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d5e17-125">Install Entity Framework 6</span></span>
> * <span data-ttu-id="d5e17-126">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="d5e17-126">Create the data model</span></span>
> * <span data-ttu-id="d5e17-127">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="d5e17-127">Create the database context</span></span>
> * <span data-ttu-id="d5e17-128">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="d5e17-128">Initialize DB with test data</span></span>
> * <span data-ttu-id="d5e17-129">將 EF 6 設定為使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="d5e17-129">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="d5e17-130">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="d5e17-130">Create controller and views</span></span>
> * <span data-ttu-id="d5e17-131">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="d5e17-131">View the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5e17-132">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5e17-132">Prerequisites</span></span>

* [<span data-ttu-id="d5e17-133">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d5e17-133">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a><span data-ttu-id="d5e17-134">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d5e17-134">Create an MVC web app</span></span>

1. <span data-ttu-id="d5e17-135">開啟 Visual Studio 並建立C#web 專案使用**ASP.NET Web 應用程式 (.NET Framework)** 範本。</span><span class="sxs-lookup"><span data-stu-id="d5e17-135">Open Visual Studio and create a C# web project using the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="d5e17-136">將專案命名為*ContosoUniversity* ，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-136">Name the project *ContosoUniversity* and select **OK**.</span></span>

   ![在 Visual Studio 中新增專案對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. <span data-ttu-id="d5e17-138">在 **新增 ASP.NET Web 應用程式集 ContosoUniversity**，選取**MVC**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-138">In **New ASP.NET Web Application - ContosoUniversity**, select **MVC**.</span></span>

   ![新 web 應用程式 對話方塊在 Visual Studio 中](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > <span data-ttu-id="d5e17-140">根據預設，**驗證**選項設定為**不需要驗證**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-140">By default, the **Authentication** option is set to **No Authentication**.</span></span> <span data-ttu-id="d5e17-141">本教學課程中，web 應用程式不需要使用者登入。</span><span class="sxs-lookup"><span data-stu-id="d5e17-141">For this tutorial, the web app doesn't require users to sign in.</span></span> <span data-ttu-id="d5e17-142">此外，它不會限制存取權依據誰登入。</span><span class="sxs-lookup"><span data-stu-id="d5e17-142">Also, it doesn't restrict access based on who's signed in.</span></span>

1. <span data-ttu-id="d5e17-143">選取 [確定] 建立專案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-143">Select **OK** to create the project.</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="d5e17-144">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="d5e17-144">Set up the site style</span></span>

<span data-ttu-id="d5e17-145">一些簡單的變更會設定網站的功能表、配置和首頁。</span><span class="sxs-lookup"><span data-stu-id="d5e17-145">A few simple changes will set up the site menu, layout, and home page.</span></span>

1. <span data-ttu-id="d5e17-146">開啟*Views\Shared\\_Layout.cshtml*，並進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="d5e17-146">Open *Views\Shared\\_Layout.cshtml*, and make the following changes:</span></span>

   - <span data-ttu-id="d5e17-147">將每個出現的"My ASP.NET Application"和"Application name"變更為"Contoso University"。</span><span class="sxs-lookup"><span data-stu-id="d5e17-147">Change each occurrence of "My ASP.NET Application" and "Application name" to "Contoso University".</span></span>
   - <span data-ttu-id="d5e17-148">新增功能表項目為學生、 課程、 講師和部門，並刪除連絡人項目。</span><span class="sxs-lookup"><span data-stu-id="d5e17-148">Add menu entries for Students, Courses, Instructors, and Departments, and delete the Contact entry.</span></span>

   <span data-ttu-id="d5e17-149">下列程式碼片段中，會反白顯示所做的變更：</span><span class="sxs-lookup"><span data-stu-id="d5e17-149">The changes are highlighted in the following code snippet:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. <span data-ttu-id="d5e17-150">在  *Views\Home\Index.cshtml*，檔案的內容取代為下列的程式碼，以使用關於此應用程式的文字取代關於 ASP.NET 和 MVC 的文字：</span><span class="sxs-lookup"><span data-stu-id="d5e17-150">In *Views\Home\Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. <span data-ttu-id="d5e17-151">按下 Ctrl + F5 來執行網站。</span><span class="sxs-lookup"><span data-stu-id="d5e17-151">Press Ctrl+F5 to run the web site.</span></span> <span data-ttu-id="d5e17-152">您會看到與主功能表的 [首頁] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d5e17-152">You see the home page with the main menu.</span></span>

## <a name="install-entity-framework-6"></a><span data-ttu-id="d5e17-153">安裝 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d5e17-153">Install Entity Framework 6</span></span>

1. <span data-ttu-id="d5e17-154">從**工具**功能表上，選擇**NuGet 套件管理員**，然後選擇**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-154">From the **Tools** menu, choose **NuGet Package Manager**, and then choose **Package Manager Console**.</span></span>

2. <span data-ttu-id="d5e17-155">在 [ **Package Manager Console** ] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5e17-155">In the **Package Manager Console** window, enter the following command:</span></span>

   ```text
   Install-Package EntityFramework
   ```

<span data-ttu-id="d5e17-156">這個步驟是，本教學課程有您手動執行，但是，無法在完成自動由 ASP.NET MVC 樣板功能的幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="d5e17-156">This step is one of a few steps that this tutorial has you do manually, but that could have been done automatically by the ASP.NET MVC scaffolding feature.</span></span> <span data-ttu-id="d5e17-157">您的所作所為它們以手動方式，讓您可以看到使用 Entity Framework (EF) 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="d5e17-157">You're doing them manually so that you can see the steps required to use Entity Framework (EF).</span></span> <span data-ttu-id="d5e17-158">您將更新版本使用 scaffolding 建立 MVC 控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="d5e17-158">You'll use scaffolding later to create the MVC controller and views.</span></span> <span data-ttu-id="d5e17-159">替代方法是讓 scaffolding 自動安裝 EF NuGet 套件、 建立資料庫內容類別，以及建立連接字串。</span><span class="sxs-lookup"><span data-stu-id="d5e17-159">An alternative is to let scaffolding automatically install the EF NuGet package, create the database context class, and create the connection string.</span></span> <span data-ttu-id="d5e17-160">當您準備好這麼這樣一來時，您只需要為略過這些步驟，並在您建立實體類別之後，建立 MVC 控制器的結構。</span><span class="sxs-lookup"><span data-stu-id="d5e17-160">When you're ready to do it that way, all you have to do is skip those steps and scaffold your MVC controller after you create your entity classes.</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="d5e17-161">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="d5e17-161">Create the data model</span></span>

<span data-ttu-id="d5e17-162">接下來您會為 Contoso 大學應用程式建立實體類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-162">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="d5e17-163">您首先要使用下列三個實體：</span><span class="sxs-lookup"><span data-stu-id="d5e17-163">You'll start with the following three entities:</span></span>

<span data-ttu-id="d5e17-164">**Course** <-> **註冊** <-> **學生**</span><span class="sxs-lookup"><span data-stu-id="d5e17-164">**Course** <-> **Enrollment** <-> **Student**</span></span>

| <span data-ttu-id="d5e17-165">實體</span><span class="sxs-lookup"><span data-stu-id="d5e17-165">Entities</span></span> | <span data-ttu-id="d5e17-166">Relationship</span><span class="sxs-lookup"><span data-stu-id="d5e17-166">Relationship</span></span> |
| -------- | ------------ |
| <span data-ttu-id="d5e17-167">課程來註冊</span><span class="sxs-lookup"><span data-stu-id="d5e17-167">Course to Enrollment</span></span> | <span data-ttu-id="d5e17-168">一對多</span><span class="sxs-lookup"><span data-stu-id="d5e17-168">One-to-many</span></span> |
| <span data-ttu-id="d5e17-169">若要註冊的學生</span><span class="sxs-lookup"><span data-stu-id="d5e17-169">Student to Enrollment</span></span> | <span data-ttu-id="d5e17-170">一對多</span><span class="sxs-lookup"><span data-stu-id="d5e17-170">One-to-many</span></span> |

<span data-ttu-id="d5e17-171">在 `Student` 和 `Enrollment` 實體之間存在一對多關聯性，`Course` 與 `Enrollment` 實體之間也存在一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-171">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="d5e17-172">換句話說，一位學生可以註冊並參加任何數目的課程，而一個課程也可以有任何數目的學生註冊。</span><span class="sxs-lookup"><span data-stu-id="d5e17-172">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="d5e17-173">在下列章節中，您將建立這些實體的每個類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-173">In the following sections, you'll create a class for each one of these entities.</span></span>

> [!NOTE]
> <span data-ttu-id="d5e17-174">如果您嘗試編譯專案，才能完成建立所有這些實體類別時，您會收到編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5e17-174">If you try to compile the project before you finish creating all of these entity classes, you'll get compiler errors.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="d5e17-175">Student 實體</span><span class="sxs-lookup"><span data-stu-id="d5e17-175">The Student entity</span></span>

- <span data-ttu-id="d5e17-176">在*模型*資料夾中，建立名為的類別檔案*Student.cs*中的資料夾上按一下滑鼠右鍵**方案總管 中**，然後選擇**新增**  > **類別**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-176">In the *Models* folder, create a class file named *Student.cs* by right-clicking on the folder in **Solution Explorer** and choosing **Add** > **Class**.</span></span> <span data-ttu-id="d5e17-177">使用下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5e17-177">Replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="d5e17-178">`ID` 屬性會成為資料庫資料表中的主索引鍵資料行，並對應至這個類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-178">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="d5e17-179">根據預設，Entity Framework 的屬性解譯，稱為`ID`或是*classname* `ID`為主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d5e17-179">By default, Entity Framework interprets a property that's named `ID` or *classname* `ID` as the primary key.</span></span>

<span data-ttu-id="d5e17-180">`Enrollments` 屬性為*導覽屬性*。</span><span class="sxs-lookup"><span data-stu-id="d5e17-180">The `Enrollments` property is a *navigation property*.</span></span> <span data-ttu-id="d5e17-181">導覽屬性會保留與此實體相關的其他實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-181">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="d5e17-182">在此情況下，`Enrollments`的屬性`Student`實體將保存的所有`Enrollment`相關的實體`Student`實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-182">In this case, the `Enrollments` property of a `Student` entity will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="d5e17-183">換句話說，如果給定`Student`資料庫中的資料列有兩個相關`Enrollment`資料列 (包含該學生的主索引鍵的資料列中的值及其`StudentID`外部索引鍵資料行)，該`Student`實體的`Enrollments`導覽屬性將包含這兩個`Enrollment`實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-183">In other words, if a given `Student` row in the database has two related `Enrollment` rows (rows that contain that student's primary key value in their `StudentID` foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="d5e17-184">導覽屬性通常會定義為`virtual`，讓他們可以利用某些 Entity Framework 功能這類*消極式載入*。</span><span class="sxs-lookup"><span data-stu-id="d5e17-184">Navigation properties are typically defined as `virtual` so that they can take advantage of certain Entity Framework functionality such as *lazy loading*.</span></span> <span data-ttu-id="d5e17-185">(將會說明消極式載入稍後，在[讀取相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)稍後在本系列教學課程。)</span><span class="sxs-lookup"><span data-stu-id="d5e17-185">(Lazy loading will be explained later, in the [Reading Related Data](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series.)</span></span>

<span data-ttu-id="d5e17-186">若導覽屬性可保有多個實體 (例如在多對多或一對多關聯性中的情況)，其類型必須為一個清單，使得實體可以在該清單中新增、刪除或更新，例如 `ICollection`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-186">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection`.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="d5e17-187">Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="d5e17-187">The Enrollment entity</span></span>

- <span data-ttu-id="d5e17-188">在 *Models* 資料夾中，建立 *Enrollment.cs*，然後使用下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5e17-188">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="d5e17-189">`EnrollmentID`屬性會是主索引鍵，此實體會使用*classname* `ID`模式，而非`ID`本身為您在看到`Student`實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-189">The `EnrollmentID` property will be the primary key; this entity uses the *classname* `ID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="d5e17-190">通常您會選擇一個模式，然後在您整個資料模型中使用此模式。</span><span class="sxs-lookup"><span data-stu-id="d5e17-190">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="d5e17-191">在這裡，此變化僅作為向您展示使用不同模式之用。</span><span class="sxs-lookup"><span data-stu-id="d5e17-191">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="d5e17-192">在稍後的教學課程中，您會看到如何使用`ID`而不需要`classname`更輕鬆地在資料模型中實作繼承。</span><span class="sxs-lookup"><span data-stu-id="d5e17-192">In a later tutorial, you'll see how using `ID` without `classname` makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="d5e17-193">`Grade`屬性是[列舉](/ef/ef6/modeling/code-first/data-types/enums)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-193">The `Grade` property is an [enum](/ef/ef6/modeling/code-first/data-types/enums).</span></span> <span data-ttu-id="d5e17-194">問號之後`Grade`型別宣告表示`Grade`屬性是[可為 null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-194">The question mark after the `Grade` type declaration indicates that the `Grade` property is [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types).</span></span> <span data-ttu-id="d5e17-195">為 null 的成績等級是不同於成績為零： null 表示成績未知或尚未指派。</span><span class="sxs-lookup"><span data-stu-id="d5e17-195">A grade that's null is different from a zero grade — null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="d5e17-196">`StudentID` 屬性是外部索引鍵，對應的導覽屬性是 `Student`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-196">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="d5e17-197">`Enrollment` 實體與一個 `Student` 實體關聯，因此屬性僅能保有單一 `Student` 實體 (不像您先前看到的 `Student.Enrollments` 導覽屬性可保有多個 `Enrollment` 實體)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-197">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="d5e17-198">`CourseID` 屬性是外部索引鍵，對應的導覽屬性是 `Course`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-198">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="d5e17-199">一個 `Enrollment` 實體與一個 `Course` 實體建立關聯。</span><span class="sxs-lookup"><span data-stu-id="d5e17-199">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="d5e17-200">Entity Framework 的屬性解譯為外部索引鍵屬性是否將它命名 *&lt;導覽屬性名稱&gt;&lt;主索引鍵屬性名稱&gt;* (例如`StudentID`for`Student`導覽屬性，因為`Student`實體的主索引鍵是`ID`)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-200">Entity Framework interprets a property as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="d5e17-201">外部索引鍵屬性也可以命名相同只要 *&lt;主索引鍵屬性名稱&gt;* (例如`CourseID`因為`Course`實體的主索引鍵是`CourseID`)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-201">Foreign key properties can also be named the same simply *&lt;primary key property name&gt;* (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="d5e17-202">Course 實體</span><span class="sxs-lookup"><span data-stu-id="d5e17-202">The Course entity</span></span>

- <span data-ttu-id="d5e17-203">在 *模型*資料夾中，建立*Course.cs*，以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5e17-203">In the *Models* folder, create *Course.cs*, replacing the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="d5e17-204">`Enrollments` 屬性為導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-204">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="d5e17-205">`Course` 實體可以與任何數量的 `Enrollment` 實體相關。</span><span class="sxs-lookup"><span data-stu-id="d5e17-205">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="d5e17-206">我們將進一步討論<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute>在稍後的教學課程中，在這一系列的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-206">We'll say more about the <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> attribute in a later tutorial in this series.</span></span> <span data-ttu-id="d5e17-207">基本上，此屬性可讓您為課程輸入主索引鍵，而非讓資料庫產生它。</span><span class="sxs-lookup"><span data-stu-id="d5e17-207">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="d5e17-208">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="d5e17-208">Create the database context</span></span>

<span data-ttu-id="d5e17-209">協調 Entity Framework 功能，為指定的資料模型的主要類別是*資料庫內容*類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-209">The main class that coordinates Entity Framework functionality for a given data model is the *database context* class.</span></span> <span data-ttu-id="d5e17-210">您建立這個類別衍生自[System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-210">You create this class by deriving from the [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) class.</span></span> <span data-ttu-id="d5e17-211">在您的程式碼中，您可以指定資料模型中包含哪些實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-211">In your code, you specify which entities are included in the data model.</span></span> <span data-ttu-id="d5e17-212">您也可以自訂某些 Entity Framework 行為。</span><span class="sxs-lookup"><span data-stu-id="d5e17-212">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="d5e17-213">在此專案中，類別命名為 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-213">In this project, the class is named `SchoolContext`.</span></span>

- <span data-ttu-id="d5e17-214">ContosoUniversity 專案中建立資料夾，請以滑鼠右鍵按一下專案中的**方案總管**，按一下 **新增**，然後按一下**新資料夾**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-214">To create a folder in the ContosoUniversity project, right-click the project in **Solution Explorer** and click **Add**, and then click **New Folder**.</span></span> <span data-ttu-id="d5e17-215">將新資料夾命名*DAL* （適用於資料存取層）。</span><span class="sxs-lookup"><span data-stu-id="d5e17-215">Name the new folder *DAL* (for Data Access Layer).</span></span> <span data-ttu-id="d5e17-216">在該資料夾中，建立新的類別檔案，名為*SchoolContext.cs*，並以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="d5e17-216">In that folder, create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a><span data-ttu-id="d5e17-217">指定實體集</span><span class="sxs-lookup"><span data-stu-id="d5e17-217">Specify entity sets</span></span>

<span data-ttu-id="d5e17-218">此程式碼會建立[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)每一個實體集的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-218">This code creates a [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) property for each entity set.</span></span> <span data-ttu-id="d5e17-219">在 Entity Framework 詞彙*實體集*通常會對應到資料庫資料表，以及*實體*對應至資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="d5e17-219">In Entity Framework terminology, an *entity set* typically corresponds to a database table, and an *entity* corresponds to a row in the table.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d5e17-220">您可以省略`DbSet<Enrollment>`和`DbSet<Course>`陳述式和它的運作。</span><span class="sxs-lookup"><span data-stu-id="d5e17-220">You can omit the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="d5e17-221">Entity Framework 會隱含它們，因為`Student`odkazy`Enrollment`實體並`Enrollment`實體參考`Course`實體。</span><span class="sxs-lookup"><span data-stu-id="d5e17-221">Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

### <a name="specify-the-connection-string"></a><span data-ttu-id="d5e17-222">指定的連接字串</span><span class="sxs-lookup"><span data-stu-id="d5e17-222">Specify the connection string</span></span>

<span data-ttu-id="d5e17-223">連接字串 （其中您稍後會加入至 Web.config 檔案） 的名稱會傳遞至建構函式。</span><span class="sxs-lookup"><span data-stu-id="d5e17-223">The name of the connection string (which you'll add to the Web.config file later) is passed in to the constructor.</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

<span data-ttu-id="d5e17-224">您也可以傳入連接字串而不是儲存在 Web.config 檔案中的其中一個的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5e17-224">You could also pass in the connection string itself instead of the name of one that is stored in the Web.config file.</span></span> <span data-ttu-id="d5e17-225">如需使用指定的資料庫選項的詳細資訊，請參閱[連接字串和模型](/ef/ef6/fundamentals/configuring/connection-strings)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-225">For more information about options for specifying the database to use, see [Connection strings and models](/ef/ef6/fundamentals/configuring/connection-strings).</span></span>

<span data-ttu-id="d5e17-226">如果您未指定連接字串或其中一個名稱明確，Entity Framework 會假設此連接字串名稱是類別名稱相同。</span><span class="sxs-lookup"><span data-stu-id="d5e17-226">If you don't specify a connection string or the name of one explicitly, Entity Framework assumes that the connection string name is the same as the class name.</span></span> <span data-ttu-id="d5e17-227">在此範例中的預設連接字串名稱就得`SchoolContext`，等同於您要明確指定。</span><span class="sxs-lookup"><span data-stu-id="d5e17-227">The default connection string name in this example would then be `SchoolContext`, the same as what you're specifying explicitly.</span></span>

### <a name="specify-singular-table-names"></a><span data-ttu-id="d5e17-228">指定單數資料表名稱</span><span class="sxs-lookup"><span data-stu-id="d5e17-228">Specify singular table names</span></span>

<span data-ttu-id="d5e17-229">`modelBuilder.Conventions.Remove`中的陳述式[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法會防止資料表名稱的複數化。</span><span class="sxs-lookup"><span data-stu-id="d5e17-229">The `modelBuilder.Conventions.Remove` statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method prevents table names from being pluralized.</span></span> <span data-ttu-id="d5e17-230">如果您沒有這麼做，在資料庫中產生的資料表就會命名為`Students`， `Courses`，和`Enrollments`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-230">If you didn't do this, the generated tables in the database would be named `Students`, `Courses`, and `Enrollments`.</span></span> <span data-ttu-id="d5e17-231">相反地，資料表名稱會`Student`， `Course`，和`Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="d5e17-231">Instead, the table names will be `Student`, `Course`, and `Enrollment`.</span></span> <span data-ttu-id="d5e17-232">針對是否要複數化資料表名稱，開發人員並沒有共識。</span><span class="sxs-lookup"><span data-stu-id="d5e17-232">Developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="d5e17-233">本教學課程使用的單數形式，但很重要的一點是，您可以選取任何您想要包含或省略這行程式碼的表單。</span><span class="sxs-lookup"><span data-stu-id="d5e17-233">This tutorial uses the singular form, but the important point is that you can select whichever form you prefer by including or omitting this line of code.</span></span>

## <a name="initialize-db-with-test-data"></a><span data-ttu-id="d5e17-234">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="d5e17-234">Initialize DB with test data</span></span>

<span data-ttu-id="d5e17-235">Entity Framework 可以自動建立 （或卸除並重新建立） 為您的應用程式執行時的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-235">Entity Framework can automatically create (or drop and re-create) a database for you when the application runs.</span></span> <span data-ttu-id="d5e17-236">您可以指定每次執行應用程式，或此模型會與現有的資料庫同步處理時，才，應該完成這。</span><span class="sxs-lookup"><span data-stu-id="d5e17-236">You can specify that this should be done every time your application runs or only when the model is out of sync with the existing database.</span></span> <span data-ttu-id="d5e17-237">您也可以撰寫`Seed`方法，Entity Framework 會自動呼叫之後才能填入測試資料建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-237">You can also write a `Seed` method that Entity Framework automatically calls after creating the database in order to populate it with test data.</span></span>

<span data-ttu-id="d5e17-238">預設行為是建立資料庫，如果它不存在 （且擲回例外狀況，如果模型已變更，而且資料庫已經存在）。</span><span class="sxs-lookup"><span data-stu-id="d5e17-238">The default behavior is to create a database only if it doesn't exist (and throw an exception if the model has changed and the database already exists).</span></span> <span data-ttu-id="d5e17-239">在本節中，您會指定資料庫應該卸除並重新建立每次模型變更時。</span><span class="sxs-lookup"><span data-stu-id="d5e17-239">In this section, you'll specify that the database should be dropped and re-created whenever the model changes.</span></span> <span data-ttu-id="d5e17-240">卸除資料庫時，會造成您的所有資料遺失。</span><span class="sxs-lookup"><span data-stu-id="d5e17-240">Dropping the database causes the loss of all your data.</span></span> <span data-ttu-id="d5e17-241">這通常是好在開發期間，因為`Seed`資料庫重新建立，而且將會重新建立您的測試資料時，會執行方法。</span><span class="sxs-lookup"><span data-stu-id="d5e17-241">This is generally okay during development, because the `Seed` method will run when the database is re-created and will re-create your test data.</span></span> <span data-ttu-id="d5e17-242">但在生產環境中通常不想遺失所有資料，每當您需要變更資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="d5e17-242">But in production you generally don't want to lose all your data every time you need to change the database schema.</span></span> <span data-ttu-id="d5e17-243">稍後您會看到如何使用 Code First 移轉來變更資料庫結構描述，而不是卸除並重新建立資料庫來處理模型變更。</span><span class="sxs-lookup"><span data-stu-id="d5e17-243">Later you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

1. <span data-ttu-id="d5e17-244">在 DAL 資料夾中，建立新的類別檔案，名為*SchoolInitializer.cs*會使資料庫建立時所需的下列程式碼取代範本程式碼和測試資料載入至新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-244">In the DAL folder, create a new class file named *SchoolInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="d5e17-245">`Seed`方法會採用資料庫內容物件做為輸入參數，並在方法中的程式碼會使用該物件來將新實體新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-245">The `Seed` method takes the database context object as an input parameter, and the code in the method uses that object to add new entities to the database.</span></span> <span data-ttu-id="d5e17-246">每個實體類型，程式碼會建立新實體的集合，將它們新增至適當`DbSet`屬性，然後按一下 儲存至資料庫的變更。</span><span class="sxs-lookup"><span data-stu-id="d5e17-246">For each entity type, the code creates a collection of new  entities, adds them to the appropriate `DbSet` property, and then saves the changes to the database.</span></span> <span data-ttu-id="d5e17-247">不需要呼叫`SaveChanges`實體的每一個群組之後的方法，做為在這裡，完成，但這麼做可協助您找出問題的來源，如果程式碼寫入資料庫時發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d5e17-247">It isn't necessary to call the `SaveChanges` method after each group of entities, as is done here, but doing that helps you locate the source of a problem if an exception occurs while the code is writing to the database.</span></span>

2. <span data-ttu-id="d5e17-248">若要告訴 Entity Framework 使用初始設定式類別，將新增項目`entityFramework`應用程式中的項目*Web.config*檔的檔案 （在根專案資料夾中），如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d5e17-248">To tell Entity Framework to use your initializer class, add an element to the `entityFramework` element in the application *Web.config* file (the one in the root project folder), as shown in the following example:</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   <span data-ttu-id="d5e17-249">`context type`指定完整的內容類別名稱和組件，而`databaseinitializer type`指定初始設定式類別和組件中的完整的名稱。</span><span class="sxs-lookup"><span data-stu-id="d5e17-249">The `context type` specifies the fully qualified context class name and the assembly it's in, and the `databaseinitializer type` specifies the fully qualified name of the initializer class and the assembly it's in.</span></span> <span data-ttu-id="d5e17-250">(當您不想要使用初始設定式的 EF 時，您可以設定屬性`context`項目： `disableDatabaseInitialization="true"`。)如需詳細資訊，請參閱 <<c0> [ 組態檔設定](/ef/ef6/fundamentals/configuring/config-file)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-250">(When you don't want EF to use the initializer, you can set an attribute on the `context` element: `disableDatabaseInitialization="true"`.) For more information, see [Configuration File Settings](/ef/ef6/fundamentals/configuring/config-file).</span></span>

   <span data-ttu-id="d5e17-251">設定初始設定式的替代方法*Web.config*檔案是要在程式碼中加上`Database.SetInitializer`陳述式來`Application_Start`中的方法*Global.asax.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-251">An alternative to setting the initializer in the *Web.config* file is to do it in code by adding a `Database.SetInitializer` statement to the `Application_Start` method in the *Global.asax.cs* file.</span></span> <span data-ttu-id="d5e17-252">如需詳細資訊，請參閱 <<c0> [ 了解在 Entity Framework Code First 資料庫初始設定式](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-252">For more information, see [Understanding Database Initializers in Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).</span></span>

<span data-ttu-id="d5e17-253">應用程式現在已設定，讓您存取資料庫一次執行應用程式的第一次時，Entity Framework 會比較模型資料庫 (您`SchoolContext`和實體類別)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-253">The application is now set up so that when you access the database for the first time in a given run of the application, Entity Framework compares the database to the model (your `SchoolContext` and entity classes).</span></span> <span data-ttu-id="d5e17-254">如果沒有差異，應用程式會卸除並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-254">If there's a difference, the application drops and re-creates the database.</span></span>

> [!NOTE]
> <span data-ttu-id="d5e17-255">當您部署在生產網頁伺服器應用程式時，您必須移除或停用程式碼，會卸除並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-255">When you deploy an application to a production web server, you must remove or disable code that drops and re-creates the database.</span></span> <span data-ttu-id="d5e17-256">您將在稍後的教學課程中，在這一系列來這麼做。</span><span class="sxs-lookup"><span data-stu-id="d5e17-256">You'll do that in a later tutorial in this series.</span></span>

## <a name="set-up-ef-6-to-use-localdb"></a><span data-ttu-id="d5e17-257">將 EF 6 設定為使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="d5e17-257">Set up EF 6 to use LocalDB</span></span>

<span data-ttu-id="d5e17-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)是輕量版的 SQL Server Express database engine。</span><span class="sxs-lookup"><span data-stu-id="d5e17-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) is a lightweight version of the SQL Server Express database engine.</span></span> <span data-ttu-id="d5e17-259">輕鬆安裝和設定、 啟動隨選、 並以使用者模式執行。</span><span class="sxs-lookup"><span data-stu-id="d5e17-259">It's easy to install and configure, starts on demand, and runs in user mode.</span></span> <span data-ttu-id="d5e17-260">LocalDB 以特殊的執行模式執行的 SQL Server Express，可讓您使用資料庫作為 *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-260">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="d5e17-261">您可以將 LocalDB 資料庫檔案放在*應用程式\_資料*web 專案，如果您想要能夠將複製的資料庫專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d5e17-261">You can put LocalDB database files in the *App\_Data* folder of a web project if you want to be able to copy the database with the project.</span></span> <span data-ttu-id="d5e17-262">在 SQL Server Express 使用者執行個體功能也可讓您能夠使用 *.mdf*檔案，但使用者執行個體功能已被取代; 因此，建議使用的 LocalDB *.mdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-262">The user instance feature in SQL Server Express also enables you to work with *.mdf* files, but the user instance feature is deprecated; therefore, LocalDB is recommended for working with *.mdf* files.</span></span> <span data-ttu-id="d5e17-263">使用 Visual Studio 預設會安裝 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="d5e17-263">LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="d5e17-264">一般而言，SQL Server Express 不用於生產環境 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d5e17-264">Typically, SQL Server Express is not used for production web applications.</span></span> <span data-ttu-id="d5e17-265">LocalDB 尤其不建議用於生產環境 web 應用程式因為它不是設計來搭配 IIS 運作。</span><span class="sxs-lookup"><span data-stu-id="d5e17-265">LocalDB in particular is not recommended for production use with a web application because it's not designed to work with IIS.</span></span>

- <span data-ttu-id="d5e17-266">在本教學課程中，您將使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="d5e17-266">In this tutorial, you'll work with LocalDB.</span></span> <span data-ttu-id="d5e17-267">開啟應用程式*Web.config*檔案，並新增`connectionStrings`上述項目`appSettings`項目，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d5e17-267">Open the application *Web.config* file and add a `connectionStrings` element preceding the `appSettings` element, as shown in the following example.</span></span> <span data-ttu-id="d5e17-268">(請確定您更新*Web.config*根專案資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-268">(Make sure you update the *Web.config* file in the root project folder.</span></span> <span data-ttu-id="d5e17-269">另外還有*Web.config*中的檔案*檢視*您不需要更新的子資料夾。)</span><span class="sxs-lookup"><span data-stu-id="d5e17-269">There's also a *Web.config* file in the *Views* subfolder that you don't need to update.)</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

<span data-ttu-id="d5e17-270">您已新增連接字串會指定使用 Entity Framework 會使用名為 LocalDB 資料庫*ContosoUniversity1.mdf*。</span><span class="sxs-lookup"><span data-stu-id="d5e17-270">The connection string you've added specifies that Entity Framework will use a LocalDB database named *ContosoUniversity1.mdf*.</span></span> <span data-ttu-id="d5e17-271">（尚不存在的資料庫，但 EF 會建立它）。如果您想要在其中建立資料庫您*應用程式\_資料*資料夾中，您可以新增`AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf`的連接字串。</span><span class="sxs-lookup"><span data-stu-id="d5e17-271">(The database doesn't exist yet but EF will create it.) If you want to create the database in your *App\_Data* folder, you could add `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` to the connection string.</span></span> <span data-ttu-id="d5e17-272">如需有關連接字串的詳細資訊，請參閱 < [ASP.NET Web 應用程式的 SQL Server 連接字串](/previous-versions/aspnet/jj653752(v=vs.110))。</span><span class="sxs-lookup"><span data-stu-id="d5e17-272">For more information about connection strings, see [SQL Server Connection Strings for ASP.NET Web Applications](/previous-versions/aspnet/jj653752(v=vs.110)).</span></span>

<span data-ttu-id="d5e17-273">您實際上不需要在連接字串*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-273">You don't actually need a connection string in the *Web.config* file.</span></span> <span data-ttu-id="d5e17-274">如果您未提供的連接字串，Entity Framework 會使用預設連接字串，根據您的內容類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-274">If you don't supply a connection string, Entity Framework uses a default connection string based on your context class.</span></span> <span data-ttu-id="d5e17-275">如需詳細資訊，請參閱 < [Code First 至新的資料庫](/ef/ef6/modeling/code-first/workflows/new-database)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-275">For more information, see [Code First to a New Database](/ef/ef6/modeling/code-first/workflows/new-database).</span></span>

## <a name="create-controller-and-views"></a><span data-ttu-id="d5e17-276">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="d5e17-276">Create controller and views</span></span>

<span data-ttu-id="d5e17-277">現在您將建立顯示資料的網頁。</span><span class="sxs-lookup"><span data-stu-id="d5e17-277">Now you'll create a web page to display data.</span></span> <span data-ttu-id="d5e17-278">會自動要求資料的程序就會觸發建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-278">The process of requesting the data automatically triggers the creation of the database.</span></span> <span data-ttu-id="d5e17-279">您一開始先建立新的控制器。</span><span class="sxs-lookup"><span data-stu-id="d5e17-279">You'll begin by creating a new controller.</span></span> <span data-ttu-id="d5e17-280">但您這麼做之前，建置專案，以供 MVC 控制器的 scaffolding 的模型和內容的類別。</span><span class="sxs-lookup"><span data-stu-id="d5e17-280">But before you do that, build the project to make the model and context classes available to MVC controller scaffolding.</span></span>

1. <span data-ttu-id="d5e17-281">以滑鼠右鍵按一下**控制站**資料夾中的**方案總管**，選取**新增**，然後按一下**新增 Scaffold 項目**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-281">Right-click the **Controllers** folder in **Solution Explorer**, select **Add**, and then click **New Scaffolded Item**.</span></span>
2. <span data-ttu-id="d5e17-282">在**新增 Scaffold**對話方塊中，選取**使用 MVC 5 控制器與檢視，Entity Framework**，然後選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-282">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework**, and then choose **Add**.</span></span>

     ![在 Visual Studio 中 [新增 Scaffold] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. <span data-ttu-id="d5e17-284">在 [**新增控制器**] 對話方塊中，進行下列選擇，，然後選擇**新增**:</span><span class="sxs-lookup"><span data-stu-id="d5e17-284">In the **Add Controller** dialog box, make the following selections, and then choose **Add**:</span></span>

   - <span data-ttu-id="d5e17-285">模型類別：**學生 (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-285">Model class: **Student (ContosoUniversity.Models)**.</span></span> <span data-ttu-id="d5e17-286">（如果您沒有看到此選項，在下拉式清單中的，建置專案並再試一次）。</span><span class="sxs-lookup"><span data-stu-id="d5e17-286">(If you don't see this option in the drop-down list, build the project and try again.)</span></span>
   - <span data-ttu-id="d5e17-287">資料內容類別：**SchoolContext (ContosoUniversity.DAL)**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-287">Data context class: **SchoolContext (ContosoUniversity.DAL)**.</span></span>
   - <span data-ttu-id="d5e17-288">控制器名稱：**StudentController** (不 StudentsController)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-288">Controller name: **StudentController** (not StudentsController).</span></span>
   - <span data-ttu-id="d5e17-289">保留其他欄位的預設值。</span><span class="sxs-lookup"><span data-stu-id="d5e17-289">Leave the default values for the other fields.</span></span>

     <span data-ttu-id="d5e17-290">當您按一下 **新增**，建立框架*StudentController.cs*檔案和一組檢視 (*.cshtml*檔案)，可以使用該控制器。</span><span class="sxs-lookup"><span data-stu-id="d5e17-290">When you click **Add**, the scaffolder creates a *StudentController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span> <span data-ttu-id="d5e17-291">未來當您建立使用 Entity Framework 的專案，您也可以利用的框架的一些額外的功能： 建立第一個模型類別，請勿建立連接字串，然後在 **新增控制器**  方塊中指定 **新的資料內容** 藉由選取 **+** 旁邊 **資料內容類別**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-291">In the future when you create projects that use Entity Framework, you can also take advantage of some additional functionality of the scaffolder: create your first model class, don't create a connection string, and then in the **Add Controller** box specify **New data context** by selecting the **+** button next to **Data context class**.</span></span> <span data-ttu-id="d5e17-292">框架會建立您`DbContext`類別和您的連線字串以及控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="d5e17-292">The scaffolder will create your `DbContext` class and your connection string as well as the controller and views.</span></span>
4. <span data-ttu-id="d5e17-293">Visual Studio 會開啟*Controllers\StudentController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-293">Visual Studio opens the *Controllers\StudentController.cs* file.</span></span> <span data-ttu-id="d5e17-294">您會看到類別變數已經建立的資料庫內容物件具現化：</span><span class="sxs-lookup"><span data-stu-id="d5e17-294">You see that a class variable has been created that instantiates a database context object:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     <span data-ttu-id="d5e17-295">`Index`動作方法會取得一份的學生*學生*實體集，請閱讀`Students`的資料庫內容執行個體的屬性：</span><span class="sxs-lookup"><span data-stu-id="d5e17-295">The `Index` action method gets a list of students from the *Students* entity set by reading the `Students` property of the database context instance:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     <span data-ttu-id="d5e17-296">*Student\Index.cshtml*檢視以表格顯示這份清單：</span><span class="sxs-lookup"><span data-stu-id="d5e17-296">The *Student\Index.cshtml* view displays this list in a table:</span></span>

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. <span data-ttu-id="d5e17-297">按 Ctrl + F5 執行專案。</span><span class="sxs-lookup"><span data-stu-id="d5e17-297">Press Ctrl+F5 to run the project.</span></span> <span data-ttu-id="d5e17-298">（如果您收到 「 無法建立陰影複製 」 的錯誤時，關閉瀏覽器並再試一次）。</span><span class="sxs-lookup"><span data-stu-id="d5e17-298">(If you get a "Cannot create Shadow Copy" error, close the browser and try again.)</span></span>

     <span data-ttu-id="d5e17-299">按一下 **學生**索引標籤來查看測試資料，`Seed`插入的方法。</span><span class="sxs-lookup"><span data-stu-id="d5e17-299">Click the **Students** tab to see the test data that the `Seed` method inserted.</span></span> <span data-ttu-id="d5e17-300">根據如何窄瀏覽器視窗是，您會看到的最上層的網址列中的學生 索引標籤連結，或您必須按一下右上角來查看連結。</span><span class="sxs-lookup"><span data-stu-id="d5e17-300">Depending on how narrow your browser window is, you'll see the Student tab link in the top address bar or you'll have to click the upper right corner to see the link.</span></span>

     ![功能表按鈕](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a><span data-ttu-id="d5e17-302">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="d5e17-302">View the database</span></span>

<span data-ttu-id="d5e17-303">當您執行 Students 頁面並應用程式嘗試存取資料庫時，EF 會發現有任何資料庫，並建立一個。</span><span class="sxs-lookup"><span data-stu-id="d5e17-303">When you ran the Students page and the application tried to access the database, EF discovered that there was no database and created one.</span></span> <span data-ttu-id="d5e17-304">EF 然後會執行 seed 方法，來填入資料的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-304">EF then ran the seed method to populate the database with data.</span></span>

<span data-ttu-id="d5e17-305">您可以使用**伺服器總管**或是**SQL Server 物件總管**(SSOX)，以在 Visual Studio 中檢視的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5e17-305">You can use either **Server Explorer** or **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span> <span data-ttu-id="d5e17-306">本教學課程中，您將使用**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="d5e17-306">For this tutorial, you'll use **Server Explorer**.</span></span>

1. <span data-ttu-id="d5e17-307">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d5e17-307">Close the browser.</span></span>
2. <span data-ttu-id="d5e17-308">在**伺服器總管**，展開**資料連接**（您可能需要先選取 [重新整理] 按鈕），展開**學校內容 (ContosoUniversity)**，然後展開**資料表**以查看新的資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="d5e17-308">In **Server Explorer**, expand **Data Connections** (you may need to select the refresh button first), expand **School Context (ContosoUniversity)**, and then expand **Tables** to see the tables in your new database.</span></span>

3. <span data-ttu-id="d5e17-309">以滑鼠右鍵按一下**學生**資料表，然後按一下**顯示資料表資料**以查看所建立的資料行和資料列插入至資料表。</span><span class="sxs-lookup"><span data-stu-id="d5e17-309">Right-click the **Student** table and click **Show Table Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

4. <span data-ttu-id="d5e17-310">關閉**伺服器總管**連接。</span><span class="sxs-lookup"><span data-stu-id="d5e17-310">Close the **Server Explorer** connection.</span></span>

<span data-ttu-id="d5e17-311">*ContosoUniversity1.mdf*並 *.ldf*資料庫檔案位於 *%USERPROFILE%* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d5e17-311">The *ContosoUniversity1.mdf* and *.ldf* database files are in the *%USERPROFILE%* folder.</span></span>

<span data-ttu-id="d5e17-312">因為您使用`DropCreateDatabaseIfModelChanges`初始設定式，您可以現在進行的變更`Student`類別，請再次執行應用程式，以及資料庫會自動重新建立以符合您的變更。</span><span class="sxs-lookup"><span data-stu-id="d5e17-312">Because you're using the `DropCreateDatabaseIfModelChanges` initializer, you could now make a change to the `Student` class, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="d5e17-313">例如，如果您加入`EmailAddress`屬性，以`Student`類別，請再次執行 Students 頁面以及再查看資料表一次，您將會看到新`EmailAddress`資料行。</span><span class="sxs-lookup"><span data-stu-id="d5e17-313">For example, if you add an `EmailAddress` property to the `Student` class, run the Students page again, and then look at the table again, you'll see a new `EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="d5e17-314">慣例</span><span class="sxs-lookup"><span data-stu-id="d5e17-314">Conventions</span></span>

<span data-ttu-id="d5e17-315">您必須撰寫 Entity framework 能夠為您建立完整的資料庫中的程式碼數量非常小，因為*慣例*，可讓 Entity Framework 的假設。</span><span class="sxs-lookup"><span data-stu-id="d5e17-315">The amount of code you had to write in order for Entity Framework to be able to create a complete database for you is minimal because of *conventions*, or assumptions that Entity Framework makes.</span></span> <span data-ttu-id="d5e17-316">其中一些已註明，或用來而您知道它們的存在：</span><span class="sxs-lookup"><span data-stu-id="d5e17-316">Some of them have already been noted or were used without your being aware of them:</span></span>

- <span data-ttu-id="d5e17-317">複數化的形式的實體類別名稱會用於資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="d5e17-317">The pluralized forms of entity class names are used as table names.</span></span>
- <span data-ttu-id="d5e17-318">實體屬性名稱會用於資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="d5e17-318">Entity property names are used for column names.</span></span>
- <span data-ttu-id="d5e17-319">名為實體屬性`ID`或是*classname* `ID`被視為主索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-319">Entity properties that are named `ID` or *classname* `ID` are recognized as primary key properties.</span></span>
- <span data-ttu-id="d5e17-320">是否將它命名，將會解譯為外部索引鍵屬性的屬性 *&lt;導覽屬性名稱&gt;&lt;主索引鍵屬性名稱&gt;* (比方說，`StudentID`如`Student`導覽屬性，因為`Student`實體的主索引鍵是`ID`)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-320">A property is interpreted as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="d5e17-321">外部索引鍵屬性也可以命名相同只要&lt;主索引鍵屬性名稱&gt;(例如`EnrollmentID`因為`Enrollment`實體的主索引鍵是`EnrollmentID`)。</span><span class="sxs-lookup"><span data-stu-id="d5e17-321">Foreign key properties can also be named the same simply &lt;primary key property name&gt; (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="d5e17-322">您已了解可以覆寫慣例。</span><span class="sxs-lookup"><span data-stu-id="d5e17-322">You've seen that conventions can be overridden.</span></span> <span data-ttu-id="d5e17-323">例如，指定資料表名稱不應該要複數化，，和更新版本，您會看到如何明確地標示為外部索引鍵屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="d5e17-323">For example, you specified that table names shouldn't be pluralized, and you'll see later how to explicitly mark a property as a foreign key property.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="d5e17-324">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="d5e17-324">Get the code</span></span>

[<span data-ttu-id="d5e17-325">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="d5e17-325">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="d5e17-326">其他資源</span><span class="sxs-lookup"><span data-stu-id="d5e17-326">Additional resources</span></span>

<span data-ttu-id="d5e17-327">如需有關 EF 6 的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="d5e17-327">For more about EF 6, see these articles:</span></span>

* [<span data-ttu-id="d5e17-328">ASP.NET 資料存取 - 建議資源</span><span class="sxs-lookup"><span data-stu-id="d5e17-328">ASP.NET Data Access - Recommended Resources</span></span>](../../../../whitepapers/aspnet-data-access-content-map.md)

* [<span data-ttu-id="d5e17-329">程式碼的第一個慣例</span><span class="sxs-lookup"><span data-stu-id="d5e17-329">Code First Conventions</span></span>](/ef/ef6/modeling/code-first/conventions/built-in)

* [<span data-ttu-id="d5e17-330">建立更複雜的資料模型</span><span class="sxs-lookup"><span data-stu-id="d5e17-330">Creating a More Complex Data Model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a><span data-ttu-id="d5e17-331">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d5e17-331">Next steps</span></span>

<span data-ttu-id="d5e17-332">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="d5e17-332">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d5e17-333">建立 MVC web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d5e17-333">Created an MVC web app</span></span>
> * <span data-ttu-id="d5e17-334">設定網站樣式</span><span class="sxs-lookup"><span data-stu-id="d5e17-334">Set up the site style</span></span>
> * <span data-ttu-id="d5e17-335">安裝的 Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d5e17-335">Installed Entity Framework 6</span></span>
> * <span data-ttu-id="d5e17-336">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="d5e17-336">Created the data model</span></span>
> * <span data-ttu-id="d5e17-337">建立資料庫內容</span><span class="sxs-lookup"><span data-stu-id="d5e17-337">Created the database context</span></span>
> * <span data-ttu-id="d5e17-338">使用測試資料將 DB 初始化</span><span class="sxs-lookup"><span data-stu-id="d5e17-338">Initialized DB with test data</span></span>
> * <span data-ttu-id="d5e17-339">將 EF 6 設定為使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="d5e17-339">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="d5e17-340">建立控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="d5e17-340">Created controller and views</span></span>
> * <span data-ttu-id="d5e17-341">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="d5e17-341">Viewed the database</span></span>

<span data-ttu-id="d5e17-342">請前往下一篇文章，以了解如何檢閱和自訂的建立、 讀取、 更新、 刪除 (CRUD) 程式碼，在您的控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="d5e17-342">Advance to the next article to learn how to review and customize the create, read, update, delete (CRUD) code in your controllers and views.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d5e17-343">實作基本的 CRUD 功能</span><span class="sxs-lookup"><span data-stu-id="d5e17-343">Implement basic CRUD functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)