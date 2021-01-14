---
uid: config-builder
title: ASP.NET 的設定產生器 \(部分機器翻譯\)
author: rick-anderson
description: 瞭解如何從外部來源 web.config 值以外的來源取得設定資料。
ms.author: riande
ms.date: 7/17/2020
msc.type: content
ms.openlocfilehash: 04bc6bcc2d9d0be561f8b1f2d909d8c46d90ad81
ms.sourcegitcommit: 1dd64aab844e52ed27819c4ae62167081a067134
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98206110"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="7316e-103">ASP.NET 的設定產生器 \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="7316e-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="7316e-104">[Stephen Molloy](https://github.com/StephenMolloy)與[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7316e-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7316e-105">設定產生器提供新式且 agile 的機制，可讓 ASP.NET 應用程式從外部來源取得設定值。</span><span class="sxs-lookup"><span data-stu-id="7316e-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="7316e-106">設定產生器：</span><span class="sxs-lookup"><span data-stu-id="7316e-106">Configuration builders:</span></span>

* <span data-ttu-id="7316e-107">可在 .NET Framework 4.7.1 和更新版本中使用。</span><span class="sxs-lookup"><span data-stu-id="7316e-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="7316e-108">提供可用於讀取設定值的彈性機制。</span><span class="sxs-lookup"><span data-stu-id="7316e-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="7316e-109">解決應用程式移至容器和雲端導向環境時的一些基本需求。</span><span class="sxs-lookup"><span data-stu-id="7316e-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="7316e-110">可以用來改善設定資料的保護，方法是從先前無法使用的來源進行繪製 (例如，在 .NET 設定系統中) 的 Azure Key Vault 和環境變數。</span><span class="sxs-lookup"><span data-stu-id="7316e-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="7316e-111">索引鍵/值設定產生器</span><span class="sxs-lookup"><span data-stu-id="7316e-111">Key/value configuration builders</span></span>

<span data-ttu-id="7316e-112">設定產生器可以處理的常見案例是為遵循索引鍵/值模式的設定區段提供基本的索引鍵/值取代機制。</span><span class="sxs-lookup"><span data-stu-id="7316e-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="7316e-113">Configurationbuilders.ignoreloadfailure 的 .NET Framework 概念不限於特定的設定區段或模式。</span><span class="sxs-lookup"><span data-stu-id="7316e-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="7316e-114">不過， (github 中的許多設定產生器 `Microsoft.Configuration.ConfigurationBuilders` ， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) 在機碼/值模式中運作。 [](https://github.com/aspnet/MicrosoftConfigurationBuilders)</span><span class="sxs-lookup"><span data-stu-id="7316e-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="7316e-115">索引鍵/值設定產生器設定</span><span class="sxs-lookup"><span data-stu-id="7316e-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="7316e-116">下列設定適用于中的所有索引鍵/值設定產生器 `Microsoft.Configuration.ConfigurationBuilders` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="7316e-117">模式</span><span class="sxs-lookup"><span data-stu-id="7316e-117">Mode</span></span>

<span data-ttu-id="7316e-118">設定產生器會使用索引鍵/值資訊的外部來源來填入設定系統的選取索引鍵/值元素。</span><span class="sxs-lookup"><span data-stu-id="7316e-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="7316e-119">具體而言， `<appSettings/>` 和 `<connectionStrings/>` 區段會從設定產生器獲得特殊處理。</span><span class="sxs-lookup"><span data-stu-id="7316e-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="7316e-120">產生器可在三種模式中運作：</span><span class="sxs-lookup"><span data-stu-id="7316e-120">The builders work in three modes:</span></span>

* <span data-ttu-id="7316e-121">`Strict` -預設模式。</span><span class="sxs-lookup"><span data-stu-id="7316e-121">`Strict` - The default mode.</span></span> <span data-ttu-id="7316e-122">在此模式中，設定產生器只會操作知名的索引鍵/值中心設定區段。</span><span class="sxs-lookup"><span data-stu-id="7316e-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="7316e-123">`Strict` 模式會列舉區段中的每個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7316e-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="7316e-124">如果在外部來源中找到相符的索引鍵：</span><span class="sxs-lookup"><span data-stu-id="7316e-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="7316e-125">設定產生器會將產生的設定區段中的值取代為外部來源的值。</span><span class="sxs-lookup"><span data-stu-id="7316e-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="7316e-126">`Greedy` -此模式與模式密切相關 `Strict` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="7316e-127">而不是僅限於原始設定中已存在的金鑰：</span><span class="sxs-lookup"><span data-stu-id="7316e-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="7316e-128">設定產生器會將外部來源中的所有索引鍵/值組新增至產生的設定區段。</span><span class="sxs-lookup"><span data-stu-id="7316e-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="7316e-129">`Expand` -在將原始 XML 剖析為設定區段物件之前，先對其進行操作。</span><span class="sxs-lookup"><span data-stu-id="7316e-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="7316e-130">您可以將它視為字串中的標記擴充。</span><span class="sxs-lookup"><span data-stu-id="7316e-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="7316e-131">符合模式的原始 XML 字串的任何部分 `${token}` 都是標記展開的候選項目。</span><span class="sxs-lookup"><span data-stu-id="7316e-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="7316e-132">如果在外部來源中找不到對應的值，則不會變更權杖。</span><span class="sxs-lookup"><span data-stu-id="7316e-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="7316e-133">在此模式中的產生器不限於 `<appSettings/>` 和 `<connectionStrings/>` 區段。</span><span class="sxs-lookup"><span data-stu-id="7316e-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="7316e-134">下列 *web.config* 的標記會在模式中啟用 [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) `Strict` ：</span><span class="sxs-lookup"><span data-stu-id="7316e-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="7316e-135">下列程式碼會讀取 `<appSettings/>` 並 `<connectionStrings/>` 顯示在先前的 *web.config* 檔案中：</span><span class="sxs-lookup"><span data-stu-id="7316e-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="7316e-136">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="7316e-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="7316e-137">如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。</span><span class="sxs-lookup"><span data-stu-id="7316e-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="7316e-138">環境變數的值（如果有設定的話）。</span><span class="sxs-lookup"><span data-stu-id="7316e-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="7316e-139">例如， `ServiceID` 將包含：</span><span class="sxs-lookup"><span data-stu-id="7316e-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="7316e-140">如果未設定環境變數，則為「從 web.config ServiceID 值」 `ServiceID` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="7316e-141">環境變數的值 `ServiceID` （如果有設定的話）。</span><span class="sxs-lookup"><span data-stu-id="7316e-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="7316e-142">下圖顯示 `<appSettings/>` 環境編輯器中上述 *web.config* 檔案集的索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="7316e-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/env.png)

<span data-ttu-id="7316e-144">注意：您可能需要結束並重新啟動 Visual Studio，才能查看環境變數中的變更。</span><span class="sxs-lookup"><span data-stu-id="7316e-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="7316e-145">前置詞處理</span><span class="sxs-lookup"><span data-stu-id="7316e-145">Prefix handling</span></span>

<span data-ttu-id="7316e-146">金鑰首碼可以簡化設定金鑰的原因，如下：</span><span class="sxs-lookup"><span data-stu-id="7316e-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="7316e-147">.NET Framework 設定很複雜，而且是嵌套的。</span><span class="sxs-lookup"><span data-stu-id="7316e-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="7316e-148">外部索引鍵/值來源通常是基本的，而且本質上是平面的。</span><span class="sxs-lookup"><span data-stu-id="7316e-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="7316e-149">例如，環境變數不是嵌套的。</span><span class="sxs-lookup"><span data-stu-id="7316e-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="7316e-150">使用下列任何一種方法，透過 `<appSettings/>` 環境變數將和插入至設定 `<connectionStrings/>` ：</span><span class="sxs-lookup"><span data-stu-id="7316e-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="7316e-151">`EnvironmentConfigBuilder`在預設模式中使用， `Strict` 並在設定檔中使用適當的索引鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="7316e-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="7316e-152">上述程式碼和標記採用此方法。</span><span class="sxs-lookup"><span data-stu-id="7316e-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="7316e-153">使用這個方法時，和中 **不** 能有相同名稱的索引鍵 `<appSettings/>` `<connectionStrings/>` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="7316e-154">`EnvironmentConfigBuilder`在模式中使用兩個 `Greedy` 具有不同前置詞和的 `stripPrefix` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="7316e-155">使用這個方法時，應用程式可以讀取 `<appSettings/>` ， `<connectionStrings/>` 而不需要更新設定檔。</span><span class="sxs-lookup"><span data-stu-id="7316e-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="7316e-156">下一節  [stripPrefix](#stripprefix)將示範如何進行。</span><span class="sxs-lookup"><span data-stu-id="7316e-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="7316e-157">使用具有相異前置詞的兩個 `EnvironmentConfigBuilder` `Greedy` 模式。</span><span class="sxs-lookup"><span data-stu-id="7316e-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="7316e-158">使用這個方法時，您不能有重複的索引鍵名稱，因為索引鍵名稱必須以前置詞不同。</span><span class="sxs-lookup"><span data-stu-id="7316e-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="7316e-159">例如：</span><span class="sxs-lookup"><span data-stu-id="7316e-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="7316e-160">使用上述標記時，相同的一般索引鍵/值來源可以用來填入兩個不同區段的設定。</span><span class="sxs-lookup"><span data-stu-id="7316e-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="7316e-161">下圖顯示 `<appSettings/>` `<connectionStrings/>` 環境編輯器中上述 *web.config* 檔案集的和索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="7316e-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/prefix.png)

<span data-ttu-id="7316e-163">下列程式碼會讀取 `<appSettings/>` `<connectionStrings/>` 上述 *web.config* 檔案中包含的和索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="7316e-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="7316e-164">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="7316e-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="7316e-165">如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。</span><span class="sxs-lookup"><span data-stu-id="7316e-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="7316e-166">環境變數的值（如果有設定的話）。</span><span class="sxs-lookup"><span data-stu-id="7316e-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="7316e-167">例如，使用先前的 *web.config* 檔案、先前環境編輯器映射中的索引鍵/值和先前的程式碼，會設定下列值：</span><span class="sxs-lookup"><span data-stu-id="7316e-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="7316e-168">Key</span><span class="sxs-lookup"><span data-stu-id="7316e-168">Key</span></span>              | <span data-ttu-id="7316e-169">值</span><span class="sxs-lookup"><span data-stu-id="7316e-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="7316e-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="7316e-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="7316e-171">從 env 變數 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="7316e-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="7316e-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="7316e-172">AppSetting_default</span></span>            | <span data-ttu-id="7316e-173">來自 env 的 AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="7316e-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="7316e-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="7316e-174">ConnStr_default</span></span>         | <span data-ttu-id="7316e-175">來自 env 的 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="7316e-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="7316e-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="7316e-176">stripPrefix</span></span>

<span data-ttu-id="7316e-177">`stripPrefix`：布林值，預設為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="7316e-178">上述的 XML 標記會將應用程式設定與連接字串分開，但需要 *web.config* 檔中的所有機碼才能使用指定的前置詞。</span><span class="sxs-lookup"><span data-stu-id="7316e-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="7316e-179">例如，必須將前置詞 `AppSetting` 新增至機 `ServiceID` 碼 ( "AppSetting_ServiceID" ) 。</span><span class="sxs-lookup"><span data-stu-id="7316e-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="7316e-180">使用 `stripPrefix` 時，不會在 *web.config* 檔案中使用前置詞。</span><span class="sxs-lookup"><span data-stu-id="7316e-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="7316e-181">Configuration builder 來源中必須要有首碼 (例如，在環境中。 ) 我們預期大部分的開發人員會使用 `stripPrefix` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="7316e-182">應用程式通常會去除前置詞。</span><span class="sxs-lookup"><span data-stu-id="7316e-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="7316e-183">下列 *web.config* 會去除前置詞：</span><span class="sxs-lookup"><span data-stu-id="7316e-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="7316e-184">在上述 *web.config* 檔案中，索引 `default` 鍵同時位於 `<appSettings/>` 和 `<connectionStrings/>` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="7316e-185">下圖顯示 `<appSettings/>` `<connectionStrings/>` 環境編輯器中上述 *web.config* 檔案集的和索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="7316e-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![環境編輯器](config-builder/static/prefix.png)

<span data-ttu-id="7316e-187">下列程式碼會讀取 `<appSettings/>` `<connectionStrings/>` 上述 *web.config* 檔案中包含的和索引鍵/值：</span><span class="sxs-lookup"><span data-stu-id="7316e-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="7316e-188">上述程式碼會將屬性值設定為：</span><span class="sxs-lookup"><span data-stu-id="7316e-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="7316e-189">如果未在環境變數中設定索引鍵，則為 *web.config* 檔中的值。</span><span class="sxs-lookup"><span data-stu-id="7316e-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="7316e-190">環境變數的值（如果有設定的話）。</span><span class="sxs-lookup"><span data-stu-id="7316e-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="7316e-191">例如，使用先前的 *web.config* 檔案、先前環境編輯器映射中的索引鍵/值和先前的程式碼，會設定下列值：</span><span class="sxs-lookup"><span data-stu-id="7316e-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="7316e-192">Key</span><span class="sxs-lookup"><span data-stu-id="7316e-192">Key</span></span>              | <span data-ttu-id="7316e-193">值</span><span class="sxs-lookup"><span data-stu-id="7316e-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="7316e-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="7316e-194">ServiceID</span></span>           | <span data-ttu-id="7316e-195">從 env 變數 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="7316e-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="7316e-196">預設</span><span class="sxs-lookup"><span data-stu-id="7316e-196">default</span></span>            | <span data-ttu-id="7316e-197">來自 env 的 AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="7316e-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="7316e-198">預設</span><span class="sxs-lookup"><span data-stu-id="7316e-198">default</span></span>         | <span data-ttu-id="7316e-199">來自 env 的 ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="7316e-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="7316e-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="7316e-200">tokenPattern</span></span>

<span data-ttu-id="7316e-201">`tokenPattern`：字串，預設為 `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="7316e-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="7316e-202">產生器的 `Expand` 行為會搜尋原始 XML 中的權杖，看起來像這樣 `${token}` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="7316e-203">搜尋是使用預設的正則運算式來完成 `@"\$\{(\w+)\}"` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="7316e-204">相符的字元組 `\w` 比 XML 更嚴格，而且有許多設定來源允許。</span><span class="sxs-lookup"><span data-stu-id="7316e-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="7316e-205">`tokenPattern`當 `@"\$\{(\w+)\}"` 權杖名稱中所需的字元數超過時，請使用。</span><span class="sxs-lookup"><span data-stu-id="7316e-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="7316e-206">`tokenPattern`字串</span><span class="sxs-lookup"><span data-stu-id="7316e-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="7316e-207">可讓開發人員變更用於標記比對的 RegEx。</span><span class="sxs-lookup"><span data-stu-id="7316e-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="7316e-208">未進行任何驗證，以確定它是格式正確且不危險的 RegEx。</span><span class="sxs-lookup"><span data-stu-id="7316e-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="7316e-209">它必須包含一個 capture 群組。</span><span class="sxs-lookup"><span data-stu-id="7316e-209">It must contain a capture group.</span></span> <span data-ttu-id="7316e-210">整個 RegEx 都必須符合整個標記。</span><span class="sxs-lookup"><span data-stu-id="7316e-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="7316e-211">第一個捕獲必須是要在設定來源中查閱的權杖名稱。</span><span class="sxs-lookup"><span data-stu-id="7316e-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="7316e-212">Microsoft.Configuration.ConfigurationBuilders 中的設定產生器</span><span class="sxs-lookup"><span data-stu-id="7316e-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="7316e-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="7316e-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="7316e-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：</span><span class="sxs-lookup"><span data-stu-id="7316e-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="7316e-215">是最簡單的設定產生器。</span><span class="sxs-lookup"><span data-stu-id="7316e-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="7316e-216">從環境中讀取值。</span><span class="sxs-lookup"><span data-stu-id="7316e-216">Reads values from the environment.</span></span>
* <span data-ttu-id="7316e-217">沒有任何額外的設定選項。</span><span class="sxs-lookup"><span data-stu-id="7316e-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="7316e-218">`name`屬性值是任意的。</span><span class="sxs-lookup"><span data-stu-id="7316e-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="7316e-219">**注意：** 在 Windows 容器環境中，執行時間設定的變數只會插入進入點進程環境。</span><span class="sxs-lookup"><span data-stu-id="7316e-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="7316e-220">以服務或非 EntryPoint 進程的形式執行的應用程式，除非透過容器中的機制插入這些變數，否則不會收取這些變數。</span><span class="sxs-lookup"><span data-stu-id="7316e-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="7316e-221">若是以 [IIS](https://github.com/Microsoft/iis-docker/pull/41) / [ASP.NET](https://github.com/Microsoft/aspnet-docker)為基礎的容器， [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)的目前版本只會在 *DefaultAppPool* 中處理此項。</span><span class="sxs-lookup"><span data-stu-id="7316e-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="7316e-222">其他以 Windows 為基礎的容器變體可能需要針對非 EntryPoint 進程開發自己的插入機制。</span><span class="sxs-lookup"><span data-stu-id="7316e-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="7316e-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="7316e-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="7316e-224">絕對不要在原始程式碼中儲存密碼、機密的連接字串或其他機密資料。</span><span class="sxs-lookup"><span data-stu-id="7316e-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="7316e-225">生產秘密不應用於開發或測試。</span><span class="sxs-lookup"><span data-stu-id="7316e-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="7316e-226">此 configuration builder 提供類似于 [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets)的功能。</span><span class="sxs-lookup"><span data-stu-id="7316e-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="7316e-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用於 .NET Framework 專案中，但必須指定秘密檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="7316e-228">或者，您可以在專案檔中定義 `UserSecretsId` 屬性，並在正確的位置中建立原始秘密檔案以進行讀取。</span><span class="sxs-lookup"><span data-stu-id="7316e-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="7316e-229">為了將外部相依性從專案中排除，秘密檔案的格式為 XML。</span><span class="sxs-lookup"><span data-stu-id="7316e-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="7316e-230">XML 格式是執行的詳細資料，不應該依賴此格式。</span><span class="sxs-lookup"><span data-stu-id="7316e-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="7316e-231">如果您需要與 .NET Core 專案共用檔案 *secrets.js* ，請考慮使用 [SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。</span><span class="sxs-lookup"><span data-stu-id="7316e-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="7316e-232">`SimpleJsonConfigBuilder`.Net Core 的格式也應該視為可能變更的實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7316e-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="7316e-233">的設定屬性 `UserSecretsConfigBuilder` ：</span><span class="sxs-lookup"><span data-stu-id="7316e-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="7316e-234">`userSecretsId` -這是識別 XML 秘密檔案的慣用方法。</span><span class="sxs-lookup"><span data-stu-id="7316e-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="7316e-235">其運作方式類似于 .NET Core，它會使用 `UserSecretsId` 專案屬性來儲存此識別碼。</span><span class="sxs-lookup"><span data-stu-id="7316e-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="7316e-236">字串必須是唯一的，不需要是 GUID。</span><span class="sxs-lookup"><span data-stu-id="7316e-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="7316e-237">使用這個屬性時，會 `UserSecretsConfigBuilder` `%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml` 針對屬於此識別碼的秘密檔案，查看已知的本機位置 () 。</span><span class="sxs-lookup"><span data-stu-id="7316e-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="7316e-238">`userSecretsFile` -選擇性的屬性，指定包含密碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="7316e-239">`~`字元可以在開頭用來參考應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="7316e-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="7316e-240">這是必要屬性或 `userSecretsId` 屬性。</span><span class="sxs-lookup"><span data-stu-id="7316e-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="7316e-241">如果同時指定兩者，則 `userSecretsFile` 會優先使用。</span><span class="sxs-lookup"><span data-stu-id="7316e-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="7316e-242">`optional`：布林值，預設值 `true` -如果找不到秘密檔案，則防止例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7316e-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="7316e-243">`name`屬性值是任意的。</span><span class="sxs-lookup"><span data-stu-id="7316e-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="7316e-244">秘密檔案的格式如下：</span><span class="sxs-lookup"><span data-stu-id="7316e-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="7316e-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="7316e-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="7316e-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)會讀取儲存在[Azure Key Vault](/azure/key-vault/key-vault-whatis)中的值。</span><span class="sxs-lookup"><span data-stu-id="7316e-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="7316e-247">`vaultName` 需要 (保存庫的名稱或保存庫) 的 URI。</span><span class="sxs-lookup"><span data-stu-id="7316e-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="7316e-248">其他屬性則可控制要連接的保存庫，但只有在應用程式未在搭配使用的環境中執行時才需要 `Microsoft.Azure.Services.AppAuthentication` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="7316e-249">Azure 服務驗證程式庫可讓您在可能的情況下，自動從執行環境中挑選連接資訊。</span><span class="sxs-lookup"><span data-stu-id="7316e-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="7316e-250">您可以藉由提供連接字串，覆寫自動挑選連接資訊。</span><span class="sxs-lookup"><span data-stu-id="7316e-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="7316e-251">`vaultName` -如果未提供，則為必要項 `uri` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="7316e-252">在您的 Azure 訂用帳戶中，指定要從中讀取索引鍵/值組的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="7316e-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="7316e-253">`uri` -連接到具有指定值的其他 Key Vault 提供者 `uri` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-253">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="7316e-254">如果未指定，Azure (`vaultName`) 是保存庫提供者。</span><span class="sxs-lookup"><span data-stu-id="7316e-254">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="7316e-255">`version` -Azure Key Vault 提供秘密的版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="7316e-255">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="7316e-256">如果 `version` 指定了，產生器只會抓取符合此版本的秘密。</span><span class="sxs-lookup"><span data-stu-id="7316e-256">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="7316e-257">`preloadSecretNames` -根據預設，此產生器會在初始化時 querys 金鑰保存庫中的 **所有** 金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="7316e-257">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="7316e-258">若要防止讀取所有索引鍵值，請將這個屬性設定為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-258">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="7316e-259">將此設定為 `false` 一次讀取一個秘密。</span><span class="sxs-lookup"><span data-stu-id="7316e-259">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="7316e-260">如果保存庫允許「取得」存取，而不是「列出」存取權，則一次讀取一個秘密會很有用。</span><span class="sxs-lookup"><span data-stu-id="7316e-260">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="7316e-261">**注意：** 使用 `Greedy` 模式時， `preloadSecretNames` 必須 `true` (預設值。 ) </span><span class="sxs-lookup"><span data-stu-id="7316e-261">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="7316e-262">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="7316e-262">KeyPerFileConfigBuilder</span></span>

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

<span data-ttu-id="7316e-263">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) 是基本的設定產生器，會使用目錄的檔案做為值的來源。</span><span class="sxs-lookup"><span data-stu-id="7316e-263">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="7316e-264">檔案的名稱是索引鍵，而內容則是值。</span><span class="sxs-lookup"><span data-stu-id="7316e-264">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="7316e-265">在協調的容器環境中執行時，此設定產生器會很有用。</span><span class="sxs-lookup"><span data-stu-id="7316e-265">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="7316e-266">Docker Swarm 和 Kubernetes 這類系統會 `secrets` 以每個檔案的方式，為其協調的 windows 容器提供此金鑰。</span><span class="sxs-lookup"><span data-stu-id="7316e-266">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="7316e-267">屬性詳細資料：</span><span class="sxs-lookup"><span data-stu-id="7316e-267">Attribute details:</span></span>

* <span data-ttu-id="7316e-268">`directoryPath` - 必要項。</span><span class="sxs-lookup"><span data-stu-id="7316e-268">`directoryPath` - Required.</span></span> <span data-ttu-id="7316e-269">指定要在其中尋找值的路徑。</span><span class="sxs-lookup"><span data-stu-id="7316e-269">Specifies a path to look in for values.</span></span> <span data-ttu-id="7316e-270">適用於 Windows 的 Docker 的秘密預設會儲存在 *C:\ProgramData\Docker\secrets* 目錄中。</span><span class="sxs-lookup"><span data-stu-id="7316e-270">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="7316e-271">`ignorePrefix` -會排除開頭為此前置詞的檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-271">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="7316e-272">預設為 "ignore."。</span><span class="sxs-lookup"><span data-stu-id="7316e-272">Defaults to "ignore.".</span></span>
* <span data-ttu-id="7316e-273">`keyDelimiter` -預設值為 `null` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-273">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="7316e-274">如果有指定，設定產生器會流經目錄的多個層級，並使用此分隔符號來建立索引鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="7316e-274">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="7316e-275">如果此值為 `null` ，則設定產生器只會查看目錄的最上層。</span><span class="sxs-lookup"><span data-stu-id="7316e-275">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="7316e-276">`optional` -預設值為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-276">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="7316e-277">指定如果來原始目錄不存在，設定產生器是否應造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="7316e-277">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="7316e-278">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="7316e-278">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="7316e-279">絕對不要在原始程式碼中儲存密碼、機密的連接字串或其他機密資料。</span><span class="sxs-lookup"><span data-stu-id="7316e-279">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="7316e-280">生產秘密不應用於開發或測試。</span><span class="sxs-lookup"><span data-stu-id="7316e-280">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="7316e-281">.NET Core 專案經常會使用 JSON 檔案進行設定。</span><span class="sxs-lookup"><span data-stu-id="7316e-281">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="7316e-282">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder 可讓您在 .NET Framework 中使用 .NET Core JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-282">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="7316e-283">此 configuration builder 提供從一般索引鍵/值來源到 .NET Framework 設定的特定索引鍵/值區域的基本對應。</span><span class="sxs-lookup"><span data-stu-id="7316e-283">This configuration builder provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="7316e-284">此 configuration builder 不 **提供階層** 式設定。</span><span class="sxs-lookup"><span data-stu-id="7316e-284">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="7316e-285">JSON 備份檔案類似于字典，而不是複雜的階層式物件。</span><span class="sxs-lookup"><span data-stu-id="7316e-285">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="7316e-286">您可以使用多層級的階層式檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-286">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="7316e-287">此提供者會 `flatten` 在每個層級上附加屬性名稱， `:` 並使用做為分隔符號，以提供深度。</span><span class="sxs-lookup"><span data-stu-id="7316e-287">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="7316e-288">屬性詳細資料：</span><span class="sxs-lookup"><span data-stu-id="7316e-288">Attribute details:</span></span>

* <span data-ttu-id="7316e-289">`jsonFile` - 必要項。</span><span class="sxs-lookup"><span data-stu-id="7316e-289">`jsonFile` - Required.</span></span> <span data-ttu-id="7316e-290">指定要讀取的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="7316e-290">Specifies the JSON file to read from.</span></span> <span data-ttu-id="7316e-291">`~`字元可以在開頭用來參考應用程式根目錄。</span><span class="sxs-lookup"><span data-stu-id="7316e-291">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="7316e-292">`optional` -布林值，預設值為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="7316e-292">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="7316e-293">如果找不到 JSON 檔案，則避免擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7316e-293">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="7316e-294">`jsonMode` - `[Flat|Sectional]`.</span><span class="sxs-lookup"><span data-stu-id="7316e-294">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="7316e-295">`Flat` 是預設值。</span><span class="sxs-lookup"><span data-stu-id="7316e-295">`Flat` is the default.</span></span> <span data-ttu-id="7316e-296">當 `jsonMode` 為時 `Flat` ，JSON 檔案是單一的一般索引鍵/值來源。</span><span class="sxs-lookup"><span data-stu-id="7316e-296">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="7316e-297">`EnvironmentConfigBuilder`和 `AzureKeyVaultConfigBuilder` 也是單一的平面索引鍵/值來源。</span><span class="sxs-lookup"><span data-stu-id="7316e-297">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="7316e-298">`SimpleJsonConfigBuilder`在模式中設定時 `Sectional` ：</span><span class="sxs-lookup"><span data-stu-id="7316e-298">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="7316e-299">JSON 檔案在概念上只會在最上層分成多個字典。</span><span class="sxs-lookup"><span data-stu-id="7316e-299">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="7316e-300">每個字典只會套用至符合附加至其最上層屬性名稱的設定區段。</span><span class="sxs-lookup"><span data-stu-id="7316e-300">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="7316e-301">例如：</span><span class="sxs-lookup"><span data-stu-id="7316e-301">For example:</span></span>

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

## <a name="configuration-builders-order"></a><span data-ttu-id="7316e-302">設定產生器順序</span><span class="sxs-lookup"><span data-stu-id="7316e-302">Configuration builders order</span></span>

<span data-ttu-id="7316e-303">請參閱[aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub 存放庫中的[configurationbuilders.ignoreloadfailure 執行順序](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution)。</span><span class="sxs-lookup"><span data-stu-id="7316e-303">See [ConfigurationBuilders Order of Execution](https://github.com/aspnet/MicrosoftConfigurationBuilders/blob/master/README.md#configurationbuilders-order-of-execution) in the [aspnet/MicrosoftConfigurationBuilders](https://github.com/aspnet/MicrosoftConfigurationBuilders) GitHub repository.</span></span>

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="7316e-304">執行自訂索引鍵/值設定產生器</span><span class="sxs-lookup"><span data-stu-id="7316e-304">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="7316e-305">如果設定產生器不符合您的需求，您可以撰寫自訂程式。</span><span class="sxs-lookup"><span data-stu-id="7316e-305">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="7316e-306">`KeyValueConfigBuilder`基底類別會處理替代模式和大部分前置詞的考慮。</span><span class="sxs-lookup"><span data-stu-id="7316e-306">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="7316e-307">執行專案只需要：</span><span class="sxs-lookup"><span data-stu-id="7316e-307">An implementing project need only:</span></span>

* <span data-ttu-id="7316e-308">繼承自基類，並透過和來執行索引鍵/值組的基本來源 `GetValue` `GetAllValues` ：</span><span class="sxs-lookup"><span data-stu-id="7316e-308">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="7316e-309">將 [Microsoft.Configuration.ConfigurationBuilders](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) 加入至專案。</span><span class="sxs-lookup"><span data-stu-id="7316e-309">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="7316e-310">`KeyValueConfigBuilder`基類可在索引鍵/值設定產生器之間提供大部分的工作和一致行為。</span><span class="sxs-lookup"><span data-stu-id="7316e-310">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7316e-311">其他資源</span><span class="sxs-lookup"><span data-stu-id="7316e-311">Additional resources</span></span>

* [<span data-ttu-id="7316e-312">Configuration builder GitHub 存放庫</span><span class="sxs-lookup"><span data-stu-id="7316e-312">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="7316e-313">使用 .NET 對 Azure Key Vault 進行服務對服務驗證</span><span class="sxs-lookup"><span data-stu-id="7316e-313">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
