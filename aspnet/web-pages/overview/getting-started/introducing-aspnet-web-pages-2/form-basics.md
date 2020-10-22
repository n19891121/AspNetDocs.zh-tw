---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 簡介 ASP.NET Web Pages-HTML 表單基本概念 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將說明如何建立輸入表單的基本概念，以及當您使用 ASP.NET Web Pages (Razor) 時如何處理使用者的輸入。 現在您可以 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345460"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>簡介 ASP.NET Web Pages-HTML 表單基本概念

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程將說明如何建立輸入表單的基本概念，以及當您使用 ASP.NET Web Pages (Razor) 時如何處理使用者的輸入。 現在您已經有資料庫，您將使用您的表單技能，讓使用者在資料庫中尋找特定的電影。 它會假設您已完成 [使用 ASP.NET Web Pages 顯示資料的簡介](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。
> 
> 您將學到什麼：
> 
> - 如何使用標準 HTML 元素建立表單。
> - 如何在表單中讀取使用者的輸入。
> - 如何建立 SQL 查詢，以選擇性地使用使用者提供的搜尋字詞來取得資料。
> - 如何讓頁面中的欄位「記住」使用者輸入的內容。
>   
> 
> 討論的功能/技術：
> 
> - `Request` 物件。
> - SQL `Where` 子句。

## <a name="what-youll-build"></a>您要建置的內容

在上一個教學課程中，您已建立資料庫、將資料新增至其中，然後使用 `WebGrid` helper 來顯示資料。 在本教學課程中，您將新增搜尋方塊，讓您尋找特定內容類型或其標題包含您所輸入之任何單字的電影。  (例如，您將能夠找到類型為 "Action" 或標題包含 "Harry" 或 "艾德" 的所有電影。) 

當您完成本教學課程時，您將會看到如下的頁面：

![具有內容類型與標題搜尋的電影頁面](form-basics/_static/image1.png)

頁面的清單部分與最後一個教學課程中的 &mdash; 方格相同。 差別在於，方格只會顯示您搜尋的電影。

## <a name="about-html-forms"></a>關於 HTML 表單

 (如果您有建立 HTML 表單的經驗，以及與之間的 `GET` 差異 `POST` ，您可以略過本節。 ) 

表單具有使用者輸入元素 &mdash; 、按鈕、選項按鈕、核取方塊、下拉式清單等等。 使用者會填入這些控制項或進行選取，然後按一下按鈕來提交表單。

此範例說明表單的基本 HTML 語法：

[!code-html[Main](form-basics/samples/sample1.html)]

當此標記在頁面中執行時，它會建立如下圖所示的簡單表單：

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

`<form>`元素包含要提交的 HTML 元素。  (一個容易犯的錯誤，就是將專案加入至頁面，但忘了將它們放在 `<form>` 元素內。 在此情況下，不會提交任何專案。 ) `method` 屬性會告知瀏覽器如何提交使用者輸入。 如果您是在伺服器上執行更新，請將此設定為， `post` `get` 如果您只是從伺服器提取資料，則設定為。

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET、POST 和 HTTP 動詞命令安全**
> 
> HTTP 是瀏覽器和伺服器用來交換資訊的通訊協定，在其基本作業中非常簡單。 瀏覽器只會使用幾個動詞命令對伺服器提出要求。 當您撰寫 web 的程式碼時，瞭解這些動詞以及瀏覽器和伺服器如何使用它們會很有説明。 目前最常使用的動詞是：
> 
> - `GET`. 瀏覽器會使用此動詞命令從伺服器提取某個東西。 例如，當您在瀏覽器中輸入 URL 時，瀏覽器會執行 `GET` 操作來要求您想要的頁面。 如果頁面包含圖形，則瀏覽器會執行其他 `GET` 作業來取得影像。 如果作業 `GET` 必須將資訊傳遞至伺服器，則會在查詢字串中將資訊當作 URL 的一部分來傳遞。
> - `POST`. 瀏覽器會傳送 `POST` 要求，以便提交要在伺服器上新增或變更的資料。 例如， `POST` 使用動詞來建立資料庫中的記錄，或是變更現有的記錄。 在大部分的情況下，當您填寫表單，然後按一下 [提交] 按鈕時，瀏覽器會執行 `POST` 操作。 在作業中 `POST` ，傳遞至伺服器的資料會在頁面主體中。
> 
> 這些動詞的重要差異在於，作業 `GET` 不應該變更伺服器上的任何資訊，或將它以稍微更抽象的方式進行，而 `GET` 不會導致伺服器上的狀態變更。 您可以視需要 `GET` 在相同的資源上執行一次作業，而且這些資源不會變更。  (作業 `GET` 通常稱為「安全」，或使用技術詞彙，是 *等冪*的。相反地，) 相反地， `POST` 每當您執行作業時，要求就會變更伺服器上的某些內容。
> 
> 有兩個範例將有助於說明這種差異。 當您使用 Bing 或 Google 等引擎來執行搜尋時，您會填入由一個文字方塊所組成的表單，然後按一下 [搜尋] 按鈕。 瀏覽器會執行作業 `GET` ，並將您在 URL 中輸入的值輸入至該方塊。 `GET`針對此類型的表單使用作業是正常的，因為搜尋作業不會變更伺服器上的任何資源，而只會提取資訊。
> 
> 現在請考慮在線上排序某個東西的流程。 填寫訂單詳細資料，然後按一下 [提交] 按鈕。 這項作業將會是 `POST` 要求，因為此作業會導致伺服器上的變更，例如新的訂單記錄、您的帳戶資訊變更，還有其他許多變更。 與作業不同的是 `GET` ，您不能重複 `POST` 要求，如果您這樣做，每次重新提交要求時，就會在伺服器上產生新的訂單。  (在這種情況下，網站通常會警告您不要按一次 [提交] 按鈕，或停用 [提交] 按鈕，讓您不會意外重新提交表單。 ) 
> 
> 在本教學課程的過程中，您將使用 `GET` `POST` 作業和作業來處理 HTML 表單。 在每個案例中，我們將說明您所使用的動詞為何是適當的。
> 
>  (若要深入瞭解 HTTP 動詞命令，請參閱 W3C 網站上的 [方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 文章。 ) 

大部分的使用者輸入元素都是 HTML `<input>` 元素。 它們看起來像 `<input type="type" name="name">,` 是 *型* 別指出您想要的使用者輸入控制項種類。 這些是常見的元素：

- 文字方塊： `<input type="text">`
- 核取方塊： `<input type="check">`
- 選項按鈕： `<input type="radio">`
- 按鈕： `<input type="button">`
- 提交按鈕： `<input type="submit">`

您也可以使用專案 `<textarea>` 來建立多行文字方塊，並使用 `<select>` 元素來建立下拉式清單或可滾動清單。  (需 HTML form 元素的詳細資訊，請參閱 W3Schools 網站上的 [Html 表單和輸入](http://www.w3schools.com/html/html_forms.asp) 。 ) 

`name`屬性非常重要，因為名稱會是您稍後將如何取得元素值的方式，如您稍後所見。

有趣的部分就是您的網頁開發人員與使用者的輸入。 沒有與這些元素相關聯的內建行為。 相反地，您必須取得使用者輸入或選取的值，並對其進行一些動作。 這就是您將在本教學課程中學習的內容。

> [!TIP] 
> 
> **HTML5 和輸入表單**
> 
> 您可能已經知道，HTML 正在轉換，而最新版本 (HTML5) 包含可讓使用者以更直覺的方式輸入資訊的支援。 例如，在 HTML5 中，您 (網頁開發人員) 可以告訴網頁您希望使用者輸入日期。 然後，瀏覽器就可以自動顯示行事曆，而不需要使用者手動輸入日期。 不過，HTML5 是新的，但在所有瀏覽器中都不受支援。
> 
> ASP.NET Web Pages 支援 HTML5 輸入至使用者瀏覽器的範圍。 若要瞭解 HTML5 中元素的新屬性 `<input>` ，請參閱 W3Schools 網站上的 [HTML &lt; 輸入 &gt; 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp) 。

## <a name="creating-the-form"></a>建立表單

在 WebMatrix 的 [檔案] **工作區中，開啟 [** *電影. cshtml* ] 頁面。

在結束記號之後， `</h1>` 以及呼叫的開頭 `<div>` 標記之前 `grid.GetHtml` ，加入下列標記：

[!code-html[Main](form-basics/samples/sample2.html)]

此標記會建立表單，其中包含名為的文字方塊 `searchGenre` 和提交按鈕。 [文字方塊] 和 [提交] 按鈕會包含在 `<form>` `method` 屬性設為的專案中 `get` 。  (別忘了，如果您未在專案內放置文字方塊和送出按鈕 `<form>` ，當您按一下按鈕時，就不會送出任何專案。 ) 您使用這裡的動詞，是 `GET` 因為您要建立的表單不會在伺服器上進行任何變更，所以只會產生搜尋結果。  (在上一個教學課程中，您使用了 `post` 方法，也就是您將變更提交至伺服器的方式。 在下一個教學課程中，您將會再次看到。 ) 

執行頁面。 雖然您尚未為表單定義任何行為，但您可以看到它的樣子：

![具有內容類型搜尋方塊的電影頁面](form-basics/_static/image3.png)

在文字方塊中輸入值，例如 "喜劇"。 然後按一下 [ **搜尋**內容類型]。

記下頁面的 URL。 因為您將專案 `<form>` 的 `method` 屬性設定為 `get` ，所以您輸入的值現在是 URL 中查詢字串的一部分，如下所示：

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>讀取表單值

此頁面已經包含一些可取得資料庫資料的程式碼，並在方格中顯示結果。 現在您必須新增一些程式碼來讀取文字方塊的值，以便執行包含搜尋詞彙的 SQL 查詢。

因為您將表單的方法設定為 `get` ，所以您可以使用類似下列的程式碼來讀取在文字方塊中輸入的值：

`var searchTerm = Request.QueryString["searchGenre"];`

物件 `Request.QueryString` (物件的 `QueryString` 屬性) 包含在作業中 `Request` 提交的元素值 `GET` 。 `Request.QueryString`屬性包含*集合* (在表單中提交值的清單) 。 若要取得任何個別值，請指定您想要的專案名稱。 這就是為什麼您必須在專案 `name` 上擁有屬性， `<input>` (可 `searchTerm` 建立文字方塊的) 。  (如需物件的詳細資訊 `Request` ，請稍後參閱 [側邊欄](#BKMK_TheRequestObject) 。 ) 

它夠簡單，可以讀取文字方塊的值。 但是，如果使用者未在文字方塊中完全輸入任何內容，但是按一下 [ **搜尋** ]，則可以忽略該點，因為沒有任何專案可以搜尋。

下列程式碼顯示如何執行這些條件的範例。  (您還不需要加入此程式碼;您稍後將會這麼做。 ) 

[!code-csharp[Main](form-basics/samples/sample3.cs)]

測試會以這種方式細分：

- 取得的值，也就 `Request.QueryString["searchGenre"]` 是在名為的元素中輸入的值 `<input>` `searchGenre` 。
- 使用方法瞭解是否為空的 `IsEmpty` 。 這個方法是用來判斷是否有某個專案 (的標準方式，) 包含值的表單元素。 但事實上，您只在意它 *不* 是空的，因此 .。。
- 將 `!` 運算子加入 `IsEmpty` 測試前面。  (`!` 運算子表示邏輯 NOT) 。

在純文字中，整個 `if` 條件會轉譯成下列內容：*如果表單的 searchGenre 元素不是空的，則*.。。

此區塊會設定用來建立使用搜尋字詞之查詢的階段。 您將在下一節中執行該動作。

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Request 物件**
> 
> `Request`物件包含當要求或提交頁面時，瀏覽器傳送至應用程式的所有資訊。 此物件包含使用者提供的任何資訊，例如文字方塊值或要上傳的檔案。 它也包含各種額外的資訊，例如 cookie、URL 查詢字串中的值 (如果有任何) 、正在執行之頁面的檔案路徑、使用者使用的瀏覽器類型、在瀏覽器中設定的語言清單等等。
> 
> `Request`物件是值的*集合* (清單) 。 您可以藉由指定名稱，從集合中取得個別的值：
> 
> `var someValue = Request["name"];`
> 
> `Request`物件實際上會公開數個子集。 例如：
> 
> - `Request.Form``<form>`如果要求是要求，則提供來自已提交專案內元素的值 `POST` 。
> - `Request.QueryString` 只提供 URL 查詢字串中的值。  (在類似的 URL 中 `http://mysite/myapp/page?searchGenre=action&page=2` ， `?searchGenre=action&page=2` url 的區段是查詢字串。 ) 
> - `Request.Cookies` 集合可讓您存取瀏覽器已傳送的 cookie。
> 
> 若要取得您知道已提交表單中的值，您可以使用 `Request["name"]` 。 或者，您可以使用 `Request.Form["name"]` (針對 `POST` 要求) 或 `Request.QueryString["name"]` (`GET`) 要求的特定版本。 當然， *name* 是要取得之專案的名稱。
> 
> 您要取得之專案的名稱在您所使用的集合中必須是唯一的。 這就是 `Request` 物件提供的子集，例如 `Request.Form` 和 `Request.QueryString` 。 假設您的頁面包含名為的 form 元素 `userName` ，而且 *也* 包含名為的 cookie `userName` 。 如果您 `Request["userName"]` 想要的話，就不會看到表單值或 cookie。 但是，如果您取得 `Request.Form["userName"]` 或 `Request.Cookie["userName"]` ，就會明確瞭解要取得的值。
> 
> 使用 `Request` 您感興趣的子集（例如或）是很好的作法 `Request.Form` `Request.QueryString` 。 針對您在本教學課程中建立的簡單頁面，它可能不會真正產生任何差異。 不過，當您建立更複雜的頁面時，使用明確版本 `Request.Form` 或 `Request.QueryString` 可協助您避免頁面包含表單 (或多個表單) 、cookie、查詢字串值等時可能發生的問題。

## <a name="creating-a-query-by-using-a-search-term"></a>使用搜尋字詞建立查詢

既然您已經知道如何取得使用者所輸入的搜尋字詞，就可以建立使用它的查詢。 請記住，若要從資料庫中取得所有電影專案，您會使用類似下列語句的 SQL 查詢：

`SELECT * FROM Movies`

若只要取得特定電影，您必須使用包含子句的查詢 `Where` 。 此子句可讓您設定查詢所傳回之資料列的條件。 以下是範例：

`SELECT * FROM Movies WHERE Genre = 'Action'`

基本格式為 `WHERE column = value` 。 您可以使用不同的運算子 `=` ，例如 `>` (大於) 、 `<` (小於) 、 `<>` (不等於) 、 `<=` (小於或等於) 等，視您要尋找的內容而定。

如果您想知道，SQL 語句不區分大小寫，與 &mdash; `SELECT` `Select` (或甚至 `select`) 相同。 不過，使用者通常會將 SQL 語句中的關鍵字大寫，例如 `SELECT` 和 `WHERE` ，以便更容易閱讀。

### <a name="passing-the-search-term-as-a-parameter"></a>傳遞搜尋詞彙作為參數

搜尋特定的類型很容易 (`WHERE Genre = 'Action'`) ，但是您想要能夠搜尋使用者輸入的任何內容類型。 若要這樣做，您可以建立 SQL 查詢，其中包含要搜尋之值的預留位置。 它看起來會像這個命令：

`SELECT * FROM Movies WHERE Genre = @0`

預留位置是 `@` 後面接著零的字元。 您可能會猜到，查詢可能包含多個預留位置，而且會命名為 `@0` 、、等等 `@1` `@2` 。

若要設定查詢並實際將該值傳遞給它，您可以使用如下所示的程式碼：

[!code-sql[Main](form-basics/samples/sample4.sql)]

這段程式碼與您在方格中顯示資料所做的一樣。 唯一的差異如下：

- 查詢包含 () 的預留位置 `WHERE Genre = @0"` 。
- 查詢會放入變數 (`selectCommand`) ; 之前，您會將查詢直接傳遞給 `db.Query` 方法。
- 當您呼叫 `db.Query` 方法時，會傳遞查詢和值以用於預留位置。  (如果查詢有多個預留位置，您會將它們全部作為個別值傳遞給方法。 ) 

如果您將這些專案全部放在一起，您會得到下列程式碼：

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **重要！** 使用預留位置 (例如 `@0`) 將值傳遞給 SQL 命令對安全性而言 *非常重要* 。 您在這裡看到的方式（具有變數資料的預留位置）是您應該用來建立 SQL 命令的唯一方式。
> 
> 絕對不要建立 SQL 語句，方法是將 (串連) 常值文字和您從使用者取得的值。 將使用者輸入串連成 SQL 語句，會將您的網站開啟至 *sql 插入式攻擊* ，惡意使用者將值提交至您的頁面，以攻擊您的資料庫。  (您可以在 [SQL 插入](https://msdn.microsoft.com/library/ms161953.aspx) MSDN 網站的文章中閱讀更多內容。 ) 

## <a name="updating-the-movies-page-with-search-code"></a>使用搜尋程式碼更新電影頁面

現在您可以更新 *電影* 檔中的程式碼。 若要開始，請將頁面頂端程式碼區塊中的程式碼取代為下列程式碼：

[!code-csharp[Main](form-basics/samples/sample6.cs)]

差別在於，您已將查詢放入 `selectCommand` 變數中，以便稍後傳遞給您 `db.Query` 。 將 SQL 語句放入變數中，可讓您變更語句，這是執行搜尋所要執行的動作。

您也移除了這兩行，您稍後會將這些行放回：

[!code-csharp[Main](form-basics/samples/sample7.cs)]

您不想要執行查詢 (也就是呼叫) ， `db.Query` 而且您也不想要初始化 `WebGrid` helper。 您將會在找出必須執行的 SQL 語句之後，執行這些動作。

在這個重寫的區塊之後，您可以新增處理搜尋的邏輯。 完成的程式碼看起來會如下所示。 更新頁面中的程式碼，使其符合此範例：

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

頁面現在的運作方式如下。 每次頁面執行時，程式碼就會開啟資料庫，並將 `selectCommand` 變數設定為 SQL 語句，以取得資料表中的所有記錄 `Movies` 。 程式碼也會初始化 `searchTerm` 變數。

但是，如果目前的要求包含專案的值 `searchGenre` ，則程式碼會將設定 `selectCommand` 為不同的查詢（也就是包含 `Where` 子句來搜尋內容類型的查詢）。 它也會設定 `searchTerm` 為搜尋方塊所傳遞的內容 (這可能不) 。

無論在哪一個 SQL 語句中 `selectCommand` ，程式碼都會呼叫 `db.Query` 來執行查詢，並將它傳遞至其中的任何內容 `searchTerm` 。 如果沒有任何專案 `searchTerm` ，則不重要，因為在此情況下，不會有任何參數可將值傳遞給 `selectCommand` 。

最後，程式碼會 `WebGrid` 使用查詢結果來初始化 helper，就像之前一樣。

您可以看到，將 SQL 語句和搜尋詞彙放入變數中，就可以在程式碼中加入彈性。 您稍後會在本教學課程中看到，您可以使用這個基本架構，並針對不同的搜尋類型繼續新增邏輯。

## <a name="testing-the-search-by-genre-feature"></a>測試依類型搜尋的功能

在 WebMatrix 中，執行 [ *cshtml* ] 頁面。 您會看到含有內容類型之文字方塊的頁面。

輸入您為其中一個測試記錄輸入的內容類型，然後按一下 [ **搜尋**]。 這次您只會看到符合該內容類型的影片清單：

![搜尋類型 ' Comedies ' 後的電影頁面清單](form-basics/_static/image4.png)

輸入不同的內容類型，然後再次搜尋。 請嘗試使用全部小寫或全部大寫字母來輸入內容類型，讓您可以看到搜尋不區分大小寫。

## <a name="remembering-what-the-user-entered"></a>「記住」使用者輸入的內容

您可能已經注意到，當您輸入內容類型並按一下 [ **搜尋**內容類型] 之後，就會看到該內容類型的清單。 不過，搜尋文字方塊是空的 &mdash; ，換句話說，它並不記得您輸入的內容。

請務必瞭解為何會發生這種行為。 當您提交頁面時，瀏覽器會將要求傳送至 web 伺服器。 當 ASP.NET 取得要求時，它會建立頁面的全新實例、在其中執行程式碼，然後再次將頁面轉譯至瀏覽器。 但實際上，頁面並不知道您是使用舊版本身。 所有的 it 都知道，它收到的要求中有一些表單資料。

每次您第一次要求頁面時， &mdash; 或提交該頁面時， &mdash; 您都會收到新的頁面。 Web 服務器沒有您最後一個要求的記憶體。 兩者都不會 ASP.NET，瀏覽器也不會執行。 這兩個頁面的個別實例之間的唯一連接，就是您在它們之間傳輸的任何資料。 例如，如果您提交頁面，新的頁面實例可以取得先前實例所傳送的表單資料。  (在頁面之間傳遞資料的另一種方式是使用 cookie。 ) 

描述這種情況的正式方式是說，網頁是 *無狀態*的。 網頁伺服器和頁面本身以及頁面中的專案，並不會維護頁面先前狀態的任何相關資訊。 這是以這種方式設計的，因為維護個別要求的狀態時，可能會很快耗盡 web 伺服器的資源，而這通常會處理數千個（甚至是每秒數十萬個要求）。

這就是為什麼文字方塊是空的。 送出頁面之後，ASP.NET 就會建立新的網頁實例，並執行程式碼和標記。 該程式碼中沒有告訴 ASP.NET 將值放入文字方塊中的內容。 因此 ASP.NET 不會執行任何動作，而且文字方塊會轉譯，而不會有值。

其實有一個簡單的方法可以解決這個問題。 您在文字方塊中輸入的內容可以在其所在 *的程式碼中使用* &mdash; `Request.QueryString["searchGenre"]` 。

更新文字方塊的標記 `value` ，讓屬性從中取得值 `searchTerm` ，如下列範例所示：

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

在此頁面上，您也可以將 `value` 屬性設定為 `searchTerm` 變數，因為該變數也包含您輸入的內容類型。 但是，使用 `Request` 物件來設定 `value` 屬性（如下所示）是完成這項工作的標準方式。  (假設您甚至想要 &mdash; 在某些情況下這麼做，您可能會想要在欄位中呈現 *沒有* 值的頁面。 這完全取決於應用程式的進展。 ) 

> [!NOTE]
> 您無法「記住」用於密碼的文字方塊值。 這會是一個安全性漏洞，可讓使用者使用程式碼填寫密碼欄位。

再次執行頁面，輸入內容類型，然後按一下 [ **搜尋**內容類型]。 這次不只是您看到搜尋的結果，而且文字方塊會記住您上次輸入的內容：

![頁面顯示文字方塊已「記住」先前的專案](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>搜尋標題中的任何單字

您現在可以搜尋任何內容類型，但您也可能想要搜尋標題。 當您搜尋時，很難正確地取得標題，因此您可以搜尋出現在標題內任何位置的單字。 若要在 SQL 中執行此作業，您可以使用 `LIKE` 運算子和語法，如下所示：

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

此命令會取得其標題包含 "艾德" 的所有電影。 當您使用 `LIKE` 運算子時，您會在搜尋詞彙中包含萬用字元 `%` 。 搜尋 `LIKE 'adventure%'` 表示「開頭為「冒險」」。  (技術上來說，這表示「「冒險」後面接著任何「字串」。) 同樣地，搜尋詞彙 `LIKE '%adventure'` 表示「任何內容，後面接著字串 ' 冒險 '」，這是另一種表示「以 ' 冒險 ' 結尾」的方法。

因此，搜尋詞彙 `LIKE '%adventure%'` 表示「在標題中的任意位置」。  (技術上，「標題中的任何專案，後面接著「冒險」，後面接著任何專案」。) 

在專案內 `<form>` ，于內容類型搜尋的結束記號下加入下列標記， `</div>` (緊接在結尾 `</form>` 元素) 之前：

[!code-html[Main](form-basics/samples/sample10.html)]

處理這項搜尋的程式碼類似于內容搜尋的程式碼，不同之處在于您必須組合 `LIKE` 搜尋。 在頁面頂端的程式碼區塊內，在 `if` 內容類型搜尋的區塊之後加入此區塊 `if` ：

[!code-csharp[Main](form-basics/samples/sample11.cs)]

此程式碼會使用您稍早所見的相同邏輯，不同之處在于搜尋會使用 `LIKE` 運算子，而且程式碼會將 "" 放在 `%` 搜尋字詞的前後。

請注意，在頁面中新增另一個搜尋是很容易的。 您只需要：

- 建立 `if` 測試的區塊，以查看相關的搜尋方塊是否具有值。
- 將 `selectCommand` 變數設定為新的 SQL 語句。
- 將變數設定為 `searchTerm` 要傳遞給查詢的值。

以下是完整的程式碼區塊，其中包含標題搜尋的新邏輯：

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

以下是此程式碼的功能摘要：

- 變數 `searchTerm` 和 `selectCommand` 會在頂端初始化。 您要將這些變數設定為適當的搜尋字詞 (如果有任何) 和適當的 SQL 命令是根據使用者在頁面中執行的內容而定。 預設搜尋是從資料庫取得所有電影的簡單案例。
- 在和的測試 `searchGenre` 中 `searchTitle` ，程式碼會將設定 `searchTerm` 為您想要搜尋的值。 這些程式碼區塊也 `selectCommand` 會針對該搜尋設定為適當的 SQL 命令。
- `db.Query`方法只會叫用一次，並使用任何 SQL 命令， `selectedCommand` 以及任何值在中 `searchTerm` 。 如果沒有搜尋詞彙 (沒有內容類型，而且沒有任何標題字) ，的值 `searchTerm` 就是空字串。 不過，這並不重要，因為在此情況下，查詢不需要參數。

## <a name="testing-the-title-search-feature"></a>測試標題搜尋功能

現在您可以測試已完成的搜尋頁面。 執行 *電影. cshtml*。

輸入內容類型，然後按一下 [ **搜尋**內容類型]。 方格會顯示該內容類型的電影，就像之前一樣。

輸入標題文字，然後按一下 [ **搜尋標題**]。 方格會顯示標題中有該單字的電影。

![搜尋標題中的 ' a ' 之後的電影頁面清單](form-basics/_static/image6.png)

將兩個文字方塊保持空白，然後按一下其中一個按鈕。 方格會顯示所有電影。

## <a name="combining-the-queries"></a>合併查詢

您可能會注意到，您可以執行的搜尋是獨佔的。 即使兩個搜尋方塊中都有值，您也無法同時搜尋標題和內容類型。 例如，您無法搜尋標題包含 "艾德" 的所有動作電影。  (在現在為頁面撰寫程式碼時，如果您同時輸入內容類型和標題的值，則會優先使用標題搜尋。 ) 若要建立結合條件的搜尋，您必須建立具有如下語法的 SQL 查詢：

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

而且，您必須使用如下所示的語句來執行查詢 (大約說) ：

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

如您所見，建立邏輯以允許許多搜尋準則排列可能有點相關。 因此，我們將在此停止。

## <a name="coming-up-next"></a>後續推出

在下一個教學課程中，您將建立使用表單的頁面，讓使用者將電影新增至資料庫。

## <a name="complete-listing-for-movie-page-updated-with-search"></a>影片頁面的完整清單 (以搜尋) 更新

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法進行 ASP.NET 網頁程式設計簡介](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 網站上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)
- W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章

> [!div class="step-by-step"]
> [上一個](displaying-data.md) 
> [下一步](entering-data.md)
