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
# <a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="c5496-104">簡介 ASP.NET Web Pages-HTML 表單基本概念</span><span class="sxs-lookup"><span data-stu-id="c5496-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>

<span data-ttu-id="c5496-105"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c5496-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c5496-106">本教學課程將說明如何建立輸入表單的基本概念，以及當您使用 ASP.NET Web Pages (Razor) 時如何處理使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="c5496-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="c5496-107">現在您已經有資料庫，您將使用您的表單技能，讓使用者在資料庫中尋找特定的電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="c5496-108">它會假設您已完成 [使用 ASP.NET Web Pages 顯示資料的簡介](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。</span><span class="sxs-lookup"><span data-stu-id="c5496-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="c5496-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="c5496-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="c5496-110">如何使用標準 HTML 元素建立表單。</span><span class="sxs-lookup"><span data-stu-id="c5496-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="c5496-111">如何在表單中讀取使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="c5496-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="c5496-112">如何建立 SQL 查詢，以選擇性地使用使用者提供的搜尋字詞來取得資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="c5496-113">如何讓頁面中的欄位「記住」使用者輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="c5496-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="c5496-114">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="c5496-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="c5496-115">`Request` 物件。</span><span class="sxs-lookup"><span data-stu-id="c5496-115">The `Request` object.</span></span>
> - <span data-ttu-id="c5496-116">SQL `Where` 子句。</span><span class="sxs-lookup"><span data-stu-id="c5496-116">The SQL `Where` clause.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="c5496-117">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="c5496-117">What You'll Build</span></span>

<span data-ttu-id="c5496-118">在上一個教學課程中，您已建立資料庫、將資料新增至其中，然後使用 `WebGrid` helper 來顯示資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="c5496-119">在本教學課程中，您將新增搜尋方塊，讓您尋找特定內容類型或其標題包含您所輸入之任何單字的電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="c5496-120"> (例如，您將能夠找到類型為 "Action" 或標題包含 "Harry" 或 "艾德" 的所有電影。) </span><span class="sxs-lookup"><span data-stu-id="c5496-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="c5496-121">當您完成本教學課程時，您將會看到如下的頁面：</span><span class="sxs-lookup"><span data-stu-id="c5496-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![具有內容類型與標題搜尋的電影頁面](form-basics/_static/image1.png)

<span data-ttu-id="c5496-123">頁面的清單部分與最後一個教學課程中的 &mdash; 方格相同。</span><span class="sxs-lookup"><span data-stu-id="c5496-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="c5496-124">差別在於，方格只會顯示您搜尋的電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="c5496-125">關於 HTML 表單</span><span class="sxs-lookup"><span data-stu-id="c5496-125">About HTML Forms</span></span>

<span data-ttu-id="c5496-126"> (如果您有建立 HTML 表單的經驗，以及與之間的 `GET` 差異 `POST` ，您可以略過本節。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="c5496-127">表單具有使用者輸入元素 &mdash; 、按鈕、選項按鈕、核取方塊、下拉式清單等等。</span><span class="sxs-lookup"><span data-stu-id="c5496-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="c5496-128">使用者會填入這些控制項或進行選取，然後按一下按鈕來提交表單。</span><span class="sxs-lookup"><span data-stu-id="c5496-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="c5496-129">此範例說明表單的基本 HTML 語法：</span><span class="sxs-lookup"><span data-stu-id="c5496-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="c5496-130">當此標記在頁面中執行時，它會建立如下圖所示的簡單表單：</span><span class="sxs-lookup"><span data-stu-id="c5496-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![在瀏覽器中呈現的基本 HTML 表單](form-basics/_static/image2.png)

<span data-ttu-id="c5496-132">`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="c5496-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="c5496-133"> (一個容易犯的錯誤，就是將專案加入至頁面，但忘了將它們放在 `<form>` 元素內。</span><span class="sxs-lookup"><span data-stu-id="c5496-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="c5496-134">在此情況下，不會提交任何專案。 ) `method` 屬性會告知瀏覽器如何提交使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="c5496-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="c5496-135">如果您是在伺服器上執行更新，請將此設定為， `post` `get` 如果您只是從伺服器提取資料，則設定為。</span><span class="sxs-lookup"><span data-stu-id="c5496-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="c5496-136">**GET、POST 和 HTTP 動詞命令安全**</span><span class="sxs-lookup"><span data-stu-id="c5496-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="c5496-137">HTTP 是瀏覽器和伺服器用來交換資訊的通訊協定，在其基本作業中非常簡單。</span><span class="sxs-lookup"><span data-stu-id="c5496-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="c5496-138">瀏覽器只會使用幾個動詞命令對伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="c5496-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="c5496-139">當您撰寫 web 的程式碼時，瞭解這些動詞以及瀏覽器和伺服器如何使用它們會很有説明。</span><span class="sxs-lookup"><span data-stu-id="c5496-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="c5496-140">目前最常使用的動詞是：</span><span class="sxs-lookup"><span data-stu-id="c5496-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="c5496-141">`GET`.</span><span class="sxs-lookup"><span data-stu-id="c5496-141">`GET`.</span></span> <span data-ttu-id="c5496-142">瀏覽器會使用此動詞命令從伺服器提取某個東西。</span><span class="sxs-lookup"><span data-stu-id="c5496-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="c5496-143">例如，當您在瀏覽器中輸入 URL 時，瀏覽器會執行 `GET` 操作來要求您想要的頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="c5496-144">如果頁面包含圖形，則瀏覽器會執行其他 `GET` 作業來取得影像。</span><span class="sxs-lookup"><span data-stu-id="c5496-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="c5496-145">如果作業 `GET` 必須將資訊傳遞至伺服器，則會在查詢字串中將資訊當作 URL 的一部分來傳遞。</span><span class="sxs-lookup"><span data-stu-id="c5496-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="c5496-146">`POST`.</span><span class="sxs-lookup"><span data-stu-id="c5496-146">`POST`.</span></span> <span data-ttu-id="c5496-147">瀏覽器會傳送 `POST` 要求，以便提交要在伺服器上新增或變更的資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="c5496-148">例如， `POST` 使用動詞來建立資料庫中的記錄，或是變更現有的記錄。</span><span class="sxs-lookup"><span data-stu-id="c5496-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="c5496-149">在大部分的情況下，當您填寫表單，然後按一下 [提交] 按鈕時，瀏覽器會執行 `POST` 操作。</span><span class="sxs-lookup"><span data-stu-id="c5496-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="c5496-150">在作業中 `POST` ，傳遞至伺服器的資料會在頁面主體中。</span><span class="sxs-lookup"><span data-stu-id="c5496-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="c5496-151">這些動詞的重要差異在於，作業 `GET` 不應該變更伺服器上的任何資訊，或將它以稍微更抽象的方式進行，而 `GET` 不會導致伺服器上的狀態變更。</span><span class="sxs-lookup"><span data-stu-id="c5496-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="c5496-152">您可以視需要 `GET` 在相同的資源上執行一次作業，而且這些資源不會變更。</span><span class="sxs-lookup"><span data-stu-id="c5496-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="c5496-153"> (作業 `GET` 通常稱為「安全」，或使用技術詞彙，是 *等冪*的。相反地，) 相反地， `POST` 每當您執行作業時，要求就會變更伺服器上的某些內容。</span><span class="sxs-lookup"><span data-stu-id="c5496-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="c5496-154">有兩個範例將有助於說明這種差異。</span><span class="sxs-lookup"><span data-stu-id="c5496-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="c5496-155">當您使用 Bing 或 Google 等引擎來執行搜尋時，您會填入由一個文字方塊所組成的表單，然後按一下 [搜尋] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5496-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="c5496-156">瀏覽器會執行作業 `GET` ，並將您在 URL 中輸入的值輸入至該方塊。</span><span class="sxs-lookup"><span data-stu-id="c5496-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="c5496-157">`GET`針對此類型的表單使用作業是正常的，因為搜尋作業不會變更伺服器上的任何資源，而只會提取資訊。</span><span class="sxs-lookup"><span data-stu-id="c5496-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="c5496-158">現在請考慮在線上排序某個東西的流程。</span><span class="sxs-lookup"><span data-stu-id="c5496-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="c5496-159">填寫訂單詳細資料，然後按一下 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5496-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="c5496-160">這項作業將會是 `POST` 要求，因為此作業會導致伺服器上的變更，例如新的訂單記錄、您的帳戶資訊變更，還有其他許多變更。</span><span class="sxs-lookup"><span data-stu-id="c5496-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="c5496-161">與作業不同的是 `GET` ，您不能重複 `POST` 要求，如果您這樣做，每次重新提交要求時，就會在伺服器上產生新的訂單。</span><span class="sxs-lookup"><span data-stu-id="c5496-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="c5496-162"> (在這種情況下，網站通常會警告您不要按一次 [提交] 按鈕，或停用 [提交] 按鈕，讓您不會意外重新提交表單。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="c5496-163">在本教學課程的過程中，您將使用 `GET` `POST` 作業和作業來處理 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="c5496-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="c5496-164">在每個案例中，我們將說明您所使用的動詞為何是適當的。</span><span class="sxs-lookup"><span data-stu-id="c5496-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="c5496-165"> (若要深入瞭解 HTTP 動詞命令，請參閱 W3C 網站上的 [方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) 文章。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>

<span data-ttu-id="c5496-166">大部分的使用者輸入元素都是 HTML `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="c5496-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="c5496-167">它們看起來像 `<input type="type" name="name">,` 是 *型* 別指出您想要的使用者輸入控制項種類。</span><span class="sxs-lookup"><span data-stu-id="c5496-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="c5496-168">這些是常見的元素：</span><span class="sxs-lookup"><span data-stu-id="c5496-168">These elements are the common ones:</span></span>

- <span data-ttu-id="c5496-169">文字方塊： `<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="c5496-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="c5496-170">核取方塊： `<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="c5496-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="c5496-171">選項按鈕： `<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="c5496-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="c5496-172">按鈕： `<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="c5496-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="c5496-173">提交按鈕： `<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="c5496-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="c5496-174">您也可以使用專案 `<textarea>` 來建立多行文字方塊，並使用 `<select>` 元素來建立下拉式清單或可滾動清單。</span><span class="sxs-lookup"><span data-stu-id="c5496-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="c5496-175"> (需 HTML form 元素的詳細資訊，請參閱 W3Schools 網站上的 [Html 表單和輸入](http://www.w3schools.com/html/html_forms.asp) 。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="c5496-176">`name`屬性非常重要，因為名稱會是您稍後將如何取得元素值的方式，如您稍後所見。</span><span class="sxs-lookup"><span data-stu-id="c5496-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="c5496-177">有趣的部分就是您的網頁開發人員與使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="c5496-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="c5496-178">沒有與這些元素相關聯的內建行為。</span><span class="sxs-lookup"><span data-stu-id="c5496-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="c5496-179">相反地，您必須取得使用者輸入或選取的值，並對其進行一些動作。</span><span class="sxs-lookup"><span data-stu-id="c5496-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="c5496-180">這就是您將在本教學課程中學習的內容。</span><span class="sxs-lookup"><span data-stu-id="c5496-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="c5496-181">**HTML5 和輸入表單**</span><span class="sxs-lookup"><span data-stu-id="c5496-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="c5496-182">您可能已經知道，HTML 正在轉換，而最新版本 (HTML5) 包含可讓使用者以更直覺的方式輸入資訊的支援。</span><span class="sxs-lookup"><span data-stu-id="c5496-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="c5496-183">例如，在 HTML5 中，您 (網頁開發人員) 可以告訴網頁您希望使用者輸入日期。</span><span class="sxs-lookup"><span data-stu-id="c5496-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="c5496-184">然後，瀏覽器就可以自動顯示行事曆，而不需要使用者手動輸入日期。</span><span class="sxs-lookup"><span data-stu-id="c5496-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="c5496-185">不過，HTML5 是新的，但在所有瀏覽器中都不受支援。</span><span class="sxs-lookup"><span data-stu-id="c5496-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="c5496-186">ASP.NET Web Pages 支援 HTML5 輸入至使用者瀏覽器的範圍。</span><span class="sxs-lookup"><span data-stu-id="c5496-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="c5496-187">若要瞭解 HTML5 中元素的新屬性 `<input>` ，請參閱 W3Schools 網站上的 [HTML &lt; 輸入 &gt; 類型屬性](http://www.w3schools.com/html/html_form_input_types.asp) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>

## <a name="creating-the-form"></a><span data-ttu-id="c5496-188">建立表單</span><span class="sxs-lookup"><span data-stu-id="c5496-188">Creating the Form</span></span>

<span data-ttu-id="c5496-189">在 WebMatrix 的 [檔案] **工作區中，開啟 [** *電影. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="c5496-190">在結束記號之後， `</h1>` 以及呼叫的開頭 `<div>` 標記之前 `grid.GetHtml` ，加入下列標記：</span><span class="sxs-lookup"><span data-stu-id="c5496-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="c5496-191">此標記會建立表單，其中包含名為的文字方塊 `searchGenre` 和提交按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5496-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="c5496-192">[文字方塊] 和 [提交] 按鈕會包含在 `<form>` `method` 屬性設為的專案中 `get` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="c5496-193"> (別忘了，如果您未在專案內放置文字方塊和送出按鈕 `<form>` ，當您按一下按鈕時，就不會送出任何專案。 ) 您使用這裡的動詞，是 `GET` 因為您要建立的表單不會在伺服器上進行任何變更，所以只會產生搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="c5496-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="c5496-194"> (在上一個教學課程中，您使用了 `post` 方法，也就是您將變更提交至伺服器的方式。</span><span class="sxs-lookup"><span data-stu-id="c5496-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="c5496-195">在下一個教學課程中，您將會再次看到。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="c5496-196">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-196">Run the page.</span></span> <span data-ttu-id="c5496-197">雖然您尚未為表單定義任何行為，但您可以看到它的樣子：</span><span class="sxs-lookup"><span data-stu-id="c5496-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![具有內容類型搜尋方塊的電影頁面](form-basics/_static/image3.png)

<span data-ttu-id="c5496-199">在文字方塊中輸入值，例如 "喜劇"。</span><span class="sxs-lookup"><span data-stu-id="c5496-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="c5496-200">然後按一下 [ **搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="c5496-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="c5496-201">記下頁面的 URL。</span><span class="sxs-lookup"><span data-stu-id="c5496-201">Take note of the URL of the page.</span></span> <span data-ttu-id="c5496-202">因為您將專案 `<form>` 的 `method` 屬性設定為 `get` ，所以您輸入的值現在是 URL 中查詢字串的一部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5496-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="c5496-203">讀取表單值</span><span class="sxs-lookup"><span data-stu-id="c5496-203">Reading Form Values</span></span>

<span data-ttu-id="c5496-204">此頁面已經包含一些可取得資料庫資料的程式碼，並在方格中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="c5496-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="c5496-205">現在您必須新增一些程式碼來讀取文字方塊的值，以便執行包含搜尋詞彙的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="c5496-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="c5496-206">因為您將表單的方法設定為 `get` ，所以您可以使用類似下列的程式碼來讀取在文字方塊中輸入的值：</span><span class="sxs-lookup"><span data-stu-id="c5496-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="c5496-207">物件 `Request.QueryString` (物件的 `QueryString` 屬性) 包含在作業中 `Request` 提交的元素值 `GET` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="c5496-208">`Request.QueryString`屬性包含*集合* (在表單中提交值的清單) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="c5496-209">若要取得任何個別值，請指定您想要的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="c5496-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="c5496-210">這就是為什麼您必須在專案 `name` 上擁有屬性， `<input>` (可 `searchTerm` 建立文字方塊的) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="c5496-211"> (如需物件的詳細資訊 `Request` ，請稍後參閱 [側邊欄](#BKMK_TheRequestObject) 。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="c5496-212">它夠簡單，可以讀取文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="c5496-213">但是，如果使用者未在文字方塊中完全輸入任何內容，但是按一下 [ **搜尋** ]，則可以忽略該點，因為沒有任何專案可以搜尋。</span><span class="sxs-lookup"><span data-stu-id="c5496-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="c5496-214">下列程式碼顯示如何執行這些條件的範例。</span><span class="sxs-lookup"><span data-stu-id="c5496-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="c5496-215"> (您還不需要加入此程式碼;您稍後將會這麼做。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="c5496-216">測試會以這種方式細分：</span><span class="sxs-lookup"><span data-stu-id="c5496-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="c5496-217">取得的值，也就 `Request.QueryString["searchGenre"]` 是在名為的元素中輸入的值 `<input>` `searchGenre` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="c5496-218">使用方法瞭解是否為空的 `IsEmpty` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="c5496-219">這個方法是用來判斷是否有某個專案 (的標準方式，) 包含值的表單元素。</span><span class="sxs-lookup"><span data-stu-id="c5496-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="c5496-220">但事實上，您只在意它 *不* 是空的，因此 .。。</span><span class="sxs-lookup"><span data-stu-id="c5496-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="c5496-221">將 `!` 運算子加入 `IsEmpty` 測試前面。</span><span class="sxs-lookup"><span data-stu-id="c5496-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="c5496-222"> (`!` 運算子表示邏輯 NOT) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="c5496-223">在純文字中，整個 `if` 條件會轉譯成下列內容：*如果表單的 searchGenre 元素不是空的，則*.。。</span><span class="sxs-lookup"><span data-stu-id="c5496-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="c5496-224">此區塊會設定用來建立使用搜尋字詞之查詢的階段。</span><span class="sxs-lookup"><span data-stu-id="c5496-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="c5496-225">您將在下一節中執行該動作。</span><span class="sxs-lookup"><span data-stu-id="c5496-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="c5496-226">**Request 物件**</span><span class="sxs-lookup"><span data-stu-id="c5496-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="c5496-227">`Request`物件包含當要求或提交頁面時，瀏覽器傳送至應用程式的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="c5496-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="c5496-228">此物件包含使用者提供的任何資訊，例如文字方塊值或要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5496-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="c5496-229">它也包含各種額外的資訊，例如 cookie、URL 查詢字串中的值 (如果有任何) 、正在執行之頁面的檔案路徑、使用者使用的瀏覽器類型、在瀏覽器中設定的語言清單等等。</span><span class="sxs-lookup"><span data-stu-id="c5496-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="c5496-230">`Request`物件是值的*集合* (清單) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="c5496-231">您可以藉由指定名稱，從集合中取得個別的值：</span><span class="sxs-lookup"><span data-stu-id="c5496-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="c5496-232">`Request`物件實際上會公開數個子集。</span><span class="sxs-lookup"><span data-stu-id="c5496-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="c5496-233">例如：</span><span class="sxs-lookup"><span data-stu-id="c5496-233">For example:</span></span>
> 
> - <span data-ttu-id="c5496-234">`Request.Form``<form>`如果要求是要求，則提供來自已提交專案內元素的值 `POST` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="c5496-235">`Request.QueryString` 只提供 URL 查詢字串中的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="c5496-236"> (在類似的 URL 中 `http://mysite/myapp/page?searchGenre=action&page=2` ， `?searchGenre=action&page=2` url 的區段是查詢字串。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="c5496-237">`Request.Cookies` 集合可讓您存取瀏覽器已傳送的 cookie。</span><span class="sxs-lookup"><span data-stu-id="c5496-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="c5496-238">若要取得您知道已提交表單中的值，您可以使用 `Request["name"]` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="c5496-239">或者，您可以使用 `Request.Form["name"]` (針對 `POST` 要求) 或 `Request.QueryString["name"]` (`GET`) 要求的特定版本。</span><span class="sxs-lookup"><span data-stu-id="c5496-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="c5496-240">當然， *name* 是要取得之專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="c5496-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="c5496-241">您要取得之專案的名稱在您所使用的集合中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c5496-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="c5496-242">這就是 `Request` 物件提供的子集，例如 `Request.Form` 和 `Request.QueryString` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="c5496-243">假設您的頁面包含名為的 form 元素 `userName` ，而且 *也* 包含名為的 cookie `userName` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="c5496-244">如果您 `Request["userName"]` 想要的話，就不會看到表單值或 cookie。</span><span class="sxs-lookup"><span data-stu-id="c5496-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="c5496-245">但是，如果您取得 `Request.Form["userName"]` 或 `Request.Cookie["userName"]` ，就會明確瞭解要取得的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="c5496-246">使用 `Request` 您感興趣的子集（例如或）是很好的作法 `Request.Form` `Request.QueryString` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="c5496-247">針對您在本教學課程中建立的簡單頁面，它可能不會真正產生任何差異。</span><span class="sxs-lookup"><span data-stu-id="c5496-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="c5496-248">不過，當您建立更複雜的頁面時，使用明確版本 `Request.Form` 或 `Request.QueryString` 可協助您避免頁面包含表單 (或多個表單) 、cookie、查詢字串值等時可能發生的問題。</span><span class="sxs-lookup"><span data-stu-id="c5496-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>

## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="c5496-249">使用搜尋字詞建立查詢</span><span class="sxs-lookup"><span data-stu-id="c5496-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="c5496-250">既然您已經知道如何取得使用者所輸入的搜尋字詞，就可以建立使用它的查詢。</span><span class="sxs-lookup"><span data-stu-id="c5496-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="c5496-251">請記住，若要從資料庫中取得所有電影專案，您會使用類似下列語句的 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="c5496-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="c5496-252">若只要取得特定電影，您必須使用包含子句的查詢 `Where` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="c5496-253">此子句可讓您設定查詢所傳回之資料列的條件。</span><span class="sxs-lookup"><span data-stu-id="c5496-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="c5496-254">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="c5496-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="c5496-255">基本格式為 `WHERE column = value` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="c5496-256">您可以使用不同的運算子 `=` ，例如 `>` (大於) 、 `<` (小於) 、 `<>` (不等於) 、 `<=` (小於或等於) 等，視您要尋找的內容而定。</span><span class="sxs-lookup"><span data-stu-id="c5496-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="c5496-257">如果您想知道，SQL 語句不區分大小寫，與 &mdash; `SELECT` `Select` (或甚至 `select`) 相同。</span><span class="sxs-lookup"><span data-stu-id="c5496-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="c5496-258">不過，使用者通常會將 SQL 語句中的關鍵字大寫，例如 `SELECT` 和 `WHERE` ，以便更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="c5496-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="c5496-259">傳遞搜尋詞彙作為參數</span><span class="sxs-lookup"><span data-stu-id="c5496-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="c5496-260">搜尋特定的類型很容易 (`WHERE Genre = 'Action'`) ，但是您想要能夠搜尋使用者輸入的任何內容類型。</span><span class="sxs-lookup"><span data-stu-id="c5496-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="c5496-261">若要這樣做，您可以建立 SQL 查詢，其中包含要搜尋之值的預留位置。</span><span class="sxs-lookup"><span data-stu-id="c5496-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="c5496-262">它看起來會像這個命令：</span><span class="sxs-lookup"><span data-stu-id="c5496-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="c5496-263">預留位置是 `@` 後面接著零的字元。</span><span class="sxs-lookup"><span data-stu-id="c5496-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="c5496-264">您可能會猜到，查詢可能包含多個預留位置，而且會命名為 `@0` 、、等等 `@1` `@2` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="c5496-265">若要設定查詢並實際將該值傳遞給它，您可以使用如下所示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="c5496-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="c5496-266">這段程式碼與您在方格中顯示資料所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="c5496-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="c5496-267">唯一的差異如下：</span><span class="sxs-lookup"><span data-stu-id="c5496-267">The only differences are:</span></span>

- <span data-ttu-id="c5496-268">查詢包含 () 的預留位置 `WHERE Genre = @0"` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="c5496-269">查詢會放入變數 (`selectCommand`) ; 之前，您會將查詢直接傳遞給 `db.Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="c5496-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="c5496-270">當您呼叫 `db.Query` 方法時，會傳遞查詢和值以用於預留位置。</span><span class="sxs-lookup"><span data-stu-id="c5496-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="c5496-271"> (如果查詢有多個預留位置，您會將它們全部作為個別值傳遞給方法。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="c5496-272">如果您將這些專案全部放在一起，您會得到下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c5496-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="c5496-273">**重要！**</span><span class="sxs-lookup"><span data-stu-id="c5496-273">**Important!**</span></span> <span data-ttu-id="c5496-274">使用預留位置 (例如 `@0`) 將值傳遞給 SQL 命令對安全性而言 *非常重要* 。</span><span class="sxs-lookup"><span data-stu-id="c5496-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="c5496-275">您在這裡看到的方式（具有變數資料的預留位置）是您應該用來建立 SQL 命令的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="c5496-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="c5496-276">絕對不要建立 SQL 語句，方法是將 (串連) 常值文字和您從使用者取得的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="c5496-277">將使用者輸入串連成 SQL 語句，會將您的網站開啟至 *sql 插入式攻擊* ，惡意使用者將值提交至您的頁面，以攻擊您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="c5496-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="c5496-278"> (您可以在 [SQL 插入](https://msdn.microsoft.com/library/ms161953.aspx) MSDN 網站的文章中閱讀更多內容。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>

## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="c5496-279">使用搜尋程式碼更新電影頁面</span><span class="sxs-lookup"><span data-stu-id="c5496-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="c5496-280">現在您可以更新 *電影* 檔中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c5496-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="c5496-281">若要開始，請將頁面頂端程式碼區塊中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c5496-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="c5496-282">差別在於，您已將查詢放入 `selectCommand` 變數中，以便稍後傳遞給您 `db.Query` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="c5496-283">將 SQL 語句放入變數中，可讓您變更語句，這是執行搜尋所要執行的動作。</span><span class="sxs-lookup"><span data-stu-id="c5496-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="c5496-284">您也移除了這兩行，您稍後會將這些行放回：</span><span class="sxs-lookup"><span data-stu-id="c5496-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="c5496-285">您不想要執行查詢 (也就是呼叫) ， `db.Query` 而且您也不想要初始化 `WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="c5496-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="c5496-286">您將會在找出必須執行的 SQL 語句之後，執行這些動作。</span><span class="sxs-lookup"><span data-stu-id="c5496-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="c5496-287">在這個重寫的區塊之後，您可以新增處理搜尋的邏輯。</span><span class="sxs-lookup"><span data-stu-id="c5496-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="c5496-288">完成的程式碼看起來會如下所示。</span><span class="sxs-lookup"><span data-stu-id="c5496-288">The completed code will look like the following.</span></span> <span data-ttu-id="c5496-289">更新頁面中的程式碼，使其符合此範例：</span><span class="sxs-lookup"><span data-stu-id="c5496-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="c5496-290">頁面現在的運作方式如下。</span><span class="sxs-lookup"><span data-stu-id="c5496-290">The page now works like this.</span></span> <span data-ttu-id="c5496-291">每次頁面執行時，程式碼就會開啟資料庫，並將 `selectCommand` 變數設定為 SQL 語句，以取得資料表中的所有記錄 `Movies` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="c5496-292">程式碼也會初始化 `searchTerm` 變數。</span><span class="sxs-lookup"><span data-stu-id="c5496-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="c5496-293">但是，如果目前的要求包含專案的值 `searchGenre` ，則程式碼會將設定 `selectCommand` 為不同的查詢（也就是包含 `Where` 子句來搜尋內容類型的查詢）。</span><span class="sxs-lookup"><span data-stu-id="c5496-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="c5496-294">它也會設定 `searchTerm` 為搜尋方塊所傳遞的內容 (這可能不) 。</span><span class="sxs-lookup"><span data-stu-id="c5496-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="c5496-295">無論在哪一個 SQL 語句中 `selectCommand` ，程式碼都會呼叫 `db.Query` 來執行查詢，並將它傳遞至其中的任何內容 `searchTerm` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="c5496-296">如果沒有任何專案 `searchTerm` ，則不重要，因為在此情況下，不會有任何參數可將值傳遞給 `selectCommand` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="c5496-297">最後，程式碼會 `WebGrid` 使用查詢結果來初始化 helper，就像之前一樣。</span><span class="sxs-lookup"><span data-stu-id="c5496-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="c5496-298">您可以看到，將 SQL 語句和搜尋詞彙放入變數中，就可以在程式碼中加入彈性。</span><span class="sxs-lookup"><span data-stu-id="c5496-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="c5496-299">您稍後會在本教學課程中看到，您可以使用這個基本架構，並針對不同的搜尋類型繼續新增邏輯。</span><span class="sxs-lookup"><span data-stu-id="c5496-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="c5496-300">測試依類型搜尋的功能</span><span class="sxs-lookup"><span data-stu-id="c5496-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="c5496-301">在 WebMatrix 中，執行 [ *cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="c5496-302">您會看到含有內容類型之文字方塊的頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="c5496-303">輸入您為其中一個測試記錄輸入的內容類型，然後按一下 [ **搜尋**]。</span><span class="sxs-lookup"><span data-stu-id="c5496-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="c5496-304">這次您只會看到符合該內容類型的影片清單：</span><span class="sxs-lookup"><span data-stu-id="c5496-304">This time you see a listing of just the movies that match that genre:</span></span>

![搜尋類型 ' Comedies ' 後的電影頁面清單](form-basics/_static/image4.png)

<span data-ttu-id="c5496-306">輸入不同的內容類型，然後再次搜尋。</span><span class="sxs-lookup"><span data-stu-id="c5496-306">Enter a different genre and search again.</span></span> <span data-ttu-id="c5496-307">請嘗試使用全部小寫或全部大寫字母來輸入內容類型，讓您可以看到搜尋不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="c5496-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="c5496-308">「記住」使用者輸入的內容</span><span class="sxs-lookup"><span data-stu-id="c5496-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="c5496-309">您可能已經注意到，當您輸入內容類型並按一下 [ **搜尋**內容類型] 之後，就會看到該內容類型的清單。</span><span class="sxs-lookup"><span data-stu-id="c5496-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="c5496-310">不過，搜尋文字方塊是空的 &mdash; ，換句話說，它並不記得您輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="c5496-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="c5496-311">請務必瞭解為何會發生這種行為。</span><span class="sxs-lookup"><span data-stu-id="c5496-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="c5496-312">當您提交頁面時，瀏覽器會將要求傳送至 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c5496-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="c5496-313">當 ASP.NET 取得要求時，它會建立頁面的全新實例、在其中執行程式碼，然後再次將頁面轉譯至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c5496-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="c5496-314">但實際上，頁面並不知道您是使用舊版本身。</span><span class="sxs-lookup"><span data-stu-id="c5496-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="c5496-315">所有的 it 都知道，它收到的要求中有一些表單資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="c5496-316">每次您第一次要求頁面時， &mdash; 或提交該頁面時， &mdash; 您都會收到新的頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="c5496-317">Web 服務器沒有您最後一個要求的記憶體。</span><span class="sxs-lookup"><span data-stu-id="c5496-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="c5496-318">兩者都不會 ASP.NET，瀏覽器也不會執行。</span><span class="sxs-lookup"><span data-stu-id="c5496-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="c5496-319">這兩個頁面的個別實例之間的唯一連接，就是您在它們之間傳輸的任何資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="c5496-320">例如，如果您提交頁面，新的頁面實例可以取得先前實例所傳送的表單資料。</span><span class="sxs-lookup"><span data-stu-id="c5496-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="c5496-321"> (在頁面之間傳遞資料的另一種方式是使用 cookie。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="c5496-322">描述這種情況的正式方式是說，網頁是 *無狀態*的。</span><span class="sxs-lookup"><span data-stu-id="c5496-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="c5496-323">網頁伺服器和頁面本身以及頁面中的專案，並不會維護頁面先前狀態的任何相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c5496-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="c5496-324">這是以這種方式設計的，因為維護個別要求的狀態時，可能會很快耗盡 web 伺服器的資源，而這通常會處理數千個（甚至是每秒數十萬個要求）。</span><span class="sxs-lookup"><span data-stu-id="c5496-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="c5496-325">這就是為什麼文字方塊是空的。</span><span class="sxs-lookup"><span data-stu-id="c5496-325">So that's why the text box was empty.</span></span> <span data-ttu-id="c5496-326">送出頁面之後，ASP.NET 就會建立新的網頁實例，並執行程式碼和標記。</span><span class="sxs-lookup"><span data-stu-id="c5496-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="c5496-327">該程式碼中沒有告訴 ASP.NET 將值放入文字方塊中的內容。</span><span class="sxs-lookup"><span data-stu-id="c5496-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="c5496-328">因此 ASP.NET 不會執行任何動作，而且文字方塊會轉譯，而不會有值。</span><span class="sxs-lookup"><span data-stu-id="c5496-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="c5496-329">其實有一個簡單的方法可以解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="c5496-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="c5496-330">您在文字方塊中輸入的內容可以在其所在 *的程式碼中使用* &mdash; `Request.QueryString["searchGenre"]` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="c5496-331">更新文字方塊的標記 `value` ，讓屬性從中取得值 `searchTerm` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="c5496-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="c5496-332">在此頁面上，您也可以將 `value` 屬性設定為 `searchTerm` 變數，因為該變數也包含您輸入的內容類型。</span><span class="sxs-lookup"><span data-stu-id="c5496-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="c5496-333">但是，使用 `Request` 物件來設定 `value` 屬性（如下所示）是完成這項工作的標準方式。</span><span class="sxs-lookup"><span data-stu-id="c5496-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="c5496-334"> (假設您甚至想要 &mdash; 在某些情況下這麼做，您可能會想要在欄位中呈現 *沒有* 值的頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="c5496-335">這完全取決於應用程式的進展。 ) </span><span class="sxs-lookup"><span data-stu-id="c5496-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="c5496-336">您無法「記住」用於密碼的文字方塊值。</span><span class="sxs-lookup"><span data-stu-id="c5496-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="c5496-337">這會是一個安全性漏洞，可讓使用者使用程式碼填寫密碼欄位。</span><span class="sxs-lookup"><span data-stu-id="c5496-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>

<span data-ttu-id="c5496-338">再次執行頁面，輸入內容類型，然後按一下 [ **搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="c5496-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="c5496-339">這次不只是您看到搜尋的結果，而且文字方塊會記住您上次輸入的內容：</span><span class="sxs-lookup"><span data-stu-id="c5496-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![頁面顯示文字方塊已「記住」先前的專案](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="c5496-341">搜尋標題中的任何單字</span><span class="sxs-lookup"><span data-stu-id="c5496-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="c5496-342">您現在可以搜尋任何內容類型，但您也可能想要搜尋標題。</span><span class="sxs-lookup"><span data-stu-id="c5496-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="c5496-343">當您搜尋時，很難正確地取得標題，因此您可以搜尋出現在標題內任何位置的單字。</span><span class="sxs-lookup"><span data-stu-id="c5496-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="c5496-344">若要在 SQL 中執行此作業，您可以使用 `LIKE` 運算子和語法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5496-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="c5496-345">此命令會取得其標題包含 "艾德" 的所有電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="c5496-346">當您使用 `LIKE` 運算子時，您會在搜尋詞彙中包含萬用字元 `%` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="c5496-347">搜尋 `LIKE 'adventure%'` 表示「開頭為「冒險」」。</span><span class="sxs-lookup"><span data-stu-id="c5496-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="c5496-348"> (技術上來說，這表示「「冒險」後面接著任何「字串」。) 同樣地，搜尋詞彙 `LIKE '%adventure'` 表示「任何內容，後面接著字串 ' 冒險 '」，這是另一種表示「以 ' 冒險 ' 結尾」的方法。</span><span class="sxs-lookup"><span data-stu-id="c5496-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="c5496-349">因此，搜尋詞彙 `LIKE '%adventure%'` 表示「在標題中的任意位置」。</span><span class="sxs-lookup"><span data-stu-id="c5496-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="c5496-350"> (技術上，「標題中的任何專案，後面接著「冒險」，後面接著任何專案」。) </span><span class="sxs-lookup"><span data-stu-id="c5496-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="c5496-351">在專案內 `<form>` ，于內容類型搜尋的結束記號下加入下列標記， `</div>` (緊接在結尾 `</form>` 元素) 之前：</span><span class="sxs-lookup"><span data-stu-id="c5496-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="c5496-352">處理這項搜尋的程式碼類似于內容搜尋的程式碼，不同之處在于您必須組合 `LIKE` 搜尋。</span><span class="sxs-lookup"><span data-stu-id="c5496-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="c5496-353">在頁面頂端的程式碼區塊內，在 `if` 內容類型搜尋的區塊之後加入此區塊 `if` ：</span><span class="sxs-lookup"><span data-stu-id="c5496-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="c5496-354">此程式碼會使用您稍早所見的相同邏輯，不同之處在于搜尋會使用 `LIKE` 運算子，而且程式碼會將 "" 放在 `%` 搜尋字詞的前後。</span><span class="sxs-lookup"><span data-stu-id="c5496-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="c5496-355">請注意，在頁面中新增另一個搜尋是很容易的。</span><span class="sxs-lookup"><span data-stu-id="c5496-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="c5496-356">您只需要：</span><span class="sxs-lookup"><span data-stu-id="c5496-356">All you had to do was:</span></span>

- <span data-ttu-id="c5496-357">建立 `if` 測試的區塊，以查看相關的搜尋方塊是否具有值。</span><span class="sxs-lookup"><span data-stu-id="c5496-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="c5496-358">將 `selectCommand` 變數設定為新的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="c5496-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="c5496-359">將變數設定為 `searchTerm` 要傳遞給查詢的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="c5496-360">以下是完整的程式碼區塊，其中包含標題搜尋的新邏輯：</span><span class="sxs-lookup"><span data-stu-id="c5496-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="c5496-361">以下是此程式碼的功能摘要：</span><span class="sxs-lookup"><span data-stu-id="c5496-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="c5496-362">變數 `searchTerm` 和 `selectCommand` 會在頂端初始化。</span><span class="sxs-lookup"><span data-stu-id="c5496-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="c5496-363">您要將這些變數設定為適當的搜尋字詞 (如果有任何) 和適當的 SQL 命令是根據使用者在頁面中執行的內容而定。</span><span class="sxs-lookup"><span data-stu-id="c5496-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="c5496-364">預設搜尋是從資料庫取得所有電影的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="c5496-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="c5496-365">在和的測試 `searchGenre` 中 `searchTitle` ，程式碼會將設定 `searchTerm` 為您想要搜尋的值。</span><span class="sxs-lookup"><span data-stu-id="c5496-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="c5496-366">這些程式碼區塊也 `selectCommand` 會針對該搜尋設定為適當的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="c5496-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="c5496-367">`db.Query`方法只會叫用一次，並使用任何 SQL 命令， `selectedCommand` 以及任何值在中 `searchTerm` 。</span><span class="sxs-lookup"><span data-stu-id="c5496-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="c5496-368">如果沒有搜尋詞彙 (沒有內容類型，而且沒有任何標題字) ，的值 `searchTerm` 就是空字串。</span><span class="sxs-lookup"><span data-stu-id="c5496-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="c5496-369">不過，這並不重要，因為在此情況下，查詢不需要參數。</span><span class="sxs-lookup"><span data-stu-id="c5496-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="c5496-370">測試標題搜尋功能</span><span class="sxs-lookup"><span data-stu-id="c5496-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="c5496-371">現在您可以測試已完成的搜尋頁面。</span><span class="sxs-lookup"><span data-stu-id="c5496-371">Now you can test your completed search page.</span></span> <span data-ttu-id="c5496-372">執行 *電影. cshtml*。</span><span class="sxs-lookup"><span data-stu-id="c5496-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="c5496-373">輸入內容類型，然後按一下 [ **搜尋**內容類型]。</span><span class="sxs-lookup"><span data-stu-id="c5496-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="c5496-374">方格會顯示該內容類型的電影，就像之前一樣。</span><span class="sxs-lookup"><span data-stu-id="c5496-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="c5496-375">輸入標題文字，然後按一下 [ **搜尋標題**]。</span><span class="sxs-lookup"><span data-stu-id="c5496-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="c5496-376">方格會顯示標題中有該單字的電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-376">The grid displays movies that have that word in the title.</span></span>

![搜尋標題中的 ' a ' 之後的電影頁面清單](form-basics/_static/image6.png)

<span data-ttu-id="c5496-378">將兩個文字方塊保持空白，然後按一下其中一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5496-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="c5496-379">方格會顯示所有電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="c5496-380">合併查詢</span><span class="sxs-lookup"><span data-stu-id="c5496-380">Combining the Queries</span></span>

<span data-ttu-id="c5496-381">您可能會注意到，您可以執行的搜尋是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="c5496-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="c5496-382">即使兩個搜尋方塊中都有值，您也無法同時搜尋標題和內容類型。</span><span class="sxs-lookup"><span data-stu-id="c5496-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="c5496-383">例如，您無法搜尋標題包含 "艾德" 的所有動作電影。</span><span class="sxs-lookup"><span data-stu-id="c5496-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="c5496-384"> (在現在為頁面撰寫程式碼時，如果您同時輸入內容類型和標題的值，則會優先使用標題搜尋。 ) 若要建立結合條件的搜尋，您必須建立具有如下語法的 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="c5496-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="c5496-385">而且，您必須使用如下所示的語句來執行查詢 (大約說) ：</span><span class="sxs-lookup"><span data-stu-id="c5496-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="c5496-386">如您所見，建立邏輯以允許許多搜尋準則排列可能有點相關。</span><span class="sxs-lookup"><span data-stu-id="c5496-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="c5496-387">因此，我們將在此停止。</span><span class="sxs-lookup"><span data-stu-id="c5496-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="c5496-388">後續推出</span><span class="sxs-lookup"><span data-stu-id="c5496-388">Coming Up Next</span></span>

<span data-ttu-id="c5496-389">在下一個教學課程中，您將建立使用表單的頁面，讓使用者將電影新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="c5496-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="c5496-390">影片頁面的完整清單 (以搜尋) 更新</span><span class="sxs-lookup"><span data-stu-id="c5496-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="c5496-391">其他資源</span><span class="sxs-lookup"><span data-stu-id="c5496-391">Additional Resources</span></span>

- [<span data-ttu-id="c5496-392">使用 Razor 語法進行 ASP.NET 網頁程式設計簡介</span><span class="sxs-lookup"><span data-stu-id="c5496-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="c5496-393">W3Schools 網站上的[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)</span><span class="sxs-lookup"><span data-stu-id="c5496-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="c5496-394">W3C 網站上的[方法定義](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)文章</span><span class="sxs-lookup"><span data-stu-id="c5496-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c5496-395">[上一個](displaying-data.md) 
> [下一步](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="c5496-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>
