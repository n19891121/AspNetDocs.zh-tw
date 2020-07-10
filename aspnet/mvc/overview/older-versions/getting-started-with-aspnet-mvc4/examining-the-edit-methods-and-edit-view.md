---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: 檢查編輯方法和編輯檢視 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 .。。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 85ad9a5758d70b5fe4ed792efb80217d7b3e2132
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162958"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>檢查編輯方法與編輯檢視

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > 本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、更容易遵循，並示範更多功能。

在本節中，您將檢查針對電影控制器產生的動作方法和 views。 接著，您將新增自訂搜尋頁面。

執行應用程式並流覽至 `Movies` 控制器，方法是將 */Movies*附加至瀏覽器網址列中的 URL。 將滑鼠指標放在**編輯**連結上方，以查看其所連結的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

[**編輯**] 連結是由 `Html.ActionLink` *Views\Movies\Index.cshtml*視圖中的方法所產生：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![.Html](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`物件是使用[WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基類上的屬性所公開的協助程式。 `ActionLink`Helper 的方法可讓您輕鬆地動態產生連結至控制器上動作方法的 HTML 超連結。 方法的第一個引數 `ActionLink` 是要呈現的連結文字 (例如， `<a>Edit Me</a>`) 。 第二個引數是要叫用之動作方法的名稱。 最後一個引數是[匿名物件](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，它會在此案例中產生路由資料 (，這是 4) 的識別碼。

上圖所示的產生連結是 `http://localhost:xxxxx/Movies/Edit/4` 。  (在*應用程式 \_ Start\RouteConfig.cs*中建立的預設路由) 採用 URL 模式 `{controller}/{action}/{id}` 。 因此，ASP.NET 會將參數轉譯為 `http://localhost:xxxxx/Movies/Edit/4` 控制站的 `Edit` 動作方法，並將 `Movies` 參數 `ID` 等於4。 檢查*應用程式 \_ Start\RouteConfig.cs*檔中的下列程式碼。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

您也可以使用查詢字串來傳遞動作方法參數。 例如，URL 也會將 `http://localhost:xxxxx/Movies/Edit?ID=4` 參數4傳遞 `ID` 至 `Edit` 控制器的動作方法 `Movies` 。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

開啟 `Movies` 控制器。 這兩個 `Edit` 動作方法如下所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

請注意，第二個 `Edit` 動作方法的前面是 `HttpPost` 屬性。 這個屬性指定方法的多載只能 `Edit` 針對 POST 要求叫用。 您可以將 `HttpGet` 屬性套用至第一個 edit 方法，但這不是必要的，因為它是預設值。  (我們會參考隱含指派 `HttpGet` 屬性做為方法的動作方法 `HttpGet` 。 ) 

`HttpGet` `Edit` 方法會採用 movie ID 參數、使用 Entity Framework 方法來查詢電影， `Find` 並將選取的影片傳回編輯檢視。 如果在沒有參數的情況下呼叫方法，ID 參數會指定[預設值](https://msdn.microsoft.com/library/dd264739.aspx)為零 `Edit` 。 如果找不到電影，則會傳回[HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 。 當 Scaffolding 系統建立 Edit 檢視時，它會檢查 `Movie` 類別，並建立程式碼為類別的每個屬性轉譯 `<label>` 和 `<input>` 元素。 下列範例顯示已產生的編輯檢視：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

請注意，view 範本在檔案 `@model MvcMovie.Models.Movie` 頂端有一個語句，這表示此視圖需要視圖範本的模型為類型 `Movie` 。

Scaffold 程式碼會使用數個*helper 方法*來簡化 HTML 標籤。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)Helper 會顯示欄位的名稱 &quot; ， (標題 &quot; 、ReleaseDate、內容類型 &quot; &quot; &quot; &quot; 或 &quot; 價格 &quot;) 。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)Helper 會呈現 HTML 專案 `<input>` 。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)Helper 會顯示與該屬性相關聯的任何驗證訊息。

執行應用程式，並流覽至 */Movies* URL。 按一下 [**編輯**] 連結。 在瀏覽器中，檢視頁面的原始檔。 Form 元素的 HTML 如下所示。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`元素位於 HTML 元素中， `<form>` 其 `action` 屬性設定為張貼至 */Movies/Edit* URL。 當您按一下 [**編輯**] 按鈕時，表單會將資料張貼至伺服器。

## <a name="processing-the-post-request"></a>處理 POST 要求

下列清單顯示 `HttpPost` 版本的 `Edit` 動作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 模型](https://msdn.microsoft.com/magazine/hh781022.aspx)系結器會採用已張貼的表單值，並建立當做 `Movie` 參數傳遞的物件 `movie` 。 `ModelState.IsValid` 方法會驗證表單中提交的資料可用於修改 (編輯或更新) `Movie` 物件。 如果資料有效，則會將電影資料儲存至 `Movies` `db(MovieDBContext` 實例) 的集合。 新的電影資料會藉由呼叫的方法，儲存至資料庫 `SaveChanges` `MovieDBContext` 。 儲存資料之後，程式碼會將使用者重新導向至 `Index` 類別的動作方法 `MoviesController` ，這會顯示電影集合的，包括剛進行的變更。

如果張貼的值無效，則會在表單中重新顯示。 `Html.ValidationMessageFor`*編輯 cshtml*視圖範本中的協助程式會負責顯示適當的錯誤訊息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 若要針對使用逗點 (的非英文地區設定支援 jQuery 驗證 &quot; ， &quot;) 為小數點，您必須包含*globalize.js*和您的特定*文化特性/globalize.cultures.js*檔案 (從 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 和 JavaScript 使用 `Globalize.parseFloat` 。 下列程式碼顯示對 Views\Movies\Edit.cshtml 檔案所做的修改，以使用 &quot; fr-fr 文化特性 &quot; ：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Decimal 欄位可能需要逗號，而不是小數點。 做為暫時的修正程式，您可以將全球化元素新增至專案根 web.config 檔案。 下列程式碼顯示將文化特性設定為美國英文的全球化元素。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

所有 `HttpGet` 方法都遵循類似的模式。 它們會取得電影物件 (或物件清單（在) 的情況下）， `Index` 並將模型傳遞給視圖。 方法會將 `Create` 空的 movie 物件傳遞至 Create view。 建立、編輯、刪除或以其他方式修改資料的所有方法都會在方法的 `HttpPost` 多載中執行這個動作。 修改 HTTP GET 方法中的資料會有安全性風險，如 blog 文章[ASP.NET MVC Tip #46 –請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的資料也會違反 HTTP 最佳做法和架構[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式，這會指定 GET 要求不應該變更應用程式的狀態。 也就是說，執行 GET 作業應該是安全的作業，沒有任何副作用，而且不會修改您的保存資料。

## <a name="adding-a-search-method-and-search-view"></a>加入搜尋方法和搜尋視圖

在本節中，您將新增 `SearchIndex` 動作方法，讓您依據內容類型或名稱來搜尋電影。 這將可使用 */Movies/SearchIndex* URL 取得。 要求會顯示 HTML 表單，其中包含使用者可以輸入以搜尋電影的輸入元素。 當使用者提交表單時，動作方法會取得使用者所張貼的搜尋值，並使用這些值來搜尋資料庫。

## <a name="displaying-the-searchindex-form"></a>顯示 SearchIndex 表單

首先，將 `SearchIndex` 動作方法加入至現有的 `MoviesController` 類別。 方法會傳回包含 HTML 表單的視圖。 此程式碼如下：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

方法的第一行會 `SearchIndex` 建立下列[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查詢來選取電影：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

此查詢定義于此時，但尚未針對資料存放區執行。

如果 `searchString` 參數包含字串，則會使用下列程式碼修改電影查詢來篩選搜尋字串的值：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

上述 `s => s.Title` 程式碼是 [Lambda 運算式](https://msdn.microsoft.com/library/bb397687.aspx)。 Lambda 用於以方法為基礎的[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查詢，做為標準查詢運算子方法的引數，例如上述程式碼中所使用的[Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)方法。 定義 LINQ 查詢時，或呼叫方法（例如或）時，不會執行它們 `Where` `OrderBy` 。 相反地，查詢執行會延後，這表示運算式的評估會延遲，直到其實現的值實際反復執行，或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 呼叫方法為止。 在此 `SearchIndex` 範例中，會在 SearchIndex 視圖中執行查詢。 如需延後查詢執行的詳細資訊，請參閱[查詢執行](https://msdn.microsoft.com/library/bb738633.aspx)。

現在您可以執行 `SearchIndex` 會向使用者顯示表單的視圖。 在方法內按一下滑鼠右鍵 `SearchIndex` ，然後按一下 [**加入視圖**]。 在 [**加入視圖**] 對話方塊中，指定您要將 `Movie` 物件當做模型類別傳遞至視圖範本。 在 [ **Scaffold 範本**] 清單中，選擇 [**清單**]，然後按一下 [**新增**]。

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

當您按一下 [**新增**] 按鈕時，就會建立*Views\Movies\SearchIndex.cshtml* view 範本。 由於您已在**Scaffold 範本**清單中選取 [**清單**]，Visual Studio 自動產生 (scaffold) 視圖中的某些預設標記。 此樣板建立了 HTML 表單。 它會檢查 `Movie` 類別並建立程式碼，以 `<label>` 針對類別的每個屬性轉譯元素。 下列清單顯示已產生的 Create view：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

執行應用程式，並流覽至 */Movies/SearchIndex*。 將查詢字串 (例如 `?searchString=ghost`) 附加至 URL。 隨即顯示篩選過的電影。

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

如果您將方法的簽章變更 `SearchIndex` 為具有名為的參數 `id` ，則 `id` 參數會符合 global.asax 檔案 `{id}` 中設定之預設路由的*Global.asax*預留位置。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

原始方法如下所 `SearchIndex` 示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

修改過的 `SearchIndex` 方法看起來會像這樣：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

但是，您不能期望使用者在每次想要搜尋電影時修改 URL。 現在您要新增 UI，以協助他們篩選電影。 如果您變更方法的簽章 `SearchIndex` 來測試如何傳遞路由系結識別碼參數，請將其變更為，讓您的 `SearchIndex` 方法接受名為的字串參數 `searchString` ：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

開啟*Views\Movies\SearchIndex.cshtml*檔案，然後在之後 `@Html.ActionLink("Create New", "Create")` ，新增下列內容：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

下列範例會顯示*Views\Movies\SearchIndex.cshtml*檔案的一部分，其中包含新增的篩選標記。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`Helper 會建立一個開頭 `<form>` 標記。 `Html.BeginForm`當使用者按一下 [**篩選**] 按鈕來提交表單時，helper 會使表單張貼至其本身。

執行應用程式，然後嘗試搜尋電影。

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

方法沒有任何多載 `HttpPost` `SearchIndex` 。 您不需要它，因為方法不會變更應用程式的狀態，而只會篩選資料。

您可以新增下列 `HttpPost SearchIndex` 方法。 在此情況下，動作啟動程式會符合 `HttpPost SearchIndex` 方法，而 `HttpPost SearchIndex` 方法會如下圖所示執行。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

不過，即使您新增這個 `HttpPost` 版本的 `SearchIndex` 方法，在如何全部實作此方法方面仍然有其限制。 假設您想要將特定的搜尋加為書籤，或者想要傳送連結給朋友，讓他們可以點選來查看相同的電影篩選清單。 請注意，HTTP POST 要求的 URL 與 GET 要求的 url 相同 (localhost： xxxxx/電影/SearchIndex) --URL 本身沒有搜尋資訊。 目前，搜尋字串資訊會以表單欄位值的形式傳送至伺服器。 這表示您無法在 URL 中以書簽或傳送給朋友，來捕捉該搜尋資訊。

解決方案是使用的多載 `BeginForm` ，指定 POST 要求應將搜尋資訊新增至 URL，而且應該將其路由傳送至方法的 HttpGet 版本 `SearchIndex` 。 以下列內容取代現有的無參數 `BeginForm` 方法：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

現在當您提交搜尋時，URL 會包含搜尋查詢字串。 即使您有 `HttpPost SearchIndex` 方法，搜尋也會移至 `HttpGet SearchIndex` 動作方法。

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>依內容類型加入搜尋

如果您已新增 `HttpPost` 方法的版本 `SearchIndex` ，請立即將其刪除。

接下來，您將新增一項功能，讓使用者依內容類型搜尋電影。 以下列程式碼取代 `SearchIndex` 方法：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

這個版本的 `SearchIndex` 方法會採用額外的參數，亦即 `movieGenre` 。 前幾行程式碼會建立 `List` 物件，以保存資料庫中的電影內容內容。

下列程式碼是一種 LINQ 查詢，其會從資料庫中擷取所有的內容類型。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

程式碼會使用 `AddRange` 泛型集合的方法 `List` ，將所有不同的內容組加入清單中。  (不含 `Distinct` 修飾詞，則會新增重複的內容，例如，喜劇會在我們的範例) 中新增兩次。 然後，程式碼會將內容清單儲存在 `ViewBag` 物件中。

下列程式碼顯示如何檢查 `movieGenre` 參數。 如果不是空的，則程式碼會進一步限制電影查詢，將選取的電影限制為指定的類型。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>將標記加入至 SearchIndex 視圖，以支援依內容類型搜尋

將 `Html.DropDownList` helper 新增至*Views\Movies\SearchIndex.cshtml*檔案，在協助程式之前 `TextBox` 。 完成的標記如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

執行應用程式，並流覽至 */Movies/SearchIndex*。 依內容類型、電影名稱和這兩個準則來嘗試搜尋。

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

在本節中，您會檢查架構所產生的 CRUD 動作方法和 views。 您建立了搜尋動作方法和 view，讓使用者依電影標題和內容類型進行搜尋。 在下一節中，您將瞭解如何將屬性加入至 `Movie` 模型，以及如何加入會自動建立測試資料庫的初始化運算式。

> [!div class="step-by-step"]
> [上一個](accessing-your-models-data-from-a-controller.md) 
> [下一步](adding-a-new-field-to-the-movie-model-and-table.md)
