---
title: ASP.NET Core 中的 Razor 頁面與 EF Core - 更新相關資料 - 7/8
author: rick-anderson
description: 在本教學課程中，您會藉由更新外部索引鍵欄位和導覽屬性來更新相關資料。
ms.author: riande
ms.date: 11/15/2017
uid: data/ef-rp/update-related-data
ms.openlocfilehash: 4306118240c052585a5c2eeb2053ce03534b547c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57061215"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---update-related-data---7-of-8"></a><span data-ttu-id="50b5a-103">ASP.NET Core 中的 Razor 頁面與 EF Core - 更新相關資料 - 7/8</span><span class="sxs-lookup"><span data-stu-id="50b5a-103">Razor Pages with EF Core in ASP.NET Core - Update Related Data - 7 of 8</span></span>

<span data-ttu-id="50b5a-104">作者：[Tom Dykstra](https://github.com/tdykstra) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="50b5a-104">By [Tom Dykstra](https://github.com/tdykstra), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="50b5a-105">本教學課程將示範如何更新相關資料。</span><span class="sxs-lookup"><span data-stu-id="50b5a-105">This tutorial demonstrates updating related data.</span></span> <span data-ttu-id="50b5a-106">若您遇到無法解決的問題，請[下載或檢視完整應用程式。](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)</span><span class="sxs-lookup"><span data-stu-id="50b5a-106">If you run into problems you can't solve, [download or view the completed app.](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)</span></span> <span data-ttu-id="50b5a-107">[下載指示](xref:index#how-to-download-a-sample)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-107">[Download instructions](xref:index#how-to-download-a-sample).</span></span>

<span data-ttu-id="50b5a-108">下圖顯示一些完成的頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-108">The following illustrations shows some of the completed pages.</span></span>

<span data-ttu-id="50b5a-109">![課程 [編輯] 頁面](update-related-data/_static/course-edit.png)
![講師 [編輯] 頁面](update-related-data/_static/instructor-edit-courses.png)</span><span class="sxs-lookup"><span data-stu-id="50b5a-109">![Course Edit page](update-related-data/_static/course-edit.png)
![Instructor Edit page](update-related-data/_static/instructor-edit-courses.png)</span></span>

<span data-ttu-id="50b5a-110">檢查並測試 *Create* 與 *Edit* 課程頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-110">Examine and test the Create and Edit course pages.</span></span> <span data-ttu-id="50b5a-111">建立新的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-111">Create a new course.</span></span> <span data-ttu-id="50b5a-112">部門是依照其主索引鍵 (整數) 來進行選取，而不是它的名稱。</span><span class="sxs-lookup"><span data-stu-id="50b5a-112">The department is selected by its primary key (an integer), not its name.</span></span> <span data-ttu-id="50b5a-113">編輯新的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-113">Edit the new course.</span></span> <span data-ttu-id="50b5a-114">當您完成測試時，請刪除新的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-114">When you have finished testing, delete the new course.</span></span>

## <a name="create-a-base-class-to-share-common-code"></a><span data-ttu-id="50b5a-115">建立要共用通用程式碼的基底類別</span><span class="sxs-lookup"><span data-stu-id="50b5a-115">Create a base class to share common code</span></span>

<span data-ttu-id="50b5a-116">`Courses/Create` 和 `Courses/Edit` 頁面每個都需要部門名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="50b5a-116">The Courses/Create and Courses/Edit pages each need a list of department names.</span></span> <span data-ttu-id="50b5a-117">請針對 *Create* 和 *Edit* 頁面建立 *Pages/Courses/DepartmentNamePageModel.cshtml.cs* 基底類別：</span><span class="sxs-lookup"><span data-stu-id="50b5a-117">Create the *Pages/Courses/DepartmentNamePageModel.cshtml.cs* base class for the Create and Edit pages:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/DepartmentNamePageModel.cshtml.cs?highlight=9,11,20-21)]

<span data-ttu-id="50b5a-118">上述程式碼會建立 [SelectList](/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) 以包含部門名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="50b5a-118">The preceding code creates a [SelectList](/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) to contain the list of department names.</span></span> <span data-ttu-id="50b5a-119">如果指定了 `selectedDepartment`，就會在 `SelectList` 中選取該部門。</span><span class="sxs-lookup"><span data-stu-id="50b5a-119">If `selectedDepartment` is specified, that department is selected in the `SelectList`.</span></span>

<span data-ttu-id="50b5a-120">*Create* 和 *Edit* 頁面模型類別將衍生自 `DepartmentNamePageModel`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-120">The Create and Edit page model classes will derive from `DepartmentNamePageModel`.</span></span>

## <a name="customize-the-courses-pages"></a><span data-ttu-id="50b5a-121">自訂 [課程] 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-121">Customize the Courses Pages</span></span>

<span data-ttu-id="50b5a-122">當新的課程實體建立時，其必須要與現有的部門具有關聯性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="50b5a-123">為了在建立課程新增部門，*Create* 和 *Edit* 的基底類別包含用來選取部門的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="50b5a-123">To add a department while creating a course, the base class for Create and Edit contains a drop-down list for selecting the department.</span></span> <span data-ttu-id="50b5a-124">下拉式清單會設定 `Course.DepartmentID` 外部索引鍵 (FK) 屬性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-124">The drop-down list sets the `Course.DepartmentID` foreign key (FK) property.</span></span> <span data-ttu-id="50b5a-125">EF Core 則使用 `Course.DepartmentID` FK 來載入 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-125">EF Core uses the `Course.DepartmentID` FK to load the `Department` navigation property.</span></span>

![建立課程](update-related-data/_static/ddl.png)

<span data-ttu-id="50b5a-127">以下列程式碼更新 *Create* 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-127">Update the Create page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Create.cshtml.cs?highlight=7,18,32-999)]

<span data-ttu-id="50b5a-128">上述程式碼：</span><span class="sxs-lookup"><span data-stu-id="50b5a-128">The preceding code:</span></span>

* <span data-ttu-id="50b5a-129">衍生自 `DepartmentNamePageModel`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-129">Derives from `DepartmentNamePageModel`.</span></span>
* <span data-ttu-id="50b5a-130">使用 `TryUpdateModelAsync` 來防止[大量指派](xref:data/ef-rp/crud#overposting) (overposting)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-130">Uses `TryUpdateModelAsync` to prevent [overposting](xref:data/ef-rp/crud#overposting).</span></span>
* <span data-ttu-id="50b5a-131">以 `DepartmentNameSL` (來自基底類別) 取代 `ViewData["DepartmentID"]`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-131">Replaces `ViewData["DepartmentID"]` with `DepartmentNameSL` (from the base class).</span></span>

<span data-ttu-id="50b5a-132">`ViewData["DepartmentID"]` 已取代為強型別的 `DepartmentNameSL`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-132">`ViewData["DepartmentID"]` is replaced with the strongly typed `DepartmentNameSL`.</span></span> <span data-ttu-id="50b5a-133">強型別的模型優先於弱型別。</span><span class="sxs-lookup"><span data-stu-id="50b5a-133">Strongly typed models are preferred over weakly typed.</span></span> <span data-ttu-id="50b5a-134">如需詳細資訊，請參閱[弱型別資料 (ViewData 和 ViewBag)](xref:mvc/views/overview#VD_VB)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-134">For more information, see [Weakly typed data (ViewData and ViewBag)](xref:mvc/views/overview#VD_VB).</span></span>

### <a name="update-the-courses-create-page"></a><span data-ttu-id="50b5a-135">更新 Courses 的 *Create* 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-135">Update the Courses Create page</span></span>

<span data-ttu-id="50b5a-136">以下列標記更新 *Pages/Courses/Create.cshtml*：</span><span class="sxs-lookup"><span data-stu-id="50b5a-136">Update *Pages/Courses/Create.cshtml* with the following markup:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Courses/Create.cshtml?highlight=29-34)]

<span data-ttu-id="50b5a-137">上述標記會進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="50b5a-137">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="50b5a-138">將標題從 **DepartmentID** 變更為 **Department**。</span><span class="sxs-lookup"><span data-stu-id="50b5a-138">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="50b5a-139">以 `DepartmentNameSL` (來自基底類別) 取代 `"ViewBag.DepartmentID"`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-139">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>
* <span data-ttu-id="50b5a-140">新增 [選取部門] 選項。</span><span class="sxs-lookup"><span data-stu-id="50b5a-140">Adds the "Select Department" option.</span></span> <span data-ttu-id="50b5a-141">這項變更會呈現 [選取部門] ，而不是第一個部門。</span><span class="sxs-lookup"><span data-stu-id="50b5a-141">This change renders "Select Department" rather than the first department.</span></span>
* <span data-ttu-id="50b5a-142">未選取部門時，請新增驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="50b5a-142">Adds a validation message when the department isn't selected.</span></span>

<span data-ttu-id="50b5a-143">Razor 頁面使用[選取標籤協助程式](xref:mvc/views/working-with-forms#the-select-tag-helper)：</span><span class="sxs-lookup"><span data-stu-id="50b5a-143">The Razor Page uses the [Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper):</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Courses/Create.cshtml?range=28-35&highlight=3-6)]

<span data-ttu-id="50b5a-144">測試 *Create* 頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-144">Test the Create page.</span></span> <span data-ttu-id="50b5a-145">*Create* 頁面會顯示部門名稱，而不是部門識別碼。</span><span class="sxs-lookup"><span data-stu-id="50b5a-145">The Create page displays the department name rather than the department ID.</span></span>

### <a name="update-the-courses-edit-page"></a><span data-ttu-id="50b5a-146">更新 Courses 的 *Edit* 頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-146">Update the Courses Edit page.</span></span>

<span data-ttu-id="50b5a-147">以下列程式碼更新 *Edit* 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-147">Update the edit page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Edit.cshtml.cs?highlight=8,28,35,36,40,47-999)]

<span data-ttu-id="50b5a-148">這些變更類似於 *Create* 頁面模型中所做的變更。</span><span class="sxs-lookup"><span data-stu-id="50b5a-148">The changes are similar to those made in the Create page model.</span></span> <span data-ttu-id="50b5a-149">在上述程式碼中，`PopulateDepartmentsDropDownList` 會傳入部門識別碼，以選取下拉式清單中指定的部門。</span><span class="sxs-lookup"><span data-stu-id="50b5a-149">In the preceding code, `PopulateDepartmentsDropDownList` passes in the department ID, which select the department specified in the drop-down list.</span></span>

<span data-ttu-id="50b5a-150">以下列標記更新 *Pages/Courses/Edit.cshtml*：</span><span class="sxs-lookup"><span data-stu-id="50b5a-150">Update *Pages/Courses/Edit.cshtml* with the following markup:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Courses/Edit.cshtml?highlight=17-20,32-35)]

<span data-ttu-id="50b5a-151">上述標記會進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="50b5a-151">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="50b5a-152">顯示課程識別碼。</span><span class="sxs-lookup"><span data-stu-id="50b5a-152">Displays the course ID.</span></span> <span data-ttu-id="50b5a-153">通常不會顯示實體的主索引鍵 (PK)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-153">Generally the Primary Key (PK) of an entity isn't displayed.</span></span> <span data-ttu-id="50b5a-154">PK 對使用者來說通常是沒有意義的。</span><span class="sxs-lookup"><span data-stu-id="50b5a-154">PKs are usually meaningless to users.</span></span> <span data-ttu-id="50b5a-155">在此情況下，PK 是課程編號。</span><span class="sxs-lookup"><span data-stu-id="50b5a-155">In this case, the PK is the course number.</span></span>
* <span data-ttu-id="50b5a-156">將標題從 **DepartmentID** 變更為 **Department**。</span><span class="sxs-lookup"><span data-stu-id="50b5a-156">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="50b5a-157">以 `DepartmentNameSL` (來自基底類別) 取代 `"ViewBag.DepartmentID"`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-157">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>

<span data-ttu-id="50b5a-158">此頁面包含課程編號的隱藏欄位 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-158">The page contains a hidden field (`<input type="hidden">`) for the course number.</span></span> <span data-ttu-id="50b5a-159">新增 `<label>` 標籤協助程式與 `asp-for="Course.CourseID"` 無法免除隱藏欄位的需求。</span><span class="sxs-lookup"><span data-stu-id="50b5a-159">Adding a `<label>` tag helper with `asp-for="Course.CourseID"` doesn't eliminate the need for the hidden field.</span></span> <span data-ttu-id="50b5a-160">當使用者按一下 [儲存]  時，需要有 `<input type="hidden">` 才能將課程編號包含在張貼資料中。</span><span class="sxs-lookup"><span data-stu-id="50b5a-160">`<input type="hidden">` is required for the course number to be included in the posted data when the user clicks **Save**.</span></span>

<span data-ttu-id="50b5a-161">測試更新過的程式碼。</span><span class="sxs-lookup"><span data-stu-id="50b5a-161">Test the updated code.</span></span> <span data-ttu-id="50b5a-162">建立、編輯和刪除課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-162">Create, edit, and delete a course.</span></span>

## <a name="add-asnotracking-to-the-details-and-delete-page-models"></a><span data-ttu-id="50b5a-163">將 AsNoTracking 新增至 *Details* 和 *Delete* 頁面模型</span><span class="sxs-lookup"><span data-stu-id="50b5a-163">Add AsNoTracking to the Details and Delete page models</span></span>

<span data-ttu-id="50b5a-164">不需要追蹤時，[AsNoTracking](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) 可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="50b5a-164">[AsNoTracking](/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) can improve performance when tracking isn't required.</span></span> <span data-ttu-id="50b5a-165">將 `AsNoTracking` 新增至 *Delete* 和 *Details* 頁面模型。</span><span class="sxs-lookup"><span data-stu-id="50b5a-165">Add `AsNoTracking` to the Delete and Details page model.</span></span> <span data-ttu-id="50b5a-166">下列程式碼顯示已更新的 *Delete* 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-166">The following code shows the updated Delete page model:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Delete.cshtml.cs?name=snippet&highlight=21,23,40,41)]

<span data-ttu-id="50b5a-167">在 *Pages/Courses/Details.cshtml.cs* 檔案中更新 `OnGetAsync` 方法：</span><span class="sxs-lookup"><span data-stu-id="50b5a-167">Update the `OnGetAsync` method in the *Pages/Courses/Details.cshtml.cs* file:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Courses/Details.cshtml.cs?name=snippet)]

### <a name="modify-the-delete-and-details-pages"></a><span data-ttu-id="50b5a-168">修改 *Delete* 和 *Details* 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-168">Modify the Delete and Details pages</span></span>

<span data-ttu-id="50b5a-169">以下列標記更新 [刪除 Razor] 頁面：</span><span class="sxs-lookup"><span data-stu-id="50b5a-169">Update the Delete Razor page with the following markup:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Courses/Delete.cshtml?highlight=15-20)]

<span data-ttu-id="50b5a-170">對 *Details* 頁面進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="50b5a-170">Make the same changes to the Details page.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="50b5a-171">測試 [課程] 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-171">Test the Course pages</span></span>

<span data-ttu-id="50b5a-172">測試建立、編輯、詳細資料和刪除。</span><span class="sxs-lookup"><span data-stu-id="50b5a-172">Test create, edit, details, and delete.</span></span>

## <a name="update-the-instructor-pages"></a><span data-ttu-id="50b5a-173">更新講師頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-173">Update the instructor pages</span></span>

<span data-ttu-id="50b5a-174">下列各節會更新講師頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-174">The following sections update the instructor pages.</span></span>

### <a name="add-office-location"></a><span data-ttu-id="50b5a-175">新增辦公室位置</span><span class="sxs-lookup"><span data-stu-id="50b5a-175">Add office location</span></span>

<span data-ttu-id="50b5a-176">當您編輯講師記錄時，可能會想要更新講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="50b5a-176">When editing an instructor record, you may want to update the instructor's office assignment.</span></span> <span data-ttu-id="50b5a-177">`Instructor` 實體與 `OfficeAssignment` 實體具有一對零或一的關聯性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-177">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity.</span></span> <span data-ttu-id="50b5a-178">必須處理講師程式碼：</span><span class="sxs-lookup"><span data-stu-id="50b5a-178">The instructor code must handle:</span></span>

* <span data-ttu-id="50b5a-179">如果使用者清除辦公室指派，請刪除 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-179">If the user clears the office assignment, delete the `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="50b5a-180">如果使用者輸入辦公室指派，但它是空的，請建立新的 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-180">If the user enters an office assignment and it was empty, create a new `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="50b5a-181">如果使用者變更辦公室指派，請更新 `OfficeAssignment` 實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-181">If the user changes the office assignment, update the `OfficeAssignment` entity.</span></span>

<span data-ttu-id="50b5a-182">以下列程式碼更新講師 [編輯] 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-182">Update the instructors Edit page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Edit1.cshtml.cs?name=snippet&highlight=20-23,32,39-999)]

<span data-ttu-id="50b5a-183">上述程式碼：</span><span class="sxs-lookup"><span data-stu-id="50b5a-183">The preceding code:</span></span>

- <span data-ttu-id="50b5a-184">針對 `OfficeAssignment` 導覽屬性使用積極式載入從資料庫中取得目前的 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-184">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span>
- <span data-ttu-id="50b5a-185">使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-185">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="50b5a-186">`TryUpdateModel` 會防止[大量指派](xref:data/ef-rp/crud#overposting) (overposting)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-186">`TryUpdateModel` prevents [overposting](xref:data/ef-rp/crud#overposting).</span></span>
- <span data-ttu-id="50b5a-187">如果辦公室位置為空白，請將 `Instructor.OfficeAssignment` 設定為 Null。</span><span class="sxs-lookup"><span data-stu-id="50b5a-187">If the office location is blank, sets `Instructor.OfficeAssignment` to null.</span></span> <span data-ttu-id="50b5a-188">當 `Instructor.OfficeAssignment` 為 Null 時，將會刪除 `OfficeAssignment` 資料表中的相關資料列。</span><span class="sxs-lookup"><span data-stu-id="50b5a-188">When `Instructor.OfficeAssignment` is null, the related row in the `OfficeAssignment` table is deleted.</span></span>

### <a name="update-the-instructor-edit-page"></a><span data-ttu-id="50b5a-189">更新講師 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-189">Update the instructor Edit page</span></span>

<span data-ttu-id="50b5a-190">使用辦公室位置更新 *Pages/Instructors/Edit.cshtml*：</span><span class="sxs-lookup"><span data-stu-id="50b5a-190">Update *Pages/Instructors/Edit.cshtml* with the office location:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Instructors/Edit1.cshtml?highlight=29-33)]

<span data-ttu-id="50b5a-191">請確認您可以變更講師辦公室位置。</span><span class="sxs-lookup"><span data-stu-id="50b5a-191">Verify you can change an instructors office location.</span></span>

## <a name="add-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="50b5a-192">將課程指派新增至講師 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-192">Add Course assignments to the instructor Edit page</span></span>

<span data-ttu-id="50b5a-193">講師可教授任何數量的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-193">Instructors may teach any number of courses.</span></span> <span data-ttu-id="50b5a-194">在本節中，您可以新增變更課程指派的能力。</span><span class="sxs-lookup"><span data-stu-id="50b5a-194">In this section, you add the ability to change course assignments.</span></span> <span data-ttu-id="50b5a-195">下圖顯示已更新的講師 [編輯] 頁面：</span><span class="sxs-lookup"><span data-stu-id="50b5a-195">The following image shows the updated instructor Edit page:</span></span>

![講師 [編輯] 頁面與課程](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="50b5a-197">`Course` 和 `Instructor` 具有多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-197">`Course` and `Instructor` has a many-to-many relationship.</span></span> <span data-ttu-id="50b5a-198">若要新增和移除關聯性，您必須在 `CourseAssignments` 聯結實體集中新增和移除實體。</span><span class="sxs-lookup"><span data-stu-id="50b5a-198">To add and remove relationships, you add and remove entities from the `CourseAssignments` join entity set.</span></span>

<span data-ttu-id="50b5a-199">核取方塊可變更指派給講師的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-199">Check boxes enable changes to courses an instructor is assigned to.</span></span> <span data-ttu-id="50b5a-200">資料庫中的每個課程各顯示一個核取方塊。</span><span class="sxs-lookup"><span data-stu-id="50b5a-200">A check box is displayed for every course in the database.</span></span> <span data-ttu-id="50b5a-201">已核取指派給講師的課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-201">Courses that the instructor is assigned to are checked.</span></span> <span data-ttu-id="50b5a-202">使用者可選取或清除核取方塊來變更課程指派。</span><span class="sxs-lookup"><span data-stu-id="50b5a-202">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="50b5a-203">如果課程數目大上許多：</span><span class="sxs-lookup"><span data-stu-id="50b5a-203">If the number of courses were much greater:</span></span>

* <span data-ttu-id="50b5a-204">您可能會使用不同的使用者介面來顯示課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-204">You'd probably use a different user interface to display the courses.</span></span>
* <span data-ttu-id="50b5a-205">操作聯結實體來建立或刪除關聯性的方法不會變更。</span><span class="sxs-lookup"><span data-stu-id="50b5a-205">The method of manipulating a join entity to create or delete relationships wouldn't change.</span></span>

### <a name="add-classes-to-support-create-and-edit-instructor-pages"></a><span data-ttu-id="50b5a-206">新增類別來支援 *Create* 和 *Edit* 講師頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-206">Add classes to support Create and Edit instructor pages</span></span>

<span data-ttu-id="50b5a-207">以下列程式碼建立 *SchoolViewModels/AssignedCourseData.cs*：</span><span class="sxs-lookup"><span data-stu-id="50b5a-207">Create *SchoolViewModels/AssignedCourseData.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

<span data-ttu-id="50b5a-208">`AssignedCourseData` 類別包含資料，用來建立講師所指派課程的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="50b5a-208">The `AssignedCourseData` class contains data to create the check boxes for assigned courses by an instructor.</span></span>

<span data-ttu-id="50b5a-209">建立 *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* 基底類別：</span><span class="sxs-lookup"><span data-stu-id="50b5a-209">Create the *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* base class:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/InstructorCoursesPageModel.cshtml.cs)]

<span data-ttu-id="50b5a-210">`InstructorCoursesPageModel` 是您將用於 *Edit* 和 *Create* 頁面模型的基底類別。</span><span class="sxs-lookup"><span data-stu-id="50b5a-210">The `InstructorCoursesPageModel` is the base class you will use for the Edit and Create page models.</span></span> <span data-ttu-id="50b5a-211">`PopulateAssignedCourseData` 會讀取所有 `Course` 實體來擴展 `AssignedCourseDataList`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-211">`PopulateAssignedCourseData` reads all `Course` entities to populate `AssignedCourseDataList`.</span></span> <span data-ttu-id="50b5a-212">對於每個課程，此程式碼設定 `CourseID`、標題以及是否將講師指派給課程。</span><span class="sxs-lookup"><span data-stu-id="50b5a-212">For each course, the code sets the `CourseID`, title, and whether or not the instructor is assigned to the course.</span></span> <span data-ttu-id="50b5a-213">[HashSet](/dotnet/api/system.collections.generic.hashset-1) 用來建立有效查閱。</span><span class="sxs-lookup"><span data-stu-id="50b5a-213">A [HashSet](/dotnet/api/system.collections.generic.hashset-1) is used to create efficient lookups.</span></span>

### <a name="instructors-edit-page-model"></a><span data-ttu-id="50b5a-214">講師 *Edit* 頁面模型</span><span class="sxs-lookup"><span data-stu-id="50b5a-214">Instructors Edit page model</span></span>

<span data-ttu-id="50b5a-215">以下列程式碼更新講師 [編輯] 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-215">Update the instructor Edit page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Edit.cshtml.cs?name=snippet&highlight=1,20-24,30,34,41-999)]

<span data-ttu-id="50b5a-216">上述程式碼會處理辦公室指派變更。</span><span class="sxs-lookup"><span data-stu-id="50b5a-216">The preceding code handles office assignment changes.</span></span>

<span data-ttu-id="50b5a-217">更新講師 Razor 檢視：</span><span class="sxs-lookup"><span data-stu-id="50b5a-217">Update the instructor Razor View:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Instructors/Edit.cshtml?highlight=34-59)]

<a id="notepad"></a>
> [!NOTE]
> <span data-ttu-id="50b5a-218">當您將程式碼貼上到 Visual Studio 時，分行符號可能會產生變更，致使程式碼失效。</span><span class="sxs-lookup"><span data-stu-id="50b5a-218">When you paste the code in Visual Studio, line breaks are changed in a way that breaks the code.</span></span> <span data-ttu-id="50b5a-219">按下 Ctrl+Z 來復原自動格式化。</span><span class="sxs-lookup"><span data-stu-id="50b5a-219">Press Ctrl+Z one time to undo the automatic formatting.</span></span> <span data-ttu-id="50b5a-220">Ctrl+Z 會修正分行符號，使它們看起來就跟您在這裡看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="50b5a-220">Ctrl+Z fixes the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="50b5a-221">縮排不一定要是完美的，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@:</tr>` 必須要如顯示般各自在獨立的一行上。</span><span class="sxs-lookup"><span data-stu-id="50b5a-221">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown.</span></span> <span data-ttu-id="50b5a-222">當選取新的程式碼區塊時，按下 Tab 鍵三次來讓新的程式碼對準現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="50b5a-222">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span> <span data-ttu-id="50b5a-223">[使用此連結](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)票選或檢閱這個錯誤的狀態。</span><span class="sxs-lookup"><span data-stu-id="50b5a-223">Vote on or review the status of this bug [with this link](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html).</span></span>

<span data-ttu-id="50b5a-224">上述程式碼會建立一個 HTML 資料表，該資料表中有三個資料行。</span><span class="sxs-lookup"><span data-stu-id="50b5a-224">The preceding code creates an HTML table that has three columns.</span></span> <span data-ttu-id="50b5a-225">每個資料行都有一個核取方塊，以及內含課程編號和標題 (title) 的標題 (caption)。</span><span class="sxs-lookup"><span data-stu-id="50b5a-225">Each column has a check box and a caption containing the course number and title.</span></span> <span data-ttu-id="50b5a-226">所有核取方塊都具有相同的名稱 ("selectedCourses")。</span><span class="sxs-lookup"><span data-stu-id="50b5a-226">The check boxes all have the same name ("selectedCourses").</span></span> <span data-ttu-id="50b5a-227">使用相同的名稱可告知模型繫結器將它們視為一個群組。</span><span class="sxs-lookup"><span data-stu-id="50b5a-227">Using the same name informs the model binder to treat them as a group.</span></span> <span data-ttu-id="50b5a-228">每個核取方塊的 Value 屬性都會設定為 `CourseID`。</span><span class="sxs-lookup"><span data-stu-id="50b5a-228">The value attribute of each check box is set to `CourseID`.</span></span> <span data-ttu-id="50b5a-229">當頁面發佈時，模型繫結器便會傳遞只包含所選取核取方塊之 `CourseID` 值的陣列。</span><span class="sxs-lookup"><span data-stu-id="50b5a-229">When the page is posted, the model binder passes an array that consists of the `CourseID` values for only the check boxes that are selected.</span></span>

<span data-ttu-id="50b5a-230">一開始呈現核取方塊時，指派給講師的課程已核取屬性。</span><span class="sxs-lookup"><span data-stu-id="50b5a-230">When the check boxes are initially rendered, courses assigned to the instructor have checked attributes.</span></span>

<span data-ttu-id="50b5a-231">執行應用程式，並測試已更新的講師 [編輯] 頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-231">Run the app and test the updated instructors Edit page.</span></span> <span data-ttu-id="50b5a-232">變更一些課程指派。</span><span class="sxs-lookup"><span data-stu-id="50b5a-232">Change some course assignments.</span></span> <span data-ttu-id="50b5a-233">所做的變更會反映在 [索引] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="50b5a-233">The changes are reflected on the Index page.</span></span>

<span data-ttu-id="50b5a-234">注意:這裡所用來編輯講師課程資料的方法在課程的數量有限時運作相當良好。</span><span class="sxs-lookup"><span data-stu-id="50b5a-234">Note: The approach taken here to edit instructor course data works well when there's a limited number of courses.</span></span> <span data-ttu-id="50b5a-235">針對更大的集合，不同的 UI 和不同的更新方法可能更有用且更有效率。</span><span class="sxs-lookup"><span data-stu-id="50b5a-235">For collections that are much larger, a different UI and a different updating method would be more useable and efficient.</span></span>

### <a name="update-the-instructors-create-page"></a><span data-ttu-id="50b5a-236">更新講師 *Create* 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-236">Update the instructors Create page</span></span>

<span data-ttu-id="50b5a-237">以下列程式碼更新講師 *Create* 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-237">Update the instructor Create page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Create.cshtml.cs)]

<span data-ttu-id="50b5a-238">上述程式碼類似於 *Pages/Instructors/Edit.cshtml.cs* 程式碼。</span><span class="sxs-lookup"><span data-stu-id="50b5a-238">The preceding code is similar to the *Pages/Instructors/Edit.cshtml.cs* code.</span></span>

<span data-ttu-id="50b5a-239">以下列標記更新講師 [建立 Razor] 頁面：</span><span class="sxs-lookup"><span data-stu-id="50b5a-239">Update the instructor Create Razor page with the following markup:</span></span>

[!code-cshtml[](intro/samples/cu/Pages/Instructors/Create.cshtml?highlight=32-62)]

<span data-ttu-id="50b5a-240">測試講師 *Create* 頁面。</span><span class="sxs-lookup"><span data-stu-id="50b5a-240">Test the instructor Create page.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="50b5a-241">更新 *Delete* 頁面</span><span class="sxs-lookup"><span data-stu-id="50b5a-241">Update the Delete page</span></span>

<span data-ttu-id="50b5a-242">以下列程式碼更新 *Delete* 頁面模型：</span><span class="sxs-lookup"><span data-stu-id="50b5a-242">Update the Delete page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Instructors/Delete.cshtml.cs?highlight=5,40-999)]

<span data-ttu-id="50b5a-243">上述程式碼會進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="50b5a-243">The preceding code makes the following changes:</span></span>

* <span data-ttu-id="50b5a-244">為 `CourseAssignments` 導覽屬性使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="50b5a-244">Uses eager loading for the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="50b5a-245">必須包含 `CourseAssignments`，否則刪除講師時不會刪除它們。</span><span class="sxs-lookup"><span data-stu-id="50b5a-245">`CourseAssignments` must be included or they aren't deleted when the instructor is deleted.</span></span> <span data-ttu-id="50b5a-246">若要避免需要讀取們，您可以在資料庫中設定串聯刪除。</span><span class="sxs-lookup"><span data-stu-id="50b5a-246">To avoid needing to read them, configure cascade delete in the database.</span></span>

* <span data-ttu-id="50b5a-247">若要刪除的講師已指派為任何部門的系統管理員，請先從這些部門中移除講師的指派。</span><span class="sxs-lookup"><span data-stu-id="50b5a-247">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="50b5a-248">[上一頁](xref:data/ef-rp/read-related-data)
> [下一頁](xref:data/ef-rp/concurrency)</span><span class="sxs-lookup"><span data-stu-id="50b5a-248">[Previous](xref:data/ef-rp/read-related-data)
[Next](xref:data/ef-rp/concurrency)</span></span>
