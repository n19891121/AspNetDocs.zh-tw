---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: 使用 ASP.NET Web API 2 中的屬性路由建立 REST API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045178"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a>使用 ASP.NET Web API 2 中的屬性路由建立 REST API

由 [Mike Wasson](https://github.com/MikeWasson)

Web API 2 支援新的路由類型，稱為 *屬性路由*。 如需屬性路由的一般總覽，請參閱 [WEB API 2 中的屬性路由](attribute-routing-in-web-api-2.md)。 在本教學課程中，您將使用屬性路由來建立書籍集合的 REST API。 API 將支援下列動作：

| 動作 | 範例 URI |
| --- | --- |
| 取得所有書籍的清單。 | /api/books |
| 依識別碼取得書籍。 | /api/books/1 |
| 取得書籍的詳細資料。 | /api/books/1/details |
| 依內容類型取得書籍清單。 | /api/books/fantasy |
| 依發行日期取得書籍清單。 | /api/books/date/2013-02-16/api/books/date/2013/02/16 (替代表單)  |
| 取得特定作者的書籍清單。 | /api/authors/1/books |

所有方法都是唯讀 (HTTP GET 要求) 。

針對資料層，我們會使用 Entity Framework。 書籍記錄會有下欄欄位：

- 識別碼
- 標題
- Genre
- 發行日期
- 價格
- 描述
- 作者 (外鍵給作者資料表) 

但是針對大部分的要求，API 會傳回此資料的子集 (標題、作者和內容類型) 。 若要取得完整記錄，用戶端要求 `/api/books/{id}/details` 。

## <a name="prerequisites"></a>先決條件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) 社區、Professional 或 Enterprise edition。

## <a name="create-the-visual-studio-project"></a>建立 Visual Studio 專案

從執行 Visual Studio 開始。 從 [檔案]**** 功能表選取 [新增]****，再選取 [專案]****。

展開 [**已安裝**的  >  **Visual c #** ] 類別。 選取 [ **Visual c #**] 底下的 [ **Web**]。 在專案範本清單中，選取 [ **ASP.NET Web 應用程式 (] .NET Framework) **。 將專案命名為 &quot; >booksapi &quot; 。

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

在 [ **新增 ASP.NET Web 應用程式** ] 對話方塊中，選取 **空白** 範本。 在 [新增資料夾和核心參考] 底下，選取 [ **WEB API** ] 核取方塊。 按一下 [確定]。

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

這會建立針對 Web API 功能設定的基本架構專案。

### <a name="domain-models"></a>領域模型

接下來，加入網域模型的類別。 在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。 選取 [ **新增**]，然後選取 [ **類別**]。 將類別命名為 `Author`。

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

以下列程式碼取代 Author.cs 中的程式碼：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

現在新增另一個名為 `Book` 的類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a>新增 Web API 控制器

在此步驟中，我們將新增使用 Entity Framework 作為資料層的 Web API 控制器。

按 CTRL+SHIFT+B 以建置專案。 Entity Framework 使用反映來探索模型的屬性，因此需要已編譯的元件才能建立資料庫架構。

在 [方案總管] 中，於 Controllers 資料夾上按一下滑鼠右鍵。 選取 [ **新增**]，然後選取 [ **控制器**]。

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

在 [ **新增 Scaffold** ] 對話方塊中， **使用 Entity Framework 選取 [具有動作的 Web API 2 控制器**]。

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

在 [ **新增控制器** ] 對話方塊中，針對 [ **控制器名稱**] 輸入 &quot; BooksController &quot; 。 選取 [ &quot; 使用非同步控制器動作 &quot; ] 核取方塊。 針對 [ **模型類別**]，選取 [ &quot; 書籍] &quot; 。  (如果您沒有看到 `Book` 下拉式清單中列出的類別，請確定您已建立專案。 ) 然後按一下 [+] 按鈕。

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

按一下 [**新增資料內容**] 對話方塊中的 [**加入**]。

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

按一下 [**新增控制器**] 對話方塊中的 [**新增**]。 此樣板會新增名為 `BooksController` 的類別，該類別會定義 API 控制器。 它也會在 [模型] 資料夾中加入名為的類別 `BooksAPIContext` ，該類別會定義 Entity Framework 的資料內容。

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a>植入資料庫

從 [工具] 功能表選取 [ **NuGet 封裝管理員**]，然後選取 **封裝管理員主控台**。

在 [Package Manager Console] 視窗中，輸入下列命令：

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

此命令會建立一個 [遷移] 資料夾，並新增名為 Configuration.cs 的新程式碼檔案。 開啟此檔案，並將下列程式碼加入至 `Configuration.Seed` 方法。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

在封裝管理員主控台] 視窗中，輸入下列命令。

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

這些命令會建立本機資料庫，並叫用種子方法來填入資料庫。

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a>新增 DTO 類別

如果您現在執行應用程式，並將 GET 要求傳送至/api/books/1，回應看起來會像下面這樣。  (我新增了縮排，以提供可讀性。 ) 

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

相反地，我希望此要求傳回欄位的子集。 此外，我希望它傳回作者的姓名，而不是作者識別碼。 為了達成此目的，我們將修改控制器方法，以 *傳回資料傳輸物件* (DTO) 而非 EF 模型。 DTO 是專為攜帶資料而設計的物件。

在方案總管中，以滑鼠右鍵按一下專案，**然後選取 [**  |  **新增資料夾**]。 將資料夾命名為 &quot; dto &quot; 。 `BookDto`使用下列定義，將名為的類別新增至 dto 資料夾：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

新增另一個名為 `BookDetailDto`的類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

接下來，更新 `BooksController` 類別以傳回 `BookDto` 實例。 我們將使用可 [查詢的. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 方法將 `Book` 實例投影至 `BookDto` 實例。 以下是控制器類別的更新程式碼。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> 我刪除了 `PutBook` 、 `PostBook` 和 `DeleteBook` 方法，因為本教學課程不需要它們。

現在，如果您執行應用程式並要求/api/books/1，回應主體看起來應該像這樣：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a>新增路由屬性

接下來，我們會將控制器轉換成使用屬性路由。 首先，將 **RoutePrefix** 屬性新增至控制器。 這個屬性會定義此控制器上所有方法的初始 URI 區段。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

然後，將 **[Route]** 屬性新增至控制器動作，如下所示：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

每個控制器方法的路由範本都是前置詞加上 **route** 屬性中所指定的字串。 如果是 `GetBook` 方法，路由範本會包含參數化的字串 &quot; {id： int} &quot; ，如果 URI 區段包含整數值，則會相符。

| 方法 | 路由範本 | 範例 URI |
| --- | --- | --- |
| `GetBooks` | 「api/書籍」 | `http://localhost/api/books` |
| `GetBook` | "api/書籍/{id： int}" | `http://localhost/api/books/5` |

## <a name="get-book-details"></a>取得書籍詳細資料

為了取得書籍詳細資料，用戶端會將 GET 要求傳送至 `/api/books/{id}/details` ，其中 *{id}* 是書籍的識別碼。

將下列方法新增至 `BooksController` 類別。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

如果您要求 `/api/books/1/details` ，回應看起來像這樣：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a>依內容類型取得書籍

若要取得特定類型的書籍清單，用戶端會將 GET 要求傳送至，其中內容類型是內容類型的 `/api/books/genre` 名稱。 *genre* (例如，`/api/books/fantasy`)。

將下列方法新增至 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

在這裡，我們會在 URI 範本中定義包含 {類型} 參數的路由。 請注意，Web API 可以區分這兩個 Uri，並將其路由傳送至不同的方法：

`/api/books/1`

`/api/books/fantasy`

這是因為 `GetBook` 方法包含「識別碼」區段必須是整數值的條件約束：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

如果您要求/api/books/fantasy，回應看起來會像這樣：

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a>依作者取得書籍

為了取得特定作者的書籍清單，用戶端會將 GET 要求傳送至 `/api/authors/id/books` ，其中 *id* 是作者的識別碼。

將下列方法新增至 `BooksController` 。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

這個範例很有趣，因為 &quot; 書籍 &quot; 會被視為作者的子資源 &quot; &quot; 。 此模式在 RESTful Api 中相當常見。

路由範本中的波浪線 (~) 會覆寫 **RoutePrefix** 屬性中的路由前置詞。

## <a name="get-books-by-publication-date"></a>依發行日期取得書籍

若要依發行日期取得書籍清單，用戶端會將 GET 要求傳送至 `/api/books/date/yyyy-mm-dd` ，其中 *yyyy mm* 為日期。

以下是執行這項作業的一種方式：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

`{pubdate:datetime}`參數限制為符合**日期時間**值。 這是可行的，但其實比我們想要的還寬鬆。 例如，這些 Uri 也會與路由相符：

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

允許這些 Uri 沒有任何問題。 不過，您可以將正則運算式條件約束新增至路由範本，以限制特定格式的路由：

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

現在只有格式為 yyyy-mm-dd 的日期才 &quot; &quot; 會相符。 請注意，我們不會使用 RegEx 來驗證我們是否有實際的日期。 當 Web API 嘗試將 URI 區段轉換成 **DateTime** 實例時，便會進行處理。 不正確日期，例如 ' 2012-47-99 ' 將無法轉換，而且用戶端會收到404錯誤。

您也可以 `/api/books/date/yyyy/mm/dd` 使用不同的 RegEx 來新增另一個 **[Route]** 屬性，以支援 () 的斜線分隔符號。

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

這裡有一個很微妙但很重要的詳細資料。 第二個路由範本在 \* {pubdate} 參數的開頭有萬用字元字元 () ：

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

這會告訴路由引擎 {pubdate} 應該符合 URI 的其餘部分。 範本參數預設會符合單一 URI 區段。 在此情況下，我們希望 {pubdate} 跨越數個 URI 區段：

`/api/books/date/2013/06/17`

## <a name="controller-code"></a>控制器程式碼

以下是 BooksController 類別的完整程式碼。

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a>總結

當您設計 API 的 Uri 時，屬性路由可提供更多的控制權和更大的彈性。
