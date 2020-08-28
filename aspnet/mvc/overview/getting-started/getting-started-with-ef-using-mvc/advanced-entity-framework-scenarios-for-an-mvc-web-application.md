---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例
description: 本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 的 ASP.NET web 應用程式的基本概念時，這些主題將有所説明。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 2bfa4401c73b56be87502ffbb189abab3c59c226
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044996"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例

在上一個教學課程中，您已執行每個階層的資料表繼承。 本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 的 ASP.NET web 應用程式的基本概念時，這些主題將有所説明。 前幾節有逐步指示，引導您完成程式碼，並使用 Visual Studio 來完成工作。接下來的章節會介紹幾個主題，並提供一些簡短的簡介，後面接著資源連結以取得詳細資訊。

在這些主題中，您將會使用已建立的頁面。 若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數目：

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

在本教學課程中，您：

> [!div class="checklist"]
> * 執行原始 SQL 查詢
> * 執行無追蹤查詢
> * 檢查傳送至資料庫的 SQL 查詢

您也會瞭解：

> [!div class="checklist"]
> * 建立抽象層
> * Proxy 類別
> * 自動變更偵測
> * 自動驗證
> * Entity Framework Power Tools
> * Entity Framework 來源程式碼

## <a name="prerequisite"></a>必要條件

* [實作繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>執行原始 SQL 查詢

Entity Framework Code First API 包含可讓您將 SQL 命令直接傳遞至資料庫的方法。 您有下列選項：

- 針對傳回實體類型的查詢，請使用 [DbSet. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 方法。 傳回的物件必須是物件所預期的型別 `DbSet` ，而且除非您關閉追蹤功能，否則資料庫內容會自動追蹤這些物件。  (請參閱下一節 [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 方法。 ) 
- 針對傳回非實體之類型的查詢，請使用 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 方法。 即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。
- 針對非查詢命令使用 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 。

使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。 它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。 但是當您需要執行手動建立的特定 SQL 查詢時，有一些例外狀況，而這些方法可以讓您處理這類例外狀況。

如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。 執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。 在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。

### <a name="calling-a-query-that-returns-entities"></a>呼叫傳回實體的查詢

[DbSet &lt; &gt; TEntity](https://msdn.microsoft.com/library/gg696460.aspx)類別所提供的方法，可讓您用來執行查詢，以傳回類型的實體 `TEntity` 。 若要查看其運作方式，您將變更控制器方法中的程式碼 `Details` `Department` 。

在 *DepartmentController.cs*的方法中 `Details` ，以 `db.Departments.FindAsync` 方法呼叫取代方法呼叫 `db.Departments.SqlQuery` ，如下列反白顯示的程式碼所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

若要確認新的程式碼運作正常，請選取 [部門] **** 索引標籤，然後針對其中一個部門選取 [詳細資料] ****。 請確定所有的資料都如預期般顯示。

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>呼叫傳回其他類型之物件的查詢

先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。 在 *HomeController.cs* 中執行此動作的程式碼會使用 LINQ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

假設您想要撰寫程式碼，以直接在 SQL 中取出此資料，而不是使用 LINQ。 若要這樣做，您必須執行查詢來傳回實體物件以外的內容，這表示您需要使用 [SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 方法。

在 *HomeController.cs*中，以 SQL 語句取代方法中的 LINQ 語句 `About` ，如下列醒目提示的程式碼所示：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

執行 [關於] 頁面。 確認它顯示的資料與之前相同。

### <a name="calling-an-update-query"></a>呼叫更新查詢

假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數目。 如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。 在這一節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的點數，而您將執行 SQL 語句來進行變更 `UPDATE` 。 

在 *CourseController.cs*中， `UpdateCourseCredits` 為和新增方法 `HttpGet` `HttpPost` ：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

當控制器處理要求時 `HttpGet` ，不會在變數中傳回任何內容 `ViewBag.RowsAffected` ，而且此視圖會顯示空白的文字方塊和提交按鈕。

按一下 [ **更新** ] 按鈕時， `HttpPost` 會呼叫方法，並在 `multiplier` 文字方塊中輸入值。 然後，程式碼會執行更新課程的 SQL，並將受影響的資料列數目傳回給變數中的 view `ViewBag.RowsAffected` 。 當 view 取得該變數中的值時，會顯示已更新的資料列數目，而不是文字方塊和提交按鈕。

在 [ *CourseController.cs*] 中，以滑鼠右鍵按一下其中一種 `UpdateCourseCredits` 方法，然後按一下 [ **加入視圖**]。 [ **加入視圖** ] 對話方塊隨即出現。 保留預設值，然後選取 [ **新增**]。

在 *Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

藉由選取 [課程] **** 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。 在文字方塊中輸入數目：

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

按一下 [更新] 。 您會看到受影響的資料列數目。

按一下 [回到清單]****，以查看課程與已修訂學分數的清單。

如需有關原始 SQL 查詢的詳細資訊，請參閱 MSDN 上的 [原始 Sql 查詢](https://msdn.microsoft.com/data/jj592907) 。

## <a name="no-tracking-queries"></a>無追蹤查詢

當資料庫內容擷取資料表資料列並建立代表他們的實體物件時，根據預設，它會追蹤在記憶體中的實體是否與資料庫中的內容保持同步。 記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。 這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。

您可以使用 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 方法來停用記憶體中的實體物件追蹤。 您會想要進行這項操作的常見案例包括下列情況：

- 查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。
- 您想要附加實體以進行更新，但先前已針對不同用途抓取相同的實體。 由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。 處理這種情況的其中一種方式是使用 `AsNoTracking` 選項搭配先前的查詢。

如需示範如何使用 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 方法的範例，請參閱 [本教學課程的先前版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 此版本的教學課程不會在編輯方法中的模型系結器建立的實體上設定修改過的旗標，因此不需要 `AsNoTracking` 。

## <a name="examine-sql-sent-to-database"></a>檢查傳送至資料庫的 SQL

有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。 在先前的教學課程中，您已瞭解如何在攔截器程式碼中進行這項作業;現在您會看到一些方法，而不需要撰寫攔截器程式碼。 若要試試看，您將會看到一個簡單的查詢，然後查看當您新增諸如立即載入、篩選和排序等選項時，會發生什麼事。

在 *控制器/CourseController*中，以 `Index` 下列程式碼取代方法，以暫時停止積極式載入：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

現在在語句 (F9 上設定中斷點， `return` 並) 該行上的游標。 按下 **F5** 以在偵測模式中執行專案，然後選取 [課程索引] 頁面。 當程式碼到達中斷點時，檢查 `sql` 變數。 您會看到傳送給 SQL Server 的查詢。 這是簡單的 `Select` 語句。

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.sql)]

按一下放大鏡以查看 **文字視覺化**中的查詢。

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

現在您會將下拉式清單新增至課程索引頁面，讓使用者可以篩選特定部門。 您將依標題排序課程，並指定導覽屬性的積極式載入 `Department` 。

在 *CourseController.cs*中，以 `Index` 下列程式碼取代方法：

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

還原語句上的中斷點 `return` 。

方法會在參數中接收選取的下拉式清單值 `SelectedDepartment` 。 如果未選取任何專案，此參數將會是 null。

`SelectList`包含所有部門的集合會傳遞至下拉式清單的 [view]。 傳遞給此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。

針對存放 `Get` 庫的方法 `Course` ，程式碼會指定篩選運算式、排序次序，以及導覽屬性的積極式載入 `Department` 。 如果下拉式清單中沒有選取任何專案，則篩選運算式一律會傳回 `true` (也就是 `SelectedDepartment` null) 。

在 *Views\Course\Index.cshtml*中，緊接在開頭 `table` 標記之前，加入下列程式碼以建立下拉式清單和 [提交] 按鈕：

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

在仍然設定中斷點的情況下，執行 [課程索引] 頁面。 在程式碼第一次叫用中斷點時繼續進行，如此頁面就會顯示在瀏覽器中。 從下拉式清單中選取部門，然後按一下 [ **篩選**]。

這次第一個中斷點將是針對下拉式清單中的部門查詢。 略過該變數，並 `query` 在程式碼下一次到達中斷點時查看變數，以查看 `Course` 查詢現在的樣子。 您會看到如下所示的內容：

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

您可以看到查詢現在是一項查詢，它會 `JOIN` 載入 `Department` 資料以及 `Course` 資料，並且包含 `WHERE` 子句。

移除 `var sql = courses.ToString()` 該行。

## <a name="create-an-abstraction-layer"></a>建立抽象層

許多開發人員撰寫程式碼以實作存放庫和工作單元模式，作為使用 Entity Framework 之程式碼周圍的包裝函式。 這些模式主要用來建立資料存取層和應用程式的商務邏輯層之間的抽象層。 實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。 不過，撰寫額外的程式碼來執行這些模式，對於使用 EF 的應用程式來說，不一定是最佳選擇，原因如下：

- EF 內容類別本身會隔離您的程式碼與資料存放區特有的程式碼。
- EF 內容類別可作為您使用 EF 進行之資料庫更新的工作單元類別。
- Entity Framework 6 中引進的功能，可讓您更輕鬆地執行 TDD，而不需要撰寫存放庫程式碼。

如需如何執行存放庫和工作單元模式的詳細資訊，請參閱 [本教學課程系列的 Entity Framework 5 版](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。 如需在 Entity Framework 6 中實施 TDD 之方法的相關資訊，請參閱下列資源：

- [EF6 如何讓模擬 DbSets 更容易](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [使用模擬架構進行測試](https://msdn.microsoft.com/data/dn314429)
- [使用您自己的測試進行測試的雙精度浮點數](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>Proxy 類別

當 Entity Framework 建立實體實例時 (例如，當您執行) 的查詢時，通常會將其建立為動態產生的衍生型別實例，作為實體的 proxy。 例如，請參閱下列兩個偵錯工具映射。 在第一個影像中，您會在具 `student` 現化實體之後，看到變數是預期的 `Student` 類型。 在第二個影像中，使用 EF 從資料庫讀取 student 實體之後，您會看到 proxy 類別。

![Proxy 類別之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![Proxy 類別之後](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

此 proxy 類別會覆寫實體的一些虛擬屬性，以便在存取屬性時自動插入用來執行動作的勾點。 這項機制使用的一個函數是消極式載入。

大部分的情況下，您不需要察覺 proxy 的使用，但有一些例外狀況：

- 在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。 例如，當您序列化實體時，您通常會想要 POCO 類別，而不是 proxy 類別。 避免序列化問題的其中一種方式，是將資料傳輸物件序列化 (Dto) 而不是實體物件，如 [使用 WEB API 搭配 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 教學課程中所示。 另一種方式是 [停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)。
- 當您使用運算子具現化實體類別時 `new` ，您不會取得 proxy 實例。 這表示您不會取得延遲載入和自動變更追蹤等功能。 這通常是正常的;您通常不需要消極式載入，因為您要建立的新實體不在資料庫中，而且如果您將實體明確標示為，通常不需要變更追蹤 `Added` 。 但是，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的 [create](https://msdn.microsoft.com/library/gg679504.aspx) 方法，以 proxy 建立新的實體實例 `DbSet` 。
- 您可能會想要從 proxy 類型取得實際的實體類型。 您可以使用類別的 [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 方法 `ObjectContext` ，來取得 proxy 型別實例的實際實體型別。

如需詳細資訊，請參閱 MSDN 上 [的](https://msdn.microsoft.com/data/JJ592886.aspx) 使用 proxy。

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

如果您要追蹤大量的實體，並且在迴圈中多次呼叫其中一種方法，您可以使用 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 屬性暫時關閉自動變更偵測，以獲得大幅的效能改進。 如需詳細資訊，請參閱 MSDN 上的 [自動偵測變更](https://msdn.microsoft.com/data/jj556205) 。

## <a name="automatic-validation"></a>自動驗證

當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更之實體的所有屬性中的資料。 如果您已更新大量的實體，而且已經驗證資料，則這項工作是不必要的，而且您可以暫時關閉驗證，讓儲存變更的程式花較少的時間。 您可以使用 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 屬性來這麼做。 如需詳細資訊，請參閱 MSDN 上的 [驗證](https://msdn.microsoft.com/data/gg193959) 。

## <a name="entity-framework-power-tools"></a>Entity Framework Power Tools

[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) 是 Visual Studio 的增益集，可用來建立這些教學課程中所示的資料模型圖表。 這些工具也可以執行其他功能，例如，根據現有資料庫中的資料表來產生實體類別，以便您可以將資料庫用於 Code First。 安裝工具之後，內容功能表中會出現一些額外的選項。 例如，當您以滑鼠右鍵按一下 **方案總管**中的內容類別時，您會看到並 **Entity Framework** 選項。 這讓您能夠產生圖表。 當您使用 Code First 不能變更圖表中的資料模型，但您可以移動一些東西，讓您更容易瞭解。

![EF 圖表](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Entity Framework 來源程式碼

您可以從 [GitHub](https://github.com/aspnet/EntityFramework6)取得 Entity Framework 6 的原始程式碼。 您可以提出 bug，也可以為 EF 原始程式碼貢獻自己的增強功能。

雖然原始程式碼已開啟，但 Entity Framework 是 Microsoft 產品的完整支援。 Microsoft Entity Framework 小組將控制接受哪些貢獻，並測試所有的程式碼變更以確保每次發行的品質。

## <a name="acknowledgments"></a>通知

- Tom Dykstra 撰寫了本教學課程的原始版本，共同撰寫了 EF 5 更新，並撰寫了 EF 6 更新。 Tom 是 Microsoft Web Platform and Tools 內容小組的資深程式設計作者。
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 大部分的工作更新了 EF 5 和 MVC 4 的教學課程，並共同撰寫了 ef 6 更新。 Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。
- [Rowan 莎莎](http://www.romiller.com) 和 Entity Framework 團隊的其他成員協助進行程式碼審核，並協助您在更新 EF 5 和 ef 6 的教學課程時，在發生遷移的許多問題時進行調試。

## <a name="troubleshoot-common-errors"></a>常見問題疑難排解

### <a name="cannot-createshadow-copy"></a>無法建立/陰影複製

錯誤訊息：

> &lt; &gt; 當該檔案已經存在時，無法建立/陰影複製 ' filename '。

解決方案

等候幾秒鐘，然後重新整理頁面。

### <a name="update-database-not-recognized"></a>更新-資料庫無法辨認

從 PMC) 的命令 (的錯誤訊息 `Update-Database` ：

> 「更新資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可操作程式的名稱。 請檢查名稱拼字，如果名稱含有路徑，請確認路徑正確，然後再試一次。

解決方案

結束 Visual Studio。 重新開啟專案，然後再試一次。

### <a name="validation-failed"></a>驗證失敗

從 PMC) 的命令 (的錯誤訊息 `Update-Database` ：

> 一或多個實體的驗證失敗。 如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。

解決方案

發生此問題的其中一個原因是方法執行時發生驗證錯誤 `Seed` 。 請參閱 [植入和偵測 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 以取得對方法進行偵錯工具的秘訣 `Seed` 。

### <a name="http-50019-error"></a>HTTP 500.19 錯誤

錯誤訊息：

> HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的頁面，因為頁面的相關設定資料無效。

解決方案

您可以取得此錯誤的其中一種方式，就是使用多個解決方案複本，每個複本都使用相同的埠號碼。 您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決這個問題。 如果無法運作，請嘗試變更埠號碼。 以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。 選取 [ **Web** ] 索引標籤，然後變更 [ **專案 Url** ] 文字方塊中的埠號碼。

### <a name="error-locating-sql-server-instance"></a>搜尋 SQL Server 執行個體時發生錯誤

錯誤訊息：

> 和 SQL Server 建立連線時，發生與網路相關或執行個體特定的錯誤。 找不到或無法存取伺服器。 檢查執行個體名稱是否正確以及 SQL Server 執行個體是否設定為允許遠端連接。 (提供者：SQL 網路介面，錯誤：26 - 搜尋指定的伺服器/執行個體時發生錯誤)

解決方案

檢查連接字串。 如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

 如需有關如何使用 Entity Framework 來處理資料的詳細資訊，請參閱 [MSDN 上的 EF 檔頁面](https://msdn.microsoft.com/data/ee712907) 和 [ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)。

如需如何在建立 web 應用程式之後進行部署的詳細資訊，請參閱 MSDN Library 中的 [ASP.NET Web 部署-建議的資源](../../../../whitepapers/aspnet-web-deployment-content-map.md) 。

如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱 [ASP.NET Mvc 建議的資源](../recommended-resources-for-mvc.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您：

> [!div class="checklist"]
> * 執行原始 SQL 查詢
> * 執行無追蹤查詢
> * 檢查傳送至資料庫的 SQL 查詢

您也已瞭解：

> [!div class="checklist"]
> * 建立抽象層
> * Proxy 類別
> * 自動變更偵測
> * 自動驗證
> * Entity Framework Power Tools
> * Entity Framework 來源程式碼

這一系列的教學課程會在 ASP.NET MVC 應用程式中使用 Entity Framework 完成。 如果您想要瞭解 EF Database First，請參閱資料庫第一個教學課程系列。
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)
