---
uid: webhooks/index
title: ASP.NET網頁概述 |微軟文件
author: rick-anderson
description: ASP.NET網路鉤子的簡介。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa5fa190386ec803a6801de2d815c948677fe1f5
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675434"
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET WebHooks 概述

WebHooks 是一種輕巧級的 HTTP 模式,提供簡單的 pub/子模型,用於將 Web API 和 SaaS 服務連接在一起。 當服務中發生事件時,通知以 HTTP POST 請求的形式發送給註冊訂閱者。 POST 請求包含有關事件的資訊,使接收方能夠採取相應行動。

由於其簡單性,WebHook已經暴露出大量的服務,包括[Dropbox,GitHub,](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[GitHub](https://www.github.com/)[,MailChimp,PayPal,](http://www.mailchimp.com/)[鬆弛](http://www.slack.com),[PayPal](http://www.paypal.com/)[條紋](http://www.stripe.com),[特雷洛](http://www.trello.com/),以及更多。 例如,WebHook 可以指示[Dropbox](http://dropbox.com/)中的檔已更改,或者已在 GitHub 中提交代碼更改,或者已在[PayPal](http://www.paypal.com/)中啟動付款,或者已在[Trello](http://www.trello.com/)中創建了一張卡。 可能性是無窮無盡的!

Microsoft ASP.NET WebHooks 使傳送和接收 WebHook 變得更容易,作為 ASP.NET 應用程式的一部分:

* 在接收端,它提供了一個用於接收和處理來自任意數量的 WebHook 提供商的 WebHook 的通用模型。 它出來的盒子與[支援Dropbox,GitHub,](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[,MailChimp,](http://www.mailchimp.com/)[貝寶](http://www.paypal.com/),[推手](http://www.pusher.com),[銷售部隊](http://www.salesforce.com),[鬆弛](http://www.slack.com),[條紋](http://www.stripe.com),[特雷洛](http://www.trello.com/)[,WordPress](http://www.wordpress.com)和[Zendesk,](https://www.zendesk.com/)但它是很容易添加支援更多。 [GitHub](https://www.github.com/)

* 在發送端,它支援管理和存儲訂閱以及向正確的訂閱者集發送事件通知。 這允許您定義您自己的事件集,訂閱者可以訂閱這些事件,並在事件發生時通知它們。

這兩個部分可以一起使用,也可以分開使用,具體取決於您的方案。 如果您只需要從其他服務接收 WebHook,則只需使用接收方部件;如果你只想公開WebHook供他人使用,那麼你可以這樣做。

代碼以web API 2ASP.NET,ASP.NET MVC 5,在[GitHub 上作為 OSS](https://github.com/aspnet/WebHooks)提供。

## <a name="webhooks-overview"></a>網頁概述

WebHooks 是一種模式,這意味著它因服務而異,但基本思想是相同的。 您可以將 WebHooks 視為一個簡單的 pub/子模型,用戶可以訂閱在其他地方發生的事件。 事件通知作為 HTTP POST 請求傳播,其中包含有關事件本身的資訊。

通常,HTTP POST 請求包含由 WebHook 發送方確定的 JSON 物件或 HTML 表單數據,包括有關導致 WebHook 觸發的事件的資訊。 例如,由於在特定存儲庫中打開新問題[,GitHub](https://www.github.com/)的 WebHook POST 請求正文如下所示:

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

為了確保 WebHook 確實來自預期的發送方,POST 請求以某種方式受到保護,然後由接收方進行驗證。 例如[,GitHub WebHooks](https://developer.github.com/webhooks/)包括一個*X-Hub 簽名*HTTP 標頭,其中包含請求正文的哈希,由接收方實現進行檢查,因此您不必擔心。

WebHook 流通常如下所示:

* WebHook 發送者公開用戶端可以訂閱的事件。 這些事件描述對系統的可觀察更改,例如插入了新的數據項、進程已完成或其他內容。

* WebHook 接收器透過註冊包含四個內容的 WebHook 進行訂閱:

     1. 以 HTTP POST 請求的形式發布事件通知的 URI;

     2. 一組篩選器,描述應為其觸發 WebHook 的特定事件;

     3. 用於對 HTTP POST 請求進行簽名的金鑰;

     4. 要包含在 HTTP POST 請求中的其他數據。 例如,這可以是 HTTP POST 請求正文中包含的其他 HTTP 標頭欄位或屬性。

* 事件發生後,將找到匹配的 WebHook 註冊,並提交 HTTP POST 請求。 通常,如果收件者由於某種原因未回應或 HTTP POST 請求導致錯誤回應,則多次重試 HTTP POST 請求的生成。

## <a name="webhooks-processing-pipeline"></a>WebHooks 處理導管

Microsoft ASP.NET WebHooks 處理管道以造訪傳入 WebHook 如下所示:

![ASP.NET WebHooks 處理導管](_static/WebHookReceivers.png)

這裡的兩個關鍵概念是*接收器*與*處理程式*:

* *接收方*負責處理來自給定發件者的 WebHook 的特定風格,並強制進行安全檢查,以確保 WebHook 請求確實來自預期的寄件者。

* *處理程式*通常是使用者代碼運行處理特定 WebHook 的位置。

在以下節點中,這些概念將更詳細地描述。
