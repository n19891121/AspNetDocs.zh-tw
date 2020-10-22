---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 將 SignalR 使用者對應至連接 |Microsoft Docs
author: bradygaster
description: 本主題說明如何保留使用者和其連線的相關資訊。 派翠克 Fletcher 有助於撰寫本主題。 本主題中使用的軟體版本 .。。
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345421"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="456b8-105">將 SignalR 使用者對應至連線</span><span class="sxs-lookup"><span data-stu-id="456b8-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="456b8-106"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="456b8-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="456b8-107">本主題說明如何保留使用者和其連線的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="456b8-108">派翠克 Fletcher 有助於撰寫本主題。</span><span class="sxs-lookup"><span data-stu-id="456b8-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="456b8-109">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="456b8-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="456b8-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="456b8-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="456b8-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="456b8-111">.NET 4.5</span></span>
> - <span data-ttu-id="456b8-112">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="456b8-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="456b8-113">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="456b8-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="456b8-114">如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="456b8-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="456b8-115">問題與意見</span><span class="sxs-lookup"><span data-stu-id="456b8-115">Questions and comments</span></span>
>
> <span data-ttu-id="456b8-116">請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="456b8-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="456b8-117">如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="456b8-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="456b8-118">簡介</span><span class="sxs-lookup"><span data-stu-id="456b8-118">Introduction</span></span>

<span data-ttu-id="456b8-119">連接至中樞的每個用戶端都會傳遞唯一的連線識別碼。您可以在中樞內容的屬性中取得此值 `Context.ConnectionId` 。</span><span class="sxs-lookup"><span data-stu-id="456b8-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="456b8-120">如果您的應用程式需要將使用者對應到連接識別碼並保存該對應，您可以使用下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="456b8-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="456b8-121">使用者識別碼提供者 (SignalR 2) </span><span class="sxs-lookup"><span data-stu-id="456b8-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="456b8-122">[記憶體內部儲存體](#inmemory)，例如字典</span><span class="sxs-lookup"><span data-stu-id="456b8-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="456b8-123">每位使用者的 SignalR 群組</span><span class="sxs-lookup"><span data-stu-id="456b8-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="456b8-124">[永久的外部儲存體](#database)，例如資料庫資料表或 Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="456b8-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="456b8-125">本主題會顯示上述各項的各項。</span><span class="sxs-lookup"><span data-stu-id="456b8-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="456b8-126">您可以使用 `OnConnected` 類別的、 `OnDisconnected` 和 `OnReconnected` 方法 `Hub` 來追蹤使用者的連接狀態。</span><span class="sxs-lookup"><span data-stu-id="456b8-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="456b8-127">您應用程式的最佳方法取決於：</span><span class="sxs-lookup"><span data-stu-id="456b8-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="456b8-128">裝載應用程式的 web 伺服器數目。</span><span class="sxs-lookup"><span data-stu-id="456b8-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="456b8-129">您是否需要取得目前已連線使用者的清單。</span><span class="sxs-lookup"><span data-stu-id="456b8-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="456b8-130">您是否需要在應用程式或伺服器重新開機時保存群組和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="456b8-131">呼叫外部伺服器的延遲是否為問題。</span><span class="sxs-lookup"><span data-stu-id="456b8-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="456b8-132">下表說明哪些方法適用于這些考慮。</span><span class="sxs-lookup"><span data-stu-id="456b8-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="456b8-133">一部以上的伺服器</span><span class="sxs-lookup"><span data-stu-id="456b8-133">More than one server</span></span> | <span data-ttu-id="456b8-134">取得目前連線的使用者清單</span><span class="sxs-lookup"><span data-stu-id="456b8-134">Get list of currently connected users</span></span> | <span data-ttu-id="456b8-135">重新開機後保存資訊</span><span class="sxs-lookup"><span data-stu-id="456b8-135">Persist information after restarts</span></span> | <span data-ttu-id="456b8-136">最佳效能</span><span class="sxs-lookup"><span data-stu-id="456b8-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="456b8-137">UserID 提供者</span><span class="sxs-lookup"><span data-stu-id="456b8-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="456b8-138">記憶體內</span><span class="sxs-lookup"><span data-stu-id="456b8-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="456b8-139">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="456b8-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="456b8-140">永久性、外部</span><span class="sxs-lookup"><span data-stu-id="456b8-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="456b8-141">IUserID 提供者</span><span class="sxs-lookup"><span data-stu-id="456b8-141">IUserID provider</span></span>

<span data-ttu-id="456b8-142">這項功能可讓使用者透過新的介面 IUserIdProvider，指定 userId 是以 IRequest 為基礎。</span><span class="sxs-lookup"><span data-stu-id="456b8-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="456b8-143">**IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="456b8-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="456b8-144">依預設，會有一個使用使用者 `IPrincipal.Identity.Name` 做為使用者名稱的實作為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="456b8-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="456b8-145">若要變更此項，請 `IUserIdProvider` 在您的應用程式啟動時，使用全域主機註冊您的執行：</span><span class="sxs-lookup"><span data-stu-id="456b8-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="456b8-146">從中樞內，您將能夠透過下列 API 將訊息傳送給這些使用者：</span><span class="sxs-lookup"><span data-stu-id="456b8-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="456b8-147">**將訊息傳送給特定使用者**</span><span class="sxs-lookup"><span data-stu-id="456b8-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="456b8-148">記憶體內部儲存體</span><span class="sxs-lookup"><span data-stu-id="456b8-148">In-memory storage</span></span>

<span data-ttu-id="456b8-149">下列範例示範如何在儲存在記憶體中的字典中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="456b8-150">字典會使用 `HashSet` 來儲存連接識別碼。使用者在任何時候都可以有一個以上的 SignalR 應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="456b8-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="456b8-151">例如，透過多個裝置或多個瀏覽器索引標籤連線的使用者，將會有一個以上的連接識別碼。</span><span class="sxs-lookup"><span data-stu-id="456b8-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="456b8-152">如果應用程式關閉，所有資訊都會遺失，但會在使用者重新建立連線時重新填入。</span><span class="sxs-lookup"><span data-stu-id="456b8-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="456b8-153">如果您的環境包含一部以上的網頁伺服器，記憶體內部儲存體將無法運作，因為每部伺服器都有個別的連接集合。</span><span class="sxs-lookup"><span data-stu-id="456b8-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="456b8-154">第一個範例顯示的類別會管理使用者與連接的對應。</span><span class="sxs-lookup"><span data-stu-id="456b8-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="456b8-155">HashSet 的索引鍵將會是使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="456b8-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="456b8-156">下一個範例顯示如何使用中樞的連接對應類別。</span><span class="sxs-lookup"><span data-stu-id="456b8-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="456b8-157">類別的實例會儲存在變數名稱中 `_connections` 。</span><span class="sxs-lookup"><span data-stu-id="456b8-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="456b8-158">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="456b8-158">Single-user groups</span></span>

<span data-ttu-id="456b8-159">您可以為每個使用者建立群組，然後當您只想要存取該使用者時，將訊息傳送至該群組。</span><span class="sxs-lookup"><span data-stu-id="456b8-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="456b8-160">每個群組的名稱都是使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="456b8-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="456b8-161">如果使用者有一個以上的連線，則每個連接識別碼都會新增至使用者的群組。</span><span class="sxs-lookup"><span data-stu-id="456b8-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="456b8-162">當使用者中斷連線時，您不應該從群組手動移除該使用者。</span><span class="sxs-lookup"><span data-stu-id="456b8-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="456b8-163">SignalR 架構會自動執行此動作。</span><span class="sxs-lookup"><span data-stu-id="456b8-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="456b8-164">下列範例顯示如何執行單一使用者群組。</span><span class="sxs-lookup"><span data-stu-id="456b8-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="456b8-165">永久的外部儲存體</span><span class="sxs-lookup"><span data-stu-id="456b8-165">Permanent, external storage</span></span>

<span data-ttu-id="456b8-166">本主題說明如何使用資料庫或 Azure 資料表儲存體來儲存連接資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="456b8-167">當您有多部網頁伺服器時，這個方法會運作，因為每一部網頁伺服器都可以與相同的資料存放庫互動。</span><span class="sxs-lookup"><span data-stu-id="456b8-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="456b8-168">如果您的 web 伺服器停止運作或應用程式重新開機，則 `OnDisconnected` 不會呼叫該方法。</span><span class="sxs-lookup"><span data-stu-id="456b8-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="456b8-169">因此，您的資料存放庫可能會有不再有效之連接識別碼的記錄。</span><span class="sxs-lookup"><span data-stu-id="456b8-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="456b8-170">若要清除這些孤立的記錄，您可能會想要讓任何在與您應用程式相關的時間範圍以外建立的連線失效。</span><span class="sxs-lookup"><span data-stu-id="456b8-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="456b8-171">本章節中的範例包含在建立連線時追蹤的值，但不會顯示如何清除舊的記錄，因為您可能會想要以背景進程的形式來進行。</span><span class="sxs-lookup"><span data-stu-id="456b8-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="456b8-172">資料庫</span><span class="sxs-lookup"><span data-stu-id="456b8-172">Database</span></span>

<span data-ttu-id="456b8-173">下列範例示範如何在資料庫中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="456b8-174">您可以使用任何資料存取技術;但是，下列範例顯示如何使用 Entity Framework 定義模型。</span><span class="sxs-lookup"><span data-stu-id="456b8-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="456b8-175">這些實體模型會對應至資料庫資料表和欄位。</span><span class="sxs-lookup"><span data-stu-id="456b8-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="456b8-176">視應用程式的需求而定，您的資料結構可能會有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="456b8-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="456b8-177">第一個範例顯示如何定義可以與許多連接實體相關聯的使用者實體。</span><span class="sxs-lookup"><span data-stu-id="456b8-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="456b8-178">然後，您可以從中樞使用如下所示的程式碼來追蹤每個連接的狀態。</span><span class="sxs-lookup"><span data-stu-id="456b8-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="456b8-179">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="456b8-179">Azure table storage</span></span>

<span data-ttu-id="456b8-180">下列 Azure 資料表儲存體範例類似于資料庫範例。</span><span class="sxs-lookup"><span data-stu-id="456b8-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="456b8-181">它不包含開始使用 Azure 資料表儲存體服務所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="456b8-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="456b8-182">如需詳細資訊，請參閱 [如何使用 .net 的資料表儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="456b8-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="456b8-183">下列範例顯示用來儲存連接資訊的資料表實體。</span><span class="sxs-lookup"><span data-stu-id="456b8-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="456b8-184">它會依使用者名稱來分割資料，並依連線識別碼來識別每個實體，讓使用者可以隨時擁有多個連接。</span><span class="sxs-lookup"><span data-stu-id="456b8-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="456b8-185">在中樞內，您可以追蹤每個使用者連接的狀態。</span><span class="sxs-lookup"><span data-stu-id="456b8-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
