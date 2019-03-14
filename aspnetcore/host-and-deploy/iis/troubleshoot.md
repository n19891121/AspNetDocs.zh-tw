---
title: 針對 IIS 上的 ASP.NET Core 進行疑難排解
author: guardrex
description: 了解如何診斷 ASP.NET Core 應用程式的 Internet Information Services (IIS) 部署問題。
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: 68fcd578c051ae9ba6234cad0465a7ef42f1ed14
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57035585"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>針對 IIS 上的 ASP.NET Core 進行疑難排解

作者：[Luke Latham](https://github.com/guardrex)

本文說明以 [Internet Information Services (IIS)](/iis) 裝載 ASP.NET Core 應用程式時，如何診斷此應用程式的啟動問題。 本文中資訊適用的裝載環境是 Windows Server 和 Windows 桌面上的 IIS。

::: moniker range=">= aspnetcore-2.2"

在 Visual Studio 中，進行偵錯時，ASP.NET Core 專案會預設為 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 裝載環境。 在本機偵錯時發生的「502.5 - 處理序失敗」或「500.30 - 啟動失敗」可以使用本主題中的建議在該位置進行疑難排解。

::: moniker-end

::: moniker range="< aspnetcore-2.2"

在 Visual Studio 中，進行偵錯時，ASP.NET Core 專案會預設為 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 裝載環境。 在本機偵錯時發生的「502.5 處理序失敗」可以使用本主題中的建議來進行疑難排解。

::: moniker-end

其他疑難排解主題：

<xref:host-and-deploy/azure-apps/troubleshoot>  
雖然 App Service 使用 [ASP.NET Core 模組](xref:host-and-deploy/aspnet-core-module)和 IIS 來裝載應用程式，但如需 App Service 特定的指示，請參閱其專屬的主題。

<xref:fundamentals/error-handling>  
了解在本機系統上進行開發時，如何處理 ASP.NET Core 應用程式中的錯誤。

[了解使用 Visual Studio 進行偵錯](/visualstudio/debugger/getting-started-with-the-debugger)  
本主題將介紹 Visual Studio 偵錯工具的功能。

[使用 Visual Studio Code 進行偵錯](https://code.visualstudio.com/docs/editor/debugging) \(英文\)  
了解 Visual Studio Code 中內建的偵錯支援。

## <a name="app-startup-errors"></a>應用程式啟動錯誤

### <a name="5025-process-failure"></a>502.5 處理序失敗

背景工作處理序失敗。 應用程式未啟動。

ASP.NET Core 模組嘗試啟動後端 dotnet 處理序，但無法啟動。 通常從[應用程式事件記錄檔](#application-event-log)和 [ASP.NET Core 模組 stdout 記錄檔](#aspnet-core-module-stdout-log)中的項目，即可判斷啟動失敗的原因。 

因為目標 ASP.NET Core 共用架構的版本不存在，導致應用程式設定錯誤是常見的失敗狀況。 請檢查安裝在目標機器上的 ASP.NET Core 共用架構版本為何。

當裝載或應用程式設定錯誤造成背景工作處理序發生失敗時，會傳回 [502.5 處理序失敗] 錯誤頁面：

![顯示 [502.5 處理序失敗] 頁面的瀏覽器視窗](troubleshoot/_static/process-failure-page.png)

::: moniker range=">= aspnetcore-2.2"

### <a name="50030-in-process-startup-failure"></a>500.30 同處理序啟動失敗

背景工作處理序失敗。 應用程式未啟動。

ASP.NET Core 模組嘗試啟動 .NET Core CLR 同處理序，但無法啟動。 通常從[應用程式事件記錄檔](#application-event-log)和 [ASP.NET Core 模組 stdout 記錄檔](#aspnet-core-module-stdout-log)中的項目，即可判斷啟動失敗的原因。 

因為目標 ASP.NET Core 共用架構的版本不存在，導致應用程式設定錯誤是常見的失敗狀況。 請檢查安裝在目標機器上的 ASP.NET Core 共用架構版本為何。

### <a name="5000-in-process-handler-load-failure"></a>500.0 同處理序處理常式載入失敗

背景工作處理序失敗。 應用程式未啟動。

The ASP.NET Core 模組找不到 .NET Core CLR，並尋找同處理序要求處理常式 (*aspnetcorev2_inprocess.dll*)。 請檢查︰

* 應用程式以 [Microsoft.AspNetCore.Server.IIS](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IIS) NuGet 套件或 [Microsoft.AspNetCore.App 中繼套件](xref:fundamentals/metapackage-app)為目標。
* 應用程式設為目標的 ASP.NET Core 共用架構版本有安裝在目標機器上。

### <a name="5000-out-of-process-handler-load-failure"></a>500.0 跨處理序處理常式載入失敗

背景工作處理序失敗。 應用程式未啟動。

ASP.NET Core 模組找不到跨處理序裝載要求處理常式。 請確定 *aspnetcorev2_outofprocess.dll* 出現在子資料夾中，且位於 *aspnetcorev2.dll* 旁。 

::: moniker-end

### <a name="500-internal-server-error"></a>500 內部伺服器錯誤

應用程式啟動，但有錯誤導致伺服器無法完成要求。

此錯誤是在啟動或建立回應時，在應用程式的程式碼內發生。 回應可能未包含任何內容，或是回應可能在瀏覽器中以「500 內部伺服器錯誤」的形式出現。 「應用程式事件記錄檔」通常會指出該應用程式已正常啟動。 從伺服器的觀點來看，這是正確的。 應用程式已啟動，但無法產生有效的回應。 請在伺服器上[於命令提示字元中執行應用程式](#run-the-app-at-a-command-prompt)或[啟用 ASP.NET Core 模組 stdout 記錄檔](#aspnet-core-module-stdout-log)，以針對問題進行疑難排解。

### <a name="failed-to-start-application-errorcode-0x800700c1"></a>無法啟動應用程式 (ErrorCode '0x800700c1')

```
EventID: 1010
Source: IIS AspNetCore Module V2
Failed to start application '/LM/W3SVC/6/ROOT/', ErrorCode '0x800700c1'.
```

應用程式無法啟動，因為無法載入應用程式的組件 (*.dll*)。

當已發行的應用程式與 w3wp/iisexpress 處理序之間出現位元不符的情況時，就會發生此錯誤。

確認應用程式集區的 32 位元設定正確：

1. 在 IIS 管理員的 [應用程式集區] 中，選取應用程式集區。
1. 在 [動作] 面板中，選取 [編輯應用程式集區] 下的 [進階設定]。
1. 設定 [啟用 32 位元應用程式]：
   * 如果部署 32 位元 (x86) 應用程式，請將值設定為 `True`。
   * 如果部署 64 位元 (x64) 應用程式，請將值設定為 `False`。

### <a name="connection-reset"></a>連線重設

如果是在傳送標頭之後才發生錯誤，則當發生錯誤時，伺服器已來不及傳送「500 內部伺服器錯誤」。 通常是在將回應的複雜物件序列化的期間發生錯誤時，會發生此錯誤。 這類錯誤會在用戶端上顯示為「連線重設」錯誤。 [應用程式記錄](xref:fundamentals/logging/index)可協助針對這些類型的錯誤進行疑難排解。

## <a name="default-startup-limits"></a>預設啟動限制

ASP.NET Core 模組上已設定預設的 *startupTimeLimit* 120 秒。 保留預設值時，在模組記錄處理序失敗之前，應用程式最多可花費兩分鐘來進行啟動。 如需有關設定模組的資訊，請參閱 [aspNetCore 元素的屬性](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。

## <a name="troubleshoot-app-startup-errors"></a>針對應用程式啟動錯誤進行疑難排解

### <a name="enable-the-aspnet-core-module-debug-log"></a>啟用 ASP.NET Core 模組偵錯記錄

將下列處理常式設定新增至應用程式的 *web.config* 檔案，以啟用 ASP.NET Core 模組偵錯記錄：

```xml
<aspNetCore ...>
  <handlerSettings>
    <handlerSetting name="debugLevel" value="file" />
    <handlerSetting name="debugFile" value="c:\temp\ancm.log" />
  </handlerSettings>
</aspNetCore>
```

確認為記錄指定的路徑存在，而且應用程式集區的身分識別具有該位置的寫入權限。

### <a name="application-event-log"></a>應用程式事件記錄檔

存取「應用程式事件記錄檔」：

1. 開啟 [開始] 功能表，搜尋**事件檢視器**，然後選取 [事件檢視器]應用程式。
1. 在 [事件檢視器] 中，開啟 [Windows 記錄] 節點。
1. 選取 [應用程式] 以開啟「應用程式事件記錄檔」。
1. 搜尋與失敗應用程式相關的錯誤。 錯誤在 [來源] 資料行中的值會是 *IIS AspNetCore Module* 或 *IIS Express AspNetCore Module*。

### <a name="run-the-app-at-a-command-prompt"></a>在命令提示字元中執行應用程式

許多啟動錯誤不會在「應用程式事件記錄檔」中產生實用的資訊。 您可以藉由在主控系統上的命令提示字元中執行應用程式，來找出一些錯誤的原因。

#### <a name="framework-dependent-deployment"></a>與 Framework 相依的部署

如果應用程式是[架構相依部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)：

1. 在命令提示字元中，瀏覽至部署資料夾，然後使用 *dotnet.exe* 來執行應用程式組件以執行應用程式。 在下列命令中，請以應用程式組件的名稱取代 \<assembly_name>：`dotnet .\<assembly_name>.dll`。
1. 來自應用程式的主控台輸出若有顯示任何錯誤，就會寫入至主控台視窗。
1. 如果是在對應用程式發出要求時發生錯誤，請對 Kestrel 進行接聽的主機和連接埠發出要求。 如果使用預設主機和連接埠，請對 `http://localhost:5000/` 發出要求。 如果應用程式在 Kestrel 端點位址正常回應，則問題與主機組態有關的機率較大，而與應用程式本身有關的機率較小。

#### <a name="self-contained-deployment"></a>自封式部署

如果應用程式是[自封式部署](/dotnet/core/deploying/#self-contained-deployments-scd)：

1. 在命令提示字元中，瀏覽至部署資料夾，然後執行應用程式的可執行檔。 在下列命令中，請以應用程式組件的名稱取代 \<assembly_name>：`<assembly_name>.exe`。
1. 來自應用程式的主控台輸出若有顯示任何錯誤，就會寫入至主控台視窗。
1. 如果是在對應用程式發出要求時發生錯誤，請對 Kestrel 進行接聽的主機和連接埠發出要求。 如果使用預設主機和連接埠，請對 `http://localhost:5000/` 發出要求。 如果應用程式在 Kestrel 端點位址正常回應，則問題與主機組態有關的機率較大，而與應用程式本身有關的機率較小。

### <a name="aspnet-core-module-stdout-log"></a>ASP.NET Core 模組 stdout 記錄檔

啟用及檢視 stdout 記錄檔：

1. 瀏覽至主控系統上網站的部署資料夾。
1. 如果 [logs] 資料夾不存在，請建立該資料夾。 如需有關如何讓 MSBuild 在部署中自動建立 [logs] 資料夾的指示，請參閱[目錄結構](xref:host-and-deploy/directory-structure)主題。
1. 編輯 *web.config* 檔案。 將 **stdoutLogEnabled** 設定為 `true`，並將 **stdoutLogFile** 路徑變更為指向 [logs] 資料夾 (例如 `.\logs\stdout`)。 路徑中的 `stdout` 是記錄檔名稱前置詞。 建立記錄檔時，系統會自動新增時間戳記、處理序識別碼及副檔名。 使用 `stdout` 作為檔案名稱前置詞時，一般記錄檔會命名為 *stdout_20180205184032_5412.log*。 
1. 請確定您的應用程式集區身分識別具有 *logs* 資料夾的寫入權限。
1. 儲存已更新的 *web.config* 檔案。
1. 對應用程式發出要求。
1. 瀏覽至 [logs] 資料夾。 尋找並開啟最新的 stdout 記錄檔。
1. 研究記錄檔以了解錯誤。

> [!IMPORTANT]
> 完成疑難排解時，請停用 stdout 記錄。

1. 編輯 *web.config* 檔案。
1. 將 **stdoutLogEnabled** 設定為 `false`。
1. 儲存檔案。

> [!WARNING]
> 如果無法停用 stdout 記錄檔，可能會造成應用程式或伺服器發生失敗。 因為它並沒有記錄檔大小或數量上的限制。
>
> 針對 ASP.NET Core 應用程式中的例行性記錄，請使用會限制記錄檔大小並輪替記錄檔的記錄程式庫。 如需詳細資訊，請參閱[協力廠商記錄提供者](xref:fundamentals/logging/index#third-party-logging-providers)。

## <a name="enable-the-developer-exception-page"></a>啟用開發人員例外頁面

在開發環境中，可以將 `ASPNETCORE_ENVIRONMENT` [環境變數新增至 web.config](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 來執行應用程式。 只要主機產生器上的 `UseEnvironment` 不會覆寫應用程式啟動內的環境，設定該環境變數便可允許在應用程式執行時顯示[開發人員例外狀況頁面](xref:fundamentals/error-handling)。

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout"
      hostingModel="InProcess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

只有在沒有對網際網路公開的暫存和測試伺服器上使用時，才建議為 `ASPNETCORE_ENVIRONMENT` 設定環境變數。 進行疑難排解之後，請從 *web.config* 檔案中移除環境變數。 如需有關在 *web.config* 中設定環境變數的資訊，請參閱 [aspNetCore 的 environmentVariables 子元素](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)。

## <a name="common-startup-errors"></a>常見的啟動錯誤

請參閱 <xref:host-and-deploy/azure-iis-errors-reference>。 參考主題涵蓋了大多數導致應用程式無法啟動的常見問題。

## <a name="obtain-data-from-an-app"></a>從應用程式取得資料

若應用程式能夠回應要求、請使用終端機內嵌中介軟體從應用程式取得要求、連線與額外資料。 如如需詳細資訊與範例程式碼，請參閱 <xref:test/troubleshoot#obtain-data-from-an-app>。

## <a name="slow-or-hanging-app"></a>回應緩慢或無回應的應用程式

當應用程式針對要求回應緩慢或無回應時，請取得[傾印檔案](/visualstudio/debugger/using-dump-files)並加以分析。 您可以使用下列任何工具來取得傾印檔案：

* [ProcDump](/sysinternals/downloads/procdump)
* [DebugDiag](https://www.microsoft.com/download/details.aspx?id=49924)
* WinDbg：[下載適用於 Windows 的偵錯工具](https://developer.microsoft.com/windows/hardware/download-windbg)、[使用 WinDbg 進行偵錯](/windows-hardware/drivers/debugger/debugging-using-windbg)

## <a name="remote-debugging"></a>遠端偵錯

請參閱 Visual Studio 文件中的[在 Visual Studio 2017 中針對遠端 IIS 電腦上的 ASP.NET Core 進行遠端偵錯](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) \(機器翻譯\)。

## <a name="application-insights"></a>Application Insights

[Application Insights](/azure/application-insights/) 提供來自 IIS 所裝載應用程式的遙測資料，包括錯誤記錄和報告功能。 Application Insights 只能針對在應用程式啟動之後，應用程式記錄功能變成可用時所發生的錯誤提出報告。 如需詳細資訊，請參閱 [ASP.NET Core 的 Application Insights](/azure/application-insights/app-insights-asp-net-core)。

## <a name="additional-advice"></a>額外建議

有時，在升級開發電腦上的 .NET Core SDK 或應用程式內的套件版本之後，正常運作的應用程式便立即發生失敗。 在某些情況下，執行主要升級時，不一致的套件可能會中斷應用程式。 大多數這些問題都可依照下列指示來進行修正：

1. 刪除 [bin] 和 [obj] 資料夾。
1. 清除位於 *%UserProfile%\\.nuget\\packages* 和 *%LocalAppData%\\Nuget\\v3-cache*的套件快取。
1. 還原並重建專案。
1. 先確認已將伺服器上先前的部署完全刪除，再重新部署應用程式。

> [!TIP]
> 有一個便利的方式可以清除套件快取，就是從命令提示字元執行 `dotnet nuget locals all --clear`。
>
> 您也可以使用 [nuget.exe](https://www.nuget.org/downloads) 工具並執行 `nuget locals all -clear` 命令，來清除套件快取。 *nuget.exe* 並未隨附在 Windows 桌面作業系統的安裝中，必須另外從 [NuGet 網站](https://www.nuget.org/downloads)取得。

## <a name="additional-resources"></a>其他資源

* <xref:test/troubleshoot>
* <xref:fundamentals/error-handling>
* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/aspnet-core-module>
* <xref:host-and-deploy/azure-apps/troubleshoot>
