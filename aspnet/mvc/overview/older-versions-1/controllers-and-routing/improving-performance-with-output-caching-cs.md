---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 通過輸出緩存 (C#) 提高性能 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何利用輸出緩存來顯著提高ASP.NET MVC Web 應用程式的性能。 你。。。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: a6dd43320117e235d12a13aa894302bbc767727c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542712"
---
# <a name="improving-performance-with-output-caching-c"></a>使用輸出快取改善效能 (C#)

由[微軟](https://github.com/microsoft)

> 在本教學中,您將瞭解如何利用輸出緩存來顯著提高ASP.NET MVC Web 應用程式的性能。 您將瞭解如何緩存從控制器操作返回的結果,以便在每次新用戶調用該操作時都不需要創建相同的內容。

本教學的目的是說明如何透過利用輸出緩存顯著提高ASP.NET MVC 應用程式的性能。 輸出緩存使您能夠快取控制器操作傳回的內容。 這樣,每次調用相同的控制器操作時,不需要生成相同的內容。

例如,假設您ASP.NET MVC 應用程式在名為 Index 的檢視中顯示資料庫記錄的清單。 通常,每次使用者調用返回 Index 視圖的控制器操作時,必須通過執行資料庫查詢從資料庫檢索資料庫記錄集。

另一方面,如果利用輸出緩存,則可以避免在每次任何用戶調用相同的控制器操作時執行資料庫查詢。 可以從緩存中檢視,而不是從控制器操作中重新生成檢視。 快取使您能夠避免在伺服器上執行冗餘工作。

## <a name="enabling-output-caching"></a>開啟輸出快取

通過將 [OutputCache] 屬性添加到單個控制器操作或整個控制器類來啟用輸出緩存。 例如,清單 1 中的控制器公開名為 Index() 的操作。 索引() 操作的輸出緩存 10 秒。

**清單1 = 控制器\主控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

在 ASP.NET MVC 的 Beta 版本中,輸出[http://www.MySite.com/](http://www.mysite.com/)緩存不適用於像的 URL。 相反,您必須輸入像[http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)的 URL。 

在清單 1 中,索引() 操作的輸出緩存 10 秒。 如果您願意,可以指定更長的緩存持續時間。 例如,如果要緩存控制器操作的輸出一天,則可以指定 86400 秒(60\*秒\*60 分鐘 24 小時)的緩存持續時間。

不能保證內容將在您指定的時間量內緩存。 當記憶體資源變低時,緩存將自動開始驅逐內容。

清單 1 中的主控制器返回清單 2 中的索引檢視。 這個觀點沒有什麼特別之處。 索引檢視僅顯示當前時間(參見圖 1)。

**清單 2 = 檢視\home_Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**圖 1 = 快取索引檢視**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

如果透過在瀏覽器的位址列中輸入 URL /Home/Index 並反覆點擊瀏覽器中的「刷新/重新載入」按鈕來多次調用 Index() 操作,則 Index 檢視顯示的時間在 10 秒內不會更改。 將顯示相同的時間,因為視圖是緩存的。

請務必瞭解,對於訪問應用程式的每個人,緩存相同的視圖。 調用 Index() 操作的任何人都可以獲得相同的索引檢視緩存版本。 這意味著 Web 伺服器為索引檢視提供服務而必須執行的工作量將大大減少。

清單2中的視圖碰巧在做一些非常簡單的事情。 視圖僅顯示當前時間。 但是,您可以同樣輕鬆地緩存顯示一組資料庫記錄的檢視。 在這種情況下,每次調用返回檢視的控制器操作時,就不需要從資料庫中檢索資料庫記錄集。 快取可以減少 Web 伺服器和資料庫伺服器必須執行的工作量。

不要在 MVC 檢視&lt;中 使用頁面&gt;%@ 輸出快取 % 指令。 此指令正在從 Web 窗體世界中出血,不應在 mVC 應用程式中 ASP.NET 中使用。

## <a name="where-content-is-cached"></a>快取內容的位置

預設情況下,當您使用 [OutputCache] 屬性時,內容緩存在三個位置:Web 伺服器、任何代理伺服器和 Web 瀏覽器。 您可以通過修改 [OutputCache] 屬性的位置屬性來準確控制內容的緩存位置。

您可以將「位置」屬性設定為以下任一值:

> ·任何
> 
> ·客戶
> 
> ·下游
> 
> ·伺服器
> 
> ·沒有
> 
> ·伺服器和用戶端

默認情況下,"位置"屬性具有"Any"的值。 但是,在某些情況下,您可能只想在瀏覽器或伺服器上緩存。 例如,如果要緩存針對每個使用者進行個人化的資訊,則不應在伺服器上緩存資訊。 如果要向不同的用戶顯示不同的資訊,則應僅在用戶端上緩存資訊。

例如,清單 3 中的控制器公開名為 GetName() 的操作,該操作傳回當前使用者名稱。 如果 Jack 登錄到網站並調用 GetName() 操作,則該操作將返回字串「嗨傑克」。 如果,隨後,Jill登錄到網站並調用 GetName() 操作,那麼她也將得到字串「嗨傑克」。。 在 Jack 最初呼叫控制器操作後,字串將緩存在 Web 伺服器上,供所有使用者使用。

**清單3 = 控制器\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

最有可能的是,清單 3 中的控制器不能以您想要的方式工作。 您不想向吉爾顯示「嗨傑克」的消息。

不應在伺服器緩存中緩存個性化內容。 但是,您可能希望在瀏覽器緩存中緩存個性化內容以提高性能。 如果在瀏覽器中緩存內容,並且使用者多次調用同一控制器操作,則可以從瀏覽器緩存而不是伺服器檢索內容。

清單 4 中修改後的控制器快取 GetName() 操作的輸出。 但是,內容僅緩存在瀏覽器上,而不是伺服器上。 這樣,當多個使用者調用 GetName() 方法時,每個人都會獲得自己的使用者名,而不是其他人的使用者名。

**清單4 = 控制器\使用者控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

請注意,清單 4 中的 [OutputCache] 屬性包含一個位置屬性設置為值輸出緩存位置.用戶端。 [輸出緩存] 屬性還包括 NoStore 屬性。 NoStore 屬性用於通知代理伺服器和瀏覽器它們不應存儲緩存內容的永久副本。

## <a name="varying-the-output-cache"></a>變更輸出快取

在某些情況下,您可能需要相同內容的不同緩存版本。 例如,假設您正在創建一個母版/詳細資訊頁。 母版頁顯示電影標題的清單。 按一下標題時,您將獲得所選影片的詳細資訊。

如果緩存詳細資訊頁,則無論單擊哪個影片,都會顯示同一影片的詳細資訊。 第一個用戶選擇的第一個影片將顯示給所有將來的使用者。

您可以通過利用 [OutputCache] 屬性的 VaryByParam 屬性來解決此問題。 此屬性使您能夠在表單參數或查詢字串參數不同時創建相同內容的不同快取版本。

例如,清單 5 中的控制器公開名為 Master() 和詳細資訊() 的兩個操作。 Master() 操作傳回影片標題清單,詳細資訊() 操作傳回所選影片的詳細資訊。

**清單5 = 控制器\電影控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master() 操作包括一個具有值"無"的 VaryByParam 屬性。 調用 Master() 操作時,將返回主檢視的相同緩存版本。 忽略任何表單參數或查詢字串參數(參見圖 2)。

**圖 2 = /電影/主檢視**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**圖 3 = /電影/詳細資訊檢視**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

詳細資訊() 操作包括一個帶值"Id"的 VaryByParam 屬性。 當將 Id 參數的不同值傳遞給控制器操作時,將生成「詳細資訊」檢視的不同緩存版本。

請務必瞭解,使用 VaryByParam 屬性會導致緩存更多,而不是更少。 為 Id 參數的每個不同版本創建「詳細資訊」檢視的不同緩存版本。

您可以將 VaryByParam 屬性設定為以下值:

> \*• 每當窗體或查詢字串參數發生變化時,都會創建不同的緩存版本。
> 
> 沒有 = 從不建立不同的快取版本
> 
> 參數的分號清單 = 每當清單中的任何窗體或查詢字串參數發生變化時,建立不同的緩存版本

## <a name="creating-a-cache-profile"></a>建立快取設定檔

作為透過修改 [OutputCache] 屬性的屬性來配置輸出緩存屬性的替代方法,您可以在 Web 設定 (web.config) 檔案中創建快取設定檔。 在 Web 設定檔中建立快取配置檔具有幾個重要優勢。

首先,通過在 Web 設定檔中配置輸出緩存,可以控制控制器操作如何在一個中心位置緩存內容。 您可以創建一個快取設定檔,並將設定檔應用於多個控制器或控制器操作。

其次,您可以修改 Web 配置檔,而無需重新編譯應用程式。 如果需要禁用已部署到生產中的應用程式的快取,則只需修改 Web 設定檔中定義的快取設定檔即可。 將自動檢測並應用對 Web 配置檔的任何更改。

例如,清單&lt;&gt;6 中的快取 Web 配置部分定義名為 Cache1Hour 的快取設定檔。 &lt;快取&gt;部分必須出現在 Web&lt;設定檔的 system.web&gt;部分中。

**清單6 = Web.config 的快取部分**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

清單7中的控制器說明了如何將 Cache1Hour 配置檔應用於具有 [OutputCache] 屬性的控制器操作。

**清單7 = 控制器\設定檔案控制器.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

如果調用清單 7 中控制器公開的 Index() 操作,則將返回相同的時間 1 小時。

## <a name="summary"></a>總結

輸出緩存為您提供了一種非常簡單的方法來顯著提高ASP.NET MVC 應用程式的性能。 在本教學中,您學習了如何使用 [OutputCache] 屬性來緩存控制器操作的輸出。 您還學習了如何修改 [OutputCache] 屬性的屬性,如持續時間和 VaryByParam 屬性,以修改內容的緩存方式。 最後,您學習了如何在 Web 設定檔中定義快取設定檔。

> [!div class="step-by-step"]
> [前一個](understanding-action-filters-cs.md)
> [下一個](adding-dynamic-content-to-a-cached-page-cs.md)
