---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: 在圖表中顯示數據,其中ASP.NET網頁 (Razor) |微軟文件
author: rick-anderson
description: 本章介紹如何在圖表中顯示數據。 在前面的章節中,您學習了如何在網格中手動顯示數據。 本章解釋...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: ad55d4898ee39e0239ef8b0bd5eea6387af3c816
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542881"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>在圖表中顯示具有 ASP.NET 網頁(Razor)的資料

由[微軟](https://github.com/microsoft)

> 本文介紹如何使用圖表使用`Chart`説明程式在ASP.NET網頁 (Razor) 網站中顯示數據。
> 
> **您將學習:**
> 
> - 如何在圖表中顯示數據。
> - 如何使用內置主題對圖表進行樣式設置。
> - 如何保存圖表以及如何緩存圖表以獲得更好的性能。
> 
> 以下是本文介紹的ASP.NET程式設計功能:
> 
> - 幫手`Chart`
> 
> > [!NOTE]
> > 本文中的資訊適用於ASP.NET網頁 1.0 和網頁 2。

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>圖表說明程式

當您要以圖形形式顯示數據時,可以使用`Chart`幫助程式。 `Chart`説明程式可以渲染顯示各種圖表類型中的數據的圖像。 它支援許多格式設定和標籤選項。 `Chart`説明程式可以呈現 30 多種圖表類型,包括您可能從 Microsoft Excel 或其他工具&#8212;區域圖、條形圖、柱形圖、折線圖和餅圖等工具中熟悉的所有類型的圖表,以及更專業的圖表(如股票圖表)。

| **面積圖**![描述:面積圖類型的圖片](7-displaying-data-in-a-chart/_static/image1.jpg) | **條形圖**![說明:條形圖類型的圖片](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **柱形圖**![說明:柱形圖類型的圖片](7-displaying-data-in-a-chart/_static/image3.jpg) | **折線圖**![描述:折線圖類型的圖片](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **圓形圖**![說明:圓形圖類型的圖片](7-displaying-data-in-a-chart/_static/image5.jpg) | **股票圖表**![描述:股票圖表類型的圖片](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>圖表項目

圖表顯示數據和其他元素,如圖例、軸、系列等。 下圖顯示了使用`Chart`幫助器時可以自定義的許多圖表元素。 本文介紹如何設置其中某些(不是全部)元素。

![標題:顯示圖表元素的圖片](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>從資料建立圖表

在圖表中顯示的數據可以來自陣列、從資料庫返回的結果或 XML 檔中的數據。

### <a name="using-an-array"></a>使用陣列

如ASP.NET[網頁程式設計簡介中所述,使用Razor語法](https://go.microsoft.com/fwlink/?LinkId=202890)程式設計,陣列允許您在單個變數中存儲類似項的集合。 可以使用陣列來包含要包含在圖表中的數據。

此過程展示如何使用預設圖表類型從陣列中的數據建立圖表。 它還演示如何在頁面中顯示圖表。

1. 建立名為*ChartArrayBasic.cshtml*的新檔案。
2. 將現有內容取代為以下內容: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    代碼首先創建一個新圖表並設置其寬度和高度。 使用`AddTitle`方法指定圖表標題。 要新增資料,請使用方法`AddSeries`。 在此範例中`name`,使用`xValue``yValues``AddSeries`方法的和參數。 參數`name`顯示在圖表例中。 該`xValue`參數包含沿圖表水平軸顯示的數據陣列。 該`yValues`參數包含用於繪製圖表垂直點的數據陣列。

    該方法`Write`實際上呈現圖表。 在這種情況下,由於您沒有指定圖表類型,`Chart`説明程式將呈現其預設圖表,即柱形圖。
3. 在瀏覽器中運行頁面。 瀏覽器顯示圖表。 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>對圖表資料使用資料庫查詢

如果要繪製圖表的資訊位於資料庫中,則可以運行資料庫查詢,然後使用結果中的資料創建圖表。 此過程展示如何讀取和顯示在[文章"使用ASP.NET網頁網站中的資料庫簡介](https://go.microsoft.com/fwlink/?LinkId=202893)"中創建的資料庫中的數據。

1. 如果該資料夾不存在,則向網站的根目錄添加*應用\_數據*資料夾。
2. 在 *「\_應用資料*」資料夾中,添加名為*SmallBakery.sdf*的資料庫檔案,該檔在[「使用ASP.NET網頁網站中的資料庫簡介」中](https://go.microsoft.com/fwlink/?LinkId=202893)所述。
3. 建立名為*ChartDataQuery.cshtml*的新檔案。
4. 將現有內容取代為以下內容:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    代碼首先打開 SmallBakery 資料庫並將其分配給`db`名為的 變數。 此變數表示可用於`Database`讀取資料庫和寫入資料庫的物件。 接下來,代碼運行 SQL 查詢以獲取每個產品的名稱和價格。 代碼創建一個新圖表,並通過調用圖表`DataBindTable`的方法將資料庫查詢傳遞給它。 此方法採用兩個參數:`dataSource`參數用於查詢中的數據`xField`, 該參數允許您設定用於圖表 x 軸的資料列。

    作為使用 方法的替代`DataBindTable`方法 ,`AddSeries``Chart`可以使用 幫助器的方法。 該方法`AddSeries`允許您設置`xValue``yValues`和 參數。 例如,而不是使用如下所示`DataBindTable`的方法:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    可以使用以下的方法`AddSeries`:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    兩者都呈現相同的結果。 該方法`AddSeries`更靈活,因為您可以更明確地指定圖表類型和數據,但如果不需要額外的靈活性`DataBindTable`, 則該方法更易於使用。
5. 在瀏覽器中運行頁面。 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>使用 XML 資料

圖表的第三個選項是使用 XML 檔案作為圖表的數據。 這要求 XML 檔也具有描述 XML 結構的架構檔 *(.xsd*檔)。 此過程展示如何從 XML 檔讀取數據。

1. 在*應用\_資料*資料夾中,創建名為*data.xml*的新 XML 檔。
2. 將現有 XML 替換為以下內容,即有關虛構公司員工的一些 XML 數據。 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 在*應用\_資料*資料夾中,創建名為*data.xsd*的新 XML 檔。 (請注意,這次的擴展是 *.xsd*.)
4. 將現有 XML 取代為以下內容: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 在網站的根目錄中,創建一個名為*ChartDataXML.cshtml*的新檔。
6. 將現有內容取代為以下內容: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    代碼首先創建一個`DataSet`物件。 此物件用於管理從 XML 檔讀取的數據,並根據架構檔中的資訊對其進行組織。 (請注意,代碼的頂部包括敘述`using SystemData`。 這是為了能夠處理`DataSet`物件所必需的。 有關詳細資訊,請參閱[&quot;本文後面的&quot;使用 語句和完全限定名稱](#SB_UsingStatements)。

    接下來,代碼基於數據集創建`DataView`一個物件。 數據視圖提供圖表可以綁定到&#8212;的物件,即讀取和繪圖。 `AddSeries`圖表使用 方法綁定到數據,如您前面在繪製陣列數據圖表時所看到的那樣,但`xValue`此`yValues`時間和`DataView`參數設置為 物件除外。

    此示例還演示如何指定特定的圖表類型。 在`AddSeries`方法中添加數據時`chartType`, 參數也會設置為顯示圓體圖。
7. 在瀏覽器中運行頁面。 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>「使用」語句和完全限定的名稱
> 
> 使用 Razor 語法 ASP.NET 網頁的 .NET 框架由數千個元件(類)組成。 為了使使用所有這些類可以管理,它們被組織成*命名空間*,有點像庫。 例如,`System.Web`命名空間包含支援瀏覽器/ 伺服器通訊的`System.Xml`類別, 命名空間包含用於建立和讀取 XML`System.Data`檔的類別, 並且命名空間包含允許您處理資料的類別。
> 
> 為了訪問 .NET Framework 中的任何給定類,代碼不僅需要瞭解類名稱,還需要瞭解類中的命名空間。 例如,為了使用`Chart`幫助程式,代碼需要查找`System.Web.Helpers.Chart`類,該類將命名空間`System.Web.Helpers`() 與類名稱`Chart`( ( ) 合併在一起。 這稱為類的*完全限定*名稱&#8212;其在 .NET 框架的龐大範圍內的完整、明確位置。 在代碼中,如下所示:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 但是,每次要引用類或説明程式時,必須使用這些長而完全限定的名稱是繁瑣的(且容易出錯)。 因此,為了更輕鬆地使用類名,可以*導入*您感興趣的命名空間,這通常只是 .NET 框架中許多命名空間中的少數。 如果已匯入命名空間,則只能使用類別名稱`Chart`( ) 而不是完全限定`System.Web.Helpers.Chart`的名稱 ( 。 當代碼運行並遇到類名稱時,它可以只查看已導入的命名空間來查找該類。
> 
> 當您使用帶有 Razor 語法的ASP.NET網頁創建網頁時,您通常每次都使用相同的類集`WebPage`,包括類、各種幫助器等。 為了節省您每次創建網站時導入相關命名空間的工作,ASP.NET進行了配置,以便自動為每個網站導入一組核心命名空間。 這就是為什麼到目前為止您不必處理命名空間或導入名稱空間的原因;您使用的所有類都位於已導入的命名空間中。
> 
> 但是,有時您需要使用不在自動導入的命名空間中的類。 在這種情況下,可以使用該類的完全限定名稱,也可以手動導入包含該類的命名空間。 要匯入命名空間,請使用`using`語句(`import`在 Visual Basic 中),如您前面的範例一樣。
> 
> 例如,`DataSet`類別位於命名空間`System.Data`中 。 命名`System.Data`空間不能自動可用於ASP.NET Razor 頁面。 因此,要使用完全限定`DataSet`名稱使用類,可以使用如下所示的代碼:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 如果必須重複使用類,`DataSet`則可以匯入以下的命名空間,然後在代碼中僅使用類別名稱:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 可以為要引用`using`的任何其他 .NET框架命名空間添加語句。 但是,如上所述,您不需要經常執行此操作,因為要使用的大多數類都位於命名空間中,名稱空間由ASP.NET自動導入,用於 *.cshtml*和 *.vbhtml*頁面。

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>在網頁內顯示圖表

在到目前為止看到的範例中,您將創建一個圖表,然後將圖表作為圖形直接呈現給瀏覽器。 但是,在許多情況下,您希望將圖表顯示為頁面的一部分,而不僅僅是在瀏覽器中。 為此,需要兩步過程。 第一步是創建生成圖表的頁面,正如您已經看到的那樣。

第二步是在另一頁中顯示生成的圖像。 要顯示影像,請使用`<img>`HTML 元素,就像顯示任何影像一樣。 但是`<img>`,該元素引用的不是 *.jpg*或 *.png*檔,而是`Chart`引用包含創建圖表 的説明器的 *.cshtml*檔。 當顯示頁執行時,`<img>`元素取得幫助器`Chart`的 輸出並呈現圖表。

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 建立名為*ShowChart.cshtml*的檔案。
2. 將現有內容取代為以下內容: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    代碼使用`<img>`元素 來顯示您在*ChartArrayBasic.cshtml*檔案中建立的圖表。
3. 在瀏覽器中運行網頁。 *ShowChart.cshtml*檔案基於*ChartArrayBasic.cshtml*檔案中的代碼顯示圖表圖像。

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>設定圖表樣式

`Chart`幫助程式支援大量選項,這些選項允許您自定義圖表的外觀。 您可以設置顏色、字體、邊框等。 自訂圖表外觀的一種簡單方法是使用*主題*。 佈景主題是指定如何使用字型、色彩、標籤、調色盤、框線和效果來呈現圖表的資訊集合。 (請注意,圖表的樣式並不指示圖表的類型。

下表列出了內置主題。

| 佈景主題 | 描述 |
| --- | --- |
| `Vanilla` | 在白色背景上顯示紅色列。 |
| `Blue` | 在藍色漸變背景上顯示藍色列。 |
| `Green` | 在綠色漸變背景上顯示藍色列。 |
| `Yellow` | 在黃色漸變背景上顯示橙色列。 |
| `Vanilla3D` | 在白色背景上顯示三維紅色列。 |

您可以指定建立新圖表時要使用的主題。

1. 建立名為*ChartStyleGreen.cshtml*的新檔。
2. 將頁面中的現有內容取代為以下內容:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    此代碼與使用資料庫進行資料的早期示例相同,但在創建`theme``Chart`物件時添加參數。 下面顯示了變更的代碼:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 在瀏覽器中運行頁面。 您看到的資料與以前相同,但圖表看起來更精美: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>儲存圖表

當您在本文中看到的幫助`Chart`器時,説明程式每次調用圖表時都會從頭開始重新創建圖表。 如有必要,圖表的代碼還會重新查詢資料庫或重新讀取 XML 檔以獲取數據。 在某些情況下,執行此操作可能是一個複雜的操作,例如,如果您要查詢的資料庫很大,或者 XML 檔包含大量數據。 即使圖表不涉及大量數據,動態創建圖像的過程也會佔用伺服器資源,如果許多人請求顯示圖表的頁面或頁面,也會對網站的性能產生影響。

為了幫助減少創建圖表的潛在性能影響,可以在第一次創建圖表時創建圖表,然後保存它。 當再次需要圖表時,而不是重新生成它時,只需獲取保存的版本並呈現它。

您可以透過以下方式儲存圖表:

- 將圖表緩存在計算機記憶體中(在伺服器上)。
- 將圖表另存為圖像檔。
- 將圖表另存為 XML 檔。 此選項允許您在保存圖表之前對其進行修改。

### <a name="caching-a-chart"></a>快取圖表

創建圖表後,可以緩存它。 緩存圖表意味著,如果需要再次顯示圖表,則不必重新創建圖表。 在緩存中保存圖表時,會為它提供一個必須是唯一的圖表的鍵。

如果伺服器記憶體不足,則保存到快取的圖表可能會被刪除。 此外,如果應用程式出於任何原因重新啟動,緩存將被清除。 因此,使用快取圖表的標準方法是始終檢查緩存中是否可用,如果沒有,則先創建或重新創建它。

1. 在網站的根目錄,創建一個名為*ShowCachedChart.cshtml*的檔。
2. 將現有內容取代為以下內容: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    該`<img>`標記包括`src`指向*ChartSaveToCache.cshtml*檔並將密鑰作為查詢字串傳遞到頁面的屬性。 該鍵包含「我的圖表&quot;&quot;鍵」的值。 *ChartSaveToCache.cshtml*檔案包含建立圖`Chart`表 的説明程式。 您將在一瞬間創建此頁面。

    在頁面的末尾有一個指向*名為ClearCache.cshtml*的頁面的連結。 稍後還將創建該頁面。 您只需要*ClearCache.cshtml*來測試此範例的快取 -它不是使用快取的圖表時通常包含的連結或頁面。
3. 在網站的根目錄,創建一個名為*ChartSaveToCache.cshtml*的新檔。
4. 將現有內容取代為以下內容:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    代碼首先檢查是否傳遞了任何內容作為查詢字串中的鍵值。 如果是這樣,代碼會嘗試通過調用`GetFromCache`方法並傳遞密鑰來從快取中讀取圖表。 如果事實證明該鍵下的緩存中沒有任何內容(在首次請求圖表時發生),則代碼將像往常一樣創建圖表。 圖表完成後,代碼通過調用`SaveToCache`將其保存到緩存中。 該方法需要一個鍵(以便以後可以請求圖表),以及圖表應保存在緩存中的時間量。 (快取圖表的確切時間取決於您認為圖表表示的數據可能會更改的頻率。該方法`SaveToCache`還需要一`slidingExpiration`個 參數&#8212;如果設置為 true,則每次訪問圖表時都會重置超時計數器。 在這種情況下,它實際上意味著圖表的緩存條目在上次有人訪問圖表后 2 分鐘過期。 (滑動過期的替代方法是絕對過期的,這意味著緩存條目在放入緩存后正好 2 分鐘后過期,無論訪問頻率如何。

    最後,程式碼使用`WriteFromCache`方法 從緩存中獲取和呈現圖表。 請注意,此方法位於檢查緩存`if`的塊之外,因為它將從緩存中獲取圖表,無論圖表是開始還是必須生成並保存在緩存中。

    請注意,在此示例中,`AddTitle`該方法包含時間戳。 (它將當前日期和時間&#8212;&#8212;`DateTime.Now`添加到標題中。
5. 建立名為*ClearCache.cshtml*的新頁面,並將其內容取代為以下內容:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    此頁使用`WebCache`幫助程式刪除在*ChartSaveToCache.cshtml*中快取的圖表。 如前所述,您通常不必有這樣的頁面。 您在此處創建它只是為了更輕鬆地測試快取。
6. 在瀏覽器中運行*ShowCachedChart.cshtml*網頁。 該頁面基於*ChartSaveToCache.cshtml*檔中的代碼顯示圖表圖像。 記下時間戳在圖表標題中的內容。 

    ![說明:圖表標題中帶有時間戳的基本圖表圖片](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 關閉瀏覽器。
8. 再次運行*ShowCachedChart.cshtml。* 請注意,時間戳與以前相同,表示圖表未重新生成,而是從緩存中讀取。
9. 在*ShowCachedChart.cshtml*中,按一下**清除快取**連結。 這將帶您到*ClearCache.cshtml*,它報告緩存已清除。
10. 按下 **「返回顯示快取圖表.cshtml」** 連結,或從 WebMatrix 重新執行*ShowCachedChart.cshtml。* 請注意,此時間戳已更改,因為緩存已清除。 因此,代碼必須重新生成圖表並將其放回緩存中。

### <a name="saving-a-chart-as-an-image-file"></a>儲存圖表為影像檔案

您還可以將圖表另存為伺服器上的圖像檔(例如,作為 *.jpg*檔)。 然後,您可以像使用任何圖像的方式使用圖像檔。 優點是檔被存儲而不是保存到臨時緩存。 您可以在不同時間(例如,每小時)保存新的圖表圖像,然後保留隨時間變化的永久記錄。 請注意,必須確保 Web 應用程式具有將檔案儲存到要放置圖像檔的伺服器上的資料夾的許可權。

1. 在網站的根目錄,創建名為*\_ChartFiles 的*資料夾(如果該資料夾不存在)。
2. 在網站的根目錄,創建一個名為*ChartSave.cshtml*的新檔。
3. 將現有內容取代為以下內容:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    代碼首先通過調用`File.Exists`方法檢查 *.jpg*檔是否存在。 如果檔案不存在,代碼會從陣列建立新`Chart`。 這一次,代碼調用`Save`方法並`path`傳遞 參數以指定保存圖表的位置的文件路徑和檔名。 在頁面正文中,`<img>`元素使用路徑指向要顯示的 *.jpg*檔。
4. 運行*ChartSave.cshtml*檔。
5. 返回到 WebMatrix。 請注意,名為*chart01.jpg*的圖像檔已儲存在*\_圖表檔*資料夾中。

### <a name="saving-a-chart-as-an-xml-file"></a>儲存圖表為 XML 檔

最後,您可以將圖表另存為伺服器上的 XML 檔。 使用此方法對快取圖表或將圖表保存到檔中的一個優點是,如果需要,可以在顯示圖表之前修改 XML。 應用程式必須具有要放置映像檔的伺服器上的資料夾的讀/寫許可權。

1. 在網站的根目錄,創建一個名為*ChartSaveXml.cshtml*的新檔。
2. 將現有內容取代為以下內容:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    此代碼類似於您之前在快取中儲存圖表時看到的代碼,只不過它使用 XML 檔。 代碼首先通過調用`File.Exists`方法檢查 XML 檔是否存在。 如果文件確實存在,代碼將創建一個新`Chart`物件,並將檔名`themePath`作為 參數傳遞。 這將基於 XML 檔中的任何內容建立圖表。 如果 XML 檔不存在,代碼將創建一個類似於正常圖表的圖表,然後`SaveXml`調用 以儲存它。 圖表使用 方法呈現`Write`, 如您以前看到的那樣。

    與顯示快取的頁面一樣,此代碼在圖表標題中包括時間戳。
3. 建立名為*ChartDisplayXMLChart.cshtml*的新頁面,並新增以下標記: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 運行*圖表顯示XMLChart.cshtml*頁面。 將顯示圖表。 記下圖表標題中的時間戳。
5. 關閉瀏覽器。
6. 在 WebMatrix 中,右鍵按*\_一下圖表檔*資料夾,按下 **「刷新**」,然後打開該資料夾。 此資料夾中的*XMLChart.xml*`Chart`檔案由 幫助程式創建。 

    ![說明:顯示圖表説明程式創建的 XMLChart.xml 檔的_ChartFiles資料夾。](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 再次執行*圖表顯示XMLChart.cshtml*頁面。 該圖表顯示的時間戳與首次運行頁面時的時間戳相同。 這是因為圖表是從您之前保存的 XML 生成的。
8. 在 WebMatrix 中,開啟*\_圖表檔案*資料夾並刪除*XMLChart.xml*檔案。
9. 再次執行*圖表顯示XMLChart.cshtml*頁面。 這一次,時間戳將更新,因為`Chart`幫助程式必須重新創建 XML 檔。 如果需要,請檢查*\_ChartFiles*資料夾,並注意到 XML 檔已返回。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [ASP.NET網頁網站中使用資料庫的簡介](https://go.microsoft.com/fwlink/?LinkId=202893)
- [在ASP.NET網頁網站中使用緩存以提高性能](https://go.microsoft.com/fwlink/?LinkId=202903)
- [圖表類別](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99))(ASP.NET MSDN 上的網頁 API 引用)
