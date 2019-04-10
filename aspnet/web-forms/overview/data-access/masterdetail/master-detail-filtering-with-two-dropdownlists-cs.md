---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
title: 主版/詳細篩選使用兩個 dropdownlist 進行 (C#) |Microsoft Docs
author: rick-anderson
description: 本教學課程中展開主要/詳細資料關聯性，加入第三個圖層，使用兩個 DropDownList 控制項來選取所需的父代和祖系記錄...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ac4b0d77-4816-4ded-afd0-88dab667aedd
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
msc.type: authoredcontent
ms.openlocfilehash: 03d0cd7e835b5526af60a21679260f849714c37e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59421286"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-c"></a>使用兩個 DropDownList 進行主要/詳細資料篩選 (C#)

藉由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_8_CS.exe)或[下載 PDF](master-detail-filtering-with-two-dropdownlists-cs/_static/datatutorial08cs1.pdf)

> 本教學課程會展開加入第三個圖層，使用兩個 DropDownList 控制項來選取所需的父代和祖系資料錄的主版/詳細資料關聯性。


## <a name="introduction"></a>簡介

在 [先前的教學課程](master-detail-filtering-with-a-dropdownlist-cs.md)我們檢查如何顯示簡單的主版/詳細資料報表中使用單一的 DropDownList 填入類別和 GridView，顯示屬於所選分類的產品。 此報表模式適用於顯示記錄有一對多關聯性，可以輕鬆地擴充，可針對包含多個的其中一個對多關聯性的案例。 例如，訂單輸入系統都必須對應至客戶、 訂單及訂單行項目資料表。 指定的客戶可能會有多個與包含多個項目的每筆訂單的訂單。 具有兩個 dropdownlist 進行和 GridView 的使用者，可以呈現這類資料。 第一個 DropDownList 會對第二個資料庫中的每個客戶的清單項目之一的內容所選取的客戶所下訂單。 GridView 會列出從選取的訂單明細項目。

雖然 Northwind 資料庫包含標準客戶/順序/訂單詳細資料資訊在其`Customers`， `Orders`，和`Order Details`架構中未擷取的資料表，這些資料表。 然而，我們仍然可以說明如何使用兩個相依的 dropdownlist 進行。 第一個 DropDownList 會列出類別目錄以及第二個屬於所選分類的產品。 DetailsView 會列出所選產品的詳細資料。

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>步驟 1：建立和填入類別 DropDownList

我們第一個目標是要加入列出的類別目錄的 DropDownList。 這些步驟在先前的教學課程中，已檢查詳細資料，但摘要說明如下，為求完整性。

開啟`MasterDetailsDetails.aspx`頁面中`Filtering`資料夾中，將 DropDownList 新增至頁面上，設定其`ID`屬性設`Categories`，然後按一下 設定資料來源中的 連結它的智慧標籤。 從資料來源組態精靈] 選擇 [加入新的資料來源。


[![Add DropDownList 新的資料來源](master-detail-filtering-with-two-dropdownlists-cs/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image1.png)

**圖 1**:加入新的資料來源的 DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image3.png))


新的資料來源，當然，應該 ObjectDataSource。 命名新 ObjectDataSource `CategoriesDataSource` ，並讓它叫用`CategoriesBLL`物件的`GetCategories()`方法。


[![C若要使用 CategoriesBLL 類別選擇](master-detail-filtering-with-two-dropdownlists-cs/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image4.png)

**圖 2**:選擇要使用`CategoriesBLL`類別 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image6.png))


[![C設定為使用 GetCategories() 方法的 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image7.png)

**圖 3**:設定要使用 ObjectDataSource`GetCategories()`方法 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image9.png))


在設定 ObjectDataSource 後我們仍然需要指定哪一個資料來源欄位應該會顯示在`Categories`DropDownList 和哪一個應設定為清單項目的值。 設定`CategoryName`欄位做為顯示和`CategoryID`做為每個清單項目的值。


[![Have DropDownList 顯示類別名稱] 欄位和做為值使用 CategoryID](master-detail-filtering-with-two-dropdownlists-cs/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image10.png)

**圖 4**:DropDownList 顯示`CategoryName`欄位，並使用`CategoryID`的值 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image12.png))


現在我們有 DropDownList 控制項 (`Categories`)，並填入來自記錄`Categories`資料表。 當使用者選擇新的類別從 DropDownList，我們會想要重新整理產品，我們將在步驟 2 中建立的 DropDownList 發生回傳。 因此，請檢查啟用 AutoPostBack 選項`categories`DropDownList 的智慧標籤。


[![E啟用的類別 DropDownList AutoPostBack](master-detail-filtering-with-two-dropdownlists-cs/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image13.png)

**圖 5**:Povolit vlastnost AutoPostBack，如`Categories`DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image15.png))


## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>步驟 2：第二個 DropDownList 以顯示所選的分類的產品

使用`Categories`DropDownList 完成下, 一步是要顯示屬於所選分類的產品的 DropDownList。 若要這麼做，將另一個 DropDownList 新增至名為頁面`ProductsByCategory`。 如同`Categories`下拉式清單中，建立的新 ObjectDataSource `ProductsByCategory` DropDownList 名為`ProductsByCategoryDataSource`。


[![Add ProductsByCategory DropDownList 新的資料來源](master-detail-filtering-with-two-dropdownlists-cs/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image16.png)

**圖 6**:加入新的資料來源，如`ProductsByCategory`DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image18.png))


[![Create 新 ObjectDataSource 名為 ProductsByCategoryDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image19.png)

**圖 7**:建立新的 ObjectDataSource 具名`ProductsByCategoryDataSource`([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image21.png))


由於`ProductsByCategory`DropDownList 以顯示屬於所選取的類別目錄，只要這些產品的需求有叫用的 ObjectDataSource`GetProductsByCategoryID(categoryID)`方法從`ProductsBLL`物件。


[![C若要使用 ProductsBLL 類別選擇](master-detail-filtering-with-two-dropdownlists-cs/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image22.png)

**圖 8**:選擇要使用`ProductsBLL`類別 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image24.png))


[![C設定為使用 GetProductsByCategoryID(categoryID) 方法的 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image25.png)

**圖 9**:設定要使用 ObjectDataSource`GetProductsByCategoryID(categoryID)`方法 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image27.png))


我們需要在精靈的最後一個步驟中指定的值*`categoryID`* 參數。 將此參數指派給選取的項目從`Categories`DropDownList。


[![Pull categoryID 類別 DropDownList 中的參數值](master-detail-filtering-with-two-dropdownlists-cs/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image28.png)

**圖 10**:提取*`categoryID`* 參數值，從`Categories`DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image30.png))


使用 ObjectDataSource 設定，全都是指定哪些資料來源欄位用於顯示和 DropDownList 項目的值。 顯示`ProductName`欄位，並使用`ProductID`欄位的值。


[![S指定資料來源欄位使用的 DropDownList ListItems 的文字和值屬性](master-detail-filtering-with-two-dropdownlists-cs/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image31.png)

**圖 11**:指定資料來源欄位使用 DropDownList `ListItem` s'`Text`並`Value`屬性 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image33.png))


使用 ObjectDataSource 和`ProductsByCategory`DropDownList 設定我們的頁面會顯示兩個 dropdownlist 進行： 第二個會列出這些屬於所選分類的產品時，第一個會列出所有類別。 當使用者從第一個 DropDownList 中選取新的類別時，會發生回傳，第二個 DropDownList 會重新繫結，顯示這些產品屬於新選取的類別目錄。 圖 12 和 13 顯示`MasterDetailsDetails.aspx`中透過瀏覽器檢視時的動作。


[![W當第一次瀏覽] 頁面上，「 飲料 」 分類是已選取](master-detail-filtering-with-two-dropdownlists-cs/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image34.png)

**圖 12**:當第一次瀏覽的頁面，選取 「 飲料 」 分類 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image36.png))


[![Choosing 不同的類別會顯示新的類別目錄的產品](master-detail-filtering-with-two-dropdownlists-cs/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image37.png)

**圖 13**:選擇不同的類別目錄會顯示新的類別目錄的產品 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image39.png))


目前`productsByCategory`下拉式清單中，變更時，並未*不*造成回傳。 不過，我們想要在我們新增了 DetailsView 來顯示選取之的產品的詳細資料 (步驟 3) 後，就會發生回傳。 因此，請檢查啟用 AutoPostBack 核取方塊`productsByCategory`DropDownList 的智慧標籤。


[![E啟用 productsByCategory DropDownList AutoPostBack 功能](master-detail-filtering-with-two-dropdownlists-cs/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image40.png)

**圖 14**:啟用 AutoPostBack 功能，以便`productsByCategory`DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image42.png))


## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>步驟 3：使用 DetailsView 來顯示所選產品的詳細資料

最後一個步驟是在 DetailsView 中顯示所選產品的詳細資料。 若要達成此目的，新增至網頁的 DetailsView，設定其`ID`屬性設`ProductDetails`，並為它建立新的 ObjectDataSource。 設定提取其資料從 ObjectDataSource`ProductsBLL`類別的`GetProductByProductID(productID)`使用所選的值的方法`ProductsByCategory`DropDownList 值*`productID`* 參數。


[![C若要使用 ProductsBLL 類別選擇](master-detail-filtering-with-two-dropdownlists-cs/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image43.png)

**圖 15**:選擇要使用`ProductsBLL`類別 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image45.png))


[![C設定為使用 GetProductByProductID(productID) 方法的 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image46.png)

**圖 16**:設定要使用 ObjectDataSource`GetProductByProductID(productID)`方法 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image48.png))


[![Pull productID ProductsByCategory DropDownList 中的參數值](master-detail-filtering-with-two-dropdownlists-cs/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image49.png)

**圖 17**:提取*`productID`* 參數值，從`ProductsByCategory`DropDownList ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image51.png))


您可以選擇在 DetailsView 中顯示任何可用的欄位。 我選擇移除`ProductID`， `SupplierID`，和`CategoryID`欄位和重新排列及格式化其餘的欄位。 此外，我清除 DetailsView`Height`和`Width`屬性，可讓 DetailsView 展開至最佳顯示效果所需的寬度，其資料，而不需要它限制為指定的大小。 以下顯示完整的標記：


[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample1.aspx)]

花點時間試用`MasterDetailsDetails.aspx`瀏覽器中的頁面。 乍看之下似乎，一切都運作所需，但還有一個微妙的問題。 當您選擇新的類別`ProductsByCategory`DropDownList 會更新為包含選取之類別目錄，這些產品，但`ProductDetails`DetailsView 持續顯示先前的產品資訊。 選擇所選分類的不同產品時，會更新 DetailsView。 此外，如果夠徹底測試，您會發現，如果您持續選擇新的類別目錄 (例如選擇飲料`Categories`下拉式清單中，則 「 調味品 」，然後 Confections) 每個其他的類別選項會導致`ProductDetails`DetailsView 重新整理。

為了將實體化此問題，讓我們看看一個特定的範例。 當您第一次造訪網頁時所選取的飲料類別和相關的產品中所載入`ProductsByCategory`DropDownList。 Chai 是所選的產品，而且其詳細資料會顯示在`ProductDetails`DetailsView，如 圖 18 所示。


[![T在 DetailsView 中會顯示他選取產品的詳細資料](master-detail-filtering-with-two-dropdownlists-cs/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image52.png)

**圖 18**:在 DetailsView 中會顯示選取之產品的詳細資料 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image54.png))


如果您將從飲料的類別選項變更為 「 調味品 」 時，就會發生回傳和`ProductsByCategory`DropDownList 會相應地更新，但 DetailsView 仍顯示 Chai 詳細資料。


[![T他先前選取產品的詳細資料都仍顯示](master-detail-filtering-with-two-dropdownlists-cs/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image55.png)

**圖 19**:仍然顯示的先前選取產品的詳細資料 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image57.png))


挑選新的產品，從清單重新整理 DetailsView，如預期般運作。 如果您之後變更產品挑選新的類別，DetailsView 一次不會重新整理。 不過，如果不要選擇新的產品，您會選取新的類別，就會重新整理 DetailsView。 在世界情形這裡？

問題是網頁的生命週期中的時間問題。 每次要求頁面時繼續進行一些步驟，為其呈現方式。 在其中一個步驟中 ObjectDataSource 控制項，看看是否有任一的核取其`SelectParameters`值已變更。 因此，資料 Web 控制項繫結至 ObjectDataSource 會知道它需要重新整理其顯示。 例如，當新的類別目錄選取時， `ProductsByCategoryDataSource` ObjectDataSource 會偵測已變更其參數值和`ProductsByCategory`DropDownList 重新繫結本身，取得所選分類的產品。

在此情況下，就會發生此問題是在頁面生命週期的 ObjectDataSources 檢查已變更的參數中的點就會發生*之前*的相關聯的資料 Web 控制項重新繫結。 因此，當您選取新的類別時`ProductsByCategoryDataSource`ObjectDataSource 偵測到它的參數值的變更。 使用 ObjectDataSource `ProductDetails` DetailsView，不過，不會注意任何這類變更因為`ProductsByCategory`DropDownList 尚未重新繫結。 稍後的生命週期`ProductsByCategory`DropDownList 重新繫結至其 ObjectDataSource，抓取新選取的分類的產品。 雖然`ProductsByCategory`DropDownList 的值已變更， `ProductDetails` DetailsView 的 ObjectDataSource 已完成其參數值檢查; 因此，DetailsView 會顯示其先前的結果。 這種互動是以 圖 20 所示。


[![T他 ProductsByCategory DropDownList 值變更之後 ProductDetails DetailsView 的 ObjectDataSource 會檢查變更](master-detail-filtering-with-two-dropdownlists-cs/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image58.png)

**圖 20**:`ProductsByCategory` DropDownList 值變更之後`ProductDetails`DetailsView 的 ObjectDataSource 會檢查變更 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image60.png))


若要補救這我們需要明確地重新繫結`ProductDetails`DetailsView 之後`ProductsByCategory`已繫結 DropDownList。 我們可以呼叫來完成這`ProductDetails`DetailsView 的`DataBind()`方法時`ProductsByCategory`DropDownList 的`DataBound`引發事件。 加入下列事件處理常式程式碼，以`MasterDetailsDetails.aspx`頁面的程式碼後置類別 (請參閱 「[以程式設計方式設定 ObjectDataSource 的參數值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)「 如需有關如何加入事件處理常式的討論):


[!code-csharp[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample2.cs)]

此明確呼叫之後`ProductDetails`DetailsView 的`DataBind()`方法已加入，本教學課程可以正常運作。 圖 21 反白顯示已變更如何補救我們先前的問題。


[![T他 ProductDetails DetailsView 是明確地重新整理時 ProductsByCategory DropDownList 的資料繫結事件引發時](master-detail-filtering-with-two-dropdownlists-cs/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image61.png)

**圖 21**:`ProductDetails` DetailsView 時，明確地重新整理`ProductsByCategory`DropDownList 的`DataBound`引發事件 ([按一下以檢視完整大小的影像](master-detail-filtering-with-two-dropdownlists-cs/_static/image63.png))


## <a name="summary"></a>總結

DropDownList 作為主版/詳細報告的理想的使用者介面項目之間的主要和詳細的記錄沒有一個對多關聯性。 在先前的教學課程中，我們了解如何使用單一的 DropDownList 來篩選所選取的類別顯示產品的內容。 在本教學課程我們產品的 GridView 取代下拉式清單中，並用 DetailsView 來顯示所選產品的詳細資料。 在本教學課程所討論的概念，可以輕鬆擴充到資料模型包含多個的其中一個對多關聯性，例如客戶、 訂單及訂單項目中。 一般情況下，您可以隨時加入 dropdownlist 進行的每個 「 一 」 實體中的一對多關聯性中。

快樂地寫程式 ！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七個 ASP 書籍和的創辦人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年從事 Microsoft Web 技術工作。 Scott 會擔任獨立的顧問、 培訓講師和作家。 他最新的著作是[ *Sams 教導您自己 ASP.NET 2.0 在 24 小時內*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在觸達[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或透過他的部落格，這位於 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多實用的檢閱者檢閱。 本教學課程中的潛在客戶檢閱者已 Hilton Giesenow。 有興趣檢閱我即將推出的 MSDN 文章嗎？ 如果是這樣，psychic 在[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](master-detail-filtering-with-a-dropdownlist-cs.md)
> [下一頁](master-detail-filtering-across-two-pages-cs.md)
