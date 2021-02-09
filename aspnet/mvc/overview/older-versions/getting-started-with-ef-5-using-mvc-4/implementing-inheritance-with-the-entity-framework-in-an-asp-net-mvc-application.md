---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行繼承， (8/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: de86dd0d1a8e1b68d14971d328fe88a7fdb3e9b1
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984779"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="45cf3-103">使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行繼承， (8/10) </span><span class="sxs-lookup"><span data-stu-id="45cf3-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>

<span data-ttu-id="45cf3-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="45cf3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="45cf3-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="45cf3-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="45cf3-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="45cf3-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="45cf3-107">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="45cf3-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="45cf3-108">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="45cf3-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="45cf3-109">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="45cf3-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="45cf3-110">在上一個教學課程中，您已處理平行存取例外狀況。</span><span class="sxs-lookup"><span data-stu-id="45cf3-110">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="45cf3-111">本教學課程將示範如何在資料模型中實作繼承。</span><span class="sxs-lookup"><span data-stu-id="45cf3-111">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="45cf3-112">在物件導向程式設計中，您可以使用繼承來消除多餘的程式碼。</span><span class="sxs-lookup"><span data-stu-id="45cf3-112">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="45cf3-113">在本教學課程中，您將變更 `Instructor` 和 `Student` 類別，讓它們衍生自 `Person` 基底類別，而此基底類別包含講師和學生通用的屬性，例如 `LastName`。</span><span class="sxs-lookup"><span data-stu-id="45cf3-113">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="45cf3-114">您不會新增或變更任何網頁，但是您將變更一些程式碼，這些變更將會自動反映在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="45cf3-114">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="45cf3-115">每個階層的資料表與每一類型的資料表繼承</span><span class="sxs-lookup"><span data-stu-id="45cf3-115">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="45cf3-116">在物件導向程式設計中，您可以使用繼承來更輕鬆地使用相關類別。</span><span class="sxs-lookup"><span data-stu-id="45cf3-116">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="45cf3-117">例如， `Instructor` `Student` 資料模型中的和類別 `School` 共用數個屬性，因此會產生多餘的程式碼：</span><span class="sxs-lookup"><span data-stu-id="45cf3-117">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="45cf3-119">假設您想要針對 `Instructor` 和 `Student` 實體所共用的屬性消除多餘的程式碼。</span><span class="sxs-lookup"><span data-stu-id="45cf3-119">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="45cf3-120">您可以建立 `Person` 只包含這些共用屬性的基類，然後讓 `Instructor` 和 `Student` 實體繼承自該基類，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="45cf3-120">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="45cf3-122">有幾種方式可以在資料庫中表示此繼承結構。</span><span class="sxs-lookup"><span data-stu-id="45cf3-122">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="45cf3-123">您可以有一個 `Person` 資料表，其中包含與學生和講師在單一資料表中的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="45cf3-123">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="45cf3-124">某些資料行只能套用至講師 (`HireDate`) ，有些則只適用于學生 (`EnrollmentDate`) ， () `LastName` `FirstName` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-124">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="45cf3-125">一般而言，您會有 *鑒別* 子資料行，以指出每個資料列所代表的類型。</span><span class="sxs-lookup"><span data-stu-id="45cf3-125">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="45cf3-126">例如，鑑別子資料行的 "Instructor" 代表講師，而 "Student" 代表學生。</span><span class="sxs-lookup"><span data-stu-id="45cf3-126">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![每 hierarchy_example 一份資料表](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="45cf3-128">從單一資料庫資料表產生實體繼承結構的這種模式稱為「 *每個* 階層的資料表」， (TPH) 繼承。</span><span class="sxs-lookup"><span data-stu-id="45cf3-128">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="45cf3-129">替代方法是讓資料庫看起來更像繼承結構。</span><span class="sxs-lookup"><span data-stu-id="45cf3-129">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="45cf3-130">例如，您可能只有資料表中的名稱欄位 `Person` ，而且具有不同 `Instructor` `Student` 的資料表和 [日期] 欄位。</span><span class="sxs-lookup"><span data-stu-id="45cf3-130">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![每 type_inheritance 一份資料表](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="45cf3-132">為每個實體類別建立資料庫資料表的這種模式， (TPT) 繼承的 *每個類型* 都稱為 table。</span><span class="sxs-lookup"><span data-stu-id="45cf3-132">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="45cf3-133">因為 TPT 模式可能會導致複雜的聯結查詢，所以 TPH 繼承模式通常會在 Entity Framework 中提供比 TPT 繼承模式更好的效能。</span><span class="sxs-lookup"><span data-stu-id="45cf3-133">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="45cf3-134">本教學課程將示範如何實作 TPH 繼承。</span><span class="sxs-lookup"><span data-stu-id="45cf3-134">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="45cf3-135">您將執行下列步驟來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="45cf3-135">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="45cf3-136">建立 `Person` 類別，並變更 `Instructor` `Student` 要衍生自的和類別 `Person` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-136">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="45cf3-137">將模型對資料庫對應程式碼加入至資料庫內容類別。</span><span class="sxs-lookup"><span data-stu-id="45cf3-137">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="45cf3-138">在 `InstructorID` `StudentID` 整個專案中變更和參考 `PersonID` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-138">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="45cf3-139">建立 Person 類別</span><span class="sxs-lookup"><span data-stu-id="45cf3-139">Creating the Person Class</span></span>

 <span data-ttu-id="45cf3-140">注意：在您更新使用這些類別的控制器之前，您無法在建立下列類別之後編譯專案。</span><span class="sxs-lookup"><span data-stu-id="45cf3-140">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="45cf3-141">在 [ *模型* ] 資料夾中，建立 *Person.cs* ，並以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="45cf3-141">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="45cf3-142">在 *Instructor.cs* 中， `Instructor` 從類別衍生類別 `Person` ，並移除索引鍵和名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="45cf3-142">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="45cf3-143">程式碼看起來應該如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45cf3-143">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="45cf3-144">對 *Student.cs* 進行類似的變更。</span><span class="sxs-lookup"><span data-stu-id="45cf3-144">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="45cf3-145">`Student`類別看起來會如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45cf3-145">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="45cf3-146">將 Person 實體類型加入至模型</span><span class="sxs-lookup"><span data-stu-id="45cf3-146">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="45cf3-147">在 *SchoolCoNtext.cs* 中，新增 `DbSet` `Person` 實體類型的屬性：</span><span class="sxs-lookup"><span data-stu-id="45cf3-147">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="45cf3-148">這就是 Entity Framework 為了設定單表繼承而必須執行的所有工作。</span><span class="sxs-lookup"><span data-stu-id="45cf3-148">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="45cf3-149">如您所見，重新建立資料庫時，它會有一個 `Person` 資料表來取代 `Student` 和 `Instructor` 資料表。</span><span class="sxs-lookup"><span data-stu-id="45cf3-149">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="45cf3-150">將 InstructorID 和 StudentID 變更為 PersonID</span><span class="sxs-lookup"><span data-stu-id="45cf3-150">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="45cf3-151">在 *SchoolCoNtext.cs* 的 Instructor-Course 對應語句中，變更 `MapRightKey("InstructorID")` 為 `MapRightKey("PersonID")` ：</span><span class="sxs-lookup"><span data-stu-id="45cf3-151">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="45cf3-152">這不是必要的變更;它只會變更多對多聯結資料表中 InstructorID 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="45cf3-152">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="45cf3-153">如果您將名稱保留為 InstructorID，應用程式仍然可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="45cf3-153">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="45cf3-154">以下是已完成的 *SchoolCoNtext.cs*：</span><span class="sxs-lookup"><span data-stu-id="45cf3-154">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="45cf3-155">接下來，您必須 `InstructorID` 將 `PersonID` `StudentID` `PersonID` _Migrations \* 資料夾中時間戳記的遷移檔案，在專案中變更為和。</span><span class="sxs-lookup"><span data-stu-id="45cf3-155">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except** _ in the time-stamped migrations files in the _Migrations* folder.</span></span> <span data-ttu-id="45cf3-156">若要這樣做，您只會找到並開啟需要變更的檔案，然後對開啟的檔案執行全域變更。</span><span class="sxs-lookup"><span data-stu-id="45cf3-156">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="45cf3-157">在 [ *遷移* ] 資料夾中，您應該變更的唯一檔案是 *Migrations\Configuration.cs.*</span><span class="sxs-lookup"><span data-stu-id="45cf3-157">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="45cf3-158">從 Visual Studio 中關閉所有開啟的檔案開始。</span><span class="sxs-lookup"><span data-stu-id="45cf3-158">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="45cf3-159">在 [**編輯**] 功能表中，按一下 [**尋找並取代--尋找所有** 檔案]，然後在專案中搜尋包含的所有檔案 `InstructorID` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-159">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="45cf3-160">在 [**尋找結果**] 視窗中開啟每 \*\* 個檔案，在 [遷移] 資料夾中開啟 [ &lt; 時間戳記] &gt; _ \_ .cs \* 的檔案，方法是按兩下每個檔案的一行。 </span><span class="sxs-lookup"><span data-stu-id="45cf3-160">Open each file in the **Find Results** window **_except_* _ the &lt;time-stamp&gt;_\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="45cf3-161">開啟 [檔案 **中取代** ] 對話方塊，並將 [ **查詢** ] 變更為 **所有開啟** 的檔。</span><span class="sxs-lookup"><span data-stu-id="45cf3-161">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="45cf3-162">使用 [檔案 **中取代** ] 對話方塊，將全部變更 `InstructorID` 為 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="45cf3-162">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="45cf3-163">尋找專案中包含的所有檔案 `StudentID` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-163">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="45cf3-164">在 [**尋找結果**] 視窗中開啟每 \*\* 個檔案，在 [遷移] 資料夾中開啟 [ &lt; 時間戳記] &gt; _ \_ \* .cs \* 的檔案，方法是按兩下每個檔案的一行。 </span><span class="sxs-lookup"><span data-stu-id="45cf3-164">Open each file in the **Find Results** window **_except_* _ the &lt;time-stamp&gt;_\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="45cf3-165">開啟 [檔案 **中取代** ] 對話方塊，並將 [ **查詢** ] 變更為 **所有開啟** 的檔。</span><span class="sxs-lookup"><span data-stu-id="45cf3-165">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="45cf3-166">使用 [檔案 **中取代** ] 對話方塊，將全部變更 `StudentID` 為 `PersonID` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-166">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="45cf3-167">建置專案。</span><span class="sxs-lookup"><span data-stu-id="45cf3-167">Build the project.</span></span>

<span data-ttu-id="45cf3-168"> (請注意，這會示範 `classnameID` 命名主鍵的模式缺點。</span><span class="sxs-lookup"><span data-stu-id="45cf3-168">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="45cf3-169">如果您在沒有首碼類別名稱的情況下命名 primary key ID，現在就 *不* 需要重新命名。 ) </span><span class="sxs-lookup"><span data-stu-id="45cf3-169">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="45cf3-170">建立和更新遷移檔案</span><span class="sxs-lookup"><span data-stu-id="45cf3-170">Create and Update a Migrations File</span></span>

<span data-ttu-id="45cf3-171">在封裝管理員主控台中 (PMC) 上，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="45cf3-171">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="45cf3-172">`Update-Database`在 PMC 中執行命令。</span><span class="sxs-lookup"><span data-stu-id="45cf3-172">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="45cf3-173">此命令將會在此時失敗，因為我們有遷移不知道如何處理的現有資料。</span><span class="sxs-lookup"><span data-stu-id="45cf3-173">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="45cf3-174">而您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="45cf3-174">You get the following error:</span></span>

<span data-ttu-id="45cf3-175">*ALTER TABLE 語句與外鍵條件約束「FK dbo」衝突 \_ 。部門 \_ dbo。Person \_ PersonID」。衝突發生在資料庫 "ContosoUniversity" 中，資料表 "dbo。Person "，資料行 ' PersonID '。*</span><span class="sxs-lookup"><span data-stu-id="45cf3-175">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="45cf3-176">開啟 *\& [遷移 lt; timestamp &gt; \_ Inheritance.cs]* ，並 `Up` 以下列程式碼取代方法：</span><span class="sxs-lookup"><span data-stu-id="45cf3-176">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="45cf3-177">再次執行 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="45cf3-177">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="45cf3-178">您可以在遷移資料並進行架構變更時，收到其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="45cf3-178">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="45cf3-179">如果您收到無法解決的遷移錯誤，可以藉由變更 *Web.config* 檔案中的連接字串或刪除資料庫，繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="45cf3-179">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="45cf3-180">最簡單的方法是在 *Web.config* 檔案中重新命名資料庫。</span><span class="sxs-lookup"><span data-stu-id="45cf3-180">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="45cf3-181">例如，將資料庫名稱變更為 CU \_ 測試，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="45cf3-181">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="45cf3-182">有了新的資料庫，就不會有要遷移的資料，而且 `update-database` 命令更可能會在沒有錯誤的情況下完成。</span><span class="sxs-lookup"><span data-stu-id="45cf3-182">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="45cf3-183">如需有關如何刪除資料庫的指示，請參閱 [如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="45cf3-183">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="45cf3-184">如果您採用此方法來繼續進行本教學課程，請略過本教學課程結尾的部署步驟，因為部署的網站會在自動執行遷移時取得相同的錯誤。</span><span class="sxs-lookup"><span data-stu-id="45cf3-184">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="45cf3-185">如果您想要針對遷移錯誤進行疑難排解，最佳的資源是其中一個 Entity Framework 論壇或 StackOverflow.com。</span><span class="sxs-lookup"><span data-stu-id="45cf3-185">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>

## <a name="testing"></a><span data-ttu-id="45cf3-186">測試</span><span class="sxs-lookup"><span data-stu-id="45cf3-186">Testing</span></span>

<span data-ttu-id="45cf3-187">執行網站並嘗試各種不同的頁面。</span><span class="sxs-lookup"><span data-stu-id="45cf3-187">Run the site and try various pages.</span></span> <span data-ttu-id="45cf3-188">一切項目的運作與之前一樣。</span><span class="sxs-lookup"><span data-stu-id="45cf3-188">Everything works the same as it did before.</span></span>

<span data-ttu-id="45cf3-189">在 **伺服器總管中，** 依序展開 [ **SchoolCoNtext** ] 和 [ **資料表]**，然後您會看到 **學生** 和 **講師** 資料表已被 **Person** 資料表取代。</span><span class="sxs-lookup"><span data-stu-id="45cf3-189">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="45cf3-190">展開 [ **Person** ] 資料表，您會看到它的所有資料行都是在 **學生** 和 **講師** 資料表中。</span><span class="sxs-lookup"><span data-stu-id="45cf3-190">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="45cf3-192">以滑鼠右鍵按一下 Person 資料表，然後按一下 [顯示資料表資料] 以查看鑑別子資料行。</span><span class="sxs-lookup"><span data-stu-id="45cf3-192">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="45cf3-193">下圖說明新 School 資料庫的結構：</span><span class="sxs-lookup"><span data-stu-id="45cf3-193">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="45cf3-195">摘要</span><span class="sxs-lookup"><span data-stu-id="45cf3-195">Summary</span></span>

<span data-ttu-id="45cf3-196">`Person`、和類別現在已針對每個階層的資料表繼承執行 `Student` `Instructor` 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-196">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="45cf3-197">如需有關這個和其他繼承結構的詳細資訊，請參閱 Morteza Manavi 的 blog 上的 [繼承對應策略](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="45cf3-197">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="45cf3-198">在下一個教學課程中，您將會看到一些方法來執行存放庫和工作單元模式。</span><span class="sxs-lookup"><span data-stu-id="45cf3-198">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="45cf3-199">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="45cf3-199">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="45cf3-200">[上一個](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="45cf3-200">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
