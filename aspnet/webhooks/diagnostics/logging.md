---
uid: webhooks/diagnostics/logging
title: ASP.NET WebHook 記錄 |微軟文件
author: rick-anderson
description: 如何ASP.NET WebHook 進行登錄。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: 350732acbd3a73bddb8f8b20dcd50c225d89be82
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675350"
---
# <a name="aspnet-webhooks-logging"></a><span data-ttu-id="88bf1-103">ASP.NET WebHooks 紀錄記錄</span><span class="sxs-lookup"><span data-stu-id="88bf1-103">ASP.NET WebHooks logging</span></span>

<span data-ttu-id="88bf1-104">微軟ASP.NETWebHooks使用日誌記錄作為報告問題和問題的一種方式。</span><span class="sxs-lookup"><span data-stu-id="88bf1-104">Microsoft ASP.NET WebHooks uses logging as a way of reporting issues and problems.</span></span> <span data-ttu-id="88bf1-105">默認情況下,日誌使用[System.診斷.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)編寫,可以使用[跟蹤偵聽器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日誌流一樣進行編寫日誌。</span><span class="sxs-lookup"><span data-stu-id="88bf1-105">By default logs are written using [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) where they can be manged using [Trace Listeners](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) like any other log stream.</span></span>

<span data-ttu-id="88bf1-106">將 Web 應用程式部署為 Azure Web 應用時,將自動拾取日誌,並[可以與其他系統](https://msdn.microsoft.com/library/system.diagnostics.trace)一起管理。</span><span class="sxs-lookup"><span data-stu-id="88bf1-106">When deploying your Web Application as an Azure Web App, the logs are automatically picked up and can be managed together with any other [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) logging.</span></span> <span data-ttu-id="88bf1-107">有關詳細資訊,請參閱在[Azure 應用服務中為 Web 應用啟用診斷日誌記錄](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span><span class="sxs-lookup"><span data-stu-id="88bf1-107">For details, please see [Enable diagnostics logging for web apps in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)</span></span>

<span data-ttu-id="88bf1-108">此外,可以直接從 Visual Studio 內部獲取日誌,如[使用 Visual Studio 在 Azure 應用服務中排除 Web 應用時](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)所述。</span><span class="sxs-lookup"><span data-stu-id="88bf1-108">In addition, logs can be obtained straight from inside Visual Studio as described in [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="redirecting-logs"></a><span data-ttu-id="88bf1-109">重定向紀錄</span><span class="sxs-lookup"><span data-stu-id="88bf1-109">Redirecting Logs</span></span>

<span data-ttu-id="88bf1-110">可以提供可直接登錄到日誌管理員(如[Log4Net](http://logging.apache.org/log4net/)和[NLog)](http://nlog-project.org/)的備用日誌記錄實現,而不是將日誌寫入[System.診斷.Trace。](https://msdn.microsoft.com/library/system.diagnostics.trace)</span><span class="sxs-lookup"><span data-stu-id="88bf1-110">Instead of writing logs to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace), it is possible to provide an alternate logging implementation that can log directly to a log manager such as [Log4Net](http://logging.apache.org/log4net/) and [NLog](http://nlog-project.org/).</span></span> <span data-ttu-id="88bf1-111">只需提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的實現,並將其註冊到您選擇的依賴項注入引擎,它將被 Microsoft ASP.NET WebHooks 拾取。</span><span class="sxs-lookup"><span data-stu-id="88bf1-111">Simply provide an implementation of [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) and register it with a dependency injection engine of your choice and it will get picked up by Microsoft ASP.NET WebHooks.</span></span> <span data-ttu-id="88bf1-112">有關詳細資訊,請參閱[ASP.NET Web API 2 中的相依項注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="88bf1-112">Please see [Dependency Injection in ASP.NET Web API 2](https://www.asp.net/web-api/overview/advanced/dependency-injection) for details.</span></span>
