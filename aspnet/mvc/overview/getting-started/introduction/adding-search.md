---
uid: mvc/overview/getting-started/introduction/adding-search
title: 搜尋 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: be4e4d13e574b0fcb77d2d0fb8c6f58041b1ece2
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044838"
---
# <a name="search"></a>搜尋

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="adding-a-search-method-and-search-view"></a>新增搜尋方法和搜尋視圖

在本節中，您會將搜尋功能新增至 `Index` 動作方法，讓您依據內容類型或名稱來搜尋電影。

## <a name="prerequisites"></a>先決條件

若要比對此區段的螢幕擷取畫面，您必須 (F5) 執行應用程式，並將下列電影新增至資料庫。

| 標題 | 發行日期 | Genre | 價格 |
| ----- | ------------ | ----- | ----- |
| Ghostbusters | 6/8/1984 | 喜劇 | 6.99 |
| Ghostbusters II | 6/16/1989 | 喜劇 | 6.99 |
| Apes 的地球 | 3/27/1986 | 動作 | 5.99 |

## <a name="updating-the-index-form"></a>更新索引表單

首先，將 `Index` 動作方法更新為現有的 `MoviesController` 類別。 此程式碼如下：

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

方法的第一行會 `Index` 建立下列 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 查詢來選取電影：

[!code-csharp[Main](adding-search/samples/sample2.cs)]

此查詢已在此時定義，但尚未針對資料庫執行。

如果 `searchString` 參數包含字串，則會使用下列程式碼修改電影查詢來篩選搜尋字串的值：

[!code-csharp[Main](adding-search/samples/sample3.cs)]

上述 `s => s.Title` 程式碼是 [Lambda 運算式](https://msdn.microsoft.com/library/bb397687.aspx)。 在以方法為基礎的 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) 查詢中，lambda 會用來作為標準查詢運算子方法的引數，例如在上述程式碼中使用的 [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) 方法。 當 LINQ 查詢定義時，或藉由呼叫方法（例如或）進行修改時，不會執行 LINQ 查詢 `Where` `OrderBy` 。 相反地，查詢執行會延後，這表示運算式的評估會延遲，直到實際反覆運算其實現值或 [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) 呼叫方法為止。 在此 `Search` 範例中，查詢會在 *Index. cshtml* 視圖中執行。 如需延後查詢執行的詳細資訊，請參閱[查詢執行](https://msdn.microsoft.com/library/bb738633.aspx)。

> [!NOTE]
> [Contains](https://msdn.microsoft.com/library/bb155125.aspx)方法是在資料庫上執行，而不是上述的 c # 程式碼。 在資料庫上，[包含](https://msdn.microsoft.com/library/bb155125.aspx)[類似 SQL](https://msdn.microsoft.com/library/ms179859.aspx)的對應，它不區分大小寫。

現在您可以更新 `Index` 將向使用者顯示表單的視圖。

執行應用程式，並流覽至 */Movies/Index*。 將查詢字串 (例如 `?searchString=ghost`) 附加至 URL。 隨即顯示篩選過的電影。

![SearchQryStr](adding-search/_static/image1.png)

如果您將方法的簽章變更 `Index` 為具有名為的參數 `id` ， `id` 參數將符合 `{id}` *應用程式 \_ Start\RouteConfig.cs* 檔中所設定之預設路由的預留位置。

[!code-json[Main](adding-search/samples/sample4.txt)]

原始的 `Index` 方法如下所示：

[!code-csharp[Main](adding-search/samples/sample5.cs)]

修改後的 `Index` 方法看起來會像這樣：

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

您現在可以將搜尋標題作為路由資料 (URL 區段) 傳遞，而不是作為查詢字串值。

![](adding-search/_static/image2.png)

但是，您不能期望使用者在每次想要搜尋電影時修改 URL。 因此，現在您將新增可協助他們篩選電影的 UI。 如果您變更方法的簽章 `Index` 以測試如何傳遞路由系結識別碼參數，請將其變更回，讓您的 `Index` 方法接受名為的字串參數 `searchString` ：

[!code-csharp[Main](adding-search/samples/sample7.cs)]

開啟 *Views\Movies\Index.cshtml* 檔案，並在之後 `@Html.ActionLink("Create New", "Create")` 新增下列反白顯示的表單標記：

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

`Html.BeginForm`Helper 會建立開頭 `<form>` 標記。 `Html.BeginForm`當使用者按一下 [**篩選**] 按鈕來提交表單時，helper 會讓表單張貼至本身。

在顯示和編輯檢視檔案時，Visual Studio 2013 會有很好的改進。 當您執行應用程式並開啟 view 檔案時，Visual Studio 2013 會叫用正確的控制器動作方法來顯示視圖。

![](adding-search/_static/image3.png)

在 Visual Studio 中開啟索引視圖， (如上圖所示) 中，請按一下 Ctr F5 或 F5 來執行應用程式，然後嘗試搜尋電影。

![](adding-search/_static/image4.png)

沒有方法的多載 `HttpPost` `Index` 。 您不需要它，因為方法不會變更應用程式的狀態，而只是篩選資料。

您可以新增下列 `HttpPost Index` 方法。 在此情況下，動作啟動程式會符合 `HttpPost Index` 方法，而 `HttpPost Index` 方法會如下圖所示執行。

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

不過，即使您新增這個 `HttpPost` 版本的 `Index` 方法，在如何全部實作此方法方面仍然有其限制。 假設您想要將特定的搜尋加為書籤，或者想要傳送連結給朋友，讓他們可以點選來查看相同的電影篩選清單。 請注意，HTTP POST 要求的 URL 與 GET 要求的 URL 相同 (localhost： xxxxx/電影/Index) --URL 本身沒有搜尋資訊。 現在，搜尋字串資訊會以表單欄位值的形式傳送至伺服器。 這表示您無法在 URL 中捕獲該搜尋資訊以將其加入書簽或傳送給朋友。

解決方案是使用的多載 `BeginForm` ，指定 POST 要求應將搜尋資訊新增至 URL，而且應該將它路由傳送至 `HttpGet` 方法的版本 `Index` 。 以下列標記取代現有的無參數 `BeginForm` 方法：

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

現在當您提交搜尋時，URL 會包含搜尋查詢字串。 即使您有 `HttpPost Index` 方法，搜尋也會移至 `HttpGet Index` 動作方法。

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a>依內容類型新增搜尋

如果您已新增 `HttpPost` 方法的版本 `Index` ，請立即將其刪除。

接下來，您將新增功能，讓使用者依內容類型搜尋電影。 以下列程式碼取代 `Index` 方法：

[!code-csharp[Main](adding-search/samples/sample11.cs)]

此版本的 `Index` 方法會採用額外的參數，亦即 `movieGenre` 。 前幾行程式碼會建立一個 `List` 物件來保存資料庫中的電影內容。

下列程式碼是一種 LINQ 查詢，其會從資料庫中擷取所有的內容類型。

[!code-csharp[Main](adding-search/samples/sample12.cs)]

程式碼會使用 `AddRange` 泛型集合的方法 `List` ，將所有相異的內容加入至清單。  (不含 `Distinct` 修飾詞，就會加入重複的內容，例如，喜劇會在我們的範例) 中加入兩次。 然後，程式碼會將內容清單儲存在 `ViewBag.MovieGenre` 物件中。 將類別目錄資料 (這類電影內容) 做為中的 [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) 物件 `ViewBag` ，然後在下拉式清單方塊中存取類別資料是 MVC 應用程式的一般方法。

下列程式碼顯示如何檢查 `movieGenre` 參數。 如果不是空的，則程式碼會進一步限制電影查詢，將選取的電影限制為指定的類型。

[!code-csharp[Main](adding-search/samples/sample13.cs)]

如先前所述，在動作方法傳回) 之後，查詢就不會在資料庫上執行，直到電影清單反復查看在視圖中發生的 (為止 `Index` 。

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a>將標記新增至索引視圖，以支援依內容類型搜尋

在 Views\Movies\Index.cshtml 檔案中加入 helper 之前的協助程式 `Html.DropDownList` *Views\Movies\Index.cshtml* `TextBox` 。 完成的標記如下所示：

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

在下列程式碼中：

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

參數 "MovieGenre" 會提供 `DropDownList` helper 在中尋找的索引鍵 `IEnumerable<SelectListItem>` `ViewBag` 。 `ViewBag`已在動作方法中填入：

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

"All" 參數提供選項標籤。 如果您在瀏覽器中檢查該選擇，將會看到其 "value" 屬性是空的。 因為我們的控制器只 `if` 會篩選字串不是 `null` 或空白，所以提交空白值以 `movieGenre` 顯示所有內容。

您也可以設定預設選取的選項。 如果您想要將 "喜劇" 作為預設選項，您可以變更控制器中的程式碼，如下所示：

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

執行應用程式，並流覽至 */Movies/Index*。 依內容類型、電影名稱，以及這兩個準則來嘗試搜尋。

![](adding-search/_static/image8.png)

在本節中，您建立了搜尋動作方法和視圖，讓使用者依電影標題和內容類型進行搜尋。 在下一節中，您將瞭解如何將屬性加入至 `Movie` 模型，以及如何加入會自動建立測試資料庫的初始化運算式。

> [!div class="step-by-step"]
> [上一個](examining-the-edit-methods-and-edit-view.md) 
> [下一步](adding-a-new-field.md)
