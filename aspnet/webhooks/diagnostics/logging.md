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
# <a name="aspnet-webhooks-logging"></a>ASP.NET WebHooks 紀錄記錄

微軟ASP.NETWebHooks使用日誌記錄作為報告問題和問題的一種方式。 默認情況下,日誌使用[System.診斷.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)編寫,可以使用[跟蹤偵聽器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)像任何其他日誌流一樣進行編寫日誌。

將 Web 應用程式部署為 Azure Web 應用時,將自動拾取日誌,並[可以與其他系統](https://msdn.microsoft.com/library/system.diagnostics.trace)一起管理。 有關詳細資訊,請參閱在[Azure 應用服務中為 Web 應用啟用診斷日誌記錄](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

此外,可以直接從 Visual Studio 內部獲取日誌,如[使用 Visual Studio 在 Azure 應用服務中排除 Web 應用時](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)所述。

## <a name="redirecting-logs"></a>重定向紀錄

可以提供可直接登錄到日誌管理員(如[Log4Net](http://logging.apache.org/log4net/)和[NLog)](http://nlog-project.org/)的備用日誌記錄實現,而不是將日誌寫入[System.診斷.Trace。](https://msdn.microsoft.com/library/system.diagnostics.trace) 只需提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的實現,並將其註冊到您選擇的依賴項注入引擎,它將被 Microsoft ASP.NET WebHooks 拾取。 有關詳細資訊,請參閱[ASP.NET Web API 2 中的相依項注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)。
