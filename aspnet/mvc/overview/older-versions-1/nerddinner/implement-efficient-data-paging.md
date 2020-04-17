---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 實現高效的數據分頁 |微軟文件
author: rick-anderson
description: 步驟 8 演示如何向 /Dinners URL 添加尋呼支援,以便我們一次不顯示 1000 份晚餐,我們僅在...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: a833553fe44b62b136f7eb55c7e00eca0b0462c6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541321"
---
# <a name="implement-efficient-data-paging"></a>實作有效率的資料分頁

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第8步,該教程示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。
> 
> 步驟 8 演示如何向我們的 /Dinners URL 添加尋呼支援,以便我們一次只顯示 10 份即將舉辦的晚餐,並且允許最終使用者以 SEO 友好的方式回傳整個清單。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-8-paging-support"></a>神經晚餐步驟 8: 尋呼支援

如果我們的網站成功,它將有成千上萬的即將到來的晚餐。 我們需要確保我們的 UI 擴展以處理所有這些晚餐,並允許用戶瀏覽它們。 為了啟用這一點,我們將添加分頁支援到我們的 */Dinners* URL,以便我們不是一次顯示 1000 份晚餐,而是一次只顯示 10 份即將舉辦的晚餐 -並允許最終使用者以 SEO 友好的方式回傳和轉發整個清單。

### <a name="index-action-method-recap"></a>索引() 操作方法回顧

我們的 DinnersController 類別中的 Index() 操作方法目前所示:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

當對 */Dinners* URL 發出請求時,它會檢索所有即將舉辦的晚宴的清單,然後呈現所有這些晚宴的清單:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>瞭解可&lt;查詢 T&gt;

*IQuery&lt;&gt;T*是 LINQ 作為 .NET 3.5 的一部分引入的介面。 它支持強大的"延遲執行"方案,我們可以利用這些場景來實現分頁支援。

在我們的晚餐存儲庫中,我們將從我們的「查找晚餐&lt;&gt;」 方法返回一個可查詢的晚餐序列:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

我們的 Find&lt;&gt;對托 晚餐() 方法傳回的 I 可查詢晚餐物件封裝了一個查詢,以便使用 LINQ 從我們的資料庫中檢索 Dinner 物件,使用 LINQ 到 SQL。 重要的是,在我們嘗試訪問/反覆運算查詢中的數據之前,或者直到我們調用查詢上的 ToList() 方法之前,它不會對資料庫執行查詢。 調用我們的 Find 對興晚餐() 方法的代碼可以選擇在執行查詢之前向&lt;IQuery Dinner&gt;物件添加其他「連結」操作/篩選器。 然後,LINQ 到 SQL 足夠智慧,在請求數據時對資料庫執行組合查詢。

為了實現分頁邏輯,我們可以更新我們的 DinnersController Index() 操作方法,以便它在調用 ToList() 之前,將其他「&lt;跳&gt;過」和「 獲取 」運算元應用於返回的可查詢晚餐序列:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上述代碼跳過資料庫中即將進行的 10 份晚餐,然後返回 20 份晚餐。 LINQ 到 SQL 足夠智慧,可以建構最佳化的 SQL 查詢,該查詢在 SQL 資料庫中執行此跳過邏輯,而不是在 Web 伺服器中執行此跳過邏輯。 這意味著,即使我們資料庫中有數百萬個即將推出的 Dinner,也只能檢索我們想要的 10 個,作為此請求的一部分(使其高效且可擴展)。

### <a name="adding-a-page-value-to-the-url"></a>新增頁面的頁面值

我們希望我們的 URL 包含一個「頁面」參數,指示使用者請求的「晚餐範圍」,而不是對特定頁面範圍進行硬編碼。

#### <a name="using-a-querystring-value"></a>使用查詢字串值

下面的程式碼展示如何更新我們的 Index() 操作方法以支援查詢字串參數,並啟用 URL,如 */Dinners page_2*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上面的 Index() 操作方法具有名為「頁」的參數。 參數聲明為空整數(即 int? 指示)。 這意味著 */Dinners?page_2* URL將導致將值"2"作為參數值傳遞。 */Dinners* URL(沒有查詢字串值)將導致傳遞空值。

我們將頁面值乘以頁面大小(本例中為 10 行),以確定要跳過的晚餐數。 我們使用[C# null"合併「運算符 (?),](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx)在處理可無類型時非常有用。 如果頁面參數為空,上述代碼將值為 0 分配給頁。

#### <a name="using-embedded-url-values"></a>使用嵌入式網址值

使用查詢字串值的替代方法是將頁面參數嵌入到實際 URL 本身中。 例如 *:/晚餐/頁/2*或 */Dinner/2*。 ASP.NET MVC 包含強大的 URL 路由引擎,便於支援類似方案。

我們可以註冊自定義路由規則,將任何傳入 URL 或 URL 格式映射到所需的任何控制器類或操作方法。 我們只需要在我們的項目中打開 Global.asax 檔:

![](implement-efficient-data-paging/_static/image2.png)

然後使用 MapRoute() 幫助器方法註冊新的映射規則,如對路由的第一次調用。地圖路線() 如下:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

上圖,我們正在註冊一個名為"即將推出的晚餐"的新路由規則。 我們指示它有 URL 格式"Dinners/page/{頁面}" - 其中 [頁面] 是嵌入在 URL 中的參數值。 MapRoute() 方法的第三個參數指示我們應該映射此格式與 DinnersController 類上的 Index() 操作方法相匹配的 URL。

我們可以在查詢字串方案中使用我們以前完全相同的 Index() 代碼,除非現在我們的「頁面」參數將來自 URL 而不是查詢字串:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

現在,當我們運行應用程式並輸入 */Dinner 時*,我們將看到前 10 場即將舉辦的晚宴:

![](implement-efficient-data-paging/_static/image3.png)

當我們輸入 */Dinner/Page/1*時,我們將看到晚餐的下一頁:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>新增網頁瀏覽 UI

完成尋呼方案的最後一步是在我們的視圖範本中實現「下一步」和「上一個」導航 UI,以便用戶輕鬆跳過 Dinner 數據。

要正確實現這一點,我們需要知道資料庫中的 Dinner 的總數,以及它轉換為的數據頁數。 然後,我們需要計算當前請求的「頁面」值是在數據開頭還是結尾,並相應地顯示或隱藏「上一個」 和「下一個」 的 UI。 我們可以在 Index() 操作方法中實現此邏輯。 或者,我們可以向專案添加幫助器類,以更可重用的方式封裝此邏輯。

下面是一個簡單的"分頁清單"幫助器類,派生自內置於 .NET&lt;&gt;框架中的清單 T 集合類。 它實現了一個可重用的集合類,可用於分頁任何 IQuery 數據序列。 &lt;在我們的 NerdDinner 應用程式中,我們將針對 IQuery Dinner&gt;結果進行工作,但它在其他應用程式方案中可以同樣&lt;輕鬆&gt;地用於&lt;I&gt;可查詢 產品或可 查詢客戶 結果:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

請注意,它如何計算,然後公開屬性,如"頁面索引","頁面大小","總計數"和"總頁"。 然後,它還公開兩個幫助屬性"Has上頁"和"HasNextPage",指示集合中的數據頁是原始序列的開頭還是結尾。 上述代碼將導致運行兩個 SQL 查詢 - 第一個查詢檢索 Dinner 物件總數的計數(這不會返回物件- 而是執行返回整數的"SELECT COUNT"語句),第二個代碼將僅從資料庫中檢索當前數據頁所需的數據行。

然後,我們可以更新我們的晚餐控制器.Index() 説明方法,從我們的晚餐存儲庫創建一&lt;&gt;個 PaginatedList 晚餐。

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

然後,我們可以更新 [Views_Dinners_Index.aspx 視圖範本》,&lt;以便從ViewPage NerdDinner.Helpers.PaginatedList&lt;&gt;&gt;&lt;晚餐&lt;&gt;&gt;而不是ViewPage IE500s 晚宴上繼承,然後將以下代碼添加到視圖範本的底部,以顯示或隱藏下一個和以前的導航 UI:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

請注意,我們使用 Html.RouteLink() 説明器方法生成超連結的方式。 此方法類似於我們以前使用過的 Html.ActionLink() 説明程式方法。 區別在於,我們使用在 Global.asax 檔中設置的"即將到達的晚餐"路由規則生成 URL。 這可確保我們將生成索引() 操作方法的 URL,該方法的格式為 *:/Dinners/page/{page}* - 其中 [page] 值是我們基於當前 PageIndex 提供上述變數。

現在,當我們再次運行應用程式時,我們將在瀏覽器中一次看到 10 份晚餐:

![](implement-efficient-data-paging/_static/image5.png)

我們還在頁面&lt;&lt;&lt;&gt;&gt;底部&gt;具有和導航 UI,允許我們使用搜尋引擎可存取的網址 向前和向後跳過資料:

![](implement-efficient-data-paging/_static/image6.png)

| **側主題:瞭解可&lt;查詢 T 的含義&gt;** |
| --- |
| IQueryable&lt; &gt; T 是一個非常強大的功能,支援各種有趣的延遲執行方案(如分頁和基於合成的查詢)。 與所有強大的功能一樣,您希望小心如何使用它,並確保它不受濫用。 請務必認識到,從存儲庫返回 IQuery&lt;&gt;可查詢 T 結果可以調用代碼來追加到它上的鏈式運算符方法,從而參與最終查詢執行。 如果不想提供此能力的調用代碼,則應&lt;傳回 IList T&gt;或&lt;IE55ble T&gt;結果 - 其中包含已執行的查詢的結果。 對於分頁方案,這將要求您將實際數據暫停邏輯推送到被調用的存儲庫方法中。 在此方案中,我們可能會更新我們的 Find對價晚餐() 查找方法,以有一個簽名,該簽名要麼返回一個分&lt;&gt;頁清單&lt;:paginatedList 晚餐查找要約晚餐(int pageIndex,int page_info=2>)=或返回 IList 晚餐&gt;,並使用&lt;"&gt;總計數"外參數返回晚餐的 總數 :Ilist 晚餐查找要約晚餐(int 頁索引,int 頁大小) |

### <a name="next-step"></a>後續步驟

現在,讓我們來看看如何向應用程式添加身份驗證和授權支援。

> [!div class="step-by-step"]
> [前一個](re-use-ui-using-master-pages-and-partials.md)
> [下一個](secure-applications-using-authentication-and-authorization.md)
