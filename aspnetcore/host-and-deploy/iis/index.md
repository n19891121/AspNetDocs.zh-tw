---
title: 在使用 IIS 的 Windows 上裝載 ASP.NET Core
author: guardrex
description: 了解如何在 Windows Server Internet Information Services (IIS) 上裝載 ASP.NET Core 應用程式。
ms.author: riande
ms.custom: mvc
ms.date: 02/19/2019
uid: host-and-deploy/iis/index
---
# <a name="host-aspnet-core-on-windows-with-iis"></a>在使用 IIS 的 Windows 上裝載 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex)

[安裝 .NET Core 裝載套件組合](#install-the-net-core-hosting-bundle)

## <a name="supported-operating-systems"></a>支援的作業系統

支援下列作業系統：

* Windows 7 或更新版本
* Windows Server 2008 R2 或更新版本

[HTTP.sys 伺服器](xref:fundamentals/servers/httpsys) (先前稱為 WebListener) 不適用搭配 IIS 的反向 Proxy 設定。 請使用 [Kestrel 伺服器](xref:fundamentals/servers/kestrel)。

如需在 Azure 中裝載的資訊，請參閱 <xref:host-and-deploy/azure-apps/index>。

## <a name="supported-platforms"></a>支援的平台

支援針對 32 位元 (x86) 與 64 位元 (x64) 部署發行的應用程式。 除非應用程式符合下列條件，否則請部署 32 位元應用程式：

* 需要提供給 64 位元應用程式使用的較大虛擬記憶體位址空間。
* 需要較大的 IIS 堆疊大小。
* 有 64 位元原生相依性。

## <a name="application-configuration"></a>應用程式組態

### <a name="enable-the-iisintegration-components"></a>啟用 IISIntegration 元件

::: moniker range=">= aspnetcore-2.1"

一般的 *Program.cs* 會呼叫 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 以開始設定主機：

```csharp
public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

一般的 *Program.cs* 會呼叫 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 以開始設定主機：

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

**同處理序主控模型**

`CreateDefaultBuilder` 會呼叫 `UseIIS` 方法來啟動 [CoreCLR](/dotnet/standard/glossary#coreclr)，並在 IIS 工作者處理序 (*w3wp.exe* 或 *iisexpress.exe*) 內裝載應用程式。 效能測試指出，相較於跨處理序裝載 .NET Core 應用程式，並將要求 Proxy 處理至 [Kestrel](xref:fundamentals/servers/kestrel) 伺服器，裝載於同處理序可提供明顯更高的要求輸送量。

以 .NET Framework 為目標的 ASP.NET Core 應用程式不支援處理序內裝載模型。

**跨處理序裝載模型**

若是使用 IIS 的跨處理序裝載，`CreateDefaultBuilder` 會將 [Kestrel](xref:fundamentals/servers/kestrel) 伺服器設為網頁伺服器，並設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)的基底路徑與連接埠來啟用 IIS 整合。

ASP.NET Core 模組會產生要指派給後端處理序的動態連接埠。 `CreateDefaultBuilder` 會呼叫 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 方法。 `UseIISIntegration` 會將 Kestrel 設定為在位於 localhost IP 位址 (`127.0.0.1`) 的動態連接埠上接聽。 若動態連接埠是 1234，Kestrel 會在 `127.0.0.1:1234` 接聽。 此設定會取代由下列項目提供的其他 URL 設定：

* `UseUrls`
* [Kestrel 的接聽 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [設定](xref:fundamentals/configuration/index) (或[命令列 --urls 選項](xref:fundamentals/host/web-host#override-configuration))

在使用模組時不需要呼叫 `UseUrls` 或 Kestrel 的 `Listen` API。 若呼叫 `UseUrls` 或 `Listen`，Kestrel 只會接聽未使用 IIS 執行應用程式時指定的連接埠。

如需處理序內和處理序外裝載模型的詳細資訊，請參閱 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)及 [ASP.NET Core 模組設定參考](xref:host-and-deploy/aspnet-core-module)。

::: moniker-end

::: moniker range="= aspnetcore-2.1"

`CreateDefaultBuilder` 會將 [Kestrel](xref:fundamentals/servers/kestrel) 伺服器設為網頁伺服器，並設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)的基底路徑與連接埠來啟用 IIS 整合。

ASP.NET Core 模組會產生要指派給後端處理序的動態連接埠。 `CreateDefaultBuilder` 會呼叫 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 方法。 `UseIISIntegration` 會將 Kestrel 設定為在位於 localhost IP 位址 (`127.0.0.1`) 的動態連接埠上接聽。 若動態連接埠是 1234，Kestrel 會在 `127.0.0.1:1234` 接聽。 此設定會取代由下列項目提供的其他 URL 設定：

* `UseUrls`
* [Kestrel 的接聽 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [設定](xref:fundamentals/configuration/index) (或[命令列 --urls 選項](xref:fundamentals/host/web-host#override-configuration))

在使用模組時不需要呼叫 `UseUrls` 或 Kestrel 的 `Listen` API。 若呼叫 `UseUrls` 或 `Listen`，Kestrel 只會接聽未使用 IIS 執行應用程式時指定的連接埠。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

`CreateDefaultBuilder` 會將 [Kestrel](xref:fundamentals/servers/kestrel) 伺服器設為網頁伺服器，並設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)的基底路徑與連接埠來啟用 IIS 整合。

ASP.NET Core 模組會產生要指派給後端處理序的動態連接埠。 `CreateDefaultBuilder` 會呼叫 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 方法。 `UseIISIntegration` 會將 Kestrel 設定為在位於 localhost IP 位址 (`localhost`) 的動態連接埠上接聽。 若動態連接埠是 1234，Kestrel 會在 `localhost:1234` 接聽。 此設定會取代由下列項目提供的其他 URL 設定：

* `UseUrls`
* [Kestrel 的接聽 API](xref:fundamentals/servers/kestrel#endpoint-configuration)
* [設定](xref:fundamentals/configuration/index) (或[命令列 --urls 選項](xref:fundamentals/host/web-host#override-configuration))

在使用模組時不需要呼叫 `UseUrls` 或 Kestrel 的 `Listen` API。 若呼叫 `UseUrls` 或 `Listen`，Kestrel 只會接聽未使用 IIS 執行應用程式時指定的連接埠。

::: moniker-end

::: moniker range="< aspnetcore-2.0"

在應用程式相依性的 [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 套件中包含相依性。 將 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 延伸模組新增到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 來使用 IIS 整合中介軟體：

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<xref:Microsoft.AspNetCore.Hosting.WebHostBuilderKestrelExtensions.UseKestrel*> 與 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilderIISExtensions.UseIISIntegration*> 都是必要項目。 呼叫 `UseIISIntegration` 的程式碼並不會影響程式碼的可攜性。 若應用程式不在 IIS 背後執行 (例如，應用程式直接在 Kestrel 上執行)，`UseIISIntegration` 就不會運作。

ASP.NET Core 模組會產生要指派給後端處理序的動態連接埠。 `UseIISIntegration` 會將 Kestrel 設定為在位於 localhost IP 位址 (`localhost`) 的動態連接埠上接聽。 若動態連接埠是 1234，Kestrel 會在 `localhost:1234` 接聽。 此設定會取代由下列項目提供的其他 URL 設定：

* `UseUrls`
* [設定](xref:fundamentals/configuration/index) (或[命令列 --urls 選項](xref:fundamentals/host/web-host#override-configuration))

使用模組時不需要呼叫 `UseUrls`。 若呼叫 `UseUrls`，Kestrel 只會接聽未使用 IIS 執行應用程式時指定的連接埠。

若要在 ASP.NET Core 1.0 應用程式上呼叫 `UseUrls`，請在呼叫 `UseIISIntegration`**前**予以呼叫，以避免模組設定的連接埠受到覆寫。 在 ASP.NET Core 1.1 中，因為模組設定會覆寫 `UseUrls`，所以不需要呼叫順序。

::: moniker-end

如需代管的詳細資訊，請參閱[在 ASP.NET Core 中代管](xref:fundamentals/index#host)。

### <a name="iis-options"></a>IIS 選項

::: moniker range=">= aspnetcore-2.2"

**同處理序主控模型**

若要設定 IIS 伺服器選項，請在 <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> 中加入 <xref:Microsoft.AspNetCore.Builder.IISServerOptions> 的服務設定。 下列範例會停用 AutomaticAuthentication：

```csharp
services.Configure<IISServerOptions>(options => 
{
    options.AutomaticAuthentication = false;
});
```

| 選項                         | 預設 | 設定 |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | 若為 `true`，IIS 伺服器會設定由 [Windows 驗證](xref:security/authentication/windowsauth)所驗證的 `HttpContext.User`。 若為 `false`，則伺服器僅會對 `HttpContext.User` 提供身分識別，並在 `AuthenticationScheme` 明確要求時回應挑戰。 必須在 IIS 中啟用 Windows 驗證以讓 `AutomaticAuthentication` 作用。 如需詳細資訊，請參閱 [Windows 驗證](xref:security/authentication/windowsauth)。 |
| `AuthenticationDisplayName`    | `null`  | 設定使用者在登入頁面上看到的顯示名稱。 |

**跨處理序裝載模型**

::: moniker-end

若要設定 IIS 選項，請在 <xref:Microsoft.AspNetCore.Hosting.IStartup.ConfigureServices*> 中加入 <xref:Microsoft.AspNetCore.Builder.IISOptions> 的服務設定。 下列範例會防止應用程式填入 `HttpContext.Connection.ClientCertificate`：

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| 選項                         | 預設 | 設定 |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | 若為 `true`，IIS 整合中介軟體會設定由 [Windows Authentication](xref:security/authentication/windowsauth) 所驗證的 `HttpContext.User`。 如果為 `false`，則驗證中介軟體僅針對 `HttpContext.User` 提供身分識別，並在游 `AuthenticationScheme` 提出明確要求時回應挑戰。 必須在 IIS 中啟用 Windows 驗證以讓 `AutomaticAuthentication` 作用。 如需詳細資訊，請參閱 [Windows 驗證](xref:security/authentication/windowsauth)主題。 |
| `AuthenticationDisplayName`    | `null`  | 設定使用者在登入頁面上看到的顯示名稱。 |
| `ForwardClientCertificate`     | `true`  | 如果為 `true` 且 `MS-ASPNETCORE-CLIENTCERT` 要求標頭已存在，則會填入 `HttpContext.Connection.ClientCertificate`。 |

### <a name="proxy-server-and-load-balancer-scenarios"></a>Proxy 伺服器和負載平衡器案例

用來設定轉送標頭中介軟體及 ASP.NET Core 模組的 IIS Integration 中介軟體會設定為轉送配置 (HTTP/HTTPS) 及發出要求的遠端 IP 位址。 其他 Proxy 伺服器和負載平衡器後方託管的應用程式可能需要其他設定。 如需詳細資訊，請參閱[設定 ASP.NET Core 以處理 Proxy 伺服器和負載平衡器](xref:host-and-deploy/proxy-load-balancer)。

### <a name="webconfig-file"></a>web.config 檔案

*web.config* 檔案是用來設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)。 發佈專案時，由 MSBuild 目標 (`_TransformWebConfig`) 處理 *web.config* 檔案的建立、轉換及發佈。 此目標存在於 Web SDK 目標 (`Microsoft.NET.Sdk.Web`)。 SDK 設定在專案檔的頂端：

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

如果專案中沒有 *web.config* 檔案，則系統會使用正確的 *processPath* 和 *arguments* 建立該檔案以設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)，並將該檔案移至[已發行的輸出](xref:host-and-deploy/directory-structure)。

如果 *web.config* 檔案存在於專案中，則系統會使用正確的 *processPath* 和 *arguments* 來轉換該檔案以設定 ASP.NET Core 模組，然後將它移至已發行的輸出。 轉換不會修改檔案中的 IIS 組態設定。

*web.config* 檔案可提供能控制作用中 IIS 模組的額外 IIS 組態設定。 如需能處理 ASP.NET Core 應用程式要求之 IIS 模組的相關資訊，請參閱 [IIS 模組](xref:host-and-deploy/iis/modules)主題。

為防止 Web SDK 轉換 *web.config* 檔案，請使用專案檔中的 **\<IsTransformWebConfigDisabled>** 屬性：

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

使 Web SDK 無法轉換檔案時，應該由開發人員手動設定 *processPath* 和 *arguments*。 如需詳細資訊，請參閱 [ASP.NET Core 模組組態參考](xref:host-and-deploy/aspnet-core-module)。

### <a name="webconfig-file-location"></a>web.config 檔案位置

為了正確設定 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)，*web.config* 檔案必須存在於已部署應用程式的內容根路徑 (通常是應用程式基底路徑)。 這是與提供給 IIS 的網站實體路徑相同的位置。 應用程式的根目錄需有 *web.config* 檔案，才能使用 Web Deploy 發行多個應用程式。

機密檔案存在於應用程式的實體路徑上，例如 *\<組件>.runtimeconfig.json*、*\<組件>.xml* (XML 文件註解)，以及 *\<組件>.deps.json*。 當 *web.config* 檔案存在且網站正常啟動時，在有人要求機密檔案的情況下，IIS 並不會提供它們。 若 *web.config* 檔案遺失或沒有正確命名，或是無法設定網站以正常啟動，IIS 可能會公開提供機密檔案。

***web.config* 檔案必須持續存在於部署之中、已正確命名，並能夠設定網站以正常啟動。無論在任何情況下，請都不要從生產環境部署移除 *web.config* 檔案。**

### <a name="transform-webconfig"></a>轉換 web.config

如需在發佈時轉換 *web.config* (例如依據設定、設定檔或環境設定環境變數)，請參閱<xref:host-and-deploy/iis/transform-webconfig>。

## <a name="iis-configuration"></a>IIS 組態

**Windows Server 作業系統**

啟用**網頁伺服器 (IIS)** 伺服器角色，並建立角色服務。

1. 使用來自 [管理] 功能表的 [新增角色及功能] 精靈，或是 [伺服器管理員] 中的連結。 在**伺服器角色**步驟中，核取 [網頁伺服器 (IIS)] 方塊。

   ![在選取伺服器角色步驟中選取網頁伺服器 IIS 角色。](index/_static/server-roles-ws2016.png)

1. 在 [功能] 步驟之後，[角色服務] 步驟會針對網頁伺服器 (IIS) 進行載入。 選取所需的 IIS 角色服務或接受所提供的預設角色服務。

   ![在選取角色服務步驟中，選取預設的角色服務。](index/_static/role-services-ws2016.png)

   **Windows 驗證 (選擇性)**  
   若要啟用 Windows 驗證，請展開下列節點：[網頁伺服器] > [安全性]。 選取 [Windows 驗證] 功能。 如需詳細資訊，請參閱 [Windows 驗證 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 和[設定 Windows 驗證](xref:security/authentication/windowsauth)。

   **WebSocket (選擇性)**  
   WebSocket 由 ASP.NET Core 1.1 或更新版本所支援。 若要啟用 WebSockets，請展開下列節點：[網頁伺服器] > [應用程式開發]。 選取 [WebSocket 通訊協定] 功能。 如需詳細資訊，請參閱 [WebSockets](xref:fundamentals/websockets)。

1. 透過**確認**步驟繼續作業，安裝網頁伺服器角色和服務。 安裝**網頁伺服器 (IIS)** 角色之後，不需要重新啟動伺服器/IIS。

**Windows 桌面作業系統**

啟用 [IIS 管理主控台] 和 [World Wide Web 服務]。

1. 瀏覽至控制台 > [程式] > [程式和功能] > [開啟或關閉 Windows 功能] (畫面左側)。

1. 開啟 [Internet Information Services] 節點。 開啟 [Web 管理工具] 節點。

1. 核取 [IIS 管理主控台] 方塊。

1. [World Wide Web Services] (全球資訊網服務) 核取方塊。

1. 接受**全球資訊網服務**的預設功能，或自訂 IIS 功能。

   **Windows 驗證 (選擇性)**  
   若要啟用 Windows 驗證，請展開下列節點：[World Wide Web 服務] > [安全性]。 選取 [Windows 驗證] 功能。 如需詳細資訊，請參閱 [Windows 驗證 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 和[設定 Windows 驗證](xref:security/authentication/windowsauth)。

   **WebSocket (選擇性)**  
   WebSocket 由 ASP.NET Core 1.1 或更新版本所支援。 若要啟用 WebSockets，請展開下列節點：[World Wide Web 服務] > [應用程式開發功能]。 選取 [WebSocket 通訊協定] 功能。 如需詳細資訊，請參閱 [WebSockets](xref:fundamentals/websockets)。

1. 若 IIS 安裝需要重新啟動，請重新啟動系統。

![選取 [Windows 功能] 中的 [IIS 管理主控台] 和 [World Wide Web Services] (全球資訊網服務)。](index/_static/windows-features-win10.png)

## <a name="install-the-net-core-hosting-bundle"></a>安裝 .NET Core 裝載套件組合

在主控系統上安裝 .NET Core 裝載套件組合。 套件組合會安裝 .NET Core 執行階段、.NET Core 程式庫和 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)。 此模組可讓 ASP.NET Core 應用程式在 IIS 背後執行。 如果系統沒有網際網路連線，請先取得並安裝 [Microsoft Visual C++ 2015 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=53840)，再安裝 .NET Core 裝載套件組合。

> [!IMPORTANT]
> 若裝載套件組合在 IIS 之前安裝，則必須對該套件組合安裝進行修復。 請在安裝 IIS 之後，再次執行裝載套件組合安裝程式。

### <a name="direct-download-current-version"></a>直接下載 (目前版本)

使用下列連結下載安裝程式：

[目前的 .NET Core 裝載套件組合安裝程式 (直接下載)](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

### <a name="earlier-versions-of-the-installer"></a>安裝程式的先前版本

若要取得安裝程式的先前版本：

1. 瀏覽至 [.NET 下載封存](https://www.microsoft.com/net/download/archives)。
1. 在 [.NET Core] 下，選取 .NET Core 版本。
1. 在 [執行應用程式 - 執行階段] 欄中，尋找想要的 .NET Core 執行階段版本列。
1. 使用**執行階段與裝載套件組合**連結。

> [!WARNING]
> 某些安裝程式包含已達到期生命週期結束 (EOL) 的發行版本，這些發行版本已不受 Microsoft 支援。 如需詳細資訊，請參閱[支援原則](https://www.microsoft.com/net/download/dotnet-core/2.0) \(英文 \)。

### <a name="install-the-hosting-bundle"></a>安裝裝載套件組合

1. 在伺服器上執行安裝程式。 從系統管理員命令殼層執行安裝程式時，有 下列參數可用：

   * `OPT_NO_ANCM=1` &ndash; 跳過安裝 ASP.NET Core 模組。
   * `OPT_NO_RUNTIME=1` &ndash; 跳過安裝 .NET Core 執行階段。
   * `OPT_NO_SHAREDFX=1` &ndash; 跳過安裝 ASP.NET 共用架構 (ASP.NET 執行階段)。
   * `OPT_NO_X86=1` &ndash; 跳過安裝 x86 執行階段。 當您確定不會裝載 32 位元應用程式時，請使用此參數。 如果將來有可能同時裝載 32 位元和 64 位元應用程式，請不要使用此參數並安裝這兩個執行階段。
   * `OPT_NO_SHARED_CONFIG_CHECK=1` &ndash; 停用使用 IIS 共用設定 (當共用設定 (*applicationHost.config*) 位於與 IIS 安裝相同的機器上時) 進行檢查。 *只在 ASP.NET Core 2.2 或更新版本的裝載套件組合安裝程式上可用。* 如需詳細資訊，請參閱<xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration>。
1. 請重新啟動系統，或是從命令殼層依序執行 **net stop was /y** 和 **net start w3svc**。 重新啟動 IIS 將能偵測到由安裝程式對系統路徑 (此為環境變數) 所做出的變更。

如果 Windows 裝載套件組合安裝程式偵測到 IIS 需要重設才能完成安裝，安裝程式會重設 IIS。 如果安裝程式觸發 IIS 重設，所有 IIS 應用程式集區和網站都會重新啟動。

> [!NOTE]
> 如需 IIS 共用組態的資訊，請參閱[使用 IIS 共用組態的 ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)。

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a>使用 Visual Studio 發佈時安裝 Web Deploy

將應用程式部署到具有 [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) 的伺服器時，請在伺服器上安裝最新版的 Web Deploy。 若要安裝 Web Deploy，請使用 [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) 或從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=43717)直接取得安裝程式。 慣用的方法是使用 WebPI。 WebPI 提供獨立的安裝程式和組態以裝載提供者。

## <a name="create-the-iis-site"></a>建立 IIS 網站

1. 在主控系統上，請建立資料夾以容納應用程式的已發行資料夾和檔案。 應用程式的部署配置已詳述於[目錄結構](xref:host-and-deploy/directory-structure)主題。

1. 在 [IIS 管理員] 中，於 [連線] 面板中開啟伺服器的節點。 以滑鼠右鍵按一下 [網站] 資料夾。 從操作功能表選取 [新增網站]。

1. 提供**網站名稱**，並將**實體路徑**設定為應用程式的部署資料夾。 透過選取 [確定] 來提供**繫結**設定並建立網站：

   ![在新增網站步驟中提供站台名稱、實體路徑和主機名稱。](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > 請**勿**使用最上層萬用字元繫結 (`http://*:80/`與 `http://+:80`)。 最上層萬用字元繫結可能暴露您的應用程式安全性弱點。 這對強式與弱式萬用字元皆適用。 請使用明確主機名稱，而非萬用字元。 若您擁有整個父網域 (與具弱點的 `*.com` 相對) 的控制權，則子網域萬用字元繫結 (例如 `*.mysub.com`) 就沒有此安全性風險。 如需詳細資訊，請參閱 [rfc7230 5.4 節](https://tools.ietf.org/html/rfc7230#section-5.4)。

1. 在伺服器的節點之下，選取 [應用程式集區]。

1. 以滑鼠右鍵按一下網站的應用程式集區，然後從操作功能表選取 [基本設定]。

1. 在 [編輯應用程式集區] 視窗中，將 [.NET CLR 版本] 設定為 [沒有受控碼]：

   ![將 .NET CLR 版本設為 [沒有受控碼]。](index/_static/edit-apppool-ws2016.png)

    ASP.NET Core 會在不同的處理序中執行，並管理執行階段。 ASP.NET Core 不依賴載入桌面 CLR。 將 [.NET CLR 版本] 設為 [沒有受控碼] 是選擇性的。

1. *ASP.NET Core 2.2 或更新版本*：對於使用[同處理序主控模型](xref:fundamentals/servers/index#in-process-hosting-model)的 64 位元 (x64) [自封式部署](/dotnet/core/deploying/#self-contained-deployments-scd)，會停用 32 位元 (x86) 處理序的應用程式集區。

   在 IIS 管理員的 [動作] 資訊看板 > [應用程式集區] 中，選取 [設定應用程式集區預設值] 或 [進階設定]。 找到 [啟用 32 位元應用程式]，然後將其值設定為 `False`。 此設定不會影響為[處理程序外裝載](xref:host-and-deploy/aspnet-core-module#out-of-process-hosting-model)部署的應用程式。

1. 確認處理序模型身分識別具有適當的權限。

   如果您將應用程式集區的預設身分識別 ([處理序模型] > [身分識別]) 從 **ApplicationPoolIdentity** 變更為其他身分識別，請確認新的身分識別具有必要權限，可存取應用程式的資料夾、資料庫和其他必要的資源。 例如，應用程式集區需要針對應用程式讀取和寫入檔案的資料夾取得讀取和寫入權限。

**Windows 驗證設定 (選擇性)**  
如需詳細資訊，請參閱[設定 Windows 驗證](xref:security/authentication/windowsauth)主題。

## <a name="deploy-the-app"></a>部署應用程式

將應用程式部署至在主控系統上建立的資料夾。 [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) 是建議的部署機制。

### <a name="web-deploy-with-visual-studio"></a>使用 Visual Studio 的 Web Deploy

請參閱[適用於 ASP.NET Core 應用程式部署的 Visual Studio 發行設定檔](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles)主題，了解如何建立搭配 Web Deploy 使用的發行設定檔。 如果裝載提供者提供或支援建立發行設定檔，請下載其設定檔，並使用 Visual Studio 的 [發行] 對話方塊匯入其設定檔。

![[發佈] 對話方塊頁](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a>Visual Studio 外部的 Web Deploy

透過命令列也可以在 Visual Studio 外部使用 [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy)。 如需詳細資訊，請參閱 [Web 部署工具](/iis/publish/using-web-deploy/use-the-web-deployment-tool)。

### <a name="alternatives-to-web-deploy"></a>Web Deploy 的替代項目

使用數種方法的其中一種將應用程式移到主控系統，例如手動複製、Xcopy、Robocopy 或 PowerShell。

如需 IIS 的 ASP.NET Core 部署詳細資訊，請參閱 [IIS 系統管理員的部署資源](#deployment-resources-for-iis-administrators)一節。

## <a name="browse-the-website"></a>瀏覽網站

![Microsoft Edge 瀏覽器已載入 IIS 啟動頁面。](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a>已鎖定的部署檔案

當應用程式執行時，會鎖定部署資料夾中的檔案。 無法於部署期間覆寫已鎖定的檔案。 若要釋放部署中的已鎖定檔案，請使用下列其中**一種**方法停止應用程式集區：

* 使用 Web Deploy 並參考專案檔中的 `Microsoft.NET.Sdk.Web`。 *app_offline.htm* 檔案是放在 Web 應用程式目錄的根目錄中。 當檔案存在時，ASP.NET Core 模組會正常關閉應用程式，並在部署期間提供 *app_offline.htm* 檔案。 如需詳細資訊，請參閱 [ASP.NET Core 模組組態參考](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)。
* 在伺服器上的 IIS 管理員中手動停止應用程式集區。
* 使用 PowerShell 卸除 *app_offline.html* (需要 PowerShell 5 或更新版本)：

  ```PowerShell
  $pathToApp = 'PATH_TO_APP'

  # Stop the AppPool
  New-Item -Path $pathToApp app_offline.htm

  # Provide script commands here to deploy the app

  # Restart the AppPool
  Remove-Item -Path $pathToApp app_offline.htm

  ```

## <a name="data-protection"></a>資料保護

[ASP.NET Core 資料保護堆疊](xref:security/data-protection/introduction)是由數個 ASP.NET Core [中介軟體](xref:fundamentals/middleware/index)所使用，包括用於驗證的中介軟體。 即使資料保護 API 不是由使用者程式碼呼叫，仍應使用部署指令碼或是在使用者程式碼中設定資料保護，以建立持續性的密碼編譯[金鑰存放區](xref:security/data-protection/implementation/key-management)。 如不設定資料保護，金鑰會保留在記憶體中，並於應用程式重新啟動時捨棄。

如果 Keyring 儲存在記憶體中，則當應用程式重新啟動時：

* 所有以 Cookie 為基礎的驗證權杖都會失效。 
* 當使用者提出下一個要求時，需要再次登入。 
* 所有以 Keyring 保護的資料都無法再解密。 這可能會包含 [CSRF 權杖](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration)和 [ASP.NET Core MVC TempData cookie](xref:fundamentals/app-state#tempdata)。

若要在 IIS 下設定資料保護以保存 Keyring，請使用下列其中**一種**方法：

* **建立資料保護登錄機碼**

  ASP.NET Core 應用程式所使用的資料保護金鑰會儲存在應用程式外部的登錄中。 若要保存指定應用程式的金鑰，請為應用程式集區建立登錄機碼。

  若為獨立的非Web 伺服陣列 IIS 安裝，請針對搭配使用 ASP.NET Core 應用程式的每個應用程式集區，使用[資料保護 Provision-AutoGenKeys.ps1 PowerShell 指令碼](https://github.com/aspnet/AspNetCore/blob/master/src/DataProtection/Provision-AutoGenKeys.ps1)。 此指令碼會在 HKLM 登錄中建立登錄機碼，只有應用程式之應用程式集區的背景工作處理序帳戶可以存取它。 在待用期間使用 DPAPI 和全電腦金鑰加密金鑰。

  在 Web 伺服陣列案例中，應用程式可以設定成使用 UNC 路徑來儲存其資料保護 Keyring。 根據預設，資料保護金鑰不予加密。 請確保網路共用的檔案權限僅限於執行應用程式的 Windows 帳戶。 可以使用 X509 憑證來保護待用的金鑰。 請考慮下列讓使用者上傳憑證的機制：將憑證放入使用者的受信任憑證存放區，並確保在執行使用者應用程式的所有電腦上都能使用這些憑證。 如需詳細資訊，請參閱[設定 ASP.NET Core 資料保護](xref:security/data-protection/configuration/overview)。

* **設定 IIS 應用程式集區載入使用者設定檔**

  此設定位在應用程式集區 [進階設定] 下的 [處理序模型] 區段中。 將 [載入使用者設定檔] 設為 `True`。 當設定為 `True` 時，金鑰會儲存在使用者設定檔目錄中，且使用具有使用者帳戶專屬金鑰的 DPAPI 保護。 金鑰會保存到 *%LOCALAPPDATA%/ASP.NET/DataProtection-Keys* 資料夾。

  應用程式集區的 [setProfileEnvironment 屬性](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration)也必須啟用。 `setProfileEnvironment` 的預設值為 `true`。 在某些情況下 (例如 Windows OS)，`setProfileEnvironment` 會設為 `false`。 如果金鑰並未如預期地儲存在使用者設定檔目錄中：

  1. 瀏覽至 *%windir%/system32/inetsrv/config* 資料夾。
  1. 開啟 *applicationHost.config* 檔案。
  1. 找到 `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>` 項目。
  1. 確認 `setProfileEnvironment` 屬性不存在 (其預設值為 `true`)，或明確地將屬性值設為 `true`。

* **將檔案系統當作 Keyring 存放區使用**

  調整應用程式程式碼，以[將檔案系統當作 Keyring 存放區使用](xref:security/data-protection/configuration/overview)。 使用 X509 憑證來保護 Keyring，並確保憑證是受信任的憑證。 如果憑證為自我簽署，請將憑證放在受信任的根存放區。

  在 Web 伺服陣列中使用 IIS 時：

  * 請使用所有電腦都可以存取的檔案共用。
  * 將 X509 憑證部署到每一部電腦。 設定[程式碼中的資料保護](xref:security/data-protection/configuration/overview)。

* **設定資料保護的全電腦原則**

  針對取用資料保護 API 的所有應用程式，資料保護系統僅支援有限的預設[全電腦原則](xref:security/data-protection/configuration/machine-wide-policy)設定。 如需詳細資訊，請參閱<xref:security/data-protection/introduction>。

## <a name="virtual-directories"></a>虛擬目錄

ASP.NET Core 應用程式不支援 [IIS 虛擬目錄](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#virtual-directories)。 應用程式能以[子應用程式](#sub-applications)的形式裝載。

## <a name="sub-applications"></a>子應用程式

ASP.NET Core 應用程式能以 [IIS 子應用程式](/iis/get-started/planning-your-iis-architecture/understanding-sites-applications-and-virtual-directories-on-iis#applications)的形式裝載。 子應用程式的路徑會成為根應用程式 URL 的一部分。

::: moniker range="< aspnetcore-2.2"

子應用程式不應該包括 ASP.NET Core 模組做為處理常式。 如果您在子應用程式的 *web.config* 檔案中將模組新增為處理常式，則嘗試瀏覽子應用程式時，會收到參考錯誤設定檔的 *500.19 內部伺服器錯誤*。

下列範例顯示 ASP.NET Core 子應用程式的已發佈 *web.config* 檔案：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

在 ASP.NET Core 應用程式下裝載非 ASP.NET Core 子應用程式時，請明確移除子應用程式 *web.config* 檔案中已繼承的處理常式：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\MyApp.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

子應用程式內的靜態資產連結應該使用波狀符號與斜線 (`~/`) 標記法。 波狀符號與斜線標記法會觸發[標記協助程式](xref:mvc/views/tag-helpers/intro)以將子應用程式的路徑基底附加到轉譯的相對連結前面。 針對位於 `/subapp_path` 的子應用程式，使用 `src="~/image.png"` 連結的影像會轉譯為 `src="/subapp_path/image.png"`。 根應用程式的靜態檔案中介軟體不會處理靜態檔案要求。 要求會由子應用程式的靜態檔案中介軟體處理。

若靜態資產的 `src` 屬性是設定為絕對路徑 (例如，`src="/image.png"`)，會以不使用子應用程式路徑基底的方式轉譯連結。 根應用程式的靜態檔案中介軟體會嘗試從根應用程式的 [webroot](xref:fundamentals/index#web-root) 提供資產，這會導致「404 - 找不到」回應 (除非根應用程式可存取靜態資產)。

裝載 ASP.NET Core 應用程式做為另一個 ASP.NET Core 應用程式下的子應用程式：

1. 為子應用程式建立應用程式集區。 將 [.NET CLR 版本] 設定為 [沒有 Managed 程式碼]。

1. 使用根網站下資料夾中的子應用程式在 IIS 管理員中新增根網站。

1. 以滑鼠右鍵按一下 IIS 管理員中的子應用程式資料夾，然後選取 [轉換成應用程式]。

1. 在 [新增應用程式] 對話方塊中，使用 [應用程式集區] 的[選取] 按鈕來指派您為子應用程式建立的應用程式集區。 選取 [確定]。

將不同的應用程式集區指派給子應用程式是使用同處理序裝載模型。

如需有關同處理序裝載模型與如何設定 ASP.NET Core 模組的詳細資訊，請參閱 <xref:host-and-deploy/aspnet-core-module> 與 <xref:host-and-deploy/aspnet-core-module>。

## <a name="configuration-of-iis-with-webconfig"></a>使用 web.config 的 IIS 組態

在對使用了 ASP.NET Core 模組的 ASP.NET Core 有作用的 IIS 情境下，設定會受 *web.config* 的 `<system.webServer>` 區段影響。 舉例來說，IIS 設定對動態壓縮有作用。 如果在伺服器層級將 IIS 設為使用動態壓縮，應用程式 *web.config* 檔案中的 `<urlCompression>` 元素則可為 ASP.NET Core 應用程式予以停用。

如需詳細資訊，請參閱 [\<system.webServer> 的設定參考](/iis/configuration/system.webServer/)、[ASP.NET Core 模組設定參考](xref:host-and-deploy/aspnet-core-module)以及 [IIS 模組與 ASP.NET Core](xref:host-and-deploy/iis/modules)。 若要設定在隔離的應用程式集區中執行之個別應用程式的環境變數 (支援 IIS 10.0 或更新版本)，請參閱 IIS 參考文件之[環境變數 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主題的 *AppCmd.exe 命令*一節。

## <a name="configuration-sections-of-webconfig"></a>web.config 的組態區段

ASP.NET Core 應用程式的設定不使用 *web.config* 中 ASP.NET 4.x 應用程式的設定區段：

* `<system.web>`
* `<appSettings>`
* `<connectionStrings>`
* `<location>`

使用其他組態提供者設定的 ASP.NET Core 應用程式。 如需詳細資訊，請參閱[組態](xref:fundamentals/configuration/index)。

## <a name="application-pools"></a>應用程式集區

::: moniker range=">= aspnetcore-2.2"

應用程式集區隔離取決於裝載模型：

* 處理序內裝載 &ndash; 應用程式必須在分開的應用程式集區中執行。
* 處理序外裝載 &ndash; 建議藉由在各自的應用程式集區中執行每個應用程式，以將應用程式互相隔離。

IIS [新增網站] 對話方塊預設每個應用程式皆為單一應用程式集區。 當提供 [網站名稱] 時，文字會自動轉移至 [應用程式集區] 文字方塊。 新增網站時，會使用該網站名稱建立新的應用程式集區。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

在伺服器上裝載多個網站時，建議您在其各自的應用程式集區中執行各個應用程式，讓應用程式彼此隔離。 IIS [新增網站] 對話方塊預設成此組態。 當提供 [網站名稱] 時，文字會自動轉移至 [應用程式集區] 文字方塊。 新增網站時，會使用該網站名稱建立新的應用程式集區。

::: moniker-end

## <a name="application-pool-identity"></a>應用程式集區身分識別

應用程式集區身分識別帳戶可讓應用程式在唯一的帳戶下執行，不必建立及管理網域或本機帳戶。 在 IIS 8.0 或更新版本中，IIS 管理背景工作處理序 (WAS) 會使用新的應用程式集區名稱建立虛擬帳戶，並預設在此帳戶下執行應用程式集區的背景工作處理序。 在 IIS 管理主控台中，於應用程式集區的 [進階設定] 下，確定 [身分識別] 設定為使用 **ApplicationPoolIdentity**：

![應用程式集區進階設定對話方塊](index/_static/apppool-identity.png)

IIS 管理程序會在 Windows 安全系統中，以應用程式集區的名稱建立安全識別碼。 可使用此身分識別來保護資源。 不過，此身分識別不是真正的使用者帳戶，也不會顯示在 Windows 使用者管理主控台中。

如果 IIS 背景工作處理序需要提升應用程式的存取權限，請修改包含應用程式的目錄存取控制清單 (ACL)：

1. 開啟 Windows 檔案總管，巡覽至目錄。

1. 以滑鼠右鍵按一下目錄並選取 [屬性]。

1. 依序選取 [安全性] 索引標籤下的 [編輯] 按鈕和 [新增] 按鈕。

1. 選取 [位置] 按鈕，並確定選取系統。

1. 在 [輸入要選取的物件名稱] 區域中，輸入 **IIS AppPool\\<app_pool_name>**。 選取 [檢查名稱] 按鈕。 針對 [DefaultAppPool]，請使用 **IIS AppPool\DefaultAppPool** 檢查名稱。 選取 [檢查名稱] 按鈕時，[DefaultAppPool] 的值便會顯示於物件名稱區域中。 您無法直接將應用程式集區名稱輸入至物件名稱區域。 檢查物件名稱時，請使用 **IIS AppPool\\<app_pool_name>** 的格式。

   ![針對應用程式資料夾選取使用者或群組對話方塊：在選取 [檢查名稱] 之前，"DefaultAppPool" 這個應用程式集區名稱在物件名稱區域中會附加至 "IIS AppPool\"。](index/_static/select-users-or-groups-1.png)

1. 選取 [確定]。

   ![針對應用程式資料夾選取使用者或群組對話方塊：選取 [檢查名稱] 之後，物件名稱 "DefaultAppPool" 會顯示在物件名稱區域中。](index/_static/select-users-or-groups-2.png)

1. 預設應該會授與讀取 &amp; 執行權限。 請視需要提供其他權限。

也可使用 **ICACLS** 工具透過命令提示字元授與存取權限。 使用 *DefaultAppPool*作為範例，將會使用下列命令：

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

如需詳細資訊，請參閱 [icacls](/windows-server/administration/windows-commands/icacls) 主題。

## <a name="http2-support"></a>HTTP/2 支援

::: moniker range=">= aspnetcore-2.2"

在下列 IIS 部署案例中，ASP.NET Core 支援 [HTTP/2](https://httpwg.org/specs/rfc7540.html)：

* 同處理序
  * Windows Server 2016/Windows 10 或更新版本；IIS 10 或更新版本
  * TLS 1.2 或更新版本連線
* 跨處理序
  * Windows Server 2016/Windows 10 或更新版本；IIS 10 或更新版本
  * 公開 Edge Server 連線使用 HTTP/2，但是對 [Kestrel 伺服器](xref:fundamentals/servers/kestrel)的反向 Proxy 連線使用 HTTP/1.1。
  * TLS 1.2 或更新版本連線

針對建立 HTTP/2 連線時的同處理序部署，[HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) 會回報 `HTTP/2`。 針對建立 HTTP/2 連線時的跨處理序部署，[HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) 會回報 `HTTP/1.1`。

如需有關同處理序和跨處理序主控模型的詳細資訊，請參閱 <xref:host-and-deploy/aspnet-core-module> 主題和 <xref:host-and-deploy/aspnet-core-module>。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

[HTTP/2](https://httpwg.org/specs/rfc7540.html) 支援符合下列基本需求的跨處理序部署：

* Windows Server 2016/Windows 10 或更新版本；IIS 10 或更新版本
* 公開 Edge Server 連線使用 HTTP/2，但是對 [Kestrel 伺服器](xref:fundamentals/servers/kestrel)的反向 Proxy 連線使用 HTTP/1.1。
* 目標 Framework：不適用於跨處理序部署，因為 HTTP/2 連線完全由 IIS 處理。
* TLS 1.2 或更新版本連線

如果已建立 HTTP/2 連線，[HttpRequest.Protocol](xref:Microsoft.AspNetCore.Http.HttpRequest.Protocol*) 會報告 `HTTP/1.1`。

::: moniker-end

HTTP/2 預設為啟用。 如果 HTTP/2 連線尚未建立，連線會退為 HTTP/1.1。 如需使用 IIS 部署之 HTTP/2 設定的詳細資訊，請參閱 [IIS 上的 HTTP/2](/iis/get-started/whats-new-in-iis-10/http2-on-iis)。

## <a name="cors-preflight-requests"></a>CORS 預檢要求

*此節只適用於以 .NET Framework 為目標的 ASP.NET Core 應用程式。*

針對以 .NET Framework 為目標的 ASP.NET Core 應用程式，在 IIS 中OPTIONS 要求預設不會傳遞到應用程式。 若要了解如何在 *web.config* 中設定應用程式的 IIS 處理常式以傳遞 OPTIONS 要求，請參閱[在 ASP.NET Web API 2 中啟用跨原始來源要求：CORS 如何運作](/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api#how-cors-works)。

## <a name="deployment-resources-for-iis-administrators"></a>IIS 系統管理員的部署資源

請參閱 IIS 文件以深入了解 IIS。  
[IIS 文件](/iis)

了解 .NET Core 應用程式部署模型。  
[.NET Core 應用程式部署](/dotnet/core/deploying/)

了解 ASP.NET Core 模組如何讓 Kestrel Web 伺服器將 IIS 或 IIS Express 作為反向 Proxy 伺服器使用。  
[ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)

了解如何設定 ASP.NET Core 模組以裝載 ASP.NET Core 應用程式。  
[ASP.NET Core 模組組態參考](xref:host-and-deploy/aspnet-core-module)

了解已發行之 ASP.NET Core 應用程式的目錄結構。  
[目錄結構](xref:host-and-deploy/directory-structure)

探索 ASP.NET Core 應用程式的使用中和非使用中 IIS 模組，管理 IIS 模組的方式。  
[IIS 模組](xref:host-and-deploy/iis/troubleshoot)

了解如何診斷 ASP.NET Core 應用程式的 IIS 部署問題。  
[疑難排解](xref:host-and-deploy/iis/troubleshoot)

區分在 IIS 上裝載 ASP.NET Core 應用程式時的常見錯誤。  
[Azure App Service 和 IIS 常見的錯誤參考](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a>其他資源

* <xref:test/troubleshoot>
* [ASP.NET Core 簡介](xref:index)
* [Microsoft IIS 官方網站](https://www.iis.net/)
* [Windows Server 技術內容庫](/windows-server/windows-server)
* [ISS 上的 HTTP/2](/iis/get-started/whats-new-in-iis-10/http2-on-iis)
* <xref:host-and-deploy/iis/transform-webconfig>
