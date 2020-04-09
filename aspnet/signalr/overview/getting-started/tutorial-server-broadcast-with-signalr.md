---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教程:使用 SignalR 2 進行伺服器廣播 |微軟文件
author: tdykstra
description: 本教學示範如何建立使用ASP.NET SignalR 2 提供伺服器廣播功能的 Web 應用程式。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676094"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>教學:使用 SignalR 2 進行伺服器廣播

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

本教學示範如何建立使用ASP.NET SignalR 2 提供伺服器廣播功能的 Web 應用程式。 伺服器廣播意味著伺服器啟動發送到用戶端的通信。

您將在本教學中創建的應用程式類比股票代碼,這是伺服器廣播功能的典型方案。 伺服器定期隨機更新股票價格並將更新廣播給所有連接的用戶端。 在瀏覽器中,"更改"和 **"** 列"中的數位**%** 和符號會動態更改,以回應來自伺服器的通知。 如果打開其他瀏覽器到同一 URL,它們都同時顯示相同的數據和對數據的相同更改。

![建立 Web](tutorial-server-broadcast-with-signalr/_static/image1.png)

在本教學課程中，您：

> [!div class="checklist"]
> * 建立專案
> * 設定伺服器程式碼
> * 檢查伺服器代碼
> * 設定客戶端碼
> * 檢查客戶端碼
> * 測試應用程式
> * 啟用記錄

> [!IMPORTANT]
> 如果不想完成構建應用程式的步驟,可以在新的空ASP.NET Web 應用程式專案中安裝 SignalR.sample 包。 如果不執行本教程中的步驟,安裝 NuGet 包,則必須按照*readme.txt*檔中的說明進行操作。 要執行套件,您需要添加一個 OWIN 啟動`ConfigureSignalR`類, 該類調用已安裝套件中的方法。 如果不添加 OWIN 啟動類,您將收到錯誤。 請參閱本文[的「安裝庫存價格」示例](#install-the-stockticker-sample)部分。

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。

## <a name="create-the-project"></a>建立專案

本節演示如何使用 Visual Studio 2017 創建空ASP.NET Web 應用程式。

1. 在可視化工作室中,創建一個ASP.NET Web 應用程式。

    ![建立 Web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 在新**ASP.NET Web 應用程式 - SignalR.StockTicker**視窗中,保留 **「空**」並選擇 **「確定**」 。

## <a name="set-up-the-server-code"></a>設定伺服器程式碼

在本節中,您可以設置在伺服器上運行的代碼。

### <a name="create-the-stock-class"></a>建立"庫存'類別

首先創建用於存儲和傳輸庫存資訊*的Stock*模型類。

1. 在**解決方案資源管理器**中,右鍵單擊專案並選擇 **「添加** > **類**」。

1. 命名類*Stock*並將其添加到專案中。

1. 將*Stock.cs*檔案的代碼取代為以下代碼:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    建立股票時要設定的兩個屬性是`Symbol`(例如,微軟的 MSFT)和`Price`。 其他屬性取決於設置`Price`的方式和時間。 第一次設定`Price`時,值將傳播到`DayOpen`。 `Price`之後,當您設置 時,應用根據`Change``PercentChange``Price``DayOpen`和之間的差異計算和 屬性值。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>建立股票價格中心和股票提克類

您將使用 SignalR 中心 API 來處理伺服器到用戶端的互動。 派生`StockTickerHub`自 SignalR`Hub`類的類將處理來自用戶端的接收連接和方法調用。 您必須維護庫存資料並執行物件`Timer`。 該`Timer`物件將定期觸發獨立於用戶端連接的價格更新。 不能將這些函數放在`Hub`類中,因為中心是瞬態的。 應用為中心中的每個`Hub`任務創建一個類實例,例如從用戶端到伺服器的連接和調用。 因此,保存庫存數據、更新價格和廣播價格更新的機制必須運行在單獨的類中。 您將命名此類別`StockTicker`。

![從斯托克蒂克廣播](tutorial-server-broadcast-with-signalr/_static/image3.png)

您只需要在伺服器上執行類的`StockTicker`一個實例,因此您需要設置從每個`StockTickerHub`實例到 singleton`StockTicker`實例的引用。 類`StockTicker`必須廣播給客戶端,因為它具有股票數據並觸發更新,`StockTicker``Hub`但不是類。 類`StockTicker`必須獲取對 SignalR 中心連接上下文物件的引用。 然後,它可以使用 SignalR 連接上下文物件廣播到用戶端。

#### <a name="create-stocktickerhubcs"></a>建立StockTickerHub.cs

1. 在**解決方案資源管理器**中,右鍵單擊專案並**Add** > 選擇「**添加新項**」。

1. 新增**新項目 - SignalR.StockTicker**中,選擇 **「已安裝** > **的視覺 C#** > **Web** > **訊號R」,** 然後選擇**訊號 R 集線器類別 (v2)。**

1. 命名類*StockTickerHub*並將其添加到專案中。

    此步驟將創建*StockTickerHub.cs*類檔。 同時,它將一組支援 SignalR 的文稿檔和程式集引用添加到專案中。

1. 將*StockTickerHub.cs*檔案中的代碼取代為以下代碼:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 儲存檔案。

應用使用[Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類定義客戶端可以在伺服器上調用的方法。 您正在定義方法: `GetAllStocks()`。 當用戶端最初連接到伺服器時,它將調用此方法來獲取所有股票及其當前價格的清單。 該方法可以同步運行並返回`IEnumerable<Stock>`,因為它正在從記憶體返回數據。

如果方法必須通過執行涉及等待(如資料庫查找或 Web 服務調用)來獲取數據,則`Task<IEnumerable<Stock>>`可以指定為返回值以啟用非同步處理。 有關詳細資訊,請參閱[ASP.NET 訊號 R 集線器 API 指南 - 伺服器 - 何時非同步執行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。

該`HubName`屬性指定應用如何在用戶端上的 JavaScript 代碼中引用 Hub。 如果不使用此屬性,用戶端上的預設名稱是類別名稱的 camelCase 版本,在這種情況下,該`stockTickerHub`版本為 。

稍後在創建`StockTicker`類時將看到,應用在其靜`Instance`態 屬性中創建該類的單例實例。 無論連接或斷開連接的`StockTicker`用戶端數,該單例實例都位於記憶體中。 該實例是`GetAllStocks()`該方法用於返回當前庫存資訊的方法。

#### <a name="create-stocktickercs"></a>建立StockTicker.cs

1. 在**解決方案資源管理器**中,右鍵單擊專案並選擇 **「添加** > **類**」。

1. 命名類*StockTicker*並將其添加到專案中。

1. 將*StockTicker.cs*檔案中的代碼取代為以下代碼:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

由於所有線程都將運行同一個 StockTicker 代碼實例,因此 StockTicker 類必須具有線程安全。

### <a name="examine-the-server-code"></a>檢查伺服器代碼

如果檢查伺服器代碼,它將説明您瞭解應用的工作原理。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>將單例實體儲存在靜態欄位

代碼初始化使用類的實例`_instance``Instance`支援 屬性的靜態欄位。 由於構造函數是私有的,因此它是應用可以創建的唯一類實例。 套用`_instance`對欄位使用[延遲初始化](/dotnet/framework/performance/lazy-initialization)。 這不是出於性能原因。 它確保實例創建是線程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

每次用戶端連接到伺服器時,在單獨的線程中運行的 StockTickerHub 類的新實`StockTicker.Instance`例從 靜態屬性獲取 StockTicker 單例實`StockTickerHub`例,如您在 類中前面看到的。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>儲存庫存資料儲存在併發字典中

建構函數使用一些樣本庫存`_stocks`數據初始化集合,並`GetAllStocks`返回數據。 如前所述,此股票集合由返回`StockTickerHub.GetAllStocks`,這是用戶端可以調用的類`Hub`中的 伺服器方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

出於線程安全,股票集合定義為[併發字典](https://msdn.microsoft.com/library/dd287191.aspx)類型。 作為替代方法,您可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)物件,並在對字典進行更改時顯式鎖定字典。

對於此示例應用程式,可以將應用程序數據存儲在記憶體中,並在應用釋放`StockTicker`實例時丟失數據。 在實際應用程式中,您將像資料庫一樣使用後端數據存儲。

#### <a name="periodically-updating-stock-prices"></a>定期更新股票價格

建構函數啟動一個`Timer`物件,該物件定期調用隨機更新股票價格的方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`呼叫`UpdateStockPrices`, 在狀態參數中傳遞為 null。 在更新價格之前,應用會鎖定`_updateStockPricesLock`物件。 代碼檢查另一個線程是否已更新價格,然後調用`TryUpdateStockPrice`清單中的每個股票。 該方法`TryUpdateStockPrice`決定是否更改股票價格,以及更改多少股票價格。 如果股票價格發生變化,應用將調用`BroadcastStockPrice`向所有連接的用戶端廣播股票價格變化。

指定`_updatingStockPrices`[易失性](https://msdn.microsoft.com/library/x13ttww7.aspx)的標誌,以確保它是線程安全的。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

在實際應用程式中,`TryUpdateStockPrice`該方法將調用 Web 服務來查找價格。 在此代碼中,應用程式使用隨機數生成器隨機進行更改。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>取得 SignalR 中文,以便 StockTicker 類別可以廣播給用戶端

由於價格變化源自物件,`StockTicker`因此需要在所有連接的用戶端上調`updateStockPrice`用 方法的物件。 在類`Hub`中,您有用於調用用戶端方法的 API,`StockTicker`但不派`Hub`生自類 ,`Hub`並且沒有對任何 物件的引用。 要廣播到已連接的用戶端`StockTicker`,類必須`StockTickerHub`獲取 類的 SignalR 上下文實例,並用它來調用用戶端上的方法。

當代碼創建單例類實例、傳遞該引用到構造函數時獲取對 SignalR 上下`Clients`文的引用,構造函數將其放入屬性中。

您只想獲取上下文一次的原因有兩個:獲取上下文是一項昂貴的任務,一次獲取上下文可確保應用保留發送到用戶端的消息的預期順序。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

通過取得`Clients`內容的屬性並將其放入屬性,`StockTickerClient`可以編寫代碼來呼叫`Hub`與類中看起來相同的用戶端方法。 例如,要廣播到所有用戶端,您可以寫入`Clients.All.updateStockPrice(stock)`。

您`updateStockPrice`呼`BroadcastStockPrice`叫的方法尚不存在。 稍後,當您編寫在用戶端上運行的代碼時,將添加它。 您可以在此處引用,`updateStockPrice``Clients.All`因為 是動態的,這意味著應用將在運行時計算運算式。 執行此方法調用時,SignalR 將向用戶端發送方法名稱和參數值,如果用戶端具有`updateStockPrice`名為的方法,則應用將調用該方法並將參數值傳遞給用戶端。

`Clients.All`表示發送到所有用戶端。 SignalR 為您提供了其他選項來指定要發送到的用戶端或用戶端群組。 有關詳細資訊,請參閱[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>註冊訊號R路由

伺服器需要知道要攔截哪個 URL 並定向到 SignalR。 為此,添加 OWIN 啟動類:

1. 在**解決方案資源管理器**中,右鍵單擊專案並**Add** > 選擇「**添加新項**」。

1. 在 **'新增新項目 - SignalR.StockTicker' 中選擇****' 已安裝** > **的視覺化 C#** > **Web"** 然後選擇**OWIN 啟動類別**。

1. 命名類 *「啟動」* 並選擇 **「確定**」。

1. 將*Startup.cs*檔案中的預設代碼取代此代碼:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

您現在已完成伺服器代碼的設置。 在下一節中,您將設置用戶端。

## <a name="set-up-the-client-code"></a>設定客戶端碼

在本節中,設置在用戶端上運行的代碼。

### <a name="create-the-html-page-and-javascript-file"></a>建立 HTML 頁面與 JavaScript 檔案

HTML 頁面將顯示數據,JAVAScript 檔案將組織數據。

#### <a name="create-stocktickerhtml"></a>建立股票Ticker.html

首先,您將添加 HTML 用戶端。

1. 在**解決方案資源管理員**中,右鍵單擊專案並選擇「**添加** > **HTML 頁面**」 。。

1. 命名檔案*庫存Ticker*並選擇 **「確定**」。

1. 將*StockTicker.html*檔案中的預設代碼取代為以下代碼:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML 創建一個包含五列的表、一個標題行和一個包含一個跨所有五列的單元格的數據行。 數據行顯示"載入..."當應用程式啟動時,瞬間。 JavaScript 代碼將刪除該行,並在其位置添加從伺服器檢索的股票數據行。

    文稿標記指定:

    * jQuery 文本檔。

    * SignalR 核心文本檔。

    * SignalR 代理文本檔。

    * 稍後將創建的 StockTicker 文稿檔。

    應用程式動態生成 SignalR 代理文本檔。 它指定"/信號器/集線器"URL,併為 的 Hub 類(本例中)`StockTickerHub.GetAllStocks`為 定義方法的代理方法。 如果您願意,可以使用[SignalR 實用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手動生成此 JavaScript 檔。 不要忘記在方法調用中`MapHubs`禁用動態文件創建。

1. 在**解決方案資源管理員中**,展開**文稿**。

    jQuery 和 SignalR 的文本庫在項目中可見。

    > [!IMPORTANT]
    > 包管理器將安裝更高版本的 SignalR 腳本。

1. 更新代碼塊中的腳本引用,以對應於專案中的腳本檔版本。

1. 在**解決方案資源管理器**中,右鍵按*一下 StockTicker.html*,然後選擇 **「設定為起始頁**」 。。

#### <a name="create-stocktickerjs"></a>建立庫存Ticker.js

現在創建 JavaScript 檔案。

1. 在**解決方案資源管理員**中,右鍵單擊專案並選擇 **「添加** > **JAvaScript 檔案**」。。

1. 命名檔案*庫存Ticker*並選擇 **「確定**」。

1. 將此代碼加入*StockTicker.js*檔案:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>檢查客戶端碼

如果檢查客戶端代碼,它將説明您瞭解客戶端代碼如何與伺服器代碼交互以使應用正常工作。

#### <a name="starting-the-connection"></a>啟動連線

`$.connection`指 SignalR 代理。 代碼獲取對類代理的引用,`StockTickerHub`並將其放入變數中。 `ticker` 代理名稱是由`HubName`屬性設定的名稱:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

定義所有變數和函數後,檔中的最後一行代碼通過調用 SignalR 函數初始化 SignalR`start`連接。 函數`start`非同步執行並傳回[jQuery 延遲物件](http://api.jquery.com/category/deferred-object/)。 可以調用完成函數來指定應用完成非同步操作時要調用的函數。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>取得所有股票

該`init`函數調用伺服器上`getAllStocks`的函數,並使用伺服器返回的資訊來更新庫存表。 請注意,默認情況下,您必須在用戶端上使用 camelCasing,即使方法名稱在伺服器上是 pascalcase 的。 CamelCasing 規則僅適用於方法,不適用於物件。 例如,`stock.Symbol`您參考`stock.Price`與`stock.symbol`,`stock.price`而不是或 。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

在`init`方法中,應用透過`formatStock`調用物件的屬性`stock`格式化,然後調`supplant`用將變數中的`rowTemplate`占位符替換`stock`為 物件屬性值,為從伺服器接收的每個股票物件的表行創建 HTML。 然後,生成的 HTML 將追加到庫存表中。

> [!NOTE]
> 通過將其`init`作為`callback`在非`start`同步函數完成後執行的函數傳入來調用。 如果在調用`start``init`後 調用作為單獨的 JavaScript 語句調用 ,則函數將失敗,因為它將立即運行,而無需等待啟動函數完成建立連接。 在這種情況下,`init`該函數將嘗試`getAllStocks`在 應用建立伺服器連接之前調用該函數。

#### <a name="getting-updated-stock-prices"></a>取得更新的股票價格

當伺服器更改股票價格時,它將調用`updateStockPrice`連接的用戶端。 應用將該函數添加到代理的用戶端屬性,`stockTicker`使其可用於來自伺服器的調用。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

該`updateStockPrice`函數將從伺服器接收的 Stock 物件格式化為表行,其方式`init`與函數 中相同。 它不是將行追加到表中,而是在表中查找股票的當前行,並將該行替換為新行。

## <a name="test-the-application"></a>測試應用程式

您可以測試應用以確保其正常工作。 您將看到所有瀏覽器視窗顯示股票價格波動的即時庫存表。

1. 在工具列中,打開**腳本調試**,然後選擇播放按鈕以在除錯模式下運行應用。

    ![用戶打開調試模式和選擇播放的屏幕截圖。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    將開啟瀏覽器視窗,顯示**即時庫存表**。 庫存表最初顯示"載入..."行,然後,在很短的時間后,應用程序顯示初始股票數據,然後股票價格開始變化。

1. 從瀏覽器複製 URL,打開另外兩個瀏覽器,並將 URL 貼上到位址列中。

    初始庫存顯示與第一個瀏覽器相同,更改同時發生。

1. 關閉所有瀏覽器,打開新瀏覽器,然後轉到相同的 URL。

    StockTicker 單例物件繼續在伺服器中運行。 **即時庫存表**顯示,股票繼續變化。 您看不到具有零更改數位的初始表。

1. 關閉瀏覽器。

## <a name="enable-logging"></a>啟用記錄

SignalR 具有內建日誌記錄功能,您可以在用戶端上啟用該功能,以幫助進行故障排除。 在本節中,您可以啟用日誌記錄,並查看範例,這些範例顯示了日誌如何告訴您 SignalR 正在使用以下哪種傳輸方法:

* [WebSockets,](http://en.wikipedia.org/wiki/WebSocket)由IIS 8和當前瀏覽器支援。

* [伺服器發送的事件](http://en.wikipedia.org/wiki/Server-sent_events),由 Internet 資源管理器以外的瀏覽器支援。

* [永久幀](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe),由 Internet 資源管理員支援。

* [Ajax長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling),由所有瀏覽器支援。

對於任何給定的連接,SignalR 選擇伺服器和用戶端都支援的最佳傳輸方法。

1. 開啟*股票Ticker.js*.

1. 新增此突顯的代碼列,以便在檔案末尾初始化連線的代碼之前啟用紀錄記錄:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. 按**F5**以運行專案。

1. 打開瀏覽器的開發人員工具視窗,然後選擇主控台以查看日誌。 您可能需要刷新頁面才能看到 SignalR 協商新連線傳輸方法的日誌。

    * 如果您在 Windows 8 (IIS 8) 上運行 Internet 資源管理器 10,則傳輸方法是**WebSocket。**

    * 如果您在 Windows 7(IIS 7.5)上執行 Internet 資源管理員 10,則傳輸方法是**iframe**。

    * 如果您在 Windows 8 (IIS 8) 上運行 Firefox 19,則傳輸方法是**WebSocket。**

        > [!TIP]
        > 在 Firefox 中,安裝 Firebug 外接程式以獲取控制台視窗。

    * 如果您在 Windows 7(IIS 7.5)上運行 Firefox 19,則傳輸方法是**伺服器發送**的事件。

## <a name="install-the-stockticker-sample"></a>安裝庫存價格範例

[微軟.AspNet.SignalR.sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安裝StockTicker應用程式。 與從頭開始創建的簡化版本相比,NuGet 包包含的功能更多。 在本教學的這一部分中,您可以安裝 NuGet 包並查看新功能和實現這些功能的代碼。

> [!IMPORTANT]
> 如果不執行本教程的早期步驟,安裝包,則必須向專案添加 OWIN 啟動類。 NuGet 套件的此 readme.txt 檔解釋了此步驟。

### <a name="install-the-signalrsample-nuget-package"></a>安裝訊號R.樣品 NuGet 封裝

1. 在**解決方案資源管理員**中,右鍵單擊專案並選擇 **「管理 NuGet 包**」 。。

1. 在**NuGet 套件管理器中:SignalR.StockTicker**,選擇 **「瀏覽**」。

1. 從**包源**中,選擇**nuget.org。**

1. 在搜尋框中輸入*SignalR.範例*,然後選擇**Microsoft.AspNet.SignalR.範例** > **安裝**。

1. 在**解決方案資源管理員中**,展開*SignalR.Sample*資料夾。

    安裝 SignalR.Sample 包創建了資料夾及其內容。

1. 在*SignalR.sample*資料夾中,右鍵單擊*StockTicker.html*,然後選擇「**設定為起始頁**」。

    > [!NOTE]
    > 安裝 SignalR.sample NuGet 套件可能會更改*文稿*資料夾中的 jQuery 版本。 包在*SignalR.Sample*資料夾中安裝的新*StockTicker.html*檔案將與包安裝的 jQuery 版本同步,但如果要再次運行原始*StockTicker.html*檔,您可能需要首先更新腳本標記中的 jQuery 引用。

### <a name="run-the-application"></a>執行應用程式

 您在第一個應用中看到的表具有有用的功能。 完整的股票代碼應用程式顯示新的功能:一個水準滾動視窗,顯示股票數據和股票的變化顏色,因為他們的上升和下降。

1. 按 **F5** 以執行應用程式。

     首次運行應用時,"市場"是"關閉的",您將看到一個靜態表和一個未滾動的刻度視窗。

1. 選擇**公開市場**。

    ![即時代碼的屏幕截圖。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **即時庫存報價框**開始水準滾動,伺服器開始隨機廣播股票價格變化。

    * 每次股票價格變化時,應用程式都會更新**即時庫存表**和**即時股票報價器**。

    * 當股票價格變化為正時,應用程式將顯示具有綠色背景的股票。

    * 當更改為負時,應用程式將顯示具有紅色背景的股票。

1. 選擇**關閉市場**。

    * 表更新停止。

    * 刻度線停止滾動。

1. 選取 [重設]****。

    * 重置所有庫存數據。

    * 應用在價格更改開始之前還原初始狀態。

1. 從瀏覽器複製 URL,打開另外兩個瀏覽器,並將 URL 貼上到位址列中。

1. 在每個瀏覽器中,您都會看到相同的數據同時動態更新。

1. 當您選擇任何控制項時,所有瀏覽器都同時以相同的方式回應。

### <a name="live-stock-ticker-display"></a>即時庫存報價顯示

**即時庫存報價顯示**是按 CSS 樣式`<div>`格式化為 單行的元素中的無序列表。 應用以與表相同的方式初始化和更新代碼:透過在`<li>`樣本字串中替換占位符並動態地將`<li>`元素添加到`<ul>`元素。 該應用程式包括使用 jQuery`animate`函數來更改 中無序列表的邊距左側`<div>`滾動。

#### <a name="signalrsample-stocktickerhtml"></a>訊號R.樣品庫存Ticker.html

股票代碼 HTML 碼:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>信號R.樣品庫存Ticker.css

股票代碼 CSS 碼:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>訊號R.樣品信號R.StockTicker.js

使其捲動的 jQuery 代碼:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>用戶端可呼叫的伺服器上的其他方法

為了增加應用的靈活性,應用可以調用其他方法。

#### <a name="signalrsample-stocktickerhubcs"></a>訊號R.樣品StockTickerHub.cs

該`StockTickerHub`類別定義了客戶端可以調用的其他四種方法:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

套用`OpenMarket`,`CloseMarket`並`Reset`回應頁面頂部的按鈕。 它們演示了一個用戶端觸發狀態更改的模式,該更改將立即傳播到所有用戶端。 這些方法中的每種方法都調用類中`StockTicker`導致市場狀態更改然後廣播新狀態的方法。

#### <a name="signalrsample-stocktickercs"></a>信號R.樣品StockTicker.cs

在類`StockTicker`中,應用使用`MarketState``MarketState`返回 枚舉值的屬性維護市場狀態:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

變更市場狀態的每個方法都會在鎖區內執行此操作,`StockTicker`因為類別必須是線程安全的:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

為了確保此代碼是線程安全的,支援指定的`_marketState``MarketState``volatile`屬性的欄位:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange`和`BroadcastMarketReset`方法與您已經看到的廣播股票價格方法類似,但它們調用在用戶端定義的不同方法:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>伺服器可以呼叫的用戶端上的其他功能

該`updateStockPrice`函數現在同時處理表和刻度顯示,它`jQuery.Color`用於閃爍紅色和綠色。

*SignalR.StockTicker.js*中的新功能根據市場狀態啟用和禁用按鈕。 它們還會停止或啟動**即時庫存刻度**水平滾動。 由於許多函數被添加到`ticker.client`,應用程式使用[jQuery 擴展函數](http://api.jquery.com/jQuery.extend/)來添加它們。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立連線後的其他客戶端設定

用戶端建立連接後,它還有一些額外的工作要做:

* 瞭解市場是開放的還是關閉的,以調用適當的`marketOpened`或`marketClosed`功能。

* 將伺服器方法調用附加到按鈕。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

伺服器方法直到應用建立連接後才會連接到按鈕。 因此,代碼在伺服器方法可用之前無法調用它們。

## <a name="additional-resources"></a>其他資源

在本教學中,您學習了如何對將消息從伺服器廣播到所有連接用戶端的 SignalR 應用程式進行程式設計。 現在,您可以定期廣播消息,並回應來自任何用戶端的通知。 您可以使用多線程單例實例的概念在多人線上遊戲方案中維護伺服器狀態。 例如,請參閱基於[SignalR 的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。

有關顯示對等通訊場景的教學,請參閱[使用 SignalR 入門](introduction-to-signalr.md)與使用[SignalR 進行即時更新](tutorial-high-frequency-realtime-with-signalr.md)。

有關 SignalR 的更多,請參閱以下資源:

* [ASP.NET SignalR](../../index.md)
* [信號器專案](http://signalr.net/)
* [訊號R GitHub 與範例](https://github.com/SignalR/SignalR)
* [信號R維琪](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您：

> [!div class="checklist"]
> * 已建立項目
> * 設定伺服器程式碼
> * 檢查伺服器代碼
> * 設定客戶端碼
> * 檢查客戶端碼
> * 測試應用程式
> * 開啟紀錄記錄

進入下一篇文章,瞭解如何創建使用ASP.NET SignalR 2的即時 Web 應用程式。
> [!div class="nextstepaction"]
> [使用 SignalR 建立即時 Web 應用程式](real-time-web-applications-with-signalr.md)
