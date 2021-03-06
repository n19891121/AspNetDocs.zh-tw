---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: 檢查編輯方法和編輯檢視 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 6cef963910b957e8b4ad7c7909385f6dbdff95c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582436"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>檢查編輯方法與編輯檢視

依[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本節中，您將檢查針對電影控制器產生的 `Edit` 動作方法和 views。 但首先我們要進行簡短的 diversion，讓發行日期看起來更好。 開啟*Models\Movie.cs*檔案，並新增反白顯示的行，如下所示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

您也可以讓日期文化特性如下所示：

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

接下來的教學課程中將涵蓋 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。 [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) 屬性指定要顯示的欄位名稱 (在本例中為 "Release Date"，而不是 "ReleaseDate")。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性會指定資料的類型（在此案例中為日期），因此不會顯示儲存在欄位中的時間資訊。 Chrome 瀏覽器中錯誤呈現日期格式的 bug 需要[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性。

執行應用程式，並流覽至 `Movies` 控制器。 將滑鼠指標放在**編輯**連結上方，以查看其所連結的 URL。

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

[**編輯**] 連結是由 [ *Views\Movies\Index.cshtml* ] 視圖中的 [`Html.ActionLink`] 方法所產生：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![.Html](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html` 物件是使用[WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx)基類上的屬性所公開的協助程式。 Helper 的 `ActionLink` 方法，可讓您輕鬆地動態產生連結至控制器上動作方法的 HTML 超連結。 `ActionLink` 方法的第一個引數是要呈現的連結文字（例如，`<a>Edit Me</a>`）。 第二個引數是要叫用之動作方法的名稱（在此案例中為 `Edit` 動作）。 最後一個引數是[匿名物件](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx)，它會產生路由資料（在此案例中，識別碼為4）。

上圖中顯示的產生連結 `http://localhost:1234/Movies/Edit/4`。 預設路由（在*應用程式\_Start\RouteConfig.cs*中建立）會採用 URL 模式 `{controller}/{action}/{id}`。 因此，ASP.NET 會將 `http://localhost:1234/Movies/Edit/4` 轉譯為 `Movies` 控制器 `Edit` 動作方法的要求，其參數 `ID` 等於4。 檢查*應用程式\_Start\RouteConfig.cs*檔案中的下列程式碼。 [Maproute.html](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法是用來將 HTTP 要求路由傳送至正確的控制器和動作方法，並提供選擇性的 ID 參數。 [Maproute.html](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md)方法也會由[HtmlHelpers](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) （例如 `ActionLink`）用來產生指定的控制器、動作方法和任何路由資料的 url。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

您也可以使用查詢字串來傳遞動作方法參數。 例如，URL `http://localhost:1234/Movies/Edit?ID=3` 也會將參數 `ID` 3 傳遞給 `Movies` 控制器的 `Edit` 動作方法。

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

開啟 `Movies` 控制器。 這兩個 `Edit` 動作方法如下所示。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

請注意，第二個 `Edit` 動作方法的前面是 `HttpPost` 屬性。 這個屬性指定只能針對 POST 要求叫用 `Edit` 方法的多載。 您可以將 `HttpGet` 屬性套用至第一個 edit 方法，但這不是必要的，因為它是預設值。 （我們會參考隱含指派 `HttpGet` 屬性做為 `HttpGet` 方法的動作方法）。[Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)屬性是另一個重要的安全性機制，可防止駭客將資料張貼到您的模型。 您應該只在您想要變更的 bind 屬性中包含屬性。 您可以在我的[防止大量指派安全性注意事項](https://go.microsoft.com/fwlink/?LinkId=317598)中閱讀關於防止大量指派和 bind 屬性的資訊。 在本教學課程中使用的簡單模型中，我們將會系結模型中的所有資料。 [ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)屬性是用來防止偽造要求，並與編輯檢視檔案（*Views\Movies\Edit.cshtml*）中的 `@Html.AntiForgeryToken()` 配對，如下所示：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()` 會在 `Movies` 控制器的 `Edit` 方法中，產生一個必須符合的隱藏格式防偽造 token。 若要深入瞭解跨網站偽造要求（也稱為 XSRF 或 CSRF），請參閱我在[MVC 中的 XSRF/CSRF 防護](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)教學課程。

`HttpGet` `Edit` 方法會採用 movie ID 參數、使用 Entity Framework `Find` 方法來查詢電影，並將選取的影片傳回編輯檢視。 如果找不到電影，則會傳回[HttpNotFound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) 。 當 Scaffolding 系統建立 Edit 檢視時，它會檢查 `Movie` 類別，並建立程式碼為類別的每個屬性轉譯 `<label>` 和 `<input>` 元素。 下列範例顯示 visual studio 範例系統所產生的編輯檢視：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

請注意，view 範本在檔案頂端有一個 `@model MvcMovie.Models.Movie` 語句，這表示此視圖預期視圖範本的模型是 `Movie`的類型。

Scaffold 程式碼會使用數個*helper 方法*來簡化 HTML 標籤。 [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) helper 會顯示欄位的名稱（&quot;Title&quot;、&quot;ReleaseDate&quot;、&quot;內容類型&quot;或 &quot;價格&quot;）。 [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) helper 會呈現 HTML `<input>` 元素。 [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) helper 會顯示與該屬性相關聯的任何驗證訊息。

執行應用程式，並流覽至 */Movies* URL。 按一下 **Edit** 連結。 在瀏覽器中，檢視頁面的原始檔。 Form 元素的 HTML 如下所示。

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>` 專案位於 HTML `<form>` 元素中，其 `action` 屬性設定為張貼至 */Movies/Edit* URL。 當您按一下 [**儲存**] 按鈕時，表單會將資料張貼至伺服器。 第二行會顯示 `@Html.AntiForgeryToken()` 呼叫所產生的隱藏[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token。

## <a name="processing-the-post-request"></a>處理 POST 要求

下列清單顯示 `HttpPost` 版本的 `Edit` 動作方法。

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[ValidateAntiForgeryToken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx)屬性會驗證在視圖中由 `@Html.AntiForgeryToken()` 呼叫所產生的[XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) token。

[ASP.NET MVC 模型](https://msdn.microsoft.com/library/dd410405.aspx)系結器會採用已張貼的表單值，並建立當做 `movie` 參數傳遞的 `Movie` 物件。 `ModelState.IsValid` 會確認表單中提交的資料可以用來修改（編輯或更新） `Movie` 物件。 如果資料有效，則會將電影資料儲存至 `db`（`MovieDBContext` 實例）的 `Movies` 集合。 新的電影資料會藉由呼叫 `MovieDBContext`的 `SaveChanges` 方法，儲存至資料庫。 儲存資料之後，程式碼將使用者重新導向至 `Index` 類別的 `MoviesController` 動作方法，此方法會顯示電影集合，包括剛剛所進行的變更。

一旦用戶端驗證判斷欄位的值無效，就會顯示錯誤訊息。 如果 JavaScript 已停用，則會停用用戶端驗證。 不過，伺服器偵測到張貼的值是不正確，而且表單值會重新顯示，並出現錯誤訊息。

稍後在本教學課程中會更詳細地檢查驗證。

[*編輯 cshtml* ] 視圖範本中的 `Html.ValidationMessageFor` helper 會負責顯示適當的錯誤訊息。

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

所有的 `HttpGet` 方法都遵循類似的模式。 他們會取得電影物件（或物件清單，如果是 `Index`），並將模型傳遞給視圖。 `Create` 方法會將空的 movie 物件傳遞至 Create view。 建立、編輯、刪除或以其他方式修改資料的所有方法都會在方法的 `HttpPost` 多載中執行這個動作。 修改 HTTP GET 方法中的資料會有安全性風險，如 blog 文章[ASP.NET MVC Tip #46 –請勿使用刪除連結，因為它們會建立安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)。 修改 GET 方法中的資料也會違反 HTTP 最佳做法和架構[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer)模式，這會指定 GET 要求不應該變更應用程式的狀態。 也就是說，執行 GET 作業應該是安全的作業，沒有任何副作用，而且不會修改您的保存資料。

## <a name="jquery-validation-for-non-english-locales"></a>非英文地區設定的 jQuery 驗證

如果您使用美式英文的電腦，可以略過本節並移至下一個教學課程。 您可以在這裡下載本教學[課程](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)的全球化版本。 如需國際化的絕佳兩個部分教學課程，請參閱[Nadeem 的 ASP.NET MVC 5 國際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)。

> [!NOTE]
> 若要支援對小數點使用逗號（&quot;、&quot;）之非英文地區設定的 jQuery 驗證，以及非英文日期格式，您必須包含*全球化 .js*和您的特定*文化特性/全球化。文化特性 .js*檔案（從[https://github.com/jquery/globalize](https://github.com/jquery/globalize) ）和 JavaScript，以使用 `Globalize.parseFloat`。 您可以從 NuGet 取得 jQuery 非英文驗證。 （如果您使用英文地區設定，請勿安裝全球化）。

1. 從 [**工具**] 功能表按一下 [ **NuGet 套件管理員**]，然後按一下 [**管理方案的 NuGet 套件**]。

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. 在左窗格中，選取<strong>[流覽] *。</strong>* （請參閱下圖）。
3. 在 [輸入] 方塊中，輸入 [全球化] * *。

    ![](examining-the-edit-methods-and-edit-view/_static/image6.png) 選擇 [`jQuery.Validation.Globalize`]，選擇 [`MvcMovie`]，然後按一下 [**安裝**]。 *Scripts\jquery.globalize\globalize.js*檔案將會新增至您的專案。 \* Scripts\jquery.globalize\cultures\* 資料夾將包含許多文化特性 JavaScript 檔案。 請注意，安裝此套件可能需要5分鐘的時間。

   下列程式碼顯示 Views\Movies\Edit.cshtml 檔案的修改：

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

若要避免在每個編輯檢視中重複此程式碼，您可以將它移至配置檔案。 若要優化腳本下載，請參閱我的教學課程[捆綁和縮制](../../performance/bundling-and-minification.md)。

如需詳細資訊，請參閱[ASP.NET mvc 3 國際化](http://afana.me/post/aspnet-mvc-internationalization.aspx)和[ASP.NET mvc 3 國際化-第2部分（NerdDinner）](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx)。

做為暫時的修正，如果您無法在地區設定中使用驗證，您可以強制電腦使用美式英文，或者您可以在瀏覽器中停用 JavaScript。 若要強制電腦使用美式英文，您可以將全球化元素新增至*專案根 web.config 檔案。* 下列程式碼顯示將文化特性設定為美國英文的全球化元素。

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a>在下一個教學課程中，我們將會實行搜尋功能。

> [!div class="step-by-step"]
> [上一頁](accessing-your-models-data-from-a-controller.md)
> [下一頁](adding-search.md)
