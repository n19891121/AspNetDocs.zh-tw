---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: ae3258872df798f52d8e031dc8ebf01b4f0a7358
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045126"
---
# <a name="adding-a-controller"></a>新增控制器

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

MVC 代表 *模型-視圖控制器*。 MVC 是一種模式，用來開發妥善架構、可測試且容易維護的應用程式。 以 MVC 為基礎的應用程式包含：

- **M** ) ：代表應用程式資料的類別，以及使用驗證邏輯來強制執行該資料之商務規則的類別。
- **V** >v) ：您的應用程式用來動態產生 HTML 回應的範本檔案。
- **C** ) ：處理傳入瀏覽器要求的類別、取出模型資料，然後指定將回應傳回給瀏覽器的視圖範本。

我們將在本教學課程系列中涵蓋這些概念，並示範如何使用它們來建立應用程式。

讓我們從建立控制器類別開始。 在 **方案總管**中，以滑鼠右鍵按一下 [ *控制器* ] 資料夾，然後按一下 [ **新增**]，然後按一下 [ **控制器**]。

![](adding-a-controller/_static/image1.png)

在 [ **新增 Scaffold** ] 對話方塊中，按一下 [ **MVC 5 控制器-空白**]，然後按一下 [ **新增**]。

![](adding-a-controller/_static/image2.png)  

將新控制器命名為 ">helloworldcontroller.cs"，然後按一下 [ **新增**]。

![新增控制器](adding-a-controller/_static/image3.png)

請注意， **方案總管** 已建立名為 *HelloWorldController.cs* 的新檔案和新的資料夾 *Views\HelloWorld*。 控制器已在 IDE 中開啟。

![](adding-a-controller/_static/image4.png)

以下列程式碼取代檔案的內容。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法會傳回 HTML 字串作為範例。 控制器命名為 `HelloWorldController` ，第一個方法名為 `Index` 。 讓我們從瀏覽器叫用它。 執行應用程式 (按 F5 或 Ctrl + F5) 。 在瀏覽器中，將 &quot; HelloWorld 附加 &quot; 至網址列中的路徑。  (例如，在下圖中， `http://localhost:1234/HelloWorld.`) 瀏覽器中的頁面看起來會像下列螢幕擷取畫面。 在上述方法中，程式碼會直接傳回字串。 您已告訴系統只傳回一些 HTML，而且的確是！

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別 (以及它們內的不同動作方法) 。 ASP.NET MVC 使用的預設 URL 路由邏輯會使用如下的格式來判斷要叫用的程式碼：

`/[Controller]/[ActionName]/[Parameters]`

您可以在 *應用程式 \_ 啟動/>start\routeconfig.cs .cs* 檔案中設定路由的格式。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

當您執行應用程式但未提供任何 URL 區段時，它會預設為在上述程式碼的 [預設值] 區段中指定的 "Home" 控制器和 "Index" 動作方法。

URL 的第一個部分會決定要執行的控制器類別。 因此， */HelloWorld* 會對應到 `HelloWorldController` 類別。 URL 的第二個部分會決定要執行之類別上的動作方法。 因此， */HelloWorld/Index* 會讓 `Index` 類別的方法 `HelloWorldController` 執行。 請注意，我們只需要流覽至 */HelloWorld* ，而且 `Index` 預設會使用方法。 這是因為名為的方法 `Index` 是預設方法，如果未明確指定，就會在控制器上呼叫它。 URL 區段的第三個部分 (`Parameters`) 是路由資料。 我們稍後會在本教學課程中看到路由資料。

瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome`方法會執行並傳回字串， &quot; 此為歡迎動作方法 ... &quot; 。 預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]` 。 在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。 您尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image6.png)

讓我們稍微修改範例，讓您可以將 URL 中的一些參數資訊傳遞給控制器 (例如， */HelloWorld/Welcome？ name = Scott &amp; numtimes is = 4*) 。 變更您的 `Welcome` 方法以包含兩個參數，如下所示。 請注意，程式碼會使用 c # 選擇性參數功能，指出 `numTimes` 如果沒有針對該參數傳遞任何值，參數應該預設為1。

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> 安全性注意事項：上述程式碼會使用 [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) 來保護應用程式免于遭受惡意輸入 (亦即 JavaScript) 。 如需詳細資訊，請參閱 [如何：將 HTML 編碼套用至字串，以防止 Web 應用程式中的腳本](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)惡意探索。

 執行您的應用程式，並流覽至範例 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`) 。 您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。 [ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會將指定的參數從網址列中的查詢字串，自動對應到您方法中的參數。

![](adding-a-controller/_static/image7.png)

在上述範例中， `Parameters` 不會使用 URL 區段 () ， `name` 而且會將和 `numTimes` 參數當做 [查詢字串](http://en.wikipedia.org/wiki/Query_string)傳遞。 ？ 上述 URL 中的 (問號) 是分隔符號，而查詢字串接下來。 &amp; 字元可分隔查詢字串。

以下列程式碼取代歡迎方法：

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

執行應用程式，並輸入下列 URL： `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

這一次，第三個 URL 區段符合路由參數， `ID.` `Welcome` 動作方法包含的參數 (`ID`) 符合方法中的 URL 規格 `RegisterRoutes` 。

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

在 ASP.NET MVC 應用程式中，以路由資料的形式傳遞參數更為常見， (像我們在) 以上的識別碼，而不是將它們當作查詢字串傳遞。 您也可以新增路由，以將 `name` 和 `numtimes` in 參數傳遞為 URL 中的路由資料。 在 *應用程式 \_ Start\RouteConfig.cs* 檔中，新增 "Hello" 路由：

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

執行應用程式，並流覽至 `/localhost:XXX/HelloWorld/Welcome/Scott/3` 。

![](adding-a-controller/_static/image9.png)

對於許多 MVC 應用程式來說，預設路由會正常運作。 您稍後會在本教學課程中瞭解如何使用模型系結器來傳遞資料，而您不需要修改該的預設路由。

在這些範例中，控制器已執行 &quot; MVC 的 VC &quot; 部分（也就是，view 和 controller 工作）。 控制器會直接傳回 HTML。 一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。 相反地，我們通常會使用個別的 view 範本檔案來協助產生 HTML 回應。 接下來讓我們來看看如何進行。

> [!div class="step-by-step"]
> [上一個](getting-started.md) 
> [下一步](adding-a-view.md)
