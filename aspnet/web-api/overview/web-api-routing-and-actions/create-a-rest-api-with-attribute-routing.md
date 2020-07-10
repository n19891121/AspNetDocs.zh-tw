---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: 在 ASP.NET Web API 2 中建立具有屬性路由的 REST API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188781"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>使用 ASP.NET Web API 2 中的屬性路由建立 REST API

由[Mike Wasson](https://github.com/MikeWasson)

Web API 2 支援新類型的路由，稱為*屬性路由*。 如需屬性路由的一般總覽，請參閱[WEB API 2 中的屬性路由](attribute-routing-in-web-api-2.md)。 在本教學課程中，您將使用屬性路由來建立書籍集合的 REST API。 API 將支援下列動作：

| 動作 | 範例 URI |
| --- | --- |
| 取得所有書籍的清單。 | /api/books |
| 依識別碼取得書籍。 | /api/books/1 |
| 取得書籍的詳細資料。 | /api/books/1/details |
| 依內容類型取得書籍清單。 | /api/books/fantasy |
| 依發行日期取得書籍清單。 | /api/books/date/2013-02-16/api/books/date/2013/02/16 (替代表單)  |
| 取得特定作者的書籍清單。 | /api/authors/1/books |

所有方法都是唯讀的 (HTTP GET 要求) 。

針對資料層，我們將使用 Entity Framework。 書籍記錄會有下欄欄位：

- 識別碼
- 標題
- Genre
- 發行日期
- 價格
- 描述
- 作者資料表的 AuthorID (外鍵) 

不過，針對大部分的要求，API 會傳回此資料的子集， (標題、作者和內容類型) 。 若要取得完整的記錄，用戶端會要求 `/api/books/{id}/details` 。

## <a name="prerequisites"></a>必要條件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區、Professional 或 Enterprise edition。

## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

從執行 Visual Studio 開始。 從 [檔案]**** 功能表選取 [新增]****，再選取 [專案]****。

展開 [**已安裝**的  >  **Visual c #** ] 類別。 在 [ **Visual c #**] 底下，選取 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET Web 應用程式 (] .NET Framework) **]。 將專案命名為 &quot; BooksAPI &quot; 。

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

在 [**新增 ASP.NET Web 應用程式**] 對話方塊中，選取 [**空白**] 範本。 在 [新增資料夾和核心參考] 底下，選取 [ **WEB API** ] 核取方塊。 按一下 [確定]。

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

這會建立針對 Web API 功能所設定的基本架構專案。

### <a name="domain-models"></a>領域模型

接下來，加入網域模型的類別。 在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。 選取 [**新增**]，然後選取 [**類別**]。 將類別命名為 `Author`。

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

將 Author.cs 中的程式碼取代為下列內容：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

現在，新增另一個名為 `Book` 的類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>新增 Web API 控制器

在此步驟中，我們將新增使用 Entity Framework 做為資料層的 Web API 控制器。

按 CTRL+SHIFT+B 以建置專案。 Entity Framework 會使用反映來探索模型的屬性，因此需要已編譯的元件來建立資料庫架構。

在 [方案總管] 中，於 Controllers 資料夾上按一下滑鼠右鍵。 選取 [**新增**]，然後選取 [**控制器**]。

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

在 [**新增 Scaffold** ] 對話方塊中，選取 [**具有動作的 Web API 2 控制器]，並使用 Entity Framework**。

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

在 [**新增控制器**] 對話方塊的 [**控制器名稱**] 中，輸入 &quot; BooksController &quot; 。 選取 [ &quot; 使用非同步控制器動作 &quot; ] 核取方塊。 針對 [**模型類別**]，選取 [ &quot; 書籍] &quot; 。  (如果您沒有看到 `Book` 下拉式清單中列出的類別，請確定您已建立專案。 ) 然後按一下 [+] 按鈕。

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

按一下 [**新增資料內容**] 對話方塊中的 [**加入**]。

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

按一下 [**新增控制器**] 對話方塊中的 [**新增**]。 此架構會新增名為 `BooksController` 的類別，以定義 API 控制器。 它也會在 [模型] 資料夾中新增名為的類別 `BooksAPIContext` ，以定義 Entity Framework 的資料內容。

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>植入資料庫

從 [工具] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。

在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

此命令會建立一個 [遷移] 資料夾，並新增名為 Configuration.cs 的新程式碼檔案。 開啟此檔案，並將下列程式碼新增至 `Configuration.Seed` 方法。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

在 [套件管理員主控台] 視窗中，輸入下列命令。

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

這些命令會建立本機資料庫，並叫用種子方法來填入資料庫。

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>新增 DTO 類別

如果您現在執行應用程式，並將 GET 要求傳送至/api/books/1，回應看起來會像下面這樣。  (我加入縮排以利閱讀。 ) 

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

相反地，我想要此要求傳回欄位的子集。 此外，我希望它傳回作者的名稱，而不是作者識別碼。 為了達成此目的，我們將修改控制器方法，以傳回 (DTO) 的*資料傳輸物件*，而不是 EF 模型。 DTO 是專門設計來攜帶資料的物件。

在方案總管中，以滑鼠右鍵按一下專案，**然後選取 [** 新增] [  |  **新增資料夾**]。 將資料夾命名為 &quot; dto &quot; 。 `BookDto`使用下列定義，將名為的類別新增至 dto 資料夾：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

新增另一個名為 `BookDetailDto`的類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

接下來，更新 `BooksController` 類別以傳回 `BookDto` 實例。 我們將使用可[查詢的. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx)方法將 `Book` 實例投影至 `BookDto` 實例。 以下是控制器類別的更新程式碼。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> 我刪除了 `PutBook` 、 `PostBook` 和 `DeleteBook` 方法，因為本教學課程不需要它們。

現在，如果您執行應用程式並要求/api/books/1，回應主體看起來應該像這樣：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>新增路由屬性

接下來，我們會將控制器轉換成使用屬性路由。 首先，將**RoutePrefix**屬性新增至控制器。 這個屬性會定義此控制器上所有方法的初始 URI 區段。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

然後，將 **[Route]** 屬性新增至控制器動作，如下所示：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

每個控制器方法的路由範本是前置詞加上**route**屬性中所指定的字串。 針對 `GetBook` 方法，路由範本會包含參數化字串 &quot; {id： int} &quot; ，如果 URI 區段包含整數值，則會符合此專案。

| 方法 | 路由範本 | 範例 URI |
| --- | --- | --- |
| `GetBooks` | 「api/書籍」 | `http://localhost/api/books` |
| `GetBook` | "api/書籍/{id： int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>取得書籍詳細資料

若要取得書籍詳細資料，用戶端會將 GET 要求傳送至 `/api/books/{id}/details` ，其中 *{id}* 是書的識別碼。

將下列方法新增至 `BooksController` 類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

如果您要求 `/api/books/1/details` ，回應看起來會像這樣：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>依內容類型取得書籍

若要取得特定類型的書籍清單，用戶端會將 GET 要求傳送至，其中內容類型為內容類型的 `/api/books/genre` 名稱。 *genre* (例如，`/api/books/fantasy`)。

將下列方法新增至 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

在這裡，我們將定義一個路由，其中包含 URI 範本中的 {內容類型} 參數。 請注意，Web API 能夠區分這兩個 Uri，並將它們路由傳送至不同的方法：

`/api/books/1`

`/api/books/fantasy`

這是因為 `GetBook` 方法包含「識別碼」區段必須是整數值的條件約束：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

如果您要求/api/books/fantasy，回應看起來會像這樣：

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>依作者取得書籍

若要取得特定作者的書籍清單，用戶端會將 GET 要求傳送至 `/api/authors/id/books` ，其中*id*是作者的識別碼。

將下列方法新增至 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

這個範例很有趣，因為 &quot; 書籍 &quot; 會被視為作者的子資源 &quot; &quot; 。 此模式在 RESTful Api 中相當常見。

路由範本中的波狀符號 (~) 會覆寫**RoutePrefix**屬性中的路由前置詞。

## <a name="get-books-by-publication-date"></a>依發行日期取得書籍

若要依發行日期取得書籍清單，用戶端會將 GET 要求傳送至 `/api/books/date/yyyy-mm-dd` ，其中*yyyy-mm-dd*是日期。

以下是其中一種方法：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`參數限制為符合**日期時間**值。 這是可行的，但實際上比我們想要的更寬鬆。 例如，這些 Uri 也會符合路由：

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

允許這些 Uri 不會有任何問題。 不過，您可以藉由將正則運算式條件約束加入至路由範本，來限制特定格式的路由：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

現在，只有格式為 yyyy-mm-dd 的日期才 &quot; &quot; 會相符。 請注意，我們不會使用 RegEx 來驗證我們是否獲得實際的日期。 當 Web API 嘗試將 URI 區段轉換成**DateTime**實例時，就會進行處理。 不正確日期（例如 ' 2012-47-99 '）將無法轉換，而且用戶端會收到404錯誤。

您也可以藉 `/api/books/date/yyyy/mm/dd` 由使用不同的 RegEx 新增另一個 **[Route]** 屬性，來支援斜線分隔符號 () 。

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

這裡有一個微妙但重要的詳細資料。 第二個路由範本在 \* {pubdate} 參數開頭有一個萬用字元 () ：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

這會告訴路由引擎，{pubdate} 應該符合 URI 的其餘部分。 根據預設，範本參數會符合單一 URI 區段。 在此情況下，我們希望 {pubdate} 跨越數個 URI 區段：

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>控制器程式碼

以下是 BooksController 類別的完整程式碼。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>摘要

在設計 API 的 Uri 時，屬性路由可讓您擁有更多控制權和更大的彈性。
