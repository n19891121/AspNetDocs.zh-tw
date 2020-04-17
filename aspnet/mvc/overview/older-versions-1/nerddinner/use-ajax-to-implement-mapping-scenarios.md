---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 實現映射機制 :微軟文件
author: rick-anderson
description: 步驟 11 展示如何將 AJAX 映射支援整合到我們的 NerdDinner 應用程式中,使正在建立、編輯或查看晚餐的使用者能夠查看 l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: f2e2640eb421d5ee8006915f46cbe1090b8d21ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542582"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 實作對應實例

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第11步,該教學示範如何使用mVC 1構建小型但完整的Web應用程式ASP.NET。
> 
> 步驟 11 展示如何將 AJAX 映射支援整合到我們的 NerdDinner 應用程式中,使正在創建、編輯或查看晚餐的用戶能夠以圖形方式查看晚餐的位置。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>神經晚餐第11步:集成AJAX地圖

現在,我們將通過集成 AJAX 映射支援,使我們的應用程式在視覺上更加精彩。 這將使創建、編輯或查看晚餐的用戶能夠以圖形方式查看晚餐的位置。

### <a name="creating-a-map-partial-view"></a>建立地圖部分檢視

我們將在應用程式中的幾個位置使用映射功能。 為了保持我們的代碼 DRY,我們將將通用映射功能封裝在單個部分範本中,我們可以在多個控制器操作和視圖中重複使用。 我們將此部分檢視命名為"map.ascx",並在[Views_Dinners] 目錄中創建它。

我們可以通過右鍵單擊「視圖\Dinners」目錄並選擇「添加視圖&gt;」功能表命令來創建 map.ascx 部分內容。 我們將檢視命名為「Map.ascx」,將其作為部分檢視選中,並指示我們將通過一個強類型「Dinner」模型類:

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

當我們按下「添加」按鈕時,將創建部分範本。 然後,我們將更新 Map.ascx 檔,以包含以下內容:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一&lt;個&gt;腳本引用指向 Microsoft 虛擬地球 6.2 映射庫。 第二&lt;&gt;個 文稿引用指向我們即將創建的 map.js 檔,該檔將封裝我們常見的 Javascript 映射邏輯。 div &lt;id="theMap"&gt;元素是虛擬地球將用來承載地圖的 HTML 容器。

然後,我們有一個&lt;嵌入&gt;式 腳本塊,其中包含特定於此視圖的兩個 JavaScript 函數。 第一個函數使用 jQuery 來連接在頁面準備好運行用戶端文本時執行的函數。 它調用 LoadMap() 説明器函數,我們將在 Map.js 文本檔中定義該函數以載入虛擬地球地圖控制項。 第二個函數是回調事件處理程式,該處理程式向標識位置的地圖添加引腳。

請注意,如何在用戶端腳本塊中使用伺服器端&lt;%+%&gt;塊來嵌入要映射到 JAVAScript 的 Dinner 的緯度和經度。 這是一種有用的技術來輸出用戶端文本可以使用的動態值(無需單獨的 AJAX 調用伺服器即可檢索值 , 使其更快)。 &lt;當檢視在伺服器上&gt;呈現時,%= % 塊將執行 ,因此 HTML 的輸出將最終使用嵌入的 JavaScript 值(例如:var 緯度 = 47.64312;)。

### <a name="creating-a-mapjs-utility-library"></a>建立 Map.js 公用程式庫

現在,讓我們創建 Map.js 檔,可用於封裝地圖的 JavaScript 功能(並實現上面的 LoadMap 和 LoadPin 方法)。 我們可以通過右鍵單擊專案中的 #Scripts 目錄來執行此操作,然後選擇「&gt;添加新 專案」功能表命令,選擇 JScript 項,並將其命名為"Map.js"。

下面是我們將添加到 Map.js 檔的 JavaScript 代碼,該代碼將與虛擬地球互動以顯示我們的地圖,並為其添加位置圖釘以進行晚餐:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>將地圖與建立及編輯表單整合

現在,我們將 Map 支援與現有的創建和編輯方案集成。 好消息是,這是很容易做到的,並且不需要我們更改任何控制器代碼。 由於我們的「創建」和「編輯」視圖共用一個通用的「DinnerForm」部分視圖來實現晚餐表單 UI,因此我們可以在一個位置添加地圖,並同時使用我們的「創建」 和「編輯」 方案。

我們只需要打開 [Views_Dinners_DinnerForm.ascx 部分視圖]並更新它,以包括我們的新地圖部分。 下面是添加地圖後更新的 DinnerForm 的外觀(注意:為了簡潔起見,下面代碼段省略了 HTML 表單元素):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上面的 DinnerForm 部分將類型為「DinnerFormViewModel」的物件作為其模型類型(因為它既需要 Dinner 物件,也需要 SelectList 來填充國家/地區的下拉清單)。 我們的地圖部分只需要一個類型「Dinner」的物件作為其模型類型,因此當我們渲染地圖部分時,我們只傳遞給 DinnerFormViewModel 的 Dinner 子屬性:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我們添加到部分使用的 JavaScript 函數使用 jQuery 將「模糊」事件附加到「位址」HTML 文本框。 您可能聽說過當使用者按下或選項卡進入文本框時觸發的「焦點」 事件。 相反,當使用者退出文本框時,將觸發"模糊"事件。 上述事件處理程式在發生此情況時清除緯度和經度文本框值,然後繪製地圖上的新位址位置。 然後,我們在 map.js 檔中定義的回調事件處理程式將使用虛擬地球返回的值更新窗體上的經度和緯度文本框,具體取決於我們提供的位址。

現在,當我們再次運行我們的應用程式,然後單擊「主機晚餐」選項卡,我們將看到默認地圖顯示連同我們的標準晚餐表單元素:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

當我們鍵入位址,然後選項卡離開時,地圖將動態更新以顯示位置,並且事件處理程式將用位置值填充緯度/經度文本框:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果我們保存新晚餐,然後再次打開它進行編輯,我們會發現在頁面載入時顯示地圖位置:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次更改位址欄位時,地圖和緯度/經度座標都將更新。

現在,地圖顯示「晚餐」位置,我們還可以將「緯度和經度」窗體欄位從可見文本框更改為隱藏元素(因為每次輸入位址時,地圖都會自動更新它們)。 此,我們將從使用 Html.TextBox() HTML 說明程式切換到使用 Html.Hidden() 說明器方法:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

現在,我們的表單更加方便使用者,避免顯示原始緯度/經度(同時仍將其與資料庫中的每個晚餐一起存儲):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>將地圖與詳細資訊檢視整合

現在,我們已經將地圖與我們的創建和編輯方案集成,讓我們也將其與我們的詳細資訊方案集成。 我們只需要調用&lt;% Html.Render 部分("地圖");"&gt;詳細資訊"視圖中的百分比。

下面是完整詳細資訊檢視的原始碼(具有地圖整合)的外觀:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

現在,當用戶導航到 /Dinners/細節/[id] URL 時,他們將看到有關晚餐的詳細資訊、地圖上的晚餐位置(隨滑鼠懸停在地圖上的圖釘顯示晚餐的標題和位址),併為其提供指向 RSVP 的 AJAX 連結:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在資料庫與儲存庫中實現位置搜尋

為了完成我們的AJAX實現,讓我們向應用程式的主頁添加一個地圖,允許使用者以圖形方式搜索附近的晚餐。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

我們將首先在資料庫和數據存儲庫層中實施支援,以高效地執行基於位置的 Dinner 半徑搜索。 我們可以使用 SQL [2008 的新地理空間功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)來實現這一點,或者我們可以使用 Gary Dryden 在本文中討論的 SQL 函數方法:Rob [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) Conery 會在這裡寫關於使用 LINQ 到 SQL 的文章:[http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

為了實現此技術,我們將在 Visual Studio 中打開「伺服器資源管理器」,選擇NerdDinner資料庫,然後右鍵單擊其下的「函數」子節點,然後選擇創建新的「Scalar 值函數」:

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

然後,我們將粘貼到以下距離之間函數中:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

然後,我們將在 SQL Server 中創建一個新的表值函數,我們稱之為「最近的晚餐」:

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

此「最近的晚餐」表函數使用距離之間的幫助器功能返回我們提供它的自由經 100 英里內的所有晚餐:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

要呼叫此函數,我們將首先透過按兩下我們的#Model目錄中的NerdDinner.dbml檔向SQL設計器打開LINQ:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

然後,我們將最近 Dinner 和距離之間的函數拖動到 LINQ 到 SQL 設計器,這將導致它們作為 LINQ 上的方法添加到 SQL NerdDinnerDataContext 類:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

然後,我們可以在我們的 DinnerRepository 類中公開「FindByLocation」查詢方法,該方法使用「最近 Dinner」功能返回即將在指定位置 100 英里範圍內的晚餐:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>實現基於JSON的AJAX搜尋操作方法

現在,我們將實現一個控制器操作方法,該方法利用新的 FindByLocation() 儲存庫方法返回可用於填充地圖的 Dinner 數據清單。 我們將讓此操作方法以 JSON(JavaScript 物件表示法)格式返回 Dinner 數據,以便可以輕鬆地在用戶端上使用 JAvaScript 對其進行操作。

為了實現這一點,我們將通過右鍵單擊 \控制器目錄並選擇"添加控制&gt;器 "功能表命令創建新的"SearchController"類。 然後,我們將在新的 SearchController 類中實現「搜索ByLocation」操作方法,如下所示:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 的 SearchByLocation 操作方法在內部調用晚餐存儲庫上的 FindByLocation 方法,以獲取有關附近晚餐的清單。 但是,它不是將 Dinner 物件直接返回給用戶端,而是返回 JsonDinner 物件。 JsonDinner 類公開了 Dinner 屬性的子集(例如:出於安全原因,它不披露有 RSVP d 的晚餐人員的姓名)。 它還包括一個在晚餐上不存在的 RSVPCount 屬性,該屬性通過計算與特定晚餐關聯的 RSVP 物件數進行動態計算。

然後,我們使用 Controller 基類上的 Json() 説明器方法使用基於 JSON 的線格式返回晚餐序列。 JSON 是一種標準文本格式,用於表示簡單的數據結構。 下面是從操作方法返回時由 JSON 格式為兩個 JsonDinner 物件的清單的範例:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>使用 jQuery 呼叫基於 JSON 的 AJAX 方法

現在,我們準備更新NerdDinner應用程式的主頁,以使用搜索控制器的搜索ByLocation操作方法。 為此,我們將打開 /Views/Home/Index.aspx 檢視範本並更新該範本,使其具有文本框、搜索按鈕、地圖和名為 dinnerList 的&lt;&gt;div 元素:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

然後,我們可以向頁面添加兩個 JavaScript 函數:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

當頁面首次載入時,第一個 JavaScript 函數載入地圖。 第二個 JavaScript 函數在搜索按鈕上連接了 JavaScript 單擊事件處理程式。 按下按鈕後,它將調用 FindDinnersGivenLocation() JavaScript 函數,我們將該函數添加到我們的 Map.js 檔中:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

此查找晚餐給定位置() 函數調用映射。在虛擬地球控制上查找()以將其居於輸入的位置。 當虛擬地球地圖服務返回時,地圖。Find() 方法調用回調UpdateMapDinners回調方法,我們將其作為最後參數傳遞。

回調UpdateMapDinners()方法是完成實際工作的地方。 它使用 jQuery 的 $.post() 説明器方法對我們的 SearchController 的 SearchByLocation() 操作方法執行 AJAX 調用 - 傳遞新居中地圖的緯度和經度。 它定義了一個內聯函數,將在 $.post() 説明器方法完成時調用,並且從 SearchByLocation() 操作方法返回的 JSON 格式的晚餐結果將使用名為"dinners"的變數傳遞它。 然後,它在每個返回的晚餐上做一個foron,並使用晚餐的緯度和經度和其他屬性在地圖上添加新的圖釘。 它還在地圖右側的 HTML 晚餐清單中添加了一個晚餐條目。 然後,它會為圖釘和 HTML 清單啟用懸停事件,以便在使用者懸停在它們上時顯示有關晚餐的詳細資訊:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

現在,當我們運行應用程式並訪問主頁時,我們將顯示一張地圖。 當我們輸入城市名稱時,地圖將顯示附近即將舉辦的晚宴:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

懸停在晚餐上將顯示有關它的詳細資訊。

按下氣泡中的晚餐標題或在 HTML 清單中的右側將引導我們前往晚宴 - 然後,我們可以選擇 RSVP 進行以下操作:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>後續步驟

現在,我們已經實現了NerdDinner應用程式的所有應用程式功能。 現在,讓我們來看看如何實現自動單元測試。

> [!div class="step-by-step"]
> [前一個](use-ajax-to-deliver-dynamic-updates.md)
> [下一個](enable-automated-unit-testing.md)
