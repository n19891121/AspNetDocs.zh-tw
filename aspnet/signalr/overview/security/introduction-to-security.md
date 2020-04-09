---
uid: signalr/overview/security/introduction-to-security
title: 信號R安全簡介 |微軟文件
author: bradygaster
description: 描述在開發 SignalR 應用程式時必須考慮的安全問題。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ed562717-8591-4936-8e10-c7e63dcb570a
msc.legacyurl: /signalr/overview/security/introduction-to-security
msc.type: authoredcontent
ms.openlocfilehash: 24ce20b45543468de28ad017ba62d2f6e5a00f3b
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676192"
---
# <a name="introduction-to-signalr-security"></a><span data-ttu-id="c4e85-103">SignalR 安全性簡介</span><span class="sxs-lookup"><span data-stu-id="c4e85-103">Introduction to SignalR Security</span></span>

<span data-ttu-id="c4e85-104">由[派翠克·弗萊徹](https://github.com/pfletcher),[湯姆·菲茨麥克肯](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c4e85-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c4e85-105">本文介紹了在開發 SignalR 應用程式時必須考慮的安全問題。</span><span class="sxs-lookup"><span data-stu-id="c4e85-105">This article describes the security issues you must consider when developing a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c4e85-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="c4e85-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c4e85-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c4e85-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="c4e85-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c4e85-108">.NET 4.5</span></span>
> - <span data-ttu-id="c4e85-109">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="c4e85-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c4e85-110">本主題的早期版本</span><span class="sxs-lookup"><span data-stu-id="c4e85-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c4e85-111">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c4e85-112">問題和評論</span><span class="sxs-lookup"><span data-stu-id="c4e85-112">Questions and comments</span></span>
>
> <span data-ttu-id="c4e85-113">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="c4e85-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c4e85-114">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c4e85-115">概觀</span><span class="sxs-lookup"><span data-stu-id="c4e85-115">Overview</span></span>

<span data-ttu-id="c4e85-116">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="c4e85-116">This document contains the following sections:</span></span>

- [<span data-ttu-id="c4e85-117">訊號R安全概念</span><span class="sxs-lookup"><span data-stu-id="c4e85-117">SignalR Security Concepts</span></span>](#concepts)

    - [<span data-ttu-id="c4e85-118">驗證和授權</span><span class="sxs-lookup"><span data-stu-id="c4e85-118">Authentication and authorization</span></span>](#authentication)
    - [<span data-ttu-id="c4e85-119">連線權杖</span><span class="sxs-lookup"><span data-stu-id="c4e85-119">Connection token</span></span>](#connectiontoken)
    - [<span data-ttu-id="c4e85-120">重新連線時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="c4e85-120">Rejoining groups when reconnecting</span></span>](#rejoingroup)
- [<span data-ttu-id="c4e85-121">信號器如何防止跨網站請求偽造</span><span class="sxs-lookup"><span data-stu-id="c4e85-121">How SignalR prevents Cross-Site Request Forgery</span></span>](#csrf)
- [<span data-ttu-id="c4e85-122">訊號R安全建議</span><span class="sxs-lookup"><span data-stu-id="c4e85-122">SignalR Security Recommendations</span></span>](#recommendations)

    - [<span data-ttu-id="c4e85-123">安全通訊端字層 (SSL) 協定</span><span class="sxs-lookup"><span data-stu-id="c4e85-123">Secure Socket Layers (SSL) protocol</span></span>](#ssl)
    - [<span data-ttu-id="c4e85-124">不要將群組用作安全機制</span><span class="sxs-lookup"><span data-stu-id="c4e85-124">Do not use groups as a security mechanism</span></span>](#groupsecurity)
    - [<span data-ttu-id="c4e85-125">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="c4e85-125">Safely handling input from clients</span></span>](#input)
    - [<span data-ttu-id="c4e85-126">協調使用者狀態變更與活動連線</span><span class="sxs-lookup"><span data-stu-id="c4e85-126">Reconciling a change in user status with an active connection</span></span>](#reconcile)
    - [<span data-ttu-id="c4e85-127">自動產生的 JavaScript 代理檔</span><span class="sxs-lookup"><span data-stu-id="c4e85-127">Automatically generated JavaScript proxy files</span></span>](#autogen)
    - [<span data-ttu-id="c4e85-128">例外狀況</span><span class="sxs-lookup"><span data-stu-id="c4e85-128">Exceptions</span></span>](#exceptions)

<a id="concepts"></a>

## <a name="signalr-security-concepts"></a><span data-ttu-id="c4e85-129">訊號R安全概念</span><span class="sxs-lookup"><span data-stu-id="c4e85-129">SignalR Security Concepts</span></span>

<a id="authentication"></a>

### <a name="authentication-and-authorization"></a><span data-ttu-id="c4e85-130">驗證和授權</span><span class="sxs-lookup"><span data-stu-id="c4e85-130">Authentication and authorization</span></span>

<span data-ttu-id="c4e85-131">SignalR 不提供任何用於驗證使用者的功能。</span><span class="sxs-lookup"><span data-stu-id="c4e85-131">SignalR does not provide any features for authenticating users.</span></span> <span data-ttu-id="c4e85-132">相反,您將 SignalR 功能整合到應用程式的現有身份驗證結構中。</span><span class="sxs-lookup"><span data-stu-id="c4e85-132">Instead, you integrate the SignalR features into the existing authentication structure for an application.</span></span> <span data-ttu-id="c4e85-133">您可以像在應用程式中通常一樣對使用者進行身份驗證,並處理 SignalR 代碼中的身份驗證結果。</span><span class="sxs-lookup"><span data-stu-id="c4e85-133">You authenticate users as you would normally in your application, and work with the results of the authentication in your SignalR code.</span></span> <span data-ttu-id="c4e85-134">例如,您可以使用ASP.NET窗體身份驗證對使用者進行身份驗證,然後在中心中強制授權哪些使用者或角色調用方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-134">For example, you might authenticate your users with ASP.NET forms authentication, and then in your hub, enforce which users or roles are authorized to call a method.</span></span> <span data-ttu-id="c4e85-135">在集線器中,還可以將身份驗證資訊(如使用者名或使用者是否屬於角色)傳遞給用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4e85-135">In your hub, you can also pass authentication information, such as user name or whether a user belongs to a role, to the client.</span></span>

<span data-ttu-id="c4e85-136">SignalR 提供[授權](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx)屬性來指定哪些使用者有權存取集線器或方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-136">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users have access to a hub or method.</span></span> <span data-ttu-id="c4e85-137">將「授權」屬性應用於中心或中心中的特定方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-137">You apply the Authorize attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="c4e85-138">如果沒有"授權"屬性,則連接到集線器的用戶端可以使用集線器上的所有公共方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-138">Without the Authorize attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span> <span data-ttu-id="c4e85-139">有關集線器的詳細資訊,請參閱[SignalR 集線器的身分驗證與授權](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-139">For more information about hubs, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span>

<span data-ttu-id="c4e85-140">將`Authorize`屬性應用於中心,但不應用於持久連接。</span><span class="sxs-lookup"><span data-stu-id="c4e85-140">You apply the `Authorize` attribute to hubs, but not persistent connections.</span></span> <span data-ttu-id="c4e85-141">在使用 時強制實施授權`PersistentConnection`規則 ,必須`AuthorizeRequest`重寫 方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-141">To enforce authorization rules when using a `PersistentConnection` you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="c4e85-142">有關持久連線的詳細資訊,請參閱[SignalR 持久連線的身份驗證與授權](persistent-connection-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-142">For more information about persistent connections, see [Authentication and Authorization for SignalR Persistent Connections](persistent-connection-authorization.md).</span></span>

<a id="connectiontoken"></a>

### <a name="connection-token"></a><span data-ttu-id="c4e85-143">連線權杖</span><span class="sxs-lookup"><span data-stu-id="c4e85-143">Connection token</span></span>

<span data-ttu-id="c4e85-144">SignalR 通過驗證發件人的身份來降低執行惡意命令的風險。</span><span class="sxs-lookup"><span data-stu-id="c4e85-144">SignalR mitigates the risk of executing malicious commands by validating the identity of the sender.</span></span> <span data-ttu-id="c4e85-145">對於每個請求,用戶端和伺服器傳遞一個連接權杖,其中包含經過身份驗證的使用者的連接ID和使用者名。</span><span class="sxs-lookup"><span data-stu-id="c4e85-145">For each request, the client and server pass a connection token which contains the connection id and username for authenticated users.</span></span> <span data-ttu-id="c4e85-146">連接 ID 唯一標識每個連接的用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4e85-146">The connection id uniquely identifies each connected client.</span></span> <span data-ttu-id="c4e85-147">伺服器在創建新連接時隨機生成連接 ID,並在連接期間保留該 ID。</span><span class="sxs-lookup"><span data-stu-id="c4e85-147">The server randomly generates the connection id when a new connection is created, and persists that id for the duration of the connection.</span></span> <span data-ttu-id="c4e85-148">Web 應用程式的身份驗證機制提供使用者名。</span><span class="sxs-lookup"><span data-stu-id="c4e85-148">The authentication mechanism for the web application provides the username.</span></span> <span data-ttu-id="c4e85-149">SignalR 使用加密和數位簽名來保護連接權杖。</span><span class="sxs-lookup"><span data-stu-id="c4e85-149">SignalR uses encryption and a digital signature to protect the connection token.</span></span>

![](introduction-to-security/_static/image2.png)

<span data-ttu-id="c4e85-150">對於每個請求,伺服器驗證令牌的內容,以確保請求來自指定使用者。</span><span class="sxs-lookup"><span data-stu-id="c4e85-150">For each request, the server validates the contents of the token to ensure that the request is coming from the specified user.</span></span> <span data-ttu-id="c4e85-151">使用者名必須對應於連接 ID。通過驗證連接ID和使用者名,SignalR可防止惡意用戶輕鬆類比其他使用者。</span><span class="sxs-lookup"><span data-stu-id="c4e85-151">The username must correspond to the connection id. By validating both the connection id and the username, SignalR prevents a malicious user from easily impersonating another user.</span></span> <span data-ttu-id="c4e85-152">如果伺服器無法驗證連接權杖,則請求失敗。</span><span class="sxs-lookup"><span data-stu-id="c4e85-152">If the server cannot validate the connection token, the request fails.</span></span>

![](introduction-to-security/_static/image4.png)

<span data-ttu-id="c4e85-153">由於連接 ID 是驗證過程的一部分,因此不應向其他使用者顯示一個使用者的連接 ID 或將該值存儲在用戶端上(如 Cookie 中)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-153">Because the connection id is part of the verification process, you should not reveal one user's connection id to other users or store the value on the client, such as in a cookie.</span></span>

#### <a name="connection-tokens-vs-other-token-types"></a><span data-ttu-id="c4e85-154">連線權杖與其他權杖型態</span><span class="sxs-lookup"><span data-stu-id="c4e85-154">Connection tokens vs. other token types</span></span>

<span data-ttu-id="c4e85-155">連接令牌偶爾會被安全工具標記,因為它們看起來像是會話令牌或身份驗證令牌,如果暴露,就會造成風險。</span><span class="sxs-lookup"><span data-stu-id="c4e85-155">Connection tokens are occasionally flagged by security tools because they appear to be session tokens or authentication tokens, which poses a risk if exposed.</span></span>

<span data-ttu-id="c4e85-156">SignalR 的連接權杖不是身份驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="c4e85-156">SignalR's connection token isn't an authentication token.</span></span> <span data-ttu-id="c4e85-157">它用於確認發出此請求的使用者與創建連接的使用者相同。</span><span class="sxs-lookup"><span data-stu-id="c4e85-157">It is used to confirm that the user making this request is the same one that created the connection.</span></span> <span data-ttu-id="c4e85-158">連接權杖是必需的,因為ASP.NET SignalR允許連接在伺服器之間移動。</span><span class="sxs-lookup"><span data-stu-id="c4e85-158">The connection token is necessary because ASP.NET SignalR allows connections to move between servers.</span></span> <span data-ttu-id="c4e85-159">令牌將連接與特定使用者關聯,但不斷言發出請求的使用者的身份。</span><span class="sxs-lookup"><span data-stu-id="c4e85-159">The token associates the connection with a particular user but doesn't assert the identity of the user making the request.</span></span> <span data-ttu-id="c4e85-160">要對 SignalR 請求進行正確身份驗證,它必須具有一些其他維護使用者身份的權杖,例如 Cookie 或承載權杖。</span><span class="sxs-lookup"><span data-stu-id="c4e85-160">For a SignalR request to be properly authenticated, it must have some other token that asserts the identity of the user, such as a cookie or bearer token.</span></span> <span data-ttu-id="c4e85-161">但是,連接權杖本身不聲明請求是由該使用者發出,只是聲明令牌中包含的連接ID與該使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="c4e85-161">However, the connection token itself makes no claim that the request was made by that user, only that the connection ID contained within the token is associated with that user.</span></span>

<span data-ttu-id="c4e85-162">由於連接權杖不提供自己的身份驗證聲明,因此它不被視為"工作階段"或"身份驗證"權杖。</span><span class="sxs-lookup"><span data-stu-id="c4e85-162">Since the connection token provides no authentication claim of its own, it isn't considered a "session" or "authentication" token.</span></span> <span data-ttu-id="c4e85-163">獲取給定使用者的連接權杖並在作為其他使用者(或未身份驗證的請求)身份驗證的請求中重播該權杖將失敗,因為請求的使用者標識和存儲在權杖中的標識不匹配。</span><span class="sxs-lookup"><span data-stu-id="c4e85-163">Taking a given user's connection token and replaying it in a request authenticated as a different user (or an unauthenticated request) will fail, because the user identity of the request and the identity stored in the token won't match.</span></span>

<a id="rejoingroup"></a>

### <a name="rejoining-groups-when-reconnecting"></a><span data-ttu-id="c4e85-164">重新連線時重新加入群組</span><span class="sxs-lookup"><span data-stu-id="c4e85-164">Rejoining groups when reconnecting</span></span>

<span data-ttu-id="c4e85-165">默認情況下,SignalR 應用程式在從臨時中斷重新連接時(例如連接在連接超時之前斷開和重新建立連接時)時,將自動將使用者重新分配給相應的組。重新連接時,客戶端傳遞一個組權杖,其中包含連接ID和分配的組。</span><span class="sxs-lookup"><span data-stu-id="c4e85-165">By default, the SignalR application will automatically re-assign a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. When reconnecting, the client passes a group token that includes the connection id and the assigned groups.</span></span> <span data-ttu-id="c4e85-166">組令牌經過數位簽名和加密。</span><span class="sxs-lookup"><span data-stu-id="c4e85-166">The group token is digitally signed and encrypted.</span></span> <span data-ttu-id="c4e85-167">用戶端在重新連接後保留相同的連接 ID;因此,從重新連接的用戶端傳遞的連接ID必須與用戶端使用以前的連接ID匹配。</span><span class="sxs-lookup"><span data-stu-id="c4e85-167">The client retains the same connection id after a reconnection; therefore, the connection id passed from the reconnected client must match the previous connection id used by the client.</span></span> <span data-ttu-id="c4e85-168">此驗證可防止惡意使用者在重新連接時傳遞加入未授權組的請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-168">This verification prevents a malicious user from passing requests to join unauthorized groups when reconnecting.</span></span>

<span data-ttu-id="c4e85-169">但是,請務必注意,組令牌不會過期。</span><span class="sxs-lookup"><span data-stu-id="c4e85-169">However, it's important to note, that the group token does not expire.</span></span> <span data-ttu-id="c4e85-170">如果用戶過去屬於一個組,但被禁止從該組,該使用者可能能夠類比包含禁止組的組令牌。</span><span class="sxs-lookup"><span data-stu-id="c4e85-170">If a user belonged to a group in the past, but was banned from that group, that user may be able to mimic a group token that includes the prohibited group.</span></span> <span data-ttu-id="c4e85-171">如果需要安全地管理哪些用戶屬於哪些組,則需要將數據存儲在伺服器上,例如資料庫中。</span><span class="sxs-lookup"><span data-stu-id="c4e85-171">If you need to securely manage which users belong to which groups, you need to store that data on the server, such as in a database.</span></span> <span data-ttu-id="c4e85-172">然後,向應用程式添加邏輯,以驗證伺服器上的使用者是否屬於組。</span><span class="sxs-lookup"><span data-stu-id="c4e85-172">Then, add logic to your application that verifies on the server whether a user belongs to a group.</span></span> <span data-ttu-id="c4e85-173">驗證組成員身份的範例,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-173">For an example of verifying group membership, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<span data-ttu-id="c4e85-174">僅當連接在臨時中斷後重新連接時,自動重新加入組才適用。</span><span class="sxs-lookup"><span data-stu-id="c4e85-174">Automatically rejoining groups only applies when a connection is reconnected after a temporary disruption.</span></span> <span data-ttu-id="c4e85-175">如果用戶通過導航離開應用程式而斷開連接,或者應用程式重新啟動,則應用程式必須處理如何將該使用者添加到正確的組。</span><span class="sxs-lookup"><span data-stu-id="c4e85-175">If a user disconnects by navigating away from the application or the application restarts, your application must handle how to add that user to the correct groups.</span></span> <span data-ttu-id="c4e85-176">有關詳細資訊,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-176">For more information, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="csrf"></a>

## <a name="how-signalr-prevents-cross-site-request-forgery"></a><span data-ttu-id="c4e85-177">信號器如何防止跨網站請求偽造</span><span class="sxs-lookup"><span data-stu-id="c4e85-177">How SignalR prevents Cross-Site Request Forgery</span></span>

<span data-ttu-id="c4e85-178">跨網站請求偽造 (CSRF) 是惡意網站向使用者當前登錄的易受攻擊網站發送請求的攻擊。</span><span class="sxs-lookup"><span data-stu-id="c4e85-178">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in.</span></span> <span data-ttu-id="c4e85-179">SignalR 透過使惡意站點極不可能為 SignalR 應用程式建立有效請求來防止 CSRF。</span><span class="sxs-lookup"><span data-stu-id="c4e85-179">SignalR prevents CSRF by making it extremely unlikely for a malicious site to create a valid request for your SignalR application.</span></span>

### <a name="description-of-csrf-attack"></a><span data-ttu-id="c4e85-180">CSRF 攻擊的描述</span><span class="sxs-lookup"><span data-stu-id="c4e85-180">Description of CSRF attack</span></span>

<span data-ttu-id="c4e85-181">下面是 CSRF 攻擊的範例:</span><span class="sxs-lookup"><span data-stu-id="c4e85-181">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="c4e85-182">使用者使用表單身份驗證登錄到www.example.com。</span><span class="sxs-lookup"><span data-stu-id="c4e85-182">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="c4e85-183">伺服器對用戶進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="c4e85-183">The server authenticates the user.</span></span> <span data-ttu-id="c4e85-184">來自伺服器的回應包括身份驗證 Cookie。</span><span class="sxs-lookup"><span data-stu-id="c4e85-184">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="c4e85-185">無需註銷,使用者將訪問惡意網站。</span><span class="sxs-lookup"><span data-stu-id="c4e85-185">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="c4e85-186">此惡意網站包含以下 HTML 表單:</span><span class="sxs-lookup"><span data-stu-id="c4e85-186">This malicious site contains the following HTML form:</span></span>

    [!code-html[Main](introduction-to-security/samples/sample1.html)]

   <span data-ttu-id="c4e85-187">請注意,表單操作發佈到易受攻擊的網站,而不是惡意網站。</span><span class="sxs-lookup"><span data-stu-id="c4e85-187">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="c4e85-188">這是CSRF的「跨網站」部分。</span><span class="sxs-lookup"><span data-stu-id="c4e85-188">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="c4e85-189">用戶按一下提交按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4e85-189">The user clicks the submit button.</span></span> <span data-ttu-id="c4e85-190">瀏覽器包含帶有請求的身份驗證 Cookie。</span><span class="sxs-lookup"><span data-stu-id="c4e85-190">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="c4e85-191">請求在具有使用者身份驗證上下文的example.com伺服器上運行,並可以執行允許經過身份驗證的使用者執行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="c4e85-191">The request runs on the example.com server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="c4e85-192">儘管此示例要求使用者按下單鍵按鈕,但惡意頁面同樣可以輕鬆地運行向 SignalR 應用程式發送 AJAX 請求的腳稿。</span><span class="sxs-lookup"><span data-stu-id="c4e85-192">Although this example requires the user to click the form button, the malicious page could just as easily run a script that sends an AJAX request to your SignalR application.</span></span> <span data-ttu-id="c4e85-193">此外,使用 SSL 不會阻止 CSRF 攻擊,因為惡意網站可以發送" HTTPs://請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-193">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="c4e85-194">通常,CSRF 攻擊可能會針對使用 Cookie 進行身份驗證的網站,因為瀏覽器會將所有相關 Cookie 發送到目標網站。</span><span class="sxs-lookup"><span data-stu-id="c4e85-194">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="c4e85-195">但是,CSRF 的攻擊並不僅限於利用 Cookie。</span><span class="sxs-lookup"><span data-stu-id="c4e85-195">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="c4e85-196">例如,基本身份驗證和摘要身份驗證也容易受到攻擊。</span><span class="sxs-lookup"><span data-stu-id="c4e85-196">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="c4e85-197">使用者使用「基本」或「摘要」身份驗證登錄後,瀏覽器會自動發送憑據,直到工作階段結束。</span><span class="sxs-lookup"><span data-stu-id="c4e85-197">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

### <a name="csrf-mitigations-taken-by-signalr"></a><span data-ttu-id="c4e85-198">SignalR 採取的 CSRF 緩解措施</span><span class="sxs-lookup"><span data-stu-id="c4e85-198">CSRF mitigations taken by SignalR</span></span>

<span data-ttu-id="c4e85-199">SignalR 採取以下步驟防止惡意網站向應用程式創建有效請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-199">SignalR takes the following steps to prevent a malicious site from creating valid requests to your application.</span></span> <span data-ttu-id="c4e85-200">默認情況下,SignalR 執行這些步驟,無需在代碼中執行任何操作。</span><span class="sxs-lookup"><span data-stu-id="c4e85-200">SignalR takes these steps by default, you do not need to take any action in your code.</span></span>

- <span data-ttu-id="c4e85-201">**關閉跨網域要求**SignalR 禁用跨域請求,以防止使用者從外部域調用 SignalR 終結點。</span><span class="sxs-lookup"><span data-stu-id="c4e85-201">**Disable cross domain requests** SignalR disables cross domain requests to prevent users from calling a SignalR endpoint from an external domain.</span></span> <span data-ttu-id="c4e85-202">SignalR 認為來自外部域的任何請求都無效,並阻止請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-202">SignalR considers any request from an external domain to be invalid and blocks the request.</span></span> <span data-ttu-id="c4e85-203">我們建議您保留此默認行為;但是,我們建議您保留此默認行為。否則,惡意網站可能會誘使用戶向您的網站發送命令。</span><span class="sxs-lookup"><span data-stu-id="c4e85-203">We recommend that you keep this default behavior; otherwise, a malicious site could trick users into sending commands to your site.</span></span> <span data-ttu-id="c4e85-204">如果需要使用跨域要求,請參閱[如何建立跨域連接](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-204">If you need to use cross domain requests, see     [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain) .</span></span>
- <span data-ttu-id="c4e85-205">**在查詢字串中傳遞連接權杖,而不是 Cookie**SignalR 將連接權杖作為查詢字串值傳遞,而不是作為Cookie傳遞。</span><span class="sxs-lookup"><span data-stu-id="c4e85-205">**Pass connection token in query string, not cookie** SignalR passes the connection token as a query string value, instead of as a cookie.</span></span> <span data-ttu-id="c4e85-206">將連接權杖儲存在 Cookie 中不安全,因為當遇到惡意代碼時,瀏覽器可能會無意中轉發連接權杖。</span><span class="sxs-lookup"><span data-stu-id="c4e85-206">Storing the connection token in a cookie is unsafe because the browser can inadvertently forward the connection token when malicious code is encountered.</span></span> <span data-ttu-id="c4e85-207">此外,在查詢字串中傳遞連接權杖可防止連接權杖保留在當前連接之外。</span><span class="sxs-lookup"><span data-stu-id="c4e85-207">Also, passing the connection token in the query string prevents the connection token from persisting beyond the current connection.</span></span> <span data-ttu-id="c4e85-208">因此,惡意使用者不能根據其他使用者的身份驗證憑據發出請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-208">Therefore, a malicious user cannot make a request under another user's authentication credentials.</span></span>
- <span data-ttu-id="c4e85-209">**驗證連線權杖**如[連接權杖](#connectiontoken)部分所述,伺服器知道哪個連接ID與每個經過身份驗證的使用者相關聯。</span><span class="sxs-lookup"><span data-stu-id="c4e85-209">**Verify connection token** As described in the     [Connection token](#connectiontoken) section, the server knows which connection id is associated with each authenticated user.</span></span> <span data-ttu-id="c4e85-210">伺服器不處理來自連接 ID 與使用者名不匹配的任何請求。</span><span class="sxs-lookup"><span data-stu-id="c4e85-210">The server does not process any request from a connection id that does not match the user name.</span></span> <span data-ttu-id="c4e85-211">惡意使用者不太可能猜到有效請求,因為惡意用戶必須知道使用者名和當前隨機生成的連接 ID。連接 ID 一旦結束,該連接 ID 將變為無效。</span><span class="sxs-lookup"><span data-stu-id="c4e85-211">It is unlikely a malicious user could guess a valid request because the malicious user would have to know the user name and the current randomly-generated connection id. That connection id becomes invalid as soon as the connection is ended.</span></span> <span data-ttu-id="c4e85-212">匿名使用者不應訪問任何敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="c4e85-212">Anonymous users should not have access to any sensitive information.</span></span>

<a id="recommendations"></a>

## <a name="signalr-security-recommendations"></a><span data-ttu-id="c4e85-213">訊號R安全建議</span><span class="sxs-lookup"><span data-stu-id="c4e85-213">SignalR Security Recommendations</span></span>

<a id="ssl"></a>

### <a name="secure-socket-layers-ssl-protocol"></a><span data-ttu-id="c4e85-214">安全通訊端字層 (SSL) 協定</span><span class="sxs-lookup"><span data-stu-id="c4e85-214">Secure Socket Layers (SSL) protocol</span></span>

<span data-ttu-id="c4e85-215">SSL 協定使用加密來保護用戶端和伺服器之間的數據傳輸。</span><span class="sxs-lookup"><span data-stu-id="c4e85-215">The SSL protocol uses encryption to secure the transport of data between a client and server.</span></span> <span data-ttu-id="c4e85-216">如果您的 SignalR 應用程式在用戶端和伺服器之間傳輸敏感資訊,請使用 SSL 進行傳輸。</span><span class="sxs-lookup"><span data-stu-id="c4e85-216">If your SignalR application transmits sensitive information between the client and server, use SSL for the transport.</span></span> <span data-ttu-id="c4e85-217">有關設置 SSL 的詳細資訊,請參閱[如何在 IIS 7 上設置 SSL。](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis)</span><span class="sxs-lookup"><span data-stu-id="c4e85-217">For more information about setting up SSL, see [How to set up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<a id="groupsecurity"></a>

### <a name="do-not-use-groups-as-a-security-mechanism"></a><span data-ttu-id="c4e85-218">不要將群組用作安全機制</span><span class="sxs-lookup"><span data-stu-id="c4e85-218">Do not use groups as a security mechanism</span></span>

<span data-ttu-id="c4e85-219">組是收集相關使用者的便捷方式,但它們不是限制對敏感資訊訪問的安全機制。</span><span class="sxs-lookup"><span data-stu-id="c4e85-219">Groups are a convenient way of collecting related users, but they are not a secure mechanism for limiting access to sensitive information.</span></span> <span data-ttu-id="c4e85-220">當用戶可以在重新連接期間自動重新加入組時,尤其如此。</span><span class="sxs-lookup"><span data-stu-id="c4e85-220">This is especially true when users can automatically rejoin groups during a reconnect.</span></span> <span data-ttu-id="c4e85-221">相反,請考慮將特權使用者添加到角色,並將對中心方法的訪問限制為該角色的成員。</span><span class="sxs-lookup"><span data-stu-id="c4e85-221">Instead, consider adding privileged users to a role and limiting access to a hub method to only members of that role.</span></span> <span data-ttu-id="c4e85-222">有關基於角色限制存取的範例,請參閱[SignalR 中心的身份認證與授權](hub-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-222">For an example of restricting access based on a role, see [Authentication and Authorization for SignalR Hubs](hub-authorization.md).</span></span> <span data-ttu-id="c4e85-223">有關在重新連線時檢查使用者存取群組的範例,請參閱[使用群組](../guide-to-the-api/working-with-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-223">For an example of checking user access to groups when reconnecting, see [Working with groups](../guide-to-the-api/working-with-groups.md).</span></span>

<a id="input"></a>

### <a name="safely-handling-input-from-clients"></a><span data-ttu-id="c4e85-224">安全地處理來自用戶端的輸入</span><span class="sxs-lookup"><span data-stu-id="c4e85-224">Safely handling input from clients</span></span>

<span data-ttu-id="c4e85-225">為了確保惡意使用者不會向其他使用者發送腳本,您必須對用戶端用於廣播到其他用戶端的所有輸入進行編碼。</span><span class="sxs-lookup"><span data-stu-id="c4e85-225">To ensure that a malicious user does not send script to other users, you must encode all input from clients that is intended for broadcast to other clients.</span></span> <span data-ttu-id="c4e85-226">您應該對接收用戶端而不是伺服器上的消息進行編碼,因為 SignalR 應用程式可能具有許多不同類型的用戶端。</span><span class="sxs-lookup"><span data-stu-id="c4e85-226">You should encode messages on the receiving clients rather than the server, because your SignalR application may have many different types of clients.</span></span> <span data-ttu-id="c4e85-227">因此,HTML 編碼適用於 Web 用戶端,但對於其他類型的用戶端則不有效。</span><span class="sxs-lookup"><span data-stu-id="c4e85-227">Therefore, HTML-encoding works for a web client, but not for other types of clients.</span></span> <span data-ttu-id="c4e85-228">例如,顯示聊天消息的 Web 用戶端方法可以`html()`通過調用 函數安全地處理使用者名和消息。</span><span class="sxs-lookup"><span data-stu-id="c4e85-228">For example, a web client method to display a chat message would safely handle the user name and message by calling the `html()` function.</span></span>

[!code-html[Main](introduction-to-security/samples/sample2.html?highlight=3-4)]

<a id="reconcile"></a>

### <a name="reconciling-a-change-in-user-status-with-an-active-connection"></a><span data-ttu-id="c4e85-229">協調使用者狀態變更與活動連線</span><span class="sxs-lookup"><span data-stu-id="c4e85-229">Reconciling a change in user status with an active connection</span></span>

<span data-ttu-id="c4e85-230">如果使用者的身份驗證狀態在存在活動連接時發生更改,則使用者將收到一個錯誤,指出「使用者標識在活動 SignalR 連接期間無法更改」。</span><span class="sxs-lookup"><span data-stu-id="c4e85-230">If a user's authentication status changes while an active connection exists, the user will receive an error that states, "The user identity cannot change during an active SignalR connection."</span></span> <span data-ttu-id="c4e85-231">在這種情況下,應用程式應重新連接到伺服器,以確保連接 ID 和使用者名得到協調。</span><span class="sxs-lookup"><span data-stu-id="c4e85-231">In that case, your application should re-connect to the server to make sure the connection id and username are coordinated.</span></span> <span data-ttu-id="c4e85-232">例如,如果應用程式允許使用者在存在活動連接時註銷,則連接的用戶名將不再與為下一個請求傳入的名稱匹配。</span><span class="sxs-lookup"><span data-stu-id="c4e85-232">For example, if your application allows the user to log out while an active connection exists, the username for the connection will no longer match the name that is passed in for the next request.</span></span> <span data-ttu-id="c4e85-233">您需要在使用者註銷之前停止連接,然後重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="c4e85-233">You will want to stop the connection before the user logs out, and then restart it.</span></span>

<span data-ttu-id="c4e85-234">但是,請務必注意,大多數應用程式不需要手動停止並啟動連接。</span><span class="sxs-lookup"><span data-stu-id="c4e85-234">However, it is important to note that most applications will not need to manually stop and start the connection.</span></span> <span data-ttu-id="c4e85-235">如果應用程式在註銷後將使用者重定向到單獨的頁面(例如 Web 窗體應用程式或 MVC 應用程式中的默認行為,或在註銷後刷新當前頁面,則活動連接將自動斷開連接,不需要任何其他操作。</span><span class="sxs-lookup"><span data-stu-id="c4e85-235">If your application redirects users to a separate page after logging out, such as the default behavior in a Web Forms application or MVC application, or refreshes the current page after logging out, the active connection is automatically disconnected and does not require any additional action.</span></span>

<span data-ttu-id="c4e85-236">下面的範例展示如何在使用者狀態更改時停止和啟動連接。</span><span class="sxs-lookup"><span data-stu-id="c4e85-236">The following example shows how to stop and start a connection when the user status has changed.</span></span>

[!code-html[Main](introduction-to-security/samples/sample3.html)]

<span data-ttu-id="c4e85-237">或者,如果您的網站使用表單身份驗證的滑動過期,並且沒有活動保持身份驗證 Cookie 的有效性,則使用者的身份驗證狀態可能會更改。</span><span class="sxs-lookup"><span data-stu-id="c4e85-237">Or, the user's authentication status may change if your site uses sliding expiration with Forms Authentication, and there is no activity to keep the authentication cookie valid.</span></span> <span data-ttu-id="c4e85-238">在這種情況下,使用者將被註銷,用戶名將不再與連接令牌中的使用者名匹配。</span><span class="sxs-lookup"><span data-stu-id="c4e85-238">In that case, the user will be logged out and the user name will no longer match the user name in the connection token.</span></span> <span data-ttu-id="c4e85-239">您可以通過添加一些腳本來解決此問題,這些腳本定期請求 Web 伺服器上的資源以保持身份驗證 Cookie 的有效性。</span><span class="sxs-lookup"><span data-stu-id="c4e85-239">You can fix this problem by adding some script that periodically requests a resource on the web server to keep the authentication cookie valid.</span></span> <span data-ttu-id="c4e85-240">下面的示例演示如何每 30 分鐘請求一次資源。</span><span class="sxs-lookup"><span data-stu-id="c4e85-240">The following example shows how to request a resource every 30 minutes.</span></span>

[!code-javascript[Main](introduction-to-security/samples/sample4.js)]

<a id="autogen"></a>

### <a name="automatically-generated-javascript-proxy-files"></a><span data-ttu-id="c4e85-241">自動產生的 JavaScript 代理檔</span><span class="sxs-lookup"><span data-stu-id="c4e85-241">Automatically generated JavaScript proxy files</span></span>

<span data-ttu-id="c4e85-242">如果不想在每個使用者的 JavaScript 代理檔中包含所有中心和方法,則可以禁用該檔的自動生成。</span><span class="sxs-lookup"><span data-stu-id="c4e85-242">If you do not want to include all of the hubs and methods in the JavaScript proxy file for each user, you can disable the automatic generation of the file.</span></span> <span data-ttu-id="c4e85-243">如果有多個集線器和方法,但不希望每個使用者都瞭解所有方法,則可以選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="c4e85-243">You might choose this option if you have multiple hubs and methods, but do not want every user to be aware of all of the methods.</span></span> <span data-ttu-id="c4e85-244">通過將**啟用JavaScriptProxie設置為** **false,** 可以禁用自動生成。</span><span class="sxs-lookup"><span data-stu-id="c4e85-244">You disable automatic generation by setting **EnableJavaScriptProxies** to **false**.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample5.cs)]

<span data-ttu-id="c4e85-245">有關 JavaScript 代理檔的詳細資訊,請參閱[產生的代理及其為您做什麼](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="c4e85-245">For more information about the JavaScript proxy files, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span> <a id="exceptions"></a>

### <a name="exceptions"></a><span data-ttu-id="c4e85-246">例外狀況</span><span class="sxs-lookup"><span data-stu-id="c4e85-246">Exceptions</span></span>

<span data-ttu-id="c4e85-247">應避免將異常物件傳遞給客戶端,因為物件可能會向用戶端公開敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="c4e85-247">You should avoid passing exception objects to clients because the objects may expose sensitive information to the clients.</span></span> <span data-ttu-id="c4e85-248">相反,在顯示相關錯誤消息的用戶端上調用方法。</span><span class="sxs-lookup"><span data-stu-id="c4e85-248">Instead, call a method on the client that displays the relevant error message.</span></span>

[!code-csharp[Main](introduction-to-security/samples/sample6.cs)]
