---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
title: '有效率地分頁大量資料 (c # ) |Microsoft Docs'
author: rick-anderson
description: 使用大量資料時，資料呈現控制項的預設分頁選項不適合，因為其基礎資料來源控制項 retriev .。。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 59c01998-9326-4ecb-9392-cb9615962140
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 154bcfeed8e64869b7c32d35b4fb05b6e611dadc
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045269"
---
# <a name="efficiently-paging-through-large-amounts-of-data-c"></a>有效率地分頁大量資料 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_CS.exe) 或 [下載 PDF](efficiently-paging-through-large-amounts-of-data-cs/_static/datatutorial25cs1.pdf)

> 使用大量資料時，資料展示檔控制項的預設分頁選項不適合，因為它的基礎資料來源控制項會抓取所有記錄，即使只顯示資料的子集也一樣。 在這種情況下，我們必須開啟自訂分頁。

## <a name="introduction"></a>簡介

如先前的教學課程中所討論，您可以透過下列兩種方式之一來執行分頁：

- 只要勾選 data Web control 的智慧標籤中的 [啟用分頁] 選項，就可以實作為**預設分頁**;不過，每當您看到資料頁面時，ObjectDataSource 都會抓取*所有*的記錄，即使頁面中只會顯示其中的子集也一樣。
- **自訂分頁** 藉由只針對使用者要求的特定資料頁面，只抓取需要顯示的資料庫記錄，來改善預設分頁的效能。不過，自訂分頁需要比預設分頁更費力地執行

由於執行的便利性很簡單，請勾選核取方塊，然後再完成！ 預設分頁是一個吸引人的選項。 不過，在抓取所有記錄的方法中，它會讓它成為 implausible 的選擇，以分頁處理足夠大量的資料，或針對具有許多並行使用者的網站。 在這種情況下，我們必須開啟自訂分頁，才能提供回應式系統。

自訂分頁的挑戰是能夠撰寫查詢，以傳回特定資料頁面所需的一組精確記錄。 幸運的是，Microsoft SQL Server 2005 提供了用於排名結果的新關鍵字，可讓我們撰寫可有效率地取出適當記錄子集的查詢。 在本教學課程中，我們將瞭解如何使用這個新的 SQL Server 2005 關鍵字，在 GridView 控制項中執行自訂分頁。 雖然自訂分頁的使用者介面與預設分頁的使用者介面完全相同，但使用自訂分頁從某個頁面逐步執行到下一個頁面，可能比預設分頁更快許多。

> [!NOTE]
> 自訂分頁所呈現的確切效能提升，取決於要進行分頁的記錄總數，以及要放置在資料庫伺服器上的負載。 在本教學課程結束時，我們將探討一些粗略的計量，以展示透過自訂分頁取得的效能優勢。

## <a name="step-1-understanding-the-custom-paging-process"></a>步驟1：瞭解自訂分頁流程

逐頁查看資料時，頁面中顯示的精確記錄取決於所要求的資料頁面，以及每頁顯示的記錄數目。 例如，假設我們想要逐頁查看81產品，每頁顯示10個產品。 查看第一頁時，我們需要產品1到 10;當您看到第二頁時，我們會對產品11到20感興趣，依此類推。

有三個變數規定需要抓取哪些記錄，以及應如何轉譯分頁介面：

- **開始資料列索引** ：要顯示的資料頁面中第一個資料列的索引;您可以藉由將頁面索引與每頁顯示的記錄相乘來計算此索引，並加入一個。 例如，當逐頁查看記錄10時，對於頁面索引為 0) 的第一頁 (，起始資料列索引為 0 \* 10 + 1，或 1; 對於頁面索引為 1) 的第二頁 (，起始資料列索引為 1 \* 10 + 1 或11。
- **最大資料列** 數：每頁顯示的記錄數目上限。 此變數稱為最大資料列，自最後一頁起，傳回的記錄可能會少於頁面大小。 例如，當逐頁查看每個頁面的81產品10筆記錄時，第九個和最後一個頁面將只會有一筆記錄。 但是，沒有頁面會顯示比最大資料列值更多的記錄。
- **總記錄計數** 是要進行分頁的記錄總數。 雖然此變數不需要用來判斷要針對特定頁面抓取哪些記錄，但它確實會指示分頁介面。 例如，如果有81的產品正在進行分頁，則分頁介面知道要在分頁 UI 中顯示九個頁碼。

使用預設分頁時，開始資料列索引會計算為頁面索引和頁面大小加一的乘積，而最大資料列則只是頁面大小。 由於預設分頁會在轉譯任何頁面的資料時，從資料庫取得所有記錄，因此每個資料列的索引都是已知的，因此將移到開始資料列索引資料列的簡單工作。 此外，記錄計數總計很容易使用，因為它只是 DataTable (中的記錄數目，或是用來保存資料庫結果) 的任何物件。

如果指定了開始資料列索引和最大資料列變數，自訂分頁執行就只能傳回從開始資料列索引開始的精確記錄子集，以及之後最多資料列數的記錄。 自訂分頁提供兩個挑戰：

- 我們必須能夠有效率地將資料列索引與要進行分頁的整個資料中的每個資料列產生關聯，以便我們可以在指定的開始資料列索引處開始傳回記錄
- 我們需要提供已分頁的記錄總數

在接下來的兩個步驟中，我們將探討回應這兩個挑戰所需的 SQL 腳本。 除了 SQL 腳本，我們也需要在 DAL 和 BLL 中執行方法。

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>步驟2：傳回已分頁的記錄總數

在我們檢查如何取出所顯示頁面的精確記錄子集之前，讓我們先看看如何傳回已分頁的記錄總數。 需要這項資訊，才能正確設定分頁使用者介面。 您可以使用[ `COUNT` aggregate 函數](https://msdn.microsoft.com/library/ms175997.aspx)來取得特定 SQL 查詢所傳回的記錄總數。 例如，若要判斷資料表中的總記錄數 `Products` ，我們可以使用下列查詢：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample1.sql)]

讓 s 將方法新增至我們的 DAL，以傳回此資訊。 尤其是，我們將建立名為的 DAL 方法 `TotalNumberOfProducts()` ，以執行 `SELECT` 上面顯示的語句。

從開啟 `Northwind.xsd` 資料夾中具類型的資料集檔案開始 `App_Code/DAL` 。 接下來，以滑鼠右鍵按一下 `ProductsTableAdapter` 設計工具中的，然後選擇 [加入查詢]。 如先前的教學課程中所見，這可讓我們將新的方法加入 DAL，當叫用此方法時，將會執行特定的 SQL 語句或預存程式。 如同先前教學課程中的 TableAdapter 方法，這是選擇使用臨機操作的 SQL 語句。

![使用特定 SQL 語句](efficiently-paging-through-large-amounts-of-data-cs/_static/image1.png)

**圖 1**：使用特定 SQL 語句

在下一個畫面中，可以指定要建立的查詢類型。 因為此查詢會傳回單一純量值，所以資料表中的記錄總數會 `Products` 選擇傳回單一 `SELECT` 值選項。

![將查詢設定為使用會傳回單一值的 SELECT 語句](efficiently-paging-through-large-amounts-of-data-cs/_static/image2.png)

**圖 2**：將查詢設定為使用會傳回單一值的 SELECT 語句

指出要使用的查詢類型之後，我們必須接著指定查詢。

![從 Products 查詢使用 SELECT COUNT ( * ) ](efficiently-paging-through-large-amounts-of-data-cs/_static/image3.png)

**圖 3**：使用 Products 查詢中的 SELECT COUNT (\*) 

最後，指定方法的名稱。 如前所述，讓我們使用 `TotalNumberOfProducts` 。

![將 DAL 方法命名為 TotalNumberOfProducts](efficiently-paging-through-large-amounts-of-data-cs/_static/image4.png)

**圖 4**：命名 DAL 方法 TotalNumberOfProducts

按一下 [完成] 之後，嚮導會將 `TotalNumberOfProducts` 方法新增至 DAL。 當 SQL 查詢的結果為時，DAL 傳回的純量方法會傳回可為 null 的類型 `NULL` 。 但是，我們 `COUNT` 的查詢一律會傳回非 `NULL` 值; 而是，DAL 方法會傳回可為 null 的整數。

除了 DAL 方法之外，我們也需要 BLL 中的方法。 開啟 `ProductsBLL` 類別檔案，並新增 `TotalNumberOfProducts` 直接向下呼叫 DAL s 方法的方法 `TotalNumberOfProducts` ：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample2.cs)]

DAL s `TotalNumberOfProducts` 方法會傳回可為 null 的整數; 不過，我們已建立 `ProductsBLL` 類別的方法， `TotalNumberOfProducts` 使其傳回標準的整數。 因此，我們必須讓類別的 `ProductsBLL` `TotalNumberOfProducts` 方法傳回 DAL s 方法所傳回之可為 null 整數的值部分 `TotalNumberOfProducts` 。 的呼叫 `GetValueOrDefault()` 會傳回可為 null 的整數值（如果存在的話）; 如果可為 null 的整數，則會傳回 `null` 預設整數值0。

## <a name="step-3-returning-the-precise-subset-of-records"></a>步驟3：傳回精確的記錄子集

下一項工作是在 DAL 和 BLL 中建立方法，以接受稍早所討論的開始資料列索引和最大資料列變數，並傳回適當的記錄。 在這麼做之前，讓我們先看看所需的 SQL 腳本。 面臨的挑戰是，我們必須能夠有效率地將索引指派給整個結果中的每個資料列，讓我們可以只傳回從開始資料列索引開始 (的記錄，以及最多記錄) 的記錄數目上限。

如果資料庫資料表中已經有一個資料行做為資料列索引，這就不是一項挑戰。 乍看之下，我們可能會認為 `Products` 資料表的 `ProductID` 欄位就足夠了，因為第一個產品有 `ProductID` 1 個，第二個是2，依此類推。 不過，刪除產品時，重此方法。

有兩種一般技巧可用來有效率地將資料列索引與要逐頁查看的資料產生關聯，藉此啟用精確的記錄子集：

- **使用 SQL Server 2005 s `ROW_NUMBER()` 關鍵字** new to SQL Server 2005， `ROW_NUMBER()` 關鍵字會根據某種順序將排名與每個傳回的記錄產生關聯。 此排名可作為每個資料列的資料列索引使用。
- **使用資料表變數和 `SET ROWCOUNT` **SQL Server s [ `SET ROWCOUNT` 語句](https://msdn.microsoft.com/library/ms188774.aspx)可以用來指定在終止之前，查詢應該處理的總記錄數;[資料表變數](http://www.sqlteam.com/item.asp?ItemID=9454)是可保存表格式資料的本機 t-sql 變數，類似于[臨時表](http://www.sqlteam.com/item.asp?ItemID=2029)。 這種方法同樣適用于 Microsoft SQL Server 2005 和 SQL Server 2000 (，但此 `ROW_NUMBER()` 方法只適用于 SQL Server 2005) 。  
  
  此處的概念是建立資料表變數，此變數具有 `IDENTITY` 資料要進行分頁的資料表之主鍵的資料行和資料行。 接下來，將資料分頁的資料表內容傾印到資料表變數中，藉此將連續資料列索引 (透過 `IDENTITY` 資料表中每一筆記錄的資料行) 來建立關聯。 一旦擴展資料表變數之後， `SELECT` 就可以執行資料表變數（與基礎資料表聯結）上的語句，以提取特定記錄。 `SET ROWCOUNT`語句是用來以智慧方式限制必須傾印到資料表變數中的記錄數目。  
  
  這種方法的效率是根據所要求的頁碼，因為 `SET ROWCOUNT` 值會被指派開始資料列索引的值加上最大資料列數。 當您透過低編號的頁面（例如前幾頁的資料）進行分頁時，此方法非常有效率。 不過，它會在抓取接近結尾的頁面時，展現預設的分頁效能。

本教學課程會使用關鍵字來實行自訂分頁 `ROW_NUMBER()` 。 如需有關使用資料表變數和技術的詳細資訊 `SET ROWCOUNT` ，請參閱 [透過大型結果集進行分頁的更有效率的方法](http://www.4guysfromrolla.com/webtech/042606-1.shtml)。

`ROW_NUMBER()`關鍵字會使用下列語法，針對特定排序傳回的每一筆記錄進行排名關聯：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample3.sql)]

`ROW_NUMBER()` 傳回數值，這個值會指定與指定順序相關的每一筆記錄排名。 例如，若要查看每項產品的排名（從最昂貴到最少），我們可以使用下列查詢：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample4.sql)]

[圖 5] 顯示在 Visual Studio 中執行查詢視窗時的查詢結果。 請注意，產品會依價格排序，以及每個資料列的價格等級。

![每個傳回的記錄都會包含價格等級](efficiently-paging-through-large-amounts-of-data-cs/_static/image5.png)

**圖 5**：每個傳回的記錄都會包含價格等級

> [!NOTE]
> `ROW_NUMBER()` 只是 SQL Server 2005 中可用的許多新次序函數之一。 如需更詳盡的討論 `ROW_NUMBER()` ，以及其他次序函數，請 [使用 Microsoft SQL Server 2005 來讀取傳回排名的結果](http://www.4guysfromrolla.com/webtech/010406-1.shtml)。

依子句中的指定資料行將結果排名 `ORDER BY` `OVER` (中 `UnitPrice` ，在上述範例) 中，SQL Server 必須排序結果。 如果在資料行上有叢集索引，則這是一項快速的作業， (s) 結果是以排序，或有涵蓋索引，但在其他情況下可能更昂貴。 若要協助改善足夠的大型查詢效能，請考慮針對用來排序結果的資料行加入非叢集索引。 如需效能考慮的詳細資訊，請參閱 [SQL Server 2005 中的次序函數和效能](http://www.sql-server-performance.com/ak_ranking_functions.asp) 。

傳回的排名資訊 `ROW_NUMBER()` 無法直接在子句中使用 `WHERE` 。 不過，您可以使用衍生資料表來傳回 `ROW_NUMBER()` 結果，然後在子句中出現這些結果 `WHERE` 。 例如，下列查詢會使用衍生資料表來傳回 ProductName 和單價資料行以及 `ROW_NUMBER()` 結果，然後使用 `WHERE` 子句來傳回價格等級介於11和20之間的產品：

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample5.sql)]

更進一步擴充這個概念，我們可以利用這種方法，根據所需的起始資料列索引和最大資料列值來抓取特定的資料頁面：

[!code-html[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample6.html)]

> [!NOTE]
> 我們稍後會在本教學課程中看到， *`StartRowIndex`* ObjectDataSource 提供的是從零開始編制索引，而 `ROW_NUMBER()` SQL Server 2005 所傳回的值是從1開始編制索引。 因此， `WHERE` 子句 `PriceRank` 會傳回嚴格大於 *`StartRowIndex`* 和小於或等於的記錄 *`StartRowIndex`*  +  *`MaximumRows`* 。

現在，我們已討論過如何在 `ROW_NUMBER()` 指定開始資料列索引和最大資料列值的情況下，用來取得特定頁面的資料，我們現在需要將此邏輯實作為 DAL 和 BLL 中的方法。

建立此查詢時，我們必須決定要將結果分級的順序;讓我們依字母順序排列產品的名稱。 這表示，在本教學課程中使用自訂分頁執行時，我們將無法建立比也可以排序的自訂分頁報表。 但在下一個教學課程中，我們會看到如何提供這類功能。

在上一節中，我們建立了 DAL 方法作為臨機操作 SQL 語句。 可惜的是，TableAdapter wizard 所使用 Visual Studio 中的 T-sql 剖析器不像函式所 `OVER` 使用的語法 `ROW_NUMBER()` 。 因此，我們必須將此 DAL 方法建立為預存程式。 選取 [View] 功能表中的 [伺服器總管] (或按 Ctrl + Alt + S) 並展開 `NORTHWND.MDF` 節點。 若要加入新的預存程式，請以滑鼠右鍵按一下 [預存程式] 節點，然後選擇 [加入新的預存程式] (查看 [圖 6]) 。

![加入新的預存程式，以透過產品進行分頁](efficiently-paging-through-large-amounts-of-data-cs/_static/image6.png)

**圖 6**：加入新的預存程式，以透過產品進行分頁

這個預存程式應接受兩個整數輸入 `@startRowIndex` 參數 `@maximumRows` ，並使用 `ROW_NUMBER()` 依欄位排序的函式 `ProductName` ，只傳回大於指定 `@startRowIndex` 且小於或等於 s 的資料列 `@startRowIndex`  +  `@maximumRow` 。 在新的預存程式中輸入下列腳本，然後按一下 [儲存] 圖示，將預存程式加入至資料庫。

[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample7.sql)]

在建立預存程式之後，請花點時間進行測試。以滑鼠右鍵按一下 `GetProductsPaged` 伺服器總管中的預存程式名稱，然後選擇 [執行] 選項。 Visual Studio 接著會提示您輸入參數， `@startRowIndex` 而 `@maximumRow` (請參閱 [圖 7]) 。 請嘗試不同的值，並檢查結果。

![輸入 @startRowIndex 和參數的值 @maximumRows](efficiently-paging-through-large-amounts-of-data-cs/_static/image7.png)

<strong>圖 7</strong>：輸入 @startRowIndex 和參數的值 @maximumRows

選擇這些輸入參數值之後，輸出視窗會顯示結果。 [圖 8] 顯示針對和參數傳入10時的 `@startRowIndex` 結果 `@maximumRows` 。

[![會傳回出現在第二頁數據的記錄](efficiently-paging-through-large-amounts-of-data-cs/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image8.png)

**圖 8**：會傳回出現在第二頁數據的記錄， ([按一下以查看完整大小的影像](efficiently-paging-through-large-amounts-of-data-cs/_static/image10.png)) 

建立此預存程式之後，我們就可以開始建立 `ProductsTableAdapter` 方法。 開啟具 `Northwind.xsd` 類型的資料集，以滑鼠右鍵按一下 `ProductsTableAdapter` ，然後選擇 [加入查詢] 選項。 使用現有的預存程式，而不是使用臨機操作 SQL 語句來建立查詢。

![使用現有的預存程式建立 DAL 方法](efficiently-paging-through-large-amounts-of-data-cs/_static/image11.png)

**圖 9**：使用現有的預存程式建立 DAL 方法

接下來，系統會提示您選取要叫用的預存程式。 `GetProductsPaged`從下拉式清單中選取預存程式。

![從下拉式清單中選擇 GetProductsPaged 預存程式](efficiently-paging-through-large-amounts-of-data-cs/_static/image12.png)

**圖 10**：從下拉式清單選擇 GetProductsPaged 預存程式

接下來的畫面會詢問您預存程式所傳回的資料類型：表格式資料、單一值或無值。 由於 `GetProductsPaged` 預存程式可以傳回多個記錄，表示它會傳回表格式資料。

![指出預存程式會傳回表格式資料](efficiently-paging-through-large-amounts-of-data-cs/_static/image13.png)

**圖 11**：指出預存程式傳回表格式資料

最後，指出您想要建立之方法的名稱。 如同先前的教學課程，請繼續進行，並使用「填滿 DataTable」和「傳回 DataTable」來建立方法。 將第一個方法命名為第 `FillPaged` 二個 `GetProductsPaged` 。

![將方法命名為 FillPaged 和 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-cs/_static/image14.png)

**圖 12**：將方法命名為 FillPaged 和 GetProductsPaged

除了建立 DAL 方法來傳回特定的產品頁面之外，我們也需要在 BLL 中提供這類功能。 與 DAL 方法相同，BLL s GetProductsPaged 方法必須接受兩個整數輸入，以指定開始資料列索引和最大資料列，而且必須只傳回落在指定範圍內的那些記錄。 在 ProductsBLL 類別中建立這種類型的 BLL 方法，只會向下呼叫 DAL s GetProductsPaged 方法，如下所示：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample8.cs)]

您可以針對 BLL 方法的輸入參數使用任何名稱，但我們很快就會看到， `startRowIndex` `maximumRows` 在設定 ObjectDataSource 以使用此方法時，選擇使用並節省更多工作。

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>步驟4：設定 ObjectDataSource 使用自訂分頁

使用 BLL 和 DAL 方法來存取特定記錄子集之後，我們就可以開始建立 GridView 控制項，以使用自訂分頁來逐頁查看其基礎記錄。 首先 `EfficientPaging.aspx` ，開啟資料夾中的頁面 `PagingAndSorting` ，將 GridView 加入至頁面，並將它設定為使用新的 ObjectDataSource 控制項。 在過去的教學課程中，我們通常會將 ObjectDataSource 設定為使用 `ProductsBLL` 類別 s `GetProducts` 方法。 不過，這次我們要改用 `GetProductsPaged` 方法，因為方法會傳回 `GetProducts` 資料庫中的 *所有* 產品，而只會傳回 `GetProductsPaged` 特定的記錄子集。

![將 ObjectDataSource 設定為使用 ProductsBLL 類別 s GetProductsPaged 方法](efficiently-paging-through-large-amounts-of-data-cs/_static/image15.png)

**圖 13**：設定 ObjectDataSource 使用 ProductsBLL 類別的 GetProductsPaged 方法

由於我們要建立唯讀 GridView，請花點時間在 [插入]、[更新] 和 [刪除] 索引標籤中設定 [方法] 下拉式清單， ([無]) 。

接下來，ObjectDataSource wizard 會提示我們輸入 `GetProductsPaged` 方法 `startRowIndex` 和 `maximumRows` 輸入參數值的來源。 這些輸入參數實際上會由 GridView 自動設定，因此只要將來源設定為 [無]，然後按一下 [完成] 即可。

![將輸入參數來源保留為無](efficiently-paging-through-large-amounts-of-data-cs/_static/image16.png)

**圖 14**：將輸入參數來源保留為 None

完成 ObjectDataSource wizard 之後，GridView 將會包含每個產品資料欄位的 BoundField 或 CheckBoxField。 您可以隨意調整 GridView 的外觀。 我選擇只顯示 `ProductName` 、、 `CategoryName` `SupplierName` 、 `QuantityPerUnit` 和 `UnitPrice` BoundFields。 此外，請核取其智慧標籤中的 [啟用分頁] 核取方塊，將 GridView 設定為支援分頁。 這些變更之後，GridView 和 ObjectDataSource 宣告式標記看起來應該類似下列內容：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample9.aspx)]

但是，如果您透過瀏覽器流覽網頁，則不需要找到 GridView。

![GridView 未顯示](efficiently-paging-through-large-amounts-of-data-cs/_static/image17.png)

**圖 15**：未顯示 GridView

因為 ObjectDataSource 目前使用0做為 `GetProductsPaged` `startRowIndex` 和輸入參數的值，所以遺漏 GridView `maximumRows` 。 因此，產生的 SQL 查詢不會傳回任何記錄，因此不會顯示 GridView。

若要解決此情況，我們必須將 ObjectDataSource 設定為使用自訂分頁。 您可以在下列步驟中完成這項作業：

1. **將 objectdatasource s `EnablePaging` 屬性設為 `true` ** ，就會向 ObjectDataSource 指出它必須傳遞給 `SelectMethod` 兩個額外的參數：一個用來指定起始資料列索引 ([`StartRowIndexParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx)) ，另一個則用來指定 () 的最大資料列 [`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) 。
2. **據此設定 ObjectDataSource `StartRowIndexParameterName` 和 `MaximumRowsParameterName` 屬性** `StartRowIndexParameterName` ，和 `MaximumRowsParameterName` 屬性會指出傳入的輸入參數名稱， `SelectMethod` 以供自訂分頁之用。 根據預設，這些參數名稱是，而 `startIndexRow` `maximumRows` 這也是為什麼在 `GetProductsPaged` BLL 中建立方法時，我使用這些值做為輸入參數。 如果您選擇對 BLL 的方法（例如和）使用不同的參數名稱，例如， `GetProductsPaged` `startIndex` `maxRows` 您將需要據以設定 ObjectDataSource `StartRowIndexParameterName` 和 `MaximumRowsParameterName` 屬性 (例如，) 的 startIndex for `StartRowIndexParameterName` 和 maxRows `MaximumRowsParameterName` 。
3. **將 ObjectDataSource s [ `SelectCountMethod` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx)設定為方法的名稱，此方法會傳回透過 (所分頁的記錄總數 `TotalNumberOfProducts`) **回想一下， `ProductsBLL` 類別 s 方法會傳回 `TotalNumberOfProducts` 使用執行查詢的 DAL 方法來分頁的總記錄數 `SELECT COUNT(*) FROM Products` 。 ObjectDataSource 需要這項資訊，才能正確轉譯分頁介面。
4. 當您透過 wizard 設定 ObjectDataSource 時， ** `startRowIndex` `maximumRows` `<asp:Parameter>` 從 ObjectDataSource 的宣告式標記中移除和元素**，Visual Studio 自動新增 `<asp:Parameter>` `GetProductsPaged` 方法 s 輸入參數的兩個元素。 藉由將設定 `EnablePaging` 為 `true` ，就會自動傳遞這些參數; 如果它們也出現在宣告式語法中，ObjectDataSource 會嘗試將 *四個* 參數傳遞給 `GetProductsPaged` 方法，並將兩個參數傳遞給 `TotalNumberOfProducts` 方法。 如果您忘記移除這些專案 `<asp:Parameter>` ，當您透過瀏覽器流覽頁面時，將會收到類似下列的錯誤訊息： *ObjectDataSource ' ObjectDataSource1 ' 找不到具有參數： StartRowIndex，maximumRows 的非泛型方法 ' TotalNumberOfProducts '*。

進行這些變更之後，ObjectDataSource 的宣告式語法看起來應該如下所示：

[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample10.aspx)]

請注意， `EnablePaging` 已 `SelectCountMethod` 設定和屬性，且已 `<asp:Parameter>` 移除這些元素。 [圖 16] 顯示在進行這些變更之後，屬性視窗的螢幕擷取畫面。

![若要使用自訂分頁，請設定 ObjectDataSource 控制項](efficiently-paging-through-large-amounts-of-data-cs/_static/image18.png)

**圖 16**：若要使用自訂分頁，請設定 ObjectDataSource 控制項

進行這些變更之後，請透過瀏覽器造訪此頁面。 您應該會看到依字母順序排列的10個產品。 花點時間逐一查看資料一頁。 雖然使用者在預設分頁和自訂分頁之間沒有視覺差異，但是自訂頁面會透過大量資料更有效率地分頁，因為它只會抓取需要針對特定頁面顯示的記錄。

[![依產品名稱排序的資料會使用自訂分頁進行分頁](efficiently-paging-through-large-amounts-of-data-cs/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image19.png)

**圖 17**：依產品 s 名稱排序的資料會使用自訂分頁進行分頁 ([按一下以查看完整大小的影像](efficiently-paging-through-large-amounts-of-data-cs/_static/image21.png)) 

> [!NOTE]
> 使用自訂分頁時，ObjectDataSource 所傳回的頁面計數值 `SelectCountMethod` 會儲存在 GridView 的檢視狀態中。 其他 GridView 變數 `PageIndex` ：、 `EditIndex` 、 `SelectedIndex` 、 `DataKeys` 集合等等都會儲存在 *控制項狀態*中，不論 GridView 的屬性值為何，都會保存該狀態 `EnableViewState` 。 由於此 `PageCount` 值會在使用 view 狀態的回傳之間保存，因此使用包含連結的頁面介面將您帶到最後一個頁面時，必須啟用 GridView 的檢視狀態。  (如果您的分頁介面未包含最後一頁的直接連結，您可能會停用 [view state]。 ) 

按一下 [最後一頁] 連結會導致回傳，並指示 GridView 更新其 `PageIndex` 屬性。 如果按一下 [最後一頁] 連結，GridView 會將其 `PageIndex` 屬性指派給一個小於其屬性的值 `PageCount` 。 停用 view 狀態時， `PageCount` 值會在回傳之間遺失， `PageIndex` 而會將最大整數值指派給。 接下來，GridView 會透過將和屬性相乘來嘗試判斷起始資料列索引 `PageSize` `PageCount` 。 這會導致， `OverflowException` 因為產品超過允許的整數大小上限。

## <a name="implement-custom-paging-and-sorting"></a>執行自訂分頁和排序

目前的自訂分頁執行需要在建立預存程式時，以靜態方式指定資料分頁的順序 `GetProductsPaged` 。 不過，您可能已經注意到，除了啟用分頁選項以外，GridView 的智慧標籤還包含 [啟用排序] 核取方塊。 可惜的是，使用目前的自訂分頁執行將排序支援新增至 GridView，只會在目前已查看的資料頁面上排序記錄。 例如，如果您將 GridView 設定為也支援分頁，然後在流覽資料的第一頁時，依產品名稱以遞減順序排序，就會反轉頁面1上產品的順序。 如圖18所示，這種方式會在以反向字母順序排序時，顯示 Carnarvon 虎做為第一個產品，這會忽略 Carnarvon 虎之後的71其他產品（依字母順序）。只有第一個頁面上的記錄會被視為排序。

[![只會排序目前頁面上顯示的資料](efficiently-paging-through-large-amounts-of-data-cs/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image22.png)

**圖 18**：只有目前頁面上顯示的資料會排序 ([按一下以查看完整大小的影像](efficiently-paging-through-large-amounts-of-data-cs/_static/image24.png)) 

排序只適用于目前的資料頁面，因為排序是在從 BLL s 方法取出資料之後發生 `GetProductsPaged` ，而且這個方法只會傳回特定頁面的那些記錄。 若要正確地執行排序，我們必須將排序運算式傳遞至 `GetProductsPaged` 方法，以便在傳回特定的資料頁面之前，先適當地排列資料的等級。 我們將在下一個教學課程中瞭解如何完成這項工作。

## <a name="implementing-custom-paging-and-deleting"></a>執行自訂分頁和刪除

如果您在使用自訂分頁技術來將資料分頁的 GridView 中啟用刪除功能，則會發現當您刪除最後一頁的最後一筆記錄時，GridView 會消失，而不會適當地遞減 GridView `PageIndex` 。 若要重現這個錯誤，請針對我們剛剛建立的教學課程啟用刪除。 移至最後一頁 (第9頁) ，您應該會在其中看到單一產品，因為我們會逐頁查看81產品、10個產品一次。 刪除此產品。

在刪除最後一個產品時，GridView *應該* 會自動移至第八個頁面，而這類功能會使用預設分頁來呈現。 不過，有了自訂分頁之後，在最後一頁上刪除最後一個產品之後，GridView 就完全從畫面中消失了。 發生這種情況的 *精確原因是此教學* 課程的範圍外，請參閱 [從 GridView 刪除最後一個頁面](http://scottonwriting.net/sowblog/posts/7326.aspx) 上的最後一筆記錄，其中包含有關此問題來源的低層級詳細資料的自訂分頁。 總而言之，這是因為按一下 [刪除] 按鈕時，GridView 所執行的下列步驟順序：

1. 刪除記錄
2. 取得要針對指定的和顯示的適當記錄 `PageIndex``PageSize`
3. 檢查以確定不 `PageIndex` 會超過資料來源中的資料頁數; 如果有，則會自動遞減 GridView 的 `PageIndex` 屬性
4. 使用步驟2中取得的記錄，將適當的資料頁面系結至 GridView

問題源自于步驟2中， `PageIndex` 當抓取要顯示的記錄時，所使用的也是 `PageIndex` 最後一頁剛刪除唯一記錄的情況。 因此，在步驟2中，因為最後一頁的資料已不再包含任何記錄，所以 *不* 會傳回任何記錄。 然後，在步驟3中，GridView 發現其 `PageIndex` 屬性大於資料來源 (中的總頁數，因為我們已刪除最後一個) 頁面中的最後一筆記錄，因此會遞減其 `PageIndex` 屬性。 在步驟4中，GridView 會嘗試將本身系結至步驟2中所取出的資料;不過，在步驟2中，未傳回任何記錄，因此會產生空的 GridView。 使用預設分頁時，此問題並不會出現，因為在步驟2中， *所有* 記錄都會從資料來源取出。

為了修正此問題，我們有兩個選項。 第一個方法是為 GridView 的事件處理常式建立事件處理常式 `RowDeleted` ，以決定要在頁面中顯示的記錄數目是剛才刪除的。 如果只有一筆記錄，則剛刪除的記錄必須是最後一個記錄，而我們需要遞減 GridView `PageIndex` 。 當然，我們只想要 `PageIndex` 在刪除作業真的成功時更新，這可以藉由確保 `e.Exception` 屬性為來判斷 `null` 。

這種方法的運作方式是因為它會 `PageIndex` 在步驟1之後，但在步驟2之前更新。 因此，在步驟2中，會傳回適當的一組記錄。 若要完成此動作，請使用如下所示的程式碼：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample11.cs)]

替代的解決方法是為 ObjectDataSource s 事件建立事件處理常式 `RowDeleted` ，並將屬性設定 `AffectedRows` 為1的值。 在步驟1中刪除記錄之後 (但在重新取得步驟 2) 中的資料之前， `PageIndex` 如果有一或多個資料列受作業影響，則 GridView 會更新其屬性。 但是， `AffectedRows` 不會設定 ObjectDataSource 的屬性，因此會省略這個步驟。 執行此步驟的其中一種方式，是 `AffectedRows` 在刪除作業成功完成時手動設定屬性。 您可以使用類似下列的程式碼來完成這項作業：

[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample12.cs)]

這兩個事件處理常式的程式碼都可以在範例的程式碼後端類別中找到 `EfficientPaging.aspx` 。

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>比較預設和自訂分頁的效能

由於自訂分頁只會抓取所需的記錄，而預設分頁會傳回所要查看之每個頁面的 *所有* 記錄，因此會清楚自訂分頁比預設分頁更有效率。 但自訂分頁的效率就愈高？ 從預設分頁移至自訂分頁可以看到哪些效能提升？

可惜的是，這裡沒有一個大小適合的答案。 效能提升取決於許多因素，最重要的兩個是要進行分頁的記錄數目，以及放置於資料庫伺服器上的負載，以及 web 伺服器與資料庫伺服器之間的通道。 對於只有數十個記錄的小型資料表，效能差異可能會是微不足道。 但是針對大型資料表，有數千到數百個數據列，效能差異很大。

[ASP.NET 2.0 的自訂分頁（SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)）包含一些效能測試，這些測試會在使用50000記錄進行資料庫資料表的分頁時，顯示這兩個分頁技術之間的效能差異。 在這些測試中，我同時探討了使用 [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)) 的 SQL Server 層 (級執行查詢的時間，以及使用 [ASP.NET 追蹤功能](https://msdn.microsoft.com/library/y13fw6we.aspx)的 ASP.NET 網頁。 請記住，這些測試是在具有單一作用中使用者的 [我的開發] 方塊上執行，因此 unscientific 且不會模擬一般網站負載模式。 無論如何，在使用足夠大量的資料時，結果都會說明預設和自訂分頁執行時間的相對差異。

|  | **Avg. Duration (sec) ** | **Reads** |
| --- | --- | --- |
| **預設分頁 SQL Profiler** | 1.411 | 383 |
| **自訂分頁 SQL Profiler** | 0.002 | 29 |
| **預設分頁 ASP.NET 追蹤** | 2.379 | *N/A* |
| **自訂分頁 ASP.NET 追蹤** | 0.029 | *N/A* |

如您所見，若要抓取特定的資料頁面，所需的平均資料量為354，並在一段時間內完成。 在 [ASP.NET] 頁面上，自訂頁面在使用預設分頁時，可以在<sup>接近1/100 的</sup> 時間內轉譯。 請參閱 [我的文章](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) ，以取得這些結果的詳細資訊，以及您可以下載的程式碼和資料庫，以便在您自己的環境中重現這些測試。

## <a name="summary"></a>總結

預設分頁是一種標準化，可在資料 Web 控制項的智慧標籤中檢查 [啟用分頁] 核取方塊，但這種簡單的方式就是效能的成本。 使用預設分頁時，當使用者要求任何頁面的資料時，會傳回 *所有* 記錄，雖然可能只會顯示一小部分的記錄。 為了對抗這項效能負擔，ObjectDataSource 提供了一個替代分頁選項自訂分頁。

雖然自訂分頁可透過只抓取需要顯示的記錄來改善預設的分頁效能問題，但是更牽涉到執行自訂分頁。 首先，必須以正確的方式撰寫查詢， (並有效率地) 存取所要求之記錄的特定子集。 這可以透過數種方式來完成;我們在本教學課程中所探討的是使用 SQL Server 2005 s new 函式 `ROW_NUMBER()` 來排名結果，然後只傳回排名落在指定範圍內的結果。 此外，我們還需要新增一個方法來判斷要進行分頁的記錄總數。 建立這些 DAL 和 BLL 方法之後，我們也需要設定 ObjectDataSource，讓它可以判斷要進行分頁的總記錄數，並且可以正確地將開始資料列索引和最大資料列值傳遞給 BLL。

雖然執行自訂分頁的確需要一些步驟，而且不像預設分頁一樣簡單，但自訂分頁是分頁至足夠大量資料時的必要項。 如所述，自訂分頁可能會縮減 ASP.NET 網頁轉譯時間的秒數，而且可以將資料庫伺服器上的負載淡化一或多個量值順序。

快樂程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者是七個 ASP/ASP. NET 書籍和創辦人 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 [*在24小時內 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 您可以在此聯繫[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog （可在中找到） [http://ScottOnWriting.NET](http://ScottOnWriting.NET) 。

> [!div class="step-by-step"]
> [上一個](paging-and-sorting-report-data-cs.md) 
> [下一步](sorting-custom-paged-data-cs.md)
