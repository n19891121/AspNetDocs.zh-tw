---
title: ASP.NET Core 中的 Scaffold Razor 頁面
author: rick-anderson
description: 說明 Scaffolding 所產生的 Razor 頁面。
ms.author: riande
ms.date: 12/4/2018
uid: tutorials/razor-pages/page
ms.openlocfilehash: ad87e3da72c3dd6adf8cf55d16da58fa47ed5542
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57055505"
---
# <a name="scaffolded-razor-pages-in-aspnet-core"></a>ASP.NET Core 中的 Scaffold Razor 頁面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

本教學課程會檢查在先前教學課程中 Scaffolding 所建立的 Razor 頁面。

[檢視或下載](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22)範例。

## <a name="the-create-delete-details-and-edit-pages"></a>Create、Delete、Details 和 Edit 頁面

檢查 *Pages/Movies/Index.cshtml.cs* 頁面模型：

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml.cs)]

Razor 頁面衍生自 `PageModel`。 依照慣例，`PageModel` 衍生的類別稱為 `<PageName>Model`。 建構函式會使用[相依性插入](xref:fundamentals/dependency-injection)將 `RazorPagesMovieContext` 新增至頁面中。 所有 Scaffold 頁面都遵循這個模式。 如需使用 Entity Framework 進行非同步程式設計的詳細資訊，請參閱[非同步程式碼](xref:data/ef-rp/intro#asynchronous-code)。

當針對頁面提出要求時，`OnGetAsync` 方法會將電影清單傳回 Razor 頁面。 在 Razor 頁面上會呼叫 `OnGetAsync` 或 `OnGet` 來初始化頁面的狀態。 在此情況下，`OnGetAsync` 會取得電影清單並加以顯示。

當 `OnGet` 傳回 `void` 或 `OnGetAsync` 傳回 `Task` 時，並未使用任何傳回方法。 當傳回型別是 `IActionResult` 或 `Task<IActionResult>` 時，必須提供傳回陳述式。 例如，*Pages/Movies/Create.cshtml.cs* `OnPostAsync` 方法：

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml.cs?name=snippet)]

<a name="index"></a> 請檢查 *Pages/Movies/Index.cshtml* Razor 頁面：

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml)]

Razor 可以從 HTML 轉換成 C# 或 Razor 特定標記。 當 `@` 符號後面接著 [Razor 保留關鍵字](xref:mvc/views/razor#razor-reserved-keywords) 時，它會轉換成 Razor 特定標記，否則就會轉換成 C#。

`@page` Razor 指示詞可讓檔案成為 MVC 動作，這表示它可以處理要求。 `@page` 必須是頁面上的第一個 Razor 指示詞。 `@page` 是轉換成 Razor 特定標記的範例。 如需詳細資訊，請參閱 [Razor 語法](xref:mvc/views/razor#razor-syntax)。

檢查下列 HTML 協助程式中使用的 Lambda 運算式：

```cshtml
@Html.DisplayNameFor(model => model.Movie[0].Title))
```

`DisplayNameFor` HTML 協助程式會檢查 Lambda 運算式中參考的 `Title` 屬性來判斷顯示名稱。 Lambda 運算式是進行檢查而不是評估。 這表示當 `model`、`model.Movie` 或 `model.Movie[0]` 是 `null` 或空白時，不會有任何存取違規。 在評估 Lambda 運算式時 (例如，使用 `@Html.DisplayFor(modelItem => item.Title)`)，會評估模型的屬性值。

<a name="md"></a>
### <a name="the-model-directive"></a>
  @model 指示詞

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-2&highlight=2)]

`@model` 指示詞會指定傳遞至 Razor 頁面的模型類型。 在上述範例中，`@model` 行可讓 `PageModel` 衍生的類別供 Razor 頁面使用。 此模型用於頁面上的 `@Html.DisplayNameFor` 和 `@Html.DisplayFor` [HTML 協助程式](/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs#understanding-html-helpers)。

### <a name="the-layout-page"></a>版面配置頁

選取功能表連結 (**RazorPagesMovie**、**Home** 及 **Privacy**)。 每個頁面會顯示相同的功能表配置。 功能表配置會在 *Pages/Shared/_Layout.cshtml* 檔案中實作。 開啟 *Pages/Shared/_Layout.cshtml* 檔案。

[版面配置](xref:mvc/views/layout)範本可讓您在某個位置指定網站的 HTML 容器配置，然後將它套用到網站中的多個頁面。 找到 `@RenderBody()` 這行。 `RenderBody` 是一個「包裝」在版面配置頁中的預留位置，可供顯示您建立的所有頁面特定檢視。 例如，如果您選取 [Privacy] 連結，就會在 `RenderBody` 方法內呈現 **Pages/Privacy.cshtml** 檢視。

<a name="vd"></a>
### <a name="viewdata-and-layout"></a>ViewData 和 Layout

請考慮來自 *Pages/Movies/Index.cshtml* 檔案的下列程式碼：

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Index.cshtml?range=1-6&highlight=4-999)]

上述強調顯示的程式碼是 Razor 轉換成 C# 的範例。 `{` 和 `}` 字元中含括 C# 程式碼的區塊。

`PageModel` 基底類別有 `ViewData` 字典屬性，可用來新增至您想要傳遞到檢視的資料。 您可以使用索引鍵/值模式將物件新增至 `ViewData` 字典。 在上述範例中，"Title" 屬性會新增至 `ViewData` 字典。 

"Title" 屬性是用於 *Pages/Shared/_Layout.cshtml* 檔案。 下列標記會顯示 *_Layout.cshtml* 檔案的前幾行。

<!-- we need a snapshot copy of layout because we are
changing in in the next step. 
-->
[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/NU/_Layout.cshtml?highlight=6-99)]

行 `@*Markup removed for brevity.*@` 是 Razor 註解，不會出現在您的配置檔案中。 不同於 HTML 註解 (`<!-- -->`)，Razor 註解不會傳送到用戶端。

### <a name="update-the-layout"></a>更新配置

變更 *Pages/Shared/_Layout.cshtml* 檔案中的 `<title>` 元素，以顯示 **Movie** 而不是 **RazorPagesMovie**。

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Shared/_Layout.cshtml?range=1-6&highlight=6)]


在 *Pages/Shared/_Layout.cshtml* 檔案中尋找下列錨點元素。

```cshtml
<a class="navbar-brand" asp-area="" asp-page="/Index">RazorPagesMovie</a>
```

以下列標記來取代上述項目。

```cshtml
<a class="navbar-brand" asp-page="/Movies/Index">RpMovie</a>
```

上述的錨點項目是[標記協助程式](xref:mvc/views/tag-helpers/intro)。 在此情況下，它是[錨點標記協助程式](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)。 `asp-page="/Movies/Index"` 標記協助程式的屬性和值會建立 `/Movies/Index` Razor 頁面的連結。 `asp-area` 屬性值為空白，因此不會在連結中使用該區域。 如需詳細資訊，請參閱[區域](xref:mvc/controllers/areas)。

儲存變更，並按一下 **RpMovie** 連結來測試應用程式。 如有任何問題，請參閱 GitHub 中的 [_Layout.cshtml](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Shared/_Layout.cshtml) 檔案。

測試其他連結 (**Home**、**RpMovie**、**Create**、**Edit** 和 **Delete**)。 每一頁都會設定標題，您可以在瀏覽器索引標籤中看到該標題。當您將某個頁面加為書籤時，會使用標題來表示書籤。

> [!NOTE]
> 您可能無法在 `Price` 欄位中輸入小數逗號。 若要對使用逗號 (",") 作為小數點的非英文地區設定和非英文日期欄位支援 [jQuery 驗證](https://jqueryvalidation.org/)，您必須採取將應用程式全球化的步驟。 這個 [GitHub 問題 4076](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420) 有加入小數逗號的指示。

`Layout` 屬性是在 *Pages/_ViewStart.cshtml* 檔案中設定：

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/_ViewStart.cshtml)]

上述標記會針對 *Pages* 資料夾下的所有 Razor 檔案，將版面配置檔案設定為 *Pages/Shared/_Layout.cshtml*。 如需詳細資訊，請參閱 [Layout](xref:razor-pages/index#layout)。

### <a name="the-create-page-model"></a>Create 頁面模型

檢查 *Pages/Movies/Create.cshtml.cs* 頁面模型：

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetALL)]

`OnGet` 方法會初始化頁面所需的任何狀態。 建立頁面沒有任何要初始化的狀態，所以傳回 `Page`。 稍後在本教學課程中您會看到 `OnGet` 方法初始化狀態。 `Page` 方法會建立 `PageResult` 物件，用以呈現 *Create.cshtml* 頁面。

`Movie` 屬性 (property) 使用 `[BindProperty]` 屬性 (attribute) 來加入[模型繫結](xref:mvc/models/model-binding)。 當 Create 表單發佈表單值時，ASP.NET Core 執行階段會將發佈的值繫結至 `Movie` 模型。

當頁面發佈表單資料時，即會執行 `OnPostAsync` 方法：

[!code-csharp[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml.cs?name=snippetPost)]

如果沒有任何模型錯誤，將會重新顯示表單，以及任何發佈的表單資料。 大部分的模型錯誤可以在發佈表單之前，於用戶端上攔截到。 模型錯誤的範例為針對日期欄位發佈無法轉換為日期的值。 稍後的教學課程中將討論用戶端驗證和模型驗證。

如果沒有任何模型錯誤，就會儲存資料，而瀏覽器則會重新導向至 Index 頁面。

### <a name="the-create-razor-page"></a>[Create Razor] (建立 Razor) 頁面

檢查 *Pages/Movies/Create.cshtml* Razor 頁面檔案：

[!code-cshtml[](razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml)]

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

Visual Studio 會以特別的粗體字型顯示 `<form method="post">` 標籤，用於標籤協助程式：

![Create.cshtml 頁面的 VS17 檢視](page/_static/th.png)
<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

如需標籤協助程式 (例如 `<form method="post">`) 的詳細資訊，請參閱 [ASP.NET Core 中的標籤協助程式](xref:mvc/views/tag-helpers/intro)。

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

Visual Studio for Mac 會以特別的粗體字型顯示 `<form method="post">` 標籤，用於標籤協助程式。

---  
<!-- End of VS tabs -->

`<form method="post">` 項目是[表單標記協助程式](xref:mvc/views/working-with-forms#the-form-tag-helper)。 表單標記協助程式會自動包含 [antiforgery 語彙基元](xref:security/anti-request-forgery)。

Scaffolding 引擎會在模型中建立每個欄位的 Razor 標記 (除了識別碼)，如下所示：

[!code-cshtml[](~/tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=15-20)]

[驗證標記協助程式](xref:mvc/views/working-with-forms#the-validation-tag-helpers) (`<div asp-validation-summary` 和 ` <span asp-validation-for`) 會顯示驗證錯誤。 驗證將於本文稍後詳細討論到。

[標籤標記協助程式](xref:mvc/views/working-with-forms#the-label-tag-helper) (`<label asp-for="Movie.Title" class="control-label"></label>`) 會產生 `Title` 屬性 (property) 的標籤標題和 `for` 屬性 (attribute)。

[輸入標記協助程式](xref:mvc/views/working-with-forms) (`<input asp-for="Movie.Title" class="form-control" />`) 會使用[DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 屬性，並產生在用戶端上進行 jQuery 驗證所需的 HTML 屬性。

> [!div class="step-by-step"]
> [上一步：新增模型](xref:tutorials/razor-pages/model)
> [下一步：資料庫](xref:tutorials/razor-pages/sql)
