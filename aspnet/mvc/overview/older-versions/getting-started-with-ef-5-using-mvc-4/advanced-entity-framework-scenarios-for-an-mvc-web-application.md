---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC Web 應用程式的 Advanced Entity Framework 案例， (10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163437"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>MVC Web 應用程式的 Advanced Entity Framework 案例， (10) 

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。 您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。 如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已執行了儲存機制和工作單位模式。 本教學課程涵蓋下列主題：

- 執行原始 SQL 查詢。
- 執行沒有追蹤的查詢。
- 檢查傳送至資料庫的查詢。
- 使用 proxy 類別。
- 停用變更的自動偵測。
- 儲存變更時停用驗證。
- [錯誤和解決辦法](#errors)

在這些主題中，您將會使用您已建立的頁面。 若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

若要使用沒有追蹤的查詢，您必須將新的驗證邏輯新增至部門的 [編輯] 頁面：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>執行原始 SQL 查詢

Entity Framework Code First API 包括可讓您直接將 SQL 命令傳遞至資料庫的方法。 您有下列選項：

- 針對傳回實體類型的查詢使用 `DbSet.SqlQuery` 方法。 傳回的物件必須是物件所預期的類型 `DbSet` ，而且資料庫內容會自動追蹤它們，除非您關閉追蹤。  (請參閱下列有關方法的章節 `AsNoTracking` 。 ) 
- 針對傳回 `Database.SqlQuery` 不是實體之類型的查詢，請使用方法。 即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。
- 針對非查詢命令使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 。

使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。 它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。 但在某些情況下，您需要執行手動建立的特定 SQL 查詢，而且這些方法可以讓您處理這類例外狀況。

如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。 執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。 在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。

### <a name="calling-a-query-that-returns-entities"></a>呼叫傳回實體的查詢

假設您想要讓 `GenericRepository` 類別提供額外的篩選和排序彈性，而不需要您使用其他方法建立衍生類別。 達成此目標的其中一種方法是新增可接受 SQL 查詢的方法。 接著，您可以在控制器中指定您想要的任何一種篩選或排序，例如 `Where` 相依于聯結或子查詢的子句。 在本節中，您將瞭解如何執行這種方法。

`GetWithRawSql`將下列程式碼新增至*GenericRepository.cs*，以建立方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

在*CourseController.cs*中，從方法呼叫新的方法 `Details` ，如下列範例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

在此情況下，您可以使用 `GetByID` 方法，但是您會使用 `GetWithRawSql` 方法來驗證 `GetWithRawSQL` 方法是否正常運作。

執行 [詳細資料] 頁面，確認 select 查詢是否正常運作 (選取 [**課程**] 索引標籤，然後) 的 [**詳細資料**]。

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>呼叫傳回其他類型之物件的查詢

先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。 在*HomeController.cs*中執行此動作的程式碼會使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

假設您想要撰寫程式碼，直接在 SQL 中抓取這項資料，而不是使用 LINQ。 若要這麼做，您必須執行查詢來傳回實體物件以外的專案，這表示您需要使用 `Database.SqlQuery` 方法。

在*HomeController.cs*中，將方法中的 LINQ 語句取代 `About` 為下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

執行 [關於] 頁面。 它會顯示與之前相同的資料。

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>呼叫更新查詢

假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數。 如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。 在本節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的信用額度數目，而您會藉由執行 SQL 語句來進行變更 `UPDATE` 。 網頁看起來將如下圖所示：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

在上一個教學課程中，您使用了一般存放庫來讀取和更新 `Course` 控制器中的實體 `Course` 。 針對此大量更新作業，您需要建立不在一般存放庫中的新存放庫方法。 若要這麼做，您將建立 `CourseRepository` 衍生自類別的專用類別 `GenericRepository` 。

在*DAL*資料夾中，建立*CourseRepository.cs* ，並將現有的程式碼取代為下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

在*UnitOfWork.cs*中，將存放 `Course` 庫類型從變更 `GenericRepository<Course>` 為`CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

在*CourseController.cs*中，新增 `UpdateCourseCredits` 方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

這個方法將同時用於 `HttpGet` 和 `HttpPost` 。 當 `HttpGet` `UpdateCourseCredits` 方法執行時， `multiplier` 變數會是 null，而且此視圖會顯示空白的文字方塊和 [提交] 按鈕，如上圖所示。

按一下 [**更新**] 按鈕並 `HttpPost` 執行方法時， `multiplier` 將會在文字方塊中輸入值。 然後，程式碼會呼叫儲存機制 `UpdateCourseCredits` 方法，這會傳回受影響的資料列數目，而該值會儲存在 `ViewBag` 物件中。 當此視圖收到物件中受影響的資料列數目時 `ViewBag` ，它會顯示該數位，而不是文字方塊和提交按鈕，如下圖所示：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

在 [更新課程信用額度] 頁面的 [ *Views\Course* ] 資料夾中建立一個視圖：

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

在*Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

藉由選取 [課程] **** 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。 在文字方塊中輸入數目：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

按一下 [更新]  。 您會看到受影響的資料列數目：

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

按一下 [回到清單]****，以查看課程與已修訂學分數的清單。

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

如需原始 SQL 查詢的詳細資訊，請參閱 Entity Framework 小組 blog 上的[原始 Sql 查詢](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)。

## <a name="no-tracking-queries"></a>不追蹤的查詢

當資料庫內容抓取資料庫資料列並建立代表它們的實體物件時，根據預設，它會追蹤記憶體中的實體是否與資料庫中的專案同步。 記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。 這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。

您可以使用方法，指定內容是否追蹤查詢的實體物件 `AsNoTracking` 。 您會想要進行這項操作的常見案例包括下列情況：

- 此查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。
- 您想要附加實體以進行更新，但您先前已針對不同目的抓取相同的實體。 由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。 避免發生這種情況的其中一種方式，就是使用 `AsNoTracking` 選項搭配先前的查詢。

在本節中，您將會執行商務邏輯，以說明其中的第二個案例。 具體來說，您將會強制執行商務規則，指出講師不能是一個以上部門的系統管理員。

在*DepartmentController.cs*中，新增可從和方法呼叫的新方法 `Edit` ， `Create` 以確定沒有任何兩個部門具有相同的系統管理員：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

如果沒有驗證錯誤，請在方法的區塊中加入程式碼 `try` `HttpPost` `Edit` ，以呼叫這個新的方法。 此 `try` 區塊現在看起來如下列範例所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

執行部門 [編輯] 頁面，然後嘗試將部門的系統管理員變更為已經是不同部門之系統管理員的講師。 您會收到預期的錯誤訊息：

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

現在，再次執行 [部門編輯] 頁面，這次變更**預算**金額。 當您按一下 [**儲存**] 時，您會看到錯誤頁面：

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

例外狀況錯誤訊息為「」， `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` 這是因為下列事件順序所導致：

- `Edit`方法 `ValidateOneAdministratorAssignmentPerInstructor` 會呼叫方法，它會抓取所有以 Kim Abercrombie 為其系統管理員的部門。 這會導致讀取英文部門。 因為這是正在編輯的部門，所以不會回報任何錯誤。 不過，此讀取作業的結果是，從資料庫讀取的英文部門實體現在正由資料庫內容追蹤。
- `Edit`方法 `Modified` 會嘗試在 MVC 模型系結器所建立的英文部門實體上設定旗標，但因為內容已經追蹤英文部門的實體，所以失敗。

這個問題的解決方法之一，是要讓內容免于追蹤驗證查詢所抓取的記憶體中部門實體。 這麼做並沒有任何缺點，因為您將不會更新此實體，或以可從記憶體快取中獲益的方式再次讀取它。

在*DepartmentController.cs*的方法中， `ValidateOneAdministratorAssignmentPerInstructor` 指定 [無追蹤]，如下所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

重複嘗試編輯部門的**預算**金額。 這次作業會成功，而且網站會如預期般返回 [部門索引] 頁面，其中顯示修訂的預算值。

## <a name="examining-queries-sent-to-the-database"></a>檢查傳送至資料庫的查詢

有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。 若要這樣做，您可以在偵錯工具中檢查查詢變數，或呼叫查詢的 `ToString` 方法。 若要試試看，您將會看到一個簡單的查詢，然後查看當您加入積極式載入、篩選和排序等選項時，會發生什麼事。

在*控制器/CourseController*中，將 `Index` 方法取代為下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

現在，在和方法的語句上設定*GenericRepository.cs*中的中斷點 `return query.ToList();` `return orderBy(query).ToList();` `Get` 。 在 [偵錯模式] 中執行專案，然後選取 [課程索引] 頁面。 當程式碼到達中斷點時，請檢查 `query` 變數。 您會看到傳送至 SQL Server 的查詢。 這是一個簡單的 `Select` 語句：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

查詢可能太長，無法在 Visual Studio 的調試視窗中顯示。 若要查看整個查詢，您可以複製變數值，並將它貼到文字編輯器中：

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

現在您會將下拉式清單新增至 [課程索引] 頁面，讓使用者可以篩選特定部門。 您將依標題排序課程，並針對導覽屬性指定積極式載入 `Department` 。 在*CourseController.cs*中，將 `Index` 方法取代為下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

方法會在參數中接收所選下拉式清單的值 `SelectedDepartment` 。 如果未選取任何內容，此參數將會是 null。

`SelectList`包含所有部門的集合會傳遞至下拉式清單的視圖。 傳遞至此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。

針對存放 `Get` 庫的方法 `Course` ，程式碼會針對導覽屬性指定篩選條件運算式、排序次序和積極式載入 `Department` 。 `true`如果下拉式清單中未選取任何內容，則篩選運算式一律會傳回 (也就是 `SelectedDepartment` null) 。

在*Views\Course\Index.cshtml*中，于開頭標記的正後方 `table` 新增下列程式碼，以建立下拉式清單和提交按鈕：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

在類別中仍設定中斷點後 `GenericRepository` ，請執行 [課程索引] 頁面。 繼續執行程式碼叫用中斷點的前兩次，以便在瀏覽器中顯示該頁面。 從下拉式清單中選取部門，然後按一下 [**篩選**]：

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

這次，第一個中斷點將會是 [部門] 查詢的下拉式清單。 在 `query` 下一次程式碼到達中斷點時略過，並查看變數，以查看查詢的 `Course` 樣子。 您會看到如下所示的內容：

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

您可以看到查詢現在是一種會 `JOIN` 載入資料以及 `Department` `Course` 資料的查詢，而且它包含 `WHERE` 子句。

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>使用 Proxy 類別

當 Entity Framework 建立實體實例時 (例如，當您執行查詢) 時，通常會將其建立為動態產生之衍生型別的實例，作為實體的 proxy。 此 proxy 會覆寫實體的某些虛擬屬性，以插入在存取屬性時自動執行動作的勾點。 例如，這項機制是用來支援延遲載入關聯性。

在大部分的情況下，您不需要知道此 proxy 的使用方式，但有一些例外狀況：

- 在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。 例如，序列化非 proxy 實例可能會比序列化 proxy 實例更有效率。
- 當您使用運算子來具現化實體類別時 `new` ，您不會取得 proxy 實例。 這表示您不會取得延遲載入和自動變更追蹤之類的功能。 這通常沒什麼問題;您通常不需要消極式載入，因為您正在建立不在資料庫中的新實體，而且如果您將實體明確標示為，則通常不需要變更追蹤 `Added` 。 不過，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的方法來建立具有 proxy 的新實體實例 `Create` `DbSet` 。
- 您可能想要從 proxy 類型取得實際的實體類型。 您可以使用 `GetObjectType` 類別的方法 `ObjectContext` 來取得 proxy 類型實例的實際實體類型。

如需詳細資訊，[請參閱在](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)Entity Framework 小組的 blog 上使用 proxy。

## <a name="disabling-automatic-detection-of-changes"></a>停用變更的自動偵測

Entity Framework 藉由比較實體的目前值與原始值，判斷實體如何變更 (以及因此需要將哪些更新傳送至資料庫)。 查詢或附加實體時，會儲存原始值。 會導致自動變更偵測的一些方法如下：

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

如果您要追蹤大量實體，並在迴圈中多次呼叫其中一種方法，您可以使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)屬性暫時關閉自動變更偵測，以獲得顯著的效能改進。 如需詳細資訊，請參閱[自動偵測變更](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。

## <a name="disabling-validation-when-saving-changes"></a>儲存變更時停用驗證

當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更實體的所有屬性中的資料。 如果您已更新大量實體，而且您已經驗證過資料，這是不必要的工作，而且您可以暫時關閉驗證，讓儲存變更的程式更少時間。 您可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)屬性來執行此動作。 如需詳細資訊，請參閱[驗證](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。

## <a name="summary"></a>摘要

這會完成這一系列的教學課程，以在 ASP.NET MVC 應用程式中使用 Entity Framework。 您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

如需有關如何在建立 web 應用程式之後進行部署的詳細資訊，請參閱 MSDN Library 中的[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx)。

如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱[Mvc 建議資源](../../getting-started/recommended-resources-for-mvc.md)。

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>通知

- Tom 作者: dykstra 已撰寫本教學課程的原始版本，而且是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同撰寫本教學課程，而且大部分的工作都是針對 EF 5 和 MVC 4 進行更新。 Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com)和 Entity Framework 小組的其他成員會協助程式碼審核，並協助您在更新 EF 5 的教學課程時所出現的許多遷移問題。

## <a name="vb"></a>VB

最初產生教學課程時，我們提供了 c # 和 VB 版本的已完成下載專案。 在此更新中，我們將為每個章節提供 c # 可下載的專案，讓您更輕鬆地開始使用系列中的任何位置，但由於時間限制和其他優先順序，我們並未針對 VB 進行這項作業。 如果您使用這些教學課程建立 VB 專案，而且願意與他人共用，請讓我們知道。

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>錯誤和因應措施

### <a name="cannot-createshadow-copy"></a>無法建立/陰影複製

錯誤訊息：

*當該檔案已存在時，無法建立/陰影複製 ' DotNetOpenAuth '。*

解決方案：

等候幾秒鐘，然後重新整理頁面。

### <a name="update-database-not-recognized"></a>更新-無法辨識資料庫

錯誤訊息：

「*更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。請檢查名稱的拼寫，或如果已包含路徑，請確認路徑正確，然後再試一次。* 從 *`Update-Database`* PMC 中的命令 (。 ) 

解決方案：

結束 Visual Studio。 重新開啟專案，然後再試一次。

### <a name="validation-failed"></a>驗證失敗

錯誤訊息：

*一或多個實體的驗證失敗。如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。* 從 *`Update-Database`* PMC 中的命令 (。 ) 

解決方案：

此問題的其中一個原因是方法執行時的驗證錯誤 `Seed` 。 如需有關偵測方法的秘訣，請參閱[植入和偵錯工具 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 錯誤

錯誤訊息：

*HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的網頁，因為該頁面的相關設定資料無效。*

解決方案：

您可以取得此錯誤的其中一種方式是，使用相同的埠號碼，讓解決方案有多個複本。 您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。 如果無法解決問題，請嘗試變更埠號碼。 以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。 選取 [ **Web** ] 索引標籤，然後在 [**專案 Url** ] 文字方塊中變更埠號碼。

### <a name="error-locating-sql-server-instance"></a>搜尋 SQL Server 執行個體時發生錯誤

錯誤訊息：

*建立與 SQL Server 的連接時發生網路相關或實例特定的錯誤。找不到或無法存取伺服器。請確認實例名稱是否正確，以及 SQL Server 是否設定為允許遠端連線。 (提供者： SQL 網路介面，錯誤： 26-尋找指定的伺服器/實例時發生錯誤) *

解決方案：

檢查連接字串。 如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。

> [!div class="step-by-step"]
> [上一個](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
> [下一步](building-the-ef5-mvc4-chapter-downloads.md)
