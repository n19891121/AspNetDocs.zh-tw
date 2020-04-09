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
# <a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="7e8a5-104">介紹ASP.NET網頁 - HTML表單基礎知識</span><span class="sxs-lookup"><span data-stu-id="7e8a5-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>

<span data-ttu-id="7e8a5-105"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="7e8a5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="7e8a5-106">本教程介紹如何創建輸入表單以及使用ASP.NET網頁 (Razor) 時如何處理使用者輸入的基礎知識。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="7e8a5-107">現在您已經有了一個資料庫,您將使用表單技能讓用戶在資料庫中尋找特定影片。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="7e8a5-108">它假定您已經通過[介紹使用ASP.NET網頁顯示數據](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)完成了該系列。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="7e8a5-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="7e8a5-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="7e8a5-110">如何使用標準 HTML 元素建立表單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="7e8a5-111">如何讀取表單中的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="7e8a5-112">如何創建 SQL 查詢,該查詢通過使用使用者提供的搜索詞選擇性地獲取數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="7e8a5-113">如何在頁面中「記住」使用者輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="7e8a5-114">討論的功能/技術:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="7e8a5-115">`Request` 物件。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-115">The `Request` object.</span></span>
> - <span data-ttu-id="7e8a5-116">SQL`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-116">The SQL `Where` clause.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="7e8a5-117">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="7e8a5-117">What You'll Build</span></span>

<span data-ttu-id="7e8a5-118">在前面的教程中,您創建了一個資料庫,向它添加了數據,然後使用`WebGrid`幫助器來顯示數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="7e8a5-119">在本教學中,您將添加一個搜尋框,允許您查找特定流派的電影或其標題包含您輸入的任何單詞。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="7e8a5-120">(例如,您可以查找所有類型為"行動"或標題包含"Harry"或"冒險"的電影。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="7e8a5-121">完成本教學後,您將有一個像這樣的頁面:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![引入流派與標題搜尋的電影頁面](form-basics/_static/image1.png)

<span data-ttu-id="7e8a5-123">頁面的清單部分與上一教程&mdash;中網格相同。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="7e8a5-124">區別在於網格將僅顯示您搜索的電影。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="7e8a5-125">關於 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="7e8a5-125">About HTML Forms</span></span>

<span data-ttu-id="7e8a5-126">(如果您在創建 HTML 窗體方面擁有經驗,並且`GET``POST`具有和之間的差異,則可以跳過此部分。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="7e8a5-127">表單選使用者輸入元素&mdash;文字框、按鈕、單選按鈕、複選框、下拉清單等。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="7e8a5-128">使用者填寫這些控制項或進行選擇,然後透過單擊按鈕提交表單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="7e8a5-129">以下範例說明了表單的基本 HTML 語法:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="7e8a5-130">當此標籤在頁面中執行時,它將建立一個類似於下圖的簡單窗體:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

<span data-ttu-id="7e8a5-132">這個`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="7e8a5-133">(一個簡單的錯誤是向頁面添加元素,但隨後忘記將它們放入`<form>`元素中。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="7e8a5-134">在這種情況下,不會提交任何內容。該`method`屬性告訴瀏覽器如何提交使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="7e8a5-135">`post`如果在伺服器上執行更新,或者`get`只是從伺服器取得資料,則可以將此設定為</span><span class="sxs-lookup"><span data-stu-id="7e8a5-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="7e8a5-136">**取得、POST 與 HTTP 動詞安全**</span><span class="sxs-lookup"><span data-stu-id="7e8a5-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="7e8a5-137">HTTP是瀏覽器和伺服器用來交換資訊的協定,其基本操作非常簡單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="7e8a5-138">瀏覽器僅使用幾個謂詞向伺服器發出請求。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="7e8a5-139">為 Web 編寫代碼時,瞭解這些謂詞以及瀏覽器和伺服器如何使用這些謂詞會很有説明。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="7e8a5-140">遠外最常用的動詞是:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="7e8a5-141">`GET`.</span><span class="sxs-lookup"><span data-stu-id="7e8a5-141">`GET`.</span></span> <span data-ttu-id="7e8a5-142">瀏覽器使用此謂詞從伺服器獲取內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="7e8a5-143">例如,當您在瀏覽器中鍵入 URL 時,瀏覽器將`GET`執行操作 以請求所需的頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="7e8a5-144">如果頁面包含圖形,瀏覽器將執行其他`GET`操作以獲取圖像。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="7e8a5-145">如果`GET`操作必須將資訊傳遞到伺服器,則資訊將作為查詢字串中 URL 的一部分傳遞。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="7e8a5-146">`POST`.</span><span class="sxs-lookup"><span data-stu-id="7e8a5-146">`POST`.</span></span> <span data-ttu-id="7e8a5-147">瀏覽器發送`POST`請求以提交要在伺服器上添加或更改的數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="7e8a5-148">例如,謂`POST`詞用於在資料庫中創建記錄或更改現有記錄。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="7e8a5-149">大多數時候,當您填寫表單並按下提交按鈕時,瀏覽器將執行操作`POST`。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="7e8a5-150">在操作`POST`中,傳遞給伺服器的數據位於頁面正文中。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="7e8a5-151">這些謂詞之間的一個重要區別是,操作`GET`不應更改伺服器上的任何內容,或者以稍微抽象的方式將其放在操作中`GET`, 操作不會導致伺服器上的狀態更改。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="7e8a5-152">您可以根據需要多次對`GET`同一資源執行操作,並且這些資源不會更改。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="7e8a5-153">(操作`GET`通常說是"安全的",或者使用技術術語,是*冪*等的。當然,與此相反,每次執行`POST`操作時,請求都會更改伺服器上的內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="7e8a5-154">兩個例子將有助於說明這一區別。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="7e8a5-155">當您使用必應或 Google 等引擎執行搜尋時,您將填寫包含一個文字框的表單,然後單擊搜尋按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="7e8a5-156">瀏覽器執行操作`GET`,輸入到框中的值作為 URL 的一部分傳遞。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="7e8a5-157">對這種類型的`GET`窗體使用操作很好,因為搜索操作不會更改伺服器上的任何資源,因此只需獲取資訊。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="7e8a5-158">現在考慮在線訂購內容的過程。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="7e8a5-159">您填寫訂單詳細資訊,然後按一下提交按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="7e8a5-160">此操作將是一個`POST`請求,因為該操作將導致伺服器上的更改,例如新訂單記錄、帳戶資訊的更改,以及許多其他更改。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="7e8a5-161">與`GET`操作不同,您不能重複`POST`請求 - 如果重複請求,則每次重新提交請求時,都會在伺服器上生成新訂單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="7e8a5-162">(在這種情況下,網站通常會警告您不要多次按一下提交按鈕,或者將禁用提交按鈕,以便您不會意外重新提交表單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="7e8a5-163">在本教學中,您將使用`GET`操作和`POST`操作來處理 HTML 窗體。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="7e8a5-164">我們將在每種情況下解釋為什麼您使用的動詞是合適的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="7e8a5-165">(要瞭解有關 HTTP 謂詞的更多資訊,請參閱 W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>

<span data-ttu-id="7e8a5-166">大多數使用者輸入元素是`<input>`HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="7e8a5-167">它們看起來像`<input type="type" name="name">,`*類型*指示所需使用者輸入控制項的類型。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="7e8a5-168">這些元素是常見的元素:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-168">These elements are the common ones:</span></span>

- <span data-ttu-id="7e8a5-169">文字盒:`<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="7e8a5-170">勾選盒:`<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="7e8a5-171">按一個按鈕:`<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="7e8a5-172">按鈕:`<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="7e8a5-173">提交按鈕:`<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="7e8a5-174">您還可以使用`<textarea>`元素 建立多行文字`<select>`框和 元素以建立下拉清單或可滾動清單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="7e8a5-175">(HTML 表單元素的更多內容,請參考 W3Schools 網站的[HTML 表單和輸入](http://www.w3schools.com/html/html_forms.asp)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="7e8a5-176">該`name`屬性非常重要,因為名稱是以後獲取元素值的方式,稍後將看到。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="7e8a5-177">有趣的部分是您,頁面開發人員,對使用者輸入所做的操作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="7e8a5-178">沒有與這些元素關聯的內置行為。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="7e8a5-179">相反,您必須獲取使用者已輸入或選擇的值,並對其進行操作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="7e8a5-180">這是您將在本教程中學到的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="7e8a5-181">**HTML5 與輸入表單**</span><span class="sxs-lookup"><span data-stu-id="7e8a5-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="7e8a5-182">您可能知道,HTML 處於過渡狀態,最新版本 (HTML5) 包括支援使用者輸入資訊的更直觀方式。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="7e8a5-183">例如,在 HTML5 中,您可以告訴頁面您希望使用者輸入日期。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="7e8a5-184">然後,瀏覽器可以自動顯示日曆,而不是要求用戶手動輸入日期。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="7e8a5-185">但是,HTML5 是新的,並非所有瀏覽器都支援 HTML5。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="7e8a5-186">ASP.NET網頁支援 HTML5 輸入,只要使用者的瀏覽器支援 HTML5 輸入。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="7e8a5-187">有關 HTML5`<input>`中 元素的新屬性的概念,請參閱 W3Schools 網站上的 HTML[&lt;&gt;輸入 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>

## <a name="creating-the-form"></a><span data-ttu-id="7e8a5-188">建立表單</span><span class="sxs-lookup"><span data-stu-id="7e8a5-188">Creating the Form</span></span>

<span data-ttu-id="7e8a5-189">在 WebMatrix 中,在 **「檔**」工作區中,打開 *「電影.cshtml」* 頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="7e8a5-190">在結束`</h1>`標記之後`<div>``grid.GetHtml`和 撥號的開頭標記之前,添加以下標記:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="7e8a5-191">此標記創建一個表單,該表單具有名為`searchGenre`文本框和提交按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="7e8a5-192">文字框和提交按鈕包含在其`<form>``method`屬性設置`get`為 的元素中。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="7e8a5-193">(請記住,如果不將文字框和提交按鈕放在`<form>`元素中,則按一下該按鈕時不會提交任何內容。您在此處使用`GET`謂詞是因為您正在創建一個不會在伺服器上進行任何更改的窗體 - 它只是導致搜索。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="7e8a5-194">(在前面的教程中,您使用了一`post`種方法,即向伺服器提交更改的方式。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="7e8a5-195">您將在下一教程中再次看到這一點。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="7e8a5-196">運行頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-196">Run the page.</span></span> <span data-ttu-id="7e8a5-197">儘管尚未為表單定義任何行為,但您可以看到它的外觀:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![帶有「流派」搜尋框的影片頁面](form-basics/_static/image3.png)

<span data-ttu-id="7e8a5-199">在文本框中輸入一個值,如"喜劇"。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="7e8a5-200">然後點選**搜尋流派**。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="7e8a5-201">記下頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-201">Take note of the URL of the page.</span></span> <span data-ttu-id="7e8a5-202">由於將`<form>`元素的`method`屬性`get`設定為 ,因此您輸入的值現在是網址中查詢字串的一部分,如下所示:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="7e8a5-203">讀取表單</span><span class="sxs-lookup"><span data-stu-id="7e8a5-203">Reading Form Values</span></span>

<span data-ttu-id="7e8a5-204">該頁已包含一些代碼,這些代碼獲取資料庫數據並在網格中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="7e8a5-205">現在,您必須添加一些讀取文本框值的代碼,以便運行包含搜索詞的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="7e8a5-206">由於將表單的程式設定`get`為 ,因此可以使用以下的程式碼讀取輸入到文字框中的值:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="7e8a5-207">物件`Request.QueryString``QueryString``Request`(物件的屬性)包括`GET`作為 操作的一部分提交的元素的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="7e8a5-208">屬性`Request.QueryString`包含表單中提交的值*的集合*(清單)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="7e8a5-209">要取得任何單個值,請指定所需的元素的名稱。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="7e8a5-210">這就是為什麼您必須在創建文本框`name``<input>`的元素`searchTerm`( ) 上具有屬性的原因。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="7e8a5-211">( 有關物件的更多`Request`, 請參考邊[列](#BKMK_TheRequestObject)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="7e8a5-212">閱讀文本框的值非常簡單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="7e8a5-213">但是,如果使用者在文本框中根本不輸入任何內容,但無論如何都單擊 **「搜索」,** 則可以忽略該單擊,因為沒有什麼可搜索的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="7e8a5-214">以下代碼是演示如何實現這些條件的範例。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="7e8a5-215">(您不必添加此代碼,您一會兒就將添加。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="7e8a5-216">測試以這種方式分解:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="7e8a5-217">獲取的值`Request.QueryString["searchGenre"]`,即輸入到`<input>``searchGenre`名為 的元素中的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="7e8a5-218">使用`IsEmpty`方法瞭解其是否為空。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="7e8a5-219">此方法是確定某些內容(例如表單元素)是否包含值的標準方法。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="7e8a5-220">但實際上,你只關心,如果它*不*是空的,因此...</span><span class="sxs-lookup"><span data-stu-id="7e8a5-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="7e8a5-221">測試`!``IsEmpty`前添加運算子。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="7e8a5-222">(運算符`!`表示邏輯 NOT)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="7e8a5-223">在純英語中,整個`if`條件轉換為以下內容:*如果表單的 searchGenre 元素不為空,則 ...*</span><span class="sxs-lookup"><span data-stu-id="7e8a5-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="7e8a5-224">此塊設置創建使用搜索詞的查詢的階段。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="7e8a5-225">您將在下一節中執行該動作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="7e8a5-226">**要求物件**</span><span class="sxs-lookup"><span data-stu-id="7e8a5-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="7e8a5-227">該`Request`物件包含瀏覽器在請求或提交頁面時發送到應用程式的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="7e8a5-228">此物件包括使用者提供的任何資訊,如文本框值或要上傳的檔。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="7e8a5-229">它還包括各種附加資訊,如 Cookie、URL 查詢字串中的值(如果有)、正在運行的頁面的檔路徑、使用者使用的瀏覽器類型、在瀏覽器中設置的語言清單等等。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="7e8a5-230">該`Request`對像是值*的集合*(清單)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="7e8a5-231">以指定單個值的名稱,從集合中取得單個值:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="7e8a5-232">該`Request`對象實際上公開了幾個子集。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="7e8a5-233">例如：</span><span class="sxs-lookup"><span data-stu-id="7e8a5-233">For example:</span></span>
> 
> - <span data-ttu-id="7e8a5-234">`Request.Form`如果請求是`POST`請求,則從`<form>`提交 元素中的元素提供值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="7e8a5-235">`Request.QueryString`僅為您提供 URL 查詢字串中的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="7e8a5-236">(在網`http://mysite/myapp/page?searchGenre=action&page=2`址中,URL`?searchGenre=action&page=2`的部份是查詢字串。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="7e8a5-237">`Request.Cookies`集合允許您訪問瀏覽器發送的 Cookie。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="7e8a5-238">要取得您知道在提交的表單的值,可以使用`Request["name"]`。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="7e8a5-239">或者,`Request.Form["name"]`您可以使用更具體的版本(`POST`用於請求)`Request.QueryString["name"]`或`GET`(用於請求)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="7e8a5-240">當然,*名稱*是要獲取的項的名稱。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="7e8a5-241">要獲取的項的名稱必須在要使用的集合中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="7e8a5-242">這就是為什麼`Request`物件提供子集,`Request.Form`如`Request.QueryString`和 。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="7e8a5-243">假設您的頁面包含名為的`userName`表單元素,*並且還*包含名為`userName`的 Cookie。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="7e8a5-244">如果得到`Request["userName"]`,則是模糊的是想要表單值還是 Cookie。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="7e8a5-245">但是,如果您得到`Request.Form["userName"]`或`Request.Cookie["userName"]`,則明確要獲取的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="7e8a5-246">最好是具體使用您感興趣的子集`Request`,`Request.Form`例如`Request.QueryString`或 。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="7e8a5-247">對於您在本教程中創建的簡單頁面,它可能沒有任何區別。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="7e8a5-248">但是,當您創建更複雜的頁面時,使用顯式版本`Request.Form``Request.QueryString`或 可以説明您避免在頁面包含窗體(或多個窗體)、Cookie、查詢字串值等時可能出現的問題。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>

## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="7e8a5-249">使用搜尋字建立查詢</span><span class="sxs-lookup"><span data-stu-id="7e8a5-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="7e8a5-250">現在,您已經知道如何獲取使用者輸入的搜索詞,您可以創建使用它的查詢。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="7e8a5-251">請記住,要將所有影片項從資料庫中獲取出來,您使用的是 SQL 查詢,該查詢如下所示:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="7e8a5-252">要僅獲取某些影片,必須使用包含子句的`Where`查詢。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="7e8a5-253">此子句允許您設置查詢返回行的條件。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="7e8a5-254">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="7e8a5-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="7e8a5-255">基本格式為`WHERE column = value`。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="7e8a5-256">除了(`=`大`>`於 )、(小於`<`)、( 不等`<>``<=`於)、( 小於或等於)等之外,還可以使用不同的運算符,具體取決於您要查找的內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="7e8a5-257">如果您想知道,SQL 語句不是大小寫&mdash;`SELECT`敏感`Select`與`select`(或 甚至 ) 相同。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="7e8a5-258">但是,人們通常使用 SQL 語句中的關鍵`SELECT`字`WHERE`( 如和)來使其更易於閱讀。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="7e8a5-259">將搜尋字做參數</span><span class="sxs-lookup"><span data-stu-id="7e8a5-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="7e8a5-260">搜尋特定流派非常簡單 (),`WHERE Genre = 'Action'`但您希望能夠搜尋使用者輸入的任何流派。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="7e8a5-261">為此,您可以創建為 SQL 查詢,其中包含要搜尋的值的占位符。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="7e8a5-262">它會看起來像此指令:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="7e8a5-263">占位元是字元`@`後跟零。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="7e8a5-264">正如您可能猜到的,查詢可以包含多個占位符,並且它們將命名為`@0``@1``@2`、、、、、、、、、、、、、、 它們。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="7e8a5-265">要設置查詢並實際傳遞該值,請使用如下所示的代碼:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="7e8a5-266">此代碼類似於您為在網格中顯示數據所做的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="7e8a5-267">唯一的區別是:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-267">The only differences are:</span></span>

- <span data-ttu-id="7e8a5-268">查詢包含佔位元`WHERE Genre = @0"`( 。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="7e8a5-269">查詢被放入變數 (`selectCommand`;之前,您將查詢直接傳遞給`db.Query`方法 。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="7e8a5-270">調用`db.Query`方法時,將傳遞查詢和要用於占位符的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="7e8a5-271">(如果查詢有多個占位符,則將它們全部作為單獨的值傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="7e8a5-272">如果將所有這些元素放在一起,您將獲得以下代碼:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="7e8a5-273">**重要!**</span><span class="sxs-lookup"><span data-stu-id="7e8a5-273">**Important!**</span></span> <span data-ttu-id="7e8a5-274">使用佔位元`@0`(如 ) 將數值傳給 SQL 指令對於安全性*至關重要*。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="7e8a5-275">此處檢視的方式(使用變數數據的占位符)是建構 SQL 命令的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="7e8a5-276">切勿通過將從用戶獲得的文本和值組合(串聯)來建構 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="7e8a5-277">將使用者輸入串聯到 SQL 語句中會將您的網站置於*SQL 注入攻擊*中,惡意使用者向您的頁面提交入侵資料庫的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="7e8a5-278">(您可以在文章[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 網站中閱讀更多內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>

## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="7e8a5-279">使用搜尋程式碼更新電影頁面</span><span class="sxs-lookup"><span data-stu-id="7e8a5-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="7e8a5-280">現在,您可以更新 *「電影.cshtml」* 檔案中的代碼。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="7e8a5-281">首先,用以下代碼取代頁面頂部的代碼塊中的代碼:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="7e8a5-282">此處的區別是,您已將查詢放入變數中`selectCommand`,稍後將傳遞給`db.Query`該變數。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="7e8a5-283">將 SQL 語句放入變數中可以更改語句,這是執行搜索時執行的操作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="7e8a5-284">您還刪除了這兩行,稍後將重新放入:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="7e8a5-285">您還不想運行查詢(即呼叫`db.Query`),並且也不想初始`WebGrid`化 幫助程式。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="7e8a5-286">在找出必須運行哪些 SQL 語句後,您將執行這些操作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="7e8a5-287">重寫此塊后,可以添加新邏輯來處理搜索。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="7e8a5-288">已完成的代碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-288">The completed code will look like the following.</span></span> <span data-ttu-id="7e8a5-289">更新頁面中的代碼,使其與此範例符合:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="7e8a5-290">頁面現在像這樣工作。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-290">The page now works like this.</span></span> <span data-ttu-id="7e8a5-291">每次執行頁面時,代碼都會打開資料庫,`selectCommand`變數將設置為 SQL 語句,該語`Movies`句從 表中獲取所有記錄。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="7e8a5-292">代碼還會初始化`searchTerm`變數。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="7e8a5-293">但是,如果當前請求包含`searchGenre`元素的值,則代碼將`selectCommand`設置 為不同的查詢,即包含用於搜索`Where`流派的子句。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="7e8a5-294">它還設置`searchTerm`到搜索框傳遞的一切(可能什麼都不)。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="7e8a5-295">無論 SQL 語`selectCommand`句在 中哪個`db.Query`,代碼都會調用以運行查詢,`searchTerm`將其傳遞給 中的任何內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="7e8a5-296">如果`searchTerm`沒有任何內容,則無關緊要,因為在這種情況下,沒有參數可以無論如何將值傳遞給`selectCommand`。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="7e8a5-297">最後,程式碼使用查詢結果初始`WebGrid`化 説明程式,就像以前一樣。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="7e8a5-298">您可以看到,通過將 SQL 語句和搜索詞放入變數中,增加了代碼的靈活性。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="7e8a5-299">正如本教程稍後將看到的那樣,您可以使用此基本框架,並繼續為不同類型的搜索添加邏輯。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="7e8a5-300">測試依類型搜尋功能</span><span class="sxs-lookup"><span data-stu-id="7e8a5-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="7e8a5-301">在 WebMatrix 中,執行 *「電影.cshtml」* 頁。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="7e8a5-302">您將看到帶有流派文字框的頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="7e8a5-303">輸入您為其中一個測試記錄輸入的流派,然後單擊 **「搜索**」。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="7e8a5-304">這一次,你看到一個清單,只是電影匹配該流派:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-304">This time you see a listing of just the movies that match that genre:</span></span>

![電影頁面清單後搜索流派"喜劇"](form-basics/_static/image4.png)

<span data-ttu-id="7e8a5-306">輸入其他流派並再次搜索。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-306">Enter a different genre and search again.</span></span> <span data-ttu-id="7e8a5-307">嘗試使用所有小寫或所有大寫字母輸入流派,以便您可以看到搜索不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="7e8a5-308">"記住"使用者輸入的內容</span><span class="sxs-lookup"><span data-stu-id="7e8a5-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="7e8a5-309">您可能已經注意到,在您輸入一個流派並按一下**搜索流派**後,您看到了該流派的清單。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="7e8a5-310">但是,搜索文字框換句話說是&mdash;空的,它不記得您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="7e8a5-311">瞭解此行為發生的原因非常重要。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="7e8a5-312">提交頁面時,瀏覽器會向 Web 伺服器發送請求。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="7e8a5-313">當ASP.NET收到請求時,它會創建頁面的全新實例,在其中運行代碼,然後將頁面再次呈現給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="7e8a5-314">實際上,該頁面不知道您只是使用自身的早期版本。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="7e8a5-315">它只知道,它得到了一個請求,其中有一些表單數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="7e8a5-316">每次請求頁面時,無論是&mdash;首次請求還是提交&mdash;頁面 ,您都會獲得新頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="7e8a5-317">Web 伺服器沒有您上次請求的記憶體。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="7e8a5-318">瀏覽器也不ASP.NET,瀏覽器也不ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="7e8a5-319">頁面的這些單獨實例之間的唯一連接是您在它們之間傳輸的任何數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="7e8a5-320">例如,如果提交頁面,則新頁面實例可以獲取前一個實例發送的表單數據。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="7e8a5-321">(在頁面之間傳遞數據的另一種方法是使用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="7e8a5-322">描述此選項的一個正式方法是說網頁是*無狀態的*。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="7e8a5-323">Web 伺服器和頁面本身以及頁面中的元素不保留有關頁面以前狀態的任何資訊。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="7e8a5-324">Web 之所以以這種方式設計,是因為維護單個請求的狀態會迅速耗盡 Web 伺服器的資源,而 Web 伺服器通常每秒處理數千甚至數十萬個請求。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="7e8a5-325">因此,文本框為空的原因。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-325">So that's why the text box was empty.</span></span> <span data-ttu-id="7e8a5-326">提交頁面後,ASP.NET創建了該頁的新實例,並運行了代碼和標記。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="7e8a5-327">該代碼中沒有任何內容告訴ASP.NET在文字框中輸入值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="7e8a5-328">因此ASP.NET什麼都沒做,文本框呈現時沒有值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="7e8a5-329">實際上,有一個簡單的方法來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="7e8a5-330">您在文字框中輸入的流派*可在*文字框中的&mdash;代碼`Request.QueryString["searchGenre"]`中 使用。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="7e8a5-331">更新文字框的標記,以便`value`屬性從`searchTerm`獲取 其值,如下所示:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="7e8a5-332">在此頁中`value`,還可以將屬性設置`searchTerm`為 變數,因為該變數還包含您輸入的流派。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="7e8a5-333">但是,`Request`使用 物件設置如下`value`所示 的屬性是完成此任務的標準方法。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="7e8a5-334">(假設在某些情況下甚至想要執行此操作&mdash;,則可能需要呈現*沒有*欄位中值的頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="7e8a5-335">這完全取決於你的應用發生了什麼。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="7e8a5-336">您無法「記住」用於密碼的文字框的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="7e8a5-337">使用代碼允許人們填寫密碼欄位是一個安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>

<span data-ttu-id="7e8a5-338">重新執行頁面,輸入流派,然後按一次**搜尋流派**。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="7e8a5-339">這一次,您不僅看到搜尋結果,而且文字框會記住您上次輸入的內容:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![顯示文字盒已記住上一個項目](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="7e8a5-341">搜尋任何單字</span><span class="sxs-lookup"><span data-stu-id="7e8a5-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="7e8a5-342">您現在可以搜尋任何流派,但您可能還需要搜索標題。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="7e8a5-343">搜尋時很難完全正確獲取標題,因此您可以搜尋標題內任何位置的單詞。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="7e8a5-344">在 SQL 中執行此`LIKE`操作, 請使用運算子和語法,如下所示:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="7e8a5-345">此命令獲取其標題包含"冒險"的所有影片。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="7e8a5-346">使用運算子時,`LIKE`將通配符`%`作為搜尋詞的一部分。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="7e8a5-347">搜索`LIKE 'adventure%'`意味著"從'冒險'開始"。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="7e8a5-348">(從技術上講,它意味著"字串'冒險'後跟任何東西。同樣,搜索詞`LIKE '%adventure'`的意思是"任何後面跟著字串'冒險'",這是另一種方式說"以『冒險』結束"。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="7e8a5-349">因此,搜索`LIKE '%adventure%'`詞表示"與標題中的任何位置都具有『冒險性』」。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="7e8a5-350">(從技術上講,"標題中的任何內容,然後是'冒險',然後是任何東西。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="7e8a5-351">在元素`<form>`中,在流派搜尋的`</div>`關閉 標籤下方添加以下標記(就在`</form>`結束 元素之前):</span><span class="sxs-lookup"><span data-stu-id="7e8a5-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="7e8a5-352">處理此搜尋的代碼與流派搜索的代碼類似,只不過您必須組裝`LIKE`搜索。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="7e8a5-353">在頁面頂部的代碼塊中,在串流派`if``if`搜尋 的區塊之後添加此塊:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="7e8a5-354">此代碼使用之前看到的相同邏輯,只不過搜索使用`LIKE`運算符,並且代碼在搜索詞之前和之後放置""。`%`</span><span class="sxs-lookup"><span data-stu-id="7e8a5-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="7e8a5-355">請注意如何輕鬆地向頁面添加另一個搜索。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="7e8a5-356">你所要做的就是:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-356">All you had to do was:</span></span>

- <span data-ttu-id="7e8a5-357">創建測試`if`的塊以查看相關搜尋框是否具有值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="7e8a5-358">將`selectCommand`變數設置為新的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="7e8a5-359">將`searchTerm`變數設置為要傳遞給查詢的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="7e8a5-360">下面是完整的代碼塊,其中包含標題搜索的新邏輯:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="7e8a5-361">以下是此程式碼的功能摘要：</span><span class="sxs-lookup"><span data-stu-id="7e8a5-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="7e8a5-362">變數`searchTerm`和`selectCommand`在頂部初始化。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="7e8a5-363">您將根據使用者在頁面中所做的操作將這些變數設置為相應的搜索詞(如果有)和相應的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="7e8a5-364">默認搜索是從資料庫中獲取所有影片的簡單示例。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="7e8a5-365">在和`searchGenre``searchTitle`的測試中,代碼將`searchTerm`設置到要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="7e8a5-366">這些代碼塊還設置為`selectCommand`該搜索的相應 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="7e8a5-367">該方法`db.Query`僅調用一次,使用`selectedCommand`中的任何 SQL`searchTerm`命令和 中的任何值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="7e8a5-368">如果沒有搜索詞(沒有流派,沒有標題詞),則值`searchTerm`為空字串。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="7e8a5-369">但是,這並不重要,因為在這種情況下,查詢不需要參數。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="7e8a5-370">測試標題搜尋功能</span><span class="sxs-lookup"><span data-stu-id="7e8a5-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="7e8a5-371">現在,您可以測試已完成的搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-371">Now you can test your completed search page.</span></span> <span data-ttu-id="7e8a5-372">執行*電影.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7e8a5-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="7e8a5-373">輸入流派,然後單擊**搜尋流派**。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="7e8a5-374">網格顯示該流派的電影,就像以前一樣。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="7e8a5-375">輸入標題字,然後單擊 **「搜索標題**」。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="7e8a5-376">網格顯示標題中具有該單詞的電影。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-376">The grid displays movies that have that word in the title.</span></span>

![在標題中搜尋「The」後的電影頁面清單](form-basics/_static/image6.png)

<span data-ttu-id="7e8a5-378">將兩個文字框留空,然後按一下任一按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="7e8a5-379">網格顯示所有影片。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="7e8a5-380">組合查詢</span><span class="sxs-lookup"><span data-stu-id="7e8a5-380">Combining the Queries</span></span>

<span data-ttu-id="7e8a5-381">您可能會注意到,您可以執行的搜索是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="7e8a5-382">不能同時搜索標題和流派,即使兩個搜索框中都有值。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="7e8a5-383">例如,您無法搜尋標題包含「冒險」的所有動作影片。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="7e8a5-384">(現在對頁面進行編碼時,如果同時輸入流派和標題的值,則標題搜索將優先。要建立結合條件的搜索,必須創建具有如下語法的 SQL 查詢:</span><span class="sxs-lookup"><span data-stu-id="7e8a5-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="7e8a5-385">您必須使用如下語句來執行查詢(大致而言):</span><span class="sxs-lookup"><span data-stu-id="7e8a5-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="7e8a5-386">如您所見,創建邏輯以允許搜索條件的許多排列,可能會涉及一些內容。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="7e8a5-387">因此,我們將在這裡停留。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="7e8a5-388">下一步</span><span class="sxs-lookup"><span data-stu-id="7e8a5-388">Coming Up Next</span></span>

<span data-ttu-id="7e8a5-389">在下一教學中,您將創建一個頁面,該頁面使用窗體允許使用者向資料庫添加影片。</span><span class="sxs-lookup"><span data-stu-id="7e8a5-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="7e8a5-390">影片頁面的完整清單(透過搜尋更新)</span><span class="sxs-lookup"><span data-stu-id="7e8a5-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="7e8a5-391">其他資源</span><span class="sxs-lookup"><span data-stu-id="7e8a5-391">Additional Resources</span></span>

- [<span data-ttu-id="7e8a5-392">使用 Razor 語法進行 ASP.NET 網頁程式設計簡介</span><span class="sxs-lookup"><span data-stu-id="7e8a5-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="7e8a5-393">W3學校網站上的[SQL WHERE 條款](http://www.w3schools.com/sql/sql_where.asp)</span><span class="sxs-lookup"><span data-stu-id="7e8a5-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="7e8a5-394">[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 網站上的文章</span><span class="sxs-lookup"><span data-stu-id="7e8a5-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7e8a5-395">[前一個](displaying-data.md)
> [下一個](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="7e8a5-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>
