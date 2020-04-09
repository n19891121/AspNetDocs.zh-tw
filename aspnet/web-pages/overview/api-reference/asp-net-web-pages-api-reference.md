---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET網頁(Razor)API快速參考 |微軟文件
author: Rick-Anderson
description: 此頁包含一個清單,其中包含使用 Razor 語法程式設計 ASP.NET 網頁最常用的物件、屬性和方法的簡短示例。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676241"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a><span data-ttu-id="35f69-103">ASP.NET網頁 (Razor) API 快速參考</span><span class="sxs-lookup"><span data-stu-id="35f69-103">ASP.NET Web Pages (Razor) API Quick Reference</span></span>

<span data-ttu-id="35f69-104"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="35f69-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="35f69-105">此頁包含一個清單,其中包含使用 Razor 語法程式設計 ASP.NET 網頁最常用的物件、屬性和方法的簡短示例。</span><span class="sxs-lookup"><span data-stu-id="35f69-105">This page contains a list with brief examples of the most commonly used objects, properties, and methods for programming ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="35f69-106">ASP.NET網頁版本 2 中引入了標有"(v2)"的說明。</span><span class="sxs-lookup"><span data-stu-id="35f69-106">Descriptions marked with "(v2)" were introduced in ASP.NET Web Pages version 2.</span></span>
> 
> <span data-ttu-id="35f69-107">有關 API 參考文件,請參閱有關 MSDN[的 ASP.NET 網頁參考文件](https://go.microsoft.com/fwlink/?LinkId=208659)。</span><span class="sxs-lookup"><span data-stu-id="35f69-107">For API reference documentation, see the [ASP.NET Web Pages Reference Documentation](https://go.microsoft.com/fwlink/?LinkId=208659) on MSDN.</span></span>
> 
> ## <a name="software-versions"></a><span data-ttu-id="35f69-108">軟體版本</span><span class="sxs-lookup"><span data-stu-id="35f69-108">Software versions</span></span>
> 
> 
> - <span data-ttu-id="35f69-109">ASP.NET網頁 (剃鬚刀) 3</span><span class="sxs-lookup"><span data-stu-id="35f69-109">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="35f69-110">本教程還適用於ASP.NET網頁 2 和 ASP.NET網頁 1.0(標記為 v2 的功能除外)。</span><span class="sxs-lookup"><span data-stu-id="35f69-110">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0 (except for features marked v2).</span></span>

<span data-ttu-id="35f69-111">此頁包含以下參考資訊:</span><span class="sxs-lookup"><span data-stu-id="35f69-111">This page contains reference information for the following:</span></span>

- [<span data-ttu-id="35f69-112">類別</span><span class="sxs-lookup"><span data-stu-id="35f69-112">Classes</span></span>](#Classes)
- [<span data-ttu-id="35f69-113">Data</span><span class="sxs-lookup"><span data-stu-id="35f69-113">Data</span></span>](#Data)
- [<span data-ttu-id="35f69-114">協助程式</span><span class="sxs-lookup"><span data-stu-id="35f69-114">Helpers</span></span>](#Helpers)
- [<span data-ttu-id="35f69-115">驗證</span><span class="sxs-lookup"><span data-stu-id="35f69-115">Validation</span></span>](#Validation)

<a id="Classes"></a>
## <a name="classes"></a><span data-ttu-id="35f69-116">類別</span><span class="sxs-lookup"><span data-stu-id="35f69-116">Classes</span></span>

### `AppState[key], AppState[index],App`

<span data-ttu-id="35f69-117">包含應用程式中的任何頁面都可以共用的數據。</span><span class="sxs-lookup"><span data-stu-id="35f69-117">Contains data that can be shared by any pages in the application.</span></span> <span data-ttu-id="35f69-118">可以使用動態`App`屬性存取相同的資料,例如以下範例的範例 :</span><span class="sxs-lookup"><span data-stu-id="35f69-118">You can use the dynamic `App` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

<span data-ttu-id="35f69-119">將字串值轉換為布林值(真/假)。</span><span class="sxs-lookup"><span data-stu-id="35f69-119">Converts a string value to a Boolean value (true/false).</span></span> <span data-ttu-id="35f69-120">如果字串不表示真/假,則返回 false 或指定值。</span><span class="sxs-lookup"><span data-stu-id="35f69-120">Returns false or the specified value if the string does not represent true/false.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

<span data-ttu-id="35f69-121">將字串值轉換為日期/時間。</span><span class="sxs-lookup"><span data-stu-id="35f69-121">Converts a string value to date/time.</span></span> <span data-ttu-id="35f69-122">如果`DateTime.MinValue`字串不表示日期/時間,則返回或指定值。</span><span class="sxs-lookup"><span data-stu-id="35f69-122">Returns `DateTime.MinValue` or the specified value if the string does not represent a date/time.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

<span data-ttu-id="35f69-123">將字串值轉換為小數值。</span><span class="sxs-lookup"><span data-stu-id="35f69-123">Converts a string value to a decimal value.</span></span> <span data-ttu-id="35f69-124">如果字串不表示小數值,則返回 0.0 或指定值。</span><span class="sxs-lookup"><span data-stu-id="35f69-124">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

<span data-ttu-id="35f69-125">將字串值轉換為浮點。</span><span class="sxs-lookup"><span data-stu-id="35f69-125">Converts a string value to a float.</span></span> <span data-ttu-id="35f69-126">如果字串不表示小數值,則返回 0.0 或指定值。</span><span class="sxs-lookup"><span data-stu-id="35f69-126">Returns 0.0 or the specified value if the string does not represent a decimal value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

<span data-ttu-id="35f69-127">將字串值轉換為整數。</span><span class="sxs-lookup"><span data-stu-id="35f69-127">Converts a string value to an integer.</span></span> <span data-ttu-id="35f69-128">如果字串不表示整數,則返回 0 或指定值。</span><span class="sxs-lookup"><span data-stu-id="35f69-128">Returns 0 or the specified value if the string does not represent an integer.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

<span data-ttu-id="35f69-129">使用可選的其他路徑部件從本地檔案路徑創建與瀏覽器相容的 URL。</span><span class="sxs-lookup"><span data-stu-id="35f69-129">Creates a browser-compatible URL from a local file path, with optional additional path parts.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

<span data-ttu-id="35f69-130">將*值*呈現為 HTML 標記,而不是將其呈現為 HTML 編碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="35f69-130">Renders *value* as HTML markup instead of rendering it as HTML-encoded output.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

<span data-ttu-id="35f69-131">如果值可以從字串轉換為指定類型,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-131">Returns true if the value can be converted from a string to the specified type.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

<span data-ttu-id="35f69-132">如果物件或變數沒有值,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-132">Returns true if the object or variable has no value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

<span data-ttu-id="35f69-133">如果請求是 POST,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-133">Returns true if the request is a POST.</span></span> <span data-ttu-id="35f69-134">(初始請求通常是 GET。</span><span class="sxs-lookup"><span data-stu-id="35f69-134">(Initial requests are usually a GET.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

<span data-ttu-id="35f69-135">指定要應用於此頁面的佈局頁的路徑。</span><span class="sxs-lookup"><span data-stu-id="35f69-135">Specifies the path of a layout page to apply to this page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

<span data-ttu-id="35f69-136">包含當前請求中的頁面、佈局頁和部分頁面之間共享的數據。</span><span class="sxs-lookup"><span data-stu-id="35f69-136">Contains data shared between the page, layout pages, and partial pages in the current request.</span></span> <span data-ttu-id="35f69-137">可以使用動態`Page`屬性存取相同的資料,例如以下範例的範例 :</span><span class="sxs-lookup"><span data-stu-id="35f69-137">You can use the dynamic `Page` property to access the same data, as in the following example:</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

<span data-ttu-id="35f69-138">(佈局頁面)呈現不在任何命名部分中的內容頁的內容。</span><span class="sxs-lookup"><span data-stu-id="35f69-138">(Layout pages) Renders the content of a content page that is not in any named sections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

<span data-ttu-id="35f69-139">使用指定的路徑和可選的額外資料呈現內容頁。</span><span class="sxs-lookup"><span data-stu-id="35f69-139">Renders a content page using the specified path and optional extra data.</span></span> <span data-ttu-id="35f69-140">您可以`PageData`按位置(範例 1)或鍵(範例 2)獲取額外參數的值。</span><span class="sxs-lookup"><span data-stu-id="35f69-140">You can get the values of the extra parameters from `PageData` by position (example 1) or key (example 2).</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

<span data-ttu-id="35f69-141">(佈局頁面)渲染具有名稱的內容節。</span><span class="sxs-lookup"><span data-stu-id="35f69-141">(Layout pages) Renders a content section that has a name.</span></span> <span data-ttu-id="35f69-142">設置為*required*false 以使節為可選。</span><span class="sxs-lookup"><span data-stu-id="35f69-142">Set *required* to false to make a section optional.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

<span data-ttu-id="35f69-143">獲取或設置 HTTP Cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="35f69-143">Gets or sets the value of an HTTP cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

<span data-ttu-id="35f69-144">獲取在目前請求中上載的檔。</span><span class="sxs-lookup"><span data-stu-id="35f69-144">Gets the files that were uploaded in the current request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

<span data-ttu-id="35f69-145">獲取以表單(作為字串)過帳的資料。</span><span class="sxs-lookup"><span data-stu-id="35f69-145">Gets data that was posted in a form (as strings).</span></span> <span data-ttu-id="35f69-146">`Request[key]`檢查和`Request.Form``Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="35f69-146">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

<span data-ttu-id="35f69-147">取得網址查詢字串中指定的資料。</span><span class="sxs-lookup"><span data-stu-id="35f69-147">Gets data that was specified in the URL query string.</span></span> <span data-ttu-id="35f69-148">`Request[key]`檢查和`Request.Form``Request.QueryString`集合。</span><span class="sxs-lookup"><span data-stu-id="35f69-148">`Request[key]` checks both the `Request.Form` and the `Request.QueryString` collections.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

<span data-ttu-id="35f69-149">有選擇地禁用表單元素、查詢字串值、Cookie 或標頭值的請求驗證。</span><span class="sxs-lookup"><span data-stu-id="35f69-149">Selectively disables request validation for a form element, query-string value, cookie, or header value.</span></span> <span data-ttu-id="35f69-150">默認情況下啟用請求驗證,並防止使用者發佈標記或其他潛在危險內容。</span><span class="sxs-lookup"><span data-stu-id="35f69-150">Request validation is enabled by default and prevents users from posting markup or other potentially dangerous content.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

<span data-ttu-id="35f69-151">向回應添加 HTTP 伺服器標頭。</span><span class="sxs-lookup"><span data-stu-id="35f69-151">Adds an HTTP server header to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

<span data-ttu-id="35f69-152">緩存指定時間的頁面輸出。</span><span class="sxs-lookup"><span data-stu-id="35f69-152">Caches the page output for a specified time.</span></span> <span data-ttu-id="35f69-153">可選設定*滑動*以重置每個頁面存取的超時,並*更改 ByParams*以快取頁面的不同版本,以執行頁面請求中的每個不同查詢字串。</span><span class="sxs-lookup"><span data-stu-id="35f69-153">Optionally set *sliding* to reset the timeout on each page access and *varyByParams* to cache different versions of the page for each different query string in the page request.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

<span data-ttu-id="35f69-154">將瀏覽器請求重定向到新位置。</span><span class="sxs-lookup"><span data-stu-id="35f69-154">Redirects the browser request to a new location.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

<span data-ttu-id="35f69-155">設定傳送到瀏覽器的 HTTP 狀態代碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-155">Sets the HTTP status code sent to the browser.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

<span data-ttu-id="35f69-156">使用選擇的 MIME 型態將資料*內容寫入回應*。</span><span class="sxs-lookup"><span data-stu-id="35f69-156">Writes the contents of *data* to the response with an optional MIME type.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

<span data-ttu-id="35f69-157">將文件的內容寫入回應。</span><span class="sxs-lookup"><span data-stu-id="35f69-157">Writes the contents of a file to the response.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

<span data-ttu-id="35f69-158">(佈局頁面)定義具有名稱的內容節。</span><span class="sxs-lookup"><span data-stu-id="35f69-158">(Layout pages) Defines a content section that has a name.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

<span data-ttu-id="35f69-159">解碼 HTML 編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="35f69-159">Decodes a string that is HTML encoded.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

<span data-ttu-id="35f69-160">對字串進行編碼,以在 HTML 標記中呈現。</span><span class="sxs-lookup"><span data-stu-id="35f69-160">Encodes a string for rendering in HTML markup.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

<span data-ttu-id="35f69-161">返回指定虛擬路徑的伺服器物理路徑。</span><span class="sxs-lookup"><span data-stu-id="35f69-161">Returns the server physical path for the specified virtual path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

<span data-ttu-id="35f69-162">從 URL 解碼文字。</span><span class="sxs-lookup"><span data-stu-id="35f69-162">Decodes text from a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

<span data-ttu-id="35f69-163">編碼文字以放入 URL。</span><span class="sxs-lookup"><span data-stu-id="35f69-163">Encodes text to put in a URL.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

<span data-ttu-id="35f69-164">獲取或設置存在的值,直到使用者關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="35f69-164">Gets or sets a value that exists until the user closes the browser.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

<span data-ttu-id="35f69-165">顯示物件值的字串表示形式。</span><span class="sxs-lookup"><span data-stu-id="35f69-165">Displays a string representation of the object's value.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

<span data-ttu-id="35f69-166">從 URL 獲取其他數據(例如 */MyPage/ExtraData)。*</span><span class="sxs-lookup"><span data-stu-id="35f69-166">Gets additional data from the URL (for example, */MyPage/ExtraData*).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

<span data-ttu-id="35f69-167">變更指定之使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-167">Changes the password for the specified user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

<span data-ttu-id="35f69-168">使用帳戶確認令牌確認帳戶。</span><span class="sxs-lookup"><span data-stu-id="35f69-168">Confirms an account using the account confirmation token.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

<span data-ttu-id="35f69-169">使用指定的使用者名稱和密碼創建新使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="35f69-169">Creates a new user account with the specified user name and password.</span></span> <span data-ttu-id="35f69-170">要需要確認權杖,為*需要確認權杖傳遞 true。*</span><span class="sxs-lookup"><span data-stu-id="35f69-170">To require a confirmation token, pass true for *requireConfirmationToken.*</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

<span data-ttu-id="35f69-171">獲取當前登錄使用者的整數標識符。</span><span class="sxs-lookup"><span data-stu-id="35f69-171">Gets the integer identifier for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

<span data-ttu-id="35f69-172">獲取當前登錄使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="35f69-172">Gets the name for the currently logged-in user.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

<span data-ttu-id="35f69-173">生成密碼重置權杖,該權杖可以透過電子郵件發送給使用者,以便用戶可以重置密碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-173">Generates a password-reset token that can be sent in email to a user so that the user can reset the password.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

<span data-ttu-id="35f69-174">從使用者名返回用戶 ID。</span><span class="sxs-lookup"><span data-stu-id="35f69-174">Returns the user ID from the user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

<span data-ttu-id="35f69-175">如果當前使用者已登錄,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-175">Returns true if the current user is logged in.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

<span data-ttu-id="35f69-176">如果使用者已確認(例如,通過確認電子郵件)返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-176">Returns true if the user has been confirmed (for example, through a confirmation email).</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

<span data-ttu-id="35f69-177">如果當前使用者的名稱與指定的使用者名匹配,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-177">Returns true if the current user's name matches the specified user name.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

<span data-ttu-id="35f69-178">通過在 Cookie 中設置身份驗證權杖來登錄使用者。</span><span class="sxs-lookup"><span data-stu-id="35f69-178">Logs the user in by setting an authentication token in the cookie.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

<span data-ttu-id="35f69-179">通過刪除身份驗證令牌 Cookie 將用戶登出。</span><span class="sxs-lookup"><span data-stu-id="35f69-179">Logs the user out by removing the authentication token cookie.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

<span data-ttu-id="35f69-180">如果使用者未經驗證，請將 HTTP 狀態設定為 401 (未經授權)。</span><span class="sxs-lookup"><span data-stu-id="35f69-180">If the user is not authenticated, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

<span data-ttu-id="35f69-181">如果當前使用者不是指定角色之一的成員,請將 HTTP 狀態設置為 401(未授權)。</span><span class="sxs-lookup"><span data-stu-id="35f69-181">If the current user is not a member of one of the specified roles, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

<span data-ttu-id="35f69-182">如果當前使用者不是*使用者名*指定的使用者,則將 HTTP 狀態設置為 401(未授權)。</span><span class="sxs-lookup"><span data-stu-id="35f69-182">If the current user is not the user specified by *username*, sets the HTTP status to 401 (Unauthorized).</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

<span data-ttu-id="35f69-183">如果密碼重置權杖有效,則將使用者的密碼更改為新密碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-183">If the password reset token is valid, changes the user's password to the new password.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a><span data-ttu-id="35f69-184">資料</span><span class="sxs-lookup"><span data-stu-id="35f69-184">Data</span></span>

### `Database.Execute(SQLstatement [,parameters]`

<span data-ttu-id="35f69-185">執行*SQL 語句*(使用可選參數),如插入、刪除或更新,並返回受影響的記錄計數。</span><span class="sxs-lookup"><span data-stu-id="35f69-185">Executes *SQLstatement* (with optional parameters) such as INSERT, DELETE, or UPDATE and returns a count of affected records.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

<span data-ttu-id="35f69-186">傳回最近插入之資料列的識別資料行。</span><span class="sxs-lookup"><span data-stu-id="35f69-186">Returns the identity column from the most recently inserted row.</span></span>

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

<span data-ttu-id="35f69-187">開啟指定的資料庫檔案或使用*Web.config*檔中的命名連接字串指定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="35f69-187">Opens either the specified database file or the database specified using a named connection string from the *Web.config* file.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

<span data-ttu-id="35f69-188">使用連接字串打開資料庫。</span><span class="sxs-lookup"><span data-stu-id="35f69-188">Opens a database using the connection string.</span></span> <span data-ttu-id="35f69-189">(這與 使用`Database.Open`連接字串名稱的 相反。</span><span class="sxs-lookup"><span data-stu-id="35f69-189">(This contrasts with `Database.Open`, which uses a connection string name.)</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

<span data-ttu-id="35f69-190">使用*SQL 語句*(可選傳遞參數)查詢資料庫,並將結果作為集合返回。</span><span class="sxs-lookup"><span data-stu-id="35f69-190">Queries the database using *SQLstatement* (optionally passing parameters) and returns the results as a collection.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

<span data-ttu-id="35f69-191">執行*SQL 語句*(使用可選參數)並返回單個記錄。</span><span class="sxs-lookup"><span data-stu-id="35f69-191">Executes *SQLstatement* (with optional parameters) and returns a single record.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

<span data-ttu-id="35f69-192">執行*SQL 語句*(使用可選參數)並返回單個值。</span><span class="sxs-lookup"><span data-stu-id="35f69-192">Executes *SQLstatement* (with optional parameters) and returns a single value.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a><span data-ttu-id="35f69-193">協助程式</span><span class="sxs-lookup"><span data-stu-id="35f69-193">Helpers</span></span>

### `Analytics.GetGoogleHtml(webPropertyId)`

<span data-ttu-id="35f69-194">呈現指定 ID 的 Google 分析 JavaScript 代碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-194">Renders the Google Analytics JavaScript code for the specified ID.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

<span data-ttu-id="35f69-195">呈現指定專案的 StatCounter 分析 JavaScript 代碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-195">Renders the StatCounter Analytics JavaScript code for the specified project.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

<span data-ttu-id="35f69-196">呈現指定帳戶的 Yahoo 分析 JavaScript 代碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-196">Renders the Yahoo Analytics JavaScript code for the specified account.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

<span data-ttu-id="35f69-197">將搜索傳遞給必應。</span><span class="sxs-lookup"><span data-stu-id="35f69-197">Passes a search to Bing.</span></span> <span data-ttu-id="35f69-198">要指定要搜索的網站和搜尋框的標題,可以設置`Bing.SiteUrl``Bing.SiteTitle`和 屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-198">To specify the site to search and a title for the search box, you can set the `Bing.SiteUrl` and `Bing.SiteTitle` properties.</span></span> <span data-ttu-id="35f69-199">通常,您可以在*\_AppStart*頁中設置這些屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-199">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

<span data-ttu-id="35f69-200">初始化圖表。</span><span class="sxs-lookup"><span data-stu-id="35f69-200">Initializes a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

<span data-ttu-id="35f69-201">向圖表添加圖例。</span><span class="sxs-lookup"><span data-stu-id="35f69-201">Adds a legend to a chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

<span data-ttu-id="35f69-202">向圖表添加一系列值。</span><span class="sxs-lookup"><span data-stu-id="35f69-202">Adds a series of values to the chart.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

<span data-ttu-id="35f69-203">返回指定數據的哈希值。</span><span class="sxs-lookup"><span data-stu-id="35f69-203">Returns a hash for the specified data.</span></span> <span data-ttu-id="35f69-204">預設演算法`sha256`為 。</span><span class="sxs-lookup"><span data-stu-id="35f69-204">The default algorithm is `sha256`.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

<span data-ttu-id="35f69-205">讓 Facebook 使用者連接到網頁。</span><span class="sxs-lookup"><span data-stu-id="35f69-205">Lets Facebook users make a connection to pages.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

<span data-ttu-id="35f69-206">渲染用於上載檔的 UI。</span><span class="sxs-lookup"><span data-stu-id="35f69-206">Renders UI for uploading files.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

<span data-ttu-id="35f69-207">渲染指定的 Xbox 玩家代碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-207">Renders the specified Xbox gamer tag.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

<span data-ttu-id="35f69-208">渲染指定電子郵件位址的 Gravatar 圖像。</span><span class="sxs-lookup"><span data-stu-id="35f69-208">Renders the Gravatar image for the specified email address.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

<span data-ttu-id="35f69-209">以 JavaScript 物件表示法 (JSON) 格式將數據物件轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="35f69-209">Converts a data object to a string in the JavaScript Object Notation (JSON) format.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

<span data-ttu-id="35f69-210">將 JSON 編碼的輸入字串轉換為數據物件,可以反覆運算或插入到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="35f69-210">Converts a JSON-encoded input string to a data object that you can iterate over or insert into a database.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

<span data-ttu-id="35f69-211">使用指定的標題和可選 URL 呈現社交網路連結。</span><span class="sxs-lookup"><span data-stu-id="35f69-211">Renders social networking links using the specified title and optional URL.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

<span data-ttu-id="35f69-212">將錯誤消息與表單欄段關聯。</span><span class="sxs-lookup"><span data-stu-id="35f69-212">Associates an error message with a form field.</span></span> <span data-ttu-id="35f69-213">使用`ModelState`幫助程式訪問此成員。</span><span class="sxs-lookup"><span data-stu-id="35f69-213">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

<span data-ttu-id="35f69-214">將錯誤消息與窗體關聯。</span><span class="sxs-lookup"><span data-stu-id="35f69-214">Associates an error message with a form.</span></span> <span data-ttu-id="35f69-215">使用`ModelState`幫助程式訪問此成員。</span><span class="sxs-lookup"><span data-stu-id="35f69-215">Use the `ModelState` helper to access this member.</span></span>

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

<span data-ttu-id="35f69-216">如果沒有驗證錯誤,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-216">Returns true if there are no validation errors.</span></span> <span data-ttu-id="35f69-217">使用`ModelState`幫助程式訪問此成員。</span><span class="sxs-lookup"><span data-stu-id="35f69-217">Use the `ModelState` helper to access this member.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

<span data-ttu-id="35f69-218">渲染物件和任何子物件的屬性和值。</span><span class="sxs-lookup"><span data-stu-id="35f69-218">Renders the properties and values of an object and any child objects.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

<span data-ttu-id="35f69-219">呈現重新CAPTCHA驗證測試。</span><span class="sxs-lookup"><span data-stu-id="35f69-219">Renders the reCAPTCHA verification test.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

<span data-ttu-id="35f69-220">為重新 CAPTCHA 服務設置公共金鑰和私鑰。</span><span class="sxs-lookup"><span data-stu-id="35f69-220">Sets public and private keys for the reCAPTCHA service.</span></span> <span data-ttu-id="35f69-221">通常,您可以在*\_AppStart*頁中設置這些屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-221">Normally you set these properties in the *\_AppStart* page.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

<span data-ttu-id="35f69-222">返回重新CAPTCHA測試的結果。</span><span class="sxs-lookup"><span data-stu-id="35f69-222">Returns the result of the reCAPTCHA test.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

<span data-ttu-id="35f69-223">呈現有關ASP.NET網頁的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="35f69-223">Renders status information about ASP.NET Web Pages.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

<span data-ttu-id="35f69-224">為指定用戶呈現 Twitter 流。</span><span class="sxs-lookup"><span data-stu-id="35f69-224">Renders a Twitter stream for the specified user.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

<span data-ttu-id="35f69-225">為指定的搜索文本呈現Twitter流。</span><span class="sxs-lookup"><span data-stu-id="35f69-225">Renders a Twitter stream for the specified search text.</span></span>

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

<span data-ttu-id="35f69-226">渲染指定檔案的 Flash 視訊播放器,具有可選的寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="35f69-226">Renders a Flash video player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

<span data-ttu-id="35f69-227">渲染具有可選寬度和高度的指定檔的 Windows 媒體播放機。</span><span class="sxs-lookup"><span data-stu-id="35f69-227">Renders a Windows Media player for the specified file with optional width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

<span data-ttu-id="35f69-228">渲染指定 *.xap*檔案的銀光播放機,具有所需的寬度和高度。</span><span class="sxs-lookup"><span data-stu-id="35f69-228">Renders a Silverlight player for the specified *.xap* file with required width and height.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

<span data-ttu-id="35f69-229">如果找不到此物件,則傳回*由鍵*指定的物件 , 或 null。</span><span class="sxs-lookup"><span data-stu-id="35f69-229">Returns the object specified by *key*, or null if the object is not found.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

<span data-ttu-id="35f69-230">從快取中刪除*由鍵*指定的物件。</span><span class="sxs-lookup"><span data-stu-id="35f69-230">Removes the object specified by *key* from the cache.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

<span data-ttu-id="35f69-231">將*值\*\*按鍵*指定的名稱放入緩存中。</span><span class="sxs-lookup"><span data-stu-id="35f69-231">Puts *value* into the cache under the name specified by *key*.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

<span data-ttu-id="35f69-232">使用查詢中`WebGrid`的資料建立新物件。</span><span class="sxs-lookup"><span data-stu-id="35f69-232">Creates a new `WebGrid` object using data from a query.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

<span data-ttu-id="35f69-233">渲染標記以在 HTML 表中顯示數據。</span><span class="sxs-lookup"><span data-stu-id="35f69-233">Renders markup to display data in an HTML table.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

<span data-ttu-id="35f69-234">渲染`WebGrid`對象的尋呼機。</span><span class="sxs-lookup"><span data-stu-id="35f69-234">Renders a pager for the `WebGrid` object.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

<span data-ttu-id="35f69-235">從指定的路徑載入影像。</span><span class="sxs-lookup"><span data-stu-id="35f69-235">Loads an image from the specified path.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

<span data-ttu-id="35f69-236">將指定的圖像添加為浮浮浮水印。</span><span class="sxs-lookup"><span data-stu-id="35f69-236">Adds the specified image as a watermark.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

<span data-ttu-id="35f69-237">將指定的文本添加到圖像中。</span><span class="sxs-lookup"><span data-stu-id="35f69-237">Adds the specified text to the image.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

<span data-ttu-id="35f69-238">水準或垂直翻轉圖像。</span><span class="sxs-lookup"><span data-stu-id="35f69-238">Flips the image horizontally or vertically.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

<span data-ttu-id="35f69-239">在檔上載期間將圖像發佈到頁面時載入影像。</span><span class="sxs-lookup"><span data-stu-id="35f69-239">Loads an image when an image is posted to a page during a file upload.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

<span data-ttu-id="35f69-240">調整圖像的大小。</span><span class="sxs-lookup"><span data-stu-id="35f69-240">Resizes an the image.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

<span data-ttu-id="35f69-241">將圖像向左或向右旋轉。</span><span class="sxs-lookup"><span data-stu-id="35f69-241">Rotates the image to the left or the right.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

<span data-ttu-id="35f69-242">將圖像保存到指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="35f69-242">Saves the image to the specified path.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

<span data-ttu-id="35f69-243">設定 SMTP 伺服器的密碼。</span><span class="sxs-lookup"><span data-stu-id="35f69-243">Sets the password for the SMTP server.</span></span> <span data-ttu-id="35f69-244">通常,在*\_AppStart*頁中設置此屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-244">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

<span data-ttu-id="35f69-245">傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="35f69-245">Sends an email message.</span></span>

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

<span data-ttu-id="35f69-246">設置 SMTP 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="35f69-246">Sets the SMTP server name.</span></span> <span data-ttu-id="35f69-247">通常,在*\_AppStart*頁中設置此屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-247">Normally you set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

<span data-ttu-id="35f69-248">設置 SMTP 伺服器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="35f69-248">Sets the user name for the SMTP server.</span></span> <span data-ttu-id="35f69-249">通常,應在*\_AppStart*頁中設置此屬性。</span><span class="sxs-lookup"><span data-stu-id="35f69-249">Normally you should set this property in the *\_AppStart* page.</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a><span data-ttu-id="35f69-250">驗證</span><span class="sxs-lookup"><span data-stu-id="35f69-250">Validation</span></span>

### `Html.ValidationMessage(field)`

<span data-ttu-id="35f69-251">(v2)呈現指定欄位的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35f69-251">(v2) Renders a validation error message for the specified field.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

<span data-ttu-id="35f69-252">(v2)顯示所有驗證錯誤的清單。</span><span class="sxs-lookup"><span data-stu-id="35f69-252">(v2) Displays a list of all validation errors.</span></span>

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

<span data-ttu-id="35f69-253">(v2)註冊指定類型的驗證的使用者輸入元素。</span><span class="sxs-lookup"><span data-stu-id="35f69-253">(v2) Registers a user input element for the specified type of validation.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

<span data-ttu-id="35f69-254">(v2)動態呈現用於客戶端驗證的 CSS 類屬性,以便您可以格式化驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35f69-254">(v2) Dynamically renders CSS class attributes for client-side validation so that you can format validation error messages.</span></span> <span data-ttu-id="35f69-255">(要求引用相應的用戶端腳本庫,並定義 CSS 類。</span><span class="sxs-lookup"><span data-stu-id="35f69-255">(Requires that you reference the appropriate client-script libraries and that you define CSS classes.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

<span data-ttu-id="35f69-256">(v2)啟用使用者輸入欄位的客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="35f69-256">(v2) Enables client-side validation for the user input field.</span></span> <span data-ttu-id="35f69-257">(需要引用相應的用戶端腳本庫。</span><span class="sxs-lookup"><span data-stu-id="35f69-257">(Requires that you reference the appropriate client-script libraries.)</span></span>

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

<span data-ttu-id="35f69-258">(v2)如果註冊用於驗證的所有使用者輸入元素都包含有效值,則返回 true。</span><span class="sxs-lookup"><span data-stu-id="35f69-258">(v2) Returns true if all user input elements that are registred for validation contain valid values.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

<span data-ttu-id="35f69-259">(v2)指定使用者必須為使用者輸入元素提供值。</span><span class="sxs-lookup"><span data-stu-id="35f69-259">(v2) Specifies that users must provide a value for the user input element.</span></span>

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

<span data-ttu-id="35f69-260">(v2)指定用戶必須為每個使用者輸入元素提供值。</span><span class="sxs-lookup"><span data-stu-id="35f69-260">(v2) Specifies that users must provide values for each of the user input elements.</span></span> <span data-ttu-id="35f69-261">此方法不允許您指定自訂錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35f69-261">This method does not let you specify a custom error message.</span></span>

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

<span data-ttu-id="35f69-262">(v2)使用`Validation.Add`方法時指定驗證測試。</span><span class="sxs-lookup"><span data-stu-id="35f69-262">(v2) Specifies a validation test when you use the `Validation.Add` method.</span></span>

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
