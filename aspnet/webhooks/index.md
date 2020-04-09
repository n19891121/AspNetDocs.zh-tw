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
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="fd3b4-103">ASP.NET WebHooks 概述</span><span class="sxs-lookup"><span data-stu-id="fd3b4-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="fd3b4-104">WebHooks 是一種輕巧級的 HTTP 模式,提供簡單的 pub/子模型,用於將 Web API 和 SaaS 服務連接在一起。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="fd3b4-105">當服務中發生事件時,通知以 HTTP POST 請求的形式發送給註冊訂閱者。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="fd3b4-106">POST 請求包含有關事件的資訊,使接收方能夠採取相應行動。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="fd3b4-107">由於其簡單性,WebHook已經暴露出大量的服務,包括[Dropbox,GitHub,](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[GitHub](https://www.github.com/)[,MailChimp,PayPal,](http://www.mailchimp.com/)[鬆弛](http://www.slack.com),[PayPal](http://www.paypal.com/)[條紋](http://www.stripe.com),[特雷洛](http://www.trello.com/),以及更多。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="fd3b4-108">例如,WebHook 可以指示[Dropbox](http://dropbox.com/)中的檔已更改,或者已在 GitHub 中提交代碼更改,或者已在[PayPal](http://www.paypal.com/)中啟動付款,或者已在[Trello](http://www.trello.com/)中創建了一張卡。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="fd3b4-109">可能性是無窮無盡的!</span><span class="sxs-lookup"><span data-stu-id="fd3b4-109">The possibilities are endless!</span></span>

<span data-ttu-id="fd3b4-110">Microsoft ASP.NET WebHooks 使傳送和接收 WebHook 變得更容易,作為 ASP.NET 應用程式的一部分:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="fd3b4-111">在接收端,它提供了一個用於接收和處理來自任意數量的 WebHook 提供商的 WebHook 的通用模型。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="fd3b4-112">它出來的盒子與[支援Dropbox,GitHub,](http://dropbox.com/)[比特巴克](https://bitbucket.org/)[,MailChimp,](http://www.mailchimp.com/)[貝寶](http://www.paypal.com/),[推手](http://www.pusher.com),[銷售部隊](http://www.salesforce.com),[鬆弛](http://www.slack.com),[條紋](http://www.stripe.com),[特雷洛](http://www.trello.com/)[,WordPress](http://www.wordpress.com)和[Zendesk,](https://www.zendesk.com/)但它是很容易添加支援更多。 [GitHub](https://www.github.com/)</span><span class="sxs-lookup"><span data-stu-id="fd3b4-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="fd3b4-113">在發送端,它支援管理和存儲訂閱以及向正確的訂閱者集發送事件通知。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="fd3b4-114">這允許您定義您自己的事件集,訂閱者可以訂閱這些事件,並在事件發生時通知它們。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="fd3b4-115">這兩個部分可以一起使用,也可以分開使用,具體取決於您的方案。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="fd3b4-116">如果您只需要從其他服務接收 WebHook,則只需使用接收方部件;如果你只想公開WebHook供他人使用,那麼你可以這樣做。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="fd3b4-117">代碼以web API 2ASP.NET,ASP.NET MVC 5,在[GitHub 上作為 OSS](https://github.com/aspnet/WebHooks)提供。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="fd3b4-118">網頁概述</span><span class="sxs-lookup"><span data-stu-id="fd3b4-118">WebHooks Overview</span></span>

<span data-ttu-id="fd3b4-119">WebHooks 是一種模式,這意味著它因服務而異,但基本思想是相同的。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="fd3b4-120">您可以將 WebHooks 視為一個簡單的 pub/子模型,用戶可以訂閱在其他地方發生的事件。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="fd3b4-121">事件通知作為 HTTP POST 請求傳播,其中包含有關事件本身的資訊。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="fd3b4-122">通常,HTTP POST 請求包含由 WebHook 發送方確定的 JSON 物件或 HTML 表單數據,包括有關導致 WebHook 觸發的事件的資訊。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="fd3b4-123">例如,由於在特定存儲庫中打開新問題[,GitHub](https://www.github.com/)的 WebHook POST 請求正文如下所示:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-123">For example, a WebHook POST request body from [GitHub](https://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

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

<span data-ttu-id="fd3b4-124">為了確保 WebHook 確實來自預期的發送方,POST 請求以某種方式受到保護,然後由接收方進行驗證。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="fd3b4-125">例如[,GitHub WebHooks](https://developer.github.com/webhooks/)包括一個*X-Hub 簽名*HTTP 標頭,其中包含請求正文的哈希,由接收方實現進行檢查,因此您不必擔心。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="fd3b4-126">WebHook 流通常如下所示:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="fd3b4-127">WebHook 發送者公開用戶端可以訂閱的事件。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="fd3b4-128">這些事件描述對系統的可觀察更改,例如插入了新的數據項、進程已完成或其他內容。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="fd3b4-129">WebHook 接收器透過註冊包含四個內容的 WebHook 進行訂閱:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="fd3b4-130">以 HTTP POST 請求的形式發布事件通知的 URI;</span><span class="sxs-lookup"><span data-stu-id="fd3b4-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="fd3b4-131">一組篩選器,描述應為其觸發 WebHook 的特定事件;</span><span class="sxs-lookup"><span data-stu-id="fd3b4-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="fd3b4-132">用於對 HTTP POST 請求進行簽名的金鑰;</span><span class="sxs-lookup"><span data-stu-id="fd3b4-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="fd3b4-133">要包含在 HTTP POST 請求中的其他數據。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="fd3b4-134">例如,這可以是 HTTP POST 請求正文中包含的其他 HTTP 標頭欄位或屬性。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="fd3b4-135">事件發生後,將找到匹配的 WebHook 註冊,並提交 HTTP POST 請求。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="fd3b4-136">通常,如果收件者由於某種原因未回應或 HTTP POST 請求導致錯誤回應,則多次重試 HTTP POST 請求的生成。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="fd3b4-137">WebHooks 處理導管</span><span class="sxs-lookup"><span data-stu-id="fd3b4-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="fd3b4-138">Microsoft ASP.NET WebHooks 處理管道以造訪傳入 WebHook 如下所示:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![ASP.NET WebHooks 處理導管](_static/WebHookReceivers.png)

<span data-ttu-id="fd3b4-140">這裡的兩個關鍵概念是*接收器*與*處理程式*:</span><span class="sxs-lookup"><span data-stu-id="fd3b4-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="fd3b4-141">*接收方*負責處理來自給定發件者的 WebHook 的特定風格,並強制進行安全檢查,以確保 WebHook 請求確實來自預期的寄件者。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="fd3b4-142">*處理程式*通常是使用者代碼運行處理特定 WebHook 的位置。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="fd3b4-143">在以下節點中,這些概念將更詳細地描述。</span><span class="sxs-lookup"><span data-stu-id="fd3b4-143">In the following nodes these concepts are described in more details.</span></span>
