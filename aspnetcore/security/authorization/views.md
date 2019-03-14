---
title: ASP.NET Core MVC 中的檢視為基礎的授權
author: rick-anderson
description: 本文件將示範如何插入和使用授權服務內的 ASP.NET Core Razor 檢視。
ms.author: riande
ms.date: 10/30/2017
uid: security/authorization/views
ms.openlocfilehash: e497c41d4dca29fed8733f18cf727804e3f06d8c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047885"
---
# <a name="view-based-authorization-in-aspnet-core-mvc"></a>ASP.NET Core MVC 中的檢視為基礎的授權

開發人員通常會想要顯示、 隱藏或其他方式修改目前的使用者身分識別為基礎的 UI。 您可以存取透過 MVC 檢視中存在的授權服務[相依性插入](xref:fundamentals/dependency-injection)。 若要插入的 Razor 檢視中的 「 授權 」 服務，使用`@inject`指示詞：

```cshtml
@using Microsoft.AspNetCore.Authorization
@inject IAuthorizationService AuthorizationService
```

如果您想在每個檢視中的授權服務，將放`@inject`到指示詞 *_ViewImports.cshtml*檔案*檢視*目錄。 如需詳細資訊，請參閱[在檢視中插入相依性](xref:mvc/views/dependency-injection)。

使用插入的授權服務叫用`AuthorizeAsync`完全相同的方式時，您會檢查[資源為基礎的授權](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, "PolicyName")).Succeeded)
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, "PolicyName"))
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

---

在某些情況下，資源會檢視模型。 叫用`AuthorizeAsync`完全相同的方式時，您會檢查[資源為基礎的授權](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit)).Succeeded)
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit))
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

---

在上述程式碼中，模型會傳遞做為原則評估應採取的資源納入考量。

> [!WARNING]
> 不要依賴於您的應用程式 UI 項目切換可見性為唯一的授權檢查。 隱藏 UI 項目可能無法完全防止存取其相關聯的控制器動作。 例如，請考慮上面的程式碼片段中的按鈕。 使用者可以叫用`Edit`動作方法，如果他或她知道相對資源 URL 是 */Document/Edit/1*。 基於這個理由，`Edit`動作方法應該會執行它自己的授權檢查。
