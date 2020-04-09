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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="f16a8-103">ASP.NET WebHooks 源碼和 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="f16a8-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="f16a8-104">微軟ASP.NETWebHooks是微軟ASP.NET模組系列的一部分,並作為[開放源碼專案在GitHub上](https://github.com/aspnet/WebHooks)託管。</span><span class="sxs-lookup"><span data-stu-id="f16a8-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="f16a8-105">這意味著我們接受捐款,但在提交拉取請求之前,請查看[「貢獻指南](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md)」。</span><span class="sxs-lookup"><span data-stu-id="f16a8-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="f16a8-106">您現在閱讀的此連線文件也託管[在 GitHub 上作為開源](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide),並接受貢獻。</span><span class="sxs-lookup"><span data-stu-id="f16a8-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="f16a8-107">NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="f16a8-107">NuGet packages</span></span>

<span data-ttu-id="f16a8-108">[NuGet 套件](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks)分為三個部分:</span><span class="sxs-lookup"><span data-stu-id="f16a8-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="f16a8-109">[常見](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common):在發送方和接收方之間共用的通用包。</span><span class="sxs-lookup"><span data-stu-id="f16a8-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="f16a8-110">[寄件者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom):一組包,支援向他人發送您自己的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="f16a8-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="f16a8-111">發送 WebHook 的功能在[發送 WebHook](sending/senders.md)中進行了更詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="f16a8-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="f16a8-112">[接收者](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers):一組支援接收他人 WebHook 的包。</span><span class="sxs-lookup"><span data-stu-id="f16a8-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="f16a8-113">接收 WebHook 的功能在[接收 WebHook](receiving/index.md)中進行了更詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="f16a8-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
