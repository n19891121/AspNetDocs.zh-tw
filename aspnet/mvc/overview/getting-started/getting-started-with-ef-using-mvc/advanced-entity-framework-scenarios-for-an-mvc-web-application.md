---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例
description: 本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 之 ASP.NET web 應用程式的基本概念時，會很有説明。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "86188672"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例

在上一個教學課程中，您已實作為每個階層的資料表繼承。 本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 之 ASP.NET web 應用程式的基本概念時，會很有説明。 前幾節提供逐步指示，引導您逐步執行程式碼，並使用 Visual Studio 來完成工作。接下來的章節會引進數個主題，其中包含簡短的簡介，以及資源的連結以取得詳細資訊。

在這些主題中，您將會使用您已建立的頁面。 若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

在本教學課程中，您：

> [!div class="checklist"]
> * 執行原始 SQL 查詢
> * 執行沒有追蹤的查詢
> * 檢查傳送至資料庫的 SQL 查詢

您也會瞭解：

> [!div class="checklist"]
> * 建立抽象層
> * Proxy 類別
> * 自動變更偵測
> * 自動驗證
> * Entity Framework 電源工具
> * Entity Framework 原始碼

## <a name="prerequisite"></a>必要條件

* [實作繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>執行原始 SQL 查詢

Entity Framework Code First API 包括可讓您直接將 SQL 命令傳遞至資料庫的方法。 您有下列選項：

- 針對傳回實體類型的查詢，請使用[DbSet. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)方法。 傳回的物件必須是物件所預期的類型 `DbSet` ，而且資料庫內容會自動追蹤它們，除非您關閉追蹤。  (請參閱下一節中有關[AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)方法的資訊。 ) 
- 針對傳回不是實體之類型的查詢，請使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)方法。 即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。
- 針對非查詢命令使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 。

使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。 它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。 但在某些情況下，您需要執行手動建立的特定 SQL 查詢，而且這些方法可以讓您處理這類例外狀況。

如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。 執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。 在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。

### <a name="calling-a-query-that-returns-entities"></a>呼叫傳回實體的查詢

[DbSet &lt; &gt; TEntity](https://msdn.microsoft.com/library/gg696460.aspx)類別所提供的方法，可讓您用來執行傳回類型實體的查詢 `TEntity` 。 若要查看其運作方式，您將變更控制器的方法中的程式碼 `Details` `Department` 。

在*DepartmentController.cs*的方法中，以 `Details` `db.Departments.FindAsync` 方法呼叫取代方法呼叫 `db.Departments.SqlQuery` ，如下列反白顯示的程式碼所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

若要確認新的程式碼運作正常，請選取 [部門] **** 索引標籤，然後針對其中一個部門選取 [詳細資料] ****。 請確定所有資料都如預期般顯示。

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>呼叫傳回其他類型之物件的查詢

先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。 在*HomeController.cs*中執行此動作的程式碼會使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

假設您想要撰寫程式碼，直接在 SQL 中抓取這項資料，而不是使用 LINQ。 若要這麼做，您必須執行查詢來傳回實體物件以外的專案，這表示您需要使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)方法。

在*HomeController.cs*中，以 SQL 語句取代方法中的 LINQ 語句 `About` ，如下列反白顯示的程式碼所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

執行 [關於] 頁面。 確認它所顯示的資料與之前相同。

### <a name="calling-an-update-query"></a>呼叫更新查詢

假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數。 如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。 在本節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的信用額度數目，而您會藉由執行 SQL 語句來進行變更 `UPDATE` 。 

在*CourseController.cs*中，新增 `UpdateCourseCredits` 和的方法 `HttpGet` `HttpPost` ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

當控制器處理要求時 `HttpGet` ，變數中不會傳回任何內容 `ViewBag.RowsAffected` ，而且此視圖會顯示空白的文字方塊和 [提交] 按鈕。

按一下 [**更新**] 按鈕時， `HttpPost` 會呼叫方法，並 `multiplier` 在文字方塊中輸入值。 然後，程式碼會執行更新課程的 SQL，並將受影響的資料列數目傳回給變數中的 view `ViewBag.RowsAffected` 。 當 view 取得該變數中的值時，它會顯示已更新的資料列數目，而不是文字方塊和提交按鈕。

在 [ *CourseController.cs*] 中，以滑鼠右鍵按一下其中一個 `UpdateCourseCredits` 方法，然後按一下 [**加入視圖**]。 [**加入視圖**] 對話方塊隨即出現。 保留預設值，然後選取 [**新增**]。

在*Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

藉由選取 [課程] **** 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。 在文字方塊中輸入數目：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

按一下 [更新]  。 您會看到受影響的資料列數目。

按一下 [回到清單]****，以查看課程與已修訂學分數的清單。

如需原始 SQL 查詢的詳細資訊，請參閱 MSDN 上的[原始 Sql 查詢](https://msdn.microsoft.com/data/jj592907)。

## <a name="no-tracking-queries"></a>無追蹤查詢

當資料庫內容擷取資料表資料列並建立代表他們的實體物件時，根據預設，它會追蹤在記憶體中的實體是否與資料庫中的內容保持同步。 記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。 這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。

您可以使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法，在記憶體中停用實體物件的追蹤。 您會想要進行這項操作的常見案例包括下列情況：

- 查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。
- 您想要附加實體以進行更新，但您先前已針對不同目的抓取相同的實體。 由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。 處理這種情況的其中一種方式是使用 `AsNoTracking` 選項搭配先前的查詢。

如需示範如何使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法的範例，請參閱[本教學課程的先前版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 這個版本的教學課程不會在 Edit 方法中的模型系結器建立的實體上設定修改過的旗標，因此不需要 `AsNoTracking` 。

## <a name="examine-sql-sent-to-database"></a>檢查傳送至資料庫的 SQL

有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。 在先前的教學課程中，您已瞭解如何在攔截器程式碼中執行此動作;現在您會看到一些方法，而不需要撰寫攔截器程式碼。 若要試試看，您將會看到一個簡單的查詢，然後查看當您加入積極式載入、篩選和排序等選項時，會發生什麼事。

在 [*控制器/CourseController*] 中，以 `Index` 下列程式碼取代方法，以暫時停止積極式載入：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

現在在語句上設定中斷點， `return` (F9，並將游標放在該行) 上。 按**F5**以在 [調試] 模式中執行專案，然後選取 [課程索引] 頁面。 當程式碼到達中斷點時，請檢查 `sql` 變數。 您會看到傳送至 SQL Server 的查詢。 這是一個簡單的 `Select` 語句。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

按一下放大鏡以在**文字視覺化**中查看查詢。

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

現在您會將下拉式清單新增至 [課程] 索引頁面，讓使用者可以篩選特定部門。 您將依標題排序課程，並針對導覽屬性指定積極式載入 `Department` 。

在*CourseController.cs*中，將 `Index` 方法取代為下列程式碼：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

還原語句上的中斷點 `return` 。

方法會在參數中接收所選下拉式清單的值 `SelectedDepartment` 。 如果未選取任何內容，此參數將會是 null。

`SelectList`包含所有部門的集合會傳遞至下拉式清單的視圖。 傳遞至此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。

針對存放 `Get` 庫的方法 `Course` ，程式碼會針對導覽屬性指定篩選條件運算式、排序次序和積極式載入 `Department` 。 `true`如果下拉式清單中未選取任何內容，則篩選運算式一律會傳回 (也就是 `SelectedDepartment` null) 。

在*Views\Course\Index.cshtml*中，于開頭標記的正後方 `table` 新增下列程式碼，以建立下拉式清單和提交按鈕：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

在仍然設定中斷點的情況下，執行 [課程索引] 頁面。 繼續執行程式碼第一次叫用中斷點時，讓頁面顯示在瀏覽器中。 從下拉式清單中選取部門，然後按一下 [**篩選**]。

這次，第一個中斷點將會是 [部門] 查詢的下拉式清單。 在 `query` 下一次程式碼到達中斷點時略過，並查看變數，以查看查詢的 `Course` 樣子。 您會看到如下所示的內容：

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

您可以看到查詢現在是一種會 `JOIN` 載入資料以及 `Department` `Course` 資料的查詢，而且它包含 `WHERE` 子句。

移除這 `var sql = courses.ToString()` 一行。

## <a name="create-an-abstraction-layer"></a>建立抽象層

許多開發人員撰寫程式碼以實作存放庫和工作單元模式，作為使用 Entity Framework 之程式碼周圍的包裝函式。 這些模式主要用來建立資料存取層和應用程式的商務邏輯層之間的抽象層。 實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。 不過，撰寫額外的程式碼來執行這些模式並不一定是使用 EF 之應用程式的最佳選擇，原因如下：

- EF 內容類別本身會隔離您的程式碼與資料存放區特有的程式碼。
- EF 內容類別可作為您使用 EF 進行之資料庫更新的工作單元類別。
- Entity Framework 6 中引進的功能，可讓您更輕鬆地執行 TDD，而不需要撰寫存放庫程式碼。

如需如何執行儲存機制和工作單位模式的詳細資訊，請參閱[本教學課程系列的 Entity Framework 5 版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。 如需在 Entity Framework 6 中執行 TDD 之方式的詳細資訊，請參閱下列資源：

- [EF6 如何更輕鬆地啟用模擬 DbSets](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [使用模擬架構進行測試](https://msdn.microsoft.com/data/dn314429)
- [使用您自己的測試進行測試雙精度浮點數](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>Proxy 類別

當 Entity Framework 建立實體實例時 (例如，當您執行查詢) 時，通常會將其建立為動態產生之衍生型別的實例，作為實體的 proxy。 例如，請參閱下列兩個偵錯工具映射。 在第一個影像中，您會在具 `student` 現 `Student` 化實體後立即看到變數是預期的類型。 在第二個影像中，使用 EF 從資料庫讀取 student 實體之後，您會看到 proxy 類別。

![在 proxy 類別之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![Proxy 類別之後](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

此 proxy 類別會覆寫實體的某些虛擬屬性，以插入在存取屬性時自動執行動作的勾點。 此機制用於的一個函式是消極式載入。

在大部分的情況下，您不需要知道此 proxy 的使用方式，但有一些例外狀況：

- 在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。 例如，當您將實體序列化時，您通常會想要有 POCO 類別，而不是 proxy 類別。 避免序列化問題的其中一種方式，就是將資料傳輸物件序列化 (Dto) 而不是實體物件，如搭配[使用 WEB API 與 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)教學課程中所示。 另一種方式是[停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)。
- 當您使用運算子來具現化實體類別時 `new` ，您不會取得 proxy 實例。 這表示您不會取得延遲載入和自動變更追蹤之類的功能。 這通常沒什麼問題;您通常不需要消極式載入，因為您正在建立不在資料庫中的新實體，而且如果您將實體明確標示為，則通常不需要變更追蹤 `Added` 。 不過，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的[create](https://msdn.microsoft.com/library/gg679504.aspx)方法來建立具有 proxy 的新實體實例 `DbSet` 。
- 您可能想要從 proxy 類型取得實際的實體類型。 您可以使用類別的[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)方法 `ObjectContext` 來取得 proxy 類型實例的實際實體類型。

如需詳細資訊，請參閱 MSDN 上[的](https://msdn.microsoft.com/data/JJ592886.aspx)使用 proxy。

## <a name="automatic-change-detection"></a>自動變更偵測

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

如果您要追蹤大量實體，並在迴圈中多次呼叫其中一種方法，您可以使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)屬性暫時關閉自動變更偵測，以獲得顯著的效能改進。 如需詳細資訊，請參閱 MSDN 上的[自動偵測變更](https://msdn.microsoft.com/data/jj556205)。

## <a name="automatic-validation"></a>自動驗證

當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更實體的所有屬性中的資料。 如果您已更新大量實體，而且您已經驗證過資料，這是不必要的工作，而且您可以暫時關閉驗證，讓儲存變更的程式更少時間。 您可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)屬性來執行此動作。 如需詳細資訊，請參閱 MSDN 上的[驗證](https://msdn.microsoft.com/data/gg193959)。

## <a name="entity-framework-power-tools"></a>Entity Framework 電源工具

[Entity Framework Power](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) tool 是用來建立這些教學課程中所顯示之資料模型圖表的 Visual Studio 增益集。 這些工具也可以執行其他功能，例如根據現有資料庫中的資料表產生實體類別，讓您可以將資料庫與 Code First 搭配使用。 安裝工具之後，內容功能表中會出現一些額外的選項。 例如，當您以滑鼠右鍵按一下**方案總管**中的內容類別時，就會看到並**Entity Framework**選項。 這讓您能夠產生圖表。 當您使用 Code First 無法變更圖表中的資料模型，但您可以四處移動，讓它更容易瞭解。

![EF 圖表](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Entity Framework 原始碼

Entity Framework 6 的原始程式碼可從[GitHub](https://github.com/aspnet/EntityFramework6)取得。 您可以提出 bug，而您可以為 EF 原始程式碼貢獻自己的增強功能。

雖然原始程式碼已開放，但 Entity Framework 完全支援做為 Microsoft 產品。 Microsoft Entity Framework 小組將控制接受哪些貢獻，並測試所有的程式碼變更以確保每次發行的品質。

## <a name="acknowledgments"></a>通知

- Tom 作者: dykstra 寫了本教學課程的原始版本，共同撰寫了 EF 5 更新，並撰寫了 EF 6 更新。 Tom 是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 大部分的工作都是更新 EF 5 和 MVC 4 的教學課程，並共同撰寫 ef 6 更新。 Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com)和 Entity Framework 小組的其他成員可協助進行程式碼審核，並説明您在更新 ef 5 和 ef 6 教學課程時所出現的許多遷移問題。

## <a name="troubleshoot-common-errors"></a>常見問題疑難排解

### <a name="cannot-createshadow-copy"></a>無法建立/陰影複製

錯誤訊息：

> &lt;當檔案已存在時，無法建立/陰影複製 ' filename &gt; '。

解決方案

等候幾秒鐘，然後重新整理頁面。

### <a name="update-database-not-recognized"></a>更新-無法辨識資料庫

從 PMC) 中的命令 (的錯誤訊息 `Update-Database` ：

> 「更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。 請檢查名稱拼字，如果名稱含有路徑，請確認路徑正確，然後再試一次。

解決方案

結束 Visual Studio。 重新開啟專案，然後再試一次。

### <a name="validation-failed"></a>驗證失敗

從 PMC) 中的命令 (的錯誤訊息 `Update-Database` ：

> 一或多個實體的驗證失敗。 如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。

解決方案

此問題的其中一個原因是方法執行時的驗證錯誤 `Seed` 。 如需有關偵測方法的秘訣，請參閱[植入和偵錯工具 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 錯誤

錯誤訊息：

> HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的網頁，因為該頁面的相關設定資料無效。

解決方案

您可以取得此錯誤的其中一種方式是，使用相同的埠號碼，讓解決方案有多個複本。 您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。 如果無法解決問題，請嘗試變更埠號碼。 以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。 選取 [ **Web** ] 索引標籤，然後在 [**專案 Url** ] 文字方塊中變更埠號碼。

### <a name="error-locating-sql-server-instance"></a>搜尋 SQL Server 執行個體時發生錯誤

錯誤訊息：

> 和 SQL Server 建立連線時，發生與網路相關或執行個體特定的錯誤。 找不到或無法存取伺服器。 檢查執行個體名稱是否正確以及 SQL Server 執行個體是否設定為允許遠端連接。 (提供者：SQL 網路介面，錯誤：26 - 搜尋指定的伺服器/執行個體時發生錯誤)

解決方案

檢查連接字串。 如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

 如需如何使用 Entity Framework 來處理資料的詳細資訊，請參閱[MSDN 上的 EF 檔頁面](https://msdn.microsoft.com/data/ee712907)和[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)。

如需有關如何在建立 web 應用程式之後部署它的詳細資訊，請參閱 MSDN Library 中的[ASP.NET Web 部署-建議的資源](../../../../whitepapers/aspnet-web-deployment-content-map.md)。

如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱[ASP.NET Mvc 建議的資源](../recommended-resources-for-mvc.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您：

> [!div class="checklist"]
> * 執行原始 SQL 查詢
> * 未執行任何追蹤查詢
> * 已檢查傳送至資料庫的 SQL 查詢

您也瞭解到：

> [!div class="checklist"]
> * 建立抽象層
> * Proxy 類別
> * 自動變更偵測
> * 自動驗證
> * Entity Framework 電源工具
> * Entity Framework 原始碼

這會完成這一系列的教學課程，以在 ASP.NET MVC 應用程式中使用 Entity Framework。 如果您想要瞭解 EF Database First，請參閱資料庫第一個教學課程系列。
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)