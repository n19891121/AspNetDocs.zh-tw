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
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET網頁 (Razor) API 快速參考

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> 此頁包含一個清單,其中包含使用 Razor 語法程式設計 ASP.NET 網頁最常用的物件、屬性和方法的簡短示例。
> 
> ASP.NET網頁版本 2 中引入了標有"(v2)"的說明。
> 
> 有關 API 參考文件,請參閱有關 MSDN[的 ASP.NET 網頁參考文件](https://go.microsoft.com/fwlink/?LinkId=208659)。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> 
> - ASP.NET網頁 (剃鬚刀) 3
>   
> 
> 本教程還適用於ASP.NET網頁 2 和 ASP.NET網頁 1.0(標記為 v2 的功能除外)。

此頁包含以下參考資訊:

- [類別](#Classes)
- [Data](#Data)
- [協助程式](#Helpers)
- [驗證](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>類別

### `AppState[key], AppState[index],App`

包含應用程式中的任何頁面都可以共用的數據。 可以使用動態`App`屬性存取相同的資料,例如以下範例的範例 :

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

將字串值轉換為布林值(真/假)。 如果字串不表示真/假,則返回 false 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

將字串值轉換為日期/時間。 如果`DateTime.MinValue`字串不表示日期/時間,則返回或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

將字串值轉換為小數值。 如果字串不表示小數值,則返回 0.0 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

將字串值轉換為浮點。 如果字串不表示小數值,則返回 0.0 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

將字串值轉換為整數。 如果字串不表示整數,則返回 0 或指定值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

使用可選的其他路徑部件從本地檔案路徑創建與瀏覽器相容的 URL。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

將*值*呈現為 HTML 標記,而不是將其呈現為 HTML 編碼的輸出。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

如果值可以從字串轉換為指定類型,則返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

如果物件或變數沒有值,則返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

如果請求是 POST,則返回 true。 (初始請求通常是 GET。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

指定要應用於此頁面的佈局頁的路徑。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

包含當前請求中的頁面、佈局頁和部分頁面之間共享的數據。 可以使用動態`Page`屬性存取相同的資料,例如以下範例的範例 :

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(佈局頁面)呈現不在任何命名部分中的內容頁的內容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

使用指定的路徑和可選的額外資料呈現內容頁。 您可以`PageData`按位置(範例 1)或鍵(範例 2)獲取額外參數的值。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(佈局頁面)渲染具有名稱的內容節。 設置為*required*false 以使節為可選。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

獲取或設置 HTTP Cookie 的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

獲取在目前請求中上載的檔。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

獲取以表單(作為字串)過帳的資料。 `Request[key]`檢查和`Request.Form``Request.QueryString`集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

取得網址查詢字串中指定的資料。 `Request[key]`檢查和`Request.Form``Request.QueryString`集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

有選擇地禁用表單元素、查詢字串值、Cookie 或標頭值的請求驗證。 默認情況下啟用請求驗證,並防止使用者發佈標記或其他潛在危險內容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

向回應添加 HTTP 伺服器標頭。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

緩存指定時間的頁面輸出。 可選設定*滑動*以重置每個頁面存取的超時,並*更改 ByParams*以快取頁面的不同版本,以執行頁面請求中的每個不同查詢字串。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

將瀏覽器請求重定向到新位置。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

設定傳送到瀏覽器的 HTTP 狀態代碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

使用選擇的 MIME 型態將資料*內容寫入回應*。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

將文件的內容寫入回應。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(佈局頁面)定義具有名稱的內容節。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

解碼 HTML 編碼的字串。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

對字串進行編碼,以在 HTML 標記中呈現。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

返回指定虛擬路徑的伺服器物理路徑。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

從 URL 解碼文字。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

編碼文字以放入 URL。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

獲取或設置存在的值,直到使用者關閉瀏覽器。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

顯示物件值的字串表示形式。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

從 URL 獲取其他數據(例如 */MyPage/ExtraData)。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

變更指定之使用者的密碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

使用帳戶確認令牌確認帳戶。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

使用指定的使用者名稱和密碼創建新使用者帳戶。 要需要確認權杖,為*需要確認權杖傳遞 true。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

獲取當前登錄使用者的整數標識符。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

獲取當前登錄使用者的名稱。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

生成密碼重置權杖,該權杖可以透過電子郵件發送給使用者,以便用戶可以重置密碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

從使用者名返回用戶 ID。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

如果當前使用者已登錄,則返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

如果使用者已確認(例如,通過確認電子郵件)返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

如果當前使用者的名稱與指定的使用者名匹配,則返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

通過在 Cookie 中設置身份驗證權杖來登錄使用者。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

通過刪除身份驗證令牌 Cookie 將用戶登出。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

如果使用者未經驗證，請將 HTTP 狀態設定為 401 (未經授權)。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

如果當前使用者不是指定角色之一的成員,請將 HTTP 狀態設置為 401(未授權)。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

如果當前使用者不是*使用者名*指定的使用者,則將 HTTP 狀態設置為 401(未授權)。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

如果密碼重置權杖有效,則將使用者的密碼更改為新密碼。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>資料

### `Database.Execute(SQLstatement [,parameters]`

執行*SQL 語句*(使用可選參數),如插入、刪除或更新,並返回受影響的記錄計數。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

傳回最近插入之資料列的識別資料行。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

開啟指定的資料庫檔案或使用*Web.config*檔中的命名連接字串指定的資料庫。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

使用連接字串打開資料庫。 (這與 使用`Database.Open`連接字串名稱的 相反。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

使用*SQL 語句*(可選傳遞參數)查詢資料庫,並將結果作為集合返回。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

執行*SQL 語句*(使用可選參數)並返回單個記錄。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

執行*SQL 語句*(使用可選參數)並返回單個值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>協助程式

### `Analytics.GetGoogleHtml(webPropertyId)`

呈現指定 ID 的 Google 分析 JavaScript 代碼。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

呈現指定專案的 StatCounter 分析 JavaScript 代碼。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

呈現指定帳戶的 Yahoo 分析 JavaScript 代碼。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

將搜索傳遞給必應。 要指定要搜索的網站和搜尋框的標題,可以設置`Bing.SiteUrl``Bing.SiteTitle`和 屬性。 通常,您可以在*\_AppStart*頁中設置這些屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

初始化圖表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

向圖表添加圖例。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

向圖表添加一系列值。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

返回指定數據的哈希值。 預設演算法`sha256`為 。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

讓 Facebook 使用者連接到網頁。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

渲染用於上載檔的 UI。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

渲染指定的 Xbox 玩家代碼。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

渲染指定電子郵件位址的 Gravatar 圖像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

以 JavaScript 物件表示法 (JSON) 格式將數據物件轉換為字串。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

將 JSON 編碼的輸入字串轉換為數據物件,可以反覆運算或插入到資料庫中。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

使用指定的標題和可選 URL 呈現社交網路連結。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

將錯誤消息與表單欄段關聯。 使用`ModelState`幫助程式訪問此成員。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

將錯誤消息與窗體關聯。 使用`ModelState`幫助程式訪問此成員。

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

如果沒有驗證錯誤,則返回 true。 使用`ModelState`幫助程式訪問此成員。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

渲染物件和任何子物件的屬性和值。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

呈現重新CAPTCHA驗證測試。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

為重新 CAPTCHA 服務設置公共金鑰和私鑰。 通常,您可以在*\_AppStart*頁中設置這些屬性。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

返回重新CAPTCHA測試的結果。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

呈現有關ASP.NET網頁的狀態資訊。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

為指定用戶呈現 Twitter 流。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

為指定的搜索文本呈現Twitter流。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

渲染指定檔案的 Flash 視訊播放器,具有可選的寬度和高度。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

渲染具有可選寬度和高度的指定檔的 Windows 媒體播放機。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

渲染指定 *.xap*檔案的銀光播放機,具有所需的寬度和高度。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

如果找不到此物件,則傳回*由鍵*指定的物件 , 或 null。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

從快取中刪除*由鍵*指定的物件。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

將*值**按鍵*指定的名稱放入緩存中。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

使用查詢中`WebGrid`的資料建立新物件。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

渲染標記以在 HTML 表中顯示數據。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

渲染`WebGrid`對象的尋呼機。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

從指定的路徑載入影像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

將指定的圖像添加為浮浮浮水印。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

將指定的文本添加到圖像中。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

水準或垂直翻轉圖像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

在檔上載期間將圖像發佈到頁面時載入影像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

調整圖像的大小。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

將圖像向左或向右旋轉。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

將圖像保存到指定的路徑。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

設定 SMTP 伺服器的密碼。 通常,在*\_AppStart*頁中設置此屬性。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

傳送電子郵件訊息。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

設置 SMTP 伺服器名稱。 通常,在*\_AppStart*頁中設置此屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

設置 SMTP 伺服器的使用者名稱。 通常,應在*\_AppStart*頁中設置此屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>驗證

### `Html.ValidationMessage(field)`

(v2)呈現指定欄位的驗證錯誤訊息。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

(v2)顯示所有驗證錯誤的清單。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

(v2)註冊指定類型的驗證的使用者輸入元素。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

(v2)動態呈現用於客戶端驗證的 CSS 類屬性,以便您可以格式化驗證錯誤訊息。 (要求引用相應的用戶端腳本庫,並定義 CSS 類。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

(v2)啟用使用者輸入欄位的客戶端驗證。 (需要引用相應的用戶端腳本庫。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

(v2)如果註冊用於驗證的所有使用者輸入元素都包含有效值,則返回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

(v2)指定使用者必須為使用者輸入元素提供值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

(v2)指定用戶必須為每個使用者輸入元素提供值。 此方法不允許您指定自訂錯誤訊息。

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

(v2)使用`Validation.Add`方法時指定驗證測試。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
