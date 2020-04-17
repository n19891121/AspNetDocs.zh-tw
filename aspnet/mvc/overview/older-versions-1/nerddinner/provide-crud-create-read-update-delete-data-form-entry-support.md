---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD(建立、讀取、更新、刪除)資料表單輸入支援 |微軟文件
author: rick-anderson
description: 步驟 5 演示如何透過支援編輯、創建和刪除晚餐來進一步增加我們的 DinnersController 課程。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542621"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>提供 CRUD (建立、讀取、更新、刪除) 資料表單項目支援

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第5步,它介紹了如何使用 ASP.NETmVC1構建小型但完整的Web應用程式。
> 
> 步驟 5 演示如何透過支援編輯、創建和刪除晚餐來進一步增加我們的 DinnersController 課程。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>神經晚餐步驟 5:創建、更新、刪除表單方案

我們介紹了控制器和視圖,並介紹了如何使用它們在現場為 Dinner 實現清單/詳細信息體驗。 我們的下一步是進一步提高我們的 DinnersController 課程,並支援編輯、創建和刪除晚餐。

### <a name="urls-handled-by-dinnerscontroller"></a>由晚餐控制器處理的網址

我們之前向 DinnersController 添加了操作方法,這些方法對兩個 URL 進行了支援 *:/晚餐*和 */晚餐/詳細資訊/[id]。*

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */晚餐/* | GET | 顯示即將來臨的晚宴的 HTML 清單。 |
| */晚餐/詳情/[id]* | GET | 顯示有關特定晚餐的詳細資訊。 |

現在,我們將添加操作方法來實現三個附加*URL:/晚餐/編輯/[id]、/**晚餐/創建*和 */晚餐/刪除/[id]。* 這些 URL 將支援編輯現有晚餐、創建新晚餐和刪除晚餐。

我們將支援 HTTP GET 和 HTTP POST 謂詞與這些新 URL 的互動。 對這些 URL 的 HTTP GET 請求將顯示資料的初始 HTML 檢視(在"編輯"的情況下填充了 Dinner 資料的窗體,在"創建"的情況下填充了空白表單,在"刪除"的情況下顯示刪除確認螢幕)。 對這些 URL 的 HTTP POST 請求將儲存/更新/刪除我們的晚餐儲存庫中的晚餐數據(並從那裡保存到資料庫)。

| **URL** | **動詞** | **目的** |
| --- | --- | --- |
| */晚餐/編輯/[id]* | GET | 顯示填充晚餐資料的可編輯 HTML 表單。 |
| POST | 將特定 Dinner 的表單更改保存到資料庫。 |
| */晚餐/創建* | GET | 顯示一個空的 HTML 表單,允許使用者定義新的晚餐。 |
| POST | 創建新的晚餐並將其保存在資料庫中。 |
| */晚餐/刪除/[id]* | GET | 顯示刪除確認螢幕。 |
| POST | 從資料庫中刪除指定的晚餐。 |

### <a name="edit-support"></a>編輯支援

讓我們從實現"編輯"方案開始。

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET 編輯操作方法

我們將首先實現編輯操作方法的 HTTP"GET"行為。 當請求 */Dinners/Edit/[id]* URL 時,將調用此方法。 我們的實現將如下所示:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

上述代碼使用 Dinner 儲存庫檢索 Dinner 物件。 然後,它使用「晚餐」對象呈現視圖範本。 由於我們尚未將範本名稱顯式傳遞給*View()* 幫助器方法,它將使用基於約定的預設路徑來解決視圖範本:/視圖/Dinners/Edit.aspx。

現在,讓我們創建此視圖範本。 我們將在「編輯」方法中右鍵按一下並選擇「新增檢視」上下文選單命令來執行此操作:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件傳遞給檢視範本作為其模型,並選擇自動基腳模式「編輯」範本:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們添加新的「Edit.aspx」檢視範本檔。 它還將在代碼編輯器中打開新的「Edit.aspx」檢視範本, 填充了初始的「編輯」基架實現,如下所示:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

讓我們對產生的預設「編輯」基架進行一些更改,並更新編輯檢視範本以包含以下內容(這將刪除一些我們不想公開的屬性):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

當我們運行應用程式並請求 *「/晚餐/編輯/1」URL*時,我們將看到以下頁面:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

我們的檢視生成的 HTML 標記如下所示。 它是標準 HTML&lt;&gt;– 噹 按&lt;下"儲存" 輸入類型&gt;="提交" 按鈕時,具有對 */Dinners/Edit/1* URL 執行 HTTP POST 的表單元素。 已為每個&lt;可編輯屬性輸出&gt;HTML 輸入類型=「文字」/元素:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Html.BeginForm() 與 html.TextBox() html 說明器方法

我們的"Edit.aspx"檢視範本使用多個"Html 幫助程式"方法:Html.驗證摘要()、Html.BeginForm()、Html.TextBox()和 Html.驗證消息()。 除了為我們生成 HTML 標記外,這些幫助程式方法還提供內建的錯誤處理和驗證支援。

##### <a name="htmlbeginform-helper-method"></a>Html.BeginForm() 說明器方法

Html.BeginForm() 幫助器方法是在我們的標記中&lt;輸出&gt;HTML 表單元素的內容。 在我們的 Edit.aspx 檢視範本中,您會注意到,在使用此方法時,我們正在應用 C#"使用"語句。 開啟的大&lt;括弧表示表&gt;單 內容的開始,而關閉的大括&lt;弧表示&gt;/form 元素的結束:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

或者,如果您發現"使用"語句方法對於這樣的方案不自然,則可以使用 Html.BeginForm() 和 Html.EndForm() 組合 (執行相同的功能):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

呼叫 Html.BeginForm() 沒有任何參數將導致它輸出對目前請求的 URL 執行 HTTP-POST 的表單元素。 這就是為什麼我們的"編輯"視圖生成*&lt;表單操作\"/晚餐/編輯/1"方法="後&gt;"* 元素。 如果我們想要發佈到其他 URL,我們也可以將顯式參數傳遞給 Html.BeginForm()。

##### <a name="htmltextbox-helper-method"></a>Html.TextBox() 說明器方法

我們的 Edit.aspx 檢視使用 Html.TextBox() 協助器&lt;方法輸出&gt;輸入類型=「文字」/元素:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

上面的 Html.TextBox() 方法採用單個參數&lt;, 用於指定 要輸出的輸入類型的 id/name&gt;屬性= "text"/ 元素,以及用於填充文字框值的模型屬性。 例如,我們傳遞給"編輯"視圖的 Dinner 物件具有".NET 期貨"的"標題"屬性值,因此我們的 Html.TextBox("標題")方法調用輸出:*&lt;輸入 id="標題"名稱="標題"類型="文本&gt;"值=".NET 期貨"/。*

或者,我們可以使用第一個 Html.TextBox() 參數來指定元素的 ID/名稱,然後顯式傳遞值以用作第二個參數:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

通常,我們希望對輸出的值執行自定義格式設置。 內置於 .NET 的 String.Format() 靜態方法對於這些方案很有用。 我們的 Edit.aspx 檢視樣本正在使用此設定事件日期值(類型為 DateTime)的格式,以便它不顯示時間上的秒數:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

可以選擇使用 Html.TextBox() 的第三個參數來輸出其他 HTML 屬性。 下面的程式碼段演示如何&lt;在輸入類型="text"/&gt;元素上呈現額外的大小="30"屬性和類="mycssclass"屬性。 請注意,如何使用「類」@" character because "從類屬性的名稱中轉義是 C# 中的保留關鍵字:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>完整編取 HTTP-POST 編輯操作方法

現在,我們實現了"編輯"操作方法的 HTTP-GET 版本。 當使用者請求 */Dinners/Edit/1* URL 時,他們收到一個 HTML 頁面,如下所示:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

按下「保存」按鈕會導致表單發布到 */Dinners/Edit/1* URL,並使用 HTTP&lt;&gt;POST 謂 詞 提交 HTML 輸入表單值。 現在,讓我們實現編輯操作方法的 HTTP POST 行為 , 這將處理保存晚餐。

我們將首先向 DinnersController 添加一個重載的「編輯」操作方法,該控制器上具有「AcceptVerbs」屬性,指示它處理 HTTP POST 方案:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

當 [AcceptVerbs] 屬性應用於重載操作方法時,ASP.NET MVC 根據傳入的 HTTP 謂詞自動處理向相應操作方法發送請求。 HTTP POST 對 */Dinners/Edit/[id]* URL 的請求將轉到上述編輯方法,而所有其他 HTTP 謂詞請求 */Dinners/Edit/[id]* URL 將`[AcceptVerbs]`轉到我們實現的第一個編輯方法( 該方法沒有屬性)。

| **側主題:為什麼通過 HTTP 謂詞進行區分?** |
| --- |
| 您可能會問 – 為什麼我們使用單個 URL 並通過 HTTP 謂詞區分其行為? 為什麼不只有兩個單獨的 URL 來處理載入和儲存編輯更改? 例如:/Dinners/Edit/[id]以顯示初始窗體和/Dinners/保存/[id]來處理表單帖子以保存它? 發佈兩個單獨的 URL 的缺點是,如果我們發布到 /Dinners/Save/2,然後由於輸入錯誤而需要重新顯示 HTML 表單,最終使用者最終將在其瀏覽器的位址列中具有 /Dinners/Save/2 URL(因為這是表單發布到的 URL)。 如果最終使用者將此重新顯示的頁面標記為其瀏覽器收藏夾清單,或將 URL 複製/貼上並透過電子郵件發送給朋友,則他們最終將保存將來無法工作的 URL(因為該 URL 取決於帖子值)。 通過公開單個 URL(如:/Dinners/Edit/[id])並通過 HTTP 謂詞區分其處理,最終使用者可以安全地為編輯頁面添加書籤和/或將 URL 發送給其他人。 |

#### <a name="retrieving-form-post-values"></a>檢索表單過帳值

我們可以通過多種方式訪問 HTTP POST"編輯" 方法中的已發布的表單參數。 一個簡單的方法是只使用 Controller 基數上的 Request 屬性來存取表單的值:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

不過,上述方法有點冗長,尤其是在添加錯誤處理邏輯後。

此方案的更好方法是在控制器基類上利用內置*的 UpdateModel()* 説明器方法。 它支援更新使用傳入表單參數傳遞的物件的屬性。 它使用反射來確定物件上的屬性名稱,然後根據用戶端提交的輸入值自動轉換和分配值。

我們可以使用 UpdateModel() 方法使用此代碼簡化我們的 HTTP-POST 編輯操作:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

我們現在可以訪問 */Dinners/Edit/1* URL,並更改我們的晚餐標題:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

按下"保存"按鈕時,我們將執行"編輯"操作的表單帖子,更新的值將保留在資料庫中。 然後,我們將重定向到晚餐的詳細資訊 URL(將顯示新保存的值):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>處理編輯錯誤

我們當前的 HTTP-POST 實現工作正常,除非出現錯誤。

當使用者在編輯表單時出錯時,我們需要確保表單重新顯示一條資訊性錯誤消息,以指導他們修復表單。 這包括最終使用者發佈不正確的輸入(例如:格式不正確的日期字串)的情況,以及輸入格式有效但存在業務規則衝突的情況。 發生錯誤時,窗體應保留使用者最初輸入的輸入數據,以便不必手動重新填充其更改。 此過程應根據需要重複多次,直到表單成功完成。

ASP.NET MVC 包含一些不錯的內置功能,使錯誤處理和表單重新顯示變得簡單。 要查看這些功能,讓我們使用以下代碼更新我們的 Edit 操作方法:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

上述代碼與之前的實現類似,只是我們現在正在將 try/catch 錯誤處理塊包裝在工作周圍。 如果在調用 UpdateModel() 時或嘗試保存 DinnerRepository 時出現異常(如果我們試圖保存的 Dinner 物件由於模型中的規則衝突而無效,則將引發異常),則將執行 catch 錯誤處理塊。 在其中,我們迴圈對「晚餐」物件中存在的任何規則衝突,並將其添加到 ModelState 對象(我們稍後將討論)。 然後,我們重新顯示視圖。

要看到這個工作,讓我們重新運行應用程式,編輯晚餐,並更改它有一個空的標題,事件日期的"BOGUS",並使用一個英國電話號碼與國家國家值的美國。 當我們按下「保存」按鈕時,我們的 HTTP POST 編輯方法將無法保存晚餐(因為存在錯誤),並將重新顯示該窗體:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

我們的應用程式有一個體面的錯誤經驗。 具有無效輸入的文本元素以紅色突出顯示,驗證錯誤消息向最終用戶顯示。 該表單還保留使用者最初輸入的輸入數據,以便他們不必重新填充任何內容。

你可能會問,這是怎麼發生的? 標題、事件日期和 ContactPhone 文字框如何以紅色突出顯示自己,並知道要輸出最初輸入的用戶值? 錯誤訊息是如何顯示在頂部清單中的? 好消息是,這不是魔術造成的,而是因為我們使用了一些內置ASP.NET MVC 功能,使輸入驗證和錯誤處理方案變得容易。

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>瞭解模型狀態與驗證 HTML 說明器方法

控制器類具有"ModelState"屬性集合,它提供了一種指示模型物件傳遞給 View 存在錯誤的方法。 ModelState 集合中的錯誤條目標識具有問題的模型屬性的名稱(例如:"標題"、"事件日期"或"ContactPhone"),並允許指定人性化的錯誤消息(例如:"需要標題")。

*UpdateModel()* 幫助器方法在嘗試將窗體值分配給模型對象的屬性時遇到錯誤時自動填充模型狀態集合。 例如,我們的 Dinner 物件的 EventDate 屬性為「日期時間」類型。 當 UpdateModel() 方法無法在上述方案中為其分配字串值「BOGUS」時,UpdateModel() 方法向 ModelState 集合添加了一個條目,指示該屬性發生了賦值錯誤。

開發人員還可以編寫代碼,將錯誤條目顯式添加到 ModelState 集合中,就像我們在下面的"catch"錯誤處理塊中所做的一樣,該塊基於"晚餐"物件中的活動規則衝突填充了 ModelState 集合:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>HTML 說明器與模型狀態

HTML 說明器方法(如 Html.TextBox() ) - 在呈現輸出時選中 ModelState 集合。 如果項存在錯誤,則呈現使用者輸入的值和 CSS 錯誤類。

例如,在我們的「編輯」檢視中,我們使用 Html.TextBox() 説明器方法來呈現晚餐物件的事件日期:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

在錯誤方案中呈現檢視時,Html.TextBox() 方法檢查了 ModelState 集合,以查看是否存在與 Dinner 物件的「EventDate」屬性關聯的任何錯誤。 當它確定存在錯誤時,它呈現提交的使用者輸入(「BOGUS」)作為值,並將 css 錯誤類別&lt;新增到 它產生的輸入類型="textbox"/&gt;標記:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

您可以自定義 css 錯誤類的外觀,以按所需時間查看。 預設 CSS 錯誤類別 ( "輸入認證-錯誤' ) 在 *_content_site.css*樣式表中定義,如下所示:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

此 CSS 規則導致無效輸入元素突出顯示的原因如下:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>HTML.驗證訊息() 說明器方法

HTML.驗證訊息() 說明器方法可用於輸出與特定模型屬性關聯的 ModelState 錯誤訊息:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

上述代碼輸出:*&lt;跨類別=「欄位驗證錯誤&gt;」 值「BOGUS」無效&lt;/跨&gt;*

HTML.驗證訊息() 說明器方法支援第二個參數,該參數允許開發人員重寫顯示的錯誤文本訊息:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

上述代碼輸出:*&lt;跨類="欄位驗證-錯誤"/span,&gt;\*&lt;&gt;* 而不是當 EventDate 屬性存在錯誤時,而不是默認錯誤文本。

##### <a name="htmlvalidationsummary-helper-method"></a>HTML.驗證摘要() 說明器方法

HTML.驗證摘要() 說明程式方法可用於呈現摘要錯誤訊息,並附帶 ModelState&lt;&gt;&lt;集合中&gt;&lt;所有&gt;詳細錯誤訊息 的 ul li//ul 清單:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

HTML.驗證摘要() 說明程式方法採用可選字串參數 , 它定義摘要錯誤訊息,以顯示在詳細錯誤清單的上方:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

您可以選擇使用 CSS 來覆蓋錯誤列表的外觀。

#### <a name="using-a-addruleviolations-helper-method"></a>使用新增規則衝突說明程式方法

我們的初始 HTTP-POST 編輯實現使用 catch 塊中的 foreach 語句來迴圈訪問 Dinner 物件的「規則衝突」,並將它們添加到控制器的 ModelState 集合中:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

通過將「控制器幫助器」類添加到NerdDinner專案中,並在其中實現「AddRuleRule衝突」擴充方法,將説明器方法添加到ASP.NET MVC ModelState字典類,我們可以使此代碼更簡潔一些。 此擴充方法可以使用規則衝突錯誤清單封裝填充 ModelState字典所需的邏輯:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

然後,我們可以更新我們的 HTTP-POST 編輯操作方法,以使用此擴展方法使用我們的晚餐規則衝突填充 ModelState 集合。

#### <a name="complete-edit-action-method-implementations"></a>完整的編輯操作方法實現

以下代碼實現了編輯方案所需的控制器邏輯:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

我們的 Edit 實現好處是,我們的 Controller 類和 View 範本都不需要瞭解我們的 Dinner 模型正在強制執行的特定驗證或業務規則。 將來,我們可以向模型添加其他規則,並且不必對我們的控制器或視圖進行任何代碼更改,以便支援這些規則。 這為我們提供了靈活性,以便在未來以最少的代碼更改輕鬆發展我們的應用程式需求。

### <a name="create-support"></a>建立支援

我們已經完成了晚餐控制器類的"編輯"行為。 現在,讓我們繼續實現其上的"創建"支援-這將使用戶能夠添加新的晚餐。

#### <a name="the-http-get-create-action-method"></a>HTTP-GET 建立操作方法

我們將首先實現創建操作方法的 HTTP"GET"行為。 當有人訪問 */Dinners/創建*URL 時,將調用此方法。 我們的實現如下所示:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

上面的代碼將創建一個新的 Dinner 物件,並將其事件日期屬性分配為將來一周。 然後,它呈現基於新"晚餐"對象的視圖。 由於我們尚未顯式將名稱傳遞給*View()* 幫助器方法,它將使用基於約定的預設路徑來解決視圖範本:/視圖/Dinners/Create.aspx。

現在,讓我們創建此視圖範本。 我們可以在"創建操作"方法中右鍵按一下並選擇"添加檢視"上下文選單命令來執行此操作。 在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件傳遞到檢視範本,並選擇自動基腳手架「創建」範本:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

按下「添加」按鈕時,Visual Studio 會將基於腳手架的新「Create.aspx」視圖保存到「_Views_Dinners」目錄,並在 IDE 中將其打開:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

讓我們對為我們生成的預設「創建」基架檔進行一些更改,並將其修改為如下所示:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

現在,當我們運行應用程式並訪問瀏覽器中的 *「/Dinner/Create」URL*時,它將從我們的「創建操作」實現中呈現如下 UI:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>完整式 HTTP-POST 建立操作方法

我們實現了"創建操作方法"的 HTTP-GET 版本。 當使用者按下「儲存」按鈕時,它會執行表單發布到 */Dinners/Create* URL,並使用 HTTP&lt;POST 謂詞 提交&gt;HTML 輸入表單值。

現在,讓我們實現創建操作方法的 HTTP POST 行為。 我們將首先向 DinnersController 添加一個重載的「創建」操作方法,該控制器上具有「AcceptVerbs」屬性,指示它處理 HTTP POST 方案:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

我們可以通過多種方式訪問啟用 HTTP-POST 的"創建"方法中的已過帳表單參數。

一種方法是創建新的 Dinner 物件,然後使用*UpdateModel()* 説明器方法(就像我們使用"編輯"操作所做的那樣)使用張貼的表單值填充它。 然後,我們可以將其添加到 DinnerRepository 中,將其儲存到資料庫中,並將使用者重定向到「詳細資訊」操作,以便使用以下代碼顯示新創建的 Dinner:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

或者,我們可以使用一種方法,其中我們的 Create() 操作方法將 Dinner 物件作為方法參數。 然後ASP.NET MVC 將自動為我們實例化新的 Dinner 物件,使用表單輸入填充其屬性,並將其傳遞給我們的操作方法:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

上述操作方法通過檢查 ModelState.IsValid 屬性,驗證 Dinner 物件已成功填充表單後值。 如果存在輸入轉換問題(例如:EventDate 屬性的"BOGUS"字串),並且有任何問題,我們的操作方法將重新顯示窗體,則返回 false。

如果輸入值有效,則操作方法將嘗試將新 Dinner 添加到 DinnerRepository 中。 它將這項工作包裝在 try/catch 塊中,如果有任何違反業務規則的行為(這將導致晚餐存儲庫.Save() 方法引發異常,則重新顯示表單。

要查看此錯誤處理行為是否在起作用,我們可以請求 */Dinners/Create* URL 並填寫有關新晚餐的詳細資訊。 輸入或值不正確將導致重新顯示建立窗體,並突出顯示錯誤如下:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

請注意,我們的"創建"表單如何遵守與"編輯"表單完全相同的驗證和業務規則。 這是因為我們的驗證和業務規則是在模型中定義的,並且未嵌入到應用程式的 UI 或控制器中。 這意味著我們以後可以在一個位置更改/發展我們的驗證或業務規則,並在整個應用程式中應用這些規則。 我們不必更改"編輯"或"創建操作方法"中的任何代碼,即可自動遵守任何新規則或對現有規則的修改。

當我們修復輸入值並再次按下"保存"按鈕時,我們添加到 DinnerRepository 將成功,並且將添加新的 Dinner 添加到資料庫中。 然後,我們將重定向到 */Dinners/詳細資訊/[id]* URL - 我們將向這裡介紹有關新創建的晚餐的詳細資訊:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>移除支援

現在,讓我們向"刪除"支援添加到我們的晚餐控制器。

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET 移除操作方法

我們將首先實現刪除操作方法的 HTTP GET 行為。 當有人訪問 */Dinners/Delete/[id]* URL 時,將調用此方法。 以下是實現:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

操作方法嘗試檢索要刪除的"晚餐"。 如果「晚餐」存在,則根據「晚餐」對象呈現視圖。 如果物件不存在(或已被刪除),它將返回一個視圖,該視圖呈現了我們之前為"詳細資訊"操作方法創建的"NotFound"視圖範本。

我們可以在「刪除操作」方法中右鍵按一下並選擇「添加檢視」 上下文選單命令來創建「刪除」檢視範本。 在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件作為模型傳遞給視圖範本,並選擇創建空範本:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們添加新的」Delete.aspx「視圖範本檔。 我們將向樣本新增一些 HTML 和代碼,以實現如下刪除確認螢幕:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

上面的代碼顯示要刪除的 Dinner 的標題,並在最終使用者按下其中的&lt;「&gt;刪除」 按鈕時輸出對 /Dinners/Delete/[id] URL 執行 POST 的表單元素。

當我們運行應用程式並造訪有效 Dinner 物件的 *"/晚餐/刪除/[id]"URL*時,它將呈現如下 UI:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **側主題:我們為什麼要進行 POST?** |
| --- |
| 您可能會問 – 我們為什麼要在"刪除"確認&lt;螢幕&gt;中 創建 表單? 為什麼不只使用標準超連結連結到執行實際刪除操作的操作方法? 原因是,我們希望小心防範 Web 爬網者和搜尋引擎發現我們的 URL,並在跟蹤連結時無意中導致數據被刪除。 基於 HTTP-GET 的 URL 被視為「安全」的 URL,它們可以訪問/爬網,並且它們不應遵循 HTTP-POST URL。 一個好的規則是確保您始終將破壞性或數據修改操作放在 HTTP-POST 請求後面。 |

#### <a name="implementing-the-http-post-delete-action-method"></a>完整或 HTTP-POST 移除操作方法

現在,我們實現了 HTTP-GET 版本的刪除操作方法,顯示刪除確認螢幕。 當最終使用者按下「刪除」按鈕時,它將執行表單發布到 */Dinners/Dinner/[id]* URL。

現在,讓我們使用以下代碼實現刪除操作方法的 HTTP「POST」行為:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

HTTP-POST 版本的"刪除"操作方法嘗試檢索要刪除的晚餐物件。 如果找不到它(因為它已被刪除),它將呈現我們的"未找到"範本。 如果它找到晚餐,它會從晚餐存儲庫中刪除它。 然後,它呈現一個"已刪除"範本。

要實現"已刪除"範本,我們將在操作方法中右鍵單擊並選擇"添加視圖"上下文菜單。 我們將檢視命名為"已刪除",並將其命名為空範本(而不是採用強類型模型物件)。 然後,我們將向其中添加一些 HTML 內容:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

現在,當我們運行我們的應用程式,並訪問有效的晚餐物件的 *"/晚餐/刪除/[id]"URL*時,它將呈現我們的晚餐刪除確認螢幕,如下所示:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

當我們按下「刪除」按鈕時,它將對 */Dinners/Delete/[id]* URL 執行 HTTP-POST,這將從我們的資料庫中刪除晚餐,並顯示我們的「已刪除」視圖範本:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>模型繫結安全性

我們討論了使用ASP.NET MVC 的內建模型綁定功能的兩種不同的方法。 第一個使用 UpdateModel() 方法更新現有模型物件的屬性,第二個使用 ASP.NET mVC 支援將模型物件作為操作方法參數傳遞。 這兩種技術都非常強大,非常有用。

這種力量也帶來了責任。 在接受任何用戶輸入時,始終對安全性持偏執狀態很重要,在綁定物件以形成輸入時也是如此。 您應該始終小心 HTML 編碼任何使用者輸入的值,以避免 HTML 和 JavaScript 注入攻擊,並小心 SQL 注入攻擊(請注意:我們使用 LINQ 到 SQL 作為應用程式,它會自動對參數進行編碼,以防止這些類型的攻擊)。 您絕不應僅依賴客戶端驗證,並且始終使用伺服器端驗證來防止駭客試圖向您發送虛假值。

使用 ASP.NET MVC 的綁定功能時,要確保考慮的另一個安全項是綁定物件的範圍。 具體來說,您希望確保您瞭解允許綁定的屬性的安全含義,並確保僅允許最終使用者更新真正應該更新的屬性。

默認情況下,UpdateModel() 方法將嘗試更新模型物件上與傳入窗體參數值匹配的所有屬性。 同樣,默認情況下作為操作方法參數傳遞的物件可以通過窗體參數設置其所有屬性。

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>依使用方式鎖定繫結

通過提供可更新的屬性的顯式"包含清單",可以按使用方式鎖定綁定策略。 這可以通過將額外的字串陣列參數傳遞給 UpdateModel() 方法來實現,如下所示:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

作為操作方法參數傳遞的物件還支援 [Bind] 屬性,該屬性允許如下指定允許屬性的「包含清單」:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>在類型上鎖定繫結

您還可以按類型鎖定綁定規則。 這允許您指定綁定規則一次,然後將它們應用於所有控制器和操作方法的所有方案(包括 UpdateModel 和操作方法參數方案)。

您可以通過將 [Bind] 屬性添加到類型上,或透過在應用程式的 Global.asax 檔中註冊來自定義每種類型的綁定規則(對於您不擁有該類型的方案非常有用)。 然後,可以使用 Bind 屬性的「包含」和「排除」屬性來控制特定類或介面可綁定哪些屬性。

我們將在NerdDinner應用程式中對Dinner類使用此技術,並為其添加 [Bind] 屬性,將可綁定屬性清單限制為以下內容:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

請注意,我們不允許通過綁定操作 RSSP 集合,也不允許通過綁定設置 DinnerID 或託管比屬性。 出於安全原因,我們將只使用操作方法中的顯式代碼來操作這些特定屬性。

### <a name="crud-wrap-up"></a>CRUD 總結

ASP.NET MVC 包含許多內置功能,可幫助實現表單發布方案。 我們使用多種功能在晚餐存儲庫上提供 CRUD UI 支援。

我們使用以模型為中心的方法來實現我們的應用程式。 這意味著我們所有的驗證和業務規則邏輯都在我們的模型層中定義,而不是在我們的控制器或視圖中定義。 我們的 Controller 類和 View 範本都不知道我們的 Dinner 模型類正在強制執行的特定業務規則。

這將保持我們的應用程序體系結構清潔,並使其更易於測試。 將來,我們可以向模型層添加其他業務規則,而不必對我們的控制器或視圖*進行任何代碼更改*,以便支援這些規則。 這將為我們提供極大的敏捷性,以便我們在未來發展和改變我們的應用程式。

我們的晚餐控制器現在啟用晚餐列表/詳細資訊,以及創建、編輯和刪除支援。 類別的完整代碼如下所示:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>後續步驟

現在,我們的 DinnersController 類中實現了基本的 CRUD(創建、讀取、更新和刪除)支援。

現在,讓我們來看看如何使用 ViewData 和 ViewModel 類在我們的窗體上啟用更豐富的 UI。

> [!div class="step-by-step"]
> [前一個](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一個](use-viewdata-and-implement-viewmodel-classes.md)
