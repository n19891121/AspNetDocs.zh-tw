---
uid: webhooks/source
title: ASP.NET WebHooks 源代碼和 NuGet 包 |微軟文件
author: rick-anderson
description: 指向ASP.NET WebHooks 原始碼和 NuGet 套件的連結
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: ad368125878871c0e38f35152c86fe4eea143924
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675314"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET WebHooks 源碼和 NuGet 套件

微軟ASP.NETWebHooks是微軟ASP.NET模組系列的一部分,並作為[開放源碼專案在GitHub上](https://github.com/aspnet/WebHooks)託管。 這意味著我們接受捐款,但在提交拉取請求之前,請查看[「貢獻指南](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)」。

您現在閱讀的此連線文件也託管[在 GitHub 上作為開源](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide),並接受貢獻。

## <a name="nuget-packages"></a>NuGet 套件

[NuGet 套件](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分為三個部分:

* [常見](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):在發送方和接收方之間共用的通用包。

* [寄件者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):一組包,支援向他人發送您自己的 WebHook。 發送 WebHook 的功能在[發送 WebHook](sending/senders.md)中進行了更詳細的描述。

* [接收者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):一組支援接收他人 WebHook 的包。 接收 WebHook 的功能在[接收 WebHook](receiving/index.md)中進行了更詳細的描述。
