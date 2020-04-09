---
uid: webhooks/receiving/receivers
title: ASP.NET WebHook 接收器 |微軟文件
author: rick-anderson
description: ASP.NET WebHook 接收器
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675159"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET WebHook 接收器

接收 WebHook 取決於寄件者是誰。 有時,還有其他步驟註冊 WebHook,驗證訂閱者是否真正在偵聽。 某些 WebHook 提供推送到拉取模型,其中 HTTP POST 請求僅包含對事件資訊的引用,然後由該引用獨立檢索。 通常,安全模型差異很大。

Microsoft ASP.NET WebHooks 的目的是使連接 API 更簡單、更一致,而無需花費大量時間來瞭解如何處理 WebHook 的任何特定變體。

WebHook 接收器負責接受和驗證來自特定寄件者的 WebHook。 WebHook 接收器可以支援任意數量的 WebHook,每個 WebHook 都有自己的配置。 例如,GitHub WebHook 接收器可以接受來自任意數量的 GitHub 儲存庫的 WebHook。

## <a name="webhook-receiver-uris"></a>WebHook 接收器 URI

通過安裝 Microsoft ASP.NET WebHooks,您可以獲得一個常規 WebHook 控制器,該控制器接受來自開源服務數量的 WebHook 請求。 請求到達時,它會選擇已安裝的用於處理特定 WebHook 發送方的相應接收器。

此控制器的 URI 是您向服務註冊的 WebHook URI,其形式為:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

出於安全原因,許多 WebHook 接收器要求 URI 是*Htcript,* 在某些情況下,它還必須包含一個額外的查詢參數,用於強制只有目標方才能將 WebHook 發送到上述 URI。

元件`<receiver>`是接收器名稱,例如`github`或`slack`。

*{id}* 是一個可選識別碼,可用於識別特定的 WebHook 接收器設定。 這可用於向特定接收器註冊 N WebHook。 例如,以下三個 URI 可用於註冊三個獨立的 WebHook:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>安裝 WebHook 接收器

要使用 Microsoft ASP.NET WebHook 接收 WebHook,請首先為要接收 WebHook 的 WebHook 提供者或提供者安裝 Nuget 包。 Nuget 包名為[Microsoft.AspNet.WebHooks.Receivers.*,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中最後一部分表示支援的服務。 例如：

[微軟.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)支援接收來自GitHub和[微軟的WebHook.AspNet.WebHooks.Receivers.Customs.Customs](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)為接收由ASP.NETWebHooks生成的WebHook提供支援。

開箱即用,您可以找到對 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、Slack、Stripe、Trello 和 WordPress 的支援,但可以支援任意數量的其他供應商。

## <a name="configuring-a-webhook-receiver"></a>設定 WebHook 接收器

WebHook 接收器透過[IWebHookReceiverConfig 整](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)面進行配置,該介面的特定實現可以使用任何依賴項注入模型進行註冊。 預設實現使用應用程式設置,可以在 Web.config 檔中設置,或者,如果使用 Azure Web 應用,可以通過[Azure 門戶](https://portal.azure.com/)進行設置。

![API 應用程式設定](_static/AzureAppSettings.png)

應用程式設定鍵的格式如下:

```
MS_WebHookReceiverSecret_<receiver>
```

該值是與已註冊 WebHook 的 *[id]* 值符合的逗號分隔的值清單,例如:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>初始化 WebHook 接收器

WebHook 接收器透過註冊來初始化,通常在*WebApiConfig*靜態類別中,例如:

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
