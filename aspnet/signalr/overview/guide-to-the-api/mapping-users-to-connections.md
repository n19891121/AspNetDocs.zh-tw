---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 將訊號R使用者映射到連線 |微軟文件
author: bradygaster
description: 本主題演示如何保留有關使用者及其連接的資訊。 派翠克·弗萊徹説明寫了這個話題。 本主題中使用的軟體版本...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676157"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="41af7-105">將 SignalR 使用者對應至連線</span><span class="sxs-lookup"><span data-stu-id="41af7-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="41af7-106"> 作者：[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="41af7-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="41af7-107">本主題演示如何保留有關使用者及其連接的資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="41af7-108">派翠克·弗萊徹説明寫了這個話題。</span><span class="sxs-lookup"><span data-stu-id="41af7-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="41af7-109">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="41af7-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="41af7-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="41af7-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="41af7-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="41af7-111">.NET 4.5</span></span>
> - <span data-ttu-id="41af7-112">信號R版本 2</span><span class="sxs-lookup"><span data-stu-id="41af7-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="41af7-113">本主題的早期版本</span><span class="sxs-lookup"><span data-stu-id="41af7-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="41af7-114">有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="41af7-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="41af7-115">問題和評論</span><span class="sxs-lookup"><span data-stu-id="41af7-115">Questions and comments</span></span>
>
> <span data-ttu-id="41af7-116">請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。</span><span class="sxs-lookup"><span data-stu-id="41af7-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="41af7-117">如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="41af7-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="41af7-118">簡介</span><span class="sxs-lookup"><span data-stu-id="41af7-118">Introduction</span></span>

<span data-ttu-id="41af7-119">連接到集線器的每個用戶端傳遞一個唯一的連接 ID。您可以在中心上下文的屬性中`Context.ConnectionId`檢索此值。</span><span class="sxs-lookup"><span data-stu-id="41af7-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="41af7-120">如果應用程式需要將使用者映射到連接 ID 並保留該映射,則可以使用以下方式之一:</span><span class="sxs-lookup"><span data-stu-id="41af7-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="41af7-121">使用者識別碼提供者 (信號器 2)</span><span class="sxs-lookup"><span data-stu-id="41af7-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="41af7-122">[記憶體中儲存](#inmemory),如字典</span><span class="sxs-lookup"><span data-stu-id="41af7-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="41af7-123">每個使用者的訊號R組</span><span class="sxs-lookup"><span data-stu-id="41af7-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="41af7-124">[永久外部儲存](#database),如資料庫表或 Azure 儲存</span><span class="sxs-lookup"><span data-stu-id="41af7-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="41af7-125">本主題中顯示了每個實現。</span><span class="sxs-lookup"><span data-stu-id="41af7-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="41af7-126">使用類`OnConnected``OnDisconnected`的`OnReconnected`和方法`Hub`來跟蹤使用者連接狀態。</span><span class="sxs-lookup"><span data-stu-id="41af7-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="41af7-127">最適合您的應用程式的方法取決於:</span><span class="sxs-lookup"><span data-stu-id="41af7-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="41af7-128">託管應用程式的 Web 伺服器數。</span><span class="sxs-lookup"><span data-stu-id="41af7-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="41af7-129">是否需要獲取當前連接的使用者的清單。</span><span class="sxs-lookup"><span data-stu-id="41af7-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="41af7-130">在應用程式或伺服器重新啟動時是否需要保留組和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="41af7-131">調用外部伺服器的延遲是否是一個問題。</span><span class="sxs-lookup"><span data-stu-id="41af7-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="41af7-132">下表顯示了哪種方法適用於這些注意事項。</span><span class="sxs-lookup"><span data-stu-id="41af7-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="41af7-133">多台伺服器</span><span class="sxs-lookup"><span data-stu-id="41af7-133">More than one server</span></span> | <span data-ttu-id="41af7-134">取得目前連線使用者的清單</span><span class="sxs-lookup"><span data-stu-id="41af7-134">Get list of currently connected users</span></span> | <span data-ttu-id="41af7-135">重新啟動後保留資訊</span><span class="sxs-lookup"><span data-stu-id="41af7-135">Persist information after restarts</span></span> | <span data-ttu-id="41af7-136">最佳性能</span><span class="sxs-lookup"><span data-stu-id="41af7-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="41af7-137">使用者識別碼提供者</span><span class="sxs-lookup"><span data-stu-id="41af7-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="41af7-138">記憶體內</span><span class="sxs-lookup"><span data-stu-id="41af7-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="41af7-139">單使用者群組</span><span class="sxs-lookup"><span data-stu-id="41af7-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="41af7-140">永久外部</span><span class="sxs-lookup"><span data-stu-id="41af7-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="41af7-141">IUserID 供應商</span><span class="sxs-lookup"><span data-stu-id="41af7-141">IUserID provider</span></span>

<span data-ttu-id="41af7-142">此功能允許用戶透過新介面IUserIdProvider指定使用者Id基於IRequest的內容。</span><span class="sxs-lookup"><span data-stu-id="41af7-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="41af7-143">**IUserId 供應商**</span><span class="sxs-lookup"><span data-stu-id="41af7-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="41af7-144">默認情況下,將有一個使用用戶`IPrincipal.Identity.Name`作為使用者名的實現。</span><span class="sxs-lookup"><span data-stu-id="41af7-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="41af7-145">要更改此項,請在應用程式啟動`IUserIdProvider`時向全域主機註冊實現:</span><span class="sxs-lookup"><span data-stu-id="41af7-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="41af7-146">從集線器中,您可以通過以下 API 向這些使用者發送訊息:</span><span class="sxs-lookup"><span data-stu-id="41af7-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="41af7-147">**傳送使用者傳送訊息**</span><span class="sxs-lookup"><span data-stu-id="41af7-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="41af7-148">記憶體中儲存</span><span class="sxs-lookup"><span data-stu-id="41af7-148">In-memory storage</span></span>

<span data-ttu-id="41af7-149">以下範例展示如何在儲存在記憶體中的字典中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="41af7-150">字典使用儲存`HashSet`連接ID。在任何時候,使用者都可以與 SignalR 應用程式建立多個連接。</span><span class="sxs-lookup"><span data-stu-id="41af7-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="41af7-151">例如,透過多個設備或多個瀏覽器選項卡連接的使用者將具有多個連接 ID。</span><span class="sxs-lookup"><span data-stu-id="41af7-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="41af7-152">如果應用程式關閉,所有資訊都將丟失,但在使用者重新建立其連接時將重新填充該資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="41af7-153">如果環境包含多個 Web 伺服器,則記憶體中儲存不起作用,因為每台伺服器都將具有單獨的連接集合。</span><span class="sxs-lookup"><span data-stu-id="41af7-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="41af7-154">第一個範例顯示了管理使用者映射到連接的類。</span><span class="sxs-lookup"><span data-stu-id="41af7-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="41af7-155">哈希集的鍵將是使用者名。</span><span class="sxs-lookup"><span data-stu-id="41af7-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="41af7-156">下一個範例展示如何使用中心的連接映射類。</span><span class="sxs-lookup"><span data-stu-id="41af7-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="41af7-157">類的實例存儲在變數名稱`_connections`中。</span><span class="sxs-lookup"><span data-stu-id="41af7-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="41af7-158">單使用者群組</span><span class="sxs-lookup"><span data-stu-id="41af7-158">Single-user groups</span></span>

<span data-ttu-id="41af7-159">您可以為每個使用者創建一個組,然後在您只想聯繫該使用者時向該組發送消息。</span><span class="sxs-lookup"><span data-stu-id="41af7-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="41af7-160">每個組的名稱是使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="41af7-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="41af7-161">如果使用者有多個連接,則每個連接 ID 將添加到使用者的組中。</span><span class="sxs-lookup"><span data-stu-id="41af7-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="41af7-162">當用戶斷開連接時,不應手動從組中刪除使用者。</span><span class="sxs-lookup"><span data-stu-id="41af7-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="41af7-163">此操作由 SignalR 框架自動執行。</span><span class="sxs-lookup"><span data-stu-id="41af7-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="41af7-164">下面的範例示範如何實現單使用者組。</span><span class="sxs-lookup"><span data-stu-id="41af7-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="41af7-165">永久外部儲存</span><span class="sxs-lookup"><span data-stu-id="41af7-165">Permanent, external storage</span></span>

<span data-ttu-id="41af7-166">本主題演示如何使用資料庫或 Azure 表儲存來儲存連接資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="41af7-167">當您有多個 Web 伺服器時,此方法有效,因為每個 Web 伺服器都可以與同一數據儲存庫進行交互。</span><span class="sxs-lookup"><span data-stu-id="41af7-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="41af7-168">如果 Web 伺服器停止工作或應用程式重新啟動,`OnDisconnected`則不調用該方法。</span><span class="sxs-lookup"><span data-stu-id="41af7-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="41af7-169">因此,數據存儲庫可能具有不再有效的連接ID記錄。</span><span class="sxs-lookup"><span data-stu-id="41af7-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="41af7-170">要清理這些孤立記錄,您可能希望使在與您的應用程式相關的時間範圍之外創建的任何連接無效。</span><span class="sxs-lookup"><span data-stu-id="41af7-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="41af7-171">本節中的範例包括用於跟蹤創建連接時間的值,但不顯示如何清理舊記錄,因為您可能希望作為後台進程執行此操作。</span><span class="sxs-lookup"><span data-stu-id="41af7-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="41af7-172">資料庫</span><span class="sxs-lookup"><span data-stu-id="41af7-172">Database</span></span>

<span data-ttu-id="41af7-173">以下範例展示如何在資料庫中保留連接和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="41af7-174">您可以使用任何數據存取技術;但是,下面的示例演示如何使用實體框架定義模型。</span><span class="sxs-lookup"><span data-stu-id="41af7-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="41af7-175">這些實體模型對應於資料庫表和欄位。</span><span class="sxs-lookup"><span data-stu-id="41af7-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="41af7-176">您的數據結構可能因應用程式的要求而有很大差異。</span><span class="sxs-lookup"><span data-stu-id="41af7-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="41af7-177">第一個範例展示如何定義可以與許多連接實體關聯的用戶實體。</span><span class="sxs-lookup"><span data-stu-id="41af7-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="41af7-178">然後,從集線器,您可以使用下面顯示的代碼跟蹤每個連接的狀態。</span><span class="sxs-lookup"><span data-stu-id="41af7-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="41af7-179">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="41af7-179">Azure table storage</span></span>

<span data-ttu-id="41af7-180">以下 Azure 表存儲範例與資料庫範例類似。</span><span class="sxs-lookup"><span data-stu-id="41af7-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="41af7-181">它不包括開始使用 Azure 表存儲服務所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="41af7-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="41af7-182">有關詳細資訊,請參閱[如何使用 .NET 中的表儲存](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。</span><span class="sxs-lookup"><span data-stu-id="41af7-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="41af7-183">下面的範例顯示了用於存儲連接資訊的表實體。</span><span class="sxs-lookup"><span data-stu-id="41af7-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="41af7-184">它按使用者名對數據進行分區,並通過連接 ID 標識每個實體,以便用戶可以隨時具有多個連接。</span><span class="sxs-lookup"><span data-stu-id="41af7-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="41af7-185">在集線器中,您可以追蹤每個使用者的連接狀態。</span><span class="sxs-lookup"><span data-stu-id="41af7-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
