---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 適用于 MVC Web 應用程式的 Advanced Entity Framework 案例 (10/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85dd59016d904a9f654c438db977b5ae2c0187d2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045048"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>適用于 MVC Web 應用程式的 Advanced Entity Framework 案例 (10/10) 

由 [Tom Dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從開頭開始進行教學課程系列，或 [下載此章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md) ，從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已實作為存放庫和工作單元模式。 本教學課程涵蓋下列主題：

- 執行原始 SQL 查詢。
- 執行無追蹤查詢。
- 檢查傳送至資料庫的查詢。
- 使用 proxy 類別。
- 停用自動偵測變更。
- 在儲存變更時停用驗證。
- [錯誤和解決辦法](#errors)

在這些主題中，您將會使用已建立的頁面。 若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數目：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

若要使用無追蹤查詢，您可以將新的驗證邏輯新增至 [部門編輯] 頁面：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>執行原始 SQL 查詢

Entity Framework Code First API 包含可讓您將 SQL 命令直接傳遞至資料庫的方法。 您有下列選項：

- 針對傳回實體類型的查詢使用 `DbSet.SqlQuery` 方法。 傳回的物件必須是物件所預期的型別 `DbSet` ，而且除非您關閉追蹤功能，否則資料庫內容會自動追蹤這些物件。  (請參閱下一節中的 `AsNoTracking` 方法。 ) 
- 針對傳回非 `Database.SqlQuery` 實體之類型的查詢，請使用方法。 即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。
- 針對非查詢命令使用 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 。

使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。 它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。 但是當您需要執行手動建立的特定 SQL 查詢時，有一些例外狀況，而這些方法可以讓您處理這類例外狀況。

如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。 執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。 在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。

### <a name="calling-a-query-that-returns-entities"></a>呼叫傳回實體的查詢

假設您希望 `GenericRepository` 類別提供額外的篩選和排序彈性，而不需要使用其他方法建立衍生類別。 達成此目標的其中一種方法是新增可接受 SQL 查詢的方法。 然後，您可以在控制器中指定想要的任何一種篩選或排序，例如 `Where` 相依于聯結或子查詢的子句。 在本節中，您將瞭解如何執行這類方法。

藉 `GetWithRawSql` 由將下列程式碼新增至 *GenericRepository.cs*來建立方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

在 *CourseController.cs*中，從方法呼叫新的方法 `Details` ，如下列範例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

在此情況下，您可以使用 `GetByID` 方法，但您會使用 `GetWithRawSql` 方法來驗證 `GetWithRawSQL` 方法是否正常運作。

執行 [詳細資料] 頁面，確認選取查詢可正常運作 (選取 [ **課程** ] 索引標籤，然後選取一個課程) 的 **詳細資料** 。

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>呼叫傳回其他類型之物件的查詢

先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。 在 *HomeController.cs* 中執行此動作的程式碼會使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

假設您想要撰寫程式碼，以直接在 SQL 中取出此資料，而不是使用 LINQ。 若要這樣做，您必須執行查詢來傳回實體物件以外的內容，這表示您需要使用 `Database.SqlQuery` 方法。

在 *HomeController.cs*中，將方法中的 LINQ 語句取代為 `About` 下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

執行 [關於] 頁面。 它會顯示與之前相同的資料。

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>呼叫更新查詢

假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數目。 如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。 在這一節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的點數，而您將藉由執行 SQL 語句來進行變更 `UPDATE` 。 網頁看起來將如下圖所示：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

在上一個教學課程中，您已使用一般儲存機制來讀取和更新 `Course` 控制器中的實體 `Course` 。 針對此大量更新作業，您需要建立不在一般存放庫中的新存放庫方法。 若要這樣做，您將建立 `CourseRepository` 衍生自類別的專用類別 `GenericRepository` 。

在 *DAL* 資料夾中，建立 *CourseRepository.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

在 *UnitOfWork.cs*中，將存放 `Course` 庫類型從變更 `GenericRepository<Course>` 為 `CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

在 *CourseController.cs*中，新增 `UpdateCourseCredits` 方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

和都將使用這個方法 `HttpGet` `HttpPost` 。 當 `HttpGet` `UpdateCourseCredits` 方法執行時， `multiplier` 變數會是 null，而視圖會顯示空白的文字方塊和提交按鈕，如上圖所示。

當您按一下 [ **更新** ] 按鈕並 `HttpPost` 執行此方法時， `multiplier` 將會在文字方塊中輸入值。 然後，程式碼會呼叫 `UpdateCourseCredits` 存放庫方法，它會傳回受影響的資料列數目，而該值會儲存在 `ViewBag` 物件中。 當 view 收到物件中受影響的資料列數目時 `ViewBag` ，它會顯示該數位，而不是文字方塊和提交按鈕，如下圖所示：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

在 [更新課程點數] 頁面的 [ *Views\Course* ] 資料夾中建立一個 view：

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

在 *Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

藉由選取 [課程] **** 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。 在文字方塊中輸入數目：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

按一下 [更新] 。 您會看到受影響的資料列數目：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

按一下 [回到清單]****，以查看課程與已修訂學分數的清單。

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

如需有關原始 SQL 查詢的詳細資訊，請參閱 Entity Framework team blog 上的 [原始 Sql 查詢](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) 。

## <a name="no-tracking-queries"></a>不追蹤的查詢

當資料庫內容抓取資料庫資料列並建立代表它們的實體物件時，根據預設，它會追蹤記憶體中的實體是否與資料庫中的實體同步。 記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。 這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。

您可以使用方法，指定內容是否追蹤查詢的實體物件 `AsNoTracking` 。 您會想要進行這項操作的常見案例包括下列情況：

- 此查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。
- 您想要附加實體以進行更新，但先前已針對不同用途抓取相同的實體。 由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。 防止這種情況發生的其中一種方法，就是使用 `AsNoTracking` 選項搭配先前的查詢。

在本節中，您將會執行商務邏輯，以說明這些案例的第二個。 具體來說，您將強制執行一個商務規則，指出講師不能是一個以上部門的系統管理員。

在 *DepartmentController.cs*中，新增可從和方法呼叫的新方法 `Edit` ， `Create` 以確定沒有兩個部門具有相同的系統管理員：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

如果沒有任何驗證錯誤，請在方法的區塊中新增程式碼 `try` `HttpPost` `Edit` ，以呼叫這個新的方法。 `try`區塊現在看起來如下列範例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

執行 [部門編輯] 頁面，然後嘗試將部門的系統管理員變更為另一個部門的系統管理員。 您會收到預期的錯誤訊息：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

現在，再次執行部門編輯頁面，這次變更 **預算** 金額。 當您按一下 [ **儲存**] 時，會看到錯誤頁面：

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

例外狀況錯誤訊息是「」 `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` 因為下列事件順序而發生：

- `Edit`方法 `ValidateOneAdministratorAssignmentPerInstructor` 會呼叫方法，此方法會抓取以 Kim Abercrombie 為其系統管理員的所有部門。 這會導致讀取英文部門。 因為這是正在編輯的部門，所以不會回報任何錯誤。 不過，這項讀取作業的結果是，資料庫內容現在正在追蹤從資料庫讀取的英文部門實體。
- `Edit`方法會嘗試在 `Modified` MVC 模型系結器所建立的英文部門實體上設定旗標，但因為內容已經在追蹤英文部門的實體，所以會失敗。

這個問題的解決方法之一，是讓內容不能追蹤驗證查詢所抓取的記憶體中部門實體。 這樣做並沒有任何缺點，因為您不會更新此實體，也不會以它在記憶體中快取的方式來讀取它。

在 *DepartmentController.cs*中，于 `ValidateOneAdministratorAssignmentPerInstructor` 方法中指定 [無追蹤]，如下列所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

請重複嘗試編輯部門的 **預算** 金額。 這次作業成功時，網站會如預期般傳回至 [部門索引] 頁面，以顯示修改過的預算值。

## <a name="examining-queries-sent-to-the-database"></a>檢查傳送至資料庫的查詢

有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。 若要這樣做，您可以在偵錯工具中檢查查詢變數，或呼叫查詢的 `ToString` 方法。 若要試試看，您將會看到一個簡單的查詢，然後查看當您新增諸如立即載入、篩選和排序等選項時，會發生什麼事。

在 *控制器/CourseController*中，以 `Index` 下列程式碼取代方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

現在在的 *GenericRepository.cs* 中設定中斷點 `return query.ToList();` ，並在方法的語句上設定中斷點 `return orderBy(query).ToList();` `Get` 。 在「偵測模式」中執行專案，然後選取 [課程索引] 頁面。 當程式碼到達中斷點時，檢查 `query` 變數。 您會看到傳送給 SQL Server 的查詢。 這是簡單的 `Select` 語句：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.sql)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

查詢可能太長，無法在 Visual Studio 的調試時間視窗中顯示。 若要查看整個查詢，您可以複製變數值，並將它貼到文字編輯器中：

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

現在您要將下拉式清單新增至課程索引頁面，讓使用者可以篩選特定部門。 您將依標題排序課程，並指定導覽屬性的積極式載入 `Department` 。 在 *CourseController.cs*中，以 `Index` 下列程式碼取代方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

方法會在參數中接收選取的下拉式清單值 `SelectedDepartment` 。 如果未選取任何專案，此參數將會是 null。

`SelectList`包含所有部門的集合會傳遞至下拉式清單的 [view]。 傳遞給此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。

針對存放 `Get` 庫的方法 `Course` ，程式碼會指定篩選運算式、排序次序，以及導覽屬性的積極式載入 `Department` 。 如果下拉式清單中沒有選取任何專案，則篩選運算式一律會傳回 `true` (也就是 `SelectedDepartment` null) 。

在 *Views\Course\Index.cshtml*中，緊接在開頭 `table` 標記之前，加入下列程式碼以建立下拉式清單和 [提交] 按鈕：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

在類別中仍設定中斷點的情況 `GenericRepository` 下，執行課程索引頁面。 繼續進行程式碼叫用中斷點的前兩次，以便在瀏覽器中顯示頁面。 從下拉式清單中選取部門，然後按一下 [ **篩選**]：

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

這次第一個中斷點將是針對下拉式清單中的部門查詢。 略過該變數，並 `query` 在程式碼下一次到達中斷點時查看變數，以查看 `Course` 查詢現在的樣子。 您會看到如下所示的內容：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.sql)]

您可以看到查詢現在是一項查詢，它會 `JOIN` 載入 `Department` 資料以及 `Course` 資料，並且包含 `WHERE` 子句。

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>使用 Proxy 類別

當 Entity Framework 建立實體實例時 (例如，當您執行) 的查詢時，通常會將其建立為動態產生的衍生型別實例，作為實體的 proxy。 此 proxy 會覆寫實體的一些虛擬屬性，以便在存取屬性時自動插入用來執行動作的勾點。 例如，這項機制可用來支援關聯性的延遲載入。

大部分的情況下，您不需要察覺 proxy 的使用，但有一些例外狀況：

- 在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。 例如，序列化非 proxy 實例可能比序列化 proxy 實例更有效率。
- 當您使用運算子具現化實體類別時 `new` ，您不會取得 proxy 實例。 這表示您不會取得延遲載入和自動變更追蹤等功能。 這通常是正常的;您通常不需要消極式載入，因為您要建立的新實體不在資料庫中，而且如果您將實體明確標示為，通常不需要變更追蹤 `Added` 。 但是，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的方法，以 proxy 建立新的實體實例 `Create` `DbSet` 。
- 您可能會想要從 proxy 類型取得實際的實體類型。 您可以使用 `GetObjectType` 類別的方法 `ObjectContext` 來取得 proxy 型別實例的實際實體型別。

如需詳細資訊， [請參閱 Entity Framework](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) team blog 上的使用 proxy。

## <a name="disabling-automatic-detection-of-changes"></a>停用自動偵測變更

Entity Framework 藉由比較實體的目前值與原始值，判斷實體如何變更 (以及因此需要將哪些更新傳送至資料庫)。 當查詢或附加實體時，會儲存原始的值。 會導致自動變更偵測的一些方法如下：

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

如果您要追蹤大量的實體，並且在迴圈中多次呼叫其中一種方法，您可以使用 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) 屬性暫時關閉自動變更偵測，以獲得大幅的效能改進。 如需詳細資訊，請參閱 [自動偵測變更](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。

## <a name="disabling-validation-when-saving-changes"></a>在儲存變更時停用驗證

當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更之實體的所有屬性中的資料。 如果您已更新大量的實體，而且已經驗證資料，則這項工作是不必要的，而且您可以暫時關閉驗證，讓儲存變更的程式花較少的時間。 您可以使用 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) 屬性來這麼做。 如需詳細資訊，請參閱 [驗證](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。

## <a name="summary"></a>摘要

這一系列的教學課程會在 ASP.NET MVC 應用程式中使用 Entity Framework 完成。 您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

如需如何在建立 web 應用程式之後進行部署的詳細資訊，請參閱 MSDN Library 中的 [ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx) 。

如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱 [Mvc 建議的資源](../../getting-started/recommended-resources-for-mvc.md)。

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>通知

- Tom Dykstra 撰寫了本教學課程的原始版本，也是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同撰寫本教學課程，並已針對 EF 5 和 MVC 4 更新大部分的工作。 Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com) 和 Entity Framework 團隊的其他成員協助進行程式碼審核，並協助您在更新 EF 5 的教學課程時，在發生遷移的許多問題時進行調試。

## <a name="vb"></a>VB

在最初產生教學課程時，我們提供了已完成下載專案的 c # 和 VB 版本。 在這項更新中，我們會為每個章節提供一個可供下載的 c # 專案，讓您更輕鬆地從系列中的任何地方開始著手，但由於時間限制和其他優先順序，我們並不會針對 VB 進行。 如果您使用這些教學課程來建立 VB 專案，而且願意與他人共用，請讓我們知道。

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>錯誤和解決方法

### <a name="cannot-createshadow-copy"></a>無法建立/陰影複製

錯誤訊息：

*當該檔案已經存在時，無法建立/陰影複製 ' DotNetOpenAuth。*

解決方案：

等候幾秒鐘，然後重新整理頁面。

### <a name="update-database-not-recognized"></a>更新-資料庫無法辨認

錯誤訊息：

「*更新資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可操作程式的名稱。請檢查名稱的拼寫是否正確，如果包含路徑的話，請確認路徑是否正確，然後再試一次。* 從 *`Update-Database`* PMC 中的命令 (。 ) 

解決方案：

結束 Visual Studio。 重新開啟專案，然後再試一次。

### <a name="validation-failed"></a>驗證失敗

錯誤訊息：

*一或多個實體的驗證失敗。如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。* 從 *`Update-Database`* PMC 中的命令 (。 ) 

解決方案：

發生此問題的其中一個原因是方法執行時發生驗證錯誤 `Seed` 。 請參閱 [植入和偵測 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 以取得對方法進行偵錯工具的秘訣 `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 錯誤

錯誤訊息：

*HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的頁面，因為頁面的相關設定資料無效。*

解決方案：

您可以取得此錯誤的其中一種方式，就是使用多個解決方案複本，每個複本都使用相同的埠號碼。 您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。 如果無法運作，請嘗試變更埠號碼。 以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。 選取 [ **Web** ] 索引標籤，然後變更 [ **專案 Url** ] 文字方塊中的埠號碼。

### <a name="error-locating-sql-server-instance"></a>搜尋 SQL Server 執行個體時發生錯誤

錯誤訊息：

*建立與 SQL Server 的連接時發生網路相關或實例特定的錯誤。找不到或無法存取伺服器。請驗證實例名稱是否正確，並將 SQL Server 設定為允許遠端連線。 (提供者： SQL 網路介面，錯誤： 26-尋找指定的伺服器/實例時發生錯誤) *

解決方案：

請檢查連接字串。 如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。

> [!div class="step-by-step"]
> [上一個](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
> [下一步](building-the-ef5-mvc4-chapter-downloads.md)
