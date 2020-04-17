---
uid: signalr/overview/older-versions/troubleshooting
title: 信號R故障排除(信號R 1.x) |微軟文件
author: bradygaster
description: 本文介紹了開發SignalR應用的常見問題。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: e65ce086d28cff2a36c609f47a05af632081be63
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543089"
---
# <a name="signalr-troubleshooting-signalr-1x"></a><span data-ttu-id="8a4d1-103">SignalR 疑難排解 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="8a4d1-103">SignalR Troubleshooting (SignalR 1.x)</span></span>

<span data-ttu-id="8a4d1-104">由[派翠克·弗萊徹](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="8a4d1-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="8a4d1-105">本文檔介紹 SignalR 的常見故障排除問題。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-105">This document describes common troubleshooting issues with SignalR.</span></span>

<span data-ttu-id="8a4d1-106">本文檔包含以下部分。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-106">This document contains the following sections.</span></span>

- [<span data-ttu-id="8a4d1-107">用戶端與伺服器之間的呼叫方法以靜默方式失敗</span><span class="sxs-lookup"><span data-stu-id="8a4d1-107">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="8a4d1-108">其他連線問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-108">Other connection issues</span></span>](#other)
- [<span data-ttu-id="8a4d1-109">編譯與伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-109">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="8a4d1-110">視覺工作室問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-110">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="8a4d1-111">網際網路資訊服務問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-111">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="8a4d1-112">Azure 問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-112">Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="8a4d1-113">用戶端與伺服器之間的呼叫方法以靜默方式失敗</span><span class="sxs-lookup"><span data-stu-id="8a4d1-113">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="8a4d1-114">本節介紹客戶端和伺服器之間的方法調用失敗而不出現有意義的錯誤消息的可能原因。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-114">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="8a4d1-115">在 SignalR 應用程式中,伺服器沒有關於客戶端實現的方法的資訊;因此,伺服器沒有實現的方法。當伺服器調用用戶端方法時,方法名稱和參數數據將發送到用戶端,並且僅當該方法以伺服器指定的格式存在時才執行該方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-115">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="8a4d1-116">如果在用戶端上找不到匹配方法,則不發生任何操作,並且伺服器上不引發錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-116">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="8a4d1-117">要進一步調查未被調用的用戶端方法,可以在調用集線器上的 start 方法之前打開日誌記錄,以查看來自伺服器的調用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-117">To further investigate client methods not getting called, you can turn on logging before calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="8a4d1-118">要在 JavaScript 應用程式中啟用日誌記錄,請參閱[如何啟用用戶端日誌記錄(JAvaScript 用戶端版本)。](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="8a4d1-118">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="8a4d1-119">要在 .NET 用戶端應用程式中啟用日誌記錄,請參閱[如何啟用用戶端日誌記錄 (.NET 用戶端版本)。](../guide-to-the-api/hubs-api-guide-net-client.md#logging)</span><span class="sxs-lookup"><span data-stu-id="8a4d1-119">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="8a4d1-120">拼字錯誤的方法、不正確的方法簽名或不正確的中心名稱</span><span class="sxs-lookup"><span data-stu-id="8a4d1-120">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="8a4d1-121">如果被調用方法的名稱或簽名與用戶端上的適當方法不完全匹配,則調用將失敗。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-121">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="8a4d1-122">驗證伺服器調用的方法名稱是否與用戶端上的方法的名稱匹配。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-122">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="8a4d1-123">此外,SignalR 使用駱駝大小寫方法創建集線器代理,這在 JavaScript 中`SendMessage`是合適的 ,因此`sendMessage`在用戶端代理中 調用伺服器上調用的方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-123">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="8a4d1-124">如果在伺服器端代碼`HubName`中使用該屬性,請驗證所使用的名稱是否與在用戶端上創建中心的名稱匹配。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-124">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="8a4d1-125">如果不使用`HubName`該 屬性,請驗證 JavaScript 用戶端中中心的名稱是否為駱駝大小寫,例如聊天Hub而不是 ChatHub。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-125">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="8a4d1-126">用戶端上的重複方法名稱</span><span class="sxs-lookup"><span data-stu-id="8a4d1-126">Duplicate method name on client</span></span>

<span data-ttu-id="8a4d1-127">驗證用戶端上沒有僅因大小寫而異的重複方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-127">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="8a4d1-128">如果用戶端應用程式具有稱為`sendMessage`的方法,請驗證是否也沒有調`SendMessage`用 的方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-128">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="8a4d1-129">用戶端上缺少 JSON 解析器</span><span class="sxs-lookup"><span data-stu-id="8a4d1-129">Missing JSON parser on the client</span></span>

<span data-ttu-id="8a4d1-130">SignalR 需要 JSON 解析器存在以序列化伺服器和用戶端之間的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-130">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="8a4d1-131">如果客戶端沒有內置的 JSON 解析器(如 Internet Explorer 7),則需要在應用程式中包含一個。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-131">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="8a4d1-132">你可以[在這裡](http://nuget.org/packages/json2)下載JSON解析器。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-132">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="8a4d1-133">混合集線器與持久連接語法</span><span class="sxs-lookup"><span data-stu-id="8a4d1-133">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="8a4d1-134">SignalR 使用兩種通信模型:集線器和持久連接。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-134">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="8a4d1-135">調用這兩種通信模型的語法在客戶端代碼中是不同的。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-135">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="8a4d1-136">如果在伺服器代碼中添加了中心,請驗證所有用戶端代碼是否使用正確的中心語法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-136">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="8a4d1-137">**在 JavaScript 客戶端建立的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-137">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="8a4d1-138">**在 Javascript 客戶端建立中心代理的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-138">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="8a4d1-139">**將路由映射到持久連線的 C# 伺服器代碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-139">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="8a4d1-140">**C# 伺服器代碼,用於將路由映射到集線器,或者如果您有多個應用程式,則映射到多個集線器**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-140">**C# server code that maps a route to a Hub, or to multiple hubs if you have multiple applications**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="8a4d1-141">新增訂閱之前啟動的連線</span><span class="sxs-lookup"><span data-stu-id="8a4d1-141">Connection started before subscriptions are added</span></span>

<span data-ttu-id="8a4d1-142">如果在將可以從伺服器調用的方法添加到代理之前啟動中心連接,將不會接收消息。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-142">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="8a4d1-143">以下 JavaScript 代碼會無法正確啟動中心:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-143">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="8a4d1-144">**不正確的 JavaScript 客戶端碼,不允許接收中心訊息**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-144">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="8a4d1-145">而是在調用「開始」之前添加方法訂閱:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-145">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="8a4d1-146">**正確將訂閱加入中心的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-146">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="8a4d1-147">中心代理上缺少方法名稱</span><span class="sxs-lookup"><span data-stu-id="8a4d1-147">Missing method name on the hub proxy</span></span>

<span data-ttu-id="8a4d1-148">驗證在伺服器上定義的方法是否訂閱在用戶端上。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-148">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="8a4d1-149">即使伺服器定義了該方法,仍必須將其添加到用戶端代理中。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-149">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="8a4d1-150">方法可以通過以下方式添加到用戶端代理(請注意,該方法已添加到`client`中心 成員,而不是直接添加到中心):</span><span class="sxs-lookup"><span data-stu-id="8a4d1-150">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="8a4d1-151">**將方法加入到中心代理的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-151">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="8a4d1-152">未聲明為公共的集線器或中心方法</span><span class="sxs-lookup"><span data-stu-id="8a4d1-152">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="8a4d1-153">要在用戶端上可見,必須將中心實現和方法聲明為`public`。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-153">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="8a4d1-154">從其他應用程式存取集線器</span><span class="sxs-lookup"><span data-stu-id="8a4d1-154">Accessing hub from a different application</span></span>

<span data-ttu-id="8a4d1-155">信號R中心只能通過實現SignalR用戶端的應用程序進行訪問。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-155">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="8a4d1-156">SignalR 不能與其他通訊庫(如 SOAP 或 WCF Web 服務)互通。如果目標平台沒有可用的 SignalR 用戶端,則無法直接訪問伺服器的終結點。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-156">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="8a4d1-157">手動序列化資料</span><span class="sxs-lookup"><span data-stu-id="8a4d1-157">Manually serializing data</span></span>

<span data-ttu-id="8a4d1-158">SignalR 將自動使用 JSON 來序列化方法參數 - 無需自行執行。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-158">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="8a4d1-159">在 OnDisconnected 函數中的用戶端上未執行遠端中心方法</span><span class="sxs-lookup"><span data-stu-id="8a4d1-159">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="8a4d1-160">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-160">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-161">調用`OnDisconnected`時,中心已進入`Disconnected`狀態 ,不允許調用其他集線器方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-161">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="8a4d1-162">**C# 伺服器代碼,在「不斷開」事件中正確執行代碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-162">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a><span data-ttu-id="8a4d1-163">達到連線限制</span><span class="sxs-lookup"><span data-stu-id="8a4d1-163">Connection limit reached</span></span>

<span data-ttu-id="8a4d1-164">在 Windows 7 等用戶端作業系統上使用完整版本的 IIS 時,將強制實施 10 個連接限制。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-164">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="8a4d1-165">使用用戶端作業系統時,請使用IIS Express來避免此限制。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-165">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="8a4d1-166">跨域連接設定不正確</span><span class="sxs-lookup"><span data-stu-id="8a4d1-166">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="8a4d1-167">如果跨域連接(SignalR URL 與託管頁不在同一域中的連接)設置不正確,則連接可能會失敗,而不會出現錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-167">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="8a4d1-168">有關如何啟用跨域通訊的資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-168">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="8a4d1-169">使用 NTLM(活動目錄)在 .NET 用戶端中不起作用的連線</span><span class="sxs-lookup"><span data-stu-id="8a4d1-169">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="8a4d1-170">如果連接配置不正確,則使用域安全的 .NET 用戶端應用程式中的連接可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-170">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="8a4d1-171">要在網域環境中使用 SignalR,請使用以下方式設定所需的連線屬性:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-171">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="8a4d1-172">**連線認證認證的 C# 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-172">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="8a4d1-173">其他連線問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-173">Other connection issues</span></span>

<span data-ttu-id="8a4d1-174">本節介紹連接過程中發生的特定癥狀或錯誤消息的原因和解決方案。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-174">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="8a4d1-175">「必須先呼叫開始才能送出資料」錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-175">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="8a4d1-176">如果代碼在連接啟動之前引用 SignalR 物件,則通常可以看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-176">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="8a4d1-177">必須在連接完成後添加處理程式的佈線等調用伺服器上定義的調用方法。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-177">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="8a4d1-178">請注意,調用`Start`是非同步的,因此在調用完成之前可以執行調用後的代碼。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-178">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="8a4d1-179">在連線完全啟動後添加處理程式的最佳方法是將它們放入回檔函數中,該函數作為參數傳遞給 start 方法:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-179">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="8a4d1-180">**正確新增參考 SignalR 物件的事件處理程式的 JavaScript 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-180">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="8a4d1-181">如果連接在仍在引用 SignalR 物件時停止,也會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-181">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="8a4d1-182">"301 永久移動'或"302臨時移動"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-182">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="8a4d1-183">如果專案包含名為 SignalR 的資料夾,則可能會看到此錯誤,這將干擾自動創建的代理。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-183">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="8a4d1-184">為了避免此錯誤,請勿使用應用程式中調用`SignalR`的資料夾,或關閉自動代理生成。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-184">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="8a4d1-185">有關詳細資訊[,請參閱產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-185">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="8a4d1-186">.NET 或銀光用戶端中的"403 禁止"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-186">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="8a4d1-187">此錯誤可能發生在跨域環境中,其中跨域通信未正確啟用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-187">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="8a4d1-188">有關如何啟用跨域通訊的資訊,請參閱[如何建立跨網域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-188">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="8a4d1-189">要在 Silverlight 用戶端中建立跨網域連接,請參閱[來自 Silverlight 用戶端的跨域連接](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-189">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="8a4d1-190">"404 找不到錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-190">"404 Not Found" error</span></span>

<span data-ttu-id="8a4d1-191">此問題有多種原因。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-191">There are several causes for this issue.</span></span> <span data-ttu-id="8a4d1-192">驗證以下所有情況:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-192">Verify all of the following:</span></span>

- <span data-ttu-id="8a4d1-193">**中心代理地址引用格式不正確:** 如果對生成的中心代理位址的引用格式不正確,則通常可以看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-193">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="8a4d1-194">驗證對中心位址的引用是否正確。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-194">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="8a4d1-195">關於詳細資訊[,請參閱如何參考動態產生的代理](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-195">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="8a4d1-196">**在新增中心路由之前向應用程式添加路由:** 如果應用程式使用其他路由,請驗證新增的第一個路由是否呼叫`MapHubs`。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-196">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapHubs`.</span></span>

### <a name="500-internal-server-error"></a><span data-ttu-id="8a4d1-197">"500 內部伺服器錯誤"</span><span class="sxs-lookup"><span data-stu-id="8a4d1-197">"500 Internal Server Error"</span></span>

<span data-ttu-id="8a4d1-198">這是一個非常通用的錯誤,可能有各種各樣的原因。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-198">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="8a4d1-199">錯誤的詳細資訊應出現在伺服器的事件日誌中,或者可以通過調試伺服器找到。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-199">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="8a4d1-200">通過在伺服器上打開詳細的錯誤,可以獲得更詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-200">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="8a4d1-201">有關詳細資訊,請參閱如何處理[Hub 類別的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-201">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="8a4d1-202">型態錯誤:&lt;中心&gt;類型 未定義錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-202">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="8a4d1-203">如果調用`MapHubs`不正確,將導致此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-203">This error will result if the call to `MapHubs` is not made properly.</span></span> <span data-ttu-id="8a4d1-204">關於詳細資訊[,請參考如何註冊 SignalR 路由與設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-204">See [How to register the SignalR route and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="8a4d1-205">使用者代碼未處理 Json 序列化異常</span><span class="sxs-lookup"><span data-stu-id="8a4d1-205">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="8a4d1-206">驗證發送到方法的參數是否不包括不可序列化的類型(如檔句柄或資料庫連接)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-206">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="8a4d1-207">如果需要在不希望發送到用戶端的伺服器端物件上使用成員(出於安全性或序列化原因),請使用該`JSONIgnore`屬性。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-207">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="8a4d1-208">'協定錯誤:未知傳輸"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-208">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="8a4d1-209">如果用戶端不支援 SignalR 使用的傳輸,則可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-209">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="8a4d1-210">有關哪些瀏覽器可與 SignalR 一起使用的資訊,請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-210">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="8a4d1-211">"JavaScript 中心代理生成已被禁用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-211">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="8a4d1-212">如果`DisableJavaScriptProxies`設置時將發生此錯誤,同時還包括對 動態生成的代理`signalr/hubs`的引用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-212">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="8a4d1-213">有關手動建立代理的詳細資訊,請參閱[產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-213">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="8a4d1-214">連線 ID 格式不正確或使用者身份在作用 SignalR 連線期間無法變更錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-214">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="8a4d1-215">如果正在使用身份驗證,並且用戶端在停止連接之前註銷,則可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-215">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="8a4d1-216">解決方案是在註銷用戶端之前停止 SignalR 連接。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-216">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="8a4d1-217">"未捕獲錯誤:信號R:找不到 jQuery。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-217">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="8a4d1-218">請確定在 SignalR.js 檔錯誤之前引用 jQuery</span><span class="sxs-lookup"><span data-stu-id="8a4d1-218">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="8a4d1-219">SignalR JavaScript 用戶端需要 jQuery 才能運行。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-219">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="8a4d1-220">驗證對 jQuery 的引用是否正確,使用的路徑是否有效,以及對 jQuery 的引用是否位於對 SignalR 的引用之前。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-220">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="8a4d1-221">「未捕捉的類型錯誤:無法讀取屬性」&lt;屬性&gt;'未定義"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-221">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="8a4d1-222">此錯誤導致沒有正確引用 jQuery 或中心代理。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-222">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="8a4d1-223">驗證對 jQuery 和集線器代理的引用是否正確,使用的路徑是否有效,以及對 jQuery 的引用是否位於對集線器代理的引用之前。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-223">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="8a4d1-224">對集線器代理的預設引用應如下所示:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-224">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="8a4d1-225">**正確參考中心代理的 HTML 客戶端碼**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-225">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="8a4d1-226">執行時Binder異常未由使用者代碼處理錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-226">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="8a4d1-227">當使用不正確的重載`Hub.On`時,可能會出現此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-227">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="8a4d1-228">如果方法具有傳回值,則必須將傳回類型指定為泛型型態參數:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-228">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="8a4d1-229">**在用戶端上定義的方法(沒有產生的代理)**</span><span class="sxs-lookup"><span data-stu-id="8a4d1-229">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="8a4d1-230">連線 ID 不一致或頁面載入之間的連線中斷</span><span class="sxs-lookup"><span data-stu-id="8a4d1-230">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="8a4d1-231">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-231">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-232">由於中心物件託管在頁面物件中,因此在頁面刷新時將銷毀中心。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-232">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="8a4d1-233">多頁應用程式需要維護使用者和連接指示之間的關聯,以便它們在頁面載入之間保持一致。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-233">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="8a4d1-234">連接指示可以存儲在`ConcurrentDictionary`物件或資料庫中的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-234">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="8a4d1-235">"值不能為空"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-235">"Value cannot be null" error</span></span>

<span data-ttu-id="8a4d1-236">當前不支援具有可選參數的伺服器端方法;如果省略可選參數,該方法將失敗。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-236">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="8a4d1-237">有關詳細資訊,請參閱[可選參數](https://github.com/SignalR/SignalR/issues/324)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-237">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="8a4d1-238">Firefox 無法在&lt;位址&gt;建立與伺服器的連接「Firebug」 中的錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-238">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="8a4d1-239">如果 WebSocket 傳輸協商失敗,並且使用另一個傳輸,可以在 Firebug 中看到此錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-239">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="8a4d1-240">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-240">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="8a4d1-241">.NET 用戶端應用程式中的"遠端憑證根據驗證過程無效"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-241">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="8a4d1-242">如果伺服器需要自定義用戶端證書,則可以在發出請求之前向連接添加 x509 證書。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-242">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="8a4d1-243">使用此憑證加入到連線中`Connection.AddClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-243">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="8a4d1-244">驗證逾時後連接斷線</span><span class="sxs-lookup"><span data-stu-id="8a4d1-244">Connection drops after authentication times out</span></span>

<span data-ttu-id="8a4d1-245">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-245">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-246">當連接處於活動狀態時,無法修改身份驗證憑據;要刷新憑據,必須停止並重新啟動連接。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-246">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="8a4d1-247">使用 jQuery 移動時,OnConnected 被呼叫兩次</span><span class="sxs-lookup"><span data-stu-id="8a4d1-247">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="8a4d1-248">jQuery`initializePage`Mobile 的功能強制重新執行每個頁面中的文稿,從而創建第二個連接。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-248">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="8a4d1-249">此問題的解決方案包括:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-249">Solutions for this issue include:</span></span>

- <span data-ttu-id="8a4d1-250">在 JavaScript 檔之前包括對 jQuery 移動的引用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-250">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="8a4d1-251">通過設置`initializePage``$.mobile.autoInitializePage = false`禁用 函數。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-251">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="8a4d1-252">在開始連接之前,等待頁面完成初始化。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-252">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="8a4d1-253">使用伺服器傳送事件在 Silverlight 應用程式中延遲訊息</span><span class="sxs-lookup"><span data-stu-id="8a4d1-253">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="8a4d1-254">在 Silverlight 上使用伺服器發送的事件時,消息會延遲。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-254">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="8a4d1-255">要強制使用長輪詢,在啟動連接時使用以下內容:</span><span class="sxs-lookup"><span data-stu-id="8a4d1-255">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="8a4d1-256">使用永久幀協定"拒絕許可權"</span><span class="sxs-lookup"><span data-stu-id="8a4d1-256">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="8a4d1-257">這是一個已知的問題,[此處](https://github.com/SignalR/SignalR/issues/1963)描述。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-257">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="8a4d1-258">可以使用最新的 JQuery 庫看到此癥狀;解決方法是將應用程式降級為 JQuery 1.8.2。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-258">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="8a4d1-259">編譯與伺服器端錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-259">Compilation and server-side errors</span></span>

 <span data-ttu-id="8a4d1-260">以下部分包含編譯器和伺服器端運行時錯誤的可能解決方案。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-260">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="8a4d1-261">對中心實體的引用為空</span><span class="sxs-lookup"><span data-stu-id="8a4d1-261">Reference to Hub instance is null</span></span>

<span data-ttu-id="8a4d1-262">由於為每個連接創建了一個中心實例,因此無法自己在代碼中創建集線器的實例。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-262">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="8a4d1-263">要從中心外部調用方法,請參閱[如何調用用戶端方法並從中心類外部管理組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub),瞭解如何獲取對中心上下文的引用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-263">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="8a4d1-264">HTTPContext.當前.工作階段為空</span><span class="sxs-lookup"><span data-stu-id="8a4d1-264">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="8a4d1-265">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-265">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-266">SignalR 不支援ASP.NET會話狀態,因為啟用會話狀態將中斷雙工消息。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-266">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="8a4d1-267">沒有合適的方法可以重寫</span><span class="sxs-lookup"><span data-stu-id="8a4d1-267">No suitable method to override</span></span>

<span data-ttu-id="8a4d1-268">如果您使用的是來自舊文檔或博客的代碼,則可能會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-268">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="8a4d1-269">驗證您沒有引用已更改或棄用的方法的名稱(如`OnConnectedAsync`)。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-269">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="8a4d1-270">主機上下文擴展.WebSocket伺服器網址為空</span><span class="sxs-lookup"><span data-stu-id="8a4d1-270">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="8a4d1-271">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-271">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-272">此成員已棄用,不應使用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-272">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="8a4d1-273">"名為"Signalr.hubs"的路由已在路由集合中"錯誤</span><span class="sxs-lookup"><span data-stu-id="8a4d1-273">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="8a4d1-274">如果`MapHubs`應用程式調用了兩次,則將看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-274">This error will be seen if `MapHubs` is called twice by your application.</span></span> <span data-ttu-id="8a4d1-275">一些示例應用程式`MapHubs`直接調用全域應用程式檔中;其他人在包裝類中進行調用。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-275">Some example applications call `MapHubs` directly in the global application file; others make the call in a wrapper class.</span></span> <span data-ttu-id="8a4d1-276">確保應用程式不同時執行這兩種操作。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-276">Ensure that your application does not do both.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="8a4d1-277">視覺工作室問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-277">Visual Studio issues</span></span>

<span data-ttu-id="8a4d1-278">本節介紹視覺工作室中遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-278">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="8a4d1-279">文稿文件節點未顯示在解決方案資源管理員中</span><span class="sxs-lookup"><span data-stu-id="8a4d1-279">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="8a4d1-280">我們的一些教程將引導您到解決方案資源管理器中的"腳本文檔"節點進行調試。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-280">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="8a4d1-281">此節點由 JavaScript 除錯器生成,僅在 Internet 資源管理器中除錯瀏覽器客戶端時出現;如果使用 Chrome 或 Firefox,將不會顯示該節點。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-281">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="8a4d1-282">如果運行了另一個用戶端調試器(如 Silverlight 調試器),JAVAScript 調試器也不會運行。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-282">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="8a4d1-283">信號R在視覺工作室 2008 或更早版本上不起作用</span><span class="sxs-lookup"><span data-stu-id="8a4d1-283">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="8a4d1-284">這是設計的行為。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-284">This behavior is by design.</span></span> <span data-ttu-id="8a4d1-285">信號R需要 .NET 框架 4 或更高版本;這要求在 Visual Studio 2010 或更高版本中開發 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-285">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="8a4d1-286">IIS 問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-286">IIS issues</span></span>

<span data-ttu-id="8a4d1-287">本節包含互聯網資訊服務的問題。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-287">This section contains issues with Internet Information Services.</span></span>

### <a name="web-site-crashes-after-maphubs-call"></a><span data-ttu-id="8a4d1-288">地圖中心呼叫後網站崩潰</span><span class="sxs-lookup"><span data-stu-id="8a4d1-288">Web site crashes after MapHubs call</span></span>

<span data-ttu-id="8a4d1-289">此問題已在最新版本的 SignalR 中修復。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-289">This issue has been fixed in the latest version of SignalR.</span></span> <span data-ttu-id="8a4d1-290">使用 NuGet 更新安裝,驗證您使用的是最新版本的 SignalR。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-290">Verify that you are using the latest released version of SignalR by updating your installation using NuGet.</span></span>

<a id="azure"></a>

## <a name="azure-issues"></a><span data-ttu-id="8a4d1-291">Azure 問題</span><span class="sxs-lookup"><span data-stu-id="8a4d1-291">Azure issues</span></span>

<span data-ttu-id="8a4d1-292">本節包含 Microsoft Azure 的問題。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-292">This section contains issues with Microsoft Azure.</span></span>

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="8a4d1-293">變更主題名稱後,不會透過 Azure 背板接收訊息</span><span class="sxs-lookup"><span data-stu-id="8a4d1-293">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="8a4d1-294">Azure 背板使用的主題不用於使用者配置。</span><span class="sxs-lookup"><span data-stu-id="8a4d1-294">The topics used by the Azure backplane are not intended to be user-configurable.</span></span>
