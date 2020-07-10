---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/examining-the-edit-methods-and-edit-view
title: 檢查編輯方法和編輯檢視 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 .。。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 5cb3c59b-1e96-464b-b3a8-c55607201872
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: db9f6bc9edfba7d4ece575aad4c9cdc029abb7f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "86163151"
---
# <a name="examining-the-edit-methods-and-edit-view-vb"></a>檢查編輯方法與編輯檢視 (VB)

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。 開始之前，請先確定您已安裝下列必要條件。 您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以使用下列連結個別安裝必要條件：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0) (執行時間 + 工具支援) 
> 
> 如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。 [下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您偏好使用 c #，請切換到本教學課程的[c # 版本](../cs/examining-the-edit-methods-and-edit-view.md)。

在本節中，您將檢查針對電影控制器產生的動作方法和 views。 接著，您將新增自訂搜尋頁面。

執行應用程式並流覽至 `Movies` 控制器，方法是將 */Movies*附加至瀏覽器網址列中的 URL。 將滑鼠指標放在**編輯**連結上方，以查看其所連結的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

[**編輯**] 連結是由 `Html.ActionLink` *Views\Movies\Index.vbhtml*視圖中的方法所產生：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

[![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image3.png)](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`物件是在基類上使用屬性公開的 helper `WebViewPage` 。 `ActionLink`Helper 的方法可讓您輕鬆地動態產生連結至控制器上動作方法的 HTML 超連結。 方法的第一個引數 `ActionLink` 是要呈現的連結文字 (例如， `<a>Edit Me</a>`) 。 第二個引數是要叫用之動作方法的名稱。 最後一個引數是[匿名物件](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，它會在此案例中產生路由資料 (，這是 4) 的識別碼。

上圖所示的產生連結是 `http://localhost:xxxxx/Movies/Edit/4` 。 預設路由會採用 URL 模式 `{controller}/{action}/{id}` 。 因此，ASP.NET 會將參數轉譯為 `http://localhost:xxxxx/Movies/Edit/4` 控制站的 `Edit` 動作方法，並將 `Movies` 參數 `ID` 等於4。

您也可以使用查詢字串來傳遞動作方法參數。 例如，URL 也會將 `http://localhost:xxxxx/Movies/Edit?ID=4` 參數4傳遞 `ID` 至 `Edit` 控制器的動作方法 `Movies` 。

[![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image5.png)](examining-the-edit-methods-and-edit-view/_static/image4.png)

開啟 `Movies` 控制器。 這兩個 `Edit` 動作方法如下所示。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample3.vb)]

請注意，第二個 `Edit` 動作方法的前面是 `HttpPost` 屬性。 這個屬性指定方法的多載只能 `Edit` 針對 POST 要求叫用。 您可以將 `HttpGet` 屬性套用至第一個 edit 方法，但這不是必要的，因為它是預設值。  (我們會參考隱含指派 `HttpGet` 屬性做為方法的動作方法 `HttpGet` 。 ) 

`HttpGet` `Edit` 方法會採用 movie ID 參數、使用 Entity Framework 方法來查詢電影， `Find` 並將選取的影片傳回編輯檢視。 當 Scaffolding 系統建立 Edit 檢視時，它會檢查 `Movie` 類別，並建立程式碼為類別的每個屬性轉譯 `<label>` 和 `<input>` 元素。 下列範例顯示已產生的編輯檢視：

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.vbhtml)]

請注意，view 範本在檔案 `@ModelType MvcMovie.Models.Movie` 頂端有一個語句，這表示此視圖需要視圖範本的模型為類型 `Movie` 。

Scaffold 程式碼會使用數個*helper 方法*來簡化 HTML 標籤。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Helper 會顯示欄位的名稱 &quot; ， (標題 &quot; 、ReleaseDate、內容類型 &quot; &quot; &quot; &quot; 或 &quot; 價格 &quot;) 。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Helper 會顯示 HTML `<input>` 元素。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Helper 會顯示與該屬性相關聯的任何驗證訊息。

執行應用程式，並流覽至 */Movies* URL。 按一下 [**編輯**] 連結。 在瀏覽器中，檢視頁面的原始檔。 頁面中的 HTML 如下列範例所示。  (已排除功能表標記以求清楚。 ) 

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html)]

`<input>`元素位於 HTML 元素中， `<form>` 其 `action` 屬性設定為張貼至 */Movies/Edit* URL。 當您按一下 [**編輯**] 按鈕時，表單會將資料張貼至伺服器。

## <a name="processing-the-post-request"></a>處理 POST 要求

下列清單顯示 `HttpPost` 版本的 `Edit` 動作方法。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample6.vb)]

ASP.NET framework 模型系結器會採用已張貼的表單值，並建立當做 `Movie` 參數傳遞的物件 `movie` 。 `ModelState.IsValid`程式碼中的檢查會確認表單中提交的資料可用於修改 `Movie` 物件。 如果資料有效，則程式碼會將電影資料儲存至 `Movies` 實例的集合 `MovieDBContext` 。 然後，程式碼會藉由呼叫的方法，將新的電影資料儲存至資料庫，以保存 `SaveChanges` `MovieDBContext` 資料庫的變更。 儲存資料之後，程式碼會將使用者重新導向至 `Index` 類別的動作方法 `MoviesController` ，這會使更新後的電影顯示在電影清單中。

如果張貼的值無效，則會在表單中重新顯示。 `Html.ValidationMessageFor`[*編輯 vbhtml* ] 視圖範本中的協助程式會負責顯示適當的錯誤訊息。

[![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image7.png)](examining-the-edit-methods-and-edit-view/_static/image6.png)

> **地區設定的相關注意事項**如果您通常使用英文以外的地區設定，請參閱[支援使用非英文地區設定的 ASP.NET MVC 3 驗證。](https://msdn.microsoft.com/library/gg674880(VS.98).aspx)

## <a name="making-the-edit-method-more-robust"></a>讓編輯方法更健全

`HttpGet` `Edit` 由樣板系統產生的方法不會檢查傳遞給它的識別碼是否有效。 如果使用者從 URL 移除識別碼區段 (`http://localhost:xxxxx/Movies/Edit`) ，則會顯示下列錯誤：

[![Null_ID](examining-the-edit-methods-and-edit-view/_static/image9.png)](examining-the-edit-methods-and-edit-view/_static/image8.png)

使用者也可以傳遞不存在於資料庫中的識別碼，例如 `http://localhost:xxxxx/Movies/Edit/1234` 。 您可以對動作方法進行兩項變更 `HttpGet` `Edit` ，以解決這項限制。 首先， `ID` 在未明確傳遞識別碼時，將參數變更為預設值為零。 您也可以 `Find` 先檢查方法是否確實找到電影，再將 movie 物件傳回給 view 範本。 更新的 `Edit` 方法如下所示。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample7.vb)]

如果找不到電影，則 `HttpNotFound` 會呼叫方法。

所有 `HttpGet` 方法都遵循類似的模式。 它們會取得電影物件 (或物件清單（在) 的情況下）， `Index` 並將模型傳遞給視圖。 方法會將 `Create` 空的 movie 物件傳遞至 Create view。 建立、編輯、刪除或以其他方式修改資料的所有方法都會在方法的 `HttpPost` 多載中執行這個動作。 修改 HTTP GET 方法中的資料會有安全性風險，如 blog 文章[ASP.NET MVC Tip #46 –請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的資料也會違反 HTTP 最佳做法和架構 REST 模式，這會指定 GET 要求不應該變更應用程式的狀態。 換句話說，執行 GET 作業應該是不具副作用的安全作業。

## <a name="adding-a-search-method-and-search-view"></a>加入搜尋方法和搜尋視圖

在本節中，您將新增 `SearchIndex` 動作方法，讓您依據內容類型或名稱來搜尋電影。 這將可使用 */Movies/SearchIndex* URL 取得。 要求會顯示 HTML 表單，其中包含使用者可以填入的輸入專案，以便搜尋電影。 當使用者提交表單時，動作方法會取得使用者所張貼的搜尋值，並使用這些值來搜尋資料庫。

![SearchIndx_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

## <a name="displaying-the-searchindex-form"></a>顯示 SearchIndex 表單

首先，將 `SearchIndex` 動作方法加入至現有的 `MoviesController` 類別。 方法會傳回包含 HTML 表單的視圖。 此程式碼如下：

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample8.vb)]

方法的第一行會 `SearchIndex` 建立下列[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查詢來選取電影：

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample9.vb)]

此查詢定義于此時，但尚未針對資料存放區執行。

如果 `searchString` 參數包含字串，則會使用下列程式碼修改電影查詢來篩選搜尋字串的值：

如果不是字串. IsNullOrEmpty (searchString) 然後   
 電影 = 電影。其中 (函式 (s) . Title. 包含 (searchString) # A5   
 End If

定義 LINQ 查詢時，或呼叫方法（例如或）時，不會執行它們 `Where` `OrderBy` 。 相反地，查詢執行會延後，這表示運算式的評估會延遲，直到其實現的值實際反復執行，或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 呼叫方法為止。 在此 `SearchIndex` 範例中，會在 SearchIndex 視圖中執行查詢。 如需延後查詢執行的詳細資訊，請參閱[查詢執行](https://msdn.microsoft.com/library/bb738633.aspx)。

現在您可以執行 `SearchIndex` 會向使用者顯示表單的視圖。 在方法內按一下滑鼠右鍵 `SearchIndex` ，然後按一下 [**加入視圖**]。 在 [**加入視圖**] 對話方塊中，指定您要將 `Movie` 物件當做模型類別傳遞至視圖範本。 在 [ **Scaffold 範本**] 清單中，選擇 [**清單**]，然後按一下 [**新增**]。

[![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image12.png)](examining-the-edit-methods-and-edit-view/_static/image11.png)

當您按一下 [**新增**] 按鈕時，就會建立*Views\Movies\SearchIndex.vbhtml* view 範本。 由於您已在**Scaffold 範本**清單中選取 [**清單**]，因此 Visual Web Developer 會自動產生 (scaffold) 視圖中的一些預設內容。 此樣板建立了 HTML 表單。 它會檢查 `Movie` 類別並建立程式碼，以 `<label>` 針對類別的每個屬性轉譯元素。 下列清單顯示已產生的 Create view：

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.vbhtml)]

執行應用程式，並流覽至 */Movies/SearchIndex*。 將查詢字串 (例如 `?searchString=ghost`) 附加至 URL。 隨即顯示篩選過的電影。

[![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image14.png)](examining-the-edit-methods-and-edit-view/_static/image13.png)

如果您將方法的簽章變更 `SearchIndex` 為具有名為的參數 `id` ，則 `id` 參數會符合 global.asax 檔案 `{id}` 中設定之預設路由的*Global.asax*預留位置。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample11.json)]

修改過的 `SearchIndex` 方法看起來會像這樣：

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample12.vb)]

您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。

[![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image16.png)](examining-the-edit-methods-and-edit-view/_static/image15.png)

但是，您不能期望使用者在每次想要搜尋電影時修改 URL。 現在您要新增 UI，以協助他們篩選電影。 如果您變更方法的簽章 `SearchIndex` 來測試如何傳遞路由系結識別碼參數，請將其變更為，讓您的 `SearchIndex` 方法接受名為的字串參數 `searchString` ：

開啟*Views\Movies\SearchIndex.vbhtml*檔案，然後在之後 `@Html.ActionLink("Create New", "Create")` ，新增下列內容：

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample13.vbhtml)]

`Html.BeginForm`Helper 會建立一個開頭 `<form>` 標記。 `Html.BeginForm`當使用者按一下 [**篩選**] 按鈕來提交表單時，helper 會使表單張貼至其本身。

執行應用程式，然後嘗試搜尋電影。

[![SearchIndxIE9_title](examining-the-edit-methods-and-edit-view/_static/image18.png)](examining-the-edit-methods-and-edit-view/_static/image17.png)

方法沒有任何多載 `HttpPost` `SearchIndex` 。 您不需要它，因為方法不會變更應用程式的狀態，而只會篩選資料。 如果您已新增下列 `HttpPost` `SearchIndex` 方法，動作啟動者會符合 `HttpPost` `SearchIndex` 方法，而 `HttpPost` `SearchIndex` 方法會如下圖所示執行。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample14.vb)]

[![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image20.png)](examining-the-edit-methods-and-edit-view/_static/image19.png)

## <a name="adding-search-by-genre"></a>依內容類型加入搜尋

如果您已新增 `HttpPost` 方法的版本 `SearchIndex` ，請立即將其刪除。

接下來，您將新增一項功能，讓使用者依內容類型搜尋電影。 以下列程式碼取代 `SearchIndex` 方法：

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample15.vb)]

這個版本的 `SearchIndex` 方法會採用額外的參數，亦即 `movieGenre` 。 前幾行程式碼會建立 `List` 物件，以保存資料庫中的電影內容內容。

下列程式碼是一種 LINQ 查詢，其會從資料庫中擷取所有的內容類型。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample16.vb)]

程式碼會使用 `AddRange` 泛型集合的方法 `List` ，將所有不同的內容組加入清單中。  (不含 `Distinct` 修飾詞，則會新增重複的內容，例如，喜劇會在我們的範例) 中新增兩次。 然後，程式碼會將內容清單儲存在 `ViewBag` 物件中。

下列程式碼顯示如何檢查 `movieGenre` 參數。 如果不是空的，則程式碼會進一步限制電影查詢，將選取的電影限制為指定的類型。

[!code-vb[Main](examining-the-edit-methods-and-edit-view/samples/sample17.vb)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>將標記加入至 SearchIndex 視圖，以支援依內容類型搜尋

將 `Html.DropDownList` helper 新增至*Views\Movies\SearchIndex.vbhtml*檔案，在協助程式之前 `TextBox` 。 完成的標記如下所示：

[!code-vbhtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.vbhtml)]

執行應用程式，並流覽至 */Movies/SearchIndex*。 依內容類型、電影名稱和這兩個準則來嘗試搜尋。

在本節中，您會檢查架構所產生的 CRUD 動作方法和 views。 您建立了搜尋動作方法和 view，讓使用者依電影標題和內容類型進行搜尋。 在下一節中，您將瞭解如何將屬性加入至 `Movie` 模型，以及如何加入會自動建立測試資料庫的初始化運算式。

> [!div class="step-by-step"]
> [上一個](accessing-your-models-data-from-a-controller.md) 
> [下一步](adding-a-new-field.md)
