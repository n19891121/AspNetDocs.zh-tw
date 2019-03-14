---
title: ASP.NET Core 中的環境標籤協助程式
author: pkellner
description: 定義了 ASP.NET Core 環境標籤協助程式，包括所有屬性
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/environment-tag-helper
ms.openlocfilehash: 379f58ed37329f047d53adf1dcfdfd2ad6a6ca4e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028625"
---
# <a name="environment-tag-helper-in-aspnet-core"></a>ASP.NET Core 中的環境標籤協助程式

作者：[Peter Kellner](http://peterkellner.net)、[Hisham Bin Ateya](https://twitter.com/hishambinateya) 和 [Luke Latham](https://github.com/guardrex)

環境標籤協助程式依據目前的[主控環境](xref:fundamentals/environments)，有條件地轉譯含括內容。 環境標籤協助程式的單一屬性 `names`，是以逗號分隔的環境名稱清單。 如果任何提供的環境名稱符合目前環境，則會轉譯含括的內容。

如需標籤協助程式的概觀，請參閱 <xref:mvc/views/tag-helpers/intro>。

## <a name="environment-tag-helper-attributes"></a>環境標籤協助程式屬性

### <a name="names"></a>名稱

`names` 會接受單一主控環境名稱或以逗號分隔的主控環境名稱清單，這些名稱會觸發轉譯含括的內容。

環境值會與 [IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*) 所傳回的目前值比較。 比較會忽略大小寫。

下列範例使用環境標籤協助程式。 如果主控環境為「暫存」或「生產」，將會轉譯內容：

```cshtml
<environment names="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

::: moniker range=">= aspnetcore-2.0"

## <a name="include-and-exclude-attributes"></a>include 和 exclude 屬性

`include` & `exclude` 屬性會依據包含或排除的主控環境名稱，來控制含括內容的轉譯。

### <a name="include"></a>include

`include` 屬性會表現出類似 `names` 屬性的行為。 `include` 屬性值中列出的環境，必須與應用程式的主控環境 ([IHostingEnvironment.EnvironmentName](xref:Microsoft.AspNetCore.Hosting.IHostingEnvironment.EnvironmentName*)) 相符，才能轉譯 `<environment>` 標籤的內容。

```cshtml
<environment include="Staging,Production">
    <strong>HostingEnvironment.EnvironmentName is Staging or Production</strong>
</environment>
```

### <a name="exclude"></a>exclude

與 `include` 屬性相反，當主控環境與 `exclude` 屬性值中列出的環境不相符時，將轉譯 `<environment>` 標記的內容。

```cshtml
<environment exclude="Development">
    <strong>HostingEnvironment.EnvironmentName is not Development</strong>
</environment>
```

::: moniker-end

## <a name="additional-resources"></a>其他資源

* <xref:fundamentals/environments>
