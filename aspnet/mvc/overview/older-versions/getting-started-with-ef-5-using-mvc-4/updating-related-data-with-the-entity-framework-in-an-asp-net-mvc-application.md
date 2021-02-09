---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 來更新相關資料 (6/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: dcdbd746aaa06d734f0d88b88e8d864e7e4ff5e7
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984929"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>使用 ASP.NET MVC 應用程式中的 Entity Framework 來更新相關資料 (6/10) 

由 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您顯示了相關的資料;在本教學課程中，您將更新相關的資料。 針對大部分的關聯性，您可以藉由更新適當的外鍵欄位來完成這項工作。 若為多對多關聯性，Entity Framework 不會直接公開聯結資料表，因此您必須在適當的導覽屬性中明確地加入和移除實體。

下列圖例顯示了您將操作的頁面。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>自訂 Courses 的 [建立] 和 [編輯] 頁面

當新的課程實體建立時，其必須要與現有的部門具有關聯性。 若要達成此目的，Scaffold 程式碼包含了控制器方法和 [建立] 和 [編輯] 檢視，當中包含了一個可選取部門的下拉式清單。 下拉式清單 `Course.DepartmentID` 會設定外鍵屬性，而這就是 `Department` 使用適當實體載入導覽屬性的所有 Entity Framework 需求 `Department` 。 您將使用 Scaffold 程式碼，但會稍微對其進行一些變更以新增錯誤處理及排序下拉式清單。

在 *CourseController.cs* 中，刪除四個 `Edit` 和 `Create` 方法，並以下列程式碼取代它們：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList`方法會取得依名稱排序的所有部門清單、建立 `SelectList` 下拉式清單的集合，並將集合傳遞至屬性中的視圖 `ViewBag` 。 方法接受選擇性的 `selectedDepartment` 參數，可允許呼叫程式碼在呈現下拉式清單時指定選取的項目。 此視圖會將名稱傳遞 `DepartmentID` 給 [ `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)，然後協助程式知道要在物件中尋找名為的 `ViewBag` `SelectList` `DepartmentID` 。

`HttpGet` `Create` 方法 `PopulateDepartmentsDropDownList` 會呼叫方法，而不會設定選取的專案，因為針對新的課程，尚未建立部門：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` 方法會根據已指派給所編輯課程的部門識別碼，設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpPost`和的方法 `Create` `Edit` 也包含程式碼，可在發生錯誤之後重新顯示頁面時，設定選取的專案：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

這段程式碼可確保當頁面重新顯示以顯示錯誤訊息時，所選取的部門會保持選取狀態。

在 *Views\Course\Create.cshtml* 中，新增醒目提示的程式碼，以在 [ **標題** ] 欄位之前建立新的課程編號欄位。 如先前的教學課程中所述，預設不會 scaffold 主鍵欄位，但此主鍵有意義，因此您希望使用者能夠輸入金鑰值。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

在 [ *Views\Course\Edit.cshtml*]、[ *Views\Course\Delete.cshtml*] 和 [ *Views\Course\Details.cshtml*] 中，于 [ **標題** ] 欄位之前新增 [課程號碼] 欄位。 因為它是主鍵，所以會顯示，但無法變更。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

執行 [ **建立** ] 頁面 (顯示 [課程索引] 頁面，然後按一下 [ **建立新** 的) 並輸入新課程的資料：

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

按一下頁面底部的 [新增]  。 [課程索引] 頁面隨即顯示，並將新的課程新增至清單中。 [索引] 頁面中的部門名稱來自於導覽屬性，顯示關聯性已正確建立。

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

執行 [ **編輯** ] 頁面 (顯示 [課程索引] 頁面，然後按一下課程) 上的 [ **編輯** ]。

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

變更頁面上的資料，然後按一下 [儲存]。 [課程索引] 頁面會顯示已更新的課程資料。

## <a name="adding-an-edit-page-for-instructors"></a>加入講師的編輯頁面

當您編輯講師記錄時，您可能會想要更新講師的辦公室指派。 `Instructor`實體與實體具有一對零或一關聯性 `OfficeAssignment` ，這表示您必須處理下列情況：

- 如果使用者清除辦公室指派，且原先具有值，您必須移除並刪除該 `OfficeAssignment` 實體。
- 如果使用者輸入辦公室指派值，而且最初是空的，您必須建立新的 `OfficeAssignment` 實體。
- 如果使用者變更了辦公室指派的值，您必須變更現有實體中的值 `OfficeAssignment` 。

開啟 *InstructorController.cs* ，並查看 `HttpGet` `Edit` 方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

這裡的 scaffold 程式碼並不是您要的。 它會設定下拉式清單的資料，但您需要的是文字方塊。 以下列程式碼取代此方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

此程式碼會卸載 `ViewBag` 語句，並加入相關實體的積極式載入 `OfficeAssignment` 。 您無法使用方法執行積極式載入 `Find` ，因此 `Where` `Single` 會改用和方法來選取講師。

`HttpPost` `Edit` 以下列程式碼取代方法。 這會處理 office 指派更新：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

此程式碼會執行下列動作：

- 針對 `OfficeAssignment` 導覽屬性使用積極式載入從資料庫中取得目前的 `Instructor` 實體。 這與您在方法中所做的一樣 `HttpGet` `Edit` 。
- 使用從模型繫結器取得的值更新擷取的 `Instructor` 實體。 使用的 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 多載可讓您將想要包含的屬性 *列入* 允許清單。 這可防止過度張貼，如 [第二個教學](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)課程中所述。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- 如果辦公室位置是空白的，則 `Instructor.OfficeAssignment` 會將屬性設定為 null，如此就會刪除資料表中的相關資料列 `OfficeAssignment` 。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- 將變更儲存到資料庫。

在 *Views\Instructor\Edit.cshtml* 中，于 `div` [ **雇用日期** ] 欄位的專案之後，新增欄位以編輯辦公室位置：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

執行頁面 (選取 [ **講師** ] 索引標籤，然後按一下 [講師]) 上的 [ **編輯** ]。 變更 [辦公室位置]，然後按一下 [儲存]。

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>將課程指派新增至講師 [編輯] 頁面

講師可教授任何數量的課程。 現在您將藉由使用核取方塊群組，新增變更課程指派的能力來強化 Instructor [編輯] 頁面，如以下螢幕擷取畫面所示：

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

和實體之間的關聯性 `Course` `Instructor` 是多對多的，這表示您無法直接存取聯結資料表。 相反地，您會在導覽屬性中加入和移除實體 `Instructor.Courses` 。

可讓您變更講師指派之課程的 UI 為一組核取方塊。 資料庫中每個課程的核取方塊都會顯示，而該名講師目前受指派的課程會已選取狀態顯示。 使用者可選取或清除核取方塊來變更課程指派。 如果課程數目更大，您可能會想要使用不同的方法來呈現視圖中的資料，但您會使用相同的方法來操作導覽屬性，以便建立或刪除關聯性。

若要針對核取方塊清單提供資料給檢視，您必須使用一個檢視模型類別。 在 *viewmodel* 資料夾中建立 *AssignedCourseData.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

在 *InstructorController.cs* 中，以 `HttpGet` `Edit` 下列程式碼取代方法。 所做的變更已醒目提示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

程式碼會為 `Courses` 導覽屬性新增積極式載入，然後使用 `AssignedCourseData` 檢視模型類別來呼叫新的 `PopulateAssignedCourseData` 方法以提供資訊給核取方塊陣列。

方法中的程式碼會 `PopulateAssignedCourseData` 讀取所有 `Course` 的實體，以便使用 view 模型類別來載入課程清單。 針對每個課程，程式碼會檢查課程是否存在於講師的 `Courses` 導覽屬性中。 若要在檢查課程是否已指派給講師時建立有效率的查閱，指派給講師的課程會放在 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 集合中。 `Assigned` `true` 針對指派給講師的課程，屬性會設定為。 檢視會使用這個屬性，來判斷哪一個核取方塊必須顯示為已選取。 最後，會將清單傳遞至屬性中的 view `ViewBag` 。

接下來，新增當使用者按一下 [儲存] 時要執行的程式碼。 `HttpPost` `Edit` 以下列程式碼取代方法，這個程式碼會呼叫新方法，以更新 `Courses` 實體的導覽屬性 `Instructor` 。 所做的變更已醒目提示。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

因為 view 沒有實體集合，所以模型系結器 `Course` 無法自動更新 `Courses` 導覽屬性。 您不需要使用模型系結器來更新課程導覽屬性，而是在新的方法中進行 `UpdateInstructorCourses` 。 因此您必須從模型繫結器中排除 `Courses` 屬性。 這並不需要對呼叫 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 的程式碼進行任何變更，因為您使用的是 *允許清單* 多載，而且 `Courses` 不在包含清單中。

如果未選取任何核取方塊，則中的程式碼會 `UpdateInstructorCourses` 初始化 `Courses` 具有空集合的導覽屬性：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

程式碼會執行迴圈，尋訪資料庫中所有的課程，並檢查每個已指派給講師的課程，以及在檢視中選取的課程。 為了協助達成有效率的搜尋，後者的兩個集合會儲存在 `HashSet` 物件中。

若課程的核取方塊已被選取，但課程並未位於 `Instructor.Courses` 導覽屬性中，則課程便會新增至導覽屬性的集合中。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

若課程的核取方塊未被選取，但課程卻位於 `Instructor.Courses` 導覽屬性中，則課程便會從導覽屬性的集合中移除。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

在 *Views\Instructor\Edit.cshtml* 中，將下列醒目提示的程式碼新增至欄位的元素後面，以新增核取方塊陣列的 **課程** 欄位 `div` `OfficeAssignment` ：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

此程式碼會建立一個 HTML 表格，該表格中有三個資料行。 在每個資料行中，核取方塊的後方會是由課程號碼和標題組成的標題。 所有的核取方塊都有相同的名稱 ( "selectedCourses" ) ，這會通知模型系結器將它們視為群組。 `value`每個核取方塊的屬性（attribute）都會設定為頁面張貼時的值，模型系結器會將 `CourseID.` 陣列傳遞至控制器，其中只包含所 `CourseID` 選核取方塊的值。

首次轉譯這些核取方塊時，指派給講師之課程的屬性會選取這些 `checked` 屬性 (顯示已核取的) 。

變更課程指派之後，您會想要能夠在網站返回頁面時驗證變更 `Index` 。 因此，您需要將資料行加入至該頁面中的資料表。 在此情況下，您不需要使用 `ViewBag` 物件，因為您想要顯示的資訊已經在您要以 `Courses` `Instructor` 模型的形式傳遞至頁面之實體的導覽屬性中。

在 *Views\Instructor\Index.cshtml* 中，于 **Office** 標題之後立即新增 **課程** 標題，如下列範例所示：

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

然後，在 [辦公室位置詳細資料] 資料格之後，立即新增詳細資料資料格：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

執行 **講師索引** 頁面以查看指派給每個講師的課程：

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

按一下講師上的 [ **編輯** ] 以查看 [編輯] 頁面。

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

變更一些課程指派，然後按一下 [ **儲存**]。 您所做的變更會反映在 [索引] 頁面上。

 注意：編輯講師課程資料所需的方法，在有數量有限的課程時就能順利運作。 針對更大的集合，將需要不同的 UI 和不同的更新方法。  

## <a name="update-the-delete-method"></a>更新 Delete 方法

變更 HttpPost Delete 方法中的程式碼，如此一來，當刪除講師時，office 指派記錄 () 會刪除：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

如果您嘗試刪除以系統管理員身分指派給部門的講師，您將會收到參考完整性錯誤。 請參閱 [本教學課程的目前版本](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) ，以取得其他程式碼，該程式碼將會自動從任何系所指派為系統管理員的部門中移除講師。

## <a name="summary"></a>摘要

您現在已完成本簡介來使用相關資料。 到目前為止，在這些教學課程中，您已完成一系列的 CRUD 作業，但尚未處理並行問題。 下一個教學課程將介紹平行存取的主題、說明處理的選項，以及將並行處理新增至您已經為一種實體類型撰寫的 CRUD 程式碼。

您可以在 [本系列的最後一個教學](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)課程結尾處找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
