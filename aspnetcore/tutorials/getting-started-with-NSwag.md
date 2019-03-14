---
title: NSwag 與 ASP.NET Core 使用者入門
author: zuckerthoben
description: 了解如何使用 NSwag 來產生 ASP.NET Core Web API 的文件和說明頁面。
ms.author: scaddie
ms.custom: mvc
ms.date: 12/30/2018
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: c03e7513edc3240f3f13f0c190e1ca9480e476af
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037765"
---
# <a name="get-started-with-nswag-and-aspnet-core"></a>NSwag 與 ASP.NET Core 使用者入門

作者：[Christoph Nienaber](https://twitter.com/zuckerthoben)、[Rico Suter](https://rsuter.com) 及 [Dave Brock](https://twitter.com/daveabrock)

::: moniker range=">= aspnetcore-2.1"

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag) \(英文\) ([如何下載](xref:index#how-to-download-a-sample))

::: moniker-end

NSwag 提供下列功能：

 * 能夠運用 Swagger UI 和 Swagger 產生器。
 * 彈性的程式碼產生功能。

使用 NSwag 時，您不需要有現有的 API &mdash; 您可以使用包含 Swagger 的協力廠商 API，然後產生用戶端實作。 NSwag 可讓您加速開發週期，並輕鬆地因應 API 變更進行調整。

## <a name="register-the-nswag-middleware"></a>註冊 NSwag 中介軟體

註冊 NSwag 中介軟體來：

 * 為實作的 Web API 產生 Swagger 規格。
 * 提供 Swagger UI 以瀏覽並測試 Web API。

若要使用 [NSwag](https://github.com/RSuter/NSwag) ASP.NET Core 中介軟體，請安裝 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 套件。 此套件包含用以產生並提供 Swagger 規格、Swagger UI (v2 和 v3) 及 [ReDoc UI](https://github.com/Rebilly/ReDoc) 的中介軟體。

請使用下列其中一種方法來安裝 NSwag NuGet 套件：

### <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 從 [套件管理員主控台] 視窗中：
  * 移至 [檢視] > [其他視窗] > [套件管理員主控台]
  * 巡覽至 *TodoApi.csproj* 檔案所在目錄
  * 執行下列命令：

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* 從 [管理 NuGet 套件] 對話方塊中：
  * 在 [方案總管] > [管理 NuGet 套件] 中，以滑鼠右鍵按一下專案
  * 將 [套件來源] 設定為 "nuget.org"
  * 在搜尋方塊中輸入 "NSwag.AspNetCore"
  * 從 [瀏覽] 索引標籤中選取 "NSwag.AspNetCore" 套件，並按一下 [安裝]

### <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 在 [Solution Pad] > [新增套件...] 中，以滑鼠右鍵按一下 *Packages* 資料夾
* 將 [新增套件] 視窗的 [來源] 下拉式清單設定為 "nuget.org"
* 在搜尋方塊中輸入 "NSwag.AspNetCore"
* 從結果窗格中選取 "NSwag.AspNetCore" 套件，並按一下 [新增套件]

### <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

從 [整合式終端機] 執行下列命令：

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

### <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

執行下列命令：

```console
dotnet add TodoApi.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>新增和設定 Swagger 中介軟體

 請在 `Startup` 類別中執行下列步驟，以在 ASP.NET Core 應用程式中新增和設定 Swagger：

* 匯入下列命名空間：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_StartupConfigureImports)]

* 在 `ConfigureServices` 方法中，註冊所需的 Swagger 服務：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_ConfigureServices&highlight=8)]

 * 在 `Configure` 方法中，啟用中介軟體為產生的 Swagger 規格和 SwaggerUI 提供服務：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=6-7)]

 * 啟動應用程式。 瀏覽至：
   * `http://localhost:<port>/swagger` 以檢視 Swagger UI。
   * `http://localhost:<port>/swagger/v1/swagger.json` 以檢視 Swagger 規格。

## <a name="code-generation"></a>程式碼產生

您可以選擇下列其中一個選項來利用 NSwag 的程式碼產生功能：

 * [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio) &ndash; 一個能夠以 C# 或 TypeScript 產生 API 用戶端程式碼的 Windows 傳統型應用程式。
 * 可在您專案內產生程式碼的 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 或 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 套件。
* 從[命令列](https://github.com/NSwag/NSwag/wiki/CommandLine)使用 NSwag。
 * [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 套件。


### <a name="generate-code-with-nswagstudio"></a>使用 NSwagStudio 來產生程式碼

* 依照 [NSwagStudio GitHub 存放庫](https://github.com/RSuter/NSwag/wiki/NSwagStudio) \(英文\) 的指示來安裝 NSwagStudio。
 * 啟動 NSwagStudio，然後在 [Swagger Specification URL] \(Swagger 規格 URL\) 文字方塊中輸入 *swagger.json* 檔案 URL。 例如，*http://localhost:44354/swagger/v1/swagger.json*。
* 按一下 [Create local Copy] \(建立本機複本\) 按鈕，以產生 Swagger 規格的 JSON 表示法。

  ![建立 Swagger 規格的本機複本](web-api-help-pages-using-swagger/_static/CreateLocalCopy-NSwagStudio.PNG)

 * 在 [Outputs] \(輸出\) 區域中，按一下 [CSharp Client] \(CSharp 用戶端\) 核取方塊。 視您的專案而定，您也可以選擇 [TypeScript Client] \(TypeScript 用戶端\)或 [CSharp Web API Controller] \(CSharp Web API 控制器\)。 如果您選取 [CSharp Web API Controller] \(CSharp Web API 控制器\)，服務規格會重建服務，作為反向產生。
* 按一下 [Generate Outputs] \(產生輸出\)，以產生 *TodoApi.NSwag* 專案 的完整 C# 用戶端實作。 若要查看所產生的用戶端程式碼，請按一下 [CSharp Client] \(CSharp 用戶端\) 索引標籤：

```csharp
//----------------------
// <auto-generated>
//     Generated using the NSwag toolchain v12.0.9.0 (NJsonSchema v9.13.10.0 (Newtonsoft.Json v11.0.0.0)) (http://NSwag.org)
// </auto-generated>
//----------------------

namespace MyNamespace
{
    #pragma warning disable

    [System.CodeDom.Compiler.GeneratedCode("NSwag", "12.0.9.0 (NJsonSchema v9.13.10.0 (Newtonsoft.Json v11.0.0.0))")]
    public partial class TodoClient 
    {
        private string _baseUrl = "https://localhost:44354";
        private System.Net.Http.HttpClient _httpClient;
        private System.Lazy<Newtonsoft.Json.JsonSerializerSettings> _settings;
    
        public TodoClient(System.Net.Http.HttpClient httpClient)
        {
            _httpClient = httpClient; 
            _settings = new System.Lazy<Newtonsoft.Json.JsonSerializerSettings>(() => 
            {
                var settings = new Newtonsoft.Json.JsonSerializerSettings();
                UpdateJsonSerializerSettings(settings);
                return settings;
            });
        }
    
        public string BaseUrl 
        {
            get { return _baseUrl; }
            set { _baseUrl = value; }
        }

        // code omitted for brevity
```

> [!TIP]
 > C# 用戶端程式碼會根據 [Settings] \(設定\) 索引標籤中的選取項目來產生。修改設定以執行工作，例如重新命名預設的命名空間和產生同步方法。

 * 將產生的 C# 程式碼複製到將取用 API 的用戶端專案中檔案。
* 開始取用 Web API：

```csharp
 var todoClient = new TodoClient();

// Gets all to-dos from the API
 var allTodos = await todoClient.GetAllAsync();

 // Create a new TodoItem, and save it via the API.
var createdTodo = await todoClient.CreateAsync(new TodoItem());

// Get a single to-do by ID
var foundTodo = await todoClient.GetByIdAsync(1);
```

## <a name="customize-api-documentation"></a>自訂 API 文件

Swagger 提供選項來記錄物件模型，以簡化 Web API 的取用作業。

### <a name="api-info-and-description"></a>API 資訊與描述

在 `Startup.ConfigureServices` 方法中，傳遞至 `AddSwaggerDocument` 方法的組態動作會新增作者、授權和描述等資訊：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Startup2.cs?name=snippet_AddSwaggerDocument)]

Swagger UI 會顯示版本資訊：

![含有版本資訊的 Swagger UI](web-api-help-pages-using-swagger/_static/custom-info-nswag.png)

### <a name="xml-comments"></a>XML 註解

 若要啟用 XML 註解，請執行下列步驟：

# <a name="visual-studiotabvisual-studio-xml"></a>[Visual Studio](#tab/visual-studio-xml/)

::: moniker range=">= aspnetcore-2.0"

* 以滑鼠右鍵按一下 [方案總管] 中的專案，然後選取 [編輯 <專案名稱>.csproj]。
* 將醒目提示的程式碼行手動新增至 *.csproj* 檔案：

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* 以滑鼠右鍵按一下方案總管中的專案，然後選取 [屬性]
* 核取 [組建] 索引標籤的 [輸出] 區段下方的 [XML 文件檔] 方塊

::: moniker-end

# <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[Visual Studio for Mac](#tab/visual-studio-mac-xml/)

::: moniker range=">= aspnetcore-2.0"

* 從 [Solution Pad] 中，按下 [控制項]，然後按一下專案名稱。 巡覽至 [工具] > [編輯檔案]。
* 將醒目提示的程式碼行手動新增至 *.csproj* 檔案：

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

* 開啟 [專案選項] 對話方塊 > [組建] >[編譯器]
* 核取 [一般選項] 區段下方的 [產生 XML 文件] 方塊

::: moniker-end

# <a name="visual-studio-codetabvisual-studio-code-xml"></a>[Visual Studio Code](#tab/visual-studio-code-xml/)

將醒目提示的程式碼行手動新增至 *.csproj* 檔案：

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

::: moniker range="<= aspnetcore-1.1"

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/TodoApi.csproj?name=snippet_DocumentationFileElement&highlight=1-2,4)]

::: moniker-end

---

### <a name="data-annotations"></a>資料註解

::: moniker range="<= aspnetcore-2.0"

 由於 NSwag 會使用[反映](/dotnet/csharp/programming-guide/concepts/reflection)，而針對 Web API 動作建議使用的傳回型別是 [IActionResult](xref:Microsoft.AspNetCore.Mvc.IActionResult)，因此它無法推斷您動作的執行內容和傳回內容。

參考下列範例：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

 上述動作會傳回 `IActionResult`，但在動作內部則會傳回 [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*) 或 [BadRequest](xref:System.Web.Http.ApiController.BadRequest*)。 請使用資料註解來告知用戶端已知此動作要傳回哪些 HTTP 狀態碼。 使用下列屬性裝飾動作：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.0/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

 由於 NSwag 會使用[反映](/dotnet/csharp/programming-guide/concepts/reflection)，而針對 Web API 動作建議使用的傳回型別是 [ActionResult\<T>](xref:Microsoft.AspNetCore.Mvc.ActionResult`1)，因此它只能推斷 `T` 所定義的傳回型別。 您無法自動推斷其他可能的傳回型別。 

參考下列範例：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateAction)]

上述動作會傳回 `ActionResult<T>`。 在動作內部則會傳回 [CreatedAtRoute](xref:System.Web.Http.ApiController.CreatedAtRoute*)。 由於控制器是以 [[ApiController]](xref:Microsoft.AspNetCore.Mvc.ApiControllerAttribute) 屬性裝飾，因此也可能傳回 [BadRequest](xref:System.Web.Http.ApiController.BadRequest*) 回應。 如需詳細資訊，請參閱[自動 HTTP 400 回應](xref:web-api/index#automatic-http-400-responses)。 請使用資料註解來告知用戶端已知此動作要傳回哪些 HTTP 狀態碼。 使用下列屬性裝飾動作：

[!code-csharp[](../tutorials/web-api-help-pages-using-swagger/samples/2.1/TodoApi.NSwag/Controllers/TodoController.cs?name=snippet_CreateActionAttributes)]

在 ASP.NET Core 2.2 或更新版本中，您可以使用慣例，而不使用 `[ProducesResponseType]` 來明確地裝飾個別動作。 如需詳細資訊，請參閱<xref:web-api/advanced/conventions>。

::: moniker-end

 Swagger 產生器現在可以正確描述此動作，而產生的用戶端會知道呼叫端點時它們所接收的內容。 建議做法是，使用這些屬性來裝飾所有動作。 

如需 API 動作應該傳回哪些 HTTP 回應的指導方針，請參閱 [RFC 7231 規格](https://tools.ietf.org/html/rfc7231#section-4.3)。
