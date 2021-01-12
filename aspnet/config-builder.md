---
uid: config-builder
title: ASP.NET 的設定產生器 \(部分機器翻譯\)
author: rick-anderson
description: 瞭解如何從外部來源 web.config 值以外的來源取得設定資料。
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: c5a3d86487cd75d20aebe822e81f9b42d363faa7
ms.sourcegitcommit: d4e2a07eeb2cdf19f0bfbfab4a469970bc7e1c99
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2021
ms.locfileid: "98105230"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET 的設定產生器 \(部分機器翻譯\)

[Stephen Molloy](https://github.com/StephenMolloy)與[Rick Anderson](https://twitter.com/RickAndMSFT)

設定產生器提供新式且 agile 的機制，可讓 ASP.NET 應用程式從外部來源取得設定值。

設定產生器：

* 可在 .NET Framework 4.7.1 和更新版本中使用。
* 提供可用於讀取設定值的彈性機制。
* 解決應用程式移至容器和雲端導向環境時的一些基本需求。
* 可以用來改善設定資料的保護，方法是從先前無法使用的來源進行繪製 (例如，在 .NET 設定系統中) 的 Azure Key Vault 和環境變數。

## <a name="keyvalue-configuration-builders"></a>索引鍵/值設定產生器

設定產生器可以處理的常見案例是為遵循索引鍵/值模式的設定區段提供基本的索引鍵/值取代機制。 Configurationbuilders.ignoreloadfailure 的 .NET Framework 概念不限於特定的設定區段或模式。 不過， (github 中的許多設定產生器 `Microsoft.Configuration.ConfigurationBuilders` ， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) 在機碼/值模式中運作。 [](https://github.com/aspnet/MicrosoftConfigurationBuilders)

## <a name="keyvalue-configuration-builders-settings"></a>索引鍵/值設定產生器設定

下列設定適用于中的所有索引鍵/值設定產生器 `Microsoft.Configuration.ConfigurationBuilders` 。

### <a name="mode"></a>模式

設定產生器會使用索引鍵/值資訊的外部來源來填入設定系統的選取索引鍵/值元素。 具體而言， `<appSettings/>` 和 `<connectionStrings/>` 區段會從設定產生器獲得特殊處理。 產生器可在三種模式中運作：

* `Strict` -預設模式。 在此模式中，設定產生器只會操作知名的索引鍵/值中心設定區段。 `Strict` 模式會列舉區段中的每個索引鍵。 如果在外部來源中找到相符的索引鍵：

   * 設定產生器會將產生的設定區段中的值取代為外部來源的值。
* `Greedy` -此模式與模式密切相關 `Strict` 。 而不是僅限於原始設定中已存在的金鑰：

  * 設定產生器會將外部來源中的所有索引鍵/值組新增至產生的設定區段。

* `Expand` -在將原始 XML 剖析為設定區段物件之前，先對其進行操作。 您可以將它視為字串中的標記擴充。 符合模式的原始 XML 字串的任何部分 `${token}` 都是標記展開的候選項目。 如果在外部來源中找不到對應的值，則不會變更權杖。 在此模式中的產生器不限於 `<appSettings/>` 和 `<connectionStrings/>` 區段。

下列 *web.config* 的標記會在模式中啟用 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) `Strict` ：

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

下列程式碼會讀取 `<appSettings/>` 並 `<connectionStrings/>` 顯示在先前的 *web.config* 檔案中：

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。
* 環境變數的值（如果有設定的話）。

例如， `ServiceID` 將包含：

* 如果未設定環境變數，則為「從 web.config ServiceID 值」 `ServiceID` 。
* 環境變數的值 `ServiceID` （如果有設定的話）。

下圖顯示 `<appSettings/>` 環境編輯器中上述 *web.config* 檔案集的索引鍵/值：

![環境編輯器](config-builder/static/env.png)

注意：您可能需要結束並重新啟動 Visual Studio，才能查看環境變數中的變更。

### <a name="prefix-handling"></a>前置詞處理

金鑰首碼可以簡化設定金鑰的原因，如下：

* .NET Framework 設定很複雜，而且是嵌套的。
* 外部索引鍵/值來源通常是基本的，而且本質上是平面的。 例如，環境變數不是嵌套的。

使用下列任何一種方法，透過 `<appSettings/>` 環境變數將和插入至設定 `<connectionStrings/>` ：

* `EnvironmentConfigBuilder`在預設模式中使用， `Strict` 並在設定檔中使用適當的索引鍵名稱。 上述程式碼和標記採用此方法。 使用這個方法時，和中 **不** 能有相同名稱的索引鍵 `<appSettings/>` `<connectionStrings/>` 。
* `EnvironmentConfigBuilder`在模式中使用兩個 `Greedy` 具有不同前置詞和的 `stripPrefix` 。 使用這個方法時，應用程式可以讀取 `<appSettings/>` ， `<connectionStrings/>` 而不需要更新設定檔。 下一節  [stripPrefix](#stripprefix)將示範如何進行。
* 使用具有相異前置詞的兩個 `EnvironmentConfigBuilder` `Greedy` 模式。 使用這個方法時，您不能有重複的索引鍵名稱，因為索引鍵名稱必須以前置詞不同。  例如：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

使用上述標記時，相同的一般索引鍵/值來源可以用來填入兩個不同區段的設定。

下圖顯示 `<appSettings/>` `<connectionStrings/>` 環境編輯器中上述 *web.config* 檔案集的和索引鍵/值：

![環境編輯器](config-builder/static/prefix.png)

下列程式碼會讀取 `<appSettings/>` `<connectionStrings/>` 上述 *web.config* 檔案中包含的和索引鍵/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。
* 環境變數的值（如果有設定的話）。

例如，使用先前的 *web.config* 檔案、先前環境編輯器映射中的索引鍵/值和先前的程式碼，會設定下列值：

|  Key              | 值 |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | 從 env 變數 AppSetting_ServiceID|
|    AppSetting_default            | 來自 env 的 AppSetting_default 值 |
|       ConnStr_default         | 來自 env 的 ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`：布林值，預設為 `false` 。 

上述的 XML 標記會將應用程式設定與連接字串分開，但需要 *web.config* 檔中的所有機碼才能使用指定的前置詞。 例如，必須將前置詞 `AppSetting` 新增至機 `ServiceID` 碼 ( "AppSetting_ServiceID" ) 。 使用 `stripPrefix` 時，不會在 *web.config* 檔案中使用前置詞。 Configuration builder 來源中必須要有首碼 (例如，在環境中。 ) 我們預期大部分的開發人員會使用 `stripPrefix` 。

應用程式通常會去除前置詞。 下列 *web.config* 會去除前置詞：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

在上述 *web.config* 檔案中，索引 `default` 鍵同時位於 `<appSettings/>` 和 `<connectionStrings/>` 。

下圖顯示 `<appSettings/>` `<connectionStrings/>` 環境編輯器中上述 *web.config* 檔案集的和索引鍵/值：

![環境編輯器](config-builder/static/prefix.png)

下列程式碼會讀取 `<appSettings/>` `<connectionStrings/>` 上述 *web.config* 檔案中包含的和索引鍵/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。
* 環境變數的值（如果有設定的話）。

例如，使用先前的 *web.config* 檔案、先前環境編輯器映射中的索引鍵/值和先前的程式碼，會設定下列值：

|  Key              | 值 |
| ----------------- | ------------ |
|     ServiceID           | 從 env 變數 AppSetting_ServiceID|
|    預設            | 來自 env 的 AppSetting_default 值 |
|    預設         | 來自 env 的 ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`：字串，預設為 `@"\$\{(\w+)\}"`

產生器的 `Expand` 行為會搜尋原始 XML 中的權杖，看起來像這樣 `${token}` 。 搜尋是使用預設的正則運算式來完成 `@"\$\{(\w+)\}"` 。 相符的字元組 `\w` 比 XML 更嚴格，而且有許多設定來源允許。 `tokenPattern`當 `@"\$\{(\w+)\}"` 權杖名稱中所需的字元數超過時，請使用。

`tokenPattern`字串

* 可讓開發人員變更用於標記比對的 RegEx。
* 未進行任何驗證，以確定它是格式正確且不危險的 RegEx。
* 它必須包含一個 capture 群組。 整個 RegEx 都必須符合整個標記。 第一個捕獲必須是要在設定來源中查閱的權杖名稱。

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft.Configuration.ConfigurationBuilders 中的設定產生器

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：

* 是最簡單的設定產生器。
* 從環境中讀取值。
* 沒有任何額外的設定選項。
* `name`屬性值是任意的。

**注意：** 在 Windows 容器環境中，執行時間設定的變數只會插入進入點進程環境。 以服務或非 EntryPoint 進程的形式執行的應用程式，除非透過容器中的機制插入這些變數，否則不會收取這些變數。 若是以 [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)為基礎的容器， [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)的目前版本只會在 *DefaultAppPool* 中處理此項。 其他以 Windows 為基礎的容器變體可能需要針對非 EntryPoint 進程開發自己的插入機制。

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 絕對不要在原始程式碼中儲存密碼、機密的連接字串或其他機密資料。 生產秘密不應用於開發或測試。

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

此 configuration builder 提供類似于 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)的功能。

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用於 .NET Framework 專案中，但必須指定秘密檔案。 或者，您可以在專案檔中定義 `UserSecretsId` 屬性，並在正確的位置中建立原始秘密檔案以進行讀取。 為了將外部相依性從專案中排除，秘密檔案的格式為 XML。 XML 格式是執行的詳細資料，不應該依賴此格式。 如果您需要與 .NET Core 專案共用檔案 *secrets.js* ，請考慮使用 [SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。 `SimpleJsonConfigBuilder`.Net Core 的格式也應該視為可能變更的實作詳細資料。

的設定屬性 `UserSecretsConfigBuilder` ：

* `userSecretsId` -這是識別 XML 秘密檔案的慣用方法。 其運作方式類似于 .NET Core，它會使用 `UserSecretsId` 專案屬性來儲存此識別碼。 字串必須是唯一的，不需要是 GUID。 使用這個屬性時，會 `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` 針對屬於此識別碼的秘密檔案，查看已知的本機位置 () 。
* `userSecretsFile` -選擇性的屬性，指定包含密碼的檔案。 `~`字元可以在開頭用來參考應用程式根目錄。 這是必要屬性或 `userSecretsId` 屬性。 如果同時指定兩者，則 `userSecretsFile` 會優先使用。
* `optional`：布林值，預設值 `true` -如果找不到秘密檔案，則防止例外狀況。 
* `name`屬性值是任意的。

秘密檔案的格式如下：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)會讀取儲存在[Azure Key Vault](/azure/key-vault/key-vault-whatis)中的值。

`vaultName` 需要 (保存庫的名稱或保存庫) 的 URI。 其他屬性則可控制要連接的保存庫，但只有在應用程式未在搭配使用的環境中執行時才需要 `Microsoft.Azure.Services.AppAuthentication` 。 Azure 服務驗證程式庫可讓您在可能的情況下，自動從執行環境中挑選連接資訊。 您可以藉由提供連接字串，覆寫自動挑選連接資訊。

* `vaultName` -如果未提供，則為必要項 `uri` 。 在您的 Azure 訂用帳戶中，指定要從中讀取索引鍵/值組的保存庫名稱。
* `connectionString`- [Azureservicetokenprovider 會](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)可用的連接字串
* `uri` -連接到具有指定值的其他 Key Vault 提供者 `uri` 。 如果未指定，Azure (`vaultName`) 是保存庫提供者。
* `version` -Azure Key Vault 提供秘密的版本控制功能。 如果 `version` 指定了，產生器只會抓取符合此版本的秘密。
* `preloadSecretNames` -根據預設，此產生器會在初始化時 querys 金鑰保存庫中的 **所有** 金鑰名稱。 若要防止讀取所有索引鍵值，請將這個屬性設定為 `false` 。 將此設定為 `false` 一次讀取一個秘密。 如果保存庫允許「取得」存取，而不是「列出」存取權，則一次讀取一個秘密會很有用。 **注意：** 使用 `Greedy` 模式時， `preloadSecretNames` 必須 `true` (預設值。 ) 

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 是基本的設定產生器，會使用目錄的檔案做為值的來源。 檔案的名稱是索引鍵，而內容則是值。 在協調的容器環境中執行時，此設定產生器會很有用。 Docker Swarm 和 Kubernetes 這類系統會 `secrets` 以每個檔案的方式，為其協調的 windows 容器提供此金鑰。

屬性詳細資料：

* `directoryPath` - 必要項。 指定要在其中尋找值的路徑。 適用於 Windows 的 Docker 的秘密預設會儲存在 *C:\ProgramData\Docker\secrets* 目錄中。
* `ignorePrefix` -會排除開頭為此前置詞的檔案。 預設為 "ignore."。
* `keyDelimiter` -預設值為 `null` 。 如果有指定，設定產生器會流經目錄的多個層級，並使用此分隔符號來建立索引鍵名稱。 如果此值為 `null` ，則設定產生器只會查看目錄的最上層。
* `optional` -預設值為 `false` 。 指定如果來原始目錄不存在，設定產生器是否應造成錯誤。

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 絕對不要在原始程式碼中儲存密碼、機密的連接字串或其他機密資料。 生產秘密不應用於開發或測試。

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core 專案經常會使用 JSON 檔案進行設定。 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder 可讓您在 .NET Framework 中使用 .NET Core JSON 檔案。 此 configuration builder 提供從一般索引鍵/值來源到 .NET Framework 設定的特定索引鍵/值區域的基本對應。 此 configuration builder 不 **提供階層** 式設定。 JSON 備份檔案類似于字典，而不是複雜的階層式物件。 您可以使用多層級的階層式檔案。 此提供者會 `flatten` 在每個層級上附加屬性名稱， `:` 並使用做為分隔符號，以提供深度。

屬性詳細資料：

* `jsonFile` - 必要項。 指定要讀取的 JSON 檔案。 `~`字元可以在開頭用來參考應用程式根目錄。
* `optional` -布林值，預設值為 `true` 。 如果找不到 JSON 檔案，則避免擲回例外狀況。
* `jsonMode` - `[Flat|Sectional]`. `Flat` 是預設值。 當 `jsonMode` 為時 `Flat` ，JSON 檔案是單一的一般索引鍵/值來源。 `EnvironmentConfigBuilder`和 `AzureKeyVaultConfigBuilder` 也是單一的平面索引鍵/值來源。 `SimpleJsonConfigBuilder`在模式中設定時 `Sectional` ：

  * JSON 檔案在概念上只會在最上層分成多個字典。
  * 每個字典只會套用至符合附加至其最上層屬性名稱的設定區段。 例如：

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="configuration-builders-order"></a>設定產生器順序

請參閱[aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub 存放庫中的[configurationbuilders.ignoreloadfailure 執行順序](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution)。

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>執行自訂索引鍵/值設定產生器

如果設定產生器不符合您的需求，您可以撰寫自訂程式。 `KeyValueConfigBuilder`基底類別會處理替代模式和大部分前置詞的考慮。 執行專案只需要：

* 繼承自基類，並透過和來執行索引鍵/值組的基本來源 `GetValue` `GetAllValues` ：
* 將 [Microsoft.Configuration.ConfigurationBuilders](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 加入至專案。

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`基類可在索引鍵/值設定產生器之間提供大部分的工作和一致行為。

## <a name="additional-resources"></a>其他資源

* [Configuration builder GitHub 存放庫](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [使用 .NET 對 Azure Key Vault 進行服務對服務驗證](/azure/key-vault/service-to-service-authentication#connection-string-support)
