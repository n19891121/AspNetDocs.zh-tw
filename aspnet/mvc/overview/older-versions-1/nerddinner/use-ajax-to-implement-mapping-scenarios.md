---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 來執行對應案例 |Microsoft Docs
author: rick-anderson
description: 步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓正在建立、編輯或查看 dinners 的使用者查看 .。。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 03b3a27d4b761d0417160b95cc6f39a345385065
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044320"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 實作對應實例

由 [Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md) 課程的步驟11，逐步解說如何使用 ASP.NET MVC 1 建立小型但完整的 web 應用程式。
> 
> 步驟11顯示如何將 AJAX 對應支援整合到我們的 NerdDinner 應用程式，讓建立、編輯或觀賞 dinners 的使用者以圖形方式查看晚餐的位置。
> 
> 如果您使用的是 ASP.NET MVC 3，建議您遵循 [mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 或 [mvc 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 教學課程的消費者入門。

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner 步驟11：整合 AJAX 地圖

我們現在藉由整合 AJAX 對應支援，讓應用程式更具視覺效果。 這可讓正在建立、編輯或查看 dinners 的使用者以圖形方式查看晚餐的位置。

### <a name="creating-a-map-partial-view"></a>建立地圖部分視圖

我們將在應用程式內的數個地方使用對應功能。 為了讓我們的程式碼更好，我們會將常見的地圖功能封裝在單一部分範本中，以便在多個控制器動作和 views 之間重複使用。 我們會將這個部分 view 命名為 "map .ascx"，並在 \Views\Dinners 目錄中建立它。

只要以滑鼠右鍵按一下 \Views\Dinners 目錄，然後選擇 [加入視圖] 功能表命令，就可以建立對應的 .ascx 部分 &gt; 。 我們會將 view 命名為「對應 .ascx」、將它視為部分視圖，並指出我們要將它傳遞給它一個強型別「晚餐」模型類別：

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

當我們按一下 [新增] 按鈕時，將會建立部分範本。 接著，我們會更新對應的 .ascx 檔案，使其具有下列內容：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一個 &lt; 腳本 &gt; 參考會指向 Microsoft 虛擬地球6.2 對應程式庫。 第二個 &lt; 腳本 &gt; 參考會指向稍後將建立的 map.js 檔案，以封裝我們的常見 JAVAscript 對應邏輯。 &lt;Div id = "theMap" &gt; 元素是虛擬地球將用來裝載地圖的 HTML 容器。

接著，我們會有一個內嵌 &lt; &gt; 的腳本區塊，其中包含這個視圖專屬的兩個 JavaScript 函式。 第一個函式會使用 jQuery 來連接在頁面準備執行用戶端腳本時所執行的函式。 它會呼叫 LoadMap ( # A1 helper 函式，我們會在 Map.js 腳本檔中定義，以載入虛擬地球地圖控制項。 第二個函式是回呼事件處理常式，會將釘選新增至識別位置的地圖。

請注意，我們如何在 &lt; 用戶端腳本區塊內使用伺服器端% =% &gt; 區塊，以將我們想要對應的晚餐的緯度和經度內嵌至 JavaScript。 這是一項實用的技巧，可輸出用戶端腳本所能使用的動態值 (而不需要對伺服器進行個別的 AJAX 回呼來取得值，這可讓您更快速地) 。 當您在 &lt; &gt; 伺服器上轉譯視圖時，將會執行% =% 區塊，因此 HTML 的輸出最後會是內嵌的 JavaScript 值 (例如： var 緯度 = 47.64312; ) 。

### <a name="creating-a-mapjs-utility-library"></a>建立 Map.js 公用程式程式庫

現在，讓我們建立 Map.js 檔案，以用來封裝對應 (的 JavaScript 功能，並執行上述) 的 LoadMap 和 LoadPin 方法。 若要這麼做，請以滑鼠右鍵按一下專案中的 [\Scripts] 目錄，然後選擇 [加入 &gt; 新專案] 功能表命令，選取 [JScript] 專案，並將其命名為 "Map.js"。

以下是我們將在 Map.js 檔案中新增的 JavaScript 程式碼，以與虛擬地球互動以顯示我們的地圖，並為我們的 dinners 新增位置圖釘：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>整合地圖與建立和編輯表單

我們現在會將地圖支援與現有的建立和編輯案例整合。 好消息是，這相當簡單，而且不需要我們變更任何控制器程式碼。 由於我們的 [建立] 和 [編輯] 視圖會共用常見的「DinnerForm」部分視圖來實行晚餐表單 UI，因此我們可以在一個位置新增地圖，並讓我們的建立和編輯案例都使用它。

我們只需要開啟 \Views\Dinners\DinnerForm.ascx 部分視圖，並加以更新，以包含新的地圖部分。 以下是在新增對應之後，更新的 DinnerForm 會顯示的樣子 (注意：下列程式碼片段會省略 HTML 表單元素，以求簡潔) ：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上述 DinnerForm 部分會採用類型為 "DinnerFormViewModel" 的物件做為其模型類型 (因為它同時需要晚餐物件和 SelectList 來填入) 的國家/地區 dropdownlist。 我們的地圖部分只需要 "晚餐" 類型的物件作為其模型類型，因此當我們轉譯地圖部分時，我們只會將 DinnerFormViewModel 的晚餐子屬性傳遞給它：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我們已新增至部分的 JavaScript 函式會使用 jQuery 將「模糊」事件附加至「位址」 HTML 文字方塊。 您可能聽過使用者在文字方塊中按一下或定位點時所引發的「焦點」事件。 相反的是當使用者離開 textbox 時引發的「模糊」事件。 上述事件處理常式會在發生這種情況時清除緯度和經度 textbox 的值，然後在地圖上繪製新的位址位置。 接著，我們在 map.js 檔案中定義的回呼事件處理常式，將會根據我們提供的位址，使用虛擬地球所傳回的值，更新表單上的經度和緯度文字方塊。

現在當我們再次執行應用程式，並按一下 [主機晚餐] 索引標籤時，就會看到預設的地圖與標準晚餐表單元素一起顯示：

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

當我們輸入位址，然後使用 tab 鍵移出時，地圖會動態更新以顯示位置，而我們的事件處理常式會將位置值填入緯度/經度文字方塊中：

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果我們儲存新晚餐，然後再次開啟以供編輯，我們會發現在頁面載入時，會顯示地圖位置：

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次變更 [位址] 欄位時，地圖和緯度/經度座標將會更新。

現在地圖顯示晚餐位置，我們也可以將 [緯度] 和 [經度] 表單欄位從 [可見的] 文字方塊改成隱藏元素 (因為地圖會在每次輸入位址) 時自動更新。 為此，我們將使用 Html ( # A1 HTML helper 來切換為使用 Html. Hidden ( # A3 helper 方法：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

現在我們的表單更容易使用，並避免顯示原始的緯度/經度 (但仍將它們儲存在資料庫) 中的每個晚餐：

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>將地圖與詳細資料檢視整合

既然我們已將地圖與我們的建立和編輯案例整合，讓我們也將它與我們的詳細資料案例整合。 我們只需要在 &lt; &gt; 詳細資料檢視中呼叫% Html. RenderPartial ( "map" ) ;%。

以下是對應整合)  (完整詳細資料檢視的原始程式碼如下所示：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

現在，當使用者流覽至/Dinners/Details/[id] URL 時，他們會看到晚餐的詳細資料，地圖上的晚餐的位置 (完成時，會在滑鼠停留時顯示晚餐的標題和其) 的位址，並具有適用于其回復的 AJAX 連結：

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在資料庫和儲存機制中執行位置搜尋

為了完成我們的 AJAX 程式，讓我們將地圖新增至應用程式的首頁，讓使用者以圖形方式搜尋附近的 dinners。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

我們一開始會在資料庫和資料存放庫層中執行支援，以有效率地執行以位置為基礎的 radius 搜尋以進行 Dinners。 我們可以使用 [sql 2008 的新地理空間功能](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) 來執行這項操作，也可以使用 sql 函式方法來 Dryden 本文中所討論的專案， [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) 並使用與 LINQ to SQL 的 Conery 網友： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

為了執行這項技術，我們會在 Visual Studio 中開啟「伺服器總管」，選取 NerdDinner 資料庫，然後以滑鼠右鍵按一下其下的「函式」子節點，並選擇建立新的「純量值函式」：

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

接著，我們會貼上下列 DistanceBetween 函數：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

接著，我們會在 SQL Server 中建立新的資料表值函式，我們將會呼叫 "NearestDinners"：

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

這個 "NearestDinners" 資料表函數會使用 DistanceBetween helper 函式，以傳回在100英里內的所有 Dinners，以及我們提供的緯度和經度：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

為了呼叫這個函式，我們會先按兩下 \Models 目錄中的 NerdDinner 檔案，以開啟 LINQ to SQL 設計工具：

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

接著，我們會將 NearestDinners 和 DistanceBetween 函式拖曳至 LINQ to SQL 設計工具，這會在我們的 LINQ to SQL NerdDinnerDataCoNtext 類別中新增為方法：

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

接著，我們可以在 DinnerRepository 類別上公開 "FindByLocation" 查詢方法，該方法會使用 NearestDinner 函式來傳回在指定位置100英里內的即將到來 Dinners：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>執行以 JSON 為基礎的 AJAX 搜尋動作方法

我們現在會採用控制器動作方法，以利用新的 FindByLocation ( # A1 儲存機制方法來傳回可用來填入地圖的晚餐資料清單。 我們會讓此動作方法傳回 JSON (中的晚餐資料 JavaScript 物件標記法) 格式，讓您可以在用戶端使用 JavaScript 輕鬆地操作。

為了執行此操作，我們將建立新的 "SearchController" 類別，方法是以滑鼠右鍵按一下 \Controllers 目錄，然後選擇 [加入 &gt; 控制器] 功能表命令。 接著，我們將在新的 SearchController 類別內執行 "SearchByLocation" 動作方法，如下所示：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController 的 SearchByLocation 動作方法會在內部呼叫 DinnerRepository 上的 FindByLocation 方法，以取得鄰近 dinners 的清單。 但是，它會改為傳回 JsonDinner 物件，而不是直接將晚餐物件傳回給用戶端。 JsonDinner 類別會公開晚餐屬性的子集 (例如：基於安全性理由，不會洩漏晚餐) 的員工姓名。 它也包含在晚餐上不存在的 RSVPCount 屬性，而且是透過計算與特定晚餐相關聯的 RSVP 物件數目動態計算。

接著，我們會在控制器基類上使用 Json ( # A1 helper 方法，以使用以 JSON 為基礎的電傳格式傳回 dinners 序列。 JSON 是代表簡單資料結構的標準文字格式。 以下是兩個 JsonDinner 物件的 JSON 格式清單在從動作方法傳回時的樣子：

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.txt)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>使用 jQuery 呼叫以 JSON 為基礎的 AJAX 方法

我們現在已準備好更新 NerdDinner 應用程式的首頁，以使用 SearchController 的 SearchByLocation 動作方法。 為了達成此目的，我們將開啟/Views/Home/Index.aspx view 範本並加以更新，使其具有 textbox、搜尋按鈕、地圖，以及 &lt; &gt; 名為 dinnerList 的 div 元素：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

接著，我們可以將兩個 JavaScript 函式新增至頁面：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

第一個 JavaScript 函式會在頁面第一次載入時載入對應。 第二個 JavaScript 函式會在 [搜尋] 按鈕上，將 JavaScript click 事件處理常式上線。 按下按鈕時，會呼叫 FindDinnersGivenLocation ( # A1 JavaScript 函式，我們會將其新增至 Map.js 檔案：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

這個 FindDinnersGivenLocation ( # A1 函式呼叫 map。在虛擬地球控制項上尋找 ( # A3，以將其置入所輸入的位置。 當虛擬地球地圖服務傳回時，即為對應。Find ( # A1 方法會叫用 callbackUpdateMapDinners 回呼方法，並將其傳遞為最後的引數。

CallbackUpdateMapDinners ( # A1 方法是執行實際工作的地方。 它使用 jQuery 的 $. post ( # A1 helper 方法來對 SearchController 的 SearchByLocation ( # A3 動作方法執行 AJAX 呼叫，將其傳遞至新置中地圖的緯度和經度。 它定義了當 $. post ( # A1 helper 方法完成時所呼叫的內嵌函式，以及從 SearchByLocation ( # A3 動作方法傳回的 JSON 格式晚餐結果，將會使用名為 "dinners" 的變數來傳遞。 然後，它會對每個傳回的晚餐進行 foreach，然後使用晚餐的緯度和經度和其他屬性在地圖上新增新的釘選。 它也會將晚餐專案加入至地圖右邊的 dinners HTML 清單。 然後，它會將圖釘和 HTML 清單的暫留事件線線上，以便在使用者停留時顯示晚餐的詳細資料：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

現在當我們執行應用程式並流覽首頁時，我們會看到地圖。 當我們輸入城市的名稱時，地圖將會顯示即將推出的 dinners：

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

將滑鼠停留在晚餐上方會顯示其詳細資料。

按一下 [反升] 或 [HTML] 清單右邊的晚餐標題，就會將我們移至晚餐，讓我們可以選擇性地回復：

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>後續步驟

我們現在已實現 NerdDinner 應用程式的所有應用程式功能。 現在讓我們來看看如何啟用它的自動化單元測試。

> [!div class="step-by-step"]
> [上一個](use-ajax-to-deliver-dynamic-updates.md) 
> [下一步](enable-automated-unit-testing.md)
