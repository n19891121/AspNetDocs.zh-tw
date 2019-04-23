---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Pages (Razor) API 快速參考 |Microsoft Docs
author: Rick-Anderson
description: 此頁面包含最常使用的物件、 屬性和方法的程式設計含有 Razor 語法的 ASP.NET Web Pages 的簡短範例的清單。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: 547b1932c4f8d3684c668561e3fe568a0f272925
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59416502"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="d5702-103">ASP.NET Web Pages (Razor) API 快速參考</span><span class="sxs-lookup"><span data-stu-id="d5702-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="d5702-104">藉由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d5702-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d5702-105">此頁面包含最常使用的物件、 屬性和方法的程式設計含有 Razor 語法的 ASP.NET Web Pages 的簡短範例的清單。</span><span class="sxs-lookup"><span data-stu-id="d5702-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="d5702-106">ASP.NET Web Pages 中第 2 版導入標示為 「 (v2) 」 的描述。</span><span class="sxs-lookup"><span data-stu-id="d5702-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="d5702-107">如需 API 參考文件，請參閱[ASP.NET Web Pages 參考文件](https://go.microsoft.com/fwlink/?LinkId=208659)MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="d5702-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="d5702-108">軟體版本</span><span class="sxs-lookup"><span data-stu-id="d5702-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="d5702-109">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="d5702-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="d5702-110">本教學課程也適用於 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0 （除了標記 v2 的功能）。</span><span class="sxs-lookup"><span data-stu-id="d5702-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>


<span data-ttu-id="d5702-111">此頁面包含下列參考資訊：</span><span class="sxs-lookup"><span data-stu-id="d5702-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="d5702-112">類別</span><span class="sxs-lookup"><span data-stu-id="d5702-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="d5702-113">Data</span><span class="sxs-lookup"><span data-stu-id="d5702-113">Data</span></span>](#Data)
- [<span data-ttu-id="d5702-114">協助程式</span><span class="sxs-lookup"><span data-stu-id="d5702-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="d5702-115">驗證</span><span class="sxs-lookup"><span data-stu-id="d5702-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="d5702-116">類別</span><span class="sxs-lookup"><span data-stu-id="d5702-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="d5702-117">包含可由任何頁面共用應用程式中的資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="d5702-118">您可以使用動態`App`屬性來存取相同的資料，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d5702-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="d5702-119">將字串值轉換成布林值 (true/false)。</span><span class="sxs-lookup"><span data-stu-id="d5702-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="d5702-120">會傳回 false 或指定的值，如果字串不是 true/false。</span><span class="sxs-lookup"><span data-stu-id="d5702-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="d5702-121">將轉換成日期/時間的字串值。</span><span class="sxs-lookup"><span data-stu-id="d5702-121">Converts a string value to date/time.</span></span> <span data-ttu-id="d5702-122">傳回`DateTime.MinValue`或指定的值，如果字串不是日期/時間。</span><span class="sxs-lookup"><span data-stu-id="d5702-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="d5702-123">將字串值轉換成十進位值。</span><span class="sxs-lookup"><span data-stu-id="d5702-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="d5702-124">傳回 0.0 或指定的值，如果字串不是十進位值。</span><span class="sxs-lookup"><span data-stu-id="d5702-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="d5702-125">將字串值轉換成浮點數。</span><span class="sxs-lookup"><span data-stu-id="d5702-125">Converts a string value to a float.</span></span> <span data-ttu-id="d5702-126">傳回 0.0 或指定的值，如果字串不是十進位值。</span><span class="sxs-lookup"><span data-stu-id="d5702-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="d5702-127">將字串值轉換成整數。</span><span class="sxs-lookup"><span data-stu-id="d5702-127">Converts a string value to an integer.</span></span> <span data-ttu-id="d5702-128">傳回 0 或指定的值，如果字串不是整數。</span><span class="sxs-lookup"><span data-stu-id="d5702-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="d5702-129">建立本機檔案路徑，與其他的選擇性路徑部分瀏覽器相容的 URL。</span><span class="sxs-lookup"><span data-stu-id="d5702-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="d5702-130">呈現*值*為 HTML 標記，而不是轉譯為 HTML 編碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="d5702-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="d5702-131">如果此值可以從字串轉換成指定的型別，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="d5702-132">如果物件或變數沒有值，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="d5702-133">如果要求為 POST，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="d5702-134">（初始要求通常是 GET）。</span><span class="sxs-lookup"><span data-stu-id="d5702-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="d5702-135">指定要套用至這個頁面的版面配置頁的路徑。</span><span class="sxs-lookup"><span data-stu-id="d5702-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="d5702-136">包含目前要求中的頁面、 版面配置頁及部分頁面之間共用資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="d5702-137">您可以使用動態`Page`屬性來存取相同的資料，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d5702-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="d5702-138">（版面配置頁）呈現之內容頁面不是任何具名的各節中的內容。</span><span class="sxs-lookup"><span data-stu-id="d5702-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="d5702-139">呈現內容的頁面，使用指定的路徑和選擇性的額外資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="d5702-140">您可以取得的額外參數的值`PageData`的位置 （例如，1） 或索引鍵 （例如 2）。</span><span class="sxs-lookup"><span data-stu-id="d5702-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="d5702-141">（版面配置頁）呈現內容的區段名稱。</span><span class="sxs-lookup"><span data-stu-id="d5702-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="d5702-142">設定*必要*為 false，讓選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="d5702-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="d5702-143">取得或設定 HTTP cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="d5702-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="d5702-144">取得目前要求中已上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="d5702-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="d5702-145">取得 （如字串） 在表單中回傳的資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="d5702-146">`Request[key]` 檢查兩者`Request.Form`而`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="d5702-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="d5702-147">取得指定之 URL 查詢字串中的資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="d5702-148">`Request[key]` 檢查兩者`Request.Form`而`Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="d5702-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="d5702-149">選擇性地停用要求驗證表單項目、 查詢字串值、 cookie 或標頭值。</span><span class="sxs-lookup"><span data-stu-id="d5702-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="d5702-150">要求驗證預設會啟用，並防止使用者張貼的標記或其他潛在的危險的內容。</span><span class="sxs-lookup"><span data-stu-id="d5702-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="d5702-151">將 HTTP 伺服器標頭加入回應。</span><span class="sxs-lookup"><span data-stu-id="d5702-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="d5702-152">會在指定的時間，快取頁面輸出。</span><span class="sxs-lookup"><span data-stu-id="d5702-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="d5702-153">選擇性地設定*滑動*重設存取每個頁面上的逾時並*varyByParams*快取不同版本的頁面要求中的每個不同的查詢字串的頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="d5702-154">瀏覽器將要求重新導向至新位置。</span><span class="sxs-lookup"><span data-stu-id="d5702-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="d5702-155">設定傳送到瀏覽器的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="d5702-156">內容寫入*資料*來包含選擇性的 MIME 類型的回應。</span><span class="sxs-lookup"><span data-stu-id="d5702-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="d5702-157">將檔案的內容寫入至回應。</span><span class="sxs-lookup"><span data-stu-id="d5702-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="d5702-158">（版面配置頁）定義內容區段名稱。</span><span class="sxs-lookup"><span data-stu-id="d5702-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="d5702-159">將已 HTML 編碼字串解碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="d5702-160">將轉譯的 HTML 標記的字串編碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="d5702-161">傳回指定的虛擬路徑的伺服器實體路徑。</span><span class="sxs-lookup"><span data-stu-id="d5702-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="d5702-162">將解碼的 URL 中的文字。</span><span class="sxs-lookup"><span data-stu-id="d5702-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="d5702-163">將編碼將放在 URL 中的文字。</span><span class="sxs-lookup"><span data-stu-id="d5702-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="d5702-164">取得或設定值，這個值存在，直到使用者關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d5702-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="d5702-165">顯示物件的值的字串表示。</span><span class="sxs-lookup"><span data-stu-id="d5702-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="d5702-166">從 URL 取得額外的資料 (例如*MyPage/ExtraData*)。</span><span class="sxs-lookup"><span data-stu-id="d5702-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="d5702-167">變更指定之使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="d5702-168">確認使用帳戶確認語彙基元的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5702-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="d5702-169">使用指定的使用者名稱和密碼建立新的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5702-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="d5702-170">若要要求確認語彙基元，傳遞 true 值給*requireConfirmationToken。*</span><span class="sxs-lookup"><span data-stu-id="d5702-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="d5702-171">取得目前登入的使用者屬性的整數識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="d5702-172">取得目前登入的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d5702-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="d5702-173">產生可以透過電子郵件傳送給使用者，讓使用者可以重設密碼的密碼重設語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d5702-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="d5702-174">從 使用者名稱傳回使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="d5702-175">如果目前的使用者登入，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="d5702-176">如果使用者已確認 （例如，透過確認電子郵件），則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="d5702-177">如果目前的使用者名稱符合指定的使用者名稱，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="d5702-178">記錄中的使用者，藉由在 cookie 中設定驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d5702-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="d5702-179">使用者縮小記錄移除驗證語彙基元 cookie。</span><span class="sxs-lookup"><span data-stu-id="d5702-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="d5702-180">如果使用者未經過驗證，請將 HTTP 狀態設定為 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="d5702-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="d5702-181">如果目前的使用者不是其中一個指定的角色的成員，請將 HTTP 狀態設定為 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="d5702-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="d5702-182">如果目前的使用者不是所指定的使用者*username*，將 HTTP 狀態設定為 401 （未經授權）。</span><span class="sxs-lookup"><span data-stu-id="d5702-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="d5702-183">密碼重設語彙基元是否有效，請為新的密碼變更使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="d5702-184">資料</span><span class="sxs-lookup"><span data-stu-id="d5702-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="d5702-185">執行*SQLstatement* （內含選擇性參數） 例如 INSERT、 DELETE 或 UPDATE，並傳回受影響記錄的計數。</span><span class="sxs-lookup"><span data-stu-id="d5702-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="d5702-186">傳回最近插入的資料列的身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="d5702-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="d5702-187">開啟指定的資料庫檔案或使用中的具名的連接字串所指定的資料庫*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="d5702-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="d5702-188">開啟資料庫使用的連接字串。</span><span class="sxs-lookup"><span data-stu-id="d5702-188">Opens a database using the connection string.</span></span> <span data-ttu-id="d5702-189">(這樣可避免`Database.Open`，它會使用的連接字串名稱。)</span><span class="sxs-lookup"><span data-stu-id="d5702-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="d5702-190">查詢資料庫使用*SQLstatement* （並選擇性地傳遞參數），並傳回結果做為集合。</span><span class="sxs-lookup"><span data-stu-id="d5702-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="d5702-191">執行*SQLstatement* （內含選擇性參數），並傳回單一記錄。</span><span class="sxs-lookup"><span data-stu-id="d5702-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="d5702-192">執行*SQLstatement* （內含選擇性參數），並傳回單一值。</span><span class="sxs-lookup"><span data-stu-id="d5702-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="d5702-193">協助程式</span><span class="sxs-lookup"><span data-stu-id="d5702-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="d5702-194">呈現 Google Analytics JavaScript 程式碼做為指定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="d5702-195">呈現指定的專案的 StatCounter 分析 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="d5702-196">呈現指定的帳戶的 Yahoo 分析 JavaScript 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="d5702-197">傳遞至 Bing 的搜尋。</span><span class="sxs-lookup"><span data-stu-id="d5702-197">Passes a search to Bing.</span></span> <span data-ttu-id="d5702-198">若要指定要搜尋和 [搜尋] 方塊的標題的站台，您可以設定`Bing.SiteUrl`和`Bing.SiteTitle`屬性。</span><span class="sxs-lookup"><span data-stu-id="d5702-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="d5702-199">在設定這些屬性通常 *\_AppStart*頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="d5702-200">初始化圖表。</span><span class="sxs-lookup"><span data-stu-id="d5702-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="d5702-201">將圖例新增至圖表。</span><span class="sxs-lookup"><span data-stu-id="d5702-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="d5702-202">將圖表中的一系列的值。</span><span class="sxs-lookup"><span data-stu-id="d5702-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="d5702-203">傳回指定之資料的雜湊值。</span><span class="sxs-lookup"><span data-stu-id="d5702-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="d5702-204">預設的演算法是`sha256`。</span><span class="sxs-lookup"><span data-stu-id="d5702-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="d5702-205">可讓 Facebook 使用者對網頁進行連線。</span><span class="sxs-lookup"><span data-stu-id="d5702-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="d5702-206">上傳檔案的呈現 UI。</span><span class="sxs-lookup"><span data-stu-id="d5702-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="d5702-207">呈現指定的 Xbox 玩家的標記。</span><span class="sxs-lookup"><span data-stu-id="d5702-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="d5702-208">呈現指定的電子郵件地址 Gravatar 影像。</span><span class="sxs-lookup"><span data-stu-id="d5702-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="d5702-209">將資料物件轉換成 JavaScript Object Notation (JSON) 格式字串。</span><span class="sxs-lookup"><span data-stu-id="d5702-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="d5702-210">將 JSON 編碼的輸入的字串轉換成的資料物件，您可以逐一查看，或將插入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="d5702-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="d5702-211">呈現社交網路的連結，使用指定的標題和選擇性的 URL。</span><span class="sxs-lookup"><span data-stu-id="d5702-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="d5702-212">關聯表單欄位中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-212">Associates an error message with a form field.</span></span> <span data-ttu-id="d5702-213">使用`ModelState`存取這個成員的協助程式。</span><span class="sxs-lookup"><span data-stu-id="d5702-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="d5702-214">關聯表單中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-214">Associates an error message with a form.</span></span> <span data-ttu-id="d5702-215">使用`ModelState`存取這個成員的協助程式。</span><span class="sxs-lookup"><span data-stu-id="d5702-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="d5702-216">如果不有任何驗證錯誤，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="d5702-217">使用`ModelState`存取這個成員的協助程式。</span><span class="sxs-lookup"><span data-stu-id="d5702-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="d5702-218">呈現的屬性和值的物件及任何子物件。</span><span class="sxs-lookup"><span data-stu-id="d5702-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="d5702-219">呈現 reCAPTCHA 驗證測試。</span><span class="sxs-lookup"><span data-stu-id="d5702-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="d5702-220">設定 reCAPTCHA 服務的公用和私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5702-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="d5702-221">在設定這些屬性通常 *\_AppStart*頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="d5702-222">傳回 reCAPTCHA 測試的結果。</span><span class="sxs-lookup"><span data-stu-id="d5702-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="d5702-223">呈現有關 ASP.NET Web 網頁的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="d5702-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="d5702-224">呈現指定之使用者的 Twitter 資料流。</span><span class="sxs-lookup"><span data-stu-id="d5702-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="d5702-225">呈現指定的搜尋文字的 Twitter 資料流。</span><span class="sxs-lookup"><span data-stu-id="d5702-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="d5702-226">呈現指定的檔案，以選擇性的寬度和高度的快閃視訊播放器。</span><span class="sxs-lookup"><span data-stu-id="d5702-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="d5702-227">呈現 Windows Media player 使用選擇性的寬度和高度指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="d5702-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="d5702-228">呈現指定 Silverlight 播放機 *.xap*檔案所需的寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="d5702-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="d5702-229">傳回所指定的物件*金鑰*，或如果找不到物件則為 null。</span><span class="sxs-lookup"><span data-stu-id="d5702-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="d5702-230">移除所指定的物件*金鑰*從快取。</span><span class="sxs-lookup"><span data-stu-id="d5702-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="d5702-231">將放*值*到所指定的名稱下快取*金鑰*。</span><span class="sxs-lookup"><span data-stu-id="d5702-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="d5702-232">建立新`WebGrid`物件使用來自查詢的資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="d5702-233">呈現標記，以顯示 HTML 表格中的資料。</span><span class="sxs-lookup"><span data-stu-id="d5702-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="d5702-234">呈現頁面巡覽區`WebGrid`物件。</span><span class="sxs-lookup"><span data-stu-id="d5702-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="d5702-235">從指定的路徑載入映像。</span><span class="sxs-lookup"><span data-stu-id="d5702-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="d5702-236">將指定的影像，做為浮水印。</span><span class="sxs-lookup"><span data-stu-id="d5702-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="d5702-237">將指定的文字新增至映像。</span><span class="sxs-lookup"><span data-stu-id="d5702-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="d5702-238">翻轉影像，水平或垂直。</span><span class="sxs-lookup"><span data-stu-id="d5702-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="d5702-239">當映像時，會張貼至頁面上，在檔案上傳期間，請載入映像。</span><span class="sxs-lookup"><span data-stu-id="d5702-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="d5702-240">調整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="d5702-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="d5702-241">影像旋轉至左邊或右邊。</span><span class="sxs-lookup"><span data-stu-id="d5702-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="d5702-242">將影像儲存至指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="d5702-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="d5702-243">設定 SMTP 伺服器的密碼。</span><span class="sxs-lookup"><span data-stu-id="d5702-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="d5702-244">在設定此屬性通常 *\_AppStart*頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="d5702-245">傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="d5702-246">設定 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="d5702-246">Sets the SMTP server name.</span></span> <span data-ttu-id="d5702-247">在設定此屬性通常 *\_AppStart*頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="d5702-248">設定 SMTP 伺服器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d5702-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="d5702-249">通常您應該設定這個屬性 *\_AppStart*頁面。</span><span class="sxs-lookup"><span data-stu-id="d5702-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="d5702-250">驗證</span><span class="sxs-lookup"><span data-stu-id="d5702-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="d5702-251">(v2)呈現指定之欄位的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="d5702-252">(v2)顯示所有的驗證錯誤的清單。</span><span class="sxs-lookup"><span data-stu-id="d5702-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="d5702-253">(v2)註冊指定的型別驗證的使用者輸入項目。</span><span class="sxs-lookup"><span data-stu-id="d5702-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="d5702-254">(v2)動態呈現 CSS 類別屬性，用戶端驗證，如此您可以格式化驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="d5702-255">（需要您參考適當的用戶端指令碼程式庫和您定義的 CSS 類別）。</span><span class="sxs-lookup"><span data-stu-id="d5702-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="d5702-256">(v2)可讓使用者輸入欄位的用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="d5702-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="d5702-257">（需要您參考適當的用戶端指令碼程式庫）。</span><span class="sxs-lookup"><span data-stu-id="d5702-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="d5702-258">(v2)如果使用者輸入的所有項目進行驗證的 registred 包含有效的值，則傳回 true。</span><span class="sxs-lookup"><span data-stu-id="d5702-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="d5702-259">(v2)指定使用者必須提供使用者輸入項目的值。</span><span class="sxs-lookup"><span data-stu-id="d5702-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="d5702-260">(v2)指定使用者必須提供值，每個使用者輸入項目。</span><span class="sxs-lookup"><span data-stu-id="d5702-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="d5702-261">這個方法不會讓您指定自訂錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="d5702-261">This method does not let you specify a custom error message.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

<span data-ttu-id="d5702-262">(v2)指定當您使用的驗證測試`Validation.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="d5702-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
