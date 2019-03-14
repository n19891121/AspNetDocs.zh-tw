---
title: ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 中繼套件
author: Rick-Anderson
description: Microsoft.AspNetCore.All 中繼套件不建議用於 ASP.NET Core 2.1 和更新版本。
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.custom: mvc
ms.date: 10/25/2018
uid: fundamentals/metapackage
ms.openlocfilehash: d95bafd412969bb8db38499bd2ff01af510d872c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064855"
---
# <a name="microsoftaspnetcoreall-metapackage-for-aspnet-core-20"></a>ASP.NET Core 2.0 的 Microsoft.AspNetCore.All 中繼套件

> [!NOTE]
> 建議以 ASP.NET Core 2.1 及更新版本為目標的應用程式使用 [Microsoft.AspNetCore.App 中繼套件](xref:fundamentals/metapackage-app)，而非此套件。 請參閱本文章中的[從 Microsoft.AspNetCore.All 移轉到 Microsoft.AspNetCore.App](#migrate)。

這項功能需要以 .NET Core 2.x 為目標的 ASP.NET Core 2.x。

ASP.NET Core 的 [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) 中繼套件包括：

* 所有由 ASP.NET Core 小組支援的套件。
* 所有由 Entity Framework Core 支援的套件。
* ASP.NET Core 與 Entity Framework Core 所使用的內部與第三人相依性。

`Microsoft.AspNetCore.All` 套件包含 ASP.NET Core 2.x 和 Entity Framework Core 2.x 的所有功能。 以 ASP.NET Core 2.0 為目標的預設專案範本會使用此套件。

`Microsoft.AspNetCore.All` 中繼套件的版本號碼代表 ASP.NET Core 版本和 Entity Framework Core 版本。

使用 `Microsoft.AspNetCore.All` 中繼套件的應用程式會自動利用 [.NET Core 執行階段存放區](/dotnet/core/deploying/runtime-store)。 此執行階段存放區包含執行 ASP.NET Core 2.x 應用程式所需的所有執行階段資產。 當您使用 `Microsoft.AspNetCore.All` 中繼套件時，**不會**使用應用程式部署所參考之 ASP.NET Core NuGet 套件的任何資產 &mdash; .NET Core 執行階段存放區包含這些資產。 執行階段存放區中的資產會先行編譯，以改善應用程式啟動時間。

您可以使用套件修剪流程來移除未使用的套件。 發行的應用程式輸出中會排除已修剪的套件。

下列 *.csproj* 檔案參考 ASP.NET Core 的 `Microsoft.AspNetCore.All` 中繼套件：

[!code-xml[](metapackage/samples/Metapackage.All.Example.csproj?highlight=8)]

::: moniker range=">= aspnetcore-2.1"

## <a name="implicit-versioning"></a>隱含的版本設定

在 ASP.NET Core 2.1 或更新版本中，您可指定不含版本的 `Microsoft.AspNetCore.All` 套件參考。 當未指定版本時，SDK (`Microsoft.NET.Sdk.Web`) 會指定隱含的版本。 建議依賴 SDK 指定的隱含版本，而不要明確設定套件參考的版本號碼。 如果您對此方法有疑問，請在 [Discussion for the Microsoft.AspNetCore.App implicit version](https://github.com/aspnet/Docs/issues/6430) (Microsoft.AspNetCore.App 隱含版本討論區) 留下 GitHub 意見。

可攜式應用程式的隱含版本會設定為 `major.minor.0`。 共用架構向前復原機制會在已安裝共用架構中的最新相容版本上，執行應用程式。 為了保證開發、測試和生產均使用相同版本，請務必在所有環境中安裝相同版本的共用架構。 針對獨立應用程式，隱含版本號碼會設定為已安裝 SDK 隨附共用架構的 `major.minor.patch`。

在 `Microsoft.AspNetCore.All` 套件參考上指定版本號碼**不**保證會選擇該版本的共用架構。 例如，假設指定版本 "2.1.1"，但安裝 "2.1.3"。 在此情況下，應用程式會使用 "2.1.3"。 您可以停用向前復原 (修補及/或次要)，但不建議這樣做。 如需 dotnet 主機向前復原及如何設定其行為的詳細資訊，請參閱 [dotnet 主機向前復原](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)。

在專案檔中，專案的 SDK 必須設定為 `Microsoft.NET.Sdk.Web`，才能使用 `Microsoft.AspNetCore.All` 的隱含版本。 當指定 `Microsoft.NET.Sdk` SDK 時 (專案檔頂端的 `<Project Sdk="Microsoft.NET.Sdk">`)，就會產生以下警告：

*警告 NU1604:專案相依性 Microsoft.AspNetCore.All 不包含下限 （內含）。請在相依性版本包含下限，以確保還原結果一致。*

這是.NET Core 2.1 SDK 的已知的問題，並將於 .NET Core 2.2 SDK 中修正。

::: moniker-end

<a name="migrate"></a>

## <a name="migrating-from-microsoftaspnetcoreall-to-microsoftaspnetcoreapp"></a>從 Microsoft.AspNetCore.All 移轉到 Microsoft.AspNetCore.App

下列套件隨附於 `Microsoft.AspNetCore.All`，而不是 `Microsoft.AspNetCore.App` 套件。

* `Microsoft.AspNetCore.ApplicationInsights.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServices.HostingStartup`
* `Microsoft.AspNetCore.AzureAppServicesIntegration`
* `Microsoft.AspNetCore.DataProtection.AzureKeyVault`
* `Microsoft.AspNetCore.DataProtection.AzureStorage`
* `Microsoft.AspNetCore.Server.Kestrel.Transport.Libuv`
* `Microsoft.AspNetCore.SignalR.Redis`
* `Microsoft.Data.Sqlite`
* `Microsoft.Data.Sqlite.Core`
* `Microsoft.EntityFrameworkCore.Sqlite`
* `Microsoft.EntityFrameworkCore.Sqlite.Core`
* `Microsoft.Extensions.Caching.Redis`
* `Microsoft.Extensions.Configuration.AzureKeyVault`
* `Microsoft.Extensions.Logging.AzureAppServices`
* `Microsoft.VisualStudio.Web.BrowserLink`

若要從 `Microsoft.AspNetCore.All` 移到 `Microsoft.AspNetCore.App`，如果您的應用程式使用來自上述套件的任何 API，或這些套件中隨附的套件，請將參考新增到專案中的這些套件。

若前述套件的任何相依性不是 `Microsoft.AspNetCore.App` 的相依性，即不包含在內。 例如: 

* `StackExchange.Redis` 為 `Microsoft.Extensions.Caching.Redis` 的相依性
* `Microsoft.ApplicationInsights` 為 `Microsoft.AspNetCore.ApplicationInsights.HostingStartup` 的相依性

## <a name="update-aspnet-core-21"></a>更新 ASP.NET Core 2.1

建議您移轉到 `Microsoft.AspNetCore.App` 中繼套件 2.1 與更新版本。 若要繼續使用 `Microsoft.AspNetCore.All` 中繼套件並確保已部署最新的更新程式版本：

* 在開發電腦和組建伺服器：安裝最新[.NET Core SDK](https://www.microsoft.com/net/download)。
* 在 部署伺服器：安裝最新[.NET Core 執行階段](https://www.microsoft.com/net/download)。
 您的應用程式會在應用程式重新開機時，向前復原到已安裝的最新版本。
