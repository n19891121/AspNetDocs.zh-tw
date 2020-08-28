---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 26d1a66cbc022664af14e4dfe4c4b4892d409b95
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045165"
---
# <a name="accessing-your-models-data-from-a-controller"></a>從控制器存取模型資料

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本節中，您將建立新的 `MoviesController` 類別，並撰寫程式碼以抓取電影資料，並使用 view 範本在瀏覽器中顯示該資料。

請先**建立應用程式**，再繼續進行下一個步驟。 如果您未建立應用程式，您將會在新增控制器時發生錯誤。

在方案總管中，以滑鼠右鍵按一下 [ *控制器* ] 資料夾，然後按一下 [ **新增**]，然後按一下 [ **控制器**]。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

在 [ **新增 Scaffold** ] 對話方塊中，按一下 [ **具有 views 的 MVC 5 控制器]，使用 Entity Framework**]，然後按一下 [ **新增**]。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 選取 [ **Movie (MvcMovie ** ] 模型類別的 [) 模型]。
- 針對資料內容類別選取 **MovieDBCoNtext (MvcMovie) ** 。
- 在 [控制器名稱] 中輸入 **moviescontroller.cs**。

  下圖顯示已完成的對話方塊。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

按一下 [新增] 。  (如果您收到錯誤，可能是您在開始新增控制器之前未建立應用程式。 ) Visual Studio 會建立下列檔案和資料夾：

- [*控制器*] 資料夾中*的 MoviesController.cs*檔案。
- *Views\Movies*資料夾。
- 在新的*Views\Movies*資料夾中，*建立 cshtml、Delete、cshtml、Details*、. cshtml 和*Index. cshtml* 。

Visual Studio 自動建立 [crud](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (為您建立、讀取、更新和刪除) 動作方法和視圖 (自動建立 crud 動作方法和視圖，稱為「樣板) 」。 您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。

執行應用程式，並按一下 [ **MVC 電影** ] 連結 (或在 `Movies` 瀏覽器的網址列中，將 */Movies* 附加至 URL，以流覽至控制器) 。 由於應用程式是依賴 *應用程式 \_ Start\RouteConfig.cs* 檔中定義的預設路由 () ，因此瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至控制器的預設 `Index` 動作方法 `Movies` 。 換句話說，瀏覽器要求實際上與 `http://localhost:xxxxx/Movies` 瀏覽器要求相同 `http://localhost:xxxxx/Movies/Index` 。 結果是空的電影清單，因為您還沒有加入。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>建立電影

選取 **Create New** 連結。 輸入影片的一些詳細資料，然後按一下 [ **建立** ] 按鈕。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 您可能無法在 [價格] 欄位中輸入小數點或逗點。 若要支援使用逗號 (的非英文地區設定的 jQuery 驗證 &quot; 、 &quot;) 用於小數點和非英文日期格式的非英文地區設定，您必須包含 *globalize.js* 和您的特定 *文化特性/globalize.cultures.js* 檔案 (從 [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 和 JavaScript 使用 `Globalize.parseFloat` 。 我將在下一個教學課程中示範如何進行這項作業。 現在，只要輸入如 10 之類的整數。

按一下 [ **建立** ] 按鈕，會將表單張貼至伺服器，並在其中將電影資訊儲存在資料庫中。 然後，系統會將您重新導向至 */Movies* URL，您可以在清單中看到新建立的電影。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

建立幾個電影項目。 嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。

## <a name="examining-the-generated-code"></a>檢查產生的程式碼

開啟 *Controllers\MoviesController.cs* 檔案，並檢查產生的 `Index` 方法。 具有方法的影片控制器部分 `Index` 如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

對控制器的要求會 `Movies` 傳回資料表中的所有專案 `Movies` ，然後將結果傳遞給 `Index` 視圖。 類別中的下列程式列會具現 `MoviesController` 化 movie 資料庫內容，如先前所述。 您可以使用 movie 資料庫內容來查詢、編輯和刪除電影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>強型別模型和 @model 關鍵字

稍早在本教學課程中，您已看到控制器如何使用物件將資料或物件傳遞至 view 範本 `ViewBag` 。 `ViewBag`是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。

MVC 也提供將 *強* 型別物件傳遞至 view 範本的能力。 這種強型別方法可讓您在 Visual Studio 編輯器中更妥善的編譯時間檢查程式碼和更豐富的 [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 。 Visual Studio 中的樣板機制使用這種方法， (也就是在建立方法和瀏覽器時，將 *強* 型別模型) 與 `MoviesController` 類別和視圖範本一起傳遞。

在 *Controllers\MoviesController.cs* 檔案中檢查產生的 `Details` 方法。 `Details`方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`參數通常會以路由資料的形式傳遞，例如， `http://localhost:1234/movies/details/1` 會將控制器設定為電影控制器、將動作設定為，並將設定為 `details` `id` 1。 您也可以使用查詢字串傳入識別碼，如下所示：

`http://localhost:1234/movies/details?id=1`

如果找到，則會將 `Movie` 模型的實例 `Movie` 傳遞至 `Details` 視圖：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

檢查 *Views\Movies\Details.cshtml* 檔案的內容：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

藉由在「 `@model` 視圖」範本檔案的頂端加入語句，您可以指定該視圖預期的物件類型。 當您建立電影控制器時，Visual Studio 會在 *Details.cshtml* 檔案的最上方自動包含下列 `@model` 陳述式：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

這個 `@model` 指示詞可讓您使用強型別的 `Model` 物件，存取控制器傳遞至檢視的電影。 例如，在 [ *詳細資料* ] 範例中，程式碼會將每個 movie 欄位傳遞至 `DisplayNameFor` ，並使用強型別物件 [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML helper `Model` 。 `Create`和 `Edit` 方法和 view 範本也會傳遞 movie 模型物件。

檢查 MoviesController.cs 檔案中的*Index. cshtml* view 範本和 `Index` 方法*MoviesController.cs* 。 請注意程式碼在 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) `View` 動作方法中呼叫 helper 方法時，如何建立物件 `Index` 。 然後，程式碼會將此 `Movies` 清單從 `Index` 動作方法傳遞至視圖：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

當您建立電影控制器時，Visual Studio 會自動將下列 `@model` 語句包含在 *Index. cshtml* 檔案的頂端：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

這個指示 `@model` 詞可讓您使用強型別的物件，存取控制器傳遞給視圖的電影清單 `Model` 。 例如，在 *Index. cshtml* 範本中，程式碼會藉由對強型別物件執行語句，以迴圈播放影片 `foreach` `Model` ：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

因為 `Model` 物件是強型別 (為 `IEnumerable<Movie>` 物件) ，所以 `item` 迴圈中的每個物件都會輸入為 `Movie` 。 除了其他優點之外，這表示您可以在程式碼編輯器中取得程式碼和完整 IntelliSense 支援的編譯時期檢查：

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

Entity Framework Code First 偵測到提供的資料庫連接字串已指向 `Movies` 尚未存在的資料庫，所以 Code First 自動建立資料庫。 您可以藉由查看 *應用程式 \_ 資料* 資料夾來確認它是否已建立。 如果看不到 *.mdf*檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開 [*應用程式 \_ 資料*] 資料夾。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

按兩下 [ *.Mdf* ] 以開啟 [ **伺服器瀏覽器**]，然後展開 [ **資料表]** 資料夾以查看 [電影] 資料表。 請注意 [識別碼] 旁邊的按鍵圖示。 根據預設，EF 會將名為 ID 的屬性設為主鍵。 如需 EF 和 MVC 的詳細資訊，請參閱 Tom Dykstra 在 [MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)上的絕佳教學課程。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

以滑鼠右鍵按一下 `Movies` 資料表，然後選取 [ **顯示資料表資料** ] 以查看您所建立的資料。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

以滑鼠右鍵按一下 `Movies` 資料表，然後選取 [ **開啟資料表定義** ]，以查看 Entity Framework Code First 為您建立的資料表結構。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

請注意資料表的架構如何 `Movies` 對應至您稍 `Movie` 早建立的類別。 Entity Framework Code First 會根據您的類別自動建立此架構 `Movie` 。

當您完成時，請以滑鼠右鍵按一下 [ *MovieDBCoNtext* ] 並選取 [ **關閉連接**] 來關閉連接。  (如果您未關閉連線，下次執行專案時，可能會收到錯誤) 。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

您現在擁有一個資料庫和多個頁面，可用來顯示、編輯、更新和刪除資料。 在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` `SearchIndex` 可讓您在此資料庫中搜尋電影的方法和觀點。 如需搭配 MVC 使用 Entity Framework 的詳細資訊，請參閱為 [ASP.NET MVC 應用程式建立 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

> [!div class="step-by-step"]
> [上一個](creating-a-connection-string.md) 
> [下一步](examining-the-edit-methods-and-edit-view.md)
