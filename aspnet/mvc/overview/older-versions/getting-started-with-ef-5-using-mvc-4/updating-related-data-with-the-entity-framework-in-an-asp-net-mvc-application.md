---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 以 ASP.NET MVC 應用程式中的 Entity Framework 更新相關資料（6/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592445"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="29741-103">以 ASP.NET MVC 應用程式中的 Entity Framework 更新相關資料（6/10）</span><span class="sxs-lookup"><span data-stu-id="29741-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>

<span data-ttu-id="29741-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="29741-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="29741-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="29741-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="29741-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29741-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="29741-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="29741-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="29741-108">您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="29741-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="29741-109">如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="29741-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="29741-110">您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。</span><span class="sxs-lookup"><span data-stu-id="29741-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="29741-111">如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="29741-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="29741-112">在上一個教學課程中，您顯示了相關資料;在本教學課程中，您將更新相關的資料。</span><span class="sxs-lookup"><span data-stu-id="29741-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="29741-113">對於大部分的關聯性，您可以藉由更新適當的外鍵欄位來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="29741-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="29741-114">針對多對多關聯性，Entity Framework 不會直接公開聯結資料表，因此您必須明確地在適當的導覽屬性中加入和移除實體。</span><span class="sxs-lookup"><span data-stu-id="29741-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="29741-115">下列圖例顯示了您將操作的頁面。</span><span class="sxs-lookup"><span data-stu-id="29741-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="29741-118">自訂 Courses 的 [建立] 和 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="29741-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="29741-119">當新的課程實體建立時，其必須要與現有的部門具有關聯性。</span><span class="sxs-lookup"><span data-stu-id="29741-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="29741-120">若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="29741-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="29741-121">下拉式清單會設定 `Course.DepartmentID` 外鍵屬性，而這就是載入具有適當 `Department` 實體之 `Department` 導覽屬性的所有 Entity Framework 需求。</span><span class="sxs-lookup"><span data-stu-id="29741-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="29741-122">您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="29741-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="29741-123">在*CourseController.cs*中，刪除四個 `Edit` 並 `Create` 方法，並將其取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="29741-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="29741-124">`PopulateDepartmentsDropDownList` 方法會取得依名稱排序的所有部門清單、建立下拉式清單的 `SelectList` 集合，並將集合傳遞至 `ViewBag` 屬性中的 view。</span><span class="sxs-lookup"><span data-stu-id="29741-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="29741-125">方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。</span><span class="sxs-lookup"><span data-stu-id="29741-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="29741-126">此視圖會將名稱 `DepartmentID` 傳遞給[`DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)，而協助專家會知道要在 `ViewBag` 物件中尋找名為 `DepartmentID`的 `SelectList`。</span><span class="sxs-lookup"><span data-stu-id="29741-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="29741-127">`HttpGet` `Create` 方法會呼叫 `PopulateDepartmentsDropDownList` 方法，而不會設定選取的專案，因為如果是新的課程，則尚未建立部門：</span><span class="sxs-lookup"><span data-stu-id="29741-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="29741-128">`HttpGet` `Edit` 方法會根據已指派給所編輯之課程的部門識別碼，來設定選取的專案：</span><span class="sxs-lookup"><span data-stu-id="29741-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="29741-129">`Create` 和 `Edit` 的 `HttpPost` 方法也包含程式碼，可在錯誤發生後重新顯示頁面時，設定選取的專案：</span><span class="sxs-lookup"><span data-stu-id="29741-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="29741-130">這段程式碼可確保當頁面重新顯示時，如果出現錯誤訊息，則會保留選取的任何部門。</span><span class="sxs-lookup"><span data-stu-id="29741-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="29741-131">在*Views\Course\Create.cshtml*中，新增反白顯示的程式碼，以在 [**標題**] 欄位之前建立新的課程編號欄位。</span><span class="sxs-lookup"><span data-stu-id="29741-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="29741-132">如先前的教學課程中所述，預設不會 scaffold 主鍵欄位，但此主鍵有意義，因此您希望使用者能夠輸入索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="29741-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="29741-133">在 [ *Views\Course\Edit.cshtml*]、[ *Views\Course\Delete.cshtml*] 和 [ *Views\Course\Details.cshtml*] 中，于 [**標題**] 欄位前面新增 [課程編號] 欄位。</span><span class="sxs-lookup"><span data-stu-id="29741-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="29741-134">因為它是主要金鑰，所以會顯示，但無法變更。</span><span class="sxs-lookup"><span data-stu-id="29741-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="29741-135">執行 [**建立**] 頁面（顯示 [課程索引] 頁面，然後按一下 [**建立新**的]）並輸入新課程的資料：</span><span class="sxs-lookup"><span data-stu-id="29741-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="29741-137">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="29741-137">Click **Create**.</span></span> <span data-ttu-id="29741-138">[課程索引] 頁面隨即顯示，並將新課程加入清單中。</span><span class="sxs-lookup"><span data-stu-id="29741-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="29741-139">[索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。</span><span class="sxs-lookup"><span data-stu-id="29741-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="29741-141">執行 [**編輯**] 頁面（顯示課程 [索引] 頁面，然後按一下 [在課程中**編輯**]）。</span><span class="sxs-lookup"><span data-stu-id="29741-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="29741-143">變更頁面上的資料，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="29741-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="29741-144">[課程索引] 頁面隨即顯示，其中包含更新的課程資料。</span><span class="sxs-lookup"><span data-stu-id="29741-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="29741-145">新增講師的編輯頁面</span><span class="sxs-lookup"><span data-stu-id="29741-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="29741-146">當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="29741-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="29741-147">`Instructor` 實體與 `OfficeAssignment` 實體具有一對零或一關聯性，這表示您必須處理下列情況：</span><span class="sxs-lookup"><span data-stu-id="29741-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="29741-148">如果使用者清除辦公室指派，而且原先具有值，您就必須移除並刪除 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="29741-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="29741-149">如果使用者輸入辦公室指派值，而且原先是空的，您就必須建立新的 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="29741-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="29741-150">如果使用者變更辦公室指派的值，您必須變更現有 `OfficeAssignment` 實體中的值。</span><span class="sxs-lookup"><span data-stu-id="29741-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="29741-151">開啟*InstructorController.cs* ，並查看 `HttpGet` `Edit` 方法：</span><span class="sxs-lookup"><span data-stu-id="29741-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="29741-152">此處的 scaffold 程式碼不是您想要的。</span><span class="sxs-lookup"><span data-stu-id="29741-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="29741-153">它會設定下拉式清單的資料，但您需要的是文字方塊。</span><span class="sxs-lookup"><span data-stu-id="29741-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="29741-154">以下列程式碼取代此方法：</span><span class="sxs-lookup"><span data-stu-id="29741-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="29741-155">此程式碼會卸載 `ViewBag` 語句，並為相關聯的 `OfficeAssignment` 實體新增積極式載入。</span><span class="sxs-lookup"><span data-stu-id="29741-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="29741-156">您無法使用 `Find` 方法執行積極式載入，因此會改為使用 `Where` 和 `Single` 方法來選取講師。</span><span class="sxs-lookup"><span data-stu-id="29741-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="29741-157">使用下列程式碼取代 `HttpPost` `Edit` 方法。</span><span class="sxs-lookup"><span data-stu-id="29741-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="29741-158">處理 office 指派更新的：</span><span class="sxs-lookup"><span data-stu-id="29741-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="29741-159">程式碼會執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="29741-159">The code does the following:</span></span>

- <span data-ttu-id="29741-160">針對 `OfficeAssignment` 導覽屬性使用積極式載入從資料庫中取得目前的 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="29741-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="29741-161">這與您在 `HttpGet` `Edit` 方法中的做法相同。</span><span class="sxs-lookup"><span data-stu-id="29741-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="29741-162">使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="29741-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="29741-163">使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)多載可讓您將想要包含的屬性*列入*允許清單。</span><span class="sxs-lookup"><span data-stu-id="29741-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="29741-164">這可避免過度張貼，如[第二個教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述。</span><span class="sxs-lookup"><span data-stu-id="29741-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="29741-165">如果辦公室位置為空白，則會將 `Instructor.OfficeAssignment` 屬性設為 null，以便刪除 `OfficeAssignment` 資料表中的相關資料列。</span><span class="sxs-lookup"><span data-stu-id="29741-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="29741-166">將變更儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="29741-166">Saves the changes to the database.</span></span>

<span data-ttu-id="29741-167">在 [ *Views\Instructor\Edit.cshtml*] 中，于 [**雇用日期**] 欄位的 `div` 專案之後，新增欄位以編輯辦公室位置：</span><span class="sxs-lookup"><span data-stu-id="29741-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="29741-168">執行頁面（選取 [**講師**] 索引標籤，然後按一下講師上的 [**編輯**]）。</span><span class="sxs-lookup"><span data-stu-id="29741-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="29741-169">變更 [辦公室位置]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="29741-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="29741-171">將課程指派加入至講師 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="29741-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="29741-172">講師可教授任何數量的課程。</span><span class="sxs-lookup"><span data-stu-id="29741-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="29741-173">現在您將藉由使用核取方塊群組，新增變更課程指派的能力來強化 Instructor [編輯] 頁面，如以下螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="29741-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="29741-175">`Course` 和 `Instructor` 實體之間的關聯性是多對多，這表示您沒有聯結資料表的直接存取權。</span><span class="sxs-lookup"><span data-stu-id="29741-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="29741-176">相反地，您會在 `Instructor.Courses` 導覽屬性中加入和移除實體。</span><span class="sxs-lookup"><span data-stu-id="29741-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="29741-177">可讓您變更講師指派之課程的 UI 為一組核取方塊。</span><span class="sxs-lookup"><span data-stu-id="29741-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="29741-178">資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="29741-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="29741-179">使用者可選取或清除核取方塊來變更課程指派。</span><span class="sxs-lookup"><span data-stu-id="29741-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="29741-180">如果課程數很大，您可能會想要使用不同的方法來呈現視圖中的資料，但是您會使用相同的方法來操作導覽屬性，以便建立或刪除關聯性。</span><span class="sxs-lookup"><span data-stu-id="29741-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="29741-181">若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。</span><span class="sxs-lookup"><span data-stu-id="29741-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="29741-182">在*viewmodel*資料夾中建立*AssignedCourseData.cs* ，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="29741-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="29741-183">在*InstructorController.cs*中，將 `HttpGet` `Edit` 方法取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="29741-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="29741-184">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="29741-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="29741-185">程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `AssignedCourseData` 檢視模型類別來呼叫新的 `PopulateAssignedCourseData` 方法以提供資訊給核取方塊陣列。</span><span class="sxs-lookup"><span data-stu-id="29741-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="29741-186">`PopulateAssignedCourseData` 方法中的程式碼會讀取所有 `Course` 實體，以便使用 view model 類別載入課程清單。</span><span class="sxs-lookup"><span data-stu-id="29741-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="29741-187">針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="29741-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="29741-188">若要在檢查課程是否指派給講師時建立有效率的查閱，指派給講師的課程會放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合中。</span><span class="sxs-lookup"><span data-stu-id="29741-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="29741-189">針對指派講師的課程，`Assigned` 屬性設定為 [`true`]。</span><span class="sxs-lookup"><span data-stu-id="29741-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="29741-190">檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。</span><span class="sxs-lookup"><span data-stu-id="29741-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="29741-191">最後，會將清單傳遞至 `ViewBag` 屬性中的 view。</span><span class="sxs-lookup"><span data-stu-id="29741-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="29741-192">接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="29741-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="29741-193">使用下列程式碼來取代 `HttpPost` `Edit` 方法，其會呼叫新的方法來更新 `Instructor` 實體的 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="29741-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="29741-194">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="29741-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="29741-195">由於此視圖沒有 `Course` 實體的集合，因此模型系結器無法自動更新 `Courses` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="29741-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="29741-196">您不需要使用模型系結器來更新課程導覽屬性，而是在新的 `UpdateInstructorCourses` 方法中這麼做。</span><span class="sxs-lookup"><span data-stu-id="29741-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="29741-197">因此您必須從模型繫結器中排除 `Courses` 屬性。</span><span class="sxs-lookup"><span data-stu-id="29741-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="29741-198">這不需要對呼叫[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的程式碼進行任何變更，因為您使用的是*允許清單*多載，而且 `Courses` 不在包含清單中。</span><span class="sxs-lookup"><span data-stu-id="29741-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="29741-199">如果未選取任何核取方塊，`UpdateInstructorCourses` 中的程式碼會使用空集合初始化 `Courses` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="29741-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="29741-200">程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。</span><span class="sxs-lookup"><span data-stu-id="29741-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="29741-201">為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。</span><span class="sxs-lookup"><span data-stu-id="29741-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="29741-202">若課程的核取方塊已被選取，但課程並未位於 `Instructor.Courses` 導覽屬性中，則課程便會新增至導覽屬性的集合中。</span><span class="sxs-lookup"><span data-stu-id="29741-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="29741-203">若課程的核取方塊未被選取，但課程卻位於 `Instructor.Courses` 導覽屬性中，則課程便會從導覽屬性的集合中移除。</span><span class="sxs-lookup"><span data-stu-id="29741-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="29741-204">在*Views\Instructor\Edit.cshtml*中，于 [`OfficeAssignment`] 欄位的 `div` 元素後面新增下列反白顯示的程式碼，以新增包含核取方塊陣列的**課程**欄位：</span><span class="sxs-lookup"><span data-stu-id="29741-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="29741-205">此程式碼會建立一個 HTML 表格，該表格中有三個資料行。</span><span class="sxs-lookup"><span data-stu-id="29741-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="29741-206">在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。</span><span class="sxs-lookup"><span data-stu-id="29741-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="29741-207">所有核取方塊都具有相同的名稱（"selectedCourses"），這會通知模型系結器將其視為群組。</span><span class="sxs-lookup"><span data-stu-id="29741-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="29741-208">當頁面張貼時，每個核取方塊的 `value` 屬性會設定為 `CourseID.` 的值，而模型系結器只會將陣列傳遞至控制器，其中只包含選取之核取方塊的 `CourseID` 值。</span><span class="sxs-lookup"><span data-stu-id="29741-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="29741-209">一開始呈現核取方塊時，指派給講師的課程會有 `checked` 的屬性（會將其顯示為已核取）。</span><span class="sxs-lookup"><span data-stu-id="29741-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="29741-210">變更課程指派之後，您會想要能夠在網站返回 [`Index`] 頁面時，確認變更。</span><span class="sxs-lookup"><span data-stu-id="29741-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="29741-211">因此，您必須將資料行加入該頁面中的資料表。</span><span class="sxs-lookup"><span data-stu-id="29741-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="29741-212">在這種情況下，您不需要使用 `ViewBag` 物件，因為您想要顯示的資訊已經在要當做模型傳遞至頁面之 `Instructor` 實體的 `Courses` 導覽屬性中。</span><span class="sxs-lookup"><span data-stu-id="29741-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="29741-213">在*Views\Instructor\Index.cshtml*中，于**Office**標題後面新增**課程**標題，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="29741-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="29741-214">然後緊接在 [office 位置詳細資料] 儲存格後面加入新的 [詳細資料] 資料格：</span><span class="sxs-lookup"><span data-stu-id="29741-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="29741-215">執行 [**講師索引**] 頁面，查看指派給每位講師的課程：</span><span class="sxs-lookup"><span data-stu-id="29741-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="29741-217">按一下講師上的 [**編輯**] 以查看 [編輯] 頁面。</span><span class="sxs-lookup"><span data-stu-id="29741-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="29741-219">變更一些課程指派，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="29741-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="29741-220">您所做的變更會反映在 [索引] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="29741-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="29741-221">注意：在有有限數目的課程時，用來編輯講師課程資料的方法會很有用。</span><span class="sxs-lookup"><span data-stu-id="29741-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="29741-222">針對更大的集合，將需要不同的 UI 和不同的更新方法。</span><span class="sxs-lookup"><span data-stu-id="29741-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  

## <a name="update-the-delete-method"></a><span data-ttu-id="29741-223">更新 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="29741-223">Update the Delete Method</span></span>

<span data-ttu-id="29741-224">變更 HttpPost Delete 方法中的程式碼，以便在刪除講師時刪除 office 指派記錄（如果有的話）：</span><span class="sxs-lookup"><span data-stu-id="29741-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

<span data-ttu-id="29741-225">如果您嘗試刪除以系統管理員身分指派給部門的講師，您會收到參考完整性錯誤。</span><span class="sxs-lookup"><span data-stu-id="29741-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="29741-226">請參閱[本教學課程的最新版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)，以取得其他程式碼，以自動將講師從指派為系統管理員的任何部門中移除。</span><span class="sxs-lookup"><span data-stu-id="29741-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="29741-227">總結</span><span class="sxs-lookup"><span data-stu-id="29741-227">Summary</span></span>

<span data-ttu-id="29741-228">您現在已完成本簡介以使用相關資料。</span><span class="sxs-lookup"><span data-stu-id="29741-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="29741-229">到目前為止，在這些教學課程中，您已完成完整的 CRUD 作業，但尚未處理並行問題。</span><span class="sxs-lookup"><span data-stu-id="29741-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="29741-230">下一個教學課程將介紹並行處理的主題、說明用來處理它的選項，以及對您已為一個實體類型撰寫的 CRUD 程式碼新增並行處理。</span><span class="sxs-lookup"><span data-stu-id="29741-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="29741-231">您可以在[本系列的最後一個教學](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)課程結尾處找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="29741-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="29741-232">[上一頁](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [下一頁](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="29741-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
