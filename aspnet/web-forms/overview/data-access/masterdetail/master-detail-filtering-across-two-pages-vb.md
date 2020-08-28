---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: 跨兩個頁面的主要/詳細資料篩選 (VB) |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列都會包含視圖 .。。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 0e30d47a565c3b6cb9f647d54d47c10a418762f4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044970"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>跨兩個頁面進行主要/詳細資料篩選 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) 或 [下載 PDF](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> 在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列都會包含 [View Products] 連結，按一下此連結會將使用者帶到列出所選供應商產品的個別頁面。

## <a name="introduction"></a>簡介

在先前的兩個教學課程中，我們已瞭解如何使用 Dropdownlist 進行顯示主要/詳細資料包表，以顯示「主要」記錄和 [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) 或 [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) 控制項來顯示「詳細資料」。 主要/詳細資料包表使用的另一個常見模式是在一個網頁上擁有主要記錄，並在另一個網頁上顯示詳細資料。 論壇網站（如 [ASP.NET 論壇](https://forums.asp.net/)）是此模式實務的絕佳範例。 ASP.NET 論壇由各種論壇組成消費者入門、Web Form、資料展示控制項等等。 每個論壇都是由許多執行緒組成，而且每個執行緒都是由數個貼文所組成。 在 ASP.NET 論壇首頁上，會列出論壇。 按一下論壇 whisks 您的 `ShowForum.aspx` 頁面，其中會列出該論壇的往來文章。 同樣地，按一下執行緒會帶您前往 `ShowPost.aspx` ，以顯示已按下之執行緒的貼文。

在本教學課程中，我們將使用 GridView 來列出資料庫中的供應商，以執行這種模式。 GridView 中的每個供應商資料列都會包含 [View Products] 連結，按一下此連結會將使用者帶到列出所選供應商產品的個別頁面。

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>步驟1：將 `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 頁面新增至 `Filtering` 資料夾

當您在第三個教學課程中定義頁面配置時 `BasicReporting` ，在、 `Filtering` 和資料夾中新增了數個「入門」頁面 `CustomFormatting` 。 不過，我們在該時間尚未新增此教學課程的起始頁，所以請花點時間將兩個新的頁面新增至 `Filtering` 資料夾： `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 。 `SupplierListMaster.aspx` 會列出供應商)  (的「主要」記錄，同時 `ProductsForSupplierDetails.aspx` 會顯示所選供應商的產品。

建立這兩個新的頁面時，請務必將它們與 `Site.master` 主版頁面建立關聯。

![將 SupplierListMaster .aspx 和 ProductsForSupplierDetails .aspx 頁面新增至篩選資料夾](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**圖 1**：將 `SupplierListMaster.aspx` 和 `ProductsForSupplierDetails.aspx` 頁面新增至 `Filtering` 資料夾

此外，將新頁面新增至專案時，請務必適當地更新網站地圖檔 `Web.sitemap` 。 本教學課程只會 `SupplierListMaster.aspx` 使用下列 XML 內容做為篩選報表元素的子系，將頁面新增至網站地圖 `<siteMapNode>` ：

[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> 您可以使用 [Allen](http://odetocode.com/Blogs/scott/)的免費 Visual Studio [網站地圖宏](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)，在新增 ASP.NET 網頁時，協助自動化更新網站地圖檔案的程式。

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>步驟2：在中顯示供應商清單`SupplierListMaster.aspx`

`SupplierListMaster.aspx` `ProductsForSupplierDetails.aspx` 建立和頁面之後，下一步是在中建立供應商的 GridView `SupplierListMaster.aspx` 。 將 GridView 加入至頁面，並將它系結至新的 ObjectDataSource。 這個 ObjectDataSource 應該使用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法來傳回所有供應商。

[![選取 SuppliersBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**圖 2**：選取 `SuppliersBLL` 類別 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image4.png)) 

[![將 ObjectDataSource 設定為使用 GetSuppliers ( # A1 方法](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**圖 3**：設定 ObjectDataSource 以使用 `GetSuppliers()` 方法 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image7.png)) 

我們必須在每個 GridView 資料列中包含標題為 View Products 的連結，當按下時，就會將選取的資料 `ProductsForSupplierDetails.aspx` 列 `SupplierID` 值透過 querystring 傳遞給使用者。 例如，如果使用者按一下東京貿易供應商的 [View Products] 連結 (`SupplierID` 值為 4) ，則應該將它們傳送給 `ProductsForSupplierDetails.aspx?SupplierID=4` 。

若要完成此動作，請將 [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) 新增至 gridview，以將超連結加入至每個 gridview 資料列。 首先，從 GridView 的智慧標籤按一下 [編輯資料行] 連結。 接下來，從左上方的清單中選取 HyperLinkField，然後按一下 [新增]，將 HyperLinkField 包含在 GridView 的欄位清單中。

[![將 HyperLinkField 新增至 GridView](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**圖 4**：將 HyperLinkField 新增至 GridView ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image10.png)) 

HyperLinkField 可以設定為使用每個 GridView 資料列中連結的相同文字或 URL 值，也可以將這些值以系結至每個特定資料列的資料值為基礎。 若要在所有資料列上指定靜態值，請使用 HyperLinkField 的 `Text` 或 `NavigateUrl` 屬性。 由於我們希望所有資料列的連結文字都相同，因此請設定 HyperLinkField 的 `Text` 屬性來查看產品。

[![設定 HyperLinkField 的 Text 屬性來查看產品](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**圖 5**：設定 HyperLinkField 的 `Text` 屬性以查看產品 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image13.png)) 

若要將文字或 URL 值設定為根據系結至 GridView 資料列的基礎資料，請在或屬性中指定要從中提取文字或 URL 值的資料 `DataTextField` 欄位 `DataNavigateUrlFields` 。 `DataTextField` 只能設定為單一資料欄位; `DataNavigateUrlFields`不過，可以設定為以逗號分隔的資料欄位清單。 我們經常需要以目前資料列的資料欄值和一些靜態標記的組合作為文字或 URL。 例如，在本教學課程中，我們想要將 HyperLinkField 連結的 URL 設為 `ProductsForSupplierDetails.aspx?SupplierID=supplierID` ，其中 *`supplierID`* 是每個 GridView 的 row's `SupplierID` 值。 請注意，在這裡需要靜態和資料驅動值： `ProductsForSupplierDetails.aspx?SupplierID=` 連結 URL 的部分是靜態的，而 *`supplierID`* 部分是資料驅動的，因為其值是每個資料列的專屬 `SupplierID` 值。

若要表示靜態和資料驅動值的組合，請使用 `DataTextFormatString` 和 `DataNavigateUrlFormatString` 屬性。 在這些屬性中，視需要輸入靜態標記，然後使用 `{0}` 您想要 `DataTextField` 顯示或屬性中所指定之欄位值的標記 `DataNavigateUrlFields` 。 如果 `DataNavigateUrlFields` 屬性有多個指定的欄位 `{0}` ，請使用您想要插入的第一個域值、 `{1}` 第二個域值等等。

將此屬性套用到教學課程之後，我們必須將 `DataNavigateUrlFields` 屬性設定為 `SupplierID` ，因為這是需要針對每個資料列自訂其值的資料欄位，以及的 `DataNavigateUrlFormatString` 屬性 `ProductsForSupplierDetails.aspx?SupplierID={0}` 。

[![將 HyperLinkField 設定為根據建立商，包含適當的連結 URL](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**圖 6**：根據 `SupplierID` ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image16.png) ，將 HyperLinkField 設定為包含適當的連結 URL) 

新增 HyperLinkField 之後，您可以隨意自訂和重新排序 GridView 的欄位。 在我進行一些次要欄位層級自訂之後，下列標記會顯示 GridView。

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

花點時間 `SupplierListMaster.aspx` 透過瀏覽器來查看頁面。 如 [圖 7] 所示，此頁面目前列出所有供應商，包括 [View Products] 連結。 按一下 [View Products] 連結將會帶您前往 `ProductsForSupplierDetails.aspx` ，並 `SupplierID` 在查詢字串中傳遞供應商。

[![每個供應商資料列都包含 View Products 連結](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**圖 7**：每個供應商資料列都包含 [view Products] 連結 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image19.png)) 

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>步驟3：列出供應商的產品`ProductsForSupplierDetails.aspx`

此時 `SupplierListMaster.aspx` 頁面會將使用者 `ProductsForSupplierDetails.aspx` 傳送至，並 `SupplierID` 在查詢字串中傳遞選取的供應商。 本教學課程的最後一個步驟是顯示 GridView 中的產品， `ProductsForSupplierDetails.aspx` 其 `SupplierID` 等於 `SupplierID` 透過 querystring 傳遞的。 若要完成這項工作 `ProductsForSupplierDetails.aspx` ，請使用名為的新 ObjectDataSource 控制項來叫用 `ProductsBySupplierDataSource` 類別中的方法，以在頁面中新增 GridView `GetProductsBySupplierID(supplierID)` `ProductsBLL` 。

[![加入名為 ProductsBySupplierDataSource 的新 ObjectDataSource](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**圖 8**：加入名為 `ProductsBySupplierDataSource` ([按一下以查看完整大小影像](master-detail-filtering-across-two-pages-vb/_static/image22.png)) 的新 ObjectDataSource

[![選取 ProductsBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**圖 9**：選取 `ProductsBLL` 類別 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image25.png)) 

[![讓 ObjectDataSource 叫用 GetProductsBySupplierID (的可) 方法](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**圖 10**：讓 ObjectDataSource 叫用 `GetProductsBySupplierID(supplierID)` 方法 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image28.png)) 

[設定資料來源] wizard 的最後一個步驟會要求我們提供 `GetProductsBySupplierID(supplierID)` 方法參數的來源 *`supplierID`* 。 若要使用 querystring 值，請將參數來源設定為 QueryString，然後輸入要在 QueryStringField 文字方塊中使用之 querystring 值的名稱 (`SupplierID`) 。

[![從擁有者的查詢字串值填入「值」參數值](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**圖 11**： *`supplierID`* 從 Querystring 值填入參數值 `SupplierID` ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image31.png)) 

就是這麼簡單！ 圖 12 `ProductsForSupplierDetails.aspx` 按一下中的 [東京商貿] 連結來顯示頁面 `SupplierListMaster.aspx` 。

[![東京商貿提供的產品會顯示](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**圖 12**：東京商貿提供的產品顯示 ([按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image34.png)) 

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>顯示供應商資訊`ProductsForSupplierDetails.aspx`

如 [圖 12] 所示，此 `ProductsForSupplierDetails.aspx` 頁面只會列出 `SupplierID` 查詢字串中指定的所提供的產品。 不過，直接傳送到此頁面的人並不知道 [圖 12] 顯示的是東京商貿的產品。 若要解決此情況，我們也可以在此頁面中顯示供應商資訊。

從在 products GridView 上方加入 FormView 開始。 建立名為的新 ObjectDataSource 控制項，其會叫用 `SuppliersDataSource` `SuppliersBLL` 類別的 `GetSupplierBySupplierID(supplierID)` 方法。

[![選取 SuppliersBLL 類別](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**圖 13**：選取 `SuppliersBLL` 類別 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image37.png)) 

[![讓 ObjectDataSource 叫用 GetSupplierBySupplierID (的可) 方法](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**圖 14**：讓 ObjectDataSource 叫用 `GetSupplierBySupplierID(supplierID)` 方法 ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image40.png)) 

使用時 `ProductsBySupplierDataSource` ，請將 *`supplierID`* querystring 值的值指派給參數 `SupplierID` 。

[![從擁有者的查詢字串值填入「值」參數值](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**圖 15**： *`supplierID`* 從 Querystring 值填入參數值 `SupplierID` ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image43.png)) 

當將 FormView 系結至設計檢視中的 ObjectDataSource 時，Visual Studio 會自動建立 FormView 的 `ItemTemplate` 、 `InsertItemTemplate` 和，並 `EditItemTemplate` 針對 ObjectDataSource 所傳回的每個資料欄位，建立標籤和 TextBox Web 控制項。 因為我們只想要顯示供應商資訊，所以您可以隨意移除 `InsertItemTemplate` 和 `EditItemTemplate` 。 接下來，編輯 ItemTemplate，讓它在專案中顯示供應商的公司名稱， `<h3>` 並在公司名稱下顯示位址、城市、國家/地區及電話號碼。 或者，您也可以手動設定 FormView `DataSourceID` 並建立 `ItemTemplate` 標記，就像我們在「[使用 ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)」教學課程中所做的一樣。

在這些編輯之後，FormView 的宣告式標記看起來應該會如下所示：

[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

[圖 16] 顯示 `ProductsForSupplierDetails.aspx` 內含上述供應商資訊之後頁面的螢幕擷取畫面。

[![產品清單包含供應商的相關摘要](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**圖 16**：產品清單包含供應商的相關摘要 ([按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image46.png)) 

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>對 UI 套用最後的修飾 `ProductsForSupplierDetails.aspx`

為了改善這份報表的使用者體驗，我們應該對頁面進行幾項新增 `ProductsForSupplierDetails.aspx` 。 目前，使用者可從 `ProductsForSupplierDetails.aspx` 頁面回到供應商清單的唯一方法，是按一下其瀏覽器的 [上一頁] 按鈕。 讓我們將超連結控制項新增至 `ProductsForSupplierDetails.aspx` 連結回的頁面 `SupplierListMaster.aspx` ，以提供另一種方法讓使用者返回主清單。

[![加入超連結控制項，讓使用者回到 SupplierListMaster .aspx](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**圖 17**：加入超連結控制項，讓使用者回到 `SupplierListMaster.aspx` ([按一下以查看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image49.png)) 

如果使用者按一下沒有任何產品之供應商的 [View Products] 連結，則 `ProductsBySupplierDataSource` ObjectDataSource `ProductsForSupplierDetails.aspx` 不會傳回任何結果。 系結至 ObjectDataSource 的 GridView 無法轉譯任何在使用者的瀏覽器頁面上產生空白區域的標記。 為了更清楚地與使用者溝通沒有與所選供應商相關聯的產品，我們可以將 GridView 的 `EmptyDataText` 屬性設定為我們想要在發生這種情況時顯示的訊息。 我已將此屬性設定為「此供應商未提供任何產品」

Northwinds 資料庫中的所有供應商預設都會提供至少一個產品。 不過，在本教學課程中，我已手動修改 `Products` 資料表，讓供應商 Escargots Nouveaux 不再與任何產品相關聯。 [圖 18] 顯示完成此變更之後 Escargots Nouveaux 的詳細資料頁面。

[![使用者會收到通知，表示供應商未提供任何產品](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**圖 18**：使用者會收到通知，指出供應商未提供任何產品 ([按一下以觀看完整大小的影像](master-detail-filtering-across-two-pages-vb/_static/image52.png)) 

## <a name="summary"></a>摘要

雖然主要/詳細資料包表可以在單一頁面上顯示主要和詳細記錄，但在許多網站中，它們會在兩個網頁之間分開。 在本教學課程中，我們探討了如何藉由在「主要」網頁的 GridView 中列出供應商，並在 [詳細資料] 頁面中列出相關聯的產品，來執行這類主/詳細資料包表。 主要網頁中的每個供應商資料列都包含一個連結，可連至資料列值所傳遞的詳細資料頁面 `SupplierID` 。 您可以使用 GridView 的 HyperLinkField 輕鬆地新增這類資料列特定的連結。

在 [詳細資料] 頁面中，藉由叫用類別的方法，來為指定的供應商取出這些產品 `ProductsBLL` `GetProductsBySupplierID(supplierID)` 。 *`supplierID`* 參數值是使用 querystring 做為參數來源，以宣告方式指定。 我們也探討了如何使用 FormView 在詳細資料頁面中顯示供應商的詳細資料。

[下一個教學](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)課程是主要/詳細資料包表上的最後一個教學課程。 我們將探討如何在 GridView 中顯示產品清單，其中每個資料列都有 [選取] 按鈕。 按一下 [選取] 按鈕，就會在相同頁面上的 DetailsView 控制項中顯示該產品的詳細資料。

快樂程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者是七個 ASP/ASP. NET 書籍和創辦人 of [4GuysFromRolla.com](http://www.4guysfromrolla.com)，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 [*在24小時內 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 您可以在此聯繫[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog （可在中找到） [http://ScottOnWriting.NET](http://ScottOnWriting.NET) 。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核 Hilton Giesenow。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在這裡放置一行[ mitchell@4GuysFromRolla.com 。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一個](master-detail-filtering-with-two-dropdownlists-vb.md) 
> [下一步](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
