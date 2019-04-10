---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
title: 檢查編輯方法與編輯檢視 |Microsoft Docs
author: Rick-Anderson
description: 注意:本教學課程中的更新的版本可在此使用 ASP.NET MVC 5 和 Visual Studio 2013。 這是更安全、 更容易遵循，並示範...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 41eb99ca-e88f-4720-ae6d-49a958da8116
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: d22b6a02a211e61707e9660c64b87a8c08388e58
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59392088"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>檢查編輯方法與編輯檢視

藉由[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 本教學課程中的更新的版本可[此處](../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、 更容易遵循，並示範更多的功能。


在本節中，您將會檢查產生的動作方法和檢視電影控制器。 然後，您將新增自訂搜尋頁面。

執行應用程式，並瀏覽至`Movies`藉由附加的控制站 */Movies*至您的瀏覽器的網址列中的 URL。 將滑鼠指標停留**編輯**連結，以查看它所連結的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**編輯**所產生連結`Html.ActionLink`中的方法*Views\Movies\Index.cshtml*檢視：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cshtml)]

![Html.ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html`物件是使用屬性上公開的協助程式[System.Web.Mvc.WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基底類別。 `ActionLink`方法的協助程式輕鬆地以動態方式產生連結至動作方法，控制站上的 HTML 超連結。 第一個引數`ActionLink`方法會呈現的連結文字 (例如`<a>Edit Me</a>`)。 第二個引數是要叫用的動作方法的名稱。 最後一個引數是[匿名物件](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)產生路由資料 （在此案例中，識別碼為 4）。

產生上圖所示的連結是`http://localhost:xxxxx/Movies/Edit/4`。 預設路由 (在中建立*應用程式\_Start\RouteConfig.cs*) 會在 URL 模式`{controller}/{action}/{id}`。 因此，ASP.NET 會將轉譯`http://localhost:xxxxx/Movies/Edit/4`要求`Edit`動作方法的`Movies`控制站與參數`ID`等於 4。 檢查下列程式碼*應用程式\_Start\RouteConfig.cs*檔案。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs)]

您也可以傳遞使用查詢字串的動作方法參數。 例如，URL`http://localhost:xxxxx/Movies/Edit?ID=4`也會將參數傳遞`ID`為 4 到`Edit`動作方法的`Movies`控制站。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

開啟`Movies`控制站。 這兩個`Edit`動作方法如下所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cs)]

請注意，第二個 `Edit` 動作方法的前面是 `HttpPost` 屬性。 這個屬性會指定該多載`Edit`只會針對 POST 要求叫用方法。 您可以套用`HttpGet`屬性的第一個編輯方法，但並不需要因為它是預設值。 (我們會以隱含方式指派的動作方法`HttpGet`屬性為`HttpGet`方法。)

`HttpGet` `Edit`方法會接受影片識別碼參數、 查詢使用 Entity Framework 電影`Find`方法，並將選取的電影傳回 Edit 檢視。 ID 參數指定[預設值](https://msdn.microsoft.com/library/dd264739.aspx)的零，如果`Edit`參數呼叫方法。 如果找不到電影， [HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx)會傳回。 當 Scaffolding 系統建立 Edit 檢視時，它會檢查 `Movie` 類別，並建立程式碼為類別的每個屬性轉譯 `<label>` 和 `<input>` 元素。 下列範例會顯示所產生的 Edit 檢視：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cshtml)]

請注意檢視範本的都有`@model MvcMovie.Models.Movie`在檔案頂端的陳述式，這會指定檢視預期檢視範本類型模型`Movie`。

Scaffold 程式碼使用一些*helper 方法*來簡化 HTML 標記。 [ `Html.LabelFor` ](https://msdn.microsoft.com/library/gg401864(VS.98).aspx)協助程式會顯示欄位的名稱 (&quot;標題&quot;， &quot;ReleaseDate&quot;， &quot;Genre&quot;，或&quot;價格&quot;). [ `Html.EditorFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx)協助程式都可呈現 HTML`<input>`項目。 [ `Html.ValidationMessageFor` ](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx)協助程式會顯示與該屬性相關聯的任何驗證訊息。

執行應用程式，並瀏覽至 */Movies* URL。 按一下 **Edit** 連結。 在瀏覽器中，檢視頁面的原始檔。 如下所示的 HTML 表單項目。

[!code-html[Main](examining-the-edit-methods-and-edit-view/samples/sample5.html?highlight=7,10-11)]

`<input>`項目會在 HTML`<form>`項目其`action`屬性設定為發佈到 */Movies/編輯*URL。 將表單資料將會張貼至伺服器時**編輯**按一下按鈕時。

## <a name="processing-the-post-request"></a>處理 POST 要求

下列清單顯示 `HttpPost` 版本的 `Edit` 動作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cs)]

[ASP.NET MVC 模型繫結](https://msdn.microsoft.com/magazine/hh781022.aspx)採用表單的值，並建立`Movie`物件傳遞為`movie`參數。 `ModelState.IsValid` 方法會驗證表單中提交的資料可用於修改 (編輯或更新) `Movie` 物件。 如果資料是有效的電影資料會儲存至`Movies`的集合`db(MovieDBContext`執行個體)。 新的電影資料會儲存到資料庫，藉由呼叫`SaveChanges`方法的`MovieDBContext`。 儲存資料之後, 的程式碼將使用者重新導向至`Index`動作方法的`MoviesController`類別，用來顯示的電影收藏，包括剛剛所做的變更。

如果已張貼的值不是有效的它們會重新顯示在表單中。 `Html.ValidationMessageFor`中的協助程式*Edit.cshtml*檢視範本負責顯示適當的錯誤訊息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

> [!NOTE]
> 以 jQuery 驗證支援非英文的地區設定，請使用逗號 (&quot;，&quot;) 的小數點，您必須加入*globalize.js*和您的特定*cultures/globalize.cultures.js*檔案 (從[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和使用的 JavaScript `Globalize.parseFloat`。 下列程式碼會顯示在 Views\Movies\Edit.cshtml 檔案，才能使用已修改&quot;FR-FR&quot;文化特性：


[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

十進位的欄位可能需要逗號，沒有小數點。 為暫時的修正程式，您可以將 globalization 項目加入專案的根 web.config 檔案。 下列程式碼會顯示與設為 英文 （美國） 文化特性的全球化項目。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.xml)]

所有`HttpGet`方法遵循類似的模式。 他們會取得電影物件 (或物件的清單，這種案例`Index`)，並將模型傳遞至檢視。 `Create`方法會將空白電影物件傳遞給建立檢視。 建立、編輯、刪除或以其他方式修改資料的所有方法都會在方法的 `HttpPost` 多載中執行這個動作。 修改資料中的 HTTP GET 方法會造成安全性風險，部落格張貼文章中所述[ASP.NET MVC 秘訣 #46 – 不使用刪除連結，因為它們會造成安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改的 GET 方法中的資料也會違反 HTTP 最佳做法和架構[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式指定 GET 要求不應該變更應用程式的狀態。 也就是說，執行 GET 作業應該是安全的作業，沒有任何副作用，而且不會修改您的保存資料。

## <a name="adding-a-search-method-and-search-view"></a>新增搜尋方法和搜尋檢視

在本節中，您將新增`SearchIndex`動作方法，可讓您搜尋的內容類型或名稱的電影。 這會是可透過 */Movies/SearchIndex* URL。 要求將會顯示 HTML 表單，其中包含使用者可以輸入以搜尋電影的輸入項目。 當使用者提交表單時，動作方法會取得使用者張貼的搜尋值，並使用值來搜尋資料庫。

## <a name="displaying-the-searchindex-form"></a>顯示 SearchIndex 表單

加上啟動`SearchIndex`至現有的動作方法`MoviesController`類別。 此方法會傳回包含一個 HTML 表單的檢視。 程式碼如下：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

第一行`SearchIndex`方法會建立下列[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)查詢，以選取電影：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cs)]

到目前為止，定義查詢，但尚未針對資料存放區尚未執行。

如果`searchString`參數包含字串，會修改電影查詢來篩選搜尋字串，使用下列程式碼的值：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample11.cs)]

上述 `s => s.Title` 程式碼是 [Lambda 運算式](https://msdn.microsoft.com/library/bb397687.aspx)。 Lambda 會用來在以方法為基礎[LINQ](https://msdn.microsoft.com/library/bb397926.aspx)這類查詢作為標準查詢運算子方法的引數[其中](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx)上述的程式碼中使用的方法。 當定義或修改這些呼叫的方法，例如，不會執行 LINQ 查詢`Where`或`OrderBy`。 相反地，延後查詢執行，這表示延遲評估的運算式，直到實際反覆運算其實現的值或[ `ToList` ](https://msdn.microsoft.com/library/bb342261.aspx)呼叫方法。 在 [`SearchIndex`範例中，在 SearchIndex] 檢視中執行查詢。 如需延後查詢執行的詳細資訊，請參閱[查詢執行](https://msdn.microsoft.com/library/bb738633.aspx)。

現在您可以實作`SearchIndex`會向使用者顯示表單的檢視。 以滑鼠右鍵按一下`SearchIndex`方法，然後按一下**加入檢視**。 在 **加入檢視**對話方塊方塊中，指定您要傳遞`Movie`檢視範本作為模型類別的物件。 在  **Scaffold 樣板**清單中，選擇**清單**，然後按一下**新增**。

![AddSearchView](examining-the-edit-methods-and-edit-view/_static/image5.png)

當您按一下 [**新增**] 按鈕， *Views\Movies\SearchIndex.cshtml*建立檢視範本。 因為您選取**清單**中**Scaffold 樣板**清單中，自動產生的 Visual Studio (包含 scaffold 的) 某些檢視中的預設標記。 Scaffolding 將建立一個 HTML 表單。 它會檢查`Movie`類別和建立的程式碼，來呈現`<label>`類別的每一個屬性的項目。 下列清單會顯示建立檢視所產生：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample12.cshtml)]

執行應用程式，並瀏覽至 */Movies/SearchIndex*。 將查詢字串 (例如 `?searchString=ghost`) 附加至 URL。 隨即顯示篩選過的電影。

![SearchQryStr](examining-the-edit-methods-and-edit-view/_static/image6.png)

如果您變更的簽章`SearchIndex`方法具有一個名為參數`id`，則`id`參數會比對`{id}`預留位置的預設路由中的設定*Global.asax*檔案。

[!code-json[Main](examining-the-edit-methods-and-edit-view/samples/sample13.json)]

原始`SearchIndex`方法看起來像這樣：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample14.cs)]

已修改`SearchIndex`方法看起來如下：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample15.cs?highlight=1,3)]

您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。

![SearchRouteData](examining-the-edit-methods-and-edit-view/_static/image7.png)

但是，您不能期望使用者在每次想要搜尋電影時修改 URL。 所以現在您將 UI，可協助他們篩選電影。 如果您變更的簽章`SearchIndex`方法，以測試如何傳遞路由繫結的 ID 參數，將它變更以便您`SearchIndex`方法會採用字串參數，名為`searchString`:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample16.cs)]

開啟*Views\Movies\SearchIndex.cshtml*檔案，然後之後`@Html.ActionLink("Create New", "Create")`，新增下列：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample17.cshtml?highlight=2)]

下列範例示範的一部分*Views\Movies\SearchIndex.cshtml*檔案以加入篩選標記。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample18.cshtml?highlight=12-15)]

`Html.BeginForm`協助程式會建立開頭`<form>`標記。 `Html.BeginForm`協助程式會導致表單張貼至本身，當使用者提交表單時，依序按一下**篩選** 按鈕。

執行應用程式並再次嘗試搜尋電影。

![](examining-the-edit-methods-and-edit-view/_static/image8.png)

沒有任何`HttpPost`多載`SearchIndex`方法。 您不需要它，因為方法不會變更狀態的應用程式，只會篩選資料。

您可以新增下列 `HttpPost SearchIndex` 方法。 在此情況下，會比對動作啟動程式`HttpPost SearchIndex`方法，而`HttpPost SearchIndex`方法會執行下面的影像所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample19.cs)]

![SearchPostGhost](examining-the-edit-methods-and-edit-view/_static/image9.png)

不過，即使您新增這個 `HttpPost` 版本的 `SearchIndex` 方法，在如何全部實作此方法方面仍然有其限制。 假設您想要將特定的搜尋加為書籤，或者想要傳送連結給朋友，讓他們可以點選來查看相同的電影篩選清單。 請注意，HTTP POST 要求的 URL 等同於 GET 要求 URL （localhost: xxxxx/Movies/SearchIndex）--在 URL 本身沒有搜尋資訊。 權限現在，搜尋字串資訊會傳送到伺服器做為表單欄位值。 這表示您無法擷取該搜尋資訊以加上書籤，或傳送給朋友在 URL 中。

解決方法是使用的多載`BeginForm`，指定 POST 要求，應該將搜尋資訊新增至 URL 和，它應該會路由傳送至的 HttpGet 新版`SearchIndex`方法。 取代現有無參數`BeginForm`以下列方法：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample20.cshtml)]

![BeginFormPost_SM](examining-the-edit-methods-and-edit-view/_static/image10.png)

現在當您提交搜尋時，URL 會包含搜尋查詢字串。 即使您有 `HttpPost SearchIndex` 方法，搜尋也會移至 `HttpGet SearchIndex` 動作方法。

![SearchIndexWithGetURL](examining-the-edit-methods-and-edit-view/_static/image11.png)

## <a name="adding-search-by-genre"></a>新增依內容類型搜尋

如果您已新增`HttpPost`新版`SearchIndex`方法，立即將其刪除。

接下來，您將新增特定功能，讓使用者進行搜尋的電影內容類型。 以下列程式碼取代 `SearchIndex` 方法：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample21.cs)]

本版`SearchIndex`方法會採用額外的參數，也就是`movieGenre`。 建立程式碼的前幾行`List`物件來保存從資料庫的電影內容類型。

下列程式碼是一種 LINQ 查詢，其會從資料庫中擷取所有的內容類型。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample22.cs)]

程式碼會使用`AddRange`方法的泛型`List`將清單中的所有不同的內容類型的集合。 (不含`Distinct`修飾詞，會加入重複的內容類型 — 比方說，喜劇會新增兩次在我們的範例)。 程式碼再將儲存在內容類型清單`ViewBag`物件。

下列程式碼示範如何檢查`movieGenre`參數。 如果不是空的程式碼進一步限制電影查詢來限制所選的影片來指定內容類型。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample23.cs)]

## <a name="adding-markup-to-the-searchindex-view-to-support-search-by-genre"></a>將標記加入至 SearchIndex 檢視，以支援依內容類型搜尋

新增`Html.DropDownList`協助專家*Views\Movies\SearchIndex.cshtml*檔案，之前`TextBox`協助程式。 完整的標記如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample24.cshtml?highlight=4)]

執行應用程式，並瀏覽至 */Movies/SearchIndex*。 依內容類型、 電影名稱，以及這兩個準則，請嘗試搜尋。

![](examining-the-edit-methods-and-edit-view/_static/image12.png)

在本節中您可以檢查的 CRUD 動作方法和 framework 所產生的檢視。 您所建立的搜尋動作方法和檢視，可讓使用者進行搜尋電影標題和內容類型。 在下一步 區段中，您將探討如何將屬性新增至`Movie`模型，以及如何將會自動建立測試資料庫的初始設定式。

> [!div class="step-by-step"]
> [上一頁](accessing-your-models-data-from-a-controller.md)
> [下一頁](adding-a-new-field-to-the-movie-model-and-table.md)
