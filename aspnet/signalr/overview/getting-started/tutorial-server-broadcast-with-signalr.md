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
# <a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="d92b1-103">教學:使用 SignalR 2 進行伺服器廣播</span><span class="sxs-lookup"><span data-stu-id="d92b1-103">Tutorial: Server broadcast with SignalR 2</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="d92b1-104">本教學示範如何建立使用ASP.NET SignalR 2 提供伺服器廣播功能的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-104">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="d92b1-105">伺服器廣播意味著伺服器啟動發送到用戶端的通信。</span><span class="sxs-lookup"><span data-stu-id="d92b1-105">Server broadcast means that the server starts the communications sent to clients.</span></span>

<span data-ttu-id="d92b1-106">您將在本教學中創建的應用程式類比股票代碼,這是伺服器廣播功能的典型方案。</span><span class="sxs-lookup"><span data-stu-id="d92b1-106">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span> <span data-ttu-id="d92b1-107">伺服器定期隨機更新股票價格並將更新廣播給所有連接的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-107">Periodically, the server randomly updates stock prices and broadcast the updates to all connected clients.</span></span> <span data-ttu-id="d92b1-108">在瀏覽器中,"更改"和 **"** 列"中的數位**%** 和符號會動態更改,以回應來自伺服器的通知。</span><span class="sxs-lookup"><span data-stu-id="d92b1-108">In the browser, the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="d92b1-109">如果打開其他瀏覽器到同一 URL,它們都同時顯示相同的數據和對數據的相同更改。</span><span class="sxs-lookup"><span data-stu-id="d92b1-109">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

![建立 Web](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="d92b1-111">在本教學課程中，您：</span><span class="sxs-lookup"><span data-stu-id="d92b1-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d92b1-112">建立專案</span><span class="sxs-lookup"><span data-stu-id="d92b1-112">Create the project</span></span>
> * <span data-ttu-id="d92b1-113">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-113">Set up the server code</span></span>
> * <span data-ttu-id="d92b1-114">檢查伺服器代碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-114">Examine the server code</span></span>
> * <span data-ttu-id="d92b1-115">設定客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-115">Set up the client code</span></span>
> * <span data-ttu-id="d92b1-116">檢查客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-116">Examine the client code</span></span>
> * <span data-ttu-id="d92b1-117">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="d92b1-117">Test the application</span></span>
> * <span data-ttu-id="d92b1-118">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="d92b1-118">Enable logging</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d92b1-119">如果不想完成構建應用程式的步驟,可以在新的空ASP.NET Web 應用程式專案中安裝 SignalR.sample 包。</span><span class="sxs-lookup"><span data-stu-id="d92b1-119">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="d92b1-120">如果不執行本教程中的步驟,安裝 NuGet 包,則必須按照*readme.txt*檔中的說明進行操作。</span><span class="sxs-lookup"><span data-stu-id="d92b1-120">If you install the NuGet package without performing the steps in this tutorial, you must follow the instructions in the *readme.txt* file.</span></span> <span data-ttu-id="d92b1-121">要執行套件,您需要添加一個 OWIN 啟動`ConfigureSignalR`類, 該類調用已安裝套件中的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-121">To run the package you need to add an OWIN startup class which calls the `ConfigureSignalR` method in the installed package.</span></span> <span data-ttu-id="d92b1-122">如果不添加 OWIN 啟動類,您將收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d92b1-122">You will receive an error if you do not add the OWIN startup class.</span></span> <span data-ttu-id="d92b1-123">請參閱本文[的「安裝庫存價格」示例](#install-the-stockticker-sample)部分。</span><span class="sxs-lookup"><span data-stu-id="d92b1-123">See the [Install the StockTicker sample](#install-the-stockticker-sample) section of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d92b1-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d92b1-124">Prerequisites</span></span>

* <span data-ttu-id="d92b1-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。</span><span class="sxs-lookup"><span data-stu-id="d92b1-125">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="d92b1-126">建立專案</span><span class="sxs-lookup"><span data-stu-id="d92b1-126">Create the project</span></span>

<span data-ttu-id="d92b1-127">本節演示如何使用 Visual Studio 2017 創建空ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-127">This section shows how to use Visual Studio 2017 to create an empty ASP.NET Web Application.</span></span>

1. <span data-ttu-id="d92b1-128">在可視化工作室中,創建一個ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-128">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![建立 Web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. <span data-ttu-id="d92b1-130">在新**ASP.NET Web 應用程式 - SignalR.StockTicker**視窗中,保留 **「空**」並選擇 **「確定**」 。</span><span class="sxs-lookup"><span data-stu-id="d92b1-130">In the **New ASP.NET Web Application - SignalR.StockTicker** window, leave **Empty** selected and select **OK**.</span></span>

## <a name="set-up-the-server-code"></a><span data-ttu-id="d92b1-131">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-131">Set up the server code</span></span>

<span data-ttu-id="d92b1-132">在本節中,您可以設置在伺服器上運行的代碼。</span><span class="sxs-lookup"><span data-stu-id="d92b1-132">In this section, you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="d92b1-133">建立"庫存'類別</span><span class="sxs-lookup"><span data-stu-id="d92b1-133">Create the Stock class</span></span>

<span data-ttu-id="d92b1-134">首先創建用於存儲和傳輸庫存資訊*的Stock*模型類。</span><span class="sxs-lookup"><span data-stu-id="d92b1-134">You begin by creating the *Stock* model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="d92b1-135">在**解決方案資源管理器**中,右鍵單擊專案並選擇 **「添加** > **類**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-135">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="d92b1-136">命名類*Stock*並將其添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-136">Name the class *Stock* and add it to the project.</span></span>

1. <span data-ttu-id="d92b1-137">將*Stock.cs*檔案的代碼取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-137">Replace the code in the *Stock.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="d92b1-138">建立股票時要設定的兩個屬性是`Symbol`(例如,微軟的 MSFT)和`Price`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-138">The two properties that you'll set when you create stocks are `Symbol` (for example, MSFT for Microsoft) and `Price`.</span></span> <span data-ttu-id="d92b1-139">其他屬性取決於設置`Price`的方式和時間。</span><span class="sxs-lookup"><span data-stu-id="d92b1-139">The other properties depend on how and when you set `Price`.</span></span> <span data-ttu-id="d92b1-140">第一次設定`Price`時,值將傳播到`DayOpen`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-140">The first time you set `Price`, the value gets propagated to `DayOpen`.</span></span> <span data-ttu-id="d92b1-141">`Price`之後,當您設置 時,應用根據`Change``PercentChange``Price``DayOpen`和之間的差異計算和 屬性值。</span><span class="sxs-lookup"><span data-stu-id="d92b1-141">After that, when you set `Price`, the app calculates the `Change` and `PercentChange` property values based on the difference between `Price` and `DayOpen`.</span></span>

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a><span data-ttu-id="d92b1-142">建立股票價格中心和股票提克類</span><span class="sxs-lookup"><span data-stu-id="d92b1-142">Create the StockTickerHub and StockTicker classes</span></span>

<span data-ttu-id="d92b1-143">您將使用 SignalR 中心 API 來處理伺服器到用戶端的互動。</span><span class="sxs-lookup"><span data-stu-id="d92b1-143">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="d92b1-144">派生`StockTickerHub`自 SignalR`Hub`類的類將處理來自用戶端的接收連接和方法調用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-144">A `StockTickerHub` class that derives from the SignalR `Hub` class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="d92b1-145">您必須維護庫存資料並執行物件`Timer`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-145">You also need to maintain stock data and run a `Timer` object.</span></span> <span data-ttu-id="d92b1-146">該`Timer`物件將定期觸發獨立於用戶端連接的價格更新。</span><span class="sxs-lookup"><span data-stu-id="d92b1-146">The `Timer` object will periodically trigger price updates independent of client connections.</span></span> <span data-ttu-id="d92b1-147">不能將這些函數放在`Hub`類中,因為中心是瞬態的。</span><span class="sxs-lookup"><span data-stu-id="d92b1-147">You can't put these functions in a `Hub` class, because Hubs are transient.</span></span> <span data-ttu-id="d92b1-148">應用為中心中的每個`Hub`任務創建一個類實例,例如從用戶端到伺服器的連接和調用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-148">The app creates a `Hub` class instance for each task on the hub, like connections and calls from the client to the server.</span></span> <span data-ttu-id="d92b1-149">因此,保存庫存數據、更新價格和廣播價格更新的機制必須運行在單獨的類中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-149">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class.</span></span> <span data-ttu-id="d92b1-150">您將命名此類別`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-150">You'll name the class `StockTicker`.</span></span>

![從斯托克蒂克廣播](tutorial-server-broadcast-with-signalr/_static/image3.png)

<span data-ttu-id="d92b1-152">您只需要在伺服器上執行類的`StockTicker`一個實例,因此您需要設置從每個`StockTickerHub`實例到 singleton`StockTicker`實例的引用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-152">You only want one instance of the `StockTicker` class to run on the server, so you'll need to set up a reference from each `StockTickerHub` instance to the singleton `StockTicker` instance.</span></span> <span data-ttu-id="d92b1-153">類`StockTicker`必須廣播給客戶端,因為它具有股票數據並觸發更新,`StockTicker``Hub`但不是類。</span><span class="sxs-lookup"><span data-stu-id="d92b1-153">The `StockTicker` class has to broadcast to clients because it has the stock data and triggers updates, but `StockTicker` isn't a `Hub` class.</span></span> <span data-ttu-id="d92b1-154">類`StockTicker`必須獲取對 SignalR 中心連接上下文物件的引用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-154">The `StockTicker` class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="d92b1-155">然後,它可以使用 SignalR 連接上下文物件廣播到用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-155">It can then use the SignalR connection context object to broadcast to clients.</span></span>

#### <a name="create-stocktickerhubcs"></a><span data-ttu-id="d92b1-156">建立StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="d92b1-156">Create StockTickerHub.cs</span></span>

1. <span data-ttu-id="d92b1-157">在**解決方案資源管理器**中,右鍵單擊專案並**Add** > 選擇「**添加新項**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-157">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="d92b1-158">新增**新項目 - SignalR.StockTicker**中,選擇 **「已安裝** > **的視覺 C#** > **Web** > **訊號R」,** 然後選擇**訊號 R 集線器類別 (v2)。**</span><span class="sxs-lookup"><span data-stu-id="d92b1-158">In **Add New Item - SignalR.StockTicker**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="d92b1-159">命名類*StockTickerHub*並將其添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-159">Name the class *StockTickerHub* and add it to the project.</span></span>

    <span data-ttu-id="d92b1-160">此步驟將創建*StockTickerHub.cs*類檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-160">This step creates the *StockTickerHub.cs* class file.</span></span> <span data-ttu-id="d92b1-161">同時,它將一組支援 SignalR 的文稿檔和程式集引用添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-161">Simultaneously, it adds a set of script files and assembly references that supports SignalR to the project.</span></span>

1. <span data-ttu-id="d92b1-162">將*StockTickerHub.cs*檔案中的代碼取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-162">Replace the code in the *StockTickerHub.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="d92b1-163">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="d92b1-163">Save the file.</span></span>

<span data-ttu-id="d92b1-164">應用使用[Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類定義客戶端可以在伺服器上調用的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-164">The app uses the [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class to define methods the clients can call on the server.</span></span> <span data-ttu-id="d92b1-165">您正在定義方法: `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-165">You're defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="d92b1-166">當用戶端最初連接到伺服器時,它將調用此方法來獲取所有股票及其當前價格的清單。</span><span class="sxs-lookup"><span data-stu-id="d92b1-166">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="d92b1-167">該方法可以同步運行並返回`IEnumerable<Stock>`,因為它正在從記憶體返回數據。</span><span class="sxs-lookup"><span data-stu-id="d92b1-167">The method can run synchronously and return `IEnumerable<Stock>` because it's returning data from memory.</span></span>

<span data-ttu-id="d92b1-168">如果方法必須通過執行涉及等待(如資料庫查找或 Web 服務調用)來獲取數據,則`Task<IEnumerable<Stock>>`可以指定為返回值以啟用非同步處理。</span><span class="sxs-lookup"><span data-stu-id="d92b1-168">If the method had to get the data by doing something that would involve waiting, like a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="d92b1-169">有關詳細資訊,請參閱[ASP.NET 訊號 R 集線器 API 指南 - 伺服器 - 何時非同步執行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-169">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

<span data-ttu-id="d92b1-170">該`HubName`屬性指定應用如何在用戶端上的 JavaScript 代碼中引用 Hub。</span><span class="sxs-lookup"><span data-stu-id="d92b1-170">The `HubName` attribute specifies how the app will reference the Hub in JavaScript code on the client.</span></span> <span data-ttu-id="d92b1-171">如果不使用此屬性,用戶端上的預設名稱是類別名稱的 camelCase 版本,在這種情況下,該`stockTickerHub`版本為 。</span><span class="sxs-lookup"><span data-stu-id="d92b1-171">The default name on the client if you don't use this attribute, is a camelCase version of the class name, which in this case would be `stockTickerHub`.</span></span>

<span data-ttu-id="d92b1-172">稍後在創建`StockTicker`類時將看到,應用在其靜`Instance`態 屬性中創建該類的單例實例。</span><span class="sxs-lookup"><span data-stu-id="d92b1-172">As you'll see later when you create the `StockTicker` class, the app creates a singleton instance of that class in its static `Instance` property.</span></span> <span data-ttu-id="d92b1-173">無論連接或斷開連接的`StockTicker`用戶端數,該單例實例都位於記憶體中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-173">That singleton instance of `StockTicker` is in memory no matter how many clients connect or disconnect.</span></span> <span data-ttu-id="d92b1-174">該實例是`GetAllStocks()`該方法用於返回當前庫存資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-174">That instance is what the `GetAllStocks()` method uses to return current stock information.</span></span>

#### <a name="create-stocktickercs"></a><span data-ttu-id="d92b1-175">建立StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="d92b1-175">Create StockTicker.cs</span></span>

1. <span data-ttu-id="d92b1-176">在**解決方案資源管理器**中,右鍵單擊專案並選擇 **「添加** > **類**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-176">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="d92b1-177">命名類*StockTicker*並將其添加到專案中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-177">Name the class *StockTicker* and add it to the project.</span></span>

1. <span data-ttu-id="d92b1-178">將*StockTicker.cs*檔案中的代碼取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-178">Replace the code in the *StockTicker.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

<span data-ttu-id="d92b1-179">由於所有線程都將運行同一個 StockTicker 代碼實例,因此 StockTicker 類必須具有線程安全。</span><span class="sxs-lookup"><span data-stu-id="d92b1-179">Since all threads will be running the same instance of StockTicker code, the StockTicker class has to be thread-safe.</span></span>

### <a name="examine-the-server-code"></a><span data-ttu-id="d92b1-180">檢查伺服器代碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-180">Examine the server code</span></span>

<span data-ttu-id="d92b1-181">如果檢查伺服器代碼,它將説明您瞭解應用的工作原理。</span><span class="sxs-lookup"><span data-stu-id="d92b1-181">If you examine the server code, it will help you understand how the app works.</span></span>

#### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="d92b1-182">將單例實體儲存在靜態欄位</span><span class="sxs-lookup"><span data-stu-id="d92b1-182">Storing the singleton instance in a static field</span></span>

<span data-ttu-id="d92b1-183">代碼初始化使用類的實例`_instance``Instance`支援 屬性的靜態欄位。</span><span class="sxs-lookup"><span data-stu-id="d92b1-183">The code initializes the static `_instance` field that backs the `Instance` property with an instance of the class.</span></span> <span data-ttu-id="d92b1-184">由於構造函數是私有的,因此它是應用可以創建的唯一類實例。</span><span class="sxs-lookup"><span data-stu-id="d92b1-184">Because the constructor is private, it's the only instance of the class that the app can create.</span></span> <span data-ttu-id="d92b1-185">套用`_instance`對欄位使用[延遲初始化](/dotnet/framework/performance/lazy-initialization)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-185">The app uses [Lazy initialization](/dotnet/framework/performance/lazy-initialization) for the `_instance` field.</span></span> <span data-ttu-id="d92b1-186">這不是出於性能原因。</span><span class="sxs-lookup"><span data-stu-id="d92b1-186">It's not for performance reasons.</span></span> <span data-ttu-id="d92b1-187">它確保實例創建是線程安全的。</span><span class="sxs-lookup"><span data-stu-id="d92b1-187">It's to make sure the instance creation is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

<span data-ttu-id="d92b1-188">每次用戶端連接到伺服器時,在單獨的線程中運行的 StockTickerHub 類的新實`StockTicker.Instance`例從 靜態屬性獲取 StockTicker 單例實`StockTickerHub`例,如您在 類中前面看到的。</span><span class="sxs-lookup"><span data-stu-id="d92b1-188">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the `StockTicker.Instance` static property, as you saw earlier in the `StockTickerHub` class.</span></span>

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="d92b1-189">儲存庫存資料儲存在併發字典中</span><span class="sxs-lookup"><span data-stu-id="d92b1-189">Storing stock data in a ConcurrentDictionary</span></span>

<span data-ttu-id="d92b1-190">建構函數使用一些樣本庫存`_stocks`數據初始化集合,並`GetAllStocks`返回數據。</span><span class="sxs-lookup"><span data-stu-id="d92b1-190">The constructor initializes the `_stocks` collection with some sample stock data, and `GetAllStocks` returns the stocks.</span></span> <span data-ttu-id="d92b1-191">如前所述,此股票集合由返回`StockTickerHub.GetAllStocks`,這是用戶端可以調用的類`Hub`中的 伺服器方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-191">As you saw earlier, this collection of stocks is returned by `StockTickerHub.GetAllStocks`, which is a server method in the `Hub` class that clients can call.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

<span data-ttu-id="d92b1-192">出於線程安全,股票集合定義為[併發字典](https://msdn.microsoft.com/library/dd287191.aspx)類型。</span><span class="sxs-lookup"><span data-stu-id="d92b1-192">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="d92b1-193">作為替代方法,您可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)物件,並在對字典進行更改時顯式鎖定字典。</span><span class="sxs-lookup"><span data-stu-id="d92b1-193">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

<span data-ttu-id="d92b1-194">對於此示例應用程式,可以將應用程序數據存儲在記憶體中,並在應用釋放`StockTicker`實例時丟失數據。</span><span class="sxs-lookup"><span data-stu-id="d92b1-194">For this sample application, it's OK to store application data in memory and to lose the data when the app disposes of the  `StockTicker` instance.</span></span> <span data-ttu-id="d92b1-195">在實際應用程式中,您將像資料庫一樣使用後端數據存儲。</span><span class="sxs-lookup"><span data-stu-id="d92b1-195">In a real application, you would work with a back-end data store like a database.</span></span>

#### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="d92b1-196">定期更新股票價格</span><span class="sxs-lookup"><span data-stu-id="d92b1-196">Periodically updating stock prices</span></span>

<span data-ttu-id="d92b1-197">建構函數啟動一個`Timer`物件,該物件定期調用隨機更新股票價格的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-197">The constructor starts up a `Timer` object that periodically calls methods that update stock prices on a random basis.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 <span data-ttu-id="d92b1-198">`Timer`呼叫`UpdateStockPrices`, 在狀態參數中傳遞為 null。</span><span class="sxs-lookup"><span data-stu-id="d92b1-198">`Timer` calls `UpdateStockPrices`, which passes in null in the state parameter.</span></span> <span data-ttu-id="d92b1-199">在更新價格之前,應用會鎖定`_updateStockPricesLock`物件。</span><span class="sxs-lookup"><span data-stu-id="d92b1-199">Before updating prices, the app takes a lock on the `_updateStockPricesLock` object.</span></span> <span data-ttu-id="d92b1-200">代碼檢查另一個線程是否已更新價格,然後調用`TryUpdateStockPrice`清單中的每個股票。</span><span class="sxs-lookup"><span data-stu-id="d92b1-200">The code checks if another thread is already updating prices, and then it calls `TryUpdateStockPrice` on each stock in the list.</span></span> <span data-ttu-id="d92b1-201">該方法`TryUpdateStockPrice`決定是否更改股票價格,以及更改多少股票價格。</span><span class="sxs-lookup"><span data-stu-id="d92b1-201">The `TryUpdateStockPrice` method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="d92b1-202">如果股票價格發生變化,應用將調用`BroadcastStockPrice`向所有連接的用戶端廣播股票價格變化。</span><span class="sxs-lookup"><span data-stu-id="d92b1-202">If the stock price changes, the app calls `BroadcastStockPrice` to broadcast the stock price change to all connected clients.</span></span>

<span data-ttu-id="d92b1-203">指定`_updatingStockPrices`[易失性](https://msdn.microsoft.com/library/x13ttww7.aspx)的標誌,以確保它是線程安全的。</span><span class="sxs-lookup"><span data-stu-id="d92b1-203">The `_updatingStockPrices` flag designated [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to make sure it is thread-safe.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

<span data-ttu-id="d92b1-204">在實際應用程式中,`TryUpdateStockPrice`該方法將調用 Web 服務來查找價格。</span><span class="sxs-lookup"><span data-stu-id="d92b1-204">In a real application, the `TryUpdateStockPrice` method would call a web service to look up the price.</span></span> <span data-ttu-id="d92b1-205">在此代碼中,應用程式使用隨機數生成器隨機進行更改。</span><span class="sxs-lookup"><span data-stu-id="d92b1-205">In this code, the app uses a random number generator to make changes randomly.</span></span>

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="d92b1-206">取得 SignalR 中文,以便 StockTicker 類別可以廣播給用戶端</span><span class="sxs-lookup"><span data-stu-id="d92b1-206">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

<span data-ttu-id="d92b1-207">由於價格變化源自物件,`StockTicker`因此需要在所有連接的用戶端上調`updateStockPrice`用 方法的物件。</span><span class="sxs-lookup"><span data-stu-id="d92b1-207">Because the price changes originate here in the `StockTicker` object, it's the object that needs to call an `updateStockPrice` method on all connected clients.</span></span> <span data-ttu-id="d92b1-208">在類`Hub`中,您有用於調用用戶端方法的 API,`StockTicker`但不派`Hub`生自類 ,`Hub`並且沒有對任何 物件的引用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-208">In a `Hub` class, you have an API for calling client methods, but `StockTicker` doesn't derive from the `Hub` class and doesn't have a reference to any `Hub` object.</span></span> <span data-ttu-id="d92b1-209">要廣播到已連接的用戶端`StockTicker`,類必須`StockTickerHub`獲取 類的 SignalR 上下文實例,並用它來調用用戶端上的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-209">To broadcast to connected clients, the `StockTicker` class has to get the SignalR context instance for the `StockTickerHub` class and use that to call methods on clients.</span></span>

<span data-ttu-id="d92b1-210">當代碼創建單例類實例、傳遞該引用到構造函數時獲取對 SignalR 上下`Clients`文的引用,構造函數將其放入屬性中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-210">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the `Clients` property.</span></span>

<span data-ttu-id="d92b1-211">您只想獲取上下文一次的原因有兩個:獲取上下文是一項昂貴的任務,一次獲取上下文可確保應用保留發送到用戶端的消息的預期順序。</span><span class="sxs-lookup"><span data-stu-id="d92b1-211">There are two reasons why you want to get the context only once: getting the context is an expensive task, and getting it once makes sure the app preserves the intended order of messages sent to the clients.</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

<span data-ttu-id="d92b1-212">通過取得`Clients`內容的屬性並將其放入屬性,`StockTickerClient`可以編寫代碼來呼叫`Hub`與類中看起來相同的用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-212">Getting the `Clients` property of the context and putting it in the `StockTickerClient` property lets you write code to call client methods that looks the same as it would in a `Hub` class.</span></span> <span data-ttu-id="d92b1-213">例如,要廣播到所有用戶端,您可以寫入`Clients.All.updateStockPrice(stock)`。</span><span class="sxs-lookup"><span data-stu-id="d92b1-213">For instance, to broadcast to all clients you can write `Clients.All.updateStockPrice(stock)`.</span></span>

<span data-ttu-id="d92b1-214">您`updateStockPrice`呼`BroadcastStockPrice`叫的方法尚不存在。</span><span class="sxs-lookup"><span data-stu-id="d92b1-214">The `updateStockPrice` method that you're calling in `BroadcastStockPrice` doesn't exist yet.</span></span> <span data-ttu-id="d92b1-215">稍後,當您編寫在用戶端上運行的代碼時,將添加它。</span><span class="sxs-lookup"><span data-stu-id="d92b1-215">You'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="d92b1-216">您可以在此處引用,`updateStockPrice``Clients.All`因為 是動態的,這意味著應用將在運行時計算運算式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-216">You can refer to `updateStockPrice` here because `Clients.All` is dynamic, which means the app will evaluate the expression at runtime.</span></span> <span data-ttu-id="d92b1-217">執行此方法調用時,SignalR 將向用戶端發送方法名稱和參數值,如果用戶端具有`updateStockPrice`名為的方法,則應用將調用該方法並將參數值傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-217">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named `updateStockPrice`, the app will call that method and pass the parameter value to it.</span></span>

<span data-ttu-id="d92b1-218">`Clients.All`表示發送到所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-218">`Clients.All` means send to all clients.</span></span> <span data-ttu-id="d92b1-219">SignalR 為您提供了其他選項來指定要發送到的用戶端或用戶端群組。</span><span class="sxs-lookup"><span data-stu-id="d92b1-219">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="d92b1-220">有關詳細資訊,請參閱[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-220">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="d92b1-221">註冊訊號R路由</span><span class="sxs-lookup"><span data-stu-id="d92b1-221">Register the SignalR route</span></span>

<span data-ttu-id="d92b1-222">伺服器需要知道要攔截哪個 URL 並定向到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="d92b1-222">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="d92b1-223">為此,添加 OWIN 啟動類:</span><span class="sxs-lookup"><span data-stu-id="d92b1-223">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="d92b1-224">在**解決方案資源管理器**中,右鍵單擊專案並**Add** > 選擇「**添加新項**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-224">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="d92b1-225">在 **'新增新項目 - SignalR.StockTicker' 中選擇\*\*\*\*' 已安裝** > **的視覺化 C#** > **Web"** 然後選擇**OWIN 啟動類別**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-225">In **Add New Item - SignalR.StockTicker** select **Installed** > **Visual C#** > **Web** and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="d92b1-226">命名類 *「啟動」* 並選擇 **「確定**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-226">Name the class *Startup* and select **OK**.</span></span>

1. <span data-ttu-id="d92b1-227">將*Startup.cs*檔案中的預設代碼取代此代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-227">Replace the default code in the *Startup.cs* file with this code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="d92b1-228">您現在已完成伺服器代碼的設置。</span><span class="sxs-lookup"><span data-stu-id="d92b1-228">You have now finished setting up the server code.</span></span> <span data-ttu-id="d92b1-229">在下一節中,您將設置用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-229">In the next section, you'll set up the client.</span></span>

## <a name="set-up-the-client-code"></a><span data-ttu-id="d92b1-230">設定客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-230">Set up the client code</span></span>

<span data-ttu-id="d92b1-231">在本節中,設置在用戶端上運行的代碼。</span><span class="sxs-lookup"><span data-stu-id="d92b1-231">In this section, you set up the code that runs on the client.</span></span>

### <a name="create-the-html-page-and-javascript-file"></a><span data-ttu-id="d92b1-232">建立 HTML 頁面與 JavaScript 檔案</span><span class="sxs-lookup"><span data-stu-id="d92b1-232">Create the HTML page and JavaScript file</span></span>

<span data-ttu-id="d92b1-233">HTML 頁面將顯示數據,JAVAScript 檔案將組織數據。</span><span class="sxs-lookup"><span data-stu-id="d92b1-233">The HTML page will display the data and the JavaScript file will organize the data.</span></span>

#### <a name="create-stocktickerhtml"></a><span data-ttu-id="d92b1-234">建立股票Ticker.html</span><span class="sxs-lookup"><span data-stu-id="d92b1-234">Create StockTicker.html</span></span>

<span data-ttu-id="d92b1-235">首先,您將添加 HTML 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-235">First, you'll add the HTML client.</span></span>

1. <span data-ttu-id="d92b1-236">在**解決方案資源管理員**中,右鍵單擊專案並選擇「**添加** > **HTML 頁面**」 。。</span><span class="sxs-lookup"><span data-stu-id="d92b1-236">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="d92b1-237">命名檔案*庫存Ticker*並選擇 **「確定**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-237">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="d92b1-238">將*StockTicker.html*檔案中的預設代碼取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-238">Replace the default code in the *StockTicker.html* file with this code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    <span data-ttu-id="d92b1-239">HTML 創建一個包含五列的表、一個標題行和一個包含一個跨所有五列的單元格的數據行。</span><span class="sxs-lookup"><span data-stu-id="d92b1-239">The HTML creates a table with five columns, a header row, and a data row with a single cell that spans all five columns.</span></span> <span data-ttu-id="d92b1-240">數據行顯示"載入..."當應用程式啟動時,瞬間。</span><span class="sxs-lookup"><span data-stu-id="d92b1-240">The data row shows "loading..." momentarily when the app starts.</span></span> <span data-ttu-id="d92b1-241">JavaScript 代碼將刪除該行,並在其位置添加從伺服器檢索的股票數據行。</span><span class="sxs-lookup"><span data-stu-id="d92b1-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="d92b1-242">文稿標記指定:</span><span class="sxs-lookup"><span data-stu-id="d92b1-242">The script tags specify:</span></span>

    * <span data-ttu-id="d92b1-243">jQuery 文本檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-243">The jQuery script file.</span></span>

    * <span data-ttu-id="d92b1-244">SignalR 核心文本檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-244">The SignalR core script file.</span></span>

    * <span data-ttu-id="d92b1-245">SignalR 代理文本檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-245">The SignalR proxies script file.</span></span>

    * <span data-ttu-id="d92b1-246">稍後將創建的 StockTicker 文稿檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-246">A StockTicker script file that you'll create later.</span></span>

    <span data-ttu-id="d92b1-247">應用程式動態生成 SignalR 代理文本檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-247">The app dynamically generates the SignalR proxies script file.</span></span> <span data-ttu-id="d92b1-248">它指定"/信號器/集線器"URL,併為 的 Hub 類(本例中)`StockTickerHub.GetAllStocks`為 定義方法的代理方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-248">It specifies the "/signalr/hubs" URL and defines proxy methods for the methods on the Hub class, in this case, for `StockTickerHub.GetAllStocks`.</span></span> <span data-ttu-id="d92b1-249">如果您願意,可以使用[SignalR 實用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手動生成此 JavaScript 檔。</span><span class="sxs-lookup"><span data-stu-id="d92b1-249">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/).</span></span> <span data-ttu-id="d92b1-250">不要忘記在方法調用中`MapHubs`禁用動態文件創建。</span><span class="sxs-lookup"><span data-stu-id="d92b1-250">Don't forget to disable dynamic file creation in the `MapHubs` method call.</span></span>

1. <span data-ttu-id="d92b1-251">在**解決方案資源管理員中**,展開**文稿**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-251">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="d92b1-252">jQuery 和 SignalR 的文本庫在項目中可見。</span><span class="sxs-lookup"><span data-stu-id="d92b1-252">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d92b1-253">包管理器將安裝更高版本的 SignalR 腳本。</span><span class="sxs-lookup"><span data-stu-id="d92b1-253">The package manager will install a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="d92b1-254">更新代碼塊中的腳本引用,以對應於專案中的腳本檔版本。</span><span class="sxs-lookup"><span data-stu-id="d92b1-254">Update the script references in the code block to correspond to the versions of the script files in the project.</span></span>

1. <span data-ttu-id="d92b1-255">在**解決方案資源管理器**中,右鍵按*一下 StockTicker.html*,然後選擇 **「設定為起始頁**」 。。</span><span class="sxs-lookup"><span data-stu-id="d92b1-255">In **Solution Explorer**, right-click *StockTicker.html*, and then select **Set as Start Page**.</span></span>

#### <a name="create-stocktickerjs"></a><span data-ttu-id="d92b1-256">建立庫存Ticker.js</span><span class="sxs-lookup"><span data-stu-id="d92b1-256">Create StockTicker.js</span></span>

<span data-ttu-id="d92b1-257">現在創建 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="d92b1-257">Now create the JavaScript file.</span></span>

1. <span data-ttu-id="d92b1-258">在**解決方案資源管理員**中,右鍵單擊專案並選擇 **「添加** > **JAvaScript 檔案**」。。</span><span class="sxs-lookup"><span data-stu-id="d92b1-258">In **Solution Explorer**, right-click the project and select **Add** > **JavaScript File**.</span></span>

1. <span data-ttu-id="d92b1-259">命名檔案*庫存Ticker*並選擇 **「確定**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-259">Name the file *StockTicker* and select **OK**.</span></span>

1. <span data-ttu-id="d92b1-260">將此代碼加入*StockTicker.js*檔案:</span><span class="sxs-lookup"><span data-stu-id="d92b1-260">Add this code to the *StockTicker.js* file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a><span data-ttu-id="d92b1-261">檢查客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-261">Examine the client code</span></span>

<span data-ttu-id="d92b1-262">如果檢查客戶端代碼,它將説明您瞭解客戶端代碼如何與伺服器代碼交互以使應用正常工作。</span><span class="sxs-lookup"><span data-stu-id="d92b1-262">If you examine the client code, it will help you learn how the client code interacts with the server code to make the app work.</span></span>

#### <a name="starting-the-connection"></a><span data-ttu-id="d92b1-263">啟動連線</span><span class="sxs-lookup"><span data-stu-id="d92b1-263">Starting the connection</span></span>

<span data-ttu-id="d92b1-264">`$.connection`指 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="d92b1-264">`$.connection` refers to the SignalR proxies.</span></span> <span data-ttu-id="d92b1-265">代碼獲取對類代理的引用,`StockTickerHub`並將其放入變數中。 `ticker`</span><span class="sxs-lookup"><span data-stu-id="d92b1-265">The code gets a reference to the proxy for the `StockTickerHub` class and puts it in the `ticker` variable.</span></span> <span data-ttu-id="d92b1-266">代理名稱是由`HubName`屬性設定的名稱:</span><span class="sxs-lookup"><span data-stu-id="d92b1-266">The proxy name is the name that was set by the `HubName` attribute:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

<span data-ttu-id="d92b1-267">定義所有變數和函數後,檔中的最後一行代碼通過調用 SignalR 函數初始化 SignalR`start`連接。</span><span class="sxs-lookup"><span data-stu-id="d92b1-267">After you define all the variables and functions, the last line of code in the file initializes the SignalR connection by calling the SignalR `start` function.</span></span> <span data-ttu-id="d92b1-268">函數`start`非同步執行並傳回[jQuery 延遲物件](http://api.jquery.com/category/deferred-object/)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-268">The `start` function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/).</span></span> <span data-ttu-id="d92b1-269">可以調用完成函數來指定應用完成非同步操作時要調用的函數。</span><span class="sxs-lookup"><span data-stu-id="d92b1-269">You can call the done function to specify the function to call when the app finishes the asynchronous action.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a><span data-ttu-id="d92b1-270">取得所有股票</span><span class="sxs-lookup"><span data-stu-id="d92b1-270">Getting all the stocks</span></span>

<span data-ttu-id="d92b1-271">該`init`函數調用伺服器上`getAllStocks`的函數,並使用伺服器返回的資訊來更新庫存表。</span><span class="sxs-lookup"><span data-stu-id="d92b1-271">The `init` function calls the `getAllStocks` function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="d92b1-272">請注意,默認情況下,您必須在用戶端上使用 camelCasing,即使方法名稱在伺服器上是 pascalcase 的。</span><span class="sxs-lookup"><span data-stu-id="d92b1-272">Notice that, by default, you have to use camelCasing on the client even though the method name is pascal-cased on the server.</span></span> <span data-ttu-id="d92b1-273">CamelCasing 規則僅適用於方法,不適用於物件。</span><span class="sxs-lookup"><span data-stu-id="d92b1-273">The camelCasing rule only applies to methods, not objects.</span></span> <span data-ttu-id="d92b1-274">例如,`stock.Symbol`您參考`stock.Price`與`stock.symbol`,`stock.price`而不是或 。</span><span class="sxs-lookup"><span data-stu-id="d92b1-274">For example, you refer to `stock.Symbol` and `stock.Price`, not `stock.symbol` or `stock.price`.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

<span data-ttu-id="d92b1-275">在`init`方法中,應用透過`formatStock`調用物件的屬性`stock`格式化,然後調`supplant`用將變數中的`rowTemplate`占位符替換`stock`為 物件屬性值,為從伺服器接收的每個股票物件的表行創建 HTML。</span><span class="sxs-lookup"><span data-stu-id="d92b1-275">In the `init` method, the app creates HTML for a table row for each stock object received from the server by calling `formatStock` to format properties of the `stock` object, and then by calling `supplant` to replace placeholders in the `rowTemplate` variable with the `stock` object property values.</span></span> <span data-ttu-id="d92b1-276">然後,生成的 HTML 將追加到庫存表中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-276">The resulting HTML is then appended to the stock table.</span></span>

> [!NOTE]
> <span data-ttu-id="d92b1-277">通過將其`init`作為`callback`在非`start`同步函數完成後執行的函數傳入來調用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-277">You call `init` by passing it in as a `callback` function that executes after the asynchronous `start` function finishes.</span></span> <span data-ttu-id="d92b1-278">如果在調用`start``init`後 調用作為單獨的 JavaScript 語句調用 ,則函數將失敗,因為它將立即運行,而無需等待啟動函數完成建立連接。</span><span class="sxs-lookup"><span data-stu-id="d92b1-278">If you called `init` as a separate JavaScript statement after calling `start`, the function would fail because it would run immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="d92b1-279">在這種情況下,`init`該函數將嘗試`getAllStocks`在 應用建立伺服器連接之前調用該函數。</span><span class="sxs-lookup"><span data-stu-id="d92b1-279">In that case, the `init` function would try to call the `getAllStocks` function before the app establishes a server connection.</span></span>

#### <a name="getting-updated-stock-prices"></a><span data-ttu-id="d92b1-280">取得更新的股票價格</span><span class="sxs-lookup"><span data-stu-id="d92b1-280">Getting updated stock prices</span></span>

<span data-ttu-id="d92b1-281">當伺服器更改股票價格時,它將調用`updateStockPrice`連接的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-281">When the server changes a stock's price, it calls the `updateStockPrice` on connected clients.</span></span> <span data-ttu-id="d92b1-282">應用將該函數添加到代理的用戶端屬性,`stockTicker`使其可用於來自伺服器的調用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-282">The app adds the function to the client property of the `stockTicker` proxy to make it available to calls from the server.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

<span data-ttu-id="d92b1-283">該`updateStockPrice`函數將從伺服器接收的 Stock 物件格式化為表行,其方式`init`與函數 中相同。</span><span class="sxs-lookup"><span data-stu-id="d92b1-283">The `updateStockPrice` function formats a stock object received from the server into a table row the same way as in the `init` function.</span></span> <span data-ttu-id="d92b1-284">它不是將行追加到表中,而是在表中查找股票的當前行,並將該行替換為新行。</span><span class="sxs-lookup"><span data-stu-id="d92b1-284">Instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

## <a name="test-the-application"></a><span data-ttu-id="d92b1-285">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="d92b1-285">Test the application</span></span>

<span data-ttu-id="d92b1-286">您可以測試應用以確保其正常工作。</span><span class="sxs-lookup"><span data-stu-id="d92b1-286">You can test the app to make sure it's working.</span></span> <span data-ttu-id="d92b1-287">您將看到所有瀏覽器視窗顯示股票價格波動的即時庫存表。</span><span class="sxs-lookup"><span data-stu-id="d92b1-287">You'll see all browser windows display the live stock table with stock prices fluctuating.</span></span>

1. <span data-ttu-id="d92b1-288">在工具列中,打開**腳本調試**,然後選擇播放按鈕以在除錯模式下運行應用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-288">In the toolbar, turn on **Script Debugging** and then select the play button to run the app in Debug mode.</span></span>

    ![用戶打開調試模式和選擇播放的屏幕截圖。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    <span data-ttu-id="d92b1-290">將開啟瀏覽器視窗,顯示**即時庫存表**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-290">A browser window will open displaying the **Live Stock Table**.</span></span> <span data-ttu-id="d92b1-291">庫存表最初顯示"載入..."行,然後,在很短的時間后,應用程序顯示初始股票數據,然後股票價格開始變化。</span><span class="sxs-lookup"><span data-stu-id="d92b1-291">The stock table initially shows the "loading..." line, then, after a short time, the app shows the initial stock data, and then the stock prices start to change.</span></span>

1. <span data-ttu-id="d92b1-292">從瀏覽器複製 URL,打開另外兩個瀏覽器,並將 URL 貼上到位址列中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-292">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

    <span data-ttu-id="d92b1-293">初始庫存顯示與第一個瀏覽器相同,更改同時發生。</span><span class="sxs-lookup"><span data-stu-id="d92b1-293">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>

1. <span data-ttu-id="d92b1-294">關閉所有瀏覽器,打開新瀏覽器,然後轉到相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="d92b1-294">Close all browsers, open a new browser, and go to the same URL.</span></span>

    <span data-ttu-id="d92b1-295">StockTicker 單例物件繼續在伺服器中運行。</span><span class="sxs-lookup"><span data-stu-id="d92b1-295">The StockTicker singleton object continued to run in the server.</span></span> <span data-ttu-id="d92b1-296">**即時庫存表**顯示,股票繼續變化。</span><span class="sxs-lookup"><span data-stu-id="d92b1-296">The **Live Stock Table** shows that the stocks have continued to change.</span></span> <span data-ttu-id="d92b1-297">您看不到具有零更改數位的初始表。</span><span class="sxs-lookup"><span data-stu-id="d92b1-297">You don't see the initial table with zero change figures.</span></span>

1. <span data-ttu-id="d92b1-298">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d92b1-298">Close the browser.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="d92b1-299">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="d92b1-299">Enable logging</span></span>

<span data-ttu-id="d92b1-300">SignalR 具有內建日誌記錄功能,您可以在用戶端上啟用該功能,以幫助進行故障排除。</span><span class="sxs-lookup"><span data-stu-id="d92b1-300">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="d92b1-301">在本節中,您可以啟用日誌記錄,並查看範例,這些範例顯示了日誌如何告訴您 SignalR 正在使用以下哪種傳輸方法:</span><span class="sxs-lookup"><span data-stu-id="d92b1-301">In this section, you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

* <span data-ttu-id="d92b1-302">[WebSockets,](http://en.wikipedia.org/wiki/WebSocket)由IIS 8和當前瀏覽器支援。</span><span class="sxs-lookup"><span data-stu-id="d92b1-302">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>

* <span data-ttu-id="d92b1-303">[伺服器發送的事件](http://en.wikipedia.org/wiki/Server-sent_events),由 Internet 資源管理器以外的瀏覽器支援。</span><span class="sxs-lookup"><span data-stu-id="d92b1-303">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>

* <span data-ttu-id="d92b1-304">[永久幀](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe),由 Internet 資源管理員支援。</span><span class="sxs-lookup"><span data-stu-id="d92b1-304">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>

* <span data-ttu-id="d92b1-305">[Ajax長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling),由所有瀏覽器支援。</span><span class="sxs-lookup"><span data-stu-id="d92b1-305">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="d92b1-306">對於任何給定的連接,SignalR 選擇伺服器和用戶端都支援的最佳傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-306">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="d92b1-307">開啟*股票Ticker.js*.</span><span class="sxs-lookup"><span data-stu-id="d92b1-307">Open *StockTicker.js*.</span></span>

1. <span data-ttu-id="d92b1-308">新增此突顯的代碼列,以便在檔案末尾初始化連線的代碼之前啟用紀錄記錄:</span><span class="sxs-lookup"><span data-stu-id="d92b1-308">Add this highlighted line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. <span data-ttu-id="d92b1-309">按**F5**以運行專案。</span><span class="sxs-lookup"><span data-stu-id="d92b1-309">Press **F5** to run the project.</span></span>

1. <span data-ttu-id="d92b1-310">打開瀏覽器的開發人員工具視窗,然後選擇主控台以查看日誌。</span><span class="sxs-lookup"><span data-stu-id="d92b1-310">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="d92b1-311">您可能需要刷新頁面才能看到 SignalR 協商新連線傳輸方法的日誌。</span><span class="sxs-lookup"><span data-stu-id="d92b1-311">You might have to refresh the page to see the logs of SignalR negotiating the transport method for a new connection.</span></span>

    * <span data-ttu-id="d92b1-312">如果您在 Windows 8 (IIS 8) 上運行 Internet 資源管理器 10,則傳輸方法是**WebSocket。**</span><span class="sxs-lookup"><span data-stu-id="d92b1-312">If you're running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

    * <span data-ttu-id="d92b1-313">如果您在 Windows 7(IIS 7.5)上執行 Internet 資源管理員 10,則傳輸方法是**iframe**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-313">If you're running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is **iframe**.</span></span>

    * <span data-ttu-id="d92b1-314">如果您在 Windows 8 (IIS 8) 上運行 Firefox 19,則傳輸方法是**WebSocket。**</span><span class="sxs-lookup"><span data-stu-id="d92b1-314">If you're running Firefox 19 on Windows 8 (IIS 8), the transport method is **WebSockets**.</span></span>

        > [!TIP]
        > <span data-ttu-id="d92b1-315">在 Firefox 中,安裝 Firebug 外接程式以獲取控制台視窗。</span><span class="sxs-lookup"><span data-stu-id="d92b1-315">In Firefox, install the Firebug add-in to get a Console window.</span></span>

    * <span data-ttu-id="d92b1-316">如果您在 Windows 7(IIS 7.5)上運行 Firefox 19,則傳輸方法是**伺服器發送**的事件。</span><span class="sxs-lookup"><span data-stu-id="d92b1-316">If you're running Firefox 19 on Windows 7 (IIS 7.5), the transport method is **server-sent** events.</span></span>

## <a name="install-the-stockticker-sample"></a><span data-ttu-id="d92b1-317">安裝庫存價格範例</span><span class="sxs-lookup"><span data-stu-id="d92b1-317">Install the StockTicker sample</span></span>

<span data-ttu-id="d92b1-318">[微軟.AspNet.SignalR.sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample)安裝StockTicker應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-318">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) installs the StockTicker application.</span></span> <span data-ttu-id="d92b1-319">與從頭開始創建的簡化版本相比,NuGet 包包含的功能更多。</span><span class="sxs-lookup"><span data-stu-id="d92b1-319">The NuGet package includes more features than the simplified version that you created from scratch.</span></span> <span data-ttu-id="d92b1-320">在本教學的這一部分中,您可以安裝 NuGet 包並查看新功能和實現這些功能的代碼。</span><span class="sxs-lookup"><span data-stu-id="d92b1-320">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d92b1-321">如果不執行本教程的早期步驟,安裝包,則必須向專案添加 OWIN 啟動類。</span><span class="sxs-lookup"><span data-stu-id="d92b1-321">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="d92b1-322">NuGet 套件的此 readme.txt 檔解釋了此步驟。</span><span class="sxs-lookup"><span data-stu-id="d92b1-322">This readme.txt file for the NuGet package explains this step.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="d92b1-323">安裝訊號R.樣品 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="d92b1-323">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="d92b1-324">在**解決方案資源管理員**中,右鍵單擊專案並選擇 **「管理 NuGet 包**」 。。</span><span class="sxs-lookup"><span data-stu-id="d92b1-324">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="d92b1-325">在**NuGet 套件管理器中:SignalR.StockTicker**,選擇 **「瀏覽**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-325">In **NuGet Package manager: SignalR.StockTicker**, select **Browse**.</span></span>

1. <span data-ttu-id="d92b1-326">從**包源**中,選擇**nuget.org。**</span><span class="sxs-lookup"><span data-stu-id="d92b1-326">From **Package source**, select **nuget.org**.</span></span>

1. <span data-ttu-id="d92b1-327">在搜尋框中輸入*SignalR.範例*,然後選擇**Microsoft.AspNet.SignalR.範例** > **安裝**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-327">Enter *SignalR.Sample* in the search box and select **Microsoft.AspNet.SignalR.Sample** > **Install**.</span></span>

1. <span data-ttu-id="d92b1-328">在**解決方案資源管理員中**,展開*SignalR.Sample*資料夾。</span><span class="sxs-lookup"><span data-stu-id="d92b1-328">In **Solution Explorer**, expand the *SignalR.Sample* folder.</span></span>

    <span data-ttu-id="d92b1-329">安裝 SignalR.Sample 包創建了資料夾及其內容。</span><span class="sxs-lookup"><span data-stu-id="d92b1-329">Installing the SignalR.Sample package created the folder and its contents.</span></span>

1. <span data-ttu-id="d92b1-330">在*SignalR.sample*資料夾中,右鍵單擊*StockTicker.html*,然後選擇「**設定為起始頁**」。</span><span class="sxs-lookup"><span data-stu-id="d92b1-330">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then select **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d92b1-331">安裝 SignalR.sample NuGet 套件可能會更改*文稿*資料夾中的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="d92b1-331">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="d92b1-332">包在*SignalR.Sample*資料夾中安裝的新*StockTicker.html*檔案將與包安裝的 jQuery 版本同步,但如果要再次運行原始*StockTicker.html*檔,您可能需要首先更新腳本標記中的 jQuery 引用。</span><span class="sxs-lookup"><span data-stu-id="d92b1-332">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="d92b1-333">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d92b1-333">Run the application</span></span>

 <span data-ttu-id="d92b1-334">您在第一個應用中看到的表具有有用的功能。</span><span class="sxs-lookup"><span data-stu-id="d92b1-334">The table that you saw in the first app had useful features.</span></span> <span data-ttu-id="d92b1-335">完整的股票代碼應用程式顯示新的功能:一個水準滾動視窗,顯示股票數據和股票的變化顏色,因為他們的上升和下降。</span><span class="sxs-lookup"><span data-stu-id="d92b1-335">The full stock ticker application shows new features: a horizontally scrolling window that shows the stock data and stocks that change color as they rise and fall.</span></span>

1. <span data-ttu-id="d92b1-336">按 **F5** 以執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-336">Press **F5** to run the app.</span></span>

     <span data-ttu-id="d92b1-337">首次運行應用時,"市場"是"關閉的",您將看到一個靜態表和一個未滾動的刻度視窗。</span><span class="sxs-lookup"><span data-stu-id="d92b1-337">When you run the app for the first time, the "market" is "closed" and you see a static table and a ticker window that isn't scrolling.</span></span>

1. <span data-ttu-id="d92b1-338">選擇**公開市場**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-338">Select **Open Market**.</span></span>

    ![即時代碼的屏幕截圖。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * <span data-ttu-id="d92b1-340">**即時庫存報價框**開始水準滾動,伺服器開始隨機廣播股票價格變化。</span><span class="sxs-lookup"><span data-stu-id="d92b1-340">The **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span>

    * <span data-ttu-id="d92b1-341">每次股票價格變化時,應用程式都會更新**即時庫存表**和**即時股票報價器**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-341">Each time a stock price changes, the app updates both the **Live Stock Table** and the **Live Stock Ticker**.</span></span>

    * <span data-ttu-id="d92b1-342">當股票價格變化為正時,應用程式將顯示具有綠色背景的股票。</span><span class="sxs-lookup"><span data-stu-id="d92b1-342">When a stock's price change is positive, the app shows the stock with a green background.</span></span>

    * <span data-ttu-id="d92b1-343">當更改為負時,應用程式將顯示具有紅色背景的股票。</span><span class="sxs-lookup"><span data-stu-id="d92b1-343">When the change is negative, the app shows the stock with a red background.</span></span>

1. <span data-ttu-id="d92b1-344">選擇**關閉市場**。</span><span class="sxs-lookup"><span data-stu-id="d92b1-344">Select **Close Market**.</span></span>

    * <span data-ttu-id="d92b1-345">表更新停止。</span><span class="sxs-lookup"><span data-stu-id="d92b1-345">The table updates stop.</span></span>

    * <span data-ttu-id="d92b1-346">刻度線停止滾動。</span><span class="sxs-lookup"><span data-stu-id="d92b1-346">The ticker stops scrolling.</span></span>

1. <span data-ttu-id="d92b1-347">選取 [重設]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d92b1-347">Select **Reset**.</span></span>

    * <span data-ttu-id="d92b1-348">重置所有庫存數據。</span><span class="sxs-lookup"><span data-stu-id="d92b1-348">All stock data is reset.</span></span>

    * <span data-ttu-id="d92b1-349">應用在價格更改開始之前還原初始狀態。</span><span class="sxs-lookup"><span data-stu-id="d92b1-349">The app restores the initial state before price changes started.</span></span>

1. <span data-ttu-id="d92b1-350">從瀏覽器複製 URL,打開另外兩個瀏覽器,並將 URL 貼上到位址列中。</span><span class="sxs-lookup"><span data-stu-id="d92b1-350">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="d92b1-351">在每個瀏覽器中,您都會看到相同的數據同時動態更新。</span><span class="sxs-lookup"><span data-stu-id="d92b1-351">You see the same data dynamically updated at the same time in each browser.</span></span>

1. <span data-ttu-id="d92b1-352">當您選擇任何控制項時,所有瀏覽器都同時以相同的方式回應。</span><span class="sxs-lookup"><span data-stu-id="d92b1-352">When you select any of the controls, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="d92b1-353">即時庫存報價顯示</span><span class="sxs-lookup"><span data-stu-id="d92b1-353">Live Stock Ticker display</span></span>

<span data-ttu-id="d92b1-354">**即時庫存報價顯示**是按 CSS 樣式`<div>`格式化為 單行的元素中的無序列表。</span><span class="sxs-lookup"><span data-stu-id="d92b1-354">The **Live Stock Ticker** display is an unordered list in a `<div>` element formatted into a single line by CSS styles.</span></span> <span data-ttu-id="d92b1-355">應用以與表相同的方式初始化和更新代碼:透過在`<li>`樣本字串中替換占位符並動態地將`<li>`元素添加到`<ul>`元素。</span><span class="sxs-lookup"><span data-stu-id="d92b1-355">The app initializes and updates the ticker the same way as the table: by replacing placeholders in an `<li>` template string and dynamically adding the `<li>` elements to the `<ul>` element.</span></span> <span data-ttu-id="d92b1-356">該應用程式包括使用 jQuery`animate`函數來更改 中無序列表的邊距左側`<div>`滾動。</span><span class="sxs-lookup"><span data-stu-id="d92b1-356">The app includes  scrolling by using the jQuery `animate` function to vary the margin-left of the unordered list within the `<div>`.</span></span>

#### <a name="signalrsample-stocktickerhtml"></a><span data-ttu-id="d92b1-357">訊號R.樣品庫存Ticker.html</span><span class="sxs-lookup"><span data-stu-id="d92b1-357">SignalR.Sample StockTicker.html</span></span>

<span data-ttu-id="d92b1-358">股票代碼 HTML 碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-358">The stock ticker HTML code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a><span data-ttu-id="d92b1-359">信號R.樣品庫存Ticker.css</span><span class="sxs-lookup"><span data-stu-id="d92b1-359">SignalR.Sample StockTicker.css</span></span>

<span data-ttu-id="d92b1-360">股票代碼 CSS 碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-360">The stock ticker CSS code:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a><span data-ttu-id="d92b1-361">訊號R.樣品信號R.StockTicker.js</span><span class="sxs-lookup"><span data-stu-id="d92b1-361">SignalR.Sample SignalR.StockTicker.js</span></span>

<span data-ttu-id="d92b1-362">使其捲動的 jQuery 代碼:</span><span class="sxs-lookup"><span data-stu-id="d92b1-362">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="d92b1-363">用戶端可呼叫的伺服器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="d92b1-363">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="d92b1-364">為了增加應用的靈活性,應用可以調用其他方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-364">To add flexibility to the app, there are additional methods the app can call.</span></span>

#### <a name="signalrsample-stocktickerhubcs"></a><span data-ttu-id="d92b1-365">訊號R.樣品StockTickerHub.cs</span><span class="sxs-lookup"><span data-stu-id="d92b1-365">SignalR.Sample StockTickerHub.cs</span></span>

<span data-ttu-id="d92b1-366">該`StockTickerHub`類別定義了客戶端可以調用的其他四種方法:</span><span class="sxs-lookup"><span data-stu-id="d92b1-366">The `StockTickerHub` class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="d92b1-367">套用`OpenMarket`,`CloseMarket`並`Reset`回應頁面頂部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d92b1-367">The app calls `OpenMarket`, `CloseMarket`, and `Reset` in response to the buttons at the top of the page.</span></span> <span data-ttu-id="d92b1-368">它們演示了一個用戶端觸發狀態更改的模式,該更改將立即傳播到所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="d92b1-368">They demonstrate the pattern of one client triggering a change in state immediately propagated to all clients.</span></span> <span data-ttu-id="d92b1-369">這些方法中的每種方法都調用類中`StockTicker`導致市場狀態更改然後廣播新狀態的方法。</span><span class="sxs-lookup"><span data-stu-id="d92b1-369">Each of these methods calls a method in the `StockTicker` class that causes the market state change and then broadcasts the new state.</span></span>

#### <a name="signalrsample-stocktickercs"></a><span data-ttu-id="d92b1-370">信號R.樣品StockTicker.cs</span><span class="sxs-lookup"><span data-stu-id="d92b1-370">SignalR.Sample StockTicker.cs</span></span>

<span data-ttu-id="d92b1-371">在類`StockTicker`中,應用使用`MarketState``MarketState`返回 枚舉值的屬性維護市場狀態:</span><span class="sxs-lookup"><span data-stu-id="d92b1-371">In the `StockTicker` class, the app maintains the state of the market with a `MarketState` property that returns a `MarketState` enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="d92b1-372">變更市場狀態的每個方法都會在鎖區內執行此操作,`StockTicker`因為類別必須是線程安全的:</span><span class="sxs-lookup"><span data-stu-id="d92b1-372">Each of the methods that change the market state do so inside a lock block because the `StockTicker` class has to be thread-safe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="d92b1-373">為了確保此代碼是線程安全的,支援指定的`_marketState``MarketState``volatile`屬性的欄位:</span><span class="sxs-lookup"><span data-stu-id="d92b1-373">To make sure this code is thread-safe, the `_marketState` field that backs the `MarketState` property designated `volatile`:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="d92b1-374">`BroadcastMarketStateChange`和`BroadcastMarketReset`方法與您已經看到的廣播股票價格方法類似,但它們調用在用戶端定義的不同方法:</span><span class="sxs-lookup"><span data-stu-id="d92b1-374">The `BroadcastMarketStateChange` and `BroadcastMarketReset` methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="d92b1-375">伺服器可以呼叫的用戶端上的其他功能</span><span class="sxs-lookup"><span data-stu-id="d92b1-375">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="d92b1-376">該`updateStockPrice`函數現在同時處理表和刻度顯示,它`jQuery.Color`用於閃爍紅色和綠色。</span><span class="sxs-lookup"><span data-stu-id="d92b1-376">The `updateStockPrice` function now handles both the table and the ticker display, and it uses `jQuery.Color` to flash red and green colors.</span></span>

<span data-ttu-id="d92b1-377">*SignalR.StockTicker.js*中的新功能根據市場狀態啟用和禁用按鈕。</span><span class="sxs-lookup"><span data-stu-id="d92b1-377">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state.</span></span> <span data-ttu-id="d92b1-378">它們還會停止或啟動**即時庫存刻度**水平滾動。</span><span class="sxs-lookup"><span data-stu-id="d92b1-378">They also stop or start the **Live Stock Ticker** horizontal scrolling.</span></span> <span data-ttu-id="d92b1-379">由於許多函數被添加到`ticker.client`,應用程式使用[jQuery 擴展函數](http://api.jquery.com/jQuery.extend/)來添加它們。</span><span class="sxs-lookup"><span data-stu-id="d92b1-379">Since many functions are being added to `ticker.client`, the app uses the [jQuery extend function](http://api.jquery.com/jQuery.extend/) to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="d92b1-380">建立連線後的其他客戶端設定</span><span class="sxs-lookup"><span data-stu-id="d92b1-380">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="d92b1-381">用戶端建立連接後,它還有一些額外的工作要做:</span><span class="sxs-lookup"><span data-stu-id="d92b1-381">After the client establishes the connection, it has some additional work to do:</span></span>

* <span data-ttu-id="d92b1-382">瞭解市場是開放的還是關閉的,以調用適當的`marketOpened`或`marketClosed`功能。</span><span class="sxs-lookup"><span data-stu-id="d92b1-382">Find out if the market is open or closed to call the appropriate `marketOpened` or `marketClosed` function.</span></span>

* <span data-ttu-id="d92b1-383">將伺服器方法調用附加到按鈕。</span><span class="sxs-lookup"><span data-stu-id="d92b1-383">Attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="d92b1-384">伺服器方法直到應用建立連接後才會連接到按鈕。</span><span class="sxs-lookup"><span data-stu-id="d92b1-384">The server methods aren't wired up to the buttons until after the app establishes the connection.</span></span> <span data-ttu-id="d92b1-385">因此,代碼在伺服器方法可用之前無法調用它們。</span><span class="sxs-lookup"><span data-stu-id="d92b1-385">It's so the code can't call the server methods before they're available.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d92b1-386">其他資源</span><span class="sxs-lookup"><span data-stu-id="d92b1-386">Additional resources</span></span>

<span data-ttu-id="d92b1-387">在本教學中,您學習了如何對將消息從伺服器廣播到所有連接用戶端的 SignalR 應用程式進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="d92b1-387">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients.</span></span> <span data-ttu-id="d92b1-388">現在,您可以定期廣播消息,並回應來自任何用戶端的通知。</span><span class="sxs-lookup"><span data-stu-id="d92b1-388">Now you can broadcast messages on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="d92b1-389">您可以使用多線程單例實例的概念在多人線上遊戲方案中維護伺服器狀態。</span><span class="sxs-lookup"><span data-stu-id="d92b1-389">You can use the concept of multi-threaded singleton instance to maintain server state in multi-player online game scenarios.</span></span> <span data-ttu-id="d92b1-390">例如,請參閱基於[SignalR 的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-390">For an example, see [the ShootR game based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="d92b1-391">有關顯示對等通訊場景的教學,請參閱[使用 SignalR 入門](introduction-to-signalr.md)與使用[SignalR 進行即時更新](tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="d92b1-391">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="d92b1-392">有關 SignalR 的更多,請參閱以下資源:</span><span class="sxs-lookup"><span data-stu-id="d92b1-392">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="d92b1-393">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="d92b1-393">ASP.NET SignalR</span></span>](../../index.md)
* [<span data-ttu-id="d92b1-394">信號器專案</span><span class="sxs-lookup"><span data-stu-id="d92b1-394">SignalR Project</span></span>](http://signalr.net/)
* [<span data-ttu-id="d92b1-395">訊號R GitHub 與範例</span><span class="sxs-lookup"><span data-stu-id="d92b1-395">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)
* [<span data-ttu-id="d92b1-396">信號R維琪</span><span class="sxs-lookup"><span data-stu-id="d92b1-396">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="d92b1-397">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d92b1-397">Next steps</span></span>

<span data-ttu-id="d92b1-398">在本教學課程中，您：</span><span class="sxs-lookup"><span data-stu-id="d92b1-398">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d92b1-399">已建立項目</span><span class="sxs-lookup"><span data-stu-id="d92b1-399">Created the project</span></span>
> * <span data-ttu-id="d92b1-400">設定伺服器程式碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-400">Set up the server code</span></span>
> * <span data-ttu-id="d92b1-401">檢查伺服器代碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-401">Examined the server code</span></span>
> * <span data-ttu-id="d92b1-402">設定客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-402">Set up the client code</span></span>
> * <span data-ttu-id="d92b1-403">檢查客戶端碼</span><span class="sxs-lookup"><span data-stu-id="d92b1-403">Examined the client code</span></span>
> * <span data-ttu-id="d92b1-404">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="d92b1-404">Tested the application</span></span>
> * <span data-ttu-id="d92b1-405">開啟紀錄記錄</span><span class="sxs-lookup"><span data-stu-id="d92b1-405">Enabled logging</span></span>

<span data-ttu-id="d92b1-406">進入下一篇文章,瞭解如何創建使用ASP.NET SignalR 2的即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d92b1-406">Advance to the next article to learn how to create a real-time web application that uses ASP.NET SignalR 2.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d92b1-407">使用 SignalR 建立即時 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d92b1-407">Create real-time web app with SignalR</span></span>](real-time-web-applications-with-signalr.md)
