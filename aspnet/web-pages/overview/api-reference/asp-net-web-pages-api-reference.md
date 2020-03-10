---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Pages （Razor） API 快速參考 |Microsoft Docs
author: Rick-Anderson
description: 此頁面包含一份清單，其中含有最常使用的物件、屬性和方法的簡短範例，以 Razor 語法的程式設計 ASP.NET Web Pages。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574330"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web Pages （Razor） API 快速參考

由[Tom FitzMacken](https://github.com/tfitzmac)

> 此頁面包含一份清單，其中含有最常使用的物件、屬性和方法的簡短範例，以 Razor 語法的程式設計 ASP.NET Web Pages。
> 
> 以 "（v2）" 標示的描述是在 ASP.NET Web Pages 第2版中引進。
> 
> 如需 API 參考檔，請參閱 MSDN 上的[ASP.NET Web Pages 參考檔](https://go.microsoft.com/fwlink/?LinkId=208659)。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）3
>   
> 
> 本教學課程也適用于 ASP.NET Web Pages 2 和 ASP.NET Web Pages 1.0 （除了標示為 v2 的功能以外）。

此頁面包含下列各項的參考資訊：

- [類別](#Classes)
- [Data](#Data)
- [助手](#Helpers)
- [驗證](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>類別

### `AppState[key], AppState[index],App`

包含可以由應用程式中的任何頁面共用的資料。 您可以使用 [動態 `App`] 屬性來存取相同的資料，如下列範例所示：

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

將字串值轉換成布林值（true/false）。 如果字串不代表 true/false，則傳回 false 或指定的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

將字串值轉換為日期/時間。 如果字串不代表日期/時間，則傳回 `DateTime.MinValue` 或指定的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

將字串值轉換為十進位值。 如果字串不代表十進位值，則傳回0.0 或指定的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

將字串值轉換成 float。 如果字串不代表十進位值，則傳回0.0 或指定的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

將字串值轉換為整數。 如果字串不代表整數，則傳回0或指定的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

使用選擇性的其他路徑部分，從本機檔案路徑建立瀏覽器相容的 URL。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

將*值*轉譯為 html 標記，而不是將其轉譯為 html 編碼輸出。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

如果值可從字串轉換成指定的類型，則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

如果物件或變數沒有值，則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

如果要求為 POST，則傳回 true。 （初始要求通常是 GET）。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

指定要套用到此頁面的版面配置頁路徑。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

包含在目前要求中的頁面、版面配置頁及部分頁面之間共用的資料。 您可以使用 [動態 `Page`] 屬性來存取相同的資料，如下列範例所示：

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

（版面配置頁）呈現不在任何已命名區段中之內容頁面的內容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

使用指定的路徑和選擇性的額外資料呈現內容頁。 您可以從 `PageData` 依位置（範例1）或索引鍵（範例2）取得額外參數的值。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

（版面配置頁）呈現具有名稱的 content 區段。 將 [*必要*] 設定為 [false]，讓區段成為選擇性。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

取得或設定 HTTP cookie 的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

取得目前要求中已上傳的檔案。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

取得在表單中張貼的資料（以字串表示）。 `Request[key]` 會同時檢查 `Request.Form` 和 `Request.QueryString` 集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

取得 URL 查詢字串中指定的資料。 `Request[key]` 會同時檢查 `Request.Form` 和 `Request.QueryString` 集合。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

選擇性地停用表單元素、查詢字串值、cookie 或標頭值的要求驗證。 預設會啟用要求驗證，並防止使用者張貼標記或其他潛在危險的內容。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

將 HTTP 伺服器標頭新增至回應。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

快取一段指定時間的頁面輸出。 選擇性地設定*滑動*以重設每個頁面存取和*varyByParams*的超時時間，以針對頁面要求中的每個不同查詢字串快取不同版本的頁面。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

將瀏覽器要求重新導向至新的位置。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

設定傳送至瀏覽器的 HTTP 狀態碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

使用選擇性 MIME 類型，將*資料*的內容寫入至回應。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

將檔案的內容寫入至回應。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

（版面配置頁）定義具有名稱的 content 區段。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

將 HTML 編碼的字串解碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

將字串編碼以在 HTML 標籤中呈現。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

傳回指定虛擬路徑的伺服器實體路徑。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

從 URL 解碼文字。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

編碼要放入 URL 中的文字。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

取得或設定存在於使用者關閉瀏覽器之前的值。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

顯示物件值的字串表示。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

從 URL 取得其他資料（例如， */MyPage/ExtraData*）。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

變更指定之使用者的密碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

使用帳戶確認權杖確認帳戶。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

使用指定的使用者名稱和密碼，建立新的使用者帳戶。 若要要求確認權杖，請傳遞 true 以進行*requireConfirmationToken。*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

取得目前登入之使用者的整數識別碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

取得目前登入之使用者的名稱。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

產生密碼重設權杖，可透過電子郵件傳送給使用者，讓使用者可以重設密碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

從使用者名稱傳回使用者識別碼。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

如果目前使用者已登入，則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

如果已確認使用者（例如，透過確認電子郵件），則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

如果目前使用者的名稱符合指定的使用者名稱，則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

藉由在 cookie 中設定驗證 token，將使用者登入。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

藉由移除驗證權杖 cookie，將使用者登出。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

如果使用者未經驗證，請將 HTTP 狀態設定為 401 (未經授權)。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

如果目前使用者不是其中一個指定角色的成員，則會將 HTTP 狀態設定為401（未經授權）。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

如果目前使用者不是*username*所指定的使用者，會將 HTTP 狀態設定為401（未經授權）。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

如果密碼重設標記有效，會將使用者的密碼變更為新密碼。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>資料

### `Database.Execute(SQLstatement [,parameters]`

執行*SQLstatement* （包含選擇性參數），例如 INSERT、DELETE 或 UPDATE，並傳回受影響記錄的計數。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

傳回最近插入之資料列的識別資料行。

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

使用*web.config 檔案*中的命名連接字串，開啟指定的資料庫檔案或指定的資料庫。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

使用連接字串開啟資料庫。 （這與使用連接字串名稱的 `Database.Open`相反。）

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

使用*SQLstatement* （選擇性地傳遞參數）來查詢資料庫，並以集合形式傳回結果。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

執行*SQLstatement* （使用選擇性參數）並傳回單一記錄。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

執行*SQLstatement* （使用選擇性參數）並傳回單一值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>協助程式

### `Analytics.GetGoogleHtml(webPropertyId)`

呈現指定識別碼的 Google Analytics JavaScript 程式碼。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

呈現所指定專案的 StatCounter 分析 JavaScript 程式碼。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

呈現指定帳戶的 Yahoo Analytics JavaScript 程式碼。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

將搜尋傳遞給 Bing。 若要指定要搜尋的網站和 [搜尋] 方塊的標題，您可以設定 [`Bing.SiteUrl`] 和 [`Bing.SiteTitle`] 屬性。 一般來說，您會在 [ *\_AppStart* ] 頁面中設定這些屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

初始化圖表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

將圖例加入至圖表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

將一系列的值加入至圖表。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

傳回指定之資料的雜湊。 預設演算法為 `sha256`。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

讓 Facebook 使用者連接到頁面。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

呈現用來上傳檔案的 UI。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

呈現指定的 Xbox 玩家標記。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

呈現所指定電子郵件地址的 Gravatar 影像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

將資料物件轉換為 JavaScript 物件標記法（JSON）格式的字串。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

將 JSON 編碼的輸入字串轉換成您可以反復查看或插入資料庫的資料物件。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

使用指定的標題和選擇性 URL 呈現社交網路連結。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

將錯誤訊息與表單欄位產生關聯。 請使用 `ModelState` helper 來存取這個成員。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

將錯誤訊息與表單產生關聯。 請使用 `ModelState` helper 來存取這個成員。

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

如果沒有驗證錯誤，則傳回 true。 請使用 `ModelState` helper 來存取這個成員。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

呈現物件的屬性和值，以及任何子物件。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

呈現 reCAPTCHA 驗證測試。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

設定 reCAPTCHA 服務的公開和私密金鑰。 一般來說，您會在 [ *\_AppStart* ] 頁面中設定這些屬性。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

傳回 reCAPTCHA 測試的結果。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

呈現有關 ASP.NET Web Pages 的狀態資訊。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

呈現指定使用者的 Twitter 串流。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

針對指定的搜尋文字呈現 Twitter 串流。

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

以選擇性的寬度和高度，呈現指定檔案的 Flash 影片播放程式。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

使用選擇性的寬度和高度，為指定的檔案呈現 Windows Media player。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

以所需的寬度和高度，呈現指定之 *.xap*檔案的 Silverlight 播放機。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

傳回索引*鍵*所指定的物件，如果找不到物件，則傳回 null。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

從快取中移除索引*鍵*所指定的物件。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

以索引*鍵*所指定的名稱，將*值*放入快取中。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

使用查詢中的資料，建立新的 `WebGrid` 物件。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

呈現標記以在 HTML 資料表中顯示資料。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

呈現 `WebGrid` 物件的分頁。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

從指定的路徑載入影像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

將指定的影像加入為浮水印。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

將指定的文字新增至影像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

水準或垂直翻轉影像。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

在檔案上傳期間，將影像張貼到頁面時載入影像。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

調整影像大小。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

將影像向左或向右旋轉。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

將影像儲存至指定的路徑。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

設定 SMTP 伺服器的密碼。 一般來說，您會在 [ *\_AppStart* ] 頁面中設定此屬性。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

傳送電子郵件訊息。

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

設定 SMTP 伺服器名稱。 一般來說，您會在 [ *\_AppStart* ] 頁面中設定此屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

設定 SMTP 伺服器的使用者名稱。 一般來說，您應該在 [ *\_AppStart* ] 頁面中設定此屬性。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>驗證

### `Html.ValidationMessage(field)`

2呈現指定欄位的驗證錯誤訊息。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

2顯示所有驗證錯誤的清單。

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

2為指定的驗證類型註冊使用者輸入元素。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

2動態呈現用戶端驗證的 CSS 類別屬性，讓您可以格式化驗證錯誤訊息。 （您需要參考適當的用戶端腳本程式庫，並定義 CSS 類別）。

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

2啟用使用者輸入欄位的用戶端驗證。 （需要您參考適當的用戶端腳本程式庫。）

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

2如果已註冊進行驗證的所有使用者輸入元素都包含有效的值，則傳回 true。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

2指定使用者必須提供使用者輸入元素的值。

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

2指定使用者必須提供每個使用者輸入元素的值。 這個方法不會讓您指定自訂錯誤訊息。

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

2當您使用 `Validation.Add` 方法時，指定驗證測試。

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
