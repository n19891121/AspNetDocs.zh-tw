---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介紹ASP.NET網頁 - HTML表單基礎知識 |微軟文件
author: Rick-Anderson
description: 本教程介紹如何創建輸入表單以及使用ASP.NET網頁 (Razor) 時如何處理使用者輸入的基礎知識。 現在你...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676325"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>介紹ASP.NET網頁 - HTML表單基礎知識

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程介紹如何創建輸入表單以及使用ASP.NET網頁 (Razor) 時如何處理使用者輸入的基礎知識。 現在您已經有了一個資料庫,您將使用表單技能讓用戶在資料庫中尋找特定影片。 它假定您已經通過[介紹使用ASP.NET網頁顯示數據](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成了該系列。
> 
> 您將學到什麼：
> 
> - 如何使用標準 HTML 元素建立表單。
> - 如何讀取表單中的使用者輸入。
> - 如何創建 SQL 查詢,該查詢通過使用使用者提供的搜索詞選擇性地獲取數據。
> - 如何在頁面中「記住」使用者輸入的內容。
>   
> 
> 討論的功能/技術:
> 
> - `Request` 物件。
> - SQL`Where`子句。

## <a name="what-youll-build"></a>您要建置的內容

在前面的教程中,您創建了一個資料庫,向它添加了數據,然後使用`WebGrid`幫助器來顯示數據。 在本教學中,您將添加一個搜尋框,允許您查找特定流派的電影或其標題包含您輸入的任何單詞。 (例如,您可以查找所有類型為"行動"或標題包含"Harry"或"冒險"的電影。

完成本教學後,您將有一個像這樣的頁面:

![引入流派與標題搜尋的電影頁面](form-basics/_static/image1.png)

頁面的清單部分與上一教程&mdash;中網格相同。 區別在於網格將僅顯示您搜索的電影。

## <a name="about-html-forms"></a>關於 HTML 表單

(如果您在創建 HTML 窗體方面擁有經驗,並且`GET``POST`具有和之間的差異,則可以跳過此部分。

表單選使用者輸入元素&mdash;文字框、按鈕、單選按鈕、複選框、下拉清單等。 使用者填寫這些控制項或進行選擇,然後透過單擊按鈕提交表單。

以下範例說明了表單的基本 HTML 語法:

[!code-html[Main](form-basics/samples/sample1.html)]

當此標籤在頁面中執行時,它將建立一個類似於下圖的簡單窗體:

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

這個`<form>`元素包含要提交的 HTML 元素。 (一個簡單的錯誤是向頁面添加元素,但隨後忘記將它們放入`<form>`元素中。 在這種情況下,不會提交任何內容。該`method`屬性告訴瀏覽器如何提交使用者輸入。 `post`如果在伺服器上執行更新,或者`get`只是從伺服器取得資料,則可以將此設定為

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **取得、POST 與 HTTP 動詞安全**
> 
> HTTP是瀏覽器和伺服器用來交換資訊的協定,其基本操作非常簡單。 瀏覽器僅使用幾個謂詞向伺服器發出請求。 為 Web 編寫代碼時,瞭解這些謂詞以及瀏覽器和伺服器如何使用這些謂詞會很有説明。 遠外最常用的動詞是:
> 
> - `GET`. 瀏覽器使用此謂詞從伺服器獲取內容。 例如,當您在瀏覽器中鍵入 URL 時,瀏覽器將`GET`執行操作 以請求所需的頁面。 如果頁面包含圖形,瀏覽器將執行其他`GET`操作以獲取圖像。 如果`GET`操作必須將資訊傳遞到伺服器,則資訊將作為查詢字串中 URL 的一部分傳遞。
> - `POST`. 瀏覽器發送`POST`請求以提交要在伺服器上添加或更改的數據。 例如,謂`POST`詞用於在資料庫中創建記錄或更改現有記錄。 大多數時候,當您填寫表單並按下提交按鈕時,瀏覽器將執行操作`POST`。 在操作`POST`中,傳遞給伺服器的數據位於頁面正文中。
> 
> 這些謂詞之間的一個重要區別是,操作`GET`不應更改伺服器上的任何內容,或者以稍微抽象的方式將其放在操作中`GET`, 操作不會導致伺服器上的狀態更改。 您可以根據需要多次對`GET`同一資源執行操作,並且這些資源不會更改。 (操作`GET`通常說是"安全的",或者使用技術術語,是*冪*等的。當然,與此相反,每次執行`POST`操作時,請求都會更改伺服器上的內容。
> 
> 兩個例子將有助於說明這一區別。 當您使用必應或 Google 等引擎執行搜尋時,您將填寫包含一個文字框的表單,然後單擊搜尋按鈕。 瀏覽器執行操作`GET`,輸入到框中的值作為 URL 的一部分傳遞。 對這種類型的`GET`窗體使用操作很好,因為搜索操作不會更改伺服器上的任何資源,因此只需獲取資訊。
> 
> 現在考慮在線訂購內容的過程。 您填寫訂單詳細資訊,然後按一下提交按鈕。 此操作將是一個`POST`請求,因為該操作將導致伺服器上的更改,例如新訂單記錄、帳戶資訊的更改,以及許多其他更改。 與`GET`操作不同,您不能重複`POST`請求 - 如果重複請求,則每次重新提交請求時,都會在伺服器上生成新訂單。 (在這種情況下,網站通常會警告您不要多次按一下提交按鈕,或者將禁用提交按鈕,以便您不會意外重新提交表單。
> 
> 在本教學中,您將使用`GET`操作和`POST`操作來處理 HTML 窗體。 我們將在每種情況下解釋為什麼您使用的動詞是合適的。
> 
> (要瞭解有關 HTTP 謂詞的更多資訊,請參閱 W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章。

大多數使用者輸入元素是`<input>`HTML 元素。 它們看起來像`<input type="type" name="name">,`*類型*指示所需使用者輸入控制項的類型。 這些元素是常見的元素:

- 文字盒:`<input type="text">`
- 勾選盒:`<input type="check">`
- 按一個按鈕:`<input type="radio">`
- 按鈕:`<input type="button">`
- 提交按鈕:`<input type="submit">`

您還可以使用`<textarea>`元素 建立多行文字`<select>`框和 元素以建立下拉清單或可滾動清單。 (HTML 表單元素的更多內容,請參考 W3Schools 網站的[HTML 表單和輸入](http://www.w3schools.com/html/html_forms.asp)。

該`name`屬性非常重要,因為名稱是以後獲取元素值的方式,稍後將看到。

有趣的部分是您,頁面開發人員,對使用者輸入所做的操作。 沒有與這些元素關聯的內置行為。 相反,您必須獲取使用者已輸入或選擇的值,並對其進行操作。 這是您將在本教程中學到的。

> [!TIP] 
> 
> **HTML5 與輸入表單**
> 
> 您可能知道,HTML 處於過渡狀態,最新版本 (HTML5) 包括支援使用者輸入資訊的更直觀方式。 例如,在 HTML5 中,您可以告訴頁面您希望使用者輸入日期。 然後,瀏覽器可以自動顯示日曆,而不是要求用戶手動輸入日期。 但是,HTML5 是新的,並非所有瀏覽器都支援 HTML5。
> 
> ASP.NET網頁支援 HTML5 輸入,只要使用者的瀏覽器支援 HTML5 輸入。 有關 HTML5`<input>`中 元素的新屬性的概念,請參閱 W3Schools 網站上的 HTML[&lt;&gt;輸入 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp)。

## <a name="creating-the-form"></a>建立表單

在 WebMatrix 中,在 **「檔**」工作區中,打開 *「電影.cshtml」* 頁面。

在結束`</h1>`標記之後`<div>``grid.GetHtml`和 撥號的開頭標記之前,添加以下標記:

[!code-html[Main](form-basics/samples/sample2.html)]

此標記創建一個表單,該表單具有名為`searchGenre`文本框和提交按鈕。 文字框和提交按鈕包含在其`<form>``method`屬性設置`get`為 的元素中。 (請記住,如果不將文字框和提交按鈕放在`<form>`元素中,則按一下該按鈕時不會提交任何內容。您在此處使用`GET`謂詞是因為您正在創建一個不會在伺服器上進行任何更改的窗體 - 它只是導致搜索。 (在前面的教程中,您使用了一`post`種方法,即向伺服器提交更改的方式。 您將在下一教程中再次看到這一點。

運行頁面。 儘管尚未為表單定義任何行為,但您可以看到它的外觀:

![帶有「流派」搜尋框的影片頁面](form-basics/_static/image3.png)

在文本框中輸入一個值,如"喜劇"。 然後點選**搜尋流派**。

記下頁面的 URL。 由於將`<form>`元素的`method`屬性`get`設定為 ,因此您輸入的值現在是網址中查詢字串的一部分,如下所示:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>讀取表單

該頁已包含一些代碼,這些代碼獲取資料庫數據並在網格中顯示結果。 現在,您必須添加一些讀取文本框值的代碼,以便運行包含搜索詞的 SQL 查詢。

由於將表單的程式設定`get`為 ,因此可以使用以下的程式碼讀取輸入到文字框中的值:

`var searchTerm = Request.QueryString["searchGenre"];`

物件`Request.QueryString``QueryString``Request`(物件的屬性)包括`GET`作為 操作的一部分提交的元素的值。 屬性`Request.QueryString`包含表單中提交的值*的集合*(清單)。 要取得任何單個值,請指定所需的元素的名稱。 這就是為什麼您必須在創建文本框`name``<input>`的元素`searchTerm`( ) 上具有屬性的原因。 ( 有關物件的更多`Request`, 請參考邊[列](#BKMK_TheRequestObject)。

閱讀文本框的值非常簡單。 但是,如果使用者在文本框中根本不輸入任何內容,但無論如何都單擊 **「搜索」,** 則可以忽略該單擊,因為沒有什麼可搜索的。

以下代碼是演示如何實現這些條件的範例。 (您不必添加此代碼,您一會兒就將添加。

[!code-csharp[Main](form-basics/samples/sample3.cs)]

測試以這種方式分解:

- 獲取的值`Request.QueryString["searchGenre"]`,即輸入到`<input>``searchGenre`名為 的元素中的值。
- 使用`IsEmpty`方法瞭解其是否為空。 此方法是確定某些內容(例如表單元素)是否包含值的標準方法。 但實際上,你只關心,如果它*不*是空的,因此...
- 測試`!``IsEmpty`前添加運算子。 (運算符`!`表示邏輯 NOT)。

在純英語中,整個`if`條件轉換為以下內容:*如果表單的 searchGenre 元素不為空,則 ...*

此塊設置創建使用搜索詞的查詢的階段。 您將在下一節中執行該動作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **要求物件**
> 
> 該`Request`物件包含瀏覽器在請求或提交頁面時發送到應用程式的所有資訊。 此物件包括使用者提供的任何資訊,如文本框值或要上傳的檔。 它還包括各種附加資訊,如 Cookie、URL 查詢字串中的值(如果有)、正在運行的頁面的檔路徑、使用者使用的瀏覽器類型、在瀏覽器中設置的語言清單等等。
> 
> 該`Request`對像是值*的集合*(清單)。 以指定單個值的名稱,從集合中取得單個值:
> 
> `var someValue = Request["name"];`
> 
> 該`Request`對象實際上公開了幾個子集。 例如：
> 
> - `Request.Form`如果請求是`POST`請求,則從`<form>`提交 元素中的元素提供值。
> - `Request.QueryString`僅為您提供 URL 查詢字串中的值。 (在網`http://mysite/myapp/page?searchGenre=action&page=2`址中,URL`?searchGenre=action&page=2`的部份是查詢字串。
> - `Request.Cookies`集合允許您訪問瀏覽器發送的 Cookie。
> 
> 要取得您知道在提交的表單的值,可以使用`Request["name"]`。 或者,`Request.Form["name"]`您可以使用更具體的版本(`POST`用於請求)`Request.QueryString["name"]`或`GET`(用於請求)。 當然,*名稱*是要獲取的項的名稱。
> 
> 要獲取的項的名稱必須在要使用的集合中是唯一的。 這就是為什麼`Request`物件提供子集,`Request.Form`如`Request.QueryString`和 。 假設您的頁面包含名為的`userName`表單元素,*並且還*包含名為`userName`的 Cookie。 如果得到`Request["userName"]`,則是模糊的是想要表單值還是 Cookie。 但是,如果您得到`Request.Form["userName"]`或`Request.Cookie["userName"]`,則明確要獲取的值。
> 
> 最好是具體使用您感興趣的子集`Request`,`Request.Form`例如`Request.QueryString`或 。 對於您在本教程中創建的簡單頁面,它可能沒有任何區別。 但是,當您創建更複雜的頁面時,使用顯式版本`Request.Form``Request.QueryString`或 可以説明您避免在頁面包含窗體(或多個窗體)、Cookie、查詢字串值等時可能出現的問題。

## <a name="creating-a-query-by-using-a-search-term"></a>使用搜尋字建立查詢

現在,您已經知道如何獲取使用者輸入的搜索詞,您可以創建使用它的查詢。 請記住,要將所有影片項從資料庫中獲取出來,您使用的是 SQL 查詢,該查詢如下所示:

`SELECT * FROM Movies`

要僅獲取某些影片,必須使用包含子句的`Where`查詢。 此子句允許您設置查詢返回行的條件。 以下是範例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式為`WHERE column = value`。 除了(`=`大`>`於 )、(小於`<`)、( 不等`<>``<=`於)、( 小於或等於)等之外,還可以使用不同的運算符,具體取決於您要查找的內容。

如果您想知道,SQL 語句不是大小寫&mdash;`SELECT`敏感`Select`與`select`(或 甚至 ) 相同。 但是,人們通常使用 SQL 語句中的關鍵`SELECT`字`WHERE`( 如和)來使其更易於閱讀。

### <a name="passing-the-search-term-as-a-parameter"></a>將搜尋字做參數

搜尋特定流派非常簡單 (),`WHERE Genre = 'Action'`但您希望能夠搜尋使用者輸入的任何流派。 為此,您可以創建為 SQL 查詢,其中包含要搜尋的值的占位符。 它會看起來像此指令:

`SELECT * FROM Movies WHERE Genre = @0`

占位元是字元`@`後跟零。 正如您可能猜到的,查詢可以包含多個占位符,並且它們將命名為`@0``@1``@2`、、、、、、、、、、、、、、 它們。

要設置查詢並實際傳遞該值,請使用如下所示的代碼:

[!code-sql[Main](form-basics/samples/sample4.sql)]

此代碼類似於您為在網格中顯示數據所做的。 唯一的區別是:

- 查詢包含佔位元`WHERE Genre = @0"`( 。
- 查詢被放入變數 (`selectCommand`;之前,您將查詢直接傳遞給`db.Query`方法 。
- 調用`db.Query`方法時,將傳遞查詢和要用於占位符的值。 (如果查詢有多個占位符,則將它們全部作為單獨的值傳遞給方法。

如果將所有這些元素放在一起,您將獲得以下代碼:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要!** 使用佔位元`@0`(如 ) 將數值傳給 SQL 指令對於安全性*至關重要*。 此處檢視的方式(使用變數數據的占位符)是建構 SQL 命令的唯一方法。
> 
> 切勿通過將從用戶獲得的文本和值組合(串聯)來建構 SQL 語句。 將使用者輸入串聯到 SQL 語句中會將您的網站置於*SQL 注入攻擊*中,惡意使用者向您的頁面提交入侵資料庫的值。 (您可以在文章[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 網站中閱讀更多內容。

## <a name="updating-the-movies-page-with-search-code"></a>使用搜尋程式碼更新電影頁面

現在,您可以更新 *「電影.cshtml」* 檔案中的代碼。 首先,用以下代碼取代頁面頂部的代碼塊中的代碼:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

此處的區別是,您已將查詢放入變數中`selectCommand`,稍後將傳遞給`db.Query`該變數。 將 SQL 語句放入變數中可以更改語句,這是執行搜索時執行的操作。

您還刪除了這兩行,稍後將重新放入:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

您還不想運行查詢(即呼叫`db.Query`),並且也不想初始`WebGrid`化 幫助程式。 在找出必須運行哪些 SQL 語句後,您將執行這些操作。

重寫此塊后,可以添加新邏輯來處理搜索。 已完成的代碼如下所示。 更新頁面中的代碼,使其與此範例符合:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

頁面現在像這樣工作。 每次執行頁面時,代碼都會打開資料庫,`selectCommand`變數將設置為 SQL 語句,該語`Movies`句從 表中獲取所有記錄。 代碼還會初始化`searchTerm`變數。

但是,如果當前請求包含`searchGenre`元素的值,則代碼將`selectCommand`設置 為不同的查詢,即包含用於搜索`Where`流派的子句。 它還設置`searchTerm`到搜索框傳遞的一切(可能什麼都不)。

無論 SQL 語`selectCommand`句在 中哪個`db.Query`,代碼都會調用以運行查詢,`searchTerm`將其傳遞給 中的任何內容。 如果`searchTerm`沒有任何內容,則無關緊要,因為在這種情況下,沒有參數可以無論如何將值傳遞給`selectCommand`。

最後,程式碼使用查詢結果初始`WebGrid`化 説明程式,就像以前一樣。

您可以看到,通過將 SQL 語句和搜索詞放入變數中,增加了代碼的靈活性。 正如本教程稍後將看到的那樣,您可以使用此基本框架,並繼續為不同類型的搜索添加邏輯。

## <a name="testing-the-search-by-genre-feature"></a>測試依類型搜尋功能

在 WebMatrix 中,執行 *「電影.cshtml」* 頁。 您將看到帶有流派文字框的頁面。

輸入您為其中一個測試記錄輸入的流派,然後單擊 **「搜索**」。 這一次,你看到一個清單,只是電影匹配該流派:

![電影頁面清單後搜索流派"喜劇"](form-basics/_static/image4.png)

輸入其他流派並再次搜索。 嘗試使用所有小寫或所有大寫字母輸入流派,以便您可以看到搜索不區分大小寫。

## <a name="remembering-what-the-user-entered"></a>"記住"使用者輸入的內容

您可能已經注意到,在您輸入一個流派並按一下**搜索流派**後,您看到了該流派的清單。 但是,搜索文字框換句話說是&mdash;空的,它不記得您輸入的內容。

瞭解此行為發生的原因非常重要。 提交頁面時,瀏覽器會向 Web 伺服器發送請求。 當ASP.NET收到請求時,它會創建頁面的全新實例,在其中運行代碼,然後將頁面再次呈現給瀏覽器。 實際上,該頁面不知道您只是使用自身的早期版本。 它只知道,它得到了一個請求,其中有一些表單數據。

每次請求頁面時,無論是&mdash;首次請求還是提交&mdash;頁面 ,您都會獲得新頁面。 Web 伺服器沒有您上次請求的記憶體。 瀏覽器也不ASP.NET,瀏覽器也不ASP.NET。 頁面的這些單獨實例之間的唯一連接是您在它們之間傳輸的任何數據。 例如,如果提交頁面,則新頁面實例可以獲取前一個實例發送的表單數據。 (在頁面之間傳遞數據的另一種方法是使用 Cookie。

描述此選項的一個正式方法是說網頁是*無狀態的*。 Web 伺服器和頁面本身以及頁面中的元素不保留有關頁面以前狀態的任何資訊。 Web 之所以以這種方式設計,是因為維護單個請求的狀態會迅速耗盡 Web 伺服器的資源,而 Web 伺服器通常每秒處理數千甚至數十萬個請求。

因此,文本框為空的原因。 提交頁面後,ASP.NET創建了該頁的新實例,並運行了代碼和標記。 該代碼中沒有任何內容告訴ASP.NET在文字框中輸入值。 因此ASP.NET什麼都沒做,文本框呈現時沒有值。

實際上,有一個簡單的方法來解決此問題。 您在文字框中輸入的流派*可在*文字框中的&mdash;代碼`Request.QueryString["searchGenre"]`中 使用。

更新文字框的標記,以便`value`屬性從`searchTerm`獲取 其值,如下所示:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此頁中`value`,還可以將屬性設置`searchTerm`為 變數,因為該變數還包含您輸入的流派。 但是,`Request`使用 物件設置如下`value`所示 的屬性是完成此任務的標準方法。 (假設在某些情況下甚至想要執行此操作&mdash;,則可能需要呈現*沒有*欄位中值的頁面。 這完全取決於你的應用發生了什麼。

> [!NOTE]
> 您無法「記住」用於密碼的文字框的值。 使用代碼允許人們填寫密碼欄位是一個安全漏洞。

重新執行頁面,輸入流派,然後按一次**搜尋流派**。 這一次,您不僅看到搜尋結果,而且文字框會記住您上次輸入的內容:

![顯示文字盒已記住上一個項目](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>搜尋任何單字

您現在可以搜尋任何流派,但您可能還需要搜索標題。 搜尋時很難完全正確獲取標題,因此您可以搜尋標題內任何位置的單詞。 在 SQL 中執行此`LIKE`操作, 請使用運算子和語法,如下所示:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令獲取其標題包含"冒險"的所有影片。 使用運算子時,`LIKE`將通配符`%`作為搜尋詞的一部分。 搜索`LIKE 'adventure%'`意味著"從'冒險'開始"。 (從技術上講,它意味著"字串'冒險'後跟任何東西。同樣,搜索詞`LIKE '%adventure'`的意思是"任何後面跟著字串'冒險'",這是另一種方式說"以『冒險』結束"。

因此,搜索`LIKE '%adventure%'`詞表示"與標題中的任何位置都具有『冒險性』」。 (從技術上講,"標題中的任何內容,然後是'冒險',然後是任何東西。

在元素`<form>`中,在流派搜尋的`</div>`關閉 標籤下方添加以下標記(就在`</form>`結束 元素之前):

[!code-html[Main](form-basics/samples/sample10.html)]

處理此搜尋的代碼與流派搜索的代碼類似,只不過您必須組裝`LIKE`搜索。 在頁面頂部的代碼塊中,在串流派`if``if`搜尋 的區塊之後添加此塊:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此代碼使用之前看到的相同邏輯,只不過搜索使用`LIKE`運算符,並且代碼在搜索詞之前和之後放置""。`%`

請注意如何輕鬆地向頁面添加另一個搜索。 你所要做的就是:

- 創建測試`if`的塊以查看相關搜尋框是否具有值。
- 將`selectCommand`變數設置為新的 SQL 語句。
- 將`searchTerm`變數設置為要傳遞給查詢的值。

下面是完整的代碼塊,其中包含標題搜索的新邏輯:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

以下是此程式碼的功能摘要：

- 變數`searchTerm`和`selectCommand`在頂部初始化。 您將根據使用者在頁面中所做的操作將這些變數設置為相應的搜索詞(如果有)和相應的 SQL 命令。 默認搜索是從資料庫中獲取所有影片的簡單示例。
- 在和`searchGenre``searchTitle`的測試中,代碼將`searchTerm`設置到要搜索的值。 這些代碼塊還設置為`selectCommand`該搜索的相應 SQL 命令。
- 該方法`db.Query`僅調用一次,使用`selectedCommand`中的任何 SQL`searchTerm`命令和 中的任何值。 如果沒有搜索詞(沒有流派,沒有標題詞),則值`searchTerm`為空字串。 但是,這並不重要,因為在這種情況下,查詢不需要參數。

## <a name="testing-the-title-search-feature"></a>測試標題搜尋功能

現在,您可以測試已完成的搜尋頁面。 執行*電影.cshtml*.

輸入流派,然後單擊**搜尋流派**。 網格顯示該流派的電影,就像以前一樣。

輸入標題字,然後單擊 **「搜索標題**」。 網格顯示標題中具有該單詞的電影。

![在標題中搜尋「The」後的電影頁面清單](form-basics/_static/image6.png)

將兩個文字框留空,然後按一下任一按鈕。 網格顯示所有影片。

## <a name="combining-the-queries"></a>組合查詢

您可能會注意到,您可以執行的搜索是獨佔的。 不能同時搜索標題和流派,即使兩個搜索框中都有值。 例如,您無法搜尋標題包含「冒險」的所有動作影片。 (現在對頁面進行編碼時,如果同時輸入流派和標題的值,則標題搜索將優先。要建立結合條件的搜索,必須創建具有如下語法的 SQL 查詢:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

您必須使用如下語句來執行查詢(大致而言):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

如您所見,創建邏輯以允許搜索條件的許多排列,可能會涉及一些內容。 因此,我們將在這裡停留。

## <a name="coming-up-next"></a>下一步

在下一教學中,您將創建一個頁面,該頁面使用窗體允許使用者向資料庫添加影片。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>影片頁面的完整清單(透過搜尋更新)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法進行 ASP.NET 網頁程式設計簡介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3學校網站上的[SQL WHERE 條款](http://www.w3schools.com/sql/sql_where.asp)
- [方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 網站上的文章

> [!div class="step-by-step"]
> [前一個](displaying-data.md)
> [下一個](entering-data.md)
