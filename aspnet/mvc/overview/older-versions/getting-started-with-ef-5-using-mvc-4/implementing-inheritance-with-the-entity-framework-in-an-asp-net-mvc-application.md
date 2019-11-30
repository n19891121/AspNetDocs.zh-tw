---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中使用 Entity Framework 執行繼承（8/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595312"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="7d05b-103">在 ASP.NET MVC 應用程式中使用 Entity Framework 執行繼承（8之10）</span><span class="sxs-lookup"><span data-stu-id="7d05b-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="7d05b-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7d05b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7d05b-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7d05b-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="7d05b-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d05b-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="7d05b-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="7d05b-108">您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="7d05b-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="7d05b-109">如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="7d05b-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="7d05b-110">您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。</span><span class="sxs-lookup"><span data-stu-id="7d05b-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="7d05b-111">如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="7d05b-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="7d05b-112">在上一個教學課程中，您已處理並行例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7d05b-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="7d05b-113">本教學課程將示範如何在資料模型中實作繼承。</span><span class="sxs-lookup"><span data-stu-id="7d05b-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="7d05b-114">在物件導向程式設計中，您可以使用繼承來消除多餘的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7d05b-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="7d05b-115">在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。</span><span class="sxs-lookup"><span data-stu-id="7d05b-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="7d05b-116">您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="7d05b-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="7d05b-117">每個階層的資料表與每個類型的資料表繼承</span><span class="sxs-lookup"><span data-stu-id="7d05b-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="7d05b-118">在物件導向程式設計中，您可以使用繼承，讓您更輕鬆地使用相關的類別。</span><span class="sxs-lookup"><span data-stu-id="7d05b-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="7d05b-119">例如，`School` 資料模型中的 `Instructor` 和 `Student` 類別共用數個屬性，這會導致重複的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7d05b-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="7d05b-121">假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7d05b-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="7d05b-122">您可以建立只包含這些共用屬性的 `Person` 基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="7d05b-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="7d05b-124">有幾種方式可以在資料庫中表示此繼承結構。</span><span class="sxs-lookup"><span data-stu-id="7d05b-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="7d05b-125">您可以有一個 `Person` 的資料表，其中包含單一資料表中的學生和講師的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7d05b-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="7d05b-126">有些資料行僅適用于講師（`HireDate`），部分僅供學生（`EnrollmentDate`）使用，部分至（`LastName`，`FirstName`）。</span><span class="sxs-lookup"><span data-stu-id="7d05b-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="7d05b-127">一般而言，您會有一個*鑒別*子資料行，以指出每個資料列所代表的類型。</span><span class="sxs-lookup"><span data-stu-id="7d05b-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="7d05b-128">例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。</span><span class="sxs-lookup"><span data-stu-id="7d05b-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![每 hierarchy_example 一個資料表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="7d05b-130">從單一資料庫資料表產生實體繼承結構的這種模式稱為「*每個階層的資料表*」（TPH）繼承。</span><span class="sxs-lookup"><span data-stu-id="7d05b-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="7d05b-131">替代方法是讓資料庫看起來更像繼承結構。</span><span class="sxs-lookup"><span data-stu-id="7d05b-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="7d05b-132">例如，您可以只有 `Person` 資料表中的 [名稱] 欄位，而且有不同的 `Instructor` 和 `Student` 資料表與日期欄位。</span><span class="sxs-lookup"><span data-stu-id="7d05b-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![每 type_inheritance 一個資料表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="7d05b-134">為每個實體類別建立資料庫資料表的這種模式，稱為「*每一類型的資料表*」（TPT）繼承。</span><span class="sxs-lookup"><span data-stu-id="7d05b-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="7d05b-135">在 Entity Framework 中，TPH 繼承模式通常會比 TPT 繼承模式提供更好的效能，因為 TPT 模式可能會導致複雜的聯結查詢。</span><span class="sxs-lookup"><span data-stu-id="7d05b-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="7d05b-136">本教學課程將示範如何實作 TPH 繼承。</span><span class="sxs-lookup"><span data-stu-id="7d05b-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="7d05b-137">您將執行下列步驟來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="7d05b-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="7d05b-138">建立 `Person` 類別，並將 `Instructor` 和 `Student` 類別變更為從 `Person`衍生。</span><span class="sxs-lookup"><span data-stu-id="7d05b-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="7d05b-139">將模型到資料庫的對應程式碼加入至資料庫內容類別。</span><span class="sxs-lookup"><span data-stu-id="7d05b-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="7d05b-140">將整個專案的 `InstructorID` 和 `StudentID` 參考變更為 `PersonID`。</span><span class="sxs-lookup"><span data-stu-id="7d05b-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="7d05b-141">建立 Person 類別</span><span class="sxs-lookup"><span data-stu-id="7d05b-141">Creating the Person Class</span></span>

 <span data-ttu-id="7d05b-142">注意：在您更新使用這些類別的控制器之前，您將無法在建立下列類別之後編譯專案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="7d05b-143">在 [*模型*] 資料夾中，建立*Person.cs* ，並將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7d05b-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="7d05b-144">在*Instructor.cs*中，從 `Person` 類別衍生 `Instructor` 類別，並移除 [索引鍵] 和 [名稱] 欄位。</span><span class="sxs-lookup"><span data-stu-id="7d05b-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="7d05b-145">程式碼看起來應該如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7d05b-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="7d05b-146">對*Student.cs*進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="7d05b-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="7d05b-147">`Student` 類別看起來會如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7d05b-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="7d05b-148">將 Person 實體類型新增至模型</span><span class="sxs-lookup"><span data-stu-id="7d05b-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="7d05b-149">在*SchoolCoNtext.cs*中，加入 `Person` 實體類型的 `DbSet` 屬性：</span><span class="sxs-lookup"><span data-stu-id="7d05b-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="7d05b-150">這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。</span><span class="sxs-lookup"><span data-stu-id="7d05b-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="7d05b-151">如您所見，當資料庫重新建立時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。</span><span class="sxs-lookup"><span data-stu-id="7d05b-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="7d05b-152">將 InstructorID 和 StudentID 變更為 PersonID</span><span class="sxs-lookup"><span data-stu-id="7d05b-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="7d05b-153">在*SchoolCoNtext.cs*的講師課程對應語句中，將 `MapRightKey("InstructorID")` 變更為 `MapRightKey("PersonID")`：</span><span class="sxs-lookup"><span data-stu-id="7d05b-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="7d05b-154">這不是必要的變更;它只會變更多對多聯結資料表中 InstructorID 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d05b-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="7d05b-155">如果您將名稱保留為 InstructorID，應用程式仍會正常運作。</span><span class="sxs-lookup"><span data-stu-id="7d05b-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="7d05b-156">以下是已完成的*SchoolCoNtext.cs*：</span><span class="sxs-lookup"><span data-stu-id="7d05b-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="7d05b-157">接下來，您必須將 `InstructorID` 變更為 `PersonID`，並 `StudentID` 至整個專案中的 `PersonID`，***除非***[*遷移*] 資料夾中有時間戳記的遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="7d05b-158">若要這麼做，您將只會尋找並開啟需要變更的檔案，然後在開啟的檔案上執行全域變更。</span><span class="sxs-lookup"><span data-stu-id="7d05b-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="7d05b-159">在 [*遷移*] 資料夾中，您應該變更的唯一檔案是*Migrations\Configuration.cs.*</span><span class="sxs-lookup"><span data-stu-id="7d05b-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="7d05b-160">一開始先關閉 Visual Studio 中所有開啟的檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="7d05b-161">在 [**編輯**] 功能表中，按一下 [**尋找及取代--尋找所有**檔案]，然後搜尋包含 `InstructorID`之專案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="7d05b-162">在 [**尋找結果**] 視窗中開啟每個檔案，***但***在 [*遷移*] 資料夾中，按兩下每個檔案的一行，&lt;時間戳記&gt; *\_.cs*遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="7d05b-163">開啟 [檔案**中取代**] 對話方塊，然後變更 [**查看** **所有開啟**的檔]。</span><span class="sxs-lookup"><span data-stu-id="7d05b-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="7d05b-164">使用 [檔案**中取代**] 對話方塊，將所有 `InstructorID` 變更為 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="7d05b-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="7d05b-165">尋找包含 `StudentID`之專案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="7d05b-166">在 [**尋找結果**] 視窗中開啟每個檔案，***但***&lt;時間戳記&gt;會在 [*遷移*] 資料夾中，按兩下每個檔案的一行，以 *\_\*.cs*遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="7d05b-167">開啟 [檔案**中取代**] 對話方塊，然後變更 [**查看** **所有開啟**的檔]。</span><span class="sxs-lookup"><span data-stu-id="7d05b-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="7d05b-168">使用 [檔案**中取代**] 對話方塊，將所有 `StudentID` 變更為 `PersonID`。</span><span class="sxs-lookup"><span data-stu-id="7d05b-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="7d05b-169">建置專案。</span><span class="sxs-lookup"><span data-stu-id="7d05b-169">Build the project.</span></span>

<span data-ttu-id="7d05b-170">（請注意，這會示範用來命名主鍵之 `classnameID` 模式的*缺點*。</span><span class="sxs-lookup"><span data-stu-id="7d05b-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="7d05b-171">如果您已命名「主鍵識別碼」，但未在類別名稱前面加上，則現在*不*需要重新命名。）</span><span class="sxs-lookup"><span data-stu-id="7d05b-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="7d05b-172">建立和更新遷移檔案</span><span class="sxs-lookup"><span data-stu-id="7d05b-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="7d05b-173">在 [套件管理員主控台] （PMC）中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7d05b-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="7d05b-174">在 PMC 中執行 `Update-Database` 命令。</span><span class="sxs-lookup"><span data-stu-id="7d05b-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="7d05b-175">此時，此命令將會失敗，因為我們有遷移不知道如何處理的現有資料。</span><span class="sxs-lookup"><span data-stu-id="7d05b-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="7d05b-176">您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="7d05b-176">You get the following error:</span></span>

<span data-ttu-id="7d05b-177">*ALTER TABLE 語句與外鍵條件約束 "FK\_dbo 衝突。部門\_dbo。Person\_PersonID」。衝突發生在資料庫 "ContosoUniversity"，資料表 "dbo。Person 「，資料行 ' PersonID '。*</span><span class="sxs-lookup"><span data-stu-id="7d05b-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="7d05b-178">開啟 *[遷移]\&lt; 時間戳記&gt;\_Inheritance.cs* ，並以下列程式碼取代 `Up` 方法：</span><span class="sxs-lookup"><span data-stu-id="7d05b-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="7d05b-179">再次執行 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="7d05b-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="7d05b-180">當您遷移資料並進行架構變更時，可能會收到其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d05b-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="7d05b-181">如果您收到無法解決的遷移錯誤，可以藉由變更*web.config*檔案中的連接字串或刪除資料庫，繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="7d05b-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="7d05b-182">最簡單的方法是*在 web.config 檔案*中重新命名資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d05b-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="7d05b-183">例如，將資料庫名稱變更為 CU\_測試，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7d05b-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="7d05b-184">使用新的資料庫時，沒有可遷移的資料，而且 `update-database` 命令較可能會在沒有錯誤的情況下完成。</span><span class="sxs-lookup"><span data-stu-id="7d05b-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="7d05b-185">如需有關如何刪除資料庫的指示，請參閱[如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="7d05b-186">如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，因為部署的網站會在自動執行遷移時收到相同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d05b-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="7d05b-187">如果您想要針對遷移錯誤進行疑難排解，最佳資源是其中一個 Entity Framework 論壇或 StackOverflow.com。</span><span class="sxs-lookup"><span data-stu-id="7d05b-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="7d05b-188">測試</span><span class="sxs-lookup"><span data-stu-id="7d05b-188">Testing</span></span>

<span data-ttu-id="7d05b-189">執行網站並嘗試各種頁面。</span><span class="sxs-lookup"><span data-stu-id="7d05b-189">Run the site and try various pages.</span></span> <span data-ttu-id="7d05b-190">一切項目的運作與之前一樣。</span><span class="sxs-lookup"><span data-stu-id="7d05b-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="7d05b-191">在**伺服器總管中，** 依序展開 [ **SchoolCoNtext** ] 和 [**資料表]** ，您會看到 [ **Student** ] 和 [**講師**] 資料表已由 [ **Person** ] 資料表取代。</span><span class="sxs-lookup"><span data-stu-id="7d05b-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="7d05b-192">展開 [ **Person** ] 資料表，您就會看到它擁有所有用在**學生**和**講師**資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="7d05b-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="7d05b-194">以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。</span><span class="sxs-lookup"><span data-stu-id="7d05b-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="7d05b-195">下圖說明新 School 資料庫的結構：</span><span class="sxs-lookup"><span data-stu-id="7d05b-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="7d05b-197">總結</span><span class="sxs-lookup"><span data-stu-id="7d05b-197">Summary</span></span>

<span data-ttu-id="7d05b-198">現在已針對 `Person`、`Student`和 `Instructor` 類別，執行每個階層的資料表繼承。</span><span class="sxs-lookup"><span data-stu-id="7d05b-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="7d05b-199">如需有關這個和其他繼承結構的詳細資訊，請參閱 Morteza Manavi 的 blog 的[繼承對應策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7d05b-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="7d05b-200">在下一個教學課程中，您會看到一些執行存放庫和工作單位模式的方式。</span><span class="sxs-lookup"><span data-stu-id="7d05b-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="7d05b-201">您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="7d05b-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7d05b-202">[上一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="7d05b-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
