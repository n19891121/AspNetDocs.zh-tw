---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: 使用 SQL 快取相依性 (VB) |Microsoft Docs
author: rick-anderson
description: 最簡單的快取策略是讓快取的資料在指定的一段時間之後過期。 但是這個簡單的方法表示快取的資料 maintai .。。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 175169772ba04376e1bd1cb143b13a200652a9bf
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044788"
---
# <a name="using-sql-cache-dependencies-vb"></a>使用 SQL 快取相依性 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip) 或 [下載 PDF](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> 最簡單的快取策略是讓快取的資料在指定的一段時間之後過期。 但這種簡單的方法表示快取的資料與基礎資料來源不會有任何關聯，而導致過時的資料被保留太久或目前的資料已過期。 更好的方法是使用 SqlCacheDependency 類別，讓資料保持快取狀態，直到其基礎資料在 SQL database 中經過修改為止。 本教學課程將為您示範作法。

## <a name="introduction"></a>簡介

快取技術在 [使用 ObjectDataSource](caching-data-with-the-objectdatasource-vb.md) 的快取資料中檢查，而架構教學課程中的快取 [資料](caching-data-in-the-architecture-vb.md) 則使用以時間為基礎的到期日，在指定的期間之後收回快取中的資料。 這種方法最簡單的方式，就是在快取的效能提升與資料過期之間取得平衡。 藉由選取 *x* 秒的到期時間，網頁開發人員 *concedes 只享受* 快取的效能優勢，而不只是 x 秒，而是讓她的資料絕對不會超過最長 *x* 秒的時間就會過時。 當然，對於靜態資料， *x* 可以擴充至 web 應用程式的存留期，如同在 [應用程式啟動時](caching-data-at-application-startup-vb.md) 快取資料中所做的檢查。

快取資料庫資料時，通常會選擇以時間為基礎的到期日，但通常是無法充分利用的解決方案。 在理想情況下，資料庫資料會保持快取狀態，直到資料庫中的基礎資料經過修改為止。只有如此才會收回快取。 這種方法可將快取的效能優勢最大化，並將過時資料的持續時間降到最低。 不過，為了享受這些優點，必須備妥一些系統，知道基礎資料庫資料何時經過修改，並從快取中收回對應的專案。 在 ASP.NET 2.0 之前，網頁開發人員必須負責執行此系統。

ASP.NET 2.0 會提供[ `SqlCacheDependency` 類別](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)和必要的基礎結構，以判斷資料庫中發生變更的時間，以便收回對應的快取專案。 有兩種技術可判斷基礎資料的變更時間：通知和輪詢。 在討論通知和輪詢之間的差異之後，我們會建立支援輪詢所需的基礎結構，然後探索如何 `SqlCacheDependency` 在宣告式和以程式設計的案例中使用類別。

## <a name="understanding-notification-and-polling"></a>瞭解通知和輪詢

有兩種方法可用來判斷資料庫中的資料何時修改：通知和輪詢。 使用通知時，資料庫會在上次執行查詢之後變更特定查詢的結果時，自動警示 ASP.NET 執行時間，此時會收回與查詢相關聯的快取專案。 使用輪詢時，資料庫伺服器會維護上次更新特定資料表的相關資訊。 ASP.NET 執行時間會定期輪詢資料庫，以檢查在快取中輸入資料表之後有哪些變更。 已修改資料的資料表會收回其相關聯的快取專案。

通知選項需要比輪詢更少的設定，而且更細微，因為它會追蹤查詢層級（而不是資料表層級）的變更。 可惜的是，通知只適用于 Microsoft SQL Server 2005 的完整版本，也就是) 的非 Express 版 (。 不過，輪詢選項可用於從7.0 到2005的所有 Microsoft SQL Server 版本。 由於這些教學課程使用 Express 版的 SQL Server 2005，因此我們將著重于設定和使用輪詢選項。 請參閱本教學課程結尾的進一步閱讀章節，以取得 SQL Server 2005 s 通知功能的進一步資源。

使用輪詢時，資料庫必須設定為包含名為的資料表， `AspNet_SqlCacheTablesForChangeNotification` 該資料表具有三個數據行： `tableName` 、 `notificationCreated` 和 `changeId` 。 此資料表包含每個資料表的資料列，該資料列有可能需要在 web 應用程式的 SQL 快取相依性中使用的資料。 `tableName`資料行會指定資料表的名稱， `notificationCreated` 並指出資料列新增至資料表的日期和時間。 資料 `changeId` 行的型別為 `int` ，而且初始值為0。 它的值會隨著資料表的每個修改而遞增。

除了 `AspNet_SqlCacheTablesForChangeNotification` 資料表以外，資料庫也需要在可能出現在 SQL 快取相依性中的每個資料表上包含觸發程式。 每當插入、更新或刪除資料列，並在中遞增資料表的值時，就會執行這些觸發程式 `changeId` `AspNet_SqlCacheTablesForChangeNotification` 。

使用物件來快取資料時，ASP.NET 執行時間會追蹤資料表的目前 `changeId` `SqlCacheDependency` 。 系統會定期檢查資料庫，而且與 `SqlCacheDependency` `changeId` 資料庫中的值不同的任何物件都會被收回，因為不同的 `changeId` 值表示自快取資料以來，資料表已經有變更。

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>步驟1：探索 `aspnet_regsql.exe` 命令列程式

使用輪詢方法時，必須將資料庫設定為包含上述基礎結構：預先定義的資料表 (`AspNet_SqlCacheTablesForChangeNotification`) 、一些預存程式，以及每個資料表上的觸發程式，這些資料表可用於 web 應用程式中的 SQL 快取相依性。 您可以透過命令列程式 `aspnet_regsql.exe` （可在資料夾中找到）來建立這些資料表、預存程式和觸發程式 `$WINDOWS$\Microsoft.NET\Framework\version` 。 若要建立 `AspNet_SqlCacheTablesForChangeNotification` 資料表和相關聯的預存程式，請從命令列執行下列命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> 若要執行這些命令，指定的資料庫登入必須在 [`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx) 和 [`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx) 角色中。 若要檢查命令列程式傳送至資料庫的 T-sql `aspnet_regsql.exe` ，請參閱 [此 blog 專案](http://scottonwriting.net/sowblog/posts/10709.aspx)。

例如，若要將輪詢的基礎結構新增至 `pubs` 使用 Windows 驗證命名的資料庫伺服器上的 Microsoft SQL Server 資料庫 `ScottsServer` ，請流覽至適當的目錄，然後從命令列輸入：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

加入資料庫層級基礎結構之後，我們必須將觸發程式新增至將用於 SQL 快取相依性的資料表。 再次使用 `aspnet_regsql.exe` 命令列程式，但使用參數指定資料表名稱， `-t` 而不使用 `-ed` 參數使用 `-et` ，如下所示：

[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

若要將觸發程式加入 `authors` `titles` 資料庫上的和資料表 `pubs` `ScottsServer` ，請使用：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

針對此教學課程，請將觸發程式加入至 `Products` 、 `Categories` 和 `Suppliers` 資料表。 我們將在步驟3中探討特定的命令列語法。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>步驟2：參考中的 Microsoft SQL Server 2005 Express Edition 資料庫`App_Data`

`aspnet_regsql.exe`命令列程式需要資料庫和伺服器名稱，才能新增必要的輪詢基礎結構。 但是位於資料夾中的 Microsoft SQL Server 2005 Express 資料庫的資料庫和伺服器名稱是什麼 `App_Data` ？ 我認為最簡單的方法就是將資料庫附加至 `localhost\SQLExpress` 資料庫實例，然後使用 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)重新命名資料，而不需要探索資料庫和伺服器名稱。 如果您的電腦上已安裝 SQL Server 2005 的其中一個完整版本，則您可能已經在電腦上安裝 SQL Server Management Studio。 如果您只有 Express edition，可以下載免費的 [Microsoft SQL Server Management Studio Express 版](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

從關閉 Visual Studio 開始。 接著，開啟 SQL Server Management Studio，然後選擇 `localhost\SQLExpress` 使用 Windows 驗證連接到伺服器。

![附加至 localhost\SQLExpress 伺服器](using-sql-cache-dependencies-vb/_static/image1.gif)

**圖 1**：附加至 `localhost\SQLExpress` 伺服器

連接到伺服器之後，Management Studio 將會顯示伺服器，並具有資料庫、安全性等的子資料夾。 以滑鼠右鍵按一下 [資料庫] 資料夾，然後選擇 [附加] 選項。 這會顯示 [附加資料庫] 對話方塊 (請參閱 [圖 2]) 。 按一下 [加入] 按鈕，然後選取 `NORTHWND.MDF` web 應用程式資料夾中的 [資料庫] 資料夾 `App_Data` 。

[![附加 NORTHWND.MDF 檔。App_Data 資料夾中的 MDF 資料庫](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**圖 2**： `NORTHWND.MDF` 從資料夾附加資料庫 `App_Data` ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image2.png)) 

這會將資料庫加入至 [資料庫] 資料夾。 資料庫名稱可能是資料庫檔案的完整路徑，或前面加上 [GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)的完整路徑。 若要避免在使用 aspnetregsql.exe 命令列工具時必須輸入這個冗長的資料庫名稱 \_ ，請在剛剛附加的資料庫上按一下滑鼠右鍵，然後選擇 [重新命名]，將資料庫重新命名為更容易使用的名稱。 我已將資料庫重新命名為 DataTutorials。

![將附加的資料庫重新命名為更易記的名稱](using-sql-cache-dependencies-vb/_static/image3.gif)

**圖 3**：將附加的資料庫重新命名為更易記的名稱

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>步驟3：將輪詢基礎結構新增至 Northwind 資料庫

既然我們已 `NORTHWND.MDF` 從資料夾附加資料庫，就可以 `App_Data` 開始加入輪詢基礎結構。 假設您已將資料庫重新命名為 DataTutorials，請執行下列四個命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

執行這四個命令之後，以滑鼠右鍵按一下 Management Studio 中的資料庫名稱，移至 [工作] 子功能表，然後選擇 [卸離]。 然後關閉 Management Studio 然後重新開啟 Visual Studio。

一旦 Visual Studio 重新開啟後，請透過伺服器總管向內切入資料庫。 請注意，新的資料表 (`AspNet_SqlCacheTablesForChangeNotification`) 、新的預存程式，以及 `Products` 、 `Categories` 和資料表上的觸發程式 `Suppliers` 。

![資料庫現在包含必要的輪詢基礎結構](using-sql-cache-dependencies-vb/_static/image4.gif)

**圖 4**：資料庫現在包含必要的輪詢基礎結構

## <a name="step-4-configuring-the-polling-service"></a>步驟4：設定輪詢服務

在資料庫中建立所需的資料表、觸發程式和預存程式之後，最後一個步驟是設定輪詢服務，這是藉 `Web.config` 由指定要使用的資料庫和輪詢頻率（以毫秒為單位）來完成。 下列標記會每秒輪詢一次 Northwind 資料庫。

[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

專案 `name` 中的值 `<add>` ( NorthwindDB ) 將人們可讀取的名稱與特定的資料庫產生關聯。 使用 SQL 快取相依性時，我們必須參考這裡定義的資料庫名稱，以及快取資料所依據的資料表。 我們將瞭解如何使用類別，以程式設計方式將 SQL 快取相依性 `SqlCacheDependency` 與步驟6中的快取資料產生關聯。

一旦建立 SQL 快取相依性之後，輪詢系統將會每毫秒連接至元素中定義的資料庫， `<databases>` `pollTime` 並執行 `AspNet_SqlCachePollingStoredProcedure` 預存程式。 這個預存程式（使用命令列工具在步驟3中新增 `aspnet_regsql.exe` ）-會傳回 `tableName` `changeId` 中每一筆記錄的和值 `AspNet_SqlCacheTablesForChangeNotification` 。 過期的 SQL 快取相依性會從快取中收回。

此 `pollTime` 設定會導致效能與資料過期之間的取捨。 較小的 `pollTime` 值會增加對資料庫的要求數目，但會更快速地從快取中收回過時的資料。 較大的 `pollTime` 值會減少資料庫要求的數目，但會增加後端資料變更和收回相關快取專案之間的延遲。 幸運的是，資料庫要求正在執行簡單的預存程式，而該預存程式只會從簡單的輕量資料表傳回幾個資料列。 但是，請使用不同的值進行實驗， `pollTime` 以找出應用程式的資料庫存取和資料過期之間的理想平衡。 允許的最小 `pollTime` 值是500。

> [!NOTE]
> 上述範例 `pollTime` 會在元素中提供單一值 `<sqlCacheDependency>` ，但您可以選擇性地在 `pollTime` 元素中指定值 `<add>` 。 如果您指定了多個資料庫，而且想要自訂每個資料庫的輪詢頻率，這就很有用。

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>步驟5：以宣告方式使用 SQL 快取相依性

在步驟1到4中，我們探討了如何設定所需的資料庫基礎結構，以及如何設定輪詢系統。 有了這個基礎結構之後，我們就可以使用程式設計方式或宣告式技術，將專案新增至資料快取，以及相關聯的 SQL 快取相依性。 在此步驟中，我們將探討如何以宣告方式使用 SQL 快取相依性。 在步驟6中，我們將探討以程式設計的方法。

[使用 objectdatasource](caching-data-with-the-objectdatasource-vb.md)教學課程的快取資料會探索 ObjectDataSource 的宣告式快取功能。 藉由將 `EnableCaching` 屬性設定為，並將屬性設定 `True` `CacheDuration` 為某個時間間隔，ObjectDataSource 將會自動快取在指定間隔內從其基礎物件傳回的資料。 ObjectDataSource 也可以使用一或多個 SQL 快取相依性。

若要示範如何以宣告方式使用 SQL 快取相依性，請開啟 `SqlCacheDependencies.aspx` 資料夾中的頁面， `Caching` 然後從 [工具箱] 將 GridView 拖曳至設計工具。 將 GridView 設定 `ID` 為 `ProductsDeclarative` ，並從其智慧標籤選擇將其系結至名為的新 ObjectDataSource `ProductsDataSourceDeclarative` 。

[![建立名為 ProductsDataSourceDeclarative 的新 ObjectDataSource](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**圖 5**：建立名為 `ProductsDataSourceDeclarative` ([按一下以查看完整大小影像](using-sql-cache-dependencies-vb/_static/image4.png)) 的新 ObjectDataSource

將 ObjectDataSource 設定為使用 `ProductsBLL` 類別，並將 [選取] 索引標籤中的下拉式清單設定為 `GetProducts()` 。 在 [更新] 索引標籤中，選擇 `UpdateProduct` 具有三個輸入參數的多載- `productName` 、 `unitPrice` 和 `productID` 。 在 [插入] 和 [刪除] 索引標籤中，將下拉式清單設定為 [無])  (。

[![使用 UpdateProduct 多載搭配三個輸入參數](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**圖 6**：搭配三個輸入參數使用 UpdateProduct 多載 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image6.png)) 

[![將下拉式清單設定為 [插入] 和 [刪除] 索引標籤 ([無]) ](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**圖 7**：將下拉式清單設定為 [插入] 和 [刪除] 索引標籤 ([無])  ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image8.png)) 

完成設定資料來源嚮導之後，Visual Studio 將會在 GridView 中為每個資料欄位建立 BoundFields 和 CheckBoxFields。 移除所有欄位 `ProductName` ，但、 `CategoryName` 和 `UnitPrice` ，並依您的需要將這些欄位格式化。 從 GridView 的智慧標籤，勾選 [啟用分頁]、[啟用排序] 和 [啟用編輯] 核取方塊。 Visual Studio 會將 ObjectDataSource s `OldValuesParameterFormatString` 屬性設為 `original_{0}` 。 為了讓 GridView 的編輯功能正常運作，請從宣告式語法完全移除此屬性，或將它設回其預設值 `{0}` 。

最後，在 GridView 上方新增 Label Web 控制項，並將其 `ID` 屬性設定為 `ODSEvents` ，並將其 `EnableViewState` 屬性設定為 `False` 。 進行這些變更之後，您的頁面宣告式標記看起來應該會如下所示。 請注意，我對 GridView 欄位進行了許多美觀的自訂，而這些欄位並非示範 SQL 快取相依性功能的必要專案。

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

接下來，為 ObjectDataSource s 事件建立事件處理常式 `Selecting` ，並在其中新增下列程式碼：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

回想一下，ObjectDataSource s `Selecting` 事件只會在從其基礎物件中取出資料時引發。 如果 ObjectDataSource 從自己的快取存取資料，則不會引發此事件。

現在，請透過瀏覽器造訪此頁面。 由於我們尚未執行任何快取，因此每次您分頁、排序或編輯格線時，頁面應該會顯示 [正在引發的事件] 文字（如 [圖 8] 所示）。

[![每次 GridView 進行分頁、編輯或排序時，會引發選取事件的 ObjectDataSource](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**圖 8**： `Selecting` 每次 GridView 進行分頁、編輯或排序 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image10.png) 時，都會引發 ObjectDataSource s 事件) 

如我們在 [使用 ObjectDataSource](caching-data-with-the-objectdatasource-vb.md) 教學課程快取資料中所見，將 `EnableCaching` 屬性設為， `True` 會導致 ObjectDataSource 在其屬性指定的持續時間內快取其資料 `CacheDuration` 。 ObjectDataSource 也有一個屬性，此[ `SqlCacheDependency` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)會使用模式將一或多個 SQL 快取相依性新增至快取的資料：

[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

其中 *databaseName* 是中專案的屬性所指定的資料庫名稱 `name` `<add>` `Web.config` ，而 *tableName* 是資料庫資料表的名稱。 例如，若要建立根據 Northwind s 資料表的 SQL 快取相依性無限快取資料的 ObjectDataSource `Products` ，請將 objectdatasource s `EnableCaching` 屬性設為 `True` ，並將其 `SqlCacheDependency` 屬性設定為 NorthwindDB： Products。

> [!NOTE]
> 您可以使用 SQL 快取相依性 *和* 以時間為基礎的到期，將設定 `EnableCaching` 為 `True` 、 `CacheDuration` 時間間隔，以及 `SqlCacheDependency` 資料庫和資料表名稱 (s) 。 當達到以時間為基礎的到期時，或當輪詢系統注意到基礎資料庫資料已變更（以先發生者為准）時，ObjectDataSource 會收回其資料。

中的 GridView `SqlCacheDependencies.aspx` 會顯示來自兩個數據表的資料 `Products` ，而 `Categories` (product s `CategoryName` 欄位則是 `JOIN` 透過 `Categories`) 來抓取。 因此，我們想要指定兩個 SQL 快取相依性： NorthwindDB： Products;NorthwindDB：分類。

[![設定 ObjectDataSource 以支援使用 SQL 快取相依性的產品和類別進行快取](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**圖 9**：設定 ObjectDataSource 以支援在上使用 SQL 快取相依性的快取 `Products` ， `Categories` ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image12.png)) 

設定 ObjectDataSource 以支援快取之後，請透過瀏覽器重新流覽頁面。 同樣地，所引發的文字「選取事件」應該會出現在第一頁流覽，但在分頁、排序或按一下 [編輯] 或 [取消] 按鈕時應該會消失。 這是因為在將資料載入 ObjectDataSource 快取之後，它會一直留在那裡，直到 `Products` 或 `Categories` 資料表遭到修改或資料透過 GridView 更新為止。

逐頁查看方格並指出缺少「選取事件引發文字」之後，請開啟新的瀏覽器視窗，並流覽至 [編輯]、[插入] 和 [刪除] 區段中的基本教學課程， (`~/EditInsertDelete/Basics.aspx`) 。 更新產品的名稱或價格。 然後，從到第一個瀏覽器視窗，查看不同的資料頁面、排序方格，或按一下資料列的 [編輯] 按鈕。 這次，[選取引發的事件] 應該會再次出現，因為基礎資料庫資料已修改 (請參閱 [圖 10]) 。 如果文字未出現，請稍候片刻，然後再試一次。 請記住，輪詢服務會 `Products` 每毫秒檢查資料表的變更 `pollTime` ，因此在更新基礎資料和收回快取資料之間會有延遲。

[![修改 Products 資料表收回快取的產品資料](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**圖 10**：修改 Products 資料表收回快取的產品資料 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image14.png)) 

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>步驟6：以程式設計方式使用 `SqlCacheDependency` 類別

架構教學課程中的快取 [資料](caching-data-in-the-architecture-vb.md) ，探討了在架構中使用不同快取層的優點，而不是將快取與 ObjectDataSource 緊密結合在一起。 在該教學課程中，我們建立了一個 `ProductsCL` 類別來示範如何以程式設計方式使用資料快取。 若要在快取層中使用 SQL 快取相依性，請使用 `SqlCacheDependency` 類別。

使用輪詢系統時， `SqlCacheDependency` 物件必須與特定的資料庫和資料表配對相關聯。 例如，下列程式碼會建立以 `SqlCacheDependency` Northwind 資料庫資料表為基礎的物件 `Products` ：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

S 函數的兩個輸入參數 `SqlCacheDependency` 分別是資料庫和資料表名稱。 如同使用 ObjectDataSource s `SqlCacheDependency` 屬性，所使用的資料庫名稱與中專案的屬性所指定的值相同 `name` `<add>` `Web.config` 。 資料表名稱是資料庫資料表的實際名稱。

若要將 `SqlCacheDependency` 與加入至資料快取的專案產生關聯，請使用可接受相依性的其中一個方法多載 `Insert` 。 下列程式碼會將 *值* 加入至資料快取，以達無限期，但會將它與資料表上的相關聯 `SqlCacheDependency` `Products` 。 簡單來說， *值* 將會保留在快取中，直到它因為記憶體限制而收回，或因為輪詢系統偵測到 `Products` 資料表自快取以來已經變更。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

快取層 `ProductsCL` 級的類別目前 `Products` 使用以時間為基礎的到期時間為60秒，來快取資料表中的資料。 讓我們更新此類別，使其改為使用 SQL 快取相依性。 `ProductsCL` `AddCacheItem` 負責將資料加入至快取的類別 s 方法，目前包含下列程式碼：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

更新此程式碼以使用 `SqlCacheDependency` 物件，而不是快取相依性 `MasterCacheKeyArray` ：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

若要測試此功能，請將 GridView 新增至現有 GridView 底下的頁面 `ProductsDeclarative` 。 將這個新的 GridView 設定 `ID` 為， `ProductsProgrammatic` 並在其智慧標籤中，將它系結至名為的新 ObjectDataSource `ProductsDataSourceProgrammatic` 。 將 ObjectDataSource 設定為使用 `ProductsCL` 類別，分別將 [選取和更新] 索引標籤中的下拉式清單設定為 `GetProducts` 和 `UpdateProduct` 。

[![設定 ObjectDataSource 以使用 ProductsCL 類別](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**圖 11**：設定 ObjectDataSource 以使用 `ProductsCL` 類別 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image16.png)) 

[![從 [選取索引標籤] 下拉式清單中選取 GetProducts 方法](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**圖 12**： `GetProducts` 從 [選取索引標籤] 下拉式清單選取方法 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image18.png)) 

[![從 [更新] 索引標籤的下拉式清單中選擇 UpdateProduct 方法](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**圖 13**：從 [更新] 索引標籤的下拉式清單中選擇 [UpdateProduct] 方法 ([按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image20.png)) 

完成設定資料來源嚮導之後，Visual Studio 將會在 GridView 中為每個資料欄位建立 BoundFields 和 CheckBoxFields。 就像是將第一個 GridView 加入至此頁面一樣，請移除所有欄位，包括 `ProductName` 、 `CategoryName` 和，並依 `UnitPrice` 您的需要將這些欄位格式化。 從 GridView 的智慧標籤，勾選 [啟用分頁]、[啟用排序] 和 [啟用編輯] 核取方塊。 和 objectdatasource 一樣 `ProductsDataSourceDeclarative` ，Visual Studio 會將 `ProductsDataSourceProgrammatic` objectdatasource s 屬性設 `OldValuesParameterFormatString` 為 `original_{0}` 。 為了讓 GridView 的編輯功能正常運作，請將此屬性設回 (， `{0}` 或從宣告式語法中移除完全) 的屬性指派。

完成這些工作之後，產生的 GridView 和 ObjectDataSource 宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

若要測試快取層中的 SQL 快取相依性， `ProductCL` 請在類別 s 方法中設定中斷點 `AddCacheItem` ，然後開始進行調試。 當您第一 `SqlCacheDependencies.aspx` 次造訪時，應該會叫用中斷點，因為第一次要求資料並放入快取中。 接下來，移至 GridView 中的另一個頁面，或排序其中一個資料行。 這會導致 GridView 重新查詢其資料，但是應該在快取中找到資料，因為 `Products` 資料庫資料表尚未經過修改。 如果在快取中找不到資料，請確定您的電腦上有足夠的記憶體可用，然後再試一次。

逐頁查看 GridView 的幾個頁面之後，請開啟第二個瀏覽器視窗，並流覽至 [編輯]、[插入] 和 [刪除] 區段中的基本教學課程 (`~/EditInsertDelete/Basics.aspx`) 。 更新 Products 資料表中的記錄，然後從第一個瀏覽器視窗中，查看新頁面或按一下其中一個排序標頭。

在此案例中，您會看到兩個專案的其中一種：可能會叫用中斷點，表示快取的資料因為資料庫中的變更而收回;或者，將不會叫用中斷點，這表示 `SqlCacheDependencies.aspx` 現在會顯示過時的資料。 如果未叫用中斷點，很可能是因為輪詢服務自從資料變更後尚未引發。 請記住，輪詢服務會 `Products` 每毫秒檢查資料表的變更 `pollTime` ，因此在更新基礎資料和收回快取資料之間會有延遲。

> [!NOTE]
> 當您在中透過 GridView 編輯其中一項產品時，可能會出現此延遲 `SqlCacheDependencies.aspx` 。 在快取架構教學課程中的 [資料](caching-data-in-the-architecture-vb.md) 中，我們新增了快取相依性， `MasterCacheKeyArray` 以確保透過 `ProductsCL` 類別 s 方法編輯的資料已從快取 `UpdateProduct` 中收回。 不過，我們會在此步驟稍早修改方法時取代這個快取相依性 `AddCacheItem` ，因此，在 `ProductsCL` 輪詢系統記下資料表的變更之前，類別將會繼續顯示快取的資料 `Products` 。 我們將瞭解如何 `MasterCacheKeyArray` 在步驟7中重新引入快取相依性。

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>步驟7：建立多個相依性與快取專案的關聯

回想一下，快取相依性 `MasterCacheKeyArray` 是用來確保 *所有* 產品相關資料在更新時都會從快取中收回。 例如，方法會快取 `GetProductsByCategoryID(categoryID)` `ProductsDataTables` 每個唯一 *類別類別* 值的實例。 如果已收回其中一個物件，則快 `MasterCacheKeyArray` 取相依性可確保也會移除其他物件。 如果沒有這項快取相依性，當快取的資料遭到修改時，可能會有其他快取的產品資料已過期。 因此，在使用 SQL 快取相依性時，我們必須維護快取相依性 `MasterCacheKeyArray` 。 但是，資料快取 s `Insert` 方法只允許單一相依性物件。

此外，在使用 SQL 快取相依性時，可能需要將多個資料庫資料表關聯為相依性。 例如，在類別中快取的會 `ProductsDataTable` `ProductsCL` 包含每項產品的類別目錄和供應商名稱，但是此 `AddCacheItem` 方法只會使用的相依性 `Products` 。 在此情況下，如果使用者更新了類別或供應商的名稱，快取的產品資料將會保留在快取中，而且會過期。 因此，我們想要讓快取的產品資料不只相依于 `Products` 資料表，也是 `Categories` 和 `Suppliers` 資料表。

[ `AggregateCacheDependency` 類別](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)提供一種方法，讓多個相依性與快取專案產生關聯。 首先，建立 `AggregateCacheDependency` 實例。 接下來，使用 s 方法新增相依性 `AggregateCacheDependency` 集合 `Add` 。 之後將專案插入資料快取時，就會傳入 `AggregateCacheDependency` 實例。 當 *任何* 實例的相依性 `AggregateCacheDependency` 變更時，就會收回快取的專案。

以下顯示類別 s 方法的更新程式碼 `ProductsCL` `AddCacheItem` 。 方法會建立快取相依性 `MasterCacheKeyArray` `SqlCacheDependency` ，以及 `Products` 、 `Categories` 和資料表的物件 `Suppliers` 。 這些全都合併成一個 `AggregateCacheDependency` 名為的物件 `aggregateDependencies` ，接著會傳遞至 `Insert` 方法。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

測試這個新的程式碼。現在 `Products` ，、或資料表的變更會導致快取 `Categories` `Suppliers` 的資料被收回。 此外，在 `ProductsCL` `UpdateProduct` 透過 GridView 編輯產品時所呼叫的類別 s 方法會收回快取相依性 `MasterCacheKeyArray` ，這會導致快取的 `ProductsDataTable` 被收回，並在下一個要求時重新抓取資料。

> [!NOTE]
> SQL 快取相依性也可以與 [輸出](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)快取搭配使用。 如需這項功能的示範，請參閱：搭配 [SQL Server 使用 ASP.NET 輸出](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)快取。

## <a name="summary"></a>摘要

快取資料庫資料時，資料在理想情況下會保留在快取中，直到在資料庫中進行修改為止。 使用 ASP.NET 2.0，可以在宣告式和程式設計的案例中建立和使用 SQL 快取相依性。 這種方法的挑戰之一，就是探索資料何時經過修改。 完整版的 Microsoft SQL Server 2005 提供通知功能，可在查詢結果變更時警示應用程式。 若為 SQL Server 2005 與舊版 SQL Server 的 Express Edition，則必須改用輪詢系統。 幸運的是，設定必要的輪詢基礎結構相當簡單。

快樂程式設計！

## <a name="further-reading"></a>深入閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [在 Microsoft SQL Server 2005 中使用查詢通知](https://msdn.microsoft.com/library/ms175110.aspx)
- [建立查詢通知](https://msdn.microsoft.com/library/ms188669.aspx)
- [使用類別在 ASP.NET 中快取 `SqlCacheDependency`](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 註冊工具 (`aspnet_regsql.exe`) ](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [總覽 `SqlCacheDependency`](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者是七個 ASP/ASP. NET 書籍和創辦人 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 [*在24小時內 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 您可以在此聯繫[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog （可在中找到） [http://ScottOnWriting.NET](http://ScottOnWriting.NET) 。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核者是 Marko Rangel、Teresa Murphy 和 Hilton Giesenow。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在這裡放置一行[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [[上一步]](caching-data-at-application-startup-vb.md)
