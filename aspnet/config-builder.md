---
uid: config-builder
title: ASP.NET 的設定構建者
author: rick-anderson
description: 瞭解如何從外部來源的 web.config 值以外的來源取得設定資料。
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586756"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET 的設定構建者

By [Stephen Molloy](https://github.com/StephenMolloy)和[Rick Anderson](https://twitter.com/RickAndMSFT)

設定產生器提供現代化且敏捷的機制，讓 ASP.NET 應用程式從外部來源取得設定值。

設定產生器：

* .NET Framework 4.7.1 和更新版本中都有提供。
* 提供彈性的機制來讀取設定值。
* 解決應用程式移入容器和雲端焦點環境時的一些基本需求。
* 可以用來改善設定資料的保護，方法是從先前無法使用的來源（例如，Azure Key Vault 和環境變數）在 .NET 設定系統中進行繪製。

## <a name="keyvalue-configuration-builders"></a>索引鍵/值設定產生器

設定產生器可以處理的常見案例，是為遵循索引鍵/值模式的設定區段提供基本的索引鍵/值取代機制。 Configurationbuilders.ignoreloadfailure 的 .NET Framework 概念不限於特定的設定區段或模式。 不過，`Microsoft.Configuration.ConfigurationBuilders` （[github](https://github.com/aspnet/MicrosoftConfigurationBuilders)、 [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)）中的許多設定產生器都是在索引鍵/值模式內工作。

## <a name="keyvalue-configuration-builders-settings"></a>索引鍵/值設定構建者設定

下列設定適用于 `Microsoft.Configuration.ConfigurationBuilders`中的所有索引鍵/值設定產生器。

### <a name="mode"></a>Mode

設定產生器會使用索引鍵/值資訊的外部來源來填入設定系統的選取索引鍵/值元素。 具體而言，`<appSettings/>` 和 `<connectionStrings/>` 區段會收到設定產生器的特殊處理。 產生器適用于三種模式：

* `Strict`-預設模式。 在此模式中，設定產生器只會在知名的索引鍵/值中心設定區段上運作。 `Strict` 模式會列舉區段中的每個索引鍵。 如果在外部來源中找到相符的索引鍵：

   * 設定產生器會將結果設定區段中的值取代為來自外部來源的值。
* `Greedy`-此模式與 `Strict` 模式密切相關。 而不限於原始設定中已存在的金鑰：

  * 設定產生器會將外部來源中的所有機碼/值組新增至 [產生的設定] 區段。

* `Expand`-在原始 XML 上進行操作，再將它剖析成設定區段物件。 您可以將它視為字串中的標記擴充。 原始 XML 字串中符合模式 `${token}` 的任何部分都是用於標記擴充的候選項目。 如果在外部來源中找不到對應的值，則 token 不會變更。 此模式中的產生器不限於 `<appSettings/>` 和 `<connectionStrings/>` 區段。

下列*來自 web.config 的標記*會在 `Strict` 模式中啟用[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) ：

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

下列程式碼會讀取先前*web.config*檔案中顯示的 `<appSettings/>` 和 `<connectionStrings/>`：

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。
* 環境變數的值（如果已設定的話）。

例如，`ServiceID` 將包含：

* 「如果未設定環境變數 `ServiceID`，則為 web.config 中的 ServiceID 值」。
* 如果已設定，則為 `ServiceID` 環境變數的值。

下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 索引鍵/值：

![環境編輯器](config-builder/static/env.png)

注意：您可能需要結束並重新啟動 Visual Studio，才能看到環境變數的變更。

### <a name="prefix-handling"></a>前置詞處理

金鑰首碼可以簡化設定金鑰，因為：

* .NET Framework 設定是複雜且嵌套的。
* 外部索引鍵/值來源通常是基本的，而且本質上是一般的。 例如，環境變數不是嵌套的。

使用下列任何方法，透過環境變數將 `<appSettings/>` 和 `<connectionStrings/>` 插入設定中：

* 使用預設 `Strict` 模式中的 `EnvironmentConfigBuilder` 和設定檔中的適當索引鍵名稱。 上述程式碼和標記採用這種方法。 使用這種方法時，`<appSettings/>` 和 `<connectionStrings/>`中都**不**能有相同名稱的索引鍵。
* 在 `Greedy` 模式中使用兩個 `EnvironmentConfigBuilder`s，並使用不同的前置詞和 `stripPrefix`。 使用此方法，應用程式可以讀取 `<appSettings/>` 和 `<connectionStrings/>`，而不需要更新設定檔。 下一節[stripPrefix](#stripprefix)會示範如何執行此動作。
* 在具有不同前置詞的 `Greedy` 模式中使用兩個 `EnvironmentConfigBuilder`s。 使用此方法時，您不能有重複的索引鍵名稱，因為索引鍵名稱必須依前置詞而有所不同。  例如：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

使用上述標記時，可以使用相同的一般索引鍵/值來源來填入兩個不同區段的設定。

下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：

![環境編輯器](config-builder/static/prefix.png)

下列程式碼會讀取前述*web.config*檔案中包含的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。
* 環境變數的值（如果已設定的話）。

例如，使用先前的*web.config*檔案、先前環境編輯器影像中的索引鍵/值，以及先前的程式碼，會設定下列值：

|  索引鍵              | {2&gt;值&lt;2} |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | 從 env 變數 AppSetting_ServiceID|
|    AppSetting_default            | 來自 env 的 AppSetting_default 值 |
|       ConnStr_default         | 從 env ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`：布林值，預設為 `false`。 

上述 XML 標記會將應用程式設定與連接字串分開，*但 web.config 檔案*中的所有索引鍵都必須使用指定的前置詞。 例如，必須將前置詞 `AppSetting` 新增至 `ServiceID` 機碼（"AppSetting_ServiceID"）。 使用 `stripPrefix`時，不會*在 web.config 檔案*中使用前置詞。 設定產生器來源（例如環境中的）中必須有前置詞。我們預期大部分的開發人員都會使用 `stripPrefix`。

應用程式通常會去除前置詞。 下列 web.config*會去除前置*詞：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

在*前述的 web.config 檔案*中，`default` 鍵同時位於 `<appSettings/>` 和 `<connectionStrings/>`。

下圖顯示先前在環境編輯器中設定*的 web.config 檔案*中的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：

![環境編輯器](config-builder/static/prefix.png)

下列程式碼會讀取前述*web.config*檔案中包含的 `<appSettings/>` 和 `<connectionStrings/>` 索引鍵/值：

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

上述程式碼會將屬性值設定為：

* 如果未在環境變數中設定索引鍵，則*為 web.config 檔案*中的值。
* 環境變數的值（如果已設定的話）。

例如，使用先前的*web.config*檔案、先前環境編輯器影像中的索引鍵/值，以及先前的程式碼，會設定下列值：

|  索引鍵              | {2&gt;值&lt;2} |
| ----------------- | ------------ |
|     ServiceID           | 從 env 變數 AppSetting_ServiceID|
|    預設            | 來自 env 的 AppSetting_default 值 |
|    預設         | 從 env ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`：字串，預設為 `@"\$\{(\w+)\}"`

產生器的 `Expand` 行為會在原始 XML 中搜尋看起來像 `${token}`的權杖。 使用預設的正則運算式 `@"\$\{(\w+)\}"`來進行搜尋。 符合 `\w` 的字元組比 XML 更嚴格，而且有許多設定來源允許。 當令牌名稱中需要比 `@"\$\{(\w+)\}"` 更多的字元時，請使用 `tokenPattern`。

`tokenPattern`：字串：

* 可讓開發人員變更用於標記比對的 RegEx。
* 不會進行任何驗證，以確保它是格式正確、不危險的 RegEx。
* 它必須包含一個「capture 群組」。 整個 RegEx 必須符合整個 token。 第一個 capture 必須是要在設定來源中查詢的權杖名稱。

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Configurationbuilders.ignoreloadfailure 中的設定構建者

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：

* 是設定產生器的最簡單。
* 從環境讀取值。
* 沒有任何其他設定選項。
* `name` 屬性值是任意的。

**注意：** 在 Windows 容器環境中，在執行時間設定的變數只會插入進入點處理環境。 執行為服務或非進入點進程的應用程式不會挑選這些變數，除非以其他方式插入容器中的機制。 針對[IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)為基礎的容器， [ServiceMonitor](https://github.com/Microsoft/iis-docker/pull/41)的目前版本只會在*DefaultAppPool*中處理此項。 其他以 Windows 為基礎的容器變體可能需要針對非進入點進程開發自己的插入式機制。

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 絕對不要在原始程式碼中儲存密碼、敏感性連接字串或其他機密資料。 生產秘密不應用於開發或測試。

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

此設定產生器提供的功能類似于[ASP.NET Core 秘密管理員](/aspnet/core/security/app-secrets)。

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用於 .NET Framework 專案中，但必須指定秘密檔案。 或者，您可以在專案檔中定義 `UserSecretsId` 屬性，並在正確的位置中建立原始秘密檔案以供讀取。 為避免專案中的外部相依性，會將密碼檔案格式化為 XML。 XML 格式是一個執行詳細資料，且格式不應依賴。 如果您需要與 .NET Core 專案共用*秘密 json*檔案，請考慮使用[SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。 .NET Core 的 `SimpleJsonConfigBuilder` 格式也應該被視為要變更的執行詳細資料。

`UserSecretsConfigBuilder`的設定屬性：

* `userSecretsId`-這是用來識別 XML 秘密檔案的慣用方法。 其運作方式類似于 .NET Core，它會使用 `UserSecretsId` 專案屬性來儲存此識別碼。 此字串必須是唯一的，不需要是 GUID。 使用此屬性時，`UserSecretsConfigBuilder` 會尋找屬於此識別碼之秘密檔案的知名本機位置（`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`）。
* `userSecretsFile`-選擇性屬性，指定包含密碼的檔案。 在開始時，可以使用 `~` 字元來參考應用程式根目錄。 此屬性或 `userSecretsId` 屬性為必要項。 如果同時指定這兩者，`userSecretsFile` 會優先使用。
* `optional`：布林值，預設值 `true`-如果找不到秘密檔案，就會避免例外狀況。 
* `name` 屬性值是任意的。

秘密檔案具有下列格式：

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

需要 `vaultName` （保存庫的名稱或保存庫的 URI）。 其他屬性可控制要連接的保存庫，但只有在應用程式不是在與 `Microsoft.Azure.Services.AppAuthentication`搭配運作的環境中執行時才需要。 Azure 服務驗證程式庫會在可能的情況下，用來自動從執行環境中挑選連線資訊。 您可以藉由提供連接字串，覆寫自動挑選連接資訊。

* `vaultName`-如果未提供 `uri` 則為必要項。 在您的 Azure 訂用帳戶中，指定要從中讀取索引鍵/值組的保存庫名稱。
* `connectionString`- [azureservicetokenprovider 會](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)可使用的連接字串
* `uri`-使用指定的 `uri` 值連接到其他 Key Vault 提供者。 如果未指定，則 Azure （`vaultName`）是保存庫提供者。
* `version` Azure Key Vault 提供秘密的版本控制功能。 如果指定了 `version`，產生器只會抓取符合此版本的密碼。
* `preloadSecretNames`-根據預設，此產生器會在金鑰保存庫中 querys**所有**金鑰名稱（當它初始化時）。 若要避免讀取所有索引鍵值，請將此屬性設定為 `false`。 將此項設定為 `false` 一次讀取一個秘密。 如果保存庫允許「取得」存取權，而不是「列出」存取權，一次讀取一個秘密會很有用。 **注意：** 使用 `Greedy` 模式時，`preloadSecretNames` 必須 `true` （預設值）。

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

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)是基本的設定產生器，會使用目錄的檔案做為值的來源。 檔案的名稱是索引鍵，而內容則是值。 在協調的容器環境中執行時，此設定產生器可能會很有用。 Docker Swarm 和 Kubernetes 這類系統會以每個檔案的方式，為其協調的 windows 容器提供 `secrets`。

屬性詳細資料：

* `directoryPath` - 必要項。 指定要在其中尋找值的路徑。 適用於 Windows 的 Docker 秘密預設會儲存在*C:\ProgramData\Docker\secrets*目錄中。
* `ignorePrefix`-排除以這個前置詞開頭的檔案。 預設為 "ignore."。
* `keyDelimiter`-預設值為 `null`。 如果指定，則設定產生器會遍歷目錄的多個層級，並使用此分隔符號來建立索引鍵名稱。 如果此值為 `null`，則設定產生器只會查看目錄的最上層。
* `optional`-預設值為 `false`。 指定如果來原始目錄不存在，設定產生器是否應該造成錯誤。

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 絕對不要在原始程式碼中儲存密碼、敏感性連接字串或其他機密資料。 生產秘密不應用於開發或測試。

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core 專案經常會使用 JSON 檔案進行設定。 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder 允許在 .NET Framework 中使用 .NET Core JSON 檔案。 此設定產生器提供從一般索引鍵/值來源到 .NET Framework 設定的特定索引鍵/值區域的基本對應。 此設定產生器**不提供階層**式設定。 JSON 支援檔案類似于字典，而不是複雜的階層式物件。 可以使用多層級的階層式檔案。 此提供者 `flatten`的深度，方法是在每個層級附加屬性名稱，並使用 `:` 作為分隔符號。

屬性詳細資料：

* `jsonFile` - 必要項。 指定要從中讀取的 JSON 檔案。 在開始時，可以使用 `~` 字元來參考應用程式根目錄。
* `optional` 布林值，預設值是 `true`。 如果找不到 JSON 檔案，則防止擲回例外狀況。
* `jsonMode` - `[Flat|Sectional]`. `Flat` 是預設值。 當 `jsonMode` `Flat`時，JSON 檔案是單一的一般索引鍵/值來源。 `EnvironmentConfigBuilder` 和 `AzureKeyVaultConfigBuilder` 也是單一的一般索引鍵/值來源。 當 `SimpleJsonConfigBuilder` 設定為 `Sectional` 模式時：

  * 在概念上，JSON 檔案會分成多個字典，而不是在最上層。
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

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>執行自訂索引鍵/值設定產生器

如果設定產生器不符合您的需求，您可以撰寫一個自訂的程式。 `KeyValueConfigBuilder` 基類會處理替代模式和大部分前置詞的顧慮。 執行專案只需要：

* 繼承自基類，並透過 `GetValue` 和 `GetAllValues`來執行索引鍵/值組的基本來源：
* 將[configurationbuilders.ignoreloadfailure](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)新增至專案。

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder` 基類在索引鍵/值設定產生器中提供許多工作和一致的行為。

## <a name="additional-resources"></a>其他資源

* [設定構建者 GitHub 存放庫](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [使用 .NET Azure Key Vault 的服務對服務驗證](/azure/key-vault/service-to-service-authentication#connection-string-support)
