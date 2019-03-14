---
title: ASP.NET Core MVC 的相容性版本
author: rick-anderson
description: 探索 Startup 類別如何在 ASP.NET Core 中設定服務和應用程式的要求管線。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2019
uid: mvc/compatibility-version
ms.openlocfilehash: b360da105799a1dccb1902e167e50e78864b76a9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048015"
---
# <a name="compatibility-version-for-aspnet-core-mvc"></a>ASP.NET Core MVC 的相容性版本

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

<xref:Microsoft.Extensions.DependencyInjection.MvcCoreMvcBuilderExtensions.SetCompatibilityVersion*> 方法可讓應用程式加入或退出 ASP.NET Core MVC 2.1 或更新版本所引入的可能重大行為變更。 這些可能的重大行為變更通常在於 MVC 子系統的運作方式，以及執行階段呼叫**您的程式碼**的方式。 透過選擇加入，您可以取得最新的行為和 ASP.NET Core 的長期行為。

下列程式碼會將相容性模式設定為 ASP.NET Core 2.2：

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup.cs?name=snippet1)]

建議您使用最新版本 (`CompatibilityVersion.Version_2_2`) 測試應用程式。 預計大部分的應用程式都不會使用最新版本進行重大行為變更。

呼叫 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)` 的應用程式會受到保護，防止執行 ASP.NET Core 2.1 MVC 和更新版本的 2.x 版所引進的可能重大行為變更。 這項保護：

* 不適用於所有 2.1 和更新版本的變更，它的目標是 MVC 子系統中的可能重大 ASP.NET Core 執行階段行為變更。
* 不會擴充到下一個主要版本。

適用於 ASP.NET Core 2.1 和更新版本的 2.x 應用程式且**不會**呼叫 `SetCompatibilityVersion` 的預設相容性為 2.0 相容性。 也就是說，不呼叫 `SetCompatibilityVersion` 等同於呼叫 `SetCompatibilityVersion(CompatibilityVersion.Version_2_0)`。

下列程式碼會將相容性模式設定為 ASP.NET Core 2.2，但下列行為除外：

* <xref:Microsoft.AspNetCore.Mvc.MvcOptions.AllowCombiningAuthorizeFilters>
* <xref:Microsoft.AspNetCore.Mvc.MvcOptions.InputFormatterExceptionPolicy>

[!code-csharp[Main](compatibility-version/samples/2.x/CompatibilityVersionSample/Startup2.cs?name=snippet1)]

對於出現重大行為變更的應用程式，使用適當的相容性參數：

* 可讓您使用最新版本，並選擇退出特定的重大行為變更。
* 讓您有時間來更新您的應用程式，使其適用於最新的變更。

<xref:Microsoft.AspNetCore.Mvc.MvcOptions> 文件充分說明變更的項目，以及所做變更對於大部分使用者來說都得到改善的原因。

在未來某個日期將會推出 [ASP.NET Core 3.0 版](https://github.com/aspnet/Home/wiki/Roadmap)。 3.0 版將移除相容性參數支援的舊行為。 我們覺得這些是有利於幾乎所有使用者的正向變更。 現在引進這些變更，大部分的應用程式皆可獲益，而其他人則有時間來更新其應用程式。
