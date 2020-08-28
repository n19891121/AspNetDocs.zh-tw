---
title: 將視圖新增至 MVC 應用程式
author: Rick-Anderson
description: 將視圖新增至 MVC 應用程式
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: b8400036cc689d3cd2fec54b3191252d296ade41
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045009"
---
# <a name="adding-a-view"></a>新增檢視

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在這一節中，您將修改 `HelloWorldController` 類別以使用「查看範本」檔案，將產生 HTML 回應的程式完全封裝到用戶端。 

您將使用 [Razor view 引擎](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)來建立 view 範本檔案。 Razor 型視圖範本的副檔名為 *cshtml* ，並提供使用 c # 建立 HTML 輸出的簡潔方式。 Razor 可將撰寫視圖範本時所需的字元數和按鍵次數降到最低，並啟用快速、流暢的編碼工作流程。

目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。 將 `Index` 方法變更為呼叫控制器 [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) 方法，如下列程式碼所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

`Index`上述方法會使用 view 範本來產生瀏覽器的 HTML 回應。 控制器方法 (也稱為 [動作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)) （例如 `Index` 上述方法）通常會傳回 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (或衍生自 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)) 的類別，而不是字串之類的基本類型。

以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，然後按一下 [ **新增**]，再按一下 [ **具有版面配置的 MVC 5 視圖頁面] (Razor) **。
  
![](adding-a-view/_static/image1.png)   
  
在 [ **指定專案的名稱** ] 對話方塊中，輸入 [ *索引*]，然後按一下 **[確定]**。  
  
![](adding-a-view/_static/image2.png)  
  
在 [**選取版面配置頁面**] 對話方塊中，接受預設的** \_ Layout** ，然後按一下 **[確定]**。  
  
![](adding-a-view/_static/image3.png)  
  
在上圖中，已選取左窗格中的 [ *Views\Shared* ] 資料夾。 如果您在另一個資料夾中有自訂的版面配置檔案，您可以選取它。 我們稍後會在本教學課程中討論版面配置檔案

*MvcMovie\Views\HelloWorld\Index.cshtml*檔案會建立。

![](adding-a-view/_static/image4.png)

新增下列反白顯示的標記。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

以滑鼠右鍵按一下 [ *Index* ]，然後 **在 [瀏覽器] 中**選取 [View]。

![PI](adding-a-view/_static/image5.png)

您也可以用滑鼠右鍵按一下 [*索引*]，然後選取**Page Inspector 中**的 [View]。 如需詳細資訊，請參閱 [Page Inspector 教學](../../views/using-page-inspector-in-aspnet-mvc.md) 課程。

或者，執行應用程式並流覽至 `HelloWorld` 控制器 (`http://localhost:xxxx/HelloWorld`) 。 `Index`您控制器中的方法不會執行太多工作，而只是執行語句 `return View()` ，這會指定方法應該使用 view 範本檔案來呈現瀏覽器的回應。 因為您未明確指定要使用的視圖範本檔案名，ASP.NET MVC 預設為使用 \Views\HelloWorld 資料夾中的*\Views\HelloWorld*資料夾中的*Index. cshtml* view 檔案。 下圖顯示 &quot; 來自我們的視圖範本的字串 Hello！ &quot; 在視圖中進行硬式編碼。

![](adding-a-view/_static/image6.png)

看起來不錯。 不過請注意，瀏覽器的標題列會顯示「索引-我的 ASP.NET 應用程式」，而頁面頂端的大連結則顯示「應用程式名稱」。 根據您瀏覽器視窗的大小，您可能需要按一下右上方的三個橫條，才能看到 **首頁**、 **About**、 **Contact**、 **Register** 和 **登入** 連結。

## <a name="changing-views-and-layout-pages"></a>變更視圖和版面配置頁面

首先，您想要變更 &quot; 頁面頂端的應用程式名稱 &quot; 連結。 該文字在每個頁面中都是通用的。 它其實只會在專案中的一個位置進行，即使它出現在應用程式的每個頁面上也一樣。 移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 [配置檔] * \_ 。* 這個檔案稱為版面配置 *頁面* ，它位於所有其他頁面使用的共用資料夾中。

![_LayoutCshtml](adding-a-view/_static/image7.png)

版面配置範本可讓您在某個位置指定網站的 HTML 容器配置，然後將它套用到網站中的多個頁面。 找到 `@RenderBody()` 這行。 `RenderBody` 是顯示您建立之所有檢視特定頁面的預留位置，「包裝」&quot;&quot;在版面配置頁中。 例如，如果您選取 [ **關於** ] 連結，則會在方法內轉譯 *Views\Home\About.cshtml* view `RenderBody` 。

變更標題元素的內容。 將版面配置 [範本中的](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) [從 &quot; 應用程式名稱] 變更 &quot; 為 [ &quot; MVC 電影] &quot; ，並將控制器從變更 `Home` 為 `Movies` 。 完整的版面配置檔案如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

執行應用程式，並注意它現在會顯示 &quot; MVC 電影 &quot; 。 按一下 [ **關於** ] 連結，您也會看到該頁面如何顯示 &quot; MVC 電影 &quot; 。 我們可以在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。

![](adding-a-view/_static/image8.png)

當我們先建立 *Views\HelloWorld\Index.cshtml* 檔案時，它會包含下列程式碼：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

上述的 Razor 程式碼會明確地設定版面配置頁面。 檢查 *Views \\ _ViewStart cshtml* 檔案，其中包含完全相同的 Razor 標記。 *[Views \\ _ViewStart 的 views](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* 檔案會定義所有視圖都將使用的一般配置，因此您可以將該程式碼從*Views\HelloWorld\Index.cshtml*檔中批註出來或移除。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

您可以使用 `Layout` 屬性來設定不同的版面配置檢視，或將它設定為 `null`，因此不會使用任何版面配置檔案。

現在，讓我們來變更索引視圖的標題。

開啟 *MvcMovie\Views\HelloWorld\Index.cshtml*。 有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後在第二個標頭中 (`<h2>` 元素) 。 您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

為了指出要顯示的 HTML 標題，上述程式碼會設定 `Title` 物件 (的屬性，該 `ViewBag` 物件位於 *Index. cshtml* view 範本) 中。 請注意，配置範本 ( *Views\Shared \\ _Layout. cshtml* ) 會使用專案中的這個值， `<title>` 做為 `<head>` 我們先前修改過之 HTML 區段的一部分。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

使用這 `ViewBag` 種方法，您可以輕鬆地在您的視圖範本和版面配置檔案之間傳遞其他參數。

執行應用程式。 請注意，瀏覽器標題、主要標題和次要標題已變更 (如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。 在您的瀏覽器中按 Ctrl + F5，以強制載入來自伺服器的回應。 ) 瀏覽器標題是以 `ViewBag.Title` 我們在*Index. cshtml* view 範本中所設定的，以及在版面配置檔案 &quot; 中新增的其他電影應用程式所建立。 &quot;

另外也請注意， *Index. cshtml* view 範本中的內容如何與* \_ Layout* view 範本合併，並將單一 HTML 回應傳送至瀏覽器。 版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。

![](adding-a-view/_static/image9.png)

&quot;這就是我們的一些資料 &quot; (在此情況下 &quot; ，我們的視圖範本的 Hello！ &quot; message) 是硬式編碼的。 MVC 應用程式有一個 &quot; V &quot; (view) 而且您有 &quot; C &quot; (控制器) ，但是沒有任何 &quot; M &quot; (模型) 。 不久之後，我們將逐步解說如何建立資料庫，並從中取出模型資料。

## <a name="passing-data-from-the-controller-to-the-view"></a>將資料從控制器傳遞至檢視

在我們移至資料庫並討論模型之前，讓我們先討論如何從控制器將資訊傳遞給視圖。 系統會叫用控制器類別以回應傳入的 URL 要求。 控制器類別可讓您撰寫程式碼來處理傳入瀏覽器要求、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。 然後，您可以從控制器使用 View 範本，以產生並格式化瀏覽器的 HTML 回應。

控制器會負責提供所需的資料或物件，讓「視圖」範本能夠呈現瀏覽器的回應。 最佳做法：「 **視圖」範本永遠不應該執行商務邏輯，或直接與資料庫互動**。 相反地，「視圖」範本應該只適用于控制器提供給它的資料。 維護這 &quot; 項考慮會 &quot; 讓您的程式碼保持乾淨、可測試且更容易維護。

目前， `Welcome` 類別中的動作方法 `HelloWorldController` 會接受 `name` 和參數，然後將 `numTimes` 值直接輸出至瀏覽器。 讓控制器改為使用 view 範本，而不是讓控制器將此回應轉譯為字串。 檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。 若要這麼做，您可以讓控制器將動態資料放 (參數，) 視圖範本在可存取的物件中所需的資料 `ViewBag` 。

返回 *HelloWorldController.cs* 檔案並變更 `Welcome` 方法，以將 `Message` 和值加入 `NumTimes` 至 `ViewBag` 物件。 `ViewBag` 是動態物件，這表示您可以在其中放置任何您想要的內容; `ViewBag` 除非您將某個內容放在其中，否則物件沒有定義的屬性。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將 (和) 的具名引數， `name` `numTimes` 從網址列中的查詢字串對應到您方法中的參數。 完整的 *HelloWorldController.cs* 檔案如下所示：

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

現在 `ViewBag` 物件包含將會自動傳遞給視圖的資料。 接下來，您需要一個歡迎使用的視圖範本！ 在 [ **組建** ] 功能表中，選取 [ **組建方案** (] 或 [Ctrl + Shift + B]) 以確定專案已編譯。 以滑鼠右鍵按一下 [ *Views\HelloWorld* ] 資料夾，然後按一下 [ **新增**]，再按一下 [ **具有版面配置的 MVC 5 視圖頁面] (Razor) **。
  
![](adding-a-view/_static/image10.png)   
  
在 [ **指定專案的名稱** ] 對話方塊中，輸入 [ *歡迎使用*]，然後按一下 **[確定]**。   
  
在 [**選取版面配置頁面**] 對話方塊中，接受預設的** \_ Layout** ，然後按一下 **[確定]**。  
  
![](adding-a-view/_static/image11.png)   

*MvcMovie\Views\HelloWorld\Welcome.cshtml*檔案會建立。

取代 *歡迎的 cshtml* 檔案中的標記。 您將會建立一個迴圈，並以 &quot; &quot; 使用者指出的次數來顯示 Hello。 完整的 *歡迎* 檔如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

執行應用程式，並流覽至下列 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

現在會從 URL 取得資料，並使用 [模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結器將資料傳遞至控制器。 控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞給視圖。 然後，此視圖會將資料顯示為使用者的 HTML。

![](adding-a-view/_static/image12.png)

在上述範例中，我們使用了 `ViewBag` 物件將資料從控制器傳遞至 view。 稍後在教學課程中，我們將使用檢視模型將控制器中的資料傳遞至檢視。 傳遞資料的視圖模型方法通常比查看包方法更慣用。 如需詳細資訊，請參閱 blog 專案 [動態型強](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 型別查看。 

這是 &quot; 模型的 M 類型 &quot; ，但不是資料庫種類。 讓我們運用所學的內容，建立電影的資料庫。

> [!div class="step-by-step"]
> [上一個](adding-a-controller.md) 
> [下一步](adding-a-model.md)
