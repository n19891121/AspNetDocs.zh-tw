---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: 使用 LINQ 創建模型類到 SQL (VB) |微軟文件
author: rick-anderson
description: 本教學的目的是解釋為mVC應用程式創建模型類的方法ASP.NET。 在本教學中,您將瞭解如何建構模型 c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 1a6133227eedc8934af7bf872532ca667b97d0f8
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542699"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>使用 LINQ to SQL 建立模型類別 (VB)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> 本教學的目的是解釋為mVC應用程式創建模型類的方法ASP.NET。 在本教學中,您將瞭解如何利用 Microsoft LINQ 到 SQL 構建模型類並執行資料庫訪問。

本教學的目的是解釋為mVC應用程式創建模型類的方法ASP.NET。 在本教學中,您將瞭解如何利用 Microsoft LINQ 到 SQL 構建模型類並執行資料庫訪問。

在本教程中,我們將構建一個基本的 Movie 資料庫應用程式。 我們從以最快、最簡單的方式創建 Movie 資料庫應用程式開始。 我們直接從控制器操作執行所有數據訪問。

接下來,您將瞭解如何使用儲存庫模式。 使用存儲庫模式需要多一點工作。 但是,採用此模式的優點是,它使您能夠構建能夠適應更改且易於測試的應用程式。

## <a name="what-is-a-model-class"></a>什麼是模型類?

MVC 模型包含 MVC 檢視或 MVC 控制器中未包含的所有應用程式邏輯。 特別是,MVC 模型包含所有應用程式業務和數據訪問邏輯。

您可以使用各種不同的技術來實現數據存取邏輯。 例如,您可以使用 Microsoft 實體框架、NHibernate、亞音速或 ADO.NET 類構建數據存取類。

在本教學中,我使用 LINQ 到 SQL 來查詢和更新資料庫。 LINQ 到 SQL 為您提供了一種非常簡單的與 Microsoft SQL Server 資料庫互動的方法。 但是,請務必瞭解,ASP.NET MVC 框架不以任何方式與 LINQ 綁定到 SQL。 ASP.NET MVC 與任何數據訪問技術相容。

## <a name="create-a-movie-database"></a>建立影片資料庫

在本教程中,為了說明如何構建模型類,我們構建了一個簡單的 Movie 資料庫應用程式。 第一步是創建新資料庫。 右鍵單擊解決方案資源管理器\_視窗中的應用數據資料夾,然後選擇功能表選項 **「添加,新專案**」。。 選擇 SQL Server 資料庫範本,給它取名為 MoviesDB.mdf,然後單擊 **「添加**」按鈕(參見圖 1)。

[![新增 SQL 伺服器資料庫](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**圖 01**: 新增新的 SQL Server 資料庫 ([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))

創建新資料庫后,可以通過按兩\_下應用 數據資料夾中的 MoviesDB.mdf 檔案來打開資料庫。 按兩下 MoviesDB.mdf 檔將打開伺服器資源管理器視窗(參見圖 2)。

|   | 使用視覺化 Web 開發人員時,伺服器資源管理器視窗稱為資料庫資源管理器視窗。 |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![使用伺服器資源管理員視窗](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**圖 02**: 使用伺服器資源管理員視窗 ([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))

我們需要向資料庫中添加一個表示我們電影的表。 右鍵按下「表」資料夾並選擇功能表選項 **「新增新表**」。。 選擇此功能表選項將打開表設計器(參見圖 3)。

[![使用伺服器資源管理員視窗](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**圖 03**: 表格設計器 ([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))

我們需要將以下列新增到資料庫表中:

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| Id | Int | False |
| Title | 恩瓦爾查爾 (200) | False |
| 導演 | 恩瓦爾查爾 (50) | False |

您需要對 Id 列執行兩項特殊操作。 首先,您需要通過選擇表設計器中的列並按一下鍵的圖示,將 Id 列標記為主鍵列。 LINQ 到 SQL 要求您在針對資料庫執行插入或更新時指定主鍵列。

接下來,您需要通過將值"是"分配給 **"是標識"** 屬性來將 Id 列標記為標識列(參見圖 3)。 標識列是一列,每當向表添加新數據行時,將自動分配新編號。

進行這些更改后,將表與名稱 tblMovie 保存。 您可以通過按下「儲存」按鈕儲存表。

## <a name="create-linq-to-sql-classes"></a>建立 LINQ 到 SQL 類別

我們的 MVC 模型將包含表示 tblMovie 資料庫表的 LINQ 到 SQL 類。 創建這些 LINQ 到 SQL 類的最簡單方法是右鍵按一下「模型」資料夾,選擇 **「新增、新建專案**」,選擇 LINQ 到 SQL 類範本,為類指定名稱 Movie.dbml,然後單擊 **「添加**」按鈕(參見圖 4)。

[![將 LINQ 建立 SQL 類別](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**圖 04**: 建立 LINQ 到 SQL 類別 ([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))

在創建到 SQL 類的影片 LINQ 後,將立即出現對象關係設計器。 您可以將資料庫表從伺服器資源管理器視窗拖動到對象關係設計器上,以創建 LINQ 到表示特定資料庫表的 SQL 類。 我們需要將 tblMovie 資料庫表添加到對象關係設計器上(參見圖 4)。

[![使用物件關係設計器](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**圖 05**:使用物件關係設計器 ([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))

默認情況下,對象關係設計器創建與拖動到設計器的資料庫表名稱完全相同的類。 但是,我們不想調用我們的類 tblMovie。 因此,單擊設計器中的類的名稱並將類的名稱更改為"Movie"。

最後,請記住單擊 **「儲存**」按鈕(軟盤的圖片)以將 LINQ 保存到 SQL 類。 否則,對象關係設計器不會生成 LINQ 到 SQL 類。

## <a name="using-linq-to-sql-in-a-controller-action"></a>在控制器操作中使用 LINQ 到 SQL

現在,我們有了 LINQ 到 SQL 類,我們可以使用這些類從資料庫中檢索數據。 在本節中,您將學習如何直接在控制器操作中使用 LINQ 到 SQL 類。 我們將在 MVC 檢視中顯示 tblMovies 資料庫表中的影片清單。

首先,我們需要修改 HomeController 類。 此類可以在應用程式的"控制器"資料夾中找到。 修改類,使其看起來像清單 1 中的類。

**清單1 |`Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

清單 1 中的 Index() 操作使用 LINQ 到 SQL 數據上下文類(MovieDataContext)來表示 MovieDB 資料庫。 MoveDataContext 類由可視化工作室對象關係設計器生成。

對 DataContext 執行 LINQ 查詢,以便從 tblMovies 資料庫表中檢索所有影片。 影片清單分配給名為影片的本地變數。 最後,影片清單通過檢視數據傳遞到視圖。

為了顯示影片,我們接下來需要修改索引視圖。 您可以在「檢視」資料夾中找到「索引」檢視。 更新索引檢視,使其看起來像清單 2 中的檢視。

**清單2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

請注意,修改後的索引檢視在檢視頂部&lt;包含 %#&gt;匯入 命名空間 % 指令。 此指令導入 MvcApplication1 命名空間。 我們需要這個命名空間,以便與視圖中的模型類(尤其是 Movie 類)配合使用。

清單 2 中的檢視包含一個 For Each 迴圈,該迴圈迴圈循環通過 ViewData.Model 屬性表示的所有項。 為每個影片顯示"標題"屬性的值。

請注意,ViewData.Model 屬性的值將轉換為 IE500。 這是必要的,以迴圈流覽ViewData.Model的內容。 此處的另一個選項是創建強類型視圖。 創建強類型視圖時,將ViewData.Model 屬性轉換為視圖的代碼後面類中的特定類型。

如果在修改 HomeController 類和索引檢視後運行應用程式,則您將獲得一個空白頁。 您將獲得空白頁,因為 tblMovies 資料庫表中沒有影片記錄。

為了將記錄添加到 tblMovies 資料庫表,請右鍵單擊伺服器資源管理器視窗中的 tblMovies 資料庫表(可視化 Web 開發人員中的資料庫資源管理器視窗),然後選擇功能表選項 **「顯示表數據**」。。 您可以使用顯示的網格插入影片記錄(參見圖 5)。

[![插入影片](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**圖 06**: 插入影片([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))

將一些資料庫記錄添加到 tblMovies 表並運行應用程式後,您將看到圖 7 中的頁面。 所有影片資料庫記錄都顯示在項目符號清單中。

[![使用「索引」檢視顯示影片](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**圖 07**: 顯示有索引檢視的影片([按下以檢視全尺寸影像](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))

## <a name="using-the-repository-pattern"></a>使用儲存式庫模式

在上一節中,我們直接在控制器操作中使用 LINQ 到 SQL 類。 我們直接從索引() 控制器操作中使用 MovieDataContext 類。 在簡單的應用程序的情況下,這樣做沒有錯。 但是,在控制器類中直接使用 LINQ 到 SQL 會在需要構建更複雜的應用程式時出現問題。

使用 LINQ 到控制器類中的 SQL 使將來很難切換數據存取技術。 例如,您可能決定從使用 Microsoft LINQ 切換到 SQL,轉而使用 Microsoft 實體框架作為數據存取技術。 在這種情況下,您需要重寫訪問應用程式內資料庫的每個控制器。

在控制器類中使用 LINQ 到 SQL 也會使應用程式生成單元測試變得困難。 通常,在執行單元測試時,您不希望與資料庫進行交互。 您希望使用單元測試來測試應用程式邏輯,而不是資料庫伺服器。

為了構建一個更適應未來更改且更易於測試的 MVC 應用程式,應考慮使用儲存庫模式。 使用存儲庫模式時,將創建一個單獨的存儲庫類,其中包含所有資料庫訪問邏輯。

創建存儲庫類時,將創建一個表示存儲庫類使用的所有方法的介面。 在控制器中,您可以根據介面而不是儲存庫編寫代碼。 這樣,將來可以使用不同的數據存取技術實現存儲庫。

清單3中的介面名為 IMovieRepository,它表示名為 ListAll() 的單個方法。

**清單3 |`Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

清單4中的存儲庫類實現了IMovie存儲庫介面。 請注意,它包含一個名為 ListAll() 的方法,對應於 IMovieRepository 介面所需的方法。

**清單4 |`Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

最後,清單 5 中的電影控制器類使用儲存庫模式。 它不再直接使用 LINQ 到 SQL 類。

**清單5 |`Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

請注意,清單 5 中的 MoviesController 類有兩個構造函數。 當應用程式運行時,將調用第一個構造函數,即無參數構造函數。 此構造函數創建 MovieRepository 類的實例並將其傳遞給第二個構造函數。

第二個構造函數具有單個參數:IMovie存儲庫參數。 此建構函數只需將參數的值分配給名為\_存儲庫的類級欄位。

MoviesController 類正在利用稱為依賴項注入模式的軟體設計模式。 特別是,它使用名為構造函數依賴項注入的內容。 使用閱讀馬丁福勒的以下文章,您可以閱讀有關此模式的更多內容:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

請注意,MovieController 類中的所有代碼(第一個構造函數除外)與 IMovieRepository 介面而不是實際的 MovieRepository 類進行交互。 代碼與抽象介面而不是介面的具體實現進行交互。

如果要修改應用程式使用的數據訪問技術,只需使用使用替代資料庫訪問技術的類實現 IMovieRepository 介面即可。 例如,您可以創建實體框架電影存儲庫類或子聲波電影存儲庫類。 由於控制器類是針對介面程式設計的,因此可以將IMovieRepository的新實現傳遞給控制器類,並且該類將繼續工作。

此外,如果要測試 MovieController 類,則可以將假影片儲存庫類傳遞給電影控制器。 可以使用一個類實現 IMovieRepository 類,該類實際上不訪問資料庫,但包含 IMovieRepository 介面的所有必需方法。 這樣,您可以單元測試 MoviesController 類,而無需實際訪問實際資料庫。

## <a name="summary"></a>總結

本教學的目的是展示如何利用 Microsoft LINQ 到 SQL 來創建 MVC 模型類。 我們研究了在mVC應用程式中顯示資料庫數據的兩種策略ASP.NET。 首先,我們創建了 LINQ 到 SQL 類,並直接在控制器操作中使用這些類。 使用 LINQ 到控制器中的 SQL 類使您能夠在 MVC 應用程式中快速輕鬆地顯示資料庫數據。

接下來,我們探索了一條稍微困難但絕對更良性的顯示資料庫數據的途徑。 我們利用了存儲庫模式,將所有資料庫存取邏輯放在一個單獨的儲存庫類中。 在我們的控制器中,我們針對介面而不是具體類編寫了所有代碼。 存儲庫模式的優點是,它使我們能夠在未來輕鬆更改資料庫訪問技術,並使我們能夠輕鬆測試我們的控制器類。

> [!div class="step-by-step"]
> [前一個](creating-model-classes-with-the-entity-framework-vb.md)
> [下一個](displaying-a-table-of-database-data-vb.md)
